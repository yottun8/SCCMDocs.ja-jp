---
title: Configuration Manager コンソール
titleSuffix: Configuration Manager
description: Configuration Manager コンソールでの移動について学習します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f936cf1c1317940f28691863eafdb4aa883fc1cb
ms.sourcegitcommit: aa91f0d376de03b614b70d5fc513cb384ff58db4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2018
ms.locfileid: "50216916"
---
# <a name="using-the-system-center-configuration-manager-console"></a>System Center Configuration Manager コンソールを使用する

*適用対象: System Center Configuration Manager (Current Branch)*

管理者は System Center Configuration Manager コンソールを利用し、Configuration Manager 環境を管理します。 この記事では、コンソールを移動するときの基礎について説明します。 コンソールの拡張機能は、この記事の下部にバージョンごとに記載しています。 

## <a name="connect-the-console-to-a-site-server"></a>コンソールをサイト サーバーに接続する
コンソールは、中央管理サイトまたはプライマリ サイト サーバーに接続されます。 ただし、Configuration Manager コンソールをセカンダリ サイトに接続することはできません。 必要な場合は、[Configuration Manager コンソールをインストール](../deploy/install/install-consoles.md)します。 インストール時、Configuration Manager コンソールが接続するサイト サーバーの完全修飾ドメイン名 (FQDN) を指定しました。 別のサイト サーバーに接続するには、次の手順を使用します。 

1. リボン上部の矢印をクリックし、**[新しいサイトに接続]** を選択します。
    ![コンソールを新しいサイトに接続する](media/connect-to-a-new-site.png)
2. サイト サーバーの FQDN を入力します。 サイト サーバーに以前接続したことがある場合は、ドロップダウンからサーバーを選択します。  
    ![サイト サーバーの FQDN を入力する](media/site-server-fqdn.png)
3. **[接続]** をクリックします。 

## <a name="navigate-the-console"></a>コンソールで移動する
コンソールの下の一部のオプションは、割り当てられているセキュリティ ロールによっては表示されない場合があります。 ロールの詳細については、[ロール ベース管理の基礎](../../understand/fundamentals-of-role-based-administration.md)に関するページを参照してください。 

### <a name="workspaces"></a>ワークスペース
Configuration Manager コンソールには、**ワークスペース**が 4 つあります。 
   - **資産とコンプライアンス**
   - **ソフトウェア ライブラリ**
   - **監視**
   - **管理**

 ![Configuration Manager のワークスペース](media/configuration-manager-workspaces.png)

下向き矢印をクリックし、**[ナビゲーション ペイン オプション]** を選択して、ワークスペースのボタンの順序を再変更します。 **[上へ移動]** または **[下へ移動]** する項目を選択します。 **[リセット]** をクリックして、ボタンを既定の順序に戻します。 

 ![Configuration Manager のワークスペースの順序を変更する](media/navigation-pane-options.png)

**[表示するボタンを減らす]** を選択して、ワークスペースのボタンを最小化することができます。 ワークスペースの一覧の最後のワークスペースが最初に最小化されます。 最小化されたボタンをクリックして、**[表示するボタンを増やす]** を選択すると、ボタンは元のサイズに戻ります。  

![Configuration Manager のワークスペース](media/workspace-buttons.png)


### <a name="nodes"></a>ノード
ワークスペースとは、**ノード**のコレクションです。 ノードの一例として、**ソフトウェア更新プログラム グループ** ノードがあります。 そのノードに移動したら、矢印をクリックしてナビゲーション ウィンドウを最小化できます。 

![Configuration Manager のワークスペース](media/software-update-groups-node.png)

**ナビゲーション バー**を使用すると、ナビゲーション ウィンドウが最小化されているときにコンソール内を移動できます。 

![Configuration Manager の最小化されているナビゲーション ウィンドウ](media/minimized-navigation-pane.png)

コンソールで、ノードはフォルダーに分類される場合があります。 フォルダーを直接クリックすると、通常は**機能一覧**または**ダッシュボード**に移動します。

