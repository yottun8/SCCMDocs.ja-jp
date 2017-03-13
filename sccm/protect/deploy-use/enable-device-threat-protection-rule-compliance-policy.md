---
title: "コンプライアンス ポリシーのデバイス保護規則を有効にする | System Center Configuration Manager"
description: "デバイス コンプライアンス ポリシーのモバイル脅威保護の規則を有効にします。"
ms.custom: na
ms.date: 12/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 020f43e8-738e-4a82-91be-27b10cda9665
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 498b8c02dbf1391e6331c8b9ad7b6ef0fdef22d0
ms.openlocfilehash: 319289c9b211935ba10cb6d3da386ffed3c0153e
ms.lasthandoff: 02/23/2017


---
# <a name="create-a-lookout-device-threat-protection-rule"></a>Lookout デバイス脅威保護規則の作成

*適用対象: System Center Configuration Manager (Current Branch)*

## <a name="before-you-begin"></a>始める前に

Intune で Lookout モバイル脅威保護を利用すると、モバイルの脅威を検出し、デバイス上でリスク評価を行うことができます。 Configuration Manager でコンプライアンス ポリシー規則を作成して、デバイスがポリシーに準拠しているかどうかを判別するリスク評価を含めることができます。 次に条件付きアクセス ポリシーを使用して、デバイスのポリシー準拠に基づき、Exchange、SharePoint、およびその他のサービスへのアクセスを許可またはブロックすることができます。

Lookout のデバイス脅威検出がデバイスのコンプライアンス ポリシーに影響を与えるようにする方法は次のとおりです。

-   コンプライアンス ポリシーで、**デバイス脅威保護**規則を有効にする必要があります。

-   **Intune 管理者コンソール**の **[Lookout の状態]** ページの表示を **[アクティブ]** にする必要があります。 Lookout の統合をアクティブ化する方法の詳細については、[Intune での Lookout MTP 接続の有効化](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune)に関するページを参照してください。

コンプライアンス ポリシーにデバイス脅威保護規則を作成する前に、以下を行うことをお勧めします。

1.  [Lookout デバイス脅威保護でサブスクリプションを設定する](https://docs.microsoft.com/sccm/protect/deploy-use/set-up-your-subscription-with-lookout)

2.  [Intune で、Lookout 接続を有効にする](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune)

3.  [Lookout for Work アプリを構成する](https://docs.microsoft.com/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps)

>[!NOTE]
>コンプライアンス規則は、セットアップ完了後にのみ適用されます。

## <a name="to-create-a-device-threat-protection-rule"></a>デバイス脅威保護規則を作成するには

Lookout デバイス脅威保護のセットアップの一環として、[Lookout コンソール](https://aad.lookout.com)で各種脅威を高、中、および低レベルに分類するポリシーを作成しています。 Intune のコンプライアンス ポリシーでこの脅威レベルを使用して、許容される最大脅威レベルを設定します。

Lookout デバイス脅威保護規則を作成するには:

1.  Configuration Manager コンソールで、[**資産とコンプライアンス**] ワークスペースをクリックします。

2.  [**資産とコンプライアンス**] で、[**コンプライアンス ポリシー**] を展開します。

3.  [**コンプライアンス ポリシー**] を右クリックして、[**コンプライアンス ポリシーの作成**] を選択します。

4.  コンプライアンス ポリシーの名前を入力し、[**Configuration Manager クライアントなしで管理されるデバイスのコンプライアンス規則**] を選択します。

5.  コンプライアンス ポリシーを使用してプロビジョニングされる OS プラットフォームを選択します (Android 4.1 以降または iOS 8 以降)。

6.  [**ルール**] ページで、[**新規**] をクリックして準拠デバイスの規則を指定します。

7.  [**規則の追加**] ページで、次の情報で新しい規則を定義します。
    1.  条件: デバイス脅威保護の最大リスク レベル。
    
    2.  値: 値には次のいずれかを指定できます。
        1.  **なし (セキュリティ保護あり)**: これはセキュリティ上最も安全です。 デバイスに脅威があってはならないことを意味します。 いずれかのレベルの脅威が発見された場合、デバイスは非準拠として評価されます。
        2.  **低**: 低レベルの脅威のみが存在する場合、デバイスはポリシーに準拠していると評価されます。 中レベル以上の脅威が存在する場合、デバイスは非準拠のステータスに分類されます。
        3.  **中**: デバイスで発見された脅威が低または中レベルの場合、デバイスはポリシーに準拠していると評価されます。 高レベルの脅威が検出された場合、デバイスは非準拠と判定されます。
        4.  **高**: 最も安全性が低くなります。 このレベルでは基本的にすべての脅威レベルが許容されるため、役に立つのはこのソリューションをレポート目的で使用する場合のみです。

>[!IMPORTANT]
>Office 365 やその他のサービス向けに条件付きのアクセス ポリシーを作成する場合は、上記のコンプライアンス評価を考慮して、脅威が解消されるまでは会社のリソースへの非準拠デバイスのアクセスをブロックする必要があります。
