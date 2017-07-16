---
title: "サイトの回復 | Microsoft Docs"
description: "System Center Configuration Manager でのサイトの回復について説明します。"
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: f7cd9c71287d62c9f5d36e2f032bc2a6065572ae
ms.openlocfilehash: 49eea15ea2888f8f93c33eb771c09147ba21529e
ms.contentlocale: ja-jp
ms.lasthandoff: 06/06/2017

---

#  Configuration Manager サイトの回復
<a id="recover-a-configuration-manager-site" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager サイトで障害が発生した場合や、サイト データベースのデータが損失した場合は、Configuration Manager サイトの回復を実行します。 サイトの回復の中心となる作業は、データの修復と同期です。これは、業務の中断を防ぐためにも必要な作業です。

このトピックのセクションは、Configuration Manager サイトを回復する場合に役立ちます。 バックアップを作成する場合は、[Configuration Manager のバックアップ](/sccm/protect/understand/backup-and-recovery)に関するページを参照してください。

## サイトを回復する前の注意事項
<a id="considerations-before-recovering-a-site" class="xliff"></a>
**同じバージョンおよびエディションの SQL Server を使用する必要があります:** たとえば、SQL Server 2014 で実行していたデータベースを SQL Server 2016 に復元することはできません。 同様に、SQL Server 2016 の Standard エディションで実行していたサイト データベースを SQL Server 2016 の Enterprise エディションに復元することはできません。
-   SQL Server を **シングル ユーザー モード**に設定しないでください。
-   MDF ファイルと LDF ファイルが有効であることを確認します。 サイトを回復するときに、復元するファイルの状態は確認されません。

**SQL Server Always On 可用性グループを使用して、サイト データベースをホストする場合:** [SQL Server Always On の使用準備](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery)に関するページの説明に従って、回復計画を変更します。

**データベースのレプリカを使用する場合:** データベースのレプリカ用に構成されたサイト データベースを復元した後で、データベースのレプリカを使用するためには、データベースの各レプリカを再構成して、パブリケーションとサブスクリプションの両方を再作成する必要があります。

## 回復オプションの検討
<a id="determine-your-recovery-options" class="xliff"></a>
Configuration Manager のプライマリ サイト サーバーと中央管理サイトの回復について検討すべき点が 2 つ (**サイト サーバー**と**サイト データベース**) あります。
次のセクションは、回復シナリオに最適なオプションを選択するのに役立ちます。

> [!NOTE]   
> セットアップにより、サーバーで既存の Configuration Manager サイトが検出された場合、サイトの回復を開始できますが、サイト サーバーの回復オプションが限られます。 たとえば、既存のサイト サーバーでセットアップを実行した場合は、サイト データベース サーバーは回復できますが、サイト サーバーの回復オプションは無効になっています。

### サイト サーバーの回復オプション
<a id="site-server-recovery-options" class="xliff"></a>
Configuration Manager インストール フォルダーの外に作成した **CD.Latest** フォルダーのコピーから、セットアップを開始します。
-   サイト サーバーの **[スタート]** メニューから Configuration Manager セットアップを実行する場合は、**[サイトを回復する]** オプションは使用できません。
-   Configuration Manager コンソール内から更新プログラムをインストールした後でバックアップを作成した場合は、インストール メディアのセットアップまたは Configuration Manager のインストール パスを使用してサイトを正常に再インストールすることはできません。

その後、**[サイトを回復する]** オプションを選択します。 障害が発生したサイト サーバーに対して選択できる回復オプションは次のとおりです。

