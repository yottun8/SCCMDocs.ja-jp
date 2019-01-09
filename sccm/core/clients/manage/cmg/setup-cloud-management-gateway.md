---
title: クラウド管理ゲートウェイの設定
titleSuffix: Configuration Manager
description: クラウド管理ゲートウェイ (CMG) を設定するには、この段階的なプロセスを使用します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 8f743514af8b89212b10073c07b24990ffedcb1a
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420398"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configuration Manager のクラウド管理ゲートウェイを設定する

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*  

このプロセスには、クラウド管理ゲートウェイ (CMG) を設定するために必要な手順が含まれています。 

> [!Tip]
> この機能はバージョン 1610 で[プレリリース機能](/sccm/core/servers/manage/pre-release-features)として初めて導入されました。 バージョン 1802 以降、この機能はプレリリース機能ではなくなりました。



## <a name="before-you-begin"></a>始める前に

まず、「[クラウド管理ゲートウェイの計画](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)」の記事を読みます。 この記事を使用して、CMG の設計を決定します。 

以下のチェックリストを使用して、CMG の作成に必要な情報と前提条件が揃っていることを確認します。  

- 使用する Azure 環境。 たとえば、Azure パブリック クラウドや Azure 米国政府クラウドです。  

- 設計に応じて、CMG には 1 つ以上の証明書が必要です。 詳細については、「[クラウド管理ゲートウェイの証明書](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)」を参照してください。  

- バージョン 1802 以降では、**[Azure Resource Manager の展開]** を選択します。 詳細については、[Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager) に関するページを参照してください。 CMG の Azure Resource Manager の展開には、以下の要件が必要です。  

    - **クラウド管理**のための [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) との統合。 Azure AD のユーザー探索は必要ありません。  

    - サブスクリプション管理者はサインインする必要があります。  

- CMG の従来のサービス展開には、以下の要件が必要です。  

    > [!Important]  
    > バージョン 1810 以降では、Configuration Manager での Azure の従来のサービス展開は推奨されていません。 クラウド管理ゲートウェイ用の Azure Resource Manager の展開の使用を開始します。 詳細については、[CMG の計画](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager)に関するページを参照してください。  

    - Azure サブスクリプション ID  

    - Azure 管理証明書  

- サービスのグローバル一意名。 この名前は、[CMG サーバー認証証明書](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate)に含まれています。  

- この CMG 展開の Azure リージョン。  

- スケールと冗長性に必要な VM インスタンスの数。  



## <a name="set-up-a-cmg"></a>CMG を設定する

最上位サイトで以下の手順を実行します。 このサイトはスタンドアロン プライマリ サイト、または中央管理サイトのいずれかです。

1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[Cloud Services]** を展開して **[クラウド管理ゲートウェイ]** を選択します。  

2. リボンの **[クラウド管理ゲートウェイの作成]** を選択します。  

3. バージョン 1802 以降では、ウィザードの [全般] ページで、CMG の展開方法として **[Azure Resource Manager の展開]** を選択します。  

    **[サインイン]** を選択し、Azure サブスクリプション管理者アカウントで認証を行います。 ウィザードは、Azure AD 統合の前提条件の間に格納された情報から、残りのフィールドを自動的に設定します。 複数のサブスクリプションを所有している場合は、使用する適切なサブスクリプションの**サブスクリプション ID** を選びます。

    > [!Note]  
    > バージョン 1810 以降では、Configuration Manager での Azure の従来のサービス展開は推奨されていません。 
    > 
    > 従来のサービス展開を使用する必要がある場合は、このページでそのオプションを選択します。 まず、Azure **サブスクリプション ID** を入力します。 次に **[参照]** を選択し、Azure 管理証明書の .PFX ファイルを選びます。 

4. この CMG の **Azure 環境**を指定します。 ドロップダウン リストのオプションは、展開方法に応じて異なる場合があります。  

5. **[次へ]** を選択します。 サイトで Azure への接続テストが完了するまで待ちます。  

6. ウィザードの [設定] ページで、まず、**[参照]** を選択し、CMG サーバー認証証明書の .PFX ファイルを選択します。 この証明書に含まれている名前で、必要な **[サービス FQDN]** フィールドと **[サービス名]** フィールドが設定されます。  

   > [!NOTE]  
   > バージョン 1802 以降では、CMG サーバー認証証明書でワイルドカードがサポートされます。 ワイルドカード証明書を使用する場合は、**[サービス FQDN]** フィールドのアスタリスク (\*) を CMG の適切なホスト名に置き換えます。  
   <!--491233-->  

7. **[リージョン]** ドロップダウン リストを選択して、この CMG の Azure リージョンを選択します。  

