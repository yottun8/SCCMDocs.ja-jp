---
title: Windows Hello for Business の設定
titleSuffix: Configuration Manager
description: Windows こんにちは for Business と Configuration Manager を統合する方法について説明します。
ms.date: 12/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c0593c07-5dd7-4d23-a0d8-d30165f49ef7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f403fc8c83b93c91a1d648b194e2da1c82133fe2
ms.sourcegitcommit: 94bf7d5b5beb9628cc1fdfe75451d33b5de26f8a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2019
ms.locfileid: "54152419"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager-hybrid"></a>Windows Hello for Business の設定で Configuration Manager (ハイブリッド)

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager では、Windows こんにちは for Business (旧称 Microsoft Passport for Windows)、Windows 10 デバイスの代替サインイン方法であるとを統合することができます。 Hello for Business では、パスワード、スマート カード、または仮想スマート カードの代わりに Active Directory または Azure Active Directory アカウントを使用します。 Hello for Business を使用すると、パスワードの代わりに **ユーザー ジェスチャ** を使用してログインできます。 ユーザー ジェスチャには、単純な暗証番号 (PIN)、生体認証、または指紋リーダーなどの外部のデバイスがあります。  

> [!Important]  
> 2017 年 12 月の時点で Windows こんにちは for Business の設定の構成マネージャーでは、[非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)します。 Windows Server 2016 Active Directory フェデレーション サービス登録機関 (ADFS RA) 展開は、方が簡単です、優れたユーザー エクスペリエンスを提供およびより明確な証明書の登録エクスペリエンスを備えています。 詳細については、「[Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)」を参照してください。  


Configuration Manager と Windows Hello for Business を統合するには、次の 2 つの方法があります。  

- Configuration Manager を使用して、ユーザーがサインインに使用できるジェスチャと使用できないジェスチャを制御できます。  

- Windows Hello for Business のキー格納プロバイダー (KSP) に認証証明書を格納できます。 詳細については、「[Certificate profiles](create-pfx-certificate-profiles.md)」 (証明書プロファイル) をご覧ください。  