![Configuration Manager のソフトウェア更新プログラムの機能一覧](media/software-updates-navigation-index.png)

### <a name="ribbon"></a>リボン 
リボンは、Configuration Manager コンソールの上部にあります。 リボンにはタブが 1 つ以上あり、右の矢印を使用して最小化することができます。 リボンのボタンは、ノードによって変わります。 リボンのほとんどのボタンは、右クリック メニューでも使用することができます。 
 
![Configuration Manager のソフトウェア更新プログラムの機能一覧](media/ribbon.png)

### <a name="details-pane"></a>詳細ウィンドウ
項目の追加情報は、詳細ウィンドウで確認できます。 詳細ウィンドウには、タブが 1 つ以上あります。 このタブはノードによって異なります。 
![Configuration Manager の詳細ウィンドウ](media/details-pane.png)

### <a name="columns"></a>列 
列は、追加、削除、順序変更、サイズ変更することができます。 これらのアクションでは、お好みのデータを表示することができます。 使用できる列はノードによって異なります。 既存の列見出しを右クリックし、項目をクリックして、ビューに追加するか削除します。 お好きな場所に列見出しをドラッグし、列を並べ替えます。 
![Configuration Managers での列の追加](media/add-columns.png)

列の右クリック メニューの下部で、列を並べ替えたりグループ化できます。 また、その見出しをクリックして、列で並べ替えることができます。 

![Configuration Manager での列でグループ化](media/column-group-by.png)

##<a name="console-command-line-options"></a>コンソール コマンド ライン オプション
Microsoft System Center Configuration Manager コンソールには次のコマンド ライン オプションがあります。

|オプション|説明|  
|------------|-----------------|  
|**/sms:debugview=1**|ビューが指定されているすべての ResultView に DebugView を含めます。 DebugView では、生のプロパティ (名前と値) が示されます。|  
|**/sms:NamespaceView=1**|System Center Configuration Manager コンソールに名前空間ビューを表示します。|  
|**/sms:ResetSettings**|System Center Configuration Manager コンソールで、ユーザーの永続的な接続とビューの状態を無視します (Microsoft 管理コンソール ウィンドウのサイズはリセットされません)。|  
|**/sms:IgnoreExtensions**|System Center Configuration Manager のすべての拡張機能を無効にします。|  
|**/sms:NoRestore**|System Center Configuration Manager コンソールで、前に永続化されていたノードのナビゲーションを無視します。|  

## <a name="console-improvements-in-version-1806"></a>バージョン 1806 のコンソールの機能強化
Configuration Manager バージョン 1806 では、コンソールに次の機能強化が追加されています。

- デバイス ノードの列で **[プライマリ ユーザー]** が利用できるようになりました。 <!--1357280-->
- デバイス ノードの列で **[Currently logged on user]\(現在ログオンしているユーザー\)** が利用できるようになりました。<!--1358202-->
- 次の監視のビュー用に、**[資産の詳細]** ウィンドウから情報をコピーできます。<!--1357856-->
    - コンテンツ配布のステータス
    - 展開の状態 

    ![Configuration Manager での資産の詳細のコピー](media/1810-deployment-status.PNG)

 - コンソールからフィードバックを送信します。 インターネットにアクセスできない場合、後で送信するためにコピーを保存しておくことが可能です。 <!--1357542-->
   
    - **Send a smile (気に入った機能の報告)**: 気に入ったもののフィードバックを送信します。
    - **Send a frown (問題点、改善点の報告)**: 気に入らなかったもののフィードバックを送信します。 
    - **Send a suggestion (提案の送信)**: アイデアを共有するために UserVoice に移動します。 
 
       ![Configuration Manager のフィードバックの送信](media/1810-send-a-smile.PNG)
![Configuration Manager のフィードバック フォーム](media/1810-feedback-form.PNG)

## <a name="next-steps"></a>次のステップ
> [!div class="nextstepaction"]
> [ユーザー補助機能](../../understand/accessibility-features.md)