8. バージョン 1802 で Azure Resource Manager の展開を使用する場合は、**[リソース グループ]** オプションを選択します。 
   1. **[既存のものを使用]** を選択した場合は、ドロップダウン リストから既存のリソース グループを選びます。
   2. **[新規作成]** を選択した場合は、新しいリソース グループの名前を入力します。

9. **[VM インスタンス]** フィールドに、このサービスの VM の数を入力します。 既定値は 1 ですが、CMG ごとに VM の数を 16 まで指定できます。  

10. **[証明書]** を選択して、クライアントの信頼されたルート証明書を追加します。 信頼されたルート CA を 2 つ、中間 (下位) CA を 4 つまで指定できます。  

     > [!Note]  
     > バージョン 1806 以降、CMG を作成するときに、[設定] ページで信頼されたルート証明書を指定する必要はなくなりました。 クライアント認証で Azure Active Directory (Azure AD) を使用するときにこの証明書は必要ありませんが、ウィザードで必要な場合は使用されます。 PKI クライアント認証証明書を使用する場合は、引き続き信頼されたルート証明書を CMG に追加する必要があります。<!--SCCMDocs-pr issue #2872-->  

11. 既定では、ウィザードで**クライアント証明書の失効状態を検証する**オプションが有効になります。 この検証を機能させるには、証明書失効リスト (CRL) を公開する必要があります。 CRL を公開しない場合は、このオプションの選択を解除します。  

12. バージョン 1806 以降では、ウィザードにおいて既定で次のオプションが有効にされます: **CMG をクラウド配布ポイントとして機能させて、Azure Storage からのコンテンツを提供できるようにする**。 また、CMG では、コンテンツをクライアントに提供できるようになりました。 この機能により、Azure VM の必要な証明書とコストが削減されます。  

13. **[次へ]** を選択します。  

14. CMG トラフィックを 14 日間のしきい値で監視するには、チェック ボックスをオンにして、しきい値のアラートを有効にします。 次に、しきい値と、別のアラート レベルを上げる割合を指定します。 完了したら、**[次へ]** を選択します。  

15. 設定を確認して、**[次へ]** を選択します。 Configuration Manager がサービスの設定を開始します。 ウィザードを閉じた後に、Azure でサービスが完全にプロビジョニングされるまで 5 分から 15 分かかります。 新しい CMG の **[状態]** 列を確認して、サービスの準備が完了するタイミングを判断します。  

    > [!Note]  
    > CMG 展開のトラブルシューティングを行うには、**CloudMgr.log** と **CMGSetup.log** を使用します。 詳細については、[ログ ファイル](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)に関するページを参照してください。



## <a name="configure-primary-site-for-client-certificate-authentication"></a>クライアント証明書認証用にプライマリ サイトを構成する

クライアントで CMG による認証を行うために[クライアント認証証明書](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate)を使用する場合は、以下の手順に従って各プライマリ サイトを構成します。  

1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[サイトの構成]** を展開して **[サイト]** を選択します。  

2. インターネット ベースのクライアントを割り当てるプライマリ サイトを選択して、**[プロパティ]** を選びます。  

3. プライマリ サイトのプロパティ シートの **[クライアント コンピューターの通信方法]** タブに切り替えて、**[使用可能な場合は PKI クライアント証明書 (クライアント認証機能) を使用する]** をオンにします。  

4. CRL を公開しない場合は、**[サイト システムの証明書失効リスト (CRL) をチェックする]** のオプションの選択を解除します。  



## <a name="add-the-cmg-connection-point"></a>CMG 接続ポイントを追加する

CMG 接続ポイントは、CMG と通信するためのサイト システムの役割です。 CMG 接続ポイントを追加するには、一般的な手順に従って、[サイト システムの役割をインストール](/sccm/core/servers/deploy/configure/install-site-system-roles)します。 サイト システムの役割の追加ウィザードの [システムの役割の選択] ページで、**[クラウド管理ゲートウェイ接続ポイント]** を選択します。 次に、このサーバーの接続先となる**クラウド管理ゲートウェイの名前**を選択します。 ウィザードには選択した CMG のリージョンが表示されます。 

> [!Important]
> 一部のシナリオでは、CMG 接続ポイントに[クライアント認証証明書](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate)が必要になります。 

 > [!Note]  
 > CMG サービス正常性のトラブルシューティングを行うには、**CMGService.log** と **SMS_Cloud_ProxyConnector.log** を使用します。 詳細については、[ログ ファイル](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)に関するページを参照してください。



## <a name="configure-client-facing-roles-for-cmg-traffic"></a>CMG トラフィック用にクライアントと直接接続する役割を構成する

