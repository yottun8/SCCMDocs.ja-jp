---
title: アプリケーション管理を計画する
titleSuffix: Configuration Manager
description: Configuration Manager でアプリケーションを展開するために必要な依存関係を実装および構成します。
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df936f3ab5567840560497edd60a32f3bbb9c74d
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893603"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Configuration Manager のアプリケーション管理の計画と構成

*適用対象: System Center Configuration Manager (Current Branch)*

この記事の情報は、Configuration Manager でアプリケーションを展開するために必要な依存関係を適用するのに役立ちます。  



## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  


### <a name="internet-information-services-iis"></a>インターネット インフォメーション サービス (IIS)

次のサイト システムの役割を実行するサーバーでは IIS が必要です。 
- アプリケーション カタログ Web サイト ポイント  
- アプリケーション カタログ Web サービス ポイント  
- 管理ポイント  
- 配布ポイント  

この要件に関する詳細については、「[サイトとサイト システムの前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)」を参照してください。  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>モバイル デバイス用にコード署名されたアプリケーションでの証明書

モバイル デバイスに展開するためにアプリケーションをコード署名する場合は、バージョン 3 の証明書テンプレート (**Windows Server 2008 Enterprise Edition**) を使って作成された証明書を使用しないでください。 この証明書テンプレートは、モバイル デバイス用の Configuration Manager アプリケーションと互換性のない証明書を作成します。

Active Directory 証明書サービスを使ってモバイル デバイスのアプリケーションにコード署名する場合は、バージョン 3 の証明書テンプレートを使用しないでください。


### <a name="audit-sign-in-events-for-user-device-affinity"></a>ユーザーとデバイスのアフィニティに対するサインイン イベントを監査する  

ユーザーとデバイスのアフィニティを自動的に作成する場合、サインイン イベントを監査するようにクライアントを構成します。

自動的なユーザーとデバイスのアフィニティを判断するため、Configuration Manager クライアントは Windows のセキュリティ イベント ログから種類が **[成功]** のサインイン イベントを読み取ります。 次の 2 つの監査ポリシーでこれらのイベントを有効にします。
- **アカウント ログオン イベントの監査**
- **ログオン イベントの監査**

ユーザーとデバイス間に自動的に関係を作成するには、クライアント コンピューターでこれら 2 つの設定を有効にします。 Windows グループ ポリシーを使用してこれらの設定を構成できます。

ユーザーとデバイスのアフィニティの詳細については、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)」をご覧ください。  



## <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係   


### <a name="management-point"></a>管理ポイント

クライアントは、クライアント ポリシーのダウンロード、コンテンツの特定、およびアプリケーション カタログへの接続のために管理ポイントに接続します。 クライアントが管理ポイントにアクセスできない場合は、アプリケーション カタログを使用することはできません。

> [!Note]  
> バージョン 1806 以降では、ユーザーが利用できるアプリケーションをソフトウェア センターに表示するのにアプリケーション カタログの役割は必要なくなりました。 詳しくは、「[ソフトウェア センターの構成](#bkmk_userex)」をご覧ください。<!--1358309-->  
  

### <a name="distribution-point"></a>配布ポイント

アプリケーションをクライアントに展開する前に、階層内に少なくとも 1 つの配布ポイントが必要です。 既定では、標準インストール中に、サイト サーバーに配布ポイント サイトの役割が割り当てられます。 配布ポイントの数と場所は、環境の要件によって異なります。 

配布ポイントをインストールして、コンテンツを管理する方法の詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)」を参照してください。  


### <a name="reporting-services-point"></a>レポート サービス ポイント

Configuration Manager のレポートをアプリケーション管理に使用するには、まずレポート サービス ポイントをインストールして構成します。

詳細については、[Configuration Manager のレポート](/sccm/core/servers/manage/reporting)に関する記事を参照してください。  


### <a name="client-settings"></a>クライアント設定

クライアント設定の多くは、クライアントがアプリケーションをインストールする方法とデバイス上のユーザー エクスペリエンスを制御します。 これらのクライアント設定には次のようなグループがあります。
- コンピューター エージェント  
- コンピューターの再起動  
- ソフトウェア センター  
- ソフトウェアの展開  
- ユーザーとデバイスのアフィニティ  

詳細については、以下の記事を参照してください。
- [クライアント設定について](/sccm/core/clients/deploy/about-client-settings)  
- [クライアント設定を構成する方法](/sccm/core/clients/deploy/configure-client-settings)  


