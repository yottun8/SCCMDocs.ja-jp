---
title: 可用性グループを構成する
titleSuffix: Configuration Manager
description: SCCM で SQL Server AlwaysOn 可用性グループをセットアップして管理します。
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2baafa04c315ebc7512504f042c89615b7217b4c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Configuration Manager の SQL Server Always On 可用性グループを構成する

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager で使用する可用性グループを構成し、管理するには、このトピックを参照してください。

始める前に  
-   「[System Center Configuration Manager の高可用性サイト データベースの SQL Server AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)」の内容を理解しておいてください。
-   可用性グループの使用方法と関連する手順を説明した SQL Server ドキュメントを理解しておいてください。 ドキュメントの情報は、以下のシナリオを完了するために必要になります。

> [!TIP]  
>  このトピックに掲載されている SQL Server のリンクをクリックすると、SQL Server 2016 のコンテンツが表示されます。 このバージョン以外の SQL Server を使用している場合は、そのバージョンのドキュメントを参照してください。

## <a name="create-and-configure-an-availability-group"></a>可用性グループの作成と構成
可用性グループを作成し、サイト データベースのコピーをその可用性グループに移動するには、次の手順を実行します。

この手順を完了するには、次のアカウントを使用する必要があります。
-   可用性グループに含める各コンピューターの**ローカル管理者**グループのメンバー。
-   サイト データベースをホストする各 SQL Server インスタンスの **sysadmin**。

### <a name="to-create-and-configure-an-availability-group-for-configuration-manager"></a>Configuration Manager の可用性グループを作成して構成するには  
1.  Configuration Manager サイトを停止するには、コマンド **Preinst.exe /stopsite** を使用します。 PreInst.exe の使用方法については、「[System Center Configuration Manager の階層のメンテナンス ツール (Preinst.exe)](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)」を参照してください。

2.  サイト データベースのバックアップ モデルを **単純** から **完全**に変更します。
SQL Server のドキュメントの「 [データベースの復旧モデルの表示または変更](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) 」を参照してください。 (可用性グループは完全のみをサポートします)。

3.  SQL Server を使用してサイト データベースの完全バックアップを作成します。 次に、サイト データベースをホストするサーバーを新しい可用性グループのレプリカ メンバーにするかどうかに応じて、次のいずれかを実行します。
    -   **可用性グループのメンバーにする:**  
        可用性グループの最初のプライマリ レプリカ メンバーとしてこのサーバーを使用する場合、グループ内のこのサーバーまたは別のサーバーにサイト データベースのコピーを復元する必要はありません。 データベースはプライマリ レプリカに既に存在し、後の手順で SQL Server はデータベースをセカンダリ レプリカにレプリケートします。  

      -    **可用性グループのメンバーにしない:**   
    グループのプライマリ レプリカをホストするサーバーに、サイト データベースのコピーを復元します。

    この手順を完了する方法については、SQL Server ドキュメントの「[データベースの完全バックアップの作成](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)」および「[SSMS を使用したデータベース バックアップの復元](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)」を参照してください。

4.  グループの最初のプライマリ レプリカをホストするサーバーで、[新しい可用性グループ ウィザード](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio)を使用して可用性グループを作成します。 ウィザード:
      -    **[データベースの選択]** ページで、Configuration Manager サイトのデータベースを選択します。  

      -    **[レプリカの指定]** ページで次のように構成します。
          -    **レプリカ:** セカンダリ レプリカをホストするサーバーを指定します。

          -    **リスナー**: 完全な DNS 名として **[リスナー DNS 名]** を指定します (例: **&lt;Listener_Server>.fabrikam.com**)。可用性グループのサイト データベースを使用するよう Configuration Manager を構成するときに、これが使用されます。

      -    **[最初のデータの同期を選択]** ページで、 **[完全]** を選びます。 ウィザードでは、可用性グループが作成された後に、プライマリ データベースとトランザクション ログがバックアップされます。 それから、セカンダリ レプリカをホストする各サーバーで復元されます。 (この手順を使用しない場合は、セカンダリ レプリカをホストする各サーバーにサイト データベースのコピーを復元して、グループにそのデータベースを手動で結合する必要があります)。   

5.  各レプリカで構成を確認します。   
  1.    サイト サーバーのコンピューター アカウントが、可用性グループのメンバーである各コンピューターの**ローカル管理者**グループのメンバーであることを確認します。  

  2.  前提条件の[検証スクリプト](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites)を実行して、各レプリカのサイト データベースが正しく構成されていることを確認します。

  3.    セカンダリ レプリカで構成を設定する必要がある場合は、続行する前にプライマリ レプリカをセカンダリ レプリカに手動でフェールオーバーしておく必要があります。 構成できるのはプライマリ レプリカのデータベースだけです。 詳細については、SQL Server ドキュメントの「[可用性グループの計画的な手動フェールオーバーの実行](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server)」を参照してください。

