---
title: 共同管理のために Windows 10 を準備する
titleSuffix: Configuration Manager
description: 共同管理用に Windows 10 デバイスを準備する方法について説明します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/28/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 8c025d7c7a1dc452cb96f937801656bc4d0cadab
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339599"
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
- [クラウド管理のために Azure AD でオンボードされたサイト](/sccm/core/servers/deploy/configure/azure-services-wizard)
- すべてのユーザーの EMS または Intune のライセンス
- [Azure AD の自動登録](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)が有効
- Intune のサブスクリプション &#40;MDM 機関が **Intune** に設定されたもの&#41;


   > [!Note]  
   > ハイブリッド MDM 環境 (Intune と Configuration Manager が統合された環境) では、共同管理を有効にできません。 ただし、Intune スタンドアロンへのユーザー移行を開始し、関連 Windows 10 デバイスの共同管理を有効にできます。 Intune スタンドアロンへの移行については、[ハイブリッド MDM から Intune スタンドアロンへの移行の開始](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)に関する記事をご覧ください。

### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Configuration Manager クライアントがインストールされているデバイスの追加の前提条件
- Windows 10 バージョン 1709 以降
- [ハイブリッド Azure AD への参加](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (AD と Azure AD に参加)

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Configuration Manager クライアントがインストールされていないデバイスの追加の前提条件
- Windows 10 バージョン 1709 以降
- Configuration Manager の[クラウド管理ゲートウェイ](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) (Intune を使用して Configuration Manager クライアントをインストールする場合)

> [!IMPORTANT]
> Windows 10 Mobile デバイスでは共同管理はサポートされません。


## <a name="command-line-to-install-configuration-manager-client"></a>Configuration Manager クライアントをインストールするためのコマンド ライン
まだ Configuration Manager クライアントではない Windows 10 デバイスの Intune でアプリを作成します。 次のセクションでアプリを作成するときは、次のコマンド ラインを使います。

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

たとえば、次のような値を使うものとします。

- **クラウド管理ゲートウェイ相互認証エンドポイントの URL**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    

   >[!Note]    
   >**クラウド管理ゲートウェイ相互認証エンドポイントの URL** の値には、**vProxy_Roles** SQL ビューの **MutualAuthPath** の値を使います。

- **管理ポイント (MP) の FQDN**: mp1.contoso.com    
- **サイト コード**: PS1    
- **Azure AD テナント ID**: 60a413f4-c606-4744-8adb-9476ae3XXXXX    
- **Azure AD クライアント アプリ ID**: 9fb9315f-4c42-405f-8664-ae63283XXXXX     
- **AAD リソース ID URI**: ConfigMgrServer    

  > [!Note]    
  > **AAD リソース ID URI** の値には、**vSMS_AAD_Application_Ex** SQL ビューの **IdentifierUri** の値を使います。

この場合は、次のようなコマンド ラインを使います。

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=60a413f4-c606-4744-8adb-9476ae3XXXXX AADCLIENTAPPID=9fb9315f-4c42-405f-8664-ae63283XXXXX AADRESOURCEURI=https://ConfigMgrServer"`

> [!Tip]
> サイトのコマンド ライン パラメーターは、次の手順を使って探すことができます。     
> 1. Configuration Manager コンソールで、**[管理]** > **[概要]** > **[クラウド サービス]** > **[Co-management]\(共同管理\)** の順に移動します。  
> 2. [ホーム] タブの [管理] グループで、 **[Configure co-management]\(共同管理の構成\)** を選んで共同管理オンボード ウィザードを開きます。    
> 3. [サブスクリプション] ページで **[サインイン]** をクリックして Intune テナントにサインインし、**[次へ]** をクリックします。    
> 4. [Enablement]\(有効化\) ページで、**[Devices enrolled in Intune]\(Intune に登録されているデバイス\)** セクションの **[コピー]** をクリックしてコマンド ラインをクリップボードにコピーして保存し、アプリ作成手順で使います。  
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