---
title: "ソフトウェア インベントリの表示 | リソース エクスプローラー | System Center Configuration Manager"
description: "System Center Configuration Manager でリソース エクスプローラーを使用してソフトウェア インベントリを表示します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b4ecb27cfb119ae80d1ed7d90d84c61a87b183c8


---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager でリソース エクスプローラーを使用してソフトウェア インベントリを表示する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のリソース エクスプローラーを使用して、階層内のコンピューターから収集されたソフトウェア インベントリに関する情報を表示します。  

> [!NOTE]  
>  接続先のクライアントでソフトウェア インベントリ サイクルが実行されるまで、リソース エクスプローラーにインベントリ データは表示されません。  

 Configuration Manager のリソース エクスプローラーには、ソフトウェア インベントリに関連する次のセクションがあります。  

-   **[ソフトウェア]** - リソース エクスプローラーのソフトウェア セクションには、次の 4 つのセクションがあります。  

    -   **[収集するファイル]** – ソフトウェア インベントリ中に収集されたファイルに関する情報が表示されます。  

    -   **[ファイルの詳細]** – ソフトウェア インベントリ中にインベントリされた、特定の製品または製造元に関連付けられていないファイルに関する情報が収集されます。  

    -   **[最後のソフトウェア スキャン]** – クライアント コンピューターで実行された最後のソフトウェア インベントリとファイル コレクションの日付と時刻が表示されます。  

    -   **[製品の詳細]** – ソフトウェア インベントリでインベントリされたソフトウェア製品の情報が、製造元別にグループ化されて表示されます。  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Configuration Manager コンソールからリソース エクスプローラーを実行するには  
 Configuration Manager のリソース エクスプローラーを実行するには、次の手順に従います。  

#### <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Configuration Manager コンソールからリソース エクスプローラーを実行するには  

1.  Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。  

2.  [資産とコンプライアンス **** ] ワークスペースで [デバイス **** ] をクリックするか、デバイスを表示するコレクションを開きます。  

3.  表示するインベントリが含まれているコンピューターをクリックしたら、[ホーム **** ] タブの [デバイス **** ] グループで [開始 **** ] をクリックし、[リソース エクスプローラー ****] をクリックします。 [リソース エクスプローラー **** ] ウィンドウが開きます。  

4.  [リソース エクスプローラー] ウィンドウの右ウィンドウの項目を右クリックし、[**プロパティ**] をクリックして、[*<項目名\>*** のプロパティ**] ダイアログ ボックスを開くことができます。このダイアログ ボックスには、収集されたインベントリ情報を、より読みやすい形式で表示できます。  

5.  終了したら、[リソース エクスプローラー **** ] ウィンドウを閉じます。  



<!--HONumber=Nov16_HO1-->


