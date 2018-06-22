---
title: プラットフォームの登録を有効にする
titleSuffix: Configuration Manager
description: System Center Configuration Manager と Microsoft Intune を使用してプラットフォームの登録を有効にします。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: a9163b77-a67d-4139-8272-bb1dfdb8707c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9a93d58f990738a93a489e0ee5920098ea04fce0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32345888"
---
# <a name="enable-platform-enrollment-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用してプラットフォームの登録を有効にする

*適用対象: System Center Configuration Manager (Current Branch)*

デバイスの登録を有効にするには、デバイス プラットフォームごとに必要な追加の構成があります。
  - [iOS と Mac の登録セットアップ](enroll-hybrid-ios-mac.md): Apple MDM プッシュ証明書を取得します

  - [Windows の登録セットアップ](enroll-hybrid-windows.md): DNS を構成し、Windows PC、Windows 10 Mobile デバイス、Windows Phone デバイスのすべてで登録を有効にします

  - [Android](enroll-hybrid-android.md): Android デバイスの場合、登録を有効にするために必要な追加の手順はありません

MDM 管理を有効にした後は、各ユーザーが登録できるデバイスの数を指定できます (ユーザーごとに最大 15 デバイス)。
