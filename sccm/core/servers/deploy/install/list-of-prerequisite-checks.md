---
title: 前提条件の確認
titleSuffix: Configuration Manager
description: Configuration Manager の更新プログラムに関する特定の前提条件の確認のリファレンス。
ms.date: 12/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4fdc882d63e7bf7d3189e770f230412f17ca0b63
ms.sourcegitcommit: d36e4c7082a5144e79035dd8847c8e741fa04667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2018
ms.locfileid: "53444656"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Configuration Manager の前提条件の確認の一覧

*適用対象:System Center Configuration Manager (Current Branch)*

この記事では、Configuration Manager のインストール時または更新時に行われる前提条件の確認について詳しく説明します。 詳細については、[前提条件チェッカー](/sccm/core/servers/deploy/install/prerequisite-checker)に関するページを参照してください。  



##  <a name="BKMK_Security"></a> セキュリティ権限  


### <a name="security-rights-errors"></a>［セキュリティ権限］:エラー

#### <a name="administrator-rights-on-central-administration-site"></a>中央管理サイトの管理者権限 
*適用対象:プライマリ サイト*

Configuration Manager セットアップを実行するユーザー アカウントに、中央管理サイト サーバーに対する**管理者**権限があります。

#### <a name="administrative-rights-on-expand-primary-site"></a>展開プライマリ サイトの管理者権限 
*適用対象:中央管理サイト*

階層にプライマリ サイトを展開する際に、セットアップを実行するユーザー アカウントに、スタンドアロン プライマリ サイト サーバーに対する**管理者**権限があります。

#### <a name="administrative-rights-on-site-system"></a>サイト システムの管理者権限 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

Configuration Manager セットアップを実行するユーザー アカウントに、サイト サーバーに対する**管理者**権限があります。

#### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>展開プライマリ サイトに対する中央管理サイト サーバーの管理者権限 
*適用対象:中央管理サイト*

階層にプライマリ サイトを展開する際に、中央管理サイト サーバーのコンピューター アカウントに、スタンドアロン プライマリ サイト サーバーに対する**管理者**権限があります。

#### <a name="connection-to-sql-server-on-central-administration-site"></a>中央管理サイトの SQL Server への接続 
*適用対象:プライマリ サイト*

既存の階層に含めるプライマリ サイトで Configuration Manager セットアップを実行するユーザー アカウントに、中央管理サイトの SQL Server インスタンスに対する **sysadmin** の役割があります。

#### <a name="site-server-computer-account-administrative-rights"></a>サイト サーバー コンピューター アカウントの管理者権限 
*適用対象:プライマリ サイト、サイト データベース サーバー*

サイト サーバー コンピューター アカウントに、SQL サーバーと管理ポイントに対する**管理者**権限があります。

#### <a name="sql-server-sysadmin-rights"></a>SQL Server の sysadmin 権限 
*適用対象:サイト データベース サーバー*

Configuration Manager セットアップを実行するユーザー アカウントに、サイト データベースのインストール用に選択した SQL Server インスタンスに対する **sysadmin** の役割があります。 この確認は、アクセス許可の確認のためにセットアップが SQL Server のインスタンスにアクセスできない場合も失敗します。

#### <a name="sql-server-sysadmin-rights-for-reference-site"></a>基準サイト用の SQL Server sysadmin 権限 
*適用対象:サイト データベース サーバー*

Configuration Manager セットアップを実行するユーザー アカウントに、基準サイトのデータベースとして選択した SQL Server の役割インスタンスに対する **sysadmin** の役割があります。 SQL Server の役割アクセス許可 **sysadmin** は、サイト データベースを変更するために必要です。


### <a name="security-rights-warnings"></a>［セキュリティ権限］:［警告］

#### <a name="site-system-to-sql-server-communication"></a>サイト システムから SQL Server への通信  
*適用対象:セカンダリ サイト、管理ポイント*