### <a name="security-permissions-for-application-management"></a>アプリケーション管理用のセキュリティのアクセス許可

- **アプリケーション作成者**セキュリティ ロールには、アプリケーションを作成し、変更し、廃止するのに必要なアクセス許可が含まれます。  

- **アプリケーション展開マネージャー** セキュリティ ロールには、アプリケーションを展開するために必要なアクセス許可が含まれます。  

- **[アプリケーション管理者]** セキュリティ ロールには、**[アプリケーション作成者]** および **[アプリケーション展開マネージャー]** セキュリティ ロール両方のすべてのアクセス許可が含まれます。  

詳細については、「[役割に基づいた管理の構成](/sccm/core/servers/deploy/configure/configure-role-based-administration)」を参照してください。  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>App-V 4.6 SP1 以降のクライアント (仮想アプリケーションを実行する場合)

Configuration Manager で仮想アプリケーションを作成するには、App-V 4.6 SP1 以降をデバイスにインストールします。

また、仮想アプリケーションを展開する前に、[サポート技術情報の記事 2645225](https://support.microsoft.com/help/2645225) で説明されている修正プログラムで App-V クライアントを更新します。  


### <a name="discovered-user-accounts-for-application-catalog"></a>アプリケーション カタログの検出されたユーザー アカウント

ユーザーがアプリケーション カタログでアプリケーションを表示し、要求できるようになるには、まず Configuration Manager でそのユーザー アカウントが検出されている必要があります。 詳細については、「[探索を実行する](/sccm/core/servers/deploy/configure/run-discovery)」を参照してください。  


### <a name="application-catalog-web-service-point"></a>アプリケーション カタログ Web サービス ポイント

アプリケーション カタログ Web サービス ポイントは、ソフトウェア ライブラリの利用可能なソフトウェアに関する情報を、ユーザーがアクセスするアプリケーション カタログ Web サイトに提供するサイト システムの役割です。

サイト システムの役割を構成する方法について詳しくは、このトピックの「[ソフトウェア センターの構成](#bkmk_userex)」をご覧ください。  

> [!Note]  
> バージョン 1806 以降、アプリケーション カタログ Web サービス ポイントの役割は "*不要*" になりましたが、まだ "*サポートされています*"。<!--1358309-->  
> 
> アプリケーション カタログ Web サイト ポイントの **Silverlight ユーザー エクスペリエンス**は現在サポートされていません。 詳細については、[削除された機能と非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)に関するページを参照してください。  


### <a name="application-catalog-website-point"></a>アプリケーション カタログ Web サイト ポイント

アプリケーション カタログ Web サイト ポイントは、利用可能なソフトウェアの一覧をユーザーに提供するサイト システムの役割です。
サイト システムの役割を構成する方法について詳しくは、このトピックの「[ソフトウェア センターの構成](#bkmk_userex)」をご覧ください。

> [!Note]  
> バージョン 1806 以降、アプリケーション カタログ Web サイト ポイントの役割は "*不要*" になりましたが、まだ "*サポートされています*"。<!--1358309-->  
> 
> アプリケーション カタログ Web サイト ポイントの **Silverlight ユーザー エクスペリエンス**は現在サポートされていません。 詳細については、[削除された機能と非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)に関するページを参照してください。  



## <a name="bkmk_userex"></a> ソフトウェア センターの構成  

ユーザーはソフトウェア センターから設定を変更し、アプリケーションを参照して、アプリケーションをインストールします。 Configuration Manager クライアントを Windows デバイスにインストールすると、ソフトウェア センターも自動的にインストールされます。 ソフトウェア センターは新しい現代的な外観へと一新されます。 Silverlight を使用するアプリケーション カタログにしか表示されなかったアプリ (ユーザーが利用できるアプリ) がソフトウェア センターの **[アプリケーション]** タブに表示されるようになりました。ソフトウェア センターの他の機能について詳しくは、「[ソフトウェア センターのユーザー ガイド](/sccm/core/understand/software-center)」をご覧ください。  

ソフトウェア センターの以下の機能強化を確認してください。 

#### <a name="starting-in-version-1802"></a>バージョン 1802 以降

- **[コンピューター エージェント]** グループのクライアント設定 **[新しいソフトウェア センターを使用する]** は、既定で有効になります。 前のバージョンのソフトウェア センターはサポートされなくなりました。 詳細については、[削除された機能と非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)に関するページを参照してください。  

- ユーザーは、Azure Active Directory (Azure AD) に参加しているデバイスで利用可能なアプリケーションを参照してインストールできます。 詳細については、[Azure AD 参加デバイスにユーザーが利用できるアプリケーションを展開する方法](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)に関するページを参照してください。  

#### <a name="starting-in-version-1806"></a>バージョン 1806 以降

- ソフトウェア センターの **[インストールのステータス]** タブで、アプリケーション カタログ Web サイト リンクの表示を指定します。 詳しくは、「[ソフトウェア センター](/sccm/core/clients/deploy/about-client-settings#software-center)」のクライアント設定をご覧ください。  

- ユーザーが利用できるアプリケーションをソフトウェア センターに表示するのにアプリケーション カタログの役割は必要なくなりました。 この変更は、ユーザーにアプリケーションを配布するために必要なサーバー インフラストラクチャを減らすのに役立ちます。 ソフトウェア センターは、この情報を取得するために管理ポイントに依存するようになりました。より大規模な環境を、[境界グループ](/sccm/core/servers/deploy/configure/boundary-groups#management-points)に割り当てることでより適切にスケーリングすることができます。<!--1358309-->  

    > [!Note]  
    > 現在、アプリケーション カタログを使用している場合は、Configuration Manager をバージョン 1806 に 更新しても動作し続けます。 アプリケーション カタログの Web サイト ポイントの役割と Web サービス ポイントの役割は "*不要*" になりましたが、まだ "*サポートされています*"。 アプリケーション カタログ "*Web サイト ポイント*" の **Silverlight ユーザー エクスペリエンス**は現在サポートされていません。 詳細については、[削除された機能と非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)に関するページを参照してください。 
    > 
    > 将来的にインフラストラクチャからアプリケーション カタログの役割を削除する計画を開始します。 ソフトウェア センターの機能強化を利用して管理ポイントを使用し、Configuration Manager 環境を簡素化します。  

特定のバージョンの Configuration Manager に依存するソフトウェア センターの要件を理解するには、次の表を参考にしてください。

| デバイスの種類 | サイトのバージョン | インフラストラクチャ | 
|-----------------|--------------|----------------|
| Azure AD 参加済みデバイス</br>(または "クラウド ドメイン参加済み") | 1802 または 1806 | すべてのアプリの展開に対する管理ポイント | 
| インターネット上の[ハイブリッド Azure AD 参加済み](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)デバイス | 1802 または 1806 | すべてのアプリの展開に対するクラウド管理ゲートウェイと管理ポイント |
| オンプレミスの Active Directory ドメイン参加済みデバイス | 1802 | ソフトウェア センターを介してユーザーが利用できるアプリに必要なアプリケーション カタログ |
| オンプレミスの Active Directory ドメイン参加済みデバイス | 1806 | すべてのアプリの展開に対する管理ポイント |


> [!Important]  
> Configuration Manager の新機能を利用するには、最初にクライアントを最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。



## <a name="branding-software-center"></a>ソフトウェア センターのブランド化

組織のブランド化要件を満たすようにソフトウェア センターの外観を変更します。 この構成はユーザーがソフトウェア センターを信頼するのに役立ちます。 

Configuration Manager では、次の優先順位に従って、ソフトウェア センターのカスタム ブランド化が適用されます。  

- アプリケーション カタログをインストールしていない場合 (推奨):  

    1. **ソフトウェア センター**のクライアント設定。 詳細については、「[クライアント設定について](/sccm/core/clients/deploy/about-client-settings#software-center)」を参照してください。  

    2. **[コンピューター エージェント]** グループでの **[組織名]** クライアント設定。 詳細については、「[クライアント設定について](/sccm/core/clients/deploy/about-client-settings#computer-agent)」を参照してください。  

- アプリケーション カタログをインストールしてある場合:  

    1. **ソフトウェア センター**のクライアント設定。 詳細については、「[クライアント設定について](/sccm/core/clients/deploy/about-client-settings#software-center)」を参照してください。  

    2. Microsoft Intune のサブスクリプションを Configuration Manager に接続する場合は、Intune サブスクリプションのプロパティで指定されている "*組織名*"、"*色*"、"*会社のロゴ*" がソフトウェア センターに表示されます。 詳細については、「 [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription)」をご覧ください。  

    3. アプリケーション カタログ Web サイト ポイントのプロパティで指定した "*組織名*" と "*色*"。 詳細については、「[Configuration options for Application Catalog website point](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website)」(アプリケーション カタログ Web サイト ポイントの構成オプション) をご覧ください。  

    4. **[コンピューター エージェント]** グループでの **[組織名]** クライアント設定。 詳細については、「[クライアント設定について](/sccm/core/clients/deploy/about-client-settings#computer-agent)」を参照してください。  

#### <a name="configure-software-center-branding"></a>ソフトウェア センターのブランド化を構成する
<!-- 1351224 --> 組織のブランド化要素を追加し、タブの表示を指定することにより、ソフトウェア センターの外観をカスタマイズします。 

詳細については、以下の記事を参照してください。
- [ソフトウェア センター](/sccm/core/clients/deploy/about-client-settings#software-center) グループのクライアント設定  
- [クライアント設定を構成する方法](/sccm/core/clients/deploy/configure-client-settings)  



## <a name="bkmk_appcat"></a> アプリケーション カタログをインストールして構成する  

> [!Note]  
> バージョン 1806 以降では、アプリケーション カタログの Web サイト ポイントの役割と Web サービス ポイントの役割は "*不要*" になりましたが、まだ "*サポートされています*"。 詳しくは、「[ソフトウェア センターの構成](#bkmk_userex)」をご覧ください。  
> 
> アプリケーション カタログ "*Web サイト ポイント*" の **Silverlight ユーザー エクスペリエンス**は現在サポートされていません。 詳細については、[削除された機能と非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)に関するページを参照してください。  

> [!IMPORTANT]  
>  これらの手順を実行する前に、すべての依存関係があることを確認します。 詳しくは、この記事の以下のセクションをご覧ください。
> - [Configuration Manager 外部の依存関係](#dependencies-external-to-configuration-manager)  
> - [Configuration Manager の依存関係](#configuration-manager-dependencies)


### <a name="step-1-web-server-certificate-for-https"></a>ステップ 1: HTTPS 用の Web サーバー証明書

HTTPS 接続を使用する場合は、アプリケーション カタログ Web サイト ポイントおよびアプリケーション カタログ Web サービス ポイント用のサイト システム サーバーに、Web サーバー証明書を展開します。 

クライアントでインターネットからアプリケーション カタログを使用する場合は、少なくとも 1 つの管理ポイントに Web サーバー証明書を展開します。 それをインターネットからのクライアント接続用に構成します。

証明書の要件の詳細については、[PKI 証明書の要件](/sccm/core/plan-design/network/pki-certificate-requirements)に関する記事をご覧ください。  


### <a name="step-2-client-authentication-certificate-for-https"></a>ステップ 2: HTTPS 用のクライアント認証証明書

管理ポイントへの接続にクライアント PKI 証明書を使用する場合は、クライアント認証証明書をクライアント コンピューターに展開します。 クライアントは、アプリケーション カタログに接続するためにクライアント PKI 証明書を使用することはありませんが、アプリケーション カタログを使用するには、まず管理ポイントに接続する必要があります。 

次のシナリオでは、クライアント認証証明書をクライアント コンピューターに展開します。
- イントラネットのすべての管理ポイントが、HTTPS クライアント接続のみを受け付けている。
- クライアントがインターネット経由でアプリケーション カタログに接続している。

証明書の要件の詳細については、[PKI 証明書の要件](/sccm/core/plan-design/network/pki-certificate-requirements)に関する記事をご覧ください。  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>ステップ 3: アプリケーション カタログの役割をインストールして構成する

アプリケーション カタログ Web サービス ポイントおよびアプリケーション カタログ Web サイト ポイントの両方の役割を、同じサイトにインストールします。 同じサーバー上または同じ Active Directory フォレスト内にインストールする必要はありません。 しかし、アプリケーション カタログの Web サービス ポイントは、サイト データベースと同じフォレストに置かれている必要があります。

サーバーの配置について詳しくは、「[サイト システム サーバーとサイト システムの役割の計画](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles)」をご覧ください。

> [!NOTE]  
> プライマリ サイトにアプリケーション カタログをインストールします。 セカンダリ サイトまたは中央管理サイトにインストールすることはできません。  

新しいサイト システム サーバーまたはサイト内の既存のサーバーに、アプリケーション カタログをインストールします。 一般的な手順について詳しくは、「[サイト システムの役割のインストール](/sccm/core/servers/deploy/configure/install-site-system-roles)」をご覧ください。 サイト システムの役割を追加するウィザードまたはサイト システム サーバーを作成するウィザードで、一覧から次の役割を選択します。  
- **アプリケーション カタログ Web サービス ポイント**  
- **アプリケーション カタログ Web サイト ポイント**  

> [!TIP]  
>  クライアント コンピューターがインターネット経由でアプリケーション カタログにアクセスできるようにするには、インターネット完全修飾ドメイン名 (FQDN) を指定します。  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>次にサイト システムの役割のインストールを確認する  

- ステータス メッセージ:コンポーネント **SMS_PORTALWEB_CONTROL_MANAGER** および **SMS_AWEBSVC_CONTROL_MANAGER**を使用します。  

    たとえば、**SMS_PORTALWEB_CONTROL_MANAGER** のステータス ID **1015** は、サイト コンポーネント マネージャーがアプリケーション カタログ Web サイト ポイントのインストールに成功したことを示します。  

- ログ ファイル: **SMSAWEBSVCSetup.log** および **SMSPORTALWEBSetup.log**を検索します。  

    詳細については、ログ ファイル、**awebsvcMSI.log** および **portlwebMSI.log** を検索してください。  


### <a name="step-4-configure-client-settings"></a>ステップ 4: クライアント設定を構成する

すべてのユーザーを同じ設定にする場合は、既定のクライアント設定を構成します。 または、コレクションごとにカスタムのクライアント設定を構成します。

詳細については、以下の記事を参照してください。
- [クライアント設定について](/sccm/core/clients/deploy/about-client-settings)  
    - コンピューター エージェント  
    - コンピューターの再起動  
    - ソフトウェア センター  
    - ソフトウェアの展開  
    - ユーザーとデバイスのアフィニティ  
- [クライアント設定を構成する方法](/sccm/core/clients/deploy/configure-client-settings)  

Configuration Manager クライアントでは、クライアント ポリシーの次回ダウンロード時に、これらの設定でデバイスが構成されます。 1 つのクライアントのポリシーの取得をトリガーする場合は、「[クライアントを管理する方法](/sccm/core/clients/manage/manage-clients)」をご覧ください。


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>ステップ 5: アプリケーション カタログが操作可能であることの確認

アプリケーション カタログが操作可能であることを確認するには、次の手順に従います。 

> [!NOTE]  
>  アプリケーション カタログのユーザー エクスペリエンスには、Microsoft Silverlight が必要です。 ブラウザーから直接アプリケーション カタログを使用する場合は、まずコンピューターに Microsoft Silverlight がインストールされていることを確認します。  

> [!TIP]  
>  前提条件を満たしていないことは、インストール後にアプリケーション カタログが正常に動作しない理由の中でも最も一般的なものです。 アプリケーション カタログ サイト システムの役割について、役割の前提条件を確認します。 詳細については、「[サイトとサイト システムの前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)」をご覧ください。  

ブラウザーで、アプリケーション カタログ Web サイトのアドレスを入力します。 Web ページに **[アプリケーション カタログ]**、**[アプリケーションの要求]**、**[デバイス]** の 3 つのタブが表示されることを確認します。  

アプリケーション カタログについては、以下の一覧の適切なアドレスを使用してください。&lt;サーバー&gt; は、コンピューター名、イントラネット FQDN、またはインターネット FQDN です。  

- HTTPS クライアント接続および既定のサイト システムの役割設定: **https://&lt;サーバー&gt;/CMApplicationCatalog**  

- HTTP クライアント接続および既定のサイト システムの役割設定: **http://&lt;サーバー&gt;/CMApplicationCatalog**  

- HTTPS クライアント接続およびカスタムのサイト システムの役割設定: **https://&lt;サーバー&gt;:&lt;ポート&gt;/&lt;Web アプリケーション名&gt;**  

- HTTP クライアント接続およびカスタムのサイト システムの役割設定: **http://&lt;サーバー&gt;:&lt;ポート&gt;/&lt;Web アプリケーション名&gt;**  

> [!NOTE]  
>  ドメイン管理者アカウントを使用してデバイスにサインインした場合、Configuration Manager クライアントの通知メッセージは表示されません。 たとえば、新しいソフトウェアが使用可能なことを示すメッセージなどです。  

