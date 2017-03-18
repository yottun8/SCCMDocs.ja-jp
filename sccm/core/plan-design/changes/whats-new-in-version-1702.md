---
title: "新しいバージョン 1702 | Microsoft Docs"
description: "System Center Configuration Manager のバージョン 1702 で導入された変更点および新機能について詳しく説明します。"
ms.custom: na
ms.date: 03/27/2017
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: 473ba742bea74cbfdf8cab550244ccd522523718
ms.lasthandoff: 03/04/2017

---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>System Center Configuration Manager のバージョン 1702 の新機能

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の現在のブランチの更新プログラム 1702 は、以前にインストールされておりバージョン 1606 または 1610 を実行しているサイトを対象とする、コンソール内の更新プログラムとして利用可能です。 また、新しい展開をインストールするときに使用する基準のバージョンとしても利用可能です。

> [!TIP]  
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用する必要があります。  
>  詳細については、下記のリンクをクリックしてください。    
>  -   [新しいサイトのインストール](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [サイトで更新プログラムをインストールする](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [基準バージョンと更新プログラムのバージョン](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

次の各セクションでは、Configuration Manager のバージョン 1702 で導入された変更点および新機能について詳しく説明します。  


## <a name="data-warehouse-service-point"></a>データ ウェアハウス サービス ポイント
データ ウェアハウス サービス ポイントを使用して、Configuration Manager 展開の長期的な履歴データを格納およびレポートできるようになりました。

データ ウェアハウスでは、最大 2 TB のデータをサポートし、変更追跡にはタイムスタンプが使用されます。 データの格納は、Configuration Manager サイト データベースからデータ ウェアハウス データベースへの自動化された同期によって達成されます。 この情報には、レポート サービス ポイントからアクセスできます。



詳細については、「[データ ウェアハウス サービス ポイント](/sccm/core/servers/manage/data-warehouse)」を参照してください。

