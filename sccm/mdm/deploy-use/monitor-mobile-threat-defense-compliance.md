---
title: Mobile Threat Defense コンプライアンスの監視
titleSuffix: Configuration Manager
description: Configuration Manager マネージャー コンソールからの Mobile Threat Defense パートナー コンプライアンス ステータスの監視
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cc5b38894155df35812d14397fb0d3aaea79c585
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122493"
---
# <a name="monitor-mobile-threat-defense-compliance"></a>**Mobile Threat Defense コンプライアンスの監視**

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

## <a name="to-monitor-the-overall-compliance-status"></a>全体的なコンプライアンス ステータスを監視するには

Mobile Threat Defense のステータスを監視するには、次のようにします。

1.  Configuration Manager コンソールで、**[監視]** ワークスペースをクリックします。

2.  **[監視]** ワークスペースで、**[セキュリティ]** ノードをクリックします。

ビジュアル グラフ形式で表示されるコンプライアンス ステータスの概要を、さまざまなレベルで確認することができます。 グラフの個々のセクションをクリックして、次のような詳細情報を表示することができます。 

- プラットフォームごとの、非準拠として報告されたデバイスの数
- デバイスのコンプライアンス ステータスに関連するエラー

![](http://i.imgur.com/bmPsiWk.png)

## <a name="to-monitor-the-individual-compliance-status"></a>個々のコンプライアンス ステータスを監視するには

次のようにして、個々のデバイス ステータスを確認することもできます。

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** ワークスペースをクリックします。

2.  **[デバイス]** をクリックします。

> [!TIP] 
> **[Device threat compliance]** (デバイス脅威コンプライアンス) 列と **[デバイス脅威レベル]** 列を追加して、状態を確認できます。 既定では、これらの列は表示されません。

## <a name="device-threat-protection-tab"></a>[デバイス脅威保護] タブ

さらに、**[デバイス]** 画面で、特定のデバイスを選択し、**[デバイス脅威保護]** タブをクリックして、デバイス コンプライアンス ステータスの詳細を表示することができます。 以下の列の説明と予期される値は、デバイスのコンプライアンス ステータスを分析するのに役立ちます。

> [!IMPORTANT] 
> 選択したデバイスがモバイル デバイスである場合は、[デバイスの脅威保護] タブのみが表示されます。

|列名|既定で表示|説明| 
|-|-|-|
|**説明**| はい | Mobile Threat Defense パートナーによって提供される脅威に関する詳細。 |
|**最終更新時刻**| はい | Mobile Threat Defense パートナーが Intune に脅威に関する更新済みの詳細情報を最後に送信した時刻。 |
|**脅威の重要度**| はい | 脅威の重要度は、Mobile Threat Defense パートナー コンソールでの管理者の構成に基づく個々の脅威の定義です。 次の 3 つの値の 1 つがあります。**低**、 **Medium**または**高** |
|**脅威の状態**| はい | デバイスの脅威の現在の状態。 状態があります。**アクティブな**、**解決**または**無視されます。** ユーザーが自分のデバイス上の脅威を無視、脅威がまだ存在することを示します。 |
|**脅威の種類**| はい | Mobile Threat Defense パートナーの脅威の種類。 使用可能な値:**アプリ**、**ファイル**または**OS** |
|**AAD アカウント ID**| いいえ | Azure Active Directory の一意の識別子です。 |
|**分類**| はい | Mobile Threat Defense パートナーにより提供される脅威の分類。 使用可能な値:**ルート イネーブラー、Riskware、アドウェア、Chargeware DataLeak、トロイの木馬、ワーム、ウイルスを攻撃、バックドア、ボット、AppDropper、ClickFraud、スパム、スパイウェア、SurveillanceWare、脆弱性、不明、Root Jailbrake、接続、TollFraud、SideloadedApp** |
|**デバイス ID**| いいえ | 脅威にさらされている社内参加済みデバイスに関する情報を示す Azure Active Directory のオブジェクト ID。 |
|**脅威 ID**| いいえ | Mobile Threat Defense パートナーで生成される脅威の一意の識別子。 脅威 ID は解決方法を追跡するために使用されます。 |
|**脅威 URL**| いいえ | 脅威 URL がある場合は、特定の脅威の Mobile Threat Defense パートナーの管理コンソール ビューに戻るリンクが示されます。 |

> [!TIP] 
> **既定で表示**されない列を有効にして、デバイスの Mobile Threat Defense コンプライアンス ステータスの詳細を確認できるようにしてください。
