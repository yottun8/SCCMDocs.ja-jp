---
title: "ハードウェア インベントリの表示 | リソース エクスプローラー | System Center Configuration Manager"
description: "System Center Configuration Manager でリソース エクスプローラーを使用してハードウェア インベントリを表示します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 12bf49b6a68d277c7f505ddfe37556363d0e3e53


---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager でリソース エクスプローラーを使用してハードウェア インベントリを表示する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のリソース エクスプローラーを使用して、階層内のクライアントから収集されたハードウェア インベントリに関する情報を表示します。  

> [!NOTE]  
>  リソース エクスプローラーでは、接続するクライアントでハードウェア インベントリ サイクルが実行されるまで、インベントリ データは表示されません。  

 Configuration Manager のリソース エクスプローラーには、ハードウェア インベントリに関連する次のセクションがあります。  

-   **[ハードウェア]** - 指定した Configuration Manager クライアント デバイスから収集された、最新のハードウェア インベントリが含まれます。 インベントリ項目 [ワークステーションのステータス] を確認して、デバイスがハードウェア インベントリを実行した日付と時刻を検出できます。 ****  

-   **[ハードウェア履歴]** – 前回ハードウェア インベントリが実行されてから変更されたインベントリ項目の履歴が含まれます。 一覧の各項目には、**[現在]** ノードと、1 つ以上の *<日付\>* ノードが含まれます。 現在のノードの情報と、履歴ノードの 1 つを比較して、クライアント コンピューターのハードウェア インベントリで変更された項目を見つけることができます。  

    > [!NOTE]  
    >  Configuration Manager では、**[期限切れのインベントリ履歴の削除]** サイト メンテナンス タスクで、サイトに対して指定されている日数だけ、インベントリの履歴が保持されます。  

> [!NOTE]  
>  Linux および UNIX を実行しているクライアントからハードウェア インベントリを表示する方法については、「 [How to monitor clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md)」を参照してください。  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Configuration Manager コンソールからリソース エクスプローラーを実行する方法  

1.  Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。  

2.  [資産とコンプライアンス **** ] ワークスペースで [デバイス **** ] をクリックするか、デバイスを表示するコレクションを開きます。  

3.  表示するインベントリが含まれているコンピューターをクリックしたら、[ホーム **** ] タブの [デバイス **** ] グループで [開始 **** ] をクリックし、[リソース エクスプローラー ****] をクリックします。 [リソース エクスプローラー **** ] ウィンドウが開きます。  

4.  **[リソース エクスプローラー]** ウィンドウの右ウィンドウの項目を右クリックし、**[プロパティ]** をクリックして、*[<項目名\>*** のプロパティ]** ダイアログ ボックスを開くことができます。このダイアログ ボックスには、収集されたインベントリ情報を、より読みやすい形式で表示できます。  

5.  終了したら、[リソース エクスプローラー **** ] ウィンドウを閉じます。  



<!--HONumber=Nov16_HO1-->