サイト データベース インスタンスの SQL Server サービスの実行用に構成したアカウントに、Active Directory Domain Services で有効なサービス プリンシパル名 (SPN) があります。 Kerberos 認証をサポートするには、Active Directory で有効な SPN を登録します。

#### <a name="sql-server-security-mode"></a>SQL Server のセキュリティ モード 
*適用対象:サイト データベース サーバー*

Windows 認証セキュリティ用に SQL Server が構成されています。



##  <a name="BKMK_Dependencies"></a> 依存関係

### <a name="dependencies-errors"></a>依存関係:エラー

#### <a name="active-migration-mappings-on-the-target-primary-site"></a>ターゲット プライマリ サイトにアクティブな移行へのマッピング 
*適用対象:中央管理サイト*

プライマリ サイトにアクティブな移行へのマッピングがありません。

#### <a name="active-replica-mp"></a>アクティブなレプリカ MP 
*適用対象:プライマリ サイト*

アクティブな管理ポイントのレプリカがあります。

#### <a name="bits-enabled"></a>BITS 対応 
*適用対象:管理ポイント*

管理ポイントにバックグラウンド インテリジェント転送サービス (BITS) がインストールされています。 次のいずれかの理由で、この確認が失敗する場合があります。 
- BITS がインストールされていない  
- IIS 7.0 用の IIS 6.0 WMI 互換性コンポーネントが、サーバーまたはリモート IIS ホストにインストールされていない  
- セットアップでリモート IIS 設定を確認できなかった。 IIS の共通コンポーネントがサイト サーバーにインストールされていない。  

#### <a name="case-insensitive-collation-on-sql-server"></a>SQL Server の照合順序の大文字と小文字の区別 
*適用対象:サイト データベース サーバー*

SQL Server のインストールで、**SQL_Latin1_General_CP1_CI_AS** などの大文字と小文字が区別されない照合順序が使用されています。

#### <a name="check-existing-stand-alone-primary-site-for-version-and-site-code"></a>バージョンとサイト コードについて、既存のスタンドアロン プライマリ サイトを確認する 
*適用対象:中央管理サイト、プライマリ サイト*

展開を計画しているプライマリ サイトがスタンドアロン プライマリ サイトです。 Configuration Manager のバージョンは同じですが、サイト コードがインストールする中央管理サイトとは異なっています。

#### <a name="check-for-incompatible-collection-references"></a>互換性のないコレクションを参照しているかどうかの確認 
*適用対象:中央管理サイト*

アップグレード中に、コレクションで同じ種類の他のコレクションのみが参照されます。

#### <a name="client-version-on-management-point-computer"></a>管理ポイント コンピューター上のクライアントのバージョン 
*適用対象:管理ポイント*

別のバージョンの Configuration Manager クライアントがインストールされていないサーバーに、管理ポイントをインストールします。

#### <a name="dedicated-sql-server-instance"></a>専用の SQL Server インスタンス 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

Configuration Manager サイト データベースをホストするように SQL Server の専用インスタンスを構成しています。 

別のサイトでインスタンスを使用する場合は、新しいサイト用に別のインスタンスを選択する必要があります。 別のサイトをアンインストールすることも、そのデータベースを SQL Server の別のインスタンスに移動することもできます。

#### <a name="existing-configuration-manager-server-components-on-server"></a>サーバー上の既存の Configuration Manager サーバー コンポーネント 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

サイトのインストール用に選択されたサーバーに、サイト サーバーやサイト システムの役割がまだインストールされていません。

#### <a name="firewall-exception-for-sql-server"></a>SQL Server 用のファイアウォールの例外 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト、管理ポイント*

Windows ファイアウォールが無効になっている、または適切な Windows ファイアウォールの例外が SQL Server に対して存在します。 

Sqlservr.exe または必要な TCP ポートへのリモート アクセスを許可します。 既定では、SQL Server は TCP ポート 1433 でリッスンし、SQL Server Service Broker (SSB) は TCP ポート 4022 を使用します。

