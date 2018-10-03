---
title: サイト復元
titleSuffix: Configuration Manager
description: Configuration Manager でのサイトの回復について説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4737acb34de3aebc8560f54d77b6b341c82ebf65
ms.sourcegitcommit: 6e0e5b4b7779ce03e2b56b3b5f68f4ace1acedd8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2018
ms.locfileid: "39467659"
---
#  <a name="recover-a-configuration-manager-site"></a>Configuration Manager サイトの回復

*適用対象: System Center Configuration Manager (Current Branch)*

サイトで障害が発生した場合や、サイト データベースのデータが失われた場合は、Configuration Manager サイトの回復を実行します。 サイトの回復の中心となる作業は、データの修復と同期です。これは、業務の中断を防ぐためにも必要な作業です。

この記事のセクションは、Configuration Manager サイトを回復する場合に役立ちます。 バックアップを作成する場合は、[Configuration Manager のバックアップ](/sccm/core/servers/manage/backup-and-recovery)に関するページを参照してください。



## <a name="considerations-before-recovering-a-site"></a>サイトを回復する前の注意事項

> [!Important]  
> この情報は、サイトの回復シナリオにのみ適用されます。 オンプレミスのインフラストラクチャをアップグレードしていて、障害が発生したサイトを積極的に回復しない場合は、次の記事の情報を確認してください。
> - [オンプレミス インフラストラクチャのアップグレード](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)
> - [インフラストラクチャの変更](/sccm/core/servers/manage/modify-your-infrastructure)


#### <a name="use-the-same-version-and-edition-of-sql-server"></a>同じバージョンおよびエディションの SQL Server を使用する   
たとえば、SQL Server 2014 から SQL Server 2016 へのデータベースの復元はサポートされていません。 同様に、SQL Server 2016 の Standard Edition から Enterprise Edition にサイト データベースを復元することはできません。
- SQL Server を**シングル ユーザー モード**に設定することはできません。
- MDF ファイルと LDF ファイルが有効であることを確認します。 サイトを回復するときに、ファイルの状態は確認されません。  

#### <a name="sql-server-always-on-availability-groups"></a>SQL Server の Always On 可用性グループ   
SQL Server Always On 可用性グループを使ってサイト データベースをホストする場合は、[SQL Server Always On を使用するための準備](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery)に関するページの説明に従って、回復計画を変更します。

#### <a name="database-replicas"></a>データベース レプリカ  
データベース レプリカ用に構成したサイト データベースを復元した後は、各レプリカを再構成します。 データベース レプリカを使う前に、パブリケーションとサブスクリプションを再作成します。



## <a name="determine-your-recovery-options"></a>回復オプションの検討

Configuration Manager のプライマリ サイト サーバーと中央管理サイトの回復について主に検討する必要がある 2 つの部分は、**サイト サーバー**と**サイト データベース**です。
次のセクションは、回復シナリオに最適なオプションを選択するのに役立ちます。

> [!NOTE]   
> Configuration Manager のセットアップによってサーバーで既存のサイトが検出された場合、サイトの回復を開始できますが、サイト サーバーの回復オプションは限られます。 たとえば、既存のサイト サーバーでセットアップを実行した場合は、サイト データベース サーバーは回復できますが、サイト サーバーの回復オプションは無効になっています。


### <a name="site-server-recovery-options"></a>サイト サーバーの回復オプション

Configuration Manager インストール フォルダーの外に作成した **CD.Latest** フォルダーのコピーから、Configuration Manager のセットアップを開始します。  

-   サイト サーバーの **[スタート]** メニューからセットアップを実行する場合、**[Recover a site]\(サイトを回復する\)** オプションは使用できません。  

-   バックアップを作成する前に Configuration Manager コンソール内から更新プログラムをインストールした場合は、セットアップを使って以下の場所からサイトを再インストールすることはできません。 
    - インストール メディア
    - Configuration Manager のインストール パス 

その後、**[サイトを回復する]** オプションを選択します。 障害が発生したサイト サーバーに対して選択できる回復オプションは次のとおりです。  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>既存のバックアップを使用してサイト サーバーを回復する
サイトで障害が発生する前のサイト サーバーの Configuration Manager バックアップがある場合は、このオプションを使います。 サイトは、**サイト サーバーのバックアップ** メンテナンス タスクの一部としてこのバックアップを作成します。 サイトが再インストールされ、バックアップされているサイトに基づいて、サイト設定が構成されます。  

