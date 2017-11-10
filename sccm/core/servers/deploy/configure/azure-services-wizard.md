---
title: "Azure サービス ウィザード"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager の Azure サービス ウィザードについて"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 833bc6588e079e124209d9c7adb91062e6afe6c3
ms.sourcegitcommit: d025a2cbd1ed82f42f67255c97b913f2163b3baf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configuration Manager と共に使用するように Azure サービスを構成する

*適用対象: System Center Configuration Manager (Current Branch)*

Current Branch バージョン 1706 以降、**Azure サービス ウィザード**を使用して、Configuration Manager で使用する Azure サービスの構成のプロセスを簡単にできます。

このウィザードでは、**Azure AD Web アプリ登録**を使用して、サブスクリプションと詳細な構成を行い、Azure AD との通信を認証することで、一般的な構成を行うことができます。 Web アプリを利用することで、Azure で新しい Configuration Manager コンポーネントやサービスをセットアップするたびに同じ情報を入力する必要がなくなります。

次の Azure サービスは、Azure サービス ウィザードを使用して構成できます。
-   **クラウド管理**   
    [Azure Active Directory (Azure AD) を利用し、クライアントの認証を有効にする](/sccm/core/clients/deploy/deploy-clients-cmg-azure) [Azure AD ユーザー探索を構成](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)することもできます。
-   **OMS コネクタ**
    [Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS) に接続し、OMS Log Analytics にコレクションなどのデータを同期します。
-   **Upgrade Readiness**
    [Upgrade Readiness に接続](/sccm/core/clients/manage/upgrade/upgrade-analytics)し、クライアント アップグレード互換性データを表示します。
-   **Microsoft Store for Business** [Microsoft Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) に接続し、組織用に Configuration Manager で展開できるアプリを入手します。

ウィザードでサービスを構成するとき、いくつかの共通アクションがあります。
次の設定があります。
-   *Azure 環境を構成する*: ウィザードの **[アプリ]** ページで、使用する **Azure 環境**を選択します。 サービスごとのコンテンツを参照し、公共の Azure クラウドのみに対応しているか、プライベート クラウドにも対応しているか確認してください。
-   *サーバー アプリを作成またはインポートする*: ウィザードの **[アプリ]** ページで、Azure Web アプリ登録メタデータを**作成**し、**インポート**できます。 使用できるオプションは、構成しているサービスによって異なります。 さらに、他のアプリが必要になるサービスもあります。 たとえば、**クラウド管理**サービスには、クライアントが Azure サービスとの通信で直接認証するために使用する**ネイティブ クライアント アプリ**が必要です。


Azure Web アプリの詳細については、「[Azure App Service での認証および承認](/azure/app-service/app-service-authentication-overview)」と「[Web Apps の概要](/azure/app-service-web/app-service-web-overview)」をご覧ください。


## <a name="webapp"></a> Configuration Manager で使用する Azure Active Directory Web アプリ登録の作成またはインポート

Azure サービス Web アプリ登録は Configuration Manager サイトを Azure AD に接続します。このアプリは、ご利用のインフラストラクチャで Azure サービスを使用するための前提条件です。 手順は次のとおりです。

