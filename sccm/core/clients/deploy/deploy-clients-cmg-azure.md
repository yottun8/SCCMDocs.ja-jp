---
title: "インターネットからクライアントをインストールして割り当てる | Microsoft Docs"
description: "インターネットから System Center Configuration Manager クライアントをインストールして割り当てます。"
ms.custom: na
ms.date: 8/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: "14"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 7bbcece8a7a745b3b6cc9bbd8aa283963e2b738d
ms.sourcegitcommit: 49add91eebfeaba6d1d203d3cf9927b9cacdfc8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2017
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる

Configuration Manager Cloud Services と Azure AD を使用して、次のシナリオをサポートできます。

- インターネットから手動で構成マネージャー クライアントを Windows 10 デバイスにインストールして、Configuration Manager サイトに割り当てます (クラウド管理ゲートウェイ サイト システムの役割が必要)。
- Azure AD を使用してクライアントを認証し、Configuration Manager サイトにアクセスします。 Azure AD を使用すると、クライアント認証証明書を構成して使用する必要がなくなります。
- コレクションおよびその他の Configuration Manager の操作で使用するサイト内で Azure AD ユーザーを検出します。

これを実現するためには、次の手順を使用します。

- **手順 1: Configuration Manager Cloud Services で Azure サービス アプリを設定し、Azure AD ユーザー探索を構成する**
- **手順 2: クラウド管理ゲートウェイを設定する** (オンプレミスのクライアントの場合は省略可能)
- **手順 3: クライアント設定を構成し、Windows 10 デバイスを Azure AD に参加させて、クライアントがクラウド管理ゲートウェイを使用できるようにする**
- **手順 4: Azure Active Directory ID を使用して、Configuration Manager クライアントをインストールして登録する**


## <a name="before-you-start"></a>アップグレードを開始する前に

- Azure AD テナントが必要です。
- Windows 10 を実行するデバイスで、Azure AD に参加しており、Azure AD の ID を使用してログオンしている必要があります。 参加している Azure AD に加え、クライアントもドメインに参加できます。
- 管理ポイントのサイト システムの役割に対する[既存の前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)に加え、**ASP.NET 4.5** (および自動的に選択されるその他のオプション) が、このサイト システムの役割をホストするコンピューターで有効になっていることを確認する必要があります。
- Configuration Manager を使用して、クライアントを展開するには:
    - クライアント証明書ではなく Azure AD を使って認証する場合は、HTTPS モード用に少なくとも 1 つの管理ポイントを構成します。
        クラウド管理ゲートウェイではなくクライアント証明書を使用する場合、HTTPS 管理ポイントは省略可能ですが、推奨されます。 認証に Azure AD を使用する場合は、オンプレミスのクライアントでも、インターネットのクライアントでも、HTTPS 管理ポイントが必須です。
    - インターネットのクライアントを展開する場合は、クラウド管理ゲートウェイを設定します。 Azure AD を使って認証するオンプレミスのクライアントでは、クラウド管理ゲートウェイを構成する必要はありません。


## <a name="step-1-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>手順 1: Configuration Manager Cloud Services で Azure サービス アプリを設定する

これにより、Configuration Manager サイトを Azure AD に接続します。これは、このセクションの他のすべての操作の前提条件です。 

Azure AD ユーザーの探索は、*クラウド管理*の一部として構成されています。 これを行う手順については、「*Configuration Manager と共に使用するように Azure サービスを構成する*」トピックの「[Configuration Manager と共に使用するように Azure Web アプリを作成する](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp)」の手順 **6** で詳しく説明されています。
    
手順を完了すると、Configuration Manager サイトが Azure AD に接続されます。 

## <a name="step-2-set-up-the-cloud-management-gateway"></a>手順 2: クラウド管理ゲートウェイを設定する

このトピックで説明されているクラウド管理のシナリオを可能にするために、クラウド管理ゲートウェイを設定します。 次のトピックでヘルプを検索します。 

