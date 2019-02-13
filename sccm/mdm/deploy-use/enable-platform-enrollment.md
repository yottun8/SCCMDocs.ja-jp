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
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e9c9cd6f881fd43c6d6824fbca5dc05f00fc5ea
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136747"
---
# <a name="enable-platform-enrollment-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用してプラットフォームの登録を有効にする

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

デバイスの登録を有効にするには、デバイス プラットフォームごとに必要な追加の構成があります。
  - [iOS と Mac の登録セットアップ](enroll-hybrid-ios-mac.md):Apple MDM プッシュ証明書を取得します。

  - [Windows の登録セットアップ](enroll-hybrid-windows.md):DNS を構成し、両方の Windows Pc、Windows 10 Mobile、および Windows Phone デバイスの登録を有効にします。

  - [Android](enroll-hybrid-android.md):Android デバイスの登録を有効にする追加の手順は必要ありません。

MDM 管理を有効にした後は、各ユーザーが登録できるデバイスの数を指定できます (ユーザーごとに最大 15 デバイス)。
