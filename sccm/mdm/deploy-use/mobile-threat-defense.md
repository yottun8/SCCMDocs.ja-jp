---
title: リスクに基づいてアクセスを制限する
titleSuffix: Configuration Manager
description: デバイス、ネットワーク、アプリケーションのリスクに基づいてアクセスを制限します。
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 90098dc0243e8513fe78692fe91a8390f7936eba
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56119651"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>デバイス、ネットワーク、アプリケーションのリスクに基づき、会社のリソースへのアクセスを管理する

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Mobile Threat Defense コネクターを使用すると、選択した Mobile Threat Defense ベンダーをコンプライアンス ポリシーと条件付きアクセス規則の情報ソースとして活用できます。 これにより、特に危険にさらされたモバイル デバイスから、Exchange、Sharepoint などの組織リソースに保護レイヤーを追加することができます。

> [!Important]  
> 2018 年 8 月 14 日の時点では、ハイブリッド モバイル デバイス管理は[非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)です。 詳細については、[ハイブリッド MDM の概要](/sccm/mdm/understand/hybrid-mobile-device-management)に関するページを参照してください。<!--Intune feature 2683117-->  



## <a name="what-problem-does-this-solve"></a>これはどのような問題を解決しますか。

組織は、物理的な脅威、アプリ ベースの脅威、インターネット ベースの脅威、OS の脆弱性など、新しく現れた脅威から機密データを守る必要があります。

これまで、組織は PC の防御を積極的に行ってきましたが、モバイル デバイスは監視や保護のない状態が続いていました。 モバイル プラットフォームには、アプリの分離や検証済みコンシューマー アプリ ストアなどの防御手法が組み込まれていますが、依然として高度な攻撃を受けやすい状態にあります。 今日では、仕事でモバイル デバイスを利用して、機密情報にアクセスする社員が増えています。 より高度さを増す攻撃からモバイル デバイスを守る必要があります。



## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Intune Mobile Threat Defense コネクターのしくみ

このコネクターは、Intune と選択した Mobile Threat Defense ベンダーの間に通信チャネルを作成することで、組織のリソースを保護します。 Intune Mobile Threat Defense パートナーは、直感的で簡単に展開できるモバイル デバイス向けアプリケーションを提供します。これらのアプリケーションは、脅威情報を積極的にスキャンして分析し、Intune と共有します。 この情報をレポートや強制を目的として使用します。 

たとえば、接続された Mobile Threat Defense アプリは、デバイスが man-in-the-middle 攻撃に対して脆弱なネットワークに現在接続されていることを、Mobile Threat Defense ベンダーに報告します。 この情報は共有されて、適切なリスク レベル (低、中、高) に分類されます。 このリスクを Intune で構成済みのリスク レベル許容度と比較し、デバイスが侵害されたときに選択した特定のリソースへのアクセスを無効にする必要があるかどうかを判断します。



## <a name="sample-scenarios"></a>サンプル事例

Mobile Threat Defense ソリューションによってデバイスが感染したと見なされた場合

![Mobile Threat Defense の感染デバイス](../media/mtp/MTD-image-1.png)

デバイスが修復されたときにアクセスが許可されます。

![Mobile Threat Defense のアクセス許可](../media/mtp/MTD-image-2.png)



## <a name="next-steps"></a>次のステップ

デバイス、ネットワーク、アプリケーションのリスクに基づいて、会社のリソースへのアクセスを保護する方法について説明します。次のものを使用します。

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)