-   **既存のバックアップを使用してこのサイト サーバーを回復する**: サイトで障害が発生する前に、**サイト サーバーのバックアップ** メンテナンス タスクの一部としてサイト サーバーに作成された Configuration Manager サイト サーバーをバックアップしている場合に、このオプションを使用します。 サイトが再インストールされ、バックアップされているサイトに基づいて、サイト設定が構成されます。
-   **このサイト サーバーを再インストールする**: サイト サーバーのバックアップがない場合に、このオプションを使用します。 サイト サーバーが再インストールされますが、初めてインストールしたときと同じようにして、サイト設定を指定する必要があります。
  -   障害が発生したサイトを初めてインストールしたときに使用したものと同じサイト コードとサイト データベース名を使用する必要があります。
  -   新しいオペレーティング システムを実行する新しいコンピューターにサイトを再インストールすることができます。
  -   コンピューターでは、元のサイト サーバーと同じ名前 (FQDN) を使用する必要があります。   

### サイト データベースの回復オプション
<a id="site-database-recovery-options" class="xliff"></a>
セットアップを実行するときに、次のサイト データベースの回復オプションを選択できます。
-   **バックアップ セットを使用してサイト データベースを復元する**: サイト データベースで障害が発生する前に、サイトで実行された**サイト サーバーのバックアップ** メンテナンス タスクの一部として作成された Configuration Manager サイト データベースのバックアップが存在する場合に、このオプションを使用します。 階層構造がある場合は、サイト データベースの最後のバックアップ以後に加えられた変更が、中央管理サイト (プライマリ サイトを回復するとき)、または基準プライマリ サイト (中央管理サイトを回復するとき) から取得されます。 スタンドアロンのプライマリ サイトのサイト データベースを回復する場合は、最後のバックアップ以後にサイトに加えられた変更を回復することはできません。

   階層内のサイトのサイト データベースを回復するときは、そのサイトが中央管理サイトとプライマリ サイトのどちらであるかと、最後のバックアップが SQL Server の変更の追跡の保有期間内に作成されたかどうかによって、回復方法が異なります。 詳細については、このトピックの [「サイト データベースの回復方法」](##site-database-recovery-scenarios) セクションを参照してください。
  > [!NOTE]   
  > サイト データベースが存在するのに、バックアップ セットを使用してサイト データベースを回復するオプションを選択した場合は、正常に回復できません。  

-   **このサイトの新しいデータベースを作成する**: Configuration Manager サイト データベースのバックアップがない場合に、このオプションを使用します。 階層構造がある場合は、新しいデータベースが作成され、プライマリ サイトの回復用には、中央管理サイトからレプリケートされたデータが使われ、中央管理サイトの回復用には、基準プライマリ サイトからレプリケートされたデータが使われます。 スタンドアロンのプライマリ サイトを回復する場合や、プライマリ サイトのない中央管理サイトを回復する場合は、このオプションを選択することはできません。

-   **手動で回復したサイト データベースを使用する**: Configuration Manager サイト データベースを既に回復しているが、回復プロセスを完了する必要がある場合に、このオプションを使用します。
    -   Configuration Manager では、Configuration Manager のバックアップ メンテナンス タスク、または DPM や別のプロセスを使用して実行したサイト データベース バックアップからサイト データベースを回復できます。 Configuration Manager 以外の方法を使用してサイト データベースを復元した場合は、サイト データベースの回復を完了するために、セットアップを実行して、このオプションを選択する必要があります。

    > [!NOTE]   
    > DPM を使用してサイト データベースをバックアップするときに、Configuration Manager で復元プロセスを続行する前に、DPM の手順を使用して指定の場所にサイト データベースを復元します。 DPM の詳細については、TechNet の「 [Data Protection Manager]() 」ドキュメント ライブラリを参照してください。    

    -   階層構造がある場合は、サイト データベースの最後のバックアップ以後に加えられた変更が、中央管理サイト (プライマリ サイトを回復するとき)、または基準プライマリ サイト (中央管理サイトを回復するとき) から取得されます。 スタンドアロンのプライマリ サイトのサイト データベースを回復する場合は、最後のバックアップ以後にサイトに加えられた変更を回復することはできません。     


-   **データベースの回復をスキップする**: Configuration Manager サイト データベース サーバーのデータが失われていない場合に、このオプションを使用します。 このオプションは、回復しようとしているサイト サーバーとは別のコンピューターにサイト データベースがある場合だけ選択できます。

### SQL Server の変更の追跡の保有期間
<a id="sql-server-change-tracking-retention-period" class="xliff"></a>
SQL Server のサイト データベースでは、変更の追跡機能が有効になっています。 そのため、過去のある時点以後にデータベース テーブルに加えられた変更に関する情報を、Configuration Manager が照会することができます。 保有期間とは、この変更の追跡データを残しておく期間のことです。 既定では、サイト データベースの追跡データの保有期間は 5 日に構成されています。 サイト データベースを回復するときは、バックアップがこの保有期間内に作成されたかどうかによって、回復プロセスが異なります。 たとえば、サイト データベースで障害が発生した時点で、最も新しいバックアップが作成後 7 日経過している場合は、保有期間外に作成されていることになります。

SQL Server の変更追跡の内部構造については、SQL Server チームのブログ「[Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/)」(変更追跡のクリーンアップ - パート 1) と「[Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2)」(変更追跡のクリーンアップ - パート 2) を参照してください。

### サイト データまたはグローバル データの再初期化
<a id="reinitialization-of-site-or-global-data" class="xliff"></a>
サイトのデータまたはグローバル データの再初期化とは、サイト データベースにある既存のデータを別のサイト データベースに置き換えるプロセスのことです。 たとえば、"ABC" というサイトのデータを "XYZ" というサイトのデータで再初期化するときは、次の処理が行われます。
-   サイト "XYZ" からサイト "ABC" にデータがコピーされます。
-   サイト "ABC" のサイト データベースから、サイト "XYZ" の既存のデータが削除されます。
-   サイト "XYZ" からコピーされたデータが、サイト "ABC" のサイト データベースに挿入されます。

#### 例 1
<a id="example-scenario-1" class="xliff"></a>
**プライマリ サイトで、中央管理サイトからグローバル データを再初期化する**: 回復プロセスで、プライマリ サイト データベースにあるプライマリ サイト用の既存のグローバル データが削除され、中央管理サイトからコピーされたグローバル データに置き換えられます。

#### 例 2
<a id="example-scenario-2" class="xliff"></a>
**中央管理サイトで、プライマリ サイトからサイト データを再初期化する**: 回復プロセスで、中央管理サイト データベースにある、該当するプライマリ サイト用の既存のサイト データが削除され、そのプライマリ サイトからコピーされたサイト データに置き換えられます。 他のサイト用のサイト データは影響を受けません。

### サイト データベースの回復方法
<a id="site-database-recovery-scenarios" class="xliff"></a>
サイト データベースがバックアップから復元されると、Configuration Manager は前回のデータベースのバックアップ以後にサイト データとグローバル データに加えられた変更の回復を試みます。 以下に、サイト データベースがバックアップから復元された後に Configuration Manager で開始される処理について説明します。

**回復したサイトが中央管理サイトの場合:**
-   **データベースが、変更の追跡の保有期間以内にバックアップされている場合**
    -   **グローバル データ:** バックアップ後のグローバル データの変更は、すべてのプライマリ サイトからレプリケートされます。
    -   **サイト データ:** バックアップ後のサイト データの変更は、すべてのプライマリ サイトからレプリケートされます。


-   **データベースが、変更の追跡の保有期間より前にバックアップされている場合**
    -   **グローバル データ:** 基準プライマリ サイトを指定すると、中央管理サイトは基準プライマリ サイトからのグローバル データを再初期化します。 他のすべてのプライマリ サイトを、中央管理サイトのグローバル データで再初期化します。 基準サイトを指定していない場合は、すべてのプライマリ サイトを、中央管理サイトのグローバル データ (バックアップから復元されたデータ) で再初期化します。
    -   **サイト データ:** 中央管理サイトは各プライマリ サイトからのサイト データを再初期化します。


**回復したサイトがプライマリ サイトの場合:**
-   **データベースが、変更の追跡の保有期間以内にバックアップされている場合**
    -   **グローバル データ:** バックアップ後のグローバル データの変更は、中央管理サイトからレプリケートされます。
    -   **サイト データ:** 中央管理サイトはプライマリ サイトからのサイト データを再初期化します。 バックアップ以降に加えられた変更は失われますが、データの大部分は、プライマリ サイトに情報を送信するクライアントによって、再び生成されます。


-   **データベースが、変更の追跡の保有期間より前にバックアップされている場合**
    -   **グローバル データ:** プライマリ サイトは中央管理サイトからのグローバル データを再初期化します。
    -   **サイト データ:** 中央管理サイトはプライマリ サイトからのサイト データを再初期化します。 バックアップ以降に加えられた変更は失われますが、データの大部分は、プライマリ サイトに情報を送信するクライアントによって、再び生成されます。

## サイトの回復手順
<a id="site-recovery-procedures" class="xliff"></a>
次のいずれかの手順に従って、サイト サーバーとサイト データベースを回復します。

### セットアップ ウィザードを使ってサイトの回復を開始するには
<a id="to-start-a-site-recovery-in-the-setup-wizard" class="xliff"></a>
1.  Configuration Manager インストール フォルダー外の場所に [CD.Latest フォルダー](/sccm/core/servers/manage/the-cd.latest-folde)をコピーします。
CD.Latest フォルダーのコピーから、Configuration Manager セットアップ ウィザードを実行します。

2.  [ **はじめに** ] ページで、[ **サイトを回復する**] を選択してから、[ **次へ**] をクリックします。

3.  表示される指示に従って、順次適切なオプションを選択し、ウィザードを完了します。

  -   サイトの回復中に、セットアップ プログラムによって、SQL Server で使用している SQL Server Service Broker (SSB) のポートが検出されます。 サイトの回復中に、このポートの設定を変更しないでください。変更すると、回復が完了した後で、データが正しくレプリケートされません。

  -   セットアップ ウィザードで Configuration Manager のインストールに使用する元のパスまたは新しいパスを指定できます。

### サイトの無人回復を開始するには
<a id="to-start-an-unattended-site-recovery" class="xliff"></a>
  1.    サイトを回復するのに必要な無人インストール スクリプトを準備します。  「[サイトの無人回復スクリプト ファイルのキー](/sccm/protect/understand/unattended-site-recovery-script-file-keys)」を参照してください。

  2.    コマンド **/script** オプションを使用して、Configuration Manager セットアップを実行します。 たとえば、セットアップの初期化ファイルに ConfigMgrUnattend.ini という名前を付けて、Setup コマンドを実行するコンピューターの C:\Temp ディレクトリに保存した場合、コマンドは次のようになります: **Setup /script C:\temp\ConfigMgrUnattend.ini**

  > [!NOTE]   
  >  中央管理サイトを回復した後、子サイトからの一部のサイト データのレプリケーションの確立が失敗する場合があります。 これには、ハードウェア インベントリ、ソフトウェア インベントリおよびステータス メッセージが含まれることがあります。
  >
  >  このことが発生した場合は、データベース レプリケーションの **ConfigMgrDRSSiteQueue** を再初期化する必要があります。  このためには、**SQL Server Manager** を使用して、中央管理サイトの Configuration Manager サイト データベースで次のクエリを実行します。
  >
  >  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**
  >
  >  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**


## 回復後の作業
<a id="post-recovery-tasks" class="xliff"></a>
サイトを回復した後で行わなければならない作業がいくつかあります。 次のセクションの情報を、サイトの回復プロセスを完了させるときの参考にしてください。

### ユーザー アカウントのパスワードを再入力する
<a id="re-enter-user-account-passwords" class="xliff"></a>
サイト サーバーの回復が終わったら、そのサイトに指定していたユーザー アカウントのパスワードを再入力する必要があります。これは、サイトの回復中にパスワードがリセットされるためです。 これらのアカウントは、サイトの回復が終わったときに、セットアップ ウィザードの **[完了]** ページに一覧され、回復したサイト サーバーの C:\ConfigMgrPostRecoveryActions.html に保存されます。

#### サイトの回復後にユーザー アカウントのパスワードを再入力するには
<a id="to-re-enter-user-account-passwords-after-site-recovery" class="xliff"></a>

1.  Configuration Manager コンソールを開き、回復したサイトに接続します。

2.  Configuration Manager コンソールで、[ **管理**] をクリックします。

3.  [ **管理** ] ワークスペースで、[ **セキュリティ**] を展開してから、[ **アカウント**] をクリックします。

4.  パスワードを再入力するアカウントごとに、次の操作を行います。

    1.  サイトの回復が終わったときに保存されたアカウントの一覧で、アカウントを選択します。 この一覧は、回復したサイト サーバーの C:\ConfigMgrPostRecoveryActions.html にあります。

    2.  [ **ホーム** ] タブの [ **プロパティ** ] グループで、[ **プロパティ** ] をクリックしてアカウントのプロパティを開きます。

    3.  [ **全般** ] タブで、[ **設定**] をクリックしてから、アカウントのパスワードを再入力します。

    4.  [ **確認**] をクリックし、選択したユーザー アカウントの適切なデータ ソースを選択します。[ **接続のテスト** ] をクリックして、そのユーザー アカウントでデータ ソースに接続できるかどうかを確認します。

    5.  [ **OK** ] をクリックしてパスワードの変更を保存してから、[ **OK**] をクリックします。

### サイドローディング キーの再入力
<a id="re-enter-sideloading-keys" class="xliff"></a>
サイト サーバーの回復が終わったら、そのサイトに指定していた Windows サイドローディング キーを再入力する必要があります。これは、サイトの回復中にサイドローディング キーがリセットされるためです。 サイドローディング キーを再入力すると、Configuration Manager コンソールで Windows サイドローディング キーの **[使用済みライセンス認証数]** 列内のカウントがリセットされます。 たとえば、サイト エラーが発生する前に、**[合計ライセンス認証数]** カウントが **100** に設定され、**[使用済みライセンス認証数]** がデバイスで使用されていたキーの数に相当する **90** になっていたとします。 サイトの回復後、[ **合計ライセンス認証数** ] 列には **100**と表示されますが、[ **使用済みライセンス認証数** ] 列には誤って **0**と表示されます。 しかし、新しく 10 台のデバイスがサイドローディング キーを使用すると、ライセンスの残りがなくなってしまうので、11 台目以降、キーを取得できなくなります。

### Microsoft Intune サブスクリプションの再作成
<a id="recreate-the-microsoft-intune-subscription" class="xliff"></a>
 サイト サーバー コンピューターが再イメージ化された後に Configuration Manager サイト サーバーを回復する場合、Microsoft Intune のサブスクリプションは復元されません。 サイトを回復した後、サブスクリプションを再接続する必要があります。  新しい APN 要求は作成しないでください。代わりに、最後に iOS 管理を構成または更新した現在の有効な .pem-file をアップロードしてください。 詳細については、「 [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription)」をご覧ください。

### IIS を使用するサイト システムの役割の SSL を構成する
<a id="configure-ssl-for-site-system-roles-that-use-iis" class="xliff"></a>
IIS を実行するサイト システムを回復し、障害が発生する前に、そのシステムが HTTPS 接続用に構成されていた場合は、IIS で Web サーバー証明書を使用するように再構成する必要があります。

### 回復したサイト サーバーに修正プログラムを再インストールする
<a id="reinstall-hotfixes-in-the-recovered-site-server" class="xliff"></a>
サイトの回復が終わったら、障害が発生する前にサイト サーバーに適用されていた修正プログラムを再インストールする必要があります。 サイトの回復後にセットアップ ウィザードの **[完了]** ページで、以前にインストールした修正プログラムのリストを表示します。 このリストは、回復したサイト サーバーの **C:\ConfigMgrPostRecoveryActions.html** にも保存されます。

### Reporting Services を実行しているコンピューターで使用していたカスタム レポートを復元する
<a id="recover-custom-reports-on-the-computer-running-reporting-services" class="xliff"></a>
Reporting Services で障害が発生する前に、Reporting Services のカスタム レポートを作成していた場合は、レポート サーバーのバックアップ (存在する場合) から、カスタム レポートを復元することができます。 Reporting Services のカスタム レポートの復元の詳細については、SQL Server 2008 Books Online の「 [Reporting Services インストールのバックアップおよび復元操作](http://go.microsoft.com/fwlink/p/?LinkId=228724) 」を参照してください。

### コンテンツ ファイルを回復する
<a id="recover-content-files" class="xliff"></a>
 サイト データベースには、サイト サーバーでのコンテンツ ファイルの保存場所に関する情報が含まれていますが、コンテンツ ファイル自体は、バックアップと復元プロセスで、バックアップも復元もされません。 コンテンツ ファイルを完全に回復するには、コンテンツ ライブラリのファイルとパッケージ ソース ファイルを元の場所に復元する必要があります。 コンテンツ ファイルを回復する方法はいくつかありますが、一番簡単なのは、サイト サーバーのファイル システムのバックアップからファイルを復元する方法です。

 パッケージ ソース ファイル用のファイル システムのバックアップがない場合は、最初にパッケージを作成したときと同じようにして、ファイルを手動でコピーまたはダウンロードする必要があります。 すべてのパッケージとアプリケーションのパッケージ ソースの場所を見つけるには、SQL Server で `SELECT * FROM v_Package`というクエリを実行します。 パッケージ ID の先頭の 3 文字を見ると、パッケージ ソースのサイトがわかります。 たとえば、CEN00001 というパッケージ ID では、CEN がソース サイトのサイト コードです。 パッケージのソース ファイルを復元するときは、障害発生前と同じ場所に復元する必要があります。

 コンテンツ ライブラリが含まれているファイル システムのバックアップがない場合は、次の方法でコンテンツ ファイルを復元できます。

-   **事前設定済みのコンテンツ ファイルをインポートする**: Configuration Manager 階層がある場合は、別の場所にあるすべてのパッケージとアプリケーションの事前設定済みコンテンツ ファイルを作成し、そのファイルをインポートして、サイト サーバーのコンテンツ ライブラリを回復できます。

-   **コンテンツを更新する**: パッケージまたはアプリケーションの展開の種類のコンテンツの更新操作を開始すると、コンテンツがパッケージ ソースからコンテンツ ライブラリにコピーされます。 この処理が正常に完了するには、パッケージ ソース ファイルが元の場所になければなりません。 回復したいパッケージとアプリケーションごとに、コンテンツの更新操作を行う必要があります。

### Updates Publisher を実行していたコンピューターのカスタム ソフトウェア更新プログラムを回復する
<a id="recover-custom-software-updates-on-the-computer-running-updates-publisher" class="xliff"></a>
Updates Publisher データベース ファイルをバックアップ計画に含めていた場合は、Updates Publisher を実行していたコンピューターで障害が発生したときに、そのデータベースを回復できます。 Updates Publisher の詳細については、System Center TechCenter ライブラリの「 [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) 」を参照してください。

次の手順に従って、Updates Publisher データベースを復元します。

#### Updates Publisher 2011 データベースを復元するには
<a id="to-restore-the-updates-publisher-2011-database" class="xliff"></a>
1.  回復したコンピューターに Updates Publisher を再インストールします。

2.  バックアップしていたデータベース ファイル (Scupdb.sdf) を、Updates Publisher を実行するコンピューターの %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ にコピーします。

3.  コンピューターで複数のユーザーが Updates Publisher を実行する場合は、それぞれのユーザー プロファイルの適切な場所に、データベース ファイルをコピーする必要があります。

### ユーザー状態の移行データ
<a id="user-state-migration-data" class="xliff"></a>
状態移行ポイントのサイト システムのプロパティを設定するときに、ユーザー状態の移行データを保存するフォルダーを指定しています。 ユーザー状態の移行データを保存するフォルダーのあるサーバーを回復したら、障害発生前にデータを保存していたフォルダーと同じフォルダーに、ユーザー状態の移行データを手動で復元する必要があります。

### 配布ポイント用の証明書の再生成
<a id="regenerate-the-certificates-for-distribution-points" class="xliff"></a>
サイトの復元後には、1 つまたは複数の配布ポイントに対する **cert PFX データを解読できませんでした**というエントリが distmgr.log に含まれていることがあります。 このエントリは、配布ポイントの証明書データをサイトで解読できないことを示します。 この問題を解決するには、影響を受ける配布ポイントの証明書を再生成または再インポートする必要があります。 それには [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) PowerShell コマンドレットを使用します。

### クラウドベースの配布ポイントに使用する証明書の更新
<a id="update-certificates-used-for-cloud-based-distribution-points" class="xliff"></a>
 Configuration Manager では、サイト サーバーからクラウドベースの配布ポイントへの通信に使用する管理証明書が必要です。 サイトの回復後に、クラウドベースの配布ポイントの証明書を更新する必要があります。

## セカンダリ サイトの回復
<a id="recover-a-secondary-site" class="xliff"></a>
 Configuration Manager はセカンダリ サイトのデータベースのバックアップをサポートしていませんが、セカンダリ サイトの再インストールによる回復はサポートしています。 セカンダリ サイトの回復は、Configuration Manager セカンダリ サイトで障害が発生した場合に必要になります。

### セカンダリ サイトを再インストールする場合の要件
<a id="requirements-for-reinstalling-a-secondary-site" class="xliff"></a>
-   コンピューターがセカンダリ サイトのすべての前提条件を満たしており、適切なセキュリティ権限が構成されている必要があります。
-   障害が発生したサイトに使用したのと同じインストール パスを使用する必要があります。
-   セカンダリ サイトを適切に回復するには、障害が発生したコンピューターと同じ構成 (FQDN など) のコンピューターを使用する必要があります。
-   コンピューターには、障害が発生したサイトと同じ SQL Server の構成が必要です。
  -   コンピューターに SQL Server Express がまだインストールされていない場合、セカンダリ サイトの回復中に Configuration Manager によってインストールされません。
  -   障害が発生する前にセカンダリ サイト データベースで使用していたのと同じバージョンの SQL Server および同じ SQL Server インスタンスを使用する必要があります。

### セカンダリ サイトを回復するには、次のようにします。
<a id="to-recover-a-secondary-site" class="xliff"></a>
セカンダリ サイトを回復するには、Configuration Manager コンソールの **[サイト]** ノードから、**[セカンダリ サイトの回復]** アクションを使用します。 中央管理サイトまたはプライマリ サイトの回復とは異なり、セカンダリ サイトの回復ではバックアップ ファイルを使用せず、代わりに障害が発生したセカンダリ サイトのコンピューターにセカンダリ サイトのファイルを再インストールします。 サイトの再インストール後に、セカンダリ サイトのデータが親プライマリ サイトからのデータで再初期化されます。

回復プロセスで、Configuration Manager は、セカンダリ サイトのコンピューターにコンテンツ ライブラリが存在することと、適切なコンテンツが使用できることを確認します。 適切なコンテンツが含まれている場合、セカンダリ サイトでは、既存のコンテンツ ライブラリが使用されます。 それ以外の場合、回復したセカンダリ サイトのコンテンツ ライブラリを回復するには、回復したサイトにコンテンツを再配布するかまたは事前設定する必要があります。

使用する配布ポイントがセカンダリ サイトに存在するのではない場合は、セカンダリ サイトの回復中に配布ポイントを再インストールする必要はありません。 セカンダリ サイトの回復後に、サイトが配布ポイントと自動的に同期されます。

Configuration Manager コンソールの **[サイト]** ノードから **[インストール ステータスの表示]** アクションを使用して、セカンダリ サイトの回復のステータスを確認することができます。
