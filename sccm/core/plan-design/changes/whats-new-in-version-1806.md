---
title: バージョン 1806 の新機能
titleSuffix: Configuration Manager
description: Configuration Manager Current Branch のバージョン 1806 で導入された変更点および新機能について説明します。
ms.date: 07/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c6ae28a50f3145420895b295ebe730fb7b2a9a7
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386063"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch のバージョン 1806 の新機能

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager Current Branch の更新プログラム 1806 はコンソール内の更新プログラムとして利用できます。 バージョン 1706、1710、1802 を実行しているサイトでこの更新プログラムを適用します。 <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

> [!Important]  
> この記事では現在、このバージョンの重要な機能をすべて取り上げています。 しかしながら、一部のセクションのコンテンツは、新機能に関する後続情報で更新されていません。 更新がないか、このページを定期的にご確認ください。 変更には ***[更新]*** タグが付きます。 コンテンツが最終的に承認されると、この注記は削除されます。  

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in System Center Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4101375).
-->

<!--
The following additional updates to this release are also now available:
- [Update rollup for System Center Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4057517)
-->


次の各セクションでは、Configuration Manager Current Branch のバージョン 1806 の変更点と新機能について説明します。  



<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>サイトのインフラストラクチャ

### <a name="cmpivot"></a>CMPivot
<!--1358456--> Configuration Manager では、レポートを目的として顧客が使用する、デバイス データの大規模な一元化ストアを常に提供しています。 このサイトでは、通常、週次でこのデータが収集されます。 CMPivot は新しいコンソール内ユーティリティであり、お使いの環境でリアルタイム状態のデバイスへのアクセスが提供されるようになります。 対象となるコレクション内の現在接続されているすべてのデバイス上で直ちにクエリを実行して、結果を返します。 ツール内で、このデータのフィルター処理およびグループ化が可能です。 オンライン クライアントからリアルタイム データを提供することで、業務上の質問に迅速に回答し、問題をトラブルシューティングし、セキュリティの問題に対応できます。 

詳細については、[CMPivot](/sccm/core/servers/manage/cmpivot) に関するページを参照してください。  


### <a name="site-server-high-availability"></a>サイト サーバーの高可用性
<!--1128774--> スタンドアロン プライマリ サイト サーバーの役割の高可用性は、追加のサイト サーバーをパッシブ モードでインストールするための Configuration Manager ベースのソリューションです。 パッシブ モードのサイト サーバーは、アクティブ モードになっている既存のサイト サーバーに加えられます。 パッシブ モードのサイト サーバーは、必要なときにすぐに使用できます。 

詳細については、以下の記事を参照してください。 
- [サイト サーバーの高可用性](/sccm/core/servers/deploy/configure/site-server-high-availability) 
- [フローチャート - パッシブ モードでサイト サーバーを設定する](/sccm/core/servers/deploy/configure/passive-site-server-flowchart)
- [フローチャート - サイト サーバーの昇格 (計画済)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart)
- [フローチャート - サイト サーバーの昇格 (計画外)](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart)


### <a name="improvements-to-management-insights"></a>管理分析情報の機能強化
このリリースでは、管理分析情報が次の点で機能強化されています。  

- 管理分析情報のいくつかで対策を行うことが可能になりました。 この対策は、コンソールで関連ノードに移動するか、フィルターを適用した、クエリベースのビューを表示することです。<!--1357930-->  

- プロアクティブ メンテナンスの新しいグループを 6 つの新しいルールで利用できます。通常の保守で回避される可能性がある構成問題を目立たせるのに役立ちます。<!--1352184-->  

詳細については、[管理分析情報](/sccm/core/servers/manage/management-insights)に関するページを参照してください。


### <a name="configuration-manager-tools"></a>Configuration Manager ツール
<!--1357145--> Configuration Manager のサーバー ツールとクライアント ツールがサーバーに含まれるようになりました。 サイト サーバーの `CD.Latest\SMSSETUP\Tools` フォルダーにあります。 追加でインストールする必要はなくなりました。 

詳細については、「[Configuration Manager ツール](/sccm/core/support/tools)」を参照してください。


### <a name="exclude-active-directory-containers-from-discovery"></a>探索から Active Directory コンテナーを除外する
<!--1358143--> 探索されるオブジェクト数を減らすためには、Active Directory システム探索から特定のコンテナーを除外します。 



## <a name="content-management"></a>コンテンツ管理

### <a name="configure-a-remote-content-library-for-the-site-server"></a>サイト サーバーのリモート コンテンツ ライブラリを構成する
<!--1357525--> 高可用性サイト サーバーを構成する、または中央管理サーバーやプライマリ サイト サーバー上でハード ドライブ領域を解放するには、コンテンツ ライブラリを別の記憶域の場所に再配置します。 コンテンツ ライブラリは、サイト サーバー上の別のドライブ、別のサーバー、または記憶域ネットワーク (SAN) 内のフォールトトレラント ディスクに移動します。 

