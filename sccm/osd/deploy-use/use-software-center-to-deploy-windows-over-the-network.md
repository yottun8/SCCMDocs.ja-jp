---
title: "ソフトウェア センターを使用してネットワーク経由で Windows を展開する | Configuration Manager"
description: "オペレーティング システムをソフトウェア センターに展開して、既存のコンピューターを新しいバージョンの Windows に更新したり、Windows を最新バージョンにアップグレードしたりできます。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 189fdac38760b75eb3795348f6af4ef7e83c3f20


---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>System Center Configuration Manager でソフトウェア センターを使用してネットワーク経由で Windows を展開する

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager でオペレーティング システムをインストールするためのタスク シーケンスは、ソフトウェア センターから使用可能にすることができます。 次のオペレーティング システムの展開シナリオでは、オペレーティング システムをソフトウェア センターに展開することができます。  

-   [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Windows を最新バージョンにアップグレードする](upgrade-windows-to-the-latest-version.md)  

 いずれかのオペレーティング システムの展開シナリオの手順を実行してから、次のセクションに従って、ソフトウェア センターで使用可能にする展開を準備します。  

## <a name="configure-deployment-settings"></a>展開の設定の構成  
 オペレーティング システムの展開をソフトウェア センターから利用可能にする場合は、Configuration Manager クライアントでそのオペレーティング システムが利用可能になるように展開を構成する必要があります。 これはソフトウェアの展開ウィザードの **[展開の設定]** ページか展開のプロパティの **[配置の設定]** タブで構成することができます。  **[利用できるようにする項目]** 設定で、 **[Configuration Manager クライアントのみ]** または **[Configuration Manager クライアント、メディア、PXE]**のいずれかを構成します。 オペレーティング システムを展開した後、ソフトウェア センターにターゲット コレクションのメンバーとして表示されます。  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a> コンピューターへのタスク シーケンスの展開  
 オペレーティング システムをターゲット コレクションに展開します。 詳細については、「 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)」をご覧ください。 ソフトウェア センターでオペレーティング システムを展開するとき、展開が必須か使用可能かを設定することができます。  

-   **必須の展開**: 必須の展開では、ソフトウェア センターでオペレーティング システムが利用可能になりますが、構成された割り当てスケジュールで自動的に開始されます。  

-   **使用可能な展開**: オペレーティング システムはソフトウェア センターで使用可能になり、ユーザーはオンデマンドでインストールすることができます。  



<!--HONumber=Nov16_HO1-->


