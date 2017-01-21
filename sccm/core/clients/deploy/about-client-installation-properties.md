---
title: "クライアントのインストール プロパティ | Microsoft Docs"
description: "System Center Configuration Manager のクライアント インストール プロパティについて説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: 15
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: fa6a613bb2b69be923917399da6b45f0c5cfcc6f

---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>System Center Configuration Manager のクライアント インストール プロパティについて

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager CCMSetup.exe コマンドを使用して、企業内のコンピューターに Configuration Manager クライアント ソフトウェアを手動でインストールします。  

##  <a name="a-nameaboutccmsetupa-about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> CCMSetup.exe について  
 CCMSetup.exe コマンドは、指定した管理ポイントまたは指定したソースの場所から、クライアント インストールを完了するために必要なすべてのファイルをダウンロードします。 次のようなファイルが含まれます。  

-   Configuration Manager クライアント ソフトウェアをインストールする Windows インストーラー パッケージ Client.msi。  

-   Microsoft バックグラウンド インテリジェント転送サービス (BITS) インストール ファイル (必要な場合)。  

-   Windows インストーラー インストール ファイル (必要な場合)。  

-   Configuration Manager クライアントの更新プログラムまたは修正プログラム (必要な場合)。  

> [!NOTE]  
>  Configuration Manager では、Client.msi ファイルを直接実行することはできません。  

 CCMSetup.exe には、インストールの動作をカスタマイズするためのコマンド ライン プロパティがいくつか用意されています。 また、CCMSetup.exe コマンド ラインで Client.msi の動作を変更するプロパティを指定することもできます。  

> [!IMPORTANT]  
>  Client.msi のプロパティを指定する前に、必要な CCMSetup のプロパティをすべて指定する必要があります。  

 CCMSetup.exe およびそのサポート ファイルは、Configuration Manager サイト サーバーの Configuration Manager インストール フォルダーの **[クライアント]** フォルダーにあります。 このフォルダーは **&lt;サイト サーバー名\>\SMS_&lt;サイト コード\>\Client** としてネットワークで共有されます。  

 コマンド プロンプトで、CCMSetup.exe コマンドは次の形式を使用します。  

 **CCMSetup.exe [&lt;Ccmsetup のプロパティ\>] [&lt;client.msi のセットアップ プロパティ>]**  

 例:  

 **CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01**  

 この例では、次のアクションを実行します。  

-   配布ポイントの一覧を要求し、クライアント インストール ソース ファイルをダウンロードするために SMSMP01 という名前の管理ポイントを指定します。  

-   Configuration Manager クライアント のバージョンがコンピューターに既に存在している場合に、インストールを停止するように指定します。  

-   クライアントをサイト コード S01 に割り当てるように client.msi で指定します。  

-   SMSFP01 というフォールバック ステータス ポイントを使用するように client.msi で指定します。  

> [!NOTE]  
>  プロパティにスペースを含める場合は、引用符 (" ") で囲みます。  

 次の表にあるプロパティを使って、CCMSetup.exe のインストールの動作を変更することができます。  

> [!IMPORTANT]  
>  Configuration Manager 用に Active Directory スキーマを拡張した場合は、多くのクライアント インストール プロパティが Active Directory Domain Services に発行され、Configuration Manager クライアントによって自動的に読み取られます。 Active Directory ドメイン サービスに発行されるクライアント インストールのプロパティの一覧は、「 [System Center Configuration Manager で Active Directory ドメイン サービスに発行されたクライアント インストールのプロパティについて](about-client-installation-properties-published-to-active-directory-domain-services.md)」を参照してください。  

##  <a name="a-namebkmkccmsetupcommandlinea-ccmsetupexe-command-line-properties"></a><a name="BKMK_CCMSetupCommandLine"></a> CCMSetup.exe のコマンド ライン プロパティ  

### <a name=""></a>/?  

CCMSetup.exe のコマンド ライン プロパティを表示する **[CCMSetup]** のダイアログ ボックスを開きます。  

例: **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;パス\>  

 インストール ファイルのダウンロード元の場所を指定します。 ローカルまたは UNC のインストール パスを使用できます。 ファイルはサーバー メッセージ ブロック (SMB) プロトコルを使用してダウンロードされます。  

> [!NOTE]  
>  コマンド ラインでは、インストール ファイルのダウンロード元になる代替の場所を指定するために、 **/source** プロパティを複数回使用できます。  

> [!IMPORTANT]  
>  **/source** コマンドライン プロパティを使用するには、クライアント インストールに使用する Windows ユーザー アカウントにインストール先に対して読み取りのアクセス許可が必要です。  

 例: **ccmsetup.exe /source:"\\\computer\folder"**  

