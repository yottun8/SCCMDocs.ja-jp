---
title: Azure AD でのクライアントのインストール
titleSuffix: Configuration Manager
description: 認証のために Azure Active Directory を使用して、Windows 10 デバイスで Configuration Manager クライアントをインストールして割り当てる
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 91ebb0c35687b231a6f08b7bc92cccb83cf0e602
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる

Azure AD 認証を使用して Windows 10 デバイスで Configuration Manager クライアントをインストールするには、Azure Active Directory (Azure AD) と Configuration Manager を統合します。 クライアントは、HTTPS が有効な管理ポイントと直接通信するイントラネット上に配置することができます。 CMG を通じて、あるいはインターネット ベース管理ポイントでインターネット ベースの通信を行うこともできます。 このプロセスでは Azure AD を使用して、Configuration Manager サイトに対してクライアントを認証します。 Azure AD を使用すると、クライアント認証証明書を構成して使用する必要がなくなります。



## <a name="before-you-begin"></a>始める前に

- Azure AD テナントは前提条件です。  

- デバイスの要件:  

    - Windows 10  

    - Azure AD への参加、純粋なクラウド ドメイン参加、またはハイブリッド Azure AD 参加  

- ユーザーの要件:  

    - ログオンしたユーザーは Azure AD の ID である必要があります。   

    - ユーザーがフェデレーション ID または同期 ID である場合、[Azure AD ユーザー探索](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)だけでなく、Configuration Manager の [Active Directory ユーザー探索](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser)を使用する必要があります。 ハイブリッド ID の詳細については、「[ハイブリッド ID 導入戦略の定義](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy)」を参照してください。<!--497750-->  

- 管理ポイント サイト システムの役割に関する[既存の前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq)に加え、このサーバーでは **ASP.NET 4.5** も有効にします。 ASP.NET 4.5 を有効にするときに自動的に選択される他のすべてのオプションを含めます。  

- HTTPS モードのすべての管理ポイントを構成します。 詳細については、「[PKI 証明書の要件](/sccm/core/plan-design/network/pki-certificate-requirements)」と「[IIS を実行するサイト システム用の Web サーバー証明書の展開](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)」を参照してください。  
    - クラウド管理ゲートウェイを使用している場合、そのクラウド管理ゲートウェイに対して有効にする管理ポイントにのみ HTTPS を構成する必要があります。
    - Azure AD トークンベース認証を利用してイントラネットにクライアントを展開している場合、クライアントが接触する可能性があるすべての管理ポイントで HTTPS を有効にする必要があります。 

- 必要に応じて、インターネット ベースのクライアントを展開するために[クラウド管理ゲートウェイ](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG) を設定します。 Azure AD で認証するオンプレミス クライアントの場合、CMG は必要ありません。  


## <a name="configure-azure-services-for-cloud-management"></a>クラウド管理用の Azure サービスの構成

最初のステップとして、Azure AD には Configuration Manager サイトを接続します。 このプロセスの詳細については、「[Azure サービスの構成](/sccm/core/servers/deploy/configure/azure-services-wizard)」を参照してください。 **クラウド管理**サービスへの接続を作成します。

**クラウド管理**へのオンボーディングの一環として、[Azure AD ユーザー探索](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)を有効にします。 

これらの操作が完了すると、Configuration Manager サイトが Azure AD に接続されます。 



## <a name="configure-client-settings"></a>クライアント設定を構成する

これらのクライアント設定は、Windows 10 デバイスを Azure AD に参加させる場合に役立ちます。 また、インターネット ベースのクライアントで CMG とクラウド配布ポイントを使用することもできます。

1.  「[クライアント設定を構成する方法](/sccm/core/clients/deploy/configure-client-settings)」の情報を使用して、**[クラウド サービス]** セクションの次のクライアント設定を構成します。  

    - **クラウド配布ポイントへのアクセスを許可する**: この設定を有効にすると、インターネットベースのデバイスが、構成マネージャー クライアントのインストールに必要なコンテンツを取得できるようになります。 クラウド配布ポイントでコンテンツを使用できない場合、デバイスは CMG からコンテンツを取得できます。 クライアント インストール ブートストラップでは、CMG にフォールバックするまで 4 時間、クラウド配布ポイントを再試行します。<!--495533-->  

    - **[新しい Windows 10 ドメインに参加しているデバイスを自動的に Azure Active Directory に登録する]**: **[はい]** または **[いいえ]** に設定します。 既定の設定は **[はい]** です。 この動作は、Windows 10 バージョン 1709 の既定でもあります。

    - **[クライアントでクラウド管理ゲートウェイを使用できるようにする]**: **[はい]** (既定) または **[いいえ]** に設定します。  

2.  クライアント設定を必要なデバイスのコレクションに展開します。 ユーザー コレクションには、これらの設定を展開しないでください。

デバイスが Azure AD に参加していることを確認するには、コマンド プロンプトで `dsregcmd.exe /status` を実行します。 デバイスが Azure AD に参加している場合は、結果の **[AzureAdjoined]** フィールドに **[YES]** が表示されます。



## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Azure AD の ID を使用してクライアントをインストールして登録する

Azure AD の ID を使用してクライアントを手動でインストールするには、まず、「[クライアントの手動インストール方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)」の一般的なプロセスを確認します。 

 > [!Note]  
 > デバイスは Azure AD に接続する際にインターネットにアクセスする必要がありますが、インターネット ベースである必要はありません。 

次の例は、コマンド ラインの一般的な構造を示しています。`ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

詳細については、「[クライアント インストールのプロパティ](/sccm/core/clients/deploy/about-client-installation-properties)」を参照してください。

/mp および CCMHOSTNAME プロパティでは、シナリオに応じて、以下のいずれかを指定します。
- オンプレミスの管理ポイント。 /mp プロパティのみを指定します。 CCMHOSTNAME は必要ありません。
- クラウド管理ゲートウェイ
- インターネット ベースの管理ポイント。SMSMP プロパティでは、オンプレミスまたはインターネット ベースの管理ポイントを指定します。

この例では、クラウド管理ゲートウェイを使用します。 各プロパティのサンプルの値が置き換えられます。`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Microsoft Intune で Azure AD の ID を使用してクライアントのインストールを自動化する場合は、[共同管理用に Windows 10 デバイスを準備する](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)プロセスを参照してください。



## <a name="next-steps"></a>次のステップ

完了したら、引き続き[クライアントの監視と管理](/sccm/core/clients/manage/monitor-clients)ができます。
