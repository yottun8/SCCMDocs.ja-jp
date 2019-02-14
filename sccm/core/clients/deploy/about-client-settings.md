---
title: クライアント設定
titleSuffix: Configuration Manager
description: クライアントの動作を制御する既定の設定とカスタム設定について説明します。
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b272a8988a3e8d2e09b4043c087207e62c59b274
ms.sourcegitcommit: 5e7c4d36f4cdb3390ad3b381d31a3e1e4bf3c6e1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2019
ms.locfileid: "55986588"
---
# <a name="about-client-settings-in-configuration-manager"></a>Configuration Manager のクライアント設定について

*適用対象:System Center Configuration Manager (Current Branch)*

すべてのクライアント設定は、Configuration Manager コンソールの **[管理]** ワークスペースの **[クライアント設定]** ノードから管理します。 Configuration Manager には、一連の既定の設定が用意されています。 既定のクライアント設定を変更すると、変更された設定が階層内のすべてのクライアントに適用されます。 カスタムのクライアント設定も構成でき、これらの設定をコレクションに割り当てると、既定のクライアント設定をオーバーライドします。 詳しくは、「[クライアント設定を構成する方法](/sccm/core/clients/deploy/configure-client-settings)」をご覧ください。

以下のセクションでは、設定とオプションについて詳しく説明します。  
 

## <a name="background-intelligent-transfer-service-bits"></a>バックグラウンド インテリジェント転送サービス (BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>[BITS バックグラウンド転送の最大ネットワーク帯域幅を制限する]
このオプションを **[はい]** にすると、クライアントは BITS の帯域幅調整を使います。 このグループの他の設定を構成するには、この設定を有効にする必要があります。 

### <a name="throttling-window-start-time"></a>[調整期間の開始時間]
BITS 調整期間の開始時刻 (ローカル時刻) を指定します。  

### <a name="throttling-window-end-time"></a>[調整期間の終了時間]
BITS 調整期間の終了時刻 (ローカル時刻) を指定します。 終了時刻が **[調整期間の開始時間]** と同じ場合、BITS 調整は常に有効になります。  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>[調整期間内の最大転送速度 (Kbps)]
クライアントが調整期間中に使うことができる最大転送速度を指定します。  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>[調整期間外に BITS ダウンロードを許可する]
指定した期間外にクライアントが別の BITS 設定を使えるようにします。  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>[調整期間外の最大転送速度 (Kbps)]
BITS 調整期間外にクライアントが使うことのできる最大転送速度を指定します。  



## <a name="client-cache-settings"></a>クライアント キャッシュ設定

### <a name="configure-branchcache"></a>BranchCache の構成
クライアント コンピューターを [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache) 用に設定します。 クライアントで BranchCache のキャッシュを許可する場合は、**[BranchCache の有効化]** を **[はい]** に設定します。

- **BranchCache の有効化** </br>
    クライアント コンピューターで BranchCache を有効にします。

- **BranchCache キャッシュの最大サイズ (ディスクに占める割合)** </br>
    BranchCache が使うことのできるディスクの割合です。 

### <a name="configure-client-cache-size"></a>クライアント キャッシュ サイズの構成
Windows コンピューターの構成マネージャー クライアント キャッシュには、アプリケーションとプログラムのインストールに使われる一時ファイルが格納されます。 このオプションを **[いいえ]** に設定すると、既定サイズの 5,120 MB になります。

**[はい]** を選んだ場合は、次の値を指定します。
- **最大キャッシュ サイズ (MB)**
- **最大キャッシュ サイズ (ディスクの割合)** </br>
クライアント キャッシュのサイズは、最大サイズ (メガバイト (MB) 単位) またはディスク容量の割合のいずれか少ない方まで拡張します。 

### <a name="enable-configuration-manager-client-in-full-os-to-share-content"></a>完全な OS 上の Configuration Manager クライアントでコンテンツを共有できるようにする
構成マネージャー クライアントの[ピア キャッシュ](/sccm/core/plan-design/hierarchy/client-peer-cache)を有効にします。 **[はい]** を選んでから、クライアントがピア コンピューターと通信するためのポートを指定します。 
- **初期ネットワーク ブロードキャスト用ポート** (既定値: 8004)
- **ピアからのコンテンツのダウンロード用ポート** (既定値 8003) </br>
Configuration Manager は、このトラフィックを許可する Windows Firewall 規則を自動的に構成します。 別のファイアウォールを使用する場合、このトラフィックを許可するように手動でルールを構成する必要があります。




## <a name="client-policy"></a>クライアント ポリシー  

### <a name="client-policy-polling-interval-minutes"></a>[クライアント ポリシーのポーリング間隔 (分)]

次の構成マネージャー クライアントがクライアント ポリシーをダウンロードする頻度を指定します。
-   Windows コンピューター (デスクトップ、サーバー、ラップトップなど)  
-   Configuration Manager で登録されるモバイル デバイス  
-   Mac コンピューター  
-   Linux または UNIX を実行しているコンピューター  

### <a name="enable-user-policy-on-clients"></a>クライアントでユーザー ポリシーを有効にする

このオプションを **[はい]** に設定して、[ユーザーの探索](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser)を使うと、クライアントはサインイン ユーザーの対象になっているアプリケーションとプログラムを受け取ります。  

アプリケーション カタログは、ユーザーが利用可能なソフトウェアの一覧をサイト サーバーから受け取ります。 したがって、ユーザーがアプリケーション カタログを使ってアプリケーションを表示および要求する場合は、この設定を **[はい]** に設定する必要はありません。 この設定を **[いいえ]** にすると、ユーザーはアプリケーション カタログに表示されるアプリケーションをインストールできません。  

さらに、この設定を **[いいえ]** にすると、ユーザーに対して展開された必要なアプリケーションをユーザーは受け取りません。 ユーザーは、ユーザー ポリシーの他の管理タスクも受け取りません。  

この設定は、ユーザーのコンピューターがイントラネットまたはインターネットに接続されているときに適用されます。 インターネットでもユーザー ポリシーを有効にする場合は、**[はい]** にする必要があります。  

### <a name="enable-user-policy-requests-from-internet-clients"></a>インターネット クライアントからのユーザー ポリシー要求を有効にする

ユーザーがインターネット ベースのコンピューターを使っているときもユーザー ポリシーを受け取るようにするには、このオプションを **[はい]** に設定します。 以下の要件も適用されます。  

- クライアントとサイトは、[インターネット ベースのクライアント管理](/sccm/core/clients/manage/plan-internet-based-client-management)に対してか、[クラウド管理ゲートウェイ](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)に対して構成されます。  

- **[クライアントでユーザー ポリシーを有効にする]** が **[はい]** に設定されている。  

