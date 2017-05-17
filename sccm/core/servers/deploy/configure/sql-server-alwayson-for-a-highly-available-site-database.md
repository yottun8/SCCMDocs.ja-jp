---
title: SQL Server AlwaysOn | Microsoft Docs
ms.custom: na
ms.date: 1/4/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: aaaab003ddd22f18160d4be63cfeab3a7e7f6b03
ms.contentlocale: ja-jp
ms.lasthandoff: 05/17/2017


---
# <a name="sql-server-alwayson-for-a-highly-available-site-database-for-system-center-configuration-manager"></a>System Center Configuration Manager の高可用性サイト データベースの SQL Server AlwaysOn

*適用対象: System Center Configuration Manager (Current Branch)*


 System Center Configuration Manager バージョン 1602 以降では、高可用性および障害復旧のソリューションとして、SQL Server [AlwaysOn 可用性グループ](https://msdn.microsoft.com/library/hh510230\(v=sql.120\).aspx)を使用してプライマリ サイトと中央管理サイトでサイト データベースをホストできます。 可用性グループを社内または Microsoft Azure でホストできます。  

 Microsoft Azure を使用して可用性グループをホストする場合は、SQL Server AlwaysOn 可用性グループと Azure 可用性セットを使用することで、サイト データベースの可用性をさらに向上できます。 Azure 可用性セットの詳細については、「 [仮想マシンの可用性管理](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/)」を参照してください。  

 Configuration Manager では、内部または外部の負荷分散装置の後ろにある SQL 可用性グループでサイト データベースをホストできます。 各レプリカでのファイアウォール例外の設定に加えて、次のポートに負荷分散ルールを追加する必要があります。
  - SQL over TCP: TCP 1433
  - SQL Server Service Broker: TCP 4022
  - サーバー メッセージ ブロック (SMB): TCP 445
  - RPC エンドポイント マッパー: TCP 135


可用性グループでサポートされるシナリオを次に示します。  

-   サイト データベースを、可用性グループの既定のインスタンスに移動することができます  

-   サイト データベースをホストする可用性グループでレプリカ メンバーを追加したり、削除したりすることができます  

-   サイト データベースを、可用性グループから、スタンドアロン SQL Server の指定したインスタンスまたは既定のインスタンスに移動することができます  

> [!Important]  
> ハイブリッド構成で Microsoft Intune と Configuration Manager を使用する場合、可用性グループに対するサイト データベースの移動により、データとクラウドが再同期されます。 これを回避することはできません。 



> [!NOTE]  
>  可用性グループを正しく構成して使用するには、SQL Server および SQL Server 可用性グループの構成に習熟している必要があります。 このトピックの System Center Configuration Manager の手順を行うには、SQL Server ドキュメント ライブラリにある他のドキュメントと手順が必要です。  

 **AlwaysOn 可用性グループを Configuration Manager で使用する場合、次のような既知の問題があります。**  

-   **可用性グループを使用するよう Configuration Manager を設定する時点で、すべてのレプリカ サーバーに同じファイル パスが必要です。**  

    -   可用性グループ内のデータベースを使用するようサイトをリダイレクトするために Configuration Manager のセットアップを実行するときには、グループ内の各セカンダリ レプリカ サーバーに、現在のプライマリ レプリカでサイト データベース ファイルをホストするために使われるファイル パスと同じファイル パスが存在する必要があります。 同じパスがセカンダリ レプリカに存在しない場合、セットアップでは、サイト データベースの新しい場所として可用性グループ インスタンスを追加する操作が失敗します。  

         さらに、各セカンダリ レプリカ サーバー上のローカル SQL Server サービス アカウントは、このフォルダーに対する **フル コントロール** アクセス許可を持っている必要があります。  

         セットアップで可用性グループのデータベース インスタンスを指定するときに、セカンダリ レプリカ サーバーにはこのファイルのパスのみが必要です。  セットアップ時に可用性グループのサイト データベースの使用に関する変更が完了した後は、セカンダリ レプリカ サーバーから未使用のパスを削除できます。  

         たとえば、次の場合を考えてください。  

        -   3 つの SQL Server を使用する可用性グループを作成するとします  

        -   プライマリ レプリカ サーバーは、SQL Server 2014 の新規インストールです。  既定では、データベースの .MDF および .LDF ファイルが C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA に格納されます  

        -   両方のセカンダリ レプリカ サーバーが旧バージョンから SQL Server 2014 にアップグレードされ、データベース ファイルを格納する古いファイル パス (つまり C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA) を保持します  

        -   サイト データベースをこの可用性グループに移動するよう試す前に、各セカンダリ レプリカ サーバー上で C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA というファイル パス (プライマリ レプリカで使用されるのと同じパス) を作成する必要があります。セカンダリ レプリカでこのファイル場所を使用しない場合でも必要です。  

        -   次に、各セカンダリ レプリカ上の SQL Server サービス アカウントに、そのサーバーの新規作成されたファイル場所に対するフル コントロール アクセス許可を付与します  

        -   この時点で Configuration Manager のセットアップを正常に実行して、可用性グループ内のサイト データベースをサイトに使用させることができます  

-   **セットアップを実行して、サイト データベースに可用性グループを使用させるとき、次のようなエラーが ConfigMgrSetup.log ログに記録されることがあります。**  

    -   エラー: SQL Server エラー: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]データベースが読み取り専用であるため、データベース "CM_AAA" をアップデートできませんでした。   Configuration Manager Setup 1/21/2016 4:54:59 PM  7344 (0x1CB0)  

     セットアップ操作で可用性グループのセカンダリ レプリカ上のデータベース ロールを処理しようとするときに、このようなエラーが記録されます。 これらのエラーは無視してもかまいません。
