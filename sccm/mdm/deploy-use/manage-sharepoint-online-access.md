---
title: SharePoint Online アクセスの管理
titleSuffix: Configuration Manager
description: System Center Configuration Manager の SharePoint Online 条件付きアクセスを使用して OneDrive へのアクセスを管理する方法について説明します。
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f723110abdb94dd96fb2ed7f52af681d27fccf87
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>System Center Configuration Manager での SharePoint Online アクセスの管理

*適用対象: System Center Configuration Manager (Current Branch)*


**SharePoint Online** の Configuration Manager 条件付きアクセス ポリシーにより、SharePoint Online に格納されている、OneDrive for Business ファイルへのアクセスが管理されます。 アクセスは指定した条件に基づきます。
前述のプラットフォームでは、次のアプリケーションから SharePoint Online へのアクセスを制御できます。  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android および iOS)  

-   Microsoft Word (Android および iOS)  

-   Microsoft Excel (Android および iOS)  

-   Microsoft PowerPoint (Android および iOS)  

-   Microsoft OneNote (Android および iOS)

以下を実行している PC で、Office デスクトップ アプリケーションから SharePoint Online にアクセスできます。  

-   [最新の認証](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) が有効にされた Office デスクトップ 2013 以降。  

-   Windows 7.0 または Windows 8.1  

> [!NOTE]  
>  PC はドメインに参加しているか、Intune で設定されたポリシーに準拠している必要があります。  



 対象となるユーザーが、デバイスで OneDrive などのサポートされているアプリを使用してファイルに接続しようとすると、次の評価が発生します。  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 必要なファイルに接続するには、OneDrive を実行するデバイスに次の条件が必要です。  

-   Microsoft Intune に登録されているか、ドメインに参加する PC である。  

-   Azure Active Directory (Azure AD) にデバイスを登録します。 デバイスが Intune に登録されている場合、この登録は自動的に行われます。  

     ドメインに参加する PC の場合、Azure AD に[自動的に登録](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)するように設定する必要があります。  

-   展開されているすべての Configuration Manager コンプライアンス ポリシーを遵守している。  

    Azure AD にデバイスの状態が格納されます。 指定した条件に基づいて、ファイルへのアクセスが許可またはブロックされます。  

    条件が満たされない場合、ユーザーにはログイン時に以下のいずれかのメッセージが表示されます。  

-   デバイスが Intune または Azure AD に登録されていない場合は、会社ポータルのアプリをインストールして登録する方法についての手順が示されたメッセージが表示されます。  

-   デバイスが準拠していない場合は、Intune Web ポータルにユーザーを誘導するメッセージが表示されます。 そこで問題とその修復方法に関する情報を確認することができます。  

- モバイル デバイスの場合:

  **iOS** および **Android** デバイスのブラウザーからアクセスされるときの SharePoint Online へのアクセスを制限することができます。 アクセスは、準拠デバイスの、サポートされる以下のブラウザーからのみが許可されています。  
    - Safari (iOS)
    - Chrome (Android)
    - 管理対象ブラウザー (iOS と Android)  

    サポートされていないブラウザーはブロックされます。  

-   PC の場合:  


    -   ドメインへの参加を要求するようにポリシーが設定されており、PC がドメインに参加していない場合、IT 管理者に連絡するようにメッセージが表示されます。  

    -   ドメインへの参加または準拠を要求するようにポリシーが設定されており、PC がいずれかの要件を満たしていない場合、ポータル サイト アプリをインストールして登録する方法についての手順が示されたメッセージが表示されます。  

次のアプリから SharePoint Online へのアクセスをブロックできます。  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android および iOS)  

-   Microsoft Word (Android および iOS)  

-   Microsoft Excel (Android および iOS)  

-   Microsoft PowerPoint (Android および iOS)  

-   Microsoft OneNote (Android および iOS)  



## <a name="configure-conditional-access-for-sharepoint-online"></a>SharePoint の条件付きアクセスを構成する  

