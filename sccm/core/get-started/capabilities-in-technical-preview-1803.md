---
title: Technical Preview 1803
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview バージョン 1803 で利用できる新しい機能について説明します。
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 672257141c0672a76b89ee9d78184d2a4230280f
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898360"
---
# <a name="capabilities-in-technical-preview-1803-for-system-center-configuration-manager"></a>System Center Configuration Manager の Technical Preview 1803 の機能

「オブジェクトの*適用対象: System Center Configuration Manager (Technical Preview)*

この記事では、Configuration Manager の Technical Preview バージョン 1803 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Technical Preview サイトに追加できます。 

この更新プログラムをインストールする前に、[Technical Preview](/sccm/core/get-started/technical-preview) に関する記事を確認してください。 この記事により、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、フィードバックを提供する方法についての理解を深めることができます。     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**このバージョンでお試しいただける新機能を次に示します。**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>ソースとしてのクラウド配布ポイントのプル配布ポイントのサポート  
<!--1321554--> 多くのお客様がリモート オフィスまたは支社で[プル配布ポイント](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)を使用して、WAN 全体でソース配布ポイントからコンテンツをダウンロードします。 リモート オフィスでより良好なインターネット接続を確保したい場合、あるいは WAN リンクへの負荷を減らすために、Microsoft Azure でソースとして[クラウド配布ポイント](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)を使用できるようになりました。 配布ポイント プロパティの **[プル配布ポイント]** タブでソースを追加する場合に、サイトのクラウド配布ポイントが利用可能な配布ポイントとしてリストされるようになりました。 それ以外の場合、両方のサイト システムの役割の動作は変わりません。 

### <a name="prerequisites"></a>[前提条件]
- プル配布ポイントは、Microsoft Azure と通信するためにインターネットにアクセスする必要があります。
- コンテンツは、ソース クラウドの配布ポイントに配布する必要があります。

