---
title: "プラットフォームの登録を有効にする"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager と Microsoft Intune を使用してプラットフォームの登録を有効にします。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9163b77-a67d-4139-8272-bb1dfdb8707c
caps.latest.revision: "18"
caps.handback.revision: "0"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 318e36fc751aad31d0d641d6989df06621d17acf
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2017
---
# <a name="enable-platform-enrollment-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用してプラットフォームの登録を有効にする

*適用対象: System Center Configuration Manager (Current Branch)*

デバイスの登録を有効にするには、デバイス プラットフォームごとに必要な追加の構成があります。
  - [iOS と Mac の登録セットアップ](enroll-hybrid-ios-mac.md): Apple MDM プッシュ証明書を取得します

  - [Windows の登録セットアップ](enroll-hybrid-windows.md): DNS を構成し、Windows PC、Windows 10 Mobile デバイス、Windows Phone デバイスのすべてで登録を有効にします

  - [Android](enroll-hybrid-android.md): Android デバイスの場合、登録を有効にするために必要な追加の手順はありません

MDM 管理を有効にした後は、各ユーザーが登録できるデバイスの数を指定できます (ユーザーごとに最大 15 デバイス)。
