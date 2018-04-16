---
title: Upgrade Readiness
titleSuffix: System Center Configuration Manager
description: Upgrade Readiness と Configuration Manager を統合します。 管理コンソールでアップグレードの互換性データにアクセスします。 アップグレードまたは修復対象のデバイスを指定します。
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 96f20c3559ac08cb4c5a16d1d33b74c63a02e4b7
ms.sourcegitcommit: f0bfd9fa0ec5b416f0ea2beee889b94e2ad9c97d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2018
---
# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Upgrade Readiness と System Center Configuration Manager との統合

*適用対象: System Center Configuration Manager (Current Branch)*

Upgrade Readiness (旧 Upgrade Analytics) は、[Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) の一部で、Windows 10 にアップグレードするため、ご使用の環境内のデバイスの対応性を評価および分析することができます。 特定のバージョンを構成することができます。 Upgrade Readiness と System Center Configuration Manager を統合することで、クライアントは Configuration Manager 管理コンソールでアップグレードの互換性データにアクセスできるようになります。 このデータに基づいて作成された動的なコレクションを使用して、アップグレードまたは修復対象のデバイスを指定できます。

Upgrade Readiness は、[Microsoft Operations Management Suite (OMS)](/azure/operations-management-suite/operations-management-suite-overview) で実行するソリューションです。 Upgrade Readiness の詳細については、「[Manage Windows upgrades with Upgrade Readiness](/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness)」(Upgrade Readiness を使用した Windows アップグレードの管理) を参照してください。

<!--
>[!WARNING]
>For Upgrade Readiness to function within Configuration Manager, you must upgrade to Configuration Manager version 1802. The Upgrade Readiness Connector will no longer function in Configuration Manager versions earlier than 1802. 
SMS.507205 Pulled 4/5/18 -->


## <a name="configure-clients"></a>クライアントを構成する

Upgrade Readiness は、すべての Windows Analytics ソリューションと同様に、Windows の利用統計情報に依存します。 Upgrade Readiness が十分な利用統計情報を受信するためには、次の前提条件を満たす必要があります。

- すべてのクライアントは**商用 ID キー**を使用して構成する必要があります。 
- 少なくとも基本レベルのテレメトリをレポートするには、Windows 10 クライアントにテレメトリが構成されている必要があります。
-  Windows の以前のバージョンを実行しているクライアントには、「[Get started with Upgrade Readiness](/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs)」(Upgrade Readiness の概要) の説明に従って、特定の KB がインストールされている必要があります。 また、**[クライアント設定]** でテレメトリが有効になっている必要がありますす。

商用 ID キーと Windows テレメトリは、**[クライアント設定]** で構成できます。 詳細については、「[Configuration Manager で Windows Analytics を使用する](../monitor-windows-analytics.md)」を参照してください。

>[!NOTE]
>Upgrade Readiness が環境内のデバイスから利用統計情報を想定通りに受信しない問題が発生する場合、一部の問題は [Upgrade Readiness 展開スクリプト](/windows/deployment/upgrade/upgrade-readiness-deployment-script)を使用して対処できる場合があります。 しかし、正しい KB を展開しているほとんどの環境では、**[クライアント設定]** で商用 ID キーとテレメトリを構成すれば十分です。

## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Configuration Manager と Upgrade Readiness の接続

