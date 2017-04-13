---
title: "System Center Configuration Manager と Microsoft Intune を使ったハイブリッド Windows デバイス管理のセットアップ | Microsoft Docs"
description: "System Center Configuration Manager と Microsoft Intune を使用して Windows デバイス管理を設定します。"
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 4bf5cc25c4ffb89df620b02044f43a13adc1443e
ms.openlocfilehash: c87841ee1b30ebbcbbe8cd06309d909c38c01fdf
ms.lasthandoff: 04/06/2017


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使ったハイブリッド Windows デバイス管理のセットアップ

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、IT 管理者を対象に、ユーザーが Configuration Manager と Microsoft Intune を使用して、Windows PC とモバイル デバイスを管理できるようにする方法について説明します。

## <a name="enable-windows-device-management"></a>Windows デバイスの管理を有効にする
PC やモバイル デバイスの Windows デバイスの管理を有効にするには、次の手順を使用します。

1.  任意のプラットフォームの登録をセットアップする前に、「[ハイブリッド MDM をセットアップする](setup-hybrid-mdm.md)」に記載されている前提条件と手順を完了しておきます。  
2.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[概要]** > **[クラウド サービス]** > **[Microsoft Intune サブスクリプション]** に移動します。  
3.  リボンで、**[プラットフォームの構成]** をクリックし、Windows プラットフォームを選択します。
    - Windows PC やラップトップの場合は、**[Windows]** を選択し、次の手順を実行します。
      1. **[全般]** タブで **[Windows の登録を有効にする]**をクリックします。
      2. 証明書を使用して会社ポータル アプリにコード署名して展開する場合は、「**コード署名証明書**」を参照してください。 デバイスのユーザーが Windows ストアから会社ポータル アプリをインストールすることも、管理者がコード署名せずにビジネス向け Windows ストアからアプリを展開することもできます。
      3. [Windows Hello for Business 設定](windows-hello-for-business-settings.md)を構成することもできます。
    - Windows Phone やタブレットの場合は、**[Windows Phone]** を選択し、次の手順を実行します。
      1. **[全般]** タブで、**[Windows Phone 8.1 と Windows 10 Mobile]** チェック ボックスをオンにします。 Windows Phone 8.0 はサポートされなくなりました。
      2. 組織で会社アプリをサイドロードする必要がある場合は、必要なトークンやファイルをアップロードできます。 アプリのサイドローディングの詳細については、「[Windows アプリの作成](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications)」を参照してください。
        - **アプリケーション登録トークン**
        - **.pfx ファイル**
        - **[なし]** Symantec 証明書を使用する場合は、**[Symantec 証明書の有効期限が切れる前にアラートを表示する]** を指定できます。
4. [OK **** ] をクリックしてダイアログ ボックスを閉じます。  会社ポータルを使用して、登録プロセスを簡略化するには、デバイス登録用の DNS エイリアスを作成してください。 自分のデバイスを登録する方法をユーザーに通知することができます。

## <a name="choose-how-to-enroll-windows-devices"></a>Windows デバイスの登録方法を選択する
2 つの要素によって、Windows デバイスの登録方法が決まります。
- **Azure Active Directory Premium を使用していますか?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) は、Enterprise Mobility + Security およびその他のライセンス プランに付属します。
- **どのバージョンの Windows クライアントが登録されますか?** <br>Windows 10 デバイスは、職場または学校のアカウントを追加すると自動的に登録できます。 以前のバージョンでは、会社ポータル アプリを使用して登録する必要があります。

||**Azure AD Premium**|**その他の AD**|
|----------|---------------|---------------|  
|**Windows 10**|[自動登録](#automatic-enrollment) |[会社ポータルの登録](#company-portal-enrollment)|
|**以前の Windows バージョン**|[会社ポータルの登録](#company-portal-enrollment)|[会社ポータルの登録](#company-portal-enrollment)|

## <a name="automatic-enrollment"></a>自動登録

自動登録を使用して、職場や学校のアカウントを追加し、管理されることに同意すると、会社所有や個人の Windows 10 デバイスを登録できます。 ユーザーのデバイスはバックグラウンドで登録され、Azure Active Directory に接続されます。 登録されたデバイスは Intune で管理できるようになります。 管理対象のデバイスでは、タスクについては、引き続き会社ポータルを使用できますが、登録するためにインストールする必要はありません。

**必要条件**
- Azure Active Directory Premium サブスクリプション ([試用版サブスクリプション](http://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune サブスクリプション

### <a name="configure-automatic-enrollment"></a>自動登録の構成

1. [Azure Portal](https://manage.windowsazure.com) にサインインし、左側のウィンドウで **Active Directory** ノードに移動して、ディレクトリを選択します。
2. **[構成]** タブをクリックし、**[デバイス]** というセクションまでスクロールします。
3. **[Users may workplace join devices]** (ユーザーにデバイスのワークプレースへの参加を許可する) で **[すべて]** を選択します。
4. ユーザーごとに承認するデバイスの最大数を選択します。

既定では、サービスの 2 要素認証は有効になっていません。 ただし、デバイスを登録するときには 2 要素認証をお勧めします。 このサービスの 2 要素認証を要求する前に、Azure Active Directory で 2 要素認証プロバイダーを構成し、多要素認証用にユーザー アカウントを構成する必要があります。 「[クラウドでの Azure Multi-Factor Authentication Server の概要](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud)」を参照してください。


### <a name="create-dns-alias-for-device-enrollment"></a>デバイス登録の DNS エイリアスの作成  
DNS エイリアス (CNAME レコード タイプ) により、ユーザーはサーバー アドレスを入力することなくサービスに接続することができ、デバイスの登録が容易になります。 DNS エイリアス (CNAME レコード タイプ) を作成するには、Microsoft のクラウド サービスのサーバーに、会社のドメインの URL に送信された要求をリダイレクトする会社の DNS レコードで CNAME を構成する必要があります。  たとえば、会社のドメインが contoso.com の場合、EnterpriseEnrollment.contoso.com を EnterpriseEnrollment-s.manage.microsoft.com にリダイレクトする CNAME を DNS に作成する必要があります。  

CNAME DNS エントリの作成は省略可能ですが、CNAME レコードにより、ユーザーによる登録が簡単になります。 CNAME レコードの登録が見つからない場合、ユーザーは手動で MDM サーバー名 enrollment.manage.microsoft.com を入力するように求められます。

|型|ホスト名|指定先|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 時間|

複数の UPN サフィックスがある場合は、各ドメイン名について 1 つの CNAME レコードを作成し、それぞれで EnterpriseEnrollment s.manage.microsoft.com をポイントする必要があります。 たとえば、Contoso 社でユーザーが name@contoso.com を使用しており、電子メール/UPN として name@us.contoso.com と name@eu.constoso.com も使用している場合、Contoso の DNS 管理者は次の CNAME を作成する必要があります。

|型|ホスト名|指定先|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 時間|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 時間|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 時間|

## <a name="tell-users-how-to-enroll-devices"></a>デバイスの登録方法をユーザーに通知する  

 セットアップが完了したら、デバイスを登録する方法をユーザーに知らせる必要があります。 ガイダンスとして[デバイスの登録についてユーザーに通知する項目](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)に関する記事を参照してください。 ユーザーに「[Enroll your Windows device in Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows)」 (Intune での Windows デバイスの登録) のページを案内します。 この情報は、Microsoft Intune と Configuration Manager の両方によって管理されるモバイル デバイスに適用されます。

> [!div class="button"]
[< 前のステップ](create-service-connection-point.md)  [次のステップ >](set-up-additional-management.md)