### <a name="step-1-configure-active-directory-security-groups"></a>手順 1. Active Directory セキュリティ グループを構成する  
 開始する前に、条件付きアクセス ポリシーの Azure AD セキュリティ グループを構成します。 これらのグループは、 **Office 365 管理センター**または **Intune アカウント ポータル**で構成できます。 これらのグループには、ポリシーの対象となるユーザーや、ポリシーから除外されるユーザーが含まれます。 ユーザーがポリシーの対象となる場合、ユーザーに使用される各デバイスがリソースにアクセスするには、ポリシーに準拠している必要があります。  

 SharePoint Online ポリシーには、次の 2 つのグループの種類を指定できます。  

-   **対象グループ**: ポリシーが適用されるユーザーのグループが含まれます。  

-   **例外グループ**: ポリシーから除外されるユーザーのグループが含まれるます (省略可能)。  

 ユーザーが両方のグループに含まれている場合は、ポリシーから除外されます。  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>手順 2:コンプライアンス ポリシーを構成し展開する  
 コンプライアンス ポリシーを作成して、SharePoint Online ポリシーの対象となるすべてのデバイスに展開します。  

> [!NOTE]   
>  コンプライアンス ポリシーは Intune グループ、または Configuration Manager コレクションに展開されますが、条件付きアクセス ポリシーは Azure AD セキュリティ グループを対象とします。  

 コンプライアンス ポリシーを構成する方法の詳細については、「[System Center Configuration Manager でのデバイス コンプライアンス ポリシーの管理](../../protect/deploy-use/device-compliance-policies.md)」を参照してください。  

> [!IMPORTANT]  
>  コンプライアンス ポリシーを展開していない状態で、SharePoint Online ポリシーを有効にすると、すべての対象デバイスにアクセスが許可されます。  

   

###  <a name="BKMK_OneDrive"></a> 手順 3: SharePoint Online ポリシーを構成する  

 次に、管理デバイスおよび準拠デバイスのみが SharePoint Online にアクセスできるように要求するポリシーを構成します。 このポリシーは Azure AD に格納されます。

 >[!NOTE]
 >Azure AD 管理コンソールで条件付きアクセス ポリシーを作成することもできます。 Azure AD 管理コンソールでは、Intune デバイスの条件付きアクセス ポリシーを作成することができます。 Azure AD では、これらのポリシーはデバイス ベースの条件付きアクセス ポリシーと呼ばれています。 多要素認証などの、他の条件付きアクセス ポリシーを作成することもできます。 ポータルで、Salesforce や Box など、Azure AD でサポートされるサード パーティ製エンタープライズ アプリ用の条件付きアクセス ポリシーを設定することができます。 詳細については、[Azure AD に接続されたアプリケーションのアクセスを制御する Azure AD デバイス ベースの条件付きアクセス ポリシーを設定する方法](/azure/active-directory/active-directory-conditional-access-policy-connected-applications)に関するページを参照してください。  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** をクリックします。  

