---
title: 共同管理のために Windows 10 を準備する
titleSuffix: Configuration Manager
description: 共同管理用に Windows 10 デバイスを準備する方法について説明します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 9aab4273129e6a3032d7e85d2545e6abc5b616c4
ms.sourcegitcommit: 8dd9199bfe8e27f62e9df307f1c6ac58a3b81717
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2018
ms.locfileid: "50237158"
---
# <a name="prepare-windows-10-devices-for-co-management"></a>共同管理用に Windows 10 デバイスを準備する
AD と Azure AD に参加し Microsoft Intune に登録されている Windows 10 デバイスと、Configuration Manager のクライアントで、共同管理を有効にできます。 新しい Windows 10 デバイスおよび Intune に既に登録されているデバイスでは、共同管理を有効にする前に Configuration Manager クライアントをインストールします。 既に Configuration Manager クライアントになっている Windows 10 デバイスの場合は、デバイスを Intune に登録して、Configuration Manager コンソールで共同管理を有効にできます。

> [!IMPORTANT]
> Windows 10 Mobile デバイスでは共同管理はサポートされません。



## <a name="prerequisites"></a>[前提条件]

共同管理を有効にする前に、次の前提条件が満たされている必要があります。 一般的な前提条件のほか、Configuration Manager クライアントがインストールされているデバイスとインストールされていないデバイスとで異なる前提条件があります。


### <a name="general-prerequisites"></a>一般的な前提条件

共同管理を有効にするための一般的な前提条件は次のとおりです。  

- Configuration Manager バージョン 1710 以降  

    - Configuration Manager バージョン 1806 以降では、複数の Configuration Manager インスタンスを 1 つの Intune テナントに接続できます。 <!--1357944-->  

- [クラウド管理のために Azure AD でオンボードされたサイト](/sccm/core/servers/deploy/configure/azure-services-wizard)  

- すべてのユーザーの EMS または Intune のライセンス  

- [Azure AD の自動登録](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)が有効  

- Intune のサブスクリプションと、Intune での MDM 機関が **Intune** に設定されていること。  

    - [混在機関](/sccm/mdm/deploy-use/migrate-mixed-authority)を使用している場合、まず Intune スタンドアロンへの移行を完了します。 次に、MDM 機関を Intune に設定してから、共同管理をセットアップします。<!--SCCMDocs issue #797-->


> [!Note]  
> ハイブリッド MDM 環境 (Intune と Configuration Manager が統合された環境) では、共同管理を有効にできません。 ただし、Intune スタンドアロンへのユーザー移行を開始し、関連 Windows 10 デバイスの共同管理を有効にできます。 Intune スタンドアロンへの移行については、[ハイブリッド MDM から Intune スタンドアロンへの移行の開始](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)に関する記事をご覧ください。


### <a name="prerequisite-azure-resource-manager-roles"></a>前提条件となる Azure Resource Manager の役割
<!--SCCMDocs issue #667-->Azure の役割の詳細については、[さまざまな役割](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles)に関するページをご覧ください。
|操作|必要な役割|
|----|----|
|クラウド管理ゲートウェイの設定|Azure サブスクリプション マネージャー|
|クラウド配布ポイントの設定|Azure サブスクリプション マネージャー|
|Configuration Manager コンソールからの Azure Active Directory アプリの作成|Azure Active Directory の全体管理者|
|Configuration Manager コンソールでの Azure クライアントとサーバー アプリのインポート| Configuration Manager 管理者。追加の Azure 役割は不要です。|
|共同管理ウィザードを使用した共同管理の設定| すべてのスコープの権限を持つ Configuration Manager の管理者と Azure Active Directory ユーザー権限。 


### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Configuration Manager クライアントがインストールされているデバイスの追加の前提条件

- Windows 10 バージョン 1709 以降  