詳細については、以下の記事を参照してください。 
- [コンテンツ ライブラリ](/sccm/core/plan-design/hierarchy/the-content-library)
- [フローチャート - コンテンツ ライブラリの管理](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Azure Resource Manager のためのクラウド配布ポイントのサポート
<!--1322209--> クラウド配布ポイントを作成するときに、**Azure Resource Manager の展開**を作成するためのオプションがウィザードで提供されるようになりました。 Azure Resource Manager は、リソース グループと呼ばれる単一のエンティティとしてすべてのソリューション リソースを管理するための最新のプラットフォームです。 Azure Resource Manager でクラウド配布ポイントを展開するとき、サイトは Azure Active Directory を使って必要なクラウド リソースの認証と作成を行います。 この最新の展開では、従来の Azure 管理証明書は必要ありません。 

クラウド配布ポイントの機能ドキュメントも改訂され、改善されています。 詳細については、以下の記事を参照してください。
- [クラウド配布ポイントの使用](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)   
- [クラウド配布ポイントのインストール](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>ソースとしてのクラウド配布ポイントのプル配布ポイントのサポート  
<!--1321554--> 多くのお客様がリモート オフィスまたは支社でプル配布ポイントを使用して、WAN 経由でソース配布ポイントからコンテンツをダウンロードします。 リモート オフィスでより良好なインターネット接続を確保したい場合、あるいは WAN リンクへの負荷を減らすために、Microsoft Azure でソースとしてクラウド配布ポイントを使用できるようになりました。 配布ポイント プロパティの **[プル配布ポイント]** タブでソースを追加する場合に、サイトのクラウド配布ポイントが利用可能な配布ポイントとしてリストされるようになりました。 それ以外の場合、両方のサイト システムの役割の動作は変わりません。 

詳細については、「[プル配布ポイントの使用](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)」をご覧ください。


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>ネットワークの輻そう制御を使用する配布ポイントを有効にする
<!--1358112--> Windows Low Extra Delay Background Transport (LEDBAT) は、バックグラウンド ネットワーク転送を管理するための Windows Server の機能です。 サポートされている Windows Server のバージョンで実行される配布ポイントに対して、ネットワーク トラフィックの調整に役立つオプションを有効にします。 クライアントは利用可能な場合のみ、ネットワーク帯域幅を使用します。 

詳細については、「[Windows LEDBAT](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#windows-ledbat)」を参照してください。


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>WAN の使用率を減らすためのクライアント ピア キャッシュでの部分的なダウンロードのサポート
<!--1357346--> クライアント ピア キャッシュ ソースのコンテンツを分割できるようになりました。 これにより、ネットワーク転送が最小限に抑えられ、WAN の使用率が減ります。 管理ポイントでは、コンテンツの各パートをより詳細に追跡することができます。 境界グループごとに同じ内容が複数回ダウンロードされないようにします。 

詳細については、「[一部ダウンロードのサポート](/sccm/core/plan-design/hierarchy/client-peer-cache#bkmk_parts)」を参照してください。 


### <a name="boundary-group-options-for-peer-downloads"></a>ピアのダウンロードの境界グループのオプション
<!--1356193--> 環境内のコンテンツ配布をより細かく制御できるように、境界グループに追加の設定が設けられました。 このリリースでは、次のオプションが追加されます。  

- **[この境界グループのピアのダウンロードを許可する]**: この設定は既定で有効になります。 管理ポイントでは、ピア ソースを含むコンテンツの場所のリストがクライアントに提供されます。 この設定は、配信の最適化のグループ ID 適用にも反映されます。  

- **[ピアのダウンロード中に、同じサブネット内のピアのみを使用する]**: この設定は、上記のいずれかに依存します。 このオプションを有効にした場合、管理ポイントのコンテンツの場所のリストには、クライアントと同じサブネット内にあるピア ソースのみが含まれます。  



<!-- ## Migration  -->



## <a name="client-management"></a>クライアント管理

### <a name="improvement-to-client-push-security"></a>クライアント プッシュ セキュリティの機能改善
<!--1358204--> Configuration Manager クライアントのインストールのクライアント プッシュ メソッドを使用する場合、サイトでは Kerberos 相互認証を要求できるようになりました。 この機能強化は、サーバーとクライアント間の通信をセキュリティで保護するのに役立ちます。 

詳細については、「[クライアント プッシュを使用したクライアントのインストール方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush)」を参照してください。


### <a name="bkmk_ehttp"></a> 拡張 HTTP サイト システム
<!--1356889,1358228--> HTTPS 通信の使用は、すべての Configuration Manager 通信パスで推奨されていますが、PKI 証明書の管理のオーバーヘッドが原因で、一部の顧客にとっては、この使用が困難な課題になってしまう場合があります。 Azure Active Directory (Azure AD) の統合を導入することで、一部は軽減されますが、証明書要件のすべてには対応できません。 

このリリースでは、クライアントがシステム クライアントと通信する方法を強化しました。 サイトのプロパティの **[クライアント コンピューターの通信方法]** タブで、**[HTTPS または HTTP]** のオプションを選択してから、**[HTTP サイト システムには Configuration Manager によって生成された証明書を使用する]** の新しいオプションを有効にします。 この機能は[プレリリース版の機能](/sccm/core/servers/manage/pre-release-features)です。

このオプションでは、次のプライマリ シナリオがサポートされます。  

- **HTTP 管理ポイントへのクライアント**<!--1356889-->: [Azure AD に参加したデバイス](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices)は、HTTP 用に構成された管理ポイントを使用して、クラウド管理ゲートウェイ (CMG) 経由で通信できます。 サイト サーバーは、管理ポイントに対する証明書を生成して、安全なチャネル経由での通信を可能にします。   

- **HTTP 配布ポイントへのクライアント**<!--1358228-->: ワークグループまたは Azure AD に参加しているクライアントは、HTTP 用に構成されている配布ポイントから安全なチャネル経由でコンテンツをダウンロードできます。   


### <a name="azure-ad-device-identity"></a>Azure AD デバイス ID 
<!--1358460--> [Azure AD に参加している](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices)、または[ハイブリッドの Azure AD デバイス](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices)は、サインインしている Azure AD ユーザーがいない場合、割り当てられているサイトと安全に通信できます。 現在は、CMG および管理ポイントで認証するには、クラウドベースのデバイス ID で十分になりました。  


### <a name="cmtrace-installed-with-client"></a>クライアントと共にインストールされる CMTrace
<!--1357971--> CMTrace ログ表示ツールが、Configuration Manager クライアントと共に自動的にインストールされるようになりました。 このツールは、クライアント インストール ディレクトリ (既定では、`%WinDir%\ccm\cmtrace.exe`) に追加されます。 

詳細については、「[CMTrace](/sccm/core/support/cmtrace)」を参照してください。


### <a name="cloud-management-dashboard"></a>クラウド管理ダッシュボード
<!--1358461--> 新しいクラウド管理ダッシュボードでは、クラウド管理ゲートウェイ (CMG) 使用量を一元化したビューを提供します。 Azure AD でサイトがオンボードになっている場合、クラウド ユーザーおよびデバイスに関するデータも表示します。 Configuration Manager コンソールで、**[監視]** ワークスペースに移動します。 **[クラウド管理]** ノードを選択して、ダッシュボード タイルを表示します。  

また、この機能には、トラブルシューティングを支援するリアルタイム検証のための **CMG 接続アナライザー**も含まれます。 コンソール内ユーティリティは、サービスの状態と、CMG 接続ポイント経由で CMG トラフィックを許可する任意の管理ポイントへの通信チャネルをチェックします。 Configuration Manager コンソールで、**[管理]** ワークスペースに移動します。 **[クラウド サービス]** を展開し、**[クラウド管理ゲートウェイ]** を選択します。 対象となる CMG インスタンスを選択して、リボンにある **[接続アナライザー]** をクリックします。


### <a name="improvements-to-cloud-management-gateway"></a>クラウド管理ゲートウェイの機能改善

バージョン 1806 では、クラウド管理ゲートウェイ (CMG) が次の点で機能強化されています。

#### <a name="simplified-client-bootstrap-command-line"></a>簡略化されたクライアント ブートストラップ コマンド ライン
<!--1358215--> CMG を介してインターネット上に Configuration Manager クライアントをインストールするときに、コマンド ラインで必要となるプロパティが少なくなりました。 この改善により、共同管理のための準備をするとき、Microsoft Intune で使用されるコマンド ラインのサイズが縮小されます。 

すべてのシナリオで次のコマンド ライン プロパティが必要になります。
  - CCMHOSTNAME  
  - SMSSITECODE  

PKI ベースのクライアント認証証明書ではなく、クライアント認証で Azure AD を使用する場合は、次のプロパティが必要です。
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

クライアントがイントラネットに再度ローミングされる場合は、次のプロパティが必要です。
  - SMSMP  

次の例には、上記のプロパティのすべてが含まれます。   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

<!--For more information, see [Client installation properties](/sccm/core/clients/deploy/about-client-installation-properties).-->

#### <a name="download-content-from-a-cmg"></a>CMG からコンテンツをダウンロードする
<!--1358651--> これまでは、別の役割として、クラウド配布ポイントと CMG を展開する必要がありました。 CMG では、コンテンツをクライアントに提供できるようになりました。 この機能により、Azure VM の必要な証明書とコストが削減されます。 この機能を有効にするには、CMG プロパティの **[設定]** タブで **[Allow CMG to function as a cloud distribution point and serve content from Azure storage]\(CMG をクラウド配布ポイントとして機能させて、Azure Storage からのコンテンツを提供できるようにする\)** という新しいオプションを有効にします。 

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Azure AD では信頼されたルート証明書が必要ない
<!--503899--> CMG を作成するときに、[設定] ページで[信頼されたルート証明書](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-trusted-root-certificate-to-clients)を指定する必要はなくなりました。 クライアント認証で Azure Active Directory (Azure AD) を使用するときにこの証明書は必要ありませんが、ウィザードで必要な場合は使用されます。 PKI クライアント認証証明書を使用する場合は、引き続き信頼されたルート証明書を CMG に追加する必要があります。



## <a name="co-management"></a>共同管理

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>共同管理されたデバイスのために MDM ポリシーを Microsoft Intune から同期する
<!--1357377--> 共同管理ワークロードを切り替えるときに、共同管理されたデバイスで自動的に Microsoft Intune から MDM ポリシーが同期されます。 この同期は、Configuration Manager コンソールのクライアント通知から**コンピューター ポリシーのダウンロード**操作を開始するときにも行われます。 

詳細については、「[Configuration Manager のワークロードを Intune に切り替える](/sccm/core/clients/manage/co-management-switch-workloads)」を参照してください。


### <a name="transition-new-workloads-to-intune-using-co-management"></a>共同管理を使用して Intune に新しいワークロードを移行する
次のワークロードは、共同管理を有効にした後に、Configuration Manager から Intune に移行できるようになりました。  

- **デバイス構成**<!--1357903-->: このワークロードでは、Intune を使用して MDM ポリシーを展開できます。アプリケーションの展開には Configuration Manager を引き続き使用します。  

- **Office 365**<!--1357841-->: デバイスでは、Configuration Manager から Office 365 展開をインストールしません。  

- **モバイル アプリ**<!--1357892-->: Intune から展開された使用可能なアプリが、すべてポータル サイトで使用可能になります。 Configuration Manager から展開するアプリは、ソフトウェア センターで使用できます。 この機能は[プレリリース版の機能](/sccm/core/servers/manage/pre-release-features)です。  

これらのワークロードを切り替えるには、共同管理プロパティ ページに進み、ワークロード スライド バーを Configuration Manager から**パイロット**または**すべて**に動かします。 

詳細については、「[Windows 10 デバイスの共同管理](/sccm/core/clients/manage/co-management-overview)」を参照してください。


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>1 つの Intune テナントで複数の階層をサポート
<!--1357944--> 一部のお客様は Configuration Manager 階層を複数持ち、将来、Azure Active Directory と Microsoft Intune のシングル テナントに統合することを希望します。 共同管理では、複数の Configuration Manager 環境を同じ Intune テナントに接続できるようになりました。

詳細については、「[共同管理用に Windows 10 デバイスを準備する](/sccm/core/clients/manage/co-management-prepare)」を参照してください。
 


## <a name="compliance-settings"></a>コンプライアンス設定

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Microsoft Edge 用に Windows Defender SmartScreen 設定を構成する
<!--1353701--> Microsoft Edge ブラウザーのコンプライアンス設定ポリシーにより、Windows Defender SmartScreen に次の 3 つの設定が追加されます。 
- SmartScreen を許可する
- サイトの SmartScreen プロンプトをユーザーがオーバーライドできる
- ファイルの SmartScreen プロンプトをユーザーがオーバーライドできる

詳細については、「[Microsoft Edge の設定の構成](/sccm/compliance/deploy-use/browser-profiles)」を参照してください。


### <a name="scap-extensions"></a>SCAP 拡張機能
<!--1357552--> Security Content Automation Protocol (SCAP) コンテンツをコンプライアンス設定基準に変換し、コンソール拡張機能を利用して SCAP レポートを生成します。 この機能には、クライアント コンプライアンスと XCCDF ルール コンプライアンスを視覚化するための新しいダッシュボードも含まれています。 

詳細については、[SCAP 拡張機能](/sccm/compliance/plan-design/scap/about-scap)に関するページを参照してください。



## <a name="application-management"></a>アプリケーション管理

### <a name="phased-deployment-of-applications"></a>アプリケーションの段階的な展開
<!--1358147--> アプリケーションの段階的な展開を作成します。 段階的な展開を使用すると、カスタマイズ可能な条件およびグループに基づいて、調整およびシーケンス化されたソフトウェアの展開をまとめることができます。 たとえば、アプリケーションをパイロット コレクションに展開し、成功条件に基づいてロールアウトを自動続行します。 

詳細については、以下の記事を参照してください。  

- [段階的な展開の作成](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [段階的な展開の管理と監視](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>デバイス上のすべてのユーザーに対して Windows アプリ パッケージをプロビジョニングする
<!--1358310--> デバイス上のすべてのユーザーに対して、Windows アプリ パッケージを含むアプリケーションをプロビジョニングします。 このシナリオの 1 つの一般的な例では、ある学校の生徒が使用するすべてのデバイスに、Minecraft: Education Edition などの、ビジネス向け Microsoft Store および教育機関向け Microsoft Store からアプリをプロビジョニングします。 これまでは、Configuration Manager では、これらのアプリケーションのユーザーごとのインストールのみがサポートされていました。 新しいデバイスにサインインした後、学生はアプリにアクセスするまで待機する必要があります。 これからは、すべてのユーザー用のデバイスにアプリがプロビジョニングされている場合、より迅速に生産性を高めることができます。 

詳細については、[Windows アプリケーションの作成](/sccm/apps/get-started/creating-windows-applications#bkmk_provision)に関する記述を参照してください。


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Office 365 インストーラーと Office カスタマイズ ツールの統合
<!--1358149--> Office カスタマイズ ツールが、Configuration Manager コンソールの Office 365 インストーラーと統合されました。 Office 365 の展開を作成するときに、最新の Office の管理容易性設定を動的に構成します。 Microsoft は、Office 365 の新しいビルドをリリースするとき、Office カスタマイズ ツールを更新します。 この統合により、Office 365 で新しい管理容易性設定が利用可能になるのと同時にそれを活用できます。 

詳細については、「[Office 365 アプリを展開する](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)」を参照してください。


### <a name="support-for-new-windows-app-package-formats"></a>新しい Windows アプリ パッケージ形式のサポート
<!--1357427--> Configuration Manager は、新しい Windows 10 アプリ パッケージ (.msix) とアプリ バンドル (.msixbundle) 形式の展開をサポートするようになりました。 

詳細については、[Windows アプリケーションの作成](/sccm/apps/get-started/creating-windows-applications#bkmk_general)に関する記述を参照してください。


### <a name="uninstall-application-on-approval-revocation"></a>承認を取り消したときにアプリケーションをアンインストールする
<!--1357891--> アプリケーションの承認を取り消したときの動作が変更されました。 アプリケーションの要求を拒否すると、クライアントによってユーザーのデバイスからアプリケーションがアンインストールされます。 この動作には、[オプション機能](https://docs.microsoft.com/en-us/sccm/core/servers/manage/install-in-console-updates#bkmk_options)の **[デバイスごとにユーザーのアプリケーション要求を承認します]** を有効にすることが要求されます。 

詳細については、「[アプリケーションの展開](/sccm/apps/deploy-use/deploy-applications#bkmk_approval)」をご覧ください。


### <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861--> Package Conversion Manager は統合ツールとなりました。これを使用して、従来の Configuration Manager 2007 パッケージを Configuration Manager の現在のブランチのアプリケーションに変換することができます。 その後、依存関係、要件の規則、およびユーザーとデバイスのアフィニティなど、アプリケーションの機能を使用することができます。

Configuration Manager コンソールの **[パッケージ]** ノードの次のアクションから始めます。  

   - **パッケージの分析**: パッケージを分析して、変換プロセスを開始します。  

   - **Convert Package (パッケージの変換)**: 一部のパッケージは、この操作でアプリケーションに簡単に変換することができます。  

   - **Fix and Convert (修正と変換)**: 一部のパッケージでは、アプリケーションに変換する前に問題を修正する必要があります。  

次に、**[監視]** ワークスペースの **[パッケージ変換のステータス]** に移動します。 この新しいダッシュボードには、サイトでのパッケージの全体的な分析と変換の状態が示されます。 この機能は[プレリリース版の機能](/sccm/core/servers/manage/pre-release-features)です。



## <a name="os-deployment"></a>OS の展開

### <a name="improvements-to-phased-deployments"></a>段階的な展開の機能強化

このリリースには、段階的な展開に対する次の機能改善が含まれています。  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>手動で構成されたフェーズを使用して段階的展開を作成する
<!--1358148--> タスク シーケンスについては、今後、段階的展開を作成するとき、フェーズを手動で構成します。 段階的展開の作成ウィザードの **[フェーズ]** タブから、最大 10 個のフェーズを追加します。 引き続き、既定の 2 つの段階の展開を自動的に作成できます。 

詳細については、[ 手動で構成したフェーズを使用して段階的展開を作成する](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_manual)方法に関するページを参照してください。

#### <a name="phased-deployment-status"></a>段階的な展開の状態
<!--1358577--> 段階的な展開に、ネイティブの監視機能が追加されました。 **[監視]** ワークスペースの **[展開]** ノードから段階的な展開を選択し、リボンで **[段階的な展開の状態]** をクリックします。 

詳細については、「[Manage and monitor phased deployments](/sccm/osd/deploy-use/manage-monitor-phased-deployments)」 (段階的展開の管理と監視) を参照してください。  

#### <a name="gradual-rollout-during-phased-deployments"></a>段階的な展開中の段階的なロールアウト
<!--1358578--> 段階的な展開中、各フェーズのロールアウトが段階的に発生するようになりました。 この動作は展開に関する問題のリスクを軽減するのに役立ち、クライアントへのコンテンツの配布によるネットワークの負荷を減少させます。 サイトは、各フェーズの構成に基づいて、ソフトウェアを段階的に利用可能にしていくことができます。 フェーズ内の各クライアントには、ソフトウェアが利用可能になった時間に基づく期限が設定されます。 利用可能時間と期限の間の時間枠は、フェーズ内のすべてのクライアントで同じです。 

詳細については、「[フェーズの設定](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_settings)」をご覧ください。  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Windows 10 一括アップグレード タスク シーケンスの機能強化
<!--1358500--> Windows 10 の一括アップグレード用の既定のタスク シーケンス テンプレートに、アップグレード プロセスが失敗した場合に追加する推奨アクションを備えた、新しい別のグループが含まれるようになりました。 これらのアクションによって、トラブルシューティングが容易になりました。 このようなツールの 1 つが、Windows の [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) です。 これは、Windows 10 がアップグレードに失敗した詳細な理由を取得する、スタンドアロンの診断ツールです。 

詳細については、[OS をアップグレードするタスク シーケンスの作成](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-on-failure)に関するページを参照してください。


### <a name="improvements-to-pxe-enabled-distribution-points"></a>PXE 対応の配布ポイントの機能強化
<!--1357580--> 配布ポイントのプロパティの **[PXE]** タブで、**[Windows 展開サービスなしで PXE レスポンダーを有効にする]** をオンにします。 この新しいオプションは、配布ポイントで PXE レスポンダーを有効にし、Windows 展開サービス (WDS) を必要としません。 WDS が必要ないため、Windows Server Core などのクライアントまたはサーバー OS を、PXE が有効な配布ポイントにすることができます。 この新しい PXE レスポンダー サービスは、IPv6 をサポートするだけでなく、リモート オフィスの PXE が有効な配布ポイントの柔軟性も向上させます。 

詳細については、[配布ポイントでの PXE の有効化](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)に関するページを参照してください。


### <a name="network-access-account-not-required-for-some-scenarios"></a>一部のシナリオで必要とされないネットワーク アクセス アカウント
<!--1358278,1358279--> [拡張 HTTP サイト システム](#bkmk_ehttp)機能では、ネットワーク アクセス アカウントに対する依存関係もいくつか削除されます。 **[Use Configuration Manager-generated certificates for HTTP site systems]\(HTTP サイト システム用に Configuration Manager で生成された証明書を使用する\)** という新しいサイト オプションを有効にする場合、次のシナリオでは、配布ポイントからコンテンツをダウンロードするためのネットワーク アクセス アカウントは必要ありません。  

- ブート メディアまたは PXE から実行されているタスク シーケンス
- ソフトウェア センターから実行されているタスク シーケンス  

これらのタスク シーケンスは、OS の展開用またはカスタム用の場合があります。 ワークグループ コンピューターでもサポートされます。


### <a name="other-improvements-to-os-deployment"></a>OS 展開のその他の機能強化

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>タスク シーケンス変数に格納されている機密データをマスキングする
<!--1358330--> [[タスク シーケンス変数の設定]](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) 手順で **[この値を表示しない]** という新しいオプションを選択します。 たとえば、パスワードを指定するときに使用します。 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>タスク シーケンスのコマンドの実行ステップ中にプログラム名をマスキングする
<!--1358493--> 機密性が高い可能性のあるデータが表示または記録されないようにするには、タスク シーケンス変数 **OSDDoNotLogCommand** を `TRUE` に設定します。 この変数は、[[コマンド ラインの実行]](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) タスク シーケンス ステップ中に smsts.log のプログラム名をマスキングします。   

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>ドライバーをインストールするときの DISM パラメーターのタスク シーケンス変数
<!--516679--> DISM の追加コマンドライン パラメーターを指定するには、**OSDInstallDriversAdditionalOptions** という新しいタスク シーケンス変数を使用します。 [ドライバー パッケージの適用](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage)手順設定を有効にし、**再帰処理オプションを付けて DISM を実行してドライバー パッケージをインストール**します。 

#### <a name="option-to-use-full-disk-encryption"></a>ディスク全体の暗号化を使用するオプション
<!--SCCMDocs-pr issue 2671--> [BitLocker の有効化](/sccm/osd/understand/task-sequence-steps#BKMK_EnableBitLocker)手順と [BitLocker の事前プロビジョニング](/sccm/osd/understand/task-sequence-steps#BKMK_PreProvisionBitLocker)手順の両方に**ディスク全体の暗号化を使用する**オプションが含まれるようになりました。 既定では、これらの手順により、ドライブ上の使用済み領域が暗号化されます。 高速であり、効率性に優れているため、この既定の動作をお勧めします。 組織でセットアップ中、ドライブ全体の暗号化が要求される場合、このオプションを有効にしてください。 Windows セットアップでは、ドライブ全体が暗号化されるのを待ちます。これには、特に大きなドライブで、時間がかかります。 



## <a name="software-center"></a>ソフトウェア センター

### <a name="software-center-infrastructure-improvements"></a>ソフトウェア センターのインフラストラクチャの改善
<!--1358309--> ユーザーが利用できるアプリケーションをソフトウェア センターに表示するのにアプリケーション カタログの役割は必要なくなりました。 この変更は、ユーザーにアプリケーションを配布するために必要なサーバー インフラストラクチャを減らすのに役立ちます。 ソフトウェア センターは、この情報を取得するために管理ポイントに依存するようになりました。より大規模な環境を、[境界グループ](/sccm/core/servers/deploy/configure/boundary-groups#management-points)に割り当てることでより適切にスケーリングすることができます。

> [!Note]  
> アプリケーション カタログの Web サイト ポイントの役割と Web サービス ポイントの役割は 1806 では*不要*になりましたが、依然として*サポート*されている役割です。 
> 
> アプリケーション カタログ Web サイト ポイントの **Silverlight ユーザー エクスペリエンス**は現在サポートされていません。 詳細については、[削除された機能と非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)に関するページを参照してください。  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>ソフトウェア センターのアプリケーション カタログ Web サイト リンクの表示を指定する
<!--1358214--> クライアント設定を使用して、ソフトウェア センターの **[インストール状態]** ノードに **[アプリケーション カタログ Web サイトを開く]** のリンクを表示するかどうかを制御します。  

詳細については、[ソフトウェア センターのクライアント設定](/sccm/core/clients/deploy/about-client-settings#software-center)に関するページを参照してください。

> [!Note]  
> アプリケーション カタログ Web サイト ポイントの **Silverlight ユーザー エクスペリエンス**は現在サポートされていません。 詳細については、[削除された機能と非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)に関するページを参照してください。  


### <a name="custom-tab-for-webpage-in-software-center"></a>ソフトウェア センターの Web ページのカスタム タブ
<!--1358132--> クライアント設定を使用してカスタマイズされたタブを作成し、ソフトウェア センターで Web ページを開きます。 この機能では、一貫性のある信頼性の高い方法で、エンドユーザーにコンテンツを表示することができます。 以下のリストには例がいくつか含まれています。  

- IT に連絡: 組織の IT 部門に連絡する方法に関する情報  

- IT サポート センター: サポート技術情報を検索する、サポート チケットを開くなどの IT セルフ サービス アクション。  

- エンドユーザー文書: アプリケーションの使用や Windows 10 へのアップグレードなど、さまざまな IT トピックに関する組織内のユーザー向けの記事。  

詳細については、[ソフトウェア センターのクライアント設定](/sccm/core/clients/deploy/about-client-settings#software-center)に関するページと「[ソフトウェア センターのユーザー ガイド](/sccm/core/understand/software-center)」を参照してください。


### <a name="maintenance-windows-in-software-center"></a>ソフトウェア センターのメンテナンス期間
<!--1358131--> ソフトウェア センターでは、次のスケジュールされたメンテナンス期間が表示されるようになりました。 [インストールのステータス] タブで、[すべて] のビューを [今後のタスク] に切り替えます。 ここには、スケジュールされている展開のリストと時間の範囲が表示されます。 今後のメンテナンス期間がない場合、リストは空白です。 

詳細については、「[メンテナンス期間を使用する方法](/sccm/core/clients/manage/collections/use-maintenance-windows)」と「[ソフトウェア センターのユーザー ガイド](/sccm/core/understand/software-center)」を参照してください。



## <a name="software-updates"></a>ソフトウェア更新プログラム

### <a name="third-party-software-updates"></a>サード パーティ製ソフトウェアの更新プログラム
<!--1357605, 1352101, 1358714--> サードパーティ製ソフトウェアの更新プログラムでは、Configuration Manager コンソールでパートナー カタログを購読したり、WSUS に更新プログラムを公開したりできます。 その後、既存のソフトウェア更新プログラムの管理プロセスを使用してこれらの更新プログラムを展開できます。 

詳細については、「[Enable third-party updates](/sccm/sum/deploy-use/third-party-software-updates)」 (サードパーティ製更新プログラムを有効にする) を参照してください。


### <a name="deploy-software-updates-without-content"></a>コンテンツなしのソフトウェア更新プログラムの展開
<!--1357933--> 最初にコンテンツをダウンロードして配布ポイントに配布することなく、ソフトウェア更新プログラムをデバイスに展開します。 この機能は、非常に大きい更新プログラムのコンテンツを処理する場合や、常にクライアントで Microsoft Update クラウド サービスからコンテンツを取得する場合に役立ちます。 このシナリオのクライアントでは、既に必要なコンテンツがあるピアからコンテンツをダウンロードすることもできます。 Configuration Manager クライアントで引き続きコンテンツのダウンロードが管理されるため、Configuration Manager のピア キャッシュ機能や、配信の最適化などの他のテクノロジを利用することができます。 この機能では、Windows および Office の更新プログラムを含む、Configuration Manager ソフトウェア更新プログラム管理でサポートされるすべての更新プログラムの種類がサポートされます。 

詳細については、「[ソフトウェア更新プログラムの手動展開](/sccm/sum/deploy-use/manually-deploy-software-updates)」または「[ソフトウェア更新プログラムの自動展開](/sccm/sum/deploy-use/automatically-deploy-software-updates)」の**展開パッケージなし**オプションを参照してください。


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>ソフトウェア更新アーキテクチャを使用した自動展開規則のフィルター処理
 <!--1322266--> 自動展開規則 (ADR) をフィルター処理して、Itanium や ARM64 などのアーキテクチャを除外できるようになりました。 自動展開規則の作成ウィザードの **[ソフトウェア更新プログラム]** ページで、**[アーキテクチャ]** プロパティ フィルターを利用できるようになりました。 

詳細については、「[ソフトウェア更新プログラムの自動展開](/sccm/sum/deploy-use/automatically-deploy-software-updates)」を参照してください。


### <a name="improved-wsus-maintenance"></a>向上した WSUS メンテナンス 
<!--1357898--> WSUS クリーンアップ ウィザードでは、ソフトウェアの更新ポイントのコンポーネント プロパティで定義されている置き換えの規則に従って、有効期限が切れている更新プログラムを今すぐ拒否します。 

詳細については、「[ソフトウェア更新プログラムのメンテナンス](/sccm/sum/deploy-use/software-updates-maintenance)」を参照してください。



## <a name="reporting"></a>レポート

### <a name="new-software-updates-compliance-report"></a>新しいソフトウェア更新プログラムのコンプライアンス レポート
<!--1357775--> ソフトウェア更新プログラムのコンプライアンス レポートの従来の表示には、最近サイトに接続していないクライアントからのデータが含まれていました。 新しいレポート「**コンプライアンス 9 - 全体的な正常性とコンプライアンス**」では、特定のソフトウェア更新プログラム グループのコンプライアンス結果を、"正常な" クライアントでフィルター処理できます。 このレポートでは、環境内のアクティブなクライアントの、より現実的なコンプライアンスの状態が表示されます。 

詳細については、「[ソフトウェア更新プログラムのレポート](/sccm/sum/deploy-use/monitor-software-updates#BKMK_SUReports)」を参照してください。



## <a name="inventory"></a>インベントリ

### <a name="bkmk_bigint"></a> 大きな整数値でのハードウェア インベントリの機能強化
<!--1357880--> ハードウェア インベントリには以前、4,294,967,296 (2^32) を超える整数値に対して制限がありました。 この制限は、バイト単位のハード ドライブ サイズなどの属性も対象になる場合があります。 管理ポイントはこの制限を超える整数値を処理せず、そのため、値がデータベースに格納されませんでした。 このリリースでは、制限が 18,446,744,073,709,551,616 (2^64) に引き上げられました。 

詳細については、「[Use of large integer values](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory#bkmk_bigint)」(大きな整数値の使用) を参照してください。


### <a name="hardware-inventory-default-unit-revision"></a>ハードウェア インベントリの既定の単位のリビジョン
<!--514442--> [Configuration Manager バージョン 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#site-infrastructure) では、多くのレポート ビューで使用される既定の単位が、メガバイト (MB) からギガバイト (GB) に変更されました。 [より大きな整数値のハードウェア インベントリの機能強化](#bkmk_bigint)により、また、お客様からのフィードバックに基づき、この既定の単位が再度 MB になりました。



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Configuration Manager コンソール

### <a name="product-lifecycle-dashboard"></a>製品ライフサイクル ダッシュボード
<!--1319632--> 製品ライフサイクル ダッシュボードには、Configuration Manager で管理されているデバイスにインストールされている Microsoft 製品の Microsoft ライフサイクル ポリシーの状態が表示されます。 環境内にある Microsoft 製品についての情報、サポート可能性の状態、およびサポート終了日も提供されます。 このダッシュボードを使って、各製品のサポートを利用できるかどうかを理解することができます。 この情報は、お使いの Microsoft 製品の現在のサポート期限になる前に更新を計画するのに役立ちます。   

詳細については、[製品ライフサイクル ダッシュボード](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard)に関するページを参照してください。


### <a name="copy-asset-details-from-monitoring-views"></a>監視ビューから資産の詳細をコピーする
<!--1357856--> **監視**ワークスペースの次の領域では、テキストをコピーできます。  

- **[展開]** ノードで展開を選択し、**[状態の表示]** をクリックします。 展開状態ビューの **[資産の詳細]** ウィンドウで、1 つまたは複数のデバイスを選択します。  

- **[配布ステータス]** ノードを展開し、**[コンテンツのステータス]** を選択します。 ソフトウェアを選択し、**[状態の表示]** をクリックします。 コンテンツ状態ビューの **[資産の詳細]** ウィンドウで、1 つまたは複数の配布ポイントを選択します。 

資産を右クリックし、**[コピー]** を選択します。 このアクションにより、詳細をすべて含む選択した資産がコンマ区切りリストとしてコピーされます。 これらのビューでは、キーボード ショートカット **Ctrl** + **C** も動作します。 

詳細については、「[バージョン 1806 のコンソールの機能強化](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806)」を参照してください。


### <a name="improvements-to-the-surface-dashboard"></a>Surface ダッシュボードの改善
<!--1358654--> このリリースでは、Surface ダッシュボードが次の点で改善されています。  

- Surface ダッシュボードに、グラフ特定のグラフ セクションが選択されたときに関連するデバイスのリストが表示されるようになりました。  

   - **[Surface デバイスの割合]** タイルをクリックすると、Surface デバイスのリストが開きます。  

   - **[上位 5 つのファームウェアのバージョン]** タイルのバーをクリックすると、その特定のファームウェアのバージョンを示す Surface デバイスのリストが開きます。  

- Surface ダッシュボードからこれらのデバイス リストを表示しているとき、デバイスを右クリックして一般的な操作を実行します。  

詳細については、[Surface ダッシュボード](/sccm/core/clients/manage/surface-device-dashboard)に関するページを参照してください。


### <a name="view-the-currently-signed-on-user-for-a-device"></a>デバイスに現在サインオンしているユーザーを表示する
<!--1358202--> 既定で、**[資産とコンプライアンス]** ワークスペースの **[デバイス]** ノードに **[現在ログオンしているユーザー]** の列が表示されるようになりました。 コレクション固有デバイス リストに対しても表示されます。 この値は、現在の[クライアント ステータス](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus)を示します。 ユーザーがサインオフすると、クライアントによりこの値が消去されます。 サインオンしているユーザーがいない場合、値は空白になります。 

詳細については、「[バージョン 1806 のコンソールの機能強化](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806)」を参照してください。


### <a name="submit-feedback-from-the-configuration-manager-console"></a>Configuration Manager コンソールからフィードバックを送信する  
<!--1357542-->

[気に入った機能の報告] を使ってみましょう。 Configuration Manager チームに使用感を直接伝えることができるようになりました。 フィードバックは、Configuration Manager コンソールから簡単に送信できます。 称賛、問題、提案など、あらゆるフィードバックを歓迎します。 Configuration Manager コンソールで、リボンの右上にあるスマイル ボタンをクリックします。 このフィードバックは、Configuration Manager の Microsoft 製品チームに直接送られます。 Windows 10 フィードバック ハブも使用できますが、コンソール内のフィードバック機能を使用することをお勧めします。  

詳細については、「[バージョン 1806 のコンソールの機能強化](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806)」と[製品フィードバック](/sccm/core/understand/find-help#BKMK_1806Feedback)に関するページを参照してください。



## <a name="next-steps"></a>次のステップ

このバージョンをインストールする準備ができたら、[Configuration Manager の更新プログラムのインストール](/sccm/core/servers/manage/updates)に関するページを参照してください。

> [!TIP]  
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用します。  
>
>  詳細については、下記のリンクをクリックしてください。    
>   - [新しいサイトのインストール](/sccm/core/servers/deploy/install/installing-sites)  
>   - [基準バージョンと更新プログラムのバージョン](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

既知の重大な問題については、[リリース ノート](/sccm/core/servers/deploy/install/release-notes)を参照してください。