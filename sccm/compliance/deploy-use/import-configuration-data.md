---
title: "構成データのインポート | Microsoft Docs"
description: "構成データは、キャビネット ファイル形式であり、サポートされている Service Modeling Language スキーマに準拠している場合にインポートできます。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 60d0642618a3074fc50a848f1189f4d6559ca916
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="import-configuration-data-with-system-center-configuration-manager"></a>System Center Configuration Manager で構成データをインポートする

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager コンソールで構成基準と構成項目を作成するほか、構成項目がキャビネット (cab) ファイル形式で、サポートされる Service Modeling Language (SML) スキーマに準拠している場合は、構成データをインポートできます。 構成データのインポート元:  

-   Microsoft または他のソフトウェア ベンダー サイトからダウンロードしたベスト プラクティス構成データ (構成パック)。  

-   System Center 2012 Configuration Manager 以降からエクスポートされた構成データ。  

-   外部で作成され、SML スキーマに従う構成データ。  

 System Center 2012 Configuration Manager サイト サーバーの役割のコンプライアンスを管理するのに役立つ構成パックの例については、 [System Center 2012 Configuration Manager 構成パック](http://www.microsoft.com/en-us/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all)に関するページを参照してください。  

構成基準をインポートするとき、構成基準で参照される一部またはすべての構成項目をキャビネット ファイルにも含める必要がある場合があります。 インポート処理中に、Configuration Manager は、構成基準で参照されるすべての構成項目がキャビネット ファイルにも含まれているかどうかや、既に Configuration Manager に存在するかどうかを確認します。 構成基準のインポートを試みたときに、その構成基準が参照する構成データが見つからない場合は、そのインポート処理は失敗します。  

その他にも、次のようなシナリオでインポート処理が失敗することがあります。  

-   構成データが参照する構成データを、Configuration Manager が自身のデータベースおよびキャビネット ファイル自体から見つけられない。  

-   Configuration Manager データベース内に、同じ名前で同じ構成データ バージョンの構成データが既に存在しているが、コンテンツ バージョンが異なる。  

-   Configuration Manager データベース内に、同じコンテンツ バージョンの構成データが既に存在するが、ハッシュ計算では異なるデータとして識別される。  

-   Configuration Manager データベース内に、同じ名前で新しいバージョンの構成データが既に存在するか、最近削除された。  

-   マルチサイト Configuration Manager 階層で、構成データが最初に親サイトからインポートされた。 その構成データは、子サイトではなく、同じサイトから更新する必要があります。  

### <a name="import-configuration-data"></a>構成データのインポート  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]**、**[構成アイテム]** または **[構成基準]** の順にクリックします。
2.  **[ホーム]** タブの **[作成]** グループで、**[構成データのインポート]** をクリックします。  
3.  **ファイルの選択** のページ、 **構成データのインポート ウィザード**, 、 をクリックして **追加**, 、し、次に、 **開く**  ダイアログ ボックスで、インポートする .cab ファイルを選択します。  
4.  Configuration Manager コンソールでインポートした構成データを編集可能にする場合は、**[インポートする構成項目と構成基準を含む新しいファイルを作成する]** チェックボックスをオンにします。  
5.  **[概要]** ページで、実行される操作を確認し、ウィザードを完了します。  

インポートされた構成データは、**[資産とコンプライアンス]** ワークスペースの **[コンプライアンス設定]** ノードに表示されます。  
