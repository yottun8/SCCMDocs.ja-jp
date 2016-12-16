---
title: "セットアップ コマンドライン オプション | System Center Configuration Manager"
description: "この記事の情報を使用して、スクリプトの構成やコマンド ラインからの System Center Configuration Manager のインストールを行います。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7d1f55786a42650395fcb66ee4917434feecb630

---
# <a name="command-line-options-for-setup-for-system-center-configuration-manager"></a>System Center Configuration Manager でのセットアップに使用されるコマンドライン オプション

*適用対象: System Center Configuration Manager (Current Branch)*


 スクリプトを構成するときや、コマンド ラインから System Center Configuration Manager をインストールするときには、次の表にある情報を使用します。  

##  <a name="a-namebkmksetupa-command-line-options-for-setup"></a><a name="bkmk_setup"></a> セットアップに使用されるコマンドライン オプション  
 **/DEINSTALL**  
 サイトをアンインストールします。 サイト サーバーのコンピューターからセットアップを実行する必要があります。  

 **/DONTSTARTSITECOMP**  
 サイトをインストールします。ただし、サイト コンポーネント マネージャー サービスを開始しません。 サイト コンポーネント マネージャー サービスを開始するまで、サイトはアクティブになりません。 サイト コンポーネント マネージャーは、SMS_Executive サービスと、サイトのその他のプロセスをインストールして開始する役割を持ちます。 サイトのインストールが完了した後で、サイト コンポーネント マネージャー サービスを開始すると、SMS_Executive と、サイトの運用に必要なその他のプロセスがインストールされます。  

 **/HIDDEN**  
 セットアップ中にユーザー インターフェイスを非表示にします。 このオプションは、 **/SCRIPT** オプションと共に使用する必要があります。無人インストール用スクリプト ファイルには必要なオプションをすべて指定しなければならず、そうしないとセットアップは失敗します。  

 **/NOUSERINPUT**  
 セットアップ中のユーザーによる入力を無効にしますが、 **セットアップ ウィザード** のインターフェイスは表示します。 このオプションは、 **/SCRIPT** オプションと共に使用する必要があります。無人インストール用スクリプト ファイルには必要なオプションをすべて指定しなければならず、そうしないとセットアップは失敗します。  

 **/RESETSITE**  
 サイトをリセットします。この操作で、サイトのデータベース アカウントとサービス アカウントがリセットされます。 サイト サーバーの **&lt;ConfigMgrInstallationPath\>\BIN\X64** からセットアップを実行する必要があります。 サイトのリセットの詳細については、「[System Center Configuration Manager インフラストラクチャの変更](../../../../core/servers/manage/modify-your-infrastructure.md)」トピックの「[サイト リセットの実行](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset)」セクションを参照してください。  

 **/TESTDBUPGRADE &lt;*InstanceName\DatabaseName*>**  
 サイト データベースのバックアップをテストし、アップグレード可能かどうかを確認します。 サイト データベースのインスタンス名とデータベース名を指定する必要があります。 データベース名だけを指定すると、既定のインスタンス名が使用されます。  

