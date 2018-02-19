---
title: "共同管理用に Windows 10 デバイスを準備する"
description: "共同管理用に Windows 10 デバイスを準備する方法について説明します。"
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 902787f173c714fd2a73cc657aad758bd79ce3c8
ms.sourcegitcommit: 389c4e5b4e9953b74c13b1689195f99c526fa737
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2018
---
# <a name="prepare-windows-10-devices-for-co-management"></a>共同管理用に Windows 10 デバイスを準備する
AD と Azure AD に参加し Intune に登録されている Windows 10 デバイスと、Configuration Manager のクライアントで、共同管理を有効にできます。 新しい Windows 10 デバイスおよび Intune に既に登録されているデバイスでは、共同管理を有効にする前に Configuration Manager クライアントをインストールします。 既に Configuration Manager クライアントになっている Windows 10 デバイスの場合は、デバイスを Intune に登録して、Configuration Manager コンソールで共同管理を有効にできます。

> [!IMPORTANT]
> Windows 10 Mobile デバイスでは共同管理はサポートされません。

## <a name="command-line-to-install-configuration-manager-client"></a>Configuration Manager クライアントをインストールするためのコマンド ライン
まだ Configuration Manager クライアントではない Windows 10 デバイスの Intune でアプリを作成する必要があります。 次のセクションでアプリを作成するときは、次のコマンド ラインを使います。

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*クラウド管理ゲートウェイ相互認証エンドポイントの URL*&#62;/ CCMHOSTNAME=&#60;*クラウド管理ゲートウェイ相互認証エンドポイントの URL*&#62; SMSSiteCode=&#60;*サイト コード*&#62; SMSMP=https:&#47;/&#60;*MP の FQDN*&#62; AADTENANTID=&#60;*AAD テナント ID*&#62; AADTENANTNAME=&#60;*テナント名*&#62; AADCLIENTAPPID=&#60;*AAD 統合用のサーバー アプリ ID*&#62; AADRESOURCEURI=https:&#47;/&#60;*リソース ID*&#62;”

たとえば、次のような値を使うものとします。

- **クラウド管理ゲートウェイ相互認証エンドポイントの URL**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >**クラウド管理ゲートウェイ相互認証エンドポイントの URL** の値には、**vProxy_Roles** SQL ビューの **MutualAuthPath** の値を使います。

- **管理ポイント (MP) の FQDN**: sccmmp.corp.contoso.com    
- **サイト コード**: PS1    
- **Azure AD テナント ID**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Azure AD テナント名**: contoso    
- **Azure AD クライアント アプリ ID**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **AAD リソース ID URI**: ConfigMgrServer    

  > [!Note]    
  > **AAD リソース ID URI** の値には、**vSMS_AAD_Application_Ex** SQL ビューの **IdentifierUri** の値を使います。

この場合は、次のようなコマンド ラインを使います。

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer”

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