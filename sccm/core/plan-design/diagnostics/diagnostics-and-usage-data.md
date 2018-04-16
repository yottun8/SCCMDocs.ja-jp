---
title: 診断結果と使用状況データ
titleSuffix: Configuration Manager
description: System Center Configuration Manager が収集する自身の診断および使用状況データについて説明します。
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
caps.latest.revision: 9
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5f783f11f6fbabda2fd1d6f98748e945affa878e
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2018
---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>System Center Configuration Manager の診断結果と使用状況データ

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager では、それ自体の診断および使用状況データが収集されます。このデータは、今後のリリースでインストールのエクスペリエンス、品質、セキュリティを向上させるために Microsoft によって使用されます。  

 診断および使用状況データは、それぞれの Configuration Manager 階層で有効になります。 これは、各プライマリ サイトと中央管理サイトで毎週実行される SQL Server クエリで構成されます。 階層が中央管理サイトを使用している場合、プライマリ サイトからのデータはそのサイトに複製されます。 階層の最上位のサイトでは、サービス接続ポイントが、更新プログラムをチェックするときに、この情報を送信します。 サービス接続ポイントがオフライン モードの場合、情報は、サービス接続ツールを使用して転送されます。  

> [!NOTE]  
>  Configuration Manager は、サイトの SQL Server データベースからのみデータを収集します。クライアントやサイト サーバーから直接データを収集することはありません。  

 詳細については、「[Microsoft のプライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkID=626527)」を参照してください。  

## <a name="articles"></a>記事
 Configuration Manager の診断および使用状況データの詳細については、次の記事を参照してください。  

-   [診断結果と使用状況データの使用方法](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   診断の使用状況データ収集のレベル
    - [1802 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1802)  
    - [1710 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1710)  
    - [1706 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1706)    

<!--
    - [Diagnostic data for 1702](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1702)      
    - [Diagnostic data for 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  
    - [Diagnostic data for  1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)    
    - [Diagnostic data for 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Diagnostic data for  1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
-->

-   [診断と使用状況データを収集する方法](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [診断および使用状況データを使用する方法](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [カスタマー エクスペリエンス向上プログラム (CEIP)](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

     > [!Note]  
     > Configuration Manager バージョン 1802 以降、CEIP 機能が製品から削除されます。


-   [診断および使用状況データに関してよく寄せられる質問](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>関連項目  
 [サービス接続ポイントについて](../../../core/servers/deploy/configure/about-the-service-connection-point.md)
