---
title: クライアント インストール パラメーターとプロパティ
titleSuffix: Configuration Manager
description: Configuration Manager クライアントをインストールするための ccmsetup コマンド ライン パラメーターとプロパティについて説明します。
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 61b51fcf9f624f5c2e21a99add1b55f6d6812c84
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421367"
---
# <a name="about-client-installation-parameters-and-properties-in-system-center-configuration-manager"></a>System Center Configuration Manager のクライアント インストール パラメーターとプロパティについて

*適用対象:System Center Configuration Manager (Current Branch)*

CCMSetup.exe コマンドを使用して、Configuration Manager クライアントをインストールします。 コマンド ラインでクライアント インストール パラメーターを指定すると、インストール動作が変更されます。 コマンド ラインでクライアント インストール プロパティを指定すると、インストールされたクライアント エージェントの初期構成が変更されます。



##  <a name="aboutCCMSetup"></a> CCMSetup.exe について  
 CCMSetup.exe コマンドは、クライアントのインストールに必要なファイルを管理ポイントまたはソースの場所からダウンロードします。 次のようなファイルが含まれます。  

-   クライアント ソフトウェアをインストールする Windows インストーラー パッケージ client.msi。  

-   Microsoft バックグラウンド インテリジェント転送サービス (BITS) インストール ファイル。  

-   Windows インストーラー インストール ファイル。  

-   Configuration Manager クライアントの更新プログラムまたは修正プログラム。  

