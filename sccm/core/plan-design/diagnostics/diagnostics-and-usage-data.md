---
title: "診断結果と使用状況データ | Microsoft Docs"
description: "System Center Configuration Manager が収集する自身の診断および使用状況データについて説明します。"
ms.custom: na
ms.date: 12/29/2016
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
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 24a233516058e645df2a43623855665b97b041b0
ms.openlocfilehash: 54ec4886eaad6999cdf3ffff7411942859f1a5b2


---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>System Center Configuration Manager の診断結果と使用状況データ

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager では、それ自体の診断および使用状況データが収集されます。このデータは、今後のリリースでインストールのエクスペリエンス、品質、セキュリティを向上させるために Microsoft によって使用されます。  

 診断および使用状況データは、それぞれの System Center Configuration Manager 階層で有効になります。 これは、各プライマリ サイトと中央管理サイトで毎週実行される SQL Server クエリで構成されます。 階層が中央管理サイトを使用している場合、プライマリ サイトからのデータはそのサイトに複製されます。 階層の最上位のサイトでは、サービス接続ポイントが、更新プログラムをチェックするときに、この情報を送信します。 サービス接続ポイントがオフライン モードの場合、情報は、サービス接続ツールを使用して転送されます。  

> [!NOTE]  
>  Configuration Manager は、サイトの SQL Server データベースからのみデータを収集します。クライアントやサイト サーバーから直接データを収集することはありません。  

 詳細については、「[System Center Configuration Manager プライバシーに関する声明の概要](http://go.microsoft.com/fwlink/?LinkID=626527)」を参照してください。  

 System Center Configuration Manager の診断および使用状況データの詳細については、次の記事を参照してください。  

-   [System Center Configuration Manager での診断結果と使用状況データの使用方法](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   診断の使用状況データ収集のレベル
    - [1511 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
    - [1602 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [1606 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)  
    - [1610 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  

-   [System Center Configuration Manager が診断と使用状況データを収集する方法](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [System Center Configuration Manager の診断および使用状況データを表示する方法](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [System Center Configuration Manager のカスタマー エクスペリエンス向上プログラム (CEIP)](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

-   [System Center Configuration Manager の診断および使用状況データに関してよく寄せられる質問](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>関連項目  
 [System Center Configuration Manager のサービス接続ポイントについて](../../../core/servers/deploy/configure/about-the-service-connection-point.md)



<!--HONumber=Dec16_HO5-->