### <a name="mpltcomputer"></a>/mp:&lt;コンピューター\>

 最も近い配布ポイントからクライアント インストール ファイルをダウンロードできるように、コンピューターが接続するソース管理ポイントを指定します。 配布ポイントがない、またはコンピューターが 4 時間経っても配布ポイントからファイルをダウンロードできない場合は、クライアントは指定された管理ポイントからファイルをダウンロードします。  

 クライアント接続におけるサイト システムの役割の構成によって、コンピューターは HTTP または HTTPS 接続でファイルをダウンロードします。 BITS スロットルが構成されていれば、ダウンロードは BITS スロットルを使用します。 すべての配布ポイントおよび管理ポイントが HTTPS クライアント接続のみと構成されている場合は、クライアント コンピューターに有効な公開キー基盤 (PKI) クライアント証明書があることを確認する必要があります。  

> [!NOTE]  
>  /mp **** コマンドライン プロパティを使用すると、複数の管理ポイントを指定し、コンピューターが接続に失敗しても、次の管理ポイントを試すように構成できます。 複数の管理ポイントは、値をセミコロンで区切って指定します。  

> [!IMPORTANT]  
>  このプロパティは、コンピューターが最も近いソースを見つけてクライアント インストール ファイルのダウンロードするように、最初の管理ポイントを指定するためにのみ使用されます。 インストール後にクライアントが割り当てられる管理ポイントは指定しません。 いかなるサイトのいかなる Configuration Manager 管理ポイントも指定し、クライアント インストール ファイルをダウンロードできる配布ポイントの一覧をコンピューターに送信することができます。  

 コンピューター名を使用する場合の例: **ccmsetup.exe /mp:SMSMP01**  

 FQDN を使用する場合の例: **ccmsetup.exe /mp:smsmp01.contoso.com**  

> [!TIP]  
>  クライアントが HTTPS を使用して管理ポイントに接続する場合、通常はこのオプションでコンピューター名ではなく FQDN を指定する必要があります。 指定する値は、管理ポイントの PKI 証明書のサブジェクトまたはサブジェクトの別名に含まれる必要があります。 Configuration Manager は、イントラネットでの接続の場合、この PKI 証明書でのみコンピューター名をサポートしますが、セキュリティのベスト プラクティスとして、FQDN が推奨されます。  

### <a name="retryltminutes"></a>/retry:&lt;分\>

CCMSetup.exe がインストール ファイルのダウンロードに失敗した場合の再試行間隔を指定します。 既定値は **10** 分です。 CCMSetup は、 **downloadtimeout** インストール プロパティで指定された制限に達するまで再試行し続けます。  

例: **ccmsetup.exe /retry:20**  

### <a name="noservice"></a>/noservice

CCMSetup がサービスとして実行されるのを防ぎます。 CCMSetup がサービスとして実行されると、コンピューターのローカル システム アカウントとの関連で実行されます。ローカル システム アカウントには、インストール プロセスに必要なネットワーク リソースにアクセスする十分な権利がない場合があります。 **/noservice** オプションを指定すると、CCMSetup.exe は、インストール プロセスを開始するために使用するユーザー アカウントの関連で実行されます。 さらに、スクリプトを使用して、 **/service** プロパティで CCMSetup.exe を実行すると、CCMSetup サービスはクライアント インストールを行うため、CCMSetup.exe はサービスが開始されると終了し、インストールの詳細を正しくレポートしないことがあります。 このコマンドラインが指定されていない場合は、既定では、 **/service** が使用されます。  

例: **ccmsetup.exe /noservice**  

### <a name="service"></a>/service

CCMSetup がローカル システム アカウントを使用してサービスとして実行されることを指定します。  

例: **ccmsetup.exe /service**  

### <a name="uninstall"></a>/uninstall

Configuration Manager クライアント ソフトウェアをアンインストールすることを指定します。 詳細については、「 [How to manage clients in System Center Configuration Manager](../manage/manage-clients.md)」をご覧ください。  

例: **ccmsetup.exe /uninstall**  

### <a name="logon"></a>/logon

Configuration Manager または Configuration Manager クライアントのバージョンが既にインストールされている場合にクライアント インストールを停止するように指定します。  

例: **ccmsetup.exe /logon**  

### <a name="forcereboot"></a>/forcereboot

 クライアント インストールを完了するためにクライアント コンピューターの再起動が必要な場合に、CCMSetup でクライアント コンピューターを強制的に再起動することを指定します。 このオプションが指定されていないと、CCMSetup は再起動が必要なときに終了し、次回手動で再起動した後に続行します。  

 例: **CCMSetup.exe /forcereboot**  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;優先順位\>

 クライアント インストール ファイルが HTTP 接続を介してダウンロードされるときのダウンロードの優先順位を指定します。 使用できる値は次のとおりです。  

-   FOREGROUND  

-   HIGH  

-   NORMAL  

-   LOW  

 既定値は NORMAL です。  

 例: **ccmsetup.exe /BITSPriority:HIGH**  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;分\>

