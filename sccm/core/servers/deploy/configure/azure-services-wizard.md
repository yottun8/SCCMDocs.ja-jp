---
title: Azure サービスの構成
titleSuffix: Configuration Manager
description: Configuration Manager 環境を、クラウド管理、Upgrade Readiness、ビジネス向け Microsoft ストア、Operations Management Suite 用の Azure サービスと接続します。
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b86c73f3f5662a00ca0b7f80b0c785c37aff0b1a
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2018
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configuration Manager と共に使用するように Azure サービスを構成する

*適用対象: System Center Configuration Manager (Current Branch)*

**Azure サービス ウィザード**を使用して、Configuration Manager で使用する Azure Cloud Services の構成プロセスを簡略化します。 このウィザードでは、Azure Active Directory (Azure AD) Web アプリ登録を使用して、一般的な構成エクスペリエンスが提供されます。 これらのアプリではサブスクリプションと構成の詳細が提供され、Azure AD との通信が認証されます。 アプリを利用することで、Azure で新しい Configuration Manager コンポーネントやサービスをセットアップするたびに同じ情報を入力する必要がなくなります。



## <a name="available-services"></a>利用可能なサービス

このウィザードを使用して、次の Azure サービスを構成します。  

-   **クラウド管理**: このサービスでは、Azure AD を使用して、サイトとクライアントの認証を有効にします。 この認証により、次のような他のシナリオが有効になります。  

    - [認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

    - [Azure AD ユーザー探索を構成する](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - 特定の[クラウド管理ゲートウェイ シナリオ](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)をサポートする  

-   **OMS コネクタ**: [Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS) に接続します。 OMS Log Analytics にコレクションなどのデータを同期します。  

-   **Upgrade Readiness コネクタ**: Windows Analytics [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) に接続します。 クライアント アップグレード互換性データを表示します。  

-   **ビジネス向け Microsoft Store**: [ビジネス向け Microsoft Store](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) に接続します。 Configuration Manager で展開できる、組織のストア アプリを取得します。  

### <a name="service-details"></a>サービスの詳細

次の表に、各サービスの詳細を一覧表示します。  

- **テナント**: 構成できるサービス インスタンスの数。 各インスタンスは個別の Azure テナントである必要があります。  

- **クラウド**: すべてのサービスでグローバル Azure クラウドがサポートされます。ただし、Azure 米国政府クラウドなどの、プライベート クラウドはすべてのサービスでサポートされるわけではありません。  

- **Web アプリ**: サービスで *Web アプリ/API* (Configuration Manager ではサーバー アプリともいう) の種類の Azure AD アプリを使用するかどうか。  

- **ネイティブ アプリ**: サービスで *ネイティブ* (Configuration Manager ではクライアント アプリともいう) の種類の Azure AD アプリを使用するかどうか。  

- **操作**: Configuration Manager Azure サービス ウィザードでこれらのアプリをインポートするか、作成するか。  


|[サービス]  |テナント  |クラウド  |Web アプリ  |ネイティブ アプリ  |操作  |
|---------|---------|---------|---------|---------|---------|
|クラウド管理</br>(Azure AD ユーザー探索を使用) | 複数 | パブリック | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | インポート、作成 |
|OMS コネクタ | 1 台 | パブリック、プライベート | ![サポートされています](media/green_check.png) | ![サポートされていません](media/Red_X.png) | インポート |
|Upgrade Readiness | 1 台 | パブリック | ![サポートされています](media/green_check.png) | ![サポートされていません](media/Red_X.png) | インポート |
|Microsoft Store</br>(ビジネス向けおよび教育機関向け) | 1 台 | パブリック | ![サポートされています](media/green_check.png) | ![サポートされていません](media/Red_X.png) | インポート、作成 |


### <a name="about-azure-ad-apps"></a>Azure AD アプリについて

Azure サービスごとに異なる構成が必要になります。この構成は Azure Portal で行います。 さらに、各サービスのアプリには Azure リソースに対する別のアクセス許可が必要になる場合があります。  

複数のサービスに対して 1 つのアプリを使用することができます。 Configuration Manager と Azure AD で管理するオブジェクトは 1 つだけです。 アプリのセキュリティ キーの期限が切れた場合、更新する必要があるキーは 1 つだけです。

最も安全な構成では、サービスごとに別のアプリを使用します。 1 つのサービスのみのアプリに、別のサービスでは必要としない追加のアクセス許可が必要な場合があります。 さまざまなサービスで 1 つのアプリを使用することで、そのアプリが必要とするより多くのアクセス許可をアプリに提供できます。 

Configuration Manager は、ウィザードで追加の Azure サービスを作成する際に、サービス間で共通の情報を再利用するように設計されています。 これにより、同じ情報を複数回入力する必要がなくなります。 

サービスごとの必要なアプリのアクセス許可と構成の詳細については、「[利用可能なサービス](#available-services)」の関連する Configuration Manager の記事を参照してください。 

Azure アプリの詳細については、まず、以下の記事を参照してください。
- [Azure App Service での認証および承認](/azure/app-service/app-service-authentication-overview)
- [Web Apps の概要](/azure/app-service-web/app-service-web-overview)
- [Azure AD でのアプリケーションの登録の基本](/azure/active-directory/develop/active-directory-authentication-scenarios#basics-of-registering-an-application-in-azure-ad)  
- [Azure Active Directory テナントにアプリケーションを登録する](/azure/active-directory/active-directory-app-registration)



## <a name="before-you-begin"></a>始める前に

接続するサービスを決定したら、「[サービスの詳細](#service-details)」の表を参照してください。 この表には、Azure サービス ウィザードを完了するために必要な情報が示されています。 事前に Azure AD 管理者と話し合ってください。 Azure Portal で事前にアプリを手動で作成し、アプリの詳細を Configuration Manager にインポートするかどうかを決定します。 または、Configuration Manager を使用して、Azure AD でアプリを直接作成します。 Azure AD から必要なデータを収集する場合は、この記事の他のセクションの情報を確認してください。

一部のサービスでは、Azure AD アプリに特定のアクセス許可を割り当てる必要があります。 各サービスの情報を確認して、必要なアクセス許可を判別してください。 たとえば、Web アプリをインポートする前に、Azure 管理者はまず、[Azure Portal](https://portal.azure.com) でそれを作成する必要があります。 Upgrade Readiness または OMS コネクタを構成する場合、関連する OMS ワークスペースを含むリソース グループに対して、新たに登録した Web アプリの*共同作成者* アクセス許可を付与する必要があります。 これにより、Configuration Manager からそのワークスペースへのアクセスが許可されます。 アクセス許可を割り当てるときに、**[ユーザーの追加]** ブレードでアプリ登録名を検索します。 このプロセスは、[OMS へのアクセス許可を Configuration Manager に提供する](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms)場合と同じです。 Azure 管理者は、アプリを Configuration Manager にインポートする前に、これらのアクセス許可を割り当てる必要があります。



## <a name="start-the-azure-services-wizard"></a>Azure サービス ウィザードの起動

1.  Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[Cloud Services]** を展開して **[Azure サービス]** ノードを選択します。  

2.  リボンの **[ホーム]** タブの **[Azure サービス]** グループで、**[Azure サービスの構成]** をクリックします。  

3.  Azure サービス ウィザードの **[Azure サービス]** ページで、以下の操作を行います。  

    1. Configuration Manager でオブジェクトの**名前**を指定します。  

    2. 省略可能な**説明**を指定すれば、サービスを特定するのに役立ちます。  

    3. Configuration Manager に接続する Azure サービスを選択します。  

4. **[次へ]** をクリックして、Azure サービス ウィザードの「[Azure アプリのプロパティ](#azure-app-properties)」のページに進みます。  



## <a name="azure-app-properties"></a>Azure アプリのプロパティ

Azure サービス ウィザードの**アプリ** ページで、まず、一覧から **[Azure 環境]** を選択します。 サービスで現在使用できる環境については、「[サービスの詳細](#service-details)」の表を参照してください。

アプリ ページの残りの部分は、サービスによって異なります。 サービスで使用されるアプリの種類や、使用できる操作については、「[サービスの詳細](#service-details)」の表を参照してください。 
- アプリでインポートと作成の両方の操作がサポートされている場合は、**[参照]** をクリックします。 この操作で、[サーバー アプリのダイアログ](#server-app-dialog)または[クライアント アプリのダイアログ](#client-app-dialog)が開きます。
- アプリでインポート操作のみがサポートされている場合は、**[インポート]** をクリックします。 この操作で、[アプリのインポート ダイアログ (サーバー)](#import-apps-dialog-server) または[アプリのインポート ダイアログ (クライアント)](#import-apps-dialog-client) が開きます。

このページでアプリを指定したら、**[次へ]** をクリックして、Azure サービス ウィザードの [[構成] または [探索]](#configuration-or-discovery) ページに進みます。

### <a name="web-app"></a>Web アプリ

このアプリは、Azure AD の種類の *Web アプリ/API* (Configuration Manager ではサーバー アプリともいう) です。

#### <a name="server-app-dialog"></a>サーバー アプリのダイアログ

Azure サービス ウィザードのアプリ ページで **[Web アプリ]** の **[参照]** をクリックすると、サーバー アプリのダイアログが開きます。 ここには、既存の Web アプリの以下のプロパティを示す一覧が表示されます。
- テナントのフレンドリ名
- アプリのフレンドリ名
- サービスの種類

サーバー アプリのダイアログから実行できる以下の 3 つの操作があります。
- 既存の Web アプリを再利用するには、一覧から選択します。 
- **[インポート]** をクリックして、[アプリのインポート ダイアログ](#import-apps-dialog-server)を開きます。
- **[作成]** をクリックして、[サーバー アプリケーションの作成](#create-server-application-dialog)ダイアログを開きます。

選択したら、Web アプリをインポートまたは作成し、**[OK]** をクリックしてサーバー アプリのダイアログを閉じます。 この操作で、Azure サービス ウィザードの[アプリ ページ](#azure-app-properties)に戻ります。

#### <a name="import-apps-dialog-server"></a>アプリのインポート ダイアログ (サーバー)

Azure サービス ウィザードのサーバー アプリのダイアログまたはアプリ ページで **[インポート]** をクリックすると、アプリのインポート ダイアログが開きます。 このページでは、Azure Portal で既に作成されている Azure AD Web アプリに関する情報を入力できます。 Configuration Manager にその Web アプリに関するメタデータがインポートされます。 次の情報を指定します。
- **Azure AD テナント名**
- **Azure AD テナント ID**
- **アプリケーション名**: アプリのフレンドリ名。
- **クライアント ID**
- **秘密鍵**
- **秘密鍵の有効期限**: カレンダーから未来の日付を選択します。 
- **アプリ ID URI**: この値は、Azure AD テナント内で一意である必要があります。 サービスへのアクセスを要求するために Configuration Manager クライアントで使用されるアクセス トークンにあります。 既定では、この値は https://ConfigMgrService です。  

情報を入力したら、**[確認]** をクリックします。 次に **[OK]** をクリックして、アプリのインポート ダイアログを閉じます。 この操作で、Azure サービス ウィザードの[アプリ ページ](#azure-app-properties)、または[サーバー アプリのダイアログ](#server-app-dialog)に戻ります。

#### <a name="create-server-application-dialog"></a>サーバー アプリケーションの作成ダイアログ

サーバー アプリのダイアログで **[作成]** をクリックすると、サーバー アプリケーションの作成ダイアログが開きます。 このページでは、Azure AD での Web アプリの作成が自動化されます。 次の情報を指定します。
- **アプリケーション名**: アプリのフレンドリ名。
- **ホームページ URL**: この値は Configuration Manager では使用されませんが、Azure AD で必要になります。 既定では、この値は https://ConfigMgrService です。  
- **アプリ ID URI**: この値は、Azure AD テナント内で一意である必要があります。 サービスへのアクセスを要求するために Configuration Manager クライアントで使用されるアクセス トークンにあります。 既定では、この値は https://ConfigMgrService です。  
- **秘密鍵の有効期間**: ドロップダウン リストをクリックして、**[1 年]** または **[2 年]** を選択します。 1 年が既定値です。

**[サインイン]** をクリックして、管理者ユーザーとして Azure への認証を行います。 これらの資格情報は Configuration Manager では保存されません。 この管理者には Configuration Manager のアクセス許可は必要ありません。また、Azure サービス ウィザードを実行するアカウントと同じものである必要もありません。 Azure への認証が正常に行われると、ページに参照用の **Azure AD テナント名**が表示されます。 

**[OK]** をクリックして Azure AD で Web アプリを作成し、サーバー アプリケーションの作成ダイアログを閉じます。 この操作で、[サーバー アプリのダイアログ](#server-app-dialog)に戻ります。


### <a name="native-client-app"></a>ネイティブ クライアント アプリ
    
このアプリは、Azure AD の種類の*ネイティブ* (Configuration Manager ではクライアント アプリともいう) です。

#### <a name="client-app-dialog"></a>クライアント アプリのダイアログ

Azure サービス ウィザードのアプリ ページで **[ネイティブ クライアント アプリ]** の **[参照]** をクリックすると、クライアント アプリのダイアログが開きます。 ここには、既存のネイティブ アプリの以下のプロパティを示す一覧が表示されます。
- テナントのフレンドリ名
- アプリのフレンドリ名
- サービスの種類

クライアント アプリのダイアログから実行できる以下の 3 つの操作があります。
- 既存のネイティブ アプリを再利用するには、一覧から選択します。 
- **[インポート]** をクリックして、[アプリのインポート ダイアログ](#import-apps-dialog-client)を開きます。
- **[作成]** をクリックして、[クライアント アプリケーションの作成ダイアログ](#create-client-application-dialog)を開きます。

選択したら、ネイティブ アプリをインポートまたは作成し、**[OK]** をクリックしてクライアント アプリのダイアログを閉じます。 この操作で、Azure サービス ウィザードの[アプリ ページ](#azure-app-properties)に戻ります。

#### <a name="import-apps-dialog-client"></a>アプリのインポート ダイアログ (クライアント)

クライアント アプリのダイアログで **[インポート]** をクリックすると、アプリのインポート ダイアログが開きます。 このページでは、Azure Portal で既に作成されている Azure AD ネイティブ アプリに関する情報を入力できます。 Configuration Manager にそのネイティブ アプリに関するメタデータがインポートされます。 次の情報を指定します。
- **アプリケーション名**: アプリのフレンドリ名。
- **クライアント ID** 

情報を入力したら、**[確認]** をクリックします。 次に **[OK]** をクリックして、アプリのインポート ダイアログを閉じます。 この操作で、[クライアント アプリのダイアログ](#client-app-dialog)に戻ります。

#### <a name="create-client-application-dialog"></a>クライアント アプリケーションの作成ダイアログ

クライアント アプリのダイアログで **[作成]** をクリックすると、クライアント アプリケーションの作成ダイアログが開きます。 このページでは、Azure AD のネイティブの作成が自動化されます。 次の情報を指定します。
- **アプリケーション名**: アプリのフレンドリ名。
- **応答 URL**: この値は Configuration Manager では使用されませんが、Azure AD で必要になります。 既定では、この値は https://ConfigMgrService です。 

**[サインイン]** をクリックして、管理者ユーザーとして Azure への認証を行います。 これらの資格情報は Configuration Manager では保存されません。 この管理者には Configuration Manager のアクセス許可は必要ありません。また、Azure サービス ウィザードを実行するアカウントと同じものである必要もありません。 Azure への認証が正常に行われると、ページに参照用の **Azure AD テナント名**が表示されます。 

**[OK]** をクリックして Azure AD でネイティブ アプリを作成し、クライアント アプリケーションの作成ダイアログを閉じます。 この操作で、[クライアント アプリのダイアログ](#client-app-dialog)に戻ります。


## <a name="configuration-or-discovery"></a>[構成] または [探索]

アプリ ページで Web アプリとネイティブ アプリを指定した後、Azure サービス ウィザードは、接続しているサービスに応じて、**[構成]** ページまたは **[探索]** ページに進みます。 このページの詳細はサービスによって異なります。 詳細については、以下の記事のいずれかを参照してください。  

-   **クラウド管理**サービス、**[探索]** ページ: [Azure AD ユーザー探索を構成する](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

-   **OMS コネクタ** サービス、**[構成]** ページ: [OMS への接続を構成する](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#use-the-azure-services-wizard-to-configure-the-connection-to-oms)  

-   **Upgrade Readiness コネクタ** サービス、**[構成]** ページ: [Azure ウィザードを使用して、接続を作成する](/sccm/core/clients/manage/upgrade/upgrade-analytics#use-the-azure-wizard-to-create-the-connection)  

-   **ビジネス向け Microsoft ストア** サービス、**[構成]** ページ: [ビジネス向け Microsoft Store の同期の設定](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#for-configuration-manager-version-1706-and-later)  


最後に、[概要]、[進行状況]、および [完了] の各ページを使用して Azure サービス ウィザードを完了します。 Configuration Manager での Azure サービスの構成が完了しました。 他の Azure サービスを構成する場合にも、この手順を繰り返します。


## <a name="view-the-configuration-of-an-azure-service"></a>Azure サービスの構成を表示する
構成した Azure サービスのプロパティを表示できます。 Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[Cloud Services]** を展開して **[Azure サービス]** を選択します。 表示または編集するサービスを選択し、**[プロパティ]** をクリックします。

サービスを選択し、リボンの **[削除]** をクリックした場合、この操作で Configuration Manager の接続が削除されます。 Azure AD のアプリは削除されません。 不要になったときにアプリを削除する場合は、Azure 管理者に依頼してください。 または、Azure サービス ウィザードを実行してアプリをインポートします。<!--483440-->


## <a name="cloud-management-data-flow"></a>クラウド管理データ フロー

次の図は、Configuration Manager、Azure AD、および接続されているクラウド サービス間の相互作用の概念を表すデータ フローです。 この特定の例では、Windows 10 クライアント、およびサーバー アプリとクライアント アプリの両方を含む、**クラウド管理**サービスを使用します。 他のサービスのフローもこれと似ています。

![Azure AD とクラウド管理を含む Configuration Manager のデータ フロー図](media/aad-auth.png)

1.  Configuration Manager 管理者は、Azure AD でクライアント アプリとサーバー アプリをインポートまたは作成します。  

2.  Configuration Manager の Azure AD ユーザー探索が実行されます。 サイトでは Azure AD サーバー アプリ トークンを使用して、Microsoft グラフでユーザー オブジェクトを照会します。  

3.  サイトにはユーザー オブジェクトに関するデータが格納されます。 詳細については、「[Azure AD ユーザー探索](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)」を参照してください。  

4.  Configuration Manager クライアントは Azure AD ユーザー トークンを要求します。 クライアントは Azure AD クライアント アプリのアプリケーション ID、および対象となるサーバー アプリを使用して要求を行います。 詳細については、「[Azure AD のセキュリティ トークンの要求](/azure/active-directory/develop/active-directory-authentication-scenarios#claims-in-azure-ad-security-tokens)」を参照してください。  

5.  クライアントは、Azure AD トークンをクラウド管理ゲートウェイおよび/またはオンプレミスの HTTPS が有効な管理ポイントに提示して、サイトで認証を行います。  


