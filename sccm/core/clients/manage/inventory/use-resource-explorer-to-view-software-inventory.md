---
title: "ソフトウェア インベントリを表示する | Microsoft Docs | リソース エクスプローラー"
description: "System Center Configuration Manager でリソース エクスプローラーを使用してソフトウェア インベントリを表示します。"
ms.custom: na
ms.date: 12/26/2016
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
ms.sourcegitcommit: 9206b82eca02877c30eebf146d42bcca7290eb42
ms.openlocfilehash: 6189726bbcade8229e0b2e929ebedeefdbf266a4


---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager でリソース エクスプローラーを使用してソフトウェア インベントリを表示する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のリソース エクスプローラーを使用して、階層内のコンピューターから収集されたソフトウェア インベントリに関する情報を表示します。  

> [!NOTE]  
>  クライアントでソフトウェア インベントリ サイクルが実行されるまで、リソース エクスプローラーにインベントリ データは表示されません。  

 リソース エクスプローラーは、次のソフトウェアのインベントリ情報を提供します。  

-   **ソフトウェア**:  

    -   **[収集するファイル]** – ソフトウェア インベントリ中に収集されたファイル。  

    -   **[ファイルの詳細]** – ソフトウェア インベントリ中にインベントリされた、特定の製品または製造元に関連付けられていないファイル。  

    -   **[最後のソフトウェア スキャン]** – クライアント コンピューターの最後のソフトウェア インベントリとファイル コレクションの日付と時刻。  

    -   **[製品の詳細]** – ソフトウェア インベントリでインベントリされ、製造元別にグループ化されたソフトウェア製品の情報。  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Configuration Manager コンソールからリソース エクスプローラーを実行するには  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** を選択します。

2.  **[資産とコンプライアンス]** ワークスペースで **[デバイス]** を選択するか、デバイスを表示するコレクションを開きます。  

3.  表示するインベントリが含まれているコンピューターをクリックしたら、**[ホーム]** タブの **[デバイス]** グループで **[開始]** > **[リソース エクスプローラー ]** の順に選択します。

4.  [リソース エクスプローラー] の右ペインで、項目のどれかを右クリックしてから、**[プロパティ]** を選択すると、より読みやすい形式で、収集されたインベントリ情報が表示されます。  
 



<!--HONumber=Dec16_HO5-->


