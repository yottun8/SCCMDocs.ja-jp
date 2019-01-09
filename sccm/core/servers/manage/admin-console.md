---
title: Configuration Manager コンソール
titleSuffix: Configuration Manager
description: Configuration Manager コンソールでの移動について学習します。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 16b56d59e1cba6a36f0bd8189587794a680c3865
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422880"
---
# <a name="using-the-configuration-manager-console"></a>Configuration Manager コンソールの使用

*適用対象:System Center Configuration Manager (Current Branch)*

管理者は Configuration Manager コンソールを利用し、Configuration Manager 環境を管理します。 この記事では、コンソールを移動するときの基礎について説明します。  



## <a name="connect-to-a-site-server"></a>サイト サーバーに接続する

コンソールは、中央管理サイトまたはプライマリ サイト サーバーに接続されます。 Configuration Manager コンソールをセカンダリ サイトに接続することはできません。 [Configuration Manager コンソールをインストール](/sccm/core/servers/deploy/install/install-consoles)できます。 インストール時、コンソールが接続するサイト サーバーの完全修飾ドメイン名 (FQDN) を指定しました。 

別のサイト サーバーに接続するには、次の手順を実行します。 

1. [リボン](#ribbon)上部の矢印をクリックし、**[新しいサイトに接続]** を選択します。  

    ![コンソールを新しいサイトに接続する](media/connect-to-a-new-site.png)  

2. サイト サーバーの FQDN を入力します。 サイト サーバーに以前接続したことがある場合は、ドロップダウン リストからサーバーを選択します。  

    ![[サイトの接続] ウィンドウで、サイト サーバーの FQDN を入力する](media/site-server-fqdn.png)  

3. **[接続]** を選択します。  


バージョン 1810 以降では、Configuration Manager サイトにアクセスする管理者の最低限の認証レベルを指定することができます。 この機能では、Windows にサインインする管理者には必要なレベルを持つことが強制されます。 詳細については、「[SMS プロバイダーの計画](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth)」を参照してください。 <!--1357013-->  



## <a name="navigation"></a>ナビゲーション

割り当てられているセキュリティ ロールによっては、コンソールの一部の領域が表示されない場合があります。 ロールの詳細については、[ロール ベース管理の基礎](/sccm/core/understand/fundamentals-of-role-based-administration)に関するページを参照してください。 


### <a name="workspaces"></a>ワークスペース

Configuration Manager コンソールには、**ワークスペース**が 4 つあります。  

- **資産とコンプライアンス**  

- **ソフトウェア ライブラリ**  

- **監視**  

- **管理**  

![Configuration Manager のワークスペースとコンテキスト メニュー](media/configuration-manager-workspaces.png)  

下向き矢印を選択し、**[ナビゲーション ペイン オプション]** を選択して、ワークスペースのボタンの順序を再変更します。 **[上へ移動]** または **[下へ移動]** する項目を選択します。 **[リセット]** を選択して、ボタンを既定の順序に戻します。  

 ![ワークスペースの順序を変更する [ナビゲーション ペイン オプション] ウィンドウ](media/navigation-pane-options.png)  

**[表示するボタンを減らす]** を選択して、ワークスペースのボタンを最小化します。 リストの最後のワークスペースが最初に最小化されます。 最小化されたボタンを選択して、**[表示するボタンを増やす]** を選択すると、ボタンは元のサイズに戻ります。   

![Configuration Manager コンソール内で最小化されたワークスペース](media/workspace-buttons.png)  


### <a name="nodes"></a>ノード

ワークスペースとは、**ノード**のコレクションです。 ノードの一例として、**ソフトウェア ライブラリ** ワークスペースの**ソフトウェア更新プログラム グループ** ノードがあります。 

そのノードに移動したら、矢印を選択してナビゲーション ウィンドウを最小化できます。  

![ノードの例と強調表示された最小化矢印](media/software-update-groups-node.png)  

ナビゲーション ウィンドウを最小化した場合は、**ナビゲーション バー**を使用してコンソール内を移動します。  

![Configuration Manager の最小化されているナビゲーション ウィンドウ](media/minimized-navigation-pane.png)  

コンソールで、ノードはフォルダーに分類される場合があります。 フォルダーを直接クリックすると、通常は**機能一覧**または**ダッシュボード**に移動します。  

![Configuration Manager のソフトウェア更新プログラムの機能一覧](media/software-updates-navigation-index.png)  


### <a name="ribbon"></a>リボン 

リボンは、Configuration Manager コンソールの上部にあります。 リボンにはタブが 1 つ以上あり、右の矢印を使用して最小化することができます。 リボンのボタンは、ノードによって変わります。 リボンのほとんどのボタンは、コンテキスト メニューでも使用することができます。  

![複数のタブと最小化矢印が強調表示されたリボンの例](media/ribbon.png)   


### <a name="details-pane"></a>詳細ウィンドウ

項目の追加情報は、詳細ウィンドウで確認できます。 詳細ウィンドウには、タブが 1 つ以上あります。 このタブはノードによって異なります。  

![Configuration Manager の詳細ウィンドウの例](media/details-pane.png)   


### <a name="columns"></a>列 

列は、追加、削除、順序変更、サイズ変更することができます。 これらのアクションでは、お好みのデータを表示することができます。 使用できる列はノードによって異なります。 ビューに列を追加またはビューから列を削除するには、既存の列見出しを右クリックし、項目を選択します。 お好きな場所に列見出しをドラッグし、列を並べ替えます。  

![Configuration Managers での列の追加](media/add-columns.png)  

列のコンテキスト メニューの下部で、列を並べ替えたりグループ化できます。 また、列の見出しを選択して並べ替えることもできます。  

![Configuration Manager での列でグループ化](media/column-group-by.png)  



## <a name="command-line-options"></a>コマンド ライン オプション

Configuration Manager コンソールには次のコマンド ライン オプションがあります。

|オプション|説明|  
|------------|-----------------|  
|`/sms:debugview=1`|ビューが指定されているすべての ResultView に DebugView を含めます。 DebugView では、生のプロパティ (名前と値) が示されます。|  
|`/sms:NamespaceView=1`|コンソールに名前空間ビューを表示します。|  
|`/sms:ResetSettings`|コンソールでは、ユーザーの永続的な接続状態とビューの状態は無視されます。 ウィンドウのサイズはリセットされません。|  
|`/sms:IgnoreExtensions`|Configuration Manager のすべての拡張機能を無効にします。|  
|`/sms:NoRestore`|コンソールでは、前に永続化されていたノードのナビゲーションは無視されます。|  



## <a name="tips"></a>ヒント

### <a name="send-feedback"></a>フィードバックを送信する
<!--1357542-->

バージョン 1806 からは、コンソールから製品に関するフィードバックを送信します。  

- **気に入った機能の報告**:気に入ったもののフィードバックを送信します  

- **問題点、改善点の報告**:気に入らなかったもののフィードバックを送信します  

- **提案の送信**:アイデアを共有するために UserVoice に移動します  
 
詳細については、「[製品に関するフィードバック](/sccm/core/understand/find-help#BKMK_1806Feedback)」を参照してください。


### <a name="assets-and-compliance-workspace"></a>資産とコンプライアンス ワークスペース

#### <a name="view-users-for-a-device"></a>デバイスのユーザーの表示
バージョン 1806 からは、**デバイス** ノードで次の列が使用できます。  

- **プライマリ ユーザー** <!--1357280-->  

- **現在ログオンしているユーザー** <!--1358202-->  

既定以外の列を表示する方法については、「[列](#columns)」を参照してください。


### <a name="monitoring-workspace"></a>監視ワークスペース

#### <a name="copy-details-in-monitoring-views"></a>監視ビューで詳細をコピーする
<!--1357856--> バージョン 1806 以降では、次の監視ノードの **[資産の詳細]** ウィンドウから情報をコピーできます。  

- **コンテンツ配布の状態**  

- **展開の状態**  

![[展開の状態] ビュー、資産の詳細をコピー](media/1810-deployment-status.PNG)



## <a name="next-steps"></a>次のステップ

[ユーザー補助機能](/sccm/core/understand/accessibility-features)