2.  **[SharePoint Online の条件付きアクセス ポリシーを有効にする]** を選択します。  

     ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3.  Outlook、および先進認証を使用するアプリの **[アプリケーション アクセス]** で、各プラットフォームの準拠デバイスのみにアクセスを制限することを選択できます。  

    > [!TIP]  
    >  **先進認証**では、Active Directory Authentication Library (ADAL) ベースのサインインが Office クライアントに提供されます。  
    >   
    >  -   ADAL ベースの認証を使用すると、Office クライアントでブラウザー ベースの認証 (パッシブ認証ともいう) を利用できます。 認証する際に、ユーザーはサインイン Web ページに転送されます。  
    > -   この新しいサインイン方法では、**デバイスのコンプライアンス**と、**多要素認証**が実行されたかどうかに基づいて、条件付きのアクセスなどの新しいシナリオを実現できます。  
    >   
    >  詳細については、「[Office 2013 クライアント アプリと Office 2016 クライアント アプリでの先進認証のしくみ](https://support.office.com/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517)」を参照してください。  

     Windows PC の場合は、ドメインに参加しているか、Intune に登録され、ポリシーに準拠している必要があります。 以下の要件を設定できます。  

    -   **デバイスはドメインに参加しているか準拠デバイスである必要があります**: PC はドメインに参加しているか、Intune に設定されたポリシーに準拠している必要があります。 PC がどちらの要件も満たさない場合、ユーザーはデバイスを Intune に登録するように求められます。  

    -   **デバイスはドメインに参加している必要があります**: PC は Exchange Online にアクセスするために、ドメインに参加する必要があります。 PC がドメインに参加していない場合、電子メールへのアクセスはブロックされ、ユーザーは IT 管理者に連絡するように求められます。  

    -   **デバイスは準拠デバイスである必要があります**: PC は Intune に登録され、ポリシーに準拠している必要があります。 PC が登録されていない場合は、登録方法についての手順を示したメッセージが表示されます。  

4.  SharePoint Online および OneDrive for Business への**ブラウザー アクセス**で、サポートされるブラウザーである Safari (iOS) および Chrome (Android) による Exchange Online へのアクセスのみ許可することができます。 その他のブラウザーからのアクセスはブロックされます。 OneDrive のアプリケーション アクセス用に選択した、同じプラットフォーム制限もここで適用されます。

    **Android** デバイスの場合、ユーザーは登録されたデバイスで、以下のように **[ブラウザー アクセスを有効にする]** オプションを有効にする必要があります。
    1.  **ポータル サイト アプリ**を起動します。
    2.  トリプル ドット (...) またはハードウェアのメニュー ボタンから、 **[設定]** ページに移動します。
    3.  **[ブラウザー アクセスを有効にする]** ボタンを押します。
    4.  Chrome ブラウザーでは、Office 365 からサインアウトし、Chrome を再起動します。

    **iOS および Android** プラットフォームでは、サービスへのアクセスに使用するデバイスを特定するために、Azure AD によって TLS 証明書がデバイスに対して発行されます。 デバイスには、次のスクリーンショットのように、エンド ユーザーに証明書の選択を求めるプロンプトとともに証明書が表示されます。エンド ユーザーが、ブラウザーを引き続き使用するには、この証明書を選択する必要があります。

     **iOS**

     ![iPad での証明書プロンプトのスクリーンショット](media/mdm-browser-ca-ios-cert-prompt_v2.png)

     **Outlook Web Access (OWA)**

      ![Android デバイスでの証明書プロンプトのスクリーンショット](media/mdm-browser-ca-android-cert-prompt.png)

4.  **[ホーム]** タブの **[リンク]** グループで、**[Intune コンソールでの条件付きアクセス ポリシーの構成]** をクリックします。 Configuration Manager を Intune に接続するために使用されるアカウントのユーザー名とパスワードを指定する必要がある場合があります。  

     Intune 管理コンソールが開きます。  

5.  [Microsoft Intune 管理コンソール](https://manage.microsoft.com)で、**[ポリシー]** > **[条件付きアクセス]** > **[SharePoint Online ポリシー]** の順にクリックします。  

6.  **[デバイスが準拠していない場合は、アプリの SharePoint Online へのアクセスをブロックする]** を選択します。  

7.  **[対象グループ]** で、**[変更]** をクリックして、ポリシーを適用する Azure AD セキュリティ グループを選択します。  

8.  **[例外グループ]** で、必要に応じて **[変更]** をクリックして、このポリシーから除外する Azure AD セキュリティ グループを選択します。  

9. 終了したら、 **[保存]** をクリックします。  

 条件付きアクセス ポリシーを展開する必要はありません。すぐに有効になります。  

 Intune コンソールからポリシーを管理する方法の詳細については、「[Microsoft Intune を使用した SharePoint Online アクセスの管理](/intune-classic/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)」を参照してください。  

### <a name="see-also"></a>関連項目  

 [System Center Configuration Manager でサービスへのアクセスを管理する](../../protect/deploy-use/manage-access-to-services.md)
