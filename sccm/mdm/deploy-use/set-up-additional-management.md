---
title: 追加の管理をセットアップする
titleSuffix: Configuration Manager
description: System Center Configuration Manager を使用して追加の管理をセットアップします。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d866ce901640b6e7fafb13a6c24318f26c5d5feb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131797"
---
# <a name="set-up-additional-management-with-system-center-configuration-manager"></a>System Center Configuration Manager を使用して追加の管理をセットアップする

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

(省略可能) デバイスを登録する前に、追加の管理をセットアップすることができます。 このような管理ソリューションは、デバイスの登録後に作成し、展開することができますが、多くの組織は、デバイスを管理対象にするときに展開することを好みます。

**構成アイテム**を使用すると、デバイスのプラットフォームに基づいて、登録されるデバイスで PIN を必須にする、暗号化を必須にするなどの設定を管理できます。
- [Windows 10 デバイスと Windows 8.1 デバイス](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Windows Phone デバイス](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [iOS デバイスと Mac デバイス](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Android デバイスと Samsung KNOX Standard デバイス](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

マネージド デバイスには次の**アプリケーション**を展開できます。
- [iOS アプリケーション](creating-ios-applications.md)
- [Mac アプリケーション](../../apps/get-started/creating-mac-computer-applications.md)
- [Windows PC アプリケーション](../../apps/get-started/creating-windows-applications.md)
- [Windows Phone アプリケーション](creating-windows-phone-applications.md)
- [Android アプリケーション](creating-android-applications.md)

**条件付きアクセス**を使用すると、次のような会社のリソースへのアクセスを管理できます。  
- [電子メールへのアクセス](manage-email-access.md)
- [SharePoint へのアクセス](manage-sharepoint-online-access.md)
- [Skype for Business へのアクセス](manage-skype-for-business-online-access.md)
- [Dynamic CRM Online](manage-dynamics-crm-online-access.md)

**多要素認証 (MFA)** を使用すると複数の検証方法が必要になり、ユーザーのサインインとトランザクションに対して重要な第 2 のセキュリティ層が追加されます。
これまで、Intune の登録に MFA を設定するには、Intune コンソールまたは構成マネージャー コンソールを使用していました。 今後は Intune の資格情報で [Microsoft Azure Portal](https://manage.windowsazure.com) にログインし、Azure AD を使用して MFA の設定を構成するようになります。 詳細については、[Microsoft Intune への多要素認証](https://aka.ms/mfa_ad)に関する記事を参照してください。

> [!div class="button"]
> [< 前のステップ](enable-platform-enrollment.md)  [次のステップ >](verify-mdm-configuration.md)
