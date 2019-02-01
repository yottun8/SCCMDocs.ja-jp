---
title: 1606 のチェックリスト
titleSuffix: Configuration Manager
description: System Center Configuration Manager をバージョン 1511 または 1602 からバージョン 1606 に更新する前に、実行するアクションについて説明します。
ms.date: 6/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b8584bf77a72a4feb86814014ee0239f62a91f71
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896661"
---
# <a name="checklist-for-installing-update-1606-for-system-center-configuration-manager"></a>System Center Configuration Manager の更新プログラム 1606 をインストールするためのチェックリスト

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager (現在のブランチ) のバージョン 1606 は、バージョン 1511 または 1602 からの更新で使用できる更新プログラムです。

更新プログラムとしてバージョン 1606 をインストールする前に、次の情報と、更新を開始する前に実行するアクションのチェックリストを確認します。

基準バージョンについては、「[System Center Configuration Manager の更新プログラム](../../../core/servers/manage/updates.md)」の「[基準バージョンと更新プログラムのバージョン](../../../core/servers/manage/updates.md#bkmk_Baselines)」を参照してください。

 ## <a name="about-installing-update-1606"></a>更新プログラム 1606 のインストールについて

*更新プログラム*として、1606 を階層の最上位サイトのみにインストールすることができます。 つまり、中央管理サイトがある場合はそこからインストールを開始します。そうでない場合は、スタンドアロン プライマリ サイトからインストールを開始します。  

-   中央管理サイトで更新プログラムのインストールが完了したら、子プライマリ サイトで更新プログラムが自動的にインストールされます。 サービス期間を使用して、サイトが更新プログラムをインストールするタイミングを制御することができます。 バージョン 1606 より前では、サービス期間はメンテナンス期間と呼ばれました。 詳細については、「[サイト サーバーのサービス ウィンドウ](/sccm/core/servers/manage/service-windows)」を参照してください。  

-   プライマリ親サイトが更新プログラムのインストールを完了したら、Configuration Manager コンソール内からセカンダリ サイトを手動で更新する必要があります。 セカンダリ サイト サーバーの自動更新はサポートされていません。  

サイト サーバーが更新プログラムをインストールすると、サイト サーバーにインストールされたサイト システムの役割と、リモート コンピューターにインストールされたサイト システムの役割が自動的に更新されます。 したがって、更新プログラムをインストールする前に、各サイト システム サーバーが新しい更新プログラムのバージョンの操作の新しい前提条件をすべて満たしていることを確認してください。  

更新プログラムのインストール後に Configuration Manager コンソールを初めて使用する場合、そのコンソールの更新を求められます。  これを行うには、コンソールをホストするコンピューターで Configuration Manager セットアップを実行し、コンソールを更新するオプションを選択する必要があります。 コンソールへの更新プログラムのインストールを遅らせないことをお勧めします。

 **この更新プログラムの既知の問題**   
  更新プログラム パッケージのインストール ステータスを表示したときに、次の問題が発生します。
  - バージョン 1602 から 1606 に更新する場合、ダウンロードが完了していても、**[更新プログラム パッケージのペイロードの抽出]** ステップで **[未開始]** というステータスが表示されます。
  - バージョン 1511 から 1606 に更新する際には、いくつかのステップで **[完了]** というステータスが表示されますが、**[最終更新時刻]** の値は表示されません。


## <a name="checklist"></a>チェックリスト  

 **すべてのサイトで、サポートされているバージョンの System Center Configuration Manager が実行されていることを確認する:** 更新プログラム 1606 のインストールを始めるには、階層内の各サイト サーバーが、同じバージョンの System Center Configuration Manager (バージョン 1511 または 1602 のいずれか) を実行している必要があります。

 **サイト システム サーバーにインストールされた Microsoft .NET のバージョンを確認する:** サイトで更新プログラム 1606 がインストールされると、Configuration Manager によって、次のいずれかのサイト システムの役割をホストする各コンピューターに .NET Framework 4.5.2 が自動的にインストールされます (.NET Framework 4.5 以降がまだインストールされていない場合)。  

-   登録プロキシ ポイント  

-   登録ポイント  

-   管理ポイント  

-   サービス接続ポイント  

このインストールにより、サイト システム サーバーが再起動保留中の状態になり、Configuration Manager コンポーネント ステータス ビューアーにエラーが報告される場合があります。 さらに、サーバーが再起動されるまで、サーバー上の .NET アプリケーションでランダムにエラーが発生する場合があります。  

 詳細については、「[サイトとサイト システムの前提条件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)」を参照してください。  

 **サイトと階層の状態を確認して、未解決の問題がないことを確認する:** サイトを更新する前に、サイト サーバー、サイト データベース サーバー、およびリモート コンピューターにインストールされているサイト システムの役割で、運用上のすべての問題を解決します。 運用上の問題があると、サイトの更新が失敗する可能性があります。

 詳細については、「 [System Center Configuration Manager のアラートとステータス システムの使用](../../../core/servers/manage/use-alerts-and-the-status-system.md)」を参照してください。  

 **サイト間でファイルとデータのレプリケーションを確認する:** サイト間のファイルとデータベースのレプリケーションが機能していて最新の状態であることを確認します。 遅延またはバックログにより、円滑で正常な更新が行われない場合があります。    

データベース レプリケーションには、更新プログラムを開始する前に問題を解決するために、レプリケーション リンク アナライザーを使用できます。 詳細については、「[System Center Configuration Manager での階層とレプリケーション インフラストラクチャの監視](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md)」トピックの「[レプリケーション リンク アナライザーについて](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA)」を参照してください。  

 **サイト、サイト データベース サーバー、リモートのサイト システムの役割をホストするコンピューターのオペレーティング システムに適用できる、重要な更新プログラムすべてをインストールする:** Configuration Manager 用の更新プログラムをインストールする前に、該当する各サイト システムに重要な更新プログラムをインストールします。 更新のインストール時に再起動が必要な場合は、アップグレードを開始する前に該当するコンピューターを再起動します。  

 **プライマリ サイトの管理ポイントのデータベース レプリカを無効にする:** Configuration Manager では、管理ポイントのデータベース レプリカが有効になっているプライマリ サイトを正常に更新することはできません。 データベースのレプリケーションを無効にしてから、Configuration Manager の更新プログラムをインストールしてください。  

詳細については、「[System Center Configuration Manager の管理ポイントのデータベース レプリカ](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)」を参照してください。  

 **SQL Server AlwaysOn 可用性グループを手動フェールオーバーに設定する:**  
 バージョン 1606 などの更新プログラムをインストールする前に、可用性グループで手動フェールオーバーを必ず設定してください。 サイト更新後に、自動フェールオーバーに復元できます。 詳細については、[サイト データベースの SQL Server AlwaysOn](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) に関するページを参照してください。

 **NLB を使用するソフトウェアの更新ポイントを再構成する:** Configuration Manager では、ネットワーク負荷分散 (NLB) クラスターを使用してソフトウェアの更新ポイントをホストしているサイトは、更新できません。  

ソフトウェアの更新ポイントに NLB クラスターを使用している場合、Windows PowerShell を使用して NLB クラスターを削除してください。    

 詳細については、「[System Center Configuration Manager でのソフトウェア更新プログラムの計画](../../../sum/plan-design/plan-for-software-updates.md)」をご覧ください。  

 **サイトの更新インストール時に各サイトですべてのサイト メンテナンス タスクを無効にする:** 更新プログラムをインストールする前に、更新プロセスがアクティブになっている間に実行される可能性があるサイトのメンテナンス タスクをすべて無効にします。 次のタスクが含まれますが、これらのタスクに限定されません。  

-   サイト サーバーのバックアップ  

-   期限切れのクライアント操作を削除  

-   期限切れの探索データの削除  

更新プログラムのインストール中にサイト データベースのメンテナンス タスクを実行すると、更新プログラムのインストールが失敗することができます。 タスクを無効にする前に、更新プログラムをインストールした後で構成を復元できるように、タスクのスケジュールを記録してください。  

詳細については、「[System Center Configuration Manager のメンテナンス タスク](../../../core/servers/manage/maintenance-tasks.md)」および「[System Center Configuration Manager のメンテナンス タスクのリファレンス](../../../core/servers/manage/reference-for-maintenance-tasks.md)」を参照してください。 

**Configuration Manager サーバー上でウイルス対策ソフトウェアを一時的に停止する:** サイトを更新する前に、Configuration Manager サーバー上でウイルス対策ソフトウェアを確実に停止します。 <!--SMS.503481--> 

 **中央管理サイトとプライマリ サイトのサイト データベースのバックアップを作成する:** サイトを更新する前に、サイト データベースをバックアップして、ディザスター リカバリーに使用する正常なバックアップを確実に作成できるようにします。   

詳細については、「[Backup and recovery for System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md)」 (System Center Configuration Manager のバックアップと回復) をご覧ください。  

<!-- Removed from update guidance 6/6/2017
 **Test the database upgrade on a copy of the most recent site database backup:** Before you update a System Center Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

-   You should test the site database upgrade process because when you upgrade a site, the site database might be modified.  

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.  

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.  

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.  

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.  

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.   

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, For more information, see [Step 2: Test the database upgrade before installing an update](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) from **Before you install an in-console update**.
-->

 **クライアントのパイロット運用を計画する:** クライアントを更新する更新プログラムをインストールすると、すべてのアクティブなクライアントを展開してアップグレードする前に、実稼働前環境でその新しいクライアントの更新プログラムをテストできます。   

 このオプションを活用するには、更新プログラムのインストールを開始する前に、実稼働前環境の自動アップグレードをサポートするサイトを構成する必要があります。 詳細については、次を参照してください。「[System Center Configuration Manager でのクライアントのアップグレード](../../../core/clients/manage/upgrade/upgrade-clients.md)」および   
「[System Center Configuration Manager で実稼働前コレクションのクライアント アップグレードをテストする方法](../../../core/clients/manage/upgrade/test-client-upgrades.md)」。  

 **サービス期間を使用する計画を立て、サイト サーバーで更新プログラムをインストールするタイミングを制御する:** サイト サーバーに対する更新プログラムをインストールできる期間は、サービス期間を使用して定義することができます。

これは、階層内のサイトが更新プログラムをインストールするタイミングの制御に役立ちます。
バージョン 1606 より前では、サービス期間はメンテナンス期間と呼ばれました。 詳細については、「[サイト サーバーのサービス ウィンドウ](/sccm/core/servers/manage/service-windows)」を参照してください。  

 **セットアップ前提条件チェッカーを実行する**: 更新プログラム 1606 をインストールする前に、更新プログラムのインストールとは別に前提条件チェッカーを実行することができます。 サイトへの更新プログラムのインストール時に、前提条件チェッカーが再度実行されます。  

詳細については、「**手順 3:更新プログラムをインストールする前の前提条件チェッカーの実行**」 (「[System Center Configuration Manager の更新プログラム](../../../core/servers/manage/install-in-console-updates.md)」トピック内) を参照してください。  

> [!IMPORTANT]  
>  前提条件チェッカーを更新プログラムの一部として、または単独で実行すると、サイト メンテナンス タスクに使用される一部の製品ソース ファイルが更新されます。 このため、前提条件チェッカーを実行した後で、1606 更新プログラムをインストールする前に、サイト メンテナンス タスクを実行する必要がある場合は、サイト サーバーの CD.Latest フォルダーから **Setupwpf.exe** (Configuration Manager セットアップ) を実行する必要があります。  

 **サイトを更新する:** 階層の更新プログラムのインストールを開始する準備が整いました。  
  更新プログラムをインストールするプロセス、およびサイトのコンポーネントとサイト システムの役割を再インストールするアクションが業務に及ぼす影響が少ない場合は、各サイトの通常業務時間外に更新プログラムをインストールする計画を立てることをお勧めします。

詳細については、「[System Center Configuration Manager の更新プログラム](../../../core/servers/manage/updates.md)」を参照してください。  
