---
title: クライアントのセキュリティとプライバシー
titleSuffix: Configuration Manager
description: 構成マネージャー クライアントのセキュリティとプライバシーについて説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3dfb749695ffb7a8ecdeab5e4fbed764023eb6e2
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385594"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>構成マネージャー クライアントのセキュリティとプライバシー

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、構成マネージャー クライアントのセキュリティとプライバシーの情報について説明します。 また、[Exchange Server コネクタ](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)によって管理されるモバイル デバイスに関する情報も含まれます。  



##  <a name="BKMK_Security_Clients"></a> クライアントのセキュリティのベスト プラクティス  

Configuration Manager サイトは、構成マネージャー クライアントを実行するデバイスからのデータを受け入れます。 この動作により、クライアントがサイトを攻撃するリスクが発生します。 たとえば、クライアントが形式の正しくないインベントリを送信したり、サイト システムに過剰な負荷をかけようとしたりする可能性があります。 Configuration Manager クライアントは、信頼されているデバイスにのみ展開してください。 また、セキュリティに関する次のベスト プラクティスに従うと、許可されていないデバイスや危険性のあるデバイスからサイトを保護するのに役立ちます。  

#### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>IIS を実行するサイト システムとクライアントの通信に公開キー基盤 (PKI) 証明書を使用する  

-   サイト プロパティとして、**[HTTPS のみ]** の **[サイト システム設定]** を構成します。  

-   `UsePKICert` CCMSetup プロパティを指定してクライアントをインストールします。  

-   証明書失効リスト (CRL) を使用し、必ずクライアントと通信先のサーバーが CRL にアクセスできるようにします。  

モバイル デバイス クライアントと一部のインターネット ベース クライアントでは、これらの証明書が必要です。 イントラネット上のすべてのクライアント接続にはこれらの証明書をお勧めします。  

PKI 証明書の要件および Configuration Manager の保護のために PKI 証明書を使う方法について詳しくは、[PKI 証明書の要件](/sccm/core/plan-design/network/pki-certificate-requirements)に関するページをご覧ください。  


#### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>信頼されているドメインのクライアントを自動的に承認し、他のコンピューターは手動で確認して承認する  

PKI 認証を使用できない場合は、承認処理により、Configuration Manager での管理対象となる信頼されるコンピューターを識別します。 階層には、クライアントの承認を構成するための次のオプションがあります。  
- 手動
- 信頼される側のドメイン内のコンピューターについて自動
- すべてのコンピューターについて自動  

最も安全な承認方法は、信頼されたドメインのメンバであるクライアントを自動で承認する方法です。 その後、他のすべてのコンピューターを手動で確認して承認します。 すべてのクライアントを自動で承認することは、他のアクセス制御によって信頼できないコンピューターがネットワークにアクセスできないようにしていない限り、推奨されません。  

コンピューターを手動で承認する方法について詳しくは、「[[デバイス] ノードを使用してクライアントを管理する](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode)」をご覧ください。  


#### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>クライアントが Configuration Manager 階層にアクセスするのを防ぐためにブロックに依存しない  

ブロックされたクライアントは、Configuration Manager インフラストラクチャによって拒否されます。 ブロックされたクライアントは、サイト システムと通信してポリシーをダウンロードしたり、インベントリ データをアップロードしたり、状態またはステータス メッセージを送信したりできません。 

ブロックは、次のシナリオのために設計されています。 
- OS をクライアントに展開するときに、失われたり侵害されたりしたブート メディアをブロックするため
- すべてのサイト システムが HTTPS クライアント接続を受け入れるとき 

サイト システムが HTTP クライアント接続を受け入れるときは、信頼されていないコンピューターからの Configuration Manager 階層の保護をブロックに依存しないでください。 このシナリオでは、ブロックされているクライアントが、新しい自己署名証明書とハードウェア ID でサイトに再参加する可能性があります。 

証明書の失効は、侵害された可能性のある証明書に対する第 1 の防御ラインです。 サポートされている公開キー基盤 (PKI) からの証明書失効リスト (CRL) のみを使用できます。 Configuration Manager でクライアントをブロックすることは、階層を保護するための第 2 の防御ラインとなります。  

詳しくは、[クライアントをブロックするかどうかの判断](/sccm/core/clients/deploy/plan/determine-whether-to-block-clients)に関するページをご覧ください。  


#### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>環境について実用的である最も安全なクライアント インストール方法を使用する  

-   ドメイン コンピューターでは、グループ ポリシー クライアント インストールおよびソフトウェア更新プログラムに基づくクライアント インストールの方がクライアント プッシュ インストールよりも安全なインストール方法です。  