- ドメインに参加しており構成マネージャー クライアントを実行している Windows 10 デバイスに Windows Hello for Business ポリシーを展開できます。 この構成については、「[ドメインに参加している Windows 10 デバイスで Windows Hello for Business を構成する](/sccm/protect/deploy-use/windows-hello-for-business-settings#configure-windows-hello-for-business-on-domain-joined-windows-10-devices)」で説明されています。 Configuration Manager と Intune (ハイブリッド) を使用している場合、これらの設定は、Windows 10 デバイスと Windows 10 Mobile デバイスで構成できますが、ドメインに参加しており構成マネージャー クライアントを実行しているデバイスでは構成できません。   

構成の詳細について Windows こんにちは for Business の設定の概要については、次を参照してください。 [Windows Hello for Business 設定の構成マネージャーで](/sccm/protect/deploy-use/windows-hello-for-business-settings)します。



## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Windows Hello for Business 設定を構成する (ハイブリッド)  

1. Configuration Manager コンソールで、**[管理]** > **[Cloud Services]** > **[Microsoft Intune サブスクリプション]** の順にクリックします。  

2. リストから、Microsoft Intune サブスクリプションを選び、 **[ホーム]** タブの **[サブスクリプション]** グループで、 **[プラットフォームの構成]** > **[Windows (MDM)]** をクリックします。  

3. **[Microsoft Intune サブスクリプションのプロパティ]** ダイアログ ボックスの **[Windows Hello for Business]** タブで、登録されているすべての Windows 10 および Windows 10 Mobile デバイスに影響する次の値から選びます。  

   - **[登録デバイスで Windows Hello for Business を無効にする]** または **[登録デバイスで Windows Hello for Business を有効にする]** - 登録されているすべての Windows 10 および Windows 10 Mobile デバイスで Windows Hello for Business の使用を有効または無効にします。  

   - **トラステッド プラットフォーム モジュール (TPM) の使用** - トラステッド プラットフォーム モジュール (TPM) チップでは、追加のデータのセキュリティ層を提供します。 次のいずれかの値を選択します。  

     -   **必須** (既定) - アクセス可能な TPM を装備したデバイスのみが Windows Hello for Business をプロビジョニングできます。  

     -   **優先** -デバイスは最初に TPM を使用しようとします。 これが使用できない場合、ソフトウェアの暗号化を使用できます。  

   - **PIN の最小長** - Windows Hello for Business の PIN に必要な文字の最小数を指定します。 少なくとも 4 文字を使用する必要があります (既定値は 6 文字)。  

   - **PIN の最大長** - Windows Hello for Business の PIN に使用できる文字の最大数を指定します。 127 文字まで使用できます。  

   - **PIN に小文字が必要** - Windows Hello for Business の PIN に小文字を使用する必要があるかどうかを指定します。 次の中から選択します。  

     -   **許可** -ユーザーは PIN に小文字を使用することができます。  

     -   **必須** -ユーザーは PIN に小文字を 1 文字以上含める必要があります。  

     -   **使用不可** (既定) -ユーザーは PIN に小文字を使用することができません。  

   - **PIN に大文字が必要** - Windows Hello for Business の PIN に大文字を使用する必要があるかどうかを指定します。 次の中から選択します。  

     -   **許可** -ユーザーは PIN に大文字を使用することができます。  

     -   **必須** -ユーザーは PIN に大文字を 1 文字以上含める必要があります。  

     -   **使用不可** (既定) -ユーザーは PIN に大文字を使用することができません。  

   - **特殊文字が必要** - PIN の特殊文字の使用を指定します。 次の中から選択します。  

     - **許可** -ユーザーは PIN に特殊文字を使用することができます。  

     - **必須** -ユーザーは PIN に特殊文字を 1 文字以上含める必要があります。  

     - **使用不可** (既定) -ユーザーは PIN に特殊文字を使用することができません (これは、設定を構成していない場合の動作でもあります)。  

       特殊文字には次のものが含まれます。**! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**  

   - **PIN の有効期限が必要 (日)** - PIN の変更が必要になるまでの日数を指定します。 既定は 41 日です。  

   - **前の PIN の再利用を防止** - この設定を使用すると、以前に使用した PIN の再利用を制限できます。 既定では過去 5 回の PIN を再利用することはできません。  

   - **生体認証のジェスチャを有効にする** - Windows Hello for Business の PIN の代わりとして、顔認識や指紋などの生体認証を有効にします。 ユーザーは、生体認証に失敗した場合のために、Work の PIN も設定する必要があります。  

      **[有効]** に設定されている場合は、Windows Hello for Business で生体認証が利用できます。  **[無効]** に設定されている場合は、Windows Hello for Business で生体認証が利用できません (すべてのアカウントの種類が対象)。  

   - **拡張スプーフィング対策が使用可能な場合は使用する** - デバイスでサポートされている場合に拡張スプーフィング対策を使用するかどうかを構成します。  

      **[有効]** に設定されている場合、Windows のすべてのユーザーは、サポートされている場合に顔の特徴のスプーフィング対策を使用する必要があります。  

   - **リモートの Passport を使用する** - このオプションが **[有効]** に設定されている場合、ユーザーはデスクトップ コンピューターの認証にポータブル コンパニオン デバイスとして機能するリモートの Hello for Business を使用することができます。 デスクトップ コンピューターは Azure Active Directory に参加している必要があり、コンパニオン デバイスは、Windows Hello for Business の PIN を使用して設定されている必要があります。  

4. 操作が完了したら、 **[OK]** をクリックします。  



## <a name="see-also"></a>関連項目  

[データとサイト インフラストラクチャを保護します。](/sccm/protect/understand/protect-data-and-site-infrastructure)

[Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)  
