---
title: コンプライアンス ポリシーのデバイス保護規則を有効にする
titleSuffix: Configuration Manager
description: デバイス コンプライアンス ポリシーのモバイル脅威保護の規則を有効にします。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 99a5b715-f172-46e1-ac27-ad55bde66d0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0bae054d3daa5aea8e343fef05aa4578221f17b6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133988"
---
# <a name="enable-device-threat-protection-rule-in-the-compliance-policy"></a>コンプライアンス ポリシーのデバイス脅威保護の規則を有効にする

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Intune で Lookout モバイル脅威保護を利用すると、モバイルの脅威を検出し、デバイス上でリスク評価を行うことができます。 Configuration Manager でコンプライアンス ポリシー規則を作成して、デバイスがポリシーに準拠しているかどうかを判別するリスク評価を含めることができます。 次に条件付きアクセス ポリシーを使用して、デバイスのポリシー準拠に基づき、Exchange、SharePoint、およびその他のサービスへのアクセスを許可またはブロックすることができます。

Lookout のデバイス脅威検出がデバイスのコンプライアンス ポリシーに影響を与えるようにする方法は次のとおりです。

* コンプライアンス ポリシーで、**デバイス脅威保護**規則を有効にする必要があります。

* **Intune 管理者コンソール**の **[Lookout の状態]** ページの表示を **[アクティブ]** にする必要があります。 Lookout の統合をアクティブ化する方法の詳細については、[Intune での Lookout MTP 接続の有効化](enable-lookout-connection-in-intune.md)に関するページを参照してください。


コンプライアンス ポリシーでデバイス脅威保護規則を作成する前に、[Lookout デバイス脅威保護を利用するようにサブスクリプションを設定](set-up-your-subscription-with-lookout.md)し、[Intune で Lookout 接続を有効](enable-lookout-connection-in-intune.md)にして、[Lookout for Work アプリを構成](configure-and-deploy-lookout-for-work-apps.md)することをお勧めします。 コンプライアンス規則は、セットアップ完了後にのみ適用されます。

デバイス脅威保護の規則を有効にするには、既存のコンプライアンス ポリシーを使用するか、または新しいコンプライアンス ポリシーを作成します。

Lookout デバイス脅威保護のセットアップの一環として、[Lookout コンソール](https://aad.lookout.com)で各種脅威を高、中、および低レベルに分類するポリシーを作成しています。 Intune のコンプライアンス ポリシーでこの脅威レベルを使用して、許容される最大脅威レベルを設定します。

コンプライアンス ポリシー ウィザードの **[規則]** ページで、次の情報を参考にして新しい規則を定義します。
  * 条件:デバイス脅威保護の最大リスク レベル。
  * 値: 値には、次のいずれかを指定できます。
    * **なし (セキュリティ保護)**:これは、最も安全です。 デバイスに脅威があってはならないことを意味します。 いずれかのレベルの脅威が発見された場合、デバイスは非準拠として評価されます。
    * **低**:低レベルの脅威が存在する場合のみ、デバイスは準拠として評価されます。 中レベル以上の脅威が存在する場合、デバイスは非準拠のステータスに分類されます。
    * **Medium**:デバイスは、デバイスに存在する脅威が低または中レベルの場合は準拠として評価されます。 高レベルの脅威が検出された場合、デバイスは非準拠と判定されます。
    * **高**:これは、最も安全性。 このレベルでは基本的にすべての脅威レベルが許容されるため、役に立つのはこのソリューションをレポート目的で使用する場合のみです。

Office 365 やその他のサービス向けに条件付きのアクセス ポリシーを作成する場合は、上記のコンプライアンス評価を考慮して、脅威が解消されるまでは会社のリソースへの非準拠デバイスのアクセスをブロックする必要があります。

デバイス脅威保護の状態は、**[監視]** ワークスペースの **[セキュリティ]** ノードに表示されます。
各脅威レベルの状態の概要が、視覚的なグラフで表示されます。 グラフの各セクションをクリックすると、プラットフォーム別に非準拠と報告されたデバイスの数や、報告されたエラーなどの詳細情報を確認することができます。
**[資産とコンプライアンス]** ワークスペースの **[デバイス]** で、各デバイスの状態を確認することもできます。  **[Device threat compliance]** (デバイス脅威コンプライアンス) 列と **[デバイス脅威レベル]** 列を追加して、状態を確認できます。  既定では、これらの列は表示されません。