CCMSetup がクライアント インストール ファイルのダウンロードの試行を開始してから中止するまでの時間を分単位で指定します。 既定値は **1440** 分 (1 日) です。  

例: **ccmsetup.exe /downloadtimeout:100**  

### <a name="usepkicert"></a>/UsePKICert

 指定されるとクライアントは、利用可能であれば、クライアントの認証を含んだ PKI 証明書を使用します。 有効な証明書が見つからない場合は、クライアントは HTTP 接続と自己署名した証明書の使用にフォールバックします。 このオプションが指定されないと、クライアントは自己署名した証明書を使用し、サイト システムへのすべての通信は HTTP を通じて行われます。  

> [!NOTE]  
>  PKI クライアントの証明書を使用するクライアントをインストールすると、いくつかのシナリオでは、このプロパティを指定する必要がありません。 これらのシナリオには、クライアント プッシュおよびソフトウェアの更新ポイント ベースを使用したクライアントのインストールが含まれます。 しかし、手動でクライアントをインストールするときは、このプロパティを指定し、 **/mp** プロパティを使用して HTTPS クライアント接続のみを許可するように構成された管理ポイントを指定する必要があります。 また、インターネット通信のみのクライアントをインストールする場合も、(インターネットベースの管理ポイントおよびサイト コードと共に) CCMALWAYSINF=1 プロパティを使って、このプロパティを指定する必要があります。 インターネット ベースのクライアント管理の詳細については、「[System Center Configuration Manager でのエンドポイント間の通信](../../plan-design/hierarchy/communications-between-endpoints.md)」の「[インターネットや信頼されていないフォレストからのクライアント通信に関する考慮事項](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)」を参照してください。  

 例: **CCMSetup.exe /UsePKICert**  

### <a name="nocrlcheck"></a>/NoCRLCheck

 PKI 証明書を使用して HTTP で通信するときは、クライアントが証明書の取消一覧 (CRL) を確認しないように指定します。  

 このオプションが指定されないと、クライアントは PKI を使用して HTTPS を確立する前に CRL を確認します。  

 クライアントの CRL チェックの詳細については、「 [Plan for Security 」 の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) 」 の「[Plan for security 」 の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)」を参照してください。  

 例: **CCMSetup.exe /UsePKICert /NoCRLCheck**  

### <a name="configltconfiguration-file"></a>/config:&lt;構成ファイル\>

クライアント インストールのプロパティを含むテキスト ファイルの名前を指定します。 **/noservice** CCMSetup プロパティも指定しない限り、このファイルは CCMSetup フォルダーに置く必要があります。このフォルダーは、32 ビット版と 64 ビット版のいずれのオペレーティング システムでも %Windir%\\Ccmsetup にあります。 **/noservice** プロパティを指定する場合、このファイルは CCMSetup.exe を実行するフォルダーと同じフォルダーに存在する必要があります。  

例: **CCMSetup.exe/config:&lt;構成ファイル名.txt\>**  

サイト サーバー コンピューターの &lt;Configuration Manager ディレクトリ\>\\bin\\&lt;プラットフォーム\> フォルダーにある mobileclienttemplate.tcf ファイルを使用して、正しい形式のファイルを提供します。 このファイルには、セクションに関するコメント フォームの情報と、その使用方法に関する情報が含まれています。 **Install=INSTALL=ALL**というテキストに続く [Client Install] セクションに、クライアント インストールのプロパティを指定します。  

[Client Install] セクション エントリの例: **Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100**  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;ファイル名\>

 Configuration Manager クライアントがインストールされた場合は、指定した前提条件のプログラムを CCMSetup.exe がインストールしないように指定します。  

 例: **CCMSetup.exe /skipprereq:silverlight.exe** または **CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe**  

> [!NOTE]  
>  このプロパティは複数値の入力をサポートします。 個々の値を区切るには、セミコロン文字 (;) を使用します。  

### <a name="forceinstall"></a>/forceinstall

 既存のクライアントがアンインストールされてから、新しいクライアントがインストールされることを指定します。  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;機能\>

Configuration Manager クライアントがインストールされた場合は、指定した機能を CCMSetup.exe がインストールしないように指定します。  

例: **CCMSetup.exe /ExcludeFeatures:ClientUI** は、クライアントにソフトウェア センターをインストールしません。  

> [!NOTE]  
>  このリリースでは、 **ClientUI** が、 **/ExcludeFeatures** プロパティでサポートされる唯一の値です。  

##  <a name="a-nameccmsetupreturncodesa-ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a> CCMSetup.exe のリターン コード  
 CCMSetup.exe コマンドは、コマンドが完了したときに、次のリターン コードを提供します。 コマンド実行の問題を解決するには、クライアント コンピューターで ccmsetup.log ファイルを確認して、リターン コードの問題のコンテキストと詳細を確認します。  

