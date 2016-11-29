---
title: "電源管理のセキュリティとプライバシー | System Center Configuration Manager"
description: "System Center Configuration Manager の電源管理のセキュリティとプライバシーの情報を確認します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 26880f6682e2bdf61cb7f29416e5dfded3559e8e


---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>System Center Configuration Manager の電源管理のセキュリティとプライバシー

*適用対象: System Center Configuration Manager (Current Branch)*

このセクションには、System Center Configuration Manager の電源管理のセキュリティとプライバシーの情報が含まれています。  

## <a name="security-best-practices-for-power-management"></a>電源管理に関するセキュリティのベスト プラクティス  
 電源管理に関してセキュリティ関連の推奨する運用方法はありません。  

## <a name="privacy-information-for-power-management"></a>電源管理のプライバシー情報  
 電源管理は、Windows に組み込まれている機能を使用して、業務時間の内外にわたって電力使用状況を監視し、コンピューターに電源設定を適用します。 Configuration Manager は、コンピューターを使用するユーザーのデータを含む電力使用状況に関する情報を、コンピューターから収集します。 Configuration Manager は、各コンピューターではなく、コレクションの電力使用状況を監視しますが、コレクションは、1 台のコンピューターのみを含むことができます。 電源管理は、既定では有効になっておらず、管理者による構成が必要です。  

 Configuration Manager データベースに格納される電力使用状況情報は、Microsoft に送信されることはありません。 データベースに、詳細情報は 31 日間保持され、概要情報は 13 か月間保持されます。 削除間隔は構成できません。  

 電源管理を構成する前に、プライバシー要件について検討してください。  



<!--HONumber=Nov16_HO1-->


