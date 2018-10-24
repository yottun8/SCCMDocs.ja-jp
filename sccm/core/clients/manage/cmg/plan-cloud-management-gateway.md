---
title: クラウド管理ゲートウェイの計画
titleSuffix: Configuration Manager
description: インターネットを基盤とするクライアントの管理を簡素化するクラウド管理ゲートウェイ (CMG) を計画し、設計します。
ms.date: 09/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9b25b7a5b7df42dc83bec18d38b44c7807e6dc1a
ms.sourcegitcommit: 2badee2b63ae63687795250e298f463474063100
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2018
ms.locfileid: "45601128"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Configuration Manager でクラウド管理ゲートウェイを計画する

*適用対象: System Center Configuration Manager (Current Branch)*
 
<!--1101764--> クラウド管理ゲートウェイ (CMG) は、インターネット上で構成マネージャー クライアントを管理する簡単な方法を提供します。 Microsoft Azure のクラウド サービスとして CMG を展開して、インフラストラクチャを追加せずに、インターネット上を移動する従来のクライアントを管理できます。 また、オンプレミス インフラストラクチャをインターネットに公開する必要がありません。 

> [!Tip]  
> この機能はバージョン 1610 で[プレリリース機能](/sccm/core/servers/manage/pre-release-features)として初めて導入されました。 バージョン 1802 以降、この機能はプレリリース機能ではなくなりました。  