#### <a name="reinstall-the-site-server"></a>サイト サーバーを再インストールする
サイト サーバーのバックアップがないときは、このオプションを使います。 サイト サーバーが再インストールされ、初めてインストールするときと同じようにサイト設定を指定する必要があります。  

-   障害が発生したサイトを初めてインストールしたときに使ったものと同じサイト コードとサイト データベース名を使います。  

-   新しい OS のバージョンを実行する新しいコンピューターにサイトを再インストールすることができます。  

-   サーバーは、元のサイト サーバーと同じホスト名および完全修飾ドメイン名 (FQDN) を使う必要があります。   


### <a name="site-database-recovery-options"></a>サイト データベースの回復オプション

Configuration Manager のセットアップを実行するとき、サイト データベースについては次の回復オプションがあります。  

#### <a name="recover-the-site-database-using-a-backup-set"></a>バックアップ セットを使用してサイト データベースを回復する
データベースで障害が発生する前のサイト データベースの Configuration Manager バックアップがある場合は、このオプションを使います。 サイトは、**サイト サーバーのバックアップ** メンテナンス タスクの一部としてこのバックアップを作成します。 階層においてプライマリ サイトを復元する場合、回復プロセスは最後のバックアップ後にサイト データベースに対して行われた変更を中央管理サイトから取得します。 中央管理サイトを復元する場合、回復プロセスは基準プライマリ サイトから変更を取得します。 スタンドアロンのプライマリ サイトのサイト データベースを回復する場合は、最後のバックアップ以後に行われたサイトの変更を回復することはできません。  

