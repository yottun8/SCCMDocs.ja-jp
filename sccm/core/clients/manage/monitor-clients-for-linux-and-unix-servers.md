---
title: "クライアントを監視する | Linux UNIX |System Center Configuration Manager"
description: "System Center Configuration Manager で Linux および UNIX サーバーのクライアントを監視します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 707cb13bcb62848eb42ca824137a645dfd2f9d82


---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>System Center Configuration Manager で Linux および UNIX サーバーのクライアントを監視する方法

*適用対象: System Center Configuration Manager (Current Branch)*

Windows ベースのクライアントからの情報を表示する場合と同じ方法を使用して、Linux および UNIX サーバーからの情報を System Center Configuration Manager コンソールで表示できます。  

 表示できる情報は次のとおりです。  

-   クライアントからの状態の詳細 (Configuration Manager コンソール ダッシュボード)  

-   クライアントについての詳細 (既定の Configuration Manager レポート)  

-   インベントリの詳細 (リソース エクスプローラー)  

 次のセクションでは、Linux および UNIX サーバーに関する詳細をリソース エクスプローラーとレポートを使用して表示する方法を説明します。  

##  <a name="a-namebkmkuseresourceexpforlnua-how-to-use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a> リソース エクスプローラーを使用して Linux および UNIX サーバーのインベントリを表示する方法  
 リソース エクスプローラーを使用して、Linux および UNIX サーバー上のハードウェア、およびインストールされているソフトウェアの詳細を表示できます。  

 Configuration Manager クライアントがハードウェア インベントリを Configuration Manager サイトに送信した後、リソース エクスプローラーを使用してこの情報を表示できます。 Linux および UNIX の Configuration Manager クライアントでは、インベントリの新しいクラスやビューをリソース エクスプローラーに追加しません。 Linux および UNIX のインベントリ データは、既存の WMI クラスにマップされます。 リソース エクスプローラーを使用して、Windows ベースの分類で Linux および UNIX サーバーのインベントリの詳細を表示できます。  

 たとえば、Linux および UNIX サーバーにある、ネイティブにインストールされているプログラムすべての一覧を収集できます。 ネイティブにインストールされているプログラムの例として、Linux の **.rpms** または Solaris の **.pkgs** があります。 インベントリが Linux または UNIX クライアントによって送信された後、ネイティブにインストールされている Linux または UNIX のすべてのプログラムの一覧は、Configuration Manager コンソールのリソース エクスプローラーで表示できます。  

 リソース エクスプローラーを使用する方法については、「[System Center Configuration Manager でリソース エクスプローラーを使用してハードウェア インベントリを表示する方法](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)」を参照してください。  

##  <a name="a-namebkmkusereportsforlnua-how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> レポートを使用して Linux および UNIX サーバーの情報を表示する方法  
 Configuration Manager のレポートには、Windows ベースのコンピューターからの情報と共に、Linux および UNIX サーバーからの情報が含まれています。 Linux および UNIX のデータをレポートに統合するために、追加の構成は必要ありません。  

 たとえば、オペレーティング システム バージョンのカウントという名前のレポートを実行すると、さまざまなオペレーティング システムと各オペレーティング システムを実行しているクライアントの数の一覧が表示されます。 レポートは、さまざまなオペレーティング システムで実行されている各 Configuration Manager クライアントから送信されたハードウェア インベントリ情報に基づいています。  

 Linux および UNIX サーバーのデータに固有のカスタム レポートを作成することもできます。 ハードウェア インベントリ クラス **[オペレーティング システム]** の **[キャプション]** プロパティは、レポート クエリで特定のオペレーティング システムを識別するために使用できる便利な属性です。  

 Configuration Manager でのレポートに関して詳しくは、「[System Center Configuration Manager のレポート](../../../core/servers/manage/reporting.md)」を参照してください。  



<!--HONumber=Nov16_HO1-->