CMG トラフィックを受け入れるように管理ポイントおよびソフトウェアの更新ポイント サイト システムを構成します。 インターネット ベースのクライアントにサービスを提供するすべての管理ポイントおよびソフトウェアの更新ポイントについて、プライマリ サイトで以下の手順を実行します。  

1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[サイトの構成]** を展開して **[サーバーとサイト システムの役割]** ノードを選択します。 リボンの [ホーム] タブの [表示] グループで、**[役割を持つサーバー]** を選択します。 一覧から **[管理ポイント]** を選択します。  

2. CMG トラフィック用に構成するサイト システム サーバーを選択します。 詳細ウィンドウで **[管理ポイント]** 役割を選択して、リボンの **[プロパティ]** を選択します。  

3. 管理ポイント プロパティ シートの [クライアント接続] で、**[Configuration Manager のクラウド管理ゲートウェイ トラフィックを許可する]** の横のチェック ボックスをオンにします。 
    - CMG 設計と Configuration Manager のバージョンに応じて、**HTTPS** オプションを有効にする必要がある場合があります。 詳細については、「[HTTPS 用の管理ポイントを有効にする](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https)」を参照してください。  

4. **[OK]** を選択して、管理ポイントのプロパティ ウィンドウを閉じます。   

必要に応じて追加の管理ポイント、およびすべてのソフトウェアの更新ポイントについて、これらの手順を繰り返します。 



## <a name="configure-clients-for-cmg"></a>CMG 用にクライアントを構成する

CMG とサイト システムの役割が実行されると、クライアントは次の場所の要求で CMG サービスの場所を自動的に取得します。 [認証のために Azure AD を使用して Windows 10 クライアントをインストールして割り当てる](/sccm/core/clients/deploy/deploy-clients-cmg-azure)場合を除き、CMG サービスの場所を受信するにはクライアントがイントラネット上にある必要があります。 場所の要求のポーリング サイクルは 24 時間ごとです。 通常にスケジュール設定された場所の要求を待機したくない場合は、コンピューターで SMS Agent Host サービス (ccmexec.exe) を再起動することによって、要求を強制できます。  

> [!Note]
> 既定では、すべてのクライアントは CMG ポリシーを受信します。 この動作は、クライアント設定の [[クライアントでクラウド管理ゲートウェイを使用できるようにする]](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway) で制御します。

Configuration Manager クライアントは、イントラネット上にあるか、インターネット上にあるかを自動的に判断します。 クライアントがドメイン コントローラーまたはオンプレミス管理ポイントに接続できる場合、その接続の種類が **[現在はイントラネット]** に設定されます。 それ以外の場合は、**[現在はインターネット]** に切り替え、CMG サービスの場所を使用してサイトと通信を行います。