#### <a name="iis-service-running"></a>IIS サービス実行中 
*適用対象:管理ポイント、配布ポイント*

管理ポイントまたは配布ポイント用のサーバーに IIS がインストールされ、実行されています。

#### <a name="match-collation-of-expand-primary-site"></a>展開プライマリ サイトの照合順序の一致 
*適用対象:中央管理サイト*

階層にプライマリ サイトを展開する際に、スタンドアロン プライマリ サイトのサイト データベースの照合順序が、中央管理サイトのサイト データベースと同じになっています。

#### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>登録されている Microsoft Remote Differential Compression (RDC) ライブラリ 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

RDC ライブラリが、Configuration Manager サイト サーバーに登録されています。

#### <a name="microsoft-windows-installer"></a>Microsoft Windows インストーラー 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

Windows インストーラーのバージョンを確認します。 

この確認が失敗した場合、セットアップでバージョンを確認できなかったか、インストールされたバージョンが Windows インストーラーの最小要件である 4.5 を満たしていません。

#### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Configuration Manager コンソールに最低限必要な .NET Framework のバージョン 
*適用対象:Configuration Manager コンソール*

Microsoft .NET Framework 4.0 が Configuration Manager コンソール コンピューターにインストールされています。 

#### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Configuration Manager サイト サーバーに最低限必要な .NET Framework のバージョン 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

Configuration Manager サイト サーバーで .NET Framework 3.5 がインストールされているか、有効になっています。 

#### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Configuration Manager セカンダリ サイト用 SQL Server Express エディションのインストールに最低限必要な .NET Framework のバージョン 
*適用対象:セカンダリ サイト*

Configuration Manager セカンダリ サイト サーバーで .NET Framework 4.0 がインストールされているか、有効になっています。 このバージョンは SQL Server Express で必要です。

#### <a name="parent-database-collation"></a>親データベースの照合順序 
*適用対象:プライマリ サイト、セカンダリ サイト*

サイト データベースの照合順序が、親サイトのデータベースの照合順序と一致しています。 階層内のすべてのサイトが同じデータベース照合順序を使用する必要があります。

#### <a name="primary-fqdn"></a>プライマリ FQDN 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト、サイト データベース サーバー*

コンピューターの NetBIOS 名が、完全修飾ドメイン名 (FQDN) のローカル ホスト名と一致しています。

#### <a name="required-sql-server-collation"></a>SQL Server の必須の照合順序 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

SQL Server のインスタンスが、**SQL_Latin1_General_CP1_CI_AS** 照合順序を使用するように構成されています。 

Configuration Manager サイト データベースが既にインストールされている場合、この確認はデータベースにも適用されます。 SQL Server インスタンスとデータベースの照合順序の変更方法の詳細については、[SQL の照合順序と Unicode サポート](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support)に関するページを参照してください。 

中国語の OS を使用しており、GB18030 のサポートが必要な場合、この確認は適用されません。 GB18030 サポートの有効化の詳細については、「[International support](/sccm/core/plan-design/hierarchy/international-support)」(インターナショナル サポート) を参照してください。

#### <a name="setup-source-folder"></a>セットアップ ソース フォルダー 
*適用対象:セカンダリ サイト*

セカンダリ サイトのコンピューター アカウントに、セットアップ ソース フォルダーおよび共有に対する次のアクセス許可があります。 
- NTFS ファイル システムの**読み取り**アクセス許可
- 共有の**読み取り**アクセス許可 

> [!Note]  
> 管理用共有 (C$ や D$ など) を使用する場合、セカンダリ サイトのコンピューター アカウントはサーバーの**管理者**でなければなりません。  

#### <a name="setup-source-version"></a>セットアップ ソースのバージョン 
*適用対象:セカンダリ サイト*

セカンダリ サイトのインストール用に指定されたソース フォルダーの Configuration Manager バージョンが、プライマリ サイトの Configuration Manager バージョンに一致しています。

