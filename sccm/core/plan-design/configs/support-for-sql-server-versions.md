---
title: サポートされている SQL Server のバージョン
titleSuffix: Configuration Manager
description: Configuration Manager サイト データベースをホストするための SQL Server のバージョンおよび構成要件を取得します。
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 962029dc6bc5584e1edf0bd26d4be3fc280d6204
ms.sourcegitcommit: 147aae8300831c722a559087c735df0f761b2041
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2018
ms.locfileid: "51645244"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Configuration Manager のサポートされている SQL Server バージョン

*適用対象: System Center Configuration Manager (Current Branch)*

それぞれの System Center Configuration Manager サイトには、サイト データベースをホストするためにサポートされている SQL Server バージョンおよび構成が必要です。  



##  <a name="bkmk_Instances"></a> SQL Server インスタンスと場所  
 
### <a name="central-administration-site-and-primary-sites"></a>中央管理サイトとプライマリ サイト  
 サイト データベースは SQL Server のフル インストールを使用する必要があります。  

 SQL Server は次の場所に配置できます。  

-   サイト サーバー コンピューター。  
-   サイト サーバーから離れたコンピューター。  

次のインスタンスがサポートされています。  

-   SQL Server の既定のインスタンスまたは名前付きインスタンス。  
-   複数インスタンス構成。  
-   SQL Server クラスター。 「[SQL Server クラスターを使用したサイト データベースのホスティング](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database)」を参照してください。
-   SQL Server AlwaysOn 可用性グループ。 詳しくは、「[高可用性サイト データベースの SQL Server AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)」をご覧ください。


### <a name="secondary-sites"></a>セカンダリ サイト  
 サイト データベースは SQL Server または SQL Server Express のフル インストールの既定のインスタンスを使用できます。  

 SQL Server はサイト サーバー コンピューターに配置する必要があります。  


### <a name="limitations-to-support"></a>サポートの制限事項   
 次の構成はサポートされていません。
 -   ネットワーク負荷分散 (NLB) クラスター構成の SQL Server クラスター
 -   クラスター共有ボリューム (CSV) 上の SQL Server クラスター
 -   SQL Server のデータベース ミラーリング テクノロジとピア ツー ピア レプリケーション

SQL Server のトランザクション レプリケーションは、[データベース レプリカ](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)を使用するように構成されている管理ポイントにオブジェクトをレプリケートする場合にのみサポートされます。  



