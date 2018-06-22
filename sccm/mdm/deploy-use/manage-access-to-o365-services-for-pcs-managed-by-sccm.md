---
title: O365 サービスへのアクセスの管理
titleSuffix: Configuration Manager
description: System Center Configuration Manager で管理されている PC の Office 365 サービスへの条件付きアクセスを構成する方法について説明します。
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bf7114382c956dcac6302b3fc11617ad6b5eeec
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350376"
---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>System Center Configuration Manager で管理されている PC の O365 サービスへのアクセスを管理する

*適用対象: System Center Configuration Manager (Current Branch)*

<!--1191496-->
Configuration Manager で管理されている PC の Office 365 サービスへ条件付きアクセスを構成する方法について説明します。  

> [!Note]  
> Configuration Manager では、このオプション機能は既定で無効です。 この機能は、使用する前に有効にする必要があります。 詳細については、「[更新プログラムのオプション機能の有効化](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」を参照してください。<!--505213-->  


Microsoft Intune で登録および管理されるデバイスの条件付きアクセスの構成については、「[System Center Configuration Manager でサービスへのアクセスを管理する](../../protect/deploy-use/manage-access-to-services.md)」を参照してください。 その記事では、ドメインに参加しているデバイスのうち、コンプライアンス評価対象でないデバイスについても説明します。

## <a name="supported-services"></a>サポートされているサービス  

-   Exchange Online
-   SharePoint Online

## <a name="supported-pcs"></a>サポートされている PC  

-   Windows 7
-   Windows 8.1
-   Windows 10

## <a name="supported-windows-servers"></a>サポートされている Windows サーバー

-   Windows Server 2008 R2
-   Windows Server 2012
-   Windows Server 2012 R2
-   Windows Server 2016

    > [!IMPORTANT]
    > 複数のユーザーが同時にサインインしている可能性のある Windows サーバーについては、サインインしているすべてのユーザーに同じ条件付きアクセス ポリシーを展開してください。

## <a name="configure-conditional-access"></a>条件付きアクセスの構成  
 条件付きアクセスをセットアップするには、最初にコンプライアンス ポリシーを作成して、条件付きアクセス ポリシーを構成する必要があります。 PC の条件付きアクセス ポリシーを構成する場合、Exchange Online サービスと SharePoint Online サービスにアクセスするには PC が準拠するよう要求することができます。  

### <a name="prerequisites"></a>[前提条件]  

-   ADFS の同期と O365 サブスクリプション。 O365 サブスクリプションは、Exchange Online と SharePoint Online のセットアップのためのものです。  

-   Microsoft Intune サブスクリプション。 Microsoft Intune サブスクリプションは、Configuration Manager コンソールで構成される必要があります。 Azure Active Directory にデバイスのコンプライアンス対応状態を中継するために、また、ユーザー ライセンスのために、Intune サブスクリプションが使用されます。  

 PC は、次の要件を満たす必要があります。  

-   Azure Active Directory への自動デバイス登録の[前提条件](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)   

     コンプライアンス ポリシーに基づいて Azure AD に PC を登録できます。  

    -   Windows 8.1 と Windows 10 の PC では、Active Directory グループ ポリシーを使用して、Azure AD に自動的に登録するデバイスを構成することができます。  

    -   Windows 7 の PC の場合には、System Center Configuration Manager を利用して Windows 7 PC にデバイス登録ソフトウェア パッケージを展開する必要があります。 詳細については、「[Azure Active Directory への Windows ドメイン参加済みデバイスの自動デバイス登録](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)」記事を参照してください。  

-   先進認証が [有効になっている](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)Office 2013 または Office 2016 を使用する必要があります。  

 次の手順は、Exchange Online と SharePoint Online の両方に適用されます。  

### <a name="step-1-configure-compliance-policy"></a>手順 1. コンプライアンス ポリシーの構成  
 Configuration Manager コンソールで、次の規則を含むコンプライアンス ポリシーを作成します。  

-   **Azure Active Directory への登録が必要:** この規則では、ユーザーのデバイスが Azure AD に社内参加しているかどうかを確認し、参加していない場合には Azure AD に自動的に登録します。 自動登録がサポートされているのは Windows 8.1 のみです。 Windows 7 PC の場合には、MSI を展開して自動登録を実行します。 詳細については、[Azure Active Directory への自動デバイス登録](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)に関するページを参照してください。  

-   **All required updates installed with a deadline older than a certain number of days (期限よりも特定の日数前に必要な更新プログラムをすべてインストールする):** この規則では、ユーザーのデバイス上で必要な更新プログラムについて、展開期限からの猶予期間の値を指定します。 この規則を追加すると、保留中の必要な更新プログラムも自動的にインストールされます。 **必須の自動更新**規則で、必要な更新プログラムを指定します。   

-   **BitLocker ドライブ暗号化が必要:** この規則では、デバイスのプライマリ ドライブ (C:\\ など) が BitLocker で暗号化されているかどうかを確認します。 Bitlocker 暗号化がプライマリ デバイスで有効でない場合、電子メール サービスおよび SharePoint サービスへのアクセスがブロックされます。  

-   **マルウェア対策が必要:** この規則では、System Center Endpoint Protection または Windows Defender が有効で実行されているかどうかを確認します。 無効な場合、電子メール サービスおよび SharePoint サービスへのアクセスがブロックされます。  

-   **正常性構成証明サービスにより、正常であると報告されました:** この条件には、デバイス正常性構成証明書サービスに対するデバイスのコンプライアンスを確認するための 4 つのサブ規則が含まれます。 詳細については、[正常性構成証明書](/sccm/core/servers/manage/health-attestation)に関するページを参照してください。 

    - **デバイス上で BitLocker の有効化が必要**
    - **デバイス上でセキュア ブートの有効化が必要** 
    - **デバイス上でコードの整合性の有効化が必要**
    - **デバイス上で起動時マルウェア対策の有効化が必要**  

    >[!Tip]  
    > デバイス正常性構成証明書の条件付きアクセス条件は、最初にバージョン 1710 で[プレリリース機能](/sccm/core/servers/manage/pre-release-features)として導入されました。 バージョン 1802 以降、この機能はプレリリース機能ではなくなりました。<!--1235616-->  

    > [!Note]  
    > Configuration Manager では、このオプション機能は既定で無効です。 この機能は、使用する前に有効にする必要があります。 詳細については、「[更新プログラムのオプション機能の有効化](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」を参照してください。<!--505213-->  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>手順 2. 条件付きアクセスの効果の評価  
 **条件付きアクセス コンプライアンス レポート**を実行します。 これは **[レポート]** > **[コンプライアンスと設定の管理]** の **[監視]** ワークスペースにあります。 このレポートには、すべてのデバイスのコンプライアンス対応状態が表示されます。 非対応としてレポートされるデバイスから Exchange Online および SharePoint Online へのアクセスはブロックされます。  

 ![Configuration Manager コンソール、監視ワークスペース、レポート、コンプライアンスと設定の管理: 条件付きアクセス コンプライアンス レポート](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Active Directory セキュリティ グループの構成  
 条件付きアクセス ポリシーは、ポリシーの種類に応じてユーザーのグループを対象とします。 これらのグループには、ポリシーの対象となるユーザーや、ポリシーから除外されるユーザーが含まれます。 ポリシーの対象がユーザーである場合、使用される各デバイスがサービスにアクセスするには、ポリシーに準拠している必要があります。  

 Active Directory セキュリティ ユーザー グループ。 これらのユーザー グループは、Azure Active Directory に同期される必要があります。 これらのグループを Office 365 管理センターまたは Intune アカウント ポータルで構成することもできます。  

 各ポリシーには、次の 2 つのグループの種類を指定できます。 :  

-   **対象グループ** – ポリシーが適用されるユーザー グループ。 コンプライアンスと条件付きアクセス ポリシーの両方に同じグループを使用してください。  

-   **例外グループ** – ポリシーから除外されるユーザー グループ (省略可能)。  
    ユーザーが両方に含まれている場合は、ポリシーから除外されます。  

     条件付きアクセス ポリシーの対象となるグループだけが評価されます。  

### <a name="step-3-create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>手順 3. Exchange Online および SharePoint Online の条件付きアクセス ポリシーを作成します。  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** をクリックします。  

2.  Exchange Online のポリシーを作成するには、 **[Exchange Online の条件付きアクセス ポリシーを有効にする]** を選びます。  

     SharePoint Online のポリシーを作成するには、 **[Exchange Online の条件付きアクセス ポリシーを有効にする]** を選びます。  

3.  **[ホーム]** タブの **[リンク]** グループで、**[Intune コンソールでの条件付きアクセス ポリシーの構成]** をクリックします。 Configuration Manager を Intune に接続するために使用されるアカウントのユーザー名とパスワードを指定する必要がある場合があります。  

     Intune 管理コンソールが開きます。  

4.  Exchange Online の場合は、Microsoft Intune の管理コンソールで **[ポリシー] > [条件付きアクセス] > [Exchange Online ポリシー]** をクリックします。  

     SharePoint Online の場合は、Microsoft Intune の管理コンソールで **[ポリシー] > [条件付きアクセス] > [SharePoint Online ポリシー]** をクリックします。  

5.  Windows PC の要件を **[デバイスは準拠デバイスである必要があります]** オプションに設定します。  

6.  **[対象グループ]** で、**[変更]** をクリックして、ポリシーを適用する Azure Active Directory セキュリティ グループを選択します。  

    > [!NOTE]  
    >  コンプライアンス ポリシーの展開と条件付きアクセス ポリシーの対象グループに同じセキュリティ ユーザー グループを使用してください。  

     **[例外グループ]** で、必要に応じて **[変更]** をクリックして、このポリシーから除外する Azure Active Directory セキュリティ グループを選択します。  

7.  **[保存]** をクリックしてポリシーを作成および保存します  

ユーザーはソフトウェア センターでコンプライアンス情報を表示します。 非準拠であるためブロックされた場合は、コンプライアンスの問題を修正してから新しいポリシーの評価を開始してください。  


## <a name="see-also"></a>関連項目

- [System Center Configuration Manager でのデータとサイト インフラストラクチャの保護](../../protect/understand/protect-data-and-site-infrastructure.md)
- [Configuration Manager の条件付きアクセスによるトラブルシューティング フローチャート](https://gallery.technet.microsoft.com/Conditional-access-fd747c1a?redir=0)
