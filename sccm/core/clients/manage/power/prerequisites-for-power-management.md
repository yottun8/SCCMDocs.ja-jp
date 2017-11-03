---
title: "電源管理の前提条件 | Microsoft Docs"
description: "System Center Configuration Manager の電源管理の前提条件を確認します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
caps.latest.revision: "4"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 5247bf1ce5b04264bc0d3e04c5de7f98300905c9
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2017
---
# <a name="prerequisites-for-power-management-in-system-center-configuration-manager"></a>System Center Configuration Manager の電源管理の前提条件

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の電源管理には、外部依存関係と製品内部依存関係があります。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  
 次の表は、電源管理を使用する場合の Configuration Manager 外部の依存関係の一覧です。  

|依存関係|説明|  
|----------------|----------------------|  
|クライアント コンピューターが、必要な電源状態をサポートできる必要があります。|電源管理のすべての機能を使用するには、クライアント コンピューターがスリープ、休止、スリープ状態からの復帰、および休止状態からの復帰、をサポートしている必要があります。 コンピューターがこれらの操作をサポートしているかどうかを判断するには、**[電源機能]** レポートを使用できます。 詳細については、「[How to monitor and plan for power management in System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)」(System Center Configuration Manager で電源管理を監視および計画する方法) の「[Power Capabilities report](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites)」(電源機能レポート) を参照してください。|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  
 次の表は、電源管理を使用する場合の Configuration Manager 内部の依存関係の一覧です。  

|依存関係|説明|  
|----------------|----------------------|  
|電源プランを作成し監視するには、事前に電源管理を有効化することが必要です。|電源管理を有効化して構成する方法の詳細については、「 [Configuring power management in System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md)」(System Center Configuration Manager で電源管理を構成する) を参照してください。|  
|レポート サービス ポイント|電源管理レポートを表示するには、事前にレポート サービス ポイントを構成する必要があります。 詳細については、「[System Center Configuration Manager のレポート](../../../../core/servers/manage/reporting.md)」を参照してください。|  
