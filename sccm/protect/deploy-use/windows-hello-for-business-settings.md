---
title: "Windows Hello for Business の設定 | System Center Configuration Manager"
description: "System Center Configuration Manager に Windows Hello for Business を統合する方法について説明します。"
ms.custom: na
ms.date: 10/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: 17
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2a45cfb3e00d8078fbf45bdc8a2668b7dd0a62c6
ms.openlocfilehash: 80f586763d034891aac9b87dcb38120602aa2b85


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager における Windows Hello for Business の設定

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager を、Windows 10 デバイスの代替サインイン方法である Windows Hello for Business (旧称: Microsoft Passport for Windows) と統合することができます。 Hello for Business では、パスワード、スマート カード、または仮想スマート カードの代わりに Active Directory または Azure Active Directory アカウントを使用します。  

Hello for Business を使用すると、パスワードの代わりに **ユーザー ジェスチャ** を使用してログインできます。 ユーザー ジェスチャには、単純な暗証番号 (PIN)、生体認証、または指紋リーダーなどの外部のデバイスがあります。  

 Configuration Manager と Windows Hello for Business を統合するには、次の 2 つの方法があります。  

-   Configuration Manager を使用して、ユーザーがサインインに使用できるジェスチャと使用できないジェスチャを制御できます。  

-   Windows Hello for Business のキー格納プロバイダー (KSP) に認証証明書を格納できます。 詳細については、「[Certificate profiles](introduction-to-certificate-profiles.md)」 (証明書プロファイル) をご覧ください。  

- ドメインに参加しており構成マネージャー クライアントを実行している Windows 10 デバイスに Windows Hello for Business ポリシーを展開できます。 この構成については、以下の「[ドメインに参加している Windows 10 デバイスで Windows Hello for Business を構成する](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices)」で説明されています。 Configuration Manager と Intune (ハイブリッド) を使用している場合、これらの設定は、Windows 10 デバイスと Windows 10 Mobile デバイスで構成できますが、ドメインに参加しており構成マネージャー クライアントを実行しているデバイスでは構成できません。   

## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Windows Hello for Business 設定を構成する (ハイブリッド)  

1.  Configuration Manager コンソールで、**[管理]** > **[Cloud Services]** > **[Microsoft Intune サブスクリプション]** の順にクリックします。  

3.  リストから、Microsoft Intune サブスクリプションを選び、 **[ホーム]** タブの **[サブスクリプション]** グループで、 **[プラットフォームの構成]** > **[Windows (MDM)]**をクリックします。  

4.  **[Microsoft Intune サブスクリプションのプロパティ]** ダイアログ ボックスの **[Windows Hello for Business]** タブで、登録されているすべての Windows 10 および Windows 10 Mobile デバイスに影響する次の値から選びます。  

    -   **[登録デバイスで Windows Hello for Business を無効にする]** または **[登録デバイスで Windows Hello for Business を有効にする]** - 登録されているすべての Windows 10 および Windows 10 Mobile デバイスで Windows Hello for Business の使用を有効または無効にします。  

    -   **トラステッド プラットフォーム モジュール (TPM) の使用** - トラステッド プラットフォーム モジュール (TPM) チップでは、追加のデータのセキュリティ層を提供します。 次のいずれかの値を選択します。  

        -   **必須** (既定) - アクセス可能な TPM を装備したデバイスのみが Windows Hello for Business をプロビジョニングできます。  

        -   **優先** -デバイスは最初に TPM を使用しようとします。 これが使用できない場合、ソフトウェアの暗号化を使用できます。  

    -   **PIN の最小長** - Windows Hello for Business の PIN に必要な文字の最小数を指定します。 少なくとも 4 文字を使用する必要があります (既定値は 6 文字)。  

    -   **PIN の最大長** - Windows Hello for Business の PIN に使用できる文字の最大数を指定します。 127 文字まで使用できます。  

    -   **PIN に小文字が必要** - Windows Hello for Business の PIN に小文字を使用する必要があるかどうかを指定します。 次の中から選択します。  

        -   **許可** -ユーザーは PIN に小文字を使用することができます。  

        -   **必須** -ユーザーは PIN に小文字を 1 文字以上含める必要があります。  

        -   **使用不可** (既定) -ユーザーは PIN に小文字を使用することができません。  

    -   **PIN に大文字が必要** - Windows Hello for Business の PIN に大文字を使用する必要があるかどうかを指定します。 次の中から選択します。  

        -   **許可** -ユーザーは PIN に大文字を使用することができます。  

        -   **必須** -ユーザーは PIN に大文字を 1 文字以上含める必要があります。  

        -   **使用不可** (既定) -ユーザーは PIN に大文字を使用することができません。  

    -   **特殊文字が必要** - PIN の特殊文字の使用を指定します。 次の中から選択します。  

        -   **許可** -ユーザーは PIN に特殊文字を使用することができます。  

        -   **必須** -ユーザーは PIN に特殊文字を 1 文字以上含める必要があります。  

        -   **使用不可** (既定) -ユーザーは PIN に特殊文字を使用することができません (これは、設定を構成していない場合の動作でもあります)。  

         特殊文字には次のものが含まれます: **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**  

    -   **PIN の有効期限が必要 (日)** - PIN の変更が必要になるまでの日数を指定します。 既定は 41 日です。  

    -   **前の PIN の再利用を防止** - この設定を使用すると、以前に使用した PIN の再利用を制限できます。 既定では過去 5 回の PIN を再利用することはできません。  

    -   **生体認証のジェスチャを有効にする** - Windows Hello for Business の PIN の代わりとして、顔認識や指紋などの生体認証を有効にします。 ユーザーは、生体認証に失敗した場合のために、Work の PIN も設定する必要があります。  

         **[有効]**に設定されている場合は、Windows Hello for Business で生体認証が利用できます。  **[無効]**に設定されている場合は、Windows Hello for Business で生体認証が利用できません (すべてのアカウントの種類が対象)。  

    -   **拡張スプーフィング対策が使用可能な場合は使用する** - デバイスでサポートされている場合に拡張スプーフィング対策を使用するかどうかを構成します。  

         **[有効]**に設定されている場合、Windows のすべてのユーザーは、サポートされている場合に顔の特徴のスプーフィング対策を使用する必要があります。  

    -   **リモートの Passport を使用する** - このオプションが **[有効]**に設定されている場合、ユーザーはデスクトップ コンピューターの認証にポータブル コンパニオン デバイスとして機能するリモートの Hello for Business を使用することができます。 デスクトップ コンピューターは Azure Active Directory に参加している必要があり、コンパニオン デバイスは、Windows Hello for Business の PIN を使用して設定されている必要があります。  

