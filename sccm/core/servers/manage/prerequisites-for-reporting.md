---
title: "レポートの前提条件"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager のレポートの使用に影響するさまざまな依存関係について理解します。"
ms.custom: na
ms.date: 01/29/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: 
caps.handback.revision: 
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 3feafa8a20bedfba381c29a5d7fe80a47517b6ab
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2018
---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager のレポートの前提条件

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のレポートには、外部依存関係と製品内部依存関係があります。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  
 次の表に、レポートの外部の依存関係を示します。  

|前提条件|説明|  
|------------------|----------------------|  
|SQL Server Reporting Services|Configuration Manager のレポートを使用するには、事前に SQL Server Reporting Services をインストールして構成しておく必要があります。<br /><br /> 各組織の環境内での Reporting Services の計画と展開については、SQL Server 2008 オンライン ブックの「 [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) 」を参照してください。|  
|レポート サービス ポイントを実行するコンピューターのサイト システムの役割の依存関係|[System Center Configuration Manager のサポートされている構成](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Configuration Manager 内部の依存関係  
 次の表に、Configuration Manager のレポートの依存関係を示します。  

|前提条件|説明|  
|------------------|----------------------|  
|レポート サービス ポイント|Configuration Manager のレポートを使用するには、事前にレポート サービス ポイントのサイト システムの役割を構成しておく必要があります。 レポート サービス ポイントのインストールと構成方法の詳細については、「[System Center Configuration Manager におけるレポートの構成](../../../core/servers/manage/configuring-reporting.md)」を参照してください。|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>レポート サービス ポイントでサポートされる SQL Server バージョン  
 レポート サービス データベースは、64 ビット SQL Server インストールの既定のインスタンスまたは名前付きインスタンスにインストールできます。 SQL Server インスタンスは、サイト システム サーバーまたはリモート コンピューターと併置できます。  

 次の表に、レポート サービス ポイントがサポートする SQL Server バージョンを示します。  

|SQL Server バージョン|レポート サービス ポイント|  
|------------------------|------------------------------|
|累積的な更新プログラム 2 以上を適用した SQL Server 2017<br /><br /> -   Standard<br />-   Enterprise|はい、Configuration Manager バージョン 1710 以降|  
|SQL Server 2016 SP1<br /><br /> -   Standard<br />-   Enterprise|はい| 
|SQL Server 2016<br /><br /> -   Standard<br />-   Enterprise|はい|
|SQL Server 2014 SP2<br /><br /> -   Standard<br />-   Enterprise|はい|
|SQL Server 2014 SP1<br /><br /> -   Standard<br />-   Enterprise|はい|
|SQL Server 2012 SP4 <br /><br /> -   Standard<br />-   Enterprise|はい|  
|SQL Server 2012 SP3 <br /><br /> -   Standard<br />-   Enterprise|はい|  
|SQL Server 2008 R2 SP3<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|はい、Configuration Manager 1702 より前のサポートされるバージョンの場合。|  
|SQL Server Express 2008 R2 SP3|サポートされません| 




## <a name="next-steps"></a>次のステップ
[レポートの操作とメンテナンス](operations-and-maintenance-for-reporting.md)