> [!Note]  
> この機能では、データ ストレージおよびネットワーク送信の Azure サブスクリプションへの課金が発生します。 詳細については、「[クラウドベースの配布にかかるコスト](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#BKMK_CloudDPCost)」を参照してください。



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>WAN の使用率を減らすためのクライアント ピア キャッシュでの部分的なダウンロードのサポート
<!--1357346--> クライアント ピア キャッシュ ソースのコンテンツを分割できるようになりました。 これにより、ネットワーク転送が最小限に抑えられ、WAN の使用率が減ります。 管理ポイントでは、コンテンツの各パートをより詳細に追跡することができます。 境界グループごとに同じ内容が複数回ダウンロードされないようにします。 

### <a name="example-scenario"></a>シナリオ例
Contoso には、本社 (HQ) および支社という 2 つの境界グループを持つ 1 つのプライマリ サイトがあります。 2 つの境界グループ間には 30 分のフォールバック リレーションシップがあります。 サイトの管理ポイントと配布ポイントは HQ 境界にのみ存在します。 支社の場所にはローカル配布ポイントはありません。 支社の 4 つのクライアントのうち 2 つは、ピア キャッシュ ソースとして構成されています。 

![シナリオ例で説明されているネットワーク構成の図](media/1357346-peer-cache-source-parts.png)

1. 支社の 4 つのすべてのクライアントを、コンテンツを含む展開の対象とします。 コンテンツは配布ポイントにのみ配布されています。
2. Client3 と Client4 には、展開するローカル ソースはありません。 管理ポイントは、リモート境界グループにフォールバックするまでクライアントに 30 分待機するよう指示します。
3. Client1 (PCS1) は、管理ポイントでポリシーを更新する最初のピア キャッシュ ソースです。 このクライアントがピア キャッシュ ソースとして有効になっているため、管理ポイントは、配布ポイントからパート A のダウンロードをすぐに開始するように指示します。  
4. Client2 (PCS2) が管理ポイントに接続するときに、パート A は既に進行中ですが、まだ完了していないため、管理ポイントは、配布ポイントからパート B のダウンロードをすぐに開始するように指示します。
5. PCS1 はパート A のダウンロードを終了し、すぐに管理ポイントに通知します。 パート B は既に進行中ですが、まだ完了していないため、管理ポイントは、配布ポイントからパート C のダウンロードを開始するように指示します。
6. PCS2 はパート B のダウンロードを終了し、すぐに管理ポイントに通知します。 管理ポイントは、配布ポイントからパート D のダウンロードを開始するように指示します。 
7. PCS1 はパート C のダウンロードを終了し、すぐに管理ポイントに通知します。 管理ポイントは、リモート配布ポイントから利用可能なパートがなくなったことを通知します。 管理ポイントは、ローカル ピア PCS2 からパート B をダウンロードするように指示します。
8. このプロセスは、両方のクライアント ピア キャッシュ ソースが互いにすべてのパートを取得するまで続きます。 管理ポイントは、ピア キャッシュ ソースにローカル ピアからパートをダウンロードするよう指示する前に、リモート配布ポイントからのパートに優先順位を付けます。 
9. Client3 は、30 分のフォールバック期間が過ぎた後、ポリシーを更新する最初のクライアントです。 ここで管理ポイントをもう一度確認し、クライアントに新しいローカル ソースを通知します。 WAN 経由で配布ポイントからコンテンツをすべてダウンロードするのではなく、クライアントのいずれかのピア キャッシュ ソースからコンテンツをすべてダウンロードします。 クライアントはローカル ピア ソースに優先順位を付けます。 

> [!Note]  
> クライアントのピア キャッシュ ソースの数がコンテンツ パートの数より大きい場合、管理ポイントは通常のクライアントのようにフォールバックを待機するよう追加のピア キャッシュ ソースに指示します。 


### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 その後、**[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。

1. 通常どおり、[境界グループ](/sccm/core/servers/deploy/configure/boundary-groups)と[ピア キャッシュ ソース](/sccm/core/plan-design/hierarchy/client-peer-cache)をセットアップします。
2. Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[サイトの構成]** を展開して **[サイト]** を選択します。 リボンの **[階層設定]** をクリックします。 
3. **[全般]** タブで、**コンテンツを分割するようクライアントのピア キャッシュ ソースを構成する**オプションを有効にします。 
4. コンテンツを含む必要な展開を作成します。  

   > [!Note]  
   > この機能は、必要な展開などを含め、クライアントがバックグラウンドでコンテンツをダウンロードする場合にのみ動作します。 ユーザーがソフトウェア センターで利用可能な展開をインストールする場合など、オンデマンド ダウンロードは、通常どおり動作します。  

1. コンテンツの分割ダウンロードの処理を確認するには、クライアントのピア キャッシュ ソースの **ContentTransferManager.log** と、管理ポイントの **MP_Location.log** を調べます。  
 



## <a name="maintenance-windows-in-software-center"></a>ソフトウェア センターのメンテナンス期間
<!--1358131--> ソフトウェア センターでは、次のスケジュールされたメンテナンス期間が表示されるようになりました。 [インストールのステータス] タブで、[すべて] のビューを [今後のタスク] に切り替えます。 ここには、スケジュールされている展開のリストと時間の範囲が表示されます。 今後のメンテナンス期間がない場合、リストは空白です。 

![[インストールのステータス] タブに今後の展開のリストが示されているソフトウェア センター](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>ソフトウェア センターの Web ページのカスタム タブ
<!--1358132--> カスタマイズされたタブを作成して、ソフトウェア センターで Web ページを開けるようになりました。 この機能では、一貫性のある信頼性の高い方法で、エンドユーザーにコンテンツを表示することができます。 以下のリストには例がいくつか含まれています。
- IT に連絡: 組織の IT 部門に連絡する方法に関する情報
- IT サポート センター: サポート技術情報を検索する、サポート チケットを開くなどの IT セルフ サービス アクション。
- エンドユーザー文書: アプリケーションの使用や Windows 10 へのアップグレードなど、さまざまな IT トピックに関する組織内のユーザー向けの記事。


### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 その後、**[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。

1. Configuration Manager コンソールの **[管理]** ワークスペースの **[クライアント設定]** ノードで、**[既定のクライアント設定]** ポリシーを開きます。
2. **[ソフトウェア センター]** グループを選択します。
3. **[ソフトウェア センターの設定]** では、**[カスタマイズ]** をクリックします。
4. **[タブ]** タブに切り替えます。
5. **ソフトウェア センターのカスタム タブを指定する**オプションを有効にします。
    1. **[タブ名]** テキスト フィールドに名前を入力します。 この名前は、ソフトウェア センターでユーザーに表示されるものです。
    2. **[コンテンツ URL]** テキスト フィールドに有効な URL を入力します。 この URL は、ユーザーがこのタブをクリックしたときにソフトウェア センターで表示されるコンテンツです。

> [!Tip]  
> ソフトウェア センターでは Internet Explorer コンポーネントを使用して、Web ページをレンダリングします。

## <a name="enable-third-party-software-update-support-on-clients"></a>クライアントでサード パーティ製ソフトウェア更新プログラムを有効にするサポート

サード パーティ製ソフトウェア更新プログラムについて、Configuration Manager クライアントの構成を有効にできるようになりました。 SUP コンポーネント プロパティで**サードパーティ製ソフトウェア更新プログラムを有効にする**と、SUP は、サードパーティの更新プログラムの WSUS で使用される署名証明書をダウンロードします。 <!--1357605-->

クライアント設定で **[Enable third party software updates]\(サードパーティ製ソフトウェア更新プログラムを有効にする\)** を選択すると、以下のようになります。 
- クライアントで、[イントラネットの Microsoft 更新サービスの保存場所にある署名済み更新を許可する] のポリシーが設定されます。 
- クライアントの信頼できる発行元ストアに署名証明書がインストールされます。 

### <a name="try-it-out"></a>試してみましょう。
 タスクを実行してみます。 その後、**[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。

1. Configuration Manager 階層の最上位サイトで、**[管理]** ノードに移動して、**[サイトの構成]**、**[サイト]** の順に展開します。
2. 最上位サイト サーバーを右クリックし、**[サイト コンポーネントの構成]**、**[ソフトウェアの更新ポイント]** の順に選択します。
3. **[サードパーティの更新プログラム]** タブをクリックして、**[Enable third party software updates]\(サードパーティ製ソフトウェア更新プログラムを有効にする\)** をオンにします。
4. **[クライアントの設定]** を開き、**ソフトウェア更新プログラム**の設定に移動します。
5. **[Enable third party software updates]\(サードパーティ製ソフトウェア更新プログラムを有効にする\)** が **[はい]** に設定されていることを確認します。

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>監視ビューからの資産の詳細のコピー/貼り付けを有効にする
[皆さまからのフィードバック](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det)を反映し、展開および配布ステータス監視ビューの資産の詳細ウィンドウでコピー/貼り付け機能を有効にできるようになりました。  <!--1357552-->

## <a name="scap-extensions"></a>SCAP 拡張機能
プレリリース版の SCAP 拡張機能は、SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi の Cd.latest フォルダーにあります。 プレリリース版の SCAP 拡張機能は、現在サポートされているバージョンの Configuration Manager Current Branch と LTSB 1606 にインストールできます。 詳細については、「[About the Security Content Automation Protocol (SCAP) extensions](/sccm/compliance/plan-design/scap/about-scap)」(Security Content Automation Protocol (SCAP) 拡張機能について) を参照してください。



## <a name="next-steps"></a>次のステップ
Technical Preview ブランチのインストールまたは更新については、「[System Center Configuration Manager の Technical Preview](/sccm/core/get-started/technical-preview)」をご覧ください。    