#### <a name="site-code-in-use"></a>使用中のサイト コード 
*適用対象:プライマリ サイト* 指定されたサイト コードが Configuration Manager 階層内でまだ使用されていません。 このサイトの一意のサイト コードを指定します。

#### <a name="sms-provider-in-same-domain-as-site-server"></a>サイト サーバーと同じドメイン内の SMS プロバイダー 
*適用対象:SMS プロバイダー*

SMS プロバイダーのすべてのインスタンスが、サイト サーバーと同じドメインにあります。

#### <a name="sql-server-edition"></a>SQL Server のエディション 
*適用対象:サイト データベース サーバー*

サイトの SQL Server が SQL Server Express ではありません。

#### <a name="sql-server-express-on-secondary-site"></a>セカンダリ サイトの SQL Server Express 
*適用対象:セカンダリ サイト*

SQL Server Express をセカンダリ サイト サーバーに正常にインストールできます。

#### <a name="sql-server-on-the-secondary-site-server"></a>セカンダリ サイト サーバー上の SQL Server 
*適用対象:セカンダリ サイト*

SQL Server がセカンダリ サイト サーバーにインストールされています。 セカンダリ サイト用のリモート サイトに、SQL Server をインストールすることはできません。

> [!Warning]  
> この確認は、セットアップで SQL Server の既存のインスタンスを使用するように選択した場合にのみ適用されます。  

#### <a name="sql-server-service-running-account"></a>SQL Server サービスの実行アカウント 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

SQL Server サービスのサインイン アカウントが、ローカル ユーザー アカウントや**ローカル サービス**ではありません。 

有効なドメイン アカウント、**ネットワーク サービス**、または**ローカル システム**を使用するように SQL Server サービスを構成します。

#### <a name="sql-server-tcp-port"></a>SQL Server の TCP ポート 
*適用対象:サイト データベース サーバー*

TCP が SQL Server インスタンスに対して有効になっており、静的ポートを使用するように設定されています。

#### <a name="sql-server-version"></a>SQL Server バージョン 
*適用対象:サイト データベース サーバー*

指定されたサイト データベース サーバーに、サポートされているバージョンの SQL Server がインストールされています。 

詳細については、「[Support for SQL Server versions](/sccm/core/plan-design/configs/support-for-sql-server-versions)」(SQL Server バージョンのサポート) を参照してください。

#### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>展開プライマリ サイトの資産インテリジェンス同期ポイント 
*適用対象:中央管理サイト*

階層にプライマリ サイトを展開する際に、スタンドアロン プライマリ サイトで資産インテリジェンス同期ポイントの役割がインストールされていません。

#### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>展開プライマリ サイトの Endpoint Protection ポイント 
*適用対象:中央管理サイト*

階層にプライマリ サイトを展開する際に、スタンドアロン プライマリ サイトに Endpoint Protection ポイントの役割がインストールされていません。

#### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>展開プライマリ サイトの Microsoft Intune コネクタ 
*適用対象:中央管理サイト*

階層にプライマリ サイトを展開する際に、スタンドアロン プライマリ サイトに Microsoft Intune コネクタの役割がインストールされていません。

#### <a name="usmt-installed"></a>USMT のインストール 
*適用対象:中央管理サイト、プライマリ サイト (スタンドアロンのみ)*

Windows 用 Windows アセスメント & デプロイメント キット (ADK) のユーザー状態移行ツール (USMT) コンポーネントがインストールされています。

#### <a name="validate-fqdn-of-sql-server"></a>SQL Server FQDN の検証 
*適用対象:サイト データベース サーバー*

SQL Server コンピューターの有効な FQDN を指定しています。

#### <a name="verify-central-administration-site-version"></a>中央管理サイトのバージョンの確認 
*適用対象:プライマリ サイト*

中央管理サイトの Configuration Manager のバージョンが同じです。

