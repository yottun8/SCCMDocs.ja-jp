---
title: iOS アプリケーションを作成する
titleSuffix: Configuration Manager
description: Configuration Manager で iOS デバイス用アプリケーションを作成して展開する方法。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e4a2d84fe31c3a524b876e3beb34f0e3d25d0089
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125444"
---
# <a name="create-ios-applications-in-configuration-manager"></a>Configuration Manager で iOS アプリケーションを作成する

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager アプリケーションには、デバイスにソフトウェアを展開するために必要なインストール ファイルと情報からなる、1 つまたは複数の展開の種類があります。 また、展開の種類には、ソフトウェアを展開するタイミングと方法を指定する規則があります。  

Configuration Manager アプリケーションと展開の種類を作成する手順については、[アプリケーションの作成](/sccm/apps/deploy-use/create-applications#bkmk_create)に関するページを参照してください。 

iOS デバイス用アプリケーションを作成して展開するときに、以下の考慮事項について留意してください。  

- Configuration Manager では、iOS の .ipa パッケージの展開がサポートされています。 iOS アプリをインポートするときに、プロパティ一覧 (.plist) ファイルを指定する必要はありません。 

- iOS アプリケーションを**利用可能**または**必須**として展開します。 インストールとアンインストールの両方に、ユーザーが同意する必要があります。

> [!IMPORTANT]  
>  現在、エンド ユーザーは iOS 向け Microsoft Intune ポータル サイト アプリから会社のアプリをインストールできません。 これは、iOS App Store に公開されたアプリに関する制限があるためです  (「App Store Review ガイドライン」の第 2 節をご覧ください)。 ユーザーは自分のデバイスで Intune ポータルを参照して、会社のアプリをインストールできます。 これらのアプリには、管理対象 App Store アプリおよび基幹業務アプリのパッケージが含まれます。 Intune ポータル サイト アプリで有効化されるモバイル管理機能の詳細については、[Microsoft Intune の登録済みデバイス管理機能](https://docs.microsoft.com/intune/device-enrollment)に関するページを参照してください。  