- [Configuration Manager でクラウド管理ゲートウェイを計画する](/sccm/core/clients/manage/plan-cloud-management-gateway)
- [Configuration Manager のクラウド管理ゲートウェイを設定する](/sccm/core/clients/manage/setup-cloud-management-gateway)
- [Configuration Manager でクラウド管理ゲートウェイを監視する](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway)

## <a name="step-3-configure-client-settings-to-join-windows-10-devices-with-azure-ad-and-enable-clients-to-use-the-cloud-management-gateway"></a>手順 3: クライアント設定を構成し、Windows 10 デバイスを Azure AD に参加させて、クライアントがクラウド管理ゲートウェイを使用できるようにする

1.  [クライアント設定を構成する方法](/sccm/core/clients/deploy/configure-client-settings)に関するページの情報を使用して、次のクライアント設定セクション (**[クラウド サービス]** にあります) を構成します。
    - **クラウド配布ポイントへのアクセスを許可する** - この設定を有効にすると、インターネットベースのデバイスが、構成マネージャー クライアントのインストールに必要なコンテンツを取得できるようになります。 クラウド配布ポイントでコンテンツを入手できない場合、デバイスはクラウド管理ゲートウェイに接続された管理ポイントからコンテンツを取得できます。
    - **[新しい Windows 10 ドメインに参加しているデバイスを自動的に Azure Active Directory に登録する]**: **[はい]** (既定) または **[いいえ]** に設定します。
    - **[クライアントでクラウド管理ゲートウェイを使用できるようにする]**: **[はい]** (既定) または **[いいえ]** に設定します。
2.  クライアント設定を必要なデバイスのコレクションに展開します。 ユーザー コレクションには、これらの設定を展開しないでください。

デバイスが Azure AD に参加していることを確認するには、コマンド プロンプト ウィンドウでコマンド **dsregcmd.exe/status** を実行します。 デバイスが Azure AD に参加している場合は、結果の **[AzureAdjoined]** フィールドに **[YES]** が表示されます。


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>手順 4: Azure Active Directory ID を使用して、Configuration Manager クライアントをインストールして登録する

クライアントをインストールするには、次のインストール コマンド ラインを使用して、「[System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually)」の手順に従います。 

**ccmsetup.exe /mp&#58; https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=DFD SMSMP=https://SCCMDFPSS.contoso.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011DB47 AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d17026 AADRESOURCEURI=https://contososerver**

- **/MP** – ダウンロード ソース。 インターネットからのブートストラップの場合は CMG に設定できます。
- **CCMHOSTNAME**: インターネット管理ポイントの名前。 これを見つけるには、管理対象クライアントのコマンド プロンプトから **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** を実行します。
- **SMSSiteCode**: Configuration Manager サイトのサイト コード。
- **SMSMP**: ルックアップ管理ポイントの名前。管理ポイントはイントラネットを指定することもできます。
- **AADTENANTID**、**AADTENANTNAME**: Configuration Manager にリンクした Azure AD テナントの ID と名前。 これを見つけるには、Azure AD に参加しているデバイスで、コマンド プロンプトから dsregcmd.exe/status を実行します。
- **AADCLIENTAPPID**: Azure AD のクライアント アプリ ID。 これを見つけるには、「[リソースにアクセスできる Azure Active Directory アプリケーションとサービス プリンシパルをポータルで作成する](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key)」を参照してください。
- **AADResourceUri**: 搭載された Azure AD サーバー アプリの識別子 URI。 詳細については、「[Configuration Manager と共に使用するように Azure サービスを構成する](/sccm/core/servers/deploy/configure/azure-services-wizard)」をご覧ください。




## <a name="next-steps"></a>次のステップ

完了したら、引き続き[クライアントの監視と管理](/sccm/core/clients/manage/monitor-clients)ができます。
