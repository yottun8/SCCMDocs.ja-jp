---
title: 1810 のチェックリスト
titleSuffix: Configuration Manager
description: Configuration Manager バージョン 1810 に更新する前に、実行するアクションについて説明します。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b87ac054-9b37-4725-a3f3-2340cfb10bff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ea093b71d19c2cee35caa748ae60f76a95b078c
ms.sourcegitcommit: 54e5786875c4e5f5c1b54e38ed59e96344faf9b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53817768"
---
# <a name="checklist-for-installing-update-1810-for-configuration-manager"></a>Configuration Manager の更新プログラム 1810 をインストールするためのチェックリスト

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager の Current Branch を使用している場合、バージョン 1810 のコンソール内の更新プログラムをインストールし、階層を前のバージョンから更新できます。 <!-- baseline only statement: (Because version 1802 is also available as [baseline media](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions), you can use the installation media to install the first site of a new hierarchy.)-->

バージョン 1810 の更新プログラムを取得するには、階層の最上位サイトでサービス接続ポイントを利用する必要があります。 このサイト システムの役割はオンライン モードまたはオフライン モードで使用可能です。 階層により Microsoft から更新プログラム パッケージがダウンロードされたら、それをコンソールで検索します。 **[管理]** ワークスペースで **[更新とサービス]** ノードを選択します。