#### <a name="windows-deployment-tools-installed"></a>インストールされている Windows 展開ツール 
*適用対象:SMS プロバイダー*

Windows ADK の Windows 展開ツール コンポーネントがインストールされています。

#### <a name="windows-failover-cluster"></a>Windows フェールオーバー クラスター 
*適用対象:サイト サーバー、管理ポイント、配布ポイント*

サイト サーバー、管理ポイント、または配布ポイントの役割を持つサーバーが、Windows クラスターの一部ではありません。

バージョン 1810 以降では、Configuration Manager セットアップ プロセスで、フェールオーバー クラスタリング用の Windows の役割でコンピューターにサイト サーバーの役割がインストールされるのがブロックされなくなりました。 SQL Always On では、このロールが必要なため、以前はサイト サーバーにサイト データベースを同時に配置できませんでした。 この変更により、SQL Always On とパッシブ モードのサイト サーバーを使用して、少ないサーバー数で高可用性サイトを作成できます。 詳細については、[高可用性オプション](/sccm/core/servers/deploy/configure/high-availability-options)に関するページを参照してください。 <!--1359132-->  

#### <a name="windows-pe-installed"></a>Windows PE のインストール 
*適用対象:SMS プロバイダー*

Windows ADK の Windows プレインストール環境 (PE) コンポーネントがインストールされています。


### <a name="dependencies-warnings"></a>依存関係:［警告］

#### <a name="administrative-rights-on-distribution-point"></a>配布ポイントの管理者権限 
*適用対象:配布ポイント*

セットアップを実行するユーザー アカウントに、配布ポイントに対する**管理者**権限があります。

#### <a name="administrative-rights-on-management-point"></a>管理ポイントの管理者権限 
*適用対象:管理ポイント、配布ポイント*

サイト サーバーのコンピューター アカウントに、管理ポイントと配布ポイントに対する**管理者**権限があります。

#### <a name="administrative-share-site-system"></a>管理用共有 (サイト システム) 
*適用対象:管理ポイント*

サイト システム コンピューターに必要な管理用共有があります。

#### <a name="application-compatibility"></a>アプリケーションの互換性 
*適用対象:中央管理サイト、プライマリ サイト*

現在のアプリケーションがアプリケーション スキーマに対応しています。

#### <a name="bits-installed"></a>BITS のインストール 
*適用対象:管理ポイント*

IIS でバックグラウンド インテリジェント転送サービス (BITS) がインストールされており、有効になっています。

#### <a name="configuration-for-sql-server-memory-usage"></a>SQL Server のメモリ使用量の構成 
*適用対象:サイト データベース サーバー*

SQL Server がメモリ使用制限なしに構成されています。 SQL Server のメモリに上限を構成します。

#### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>SQL Server のファイアウォールの例外 (スタンドアロン プライマリ サイト) 
*適用対象:プライマリ サイト (スタンドアロンのみ)*

Windows ファイアウォールが無効になっている、または SQL Server に対して適切な Windows ファイアウォールの例外が存在します。 

Sqlservr.exe または必要な TCP ポートへのリモート アクセスを許可します。 既定で、SQL Server では TCP ポート 1433 でリッスンし、Server Service Broker (SSB) では TCP ポート 4022 を使用します。

#### <a name="firewall-exception-for-sql-server-for-management-point"></a>管理ポイントに関する SQL Server 用のファイアウォールの例外 
*適用対象:管理ポイント*

Windows ファイアウォールが無効になっている、または SQL Server に対して適切な Windows ファイアウォールの例外が存在します。

#### <a name="iis-https-configuration"></a>IIS の HTTPS 構成 
*適用対象:管理ポイント、配布ポイント*

IIS Web サイトに HTTPS 通信プロトコル用のバインドがあります。 

HTTPS を必要とするサイトの役割をインストールする場合は、有効な公開キー基盤 (PKI) 証明書を使用して、指定されたサーバーで IIS サイト バインドを構成します。

#### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60) 
*適用対象: 中央管理サイト、プライマリ サイト、セカンダリ サイト、Configuration Manager コンソール、管理ポイント、配布ポイント*

MSXML 6.0 以降のバージョンがインストールされていることを確認します。

#### <a name="powershell-20-on-site-server"></a>サイト サーバーの PowerShell 2.0 
*適用対象:Exchange コネクタを使用するプライマリ サイト*

Configuration Manager Exchange Connector 用のサイト サーバーに、Windows PowerShell 2.0 以降のバージョンがインストールされています。 

#### <a name="remote-connection-to-wmi-on-secondary-site"></a>セカンダリ サイトの WMI へのリモート接続 
*適用対象:セカンダリ サイト*

セットアップで、セカンダリ サイト サーバーの WMI へのリモート接続を確立できます。

#### <a name="sql-server-process-memory-allocation"></a>SQL Server プロセスのメモリの割り当て 
*適用対象:サイト データベース サーバー* 

SQL Server で、中央管理サイトとプライマリ サイト用に少なくとも 8 GB、セカンダリ サイト用に少なくとも 4 GB のメモリが予約されています。

詳細については、「[[SQL Server Management Studio] を利用してメモリ オプションを構成する方法](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-includessmanstudiofullincludesssmanstudiofull-mdmd)」を参照してください。

> [!NOTE]  
> この確認は、セカンダリ サイトの SQL Server Express には適用できません。 このエディションでは、予約メモリが 1 GB に制限されます。  

#### <a name="unsupported-site-system-os-version-for-upgrade"></a>アップグレードでサポートされていないサイト システムの OS バージョン 
*適用対象:プライマリ サイト、セカンダリ サイト*

配布ポイント以外のサイト システムの役割が、Windows Server 2012 以降を実行しているサーバーにインストールされています。

詳細については、「[Configuration Manager サイト システム サーバーでサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)」を参照してください。

> [!NOTE]  
> この確認では、Azure にインストールされているサイト システムの役割や、Microsoft Intune によって使用されるクラウド ストレージ用のサイト システムの役割の状態を解決できません。 これらの役割に対する誤検知としての警告は無視します。

#### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Active Directory に発行するためのサイト サーバーのアクセス許可の確認 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

サイト サーバーのコンピューター アカウントに、Active Directory ドメイン内の **System Management** コンテナーに対する**フル コントロール** アクセス許可があります。 

詳細については、「[サイト発行のために Active Directory を準備する](/sccm/core/plan-design/network/extend-the-active-directory-schema)」を参照してください。

> [!NOTE]  
> アクセス許可を手動で確認する場合、この警告は無視できます。

#### <a name="windows-remote-management-winrm-v11"></a>Windows Remote Management (WinRM) v1.1 
*適用対象:プライマリ サイト、Configuration Manager コンソール*

帯域外管理コンソールを実行するために、プライマリ サイト サーバーまたは Configuration Manager コンソール コンピューターに WinRM 1.1 がインストールされています。 