-   アクセス制御と変更制御を適用する場合は、イメージングと手動のインストール方法を使います。  

-   バージョン 1806 以降では、Kerberos 相互認証とクライアント プッシュ インストールを使います。  

クライアント プッシュ インストールは、数多くの依存関係があるため、すべてのクライアント インストール方法の中で最も安全性が低い方法です。 そのような依存関係としては、ローカル管理アクセス許可、Admin$ 共有、ファイアウォール例外などがあります。 これらの依存関係の数と種類により、攻撃対象が増えることになります。  

バージョン 1806 以降のサイトでは、クライアント プッシュを使うと、接続を確立する前の NTLM へのフォールバックを許可しないことによって、Kerberos の相互認証を要求できます。 この機能強化は、サーバーとクライアント間の通信をセキュリティで保護するのに役立ちます。 詳しくは、[クライアント プッシュを使用したクライアントのインストール方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush)に関するページをご覧ください。<!--1358204-->  

各種のクライアント インストール方法について詳しくは、[クライアントのインストール方法](/sccm/core/clients/deploy/plan/client-installation-methods)に関するページをご覧ください。  

可能な場合は常に、Configuration Manager で必要なセキュリティ アクセス許可が最小限のクライアント インストール方法を選択します。 クライアントの展開以外の目的に使用できるアクセス許可を持つセキュリティ ロールを割り当てる管理ユーザーを制限します。 たとえば、自動クライアント アップグレードを構成するには、管理ユーザーにすべてのセキュリティ アクセス許可を付与する**完全な権限を持つ管理者**セキュリティ ロールが必要です。  

