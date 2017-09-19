---
title: "Intune に登録されたデバイスのポリシーをリモートで同期する | Microsoft Docs"
description: "Intune に登録されたデバイスのポリシーを Configuration Manager コンソールから同期する方法について説明します"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
caps.latest.revision: "18"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 387f6303611010ab3d72f796455409ebfff65099
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2017
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Intune に登録されたデバイスのポリシーを Configuration Manager コンソールからリモートで同期する

*適用対象: System Center Configuration Manager (Current Branch)*


デバイス自体のポータル サイト アプリから同期を要求するのではなく、Configuration Manager コンソールから Intune に登録されたデバイスのポリシー同期を要求できます。 

手順は次のとおりです。

1.  **[資産とコンプライアンス]** > **[概要]** > **[デバイス]** で、デバイスを選択します。
2.  **[リモート デバイスの操作]** メニューの **[同期要求の送信]** をクリックします。


5 ～ 10 分で、ポリシーのすべての変更がデバイスに同期されます。 同期要求の状態の情報を、デバイス ビューの新しい列 **[Remote Sync State]** (リモート同期の状態)、および各デバイスの **[プロパティ]** ダイアログ ボックスの [探索データ] セクションで、見ることができます。