- インターネット ベースの管理ポイントが、Windows 認証 (Kerberos または NTLM) を使ってユーザーを正しく認証する。 詳細については、[インターネットからのクライアント通信に関する考慮事項](/sccm/core/plan-design/hierarchy/communications-between-endpoints#BKMK_clientspan)のページを参照してください。  

- バージョン 1710 より、クラウド管理ゲートウェイは Azure Active Directory を使用してユーザーを正常に認証するようになりました。 詳細については、[Azure AD 参加デバイスにユーザーが利用できるアプリケーションを展開する方法](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)に関するページを参照してください。  

このオプションを **[いいえ]** に設定した場合、または上記の要件のいずれかが満たされていない場合は、インターネット上のコンピューターはコンピューター ポリシーのみを受け取ります。 この場合は、ユーザーは、インターネットベースのアプリケーション カタログからアプリケーションを表示、要求、およびインストールできます。 この設定が **[いいえ]** に設定されていて、**[クライアントでユーザー ポリシーを有効にする]** が **[はい]** に設定されている場合は、コンピューターがイントラネットに接続されるまで、ユーザーはユーザー ポリシーを受け取りません。  

> [!NOTE]  
>  インターネットベースのクライアント管理の場合、ユーザーからのアプリケーションの承認要求には、ユーザー ポリシーまたはユーザー認証は必要ありません。 クラウド管理ゲートウェイでは、アプリケーション承認要求がサポートされません。   



## <a name="cloud-services"></a>クラウド サービス

### <a name="allow-access-to-cloud-distribution-point"></a>クラウド配布ポイントへのアクセスを許可する
クライアントがクラウド配布ポイントからコンテンツを取得できるようにする場合は、このオプションを **[はい]** に設定します。 この設定を有効にする場合、デバイスがインターネット ベースである必要はありません。

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>新しい Windows 10 ドメインに参加しているデバイスを自動的に Azure Active Directory に登録する 
ハイブリッド結合をサポートするように Azure Active Directory を構成すると、Configuration Manager はこの機能対応に Windows 10 デバイスを構成します。 詳しくは、「[ハイブリッド Azure Active Directory 参加済みデバイスの構成方法](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)」をご覧ください。

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>クライアントでクラウド管理ゲートウェイを使用できるようにする
既定では、すべてのインターネット ローミング クライアントは、使用可能な任意の[クラウド管理ゲートウェイ](/sccm/core/clients/manage/plan-cloud-management-gateway)を使います。 この設定を **[いいえ]** に構成するのは、たとえば、パイロット プロジェクト中やコスト節約のためなどに、サービスの使用のスコープを設定する場合です。



##  <a name="compliance-settings"></a>コンプライアンス設定  

### <a name="enable-compliance-evaluation-on-clients"></a>[クライアントのコンプライアンス評価を有効にする]
このグループの他の設定を構成するには、このオプションを **[はい]** に設定します。
 
### <a name="schedule-compliance-evaluation"></a>[コンプライアンスの評価スケジュールを設定する]
構成基準展開の既定のスケジュールを作成するには、**[スケジュール]** を選びます。 この値は、**[構成基準の展開]** ダイアログ ボックスの基準ごとに構成できます。  

### <a name="enable-user-data-and-profiles"></a>[ユーザー データとプロファイルを有効にする]
[ユーザー データとプロファイル](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items)の構成項目を展開する場合は、**[はい]** を選びます。



## <a name="computer-agent"></a>コンピューター エージェント  

### <a name="user-notifications-for-required-deployments"></a>必要な展開のユーザー通知

次の 3 つの設定について詳しくは、「[必要な展開のユーザー通知](/sccm/apps/deploy-use/deploy-applications#user-notifications-for-required-deployments)」をご覧ください。

-   **展開期限まで 24 時間以上の場合に、ユーザーに通知する間隔 (時間)**
-   **展開期限まで 24 時間未満の場合に、ユーザーに通知する間隔 (時間)** 
-   **展開期限まで 1 時間未満の場合に、ユーザーに通知する間隔 (分)** 

### <a name="default-application-catalog-website-point"></a>既定のアプリケーション カタログ Web サイト ポイント

> [!Note]  
> バージョン 1806 以降、アプリケーション カタログ Web サイト ポイントは "*必要*" ではなくなりましたが、まだ "*サポートされています*"。 詳しくは、「[ソフトウェア センターの構成](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex)」をご覧ください。 
> 
> アプリケーション カタログ Web サイト ポイントの **Silverlight ユーザー エクスペリエンス**は現在サポートされていません。 詳細については、[削除された機能と非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)に関するページを参照してください。  

Configuration Manager は、この設定を使用して、ソフトウェア センターからアプリケーション カタログにユーザーを接続します。 アプリケーション カタログ Web サイト ポイントをホストするサーバーを指定するには、**[サイトの設定]** を選びます。 NetBIOS 名または FQDN を入力するか、自動検出を指定するか、またはカスタマイズされた展開の URL を指定します。 ほとんどの場合、自動検出が最良の選択肢となります。

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>[既定のアプリケーション カタログ Web サイトを Internet Explorer の信頼済みサイト ゾーンに追加する]

> [!Note]  
> バージョン 1806 以降、アプリケーション カタログ Web サイト ポイントは "*必要*" ではなくなりましたが、まだ "*サポートされています*"。 詳しくは、「[ソフトウェア センターの構成](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex)」をご覧ください。 
> 
> アプリケーション カタログ Web サイト ポイントの **Silverlight ユーザー エクスペリエンス**は現在サポートされていません。 詳細については、[削除された機能と非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)に関するページを参照してください。  

このオプションが **[はい]** の場合、クライアントは現在の既定のアプリケーション カタログ Web サイトの URL を Internet Explorer の信頼済みサイト ゾーンに自動的に追加します。  

この設定では、Internet Explorer の保護モードの設定が有効になっていない必要があります。 保護モードが有効になっていると、Configuration Manager クライアントがアプリケーション カタログからアプリケーションをインストールできない可能性があります。 既定では、信頼済みサイト ゾーンは、Windows 認証が必要なアプリケーション カタログへのユーザー サインインもサポートしています。  

このオプションを **[いいえ]** のままにすると、構成マネージャー クライアントはアプリケーション カタログからアプリケーションをインストールできないことがあります。 別の方法としては、クライアントが使うアプリケーション カタログの URL 用に、別のゾーンで Internet Explorer のこれらの設定を構成します。  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>[Silverlight アプリケーションが管理者特権での信頼モードで実行されることを許可する]

> [!Important]  
> Configuration Manager バージョン 1802 以降では、クライアントは Silverlight を自動的にインストールしません。
> 
> バージョン 1806 以降では、アプリケーション カタログ Web サイト ポイントの **Silverlight ユーザー エクスペリエンス**はサポートされていません。 新しいソフトウェア センターを使う必要があります。 詳しくは、「[ソフトウェア センターの構成](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex)」をご覧ください。  

ユーザーがアプリケーション カタログを使う場合は、この設定を **[はい]** にする必要があります。  

この設定を変更すると、次にユーザーがブラウザーを読み込むか、現在開いているブラウザー ウィンドウを更新したときに、有効になります。  

この設定について詳しくは、「[Microsoft Silverlight 5 用の証明書、およびアプリケーション カタログに必要な管理者特権での信頼モード](/sccm/apps/plan-design/security-and-privacy-for-application-management#BKMK_CertificatesSilverlight5)」をご覧ください。  

### <a name="organization-name-displayed-in-software-center"></a>ソフトウェア センターに表示される組織名

ソフトウェア センターでユーザーに表示する名前を入力します。 このブランド情報によって、ユーザーはこのアプリケーションを信頼されるソースとして特定できます。 この設定の優先順位について詳しくは、「[ソフトウェア センターのブランド化](/sccm/apps/plan-design/plan-for-and-configure-application-management#branding-software-center)」をご覧ください。  

### <a name="use-new-software-center"></a>新しいソフトウェア センターの使用

Configuration Manager 1802 より、既定の設定は **[はい]** です。

このオプションを **[はい]** に設定すると、すべてのクライアント コンピューターが新しいソフトウェア センターを使います。 ソフトウェア センターでは、以前はアプリケーション カタログ内だけでアクセスできた、ユーザーが利用できるアプリが表示されます。 アプリケーション カタログには Silverlight が必要ですが、ソフトウェア センターではこれは前提条件ではありません。   

バージョン 1806 以降では、アプリケーション カタログの Web サイト ポイントの役割と Web サービス ポイントの役割は "*不要*" になりましたが、まだ "*サポートされています*"。 詳しくは、「[ソフトウェア センターの構成](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex)」をご覧ください。 
 
> [!Note]  
> アプリケーション カタログ Web サイト ポイントの **Silverlight ユーザー エクスペリエンス**は現在サポートされていません。 詳細については、[削除された機能と非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)に関するページを参照してください。  

### <a name="enable-communication-with-health-attestation-service"></a>正常性構成証明サービスとの通信を有効にします

Windows 10 デバイスで[正常性構成証明](/sccm/core/servers/manage/health-attestation)を使う場合は、このオプションを **[はい]** に設定します。 この設定を有効にすると、次の設定も構成できるようになります。

### <a name="use-on-premises-health-attestation-service"></a>オンプレミスの正常性構成証明サービスを使用する

デバイスがオンプレミスのサービスを使う場合は、このオプションを **[はい]** に設定します。 Microsoft クラウド ベースのサービスを使うデバイスでは、**[いいえ]** に設定します。  

### <a name="install-permissions"></a>インストール権限

> [!IMPORTANT]  
>  この設定は、アプリケーション カタログとソフトウェア センターに適用されます。 この設定は、ユーザーがポータル サイトを使うときには効果がありません。  

ソフトウェア、ソフトウェア更新プログラム、およびタスク シーケンスのインストールをユーザーがどのように開始するのかを構成します。  

-   **[すべてのユーザー]**:ゲスト以外のアクセス許可を持つユーザーです。  

-   **[管理者のみ]**:ユーザーは、ローカルの Administrators グループのメンバーである必要があります。  

-   **[管理者とプライマリ ユーザーのみ]**:ユーザーは、ローカルの Administrators グループのメンバーであるか、コンピューターのプライマリ ユーザーである必要があります。  

-   **[ユーザー以外]**:クライアント コンピューターにサインインしたユーザーは、ソフトウェア、ソフトウェア更新プログラム、およびタスク シーケンスのインストールを開始できません。 コンピューターに必須の展開は、期限になると必ずインストールされます。 アプリケーション カタログまたはソフトウェア センターからのソフトウェアのインストールをユーザーが開始することはできません。  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>[再起動時の BitLocker PIN の入力を一時停止する]

コンピューターで BitLocker PIN の入力が必要な場合、このオプションによって、ソフトウェアのインストール後にコンピューターを再起動するときに PIN 入力の要件がバイパスされます。  

-   **[常時]**:Configuration Manager は再起動が必要なソフトウェアのインストールを実行してコンピューターを再起動した後に、BitLocker を一時的に停止させます。 この設定は、Configuration Manager によって開始されるコンピューターの再起動にのみ適用されます。 この設定を指定しても、ユーザーがコンピューターを再起動する場合は、BitLocker PIN の入力の要件は一時停止されません。 BitLocker PIN の入力要件は、Windows の起動後に再開されます。

-   **[なし]**:Configuration Manager は、再起動が必要なソフトウェアをインストールした後で、BitLocker を一時停止しません。 この場合は、ユーザーが PIN を入力して標準の起動プロセスを完了し、Windows を読み込むまで、ソフトウェアのインストールを終了できません。

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>追加のソフトウェアでアプリケーションとソフトウェア更新プログラムの展開を管理します

このオプションは、次の条件のいずれかが当てはまる場合のみ有効にします。  

-   この設定を有効にする必要があるベンダー ソリューションを使用している。  

-   Configuration Manager Software Development Kit (SDK) を使用して、クライアント エージェントの通知、アプリケーションのインストール、およびソフトウェア更新プログラムのインストールを管理している。  

> [!WARNING]  
>  これらのどの条件も当てはまらない場合にこのオプションを選ぶと、クライアントはソフトウェア更新プログラムと必要なアプリケーションをインストールしません。 この設定により、ユーザーがアプリケーション カタログからアプリケーションをインストールできなくなったり、パッケージ、プログラム、タスク シーケンスをインストールできなくなったりすることはありません。  

### <a name="powershell-execution-policy"></a>PowerShell 実行ポリシー

Configuration Manager クライアントで Windows PowerShell スクリプトを実行する方法を構成します。 これらのスクリプトは、構成項目でコンプライアンス設定を検出するときに使うことがあります。 標準スクリプトとして展開でスクリプトを送信することもあります。  

-   **[バイパス]**:構成マネージャー クライアントは、署名されていないスクリプトを実行できるように、クライアント コンピューターの Windows PowerShell 構成をバイパスします。  

-   **[制限済み]**:構成マネージャー クライアントは、クライアント コンピューターの現在の PowerShell 構成を使います。 この構成により、署名されていないスクリプトを実行できるかどうかが決まります。  

-   **[すべて署名済み]**:構成マネージャー クライアントは、信頼された発行元によって署名されている場合にのみ、スクリプトを実行します。 この制限は、クライアント コンピューターの現在の PowerShell 構成とは独立して適用されます。  

このオプションには Windows PowerShell バージョン 2.0 以降が必要です。 既定値は **[すべて署名済み]** です。  

> [!TIP]  
>  このクライアント設定によって、未署名のスクリプトの実行が失敗する場合、Configuration Manager は、このエラーを次の方法でレポートします。  
>   
> -   コンソールの **[監視]** ワークスペースには、展開ステータス エラー ID **0x87D00327** が表示されます。 "**スクリプトに署名がありません**" という説明も表示されます。  
> -   レポートには、**[探索エラー]** というエラーの種類が表示されます。 また、エラー コード **0x87D00327** と説明 "**スクリプトに署名がありません**" またはエラー コード **0x87D00320** と説明 "**スクリプトのホストがインストールされていません**" が表示されます。 レポートの例を次に示します: **資産の構成基準に含まれる構成項目のエラーの詳細**。  
> -   **DcmWmiProvider.log** ファイルには、"**スクリプトに署名がありません (エラー: 87D00327; ソース: CCM)**" というメッセージが表示されます。  

### <a name="show-notifications-for-new-deployments"></a>新しい展開の通知を表示する

使用可能になって 1 週間未満の展開の通知を表示するには、**[はい]** を選びます。 このメッセージは、クライアント エージェントが開始するたびに表示されます。

### <a name="disable-deadline-randomization"></a>[期限のランダム化を無効にする]

展開の期限が過ぎると、この設定は、クライアントが必要なソフトウェア更新プログラムのインストールにアクティブ化の待機時間 (最大 2 時間) を使うかどうかを判別します。 既定では、アクティブ化の待機時間は無効です。  

仮想デスクトップ インフラストラクチャ (VDI) のシナリオでは、この待機時間は、複数の仮想マシンを含むホスト コンピューターの CPU 処理とデータ転送の分散に役立ちます。 VDI を使わない場合でも、多くのクライアントで同時に同じ更新プログラムをインストールすると、サイト サーバーの CPU の使用率が増加して悪影響を及ぼす可能性があります。 また、この動作により、配布ポイントの速度が低下して、使用可能なネットワーク帯域幅が大幅に減少する可能性もあります。  

クライアントが展開の期限に遅れずに必要なソフトウェア更新プログラムをインストールする必要がある場合は、この設定を **[はい]** に構成します。 

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>展開期限後の実施の猶予期間 (時間)

必要なアプリケーションのインストール、またはソフトウェア更新プログラムの展開の期限が過ぎてからも、さらにユーザーに時間を与えられるようにする場合は、このオプションを **[はい]** に設定します。 この猶予期間は、ユーザーが、長い間コンピューターの電源を切っていて、多くのアプリケーションまたは更新プログラムの展開をインストールする必要がある場合のためのものです。 たとえば、ユーザーが休暇から戻ってきて、期限を過ぎたアプリケーションの展開をクライアントがインストールするのを長時間待たなければならないような場合に、この設定が役立ちます。 

1 から 120 時間の間で猶予期間を設定します。 この設定は、展開プロパティ **[ユーザー設定に従い、この展開の実施を延期する]** と共に使います。 詳細については、「[アプリケーションの展開](/sccm/apps/deploy-use/deploy-applications)」をご覧ください。


##  <a name="computer-restart"></a>コンピューターの再起動  
以下の設定は、コンピューターに適用される最短のメンテナンス期間より短い期間にする必要があります。  

-   **ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる一時的な通知を表示する (分)**
-   **ユーザーがログオフするかコンピューターを再起動するまでの時間を知らせる、ユーザーが閉じることのできないダイアログ ボックスを表示する (分)**

メンテナンス期間の詳細については、「[System Center Configuration Manager でメンテナンス期間を使用する方法](/sccm/core/clients/manage/collections/use-maintenance-windows)」を参照してください。



## <a name="delivery-optimization"></a>配信の最適化

<!-- 1324696 --> Configuration Manager の境界グループを使って、企業ネットワークおよびリモート オフィスへのコンテンツ配布を定義して調整します。 [Windows の配信最適化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)は、Windows 10 デバイス間でコンテンツを共有するための、クラウド ベースのピア ツー ピア テクノロジです。 バージョン 1802 以降、ピア間でコンテンツを共有するときは、境界グループを使うように配信の最適化を構成します。

 > [!Note]
 > 配信の最適化は Windows 10 クライアントでのみ利用できます

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>配信の最適化グループ ID の Configuration Manager 境界グループを使用します
 **[はい]** を選択すると、クライアントでの配信最適化グループ識別子として境界グループ識別子が適用されます。 クライアントは、配信の最適化クラウド サービスと通信するとき、この識別子を使って目的のコンテンツを含むピアを探します。 



##  <a name="endpoint-protection"></a>Endpoint Protection  
> [!Tip]
> 次の情報の他に、「[Example scenario:Using Endpoint Protection to protect computers from malware](/sccm/protect/deploy-use/scenarios-endpoint-protection)」 (シナリオ例: Endpoint Protection を使用してマルウェアからコンピューターを保護する) にも、Endpoint Protection クライアント設定の使用に関する詳細があります。

### <a name="manage-endpoint-protection-client-on-client-computers"></a>クライアント コンピューターの Endpoint Protection クライアントを管理する

階層内のコンピューター上の既存の Endpoint Protection クライアントおよび Windows Defender クライアントを管理する必要がある場合は、**[はい]** を選びます。  

このオプションは、Endpoint Protection クライアントを既にインストールしており、Configuration Manager によってクライアントを管理する必要がある場合に選びます。 この個別のインストールには、Configuration Manager のアプリケーションまたはパッケージとプログラムを使うスクリプト化されたプロセスが含まれます。 Configuration Manager 1802 以降、Windows 10 デバイスには、Endpoint Protection エージェントをインストールする必要がありません。 ただし、引き続き、**[クライアント コンピューターの Endpoint Protection クライアントを管理する]** を有効にする必要があります。 <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>[Endpoint Protection クライアントをクライアント コンピューターにインストールする]

クライアントをまだ実行していないクライアント コンピューターに Endpoint Protection クライアントをインストールして有効にする場合は、**[はい]** を選びます。 Configuration Manager 1802 以降、Windows 10 クライアントには、Endpoint Protection エージェントをインストールする必要がありません。  

> [!NOTE]  
>  Endpoint Protection クライアントが既にインストールされている場合は、**[いいえ]** を選んでも Endpoint Protection クライアントはアンインストールされません。 Endpoint Protection クライアントをアンインストールするには、**[クライアント コンピューターの Endpoint Protection クライアントを管理する]** クライアント設定を **[いいえ]** に設定します。 その後、パッケージとプログラムを展開して Endpoint Protection クライアントをアンインストールします。  

<!-- removed in 1806, SMS 511544
### Automatically remove previously installed antimalware software before Endpoint Protection is installed

Set this option to **Yes** for the Endpoint Protection client to attempt to uninstall other antimalware applications. Multiple antimalware clients on the same device can conflict, and impact system performance.
-->

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>メンテナンス期間外の Endpoint Protection クライアントのインストールと再起動を許可します。 クライアント インストール用のメンテナンス期間は、最短で 30 分にする必要があります。

通常のインストール動作をメンテナンス期間でオーバーライドする場合は、このオプションを **[はい]** に設定します。 この設定は、セキュリティのためにシステムのメンテナンスを優先させるビジネス要件を満たします。 

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>書き込みフィルターのある Windows Embedded デバイスに対し、Endpoint Protection クライアントのインストールをコミットする (再起動が必要)

Windows Embedded デバイスの書き込みフィルターを無効にして、デバイスを再起動するには、**[はい]** を選びます。 このアクションにより、デバイスのインストールがコミットされます。  

**[いいえ]** を選ぶと、クライアントはデバイスを再起動するとクリアされる一時的なオーバーレイにインストールされます。 このシナリオでは、別のインストールによってデバイスに変更がコミットされない限り、Endpoint Protection クライアントの完全なインストールは行われません。 これが既定の構成です。  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Endpoint Protection クライアントのインストール後に必要なコンピューターの再起動を抑制する

Endpoint Protection クライアントをインストールした後でコンピューターの再起動を抑制するには、**[はい]** を選びます。  

> [!IMPORTANT]  
>  この設定を **[いいえ]** にすると、Endpoint Protection クライアントでコンピューターの再起動が必要な場合、コンピューターは構成されているメンテナンス期間に関係なく再起動します。  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>Endpoint Protection のインストールを完了するために必要な再起動をユーザーが一定の時間延期できるようにする (時間単位)

この設定では、Endpoint Protection クライアントをインストールした後でコンピューターを再起動する必要がある場合に、ユーザーが必要な再起動を延期できる時間数を指定します。 この設定を指定するには、設定 **[Endpoint Protection クライアントのインストール後に必要なコンピューターの再起動を抑制する]** が **[いいえ]** になっている必要があります。  

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>クライアント コンピューター上で定義ファイルを初めて更新する場合は、代替ソース (Microsoft Windows Update、Microsoft Windows Server Update Services、UNC 共有など) を無効にする

Configuration Manager に初期定義の更新プログラムのみをクライアント コンピューターにインストールさせる場合は、**[はい]** を選びます。 この設定は、定義ファイルの初回更新時に、不要なネットワーク接続を避けてネットワーク帯域幅を削減するのに役立ちます。  



##  <a name="enrollment"></a>登録

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>モバイル デバイスのレガシ クライアントのポーリング間隔
**[間隔の設定]** を選び、レガシ モバイル デバイスがポリシーのポーリングを行う時間の長さ (分または時間単位) を指定します。 これらのデバイスには、Windows CE、Mac OS X、Unix、Linux などのプラットフォームが含まれます。

### <a name="polling-interval-for-modern-devices-minutes"></a>最新デバイスのポーリング間隔 (分)
最新のデバイスがポリシーのポーリングを行う間隔を分単位で入力します。 この設定は、オンプレミスのモバイル デバイス管理によって管理される Windows 10 デバイスのためのものです。

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>ユーザーがモバイル デバイスと Mac コンピューターを登録できるようにする
レガシ デバイスのユーザー ベースの登録を有効にするには、このオプションを **[はい]** に設定して、次の設定を構成します。

-   **登録プロファイル** </br>
**[プロファイルの設定]** を選び、登録プロファイルを作成または選択します。 詳しくは、「[登録のためのクライアント設定を構成する](/sccm/core/clients/deploy/deploy-clients-to-macs#configure-client-settings-for-enrollment)」をご覧ください。

### <a name="allow-users-to-enroll-modern-devices"></a>新しいデバイスの登録をユーザーに許可する
新しいデバイスのユーザー ベースの登録を有効にするには、このオプションを **[はい]** に設定して、次の設定を構成します。

-   **新しいデバイスの登録プロファイル** </br>
**[プロファイルの設定]** を選び、登録プロファイルを作成または選択します。 詳しくは、「[ユーザーが最新のデバイスを登録できるようにするための登録プロファイルを作成する](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm#bkmk_createProf)」をご覧ください。



##  <a name="hardware-inventory"></a>ハードウェア インベントリ  

### <a name="enable-hardware-inventory-on-clients"></a>［クライアントのハードウェア インベントリを有効にする］

この設定の既定値は **[はい]** です。 詳しくは、「[ハードウェア インベントリの概要](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory)」をご覧ください。

### <a name="hardware-inventory-schedule"></a>［ハードウェア インベントリのスケジュール］

クライアントがハードウェア インベントリ サイクルを実行する頻度を調整するには、**[スケジュール]** を選びます。 既定では、このサイクルは 7 日ごとに実行されます。

### <a name="maximum-random-delay-minutes"></a>最大ランダム遅延 (分)

構成マネージャー クライアントがハードウェア インベントリ サイクルを定義済みのスケジュールからランダムに変更する最大分数を指定します。 すべてのクライアントでこのランダム化を行うと、サイト サーバーのインベントリ処理の負荷分散に役立ちます。 0 から 480 分までの任意の値を指定できます。 既定では、240 分 (4 時間) に設定されます。

### <a name="maximum-custom-mif-file-size-kb"></a>カスタム MIF ファイルの最大サイズ (KB)

ハードウェア インベントリ サイクル中にクライアントが収集する各カスタム各管理情報フォーマット (MIF) ファイルに対して許容される最大サイズを、キロバイト (KB) 単位で指定します。 構成マネージャー ハードウェア インベントリ エージェントは、このサイズを超えた MIF ファイルを処理しません。 1 KB から 5,120 KB の範囲のサイズを指定できます。 既定では、この値は 250 KB に設定されます。 この設定は、通常のハードウェア インベントリ データ ファイルのサイズには影響しません。  

> [!NOTE]  
>  この設定は、既定のクライアント設定でのみ使用できます。  

### <a name="hardware-inventory-classes"></a>ハードウェア インベントリ クラス

**[クラスの設定]** を選ぶと、sms_def.mof ファイルを手動で編集することなくクライアントから収集できるハードウェア情報が表示されます。 詳しくは、「[ハードウェア インベントリを構成する方法](/sccm/core/clients/manage/inventory/configure-hardware-inventory)」をご覧ください。  

### <a name="collect-mif-files"></a>MIF ファイルを収集する

ハードウェア インベントリの実行時に Configuration Manager クライアントから MIF ファイルを収集するかどうかを指定するには、この設定を使います。  

MIF ファイルをハードウェア インベントリで収集するためには、クライアント コンピューター上の正しい場所に MIF ファイルがある必要があります。 既定では、ファイルは次のパスにあります。  

-   **IDMIF ファイル**は、Windows\System32\CCM\Inventory\Idmif フォルダーに存在する必要があります。 

-   **NOIDMIF ファイル**は、Windows\System32\CCM\Inventory\Noidmif フォルダーに存在する必要があります。

> [!NOTE]  
>  この設定は、既定のクライアント設定でのみ使用できます。

   

##  <a name="metered-internet-connections"></a>従量制インターネット接続  
 Windows 8 以降のコンピューターが Configuration Manager サイトとの通信に従量制インターネット接続を使う方法を管理します。 インターネット プロバイダーは、従量制インターネット接続を使用しているときに送受信したデータ量に基づいて課金することがあります。  

> [!NOTE]  
>  構成したクライアント設定は、次のシナリオでは適用されません。  
>   
> -   コンピューターがローミング データ接続を使っている場合、構成マネージャー クライアントは、Configuration Manager サイトへのデータ転送が必要なタスクを実行しません。  
> -   Windows ネットワーク接続のプロパティが従量制以外に構成されている場合、構成マネージャー クライアントは、接続が従量制以外であるものとして動作し、サイトにデータを転送します。  

### <a name="client-communication-on-metered-internet-connections"></a>従量制ネットワーク接続でのクライアントの通信方法

この設定には次のいずれかのオプションを選びます。  

-   **[許可]**:クライアント デバイスがローミング データ接続を使用していない場合、従量制インターネット接続でのすべてのクライアント通信を許可します。  

-   **[制限]**:従量制インターネット接続で、次のクライアント通信のみを許可します。  

    -   クライアント ポリシーの取得  

    -   クライアント状態メッセージのサイトへの送信  

    -   アプリケーション カタログを使用したソフトウェアインストール要求  

    -   必要な展開 (インストールの期限に達した場合)  

    > [!IMPORTANT]  
    >  クライアントは、従量制インターネット接続の設定に関係なく、ソフトウェア センターまたはアプリケーション カタログからのソフトウェアのインストールを常に許可します。  

    クライアントが従量制インターネット接続のデータ転送の制限に達した場合、クライアントはそれ以上 Configuration Manager サイトとの通信を試行しません。  

-   **[ブロック]**:構成マネージャー クライアントは、従量制インターネット接続を使っている場合に、Configuration Manager サイトとの通信を試行しません。 これが既定のオプションです。  



##  <a name="power-management"></a>電源管理  

### <a name="allow-power-management-of-devices"></a>デバイスの電源管理を許可する

クライアントでの電源管理を有効にするには、このオプションを **[はい]** に設定します。 詳細については、「[電源管理の概要](/sccm/core/clients/manage/power/introduction-to-power-management)」を参照してください。

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>ユーザーがデバイスを電源管理対象から外せるようにする

ソフトウェア センターのユーザーが、構成済みの電源管理設定から自分のコンピューターを除外できるようにするには、**[はい]** を選びます。  

### <a name="enable-wake-up-proxy"></a>[ウェイクアップ プロキシを有効にする]

サイトでユニキャスト パケットが構成されている場合に、サイトの Wake On LAN 設定を補足するには、**[はい]** を指定します。  

ウェイクアップ プロキシの詳細については、[クライアントをウェイク アップする方法の計画](/sccm/core/clients/deploy/plan/plan-wake-up-clients)に関するページを参照してください。  

> [!WARNING]  
>  テスト環境でウェイクアップ プロキシがどのように動作するかを理解するまで、実稼動環境でウェイクアップ プロキシを有効にしないでください。  

確認した後、必要に応じて以下の追加設定を構成します。

-   **[ウェイクアップ プロキシのポート番号 (UDP)]**:スリープ状態のコンピューターにウェイクアップ パケットを送信するためにクライアントが使うポート番号です。 既定のポート 25536 のままにするか、または適切な値に変更します。  

-   **[Wake On LAN ポート番号 (UDP)]**:サイトの **[プロパティ]** の **[ポート]** タブで Wake On LAN (UDP) ポート番号を変更していない場合は、既定値 9 のままにします。  

    > [!IMPORTANT]  
    >  この数値は、サイトの **[プロパティ]** の数値と一致する必要があります。 一方でこの数値を変更した場合、もう一方では自動的に更新されません。  

-   **ウェイクアップ プロキシ用の Windows Defender ファイアウォールの例外**:構成マネージャー クライアントは、Windows Defender ファイアウォールを実行しているデバイスのウェイクアップ プロキシのポート番号を自動的に構成します。 必要なファイアウォール プロファイルを指定するには、**[構成]** を選びます。

    クライアントが別のファイアウォールを実行している場合は、**[ウェイクアップ プロキシのポート番号 (UDP)]** を許可するように手動で構成します。  
        
-   **DirectAccess または他の介在するネットワーク デバイスで必要な場合は、IPv6 プレフィックス。複数のエントリを指定する場合は、コンマで区切ります。** ウェイクアップ プロキシがネットワーク上で機能するために必要な IPv6 プレフィックスを入力します。



##  <a name="remote-tools"></a>［リモート ツール］  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>クライアントのリモート コントロールを有効にする、ファイアウォール例外プロファイル

Configuration Manager のリモート制御機能を有効にするには、**[構成]** を選びます。 必要に応じて、クライアント コンピューターでリモート コントロールが機能するようにファイアウォールの設定を構成します。  

既定では、リモート コントロールは無効になっています。  

> [!IMPORTANT]  
>  ファイアウォール設定を構成しないと、リモート コントロールが正しく機能しない可能性があります。  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>ユーザーはソフトウェア センターでポリシー設定または通知設定を変更できる

ユーザーがソフトウェア センター内からリモート コントロール オプションを変更できるかどうかを選びます。  

### <a name="allow-remote-control-of-an-unattended-computer"></a>無人のコンピューターのリモート コントロールを許可する

ログオフまたはロックされているクライアント コンピューターに、管理者がリモート コントロールを使ってアクセスできるかどうかを選びます。 この設定が無効になっている場合、ログオンされ、ロックが解除されているコンピューターのみリモート コントロールできます。  

### <a name="prompt-user-for-remote-control-permission"></a>リモート コントロールのアクセス許可をユーザーに要求する

リモート制御セッションを許可する前にユーザーのアクセス許可を確認するメッセージをクライアント コンピューターに表示するかどうかを選びます。  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>共有クリップボードからコンテンツを転送するアクセス許可を求めるプロンプトをユーザーに表示する

リモート コントロール セッションで共有クリップボードからコンテンツを転送する前に、ユーザーはファイル転送を許可するかどうかを選択できます。 ユーザーはセッションごとに一度アクセス許可を与えるだけで済みます。 ビューアーはファイル転送するためのアクセス許可を自身に付与することはできません。

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>ローカルの Administrators グループにリモート コントロール権限を付与する

クライアント コンピューターへのリモート コントロール セッションを、リモート コントロール接続を開始するサーバーのローカル管理者が確立できるかどうかを選びます。  

### <a name="access-level-allowed"></a>許容アクセス レベル

許可するリモート制御アクセスのレベルを指定します。 次の設定から選びます。  
- **アクセスなし**
- **表示のみ**
- **フル コントロール**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>リモート コントロールとリモート アシスタンス セッションを表示できるユーザー

クライアント コンピューターへのリモート制御セッションを確立できる Windows ユーザーの名前を指定するには、**[ユーザーの設定]** を選びます。  

### <a name="show-session-notification-icon-on-taskbar"></a>タスクバーにセッション通知アイコンを表示する

アクティブなリモート コントロール セッションを示すアイコンをクライアントの Windows タスク バーに表示するには、この設定を **[はい]** に構成します。  

### <a name="show-session-connection-bar"></a>セッション接続バーを表示する

アクティブなリモート コントロール セッションを示す視認性のよいセッション接続バーをクライアントに表示するには、このオプションを **[はい]** に設定します。  

### <a name="play-a-sound-on-client"></a>クライアントで音を鳴らす

音を使用してクライアント コンピューターでリモート コントロール セッションがアクティブであることを示すには、このオプションを設定します。 次のいずれかのオプションを選択します。
- **音を鳴らさない**
- **セッションの開始時と終了時** (既定値)
- **セッションの実行中に繰り返し鳴らす**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>[要請されていないリモート アシスタンス設定を管理する]

Configuration Manager が要請されていないリモート アシスタンス セッションを管理できるようにするには、この設定を **[はい]** に構成します。  

要請されていないリモート アシスタンス セッションでは、クライアント コンピューターのユーザーはセッションを開始するアシスタンスを要求していません。  

### <a name="manage-solicited-remote-assistance-settings"></a>[要請されたリモート アシスタンス設定を管理する]

このオプションを **[はい]** に設定すると、Configuration Manager が要請されたリモート アシスタンス セッションを管理します。  

要請されたリモート アシスタンス セッションでは、クライアント コンピューターのユーザーが管理者にリモート アシスタンスを要求しています。  

### <a name="level-of-access-for-remote-assistance"></a>[リモート アシスタンスのアクセス レベル]

Configuration Manager コンソールで開始されるリモート アシスタンス セッションに割り当てるアクセス レベルを選びます。 次のいずれかのオプションを選択します。
- **なし** (既定値)
- **リモートで表示**
- **フル コントロール**

> [!NOTE]  
>  クライアント コンピューターのユーザーは、リモート アシスタンス セッションが実行されるときに常にアクセス許可を付与する必要があります。  

### <a name="manage-remote-desktop-settings"></a>リモート デスクトップ設定の管理

このオプションを **[はい]** に設定すると、Configuration Manager がコンピューターのリモート デスクトップ セッションを管理します。  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>[セッションを表示できるユーザーにリモート デスクトップ接続を許可する]

表示を許可するユーザーの一覧で指定されているユーザーをクライアントのリモート デスクトップ ローカル ユーザー グループに追加するには、このオプションを **[はい]** に設定します。  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>[Windows Vista 以降のバージョンのオペレーティング システムが実行されているコンピューターではネットワーク レベルの認証を必要とする]

ネットワーク レベル認証 (NLA) を使ってクライアント コンピューターへのリモート デスクトップ接続を確立するには、このオプションを **[はい]** に設定します。 NLA は、リモート デスクトップ接続を確立する前にユーザー認証を終了するため、最初に必要なリモート コンピューター リソースが少なくて済みます。 NLA を使うと構成がいっそう安全になります。 NLA は、悪意のあるユーザーやソフトウェアからコンピューターを保護するのに役立ち、サービス拒否攻撃からのリスクを軽減します。  



## <a name="software-center"></a>ソフトウェア センター

### <a name="select-these-new-settings-to-specify-company-information"></a>新しい設定を選択して会社の情報を指定する
ソフトウェア センターを組織のブランドにするには、このオプションを **[はい]** に設定してから、次の設定を指定します。

- **会社名**:ソフトウェア センターでユーザーに表示する組織の名前を入力します。  

- **ソフトウェア センターの配色**:**[色の選択]** をクリックして、ソフトウェア センターで主に使う色を定義します。  

- **ソフトウェア センターのロゴを選択する**:**[参照]** をクリックして、ソフトウェア センターで表示する画像を選択します。 ロゴは、400 x 100 ピクセルの JPEG、PNG、または BMP で、サイズは 750 KB である必要があります。 ロゴのファイル名にスペースが含めることはできません。  
         
### <a name="bkmk_HideUnapproved"></a> ソフトウェア センターで承認されていないアプリケーションを非表示にする
Configuration Manager バージョン 1802 以降、このオプションを有効にすると、承認を必要とするユーザーの使用可能なアプリケーションがソフトウェア センターでは非表示になります。   <!--1355146-->

### <a name="bkmk_HideInstalled"></a> ソフトウェア センターでインストール済みのアプリケーションを非表示にする
Configuration Manager バージョン 1802 以降、このオプションを有効にすると、既にインストールされているアプリケーションが、[アプリケーション] タブに表示されなくなります。Configuration Manager 1802 をインストールすると、あるいはこのバージョンにアップグレードすると、このオプションが既定として設定されます。 インストールされているアプリケーションは、[インストールの状態] タブで引き続き確認できます。<!--1357592-->   
 
### <a name="bkmk_HideAppCat"></a> ソフトウェア センターでアプリケーション カタログへのリンクを非表示にします
Configuration Manager バージョン 1806 以降、ソフトウェア センターでアプリケーション カタログ Web サイト リンクの表示を指定できるようになりました。 このオプションを設定すると、ソフトウェア センターのインストールのステータス ノードでアプリケーション カタログ Web サイト リンクが表示されなくなります。 <!--1358214-->


### <a name="software-center-tab-visibility"></a>ソフトウェア センターのタブの表示
ソフトウェア センターで次のタブを表示するには、このグループの追加設定を **[はい]** に構成します。
- **アプリケーション**
- **更新プログラム**
- **オペレーティング システム**
- **インストールのステータス**
- **デバイス コンプライアンス**
- **Options**
- **ソフトウェア センターのカスタム タブを指定する** (バージョン 1806 以降)<!--1358132-->
    - **タブ名**
    - **コンテンツ URL**

>[!NOTE]
> Web サイトの一部の機能は、ソフトウェア センターでカスタム タブとして使用すると、機能しない場合があります。 これをクライアントに展開する前に、必ず結果をテストしてください。 <!--519659-->

たとえば、組織でコンプライアンス ポリシーが使われておらず、ソフトウェア センターの [デバイス コンプライアンス] タブを非表示にする場合は、**[[デバイス コンプライアンス] タブを有効にする]** を **[いいえ]** に設定します。



## <a name="software-deployment"></a>ソフトウェアの展開  

### <a name="schedule-re-evaluation-for-deployments"></a>展開の再評価スケジュールを指定する
すべての展開に関して、Configuration Manager によって要件の規則を再評価するスケジュールを構成します。 既定値は 7 日ごとです。  

> [!IMPORTANT]  
> これは、ネットワークやサイト サーバーよりもローカル クライアントに対する影響が大きい設定です。 より頻繁にスケジュールを再評価すると、ネットワークとクライアント コンピューターのパフォーマンスが低下します。 Microsoft は、既定よりも低い値を設定することをお勧めしません。 この値を変更した場合は、パフォーマンスをよく監視してください。  

クライアントからこのアクションを開始するには、**[Configuration Manager]** コントロール パネルの **[アクション]** タブで **[アプリケーション展開の評価サイクル]** を選びます。  



##  <a name="software-inventory"></a>ソフトウェア インベントリ  

### <a name="enable-software-inventory-on-clients"></a>［クライアントのソフトウェア インベントリを有効にする］

既定では、このオプションは **[はい]** に設定されます。 詳しくは、「[ソフトウェア インベントリの概要](/sccm/core/clients/manage/inventory/introduction-to-software-inventory)」をご覧ください。

### <a name="schedule-software-inventory-and-file-collection"></a>ソフトウェア インベントリおよびファイル収集をスケジュールする

クライアントがソフトウェア インベントリおよびファイル コレクション サイクルを実行する頻度を調整するには、**[スケジュール]** を選びます。 既定では、このサイクルは 7 日ごとに実行されます。

### <a name="inventory-reporting-detail"></a>[インベントリ レポートの詳細]

インベントリを行うファイル情報のレベルとして次のいずれかを指定します。
- **ファイルのみ**
- **製品のみ**
- **全詳細情報** (既定値)

### <a name="inventory-these-file-types"></a>[これらのファイルの種類をインベントリ対象とする]

インベントリ対象のファイルの種類を指定する場合は、**[種類の設定]** を選び、次のオプションを構成します。  

> [!NOTE]  
>  複数のカスタム クライアント設定がコンピューターに適用されている場合は、各設定によって戻されるインベントリが結合されます。  

-   インベントリに新しいファイルの種類を追加するには、**[新規]** を選びます。 その後、**[インベントリされるファイルのプロパティ]** ダイアログ ボックスで次の情報を指定します。  

    -   **[名前]**:インベントリの対象にするファイルの名前を指定します。 任意の文字列を表すにはアスタリスク (**&#42;**) を使い、任意の 1 文字を表すには疑問符 (**?**) を使います。 たとえば、拡張子 .doc を持つすべてのファイルをインベントリの対象にするには、ファイル名「**\*.doc**」を指定します。  

    -   **[場所]**:**[設定]** を選ぶと、**[パスのプロパティ]** ダイアログ ボックスが開きます。 クライアントのすべてのハード ディスクで、指定したファイル、指定したパス (例: **C:\Folder**)、または指定した変数 (例: *%windir%*) を検索するように、ソフトウェア インベントリを構成します。 特定のパスにあるすべてのサブフォルダーを検索するように構成することもできます。  

    -   **[暗号化または圧縮されたファイルを除く]**:このオプションをオンにすると、圧縮されたファイルまたは暗号化されたファイルはインベントリされません。  

    -   **[Windows フォルダー内のファイルは除く]**:このオプションを選ぶと、Windows フォルダーとそのサブフォルダー内のファイルはインベントリされません。  

    **[OK]** を選んで **[インベントリされるファイルのプロパティ]** ダイアログ ボックスを閉じます。 インベントリするファイルをすべて追加し、**[OK]** を選んで **[クライアント設定の構成]** ダイアログ ボックスを閉じます。  

### <a name="collect-files"></a>[ファイルの収集]

クライアント コンピューターからファイルを収集する場合は、**[ファイルの設定]** を選んで以下の設定を構成します。  

> [!NOTE]  
>  複数のカスタム クライアント設定がコンピューターに適用されている場合は、各設定によって戻されるインベントリが結合されます。  

-   **[クライアント設定の構成]** ダイアログ ボックスで、**[新規]** を選んで収集するファイルを追加します。  

-   **[収集するファイルのプロパティ]** ダイアログ ボックスで、次の情報を入力します。  

    -   **[名前]**:収集するファイルの名前を指定します。 任意の文字列を表すにはアスタリスク (**&#42;**) を使い、任意の 1 文字を表すには疑問符 (**?**) を使います。  

    -   **[場所]**:**[設定]** を選ぶと、**[パスのプロパティ]** ダイアログ ボックスが開きます。 クライアントのすべてのハード ディスクで、収集するファイル、指定したパス (例: **C:\Folder**)、または指定した変数 (例: *%windir%*) を検索するように、ソフトウェア インベントリを構成します。 特定のパスにあるすべてのサブフォルダーを検索するように構成することもできます。  

    -   **[暗号化または圧縮されたファイルを除く]**:このオプションを選ぶと、圧縮されたファイルまたは暗号化されたファイルは収集されません。  

    -   **ファイルの合計サイズが次のサイズ (KB) を超える場合はファイルの収集を停止する**:クライアントによって指定されたファイルの収集が停止された後のファイル サイズ (キロバイト (KB) 単位) を指定します。  

    > [!NOTE]  
    >  サイト サーバーは、収集ファイルについて最近に変更されたもの順に 5 つのバージョンを収集し、`<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol` ディレクトリに格納します。 前回のソフトウェア インベントリ サイクルの後でファイルが変更されていない場合、ファイルは再収集されません。  
    >   
    >  20 MB より大きいファイルはソフトウェア インベントリでは収集されません。  
    >   
    >  **[クライアント設定の構成]** ダイアログ ボックスの **[収集した全ファイルの最大サイズ (KB)]** の値は、すべての収集されたファイルの最大サイズを示しています。 サイズがこの値に達すると、ファイルの収集は停止します。 既に収集されたファイルは保持され、サイト サーバーに送信されます。  

    > [!IMPORTANT]
    >  多数の大きいファイルを収集するようにソフトウェア インベントリを構成すると、ネットワークとサイト サーバーのパフォーマンスに悪影響となる場合があります。  

    収集されたファイルを表示する方法については、「[リソース エクスプローラーを使用してソフトウェア インベントリを表示する方法](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory)」をご覧ください。  

    **[OK]** を選んで **[収集するファイルのプロパティ]** ダイアログ ボックスを閉じます。 収集するファイルをすべて追加し、**[OK]** を選んで、**[クライアント設定の構成]** ダイアログ ボックスを閉じます。  

### <a name="set-names"></a>[名前の設定]

ソフトウェア インベントリ エージェントは、製造元と製品名をファイルのヘッダー情報から取得します。 これらの名前は、ファイルのヘッダー情報で常に標準化されているとは限りません。 リソース エクスプローラーでソフトウェア インベントリを表示すると、同じ製造元または製品の名前の異なるバージョンが表示される場合があります。 これらの表示名を標準化するには、**[名前の設定]** を選んで、次の設定を構成します。  

-   **[名前の種類]**:ソフトウェア インベントリは、製造元と製品の両方の情報を収集します。 表示名を構成する対象として、**[製造元]** または **[製品]** を選びます。  

-   **[表示名]**:**[インベントリされた名前]** の一覧の名前部分で使用する表示名を指定します。 新しい表示名を指定するには、**[新規]** を選びます。  

-   **[インベントリされた名前]**:インベントリされた名前を追加するには、**[新規]** を選択します。 この名前は、ソフトウェア インベントリでは、**[表示名]** の一覧で選んだ名前に置き換わります。 置き換える名前を複数追加することができます。  



##  <a name="software-metering"></a>ソフトウェア使用状況測定

### <a name="enable-software-metering-on-clients"></a>［クライアントでソフトウェア メータリングを有効にする］
既定では、この設定は **[いいえ]** に設定されます。 詳しくは、「[ソフトウェア使用状況測定](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering#configure-software-metering)」をご覧ください。

### <a name="schedule-data-collection"></a>データ収集のスケジュール設定
クライアントがソフトウェア使用状況測定サイクルを実行する頻度を調整するには、**[スケジュール]** を選びます。 既定では、このサイクルは 7 日ごとに実行されます。



##  <a name="software-updates"></a>ソフトウェア更新プログラム  

### <a name="enable-software-updates-on-clients"></a>クライアントのソフトウェア更新プログラムを有効にする

この設定を使用して、Configuration Manager クライアント上のソフトウェア更新プログラムを有効にします。 この設定を無効にすると、Configuration Manager がクライアントから既存の展開ポリシーを削除します。 この設定を再度有効にすると、クライアントが現在の展開ポリシーをダウンロードします。  

> [!IMPORTANT]  
>  この設定を無効にすると、ソフトウェア更新プログラムに依存するコンプライアンス ポリシーは機能しなくなります。  

### <a name="software-update-scan-schedule"></a>ソフトウェア更新プログラムのスキャンのスケジュール

クライアントがコンプライアンス評価スキャンを開始する頻度を指定するには、**[スケジュール]** を選びます。 このスキャンでは、クライアント上のソフトウェア更新プログラムのステータスを判別します (必要、インストール済みなど)。 コンプライアンス対応評価の詳細については、「[Software updates compliance assessment](/sccm/sum/understand/software-updates-introduction#BKMK_SUMCompliance)」 (ソフトウェア更新プログラムのコンプライアンス評価) を参照してください。  

既定では、このスキャンは 7 日ごとに開始する単純なスケジュールを使います。 カスタム スケジュールを作成することができます。 正確な開始日時を指定したり、世界協定時刻 (UTC) またはローカル時刻を使ったり、繰り返しの間隔を特定の曜日に構成したりできます。  

> [!NOTE]  
>  1 日未満の間隔を指定すると、Configuration Manager によって自動的に既定の 1 日に設定されます。  

> [!WARNING]  
>  クライアント コンピューターでの実際の開始時刻は、開始時刻に 2 時間までのランダムな時間を加えた時刻です。 このランダム化は、複数のクライアント コンピューターが同時にスキャンを開始してアクティブなソフトウェアの更新ポイントに接続するのを防ぎます。  

### <a name="schedule-deployment-re-evaluation"></a>[展開の再評価のスケジュール]

ソフトウェア更新クライアント エージェントが構成マネージャー クライアント コンピューターでソフトウェア更新プログラムのインストール ステータスを再評価する頻度を構成するには、**[スケジュール]** を選びます。 以前にインストールされたソフトウェア更新プログラムがクライアント上で見つからないが、まだ必要である場合、クライアントはそのソフトウェア更新プログラムを再インストールします。

ソフトウェア更新プログラムのコンプライアンスに関する企業のポリシーと、ユーザーがソフトウェア更新プログラムをアンインストールできるかどうかに基づいて、このスケジュールを調整します。 展開の再評価のすべてのサイクルで、ネットワークおよびクライアント コンピューターのプロセッサにアクティビティが発生します。 既定の設定では、7 日ごとに展開の再評価スキャンを開始する単純なスケジュールが使われます。  

> [!NOTE]  
>  1 日未満の間隔を指定すると、Configuration Manager によって自動的に既定の 1 日に設定されます。  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>いずれかのソフトウェア更新プログラムの展開期限に達した場合に、指定した期間内に期限に達する他のソフトウェア更新プログラムの展開をすべてインストールする

指定した期間内に期限を迎える必須の展開からすべてのソフトウェア更新プログラムをインストールするには、このオプションを **[はい]** に設定します。 必須のソフトウェア更新プログラムの展開が期限に達すると、クライアントは展開に含まれるソフトウェア更新プログラムのインストールを開始します。 この設定は、指定した時間内に期限を迎える他の必須展開からソフトウェア更新プログラムをインストールするかどうかを決定します。  

必須ソフトウェア更新プログラムのインストールを高速化するには、この設定を使います。 この設定は、クライアントのセキュリティを強化し、ユーザーへの通知を減らし、クライアントの再起動を少なくする可能性もあります。 既定では、この設定は **[いいえ]** に設定されています。  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>保留中の展開の期限が指定した期間内の場合は、これらの展開もすべてインストールする

以前の設定の期間を指定するには、この設定を使います。 1 から 23 時間および 1 から 365 日の値を入力できます。 この設定の既定値は、7 日間です。  

### <a name="enable-installation-of-express-installation-files-on-clients"></a>高速インストール ファイルのクライアントでのインストールを有効にする

クライアントが高速インストール ファイルを使用できるようにするには、このオプションを **[はい]** に設定します。 詳細については、「[Windows 10 更新プログラムに対する高速インストール ファイルの管理](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)」を参照してください。 


### <a name="port-used-to-download-content-for-express-installation-files"></a>高速インストール ファイルのコンテンツをダウンロードするために使用するポート

この設定は、HTTP リスナーが高速コンテンツをダウンロードするためのローカル ポートを構成します。 既定では 8005 に設定されます。 クライアントのファイアウォールでこのポートを開く必要はありません。

### <a name="enable-management-of-the-office-365-client-agent"></a>Office 365 クライアント エージェントの管理を有効にする

このオプションを **[はい]** に設定すると、Office 365 のインストール設定を構成できます。 また、Office コンテンツ配信ネットワーク (CDN) からファイルをダウンロードし、Configuration Manager でファイルをアプリケーションとして展開することもできます。 詳しくは、「[Office 365 ProPlus の更新プログラムの管理](/sccm/sum/deploy-use/manage-office-365-proplus-updates)」をご覧ください。

### <a name="enable-third-party-software-updates"></a>サードパーティ製ソフトウェア更新プログラムを有効にする 

このオプションを **[はい]** に設定すると、[イントラネットの Microsoft 更新サービスの保存場所にある署名済み更新を許可する] のポリシーが設定され、クライアントの信頼できる発行元ストアに署名証明書がインストールされます。 このクライアント設定は、Configuration Manager バージョン 1802 で追加されました。



## <a name="state-messaging"></a>状態メッセージ

### <a name="state-message-reporting-cycle-minutes"></a>［状態メッセージのレポート サイクル (分)］
クライアントが状態メッセージをレポートする頻度を指定します。 既定の設定は、15 分です。



##  <a name="user-and-device-affinity"></a>ユーザーとデバイスのアフィニティ  

### <a name="user-device-affinity-usage-threshold-minutes"></a>ユーザーとデバイスのアフィニティ使用状況のしきい値 (分)
ユーザー デバイスのアフィニティ マッピングを Configuration Manager が作成するまでの時間 (分) を指定します。 既定値は 2880 分 (2 日) です。

### <a name="user-device-affinity-usage-threshold-days"></a>ユーザーとデバイスのアフィニティ使用状況のしきい値 (日)
使用状況に基づくデバイスのアフィニティのしきい値をクライアントが測定する日数を指定します。 既定値は 30 日です。

> [!NOTE]  
>  たとえば、**[ユーザーとデバイスのアフィニティ使用状況のしきい値 (分)]** に **60** 分を指定し、**[ユーザーとデバイスのアフィニティ使用状況のしきい値 (日)]** に **5** 日を指定します。 この場合、ユーザーは、デバイスで自動アフィニティを作成するには、5 日間にわたって 60 分デバイスを使う必要があります。  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>使用状況データに基づいてユーザーとデバイスのアフィニティを自動構成する
Configuration Manager が収集する使用状況情報に基づいてユーザー デバイスの自動アフィニティを作成するには、**[はい]** を選びます。  

### <a name="allow-user-to-define-their-primary-devices"></a>ユーザーがプライマリ デバイスを定義できるようにする
この設定を **[はい]** にすると、ユーザーはソフトウェア センターで自分のプライマリ デバイスを識別できます。



## <a name="windows-analytics"></a>Windows Analytics

これらの設定について詳しくは、「[Windows Analytics にデータをレポートするようにクライアントを構成する](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics)」をご覧ください。
    
