---
title: "基本"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager の基本的な概念について説明します。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc4cdb35-f0b4-42b5-9cec-6431a8c30793
caps.latest.revision: "11"
caps.handback.revision: "0"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 1ea8c62ce4b0dd68042b08e91dd4d4d7a7b07aa8
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/01/2017
---
# <a name="fundamentals-of-system-center-configuration-manager"></a>System Center Configuration Manager の基本

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager を初めて使用する場合は、Configuration Manager の基本概念を理解するための基本的なトピックをお読みになってから、最初のサイトをインストールするセットアップを実行してください。 Configuration Manager を使い慣れている場合は、すぐに操作を開始できます。 最初に「[System Center Configuration Manager の新機能](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)」を参照することをお勧めします。  

 サポートされるオペレーティング システムと、サポートされる環境、ハードウェア要件、および容量の情報については、「 [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)」を参照してください。  

 Configuration Manager を展開する場合は、1 つ以上のサイトを展開します。  

-   **複数のサイトを展開する場合**、サイトは総称して階層と呼ばれる子から親への関係を形成します。 階層を使用して、より多くのサイトとデバイスを一元的に管理します。  データと情報は、管理するデバイスに到達するまで下位階層に送られます。 デバイスに関する情報、構成タスクと要求の結果は、上位階層に送られます。  

-   **1 つのサイトを展開する場合も**階層と呼ばれます。  

 構成タスクと構成設定には階層内のすべてのサイトに適用されるものと、個々のサイトに適用されるものがあります。  

## <a name="fundamental-concepts-for-system-center-configuration-manager"></a>System Center Configuration Manager の基本的な概念
System Center Configuration Manager の基本的な概念については、以下のトピックを参照してください。  

-   [System Center Configuration Manager のサイトおよび階層の基礎](../../core/understand/fundamentals-of-sites-and-hierarchies.md)  

-   [System Center Configuration Manager を使用したデバイス管理の基礎](../../core/understand/fundamentals-of-managing-devices.md)  

-   [System Center Configuration Manager のクライアント管理タスクの基礎](../../core/understand/fundamentals-of-client-management-tasks.md)  

-   [System Center Configuration Manager のセキュリティの基礎](../../core/understand/fundamentals-of-security.md)  