- **追加の可用性グループをホストする SQL Server:**

  バージョン 1610 をインストールする前に、可用性グループを使用して Configuration Manager のセットアップを実行するか、Configuration Manager の更新プログラムをインストールする場合は、Configuration Manager 可用性グループをホストする SQL Server の追加の可用性グループの各レプリカに、次の構成が必要となります。
    - **手動フェールオーバー**
    - **読み取り専用接続を許可**


##  <a name="bkmk_BnR"></a> SQL Server AlwaysOn 可用性グループを使用するときのバックアップと回復の変更  
 **バックアップ:**  

 可用性グループでサイト データベースを実行するときには、一般的な Configuration Manager 設定とファイルをバックアップするために組み込み**バックアップ サイト** サーバー メンテナンス タスクを引き続き実行する必要がありますが、そのバックアップで作成された MDF ファイルと LDF ファイルを使用しないようご計画ください。 代わりに、SQL Server を使用して、サイト データベースの直接バックアップを作成することを計画します。  

 さらに、データベースの復旧モデルは「完全」に設定されていることから、サイト データベースのトランザクション ログ サイズの監視および維持を計画する必要があります。  完全復旧モデルでは、データベースまたはトランザクション ログの完全バックアップが作成されるまで、トランザクションは書き込まれません。 完全復旧モデルは、可用性グループのサイト データベースを使用するための要件であり、 Configuration Manager で使用するグループの構成時にこれが設定されます。 SQL Server のバックアップと復元の詳細については、SQL Server のドキュメントの「 [SQL Server データベースのバックアップと復元](https://msdn.microsoft.com/library/ms187048\(v=sql.120\).aspx) 」を参照してください。  

 **復元:**  

 サイト復元中に可用性グループの 1 つのノードが利用可能である限り、サイト復元オプション **[データベースの回復をスキップする (このオプションは、サイト データベースが障害の影響を受けていない場合に選択してください)]**を使用できます。  

 ただし、サイトを回復する前に、可用性グループのすべてのノードが失われた場合は、可用性グループを再作成する必要があります (System Center Configuration Manager は可用性ノードを再構築/復元することができません)。グループが再作成されて、バックアップが復元および再構成されたら、サイト復元オプション **[データベースの回復をスキップする (このオプションは、サイト データベースが障害の影響を受けていない場合に選択してください)]** を使用できるようになります。  

 バックアップおよび回復の詳細については、「[System Center Configuration Manager のバックアップと回復](../../../../protect/understand/backup-and-recovery.md)」を参照してください。  

##  <a name="bkmk_create"></a> Configuration Manager で使用する可用性グループの構成  
 次の手順を開始する前に、この構成を完了するために必要な SQL Server プロシージャについて、および Configuration Manager 用に構成する可用性グループに当てはまる次の詳細について理解しておきます。  

 **System Center Configuration Manager を使用する AlwaysOn 可用性グループの要件:**  

-  *バージョン*: 可用性グループの各ノード (またはレプリカ) は、System Center Configuration Manager によってサポートされる SQL Server バージョンを実行する必要があります SQL Server でサポートされる場合、可用性グループの別々のノードで、異なるバージョンの SQL Server を実行できます。   

- *エディション*: SQL Server の Enterprise エディションを使用する必要があります。  SQL Server 2016 Standard Edition で導入された基本的な可用性グループは、Configuration Manager ではサポートされていません。


-   可用性グループには、1 つのプライマリ レプリカを含める必要があり、最大 2 つの同期セカンダリ レプリカを含めることができます。  

-  データベースを可用性グループに追加した後、プライマリ レプリカをセカンダリにフェールオーバーする (これを新しいプライマリ レプリカにする) 必要があります。その後、次のようにデータベースを構成します。
    - Trustworthy を有効にする: True に等しい
    - Service Broker を有効にする: True に等しい
    - dbowner の設定: SA に等しい

    これらの設定値を構成するために、次のスクリプトを実行できます (cm_ABC はサイト データベースの名前)。  

    >     USE master  
    >     ALTER DATABASE cm_ABC SET NEW_BROKER   
    >     ALTER DATABASE cm_ABC SET ENABLE_BROKER  
    >     ALTER DATABASE cm_ABC SET TRUSTWORTHY ON;  
    >     USE cm_ABC  
    >     EXEC sp_changedbowner 'sa'  
    >     Exec sp_configure 'max text repl size (B)', 2147483647 reconfigure



-   可用性グループには、少なくとも 1 つの **可用性グループ リスナー**が必要です。  可用性グループのサイト データベースを使用するよう Configuration Manager を構成するときには、このリスナーの仮想名が使用されます。 可用性グループに複数のリスナーを含めることができますが、Configuration Manager はそのうち 1 つだけを使用できます  

-   各プライマリ レプリカおよびセカンダリ レプリカの要件は次のとおりです。  
    - **読み取り専用接続を許可**するように設定されている
    - **既定のインスタンス**を使用する
    - **手動フェールオーバー**に設定されている  

        > [!TIP]  
        >  System Center Configuration Manager は、自動フェールオーバーが設定されていると、可用性グループ レプリカの使用をサポートします。 ただし、セットアップを実行して可用性グループのサイト データベースの使用を指定するとき、および (サイト データベースに適用される更新プログラムだけでなく) すべての更新プログラムを Configuration Manager にインストールするときには、手動フェールオーバーに設定される必要があります。  

  **可用性グループの制限事項**
   - 基本的な可用性グループ (SQL Server 2016 Standard Edition で導入) はサポートされていません。 これは、基本的な可用性グループは、Configuration Manager で使用するための要件であるセカンダリ レプリカに対する読み取りアクセスをサポートしていないためです。 詳細については、「[基本的な可用性グループ (AlwaysOn 可用性グループ)](https://msdn.microsoft.com/en-us/library/mt614935.aspx)」を参照してください。

   - 可用性グループは、サイト データベースでのみサポートされ、ソフトウェア更新データベースやレポート データベースではサポートされません   
   - 可用性グループを使用するときには、可用性グループ リスナーではなく現在のプライマリ レプリカを使用するようレポート ポイントを手動で構成する必要があります。 プライマリ レプリカが別のレプリカにフェールオーバーした場合、新しいプライマリ レプリカを使用するようレポート ポイントを再構成する必要があります。  
   - バージョン 1606 などの更新プログラムをインストールする前に、可用性グループで手動フェールオーバーを必ず設定してください。 サイト更新後に、自動フェールオーバーに復元できます。



 **可用性グループを構成して使用するために必要なアクセス許可:**  

-   サイト サーバーのコンピューター アカウントは、可用性グループのメンバーである各コンピューターの **ローカル管理者** グループのメンバーである必要があります。  

#### <a name="to-configure-an-availability-group-to-host-a-site-database"></a>サイト データベースをホストする可用性グループを構成するには  

1.  Configuration Manager サイトを停止するには、次のコマンドを使用します。  
     **Preinst.exe /stopsite**  

     Preinst.exe の使用の詳細については、「[System Center Configuration Manager の階層メンテナンス ツール (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)」を参照してください。  

2.  サイト データベースのバックアップ モデルを **単純** から **完全**に変更します。  

     SQL Server のドキュメントの「 [データベースの復旧モデルの表示または変更](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) 」を参照してください。 (可用性グループは完全のみをサポートします)。  

3.  グループのプライマリ レプリカをホストするサーバーで、 **新しい可用性グループ ウィザード** を使用して可用性グループを作成します。 ウィザード:  

    -   **[データベースの選択]** ページで、 Configuration Manager サイトのデータベースを選びます  

    -   **[レプリカの指定]** ページで次のように構成します。  

        -   **レプリカ**: セカンダリ レプリカをホストするサーバーを指定します  

        -   **[リスナー]**: 完全な DNS 名として **[リスナー DNS 名]** を指定します (例: **&lt;Listener_Server>.fabrikam.com**)。 可用性グループのサイト データベースを使用するよう Configuration Manager を構成するときに、これが使用されます。

    -   **[最初のデータの同期を選択]** ページで、 **[完全]**を選びます。 ウィザードでは、可用性グループが作成された後に、プライマリ データベースとトランザクション ログがバックアップされて、セカンダリ レプリカをホストする各サーバーに復元されます。 この手順を使用しない場合は、セカンダリ レプリカをホストする各サーバーにサイト データベースのコピーを復元して、グループにそのデータベースを手動で結合する必要があります。  

    詳細については、SQL Server のドキュメントの「 [可用性グループ ウィザードの使用](https://msdn.microsoft.com/library/hh403415\(v=sql.120\).aspx) 」を参照してください。  

4.  可用性グループを構成した後、 **TRUSTWORTHY** プロパティを使用してプライマリ レプリカにサイト データベースを構成してから、 **[CLR 統合を有効にする]**を選びます。 これらの構成方法については、SQL Server のドキュメントの「 [TRUSTWORTHY データベース プロパティ](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) 」および「  [CLR 統合の有効化](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx) 」を参照してください。  

5.  次のことを実行して、可用性グループの各セカンダリ レプリカを構成します。  

    1.  現在のプライマリ レプリカをセカンダリ レプリカに手動でフェールオーバーします。 SQL Server のドキュメントの「 [可用性グループの計画的な手動フェールオーバーの実行 (SQL Server)](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) 」を参照してください。  

    2.  **TRUSTWORTHY** プロパティを使用して新しいプライマリ レプリカにサイト データベースを構成した後、 **[CLR 統合を有効にする]**を選びます。  

6.  すべてのレプリカがプライマリ レプリカおよび構成されたデータベースに昇格されると、可用性グループを Configuration Manager で使用できるようになります。  





##  <a name="bkmk_direct"></a> 可用性グループへのサイト データベースの移動  
 インストール済みサイトのサイト データベースを可用性グループに移動できます。 まず可用性グループを作成した後、可用性グループでの操作用にデータベースを構成する必要があります。  

 この手順を完了するには、Configuration Manager のセットアップを実行するユーザー アカウントが、可用性グループのメンバーである各コンピューターの**ローカル管理者**グループ メンバーである必要があります。  

#### <a name="to-move-a-site-database-to-an-availability-group"></a>サイト データベースを可用性グループに移動するには  

1.  **&lt;Configuration Manager サイトのインストール フォルダー\>\BIN\X64\setup.exe** から **Configuration Manager のセットアップ**を実行します。  

2.  **[作業の開始]** ページで、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]**を選択し、 **[次へ]**をクリックします。  

3.  **[SQL Server の構成を変更する]** オプションを選んでから、 **[次へ]**をクリックします。  

4.  サイト データベースを次のように再構成します。  

    -   **SQL Server 名** : 可用性グループの作成時に構成した可用性グループ リスナーの仮想名を入力します。 仮想名は、**&lt;endpointServer\>.fabrikam.com** のように完全な DNS 名にする必要があります  

    -   **インスタンス:** 可用性グループの可用性グループ リスナーの既定インスタンスを指定するには、この値を空白にする必要があります。  現在のサイト データベースが名前付きインスタンスにインストールされている場合は、表示される名前付きインスタンスがクリアされる必要があります。  

    -   **データベース:** 表示される名前のままにします。 これは、現在のサイト データベースの名前です。  

5.  新しいデータベースの場所の情報を入力したら、通常のプロセスと構成でセットアップを完了します。  

##  <a name="bkmk_change"></a> アクティブな可用性グループのメンバーを追加または削除する  
 可用性グループでホストされるサイト データベースを Configuration Manager が使用するようになったら、レプリカのメンバーを削除したり、他のレプリカ メンバーを追加したりできます (1 つのプライマリ ノードおよび 2 つのセカンダリ ノードを超過しない範囲で)。  

#### <a name="to-add-a-new-replica-member"></a>新しいレプリカ メンバーを追加するには  

1.  セカンダリ レプリカとして新しいサーバーを可用性グループに追加します。 SQL Server ドキュメント ライブラリの「  [可用性グループへのセカンダリ レプリカの追加 (SQL Server)](https://msdn.microsoft.com/library/hh213247\(v=sql.120\).aspx)」を参照してください。  

2.  **Preinst.exe /stopsite** を実行して、Configuration Manager サイトを停止します。詳細については、「[Hierarchy Maintenance Tool (Preinst.exe) for System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)」(System Center Configuration Manager の階層メンテナンス ツール (Preinst.exe)) を参照してください。  

3.  各セカンダリ レプリカを構成します。 次のことを実行して、可用性グループの各セカンダリ レプリカを構成します。  

    1.  プライマリ レプリカを新しいセカンダリ レプリカに手動でフェールオーバーします。 SQL Server のドキュメントの「 [可用性グループの計画的な手動フェールオーバーの実行 (SQL Server)](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) 」を参照してください。  

    2.  新しいサーバーのデータベースを Trustworthy に構成して、CLR 統合を有効にします。 SQL Server のドキュメントの「 [TRUSTWORTHY データベース プロパティ](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) 」および「  [CLR 統合の有効化](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx)」を参照してください。  

4.  サイト コンポーネント マネージャー (**sitecomp**) および **SMS_Executive** サービスを起動して、サイトを再開します。  

#### <a name="to-remove-a-replica-member-from-the-availability-group"></a>可用性グループからレプリカ メンバーを削除するには  

-   SQL Server のドキュメントの「 [可用性グループからのセカンダリ レプリカの削除](https://msdn.microsoft.com/library/hh213149\(v=sql.120\).aspx) 」の情報を使用します。  

##  <a name="bkmk_remove"></a> 可用性グループから単一インスタンス SQL Server にサイト データベースを戻す  
 可用性グループでサイト データベースをホストする必要がなくなったときには、次の手順に従います。  

#### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>可用性グループから単一インスタンス SQL Server にサイト データベースを戻すには  

1.  Configuration Manager サイトを停止するには、次のコマンドを使用します。  
     **Preinst.exe /stopsite**  詳細については、「[System Center Configuration Manager の階層のメンテナンス ツール (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)」を参照してください。  

2.  SQL Server を使用して、プライマリ レプリカからサイト データベースの完全バックアップを作成します。 この手順を完了する方法については、SQL Server のドキュメントの「 [データベースの完全バックアップの作成](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) 」を参照してください。  

3.  可用性グループのプライマリ レプリカをホストするサーバーが、サイト データベースの単一インスタンスをホストするようになる場合は、この手順を省略できます。  

    -   SQL Server を使用して、サイト データベースをホストするサーバーにサイト データベースのバックアップを復元します。  SQL Server のドキュメントの「 [データベースのバックアップの復元 (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx) 」を参照してください。  

4.  復元されたサイト データベースで、サイト データベースのバックアップ モデルを **完全** から **単純**に変更します。  SQL Server のドキュメントの「 [データベースの復旧モデルの表示または変更](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) 」を参照してください。  

5.  **&lt;Configuration Manager サイトのインストール フォルダー\>\BIN\X64\setup.exe** から **Configuration Manager のセットアップ**を実行します。  

6.  **[作業の開始]** ページで、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]**を選択し、 **[次へ]**をクリックします。  

7.  **[SQL Server の構成を変更する]** オプションを選んでから、 **[次へ]**をクリックします。  

8.  サイト データベースを次のように再構成します。  

    -   **SQL Server 名** : サイト データベースを現在ホストするサーバーの名前を入力します。  

    -   **インスタンス:** サイト データベースをホストする名前付きインスタンスを指定するか、データベースが既定のインスタンス上にある場合は空白のままにします。  

    -   **データベース:** 表示される名前のままにします。 これは、現在のサイト データベースの名前です。  

9. 新しいデータベースの場所の情報を入力したら、通常のプロセスと構成でセットアップを完了します。 セットアップが完了したら、サイトが再起動して新しいデータベースの場所の使用を開始します。  

10. 可用性グループのメンバーであったサーバーをクリーンアップするには、SQL Server のドキュメントの「 [可用性グループの削除](https://msdn.microsoft.com/library/ff878113\(v=sql.120\).aspx) 」の説明に従います。