##  <a name="bkmk_SQLVersions"></a> サポートされている SQL Server のバージョン  
 複数のサイトを含む階層では、それぞれのサイトが異なるバージョンの SQL Server を使用してサイト データベースをホストできます。 ただし、次の条件が満たされる場合です。
 -  Configuration Manager によってサポートされている SQL Server のバージョンを使用していること。
 -  使用する SQL Server のバージョンが、Microsoft によって引き続きサポートされていること。
 -  SQL Server で、SQL Server の 2 つのバージョン間のレプリケーションをサポートしていること。 たとえば、SQL Server では SQL Server 2008 R2 と SQL Server 2016 間のレプリケーションをサポートしていません。 詳しくは、「[SQL Server レプリケーションの非推奨の機能](https://docs.microsoft.com/sql/relational-databases/replication/deprecated-features-in-sql-server-replication)」をご覧ください。



 特に指定のない限り、次のバージョンの SQL Server はすべてのアクティブ バージョンの Configuration Manager でサポートされます。 新しい SQL Server バージョンまたは Service Pack のサポートが追加されている場合、そのサポートを追加する Configuration Manager バージョンが示されます。 同様に、サポートが非推奨とされる場合は、Configuration Manager の影響を受けるバージョンの詳細を確認してください。   

特定の SQL Server Service Pack のサポートには、基本の Service Pack バージョンへの後方互換性が失われる場合を除き、累積的な更新プログラムが含まれます。 Service Pack のバージョンが示されない場合、サポートは、そのバージョンの Service Pack なしの SQL Server に対するものです。 今後、SQL Server バージョンの Service Pack がリリースされた場合、新しい Service Pack バージョンがサポートされる前に、別のサポート ステートメントが宣言されます。


> [!IMPORTANT]  
>  中央管理サイトでデータベース用に SQL Server Standard を使用する場合、階層でサポートできるクライアントの合計数が制限されます。 「 [サイジングとスケールの数値](/sccm/core/plan-design/configs/size-and-scale-numbers)」をご覧ください。

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard、Enterprise  
[Configuration Manager バージョン 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710) 以降では次のサイトの最小の[累積的な更新プログラム バージョン 2](https://support.microsoft.com/help/4052574) で、このバージョンの SQL Server を使用できます。 

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト  
<!--SMS.498506-->

### <a name="sql-server-2016-sp2-standard-enterprise"></a>SQL Server 2016 SP2: Standard、Enterprise  
<!--514985--> 次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト  

### <a name="sql-server-2016-sp1-standard-enterprise"></a>SQL Server 2016 SP1: Standard、Enterprise  
次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト  

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard、Enterprise  
次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト  

### <a name="sql-server-2014-sp3-standard-enterprise"></a>SQL Server 2014 SP3: Standard、Enterprise  
次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト

### <a name="sql-server-2014-sp2-standard-enterprise"></a>SQL Server 2014 SP2: Standard、Enterprise  
次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト

### <a name="sql-server-2014-sp1-standard-enterprise"></a>SQL Server 2014 SP1: Standard、Enterprise  
 次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト

### <a name="sql-server-2012-sp4-standard-enterprise"></a>SQL Server 2012 SP4: Standard、Enterprise  
 次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト  

### <a name="sql-server-2012-sp3-standard-enterprise"></a>SQL Server 2012 SP3: Standard、Enterprise  
 次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト  

### <a name="sql-server-2008-r2-sp3-standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3: Standard、Enterprise、Datacenter     
  このバージョンの SQL Server はサポートされません。 詳細については、「[サイト データベースとしてのサポートが非推奨とされた SQL Server バージョン](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-support-for-sql-server-versions-as-a-site-database)」をご覧ください。  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express   
[Configuration Manager バージョン 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710) 以降では次のサイトの最小の[累積的な更新プログラム バージョン 2](https://support.microsoft.com/help/4052574) で、このバージョンの SQL Server を使用できます。
-   セカンダリ サイト <!--SMS.498506-->

### <a name="sql-server-2016-express-sp2"></a>SQL Server 2016 Express SP2  
次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。
-   セカンダリ サイト

### <a name="sql-server-2016-express-sp1"></a>SQL Server 2016 Express SP1  
次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。
-   セカンダリ サイト

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。
-   セカンダリ サイト

### <a name="sql-server-2014-express-sp3"></a>SQL Server 2014 Express SP3   
次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   セカンダリ サイト  

### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2   
次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   セカンダリ サイト  

### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1   
 次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   セカンダリ サイト  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
次のサイトの累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   セカンダリ サイト  



##  <a name="bkmk_SQLConfig"></a> SQL Server の必須構成  
 サイト データベースに使用する SQL Server (SQL Server Express を含む) のすべてのインストールでの要件は次のとおりです。 Configuration Manager が SQL Server Express をセカンダリ サイト インストールの一部としてインストールするときには、これらの構成は自動的に作成されます。  

### <a name="sql-server-architecture-version"></a>SQL Server アーキテクチャのバージョン  
 Configuration Manager には、サイト データベースをホストするために 64 ビット版の SQL Server が必要です。  

### <a name="database-collation"></a>データベース照合順序  
 各サイトでは、サイトとサイト データベースの両方に使用される SQL Server のインスタンスが、 **SQL_Latin1_General_CP1_CI_AS**の照合順序を使用する必要があります。  

 Configuration Manager は、GB18030 で定義されている中国で使用するための標準を満たすために、この照合順序に対して 2 つの例外をサポートしています。 詳細については、「[インターナショナル サポート](/sccm/core/plan-design/hierarchy/international-support)」をご覧ください。  

### <a name="database-compatibility-level"></a>データベース互換性レベル   
 Configuration Manager では、サイト データベースの互換性レベルがご利用の Configuration Manager バージョンでサポートされている最小の SQL Server バージョン以上である必要があります。 たとえば、バージョン 1702 以降では、[データベースの互換性レベル](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database)が 110 以上である必要があります。 <!-- SMS.506266--> 

### <a name="sql-server-features"></a>SQL Server の機能  
 各サイト サーバーに必要な機能は、 **データベース エンジン サービス** 機能のみです。  

 Configuration Manager データベース レプリケーションは、**SQL Server レプリケーション**機能を必要としません。 ただし、[管理ポイントのデータベース レプリカ](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)を使うときは、この SQL Server の構成が必要です。  

### <a name="windows-authentication"></a>Windows 認証  
 Configuration Manager は、データベースへの接続を検証するために、**Windows 認証**を必要とします。  

### <a name="sql-server-instance"></a>SQL Server インスタンス  
 サイトごとに専用の SQL Server のインスタンスを使用します。 インスタンスには、**名前付きインスタンス** か**既定のインスタンス**を使用できます。  

### <a name="sql-server-memory"></a>SQL Server のメモリ  
 SQL Server Management Studio を使用して、 **[サーバー メモリ オプション]** で **[最小サーバー メモリ]** 設定を指定して、SQL Server のメモリを予約します。 この設定を構成する方法について詳しくは、[SQL Server メモリに関するサーバー構成オプション](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options)に関するページをご覧ください。  

-   **サイト サーバーと同じコンピューターにインストールされたデータベース サーバーの場合**: SQL Server 用のメモリをアドレス可能なシステム メモリの 50% から 80% に制限します。  

-   **専用データベース サーバー (サイト サーバーからリモート) の場合**: SQL Server 用のメモリをアドレス指定可能なシステム メモリの 80% から 90% に制限します。  

-   **使用中の各 SQL Server インスタンスのバッファー プール用のメモリ予約の場合**:  

    -   中央管理サイト: 最小で 8 ギガバイト (GB) に設定  
    -   プライマリ サイト: 最小で 8 ギガバイト (GB) に設定  
    -   セカンダリ サイト: 最小で 4 ギガバイト (GB) に設定  

### <a name="sql-nested-triggers"></a>SQL の入れ子になったトリガー  
 SQL の入れ子になったトリガーを有効にする必要があります。 詳細については、「[nested triggers サーバー構成オプションの構成](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option)」をご覧ください。 

### <a name="sql-server-clr-integration"></a>SQL Server の CLR 統合  
  サイト データベースには、SQL Server 共通言語ランタイム (CLR) を有効にする必要があります。 このオプションは、Configuration Manager のインストール時に自動的に有効になります。 CLR の詳細については、「[SQL Server の CLR 統合の概要](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)」をご覧ください。  



##  <a name="bkmk_optional"></a> SQL Server のオプション構成  
 以下の構成は、SQL Server の完全インストールを使用する各データベースのオプションです。  

### <a name="sql-server-service"></a>SQL Server サービス  
 SQL Server サービスを、以下のものを使用して実行するように構成できます。  

-   *権限の低いドメイン ユーザー* アカウント:  

    -   この構成はベスト プラクティスであり、アカウントのサービス プリンシパル名 (SPN) を手動で登録しなければならない場合があります。  

-   SQL Server を実行しているコンピューターの**ローカル システム** アカウント:  

    -   ローカル システム アカウントを使用すると、構成プロセスが簡単になります。  
    -   ローカル システム アカウントを使用すると、Configuration Manager によって自動的に SQL Server サービスの SPN が登録されます。  
    -   SQL Server サービスにローカル システム アカウントを使用することは、SQL Server のベスト プラクティスではありません。  

SQL Server を実行するコンピューターが、ローカル システム アカウントを使用して SQL Server サービスを実行していない場合、SQL Server サービスを実行するアカウントの SPN を Active Directory Domain Services で構成します。 (システム アカウントを使用する場合、SPN が自動的に登録されます)。

サイト データベースの SPN について詳しくは、「[サイト データベース サーバーの SPN の管理](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_SPN)」をご覧ください。  

SQL Server サービスで使用されるアカウントを変更する方法について詳しくは、「[SCM サービス - サービス開始アカウントを変更する](https://docs.microsoft.com/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account)」をご覧ください。  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  
レポートを実行できるようにするレポート サービス ポイントをインストールするには、SQL Server Reporting Services が必要です。  

> [!IMPORTANT]  
> 以前のバージョンから SQL Server をアップグレードした後、「*Report Builder Does Not Exist*」 (レポート ビルダーが存在しません) というエラーが表示されることがあります。  
> このエラーを解決するには、レポート サービス ポイント サイト システムの役割を再インストールする必要があります。  

### <a name="sql-server-ports"></a>SQL Server のポート  
SQL Server データベース エンジンとの通信、およびサイト間のレプリケーションには、SQL Server の既定ポート構成を使用することも、カスタム ポートを指定することもできます。  

-   **サイト間の通信** には SQL Server Service Broker が使用され、既定ではポート TCP 4022 が使用されます。  
-   SQL Server データベース エンジンとさまざまな Configuration Manager サイト システムの役割の間の**サイト内通信**では、既定でポート TCP 1433 が使用されます。 次のサイト システムの役割は、SQL Server データベースと直接通信します。  

    -   管理ポイント  
    -   SMS プロバイダー コンピューター  
    -   レポート サービス ポイント  
    -   サイト サーバー  

SQL Server を実行しているコンピューターが複数のサイトからデータベースをホストする場合、各データベースは個別の SQL Server インスタンスを使用する必要があります。 さらに、各インスタンスは一意のポート セットを使用するように構成されている必要があります。  

> [!WARNING]  
>  Configuration Manager は、動的ポートをサポートしていません。 SQL Server 名前付きインスタンスの既定動作では、データベース エンジンへの接続に動的ポートが使用されるため、名前付きインスタンスの使用時に、サイト内通信に使用する静的ポートを手動で構成する必要があります。  

SQL Server を実行しているコンピューターのファイアウォールが有効に設定されている場合は、展開で使用されているポートと、SQL Server と通信するコンピューター間のネットワーク上のあらゆる場所にあるポートを許可するように構成してください。  

特定のポートを使用する SQL Server を構成する方法の例については、「[特定の TCP ポートで受信待ちするようにサーバーを構成する](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)」をご覧ください。  



## <a name="upgrade-options-for-sql-server"></a>SQL Server のアップグレード オプション

使用している SQL Server のバージョンをアップグレードする必要がある場合は、次の方法のいずれかを使用します (簡単な方法から順に示されています)。  

- [SQL Server をインプレースでアップグレードします](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (推奨)  

- 新しいコンピューターに新しいバージョンの SQL Server をインストールしてから、Configuration Manager セットアップの[データベースの移動オプションを使用](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration)して、サイト サーバーを新しい SQL Server にポイントします  

- [バックアップと回復](/sccm/protect/understand/backup-and-recovery)を使用します。 SQL アップグレード シナリオに対するバックアップと回復の使用がサポートされています。 「[サイトを回復する前の注意事項](/sccm/protect/understand/recover-sites#considerations-before-recovering-a-site)」を確認するとき、SQL のバージョンの要件は無視してかまいません。 
