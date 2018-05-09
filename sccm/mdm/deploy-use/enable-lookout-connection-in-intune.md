---
title: Intune で Lookout MTP を有効にする
titleSuffix: Configuration Manager
description: Intune 管理コンソールで、Lookout Mobile Threat Protection を有効にします。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79a583237d882101d70442cbf6b55a5e3c0e9b11
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>Intune 管理コンソールで、Lookout MTP 接続を有効にする

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、Intune で Lookout MTP 接続を有効にする方法を説明します。 この手順を実行する前に、Lookout コンソールで Intune コネクタを構成しておきます。  まだ構成していない場合は、「[Set up your subscription with Lookout mobile threat protection](set-up-your-subscription-with-lookout.md)」(Lookout Mobile Threat Protection 用にサブスクリプションを設定する) で説明されている手順を実行します。

Intune で Lookout MTP 接続を有効にするには、[Microsoft Intune 管理者コンソール](https://manage.microsoft.com)の「**管理**」ページで、**[Third Party Service Integration]** (サード パーティ サービスの統合) を選択します。 **[Lookout の状態]** を選択し、**[MTP との同期]** をトグル ボタンを使用して有効にします。

![有効になったトグル ボタンが強調表示された、Lookout の同期ページのスクリーン ショット](media/lookout-intune-synchronization.png)

これで、Intune 管理者コンソールでの Lookout と Intune の統合の設定は完了です。  このソリューションを実装するための次の手順には、[Lookout for Work アプリ](configure-and-deploy-lookout-for-work-apps.md)の展開や、[コンプライアンス](enable-device-threat-protection-rule-compliance-policy.md) ポリシーの設定などが含まれます。

>[!IMPORTANT]
> コンプライアンス ポリシー ルールを作成し、条件付きアクセスを構成するには、事前に Lookout for Work アプリを構成する**必要があります**。 これにより、エンド ユーザーがアプリをインストールして、電子メールやその他の会社のリソースにアクセスする場合に使用できるようになります。

## <a name="next-steps"></a>次のステップ
[Lookout for Work アプリを構成する](configure-and-deploy-lookout-for-work-apps.md)