5.  操作が完了したら、 **[OK]**をクリックします。  


## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>ドメインに参加している Windows 10 デバイスで Windows Hello for Business を構成する
ドメインに参加している Windows 10 デバイスの Windows Hello for Business 設定は、次の 3 つの方法で制御できます。

- Windows Hello for Business プロファイルを作成して展開することができます。 これは、推奨される方法です。
- グループ ポリシーを使用できます。  
- PowerShell スクリプトを使用できます。

この構成に加えて、「[証明書プロファイルの構成](#configure-a-certificate-profile)」で説明されているように、証明書プロファイルも展開する必要があります。

### <a name="recommended-approach---configure-a-windows-hello-for-business-profile"></a>推奨される方法 - Windows Hello for Business プロファイルの構成  

管理コンソールの **[会社のリソースへのアクセス]** で、**[Windows Hello for Business プロファイル]** を右クリックし、**[新規]** を選択してプロファイル ウィザードを開始します。 ウィザードによって要求された設定を指定し、最後のページで設定を確認して、**[閉じる]** をクリックします。 設定の例を次に示します。  

![Windows Hello for Business の設定](../media/Hello-for-Business-settings.png)

### <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>Active Directory のグループ ポリシーを使用して Windows Hello for Business を構成する  

Active Directory のグループ ポリシーを使用して、ユーザーが Windows にログインするときに、そのユーザーの Hello for Business 資格情報をプロビジョニングするように Windows 10 ドメイン参加デバイスを構成できます。

1.  Windows Server コンピューターでサーバー マネージャーを開き、**[ツール]** > **[グループ ポリシー管理]** に移動します。    

2.  **[グループ ポリシー管理]** ダイアログ ボックスで、Automatic Workplace Join を有効にするドメインを展開します。    

3.  **[グループ ポリシー オブジェクト]**を右クリックして、 **[新規]**をクリックします。  

4.  **[新しい GPO]** ダイアログ ボックスに、新しいグループ ポリシー オブジェクトの名前 (**Windows Hello for Business を有効にする**など) を入力して、**[OK]** をクリックします。  

5.  **[グループ ポリシー オブジェクト]** ノードで、作成したオブジェクトを右クリックし、 **[編集]**をクリックします。  

6.  **[グループ ポリシー管理エディター]** ダイアログ ボックスで、**[コンピューターの構成]** > **[ポリシー]** > **[管理用テンプレート]** > **[Windows コンポーネント]** > **[Windows Hello for Business]** の順に移動します。  

7.  **[Windows Hello for Business を有効にする]** を右クリックし、**[編集]** をクリックします。   

8.  **[有効]**を選び、 **[適用]**をクリックし、 **[OK]**をクリックします。

作成したグループ ポリシー オブジェクトを任意の場所にリンクできます。 たとえば、    

   Windows 10 ドメイン参加コンピューターが配置される AD の特定の組織単位 (OU)。    

   Azure AD に自動的に登録される Windows 10 ドメイン参加コンピューターを含む特定のセキュリティ グループ。    

#### <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>Configuration Manager で PowerShell スクリプトを展開して Windows Hello for Business を構成する    
Configuration Manager アプリケーション管理を使用して、次の PowerShell スクリプトを作成して展開できます。    

```    
powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}"  
```  

Configuration Manager アプリケーション管理の詳細については、「[System Center Configuration Manager でのアプリケーション管理の概要](/sccm/apps/understand/introduction-to-application-management)」をご覧ください。  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configuration Manager で証明書プロファイルを構成して、Windows Hello for Business の登録証明書を登録する  
 Windows Hello for Business の証明書ベースのログオンまたは Microsoft Hello を使用する場合は、次の構成を行います。  

-   Configuration Manager の証明書プロファイル。  

-   証明書プロファイルで、スマート カード ログオンの EKU を使用するテンプレートを選びます。  

 詳細については、「[Certificate profiles](introduction-to-certificate-profiles.md)」 (証明書プロファイル) をご覧ください。  

### <a name="see-also"></a>関連項目  
 [System Center Configuration Manager でのデータとサイト インフラストラクチャの保護](../../protect/understand/protect-data-and-site-infrastructure.md)

 [Windows Hello for Business を使用した本人確認の管理](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport)  



<!--HONumber=Nov16_HO1-->


