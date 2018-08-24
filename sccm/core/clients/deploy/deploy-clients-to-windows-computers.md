---
title: Windows にクライアントを展開する
titleSuffix: Configuration Manager
description: 構成マネージャー クライアントを Windows コンピューターに展開する方法を説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6eaac644b876fa3adfa1a2c79e7c4c5810942d9f
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385577"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Configuration Manager でクライアントを Windows コンピューターに展開する方法

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、構成マネージャー クライアントを Windows コンピューターに展開する方法を説明します。 クライアントの展開の計画と準備について詳しくは、次の記事をご覧ください。
- [クライアント インストール方法](/sccm/core/clients/deploy/plan/client-installation-methods)  
- [Windows コンピューターにクライアントを展開するための前提条件](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers)   
- [構成マネージャー クライアントのセキュリティとプライバシー](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  
- [クライアント展開のベスト プラクティス](/sccm/core/clients/deploy/plan/best-practices-for-client-deployment)  



##  <a name="BKMK_ClientPush"></a> クライアント プッシュ インストール 

クライアント プッシュを使う方法は主に次の 3 つです。  

- サイトに対してクライアント プッシュ インストールを構成するときに、サイトが検出したコンピューターでクライアントのインストールを自動的に実行します。 この方法の範囲は、サイトの境界が境界グループとして構成されているときの、構成済みの境界です。  

- 特定のコレクションまたはコレクション内のリソースでクライアント プッシュ インストール ウィザードを実行して、クライアント プッシュ インストールを開始します。  

- クライアント プッシュ インストール ウィザードを使って、[クエリ](/sccm/core/servers/manage/queries-technical-reference)の結果に構成マネージャー クライアントをインストールします。 インストールが成功するには、クエリで返される項目の 1 つが、**System Resource** クラスからの **ResourceID** 属性である必要があります。   

サイト サーバーは、クライアント コンピューターにアクセスできない場合やセットアップ プロセスを開始できない場合、1 時間ごとに自動的にインストールを再試行します。 サーバーは、最大 7 日間再試行を続けます。  

クライアントのインストール プロセスを追跡するには、クライアントをインストールする前に、フォールバック ステータス ポイントをインストールします。 インストールしたフォールバック ステータス ポイントは、クライアント プッシュ インストール方法でクライアントをインストールするときに、自動的にクライアントに割り当てられます。 クライアントのインストールの進行状況を追跡するには、クライアント展開レポートとクライアント割り当てレポートを確認します。 

クライアント ログ ファイルは、トラブルシューティングに関する詳細な情報を提供します。 ログ ファイルには、フォールバック ステータス ポイントは不要です。 たとえば、サイト サーバー上の **CCM.log** ファイルには、コンピューターに接続するときのサイト サーバーからの問題がすべて記録されます。 クライアント上の **CCMSetup.log** ファイルには、インストール プロセスが記録されます。  

> [!IMPORTANT]  
>  クライアント プッシュが正常に実行されるように、前提条件がすべて満たされていることを確認してください。 詳細については、「[インストール方法の依存関係](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies)」をご覧ください。  


### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>検出されたコンピューターに対してクライアント プッシュを自動的に使用するようにサイトを構成する

1.  Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[サイトの構成]** を展開して **[サイト]** ノードを選択します。  

2.  サイト全体の自動クライアント プッシュ インストールを構成するサイトを選択します。  

3.  リボンの **[ホーム]** タブの **[設定]** グループで、**[クライアント インストール設定]**、**[クライアント プッシュ インストール]** の順に選択します。  

4.  [クライアント プッシュ インストールのプロパティ] ウィンドウの **[全般]** タブで、**[サイト全体にクライアントを自動的にプッシュ インストールする]** を選択します。   

5. バージョン 1806 以降では、サイトを更新すると、クライアント プッシュの Kerberos チェックが有効になります。 以前の動作と同じように、**[NTLM への接続フォールバックを許可する]** オプションは既定で有効になります。 サイトが Kerberos を使ってクライアントを認証できない場合、NTLM を使って接続が再試行されます。 セキュリティを強化するため、この設定を無効にすることをお勧めします。そのためには、NTLM フォールバックなしの Kerberos が必要です。<!--1358204-->  

    > [!Note]  
    > クライアント プッシュを使って構成マネージャー クライアントをインストールすると、サイト サーバーによってクライアントへのリモート接続が作成されます。 バージョン 1806 以降のサイトでは、接続を確立する前の NTLM へのフォールバックを許可しないことによって、Kerberos の相互認証を要求できます。 この機能強化は、サーバーとクライアント間の通信をセキュリティで保護するのに役立ちます。  
    > 
    > セキュリティ ポリシーによっては、お客様の環境は既に以前の NTLM 認証よりも Kerberos に適している場合、または Kerberos を必要としている場合があります。 これらの認証プロトコルに関するセキュリティの考慮事項について詳しくは、[NTLM を制限する Windows セキュリティ ポリシーの設定](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations)に関するページをご覧ください。  
    > 
    > この機能を使用するには、信頼された Active Directory フォレスト内にクライアントがいる必要があります。 Windows の Kerberos は、相互認証を Active Directory に依存しています。  

6.  Configuration Manager でクライアント ソフトウェアをプッシュするシステムの種類を選択します。 ドメイン コント ローラーにクライアントをインストールするかどうかを選択します。  

7.  **[アカウント]** タブで、ターゲット コンピューターに接続するときに Configuration Manager が使うアカウントを 1 つ以上指定します。 **[作成]** アイコンをクリックし、**[ユーザー名]** と 「**パスワード**」 (38 文字以内) を入力して、パスワードを確認入力してから、**[OK]** をクリックします。 クライアント プッシュ インストール アカウントを少なくとも 1 つ指定します。 クライアントをインストールするには、このアカウントにターゲット コンピューターでのローカル管理者権限が必要です。 クライアント プッシュ インストール アカウントを指定しないと、Configuration Manager はサイト システムのコンピューター アカウントを使います。 サイト システムのコンピューター アカウントを使った場合、クロス ドメインのクライアント プッシュは失敗します。  

    > [!NOTE]  
    >  セカンダリ サイトからのクライアント プッシュを使うには、クライアント プッシュを開始するセカンダリ サイトのアカウントを指定します。  
    >   
    >  クライアント プッシュ インストール アカウントについては、次の手順「[クライアント プッシュ インストール ウィザードを使用する](#use-the-client-push-installation-wizard)」をご覧ください。  

8.  **[インストールのプロパティ]** タブを完了します。

     Configuration Manager 用に Active Directory スキーマを拡張した場合、サイトでは指定された[クライアント インストール プロパティ](/sccm/core/clients/deploy/about-client-installation-properties)が Active Directory Domain Services に発行されます。 CCMSetup は、実行時にインストール プロパティがないと、Active Directory からプロパティを読み取ります。  

    > [!NOTE]  
    >  セカンダリ サイトでクライアント プッシュ インストールを有効にする場合は、**SMSSITECODE** プロパティをその親プライマリ サイトの Configuration Manager サイト コードに設定します。 Active Directory スキーマを Configuration Manager 用に拡張した場合、正しいサイトの割り当てを自動的に発見するには、このプロパティを **AUTO** に設定します。  


### <a name="use-the-client-push-installation-wizard"></a>クライアント プッシュ インストール ウィザードを使用する

1.  Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[サイトの構成]** を展開して **[サイト]** ノードを選択します。  

2.  サイト全体の自動クライアント プッシュ インストールを構成するサイトを選択します。  

3.  リボンの **[ホーム]** タブの **[設定]** グループで、**[クライアント インストール設定]**、**[クライアント プッシュ インストール]** の順に選択します。  

4.  **[インストールのプロパティ]** タブを完了します。  

    Configuration Manager 用に Active Directory スキーマを拡張した場合、サイトでは指定された[クライアント インストール プロパティ](/sccm/core/clients/deploy/about-client-installation-properties)が Active Directory Domain Services に発行されます。 CCMSetup は、実行時にインストール プロパティがないと、Active Directory からプロパティを読み取ります。   

5.  Configuration Manager コンソールで、**[資産とコンプライアンス]** ワークスペースに移動します。  

6.  **[デバイス]** ノードで、1 つ以上のコンピューターを選択します。 または、**[デバイス コレクション]** ノードで、コンピューターのコレクションを選択します。  

7.  リボンの **[ホーム]** タブで、以下のオプションのいずれかを選びます。  

    -   クライアントを 1 つまたは複数のデバイスにプッシュするには、**[デバイス]** グループで、**[クライアントのインストール]** を選択します。  

    -   クライアントをデバイスのコレクションにプッシュするには、**[コレクション]** グループで、**[クライアントのインストール]** を選択します。  

8. クライアントのインストール ウィザードの **[開始する前に]** ページで情報を確認してから、**[次へ]** を選択します。  

9. **[インストール オプション]** ページを完了します。  

10. インストールの設定を確認してから、ウィザードを完了します。  

> [!NOTE]  
> サイトがクライアント プッシュ用に構成されていない場合でも、このウィザードを使ってクライアントをインストールします。  



##  <a name="BKMK_ClientSUP"></a> ソフトウェアの更新に基づいたインストール  

ソフトウェアの更新に基づいたクライアント インストールでは、クライアントをソフトウェア更新プログラムとしてソフトウェアの更新ポイントに発行します。 初回のインストールまたはアップグレードには、この方法を使用します。  

コンピューターに構成マネージャー クライアントがインストールされている場合、クライアントはサイトからクライアント ポリシーを受け取ります。 このポリシーには、ソフトウェアの更新ポイントのサーバー名と、ソフトウェア更新プログラムの取得元のポートが含まれます。   

> [!IMPORTANT]  
>  ソフトウェアの更新に基づいたインストールの場合は、クライアントのインストールとソフトウェア更新プログラムに同じ Windows Server Update Services (WSUS) サーバーを使います。 このサーバーは、プライマリ サイトでアクティブなソフトウェアの更新ポイントである必要があります。 詳細については、「[Install a software update point](/sccm/sum/get-started/install-a-software-update-point)」 (ソフトウェアの更新ポイントのインストール) をご覧ください。  

コンピューターに構成マネージャー クライアントがインストールされていない場合は、グループ ポリシー オブジェクトを構成して割り当てます。 このグループ ポリシーでは、ソフトウェアの更新ポイントのサーバー名を指定します。  

ソフトウェア更新プログラムに基づいたクライアント インストールに、コマンド ライン プロパティを追加することはできません。 Configuration Manager 用に Active Directory スキーマを拡張した場合、クライアントのインストールでは、Active Directory Domain Services でインストール プロパティが自動的に照会されます。  

Active Directory スキーマを拡張していない場合は、グループ ポリシーを使って、クライアント インストールの設定をプロビジョニングします。 これらの設定は、ソフトウェアの更新に基づいたクライアント インストールに自動的に適用されます。 詳しくは、[クライアント インストール プロパティのプロビジョニング方法](#BKMK_Provision)に関するセクションおよび[サイトにクライアントを割り当てる方法](/sccm/core/clients/deploy/assign-clients-to-a-site)に関する記事をご覧ください。  

構成マネージャー クライアントでソフトウェアの更新ポイントを使わずにコンピューターを構成するには、次の手順を使います。 ソフトウェアの更新ポイントにクライアント ソフトウェアを発行するための手順もあります。  

> [!Tip]  
>  コンピューターが前のソフトウェアのインストールの後に保留中の再起動の状態になると、ソフトウェアの更新に基づいたクライアントのインストールによってコンピューターが再起動する可能性があります。  


### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>グループ ポリシー オブジェクトを構成してソフトウェアの更新ポイントを指定する  

1.  **グループ ポリシー管理コンソール**を使って、新規または既存のグループ ポリシー オブジェクトを開きます。  

2.  **[コンピューターの構成]**、**[管理用テンプレート]**、**[Windows コンポーネント]** の順に展開し、**[Windows Update]** を選択します。  

3.  設定 **[イントラネットの Microsoft 更新サービスの場所を指定する]** のプロパティを開いてから、**[有効]** を選択します。  

4.  **[更新を検出するためのイントラネットの更新サービスを設定する]**: ソフトウェアの更新ポイント サーバーの名前とポートを指定します。  

    -   完全修飾ドメイン名 (FQDN) を使うように Configuration Manager サイト システムを構成した場合は、FQDN 形式を使います。  

    -   Configuration Manager サイト システムが完全修飾ドメイン名 (FQDN) を使うように構成されていない場合は、短い名前の形式を使います。   

    > [!Tip]  
    >  ポート番号を確認するには、[WSUS で使用するポート設定の特定方法](/sccm/sum/plan-design/plan-for-software-updates)に関するページをご覧ください。  

     FQDN 形式の例: `http://server1.contoso.com:8530`  

5.  **イントラネット統計サーバーの設定**: 通常、この設定は同じサーバー名です。   

6.  クライアントをインストールしてソフトウェア更新プログラムを受け取るコンピューターに、グループ ポリシー オブジェクトを割り当てます。  


### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>構成マネージャー クライアントをソフトウェアの更新ポイントに発行する  

1.  Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[サイトの構成]** を展開して **[サイト]** ノードを選択します。  

2.  ソフトウェアの更新に基づいたクライアントのインストールを構成するサイトを選択します。  

3.  リボンの **[ホーム]** タブの **[設定]** グループで、**[クライアント インストール設定]** を選択し、**[ソフトウェアの更新に基づいたクライアントのインストール]** を選択します。  

4.  **[ソフトウェアの更新に基づいたクライアントのインストールを有効にする]** を選択します。  

5.  サイトのクライアントのバージョンが、ソフトウェアの更新ポイントでのバージョンより新しい場合は、**[新しいバージョンのクライアント パッケージが見つかりました]** ダイアログ ボックスが開きます。 **[はい]** をクリックして、最新バージョンを発行します。  

    > [!NOTE]  
    >  クライアント ソフトウェアをソフトウェアの更新ポイントにまだ発行していない場合、このボックスは空白になります。  

構成マネージャー クライアント用のソフトウェア更新プログラムは、新しいバージョンが存在する場合に自動的に更新されるわけではありません。 サイトを更新するときに、この手順を繰り返してクライアントを更新します。  



##  <a name="BKMK_ClientGP"></a> グループ ポリシーによるインストール 

Active Directory Domain Services のグループ ポリシーを使って、発行したり、構成マネージャー クライアントを割り当てたりします。 クライアントは、コンピューターの起動時にインストールされます。 グループ ポリシーを使うと、**[プログラムの追加と削除]** コントロール パネルにクライアントが表示され、ユーザーがインストールできるようになります。  

グループ ポリシーに基づいたインストールには、Windows インストーラー パッケージ **CCMSetup.msi** を使います。 このファイルは、サイト サーバーの `<ConfigMgr installation directory>\bin\i386` フォルダーにあります。 このファイルにプロパティを追加してインストールの動作を変更することはできません。  

> [!IMPORTANT]  
>  クライアント インストール ファイルにアクセスするためには、**管理者**権限を持っている必要があります。  

-   Active Directory スキーマが Configuration Manager 用に拡張されており、**[サイトのプロパティ]** ダイアログ ボックスの **[詳細設定]** タブで **[Active Directory Domain Services 内にこのサイトを発行する]** が選択されている場合、クライアント コンピューターは自動的に Active Directory Domain Services でインストール プロパティを検索します。 詳細については、「[Active Directory Domain Services に発行されたクライアント インストールのプロパティについて](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services)」をご覧ください。  

-   Active Directory スキーマを拡張していない場合、コンピューターの Windows レジストリにインストールのプロパティを格納するには、[クライアント インストール プロパティのプロビジョニング方法](#BKMK_Provision)に関するセクションをご覧ください。 クライアントはインストール時にこれらのインストール プロパティを使います。  

Active Directory Domain Services でグループ ポリシーを使ってソフトウェアをインストールする方法について詳しくは、「[How to use group policy to remotely install software](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server)」(グループ ポリシーを使用してソフトウェアをリモートでインストールする方法) をご覧ください。  



##  <a name="BKMK_Manual"></a> 手動インストール

**CCMSetup.exe** を使用してクライアント ソフトウェアをコンピューターに手動でインストールします。 サイト サーバー上の Configuration Manager インストール フォルダーの **Client** フォルダーで、このプログラムとそのサポート ファイルを探します。 サイトは次のようにネットワークに対してこのフォルダーを共有します。  

 `\\<Site Server Name>\SMS_<Site Code>\Client\`  

 `<Site Server Name>` はプライマリ サイト サーバーの名前、`<Site Code>` はクライアントが割り当てられているプライマリ サイト コードです。 クライアントでコマンド ラインから CCMSetup.exe を実行するには、このネットワークの場所に接続してから、コマンドを実行します。  

> [!IMPORTANT]  
>  クライアント インストール ファイルにアクセスするためには、**管理者**権限を持っている必要があります。  

CCMSetup.exe は、必要なすべての前提条件をクライアント コンピューターにコピーし、Windows インストーラー パッケージ (Client.msi) を呼び出してクライアントをインストールします。 Client.msi を直接実行することはできません。  

クライアント インストールの動作を変更するには、CCMSetup.exe と Client.msi の両方にコマンド ライン オプションを指定します。 Client.msi のプロパティを指定する前に、`/` で始まる CCMSetup のパラメーターを指定する必要があります。 次に例を示します。  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`    

この例では、クライアントは次のオプションを使ってインストールします。  

|オプション|説明|  
|--------------|-----------------|  
|`/mp:SMSMP01`|この CCMSetup パラメーターは、必要なクライアント インストール ファイルをダウンロードする管理ポイント SMSMP01 を指定します。|  
|`/logon`|この CCMSetup パラメーターは、既存の構成マネージャー クライアントがコンピューターで見つかった場合はインストールを停止するように指定します。|  
|`SMSSITECODE=AUTO`|この Client.msi プロパティは、使用する Configuration Manager サイト コードをクライアントが検索するように指定します。 たとえば、Active Directory Domain Services を使います。|  
|`FSP=SMSFP01`|Client.msi のこのプロパティで、SMSFP01 というフォールバック ステータス ポイントを使って、クライアント コンピューターから送信される状態メッセージを受信するように指定します。|  

 詳しくは、[クライアント インストールのパラメーターとプロパティ](/sccm/core/clients/deploy/about-client-installation-properties)に関するページをご覧ください。  

> [!Tip]  
> Azure AD の ID を使って最新の Windows 10 デバイスに構成マネージャー クライアントをインストールする手順については、「[認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる](/sccm/core/clients/deploy/deploy-clients-cmg-azure)」をご覧ください。 その手順は、イントラネットまたはインターネット上のクライアントに対するものです。  


### <a name="manual-installation-examples"></a>手動インストールの例

以下の例は、イントラネット上の Active Directory に参加しているクライアントに関するものです。 次の値を使います。  

- **MPSERVER**: 管理ポイントをホストするサーバー   
- **FSPSERVER**: フォールバック ステータス ポイントをホストするサーバー  
- **ABC**: サイト コード  
- **contoso.com**: ドメイン名  

すべてのサイト システム サーバーは、イントラネットの FQDN で構成されています。 Active Directory にサイト情報を発行してあります。  

クライアント コンピューターで以下の手順を始めます。  
1. ローカル管理者としてサインインします  
2. Z: ドライブを `\\MPSERVER\SMS_ABC\Client` にマップします  
3. コマンド プロンプトを Z: ドライブに切り替えます  

それから、次のいずれかのコマンドを実行します。  


#### <a name="manual-example-1"></a>手動の例 1  

`CCMSetup.exe`  

この例では、追加のパラメーターまたはプロパティなしでクライアントをインストールします。 クライアントは、次の設定を含む、Active Directory Domain Services に対して発行されたクライアント インストール プロパティで自動的に構成されます。  

- サイト コード: この設定では、クライアントの割り当て用に構成されている境界グループに、クライアントのネットワークの場所が含まれる必要があります。  
- 管理ポイント
- フォールバック ステータス ポイント
- HTTPS のみを使って通信します  

詳細については、「[Active Directory Domain Services に発行されたクライアント インストールのプロパティについて](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services)」をご覧ください。  


#### <a name="manual-example-2"></a>手動の例 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
この例では、Active Directory Domain Services が提供する自動構成をオーバーライドします。 クライアントの割り当て用に構成されている境界グループに、クライアントのネットワークの場所が含まれる必要はありません。 代わりに、インストールでは次の設定を指定します。
- サイト コード
- イントラネット管理ポイント 
- インターネット ベースの管理ポイント
- インターネットからの接続を受け入れるフォールバック ステータス ポイント
- 最長の有効期間を持つクライアント PKI 証明書 (該当する場合) を使います  



##  <a name="BKMK_ClientLogonScript"></a> ログオン スクリプトによるインストール

Configuration Manager では、構成マネージャー クライアント ソフトウェアをインストールするログオン スクリプトをサポートしています。 **CCMSetup.exe** プログラム ファイルをログオン スクリプトで使用して、クライアント インストールを開始します。  

ログオン スクリプト インストールの使用方法は、手動のクライアント インストールと同じです。 CCMSsetup.exe に対して `/logon` インストール パラメーターを指定します。 このパラメーターを指定すると、クライアントのいずれかのバージョンがコンピューターに既に存在する場合、クライアントはインストールされません。 この動作により、ログオン スクリプトが実行されるたびにクライアントの再インストールが発生することはなくなります。  

`/Source` パラメーターでインストール ソースを指定せず、`/MP` パラメーターでインストール取得元の管理ポイントを指定しないと、CCMSetup.exe は Active Directory Domain Services を検索して管理ポイントを探します。 この動作は、スキーマを Configuration Manager 用に拡張し、サイトを Active Directory Domain Services に発行している場合にのみ発生します。 または、クライアントが DNS または WINS を使用して管理ポイントを特定することもできます。  



##  <a name="BKMK_ClientApp"></a> パッケージとプログラムのインストール  

選択したデバイスのクライアント ソフトウェアをアップグレードするパッケージとプログラムを作成して展開するには、Configuration Manager を使います。 Configuration Manager には、通常使用される値をパッケージ プロパティに設定するパッケージ定義ファイルが付属しています。 追加のコマンド ライン パラメーターとプロパティを指定することで、クライアント インストールの動作をカスタマイズします。  

> [!NOTE]  
>  この方法では、Configuration Manager 2007 クライアントをアップグレードすることはできません。 代わりに、最新バージョンのクライアントが含まれたパッケージを自動的に作成して展開する自動クライアント アップグレードを使用します。 詳細については、「[クライアントをアップグレードする](/sccm/core/clients/manage/upgrade/upgrade-clients)」をご覧ください。  
>   
>  旧バージョンの構成マネージャー クライアントから移行する方法については、「[System Center Configuration Manager でのクライアント移行戦略の計画](/sccm/core/migration/planning-a-client-migration-strategy)」をご覧ください。  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>クライアント ソフトウェア用のパッケージとプログラムを作成する  

次の手順に従って、クライアント ソフトウェアをアップグレードするために構成マネージャー クライアント コンピューターに展開できる、Configuration Manager パッケージとプログラムを作成します。  

1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]** ワークスペースに移動し、**[アプリケーション管理]** を展開して **[パッケージ]** ノードを選択します。  

2.  リボンの **[ホーム]** タブの **[作成]** グループで、**[定義に基づいたパッケージの作成]** を選択します。  

3.  ウィザードの **[パッケージの定義]** ページで、**[発行元]** ドロップダウン リストから **[Microsoft]** を選択し、**[パッケージ定義]** の一覧から **[Configuration Manager クライアントのアップグレード]** を選択します。  

4.  **[ソース ファイル]** ページで、**[常にソース フォルダーからファイルを取得する]** を選択します。  

5.  **[ソース フォルダー]** ページで、**[ネットワーク パス (UNC 名)]** を選びます。 その後、クライアント インストール ファイルが含まれているサーバーと共有へのネットワーク パスを入力します。  

    > [!NOTE]  
    >  Configuration Manager の展開を実行するコンピューターが、指定したネットワーク フォルダーへのアクセス権を持っている必要があります。 ない場合、クライアントのインストールは失敗します。  

    クライアント インストールのプロパティを変更するには、**[Configuration Manager エージェントのサイレント アップグレードのプロパティ]** プログラム ダイアログ ボックスの **[全般]** タブで CCMSetup.exe のコマンド ラインを変更します。 既定のインストール プロパティは `/noservice SMSSITECODE=AUTO` です。  

6. クライアント アップグレード パッケージをホストする必要があるすべての配布ポイントにパッケージを配布します。 次に、アップグレードが必要なクライアントが含まれているデバイスのコレクションにパッケージを展開します。  



## <a name="bkmk_mdm"></a> Intune MDM で管理された Windows デバイス

Microsoft Intune で登録されたデバイスに構成マネージャー クライアントを展開します。 

この手順では、イントラネットに接続されている従来のクライアントに対するものです。 従来のクライアント認証方法を使います。 クライアントをインストールした後でデバイスを確実に管理された状態のままにするには、デバイスがイントラネット上にあり、Configuration Manager サイトの境界内にある必要があります。  

Azure AD の ID を使って最新の Windows 10 デバイスに構成マネージャー クライアントをインストールする手順については、「[認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる](/sccm/core/clients/deploy/deploy-clients-cmg-azure)」をご覧ください。

> [!NOTE]  
> 既定では、クライアント ソフトウェアがインストールされると、デバイスは Intune から登録解除されます。
> 
> バージョン 1710 以降では、クライアントは Intune から登録解除されません。 クライアントは、構成マネージャー クライアントと MDM の登録の両方を同時に持つことができます。 詳しくは、[共同管理の概要](/sccm/core/clients/manage/co-management-overview)に関するページをご覧ください。  


###  <a name="install-clients-with-intune"></a>Intune でクライアントをインストールする  

1. Intune で、Configuration Manager のクライアント インストール ファイル **ccmsetup.msi** を含む、[Windows 基幹業務アプリを追加](https://docs.microsoft.com/intune/lob-apps-windows)します。 このファイルは、サイト サーバーの `<ConfigMgr installation directory>\bin\i386` フォルダーにあります。  

2. Intune ソフトウェア パブリッシャーで、コマンド ライン パラメーターを入力します。 たとえば、イントラネット上の従来のクライアントでは次のコマンド ラインを使います。  

  `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<Your site code> DNSSUFFIX=<DNS Suffix of management point>"`  

   > [!Note]  
   > Azure AD 認証を使う最新の Windows 10 クライアントで使うコマンド ラインの例については、「[共同管理用に Windows 10 デバイスを準備する](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)」をご覧ください。  

3. 登録済みの Windows コンピューターのグループに[アプリを割り当て](https://docs.microsoft.com/intune/deploy-use/deploy-apps-in-microsoft-intune)ます。  



##  <a name="BKMK_ClientImage"></a> OS イメージのインストール

OS イメージの作成に使う参照コンピューターに、構成マネージャー クライアントをプレインストールします。   

> [!Important]  
> Configuration Manager のタスク シーケンスを使って OS イメージを展開するときに、[ConfigMgr クライアントの準備](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)タスク シーケンス ステップは、構成マネージャー クライアントを完全に削除します。  


### <a name="prepare-the-client-computer-for-imaging"></a>イメージング用にクライアント コンピューターを準備する  

1.  参照コンピューターに構成マネージャー クライアント ソフトウェアを手動でインストールします。 詳細については、[構成マネージャー クライアントの手動インストール方法](#BKMK_Manual)に関するセクションをご覧ください。  

    > [!IMPORTANT]  
    >  CCMSetup.exe コマンド ライン プロパティでクライアントに Configuration Manager サイト コードを指定しないでください。  

2.  コマンド プロンプトで「`net stop ccmexec`」と入力して、参照コンピューター上の **SMS Agent Host** サービス (Ccmexec.exe) を停止します。  

3.  参照コンピューターの **Windows** フォルダーから、ファイル **SMSCFG.INI** を削除します。  

4.  参照コンピューターのローカル コンピューター ストアに保存されている証明書を削除します。 たとえば、公開キー基盤 (PKI) 証明書を使用する場合、コンピューターをイメージ化する前に、**コンピューター**と**ユーザー**の**個人用**ストアの証明書を削除します。  

5.  クライアントを参照コンピューターとは別の Configuration Manager 階層にインストールする場合は、信頼されたルート キーを参照コンピューターから削除します。  

    > [!NOTE]  
    >  クライアントは、Active Directory Domain Services に管理ポイントを照会できない場合、信頼されたルート キーを使用して信頼された管理ポイントを検索します。 イメージングされたすべてのクライアントをマスター コンピューターと同じ階層に展開する場合は、信頼されたルート キーを所定の場所に残しておきます。 
    > 
    > クライアントを別の階層に展開する場合は、信頼されたルート キーを削除します。 また、信頼されたルート キーでクライアントをプロビジョニングします。 詳細については、「[信頼されたルート キーの計画](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK)」を参照してください。  

6.  イメージング ソフトウェアを使用して、参照コンピューターのイメージをキャプチャします。  

7.  イメージを対象コンピューターに展開します。  



##  <a name="BKMK_ClientWorkgroup"></a> ワークグループ コンピューター  

Configuration Manager は、ワークグループ内のコンピューターへのクライアント インストールをサポートします。 [構成マネージャー クライアントの手動インストール方法](#BKMK_Manual)に関するセクションで指定された方法を使って、ワークグループ コンピューターにクライアントをインストールします。  


### <a name="prerequisites"></a>[前提条件]  

-   各ワークグループ コンピューターにクライアントを手動でインストールします。 インストール時に、対話ユーザーはローカル管理者権限を持っている必要があります。  

-   Configuration Manager サイト サーバーのドメイン内のリソースにアクセスするには、このサイト用にネットワーク アクセス アカウントを構成します。 このアカウントをソフトウェアの配布サイト コンポーネントで指定します。 詳しくは、[サイト コンポーネント](/sccm/core/servers/deploy/configure/site-components)に関するページをご覧ください。  


### <a name="limitations"></a>制限事項  

-   ワークグループ クライアントは、Active Directory Domain Services から管理ポイントを特定できません。 代わりに、DNS、WINS、または別の管理ポイントを使う必要があります。  

-   グローバル ローミングはサポートされていません。 ワークグループ クライアントは、Active Directory Domain Services でサイト情報を照会できません。  

-   Active Directory 探索方法では、ワークグループ内のコンピューターを探索できません。  

-   ワークグループ コンピューターのユーザーにソフトウェアを展開することはできません。  

-   クライアント プッシュ インストール方法を使用して、ワークグループ コンピューターにクライアントをインストールすることはできません。  

-   ワークグループ クライアントの場合は、認証に Kerberos を使用できないので、手動の承認が必要です。  

-   配布ポイントとしてワークグループ クライアントを構成することはできません。 Configuration Manager では、配布ポイントであるコンピューターがドメインのメンバーに指定されている必要があります。  


### <a name="install-the-client-on-workgroup-computers"></a>ワークグループ コンピューターにクライアントインストールする  

前提条件を確認し、セクション「[Configuration Manager クライアントの手動インストール方法](#BKMK_Manual)」の指示に従います。  


#### <a name="workgroup-example-1"></a>ワークグループの例 1

この例では次の処理を行います。 
- イントラネット クライアント管理用のクライアントをインストールします
- サイト コードを指定します 
- 管理ポイントを検索するための DNS サフィックスを指定します  

   `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     
#### <a name="workgroup-example-2"></a>ワークグループの例 2

この例では、境界グループ内に構成されたネットワークの場所にクライアントを配置する必要があります。 この要件は、サイトの自動割り当てを成功させるために必要です。 コマンドには、サーバー FSPSERVER 上のフォールバック ステータス ポイントが含まれます。 このプロパティは、クライアントの展開を追跡し、クライアントの通信の問題を識別するのに役立ちます。 

   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> インターネット ベースのクライアント管理  
 
> [!Note]  
> このセクションの内容は、[クラウド管理ゲートウェイ](/sccm/core/clients/manage/plan-cloud-management-gateway)を使うクライアントには適用されません。 クラウド管理ゲートウェイを使ってインターネット ベースのクライアントをインストールするには、「[認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる](/sccm/core/clients/deploy/deploy-clients-cmg-azure)」をご覧ください。  

Configuration Manager サイトが、イントラネット上にある場合とインターネット上にある場合があるクライアントに対して[インターネットベースのクライアント管理](/sccm/core/clients/manage/plan-internet-based-client-management)をサポートするときは、次の 2 つの方法のいずれかを使って、イントラネット上のクライアントをインストールできます。  

-   クライアントをインストールするときに、Client.msi のプロパティ `CCMHOSTNAME=<internet FQDN of the internet-based management point>` を含めます。 たとえば、手動インストールやクライアント プッシュを使います。 この方法を使うときは、サイトにクライアントを直接割り当てます。 サイトの自動割り当てを使うことはできません。 [構成マネージャー クライアントの手動インストール方法](#BKMK_Manual)に関するセクションをご覧ください。この構成方法の例があります。  

-   イントラネットのクライアント管理用にクライアントをインストールしてから、インターネット ベースのクライアント管理ポイントをクライアントに割り当てます。 Configuration Manager コントロール パネルのクライアント プロパティを使うか、またはスクリプトを使って、管理ポイントを変更します。 この方法を使用するときに、自動クライアント割り当てを使用できます。 詳細については、「[クライアント インストール後のインターネット ベースのクライアント管理用のクライアントを構成するには](#BKMK_ConfigureIBCM_MP)」セクションをご覧ください。  

インターネット上のクライアントをインストールするには、以下のサポートされる方法の 1 つから選択します。  

-   これらのクライアントが VPN でイントラネットに一時的に接続するためのメカニズムを提供します。 その後、適切なクライアント インストール方法を使ってクライアントをインストールします。  

-   Configuration Manager に依存しないインストール方法を使います。 たとえば、リムーバブル メディアにクライアント インストール ソース ファイルをパッケージ化し、インストールするユーザーに送ります。 クライアント インストール ソース ファイルは、Configuration Manager サイト サーバーの `<InstallationPath>\Client` フォルダーにあります。 クライアント フォルダーを手動でコピーするスクリプトをメディアに含めます。 このフォルダーから、CCMSetup.exe および適切なすべての CCMSetup コマンド ライン プロパティを使用してクライアントをインストールします。  

> [!NOTE]  
>  Configuration Manager では、インターネット ベースの管理ポイントまたはインターネット ベースのソフトウェア更新ポイントからクライアントを直接インストールすることはサポートしていません。  

インターネット経由で管理されるクライアントは、インターネット ベースのサイト システムと通信する必要があります。 クライアントをインストールする前に、これらのクライアントが公開キー基盤 (PKI) 証明書も持っていることを確認します。 これらの証明書は Configuration Manager とは別にインストールします。 証明書の要件のについては、「[PKI 証明書の要件](/sccm/core/plan-design/network/pki-certificate-requirements)」をご覧ください。  


### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>CCMSetup コマンドライン プロパティを指定してインターネット上のクライアントをインストールする  

1.  [構成マネージャー クライアントの手動インストール方法](#BKMK_Manual)に関するセクションの指示に従います。 次のオプションを常に含めます。  

    -   CCMSetup のコマンド ライン パラメーター `/source:<local path to the copied Client folder>`  

    -   CCMSetup のコマンド ライン パラメーター `/UsePKICert`  

    -   Client.msi のプロパティ `CCMHOSTNAME=<FQDN of internet-based management point>`  

    -   Client.msi のプロパティ `SMSSIGNCERT=<local path to exported site server signing certificate>`  

    -   Client.msi のプロパティ `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    >  サイトに複数のインターネット ベースの管理ポイントがある場合、どのインターネット ベースの管理ポイントを CCMHOSTNAME プロパティに指定してもかまいません。 構成マネージャー クライアントが指定したインターネット ベースの管理ポイントに接続するときに、サイト内で使用できるインターネット ベースの管理ポイントの一覧が管理ポイントからクライアントに送信されます。 クライアントは一覧から 1 つをランダムに選びます。  

2.  クライアントで証明書失効リスト (CRL) を確認しないようにする場合は、CCMSetup コマンド ライン パラメーター `/NoCRLCheck` を指定します。  

3.  インターネット ベースのフォールバック ステータス ポイントを使用する場合、Client.msi プロパティ `FSP=<internet FQDN of the internet-based fallback status point>` を指定します。  

4.  インターネットのみのクライアント管理用にクライアントをインストールする場合、Client.msi プロパティ `CCMALWAYSINF=1` を指定します。  

5.  その他の CCMSetup コマンドライン パラメーターを指定する必要があるかどうかを確認します。 たとえば、クライアントに複数の有効な PKI 証明書がある場合は、場合によって証明書選択条件を指定する必要があります。 使用可能なプロパティの一覧については、[クライアント インストールのパラメーターとプロパティ](/sccm/core/clients/deploy/about-client-installation-properties)に関するページをご覧ください。  


#### <a name="internet-based-example"></a>インターネット ベースの例:  

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

この例では、次の動作を持つクライアントがインストールされます。
  - D ドライブのフォルダーにあるソース ファイルを使う
  - クライアント PKI 証明書を使う 
  - 有効期限の最も長い証明書を選ぶ 
  - インターネットのみのクライアント管理
  - SERVER1 という名前のインターネット ベースの管理ポイントを使うようにクライアントを割り当てる
  - contoso.com ドメインのインターネット ベースのフォールバック ステータス ポイントを割り当てる
  - ABC サイトにクライアントを割り当てる  


###  <a name="BKMK_ConfigureIBCM_MP"></a> クライアント インストール後のインターネット ベースのクライアント管理用のクライアントを構成するには  

クライアントのインストール後にインターネットベースの管理ポイントを割り当てるには、次のいずれかの手順に従います。 1 つ目の手順では手動で構成します。クライアントが少数の場合に適しています。 クライアントの数が多い場合は、2 つ目の手順が適しています。  


#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Configuration Manager コントロール パネルからクライアントをインストールした後、インターネットベースのクライアント管理用のクライアントを構成する  

1.  クライアントで **Configuration Manager** コントロール パネルを開きます。  

2.  **[インターネット]** タブで、**[インターネット FQDN]** としてインターネットベースの管理ポイントの完全修飾ドメイン名 (FQDN) を入力します。  

    > [!NOTE]  
    >  **[インターネット]** タブは、クライアントにクライアント PKI 証明書がある場合のみ使用できます。  

3.  クライアントがプロキシ サーバーを使ってインターネットにアクセスする場合は、プロキシ サーバーの設定を入力します。  


#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>クライアントのインストール後に、スクリプトを使用して、インターネットベースのクライアント管理用のクライアントを構成する  

1.  メモ帳などのテキスト エディターを開きます。  

2.  次の VBScript サンプルをコピーして、ファイルに挿入します。 *mp.contoso.com* を、使用するインターネットベースの管理ポイントのインターネット FQDN に置き換えます。  

    ``` VBScript 
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the internet-based management point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  指定したインターネット ベースの管理ポイントを削除するには、引用符内のサーバーの FQDN 値を削除します。 この行は次のようになります。`newInternetBasedManagementPointFQDN = ""`  

4.  ファイルを .vbs 拡張子で保存します。  

5.  cscript.exe を使って、次のいずれかの方法でクライアント コンピューターでスクリプトを実行します。  

    -   パッケージとプログラムを使用して、既存の Configuration Manager クライアントにファイルを展開する  

    -   Windows エクスプローラーでスクリプトをダブルクリックして、既存の Configuration Manager クライアントでファイルをローカルに実行する  

変更を適用するために、クライアントの再起動が必要になることがあります。  



##  <a name="BKMK_Provision"></a> グループ ポリシーおよびソフトウェアの更新に基づいたクライアント インストール用にクライアント インストール プロパティをプロビジョニングする

Configuration Manager のクライアント インストール プロパティでコンピューターをプロビジョニングするには、Windows グループ ポリシーを使います。 これらのプロパティは、コンピューターのレジストリに格納されます。 クライアントはインストールするときに読み取ります。 この手順は、通常必要ありませんが、次のような一部のクライアント インストール シナリオで必要となる場合があります。  

-   グループ ポリシー設定またはソフトウェア更新ベースのクライアント インストール方法を使っていて、 Active Directory スキーマを Configuration Manager 用に拡張していない場合。  

-   特定のコンピューターのクライアント インストール プロパティをオーバーライドする場合。  

> [!NOTE]  
>  CCMSetup.exe コマンド ラインで何らかのインストール プロパティを指定した場合、コンピューターにプロビジョニングされたインストール プロパティは使われません。  

Configuration Manager のインストール メディアには、**ConfigMgrInstallation.adm** というグループ ポリシー管理テンプレートが用意されています。 このテンプレートを使って、インストール プロパティでクライアント コンピューターをプロビジョニングします。   


### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>グループ ポリシー オブジェクトを使用してクライアント インストール プロパティの構成と割り当てを行う  

1.  Windows グループ ポリシー オブジェクト エディターなどのエディターを使い、新しいグループ ポリシー オブジェクトまたは既存のグループ ポリシー オブジェクトに、管理テンプレート **ConfigMgrInstallation.adm** をインポートします。 このファイルを Configuration Manager インストール メディアの `TOOLS\ConfigMgrADMTemplates` フォルダーで探します。  

2.  インポートした設定 **[クライアント展開の設定を構成する]** のプロパティを開きます。  

3.  **[有効]** を選択します。  

4.  **[CCMSetup]** ボックスに、必要な CCMSetup コマンドライン プロパティを入力します。 CCMSetup コマンド ライン プロパティの詳細と使用例については、[クライアント インストールのパラメーターとプロパティ](/sccm/core/clients/deploy/about-client-installation-properties)に関するページをご覧ください。  

5.  構成マネージャー クライアントのインストール プロパティをプロビジョニングするコンピューターにグループ ポリシー オブジェクトを割り当てます。  