WinRM 1.1 のダウンロード方法の詳細については、[サポート記事 936059](https://support.microsoft.com/help/936059) を参照してください。

#### <a name="wsus-on-site-server"></a>サイト サーバー上の WSUS 
*適用対象:中央管理サイト、プライマリ サイト*

サポートされているバージョンの Windows Server Update Services (WSUS) がサイト サーバーにインストールされています。 

サイト サーバー以外のサーバーでソフトウェアの更新ポイントを使用する場合は、サイト サーバーに WSUS 管理コンソールをインストールする必要があります。 WSUS の詳細については、「[Windows Server Update Services](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus)」を参照してください。

#### <a name="pending-configuration-item-policy-updates"></a>保留中の構成アイテム ポリシーの更新プログラム 
<!--SCCMDocs-pr issue 2814-->
*適用対象:プライマリ サイト*

バージョン 1806 以降では、バージョン 1706 以降から更新する場合、アプリケーションの展開数が多く、そのうち少なくとも 1 つで承認が必要であると、この警告が表示されることがあります。 

次の 2 つのオプションがあります。  

- 警告を無視して、更新を続行する。 この操作によって、更新中のポリシーを処理する際に、サイト サーバーに高い負荷がかかります。 更新後の管理ポイント上でも、プロセッサの負荷が増える可能性があります。  

- 要件がない、あるいは特定の OS 要件があるアプリケーションのいずれかを変更する。 その時点でのサイト サーバー上の一部の負荷を事前に処理します。 **objreplmgr.log** を確認し、管理ポイント上のプロセッサを監視します。 処理が完了したら、サイトを更新します。 更新後もさらに処理が発生する可能性がありますが、最初のオプションで警告を無視した場合よりは少なくなります。  



##  <a name="BKMK_Requirements"></a> システム要件  

### <a name="system-requirements-errors"></a>システム要件:エラー

#### <a name="server-service-is-running"></a>サーバー サービスが実行されている 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

サーバー サービスが開始され、実行されています。

#### <a name="domain-membership"></a>ドメインのメンバーシップ 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト、SMS プロバイダー、SQL Server*

Configuration Manager コンピューターが Windows ドメインのメンバーです。

#### <a name="free-disk-space-on-site-server"></a>サイト サーバーの空きディスク領域 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

サイト サーバーをインストールするには、少なくとも 15 GB の空きディスク領域が必要です。 同じサーバー上に SMS プロバイダーをインストールする場合は、さらに 1 GB の空き領域が必要です。

#### <a name="pending-system-restart"></a>システムの再起動を保留しています 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト、Configuration Manager コンソール、SMS プロバイダー、SQL Server、管理ポイント、配布ポイント*

セットアップを実行する前に、別のプログラムでサーバーを再起動することが要求されます。

バージョン 1810 以降では、この確認で回復力が高まります。 コンピューターが再起動の保留状態であるかどうかを確かめるために、次のレジストリの場所が確認されます。<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  
- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  
- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  
- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

#### <a name="read-only-domain-controller"></a>読み取り専用のドメイン コントローラー 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

サイト データベース サーバーとセカンダリ サイト サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 

詳細については、Microsoft サポート記事の「[Problems when installing SQL Server on a domain controller](https://support.microsoft.com/help/2032911)」(ドメイン コントローラーに SQL Server をインストールすると問題が発生する) を参照してください。

#### <a name="site-server-fqdn-length"></a>サイト サーバーの FQDN の長さ 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

サイト サーバーの FQDN の長さ。

#### <a name="unsupported-os-for-configuration-manager-console"></a>Configuration Manager コンソールのサポートされていない OS
*適用対象:Configuration Manager コンソール*

サポートされる OS のバージョンを実行するコンピューターに、Configuration Manager コンソールをインストールします。 

詳細については、「[Supported OS versions for the Configuration Manager console](/sccm/core/plan-design/configs/supported-operating-systems-consoles)」 (Configuration Manager コンソールでサポートされる OS バージョン) を参照してください。

#### <a name="unsupported-os-for-site-server"></a>サイト サーバーのサポートされていない OS 
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト、Configuration Manager コンソール、管理ポイント、配布ポイント*

サーバーで、サポートされている OS バージョンが実行されています。 

詳細については、[Configuration Manager サイト システム サーバーでサポートされる OS バージョン](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)に関するページを参照してください。

#### <a name="verify-database-consistency"></a>データベースの整合性の検証 
*適用対象:中央管理サイト、プライマリ サイト*

SQL Server でサイト データベースの整合性を検証します。  


### <a name="system-requirements-warnings"></a>システム要件:［警告］

#### <a name="active-directory-domain-functional-level"></a>Active Directory ドメインの機能レベル 
*適用対象:中央管理サイト、プライマリ サイト*

Active Directory ドメインの機能レベルが、最小要件の Windows Server 2008 R2 になっています。

#### <a name="domain-membership"></a>ドメインのメンバーシップ 
*適用対象:管理ポイント、配布ポイント*

Configuration Manager コンピューターが Windows ドメインのメンバーです。

#### <a name="ntfs-drive-on-site-server"></a>サイト サーバー上の NTFS ドライブ 
*適用対象:プライマリ サイト*

ディスク ドライブが NTFS ファイル システムでフォーマットされています。 セキュリティを強化するには、NTFS ファイル システムでフォーマットされたディスク ドライブにサイト サーバー コンポーネントをインストールします。

#### <a name="schema-extensions"></a>スキーマ拡張 
*適用対象:中央管理サイト、プライマリ サイト*

Active Directory スキーマが拡張されています。 拡張されている場合は、使用されたスキーマ拡張のバージョン。 

Configuration Manager では、サイト サーバーのインストールに Active Directory スキーマ拡張は必要ありません。 Microsoft では、すべての Configuration Manager 機能を十分活用するためにこれをお勧めします。 スキーマ拡張の詳細については、「[サイト発行のために Active Directory を準備する](/sccm/core/plan-design/network/extend-the-active-directory-schema)」を参照してください。

#### <a name="bkmk_changetracking"></a> SQL 変更追跡のクリーンアップ
*適用対象:サイト データベース サーバー*

バージョン 1810 以降では、サイト データベースに SQL 変更追跡データのバックログがあるかどうかを確認します。<!--SCCMDocs-pr issue 3023-->  

サイト データベースで診断ストアド プロシージャを実行することで、この確認を手動で検証します。 最初に、サイト データベースへの[診断接続](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017)を作成します。 最も簡単な方法は、SQL Server Management Studio クエリ エディターを使用して、`admin:<instance name>` に接続することです。 

専用管理者接続クエリ ウィンドウで、次のコマンドを実行します。

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

データベースのサイズやバックログのサイズに応じて、このストアド プロシージャは数分または数時間実行される場合があります。 クエリが完了すると、バックログに関連するデータの 2 つのセクションが表示されます。 最初に、**CT_Days_Old** を確認します。 この値は、syscommittab テーブル内の最も古いエントリの経過期間 (日数) を示しています。 これは、Configuration Manager の既定値である、5 日になっているはずです。 この既定値は変更しないでください。 負荷の大きいデータの処理時またはレプリケーション時に、syscommittab の最も古いエントリが 5 日を超える場合があります。 この値が 7 日を超える場合は、変更追跡データの手動クリーンアップを実行します。  

変更追跡データをクリーンアップするには、専用管理接続で次のコマンドを実行します。 

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

このコマンドでは、syscommittab と関連付けられている側のテーブルのすべてのクリーンアップを開始します。 これは数分または数時間実行される場合があります。 その進行状況を監視するには、**vLogs** ビューのクエリを実行します。 現在の進行状況を表示するには、次のクエリを実行します。 

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

#### <a name="sql-native-client"></a>SQL Native Client
<!--SCCMDocs-pr issue 3094-->
*適用対象:中央管理サイト、プライマリ サイト、セカンダリ サイト*

新しいサイトをインストールするときに、Configuration Manager によって SQL Native Client が再頒布可能コンポーネントとして自動的にインストールされます。 Configuration Manager では、SQL Native Client のアップグレードをサポートしていません。 このチェックでは、サイトに SQL Native Client のサポートされているバージョンがあることを確認します。 バージョン 1810 以降では、最小バージョンは SQL 2012 SP4 (`11.*.7001.0`) です。 

この SQL Native Client のバージョンでは、TLS 1.2 をサポートします。 詳細については、以下の記事を参照してください。
- [Microsoft SQL Server 用の TLS 1.2 のサポート](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  
- [Configuration Manager で TLS 1.2 を有効にする方法](https://support.microsoft.com/help/4040243/how-to-enable-tls-1-2-for-configuration-manager)  