> [!NOTE]  
>  Configuration Manager では、Client.msi ファイルを直接実行することはできません。  

 CCMSetup.exe によって、インストールをカスタマイズするための[コマンド ライン パラメーター](#ccmsetup-exe-command-line-parameters)が提供されます -- パラメーターは先頭に円記号が付き、慣例により小文字で表されます。 コロンの直後に値を置くことで、必要に応じてパラメーターの値を指定できます。 CCMSetup.exe コマンド ラインで client.msi の動作を変更するプロパティを指定することもできます -- 慣例により、プロパティはすべて大文字で表されます。 等号の直後に必要な値を置くことで、プロパティの値を指定します。  

> [!IMPORTANT]  
>  client.msi のプロパティを指定する前に、CCMSetup のパラメーターを指定します。  

 CCMSetup.exe およびサポート ファイルは、サイト サーバーの Configuration Manager インストール フォルダーの **[クライアント]** フォルダーにあります。 このフォルダーは **&lt;サイト サーバー名\>\SMS_&lt;サイト コード\>\Client** としてネットワークで共有されます。  

 コマンド プロンプトで、CCMSetup.exe コマンドは次の形式を使用します。  

 `CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

 次に例を示します。  

   `CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

 この例では次のことが行われます。  

-   配布ポイントの一覧を要求し、クライアント インストール ファイルをダウンロードするために SMSMP01 という名前の管理ポイントを指定します。  

-   クライアントのバージョンが既にコンピューターに存在している場合にインストールを停止するように指定します。  

-   クライアントをサイト コード S01 に割り当てるように client.msi で指定します。  

-   SMSFP01 というフォールバック ステータス ポイントを使用するように client.msi で指定します。  

> [!NOTE]  
>  パラメーターの値がスペースを含む場合は、引用符で囲みます。  


> [!IMPORTANT]  
>  Configuration Manager 用に Active Directory スキーマを拡張した場合、サイトでは多くのクライアント インストール プロパティが Active Directory Domain Services に発行されます。 Configuration Manager クライアントはこれらのプロパティを自動的に読み取ります。 詳細については、「[Active Directory Domain Services に発行されたクライアント インストールのプロパティについて](about-client-installation-properties-published-to-active-directory-domain-services.md)」を参照してください。  



##  <a name="ccmsetupexe-command-line-parameters"></a>CCMSetup.exe のコマンドライン パラメーター  

### <a name=""></a>/?  

ccmsetup.exe のコマンド ライン パラメーターを表示する **[CCMSetup]** ダイアログ ボックスを開きます。  

例: **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;パス\>  

 ファイルのダウンロード場所を指定します。 ローカルまたは UNC パスを使用します。 ファイルはサーバー メッセージ ブロック (SMB) プロトコルを使用してダウンロードされます。 **/source** を使用するには、クライアント インストール用の Windows ユーザー アカウントに、その場所に対する読み取りアクセス許可が必要です。

> [!NOTE]  
>  コマンド ラインで **/source** パラメーターを複数回使用して、ダウンロードの代替場所を指定することができます。  

 例: **ccmsetup.exe /source:"\\\computer\folder"**  

### <a name="mpltserver"></a>/mp:&lt;サーバー\>

 コンピューターの接続先のソース管理ポイントを指定します。 コンピューターではこの管理ポイントを使用して、インストール ファイルの最も近い配布ポイントを見つけます。 配布ポイントがない、またはコンピューターで 4 時間経っても配布ポイントからファイルをダウンロードできない場合、指定された管理ポイントからファイルがダウンロードされます。  

> [!IMPORTANT]  
>  このパラメーターは、ダウンロード ソースを見つけるためのコンピューターの最初の管理ポイントを指定するために使用され、任意のサイト内の任意の管理ポイントを指定できます。 クライアントは管理ポイントに*割り当て* られません。   

 クライアント接続におけるサイト システムの役割の構成によって、コンピューターは HTTP または HTTPS 接続でファイルをダウンロードします。 構成されている場合は、ダウンロードで BITS スロットルが使用されます。 すべての配布ポイントおよび管理ポイントが HTTPS クライアント接続のみに構成されている場合は、クライアント コンピューターに有効なクライアント証明書があることを確認します。  

**/mp** コマンド ライン パラメーターを使用して、複数の管理ポイントを指定できます。 コンピューターで最初の管理ポイントへの接続に失敗した場合は、指定されたリスト内の次の管理ポイントが試行されます。 複数の管理ポイントは、値をセミコロンで区切って指定します。

クライアントが HTTPS を使用して管理ポイントに接続する場合、通常はコンピューター名ではなく FQDN を指定する必要があります。 値は、管理ポイントの PKI 証明書のサブジェクトまたはサブジェクトの別名と一致している必要があります。 Configuration Manager では、イントラネットの接続のために証明書のコンピューター名を使用することがサポートされますが、FQDN を使用することが推奨されます。

コンピューター名を使用する場合の例: `ccmsetup.exe /mp:SMSMP01`  

FQDN を使用する場合の例: `ccmsetup.exe /mp:smsmp01.contoso.com`  

このパラメーターでは、クラウド管理ゲートウェイの URL を指定できます。 この URL を使用して、インターネット ベースのデバイスにクライアントをインストールします。 このパラメーターの値を取得するには、次の手順を使用します。
- クラウド管理ゲートウェイを作成します。
- アクティブなクライアントで、管理者として Windows PowerShell コマンド プロンプトを開きます。 
- `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP` コマンドを実行します。
- **/mp** パラメーターで使用する "https://" プレフィックスを追加します。

クラウド管理ゲートウェイの URL を使用する場合の例: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > **/mp** パラメーターにクラウド管理ゲートウェイの URL を指定する場合は、先頭に **https://** を指定する必要があります。


### <a name="retryltminutes"></a>/retry:&lt;分\>

CCMSetup.exe がインストール ファイルのダウンロードに失敗した場合の再試行間隔です。 CCMSetup は、**downloadtimeout** パラメーターで指定された制限に達するまで再試行し続けます。  

例: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

CCMSetup がサービスとして実行 (既定) されるのを防ぎます。 CCMSetup がサービスとして実行される場合、コンピューターのローカル システム アカウントのコンテキストで実行されます。 このアカウントには、インストールに必要なネットワーク リソースにアクセスするための十分な権限がない可能性があります。 **/noservice** を使用すると、CCMSetup.exe は、インストールを開始するために使用するユーザー アカウントの関連で実行されます。 また、スクリプトを使用して **/service** パラメーターと共に CCMSetup.exe を実行すると、サービスが開始した後に CCMSetup.exe は終了し、インストールの詳細を正しくレポートしない場合があります。   

例: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

CCMSetup がローカル システム アカウントを使用してサービスとして実行されることを指定します。  

例:`ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

クライアント ソフトウェアをアンインストールすることを指定します。 詳細については、「[クライアントを管理する方法](../manage/manage-clients.md)」を参照してください。  

例: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

任意のバージョンのクライアントが既にインストールされている場合は、このパラメーターでクライアント インストールを停止するように指定します。  

例: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 インストールを完了するためにクライアント コンピューターの再起動が必要な場合に、CCMSetup でクライアント コンピューターを強制的に再起動することを指定します。 このパラメーターが指定されていない場合、CCMSetup は再起動が必要なときに終了します。 次回手動で再起動した後に続行します。  

 例: `CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;優先順位\>

 クライアント インストール ファイルが HTTP 接続を介してダウンロードされるときのダウンロードの優先順位を指定します。 使用できる値は次のとおりです。  

- FOREGROUND  

- HIGH  

- NORMAL  

- LOW  

  既定値は NORMAL です。  

  例: `ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;分\>

CCMSetup がインストール ファイルのダウンロードを試行してから停止するまでの時間 (分単位)。 既定値は **1440** 分 (1 日) です。  

例: `ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

指定されるとクライアントは、利用可能であれば、クライアントの認証を含んだ PKI 証明書を使用します。 クライアントで有効な証明書が見つからない場合は、自己署名証明書による HTTP 接続が使用されます。 このパラメーターを使用しない場合でも、この動作は同じです。

> [!NOTE]  
>  一部のシナリオでは、クライアントをインストールし、クライアントの証明書を引き続き使用する場合、このパラメーターを指定する必要はありません。 これらのシナリオには、クライアント プッシュおよびソフトウェアの更新ポイント ベースを使用したクライアントのインストールが含まれます。 しかし、手動でクライアントをインストールするときは、このパラメーターを指定し、**/mp** パラメーターを使用して HTTPS クライアント接続のみを許可するように構成された管理ポイントを指定する必要があります。 インターネットのみの通信用にクライアントをインストールする場合も、このパラメーターを指定する必要があります。 CCMALWAYSINF=1 プロパティを、インターネット ベースの管理ポイント (CCMHOSTNAME) とサイト コード (SMSSITECODE) のプロパティと共に使用します。 インターネット ベースのクライアント管理の詳細については、「[インターネットや信頼されていないフォレストからのクライアント通信に関する考慮事項](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)」を参照してください。  

 例: `CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 PKI 証明書を使用して HTTPS で通信するときは、クライアントが証明書失効リスト (CRL) を確認しないように指定します。  

 指定しない場合、クライアントは HTTPS 接続を確立する前に CRL を確認します。  

 クライアントの CRL チェックの詳細については、「[PKI 証明書失効の計画](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)」を参照してください。  

 例: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;構成ファイル\>

クライアント インストールのプロパティを一覧表示するテキスト ファイルの名前を指定します。

- **/noservice** CCMSetup パラメーターを指定しない場合、このファイルは CCMSetup フォルダーに置く必要があります。このフォルダーは、32 ビット版と 64 ビット版のいずれのオペレーティング システムでも %Windir%\\Ccmsetup にあります。
- **/noservice** パラメーターを指定する場合、このファイルは CCMSetup.exe を実行するフォルダーと同じフォルダーに存在する必要があります。  

例: `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

正しいファイル形式を提供するには、サイト サーバーの &lt;Configuration Manager ディレクトリ\>\\bin\\&lt;プラットフォーム\> フォルダーにある mobileclienttemplate.tcf ファイルを使用します。 このファイルには、セクションに関するコメントと、その使用方法に関する情報も含まれています。 次のテキストに続く [Client Install] セクションに、クライアント インストールのプロパティを指定します。**Install=INSTALL=ALL**。  

[Client Install] セクション エントリの例: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;ファイル名\>

 Configuration Manager クライアントのインストール時に、指定した前提条件のプログラムが CCMSetup.exe でインストールされないように指定します。 このパラメーターでは複数値の入力がサポートされます。 個々の値を区切るには、セミコロン文字 (;) を使用します。  


 例: `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe` または `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`  

### <a name="forceinstall"></a>/forceinstall

 CCMSetup.exe で既存のクライアントをすべてアンインストールし、新しいクライアントをインストールするように指定します。  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;機能\>

CCMSetup.exe でクライアントをインストールするときに、指定した機能をインストールしないように指定します。  

例: `CCMSetup.exe /ExcludeFeatures:ClientUI` は、クライアントにソフトウェア センターをインストールしません。  

> [!NOTE]  
>  **ClientUI** が、**/ExcludeFeatures** パラメーターでサポートされる唯一の値です。  



##  <a name="ccmsetupReturnCodes"></a> CCMSetup.exe のリターン コード  
 CCMSetup.exe コマンドは、完了すると次のリターン コードを提供します。 問題を解決するには、クライアント コンピューターで ccmsetup.log ファイルを確認して、リターン コードのコンテキストと詳細を確認します。  

|リターン コード|意味|  
|-----------------|-------------|  
|0|成功|  
|6|エラー|  
|7|再起動が必要です|  
|8|セットアップは既に実行されています|  
|9|前提条件の評価エラー|  
|10|セットアップのマニフェスト ハッシュ検証エラー|  



## <a name="ccmsetupMsiProps"></a> Ccmsetup.msi プロパティ  
 次のプロパティを使用し、ccmsetup.msi のインストールの動作を変更できます。

### <a name="ccmsetupcmd"></a>CCMSETUPCMD 

ccmsetup.msi によってインストールされた後に ccmsetup.exe に渡されるコマンドライン パラメーターとプロパティを指定します。 他のプロパティは引用符の中に含めます。 Intune MDM インストール方法を使用して Configuration Manager クライアントをブートストラップするときにこのプロパティを使用します。 

例: `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

 > [!Tip]
 > Microsoft Intune では、コマンド ラインが 1024 文字に制限されます。 



##  <a name="clientMsiProps"></a> Client.msi のプロパティ  
 次のプロパティを使って、client.msi のインストールの動作を変更することができます。 クライアント プッシュ インストール方式を使用する場合は、**[クライアント プッシュ インストールのプロパティ]** ダイアログ ボックスの **[クライアント]** タブでプロパティを指定することもできます。  


### <a name="aadclientappid"></a>AADCLIENTAPPID

Azure Active Directory (Azure AD) クライアント アプリの ID を指定します。 クライアント アプリは、クラウド管理用に [Azure サービスを構成する](/sccm/core/servers/deploy/configure/azure-services-wizard)ときに作成またはインポートされます。 Azure 管理者は、Azure Portal からこのプロパティの値を取得することができます。 詳細については、「[アプリケーション ID の取得](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key)」を参照してください。 **AADCLIENTAPPID** プロパティの場合、これが "ネイティブ" アプリケーションの種類の ID となります。

例: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`


### <a name="aadresourceuri"></a>AADRESOURCEURI

Azure AD サーバー アプリの ID を指定します。 サーバー アプリは、クラウド管理用に [Azure サービスを構成する](/sccm/core/servers/deploy/configure/azure-services-wizard)ときに作成またはインポートされます。 [サーバー アプリケーションの作成] ダイアログでサーバー アプリを作成する場合、このプロパティは **[アプリケーション ID/URI]** になります。

Azure 管理者は、Azure Portal からこのプロパティの値を取得することができます。 **Azure Active Directory** ブレードの **[アプリの登録]** で、サーバー アプリを見つけます。 このアプリの種類は "Web アプリ/API" です。 アプリを開き、**[設定]**、**[プロパティ]** の順にクリックします。 この AADRESOURCEURI クライアント インストール プロパティで **[アプリケーション ID/URI]** の値を使用します。

例: `ccmsetup.exe AADRESOURCEURI=https://contososerver`


### <a name="aadtenantid"></a>AADTENANTID

Azure AD テナントの ID を指定します。 このテナントは、クラウド管理用に [Azure サービスを構成する](/sccm/core/servers/deploy/configure/azure-services-wizard)際に Configuration Manager にリンクされます。 このプロパティの値を取得するには、次の手順を使用します。
- 同じ Azure AD テナントに参加している Windows 10 デバイスで、コマンド プロンプトを開きます。
- `dsregcmd.exe /status` コマンドを実行します。
- [デバイスの状態] セクションで、**TenantId** の値を見つけます。 たとえば、`TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a` などです。

  > [!Note]
  > Azure 管理者は、Azure Portal でこの値を取得することもできます。 詳細については、「[テナント ID を取得する](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-tenant-id)」を参照してください。

例: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

クライアント設定およびポリシーへのアクセスを許可する 1 つまたは複数の Windows ユーザー アカウントまたはグループを指定します。 このプロパティは、Configuration Manager 管理者に、クライアント コンピューターに対するローカル管理者資格情報がない場合に役立ちます。 セミコロンで区切って、アカウントの一覧を指定します。  

例: `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

必要に応じて、クライアント インストール後に、コンピューターを再起動できるように指定します。  

> [!IMPORTANT]  
>  ユーザーがログオンしている場合でも、コンピューターは警告なしで再起動します。  

例:**CCMSetup.exe CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 クライアントが常にインターネット ベースであり、イントラネットには接続しないことを指定するには、**1** に設定します。 クライアントの接続の種類に **[常にインターネット]** と表示されます。  

 このプロパティは、インターネット ベースの管理ポイントの FQDN を指定する CCMHOSTNAME と共に使用します。 また、CCMSetup パラメーター /UsePKICert、およびサイト コードと共に使用します。  

 インターネット ベースのクライアント管理の詳細については、「[インターネットや信頼されていないフォレストからのクライアント通信に関する考慮事項](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)」を参照してください。  

 例: `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Configuration Manager サイトが信頼する、信頼されたルート証明機関の一覧である証明書発行元一覧を指定します。  

 証明書発行者リストと、これをクライアントが証明書選択プロセスで使用する方法の詳細については、「[PKI クライアント証明書の選択の計画](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection)」を参照してください。  

 ルート CA 証明書のサブジェクト属性では、この値の大文字と小文字が区別されます。 属性はコンマ (,) またはセミコロン (;) で区切ることができます。 複数のルート CA 証明書は、区分線を使用して指定します。 例:  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  サイトの **CertificateIssuers=&lt;文字列\>** をコピーするには、サイト サーバーの &lt;Configuration Manager ディレクトリ\>\bin\\&lt;プラットフォーム\> フォルダーで mobileclient.tcf ファイルを参照します。  

### <a name="ccmcertsel"></a>CCMCERTSEL

 クライアントに HTTPS 通信用の複数の証明書がある場合の証明書の選択条件を指定します。 この証明書は、クライアント認証機能を含む有効な証明書です。  

 サブジェクト名またはサブジェクトの別名の完全一致を検索 (**Subject:** を使用) することも、部分一致を検索 (**SubjectStr:** を使用) することもできます。 次に例を示します。  

 `CCMCERTSEL="Subject:computer1.contoso.com"` と指定すると、サブジェクト名またはサブジェクトの別名でコンピューター名 "computer1.contoso.com" と完全に一致する証明書を検索します。  

 `CCMCERTSEL="SubjectStr:contoso.com"` と指定すると、サブジェクト名またはサブジェクトの別名で "contoso.com" を含む証明書を検索します。  

 サブジェクト名またはサブジェクトの別名の属性でオブジェクト ID (OID) または識別名の属性を使用することもできます。たとえば、次のようになります。  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` と指定すると、オブジェクト ID として表される組織単位属性および指定したコンピューターを検索します。  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` と指定すると、識別名として表される組織単位属性および指定したコンピューターを検索します。  

> [!IMPORTANT]
>  [サブジェクト名] ボックスを使用する場合、**Subject:** では大文字と小文字が区別され、**SubjectStr:** では区別されません。  
> 
>  [サブジェクトの別名] ボックスを使用する場合、<strong>Subject:</strong> と **SubjectStr:** では大文字と小文字は区別されません。  

 証明書の選択に使用できる属性の完全な一覧は、「[PKI 証明書の選択条件としてサポートされている属性値](#BKMK_attributevalues)」に記載されています。  

 1 つ以上の証明書が検索で一致し、プロパティ CCMFIRSTCERT が「1」に設定されている場合は、有効期限の最も長い証明書が選択されます。  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 HTTPS 用のクライアント証明書が、コンピューター ストアの既定の**個人**用証明書ストアにない場合の代替の証明書ストアの名前を指定します。  

 例: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  デバッグ ログを有効にします。 設定できる値は 0 (オフ、既定) または 1 (オン) です。 このプロパティの場合、クライアントではトラブルシューティングのための低レベルの情報がログ出力されます。 実稼働サイトではこのプロパティを使用しないことをお勧めします。 過度のログ記録が実行され、ログ ファイル内で関連情報を見つけることが困難になる可能性があります。 また、デバッグ ログを有効にするには、CCMENABLELOGGING を TRUE に設定します。  

  例: `CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  既定では、このプロパティはログ記録を有効にするように TRUE に設定されています。 ログ ファイルは、Configuration Manager クライアントのインストール フォルダー内の **Logs** フォルダーに保存されます。 既定では、このフォルダーは %Windir%\CCM\Logs にあります。  

  例: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 クライアントの正常性評価ツール (ccmeval.exe) を実行する頻度です。 **1** ～ **1440** 分で設定できます。 既定では 1 日に 1 回実行されます。  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 クライアントの正常性評価ツール (ccmeval.exe) を実行する時刻です。**0** (午前) ～ **23** (午後 11 時) で指定します。 既定では午前 0 時に実行されます。  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 「1」に設定されている場合は、このプロパティはクライアントが最も有効期限の長い PKI  証明書を選択するように指定します。 この設定は、IPsec 実施でネットワーク アクセス保護を使用している場合に必要になることがあります。  

 例: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  


### <a name="ccmhostname"></a>CCMHOSTNAME

 クライアントがインターネット経由で管理される場合は、このプロパティでインターネット ベースの管理ポイントの FQDN を指定します。  

 SMSSITECODE=AUTO のインストール プロパティでこのオプションを指定しないでください。 インターネット ベースのクライアントはインターネット ベースのサイトに直接割り当てる必要があります。  

 例: `CCMSetup.exe  /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

このプロパティでは、クラウド管理ゲートウェイのアドレスを指定できます。 このプロパティの値を取得するには、次の手順を使用します。
- クラウド管理ゲートウェイを作成します。
- アクティブなクライアントで、管理者として Windows PowerShell コマンド プロンプトを開きます。 
- `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP` コマンドを実行します。
- **CCMHOSTNAME** プロパティで戻り値をそのまま使用します。

例: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > **CCMHOSTNAME** プロパティでクラウド管理ゲートウェイのアドレスを指定する場合は、**https://** などのプレフィックスを追加*しない* でください。 このプレフィックスは、クラウド管理ゲートウェイの **/mp** URL とのみ使用されます。



### <a name="ccmhttpport"></a>CCMHTTPPORT

 HTTP を介してサイト システム サーバーと通信するときにクライアントが使用するポートを指定します。 既定でポート 80 に設定されています。  

 例: `CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

HTTPS を介してサイト システム サーバーと通信するときにクライアントが使用するポートを指定します。 既定でポート 443 に設定されています。  

例: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Configuration Manager クライアント ファイルがインストールされるフォルダーを指定します。既定では *%Windir%* \CCM です。 ファイルのインストール場所に関係なく、Ccmcore.dll ファイルは常に *%Windir%\System32* フォルダーにインストールされます。 また、64 ビット OS では、Ccmcore.dll ファイルのコピーは常に *%Windir%* \SysWOW64 フォルダーにインストールされます。 このファイルでは、Configuration Manager SDK の 32 ビット バージョンのクライアント API を使用する 32 ビット アプリケーションがサポートされます。  

 例: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Configuration Manager ログ ファイルに記録する詳細レベルを指定します。 0 ～ 3 の整数を指定します。0 が最も詳細なログ出力で、3 はエラーのみがログに出力されます。 既定値は 1 です。  

例: `CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Configuration Manager ログ ファイルが最大サイズに達した場合、クライアントはバックアップとしてその名前を変更し、新しいログ ファイルを作成します。 最大サイズは 250,000 バイト (既定値)、または CCMLOGMAXSIZE プロパティで指定された値になります。

このプロパティでは、保持する以前のバージョンのログ ファイルの数を指定します。 既定値は 1 です。 このプロパティを 0 に設定すると、ログ ファイルは保持されません。  

例: `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

ログ ファイルの最大サイズ (バイト単位) です。 ログが指定されたサイズに達した場合、クライアントは履歴ファイルとしてその名前を変更し、新しいファイルを作成します。 このプロパティは、10,000 バイト以上に設定する必要があります。 既定値は 250,000 バイトです。  

例: `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 このプロパティを TRUE に設定すると、管理ユーザーは、**Configuration Manager** コントロール パネルで割り当て済みサイトを変更できなくなります。  

 例:**CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

このプロパティを TRUE に設定すると、管理ユーザーは、**Configuration Manager** コントロール パネルでクライアント キャッシュ フォルダー設定を変更できなくなります。  

例: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 クライアント用に、DNS で発行されている管理ポイントを検索する DNS ドメインを指定します。 管理ポイントが特定されると、その管理ポイントは、階層内のその他の管理ポイントについて、クライアントに通知します。 この動作は、DNS 発行を使用して特定される管理ポイントが、クライアントのサイトに存在する必要はなく、階層内のすべての管理ポイントが対象となることを意味します。  

> [!NOTE]  
>  発行された管理ポイントとクライアントが同じドメインにある場合は、このプロパティを指定する必要はありません。 この場合、DNS での管理ポイントの検索で、クライアントのドメインが自動的に使用されます。  

 Configuration Manager クライアントに対するサービスの場所の検索方法として DNS 発行を使用することの詳細については、「[サービスの場所とクライアントが割り当て済み管理ポイントを特定する方法](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)」を参照してください。  

> [!NOTE]  
>  既定では、DNS 発行は Configuration Manager で有効になっていません。  

 例: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

Configuration Manager クライアント コンピューターによって送信される状態メッセージを受信して処理するフォールバック ステータス ポイントを指定します。  

フォールバック ステータス ポイントの詳細については、「[Determine if you need a fallback status point](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point)」 (フォールバック ステータス ポイントが必要かどうかを確認する) をご覧ください。  

例: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 クライアントがインストールされる前に、Microsoft Application Virtualization (App-V) の必要最小バージョンが存在するかどうかを確認しないことを指定します。  

> [!IMPORTANT]  
>  App-V をインストールせずに Configuration Manager クライアントをインストールすると、仮想アプリケーションを展開することはできません。  

 例: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

クライアントでステータスを報告するが、見つかった問題を修復しないように指定します。  

例: `CCMSetup.exe NOTIFYONLY=TRUE`  

詳細については、「[クライアント ステータスを構成する方法](configure-client-status.md)」を参照してください。  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 クライアントに間違った Configuration Manager の信頼されたルート キーがあり、信頼された管理ポイントに接続して新しい信頼されたルート キーを取得できない場合は、このプロパティを使用して古い信頼されたルート キーを手動で削除します。 この状況は、クライアントを 1 つのサイト階層から別のサイト階層に移動したときに発生する場合があります。 このプロパティは、HTTP および HTTPS クライアント接続を使用するクライアントに適用されます。  

 例: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

[SMSSITECODE](#smssitecode)=AUTO と共に使用して、クライアント アップグレードの自動サイト再割り当てを有効にします。

例: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

一時ファイルを保存するクライアント コンピューターのクライアントキャッシュ フォルダーの場所を指定します。 既定の場所は *%Windir%\ccmcache* です。  

例: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

このプロパティを SMSCACHEFLAGS プロパティと共に使用すると、クライアント キャッシュ フォルダーの場所を制御できます。  

例: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` は、最も空き容量の大きいクライアント ディスク ドライブにクライアント キャッシュ フォルダーをインストールします。  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

クライアント キャッシュ フォルダーのインストールの詳細を指定します。 SMSCACHEFLAGS プロパティは、単独で、またはセミコロンで区切った組み合わせで使用できます。 このプロパティを指定しない場合、クライアント キャッシュ フォルダーは SMSCACHEDIR プロパティに従ってインストールされ、フォルダーは圧縮されず、SMSCACHESIZE の値は MB 単位のフォルダー サイズとして使用されます。  

既存のクライアントをアップグレードすると、この設定は無視されます。  

［プロパティ］:  

-   PERCENTDISKSPACE:フォルダー サイズを合計ディスク領域に対する割合として指定します。 このプロパティを指定する場合は、SMSCACHESIZE プロパティを使用する割合値として指定する必要もあります。  

-   PERCENTFREEDISKSPACE:フォルダー サイズをディスク空き領域に対する割合として指定します。 このプロパティを指定する場合は、SMSCACHESIZE プロパティを使用する割合値として指定する必要もあります。 たとえば、ディスクに 10 MB の空き領域があり、SMSCACHESIZE を 50 に指定した場合、フォルダー サイズは 5 MB に設定されます。 このプロパティを PERCENTDISKSPACE プロパティと共に使用することはできません。  

-   MAXDRIVE:利用可能な最大のディスクにフォルダーをインストールすることを指定します。 この値は、パスが SMSCACHEDIR プロパティと共に指定されている場合は無視されます。  

-   MAXDRIVESPACE:最大の空き領域があるディスク ドライブにフォルダーをインストールするように指定します。 この値は、パスが SMSCACHEDIR プロパティと共に指定されている場合は無視されます。  

-   NTFSONLY:NTFS ディスク ドライブにのみフォルダーをインストールするように指定します。 この値は、パスが SMSCACHEDIR プロパティと共に指定されている場合は無視されます。  

-   COMPRESS:フォルダーを圧縮形式で格納するように指定します。  

-   FAILIFNOSPACE:フォルダーをインストールするための領域が十分にない場合は、クライアント ソフトウェアを削除するように指定します。  

例: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> クライアント設定でクライアント キャッシュ フォルダーのサイズを指定できます。 これらのクライアント設定を追加すると、SMSCACHESIZE を使用して、クライアント キャッシュのサイズを指定する client.msi プロパティとして効果的に置き換えられます。 詳細については、「[キャッシュ サイズに関するクライアント設定](about-client-settings.md#client-cache-settings)」を参照してください。  

<!-- For 1602 and earlier, SMSCACHESIZE specifies the size of the client cache folder in megabyte (MB) or as a percentage when used with the PERCENTDISKSPACE or PERCENTFREEDISKSPACE property. If this property isn't set, the folder defaults to a maximum size of 5120 MB. The lowest value that you can specify is 1 MB.  -->

> [!NOTE]  
>  ダウンロードが必要な新しいパッケージが原因でフォルダーが最大サイズを超えた場合で、フォルダーを消去して十分な領域を空けることができない場合は、パッケージのダウンロードは失敗し、プログラムまたはアプリケーションは実行されません。  

既存のクライアントをアップグレードしたり、クライアントがソフトウェア更新プログラムをダウンロードしたりしたときは、この設定は無視されます。  

例: `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  クライアントを再インストールする場合、SMSCACHESIZE または SMSCACHEFLAGS インストール プロパティを使用して以前よりも小さいキャッシュ サイズを設定することはできません。 この操作を実行しようとすると、値は無視されます。 キャッシュ サイズは、前のサイズに自動的に設定されます。  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Configuration Manager インストーラーで構成設定を確認する場所と順序を指定します。 このプロパティは、各文字が特定の構成ソースを定義する 1 つまたは複数の文字で構成される文字列です。 R、P、M、および U の文字の値を単独で、または組み合わせて使用します。  

- R:レジストリで構成設定を確認します。  

  詳細については、[レジストリ内のクライアント インストール プロパティの格納に関する情報](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision)を参照してください。  

- P:コマンド プロンプトで指定したインストール プロパティで構成設定を確認します。  

- M:古いクライアントを構成マネージャー クライアント ソフトウェアでアップグレードするときに既存の設定を確認します。  

- U:インストールしたクライアントを新しいバージョンにアップグレードします (そして割り当てられたサイト コードを使用します)。  

  既定では、クライアント インストールでは `PU` が使用され、最初にインストール プロパティ、次に既存の設定がチェックされます。  

  例: `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 クライアントが Windows Internet Name Service (WINS) を使用して HTTP 接続を許可する管理ポイントを検索できるようにするかどうかを指定します。 Active Directory Domain Services または DNS に管理ポイントが見つからないときに、クライアントではこの方法を使用します。  

 このプロパティは、クライアントが名前解決に WINS を使用するかどうかに影響しません。  

 このプロパティでは 2 つの異なるモードを構成できます。  

-   NOWINS:この値はこのプロパティでは最も安全な設定であり、クライアントが WINS で管理ポイントを探すのを防ぎます。 この設定を使用する場合は、クライアントには、Active Directory ドメイン サービスといったイントラネット上、または DNS 公開の使用などで管理ポイントを探す代替の方法が用意されている必要があります。  

-   WINSSECURE (既定値):このモードでは、HTTP 接続を使用するクライアントは、WIN を使用して管理ポイントを探せます。 しかし、クライアントは管理ポイントへ接続する前に信頼されたルート キーを持っている必要があります。 詳細については、「[信頼されたルート キーの計画](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)」を参照してください。  


 例: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Configuration Manager クライアントが使用する最初の管理ポイントを指定します。  

> [!IMPORTANT]  
>  管理ポイントが HTTPS でのクライアント接続のみを受け入れる場合、管理ポイント名の先頭に https:// を付加する必要があります。  

例: `CCMSetup.exe SMSMP=smsmp01.contoso.com`

例: `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  


### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Configuration Manager の信頼されたルート キーを Active Directory Domain Services から取得できない場合は、Configuration Manager の信頼されたルート キーを指定します。 このプロパティは、HTTP および HTTPS クライアント接続を使用するクライアントに適用されます。 詳細については、「[信頼されたルート キーの計画](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)」を参照してください。  

 例: `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Configuration Manager の信頼されたルート キーを再インストールするために使用します。 信頼されたルート キーを含むファイルの完全なパスとファイル名を指定します。 このプロパティは、HTTP および HTTPS クライアント接続を使用するクライアントに適用されます。 詳細については、「[信頼されたルート キーの計画](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)」を参照してください。  

 例:'CCMSetup.exe SMSROOTKEYPATH=&lt;完全なパスとファイル名\>`  

### <a name="smssigncert"></a>SMSSIGNCERT

 サイト サーバーのエクスポートされる自己署名した証明書の完全なパスと .cer ファイル名を指定します。  

 この証明書は、 **SMS** 証明書ストアに保存されています。サブジェクト名は **Site Server** 、フレンドリ名は **Site Server Signing Certificate**です。  

 例:**CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;完全なパスとファイル名\>**  

### <a name="smssitecode"></a>SMSSITECODE

 クライアントを割り当てる Configuration Manager サイトを指定します。 この値には、3 文字のサイト コード、または AUTO という単語を指定できます。 AUTO を指定する場合、またはこのプロパティを指定しない場合、クライアントは、Active Directory Domain Services または指定した管理ポイントからのサイト割り当てを判断しようとします。 クライアントのアップグレードに対して AUTO を有効にするには、[SITEREASSIGN](#sitereassign) を TRUE に設定する必要もあります。    

> [!NOTE]  
>  インターネット ベースの管理ポイント (CCMHOSTNAME) も指定する場合は、AUTO を使用しないでください。 この場合、クライアントをそのサイトに直接割り当てる必要があります。  

 例: `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> PKI 証明書の選択条件としてサポートされている属性値  
 Configuration Manager は、PKI 証明書の選択条件として次の属性値をサポートしています。  

|OID 属性|識別名属性|属性の定義|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|ドメイン要素|  
|1.2.840.113549.1.9.1|E または E-mail|電子メール アドレス|  
|2.5.4.3|CN|共通名|  
|2.5.4.4|SN|サブジェクト名|  
|2.5.4.5|SERIALNUMBER|シリアル番号|  
|2.5.4.6|C|国番号|  
|2.5.4.7|L|地域|  
|2.5.4.8|S または ST|州または都道府県|  
|2.5.4.9|STREET|住所|  
|2.5.4.10|O|組織名|  
|2.5.4.11|OU|組織単位|  
|2.5.4.12|T または Title|タイトル|  
|2.5.4.42|G または GN または GivenName|名前|  
|2.5.4.43|I または Initials|イニシャル|  
|2.5.29.17|(値なし)|サブジェクト代替名|  
