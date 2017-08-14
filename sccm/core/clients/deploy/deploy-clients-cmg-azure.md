---
title: "インターネットからクライアントをインストールして割り当てる | Microsoft Docs"
description: "インターネットから System Center Configuration Manager クライアントをインストールして割り当てます。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: 14
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: f604557d208b2dda9dc1c6b4c4d27d896d47695e
ms.contentlocale: ja-jp
ms.lasthandoff: 07/29/2017

---

# <a name="install-and-assign-configuration-manager-clients-from-the-internet-using-azure-ad-for-authentication"></a>認証のため Azure AD を使用して、インターネットから Configuration Manager クライアントをインストールして割り当てる

Configuration Manager Cloud Services と Azure AD を使用して、次のシナリオをサポートできます。

- インターネットから手動で Configuration Manager クライアントをインストールして、Configuration Manager サイトに割り当てる (クラウド管理ゲートウェイ サイト システムの役割が必要)。
- Configuration Manager サイトにアクセスするには、Azure AD を使用してインターネット上のクライアントを認証します。 Azure AD を使用すると、クライアント認証証明書を構成して使用する必要がなくなります。
- コレクションおよびその他の Configuration Manager の操作で使用するサイト内で Azure AD ユーザーを検出します。

これを実現するためには、次の手順を使用します。

- **手順 1: クラウド管理ゲートウェイを設定する**
- **手順 2: Configuration Manager Cloud Services で Azure サービス アプリを設定する**
- **手順 3: Windows 10 デバイスを Azure AD に登録するようにクライアント設定を構成する**
- **手順 4: Azure Active Directory ID を使用して、Configuration Manager クライアントをインストールして登録する**


## <a name="before-you-start"></a>アップグレードを開始する前に

- Azure AD テナントが必要です。
- デバイスで、Windows 10 が実行され、Azure AD が参加している必要があります。 参加している Azure AD に加え、クライアントもドメインに参加できます。
- 管理ポイントのサイト システムの役割に対する[既存の前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)に加え、**ASP.NET 4.5** (および自動的に選択されるその他のオプション) が、このサイト システムの役割をホストするコンピューターで有効になっていることを確認する必要があります。
- Configuration Manager を使用して、クライアントを展開するには:
    - HTTPS モード用に少なくとも 1 つの管理ポイントを構成します。
    - クラウド管理ゲートウェイを設定します。

## <a name="step-1-set-up-the-cloud-management-gateway"></a>手順 1: クラウド管理ゲートウェイを設定する

クライアントが証明書を使用せずにインターネットから Configuration Manager サイトにアクセスできるように、クラウド管理ゲートウェイを設定します。 次のトピックでヘルプを検索します。 

- [Configuration Manager でクラウド管理ゲートウェイを計画する](/sccm/core/clients/manage/plan-cloud-management-gateway)
- [Configuration Manager のクラウド管理ゲートウェイを設定する](/sccm/core/clients/manage/setup-cloud-management-gateway)
- [Configuration Manager でクラウド管理ゲートウェイを監視する](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway)

## <a name="step-2-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>手順 2: Configuration Manager Cloud Services で Azure サービス アプリを設定する

これにより、Configuration Manager サイトを Azure AD に接続します。これは、このセクションの他のすべての操作の前提条件です。 

Azure AD ユーザーの探索は、*クラウド管理*の一部として構成されています。 これを行う手順については、「*Configuration Manager と共に使用するように Azure サービスを構成する*」トピックの「[Configuration Manager と共に使用するように Azure Web アプリを作成する](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp)」の手順 **6** で詳しく説明されています。
    
手順を完了すると、Configuration Manager サイトが Azure AD に接続されます。 

## <a name="step-3-configure-client-settings-to-register-windows-10-devices-with-azure-ad"></a>手順 3: Windows 10 デバイスを Azure AD に登録するようにクライアント設定を構成する

1.  「[クライアント設定を構成する方法](/sccm/core/clients/deploy/configure-client-settings)」の情報を使用して、次のクライアント設定セクション ([クラウド サービス] にあります) を構成します。
    - **[新しい Windows 10 ドメインに参加しているデバイスを自動的に Azure Active Directory に登録する]**: **[はい]** (既定) または **[いいえ]** に設定します。
    - **[クライアントでクラウド管理ゲートウェイを使用できるようにする]**: **[はい]** (既定) または **[いいえ]** に設定します。
2.  クライアント設定を必要なデバイスのコレクションに展開します。

デバイスが Azure AD に参加していることを確認するには、コマンド プロンプト ウィンドウでコマンド **dsregcmd.exe/status** を実行します。 デバイスが Azure AD に参加している場合は、結果の **[AzureAdjoined]** フィールドに **[YES]** が表示されます。


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>手順 4: Azure Active Directory ID を使用して、Configuration Manager クライアントをインストールして登録する

開始する前に、クライアント インストール ソース ファイルが、クライアントをインストールするデバイスのローカルに保存されていることを確認します。 次に、次のインストール コマンド ラインを使用して、「[System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually)」の手順に従います。 

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso AADCLIENTAPPID= AADRESOURCEURI=https://contososerver**

- **/NoCrlCheck**: 管理ポイントまたはクラウド管理ゲートウェイが非公開のサーバー証明書を使用する場合、クライアントが CRL の場所に到達できない場合があります。
- **/Source**: ローカル フォルダー: クライアントのインストール ファイルの場所。
- **CCMHOSTNAME**: インターネット管理ポイントの名前。 これを見つけるには、管理対象クライアントのコマンド プロンプトから **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** を実行します。
- **SMSMP**: ルックアップ管理ポイントの名前。管理ポイントはイントラネットを指定することもできます。
- **SMSSiteCode**: Configuration Manager サイトのサイト コード。
- **AADTENANTID**、**AADTENANTNAME**: Configuration Manager にリンクした Azure AD テナントの ID と名前。 これを見つけるには、Azure AD に参加しているデバイスで、コマンド プロンプトから dsregcmd.exe/status を実行します。
- **AADCLIENTAPPID**: Azure AD のクライアント アプリ ID。 これを見つけるには、「[リソースにアクセスできる Azure Active Directory アプリケーションとサービス プリンシパルをポータルで作成する](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key)」を参照してください。
- **AADResourceUri**: 搭載された Azure AD サーバー アプリの識別子 URI。


## <a name="next-steps"></a>次のステップ

完了したら、引き続き[クライアントの監視と管理](/sccm/core/clients/manage/monitor-clients)ができます。