- [ハイブリッド Azure AD 参加済み](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (AD と Azure AD に参加) または Azure AD のみ参加済み (この種類は "クラウド ドメイン参加済み" と呼ばれることがあります)。


### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Configuration Manager クライアントがインストールされていないデバイスの追加の前提条件

- Windows 10 バージョン 1709 以降  

- Configuration Manager の[クラウド管理ゲートウェイ](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) (Intune を使用して Configuration Manager クライアントをインストールする場合)  


> [!IMPORTANT]
> Windows 10 Mobile デバイスでは共同管理はサポートされません。



## <a name="command-line-to-install-configuration-manager-client"></a>Configuration Manager クライアントをインストールするためのコマンド ライン

まだ Configuration Manager クライアントではない Windows 10 デバイスの Intune でアプリを作成します。 次のセクションでアプリを作成するときは、次のコマンド ラインを使います。

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

#### <a name="example-command-line"></a>コマンドラインの例
次の値がある場合:

- **クラウド管理ゲートウェイ相互認証エンドポイントの URL**: `https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500`    

   >[!Note]    
   >**クラウド管理ゲートウェイ相互認証エンドポイントの URL** の値には、**vProxy_Roles** SQL ビューの **MutualAuthPath** の値を使います。  

- **管理ポイント (MP) の FQDN**: `mp1.contoso.com`    
- **サイト コード**: `PS1`    
- **Azure AD テナント ID**: `44b5bdda-67f5-4850-bdf4-a8ef611109e0`    
- **Azure AD クライアント アプリ ID**: `51e781eb-aac6-4265-8030-4cd1ddaa9dd0`     
- **AAD リソース ID URI**: `ConfigMgrServer`    

  > [!Note]    
  > **AAD リソース ID URI** の値には、**vSMS_AAD_Application_Ex** SQL ビューの **IdentifierUri** の値を使います。  

次のコマンド ラインを使います。

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=44b5bdda-67f5-4850-bdf4-a8ef611109e0 AADCLIENTAPPID=51e781eb-aac6-4265-8030-4cd1ddaa9dd0 AADRESOURCEURI=https://ConfigMgrServer"`


<!--1358215--> バージョン 1806 以降では、必要なコマンド ライン プロパティが減りました。  

- すべてのシナリオで次のコマンド ライン プロパティが必要になります。  
    - CCMHOSTNAME  
    - SMSSITECODE  

- PKI ベースのクライアント認証証明書ではなく、クライアント認証で Azure AD を使用する場合は、次のプロパティが必要です。  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- クライアントがイントラネットに再度ローミングされる場合は、次のプロパティが必要です。  
    - SMSMP  

次の例には、上記のプロパティのすべてが含まれます。   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

詳細については、「[クライアント インストールのプロパティ](/sccm/core/clients/deploy/about-client-installation-properties)」を参照してください。


> [!Tip]
> 次の手順を使って、サイトのコマンド ライン パラメーターを探します。     
> 
> 1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[Cloud Services]** を展開して **[共同管理]** を選択します。  
> 
> 2. リボンで **[共同管理の構成]** を選択し、共同管理オンボード ウィザードを開きます。 (共同管理を既に設定している場合は、**[プロパティ]** を選択します。 次に手順 4 に進みます。)    
> 
> 3. [サブスクリプション] ページで **[サインイン]** を選択します。 Intune テナントにサインインし、**[次へ]** をクリックします。    
> 
> 4. [有効化] ページで、**[コピー]** を選択して、コマンド ラインをクリップボードにコピーします。 次に、アプリ作成手順で使うため、コマンド ラインを保存します。  
> 
> 5. **[キャンセル]** をクリックしてウィザードを終了します。  

> [!Important]    
> コマンドラインをカスタマイズして Configuration Manager クライアントをインストールする場合は、コマンドラインが 1024 文字を超えていないことを確認してください。 コマンドラインが 1024 文字を超えると、クライアントのインストールは失敗します。



## <a name="new-windows-10-devices"></a>新しい Windows 10 デバイス

新しい Windows 10 デバイスの場合は、AutoPilot サービスを使って Out of Box Experience を構成できます。これには、AD および Azure AD へのデバイスの参加と、Intune へのデバイスの登録が含まれます。 その後、Intune にアプリを作成して Configuration Manager クライアントを展開します。  

1. 新しい Windows 10 デバイス用に AutoPilot を有効にします。 詳しくは、「[Windows AutoPilot の概要](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot)」をご覧ください。    

   > [!NOTE]   
   > バージョン 1802 以降では、Configuration Manager を使用して、ビジネス向け Microsoft Store と教育機関向け Microsoft Store に必要なデバイス情報を収集して報告します。 この情報には、デバイスのシリアル番号、Windows 製品識別子、およびハードウェア ID が含まれます。 Configuration Manager コンソールの **[監視]** ワークスペースで、**[レポート]** ノード、**[レポート]** の順に展開し、**[ハードウェア - 全般]** ノードを選びます。 新しいレポート **[Windows AutoPilot デバイス情報]** を実行し、結果を表示します。 レポート ビューアーで **[エクスポート]** アイコンをクリックして、**[CSV (コンマ区切り)]** オプションを選択します。 ファイルを保存した後、ビジネス向け Microsoft Store および教育機関向け Microsoft Store にデータをアップロードします。 詳細については、[ビジネス向け Microsoft Store および教育機関向け Microsoft Store でのデバイスの追加](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile)に関するページを参照してください。

2. Azure AD で自動登録を構成し、デバイスが Intune に自動的に登録されるようにします。 詳しくは、「 [Windows デバイスの登録](https://docs.microsoft.com/intune/windows-enroll)」をご覧ください。  

3. Configuration Manager クライアント パッケージで Intune にアプリを作成し、共同管理する Windows 10 デバイスにアプリを展開します。 [Azure AD を使ってインターネットからクライアントをインストールする](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure)手順の間に、[コマンド ラインを使って Configuration Manager クライアントをインストール](#command-line-to-install-configuration-manager-client)します。   



## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Intune に登録されていないか、Configuration Manager クライアントがインストールされている Windows 10 デバイス

Intune に登録されていないか、Configuration Manager クライアントがインストールされている Windows 10 デバイスの場合は、自動登録を使って Intune にデバイスを登録できます。 その後、Intune にアプリを作成して Configuration Manager クライアントを展開します。

1. Azure AD で自動登録を構成し、デバイスが Intune に自動的に登録されるようにします。 詳しくは、「 [Windows デバイスの登録](https://docs.microsoft.com/intune/windows-enroll)」をご覧ください。  

2. Configuration Manager クライアント パッケージで Intune にアプリを作成し、共同管理する Windows 10 デバイスにアプリを展開します。 [Azure AD を使ってインターネットからクライアントをインストールする](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure)手順の間に、[コマンド ラインを使って Configuration Manager クライアントをインストール](#command-line-to-install-configuration-manager-client)します。



## <a name="windows-10-devices-enrolled-in-intune"></a>Intune に登録されている Windows 10 デバイス

Intune に既に登録されている Windows 10 デバイスの場合は、Intune でアプリを作成して Configuration Manager クライアントを展開します。 [Azure AD を使ってインターネットからクライアントをインストールする](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure)手順の間に、[コマンド ラインを使って Configuration Manager クライアントをインストール](#command-line-to-install-configuration-manager-client)します。  



## <a name="next-steps"></a>次のステップ

[Configuration Manager のワークロードを Intune に切り替える](co-management-switch-workloads.md)
