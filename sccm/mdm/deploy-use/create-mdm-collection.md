---
title: MDM コレクションを作成する
titleSuffix: Configuration Manager
description: System Center Configuration Manager を使用して MDM コレクションを作成します。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0288b88187ead39f1cf584ebf88e3943549b01f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124014"
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用した MDM コレクションの作成

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

デバイスを管理対象に登録できるユーザーを指定するには、Configuration Manager ユーザー コレクションが必要です。 Intune のライセンスはユーザーごとに割り当てられるため、使用できるのはユーザー コレクション (デバイス コレクションではなく) のみです。

> [!NOTE]
> Intune にデバイスを登録する場合、Office 365 ポータルまたは Azure Active Directory ポータルでユーザーにライセンスを割り当てる必要はありません。 Intune サブスクリプションに関連付けられたコレクションにユーザーを含める ([後の手順](configure-intune-subscription.md)を参照) だけで済みます。

テスト目的で**ダイレクト規則**をセットアップし、デバイスを登録できる特定のユーザーを追加することができます。 Configuration Manager コンソールで、**[資産とコンプライアンス]**  >  **[ユーザー コレクション]** の順に選択し、**[ホーム]** タブ > **[作成]** グループの順にクリックしてから、**[ユーザー コレクションの作成]** をクリックします。 配布を広範にするには、**クエリ規則**を使用してユーザーを定義するようにします。 コレクションの詳細については、「[System Center Configuration Manager でコレクションを作成する方法](https://technet.microsoft.com/library/mt629371.aspx)」を参照してください。

![MDM のユーザー コレクションを作成する](../media/mdm-create-user-collection.png)

> [!div class="button"]
> [次のステップ >](confirm-dns.md)
