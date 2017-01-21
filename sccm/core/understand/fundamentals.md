---
title: "System Center Configuration Manager の基本 | Microsoft Docs"
description: "System Center Configuration Manager の基本的な概念について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc4cdb35-f0b4-42b5-9cec-6431a8c30793
caps.latest.revision: 11
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: b808e9089aabe3895892ecf3caf1610478361172

---
# <a name="fundamentals-of-system-center-configuration-manager"></a>System Center Configuration Manager の基本

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager を初めて使用する場合は、Configuration Manager の基本概念を理解するための基本的なトピックをお読みになってから、最初のサイトをインストールするセットアップ プログラムを実行してください。 Configuration Manager に慣れている場合は、「[System Center Configuration Manager の新機能](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)」から直接始めることをお勧めします。  

 サポートされるオペレーティング システムと、サポートされる環境、ハードウェア要件、および容量の情報については、「 [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)」を参照してください。  

 Configuration Manager を展開する場合は、1 つ以上のサイトを展開します。  

-   **複数のサイトを展開する場合**、サイトは総称して階層と呼ばれる子から親への関係を形成します。 階層では、より多くのサイトとデバイスを一元的に管理することができます。  データと情報は、管理するデバイスに到達するまで下位階層に送られます。 デバイスに関する情報、構成タスクと構成要求の結果は、上位階層に送られます。  

-   **1 つのサイトを展開する場合も** 階層と呼ばれます。  

 構成タスクと構成設定には階層内のすべてのサイトに適用されるものと、個々のサイトに適用されるものがあります。  


**次のトピックでは、System Center Configuration Manager の基本的な概念が説明されています。**  

-   [System Center Configuration Manager のサイトおよび階層の基礎](../../core/understand/fundamentals-of-sites-and-hierarchies.md)  

-   [System Center Configuration Manager を使用したデバイス管理の基礎](../../core/understand/fundamentals-of-managing-devices.md)  

-   [System Center Configuration Manager のクライアント管理タスクの基礎](../../core/understand/fundamentals-of-client-management-tasks.md)  

-   [System Center Configuration Manager のセキュリティの基礎](../../core/understand/fundamentals-of-security.md)  



<!--HONumber=Dec16_HO3-->


