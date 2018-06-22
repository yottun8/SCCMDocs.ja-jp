---
title: Intune に登録されたデバイスのポリシーをリモートで同期する
titleSuffix: Configuration Manager
description: Intune に登録されたデバイスのポリシーを Configuration Manager コンソールから同期する方法について説明します
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ecd2c480ab67a82539edff6daa18ef0f93628c6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32345714"
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Intune に登録されたデバイスのポリシーを Configuration Manager コンソールからリモートで同期する

*適用対象: System Center Configuration Manager (Current Branch)*


デバイス自体のポータル サイト アプリから同期を要求するのではなく、Configuration Manager コンソールから Intune に登録されたデバイスのポリシー同期を要求できます。 

手順は次のとおりです。

1.  **[資産とコンプライアンス]** > **[概要]** > **[デバイス]** で、デバイスを選択します。
2.  **[リモート デバイスの操作]** メニューの **[同期要求の送信]** をクリックします。


5 ～ 10 分で、ポリシーのすべての変更がデバイスに同期されます。 同期要求の状態の情報を、デバイス ビューの新しい列 **[Remote Sync State]** (リモート同期の状態)、および各デバイスの **[プロパティ]** ダイアログ ボックスの [探索データ] セクションで、見ることができます。
