---
title: オンプレミス インフラストラクチャのアップグレード
titleSuffix: Configuration Manager
description: SQL Server やサイト システムの OS などのインフラストラクチャをアップグレードする方法について説明します。
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dc433d63eb647ef7a0a88ada212f949783ac25c0
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2018
ms.locfileid: "34474253"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>System Center Configuration Manager をサポートするオンプレミス インフラストラクチャのアップグレード

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager を実行するサーバー インフラストラクチャをアップグレードする場合は、この記事の情報を参考にしてください。  

 - 以前バージョンの Configuration Manager から System Center Configuration Manager (current branch) に*アップグレード*する場合は、「[System Center Configuration Manager へのアップグレード](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)」をご覧ください。

- System Center Configuration Manager (current branch) インフラストラクチャを新しいバージョンに*アップグレード*する場合は、「[System Center Configuration Manager の更新プログラム](/sccm/core/servers/manage/updates)」をご覧ください。



##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a> サイト システムの OS のアップグレード  
 Configuration Manager には、次の状況で、サイト サーバーをホストするサーバーとサイト システムの役割をホストするリモート サーバーのオペレーティング システム (0S) の一括アップグレードをサポートしています。  

-   アップグレード後の Service Pack レベルが Configuration Manager によってサポートされている場合の、Windows Server の上位 Service Pack への一括アップグレード。  
-   以下の一括アップグレード。
    - Windows Server 2012 R2 から Windows Server 2016 ([詳細を参照](#bkmk_2016))。
    - Windows Server 2012 から Windows Server 2016 ([詳細を参照](#bkmk_2016))。
    - Windows Server 2012 から Windows Server 2012 R2 ([詳細を参照](#bkmk_2012r2))。
    - Windows Server 2008 R2 から Windows Server 2012 R2 ([詳細を参照](#bkmk_from2008r2))。

    > [!WARNING]  
    >  異なる OS にアップグレードする前に、サーバーから "*WSUS をアンインストールする必要があります*"。 SUSDB を残しておき、WSUS を再インストールした後で再アタッチできます。 この重要な手順について詳しくは、Windows Server ドキュメントの「[Windows Server Update Services の概要](https://technet.microsoft.com/library/hh852345.aspx)」の「新機能と変更された機能」セクションをご覧ください。  

サーバーをアップグレードするには、アップグレード先の OS によって提供されるアップグレード手順を使用します。 次の記事をご覧ください。
  -  Windows Server のドキュメントの「[Windows Server 2012 R2 のアップグレード オプション](https://technet.microsoft.com/library/dn303416.aspx)」。  
  - Windows Server のドキュメントの「[Windows Server 2016 のアップグレード オプションと変換オプション](/windows-server/get-started/supported-upgrade-paths)」。

### <a name="bkmk_2016"></a> Windows Server 2012 または Windows Server 2012 R2 から Windows Server 2016 へのアップグレード
Windows Server 2012 または Windows Server 2012 R2 から Windows Server 2016 にアップグレードする場合は、以下が適用されます。


#### <a name="before-upgrade"></a>アップグレードの前に  
-   System Center Endpoint Protection (SCEP) クライアントを削除します。 Windows Server 2016 では、SCEP クライアントの代わりとして、Windows Defender が組み込まれています。 SCEP クライアントが存在している場合、Windows Server 2016 へのアップグレードが妨げられる可能性があります。
-   WSUS ロールがサーバーにインストールされている場合は削除します。 SUSDB を残しておき、WSUS を再インストールした後で再アタッチできます。

#### <a name="after-upgrade"></a>アップグレードの後に   
-   Windows Defender が有効であり、自動開始が設定され、実行されていることを確認します。
-   次の Configuration Manager のサービスが実行されていることを確認します。
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   **Windows プロセス アクティブ化**サービスと **WWW/W3svc** サービスが有効であり、自動開始が設定され、次のサイト システムの役割で実行されていることを確認します (これらのサービスはアップグレード時に無効になります)。
  -     サイト サーバー
  -     管理ポイント
  -     アプリケーション カタログ Web サービス ポイント
  -     アプリケーション カタログ Web サイト ポイント

-   サイト システムの役割をホストする各サーバーが、そのサーバーで実行される[サイト システムの役割の前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)のすべてを引き続き満たしていることを確認します。 たとえば、BITS、WSUS を再インストールしたり、IIS の特定の設定を構成したりすることが必要になる場合があります。

-   不足している前提条件を復元した後で、もう一度サーバーを再起動して、サービスが開始され、動作していることを確認します。

-   プライマリ サイト サーバーをアップグレードしている場合、[サイト リセットを実行](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset)します。

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>リモートの Configuration Manager コンソールに関する既知の問題   
サイト サーバーまたは SMS_Provider のインスタンスをホストするサーバーを Windows Server 2016 にアップグレードした後、管理ユーザーが Configuration Manager コンソールをサイトに接続できない場合があります。 この問題を回避するには、WMI の SMS Admins グループのアクセス許可を手動で復元する必要があります。 サイト サーバーと、SMS_Provider のインスタンスをホストする各リモート サーバーで、アクセス許可を設定する必要があります。

1. 該当するサーバー上で Microsoft 管理コンソール (MMC) を開き、**WMI コントロール**のスナップインを追加し、**[ローカル コンピューター]** を選択します。
2. MMC で、**[WMI コントロール (ローカル)]** の **[プロパティ]** を開き、**[セキュリティ]** タブを選択します。
3. ルートの下のツリーを展開し、**[SMS]** ノードを選択して、**[セキュリティ]** を選択します。  **SMS Admins** グループに次のアクセス許可が付与されていることを確認します。
  -     アカウントの有効化
  -     リモートの有効化
4. **[セキュリティ] タブ**で、**[SMS]** ノードの下にある **[site_&lt;sitecode**>] ノードを選択し、次に **[セキュリティ]** を選択します。 **SMS Admins** グループに次のアクセス許可が付与されていることを確認します。
  -   メソッドの実行
  -   プロバイダーによる書き込み
  -   アカウントの有効化
  -   リモートの有効化
5. アクセス許可を保存して、Configuration Manager コンソールへのアクセスを復元します。


### <a name="bkmk_2012r2"></a>Windows Server 2012 から Windows Server 2012 R2

#### <a name="before-upgrade"></a>アップグレードの前に  
-   WSUS ロールがサーバーにインストールされている場合は削除します。 SUSDB を残しておき、WSUS を再インストールした後で再アタッチできます。

#### <a name="after-upgrade"></a>アップグレードの後に  
  - Windows 展開サービスが開始され、次のサイト システムの役割を実行していることを確認します (このサービスはアップグレード時に停止されます)。
    - サイト サーバー
    - 管理ポイント
    - アプリケーション カタログ Web サービス ポイント
    - アプリケーション カタログ Web サイト ポイント

  -     **Windows プロセス アクティブ化**サービスと **WWW/W3svc** サービスが有効であり、自動開始が設定され、次のサイト システムの役割で実行されていることを確認します (これらのサービスはアップグレード時に無効になります)。
    -   サイト サーバー
    -   管理ポイント
    -   アプリケーション カタログ Web サービス ポイント
    -   アプリケーション カタログ Web サイト ポイント


  -     サイト システムの役割をホストする各サーバーが、そのサーバーで実行される[サイト システムの役割の前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)のすべてを引き続き満たしていることを確認します。 たとえば、BITS、WSUS を再インストールしたり、IIS の特定の設定を構成したりすることが必要になる場合があります。

  不足している前提条件を復元した後で、もう一度サーバーを再起動して、サービスが開始され、動作していることを確認します。

### <a name="bkmk_from2008r2"></a>Windows Server 2008 R2 から Windows Server 2012 R2 へのアップグレード
この OS のアップグレード シナリオには、次のような条件があります。  

#### <a name="before-upgrade"></a>アップグレードの前に  
-   WSUS 3.2 をアンインストールします。  
    サーバーの OS を Windows Server 2012 R2 にアップグレードする前に、サーバーから WSUS 3.2 をアンインストールする必要があります。 この重要な手順について詳しくは、Windows Server ドキュメントの「[Windows Server Update Services の概要](https://technet.microsoft.com/library/hh852345.aspx)」の「新機能と変更された機能」セクションをご覧ください。

#### <a name="after-upgrade"></a>アップグレードの後に  
  - Windows 展開サービスが開始され、次のサイト システムの役割を実行していることを確認します (このサービスはアップグレード時に停止されます)。
    - サイト サーバー
    - 管理ポイント
    - アプリケーション カタログ Web サービス ポイント
    - アプリケーション カタログ Web サイト ポイント


  -     **Windows プロセス アクティブ化**サービスと **WWW/W3svc** サービスが有効であり、自動開始が設定され、次のサイト システムの役割で実行されていることを確認します (これらのサービスはアップグレード時に無効になります)。
    -   サイト サーバー
    -   管理ポイント
    -   アプリケーション カタログ Web サービス ポイント
    -   アプリケーション カタログ Web サイト ポイント


  -     サイト システムの役割をホストする各サーバーが、そのサーバーで実行される[サイト システムの役割の前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)のすべてを引き続き満たしていることを確認します。 たとえば、BITS、WSUS を再インストールしたり、IIS の特定の設定を構成したりすることが必要になる場合があります。

  不足している前提条件を復元した後で、もう一度サーバーを再起動して、サービスが開始され、動作していることを確認します。


### <a name="unsupported-upgrade-scenarios"></a>サポートされていないアップグレードのシナリオ
次の Windows Server のアップグレード シナリオは、よく問い合わせが寄せられますが、Configuration Manager ではサポートされていません。  

-   Windows Server 2008 から Windows Server 2012 以降  
-   Windows Server 2008 R2 から Windows Server 2012



##  <a name="BKMK_SupConfigUpgradeClient"></a> Configuration Manager クライアントの OS のアップグレード  
 次の状況で、Configuration Manager は Configuration Manager クライアントの OS の一括アップグレードをサポートします。  

-   アップグレード後の Service Pack レベルが Configuration Manager によってサポートされている場合の、Windows の上位 Service Pack への一括アップグレード。  

-   Windows のサポートされているバージョンから Windows 10 への一括アップグレード。 詳細については、「[Windows を最新バージョンにアップグレードする](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)」をご覧ください。  

-   Windows 10 のビルドからビルドへのサービス アップグレード。 詳細については、「[サービスとしての Windows の管理](../../../osd/deploy-use/manage-windows-as-a-service.md)」を参照してください。  



##  <a name="BKMK_SupConfigUpgradeDBSrv"></a> サイト データベース サーバーでの SQL Server のアップグレード  
  Configuration Manager では、サイト データベース サーバー上の SQL のサポートされたバージョンからの、SQL Server の一括アップグレードをサポートしています。 このセクションの SQL Server のアップグレード シナリオは Configuration Manager でサポートされており、各シナリオの要件を含んでいます。

 Configuration Manager によってサポートされている SQL Server のバージョンの詳細については、「[SQL Server バージョンのサポート](../../../core/plan-design/configs/support-for-sql-server-versions.md)」をご覧ください。  

 ### <a name="upgrade-the-service-pack-version-of-sql-server"></a>SQL Server のサービス パック バージョンのアップグレード    
 Configuration Manager は、アップグレード後の SQL Server の Service Pack レベルが Configuration Manager によってサポートされている場合、SQL Server の上位 Service Pack への一括アップグレードをサポートします。

 階層内に複数の Configuration Manager サイトがある場合、各サイトで異なるバージョンの SQL Server のサービス パックを実行できます。 サイトのデータベースに使用される SQL Server のサービス パックのバージョンをアップグレードするサイトの順番に制限はありません。

### <a name="upgrade-to-a-new-version-of-sql-server"></a>SQL Server の新しいバージョンへのアップグレード   
 Configuration Manager は次のバージョンへの SQL Server の一括アップグレードをサポートしています。

 - SQL Server 2017
 - SQL Server 2016  
 - SQL Server 2014  

各サイトでサイト データベースをホストする SQL Server のバージョンをアップグレードする場合は、サイトで使用される SQL Server のバージョンを、次の順序でアップグレードする必要があります。

 1. 最初に中央管理サイトで SQL Server をアップグレードします。
 2. セカンダリ サイトの親プライマリ サイトをアップグレードする前に、セカンダリ サイトをアップグレードします。
 3. 最後に親プライマリ サイトをアップグレードします。 これらのサイトには、中央管理サイトに報告する子プライマリ サイトと、階層の最上位サイトであるスタンドアロンのプライマリ サイトの両方が含まれます。

### <a name="sql-server-cardinality-estimation-level-and-the-site-database"></a>SQL Server のカーディナリティ推定レベルおよびサイト データベース   
サイト データベースを以前のバージョンの SQL Server からアップグレードすると、既存の SQL カーディナリティ推定 (CE) レベルが SQL Server のそのインスタンスで許可されている最小レベルである場合に、データベースではそのレベルが保持されます。 許可レベルより低い互換性レベルのデータベースを持つ SQL Server をアップグレードすると、データベースは SQL で許可されている最も低い互換性レベルに設定されます。

次の表に、Configuration Manager サイト データベースで推奨される互換性レベルを示します。

|SQL Server バージョン | サポートされる互換性レベル |推奨レベル|
|----------------|--------------------|--------|
| SQL Server 2017 | 140、130、120、110  | 140 |
| SQL Server 2016 | 130、120、110  | 130 |
| SQL Server 2014 | 120、110      | 110 |

サイト データベースで使用されている SQL Server の CE 互換性レベルを識別するには、サイト データベース サーバーで次の SQL クエリを実行します。  
`SELECT name, compatibility_level FROM sys.databases`

 SQL CE の互換性レベルとその設定方法の詳細については、「[ALTER DATABASE 互換性レベル (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017)」を参照してください。


SQL Server のアップグレードについて詳しくは、次の SQL Server のドキュメントをご覧ください。
-   [SQL Server 2017 へのアップグレード](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)
-   [SQL Server 2016 へのアップグレード](/sql/database-engine/install-windows/supported-version-and-edition-upgrades)
-   [SQL Server 2014 へのアップグレード](http://technet.microsoft.com/library/ms143393\(v=sql.120))  



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>サイト データベース サーバー上の SQL Server をアップグレードするには  

1.  サイトのすべての Configuration Manager サービスを停止します。  
2.  SQL Server をサポートされるバージョンにアップグレードします。  
3.  Configuration Manager サービスを再起動します。  

> [!NOTE]  
>  中央管理サイトで使用している SQL Server のエディションを Standard エディションから Datacenter エディションまたは Enterprise エディションに変更する際には、階層がサポートするクライアントの数を制限するデータベースのパーティションは変更しません。
