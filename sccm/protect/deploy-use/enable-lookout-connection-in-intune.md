---
title: "Intune での Lookout MTP の有効化 | System Center Configuration Manager"
description: "Intune 管理コンソールで、Lookout Mobile Threat Protection を有効にします。"
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9536efdd-0f29-47a8-8283-0edea7714319
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c13c6268fa76ade7feb0981f9c4a6e325e393aca
ms.openlocfilehash: a06f0b3a0080a06a0ccbfa7f3802c575aee2c9b7


---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>Intune 管理コンソールで、Lookout MTP 接続を有効にする

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、Intune で Lookout MTP 接続を有効にする方法を説明します。 この手順を実行する前に、Lookout コンソールで Intune コネクタを構成しておきます。  まだ構成していない場合は、「[Set up your subscription with Lookout mobile threat protection](set-up-your-subscription-with-lookout.md)」(Lookout Mobile Threat Protection 用にサブスクリプションを設定する) で説明されている手順を実行します。

Intune で Lookout MTP 接続を有効にするには、[Microsoft Intune 管理者コンソール](https://manage.microsoft.com)の「**管理**」ページで、**[Third Party Service Integration]** (サード パーティ サービスの統合) を選択します。 **[Lookout の状態]** を選択し、**[MTP との同期]** をトグル ボタンを使用して有効にします。

![有効になったトグル ボタンが強調表示された、Lookout の同期ページのスクリーン ショット](../media/lookout-intune-synchronization.png)

これで、Intune 管理者コンソールでの Lookout と Intune の統合の設定は完了です。  このソリューションを実装するための次の手順には、[Lookout for Work アプリ](configure-and-deploy-lookout-for-work-apps.md)の展開や、[コンプライアンス](enable-device-threat-protection-rule-compliance-policy.md) ポリシーの設定などが含まれます。

>[!IMPORTANT]
> コンプライアンス ポリシー ルールを作成し、条件付きアクセスを構成するには、事前に Lookout for Work アプリを構成する**必要があります**。 これにより、エンド ユーザーがアプリをインストールして、電子メールやその他の会社のリソースにアクセスする場合に使用できるようになります。

## <a name="next-steps"></a>次のステップ
[Lookout for Work アプリを構成する](configure-and-deploy-lookout-for-work-apps.md)



<!--HONumber=Dec16_HO3-->


