---
title: "Microsoft Intune に登録されているモバイル デバイスのソフトウェア インベントリ | Microsoft Docs"
description: "Microsoft Intune に登録されているモバイル デバイスのソフトウェア インベントリ。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 2ed79d02535768de136947e4a5b63ad186d9a3cd
ms.contentlocale: ja-jp
ms.lasthandoff: 05/17/2017

---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Microsoft Intune に登録されているモバイル デバイスのソフトウェア インベントリ

*適用対象: System Center Configuration Manager (Current Branch)*

 モバイル デバイスにインストールされているアプリのインベントリを収集できます。 インベントリに収集されるアプリは、デバイスが会社所有か個人所有かによって異なります。 個人用デバイスの場合、インベントリに収集されるアプリは、Microsoft Intune で管理されているアプリのみです。  

> [!NOTE]  
>  モバイル デバイスにインストールされているアプリのインベントリが[ハードウェア インベントリ](mobile-device-hardware-inventory-hybrid.md) プロセスの一部として収集されます。  

 個人所有のデバイスまたは会社所有のデバイスのインベントリに次のアプリが収集されます。  

|プラットフォーム|個人所有のデバイス|会社所有のデバイス|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (Configuration Manager クライアントを使用しない)|管理対象アプリのみ|管理対象アプリのみ|
|Windows 8.1 (Configuration Manager クライアントを使用しない)|管理対象アプリのみ|管理対象アプリのみ|  
|Windows Phone 8|管理対象アプリのみ|管理対象アプリのみ|  
|Windows RT|管理対象アプリのみ|管理対象アプリのみ|  
|iOS|管理対象アプリのみ|デバイスにインストールされているすべてのアプリ|  
|Android|管理対象アプリのみ|デバイスにインストールされているすべてのアプリ|  

ソフトウェア インベントリを使用したクライアント デバイスでのファイル情報の収集の詳細については、[ソフトウェア インベントリの概要](../../core/clients/manage/inventory/introduction-to-software-inventory.md)と[ソフトウェア インベントリの構成方法](../../core/clients/manage/inventory/configure-software-inventory.md)に関する記事を参照してください。