> [!IMPORTANT]  
>  運用サイト データベースでこのコマンド ライン オプションを実行することはできません。 実行するとサイト データベースがアップグレードされ、サイトが機能しなくなる可能性があります。  

 **/UPGRADE**  
 サイトの無人アップグレードを実行します。 /UPGRADE を使用する場合、ハイフン (-) を含めてプロダクト キーも指定する必要があります。 また、事前にダウンロードしたセットアップの前提条件ファイルへのパスも指定する必要があります。  

 例: **setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx &lt;外部コンポーネント ファイルへのパス\>**  

 セットアップの前提条件ファイルの詳細については、このトピックの「  [セットアップ ダウンローダー](#bkmk_SetupDownloader) 」を参照してください。  

 **/SCRIPT &lt;*SetupScriptPath*>**  
 無人インストールを実行します。**/SCRIPT** オプションを使用する場合は、セットアップ初期化ファイルが必要です。 セットアップを無人で実行する方法の詳細については、[コマンド ラインを使用するサイトのインストール](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)に関するページを参照してください。  

 **/SDKINST &lt;*FQDN*>**  
 指定したコンピューターに SMS プロバイダーをインストールします。 SMS プロバイダー コンピューターの FQDN を指定する必要があります。 SMS プロバイダーの詳細については、「[System Center Configuration Manager の SMS プロバイダーの計画](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)」を参照してください。  

 **/SDKDEINST &lt;*FQDN*>**  
 指定したコンピューターの SMS プロバイダーをアンインストールします。 SMS プロバイダー コンピューターの FQDN を指定する必要があります。  

 **/MANAGELANGS &lt;*LanguageScriptPath*>**  
 事前にインストールしたサイトにインストールされている言語を管理します。このオプションを使用するには、サイト サーバーの **&lt;ConfigMgrInstallationPath\>\BIN\X64** からセットアップを実行し、言語設定が含まれている言語スクリプト ファイルの場所を指定する必要があります。 言語セットアップ スクリプト ファイルで設定できる言語オプションの詳細については、このトピックの「 [言語を管理するためのコマンド ライン オプション](#bkmk_Lang) 」を参照してください。  

##  <a name="a-namebkmklanga-command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a> 言語を管理するためのコマンド ライン オプション  
 **Identification**  

-   **キー名:** Action  

    -   **必須:** はい  

    -   **値:** ManageLanguages  

    -   **詳細:** サイトの、サーバー、クライアント、モバイル クライアントの言語サポートを管理します。  

**Options**  

-   **キー名:** AddServerLanguages  

    -   **必須:** いいえ  

    -   **値:** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK、または ZHH  

    -   **詳細:** Configuration Manager コンソール、レポート、および Configuration Manager オブジェクトで使用できるサーバー言語を指定します。 英語は、既定で常に使用できるようになっています。  

-   **キー名:** AddClientLanguages  

    -   **必須:** いいえ  

    -   **値:** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK、または ZHH  

    -   **詳細:** クライアント コンピューターで使用できる言語を指定します。 英語は、既定で常に使用できるようになっています。  

-   **キー名:** DeleteServerLanguages  

    -   **必須:** いいえ  

    -   **値:** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK、または ZHH  

    -   **詳細:** Configuration Manager コンソール、レポートおよび Configuration Manager オブジェクトで使用できないようにする (削除する) 言語を指定します。 英語は、既定で常に使用できるようになっています。削除することはできません。  

-   **キー名:** DeleteClientLanguages  

    -   **必須:** いいえ  

    -   **値:** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK、または ZHH  

    -   **詳細:** クライアント コンピューターで使用できないようにする (削除する) 言語を指定します。 英語は、既定で常に使用できるようになっています。削除することはできません。  

-   **キー名:** MobileDeviceLanguage  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** モバイル デバイス クライアントの言語をインストールするかどうかを指定します。  

-   **キー名:** PrerequisiteComp  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = ダウンロードします。  

         1 = 既にダウンロードされています。  

    -   **詳細:** セットアップの前提条件ファイルが既にダウンロード済みかどうかを指定します。 たとえば、この値を 0 に設定すると、セットアップ時にファイルがダウンロードされます。  

-   **キー名:** PrerequisitePath  

    -   **必須:** はい  

    -   **値:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **詳細:** セットアップの前提条件ファイルのパスを指定します。 このパスは、 **PrerequisiteComp** キーに設定した値に応じて、ダウンロードしたファイルを保存するか、ダウンロード済みのファイルを見つけるために使われます。  

##  <a name="a-namebkmkunattendeda-unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a> 無人セットアップ スクリプト ファイルのキー  
 次のセクションにある表を、無人セットアップ スクリプトを記述するときの参考にしてください。 この表には、スクリプトで指定できるキーとその値、必須かどうかの別、該当するインストールの方法、およびキーの説明が示されています。  

### <a name="unattended-install-for-a-central-administration-site"></a>中央管理サイトの無人インストール  
 ここでは、中央管理サイトを無人インストールするスクリプト ファイルについて説明します。  

**Identification**  

-   **キー名:** Action  

    -   **必須:** はい  

    -   **値:** InstallCAS  

    -   **詳細:** 中央管理サイトをインストールします。  

**Options**  

-   **キー名:** ProductID  

    -   **必須:** はい  

    -   **値:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* または *Eval*  

    -   **詳細:** ダッシュを含め、インストールする Configuration Manager のプロダクト キーを指定します。 Configuration Manager の評価版をインストールするには、「**Eval**」と入力します。  

-   **キー名:** SiteCode  

    -   **必須:** はい  

    -   **値:** &lt;*SiteCode*>  

    -   **詳細:** 階層内のサイトを一意に識別する英数字 3 文字を指定します。  

-   **キー名:** SiteName  

    -   **必須:** はい  

    -   **値:** &lt;*SiteName*>  

    -   **詳細:** このサイトの名前を指定します。  

-   **キー名:** SMSInstallDir  

    -   **必須:** はい  

    -   **値:** *ConfigMgrInstallationPath*  

    -   **詳細:** Configuration Manager のプログラム ファイルのインストール フォルダーを指定します。  

-   **キー名:** SDKServer  

    -   **必須:** はい  

    -   **値:** &lt;*FQDN of SMS Provider*>  

    -   **詳細:** SMS プロバイダーをホストするサーバーの FQDN を指定します。  
        初期インストールが終わった後で、他の SMS プロバイダーを追加して構成することができます。  

-   **キー名:** PrerequisiteComp  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = ダウンロードします。  

         1 = 既にダウンロードされています。  

    -   **詳細:** セットアップの前提条件ファイルが既にダウンロード済みかどうかを指定します。 この値を 0 に設定すると、セットアップ時にファイルがダウンロードされます。  

-   **キー名:** PrerequisitePath  

    -   **必須:** はい  

    -   **値:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **詳細:** セットアップの前提条件ファイルのパスを指定します。 このパスは、PrerequisiteComp キーに設定した値に応じて、ダウンロードしたファイルを保存するか、ダウンロード済みのファイルを見つけるために使われます。  

-   **キー名:** AdminConsole  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** Configuration Manager コンソールをインストールするかどうかを指定します。  

-   **キー名:** JoinCEIP  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = 参加しません。  

         1 = 参加します。  

    -   **詳細:** カスタマー エクスペリエンス向上プログラムに参加するかどうかを指定します。  

-   **キー名:** AddServerLanguages  

    -   **必須:** いいえ  

    -   **値:** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK、または ZHH  

    -   **詳細:** Configuration Manager コンソール、レポート、および Configuration Manager オブジェクトで使用できるサーバー言語を指定します。 英語は、既定で常に使用できるようになっています。  

-   **キー名:** AddClientLanguages  

    -   **必須:** いいえ  

    -   **値:** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK、または ZHH  

    -   **詳細:** クライアント コンピューターで使用できる言語を指定します。 英語は、既定で常に使用できるようになっています。  

-   **キー名:** DeleteServerLanguages  

    -   **必須:** いいえ  

    -   **値:** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK、または ZHH  

    -   **詳細:** インストールした後でサイトを変更します。  
        Configuration Manager コンソール、レポートおよび Configuration Manager オブジェクトで使用できないようにする (削除する) 言語を指定します。 英語は、既定で常に使用できるようになっています。削除することはできません。  

-   **キー名:** DeleteClientLanguages  

    -   **必須:** いいえ  

    -   **値:** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK、または ZHH  

    -   **詳細:** インストールした後でサイトを変更します。  
        クライアント コンピューターで使用できないようにする (削除する) 言語を指定します。 英語は、既定で常に使用できるようになっています。削除することはできません。  

-   **キー名:** MobileDeviceLanguage  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** モバイル デバイス クライアントの言語をインストールするかどうかを指定します。  

**SQLConfigOptions**  

-   **キー名:** SQLServerName  

    -   **必須:** はい  

    -   **値:** *SQLServerName*  

    -   **詳細:** SQL Server を実行しているサーバーの名前、またはクラスター化されたインスタンスの名前を指定します。 ここでサイト データベースがホストされます。  

-   **キー名:** DatabaseName  

    -   **必須:** はい  

    -   **値:** *&lt;SiteDatabaseName\>* または *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **詳細:**  

         中央管理サイト データベースをインストールするために作成または使用する SQL Server データベースの名前を指定します。  

        > [!IMPORTANT]  
        >  既定のインスタンスを使用しない場合は、必ず、インスタンス名とサイト データベース名を指定してください。  

-   **キー名:** SQLSSBPort  

    -   **必須:** いいえ  

    -   **値:** &lt;*SSBPortNumber*>  

    -   **詳細:** SQL Server で使用する SQL Server Service Broker (SSB) ポートを指定します。 通常、TCP ポート 4022 に構成しますが、別のポートもサポートされています。  

-   **キー名:** SQLDataFilePath  

    -   **必須:** いいえ  

    -   **値:** &lt;*データベース .MDB ファイルへのファイル パス*>  

    -   **詳細:** データベース .MDB ファイルを作成する別の場所を指定します。  

-   **キー名:** SQLLogFilePath  

    -   **必須:** いいえ  

    -   **値:** &lt;*データベース .LDF ファイルへのファイル パス*>  

    -   **詳細:** データベース .LDF ファイルを作成する別の場所を指定します。  

**CloudConnectorOptions**  

-   **キー名:** CloudConnector  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** このサイトでサービス接続ポイントをインストールするかどうかを指定します。 サービス接続ポイントは階層の最上位層サイトでのみインストールできるため、子プライマリ サイトの場合はこの値を 0 にする必要があります。  

-   **キー名:** CloudConnectorServer  

    -   **必須:** CloudConnector が 1 の場合に必須  

    -   **値:** &lt;*サービス接続ポイント サーバーの FQDN*>  

    -   **詳細:** サービス接続ポイントのサイト システムの役割をホストするサーバーの FQDN を指定します。  

-   **キー名:** UseProxy  

    -   **必須:** CloudConnector が 1 の場合に必須  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** サービス接続ポイントがプロキシ サーバーを使用するかどうかを指定します。  

-   **キー名:** ProxyName  

    -   **必須:** UseProxy が 1 の場合に必須  

    -   **値:** &lt;*プロキシ サーバーの FQDN*>  

    -   **詳細:** サービス接続ポイントのサイト システムの役割で使用されるプロキシ サーバーの FQDN を指定します。  

-   **キー名:** ProxyPort  

    -   **必須:** UseProxy が 1 の場合に必須  

    -   **値:** &lt;*PortNumber*>  

    -   **詳細:** 使用するポート番号を指定します。  

### <a name="unattended-install-for-a-primary-site"></a>プライマリ サイトの無人インストール  
ここでは、プライマリ サイトを無人インストールするスクリプト ファイルについて説明します。  

ここでは、中央管理サイトを無人インストールするスクリプト ファイルについて説明します。  

**Identification**  

-   **キー名:** Action  

    -   **必須:** はい  

    -   **値:** InstallPrimarySite  

    -   **詳細:** プライマリ サイトをインストールします。  

**Options**  

-   **キー名:** ProductID  

    -   **必須:** はい  

    -   **値:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* または *Eval*  

    -   **詳細:** ダッシュを含め、インストールする Configuration Manager のプロダクト キーを指定します。 Configuration Manager の評価版をインストールするには、「**Eval**」と入力します。  

-   **キー名:** SiteCode  

    -   **必須:** はい  

    -   **値:** &lt;*SiteCode*>  

    -   **詳細:** 階層内のサイトを一意に識別する英数字 3 文字を指定します。  

-   **キー名:** SiteName  

    -   **必須:** はい  

    -   **値:** &lt;*SiteName*>  

    -   **詳細:** このサイトの名前を指定します。  

-   **キー名:** SMSInstallDir  

    -   **必須:** はい  

    -   **値:** *ConfigMgrInstallationPath*  

    -   **詳細:** Configuration Manager のプログラム ファイルのインストール フォルダーを指定します。  

-   **キー名:** SDKServer  

    -   **必須:** はい  

    -   **値:** &lt;*FQDN of SMS Provider*>  

    -   **詳細:** SMS プロバイダーをホストするサーバーの FQDN を指定します。  
        初期インストールが終わった後で、他の SMS プロバイダーを追加して構成することができます。  

-   **キー名:** PrerequisiteComp  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = ダウンロードします。  

         1 = 既にダウンロードされています。  

    -   **詳細:** セットアップの前提条件ファイルが既にダウンロード済みかどうかを指定します。 この値を 0 に設定すると、セットアップ時にファイルがダウンロードされます。  

-   **キー名:** PrerequisitePath  

    -   **必須:** はい  

    -   **値:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **詳細:** セットアップの前提条件ファイルのパスを指定します。 このパスは、 **PrerequisiteComp** キーに設定した値に応じて、ダウンロードしたファイルを保存するか、ダウンロード済みのファイルを見つけるために使われます。  

-   **キー名:** AdminConsole  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** Configuration Manager コンソールをインストールするかどうかを指定します。  

-   **キー名:** JoinCEIP  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = 参加しません。  

         1 = 参加します。  

    -   **詳細:** カスタマー エクスペリエンス向上プログラムに参加するかどうかを指定します。  

-   **キー名:** ManagementPoint  

    -   **必須:** いいえ  

    -   **値:** &lt;*管理ポイントのサイト サーバーの FQDN*>  

    -   **詳細:** 管理ポイントのサイト システムの役割をホストするサーバーの FQDN を指定します。  

-   **キー名:** ManagementPointProtocol  

    -   **必須:** いいえ  

    -   **値:** HTTPS または HTTP  

    -   **詳細:** 管理ポイントに使用するプロトコルを指定します。  

-   **キー名:** DistributionPoint  

    -   **必須:** いいえ  

    -   **値:** &lt;*配布ポイントのサイト サーバーの FQDN*>  

    -   **詳細:** 管理ポイントに使用するプロトコルを指定します。  

-   **キー名:** DistributionPointProtocol  

    -   **必須:** いいえ  

    -   **値:** HTTPS または HTTP  

    -   **詳細:** 配布ポイントに使用するプロトコルを指定します。  

-   **キー名:** RoleCommunicationProtocol  

    -   **必須:** はい  

    -   **値:** EnforceHTTPS または HTTPorHTTPS  

    -   **詳細:** すべてのサイト システムがクライアントからの HTTPS 通信だけを受け入れるようにするか、サイト システムの役割ごとに通信方法を構成するかを指定します。 [ **EnforceHTTPS**] を選択すると、クライアント コンピューターで、クライアント認証用の有効な PKI 証明書が必要になります。  

-   **キー名:** ClientsUsePKICertificate  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = 使用しません。  

         1 = 使用します。  

    -   **詳細:** クライアントがサイト システムの役割と通信するために、クライアント PKI 証明書を使用するかどうかを指定します。  

-   **キー名:** AddServerLanguages  

    -   **必須:** いいえ  

    -   **値:** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK、または ZHH  

    -   **詳細:** Configuration Manager コンソール、レポート、および Configuration Manager オブジェクトで使用できるサーバー言語を指定します。 英語は、既定で常に使用できるようになっています。  

-   **キー名:** AddClientLanguages  

    -   **必須:** いいえ  

    -   **値:** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK、または ZHH  

    -   **詳細:** クライアント コンピューターで使用できる言語を指定します。 英語は、既定で常に使用できるようになっています。  

-   **キー名:** DeleteServerLanguages  

    -   **必須:** いいえ  

    -   **値:** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK、または ZHH  

    -   **詳細:** インストールした後でサイトを変更します。  
        Configuration Manager コンソール、レポートおよび Configuration Manager オブジェクトで使用できないようにする (削除する) 言語を指定します。 英語は、既定で常に使用できるようになっています。削除することはできません。  

-   **キー名:** DeleteClientLanguages  

    -   **必須:** いいえ  

    -   **値:** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK、または ZHH  

    -   **詳細:** インストールした後でサイトを変更します。  
        クライアント コンピューターで使用できないようにする (削除する) 言語を指定します。 英語は、既定で常に使用できるようになっています。削除することはできません。  

-   **キー名:** MobileDeviceLanguage  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** モバイル デバイス クライアントの言語をインストールするかどうかを指定します。  

**SQLConfigOptions**  

-   **キー名:** SQLServerName  

    -   **必須:** はい  

    -   **値:** *SQLServerName*  

    -   **詳細:** SQL Server を実行しているサーバーの名前、またはクラスター化されたインスタンスの名前を指定します。 ここでサイト データベースがホストされます。  

-   **キー名:** DatabaseName  

    -   **必須:** はい  

    -   **値:** *&lt;SiteDatabaseName\>* または *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **詳細:**  

         プライマリ サイト データベースをインストールするために作成または使用する SQL Server データベースの名前を指定します。  

        > [!IMPORTANT]  
        >  既定のインスタンスを使用しない場合は、必ず、インスタンス名とサイト データベース名を指定してください。  

-   **キー名:** SQLSSBPort  

    -   **必須:** いいえ  

    -   **値:** &lt;*SSBPortNumber*>  

    -   **詳細:** SQL Server で使用する SQL Server Service Broker (SSB) ポートを指定します。 通常、TCP ポート 4022 に構成しますが、別のポートもサポートされています。  

-   **キー名:** SQLDataFilePath  

    -   **必須:** いいえ  

    -   **値:** &lt;*データベース .MDB ファイルへのファイル パス*>  

    -   **詳細:** データベース .MDB ファイルを作成する別の場所を指定します。  

-   **キー名:** SQLLogFilePath  

    -   **必須:** いいえ  

    -   **値:** &lt;*データベース .LDF ファイルへのファイル パス*>  

    -   **詳細:** データベース .LDF ファイルを作成する別の場所を指定します。  

**HierarchyExpansionOption**  

-   **キー名:** CCARSiteServer  

    -   **必須:** いいえ  

    -   **値:** &lt;*中央管理サイトの FQDN*>  

    -   **詳細:** プライマリ サイトを Configuration Manager 階層に含めるときに、アタッチする中央管理サイトを指定します。 セットアップ中に、中央管理サイトを指定する必要があります。  

-   **キー名:** CASRetryInterval  

    -   **必須:** いいえ  

    -   **値:** &lt;*間隔*>  

    -   **詳細:** 中央管理サイトとの接続が切断されたときに、接続を再試行する間隔 (分) を指定します。 たとえば、プライマリ サイトと中央管理サイトの接続が切断されると、プライマリ サイトは、このキーで指定された時間だけ待ってから、もう一度接続しようとします。  

-   **キー名:** WaitForCASTimeout  

    -   **必須:** いいえ  

    -   **値:** &lt;*タイムアウト*>  

         0 ～ 100 の値  

    -   **詳細:** プライマリ サイトが中央管理サイトに接続するときのタイムアウトの最大値 (分) を指定します。 たとえば、中央管理サイトに接続できなかった場合、プライマリ サイトは、WaitForCASTimeout で指定された時間が経過するまで、CASRetryInterval の値に従って、中央管理サイトへの接続を再試行します。 0 ～ 100 に指定できます。  

**CloudConnectorOptions**  

-   **キー名:** CloudConnector  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** このサイトでサービス接続ポイントをインストールするかどうかを指定します。 サービス接続ポイントは階層の最上位層サイトでのみインストールできるため、子プライマリ サイトの場合はこの値を 0 にする必要があります。  

-   **キー名:** CloudConnectorServer  

    -   **必須:** CloudConnector が 1 の場合に必須  

    -   **値:** &lt;*サービス接続ポイント サーバーの FQDN*\>  

    -   **詳細:** サービス接続ポイントのサイト システムの役割をホストするサーバーの FQDN を指定します。  

-   **キー名:** UseProxy  

    -   **必須:** CloudConnector が 1 の場合に必須  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** サービス接続ポイントがプロキシ サーバーを使用するかどうかを指定します。  

-   **キー名:** ProxyName  

    -   **必須:** UseProxy が 1 の場合に必須  

    -   **値:** &lt;*プロキシ サーバーの FQDN*>  

    -   **詳細:** サービス接続ポイントのサイト システムの役割で使用されるプロキシ サーバーの FQDN を指定します。  

-   **キー名:** ProxyPort  

    -   **必須:** UseProxy が 1 の場合に必須  

    -   **値:** &lt;*PortNumber*>  

    -   **詳細:** 使用するポート番号を指定します。  

### <a name="unattended-recovery-for-a-central-administration-site"></a>中央管理サイトの無人回復  
 次の情報を、無人セットアップ用スクリプト ファイルを使用して中央管理サイトを回復するときの参考にしてください。  

**Identification**  

-   **キー名:** Action  

    -   **必須:** はい  

    -   **値:** RecoverCCAR  

    -   **詳細:** 中央管理サイトを回復します。  

**RecoveryOptions**  

-   **キー名:** ServerRecoveryOptions  

    -   **必須:** はい  

    -   **値** : 1、2、または 4  

         1 = サイト サーバーと SQL Server を回復します。  

         2 = サイト サーバーだけを回復します。  

         4 = SQL Server だけを回復します。  

    -   **詳細:** セットアップでサイト サーバーと SQL Server のどちらか、または両方を回復することを指定します。 ServerRecoveryOptions の設定値によって、関連するキーの設定が異なります。  

        -   値 = 1: **SiteServerBackupLocation** キーに値を指定して、サイトのバックアップを使ってサイトを回復することができます。 値を指定しなかった場合は、バックアップを使わずにサイトが再インストールされます。  

        -   値 = 2: **SiteServerBackupLocation** キーに値を指定して、サイトのバックアップを使ってサイトを回復することができます。 値を指定しなかった場合は、バックアップを使わずにサイトが再インストールされます。  

        -   値 = 4: **DatabaseRecoveryOptions** キーに値 **10** を設定して、バックアップからサイト データベースが復元されるようにした場合は、 **BackupLocation** キーは必須です。  

-   **キー名:** DatabaseRecoveryOptions  

    -   **必須:** このキーは、ServerRecoveryOptions の値を **1** または **4** に設定したときに必要です。  

    -   **値:** 10、20、40、80  

         10 = バックアップからサイト データベースを復元します。  

         20 = 別の方法を使って手動で回復されたサイト データベースを使用します。  

         40 = サイトの新しいデータベースを作成します。 サイト データベースのバックアップがない場合に、このオプションを使用してください。 グローバル データとサイト データは、別のサイトをレプリケートすることによって回復します。  

         80 = データベースの回復をスキップします。  

    -   **詳細:** SQL Server のサイト データベースをセットアップでどのように回復するかを指定します。  

-   **キー名:** ReferenceSite  

    -   **必須:** このキーは、**DatabaseRecoveryOptions** の値を **40** に設定したときに必須です。  

    -   **値:** &lt;*ReferenceSiteFQDN*>  

    -   **詳細:** データベースのバックアップが変更の追跡の保有期間より前に作成されているか、バックアップなしでサイトを回復する場合に、中央管理サイトでグローバル データを回復するために使用する基準プライマリ サイトを指定します。  

         バックアップが変更の追跡の保有期間より前に作成されており、基準サイトを指定しなかった場合は、すべてのプライマリ サイトが、中央管理サイトから復元されたデータで再初期化されます。  

         バックアップが変更の追跡の保有期間内に作成されており、基準サイトを指定しなかった場合は、バックアップ作成以後に加えられた変更だけが、プライマリ サイトからレプリケートされます。 プライマリ サイト同士の変更内容が競合している場合は、中央管理サイトで、最初に受け取った変更内容が採用されます。  

-   **キー名:** SiteServerBackupLocation  

    -   **必須:** いいえ  

    -   **値:** &lt;*PathToSiteServerBackupSet*>  

    -   **詳細:** サイト サーバーのバックアップ セットへのパスを指定します。 このキーは、 **ServerRecoveryOptions** キーを **1** か **2**に設定したときにオプションで指定するキーです。 サイトのバックアップを使ってサイトを回復したい場合に、 **SiteServerBackupLocation** キーでバックアップの場所を指定します。 値を指定しなかった場合は、バックアップを使わずにサイトが再インストールされます。  

-   **キー名:** BackupLocation  

    -   **必須:** このキーは、**ServerRecoveryOptions** キーの値を **1** か **4** に設定し、**DatabaseRecoveryOptions** キーの値を **10** に設定したときに必須です。  

    -   **値:** &lt;*PathToSiteDatabaseBackupSet*>  

    -   **詳細:** サイト データベースのバックアップ セットへのパスを指定します。  

**Options**  

-   **キー名:** ProductID  

    -   **必須:** はい  

    -   **値:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* または *Eval*  

    -   **詳細:** ダッシュを含め、インストールする Configuration Manager のプロダクト キーを指定します。 Configuration Manager の評価版をインストールするには、「**Eval**」と入力します。  

-   **キー名:** SiteCode  

    -   **必須:** はい  

    -   **値:** &lt;*SiteCode*>  

    -   **詳細:** 階層内のサイトを一意に識別する英数字 3 文字を指定します。 障害が発生する前にサイトで使用していたサイト コードを指定する必要があります。 サイト コードの制限について詳しくは、このトピックの「 [サイト名とサイト コードについて](#bkmk_codes) 」セクションをご覧ください。  

-   **キー名:** SiteName  

    -   **必須:** いいえ  

    -   **値:** &lt;*SiteName*>  

    -   **詳細:** このサイトの名前を指定します。  

-   **キー名:** SMSInstallDir  

    -   **必須:** はい  

    -   **値:** &lt;*ConfigMgrInstallationPath*>  

    -   **詳細:** Configuration Manager のプログラム ファイルのインストール フォルダーを指定します。  

-   **キー名:** SDKServer  

    -   **必須:** はい  

    -   **値:** &lt;*FQDN of SMS Provider*>  

    -   **詳細:** SMS プロバイダーをホストするサーバーの FQDN を指定します。 障害が発生する前に SMS プロバイダーをホストしていたサーバーを指定する必要があります。  

         初期インストールが終わった後で、他の SMS プロバイダーを追加して構成することができます。 SMS プロバイダーの詳細については、「[System Center Configuration Manager の SMS プロバイダーの計画](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)」を参照してください。  

-   **キー名:** PrerequisiteComp  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = ダウンロードします。  

         1 = 既にダウンロードされています。  

    -   **詳細:** セットアップの前提条件ファイルが既にダウンロード済みかどうかを指定します。 たとえば、この値を **0**に設定すると、セットアップ時にファイルがダウンロードされます。  

-   **キー名:** PrerequisitePath  

    -   **必須:** はい  

    -   **値:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **詳細:** セットアップの前提条件ファイルのパスを指定します。 このパスは、 **PrerequisiteComp** キーに設定した値に応じて、ダウンロードしたファイルを保存するか、ダウンロード済みのファイルを見つけるために使われます。  

-   **キー名:** AdminConsole  

    -   **必須:** このキーは、**ServerRecoveryOptions** の値を **4** 以外に設定した場合に必須です。  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** Configuration Manager コンソールをインストールするかどうかを指定します。  

-   **キー名:** JoinCEIP  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = 参加しません。  

         1 = 参加します。  

    -   **詳細:** カスタマー エクスペリエンス向上プログラムに参加するかどうかを指定します。  

**SQLConfigOptions**  

-   **キー名:** SQLServerName  

    -   **必須:** はい  

    -   **値:** *SQLServerName*  

    -   **詳細:** サイト データベースをホストする SQL Server を実行しているサーバーの名前、またはクラスター化されたインスタンスの名前を指定します。 障害が発生する前にサイト データベースをホストしていたサーバーを指定する必要があります。  

-   **キー名:** DatabaseName  

    -   **必須:** はい  

    -   **値:** *&lt;SiteDatabaseName\>* または *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **詳細:**  

         中央管理サイト データベースをインストールするために作成または使用する SQL Server データベースの名前を指定します。 障害が発生する前に使用していたデータベース名と同じ名前を指定する必要があります。  

        > [!IMPORTANT]  
        >  既定のインスタンスを使用しない場合は、必ず、インスタンス名とサイト データベース名を指定してください。  

-   **キー名:** SQLSSBPort  

    -   **必須:** はい  

    -   **値:** &lt;*SSBPortNumber*>  

    -   **詳細:** SQL Server で使用する SQL Server Service Broker (SSB) ポートを指定します。 通常は、TCP ポート 4022 を使用するように SSB を構成します。 障害が発生する前に使用していた SSB ポート番号と同じ番号を指定する必要があります。  

-   **キー名:** SQLDataFilePath  

    -   **必須:** いいえ  

    -   **値:** &lt;*データベース .MDB ファイルへのファイル パス*>  

    -   **詳細:** データベース .MDB ファイルを作成する別の場所を指定します。  

-   **キー名:** SQLLogFilePath  

    -   **必須:** いいえ  

    -   **値:** &lt;*データベース .LDF ファイルへのファイル パス*>  

    -   **詳細:** データベース .LDF ファイルを作成する別の場所を指定します。  

**CloudConnectorOptions**  

-   **キー名:** CloudConnector  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** このサイトでサービス接続ポイントをインストールするかどうかを指定します。 サービス接続ポイントは階層の最上位層サイトでのみインストールできるため、子プライマリ サイトの場合はこの値を 0 にする必要があります。  

-   **キー名:** CloudConnecorServer  

    -   **必須:** CloudConnector が 1 の場合に必須  

    -   **値:** &lt;*サービス接続ポイント サーバーの FQDN*>  

    -   **詳細:** サービス接続ポイントのサイト システムの役割をホストするサーバーの FQDN を指定します。  

-   **キー名:** UseProxy  

    -   **必須:** CloudConnector が 1 の場合に必須  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** サービス接続ポイントがプロキシ サーバーを使用するかどうかを指定します。  

-   **キー名:** ProxyName  

    -   **必須:** CloudConnector が 1 の場合に必須  

    -   **値:** &lt;*プロキシ サーバーの FQDN*>  

    -   **詳細:** サービス接続ポイントのサイト システムの役割で使用されるプロキシ サーバーの FQDN を指定します。  

-   **キー名:** ProxyPort  

    -   **必須:** CloudConnector が 1 の場合に必須  

    -   **値:** &lt;*PortNumber*>  

    -   **詳細:** 使用するポート番号を指定します。  

### <a name="unattended-recovery-for-a-primary-site"></a>プライマリ サイトの無人回復  
 次の情報を、無人セットアップ用スクリプト ファイルを使ってプライマリ サイトを回復するときの参考にしてください。  

**Identification**  

-   **キー名:** Action  

    -   **必須:** はい  

    -   **値:** RecoverPrimarySite  

    -   **詳細:** プライマリ サイトを回復します。  

**RecoveryOptions**  

-   **キー名:** ServerRecoveryOptions  

    -   **必須:** はい  

    -   **値** : 1、2、または 4  

         1 = サイト サーバーと SQL Server を回復します。  

         2 = サイト サーバーだけを回復します。  

         4 = SQL Server だけを回復します。  

    -   **詳細:** セットアップでサイト サーバーと SQL Server のどちらか、または両方を回復することを指定します。 ServerRecoveryOptions の設定値によって、関連するキーの設定が異なります。  

        -   値 = 1: **SiteServerBackupLocation** キーに値を指定して、サイトのバックアップを使ってサイトを回復することができます。 値を指定しなかった場合は、バックアップを使わずにサイトが再インストールされます。  

        -   値 = 2: **SiteServerBackupLocation** キーに値を指定して、サイトのバックアップを使ってサイトを回復することができます。 値を指定しなかった場合は、バックアップを使わずにサイトが再インストールされます。  

        -   値 = 4: **DatabaseRecoveryOptions** キーに値 **10** を設定して、バックアップからサイト データベースが復元されるようにした場合は、 **BackupLocation** キーは必須です。  

-   **キー名:** DatabaseRecoveryOptions  

    -   **必須:** このキーは、ServerRecoveryOptions の値を **1** または **4** に設定したときに必要です。  

    -   **値:** 10、20、40、80  

         10 = バックアップからサイト データベースを復元します。  

         20 = 別の方法を使って手動で回復されたサイト データベースを使用します。  

         40 = サイトの新しいデータベースを作成します。 サイト データベースのバックアップがない場合に、このオプションを使用してください。 グローバル データとサイト データは、別のサイトをレプリケートすることによって回復します。  

         80 = データベースの回復をスキップします。  

    -   **詳細:** SQL Server のサイト データベースをセットアップでどのように回復するかを指定します。  

-   **キー名:** SiteServerBackupLocation  

    -   **必須:** いいえ  

    -   **値:** &lt;*PathToSiteServerBackupSet*>  

    -   **詳細:**  

         サイト サーバーのバックアップ セットがある場所を指定します。 このキーは、 **ServerRecoveryOptions** 設定の値が **1** か **2**である場合にオプションです。 サイトのバックアップを使ってサイトを回復したい場合に、 **SiteServerBackupLocation** キーでバックアップの場所を指定します。 値を指定しなかった場合は、バックアップを使わずにサイトが再インストールされます。  

-   **キー名:** BackupLocation  

    -   **必須:** このキーは、**ServerRecoveryOptions** キーの値を **1** か **4** に設定し、**DatabaseRecoveryOptions** キーの値を **10** に設定したときに必須です。  

    -   **値:** &lt;*PathToSiteDatabaseBackupSet*>  

    -   **詳細:** サイト データベースのバックアップ セットへのパスを指定します。  

**Options**  

-   **キー名:** ProductID  

    -   **必須:** はい  

    -   **値:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* または *Eval*  

    -   **詳細:** ダッシュを含め、インストールする Configuration Manager のプロダクト キーを指定します。 Configuration Manager の評価版をインストールするには、「**Eval**」と入力します。  

-   **キー名:** SiteCode  

    -   **必須:** はい  

    -   **値:** &lt;*SiteCode*>  

    -   **詳細:** 階層内のサイトを一意に識別する英数字 3 文字を指定します。 障害が発生する前にサイトで使用していたサイト コードを指定する必要があります。 サイト コードの制限について詳しくは、このトピックの「 [サイト名とサイト コードについて](#bkmk_codes) 」セクションをご覧ください。  

-   **キー名:** SiteName  

    -   **必須:** いいえ  

    -   **値:** &lt;*SiteName*>  

    -   **詳細:** このサイトの名前を指定します。  

-   **キー名:** SMSInstallDir  

    -   **必須:** はい  

    -   **値:** &lt;*ConfigMgrInstallationPath*>  

    -   **詳細:** Configuration Manager のプログラム ファイルのインストール フォルダーを指定します。  

-   **キー名:** SDKServer  

    -   **必須:** はい  

    -   **値:** &lt;*FQDN of SMS Provider*>  

    -   **詳細:** SMS プロバイダーをホストするサーバーの FQDN を指定します。 障害が発生する前に SMS プロバイダーをホストしていたサーバーを指定する必要があります。 初期インストールが終わった後で、他の SMS プロバイダーを追加して構成することができます。 SMS プロバイダーの詳細については、「[System Center Configuration Manager の SMS プロバイダーの計画](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)」を参照してください。  

-   **キー名:** PrerequisiteComp  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = ダウンロードします。  

         1 = 既にダウンロードされています。  

    -   **詳細:** セットアップの前提条件ファイルが既にダウンロード済みかどうかを指定します。 たとえば、この値を **0**に設定すると、セットアップ時にファイルがダウンロードされます。  

-   **キー名:** PrerequisitePath  

    -   **必須:** はい  

    -   **値:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **詳細:** セットアップの前提条件ファイルのパスを指定します。 このパスは、 **PrerequisiteComp** キーに設定した値に応じて、ダウンロードしたファイルを保存するか、ダウンロード済みのファイルを見つけるために使われます。  

-   **キー名:** AdminConsole  

    -   **必須:** このキーは、**ServerRecoveryOptions** の値を **4** 以外に設定した場合に必須です。  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** Configuration Manager コンソールをインストールするかどうかを指定します。  

-   **キー名:** JoinCEIP  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = 参加しません。  

         1 = 参加します。  

    -   **詳細:** カスタマー エクスペリエンス向上プログラムに参加するかどうかを指定します。  

**SQLConfigOptions**  

-   **キー名:** SQLServerName  

    -   **必須:** はい  

    -   **値:** *SQLServerName*  

    -   **詳細:** サイト データベースをホストする SQL Server を実行しているサーバーの名前、またはクラスター化されたインスタンスの名前を指定します。 障害が発生する前にサイト データベースをホストしていたサーバーを指定する必要があります。  

-   **キー名:** DatabaseName  

    -   **必須:** はい  

    -   **値:**  &lt;*SiteDatabaseName*\> または                                &lt;*InstanceName*\>\\&lt;*SiteDatabaseName*\>

    -   **詳細:**  

         中央管理サイト データベースをインストールするために作成または使用する SQL Server データベースの名前を指定します。 障害が発生する前に使用していたデータベース名と同じ名前を指定する必要があります。  

        > [!IMPORTANT]  
        >  既定のインスタンスを使用しない場合は、必ず、インスタンス名とサイト データベース名を指定してください。  

-   **キー名:** SQLSSBPort  

    -   **必須:** はい  

    -   **値:** &lt;*SSBPortNumber*>  

    -   **詳細:** SQL Server で使用する SQL Server Service Broker (SSB) ポートを指定します。 通常は、TCP ポート 4022 を使用するように SSB を構成します。 障害が発生する前に使用していた SSB ポート番号と同じ番号を指定する必要があります。  

-   **キー名:** SQLDataFilePath  

    -   **必須:** いいえ  

    -   **値:** &lt;*データベース .MDB ファイルへのファイル パス*>  

    -   **詳細:** データベース .MDB ファイルを作成する別の場所を指定します。  

-   **キー名:** SQLLogFilePath  

    -   **必須:** いいえ  

    -   **値:** &lt;*データベース .LDF ファイルへのファイル パス*>  

    -   **詳細:** データベース .LDF ファイルを作成する別の場所を指定します。  

**HierarchyExpansionOptions**  

-   **キー名:** CCARSiteServer  

    -   **必須:** 詳細を参照してください。  

    -   **値:** &lt;*SiteCodeForCentralAdministrationSite*>  

    -   **詳細:** プライマリ サイトを Configuration Manager 階層に含めるときに、アタッチする中央管理サイトを指定します。 障害が発生する前にプライマリ サイトが中央管理サイトにアタッチされていた場合は、この設定が必要です。 障害が発生する前に中央管理サイトに付いていたサイト コードを指定する必要があります。  

-   **キー名:** CASRetryInterval  

    -   **必須:** いいえ  

    -   **値:** &lt;*間隔*>  

    -   **詳細:** 中央管理サイトとの接続が切断されたときに、接続を再試行する間隔 (分) を指定します。 たとえば、中央管理サイトへの接続が失敗すると、プライマリ サイトは、 **CASRetryInterval**で指定された時間 (分) だけ待機してから、再度接続を試みます。  

-   **キー名:** WaitForCASTimeout  

    -   **必須:** いいえ  

    -   **値:** &lt;*タイムアウト*>  

    -   **詳細:** プライマリ サイトが中央管理サイトに接続するときのタイムアウトの最大値 (分) を指定します。 たとえば、中央管理サイトに接続できなかった場合、プライマリ サイトは、 **WaitForCASTimeout** で指定された時間が経過するまで、 **CASRetryInterval** の値に従って、中央管理サイトへの接続を再試行します。 0 ～ 100 に指定できます。  

**CloudConnectorOptions**  

-   **キー名:** CloudConnector  

    -   **必須:** はい  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** このサイトでサービス接続ポイントをインストールするかどうかを指定します。 サービス接続ポイントは階層の最上位層サイトでのみインストールできるため、子プライマリ サイトの場合はこの値を 0 にする必要があります。  

-   **キー名:** CloudConnecorServer  

    -   **必須:** CloudConnector が 1 の場合に必須  

    -   **値:** &lt;*サービス接続ポイント サーバーの FQDN*>  

    -   **詳細:** サービス接続ポイントのサイト システムの役割をホストするサーバーの FQDN を指定します。  

-   **キー名:** UseProxy  

    -   **必須:** CloudConnector が 1 の場合に必須  

    -   **値:** 0 または 1  

         0 = インストールしません。  

         1 = インストールします。  

    -   **詳細:** サービス接続ポイントがプロキシ サーバーを使用するかどうかを指定します。  

-   **キー名:** ProxyName  

    -   **必須:** CloudConnector が 1 の場合に必須  

    -   **値:** &lt;*プロキシ サーバーの FQDN*>  

    -   **詳細:** サービス接続ポイントのサイト システムの役割で使用されるプロキシ サーバーの FQDN を指定します。  

-   **キー名:** ProxyPort  

    -   **必須:** CloudConnector が 1 の場合に必須  

    -   **値:** &lt;*PortNumber*>  

    -   **詳細:** 使用するポート番号を指定します。  



<!--HONumber=Nov16_HO1-->