Current Branch バージョン 1706 以降、[Azure サービス ウィザード](../../../servers/deploy/configure/azure-services-wizard.md)を使用して、Configuration Manager で使用する Azure サービスの構成のプロセスを簡単にできます。 Configuration Manager と Upgrade Readiness を接続するには、[Azure Portal](https://portal.azure.com) で *[Web アプリ/API]* タイプの Azure AD アプリ登録を作成する必要があります。 アプリ登録の作成方法の詳細については、「[Azure Active Directory テナントにアプリケーションを登録する](/azure/active-directory/active-directory-app-registration)」をご覧ください。 **Azure Portal** で、Upgrade Readiness データをホストする OMS ワークスペースを含むリソース グループに対して、新しい登録済みの Web アプリの*共同作成者*アクセス許可を付与する必要もあります。 **Azure サービス ウィザード**は、このアプリ登録を使用して、Configuration Manager が Azure AD と安全に通信し、インフラストラクチャを Upgrade Readiness データに接続できるようにします。

>[!IMPORTANT]
>*共同作成者*アクセス許可は、Azure AD ユーザー ID ではなく、アプリ自体に付与する必要があります。 これは、Configuration Manager インフラストラクチャの代わりにデータにアクセスするのは登録済みアプリで、Azure AD ユーザーではないからです。 アクセス許可を与えるには、アクセス許可を割り当てるときに **[ユーザーの追加]** ブレードでアプリ登録名を検索する必要があります。 [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm) に接続するために [Configuration Manager に OMS へのアクセス許可を付与する](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms)場合も、これと同じ手順に従う必要があります。 これらの手順は、*Azure サービス ウィザード*を使用してアプリ登録が Configuration Manager にインポートされる前に完了する必要があります。

### <a name="use-the-azure-wizard-to-create-the-connection"></a>Azure ウィザードを使用して、接続を作成する

「[Configuration Manager と共に使用するように Azure サービスを構成する](../../../servers/deploy/configure/azure-services-wizard.md)」の指示に従い、上記で作成した Web アプリ登録をインポートすることで、Upgrade Readiness への接続を作成します。 

Web アプリのインポートが成功すると、*[構成]* ページに次の値があらかじめ設定され、**Azure Portal** で適切なアクセス許可が割り当てられます。 
-  Azure サブスクリプション
-  Azure リソース グループ
-  Windows Analytics ワークスペース

複数のリソース グループまたはワークスペースが使用できるのは、登録済みの Azure AD Web アプリに複数のリソース グループに対する*共同作成者*アクセス許可があるか、選択したリソース グループに複数の OMS ワークスペースが含まれている場合だけです。
 
## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Configuration Manager で Upgrade Readiness の情報を表示および使用する

Upgrade Readiness と Configuration Manager を統合したら、クライアントでのアップグレード準備の分析を表示できます。

1. Configuration Manager コンソールで、**[監視]** > **[概要]** > **[Upgrade Readiness]** の順に選択します。
2. アップグレードの準備状態、製品利用統計情報をレポートしている Windows デバイスの割合を含むデータを確認します。
3. 特定のコレクションでデバイス用のデータを表示するためにダッシュボードをフィルター処理することができます。
4. 特定の準備状態にあるデバイスを表示し、そのデバイスの動的コレクションを作成して、準備ができている場合はデバイスをアップグレードできるようにします。また、アップグレードが妨げられているデバイスを修復するための操作を実行することもできます。

## <a name="using-the-upgrade-readiness-connector-version-1702-and-earlier"></a>Upgrade Readiness コネクタ (バージョン 1702 以前) の使用

Configuration Manager バージョン 1702 以前では、Upgrade Readiness への接続を作成するには、異なる一連の手順と要件が必要です。

### <a name="prerequisites"></a>[前提条件]

- 接続を追加するために、Configuration Manager 環境で最初に[サービス接続ポイント](/sccm/core/servers/deploy/configure/about-the-service-connection-point)を[オンライン モード](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/)で構成する必要があります。 接続を環境に追加する場合、このサイト システムの役割を実行するマシンに Microsoft Monitoring Agent もインストールされます。
- "Web アプリケーションや Web API" 管理ツールとして Configuration Manager を登録し、[この登録のクライアント ID](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/) を取得します。
- Azure Active Directory で、登録済み管理ツールのクライアント キーを作成します。
- 「[Configuration Manager に OMS へのアクセス許可を付与する](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms)」の説明に従って、Azure Portal で、登録済みの Web アプリに OMS へのアクセス権を指定します。

    > [!IMPORTANT]
    > OMS へのアクセス権を構成する場合は、必ず、**共同作成者**ロールを選択し、登録済みアプリのリソース グループへのアクセス権を割り当ててください。

### <a name="create-the-connection"></a>接続を作成する

1.  Configuration Manager コンソールで、**[管理]** > **[クラウド サービス]** > **[Upgrade Readiness コネクタ]** > **[Upgrade Analytics への接続を作成します]** の順に選択し、**[Upgrade Analytics の接続を追加ウィザード]** を起動します。
3.  **[Azure Active Directory]** 画面で、**[テナント]**、**[クライアント ID]**、**[クライアントの秘密鍵]** を指定し、**[次へ]** を選択します。
4.  **[Upgrade Readiness]** 画面で、**[Azure サブスクリプション]**、**[Azure リソース グループ]**、および **[Operations Management Suite ワークスペース]** に入力し、接続設定を指定します。
5.  **[概要]** 画面で、**[次へ]** の接続設定を確認します。

    > [!NOTE]
    > Upgrade Readiness を階層の最上位サイトに接続する必要があります。 Upgrade Readiness をスタンドアロン プライマリ サイトに接続し、環境に中央管理サイトを追加する場合は、OMS 接続を削除し、新しい階層内に OMS 接続を再作成する必要があります。