|リターン コード|意味|  
|-----------------|-------------|  
|0|成功|  
|6|エラー|  
|7|再起動が必要です|  
|8|セットアップは既に実行されています|  
|9|前提条件の評価エラー|  
|10|セットアップのマニフェスト ハッシュ検証エラー|  

##  <a name="a-nameclientmsipropsa-clientmsi-properties"></a><a name="clientMsiProps"></a> Client.msi のプロパティ  
 次のプロパティを使って、client.msi のインストールの動作を変更することができます。 クライアント プッシュ インストール方式を使用する場合は、[ **クライアント プッシュ インストールのプロパティ** ] ダイアログ ボックスの [ **クライアント** ] タブでプロパティを指定することもできます。  

### <a name="ccmadmins"></a>CCMADMINS  

クライアント設定およびポリシーへのアクセスを許可する 1 つまたは複数の Windows ユーザー アカウントまたはグループを指定します。 これは、Configuration Manager 管理者に、クライアント コンピューターに対するローカル管理者資格情報がない場合に役立ちます。 セミコロンで区切って、アカウントの一覧を指定できます。  

例: **CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"**  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

クライアント インストール後に、必要に応じてコンピューターを再起動できるように指定します。  

> [!IMPORTANT]  
>  ユーザーがログオンしている場合でもコンピューターは警告なしに再起動します。  

例: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 クライアントが常にインターネットベースであり、イントラネットには接続しないことを指定するには、「1」に設定します。 クライアントの接続の種類に **[常にインターネット]**と表示されます。  

 このプロパティは、インターネットベースの管理ポイントの FQDN を指定する CCMHOSTNAME と共に使用する必要があります。 このプロパティはまた、CCMSetup プロパティ /UsePKICert およびサイト コードと共に使用する必要があります。  

 インターネット ベースのクライアント管理の詳細については、「[System Center Configuration Manager でのエンドポイント間の通信](../../plan-design/hierarchy/communications-between-endpoints.md)」の「[インターネットや信頼されていないフォレストからのクライアント通信に関する考慮事項](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)」を参照してください。  

 例: **CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC**  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Configuration Manager サイトが信頼する、信頼されたルート証明機関の一覧である証明書発行元一覧を指定します。  

 証明書発行者リストと、これをクライアントが証明書選択プロセスで使用する方法の詳細については、「 [Plan for Security 」 の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) 」 の「 [Plan for security 」 の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)」を参照してください。  

 ルート CA 証明書のオブジェクトの属性では、大文字と小文字が区別されます。 属性はコンマ (,) またはセミコロン (;) で区切ることができます。 区切り文字を使用すると、複数のルート CA 証明書を指定することができます。 例:  

 **CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &amp;#124; CN=Litware Corporate Root CA; O=Litware, Inc.”**  

> [!TIP]  
>  サイト サーバー コンピューターの &lt;Configuration Manager ディレクトリ\>\bin\\&lt;プラットフォーム\> フォルダーで mobileclient.tcf ファイルを参照して、サイト用に構成された **CertificateIssuers=&lt;文字列\>** をコピーします。  

### <a name="ccmcertsel"></a>CCMCERTSEL

 クライアントに HTTPS 通信に使用できる複数の証明書 (クライアント認証機能を含む有効な証明書) がある場合の証明書の選択条件を指定します。  

 サブジェクト名またはサブジェクトの別名の完全一致を検索 ( **Subject:**を使用) することも、サブジェクト名またはサブジェクトの別名の部分一致を検索 ( **SubjectStr:**を使用) することもできます。 例:  

 **CCMCERTSEL="Subject:computer1.contoso.com"** と指定すると、サブジェクト名またはサブジェクトの別名でコンピューター名 "computer1.contoso.com" と完全に一致する証明書を検索します。  

 **CCMCERTSEL="SubjectStr:contoso.com"** と指定すると、サブジェクト名またはサブジェクトの別名で "contoso.com" を含む証明書を検索します。  

 サブジェクト名またはサブジェクトの別名の属性でオブジェクト ID (OID) または識別名の属性を使用することもできます。たとえば、次のようになります。  

 **CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"** と指定すると、オブジェクト ID として表わされる組織単位属性および指定したコンピューターを検索します。  

 **CCMCERTSEL="SubjectAttr:OU = Computers"** と指定すると、識別名として表される組織単位属性および指定したコンピューターを検索します。  

