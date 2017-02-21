---
title: "System Center Configuration Manager と Microsoft Intune を使ったハイブリッド Windows デバイス管理のセットアップ | Microsoft Docs"
description: "System Center Configuration Manager と Microsoft Intune を使用して Windows デバイス管理を設定します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 76cb0c41865859fd410a187435d73c6a23b0c57e
ms.openlocfilehash: 7b53b094eeb1d59d052c63831eeab0e10edb5913


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使ったハイブリッド Windows デバイス管理のセットアップ

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager を Intune と共に使用して、Windows を実行しているデスクトップやノート PC、その他のデバイスをモバイル デバイスとして管理することができます。 Windows PC の自動登録を許可するように Azure Active Directory を設定することができます。 また、会社のポータル アプリを使用して登録を簡素化するように Configuration Manager を構成することもできます。


次のような Windows 登録のオプションが用意されています。

- [Azure AD での自動登録](#azure-active-directory-enrollment)
- [Windows PC](#set-up-windows-device-enrollment)
- [Windows 10 Mobile および Windows Phone デバイス](#enable-windows-phone-devices)

## <a name="azure-active-directory-enrollment"></a>Azure Active Directory 登録

自動登録を使用して、職場や学校のアカウントを追加し、管理されることに同意すると、会社所有のデバイスや個人の Windows 10 PC および Windows 10 Mobile デバイスを Intune に登録できます。 ユーザーのデバイスはバックグラウンドで登録され、Azure Active Directory に参加します。 登録されたデバイスは Intune で管理できるようになります。

**必要条件**
- Azure Active Directory Premium サブスクリプション ([試用版サブスクリプション](http://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune サブスクリプション


### <a name="configure-automatic-mdm-enrollment"></a>自動 MDM 登録の構成

1. [[Azure の管理ポータル]](https://manage.windowsazure.com) (https://manage.windowsazure.com) で、**[Active Directory]** ノードに移動して、ディレクトリを選択します。

2. **[アプリケーション]** タブをクリックすると、アプリケーションの一覧に **Microsoft Intune** が見つかります。

    ![Microsoft Intune が含まれる Azure AD アプリ](../media/aad-intune-app.png)

3. **[Microsoft Intune]** の矢印をクリックすると、Microsoft Intune を構成できるページが表示されます。

4. **[構成]** をクリックして、Microsoft Intune での自動 MDM 登録の構成を開始します。

5. Intune の URL を指定します。

  - **[MDM Enrollment URL (MDM 登録 URL)]** – 既定値を使用します。
  - **[MDM 使用条件 URL]** – 既定値を使用します。 この URL は、デバイスを登録するときにユーザーの使用条件を表示します。
  - **[MDM 準拠 URL]** – 既定値を使用します。 非準拠のデバイスが見つかった場合、この URL と共に **"アクセスが拒否されました"** というメッセージが表示されます。 この URL からアクセスできるページで、ユーザーは、自身のデバイスがポリシーに準拠していない理由と、ポリシーに準拠するための方法について理解することができます。

6.  Microsoft Intune で管理するユーザーのデバイスを指定します。 これらのユーザーの Windows 10 デバイスは、Microsoft Intune の管理対象として自動的に登録されます。

  - **すべて**
  - **グループ**
  - **なし**

7. **[保存]** を選択します。

## <a name="configure-windows-pc-enrollment"></a>Windows PC の登録の構成
 Windows モバイル デバイスの管理を有効にするには、オペレーティング システムの管理を有効にする必要があります。  DNS CNAME を追加してユーザーの登録を簡素化することもできます。

### <a name="create-dns-alias-for-device-enrollment"></a>デバイス登録の DNS エイリアスの作成  
 DNS エイリアス (CNAME レコード タイプ) を作成すると、デバイスの登録時にサーバー名が自動的に入力されるため、ユーザーがデバイスを簡単に登録できるようになります。 DNS エイリアス (CNAME レコード タイプ) を作成するには、Microsoft のクラウド サービスのサーバーに、会社のドメインの URL に送信された要求をリダイレクトする会社の DNS レコードで CNAME を構成する必要があります。  たとえば、会社の Web サイトが contoso.com の場合、EnterpriseEnrollment.contoso.com を EnterpriseEnrollment-s.manage.microsoft.com にリダイレクトする CNAME を DNS に作成する必要があります。  

 CNAME DNS エントリの作成は省略可能ですが、CNAME レコードにより、ユーザーによる登録が簡単になります。 CNAME レコードの登録が見つからない場合、ユーザーは手動で MDM サーバー名 enrollment.manage.microsoft.com を入力するように求められます。

|型|ホスト名|指定先|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  
### <a name="to-enable-enrollment-for-windows-devices"></a>Windows デバイスの登録の有効化  

1.  **前提条件** - 任意のプラットフォームの登録をセットアップする前に、「[ハイブリッド MDM をセットアップする](setup-hybrid-mdm.md)」の前提条件と手順を完了しておく必要があります。  

2.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]**  >  **[Microsoft Intune サブスクリプション]** に移動します。  

    > [!WARNING]  
    >  他の Configuration Manager のダイアログ ボックスが開いている場合は、閉じてからこの手順を続行してください。  

3.  **[ホーム]** タブで、 **[プラットフォームの構成]**、 **[Windows]**の順にクリックします。  

4.  **[全般]** タブで **[Windows の登録を有効にする]**を選択します。  

 セットアップが完了したら、デバイスを登録する方法をユーザーに知らせる必要があります。 「[デバイスの登録についてユーザーに通知する事柄](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)」に関する記事をご覧ください。 この情報は、Microsoft Intune と Configuration Manager の両方によって管理されるモバイル デバイスに適用されます。

## <a name="enable-windows-phone-devices"></a>Windows Phone デバイスの有効化  
  ユーザーが Windows Phone 8.1 以降のデバイスの登録のみを行い、Windows Phone デバイスに基幹業務アプリを展開しない場合は、Symantec 証明書は必要ありません。 Windows Phone の登録を有効にした後、ユーザーに Windows Phone ストアからポータル サイト アプリをインストールして使用デバイスを登録するよう指示する必要があります。  

  管理する Windows Phone デバイスで、次の手順を実行します。  

### <a name="to-enable-enrollment-for-windows-phone-81-and-later-devices"></a>Windows Phone 8.1 以降のデバイスの登録を有効にするには  

 1.  **前提条件** - 任意のプラットフォームの登録をセットアップする前に、「[ハイブリッド MDM をセットアップする](setup-hybrid-mdm.md)」の前提条件と手順を完了しておく必要があります。  

 2.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]**  >  **[Microsoft Intune サブスクリプション]** に移動します。  

     > [!WARNING]  
     >  他の Configuration Manager のダイアログ ボックスが開いている場合は、閉じてからこの手順を続行してください。  

 3.  **[ホーム]** タブで、 **[プラットフォームの構成]**、 **[Windows Phone]**の順にクリックします。  

 4.  **[全般]** タブで、  **[Windows Phone 8.1 と Windows 10 Mobile]**を選びます。 AET .xml ファイルのデータまたは .pfx ファイルをアップロードして、会社のポータルの展開をサポートしたり、Windows Phone ストアから会社のポータルをダウンロードするようにユーザーに指示したりできます。  

      **[OK]**をクリックします。  

  セットアップが完了したら、デバイスを登録する方法をユーザーに知らせる必要があります。 「[デバイスの登録についてユーザーに通知する事柄](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)」に関する記事をご覧ください。 この情報は、Microsoft Intune と Configuration Manager の両方によって管理されるモバイル デバイスに適用されます。  



<!--HONumber=Feb17_HO2-->