-   更新プログラムが**利用可能**として掲載されているとき、インストールできます。 バージョン 1810 のインストール前に、[更新プログラム 1810 のインストールに関する](#about-installing-update-1810)次の情報と、更新プログラムを開始する前に行う構成の[チェックリスト](#checklist)を確認します。

-   更新プログラムに**ダウンロード中**と表示され、変化がない場合、**hman.log** と **dmpdownloader.log** でエラーを確認してください。

    -   dmpdownloader.log に、更新プログラムを確認するまでに dmpdownloader プロセスに待機時間があることを示されている場合があります。 更新プログラムの再配布ファイルのダウンロードを再開するには、サイト サーバーで **SMS_Executive** サービスを再起動します。

    -   別の一般的なダウンロード問題は、 http://silverlight.dlservice.microsoft.com と http://download.microsoft.com からのダウンロードがプロキシ サーバーの設定で禁止されているときに発生するものです。

更新プログラムのインストールの詳細については、「[コンソール内の更新プログラムとサービス](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing)」を参照してください。

現在のブランチのバージョンの詳細については、「[基準バージョンと更新プログラムのバージョン](/sccm/core/servers/manage/updates#bkmk_Baselines)」を参照してください。



## <a name="about-installing-update-1810"></a>更新プログラム 1810 のインストールについて

#### <a name="sites"></a>サイト
更新プログラム 1810 は、階層の最上位サイトにインストールします。 インストールは、中央管理サイトまたはスタンドアロン プライマリ サイトから開始します。 更新プログラムを最上位サイトにインストールすると、子サイトで次の更新動作が行われます。

-   中央管理サイトが更新プログラムのインストールを完了した後、子プライマリ サイトは更新プログラムを自動的にインストールします。 サービス期間を使って、サイトが更新プログラムをインストールするタイミングを制御できます。 詳細については、「[サイト サーバーのサービス ウィンドウ](/sccm/core/servers/manage/service-windows)」を参照してください。

-   プライマリ親サイトが更新プログラムのインストールを完了した後、Configuration Manager コンソール内から各セカンダリ サイトを手動で更新します。 セカンダリ サイト サーバーの自動更新はサポートされていません。

#### <a name="site-system-roles"></a>サイト システムの役割
サイト サーバーによって更新プログラムがインストールされると、サイト システムの役割がすべて自動的に更新されます。 これらの役割は、サイト サーバー上にあるか、リモート サーバーにインストールされています。 更新プログラムをインストールする前に、各サイト システム サーバーが新しい更新プログラムのバージョンの現在の前提条件を満たしていることを確認してください。

#### <a name="configuration-manager-consoles"></a>Configuration Manager コンソール   
更新の完了後に Configuration Manager コンソールを初めて使用する場合、そのコンソールの更新を求められます。 コンソールをホストするコンピューターで Configuration Manager セットアップを実行し、コンソールを更新するオプションを選択することもできます。 できるだけ早くコンソールに更新プログラムをインストールします。 詳細については、「[System Center Configuration Manager コンソールをインストールする](/sccm/core/servers/deploy/install/install-consoles)」を参照してください。

> [!IMPORTANT]  
> 中央管理サイトで更新プログラムをインストールするときは、次の制限事項と、すべての子プライマリ サイトでも更新プログラムのインストールが完了するまで存在する遅延に注意してください。    
> - **クライアントのアップグレード**は開始しません。 これには、クライアントと実稼働前クライアントの自動更新が含まれます。 さらに、最後のサイトで更新プログラムのインストールが完了するまで、実稼働前クライアントを実稼働環境に昇格させることはできません。 最後のサイトで更新プログラムのインストールが完了すると、選択した構成に基づいてクライアントのアップグレードが開始されます。   
> - 更新プログラムで有効になる**新機能**は使うことができません。 これは、その機能のサポートがまだインストールされていないサイトに、その機能に関連するデータのレプリケーションが送信されるのを防ぐためです。 すべてのプライマリ サイトに更新プログラムがインストールされた後、機能は使用できるようになります。   
> - 中央管理サイトと子プライマリ サイトの間の**レプリケーション リンク**は、アップグレードされていないものとして表示されます。 これは、更新プログラム パックのインストール状態では、監視レプリケーション初期化に関する警告のある完了済みの状態として表示されます。 コンソールの監視ノードでは、これは "*リンク構成中*" として表示されます。


## <a name="checklist"></a>チェックリスト

#### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>すべてのサイトで、Configuration Manager のサポート対象のバージョンが実行されている  
更新プログラム 1810 のインストールを始めるには、階層内の各サイト サーバーが、同じバージョンの Configuration Manager を実行している必要があります。 1810 に更新するには、バージョン 1710、1802、または 1806 を使用している必要があります。

#### <a name="review-the-status-of-your-product-licensing"></a>製品のライセンスの状態を確認する 
この更新プログラムをインストールするには、アクティブなソフトウェア アシュアランス (SA) 契約または同等のサブスクリプション権限が必要です。 サイトを更新すると、**ソフトウェア アシュアランスの有効期限**を確認するためのオプションが **[ライセンス]** ページに表示されます。

この値は省略可能です。 ライセンスの有効期限として便利なリマインダーを指定できます。 この日付は、今後の更新プログラムをインストールするときに表示されます。 この値は、セットアップ時または更新プログラムのインストール時に既に指定している場合があります。 この値は Configuration Manager コンソールに指定することも可能です。 **[管理]** ワークスペースで **[サイトの構成]** を展開して、**[サイト]** を選択します。 リボンの **[階層設定]** をクリックして、**[ライセンス]** タブに切り替えます。

詳細については、[ライセンスとブランチの詳細](/sccm/core/understand/learn-more-editions)に関するページを参照してください。

#### <a name="review-microsoft-net-versions"></a>Microsoft .NET のバージョンを確認する 
サイトによりこの更新プログラムがインストールされると、Configuration Manager により自動的に .NET Framework 4.5.2 がインストールされます。 この前提条件がまだインストールされていない場合、次のサイト システムの役割のいずれかがホストされる各サーバーにサイトによってインストールされます。

-   管理ポイント
-   [サービス接続ポイント]
-   登録プロキシ ポイント
-   登録ポイント

このインストールにより、サイト システム サーバーが再起動保留中の状態になり、Configuration Manager コンポーネント ステータス ビューアーにエラーが報告される場合があります。 さらに、サーバーが再起動されるまで、サーバー上の .NET アプリケーションでランダムにエラーが発生する場合があります。

詳細については、「 [サイトとサイト システムの前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)」をご覧ください。

#### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Windows 10 用の Windows ADK のバージョンを確認する
Windows 10 アセスメント & デプロイメント キット (ADK) のバージョンは、Configuration Manager バージョン 1810 でサポートされている必要があります。 サポートされている Windows ADK バージョンの詳細については、「[Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)」を参照してください。 Windows ADK を更新する必要がある場合は、Configuration Manager の更新を開始する前に行います。 この順番により、既定のブート イメージが Windows PE の最新バージョンに自動的に更新されることが保証されます。 サイトの更新後、カスタム ブート イメージを手動で更新します。

Windows ADK を更新する前にサイトを更新する場合は、「[ブート イメージを使用して配布ポイントを更新する](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image)」を参照してください。

#### <a name="review-sql-server-native-client-version"></a>SQL Server Native Client バージョンを確認する
TLS 1.2 をサポートしている最小バージョンの SQL Server 2012 Native Client をインストールする必要があります。 詳細については、[前提条件の確認の一覧](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-native-client)を参照してください。

#### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>サイトと階層の状態で未解決の問題を確認する 
運用上の問題があると、サイトの更新が失敗する可能性があります。 サイトを更新する前に、次のシステムに対する運用上のすべての問題を解決します。  
- サイト サーバー  
- サイト データベース サーバー  
- 他のサーバー上のリモート サイト システムの役割   

詳細については、「 [アラートとステータス システムの使用](/sccm/core/servers/manage/use-alerts-and-the-status-system)」を参照してください。

#### <a name="review-file-and-data-replication-between-sites"></a>サイト間でファイルとデータのレプリケーションを確認する   
サイト間のファイルとデータベースのレプリケーションが機能していて最新の状態であることを確認します。 遅延またはバックログにより、円滑で正常な更新が行われない場合があります。 データベース レプリケーションには、更新プログラムを開始する前に問題を解決するために、レプリケーション リンク アナライザーを使用できます。

詳細については、「[レプリケーション リンク アナライザーについて](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA)」を参照してください。

#### <a name="install-all-applicable-critical-windows-updates"></a>該当するすべての重要な Windows 更新プログラムをインストールする
Configuration Manager をインストールおよび更新する前に、該当する各サイト システムに OS の重要な更新プログラムをインストールします。 これらのサーバーには、サイト サーバー、サイト データベース サーバー、およびリモート サイト システムの役割が含まれます。 更新のインストール時に再起動が必要な場合は、アップグレードを開始する前に該当するサーバーを再起動します。

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>プライマリ サイトの管理ポイントのデータベース レプリカを無効にする   
Configuration Manager では、管理ポイントのデータベース レプリカが有効になっているプライマリ サイトを正常に更新することはできません。 データベースのレプリケーションを無効にしてから、Configuration Manager の更新プログラムをインストールしてください。

詳細については、「[管理ポイントのデータベース レプリカ](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)」を参照してください。

#### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>SQL Server AlwaysOn 可用性グループを手動フェールオーバーに設定する   
可用性グループを使っている場合は、更新プログラムのインストールを始める前に、可用性グループが手動フェールオーバーに設定されていることを確認します。 サイトが更新された後で、自動フェールオーバーに戻すことができます。 詳細については、 [サイト データベースの SQL Server AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database) に関するページを参照してください。

#### <a name="disable-site-maintenance-tasks-at-each-site"></a>各サイトでサイト メンテナンス タスクを無効にする
更新プログラムをインストールする前に、更新プロセスがアクティブになっている間にそのサイトで実行される可能性があるサイトのメンテナンス タスクをすべて無効にします。 たとえば以下ですが、これに限定されるものではありません。

-   サイト サーバーのバックアップ
-   期限切れのクライアント操作を削除
-   期限切れの探索データの削除

更新プログラムのインストール中にサイト データベースのメンテナンス タスクを実行すると、更新プログラムのインストールが失敗することができます。 タスクを無効にする前に、更新プログラムをインストールした後で構成を復元できるように、タスクのスケジュールを記録してください。

詳細については、「 [メンテナンス タスク](/sccm/core/servers/manage/maintenance-tasks)」と「[メンテナンス タスクのリファレンス](/sccm/core/servers/manage/reference-for-maintenance-tasks)」を参照してください。

#### <a name="temporarily-stop-any-antivirus-software"></a>すべてのウイルス対策ソフトウェアを一時的に停止する 
サイトを更新する前に、Configuration Manager サーバーでウイルス対策ソフトウェアを停止します。 <!--SMS.503481--> 

#### <a name="create-a-backup-of-the-site-database"></a>サイト データベースのバックアップを作成する 
サイトを更新する前に、中央管理サイトとプライマリ サイトのサイト データベースをバックアップします。 このバックアップにより、ディザスター リカバリーに使用できる正常なバックアップがあることになります。

詳細については、「 [バックアップと回復](/sccm/protect/understand/backup-and-recovery)」を参照してください。

#### <a name="plan-for-client-piloting"></a>クライアントのパイロット運用を計画する   
クライアントを更新する更新プログラムをインストールすると、すべてのアクティブなクライアントを展開してアップグレードする前に、実稼働前環境でその新しいクライアントの更新プログラムをテストできます。 このオプションを活用するには、更新プログラムのインストールを開始する前に、実稼働前環境の自動アップグレードをサポートするサイトを構成する必要があります。

詳細については、「 [クライアントをアップグレードする](/sccm/core/clients/manage/upgrade/upgrade-clients)」および「[System Center Configuration Manager で実稼働前コレクションのクライアント アップグレードをテストする方法](/sccm/core/clients/manage/upgrade/test-client-upgrades)」を参照してください。

#### <a name="plan-to-use-service-windows"></a>サービス期間の使用を計画   
サイト サーバーにインストールできる更新プログラムの期間を定義するには、サービス期間を使います。 これは、階層内のサイトが更新プログラムをインストールするタイミングの制御に役立ちます。 詳細については、「 [サイト サーバーのサービス ウィンドウ](/sccm/core/servers/manage/service-windows)」を参照してください。

#### <a name="review-supported-extensions"></a>サポートされる拡張機能を確認する
<!--SCCMdocs#587--> Microsoft または Microsoft パートナーの他の製品で Configuration Manager を拡張する場合は、その製品でバージョン 1810 がサポートされていることを確認します。 この情報については、製品のベンダーに確認してください。 たとえば、Microsoft Deployment Toolkit [リリース ノート](/sccm/mdt/release-notes)を参照します。

#### <a name="run-the-setup-prerequisite-checker"></a>セットアップ前提条件チェッカーを実行する   
更新プログラムが**利用可能**としてコンソールに表示されているとき、更新プログラムのインストール前に、前提条件チェッカーを別個に実行できます。 (サイトへの更新プログラムのインストール時に、前提条件チェッカーが再度実行されます。)

コンソールから前提条件チェックを実行するには、**[管理]** ワークスペースに移動して、**[更新とサービス]** を選択します。 **Configuration Manager 1810** 更新プログラム パッケージを選択し、リボンの **[前提条件チェックを実行]** をクリックします。

詳細については、「[コンソール内の更新プログラムをインストールする前に](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)」の「**更新プログラムをインストールする前の前提条件チェッカーの実行**」を参照してください。

> [!IMPORTANT]  
> 前提条件チェッカーを実行すると、この手順によりサイト メンテナンス タスクに使用される一部の製品ソース ファイルが更新されます。 このため、前提条件チェッカーを実行した後で、更新プログラムをインストールする前に、サイト メンテナンス タスクを実行する必要がある場合は、サイト サーバーの CD.Latest フォルダーから **Setupwpf.exe** (Configuration Manager セットアップ) を実行する必要があります。

#### <a name="update-sites"></a>サイトを更新する   
階層の更新プログラムのインストールを開始する準備が整いました。 更新プログラムのインストールに関する情報については、「[コンソール内の更新プログラムのインストール](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)」を参照してください。

通常の業務時間外に更新プログラムのインストールを計画したい場合があります。 この手順の影響が最も少ない時間を決定します。 更新プログラムとそのアクションをインストールすると、サイト コンポーネントとサイト システムの役割が再インストールされます。

詳細については、 [Configuration Manager の更新プログラム](/sccm/core/servers/manage/updates)に関するページをご覧ください。



## <a name="post-update-checklist"></a>更新後のチェックリスト

サイトの更新後に、次のチェックリストを使用して一般的なタスクと構成を完了します。


#### <a name="confirm-version-and-restart-if-necessary"></a>バージョンを確認して再起動する (必要な場合)
各サイト サーバーおよびサイト システムの役割がバージョン 1810 に更新されていることを確認します。 コンソールで、**[バージョン]** 列を **[管理]** ワークスペースの **[サイト]** と **[配布ポイント]** ノードに追加します。 必要な場合は、サイト システムの役割が自動的に再インストールされて、新しいバージョンに更新されます。 

最初に正常に更新されないリモート サイト システムは再起動してみます。 サイト インフラストラクチャを確認し、該当するサイト サーバーとリモート サイト システム サーバーが正常に再起動されたことを確認します。 通常は、サイト システムの役割の前提条件として Configuration Manager が .NET をインストールするときにのみ、サイト サーバーが再起動されます。


#### <a name="confirm-site-to-site-replication-is-active"></a>サイト間レプリケーションがアクティブであることを確認する
Configuration Manager コンソールで次の場所に移動し、状態を表示して、レプリケーションがアクティブであることを確認します。  

-   **[監視]** ワークスペース、**[サイト階層]** ノード  

-   **[監視]** ワークスペース、**[データベースのレプリケーション]** ノード  

詳細については、以下の記事を参照してください。  
- [階層とレプリケーション インフラストラクチャの監視](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure)
- [ レプリケーション リンク アナライザーについて](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA)  


#### <a name="update-configuration-manager-consoles"></a>Configuration Manager コンソールの更新
すべてのリモートの Configuration Manager コンソールを同じバージョンに更新します。 次の場合には、コンソールを更新するようにダイアログが表示されます。  

-   コンソールを開くとき  

-   コンソールの新しいノードに移動するとき  


#### <a name="reconfigure-database-replicas-for-management-points"></a>管理ポイントのデータベース レプリカを構成する
プライマリ サイトを更新した後、サイトを更新する前にアンインストールした管理ポイント用データベース レプリカを再構成します。 詳細については、「[管理ポイントのデータベース レプリカ](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)」を参照してください。  


#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>無効にしたメンテナンス タスクを再構成する
更新プログラムのインストール前にサイトでデータベースの [メンテナンス タスク](/sccm/core/servers/manage/maintenance-tasks)を無効にした場合は、これらのタスクを再構成します。 更新前に適用されていたのと同じ設定を使用します。  


#### <a name="update-clients"></a>クライアントの更新
作成した計画に従ってクライアントをアップグレードします (特に、更新プログラムをインストールする前にクライアントのパイロット運用を構成した場合)。 詳細については、「[Windows コンピューター用クライアントをアップグレードする方法](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers)」を参照してください。  


#### <a name="third-party-extensions"></a>サード パーティの拡張機能
Configuration Manager のすべての拡張機能を使用する場合は、Configuration Manager バージョン 1810 をサポートするために最新バージョンに更新します。 


#### <a name="update-custom-boot-images-and-media"></a>カスタム ブート イメージとメディアを更新する
<!--SCCMDocs issue 775-->

既定またはカスタムどちらのブート イメージでも、使用するブート イメージの **[配布ポイントの更新]** アクションを使用します。 このアクションでは、クライアントが最新バージョンを使用できることが確認されます。 Windows ADK の新しいバージョンがない場合でも、Configuration Manager クライアント コンポーネントを更新プログラムで変更できます。 ブート イメージとメディアを更新しない場合、デバイスでタスク シーケンスの展開が失敗する可能性があります。 

サイトを更新すると、Configuration Manager によって "*既定の*" ブート イメージが自動的に更新されます。 更新されたコンテンツの配布ポイントへの配布は自動的には行われません。 このコンテンツをネットワーク全体に配布する準備ができたら、特定のブート イメージで**配布ポイントの更新**アクションを使用します。 

サイトの更新後、すべての "*カスタム*" ブート イメージを手動で更新します。 このアクションでは、必要な場合は最新のクライアント コンポーネントでブート イメージが更新され、必要に応じて現在の Windows PE のバージョンが再読み込みされて、配布ポイントにコンテンツが再配布されます。 

詳細については、「[Update distribution points with the boot image](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image)」(ブートイメージによる配布ポイントの更新) を参照してください。 