> [!IMPORTANT]  
>  [サブジェクト名] ボックスを使用する場合、 **Subject:** 選択条件値の照合プロセスでは大文字と小文字が区別され、 **SubjectStr:** 選択条件値の照合プロセスでは大文字と小文字が区別されません。  
>   
>  [サブジェクトの別名] ボックスを使用する場合、 **Subject:** 選択条件値と **SubjectStr:** 選択条件値の両方の照合プロセスで大文字と小文字が区別されません。  

 証明書の選択に使用できる属性の完全な一覧は、「 [PKI 証明書の選択条件としてサポートされている属性値](#BKMK_attributevalues)」に記載されています。  

 1 つ以上の証明書が検索で一致し、プロパティ CCMFIRSTCERT が「1」に設定されている場合は、有効期限の最も長い証明書が選択されます。  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 HTTPS 通信に使用するクライアント証明書が、コンピューター ストアの既定の **個人** 用証明書ストアにない場合の代替の証明書ストアの名前を指定します。  

 例: **CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"**  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  デバッグ ログを有効にします。 設定できる値は 0 (オフ) または 1 (オン) です。 既定値は 0 です。 この場合、クライアントでは、問題のトラブルシューティングに役立つ低レベルの情報がログ出力されます。 実稼働サイトではこのプロパティを使用しないことをお勧めします。これは、このプロパティを使用すると、過度のログ記録が実行され、ログ ファイル内で適切な情報を見つけることが困難になる可能性があるためです。 デバッグ ログを有効にするには、CCMENABLELOGGING を TRUE に設定する必要があります。  

  例: **CCMSetup.exe CCMDEBUGLOGGING=1**  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  このプロパティを TRUE に設定すると、ログが有効になります。 既定では、ログは有効になります。 ログ ファイルは、Configuration Manager クライアントのインストール フォルダー内の **Logs** フォルダーに保存されます。 既定では、このフォルダーは %Windir%\CCM\Logs にあります。  

  例: **CCMSetup.exe CCMENABLELOGGING=TRUE**  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 クライアントの正常性評価ツール (ccmeval.exe) を実行する頻度を指定します。 **1** ～ **1440** 分の値を指定できます。 このプロパティを指定しなかったり、正しくない値を指定すると、評価は 1 日 1 回実行されます。  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 クライアントの正常性評価ツール (ccmeval.exe) を実行する時刻を指定します。 **0** (午前 0 時) ～ **23** (午後 11 時) の値を指定できます。 このプロパティを指定しなかったり、正しくない値を指定すると、評価は午前 0 時に実行されます。  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 「1」に設定されている場合は、このプロパティはクライアントが最も有効期限の長い PKI  証明書を選択するように指定します。 この設定は、IPsec 実施でネットワーク アクセス保護を使用している場合に必要になることがあります。  

 例: **CCMSetup.exe /UsePKICert CCMFIRSTCERT=1**  

### <a name="ccmhostname"></a>CCMHOSTNAME

 クライアントがインターネット経由で管理される場合の、インターネットベースの管理ポイントの FQDN を指定します。  

 SMSSITECODE=AUTO のインストール プロパティでこのオプションを指定しないでください。 インターネットベースのクライアントはインターネットベースのサイトに直接割り当てる必要があります。  

 例: **CCMSetup.exe  /UsePKICert/ CCMHOSTNAME="SMSMP01.corp.contoso.com"**  

### <a name="ccmhttpport"></a>CCMHTTPPORT

 HTTP を介してサイト システム サーバーと通信するときにクライアントが使用するポートを指定します。  

 このポートを指定しない場合、既定値の 80 が使用されます。  

 例: **CCMSetup.exe CCMHTTPPORT=80**  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

HTTPS を介してサイト システム サーバーと通信するときにクライアントが使用するポートを指定します。 このポートが指定されなかった場合は、既定値の 443 が使用されます。  

例: **CCMSetup.exe /UsePKICert CCMHTTPSPORT=443**  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Configuration Manager クライアント ファイルがインストールされるフォルダーを指定します。 このプロパティを設定しない場合、クライアント ソフトウェアは *%Windir%*\CCM フォルダーにインストールされます。 ファイルのインストール場所に関係なく、Ccmcore.dll ファイルは常に *%Windir%\System32* フォルダーにインストールされます。 加えて、64 ビット オペレーティング システムでは、Configuration Manager ソフトウェア開発キット (SDK) からの Configuration Manager クライアント API の 32 ビット版を使用する 32 ビット アプリケーションをサポートするために、必ず、Ccmcore.dll ファイルのコピーが *%Windir%*\SysWOW64 フォルダーにインストールされます。  

 例: **CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"**  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Configuration Manager ログ ファイルに記録する詳細情報の量を指定します。 0 から 3 までの整数を指定します。0 が最も詳細なログ出力で、3 はエラーのみがログに出力されます。 既定値は 1 です。  

例: **CCMSetup.exe CCMLOGLEVEL=3**  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Configuration Manager ログ ファイルのサイズが 250000 バイト (または CCMLOGMAXSIZE プロパティで指定された値) になると、バックアップとして名前が変更され、新しいログ ファイルが作成されます。  

このプロパティでは、保持する以前のバージョンのログ ファイルの数を指定します。 既定値は 1 です。 このプロパティを 0 に設定すると、ログ ファイルは保持されません。  

例: **CCMSetup.exe CCMLOGMAXHISTORY=0**  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

ログ ファイルの最大サイズをバイト単位で指定します。 ログ ファイルが指定されたサイズに達すると、履歴ファイルとして名前が変更され、新しいファイルが作成されます。 このプロパティは、10000 バイト以上に設定する必要があります。 既定値は 250000 バイトです。  

例: **CCMSetup.exe CCMLOGMAXSIZE=300000**  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 TRUE に設定すると、クライアント コンピューターの管理者資格情報を持つエンドユーザーが、クライアント コンピューターのコントロール パネルで Configuration Manager を使用して、Configuration Manager クライアントの割り当て済みサイトを変更することができなくなります。  

 例: **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

「TRUE」 に設定すると、クライアント コンピューターの管理者資格情報を持つエンドユーザーが、クライアント コンピューターのコントロール パネルで Configuration Manager を使用して、Configuration Manager クライアントのプログラム クライアントのキャッシュ フォルダーの設定を変更することができなくなります。  

例: **CCMSetup.exe DISABLECACHEOPT=TRUE**  

### <a name="dnssuffix"></a>DNSSUFFIX

 クライアント用に、DNS で発行されている管理ポイントを検索する DNS ドメインを指定します。 管理ポイントが特定されると、その管理ポイントは、階層内のその他の管理ポイントについて、クライアントに通知します。 つまり、DNS 発行によって特定される管理ポイントは、クライアントのサイトに存在する必要はなく、階層内のすべての管理ポイントが対象となります。  

> [!NOTE]  
>  このプロパティは、発行された管理ポイントとクライアントが同じドメインにある場合、指定する必要はありません。 この場合、DNS での管理ポイントの検索で、クライアントのドメインが自動的に使用されます。  

 Configuration Manager クライアントに対するサービスの場所の検索方法として DNS 発行を使用することの詳細については、「[クライアントが System Center Configuration Manager のサイト リソースやサービスを検索する方法を理解する](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)」の「[サービスの場所とクライアントが割り当て済み管理ポイントを特定する方法](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)」を参照してください。  

> [!NOTE]  
>  既定では、DNS 発行は Configuration Manager で無効になっています。  

 例: **CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com**  

### <a name="fsp"></a>FSP

Configuration Manager クライアント コンピューターによって送信される状態メッセージを受信して処理するフォールバック ステータス ポイントを指定します。  

フォールバック ステータス ポイントの詳細については、「[System Center Configuration Manager クライアントのサイト システムの役割の決定](plan/determine-the-site-system-roles-for-clients.md)」の「[フォールバック ステータス ポイントが必要かどうかを判断する](plan/determine-the-site-system-roles-for-clients.md#BKMK_Determine_FSP)」を参照してください。  

例: **CCMSetup.exe FSP=SMSFP01**  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 クライアントがインストールされる前は、Microsoft Application Virtualization (App-V) の必要最小バージョンが存在するかどうかを確認しないことを指定します。  

> [!IMPORTANT]  
>  App-V をインストールせずに Configuration Manager クライアントをインストールすると、仮想アプリケーションを展開することはできません。  

 例: **CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE**  

### <a name="notifyonly"></a>NOTIFYONLY

Configuration Manager クライアントで見つかった問題について、クライアントのステータスで報告しますが、修復はしないことを指定します。  

例: **CCMSetup.exe NOTIFYONLY=TRUE**  

詳細については、「 [How to configure client status in System Center Configuration Manager](configure-client-status.md)」をご覧ください。  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Configuration Manager クライアントに間違った Configuration Manager の信頼されたルート キーがあり、信頼された管理ポイントに接続して新しい信頼されたルート キーの有効なコピーを取得できない場合は、このプロパティを使用して古い信頼されたルート キーを手動で削除する必要があります。 この状況は一般的に、クライアントを 1 つのサイト階層から別のサイト階層に移動したときに発生します。 このプロパティは、HTTP および HTTPS クライアント接続を使用するクライアントに適用されます。  

 例: **CCMSetup.exe RESETKEYINFORMATION=TRUE**  

### <a name="sitereassign"></a>SITEREASSIGN

[SMSSITECODE](#smssitecode)=AUTO と共に使用して、クライアント アップグレードの自動サイト再割り当てを有効にします。

例: **CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE**

### <a name="smscachedir"></a>SMSCACHEDIR

一時ファイルを保存するクライアント コンピューターのクライアントキャッシュ フォルダーの場所を指定します。 既定では、 *%Windir \ccmcache*にあります。  

例: **CCMSetup.exe SMSCACHEDIR="C:\Temp"**  

このプロパティを SMSCACHEFLAGS プロパティと共に使用すると、クライアント キャッシュ フォルダーの場所をさらに制御できます。  

例: **CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE** を指定すると、クライアント上の空き容量が最も大きいディスク ドライブにクライアント キャッシュ フォルダーがインストールされます。  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

一時ファイルを保存する Configuration Manager キャッシュ フォルダーを構成します。 SMSCACHEFLAGS プロパティは、単独で、またはセミコロンで区切った組み合わせで使用できます。 このプロパティを指定しない場合、クライアント キャッシュ フォルダーは SMSCACHEDIR プロパティに従ってインストールされ、フォルダーは圧縮されず、SMSCACHESIZE の値は MB 単位のフォルダー サイズとして使用されます。  

クライアント キャッシュ フォルダーのインストールの詳細を指定します。 次のプロパティを指定できます。  

-   PERCENTDISKSPACE: フォルダー サイズを合計ディスク領域に対する割合として指定します。 このプロパティを指定する場合は、SMSCACHESIZE プロパティを使用する割合値として指定する必要もあります。  

-   PERCENTFREEDISKSPACE: フォルダー サイズをディスク空き領域に対する割合として指定します。 このプロパティを指定する場合は、SMSCACHESIZE プロパティを使用する割合値として指定する必要もあります。 たとえば、ディスクに 10 MB の空き領域があり、SMSCACHESIZE を 50 に指定した場合、フォルダー サイズは 5 MB に設定されます。 このプロパティを PERCENTDISKSPACE プロパティと共に使用することはできません。  

-   MAXDRIVE: 利用できる最も大きいディスクにフォルダーをインストールすることを指定します。 この値は、パスが SMSCACHEDIR プロパティと共に指定されている場合は無視されます。  

-   MAXDRIVESPACE: 空き領域が最も大きいディスク ドライブにフォルダーをインストールするように指定します。 この値は、パスが SMSCACHEDIR プロパティと共に指定されている場合は無視されます。  

-   NTFSONLY: NTFS ファイル システムでフォーマットされたディスク ドライブにのみフォルダーをインストールするように指定します。 この値は、パスが SMSCACHEDIR プロパティと共に指定されている場合は無視されます。  

-   COMPRESS: フォルダーを圧縮形式で保持するように指定します。  

-   FAILIFNOSPACE: フォルダーをインストールするための領域が十分にない場合にクライアント ソフトウェアを削除するように指定します。  

> [!NOTE]  
>  このプロパティに複数のプロパティを指定するには、各プロパティをセミコロンで区切ります。  

このプロパティを指定しないと、クライアント キャッシュ フォルダーは SMSCACHEDIR プロパティに従って作成され、圧縮されずに SMSCACHESIZE プロパティで指定されたサイズになります。  

例: **CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS**  

> [!NOTE]  
>  既存のクライアントをアップグレードすると、この設定は無視されます。  

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Configuration Manager バージョン 1606 では、新しいクライアント設定でクライアント キャッシュ フォルダーのサイズを指定できます。 これらのクライアント設定を追加すると、SMSCACHESIZE を使用して、クライアント キャッシュのサイズを指定する client.msi プロパティとして効果的に置き換えられます。 詳細については、「[キャッシュ サイズに関するクライアント設定](about-client-settings.md#client-cache-settings)」を参照してください。  

1602 より前では、PERCENTDISKSPACE プロパティまたは PERCENTFREEDISKSPACE プロパティと共に使用する場合は、SMSCACHESIZE はクライアント キャッシュ フォルダーのサイズをメガバイト (MB) 単位またはパーセント単位で指定します。 このプロパティを設定しない場合は、フォルダーは既定の最大サイズの 5120 MB に設定されます。 指定できる最小値は 1 MB です。  

> [!NOTE]  
>  ダウンロードが必要な新しいパッケージが原因でフォルダーが最大サイズを超えた場合で、フォルダーを消去して十分な領域を空けることができない場合は、パッケージのダウンロードは失敗し、プログラムまたはアプリケーションは実行されません。  

既存のクライアントをアップグレードしたり、クライアントがソフトウェア更新プログラムをダウンロードしたりしたときは、この設定は無視されます。  

例: **CCMSetup.exe SMSCACHESIZE=100**  

> [!NOTE]  
>  クライアントをインストールする場合、SMSCACHESIZE プロパティまたは SMSCACHEFLAGS プロパティを使用して以前よりも小さいキャッシュ サイズを設定することはできません。 小さいサイズを設定しようとすると、値は無視され、キャッシュ サイズには最後の設定値が自動的に設定されます。  
>   
>  たとえば、キャッシュ サイズが既定の 5,120 MB であるクライアントをインストールしてから、キャッシュ サイズが 100 MB のクライアントを再インストールすると、再インストールされるクライアントのキャッシュ フォルダー サイズは 5,120 MB に設定されます。  


### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Configuration Manager インストーラーで構成設定を確認する場所と順序を指定します。 このプロパティは、各文字が特定の構成ソースを定義する 1 つまたは複数の文字で構成される文字列です。 次の例に示すように、R、P、M、および U の文字の値を単独で、または組み合わせて使用します。  

-   R: レジストリで構成設定を確認します。  

   詳しくは、[レジストリ内のクライアント インストール プロパティの保存に関する情報](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision)をご覧ください。  

-   P: コマンド プロンプトで指定したインストール プロパティで構成設定を確認します。  

-   M: 古いクライアントを Configuration Manager クライアント ソフトウェアでアップグレードするときに既存の設定を確認します。  

-   U: インストールしたクライアントを新しいバージョンにアップグレードします (さらに、割り当てられたサイト コードを使用します)。  

 既定では、クライアント インストールでは `PU` が使用され、最初にインストール プロパティ、次に既存の設定がチェックされます。  

 例: **CCMSetup.exe SMSCONFIGSOURCE=RP**  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 クライアントが Windows Internet Name Service (WINS) を使用して HTTP 接続を許可する管理ポイントを検索できるようにするかどうかを指定します。 Active Directory ドメイン サービスまたは DNS に管理ポイントが見つからないとき、クライアントはこの方法を使用します。  

 このプロパティは、クライアントが名前解決に WINS を使用するかどうかからは独立しています。  

 このプロパティでは 2 つの異なるモードを構成できます。  

-   NOWINS: これはこのプロパティでは最も安全な設定であり、クライアントが WINS で管理ポイントを探すのを防ぎます。  この設定を使用する場合は、クライアントには、Active Directory ドメイン サービスといったイントラネット上、または DNS 公開の使用などで管理ポイントを探す代替の方法が用意されている必要があります。  

-   WINSSECURE: このモードでは、HTTP 通信を使用するクライアントは、WIN を使用して管理ポイントを探すことができます。 しかし、クライアントは管理ポイントへ接続する前に信頼されたルート キーを持っている必要があります。 詳細については、「 [Plan for Security 」の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) 」の「 [Plan for security 」の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)」を参照してください。  

 このプロパティを指定しない場合、WINSSECURE の既定値が使用されます。  

 例: **CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS**  

### <a name="smsmp"></a>SMSMP

Configuration Manager クライアントが使用する最初の管理ポイントを指定します。  

> [!IMPORTANT]  
>  管理ポイントが HTTPS でのクライアント接続のみを受け入れる (HTTP クライアント接続を許可しない) 場合、管理ポイント名の先頭に「https://」を付加する必要があります。  

例: **CCMSetup.exe SMSMP=smsmp01.contoso.com**  

例: **CCMSetup.exe SMSMP=smsmp01.contoso.com**  

例: **CCMSetup.exe SMSMP=https://smsmp01.contoso.com**  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Configuration Manager の信頼されたルート キーを Active Directory から取得できない場合は、Configuration Manager の信頼されたルート キーを指定します。 このプロパティは、HTTP および HTTPS クライアント接続を使用するクライアントに適用されます。 詳細については、「 [Plan for Security 」の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) 」の「 [Plan for security 」の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)」を参照してください。  

 例: **CCMSetup.exe SMSPUBLICROOTKEY=&lt;キー\>**  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Configuration Manager の信頼されたルート キーを再インストールするために使用します。 信頼されたルート キーを含むファイルの完全なパスとファイル名を指定します。 このプロパティは、HTTP および HTTPS クライアント接続を使用するクライアントに適用されます。 詳細については、「 [Plan for Security 」の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) 」の「 [Plan for security 」の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)」を参照してください。  

 例: CCMSetup.exe **SMSROOTKEYPATH=&lt;完全なパスとファイル名\>**  

### <a name="smssigncert"></a>SMSSIGNCERT

 サイト サーバーのエクスポートされる自己署名した証明書の完全なパスと .cer ファイル名を指定します。  

 この証明書は、 **SMS** 証明書ストアに保存されています。サブジェクト名は **Site Server** 、フレンドリ名は **Site Server Signing Certificate**です。  

 例: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;完全なパスとファイル名\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Configuration Manager クライアントを割り当てる Configuration Manager サイトを指定します。 3 文字のサイト コードか、または AUTO を指定できます。 AUTO が指定された場合、またはこのプロパティが指定されなかった場合は、クライアントは、Active Directory Domain Services または指定した管理ポイントからの Configuration Manager サイト割り当てを判断しようと試みます。 クライアントのアップグレードに対して AUTO を有効にするには、[SITEREASSIGN](#sitereassign) を TRUE に設定する必要もあります。    

> [!NOTE]  
>  インターネットベースの管理ポイント (CCMHOSTNAME) も指定する場合、AUTO を使用しないでください。 この場合、クライアントをそのサイトに直接割り当てる必要があります。  

 例: **CCMSetup.exe SMSSITECODE=XZY**  

##  <a name="a-namebkmkattributevaluesa-supported-attribute-values-for-the-pki-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a> PKI 証明書の選択条件としてサポートされている属性値  
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



<!--HONumber=Dec16_HO3-->


