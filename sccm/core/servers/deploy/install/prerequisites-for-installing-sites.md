---
title: サイトの前提条件
titleSuffix: Configuration Manager
description: さまざまな種類の Configuration Manager サイトをインストールするための前提条件について説明します。
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 818065f4ea3f537dc565d06c278b710b224a4031
ms.sourcegitcommit: f0ec334a70d0cdd3f5f185ac7787b700947f82de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2019
ms.locfileid: "55303218"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>Configuration Manager サイトのインストールの前提条件

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

サイトのインストールを開始する前に、さまざまな種類の Configuration Manager サイトをインストールするための前提条件について説明します。



## <a name="primary-sites-and-the-central-administration-site"></a>プライマリ サイトと中央管理サイト

以下の前提条件は、次のいずれかの種類のインストールに適用されます。
- 階層の最初のサイトとしての中央管理サイト
- スタンドアロン プライマリ サイト
- 子プライマリ サイト

階層拡張の一部として中央管理サイトをインストールする場合は、「[スタンドアロン プライマリ サイトを拡張する](#bkmk_expand)」を参照してください。


###  <a name="bkmk_PrereqPri"></a> プライマリ サイトまたは中央管理サイトをインストールするための前提条件  

- サイトをインストールするユーザー アカウントには、次の権限が必要です。  

    - 次のサーバーでの**管理者**:  
        - サイト サーバー  
        - **サイト データベース**をホストする各サーバー  
        - サイトに対する **SMS プロバイダー**の各インスタンス  

    - サイト データベースをホストする SQL Server インスタンスの **Sysadmin**  

        > [!IMPORTANT]  
        >  Configuration Manager のセットアップが完了したら、セットアップを実行するユーザー アカウントと、サイト サーバー コンピューター アカウントの両方で SQL Server の sysadmin 権限を保持する必要があります。 これらのアカウントから sysadmin 権限を削除しないでください。  

- プライマリ サイトをインストールする場合は、次の権限も必要です。  

    - 最初の管理ポイントと配布ポイントをインストールする追加のサーバーの**管理者** (サイト サーバーにインストールしない場合)  

- 中央管理サイトの下に新しい子プライマリ サイトをインストールする場合は、次の権限も必要です。  

    - 中央管理サイトをホストするサーバーの**管理者**  

    - **インフラストラクチャ管理者**または**完全な権限を持つ管理者**のセキュリティ ロールと同等の、Configuration Manager 内のロール ベース管理権限  

- 正しいインストール ソース ファイルを使用して、その場所からセットアップを実行します。 別の種類のサイトのインストールに使用する適切なソース ファイルについては、「[異なる種類のサイトをインストールするためのオプション](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options)」をご覧ください。  

- サイト サーバーは、次のいずれかの方法で Microsoft から更新されたセットアップ ファイルにアクセスできる必要があります。  

    - インストールを始める前に、これらのファイルのコピーをダウンロードしてローカル ネットワークに保存します。 詳細については、「[セットアップ ダウンローダー](/sccm/core/servers/deploy/install/setup-downloader)」を参照してください。  

    - これらのファイルのローカル コピーを使用できない場合は、サイト サーバーがインターネットにアクセスできる必要があります。 サーバーは、インストールの間にこれらのファイルを Microsoft からダウンロードします。  

- サイト サーバーとサイト データベース サーバーは、すべての前提条件の構成を満たしている必要があります。 Configuration Manager のセットアップを始める前に、[前提条件チェッカーを手動で実行して](/sccm/core/servers/deploy/install/prerequisite-checker)、問題を特定し、修正します。  


### <a name="bkmk_expand"></a> スタンドアロン プライマリ サイトを拡張するための前提条件

スタンドアロン プライマリ サイトを中央管理サイトがある階層に拡張するには、スタンドアロン プライマリ サイトが次の前提条件を満たしている必要があります。

#### <a name="source-file-version-matches-site-version"></a>ソース ファイルのバージョンがサイトのバージョンと一致している
スタンドアロン プライマリ サイトのバージョンと一致するメディアを CD.Latest フォルダーから使用して、新しい中央管理サイトをインストールします。 バージョンを確実に一致させるには、スタンドアロン プライマリ サイト上の [CD.Latest フォルダー](/sccm/core/servers/manage/the-cd.latest-folder)内にあるソース ファイルを使用します。 

異なるサイトのインストールに使用する適切なソース ファイルについて詳しくは、「[異なる種類のサイトをインストールするためのオプション](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options)」をご覧ください。  

#### <a name="stop-active-migration-from-another-hierarchy"></a>別の階層からのアクティブな移行を停止する
別の Configuration Manager 階層からデータを移行するように、スタンドアロン プライマリ サイトを構成することはできません。 他の Configuration Manager 階層からのスタンドアロン プライマリ サイトへのアクティブな移行を停止し、移行のすべての構成を削除します。 次のような構成です。 
- 完了していない移行ジョブ  
- データ収集  
- アクティブなソース階層の構成  

Configuration Manager は階層の最上位サイトからデータを移行するため、このような構成が必要です。 スタンドアロン プライマリ サイトを拡張するとき、移行の構成は中央管理サイトに転送されません。  

スタンドアロン プライマリ サイトを拡張した後で、プライマリ サイトで移行を再構成する場合、中央管理サイトが移行操作を実行します。 

移行を構成する方法について詳しくは、[移行のためのソース階層とソース サイトの構成](/sccm/core/migration/configuring-source-hierarchies-and-source-sites-for-migration)に関するページをご覧ください。  

#### <a name="computer-account-as-administrator"></a>管理者としてのコンピューター アカウント
新しい中央管理サイトをホストするサーバーのコンピューター アカウントは、スタンドアロン プライマリ サイト サーバーの**管理者**グループのメンバーである必要があります。 

スタンドアロン プライマリ サイトを正常に拡張するには、中央管理サイトのコンピューター アカウントが、スタンドアロン プライマリ サイトの**管理者**権限を持っている必要があります。 これは、サイトの拡張中にのみ必要です。 サイトの拡張が完了したら、プライマリ サイトのユーザー グループからアカウントを削除できます。  

#### <a name="installation-account-permissions"></a>インストール アカウント アクセス許可
新しい中央管理サイトをインストールするために Configuration Manager セットアップを実行するユーザー アカウントには、スタンドアロン プライマリ サイトの役割ベースの管理権限が必要です。

サイト拡張の一環として中央管理サイトをインストールする場合は、その中央管理サイトをインストールするためのセットアップを実行するユーザー アカウントが、スタンドアロン プライマリ サイトの役割ベース管理において、 **完全な権限を持つ管理者**または**インフラストラクチャ管理者**として定義されている必要があります。  

#### <a name="top-level-site-roles"></a>最上位サイトの役割
サイトを拡張する前に、次のサイト システムの役割をスタンドアロン プライマリ サイトからアンインストールします。

- 資産インテリジェンス同期ポイント  
- Endpoint Protection ポイント  
- [サービス接続ポイント]  

Configuration Manager では、階層の最上位サイトにおいてのみ、これらの役割がサポートされます。 スタンドアロン プライマリ サイトを拡張する前に、これらのサイト システムの役割をアンインストールします。 サイトを拡張した後、中央管理サイトでこれらのサイト システムの役割を再インストールします。  

その他のサイト システムの役割は、すべてプライマリ サイトにインストールしたままにできます。  

#### <a name="open-the-sql-server-service-broker-port"></a>SQL Server Service Broker のポートを開く
スタンドアロン プライマリ サイトと、中央管理サイト用のサーバーの間で、SQL Server Service Broker (SSB) 用にネットワーク ポートを開く必要があります。  

Configuration Manager で、中央管理サイトとプライマリ サイト間でデータを正常にレプリケートするには、SSB で使用されるポートが 2 つのサイト間で開かれている必要があります。 中央管理サイトをインストールし、スタンドアロン プライマリ サイトを拡張するときに、前提条件のチェックでは、SSB 用に指定したポートがプライマリ サイトで開かれていることを確認しません。  

#### <a name="known-issues-with-azure-services"></a>Azure サービスに関する既知の問題
Configuration Manager で次の Azure サービスのいずれかを使用するときは、サイトの拡張後に、そのサービスへの接続を削除して再作成します。

- [Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics)  
- [アップグレードの準備](/sccm/core/clients/manage/upgrade/upgrade-readiness)  
- [ビジネス向け Microsoft ストア](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)  

次の手順でこの問題を解決してください。
 1. Configuration Manager コンソールで、**Azure サービス** ノードから Azure サービスを削除します。  

 2. Azure portal で、Azure Active Directory テナント ノードからサービスに関連付けられているテナントを削除します。 これにより、サービスに関連付けられている Azure AD Web アプリも削除されます。  

 3. Configuration Manager で使用する Azure サービスとの接続を再構成します。  



## <a name="bkmk_secondary"></a> セカンダリ サイト

次の表は、セカンダリ サイトのインストールの前提条件を示しています。

- Configuration Manager コンソールでセカンダリ サイトのインストールを構成する管理者は、**インフラストラクチャ管理者**または**完全な権限を持つ管理者**のセキュリティ ロールと同等の、役割に基づいた管理権限を持っている必要があります。  

- 親プライマリ サイトのコンピューター アカウントは、セカンダリ サイト サーバーの**管理者**である必要があります。  

- 事前にインストールした SQL Server のインスタンスをセカンダリ サイトで使用して、セカンダリ サイト データベースをホストする場合:  

    - 親プライマリ サイトのコンピューター アカウントは、セカンダリ サイト サーバーの SQL Server インスタンスの **sysadmin** 権限を持っている必要があります。  

    - セカンダリ サイト サーバー コンピューターの**ローカル システム** アカウントは、セカンダリ サイト サーバーの SQL Server インスタンスの **sysadmin** 権限を持っている必要があります。  

        > [!IMPORTANT]  
        >  Configuration Manager のセットアップが完了したら、両方のアカウントで SQL Server の sysadmin 権限を保持する必要があります。 これらのアカウントから sysadmin 権限を削除しないでください。  

- セカンダリ サイト サーバーは、すべての前提条件の構成を満たしている必要があります。 そのような構成には、SQL Server と、管理ポイントと配布ポイントの既定のサイト システムの役割が含まれます。  