6.  すべてのレプリカが要件を満たすようになったら、Configuration Manager で可用性グループを使用する準備は完了です。

## <a name="configure-a-site-to-use-the-database-in-the-availability-group"></a>可用性グループでデータベースを使用するようにサイトを構成する
[可用性グループの作成と構成](#create-and-configure-an-availability-group)が完了したら、Configuration Manager サイトのメンテナンスを使用して、可用性グループでホストされているデータベースを使用するようにサイトを構成します。

可用性グループ内のデータベースを使用して、新しいサイトをインストールする方法はサポートされていません。 たとえば、ベースライン 1702 メディアを使用している場合、単一インスタンスの SQL Server を使用してサイトをインストールする必要があります。 サイトのインストール後は、サイト データベースを可用性グループに移動することができます。

この手順を完了するには、Configuration Manager のセットアップを実行する際に、次のアカウントを使用する必要があります。
-   可用性グループのメンバーである各コンピューターの**ローカル管理者**グループのメンバー。
-   サイト データベースをホストする各 SQL Server インスタンスの **sysadmin**。

> [!IMPORTANT]
> ハイブリッド構成で Microsoft Intune と Configuration Manager を使用する場合、サイト データベースを可用性グループに移動したり、可用性グループから移動すると、データがクラウドと再同期されます。 この再同期は回避できません。

### <a name="to-configure-a-site-to-use-the-availability-group"></a>可用性グループを使用するようにサイトを構成するには
1.  **&lt;*Configuration Manager サイトのインストール フォルダー*>\BIN\X64\setup.exe** から **Configuration Manager のセットアップ**を実行します。

2.  **[作業の開始]** ページで、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]** を選択し、 **[次へ]** をクリックします。

3.  **[SQL Server の構成を変更する]** オプションを選んでから、 **[次へ]** をクリックします。

4.  サイト データベースを次のように再構成します。
    -   **SQL Server 名:** 可用性グループの作成時に構成した可用性グループ **リスナー**の仮想名を入力します。 仮想名は、**&lt;*エンドポイント サーバー*>.fabrikam.com** のように完全な DNS 名にする必要があります。  

    -   **インスタンス:** 可用性グループの*リスナー*の既定インスタンスを指定するには、この値は空白である必要があります。 現在のサイト データベースが名前付きインスタンスで実行される場合、その名前付きインスタンスが表示されます。このインスタンスはクリアする必要があります。

    -   **データベース:** 表示される名前のままにします。 これは、現在のサイト データベースの名前です。

5.  新しいデータベースの場所の情報を入力したら、通常のプロセスと構成でセットアップを完了します。



## <a name="add-or-remove-synchronous-replica-members"></a>同期レプリカ メンバーの追加または削除  
可用性グループでサイト データベースがホストされている場合、次の手順で同期レプリカ メンバーの追加と削除を行います。 サポートされるレプリカの種類と数については、可用性グループ トピックを利用するための準備の「[必要条件](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites)」で「**可用性グループの構成**」を参照してください。

以下の手順を完了するには、次のアカウントを使用する必要があります。
-   可用性グループのメンバーである各コンピューターの**ローカル管理者**グループのメンバー。
-   サイト データベースをホストしている、またはホストする予定の各 SQL Server の **sysadmin**。


### <a name="to-add-a-new-synchronous-replica-member"></a>新しい同期レプリカ メンバーを追加するには  
Configuration Manager で使用する可用性グループにセカンダリ レプリカを追加するプロセスは、複雑かつ動的で、必要とする手段や手順は、個々の環境に応じて異なります。 Microsoft では、このプロセスの簡略化に向けて、Configuration Manager の機能強化に取り組んでいます。 当面は、セカンダリ レプリカを追加する必要がある場合は、TechNet の以下のブログでガイダンスをご覧ください。
-   [ConfigMgr 1702: 既存の SQL AO AG に新しいノード (セカンダリ レプリカ) を追加する](https://blogs.technet.microsoft.com/umairkhan/2017/07/17/configmgr-1702-adding-a-new-node-secondary-replica-to-an-existing-sql-ao-ag/)

### <a name="to-remove-a-replica-member"></a>レプリカ メンバーを削除するには
この手順については、SQL Server のドキュメントの「[Remove a Secondary Replica from an Availability Group](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server)」(可用性グループからのセカンダリ レプリカの削除) の情報を使用します。  


## <a name="configure-an-asynchronous-commit-replica"></a>非同期コミット レプリカを構成する
Configuration Manager バージョン 1706 以降、Configuration Manager で使用する可用性グループに非同期レプリカを追加できます。 その場合、同期レプリカの構成に必要な構成スクリプトを実行する必要はありません。 (これは、その非同期レプリカをサイト データベースとして使用するためのサポートがないためです)。セカンダリ レプリカを可用性グループに追加する方法については、[SQL Server のドキュメント](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot))を参照してください。