1.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]** を展開して、**[Azure サービス]** をクリックします。
2.  **[ホーム]** タブの **[Azure サービス]** グループで、**[Azure サービスの構成]** をクリックします。
3.  Azure サービス ウィザードの **[Azure サービス]** ページで、Configuration Manager に接続する Azure サービスを選択します。
4.  ウィザードの **[全般]** ページで、Azure サービスの名前と説明を指定します。
5.  ウィザードの **[アプリ]** ページで、一覧から Azure 環境を選択し、**[参照]** をクリックして Azure サービスの構成に使用する *Web アプリ*と*ネイティブ クライアント アプリ* (必要な場合のみ) を選択します。

    **Web アプリ:** [参照] をクリックすると、[サーバー アプリ] ウィンドウが開きます。    
      **[サーバー アプリ]** ウィンドウで、使用するサーバー アプリを選択し、**[OK]** をクリックします。 サーバー アプリとは、Azure アカウントの構成 (クライアントのテナント ID、クライアント ID、秘密鍵など) を格納する Azure AD Web アプリ登録です。
    利用可能なアプリがない場合は、次のいずれかを使用します。

    - **作成**: Configuration Manager コンソールで入力した情報に基づいて、Azure AD Web アプリ登録の作成を自動化します。 また、アプリのフレンドリ名、ホームページ URL、アプリ ID URI、秘密鍵の有効期間を指定します。 既定では、シークレット キーの有効期間は 1 年間です。
        
        継続するには、誰かが Azure AD 資格情報でサインインし、Azure で Web アプリ作成を完了する必要があります。 Azure へのサインインに使用するアカウントは、Azure サービス ウィザードを実行するアカウントと同じである必要はありません。 Azure にサインインすると、Configuration Manager によって、Web アプリで使用するクライアント ID や秘密鍵とともに、Azure で Web アプリが作成されます。 その後、Azure Portal からこれらを表示できます。

        *作成*を使用して Web アプリを構成する場合は、Configuration Manager を使用して Azure AD で Web アプリを作成できます。
    
    - **インポート**: **Azure Portal** で既に作成されている Azure AD Web アプリに関する情報を入力して、その登録に関するメタデータを Configuration Manager にインポートします。 アプリとテナントのフレンドリ名を指定し、Configuration Manager で使用する Azure Web アプリのテナント ID、クライアント ID、シークレット キーを指定します。 情報を確認した後、**[OK]** をクリックして続行します。
        > [!NOTE]
        > **インポート**を使用する前に、[Azure Portal](https://portal.azure.com) で *[Web アプリ/API]* タイプの Azure AD アプリ登録を作成する必要があります。 アプリ登録の作成方法の詳細については、「[Azure Active Directory テナントにアプリケーションを登録する](/azure/active-directory/active-directory-app-registration)」をご覧ください。 Upgrade Readiness または Operations Management Suite を構成する場合は、Configuration Manager が OMS ワークスペースにアクセスできるようにするために、関連する OMS ワークスペースを含むリソース グループに対して、新しい登録済みの Web アプリの *[共同作成者]* アクセス許可を付与する必要もあります。 これを行うには、アクセス許可を割り当てるときに **[ユーザーの追加]** ブレードでアプリ登録名を検索する必要があります。 [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm) に接続するために [Configuration Manager に OMS へのアクセス許可を付与する](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms)場合も、これと同じ手順に従う必要があります。 こうした許可は、アプリを Configuration Manager にインポートする前に割り当てる必要があります。


    **ネイティブ クライアント アプリ:** [参照] をクリックすると、[クライアント アプリ] ウィンドウが開きます。  
     **[クライアント アプリ]** ウィンドウで、使用するクライアント アプリを選択し、**[OK]** をクリックします。

     利用可能なクライアント アプリがない場合は、次のいずれかを使用します。
     - **作成**: 新しいクライアント アプリを作成するには、**[作成]** をクリックします。 次に、アプリのフレンドリ名とリダイレクト URI を指定します。

         継続するには、誰かが Azure AD 資格情報でサインインし、Azure で Web アプリ作成を完了する必要があります。 Azure のサインインに使用するアカウントは、Azure サービス ウィザードを実行するアカウントと同じである必要はありません。 Azure にサインインすると、Configuration Manager によって、クライアント ID や秘密鍵とともに、Azure AD でネイティブ クライアント アプリが作成されます。 その後、[Azure Portal](https://portal.azure.com) でこれらを表示できます。 

     - **インポート**: Azure サブスクリプションに既に存在するクライアント アプリを使用します。 アプリのフレンドリ名とクライアント ID を指定します。 **[OK]** をクリックして続行します。

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  (**クラウド管理**サービスを構成する場合のみ) ウィザードの **[探索]** ページで、**[Azure Active Directory ユーザーの探索を有効にする]**、**[設定]** の順にクリックします。
**[Azure AD ユーザー探索設定]** ダイアログ ボックスで、検出を実行するスケジュールを設定します。 Azure AD の新規または変更されたアカウントのみをチェックする差分探索を有効にすることもできます。 Azure AD ユーザー探索の詳細については[こちら](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)をご覧ください。

7.  ウィザードを完了します。

Configuration Manager での Azure サービスの構成が完了しました。 他の Azure サービスを構成する場合にも、この手順を繰り返します。

## <a name="view-the-configuration-of-an-azure-service"></a>Azure サービスの構成を表示する
構成した Azure サービスのプロパティを表示できます。

コンソールで、**[管理]** > **[概要]** > **[Cloud Services]** > **[Azure サービス]** の順に進みます。 次に、表示または編集するサービスを選択し、**[プロパティ]** をクリックします。
