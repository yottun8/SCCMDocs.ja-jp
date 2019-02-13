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
ms.collection: M365-identity-device-management
ms.openlocfilehash: eab8f812b8772be0812437359275b80702f5760c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137747"
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Intune に登録されたデバイスのポリシーを Configuration Manager コンソールからリモートで同期する

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*


デバイス自体のポータル サイト アプリから同期を要求するのではなく、Configuration Manager コンソールから Intune に登録されたデバイスのポリシー同期を要求できます。 

手順は次のとおりです。

1.  **[資産とコンプライアンス]** > **[概要]** > **[デバイス]** で、デバイスを選択します。
2.  **[リモート デバイスの操作]** メニューの **[同期要求の送信]** をクリックします。


5 ～ 10 分で、ポリシーのすべての変更がデバイスに同期されます。 同期要求の状態の情報を、デバイス ビューの新しい列 **[Remote Sync State]** (リモート同期の状態)、および各デバイスの **[プロパティ]** ダイアログ ボックスの [探索データ] セクションで、見ることができます。