## <a name="use-the-asynchronous-replica-to-recover-your-site"></a>非同期レプリカを使用してサイトを回復する
Configuration Manager バージョン 1706 以降、非同期レプリカを使用し、サイト データベースを復元できます。 その場合、有効なプライマリ サイトを停止し、サイト データベースへの追加書き込みを防止する必要があります。 サイトの停止後、[手動で回復したデータベース](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption)の代わりに、非同期レプリカを使用することができます。

サイトを停止するには、[階層のメンテナンス ツール](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)を使用して、サイト サーバーの主要なサービスを停止します。 次のコマンド ラインを使用します: **Preinst.exe/stopsite**   

サイトを停止することは、サイト サーバーでサイト コンポーネント マネージャー サービス (sitecomp) に続いて SMS_Executive サービスを停止することと同じです。

<!-- For inclusion with passive primary site support:
> [!TIP]  
> If you use a primary passive replica (introduced in version [TBD],  you do not need to stop the passive replica. Only the active primary site must be stopped.
-->  

## <a name="stop-using-an-availability-group"></a>可用性グループの使用を停止する
可用性グループでサイト データベースをホストする必要がなくなったときには、次の手順に従います。 この手順には、サイト データベースを単一インスタンスの SQL Server に移動する操作が含まれます。

この手順を完了するには、次のアカウントを使用する必要があります。
-   可用性グループのメンバーである各コンピューターの**ローカル管理者**グループのメンバー。
-   サイト データベースをホストする各 SQL Server インスタンスの **sysadmin**。

> [!IMPORTANT]  
> ハイブリッド構成で Microsoft Intune と Configuration Manager を使用する場合、サイト データベースを可用性グループに移動したり、可用性グループから移動すると、データがクラウドと再同期されます。 これを回避することはできません。

### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>可用性グループから単一インスタンス SQL Server にサイト データベースを戻すには
1.  Configuration Manager サイトを停止するには、コマンド **Preinst.exe /stopsite** を使用します。 詳細については、「[System Center Configuration Manager の階層のメンテナンス ツール (Preinst.exe)](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)」を参照してください。

2.  SQL Server を使用して、プライマリ レプリカからサイト データベースの完全バックアップを作成します。 この手順を完了する方法については、SQL Server のドキュメントの「 [データベースの完全バックアップの作成](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) 」を参照してください。

3.  可用性グループのプライマリ レプリカであるサーバーで、サイト データベースの単一インスタンスをホストする予定の場合は、この手順を省略できます。  

    -   SQL Server を使用して、サイト データベースをホストするサーバーにサイト データベースのバックアップを復元します。 SQL Server ドキュメントの「[SSMS を使用したデータベース バックアップの復元](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)」を参照してください。   <br />  <br />

4.  サイト データベースをホストするサーバー (プライマリ レプリカ、またはサイト データベースを復元したサーバー) で、サイト データベースのバックアップ モデルを**完全**から**単純**に変更します。 SQL Server のドキュメントの「 [データベースの復旧モデルの表示または変更](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) 」を参照してください。  

5.  **&lt;*Configuration Manager サイトのインストール フォルダー*>\BIN\X64\setup.exe** から **Configuration Manager のセットアップ**を実行します。

6.  **[作業の開始]** ページで、 **[サイトのメンテナンスを実施するか、このサイトをリセットする]** を選択し、 **[次へ]** をクリックします。  

7.  **[SQL Server の構成を変更する]** オプションを選んでから、 **[次へ]** をクリックします。  

8.  サイト データベースを次のように再構成します。
    -   **SQL Server 名** : サイト データベースを現在ホストするサーバーの名前を入力します。

    -   **インスタンス:** サイト データベースをホストする名前付きインスタンスを指定するか、データベースが既定のインスタンス上にある場合は空白のままにします。

    -   **データベース:** 表示される名前のままにします。 これは、現在のサイト データベースの名前です。    

9.  新しいデータベースの場所の情報を入力したら、通常のプロセスと構成でセットアップを完了します。 セットアップが完了したら、サイトが再起動して新しいデータベースの場所の使用を開始します。    

10. 可用性グループのメンバーであったサーバーをクリーンアップするには、SQL Server のドキュメントの「 [可用性グループの削除](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server) 」の説明に従います。