>[!NOTE]
> イントラネット上とインターネット上のどちらにあるかにかかわらず、クライアントで CMG を常に使用するように強制することができます。 この構成は、テスト目的で、あるいは CMG を使用するように強制するリモート オフィスのクライアントの場合に役立ちます。 クライアントで次のレジストリ キーを設定します。
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> [CCMALWAYSINF](/sccm/core/clients/deploy/about-client-installation-properties#ccmalwaysinf) プロパティを使用して、クライアントのインストール時にこの設定を指定することもできます。

クライアントに CMG を指定するポリシーがあることを確認するには、クライアント コンピューターで管理者として Windows PowerShell コマンド プロンプトを開き、次のコマンドを実行します。`Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

このコマンドでは、クライアントで認識されているインターネット ベースの管理ポイントが表示されます。 CMG は技術的にはインターネット ベース管理ポイントではありませんが、クライアントではそのように表示されます。

 > [!Note]  
 > CMG クライアント トラフィックのトラブルシューティングを行うには、**CMGHttpHandler.log**、**CMGService.log**、**SMS_Cloud_ProxyConnector.log** を使用します。 詳細については、[ログ ファイル](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)に関するページを参照してください。



## <a name="modify-a-cmg"></a>CMG を変更する

CMG を作成したら、その設定の一部を変更できます。 Configuration Manager コンソールで CMG を選択して、**[プロパティ]** を選択します。 次のタブで、設定を構成します。  

#### <a name="general"></a>全般

- **Azure 管理証明書**: CMG の Azure 管理証明書を変更します。 このオプションは、有効期限が切れる前に証明書を更新する場合に役立ちます。  

#### <a name="settings"></a>設定

- **証明書ファイル**: CMG のサーバー認証証明書を変更します。 このオプションは、有効期限が切れる前に証明書を更新する場合に役立ちます。  

- **VM インスタンス**: サービスが Azure で使用する仮想マシンの数を変更します。 この設定では、サービスを使用やコストに関する考慮事項に基づいて、動的にスケール アップまたはスケール ダウンすることができます。  

- **証明書**: 信頼されたルートまたは中間 CA 証明書を追加または削除します。 このオプションは、新しい CA を追加する場合や、期限切れの証明書を削除する場合に役立ちます。  

- **クライアント証明書の失効を検証する**: CMG の作成時にこの設定を最初に有効にしなかった場合は、CRL を公開した後に有効にすることができます。  

- **CMG をクラウド配布ポイントとして機能させて、Azure Storage からのコンテンツを提供できるようにする**: バージョン 1806 以降では、この新しいオプションが既定で有効になります。 また、CMG では、コンテンツをクライアントに提供できるようになりました。 この機能により、Azure VM の必要な証明書とコストが削減されます。<!--1358651-->  

#### <a name="alerts"></a>アラート
アラートは、CMG を作成した後で、いつでも再構成できます。 


### <a name="redeploy-the-service"></a>サービスの再展開

次の構成など、より重要な変更には、サービスの再展開が必要です。
- 従来の展開方法から Azure Resource Manager へ
- Subscription
- サービス名
- プライベートからパブリック PKI へ
- リージョン

更新されたポリシーを受信するために、インターネット ベースのクライアントに対して常に 1 つ以上のアクティブな CMG を保持します。 インターネット ベースのクライアントは削除された CMG と通信できません。 クライアントは、イントラネットに再度ローミングされるまで新しいものを認識しません。 最初のものを削除するために 2 番目の CMG インスタンスを作成する場合、別の CMG 接続ポイントも作成します。

既定では、クライアントは 24 時間ごとにポリシーを更新するため、新しい CMG を作成してから古いものを削除するまで少なくとも 1 日待つことになります。 クライアントがオフになっているか、インターネットに接続されていない場合は、さらに長い時間待つ必要がある可能性があります。 

バージョン 1802 以降では、従来の展開方法で既存の CMG を利用している場合、Azure Resource Manager の展開方法を使用するには新しい CMG を展開する必要があります。<!--509753--> 次の 2 つの選択肢があります。  

- 同じサービス名を再利用する場合:  

    1. まず、従来の CMG を削除します。その場合、インターネット ベースのクライアントに対して 1 つ以上のアクティブな CMG を常に保持するためのガイダンスを考慮してください。  

    2. Resource Manager の展開を使用する新しい CMG を作成します。 同じサーバー認証証明書を再利用します。  

    3. 新しい CMG インスタンスを使用するように CMG 接続ポイントを再構成します。  

- 新しいサービス名を使用する場合:  

    1. Resource Manager の展開を使用する新しい CMG を作成します。 新しいサーバー認証証明書を使用します。  

    2. 新しい CMG 接続ポイントを作成して、新しい CMG にリンクします。  

    3. インターネット ベースのクライアントが新しい CMG に関するポリシーを受信するまで少なくとも 1 日待ちます。  

    4. 従来の CMG を削除します。  

> [!Tip]  
> CMG の現在のデプロイ モデルを決定するには、次の手順を実行します。<!--SCCMDocs issue #611-->  
> 1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[Cloud Services]** を展開して **[クラウド管理ゲートウェイ]** ノードを選択します。  
> 2. CMG インスタンスを選択します。  
> 3. ウィンドウの下部にある詳細ウィンドウで、**デプロイ モデル**属性を検索します。 Resource Manager のデプロイでは、この属性は **Azure Resource Manager** です。 
> 
> **デプロイ モデル**属性をリスト ビューに列として追加することもできます。  


### <a name="modifications-in-the-azure-portal"></a>Azure portal での変更

Configuration Manager コンソールで CMG のみを変更します。 Azure でサービスまたは基になる VM を直接変更することはサポートされていません。 すべての変更が気付かないうちに失われる可能性があります。 PaaS の場合と同じように、サービスではいつでも VM をリビルドすることができます。 このリビルドは、バックエンド ハードウェアのメンテナンス、あるいは VM OS への更新プログラムの適用のために行われる場合があります。


### <a name="delete-the-service"></a>サービスの削除

CMG を削除する必要がある場合は、Configuration Manager コンソールでも削除します。 Azure でコンポーネントを手動で削除すると、システムが一貫性のない状態になります。 その場合、情報が孤立した状態のままになり、予期しない動作が発生する可能性があります。 



## <a name="next-steps"></a>次のステップ

- [クラウド管理ゲートウェイのクライアントの監視](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway)
- [クラウド管理ゲートウェイについてよくあるご質問](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