階層内のサイトのサイト データベースを回復する場合、回復の動作は、中央管理サイトとプライマリ サイトで異なります。 また、最後のバックアップが SQL Server の変更追跡保持の期間内か期間外かによっても異なります。 詳細については、この記事の「[サイト データベースの回復方法](#site-database-recovery-scenarios)」セクションを参照してください。  

> [!NOTE]   
> サイト データベースが既に存在するのに、バックアップ セットを使ったサイト データベースの回復を選択した場合、回復は失敗します。   

#### <a name="create-a-new-database-for-this-site"></a>このサイトの新しいデータベースを作成する
サイト データベースのバックアップがない場合は、このオプションを使います。 階層では、回復プロセスは新しいサイト データベースを作成します。 子プライマリ サイトを復元する場合は、中央管理サイトからレプリケートすることによってデータを回復します。 中央管理サイトを復元する場合は、基準プライマリ サイトからデータをレプリケートします。 スタンドアロンのプライマリ サイトを回復する場合や、プライマリ サイトのない中央管理サイトを回復する場合は、このオプションを選択することはできません。  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>手動で回復したサイト データベースを使用する
Configuration Manager サイト データベースを既に回復してあるものの、回復プロセスを完了させる必要がある場合は、このオプションを使います。  

- Configuration Manager は、次のどのプロセスからでもサイト データベースを回復できます。  

    - Configuration Manager バックアップ メンテナンス タスク  
    - Data Protection Manager (DPM) を使用するサイト データベースのバックアップ  
    - その他のバックアップ プロセス   

    Configuration Manager 以外の方法を使用してサイト データベースを復元した場合は、セットアップを実行し、このオプションを選択して、サイト データベースの回復を完了します。  

    > [!NOTE]   
    > DPM を使用してサイト データベースをバックアップするときに、Configuration Manager で復元プロセスを続行する前に、DPM の手順を使用して指定の場所にサイト データベースを復元します。 DPM の詳細については、[Data Protection Manager](https://docs.microsoft.com/system-center/dpm) のドキュメント ライブラリを参照してください。    

- 階層においてプライマリ サイト データベースを回復する場合、回復プロセスは最後のバックアップ後にサイト データベースに対して行われた変更を中央管理サイトから取得します。 中央管理サイトを復元する場合、回復プロセスは基準プライマリ サイトから変更を取得します。 スタンドアロンのプライマリ サイトのサイト データベースを回復する場合は、最後のバックアップ以後に行われたサイトの変更を回復することはできません。   

#### <a name="skip-database-recovery"></a>データベースの回復をスキップする
Configuration Manager サイト データベース サーバーのデータが失われていない場合は、このオプションを使います。 このオプションは、回復しようとしているサイト サーバーとは別のコンピューターにサイト データベースがある場合にのみ選択できます。  


### <a name="sql-server-change-tracking-retention-period"></a>SQL Server の変更の追跡の保有期間

Configuration Manager は、SQL Server におけるサイト データベースの変更の追跡を有効にします。 そのため、過去のある時点以後にデータベース テーブルで行われた変更に関する情報を、Configuration Manager が照会することができます。 保有期間とは、この変更の追跡データを残しておく期間のことです。 既定では、サイト データベースの追跡データの保有期間は 5 日に構成されています。 サイト データベースを回復するときは、バックアップがこの保有期間内に作成されたかどうかによって、回復プロセスが異なります。 たとえば、SQL Server で障害が発生した時点で、最も新しいバックアップが作成後 7 日経過している場合は、保有期間外に作成されていることになります。

SQL Server の変更追跡の内部構造については、SQL Server チームのブログ投稿「[Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/)」(変更追跡のクリーンアップ - パート 1) と「[Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2)」(変更追跡のクリーンアップ - パート 2) を参照してください。


### <a name="reinitialization-of-site-or-global-data"></a>サイト データまたはグローバル データの再初期化

サイトのデータまたはグローバル データの再初期化とは、サイト データベースにある既存のデータを別のサイト データベースに置き換えるプロセスのことです。 たとえば、"ABC" というサイトのデータを "XYZ" というサイトのデータで再初期化するときは、次の処理が行われます。
- サイト "XYZ" からサイト "ABC" にデータがコピーされます。
- サイト "ABC" のサイト データベースから、サイト "XYZ" の既存のデータが削除されます。
- サイト "XYZ" からコピーされたデータが、サイト "ABC" のサイト データベースに挿入されます。

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-central-administration-site"></a>シナリオ例 1: プライマリ サイトを中央管理サイトのグローバル データで再初期化する  
回復プロセスで、プライマリ サイト データベースにあるプライマリ サイト用グローバル データが削除され、中央管理サイトからコピーされたグローバル データに置き換えられます。

#### <a name="example-scenario-2-the-central-administration-site-reinitializes-the-site-data-from-a-primary-site"></a>シナリオ例 2: 中央管理サイトをプライマリ サイトのサイト データで再初期化する 
回復プロセスで、中央管理サイト データベースにある、そのプライマリ サイトの既存のサイト データが削除されます。 データは、プライマリ サイトからコピーされたサイト データに置き換えられます。 他のサイトのサイト データは影響を受けません。


### <a name="site-database-recovery-scenarios"></a>サイト データベースの回復方法

サイト データベースがバックアップから復元されると、Configuration Manager は前回のデータベースのバックアップ以後にサイト データとグローバル データに加えられた変更の回復を試みます。 Configuration Manager は、サイト データベースがバックアップから復元された後で、次の処理を開始します。  

#### <a name="recovered-site-is-a-central-administration-site"></a>回復されたサイトが中央管理サイトの場合
- データベースが、変更の追跡の保有期間以内にバックアップされている場合  

     - **グローバル データ**: バックアップ後のグローバル データの変更は、すべてのプライマリ サイトからレプリケートされます。  

     - **サイト データ**: バックアップ後のサイト データの変更は、すべてのプライマリ サイトからレプリケートされます。  

- データベースが、変更の追跡の保有期間より前にバックアップされている場合  

     - **グローバル データ**: 基準プライマリ サイトが指定されていると、中央管理サイトは基準プライマリ サイトからのグローバル データを再初期化します。 他のすべてのプライマリ サイトを、中央管理サイトのグローバル データで再初期化します。 基準サイトが指定されていない場合は、すべてのプライマリ サイトが中央管理サイトのグローバル データで再初期化します。 このデータは、バックアップから復元したものです。  

     - **サイト データ**: 中央管理サイトは、各プライマリ サイトからのサイト データを再初期化します。  

#### <a name="recovered-site-is-a-primary-site"></a>回復されたサイトがプライマリ サイトの場合
- データベースが、変更の追跡の保有期間以内にバックアップされている場合  

     - **グローバル データ**: バックアップ後のグローバル データの変更は、中央管理サイトからレプリケートされます。  

     - **サイト データ**: 中央管理サイトはプライマリ サイトからのサイト データを再初期化します。 バックアップ後の変更は失われます。 クライアントは、プライマリ サイトに情報を送信するときに、ほとんどのデータを再生成します。  

- データベースが、変更の追跡の保有期間より前にバックアップされている場合  
     - **グローバル データ**: プライマリ サイトは中央管理サイトからのグローバル データを再初期化します。  

     - **サイト データ**: 中央管理サイトはプライマリ サイトからのサイト データを再初期化します。 バックアップ後の変更は失われます。 クライアントは、プライマリ サイトに情報を送信するときに、ほとんどのデータを再生成します。  



## <a name="site-recovery-procedures"></a>サイトの回復手順

次のいずれかの手順に従って、サイト サーバーとサイト データベースを回復します。


### <a name="start-a-site-recovery-in-the-setup-wizard"></a>セットアップ ウィザードでサイトの回復を開始する

1.  Configuration Manager インストール フォルダー以外の場所に [CD.Latest フォルダー](/sccm/core/servers/manage/the-cd.latest-folder)をコピーします。 CD.Latest フォルダーのコピーから、Configuration Manager セットアップ ウィザードを実行します。  

2.  **[はじめに]** ページで、**[サイトを回復する]** を選択してから、**[次へ]** をクリックします。  

3.  表示される指示に従って、順次適切なオプションを選択し、ウィザードを完了します。  

     - 回復中に、セットアップによって SQL Server で使われている SQL Server Service Broker (SSB) のポートが検出されます。 回復中に、このポートの設定を変更しないでください。変更すると、回復が完了した後で、データが正しくレプリケートされません。  

     - セットアップ ウィザードで Configuration Manager のインストールに使用する元のパスまたは新しいパスを指定できます。  


### <a name="start-an-unattended-site-recovery"></a>サイトの無人回復を開始する

1. サイトを回復するのに必要な無人インストール スクリプトを準備します。 詳細については、[サイトの無人回復](/sccm/core/servers/manage/unattended-recovery)に関するページを参照してください。  

2. `/script` コマンド ライン オプションを使って、Configuration Manager のセットアップを実行します。 たとえば、セットアップ初期化ファイル **ConfigMgrUnattend.ini** を作成します。 それを、セットアップを実行しているコンピューターの `C:\Temp` ディレクトリに保存します。 次のコマンドを使います。  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  


> [!NOTE]   
>  中央管理サイトを回復した後、子サイトからの一部のサイト データのレプリケーションの確立が失敗する場合があります。 このデータには、ハードウェア インベントリ、ソフトウェア インベントリおよびステータス メッセージが含まれることがあります。
>
>  この問題が発生した場合は、データベース レプリケーションの **ConfigMgrDRSSiteQueue** を再初期化します。 **SQL Server Manager** を使って、中央管理サイトのサイト データベースに対して次のクエリを実行します。
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```



## <a name="post-recovery-tasks"></a>回復後の作業

サイトを回復した後、サイトの回復が完了する前に、考慮する必要のある回復後タスクがいくつかあります。 次のセクションの情報を、サイトの回復プロセスを完了させるときの参考にしてください。


### <a name="reenter-user-account-passwords"></a>ユーザー アカウントのパスワードを再入力する

サイト サーバーの回復後に、サイト内のすべてのユーザー アカウントのパスワードを再入力します。 これらのパスワードは、サイトの回復中にリセットされます。 アカウントは、サイトの回復が完了した後でセットアップ ウィザードの **[完了]** ページに一覧表示されます。 この一覧は、回復されたサイト サーバーの `C:\ConfigMgrPostRecoveryActions.html` にも保存されます。

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>サイトの回復後にユーザー アカウントのパスワードを再入力する
1. Configuration Manager コンソールを開き、回復したサイトに接続します。  

2. **[管理]** ワークスペースに移動し、**[セキュリティ]** を展開して、**[アカウント]** をクリックします。  

3. 各アカウントについて、次の手順でパスワードを再入力します。  

     1. サイト回復後に示される一覧でアカウントを選択します。  

     2. リボンで **[プロパティ]** をクリックします。  

     3. **[全般]** タブの **[設定]** をクリックして、アカウントのパスワードを再入力します。  

     4. **[確認]** をクリックし、選択したユーザー アカウントの適切なデータ ソースを選択して、**[接続のテスト]** をクリックします。 このステップでは、そのユーザー アカウントがデータ ソースに接続できることをテストし、資格情報を確認します。  

     5. **[OK]** をクリックしてパスワードの変更を保存してから、**[OK]** をクリックしてアカウントのプロパティ ページを閉じます。  


### <a name="reenter-sideloading-keys"></a>サイドローディング キーを再入力する

サイト サーバーの回復後に、サイトに指定されている Windows のサイドローディング キーを再入力します。 これらのキーは、サイトの回復中にリセットされます。 サイドローディング キーを再入力すると、Windows サイドローディング キーの **[使用済みライセンス認証数]** 列のカウントがリセットされます。 

たとえば、サイト障害発生前の **[ライセンス認証総数]** の値が **100** であるものとします。 デバイスが使ったキーの数つまり **[使用済みライセンス認証数]** を **90** とします。 サイトの回復後、**[ライセンス認証総数]** にはまだ **100** と表示されていますが、**[使用済みライセンス認証数]** 列には誤って **0** と表示されます。 新しく 10 台のデバイスがサイドローディング キーを使うと、サイドローディング キーの残りがなくなるので、11 台目のデバイスはサイドローディング キーを適用できません。


### <a name="recreate-the-microsoft-intune-subscription"></a>Microsoft Intune サブスクリプションの再作成

サイト サーバーが再イメージ化された後に Configuration Manager サイト サーバーを回復する場合、Microsoft Intune のサブスクリプションは復元されません。 サイトを回復した後、サブスクリプションを再接続する必要があります。 新しい APN 要求を作成しないでください。 代わりに、現在の有効な PEM ファイルをアップロードします。 iOS 管理を最後に構成または更新したときにアップロードしたのと同じファイルを使います。 詳細については、「 [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription)」をご覧ください。


### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>IIS を使用するサイト システムの役割の SSL を構成する

IIS を実行するサイト システムを回復し、HTTPS 用に構成した場合は、Web サーバー証明書を使うように IIS を再構成します。


### <a name="reinstall-hotfixes"></a>修正プログラムを再インストールする 

サイトの回復が終わったら、障害が発生する前にサイト サーバーに適用されていた修正プログラムを再インストールする必要があります。 サイト回復後、セットアップ ウィザードの **[完了]** ページで、以前にインストールした修正プログラムのリストを表示します。 この一覧は、回復されたサイト サーバーの `C:\ConfigMgrPostRecoveryActions.html` にも保存されます。


### <a name="recover-custom-reports"></a>カスタム レポートを回復する 

SQL Server Reporting Services でカスタム レポートを作成するお客様がいます。 このコンポーネントで障害が発生したときは、レポート サーバーのバックアップからレポートを回復します。 Reporting Services のカスタム レポートの復元の詳細については、「[Reporting Services のバックアップおよび復元操作](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services)」を参照してください。


### <a name="recover-content-files"></a>コンテンツ ファイルを回復する

サイト データベースにより、サイト サーバーがコンテンツ ファイルを格納する場所が追跡されます。 コンテンツ ファイル自体は、バックアップおよび回復プロセスの一部としてバックアップまたは復元されません。 コンテンツ ファイルを完全に回復するには、コンテンツ ライブラリのファイルとパッケージ ソース ファイルを元の場所に復元します。 コンテンツ ファイルを回復するには複数の方法があります。 最も簡単な方法は、サイト サーバーのファイル システム バックアップからファイルを復元することです。

パッケージ ソース ファイルのファイル システム バックアップがない場合は、手動でコピーまたはダウンロードします。 このプロセスは、最初にパッケージを作成したときと似ています。 SQL Server で `SELECT * FROM v_Package` というクエリを実行して、すべてのパッケージとアプリケーションのパッケージ ソースの場所を見つけます。 パッケージ ID の先頭の 3 文字を見ると、パッケージ ソースのサイトがわかります。 たとえば、CEN00001 というパッケージ ID では、CEN がソース サイトのサイト コードです。 パッケージのソース ファイルを復元するときは、障害発生前と同じ場所に復元する必要があります。

コンテンツ ライブラリが含まれているファイル システムのバックアップがない場合は、次の方法でコンテンツ ファイルを復元できます。  

- **事前設定済みのコンテンツ ファイルをインポートする**: Configuration Manager 階層では、別の場所にあるすべてのパッケージとアプリケーションで事前設定済みコンテンツ ファイルを作成できます。 その事前設定済みコンテンツ ファイルをインポートして、サイト サーバーのコンテンツ ライブラリを回復します。  

- **コンテンツを更新する**: Configuration Manager によって、パッケージ ソースからコンテンツ ライブラリにコンテンツがコピーされます。 この処理が正常に完了するには、パッケージ ソース ファイルが元の場所になければなりません。 パッケージとアプリケーションごとに、この操作を実行します。


### <a name="recover-custom-software-updates"></a>カスタム ソフトウェア更新プログラムを回復する

System Center Updates Publisher データベース ファイルがバックアップ計画に含まれていた場合は、Updates Publisher コンピューターで障害が発生したときに、そのデータベースを回復できます。 Updates Publisher の詳細については、「[System Center Updates Publisher](/sccm/sum/tools/updates-publisher)」を参照してください。

#### <a name="restore-the-updates-publisher-database"></a>Updates Publisher データベースを復元する
1. 回復したコンピューターに Updates Publisher を再インストールします。  

2. バックアップ先から、Updates Publisher を実行しているコンピューターの `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` に、データベース ファイル **Scupdb.sdf** をコピーします。  

3. コンピューターで複数のユーザーが Updates Publisher を実行する場合は、各データベース ファイルを適切なユーザー プロファイルの場所にコピーします。  


### <a name="user-state-migration-data"></a>ユーザー状態の移行データ

状態移行ポイントのプロパティの一部として、ユーザー状態データを保存するフォルダーを指定します。 状態移行ポイントを回復した後、ユーザー状態データをサーバーに手動で復元します。 障害発生前にデータが格納されていたのと同じフォルダーに復元します。


### <a name="regenerate-the-certificates-for-distribution-points"></a>配布ポイント用の証明書の再生成

サイトの復元後、1 つまたは複数の配布ポイントに対する `Failed to decrypt cert PFX data` というエントリが **distmgr.log** に一覧表示されていることがあります。 このエントリは、配布ポイントの証明書データをサイトで解読できないことを示します。 この問題を解決するには、影響を受ける配布ポイントの証明書を再生成または再インポートします。 それには、[Set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint) PowerShell コマンドレットを使います。


### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>クラウドベースの配布ポイントに使用される証明書を更新する

Configuration Manager では、サイト サーバーがクラウドベースの配布ポイントと通信するために、Azure 管理証明書が必要です。 サイトの回復後に、クラウドベースの配布ポイントの証明書を更新します。



## <a name="recover-a-secondary-site"></a>セカンダリ サイトの回復

Configuration Manager はセカンダリ サイトのデータベースのバックアップをサポートしていませんが、セカンダリ サイトの再インストールによる回復はサポートしています。 セカンダリ サイトの回復は、Configuration Manager セカンダリ サイトで障害が発生した場合に必要になります。


### <a name="requirements"></a>［要件］

- サーバーがセカンダリ サイトのすべての前提条件を満たしており、適切なセキュリティ権限が構成されている必要があります。  

- 障害が発生したサイトに使用したのと同じインストール パスを使います。  

- 障害が発生したサーバーと同じ構成でサーバーを使います。 この構成には、その完全修飾ドメイン名 (FQDN) が含まれます。  

- サーバーには、障害が発生したサイトと同じ SQL Server の構成が必要です。  

     - コンピューターに SQL Server Express がまだインストールされていない場合、セカンダリ サイトの回復中に Configuration Manager によってインストールされません。  

     - 障害が発生する前にセカンダリ サイト データベースで使用していたのと同じバージョンの SQL Server および同じ SQL Server インスタンスを使用します。  


### <a name="procedure"></a>手順

Configuration Manager コンソールの **[サイト]** ノードから、**[セカンダリ サイトの回復]** アクションを使用します。 他の種類のサイトとは異なり、セカンダリ サイトの回復ではバックアップ ファイルを使いません。 このプロセスでは、障害が発生したサーバーにセカンダリ サイトのファイルが再インストールされます。 サイトの再インストール後に、セカンダリ サイトのデータが親プライマリ サイトから再初期化されます。

回復プロセスの間に、Configuration Manager はセカンダリ サイト サーバーにコンテンツ ライブラリが存在するかどうかを確認します。 また、適切なコンテンツが利用可能なことも確認します。 適切なコンテンツが含まれている場合、セカンダリ サイトでは既存のコンテンツ ライブラリが使われます。 そうでない場合は、セカンダリ サイトのコンテンツ ライブラリを回復するため、サーバーにコンテンツを再配布または事前設定します。

セカンダリ サイト サーバーに存在しない配布ポイントがある場合は、セカンダリ サイトの回復中に配布ポイントを再インストールする必要はありません。 セカンダリ サイトの回復後に、サイトが配布ポイントと自動的に同期されます。

Configuration Manager コンソールの **[サイト]** ノードから **[インストール ステータスの表示]** アクションを使って、セカンダリ サイトの回復の状態を確認できます。