それぞれのクライアント インストール方法に関する依存関係および必要なセキュリティ アクセス許可について詳しくは、「[コンピューター クライアントの前提条件](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#BKMK_prereqs_computers)」の「インストール方法の依存関係」をご覧ください。  


#### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>クライアント プッシュ インストールを使用する必要がある場合は、追加手順を実行し、クライアント プッシュ インストール アカウントを保護する  

このアカウントは、構成マネージャー クライアントがインストールされる各コンピューターのローカル **Administrators** グループのメンバーでなければなりません。 **Domain Admins** グループにはクライアント プッシュ インストール アカウントを追加しないでください。 代わりに、グローバル グループを作成して、そのグローバル グループをクライアント上のローカルの **Administrators** グループに追加します。 グループ ポリシー オブジェクトを作成し、制限されたグループ設定を追加して、クライアント プッシュ インストール アカウントをローカルの **Administrators** グループに追加します。  

セキュリティを強化するには、複数のクライアント プッシュ インストール アカウントを作成し、それぞれに限定された数のコンピューターに対する管理アクセス権を付与します。 1 つのアカウントが侵害された場合、侵害されるのはそのアカウントがアクセスできるクライアント コンピューターだけです。  


#### <a name="remove-certificates-before-imaging-clients"></a>クライアントのイメージングの前に証明書を削除する  

OS イメージを使ってクライアントを展開するときは、常に、イメージをキャプチャする前に証明書を削除します。 これらの証明書には、クライアント認証用の PKI 証明書や自己署名証明書が含まれます。 これらの証明書を削除しないと、クライアントが互いになりすましを行う可能性があります。 各クライアントのデータを検証できなくなります。  

詳しくは、「[オペレーティング システムをキャプチャするタスク シーケンスを作成する](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system)」をご覧ください。  


#### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>構成マネージャー クライアント コンピューターが次の証明書の正規コピーを取得することを確認する  

-   Configuration Manager の信頼されたルート キー証明書  

    次の両方が当てはまる場合、クライアントは有効な管理ポイントを認証するために Configuration Manager の信頼されたルート キーに依存しています。  

      - Active Directory スキーマを Configuration Manager 用に拡張していない
      - クライアントは管理ポイントと通信するときに PKI 証明書を使用しない  

    このシナリオでは、クライアントは、信頼されたルート キーを使用しない限り、管理ポイントが階層に対して信頼されていることを検証できません。 信頼されたルート キーを使用しないと、巧みな攻撃者がクライアントを偽の管理ポイントに誘導する可能性があります。  

    クライアントが Configuration Manager の信頼されたルート キーをグローバル カタログからダウンロードできない場合や PKI 証明書を使用してダウンロードできないときは、信頼されたルート キーでクライアントを事前にプロビジョニングします。 これにより、クライアントが偽の管理ポイントに誘導されないようにします。 詳細については、「[信頼されたルート キーの計画](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK)」を参照してください。  

-   サイト サーバー署名証明書  

     クライアントは、この証明書を使って、管理ポイントからダウンロードされたポリシーにサイト サーバーの署名があることを確認します。 この証明書は、サイト サーバーによって自己署名されてから Active Directory ドメイン サービスに発行されます。  

     クライアントは、サイト サーバー署名証明書をグローバル カタログからダウンロードできない場合は、既定で、管理ポイントからダウンロードします。 管理ポイントがインターネットなどの信頼されていないネットワークに公開される場合は、サイト サーバー署名証明書をクライアントに手動でインストールします。 それによって、侵害された管理ポイントから改ざんされたクライアント ポリシーをダウンロードできないようにします。  

     サイト サーバー署名証明書を手動でインストールするには、CCMSetup client.msi プロパティ **SMSSIGNCERT**を使用します。 詳しくは、[クライアント インストールのプロパティ](/sccm/core/clients/deploy/about-client-installation-properties)に関するページをご覧ください。  


#### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>クライアントが接続した最初の管理ポイントから、信頼されたルート キーをダウンロードする場合に、サイトの自動割り当てを使用しない  

新しいクライアントが不正な管理ポイントから信頼されるルート キーをダウンロードするリスクを回避するために、次のシナリオでのみサイトの自動割り当てを使用してください。  

-   クライアントが、Active Directory Domain Services に発行されている Configuration Manager サイト情報にアクセスできる  

-   クライアントに、信頼されたルート キーを事前に準備する  

-   エンタープライズ証明機関から PKI 証明書を使用して、クライアントと管理ポイント間に信頼関係を確立する  

信頼されたルート キーについて詳しくは、「[信頼されたルート キーの計画](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK)」をご覧ください。  


#### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>CCMSetup Client.msi オプション SMSDIRECTORYLOOKUP=NoWINS を指定してクライアント コンピューターをインストールする  

クライアントで使用できる最も安全なサイトおよび管理ポイントの検出方法は、Active Directory Domain Services を使用することです。 環境によってはこの方法を使用できないことがあります。 たとえば、Configuration Manager 用に Active Directory スキーマを拡張できない場合や、クライアントが信頼されていないフォレストやワークグループに存在する場合です。 この方法が使用できない場合は、代わりのサービスの場所検索方法として DNS 発行を使用します。 どちらの方法も失敗する場合、管理ポイントが HTTPS クライアント接続用に構成されていないと、クライアントは WINS を使用するようにフォールバックできます。  

WINS への発行では、他の発行方法より安全性が低下します。 **SMSDIRECTORYLOOKUP=NoWINS** を指定することにより、WINS の使用にフォールバックしないようクライアント コンピューターを構成します。 サービスの場所に WINS を使う必要がある場合は、**SMSDIRECTORYLOOKUP=WINSSECURE** を使います。 この設定が既定です。 Configuration Manager の信頼されたルート キーを使って、管理ポイントの自己署名証明書を検証します。  

> [!NOTE]  
>  クライアントで構成に **SMSDIRECTORYLOOKUP=WINSSECURE** が指定されている場合、管理ポイントが WINS から検出されると、クライアントは WMI 内にある Configuration Manager の信頼できるルート キーのコピーを確認します。  
> 
> 管理ポイントの証明書の署名とクライアントの信頼されたルート キーのコピーが一致した場合は、証明書が検証されます。 証明書の検証後に、クライアントは WINS を使って検出された管理ポイントとの通信を始めます。  
> 
> 管理ポイントの証明書の署名がクライアントの信頼されたルート キーのコピーと一致しない場合、証明書は検証されません。 証明書の検証後に、クライアントは WINS を使って検出された管理ポイントと通信しません。  


#### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>重要なソフトウェア更新プログラムを展開するのに十分なメンテナンス期間を確保する  

デバイス コレクションのメンテナンス期間を構成して、Configuration Manager がソフトウェアをそれらのデバイスにインストールできる時間を制限します。 メンテナンス期間の構成が小さすぎる場合、クライアントは重要なソフトウェア更新プログラムをインストールしない場合があります。 この動作は、ソフトウェア更新プログラムによって軽減される攻撃に対してクライアントを脆弱なままにします。  


#### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>書き込みフィルターを使用して Windows Embedded デバイスの攻撃対象領域を減らすための追加のセキュリティ予防措置を講じる  

Windows Embedded デバイスで書き込みフィルターを有効にすると、ソフトウェアのインストールや変更はオーバーレイに対してのみ行われます。 これらの変更は、デバイスの再起動後は維持されません。 Configuration Manager を使って書き込みフィルターを無効にした場合、この期間中に、埋め込みデバイスはすべてのボリュームへの変更に対して脆弱になります。 これらのボリュームには共有フォルダーが含まれます。  

Configuration Manager はこの期間中にコンピューターをロックして、ローカル管理者のみがサインインできるようにします。 可能な場合は常に、コンピューターを保護するための追加のセキュリティ予防措置を行ってください。 たとえば、ファイアウォールで追加の制限を有効にします。  

メンテナンス期間を使って変更を保持する場合は、これらの期間を慎重に計画します。 書き込みフィルターが無効になる時間を最小限にしますが、ソフトウェアのインストールと再起動が完了するのに十分な長さにします。  


#### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>ソフトウェアの更新に基づいたクライアント インストールで最新バージョンのクライアントを使用する

ソフトウェアの更新に基づいたクライアントのインストールを使用し、新しいバージョンのクライアントをサイトにインストールする場合は、発行されているソフトウェア更新プログラムを更新します。 その後、クライアントはソフトウェアの更新ポイントから最新バージョンを受信します。  

サイトを更新するとき、ソフトウェアの更新ポイントに発行されているクライアント展開のソフトウェア更新プログラムは自動的に更新されません。 構成マネージャー クライアントをソフトウェアの更新ポイントに再発行して、バージョン番号を更新します。  

詳しくは、[ソフトウェアの更新に基づいたインストールを使用した構成マネージャー クライアントのインストール方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientSUP)に関するページをご覧ください。  


#### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>信頼できる制限付きアクセス デバイスで BitLocker PIN の入力の一時停止だけを行う  

信頼でき、物理アクセスが制限されているコンピューターに対して **[再起動時の BitLocker PIN の入力を一時停止する]** を **[常時]** にするクライアント設定の構成だけを行います。

このクライアント設定を **[常時]** に設定すると、Configuration Manager はソフトウェアのインストールを完了できます。 この動作は、重要なソフトウェア更新プログラムのインストールとサービス再開に役立ちます。 攻撃者が再開プロセスをインターセプトすると、コンピューターの制御が奪われる可能性があります。 この設定は、コンピューターが信頼できるものである場合およびコンピューターへの物理アクセスが制限されている場合にのみ使用してください。 たとえば、この設定はデータ センターのサーバーに適している場合があります。  

このクライアント設定について詳しくは、[クライアントの設定](/sccm/core/clients/deploy/about-client-settings#suspend-bitlocker-pin-entry-on-restart)に関するページをご覧ください。  


#### <a name="dont-bypass-powershell-execution-policy"></a>PowerShell 実行ポリシーをバイパスしない   

**PowerShell 実行ポリシー**に対する構成マネージャー クライアントの設定を**バイパス**に構成すると、Windows は無署名の PowerShell スクリプトの実行を許可します。 この動作により、クライアント コンピューターでマルウェアが実行できる可能性があります。 このオプションが必要なときは、カスタム クライアント設定を使います。 無署名の PowerShell スクリプトを実行する必要があるクライアント コンピューターに対してのみそれを割り当てます。  

このクライアント設定について詳しくは、[クライアントの設定](/sccm/core/clients/deploy/about-client-settings#powershell-execution-policy)に関するページをご覧ください。  



##  <a name="bkmk_mobile"></a> モバイル デバイスのセキュリティのベスト プラクティス  


#### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>登録プロキシ ポイントを境界ネットワークにインストールし、登録ポイントをイントラネットにインストールする  

インターネット ベースのモバイル デバイスを Configuration Manager に登録する場合は、登録プロキシ ポイントを境界ネットワークにインストールし、登録ポイントをイントラネットにインストールします。 このようにロールを分けることで、登録ポイントを攻撃から保護するのに役立ちます。 登録ポイントを侵害した攻撃者は、認証用の証明書を取得する可能性があります。 また、モバイル デバイスを登録するユーザーの資格情報を盗むことができます。  


#### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>モバイル デバイスに対する不正アクセスを防ぐのに役立つパスワード設定を構成する  

"*Configuration Manager によって登録されるモバイル デバイスの場合*": モバイル デバイス構成項目を使用して、パスワードの複雑さを PIN として構成します。 少なくとも既定の最小パスワード長を指定します。  

"*構成マネージャー クライアントがインストールされておらず、Exchange Server コネクタによって管理されているモバイル デバイスの場合*": Exchange Server コネクタの **[パスワードの設定]** で、パスワードの複雑さが PIN になるように構成します。 少なくとも既定の最小パスワード長を指定します。  


#### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>信頼できる会社によって署名されているアプリケーションの実行のみを許可する  

信頼できる会社によって署名されている場合にのみアプリケーションの実行を許可すると、インベントリ情報およびステータス情報が改ざんされるのを防ぐのに役立ちます。 無署名のファイルのインストールをデバイスに許可してはなりません。  

"*Configuration Manager に登録したモバイル デバイスの場合*": モバイル デバイス構成項目を使って、セキュリティ設定 **[署名されていないアプリケーション]** を **[禁止]** に構成します。 **[署名されていないファイルのインストール]** を信頼できるソースに構成します。  

"*構成マネージャー クライアントがインストールされておらず、Exchange Server コネクタによって管理されているモバイル デバイスの場合*": Exchange Server コネクタの **[アプリケーション設定]** で **[署名されていないファイルのインストール]** および **[署名されていないアプリケーション]** が **[禁止]** となるようにします。  


#### <a name="lock-mobile-devices-when-not-in-use"></a>使用中でないモバイル デバイスをロックする  

モバイル デバイスを使用していないときにロックすると、特権の昇格攻撃を防ぐのに役立ちます。

"*Configuration Manager に登録したモバイル デバイスの場合*": モバイル デバイス設定項目を使ってパスワード設定 **[モバイル デバイスがロックされるまでのアイドル時間 (分)]** を構成します。  

"*構成マネージャー クライアントがインストールされておらず、Exchange Server コネクタによって管理されているモバイル デバイスの場合*": Exchange Server コネクタの **[パスワードの設定]** を構成して **[モバイル デバイスがロックされるまでのアイドル時間 (分)]** を設定します。  


#### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>モバイル デバイスを登録できるユーザーを制限する  

モバイル デバイスを登録できるユーザーを制限すると、権限の昇格を防ぐのに役立つ 許可されたユーザーだけがモバイル デバイスを登録できるようにするには、既定のクライアント設定ではなくカスタム クライアント設定を使用します。  


#### <a name="user-device-affinity-guidance-for-mobile-devices"></a>モバイル デバイスのユーザー デバイス アフィニティのガイダンス  

次のシナリオでは、Configuration Manager または Microsoft Intune で登録されたモバイル デバイスを持つユーザーにアプリケーションを展開しないでください。  

-   複数のユーザーが 1 台のモバイル デバイスを使用する。  

-   ユーザーの代理で管理者がデバイスを登録する。  

-   デバイスをインベントリから削除してから再登録する手順を行わずに、別のユーザーにデバイスを譲渡する。  

デバイスの登録は、ユーザーとデバイスのアフィニティのリレーションシップを作成します。 このリレーションシップは、登録を実行するユーザーをモバイル デバイスにマップします。 別のユーザーがモバイル デバイスを使用する場合、元のユーザーに展開されたアプリケーションを実行できます。その結果、特権が昇格する可能性があります。 同様に、管理者がユーザーのモバイル デバイスを登録する場合、ユーザーに対して展開されたアプリケーションがモバイル デバイスにインストールされません。 代わりに、管理者に対して展開されたアプリケーションがインストールされる場合があります。  

Windows コンピューターに対するユーザーとデバイスのアフィニティとは異なり、Microsoft Intune によって登録されたモバイル デバイスではユーザーとデバイスのアフィニティの情報を手動で定義できません。  

Intune によって登録されたモバイル デバイスの所有権を譲渡する場合は、最初に Intune からモバイル デバイスの登録を解除します。 これにより、ユーザーとデバイスのアフィニティのリレーションシップが削除されます。 その後、現在のユーザーにデバイスの再登録を要求します。  


#### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>ユーザーが必ず自分で Microsoft Intune にモバイル デバイスを登録する  

登録の間に、ユーザーとデバイスのアフィニティのリレーションシップが作成されます。 これにより、登録を実行するユーザーがモバイル デバイスにマップされます。 管理者がユーザーのモバイル デバイスを登録する場合、ユーザーに対して展開されたアプリケーションがモバイル デバイスにインストールされません。 代わりに、管理者に対して展開されたアプリケーションがインストールされる場合があります。  


#### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>Configuration Manager サイト サーバーと Exchange Server の間の接続を保護する   

Exchange Server がオンプレミスの場合は、IPsec を使います。 ホストされた Exchange は、SSL を使って接続を自動的に保護します。  


#### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>コンピューターに対する最小限の特権という原則を使用する  

Exchange Server コネクタで最低限必要とされるコマンドレットの一覧については、「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)」をご覧ください。  



##  <a name="bkmk_macs"></a> Mac コンピューターのセキュリティのベスト プラクティス  


#### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>クライアント ソース ファイルを安全な場所に保存してアクセスする  

Configuration Manager は、Mac コンピューターにクライアントをインストールまたは登録する前に、クライアント ソース ファイルが改ざんされたかどうかを検証しません。 信頼できるソースからこれらのファイルをダウンロードします。 安全に格納し、それらにアクセスします。  


#### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>証明書の有効期間を監視して追跡する  

業務の継続性を確保するには、Mac コンピューター用に使用する証明書の有効期間を監視および追跡します。 Configuration Manager はこの証明書の自動更新をサポートしたり、証明書の期限切れが近いことを警告したりしません。 一般的な有効期間は 1 年間です。  

証明書の更新方法については、[Mac クライアント証明書の手動更新](/sccm/core/clients/deploy/deploy-clients-to-macs#renewing-the-mac-client-certificate)に関するページをご覧ください。  


#### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>SSL に対してのみ信頼されたルート証明書を構成する  

特権の昇格から保護するために、信頼されたルート証明機関の証明書を、SSL プロトコルに対してのみ信頼されるように構成します。

Mac コンピューターを登録すると、構成マネージャー クライアントを管理するためのユーザー証明書が自動的にインストールされます。 このユーザー証明書には、その信頼チェーン内の信頼されたルート証明書が含まれます。 SSL プロトコルに対してのみこのルート証明書を信頼するように制限するには、次の手順を使用します。  

1.  Mac コンピューターで、ターミナル ウィンドウを開きます。  

2.  次のコマンドを入力します。`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3.  **[Keychain Access]\(キーチェーン アクセス\)** ダイアログ ボックスの **[Keychains]\(キーチェーン\)** セクションで、**[System]\(システム\)** をクリックします。 次に、**[Category]\(カテゴリ\)** セクションで、**[Certificates]\(証明書\)** をクリックします。  

4.  Mac クライアント証明書のルート CA 証明書を検索して、ダブルクリックします。  

5.  ルート CA 証明書のダイアログ ボックスで、**[信頼]** セクションを展開し、次の変更を行います。  

    1.  **[When using this certificate]\(この証明書を使用するとき\)**: **[Always Trust]\(常に信頼\)** の設定を **[Use System Defaults]\(システムデフォルトを使用\)** に変更します。  

    2.  **[Secure Sockets Layer (SSL)]**: **[no value specified]\(値が指定されていません\)** を **[Always Trust]\(常に信頼\)** に変更します。  

6.  ダイアログ ボックスを閉じます。 管理者のバスワードを入力するようにダイアログが表示されたら、パスワードを入力して、**[Update Settings]\(設定の更新\)** をクリックします。  

この手順を完了すると、ルート証明書は SSL プロトコルを検証するためにのみ信頼されるようになります。 Secure Mail (S/MIME)、Extensible Authentication (EAP)、コード署名などの他のプロトコルは、このルート証明書では信頼されなくなります。  

> [!NOTE]  
>  また、Configuration Manager とは独立してクライアント証明書をインストールした場合も、この手順を使います。  



##  <a name="BKMK_SecurityIssues_Clients"></a> Configuration Manager クライアントのセキュリティの問題  

次のセキュリティに関する問題には軽減策がありません。  


#### <a name="status-messages-arent-authenticated"></a>ステータス メッセージが認証されない  

ステータス メッセージに対しては認証作業は行われません。 管理ポイントが HTTP クライアント接続を受け入れると、どのデバイスでも管理ポイントにステータス メッセージを送信できます。 管理ポイントが HTTPS クライアント接続しか受け入れない場合は、デバイスは、有効なクライアント認証証明書を取得する必要がありますが、ステータス メッセージを送信することもできます。 管理ポイントは、クライアントから受け取った無効な状態メッセージを破棄します。  

この脆弱性に対していくつかの攻撃の可能性が考えられます。 
- 攻撃者は、偽のステータス メッセージを送信し、ステータス メッセージ クエリに基づいてコレクションのメンバーシップを取得することができます。 
- 任意のクライアントが、管理ポイントに大量のステータス メッセージを送信することで管理ポイントに対するサービス拒否攻撃を開始する可能性があります。 
- ステータス メッセージがステータス メッセージ フィルター規則内の動作をトリガーしている場合、攻撃者はステータス メッセージ フィルター規則をトリガーできます。 
- 攻撃者は、レポート情報を不正確なものにするステータス メッセージを送信できます。  


#### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>対象外のクライアントがポリシーの対象に変更される可能性がある  

1 つのクライアントを対象としたポリシーをまったく異なるクライアントに適用するために攻撃者が使用できる方法がいくつかあります。 たとえば、信頼されたクライアントを使用する攻撃者が、偽のインベントリ情報や探索情報を送信して、所属すべきでないコンピューターをコレクションに追加します。 そのクライアントは、そのコレクションに対するすべての展開を受け取ります。 

攻撃者がポリシーを直接変更することを防ぐのに役立つ制御が存在します。 ただし、攻撃者は、OS を再フォーマットして再展開する既存のポリシーを取得し、それを別のコンピューターに送信する場合があります。 このリダイレクトされたポリシーが、サービス拒否攻撃を作成する可能性があります。 これらの種類の攻撃には、正確なタイミングと、Configuration Manager インフラストラクチャに関する広範囲にわたる知識が必要です。  


#### <a name="client-logs-allow-user-access"></a>クライアント ログに対するユーザー アクセスが許可される  

すべてのクライアント ログ ファイルは、"*読み取り*" アクセス権を持つ **Users** グループと、"*書き込み*" アクセス権を持つ特殊な**対話**ユーザーを許可します。 詳細ログ記録を有効にすると、攻撃者がログ ファイルを読み取って、コンプライアンス対応またはシステムの脆弱性に関する情報を探す可能性があります。 ユーザーのコンテキストでクライアントがインストールするソフトウェアなどのプロセスは、権限の低いユーザー アカウントを使用してログに書き込む必要があります。 この動作は、攻撃者も権限の低いアカウントを使用してログに書き込めることを意味します。  

最も重大なリスクは、攻撃者がログ ファイル内の情報を削除できることです。 それは、管理者が監査や侵入検出のために必要な情報かもしれません。  


#### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>モバイル デバイス登録用に設計された証明書を取得するのにコンピューターが使用される  

Configuration Manager は、登録要求を処理するとき、その要求がコンピューターではなくモバイル デバイスから送られたことを確認することはできません。 要求がコンピューターから送られた場合、そのコンピューターは PKI 証明書をインストールし、その証明書を使ってコンピューターを Configuration Manager に登録することができます。 

このような特権の昇格攻撃を防ぐためには、信頼されたユーザーにのみモバイル デバイスの登録を許可します。 サイトでのデバイス登録アクティビティを注意して監視してください。  


#### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>ブロックされたクライアントがまだ管理ポイントにメッセージを送信できる

信頼しなくなったクライアントをブロックしても、クライアントがクライアント通知用のネットワーク接続を確立していた場合は、Configuration Manager はセッションを切断しません。 ブロックされたクライアントは、ネットワークから切断されるまで、引き続き管理ポイントにパケットを送信できます。 これらのパケットは、小さなキープアライブ パケットのみです。 このクライアントは、ブロック解除されるまで、Configuration Manager では管理できません。  


#### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>自動クライアント アップグレードで管理ポイントが検証されない

自動クライアント アップグレードを使うと、クライアントはクライアント ソース ファイルをダウンロードするために管理ポイントにリダイレクトされることがあります。 このシナリオで、クライアントは管理ポイントを信頼されたソースとして検証しません。  


#### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>初めて Mac コンピューターを登録する場合、DNS スプーフィングのリスクがある  

Mac コンピューターが登録中に登録プロキシ ポイントに接続するときに、多くの場合、Mac コンピューターには信頼されたルート CA 証明書がありません。 この時点で、Mac コンピューターからサーバーが信頼されておらず、ユーザーには続行するようにダイアログが表示されます。 登録プロキシ ポイントの完全修飾ドメイン名 (FQDN) が偽の DNS サーバーによって解決されると、Mac コンピューターが偽の登録プロキシ ポイントに接続され、信頼されていないソースから証明書がインストールされる可能性があります。 このリスクを低減するには、使用する環境での DNS スプーフィングを回避するベスト プラクティスに従います。  


#### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>Mac の登録では証明書の要求に制限がない  

ユーザーは新しいクライアント証明書を要求するたびに Mac コンピューターを再登録できます。 Configuration Manager は複数の要求をチェックせず、1 台のコンピューターから要求される証明書の数を制限しません。 偽のユーザーが、コマンドライン登録要求を繰り返すスクリプトを実行できます。 この攻撃により、ネットワークまたは発行元証明機関 (CA) でサービス拒否が発生する可能性があります。 このリスクを低減するには、発行元の CA で、こうした種類の疑わしい動作を注意深く監視します。 こうしたパターンの動作を示すコンピューターは、Configuration Manager 階層からすぐにブロックします。  


#### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>ワイプの確認では、デバイスが正常にワイプされたかどうかが検証されない  

ユーザーがモバイル デバイスのワイプ操作を開始し、Configuration Manager がワイプを確認するとき、検証されるのは、Configuration Manager が正常にメッセージを "*送信した*" ことです。 デバイスが要求に従って "*動作した*" ことは検証されません。 

Exchange Server コネクタで管理されるモバイル デバイスでは、ワイプの確認は、Exchange でコマンドが受信されたことを検証しますが、デバイスで受信されたかどうかは検証しません。  


#### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>Windows Embedded デバイスでの変更をコミットするオプションを使用している場合、予想よりも早くアカウントが使用不可になることがあります  

Windows Embedded デバイスが、Windows 7 より前のバージョンの OS を実行している場合、Configuration Manager によって書き込みフィルターが無効にされている間にユーザーがログオンしようとすると、Windows が許可する不正ログオン試行回数は、アカウントが使用不可になるように構成されている回数の半分だけです。 

たとえば、**アカウントのロックアウトのしきい値**のドメイン ポリシーを 6 回に構成します。 ユーザーがパスワードの入力を 3 回間違えると、アカウントがロックアウトされます。この動作は、サービス拒否攻撃を効果的に作成します。 このシナリオでユーザーが組み込みデバイスにサインインする必要がある場合、使用不可のしきい値が低くなる可能性についてユーザーに注意してください。  



##  <a name="BKMK_Privacy_Clients"></a> Configuration Manager クライアントのプライバシー情報  

構成マネージャー クライアントを展開するときは、Configuration Manager 機能のクライアント設定を有効にします。 機能の構成に使用する設定は、Configuration Manager 階層内のすべてのクライアントに適用できます。 この動作は、クライアントが内部ネットワークに直接接続されていても、リモート セッション経由で接続されていても、インターネットに接続されていても同じです。  

クライアントの情報は、SQL サーバー内の Configuration Manager データベースに格納され、Microsoft に送信されることはありません。 情報は、サイト メンテナンス タスクの**期限切れの探索データの削除**によって 90 日ごとに削除されるまで、データベースに保持されます。 削除間隔は構成できます。 

いくつかの要約または集計された診断と使用状況データは、Microsoft に送信されます。 詳細については、「[診断結果と使用状況データ](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)」を参照してください。  

Configuration Manager クライアントを構成する前に、プライバシー要件について検討してください。  


### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Configuration Managerに登録されたモバイル デバイスのプライバシー情報  

Configuration Manager でモバイル デバイスを登録するときのプライバシー情報について詳しくは、「[System Center Configuration Manager privacy statement - Mobile device addendum](/sccm/core/misc/privacy/privacy-statement-mobile-device-addendum)」(System Center Configuration Manager のプライバシーに関する声明 - モバイル デバイスに関する補遺) をご覧ください。  


### <a name="client-status"></a>クライアント ステータス  

Configuration Manager はクライアントのアクティビティを監視します。 Configuration Manager は構成マネージャー クライアントを定期的に評価し、クライアントとその依存関係に関する問題を修復することができます。 クライアント ステータスは既定で有効になります。 クライアント アクティビティのチェック用にサーバー側のメトリックを使います。 クライアント ステータスは、自己チェック、修復、およびサイトへのクライアント ステータス情報の送信に、クライアント側アクションを使います。 クライアントはユーザーが構成したスケジュールに従って、自己チェックを実行します。 クライアントはチェックの結果を Configuration Manager サイトに送信します。 この情報は、転送中、暗号化されます。  

クライアント ステータス情報は、SQL サーバー内の Configuration Manager データベースに格納され、Microsoft に送信されることはありません。 この情報は、暗号化された形式でデータベースに格納されるわけではありません。 この情報は、クライアント ステータスの設定 **[クライアント ステータス履歴を保持する日数]** で構成された値に従って削除されるまで、データベースに保持されます。 この設定の既定値は 31 日ごとです。  

Configuration Manager クライアントをクライアント ステータス チェック機能と共にインストールする前に、プライバシー要件を検討してください。  



##  <a name="BKMK_Privacy_ExchangeConnector"></a> Exchange Server コネクタを使用して管理されるモバイル デバイスのプライバシー情報  

Exchange Server コネクタは、ActiveSync プロトコルを使うことによってオンプレミスまたはホスト型の Exchange Server に接続するデバイスを見つけて管理します。 Exchange Server コネクタにより検出されたレコードは、SQL サーバーの Configuration Manager データベースに格納されます。 この情報は、Exchange Server から収集されます。 これには、モバイル デバイスが Exchange Server に送信したその他の情報は一切含まれません。  

モバイル デバイス情報がマイクロソフトに送信されることはありません。 その後、モバイル デバイス情報が SQL サーバーの Configuration Manager データベースに格納されます。 情報は、サイト メンテナンス タスクの**期限切れの探索データの削除**によって 90 日ごとに削除されるまで、データベースに保持されます。 削除間隔はユーザーが構成します。  

Exchange Server をインストールして構成する前に、プライバシー要件を検討してください。  
