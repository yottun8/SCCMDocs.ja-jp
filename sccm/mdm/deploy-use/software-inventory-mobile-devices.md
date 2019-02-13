---
title: Microsoft Intune に登録されているモバイル デバイスのソフトウェア インベントリ
titleSuffix: Configuration Manager
description: Microsoft Intune に登録されているモバイル デバイスのソフトウェア インベントリ。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91d298dae14c879e215b85483558898382c12055
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120744"
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Microsoft Intune に登録されているモバイル デバイスのソフトウェア インベントリ

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

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