> [!Note]  
> Configuration Manager では、このオプション機能は既定で無効です。 この機能は、使用する前に有効にする必要があります。 詳細については、「[更新プログラムのオプション機能の有効化](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」を参照してください。<!--505213-->  


前提条件を確立した後、Configuration Manager コンソールで次の 3 つの手順を行うことで CMG が作成されます。
1. CMG クラウド サービスを Azure に展開します。
2. CMG 接続ポイント ロールを追加します。 
3. サービスのサイトとサイト ロールを構成します。 展開し、構成すると、クライアントはオンプレミス サイト ロールがイントラネットにあるかインターネットにあるかに関わらず、シームレスにアクセスします。

この記事では、CMG について知る、自分の環境に合うように設計する、実装を計画するための基礎知識を提供します。 



## <a name="scenarios"></a>監視プロセス 

CMG が有益となるシナリオがいくつかあります。 より一般的なシナリオは次のようなシナリオです。  

- Active Directory ドメイン参加 ID のある従来の Windows クライアントを管理します。 このようなクライアントには、Windows 7、Windows 8.1、Windows 10 があります。 PKI 証明書を使用して通信チャネルをセキュリティで保護します。 管理作業には次が含まれます。  
    - ソフトウェア更新とエンドポイント保護
    - インベントリとクライアントの状態
    - コンプライアンス設定
    - デバイスにソフトウェアを配布
    - Windows 10 一括アップグレード タスク シーケンス (バージョン 1802 より)

- 最新の ID を持つ、つまり、Azure Active Directory (Azure AD) に混種か単種でクラウド ドメイン参加している従来の Windows 10 クライアントを管理します。 クライアントでは、PKI 証明書ではなく、Azure AD が認証に利用されます。 Azure AD を利用する場合、複雑な PKI システムより設定、構成、保守管理が簡単です。 管理作業は最初のシナリオと同じものに次が加わります。  
    - ユーザーにソフトウェアを配布  

- インターネット経由で Configuration Manager クライアントを Windows 10 デバイスにインストールします。 Azure AD を利用すると、デバイスでは、クライアントの登録や割り当てのために CMG に認証できます。 クライアントは手動でインストールできます。あるいは、Microsoft Intune など、別のソフトウェア配布方法を利用できます。  

- 新しいデバイス プロビジョニングと共同管理。 共同管理に CMG は必要ありません。 Windows AutoPilot、Azure AD、Microsoft Intune、Configuration Manager が関わる、新しいデバイスのエンドツーエンド シナリオの遂行に役立ちます。  

### <a name="specific-use-cases"></a>特定のユース ケース
以上のシナリオでは、次のような特定のデバイス ユース ケースが適用されることがあります。

- ラップトップなどのローミング デバイス  

- WAN または VPN よりもインターネットでの管理が安価で効率性が良いリモート/支店デバイス。  

- 合併と買収。Azure AD にデバイスを参加させ、CMG 経由で管理するのが簡単な場合があります。  

> [!Important]
> 既定ではすべてのクライアントが CMG のポリシーを受け取り、インターネットベースになるとき、その使用を開始します。 組織に当てはまるシナリオとユース ケースによっては、CMG の使い方を調べる必要があります。 詳細については、「[クライアントでクラウド管理ゲートウェイを使用できるようにする](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway)」のクライアント設定を参照してください。


## <a name="topology-design"></a>トポロジ設計

### <a name="cmg-components"></a>CMG コンポーネント
CMG の展開と操作には、次のコンポーネントが含まれます。  

- Azure の **CMG クラウド サービス**は、Configuration Manager クライアントの要求を認証し、CMG 接続ポイントに転送します。  
 
- **CMG 接続ポイント** サイト システム ロールによって、オンプレミス ネットワークから Azure の CMG サービスまで、一貫性があり、パフォーマンスが高い接続が可能になります。 また、接続情報やセキュリティ設定などの各種設定を CMG に発行します。 CMG 接続ポイントは、URL マッピングに基づき、CMG からオンプレミス ロールにクライアント要求を転送します。

- [**サービス接続ポイント**](/sccm/core/servers/deploy/configure/about-the-service-connection-point) サイト システム ロールは、あらゆる CMG 展開タスクを処理する、クラウド サービス マネージャー コンポーネントを実行します。 また、このコンポーネントは、Azure AD のサービスの正常性とログ情報も監視し、レポートします。 サービス接続ポイントが[オンライン モード](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes)であることを確認します。  

- **管理ポイント** サイト システム ロールは通常のようにクライアント要求にサービスを提供します。  

- **ソフトウェア更新ポイント** サイト システム ロールは通常のようにクライアント要求にサービスを提供します。  

- **インターネットベース クライアント**は CMG に接続し、オンプレミスの Configuration Manager コンポーネントにアクセスします。

- CMG では、**証明書ベースの HTTPS** Web サービスを使用し、クライアントとのネットワーク通信をセキュリティで保護します。  

- インターネットベースのクライアントでは、ID や認証に **PKI 証明書または Azure AD** が使用されます。  

- [**クラウド配布ポイント**](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)によって、必要に応じて、インターネットベースのクライアントにコンテンツを提供されます。  

    - バージョン 1806 からは、CMG でクライアントにコンテンツを提供できるようにもなりました。 この機能により、Azure VM の必要な証明書とコストが削減されます。 詳細については、「[CMG を変更する](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg)」を参照してください。<!--1358651-->  


### <a name="azure-resource-manager"></a>Azure Resource Manager
<!-- 1324735 --> バージョン 1802 以降、**Azure Resource Manager の展開**を利用し、CMG を作成できます。 [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) は、[リソース グループ](/azure/azure-resource-manager/resource-group-overview#resource-groups)と呼ばれる単一のエンティティとしてすべてのソリューション リソースを管理するための最新のプラットフォームです。 Azure Resource Manager で CMG を展開するとき、サイトは Azure Active Directory (Azure AD) を使って必要なクラウド リソースの認証と作成を行います。 この最新の展開では、従来の Azure 管理証明書は必要ありません。  

CMG ウィザードでは、Azure 管理証明書を使う**従来のサービス展開**のためのオプションがまだ提供されています。 リソースの展開と管理を簡単にするため、すべての新しい CMG インスタンスに Azure Resource Manager デプロイ モデル を使うことをお勧めします。 可能であれば、Resource Manager で既存の CMG インスタンスを再展開してください。 詳細については、[CMG の変更](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg)に関するページを参照してください。

> [!IMPORTANT]  
> この機能では、Azure クラウド サービス プロバイダー (CSP) のサポートは有効になりません。 Azure Resource Manager での CMG の展開では引き続き従来のクラウド サービスが使われ、CSP はこれをサポートしません。 詳細については、「[Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)」(Azure CSP で使用可能な Azure サービス) を参照してください。 


### <a name="hierarchy-design"></a>階層の設計

階層の一番上のサイトで CMG を作成します。 それが中央管理サイトである場合は、子プライマリ サイトで CMG 接続ポイントを作成します。 クラウド サービス マネージャー コンポーネントは、中央管理サイトにもある、サービス接続ポイントにあります。 この設計によって、必要に応じて、異なるプライマリ サイト間でサービスを共有できます。

Azure で複数の CMG サービスを作成できます。また、複数の CMG 接続ポイントを作成できます。 CMG 接続ポイントが複数あると、CMG からオンプレミス ロールへのクライアント トラフィックが負荷分散されます。 ネットワークの待ち時間を減らすために、関連 CMG をプライマリ サイトとして同じ地理的リージョンに割り当てます。

 > [!Note]  
 > インターネットベース クライアントと CMG はいかなる境界グループにも入りません。

管理するクライアントの数など、その他の要因も CMG の設計に影響を与えます。 詳細については、「[パフォーマンスと拡張性](#performance-and-scale)」を参照してください。

#### <a name="example-1-standalone-primary-site"></a>例 1: スタンドアロン プライマリ サイト

Contoso は、ニューヨーク市にある本社のオンプレミス データセンターにスタンドアロン プライマリ サイトを置いています。 
- 米国東部 Azure リージョンに CMG を作成し、ネットワークの待ち時間を減らします。 
- CMG 接続ポイントを 2 つ作成します。いずれも 1 つの CMG サービスにリンクされています。  

クライアントがインターネットに接続するとき、米国東部 Azure リージョンの CMG と通信します。 CMG はこの通信を両方の CMG 接続ポイントに転送します。

#### <a name="example-2-hierarchy-with-site-specific-cmg"></a>例 2: サイト固有の CMG を持つ階層

Fourth Coffee は、シアトルの本社にあるオンプレミス データセンターに中央管理サイトを置いています。 プライマリ サイトが 1 つ同じデータセンターにあり、別のプライマリ サイトがパリのヨーロッパ統括オフィスにあります。 
- 中央管理サイトで、2 つの CMG サービスを作成します。
     - 米国西部 Azure リージョンに CMG を 1 つ。
     - ヨーロッパ西部 Azure リージョンに CMG を 1 つ。
- シアトルベースのプライマリ サイトで、米国西部 CMG にリンクされている CMG 接続ポイントを作成します。
- パリベースのプライマリ サイトで、ヨーロッパ西部 CMG にリンクされている CMG 接続ポイントを作成します。

シアトルベースのクライアントがインターネットに接続するとき、米国西部 Azure リージョンの CMG と通信します。 CMG はこの通信をシアトルベースの CMG 接続ポイントに転送します。

同様に、パリベースのクライアントがインターネットに接続するとき、ヨーロッパ西部 Azure リージョンの CMG と通信します。 CMG はこの通信をパリベースの CMG 接続ポイントに転送します。 パリベースのユーザーがシアトルの本社に出張した場合、そのユーザーのコンピューターは引き続きヨーロッパ西部 Azure リージョンの CMG と通信します。 

 > [!Note]  
 > Fourth Coffee は、米国西部 CMG にリンクされているパリベースのプライマリ サイトに別の CMG 接続ポイントを作成することを検討しました。 パリベースのクライアントは、その場所に関係なく、両方の CMG を利用することになります。 この構成では負荷が分散され、サービスに冗長性が与えられますが、パリベースのクライアントが米国ベースの CMG と通信するとき、遅延が引き起こされることがあります。 Configuration Manager クライアントは現在のところ、その地理的リージョンを認識していません。そのため、地理的に近い CMG を優先的に選択しません。 クライアントは利用できる CMG を無作為に利用します。



## <a name="requirements"></a>［要件］

- CMG をホストするための **Azure サブスクリプション**。  

    - **Azure 管理者**は、設計によっては、特定のコンポーネントの初回作成に参加する必要があります。 この管理者には Configuration Manager のアクセス許可は必要ありません。  

- **CMG 接続ポイント**をホストするためのオンプレミス Windows サーバーが少なくとも 1 つ。 このロールと他の Configuration Manager サイト システム ロールは同じ場所に置くことができます。  

- **サービス接続ポイント**は[オンライン モード](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes)にする必要があります。   

- CMG の[**サーバー認証証明書**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate)。  

- Azure クラシック デプロイメントの方法を利用している場合、[**Azure 管理証明書**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#azure-management-certificate)を使用する必要があります。  

    > [!TIP]  
    > Configuration Manager バージョン 1802 以降は、**Azure Resource Manager** 展開モデルの利用をお勧めします。 この管理証明書は必要ありません。  

- クライアントの OS バージョンと認証モデルによっては、**他の証明書**が必要になることがあります。 詳細については、「[CMG 証明書](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)」を参照してください。  

    - バージョン 1802 以降では、CMG が有効なすべての[**管理ポイントで HTTPS を使用する**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https)ように構成する必要があります。  

- Windows 10 クライアントの場合、**Azure AD** との統合が必要になることがあります。 詳細については、「[Azure サービスの構成](/sccm/core/servers/deploy/configure/azure-services-wizard)」を参照してください。  

- クライアントでは **IPv4** を使用する必要があります。  



## <a name="specifications"></a>仕様

- [クライアントとデバイスのサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)に記載されているあらゆるバージョンの Windows が CMG でサポートされています。  

- CMG では、管理ポイント ロールとソフトウェア更新ポイント ロールのみサポートされます。  

- CMG では、IPv6 アドレスとのみ通信するクライアントはサポートされません。<!--495606-->  

- ネットワーク ロード バランサーを利用するソフトウェア更新ポイントは CMG と連動しません。 <!--505311-->  

- バージョン 1802 以降では、Azure Resource Model を使用する CMG 展開では、Azure クラウド サービス プロバイダー (CSP) のサポートが有効になりません。 Azure Resource Manager での CMG の展開では引き続き従来のクラウド サービスが使われ、CSP はこれをサポートしません。 詳細については、「[Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)」 (Azure CSP で使用可能な Azure サービス) を参照してください。  


### <a name="support-for-configuration-manager-features"></a>Configuration Manager の機能のサポート
次の表は、Configuration Manager 機能の CMG サポートをまとめたものです。


|機能  |サポート  |
|---------|---------|
| ソフトウェア更新プログラム     | ![サポートされています](media/green_check.png) |
| エンドポイント保護     | ![サポートされています](media/green_check.png) |
| ハードウェアとソフトウェアのインベントリ     | ![サポートされています](media/green_check.png) |
| クライアント ステータスと通知     | ![サポートされています](media/green_check.png) |
| スクリプトの実行     | ![サポートされています](media/green_check.png) |
| コンプライアンス設定     | ![サポートされています](media/green_check.png) |
| クライアント インストール<br>(Azure AD 統合で)     | ![サポートされています](media/green_check.png)  (1706) |
| ソフトウェア配布 (デバイスを対象に)     | ![サポートされています](media/green_check.png) |
| ソフトウェア配布 (ユーザーを対象とし、必須)<br>(Azure AD 統合で)     | ![サポートされています](media/green_check.png)  (1710) |
| ソフトウェア配布 (ユーザーを対象とし、利用可能)<br>([すべての要件](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![サポートされています](media/green_check.png)  (1802) |
| Windows 10 一括アップグレード タスク シーケンス     | ![サポートされています](media/green_check.png)  (1802) |
| CMPivot     | ![サポートされています](media/green_check.png)  (1806) |
| その他のタスク シーケンス シナリオ     | ![サポートされていません](media/Red_X.png) |
| クライアント プッシュ     | ![サポートされていません](media/Red_X.png) |
| サイトの自動割り当て     | ![サポートされていません](media/Red_X.png) |
| アプリケーション カタログ     | ![サポートされていません](media/Red_X.png) |
| ソフトウェア承認要求     | ![サポートされていません](media/Red_X.png) |
| Configuration Manager コンソール     | ![サポートされていません](media/Red_X.png) |
| ［リモート ツール］     | ![サポートされていません](media/Red_X.png) |
| Web サイトのレポート     | ![サポートされていません](media/Red_X.png) |
| Wake On LAN     | ![サポートされていません](media/Red_X.png) |
| Mac、Linux、UNIX クライアント     | ![サポートされていません](media/Red_X.png) |
| ピア キャッシュ     | ![サポートされていません](media/Red_X.png) |
| オンプレミス MDM     | ![サポートされていません](media/Red_X.png) |


|キー|
|--|
|![サポートされています](media/green_check.png) = この機能はサポートされているあらゆるバージョンの Configuration Manager によって、CMG でサポートされています  |
|![サポート](media/green_check.png) (*YYMM*) = この機能は、バージョン *YYMM* 以降の Configuration Manager によって、CMG でサポートされています  |
|![サポートされていません](media/Red_X.png) = この機能は CMG でサポートされていません |



## <a name="cost"></a>コスト

>[!IMPORTANT]  
>以下のコスト情報は、見積もり目的のみで提供されます。 ご利用の環境によっては、変動要素が他にも存在し、それが CMG 使用の総コストに影響を与えることがあります。

CMG では次の Azure コンポーネントが利用され、Azure サブスクリプション アカウントへの課金が発生します。

#### <a name="virtual-machine"></a>バーチャル マシン

- CMG では、PaaS (サービスとしてのプラットフォーム) として Azure Cloud Services が使用されます。 このサービスでは、計算処理コストを発生させる仮想マシン (VM) が使用されます。  

- Configuration Manager バージョン 1706 では、CMG では Standard A2 VM が使用されます。  

- Configuration Manager バージョン 1710 以降、CMG では Standard A2 V2 VM が使用されます。  

- CMG をサポートする VM インスタンスの数を選択します。 1 が既定値で、16 が最大値です。 この数値は CMG の作成時に設定されます。後で変更し、必要に応じてサービスの規模を変更できます。

- クライアントをサポートするために必要な VM の数については、「[パフォーマンスと拡張性](#performance-and-scale)」を参照してください。

- 予想されるコストについては、「[Azure の料金計算ツール](https://azure.microsoft.com/pricing/calculator/)」を参照してください。

    > [!NOTE]  
    > バーチャル マシンのコストは地域によって異なります。

#### <a name="outbound-data-transfer"></a>送信データの転送

- 課金は Azure から外に出るデータに基づきます (エグレスまたはダウンロード)。 Azure に入ってくるデータは無料です (イングレスまたはアップロード)。 Azure から外に出る CMG データには、クライアントのポリシー、クライアント通知、CMG からサイトに転送されるクライアント応答があります。 このような応答には、インベントリ レポート、ステータス メッセージ、コンプライアンス ステータスがあります。  

- CMG とクライアントの通信がなくても、何らかのバックグラウンド通信によって、CMG とオンプレミス サイトの間にネットワーク トラフィックが発生します。  

- Configuration Manager コンソールで**送信データ転送 (GB)** を表示してください。 詳細については、[CMG でクライアントを監視する方法](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway)に関するページを参照してください。  

- 予想されるコストについては、「[Azure 帯域幅の料金詳細](https://azure.microsoft.com/pricing/details/bandwidth/)」を参照してください。 データ転送の価格設定は階層になっています。 使えば使うほど、ギガバイトあたりで支払う料金が安くなります。  

- インターネットベースのクライアントの場合、クライアントあたり毎月約 100-300 MB が予想されます (*この数値は見積もり目的でのみ提供されます*)。 下の見積もりは、既定のクライアント構成用です。 上の見積もりは、もっと活動的なクライアント構成用です。 実際の使用は、クライアント設定に基づいて変わることがあります。  

   > [!NOTE]  
   > ソフトウェア更新やアプリケーションの展開など、他のアクションを実行すると、Azure から外に出るデータ転送の量が増えます。

#### <a name="content-storage"></a>コンテンツ ストレージ

- インターネットベース クライアントは、Windows Update から無料で Microsoft ソフトウェア更新コンテンツを受け取ります。 Microsoft 更新コンテンツが含まれる更新パッケージをクラウド配布ポイントに配布しないでください。配布すると、ストレージとデータ エグレスのコストが発生することがあります。  

- アプリケーションやサードパーティのソフトウェア更新など、他の必要なコンテンツの場合、クラウドの配布ポイントに配布する必要があります。 現在のところ、CMG では、コンテンツをクライアントに送信するクラウドの配布ポイントのみをサポートしています。  

- 詳細については、[クラウド配布ポイント](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost)の使用のコストに関するページを参照してください。  

- バージョン 1806 からは、CMG でクライアントにコンテンツを提供できるようにもなりました。 この機能により、Azure VM の必要な証明書とコストが削減されます。 詳細については、「[CMG を変更する](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg)」を参照してください。<!--1358651-->  


#### <a name="other-costs"></a>その他のコスト

- クラウド サービスにはそれぞれ、動的 IP アドレスが与えられます。 個々の CMG で新しい動的 IP アドレスが使用されます。 CMG あたりの VM を追加しても、このようなアドレスは増えません。  



## <a name="performance-and-scale"></a>パフォーマンスと拡張性

CMG の拡張性については、「[サイジングとスケールの数値](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)」をご覧ください。

次は、CMG パフォーマンスを改善するための推奨事項です。

- 可能な場合、CMG、CMG 接続ポイント、Configuration Manager のサイト サーバーは同じネットワーク リージョンで構成してください。待機時間を減らすことができます。  

- 現在、Configuration Manager クライアントと CMG 間の接続は、リージョンを意識していません。  

- サービスの可用性を高くするには、少なくとも 2 つの CMG とサイトあたり 2 つの CMG 接続ポイントを作成します。  

- VM インスタンスを追加することで、より多くのクライアントをサポートできるように CMG を拡張します。 Azure Load Balancer では、クライアントのサービスへの接続が制御されます。  

- CMG 接続ポイントを増やすことで、ポイント間の負荷を分散できます。 CMG では、それが接続している CMG 接続ポイントにラウンドロビンでトラフィックが送信されます。  

- サポートしているクライアント数を超えたことで CMG に高い負荷がかかっているときでも要求は処理されますが、遅延が発生することがあります。  


> [!Note]  
> Configuration Manager では、CMG 接続ポイントのクライアント数に対して絶対的な上限が課されていませんが、Windows Server では、TCP 動的ポートの既定の最大範囲が 16,384 になっています。 Configuration Manager サイトで管理している (CMG 接続ポイントが 1 つの) クライアントが 16,384 を超える場合、Windows Server の上限を増やす必要があります。 すべてのクライアントでクライアント通知のためのチャネルが保守管理されています。このチャネルは CMG 接続ポイントでポートを開いています。 netsh コマンドを使用してこの上限を増やす方法については、[Microsoft サポート記事 929851](https://support.microsoft.com/help/929851) を参照してください。



## <a name="ports-and-data-flow"></a>ポートとデータ フロー

オンプレミス ネットワークに受信ポートを開く必要はありません。 サービス接続ポイントと CMG 接続ポイントによって、Azure と CMG とのあらゆる通信が開始されます。 これらの 2 つのサイト システム ロールでは、Microsoft クラウドへの送信接続を作成できる必要があります。 サービス接続ポイントは Azure でサービスを展開し、監視します。そのため、オンライン モードにする必要があります。 CMG 接続ポイントは CMG に接続し、CMG とオンプレミス サイト システム ロールの間の通信を管理します。

CMG の概念を表す基本的なデータ フロー図: ![CMG データ フロー](media/cmg-data-flow.png)
   1. サービス接続ポイントは HTTPS ポート 443 で Azure に接続します。 Azure AD または Azure 管理証明書を利用して認証します。 サービス接続ポイントによって Azure で CMG が展開されます。 CMG によって、サーバー認証証明書を利用し、HTTPS クラウド サービスが作成されます。  

   2. CMG 接続ポイントは TCP TLS または HTTPS で Azure の CMG に接続します。 接続のオープン状態を維持し、将来の 2 方向通信のためのチャネルを構築します。   

   3. クライアントは HTTPS ポート 443 で CMG に接続します。 Azure AD またはクライアント認証証明書を利用して認証します。  

   4. CMG では、既存の接続を利用し、クライアント接続がオンプレミス CMG 接続ポイントに転送されます。 受信ファイアウォール ポートを開く必要はありません。  

   5. CMG 接続ポイントによってクライアント通信がオンプレミス管理ポイントとソフトウェア更新ポイントに転送されます。  

### <a name="required-ports"></a>必要なポート
この表は、必要なネットワーク ポートとプロトコルをまとめたものです。 *クライアント*は接続を開始し、送信ポートを必要とするデバイスです。 *サーバー*は接続を承認し、受信ポートを必要とするデバイスです。 

| クライアント  | プロトコル | ポート  | サーバー  | 説明  |
|---------|---------|---------|---------|---------|
| [サービス接続ポイント]     | HTTPS | 443        | Azure        | CMG のデプロイ |
| CMG 接続ポイント     |  TCP-TLS | 10140-10155        | CMG サービス        | CMG チャネル <sup>1</sup> を構築するための優先プロトコル |
| CMG 接続ポイント     | HTTPS | 443        | CMG サービス       | フォールバックで唯一の VM インスタンスに CMG チャネルを構築する<sup>2</sup> |
| CMG 接続ポイント     |  HTTPS   | 10124-10139     | CMG サービス       | フォールバックで 2 つ以上の VM インスタンスに CMG チャネルを構築する<sup>3</sup> |
| クライアント     |  HTTPS | 443         | CMG        | 一般クライアント通信 |
| CMG 接続ポイント      | HTTPS または HTTP | 443 または 80         | 管理ポイント<br>(バージョン 1706 または 1710) | オンプレミス トラフィック、ポートは管理ポイント構成に依存 |
| CMG 接続ポイント      | HTTPS | 443      | 管理ポイント<br>(バージョン 1802) | オンプレミス トラフィックは HTTPS にする必要あり |
| CMG 接続ポイント      | HTTPS または HTTP | 443 または 80         | ソフトウェアの更新ポイント | オンプレミス トラフィック、ポートはソフトウェア更新ポイント構成に依存 |

<sup>1</sup> CMG 接続ポイントは最初に、各 CMG VM インスタンスと長時間 TCP-TLS 接続を確立しようとします。 ポート 10140 の最初の VM インスタンスに接続します。 2 番目の VM インスタンスではポート 10141 が使用されます。最大で 16 番目のポートでポート 10155 が使用されます。 TCP TLS 接続がパフォーマンスの面で最高ですが、インターネット プロキシをサポートしていません。 CMG 接続ポイントが TCP TLS 経由で接続できない場合、HTTPS にフォールバックします。<sup>2</sup>  

<sup>2</sup> CMG 接続ポイントが TCP-TLS 経由で CMG に接続できない場合<sup>1</sup>、1 つの VM インスタンスのためにのみ、HTTPS 443 で Azure ロード バランサーに接続します。  

<sup>3</sup> 2 つ以上の VM インスタンスがある場合、CMG 接続ポイントは、HTTPS 443 ではなく、HTTPS 10124 を使用し、最初の VM インスタンスに接続します。 HTTPS 10125 で 2 番目の VM インスタンスに接続し、最大で 16 番目が HTTPS ポート 10139 で接続します。


### <a name="internet-access-requirements"></a>インターネット アクセス要件

CMG 接続ポイント サイト システムでは、Web プロキシを使用できます。 プロキシにこのロールを構成する方法については、[プロキシ サーバーのサポート](/sccm/core/plan-design/network/proxy-server-support#to-set-up-the-proxy-server-for-a-site-system-server)に関するページを参照してください。 CMG 接続ポイントには、次のエンドポイントへの接続が必要です。  

- 特定の Azure エンドポイントは、構成によって、環境ごとに異なります。 Configuration Manager はサイト データベースにこれらのエンドポイントを格納します。 Azure エンドポイントの一覧については、SQL Server の **AzureEnvironments** テーブルにクエリを実行してください。  

- ServiceManagementEndpoint (https://management.core.windows.net/)  

- StorageEndpoint (core.windows.net)  

- Configuration Manager のコンソールとクライアントによる Azure AD トークン取得については: ActiveDirectoryEndpoint (https://login.microsoftonline.com/)  

- Azure AD ユーザー検出については: AAD Graph エンドポイント (https://graph.windows.net/)  



## <a name="next-steps"></a>次のステップ

- [クラウド管理ゲートウェイの証明書](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [クラウド管理ゲートウェイのセキュリティとプライバシー](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [クラウド管理ゲートウェイのサイズとスケールの数値](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
- [クラウド管理ゲートウェイについてよくあるご質問](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Set up cloud management gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway) (クラウド管理ゲートウェイの設定)
