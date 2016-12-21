---
title: "サイト管理のセキュリティとプライバシー | System Center Configuration Manager"
description: "System Center Configuration Manager のサイト管理のセキュリティとプライバシーを最適化します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: be8002edb48506286e18b1fb8c09f92f46ff0e10


---
# <a name="security-and-privacy-for-site-administration-in-system-center-configuration-manager"></a>System Center Configuration Manager のサイト管理のセキュリティとプライバシー

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックには、System Center Configuration Manager のサイトと階層のセキュリティとプライバシーの情報が含まれています。

##  <a name="a-namebkmksecuritysitesa-security-best-practices-for-site-administration"></a><a name="BKMK_Security_Sites"></a> サイトを管理するときのセキュリティのベスト プラクティス  
 ここでは、System Center Configuration Manager のサイトと階層をセキュリティで保護するときのベスト プラクティスについて説明します。  

 **信頼されるソースからのみセットアップを実行し、セットアップ メディアとサイト サーバー間の通信チャネルをセキュリティで保護する**  

 ソース ファイルの改ざんを防ぐため、信頼されるソースからセットアップを実行します。 ファイルをネットワーク上に保存している場合は、ネットワークの場所をセキュリティで保護します。  

 ネットワークの場所からセットアップを実行する場合、ファイルがネットワーク経由で転送されるときに攻撃者によって改ざんされるのを防ぐため、セットアップ ファイルのソースの場所とサイト サーバー間で IPsec または SMB 署名を使用します。  

 また、セットアップ ダウンローダーを使用してセットアップに必要なファイルをダウンロードする場合、これらのファイルが保存されている場所がセキュリティで保護されており、セットアップの実行時にこの場所の通信チャネルがセキュリティで保護されることを確認します。  

 **System Center Configuration Manager 向けに Active Directory スキーマを拡張し、Active Directory Domain Services にサイトを発行する**  

 スキーマ拡張は、System Center Configuration Manager の実行に必須ではありませんが、信頼されるソースから Configuration Manager のクライアントとサイト サーバーが情報を取得できるため、より安全な環境が構築されます。  

 クライアントが信頼されていないドメインに属している場合、クライアントのドメインに次のサイト システムの役割を展開します。  

-   管理ポイント  

-   配布ポイント  

-   アプリケーション カタログ Web サイト ポイント  

> [!NOTE]  
>  サイト サーバーのフォレストと双方向のフォレストの信頼関係がない別のフォレストにクライアントが含まれている場合は、これらのクライアントが信頼されていないドメインに属すると見なされるように、Configuration Manager 向けの信頼されたドメインで Kerberos 認証が必要になります。 この目的には、外部の信頼は十分ではありません。  

 **IPsec を使用して、サイト システム サーバーとサイト間の通信をセキュリティで保護する**  

 Configuration Manager はサイト サーバーと SQL Server を実行するコンピューター間の通信をセキュリティで保護しますが、Configuration Manager はサイト システムの役割と SQL Server 間の通信をセキュリティで保護しません。 一部のサイト システム (登録ポイントおよびアプリケーション カタログ Web サービス ポイント) のみ、サイト間の通信を行うように HTTPS 用に構成できます。  

 追加の制御を使用してこれらのサーバー間チャネルを保護しない場合は、攻撃者がサイト システムに対してさまざまなスプーフィング攻撃や中間者攻撃を仕掛けることができてしまいます。 IPsec を使用できない場合は、SMB 署名を使用します。  

> [!NOTE]  
>  サイト サーバーとパッケージ ソース サーバー間の通信チャネルをセキュリティで保護することが、特に重要です。 この通信には SMB が使用されます。 この通信をセキュリティで保護するために IPsec を使用できない場合は、SMB 署名を使用して、クライアントがファイルをダウンロードして実行する前に、それらのファイルが改ざんされないようにしてください。  

 **サイト システムの通信用に Configuration Manager によって作成および管理されたセキュリティ グループを変更しない**  

 セキュリティ グループ:  

-   **SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>**  

-   **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>**  

-   **SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>**  

Configuration Manager は、これらのセキュリティ グループを自動的に作成して管理します。 これには、サイト システムの役割が削除された場合の、コンピューター アカウントの削除も含まれます。  

サービスの継続性を確保し、最小限の権限を付与するため、これらのグループを手動で編集しないでください。  

**クライアントがグローバル カタログ サーバーで Configuration Manager の情報を照会できない場合、信頼されたルート キーのプロビジョニング プロセスを管理する**  

クライアントがグローバル カタログ サーバーで Configuration Manager の情報を照会できない場合、クライアントは、信頼されたルート キーを使用して有効な管理ポイントを認証する必要があります。 信頼されたルート キーは、クライアントのレジストリに保存されており、グローバル ポリシーまたは手動の構成を使用して設定できます。  

クライアントは、初めて管理ポイントと通信する前に信頼されたルート キーのコピーがない場合、最初に通信した管理ポイントを信頼します。 攻撃者がクライアントを承認されていない管理ポイントに誘導するリスクを軽減するため、信頼されたルート キーをクライアントに事前に準備することができます。 詳細については、「 [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)」をご覧ください。  

**既定以外のポート番号を使用する**  

既定以外のポート番号を使用すると、攻撃者が攻撃準備として環境内を探ることが難しくなるため、セキュリティを強化できます。 既定以外のポートを使用する場合は、Configuration Manager をインストールして階層内のすべてのサイトで一貫して使用する前に、これらのポートについて計画します。 クライアント要求ポートと Wake on LAN は、既定以外のポート番号を使用できる場合の例です。  

**サイト システムで役割の分離を使用する**  

サイト システムの役割をすべて 1 台のコンピューターにインストールすることは可能ですが、この方法では単一障害点が発生するため、この方法が実稼働ネットワークで使用されることはあまりありません。  

**攻撃プロファイルを減らす**  

各サイト サーバーの役割を複数のサーバーに分離すると、あるサイト システムの脆弱性に対する攻撃が別のサイト システムで利用される可能性が少なくなります。 多くのサイト システムの役割で、サイト システムにインターネット インフォメーション サービス (IIS) をインストールすることが必要ですが、これにより、攻撃対象が増えることになります。 ハードウェア経費を削減するためにサイト システムの役割を結合する必要がある場合は、IIS のサイト システムの役割を、IIS を必要とする他のサイト システムの役割とのみ結合します。  

> [!IMPORTANT]  
>  フォールバック ステータス ポイントの役割は例外です。このサイト システムの役割は、クライアントから認証されていないデータを受け入れるため、フォールバック ステータス ポイントの役割を他の Configuration Manager サイト システムの役割に割り当てることはできません。  


**Windows Server のセキュリティのベスト プラクティスに従って、すべてのサイト システムでセキュリティ構成ウィザードを実行する**  

セキュリティ構成ウィザード (SCW) を使用して、ネットワーク上の任意のサーバーに適用できるセキュリティ ポリシーを作成できます。 System Center Configuration Manager テンプレートをインストールすると、SCW が Configuration Manager サイト システムの役割、サービス、ポート、およびアプリケーションを認識します。 SCW は、Configuration Manager に必要な通信を許可し、不要な通信をブロックします。  

セキュリティ構成ウィザードは、System Center 2012 Configuration Manager のツールキットに含まれます。ツールキットは Microsoft ダウンロード センターからダウンロードできます。[System Center 2012 – Configuration Manager のコンポーネント アドオンと拡張機能](http://go.microsoft.com/fwlink/p/?LinkId=251931)。  

**サイト システムに静的 IP アドレスを構成する**  

静的 IP アドレスの方が、名前解決攻撃から保護するのが簡単です。  

また、静的 IP アドレスを使用する (Configuration Manager でサイト システム間の通信を保護するためのセキュリティのベスト プラクティス) と、IPsec の構成も簡単になります。  

**サイト システム サーバーに他のアプリケーションをインストールしない**  

サイト システム サーバーに他のアプリケーションをインストールすると、Configuration Manager で攻撃対象が増え、互換性に関する問題が危険にさらされます。  

**サイト オプションとして署名を要求して暗号化を有効にする**  

サイトで署名オプションと暗号化オプションを有効にします。 SHA-256 ハッシュ アルゴリズムをすべてのクライアントがサポートしていることを確認し、オプション [SHA-256 を必要とする] を有効にします。 ****  

**Configuration Manager 管理ユーザーを制限および監視し、役割に基づいた管理権限を構成して、これらの管理ユーザーに最低限必要なアクセス権を付与する**  

信頼できるユーザーにのみ Configuration Manager への管理アクセスを許可し、組み込みのセキュリティ ロールを使用するかセキュリティ ロールをカスタマイズして、これらのユーザーに最小限のアクセス許可を付与します。 アプリケーション、タスク シーケンス、ソフトウェア更新プログラム、構成項目、および構成基準を作成、変更、および展開できる管理ユーザーは、Configuration Manager 階層内のデバイスを制御する可能性があります。  

管理ユーザーの割り当てと承認レベルを定期的に監査して、必要な変更を確認します。  

役割に基づいた管理の構成の詳細については、「 [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md)」を参照してください。  

**Configuration Manager のバックアップをセキュリティで保護し、バックアップ時と復元時に通信チャネルをセキュリティで保護する**  

Configuration Manager のバックアップ時に、この情報には、攻撃者がなりすましに使用する可能性がある証明書や他の機密データが含まれています。  

このデータをネットワーク経由で転送するときに SMB 署名または IPsec を使用し、バックアップの場所をセキュリティで保護します。  

**Configuration Manager コンソールからネットワークの場所にオブジェクトをエクスポートまたはインポートする場合は常に、ネットワークの場所とネットワーク チャネルをセキュリティで保護する**  

ネットワーク フォルダーにアクセスできるユーザーを制限します。  

ネットワークの場所とサイト サーバー間、および Configuration Manager コンソールを実行するコンピューターとサイト サーバー間で SMB 署名または IPsec を使用して、エクスポートしたデータが攻撃者によって改ざんされるのを防ぎます。 情報開示を防ぐため、IPsec を使用してネットワーク上のデータを暗号化します。  

**サイト システムのアンインストールに失敗した場合、またはサイト システムの機能が停止して復元できない場合に、このサーバーの Configuration Manager 証明書を他の Configuration Manager サーバーから手動で削除する**  

元々サイト システムとサイト システムの役割で確立された PeerTrust を削除するには、他のサイト システム サーバーの**信頼されたユーザー**証明書ストアにある、障害が発生したサーバーの Configuration Manager 証明書を手動で削除します。 これは、サーバーを再フォーマットせずに再設定する場合に、特に重要です。  

これらの証明書の詳細については、「System Center Configuration Manager の暗号化コントロールのテクニカル リファレンス」の「[サーバー通信の暗号化制御](../../../protect/deploy-use/cryptographic-controls-technical-reference.md)」セクションをご覧ください。  

**境界ネットワークとイントラネットをブリッジするインターネットベースのサイト システムを構成しない**  

境界ネットワークとイントラネットに接続するように、サイト システム サーバーをマルチホームに構成しないでください。 この構成により、インターネットベースのサイト システムが、インターネットとイントラネットからクライアント接続を受け入れることができるようになりますが、境界ネットワークとイントラネット間のセキュリティ境界が排除されてしまいます。  

**サイト システム サーバーが信頼されていないネットワーク (境界ネットワークなど) 上にある場合、サイト システムへの接続を開始するようにサイト サーバーを構成する**  

既定では、サイト システムは、データを転送するためにサイト サーバーへの接続を開始します。この接続は、信頼されていないネットワークから信頼されているネットワークに対して開始される場合に、セキュリティ上のリスクになる可能性があります。 サイト システムがインターネットから接続を受け入れる場合、または信頼されていないフォレストに配置されている場合、サイト システムおよびサイト システムの役割のインストール後にすべての接続が信頼されているネットワークから開始されるように、サイト システム オプション [サイト サーバーがこのサイト システムへの接続を開始する必要がある] を構成します。 ****  

**インターネットベースのクライアント管理に Web プロキシ サーバーを使用する場合、認証終了を使用して SSL への SSL ブリッジングを使用する**  

 プロキシ Web サーバーで SSL ターミネーションを構成すると、インターネットからのパケットが内部ネットワークに転送される前に検査されます。 プロキシ Web サーバーはクライアントからの接続を認証してから終了します。次に、インターネット ベースのサイト システムに認証済みの新しい接続を開きます。  

 Configuration Manager クライアント コンピューターがプロキシ Web サーバーが使用してインターネットベースのサイト システムに接続する場合、クライアント ID (クライアント GUID) はパケット ペイロード内に安全に格納されるので、管理ポイントではプロキシ Web サーバーはクライアントとは見なされません。 プロキシ Web サーバーが SSL ブリッジングの要件をサポートできない場合は、SSL トンネリングもサポートされます。 このオプションはセキュリティが劣ります。これは、インターネットからの SSL パケットが終了せずにサイト システムに転送されるため、悪意のあるコンテンツがないかどうかを検査できないためです。  

 プロキシ Web サーバーが SSL ブリッジングの要件をサポートできない場合は、SSL トンネリングを使用できます。 ただし、このオプションはセキュリティが劣ります。これは、インターネットからの SSL パケットが終了せずにサイト システムに転送されるため、悪意のあるコンテンツがないかどうかを検査できないためです。  

> [!WARNING]  
>  Configuration Manager で登録されているモバイル デバイスでは、SSL ブリッジングを使用することはできません。SSL トンネリングのみ使用する必要があります。  

**コンピューターをウェイク アップしてソフトウェアをインストールするようにサイトを構成する場合に使用する構成**  

-   従来のウェイク アップ パケットを使用する場合、サブネット向けブロードキャストではなくユニキャストを使用する  

-   サブネット向けのブロードキャストを使用する必要がある場合は、サイト サーバーのみから、既定以外のポート番号のみで IP 向けのブロードキャストを許可するルートを構成する  

さまざまな Wake On LAN テクノロジの詳細については、「[System Center Configuration Manager でクライアントをウェイクアップする方法の計画](../../../core/clients/deploy/plan/plan-wake-up-clients.md)」を参照してください。

**電子メールによる通知を使用している場合は、SMTP メール サーバーへの認証アクセスを構成するようお勧めします。**  

可能な限り、認証アクセスをサポートするメール サーバーを使用し、認証にサイト サーバーのコンピューター アカウントを使用することをお勧めします。 認証でユーザー アカウントを指定する必要がある場合は、少なくとも特権のあるアカウントを使用します。  

##  <a name="a-namebkmksecuritysiteservera-security-best-practices-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a> サイト サーバーのセキュリティのベスト プラクティス  
 ここでは、Configuration Manager サイト サーバーをセキュリティで保護するときのベスト プラクティスについて説明します。  

 **ドメイン コントローラーの代わりに Configuration Manager をメンバー サーバーにインストールする**  

 Configuration Manager のサイト サーバーとサイト システムは、ドメイン コントローラーにインストールする必要はありません。 ドメイン コントローラーは、ドメイン データベース以外のローカルのセキュリティ アカウント マネージメント (SAM) データベースを持っていません。 Configuration Manager をメンバー サーバーにインストールすると、ドメイン データベース内ではなくローカルの SAM データベース内で Configuration Manager アカウントを保持できます。  

 これにより、ドメイン コントローラーの攻撃対象も減らすことができます。  

 **ネットワーク経由でセカンダリ サイト サーバーにファイルをコピーせずに、セカンダリ サイトをインストールする**  

 セットアップを実行してセカンダリ サイトを作成する際、親サイトからセカンダリ サイトにファイルをコピーするオプションや、ネットワーク ソースの場所を使用するオプションを選択しないでください。 ネットワーク経由でファイルをコピーすると、攻撃のタイミングは難しいですが、技術を持った攻撃者がセカンダリ サイトのインストール パッケージを乗っ取り、インストール前にファイルを改ざんする可能性があります。 ファイルの転送時に IPsec または SMB を使用すると、この攻撃を軽減できます。  

 ネットワーク経由でファイルをコピーする代わりに、セカンダリ サイト サーバーで、メディアからローカル フォルダーにソース ファイルをコピーします。 次に、セカンダリ サイトを作成するセットアップの実行中に、[ **インストール ソース ファイル** ] ページで、[ **セカンダリ サイト コンピューターで、次の場所にあるソース ファイルを使用する (最もセキュリティが高い)**] を選択し、このフォルダーを指定します。  

 詳細については、「[セットアップ ウィザードを使用してサイトをインストールする](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)」トピックの「[セカンダリ サイトのインストール](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary)」をご覧ください。  

##  <a name="a-namebkmksecuritysqlservera-security-best-practices-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a> SQL Server のセキュリティのベスト プラクティス  
 Configuration Manager では、SQL Server がバックエンド データベースとして使用されます。 データベースが侵害された場合、攻撃者は Configuration Manager をバイパスして SQL Server に直接アクセスし、Configuration Manager を通じて攻撃を行うことができます。 SQL Server に対する攻撃は、非常にリスクが高いと見なし、適切に減らす必要があります。  

 ここでは、Configuration Manager 用の SQL Server をセキュリティで保護するときのベスト プラクティスについて説明します。  

 **別の SQL Server アプリケーションを実行するのに、Configuration Manager サイト データベース サーバーを使用しない**  

 Configuration Manager サイト データベース サーバーへのアクセスが増えると、Configuration Manager データのリスクが増加します。 Configuration Manager サイト データベースが侵害された場合、同じ SQL Server コンピューター上の他のアプリケーションも危険にさらされます。  

 **Windows 認証を使用するように SQL Server を構成する**  

 Configuration Manager は Windows アカウントと Windows 認証を使用してサイト データベースにアクセスしますが、SQL Server 混在モードを使用するように SQL Server を構成することも可能です。 SQL Server 混在モードでは、追加の SQL ログインでデータベースにアクセスできますが、これは不要であり、攻撃対象を増やすことになります。  

 **セカンダリ サイトで使用する SQL Server Express に最新のソフトウェア更新プログラムが適用されるように、追加の手順を実行する**  

 プライマリ サイトがインストールされると、Configuration Manager は、Microsoft ダウンロード センターから SQL Server Express をダウンロードし、プライマリ サイト サーバーにファイルをコピーします。 セカンダリ サイトをインストールし、SQL Server Express をインストールするオプションを選択している場合、Configuration Manager は以前にダウンロードしたバージョンをインストールします。新しいバージョンが利用可能であるかどうかは確認されません。 セカンダリ サイトに最新バージョンが適用されていることを確認するには、次のいずれかを実行します。  

-   セカンダリ サイトのインストール後に、セカンダリ サイト サーバーで Windows Update を実行します。  

-   セカンダリ サイトのインストール前に、セカンダリ サイト サーバーを実行するコンピューターに SQL Server Express を手動でインストールし、最新バージョンおよびソフトウェア更新プログラムをインストールしていることを確認します。 次に、セカンダリ サイトをインストールし、既存の SQL Server インスタンスを使用するオプションを選択します。  

これらのサイトおよびインストールされているすべてのバージョンの SQL Server に対して Windows Update を定期的に実行し、最新のソフトウェア更新プログラムが適用されていることを確認します。  

**SQL Server のベスト プラクティスに従う**  

使用するバージョンの SQL Server のベスト プラクティスに従います。 ただし、Configuration Manager に関する次の要件を考慮します。  

-   サイト サーバーのコンピューター アカウントが、SQL Server を実行しているコンピューターの管理者グループのメンバーである必要があります。 "管理プリンシパルを明示的にプロビジョニングする" という SQL Server の推奨事項に従う場合、サイト サーバーでセットアップを実行する際に使用するアカウントが SQL ユーザー グループのメンバーである必要があります。  

-   ドメイン ユーザー アカウントを使用して SQL Server をインストールする場合、Active Directory ドメイン サービスに発行されるサービス プリンシパル名 (SPN) にサイト サーバーのコンピューター アカウントが構成されていることを確認します。 SPN がない場合、Kerberos 認証が失敗して Configuration Manager のセットアップが失敗します。  

##  <a name="a-namebkmksecurityiisa-security-best-practices-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a> IIS を実行するサイト システムのセキュリティのベスト プラクティス  
Configuration Manager の複数のサイト システムの役割に IIS が必要です。 IIS をセキュリティで保護すると、Configuration Manager が正しく動作するようになるため、セキュリティ攻撃のリスクが軽減されます。 これを実際に行うと、IIS が必要なサーバーの数が最小限に抑えられます。 たとえば、クライアント ベースをサポートするために必要な数の管理ポイントだけを実行し、インターネットベースのクライアント管理のために高可用性とネットワーク分離を考慮します。  

 ここでは、IIS を実行するサイト システムをセキュリティで保護するときのベスト プラクティスについて説明します。  

 **不要な IIS 機能を無効にする**  

 インストールするサイト システムの役割に最小限の IIS 機能をインストールします。 詳細については、「[サイトとサイト システムの前提条件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)」をご覧ください。  

 **HTTPS を要求するようにサイト システムの役割を構成する**  

 クライアントは、HTTPS ではなく HTTP を使用してサイト システムに接続する場合、Windows 認証を使用しますが、Kerberos 認証ではなく NTLM 認証を使用するように切り替わることがあります。 NTLM 認証を使用すると、クライアントが偽のサーバーに接続する可能性があります。  

 このセキュリティのベスト プラクティスの例外は、配布ポイントです。これは、配布ポイントが HTTPS 接続用に構成されていると、パッケージ アクセス アカウントが機能しないからです。 パッケージ アクセス アカウントはコンテンツに対する承認を提供します。これにより、コンテンツにアクセスできるユーザーを制限することができます。 詳細については、「 [Security Best Practices for Content Management](../../../core/plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement)」を参照してください。  

**次のサイト システムの役割に対して IIS で証明書信頼リスト (CTL) を構成します。**  

サイト システムの役割 :  

-   HTTPS 用に構成されている配布ポイント  

-   HTTPS 用に構成され、モバイル デバイスのサポートが有効な管理  

証明書信頼リスト (CTL) は、信頼されるルート証明機関の定義済みリストです。 CTL を グループ ポリシーと PKI の展開と組み合わせて使用すると、ネットワーク上で構成されている既存の信頼されたルート証明機関を補うことができます。ネットワーク上の既存のルート証明機関には、Microsoft Windows と一緒に自動的にインストールされるものや、Windows エンタープライズ ルート証明機関によって追加されるものなどがあります。 一方、CTL が IIS で構成されている場合、CTL はこれらの信頼されたルート証明機関のサブセットを定義します。  

このサブセットによりセキュリティ管理が強化されます。その理由は、CTL によって、受け付けられるクライアント証明書が CTL にリストされている証明機関から発行されたもののみに制限されるためです。 たとえば、Windows には、VeriSign や Thawte など、有名なサードパーティ証明機関が数多く付属しています。 既定では、IIS を実行するコンピューターは、これらの既知の証明機関へチェーンされている証明書を信頼します。 リストされているサイト システムの役割に対して CTL を使用して IIS を構成しない場合、これらの証明機関から発行されたクライアント証明書を持つデバイスはどれも、有効な Configuration Manager クライアントとして受け入れられます。 IIS をこれらの証明機関を含んでいない CTL を使用して構成すると、証明書がこれらの証明機関へチェーンされている場合にクライアント接続が拒否されます。 ただし、リストされているサイト システムの役割で Configuration Manager クライアントが受け入れられるようにするには、Configuration Manager クライアントによって使用される証明機関を指定した CTL を使用して IIS を構成する必要があります。  

> [!NOTE]  
>  IIS で CTL を構成することが必要になるのは、リストされているサイト システムの役割のみです。Configuration Manager が管理ポイントに使用する証明書発行者リストは、クライアント コンピューターが HTTPS 管理ポイントに接続するときに同じ機能を提供します。  

IIS で信頼された証明機関のリストを構成する方法の詳細については、IIS のドキュメントを参照してください。  

**IIS と共にサイト サーバーをコンピューター上に配置しない**  

役割を分離すると、攻撃プロファイルを減らし、回復性を向上できます。 また、サイト サーバーのコンピューター アカウントは、通常、すべてのサイト システムの役割 (および、クライアント プッシュ インストールを使用している場合は、Configuration Manager クライアント) で管理者特権を持っています。  

**Configuration Manager に専用の IIS サーバーを使用する**  

Configuration Manager でも使用される IIS サーバーに複数の Web ベース アプリケーションをホストできますが、これにより、攻撃対象が大幅に増える可能性があります。 アプリケーションが正しく構成されていないと、攻撃者によって Configuration Manager サイト システムの制御が奪われて、階層全体の制御が奪われてしまう可能性があります。  

他の Web ベース アプリケーションを Configuration Manager サイト システムで実行する必要がある場合、Configuration Manager サイト システムにカスタム Web サイトを作成します。  

**カスタム Web サイトを使用する**  

IIS を実行するサイト システムでは、IIS に既定の Web サイトではなくカスタム Web サイトを使用するように Configuration Manager を構成できます。 サイト システムで他の Web アプリケーションを実行する場合は、カスタム Web サイトを使用する必要があります。 この設定は、特定のサイト システムの設定ではなく、サイト全体の設定です。  

サイト システムで他の Web アプリケーションを実行する場合は、セキュリティの強化に加えて、カスタム Web サイトを使用する必要があります。  

**配布ポイントの役割のインストール後に、既定の Web サイトをカスタム Web サイトに切り替える場合、既定の仮想ディレクトリを削除する**  

既定の Web サイトの使用からカスタム Web サイトの使用に変更した場合、Configuration Manager により、以前の仮想ディレクトリが削除されることはありません。 既定の Web サイトの下に Configuration Manager によって作成された、仮想ディレクトリを削除します。  

たとえば、配布ポイントで削除する仮想ディレクトリは、次のとおりです。  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**IIS Server のベスト プラクティスに従う**  

使用するバージョンの IIS Server のベスト プラクティスに従います。 ただし、特定のサイト システムの役割に対して Configuration Manager が持つ要件を考慮に入れます。 詳細については、「[サイトとサイト システムの前提条件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)」をご覧ください。  

##  <a name="a-namebkmksecuritymanagementpointa-security-best-practices-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a> 管理ポイントのセキュリティのベスト プラクティス  
 管理ポイントは、デバイスと Configuration Manager の間の基本インターフェイスです。 管理ポイントおよび管理ポイントを実行しているサーバーに対する攻撃は、非常にリスクが高いと見なし、適切に減らす必要があります。 管理ポイントの動作を注意深く監視し、ベスト プラクティスに従ってください。  

 次に、Configuration Manager で管理ポイントをセキュリティで保護するときのベスト プラクティスについて説明します。  

**管理ポイントに Configuration Manager クライアントをインストールするときに、このクライアントをその管理ポイントのサイトに割り当てる**  

 管理ポイントのサイト システムにある Configuration Manager クライアントを管理ポイントのサイト以外のサイトには割り当てないでください。  

 以前のバージョンから System Center Configuration Manager に移行する場合、できるだけ早く管理ポイント上のクライアント ソフトウェアを System Center Configuration Manager に移行します。  

##  <a name="a-namebkmksecurityfspa-security-best-practices-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a> フォールバック ステータス ポイントのセキュリティのベスト プラクティス  
 ここでは、Configuration Manager でフォールバック ステータス ポイントをインストールするときのセキュリティのベスト プラクティスについて説明します。  

 フォールバック ステータス ポイントをインストールするときのセキュリティの注意事項については、「 [Determine Whether You Require a Fallback Status Point](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md#BKMK_Determine_FSP)」を参照してください。  

**他のサイト システムの役割は、サイト システムで実行しない。また、ドメイン コントローラーにインストールしない**  

 フォールバック ステータス ポイントは、任意のコンピューターから認証されていない通信を受け入れるように設計されているため、このサイト システムの役割を他のサイト システムの役割と共に実行したり、ドメイン コントローラー上で実行すると、そのサーバーのリスクが大幅に増加します。  

**Configuration Manager でのクライアント通信に PKI 証明書を使用する場合、クライアントをインストールする前にフォールバック ステータス ポイントをインストールする**  

 Configuration Manager サイト システムが HTTP クライアント通信を受け入れない場合、PKI 関連の証明書の問題のために、クライアントが管理対象かどうかがわからないことがあります。 ただし、クライアントがフォールバック ステータス ポイントに割り当てられている場合、これらの証明書の問題はフォールバック ステータス ポイントによってレポートされます。  

 セキュリティ上の理由から、クライアントのインストール後に、フォールバック ステータス ポイントをクライアントに割り当てることはできません。この役割は、クライアントのインストール時にのみ割り当てることができます。  

**境界ネットワークでのフォールバック ステータス ポイントの使用を避ける**  

 仕様により、フォールバック ステータス ポイントは任意のクライアントからデータを受け入れます。 境界ネットワークにフォールバック ステータス ポイントを配置すると、インターネット ベース クライアントのトラブルシューティングに役立つ場合がありますが、トラブルシューティングの利点と、一般からアクセス可能なネットワークでサイト システムが認証されていないデータを受け入れるリスクとのバランスを取る必要があります。  

 境界ネットワークまたは信頼されていないネットワークにフォールバック ステータス ポイントをインストールする場合、フォールバック ステータス ポイントがサイト サーバーへの接続を開始する既定の設定ではなく、サイト サーバーがデータ転送を開始するように構成します。  

##  <a name="a-namebkmksecurityissuesclientsa-security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a> サイト管理に関するセキュリティの問題  
 Configuration Manager に関する次のセキュリティの問題を確認します。  

-   Configuration Manager には、ネットワークの攻撃に Configuration Manager を使用する承認された管理ユーザーに対する防御がありません。 承認されていない管理ユーザーは、セキュリティ上、高いリスクであり、次のようなさまざまな攻撃を仕掛ける可能性があります。  

    -   ソフトウェア開発を使用して、企業内のすべての Configuration Manager クライアント コンピューターに悪意のあるソフトウェアを自動的にインストールして実行する。  

    -   リモート コントロールを使用して、クライアントのアクセス許可なしに Configuration Manager クライアントをリモートで制御する。  

    -   ポーリング間隔を短縮してインベントリの量が膨大になるように構成し、クライアントとサーバーへのサービス拒否攻撃を行う。  

    -   階層内のいずれかのサイトを使用して、別のサイトの Active Directory データにデータを書き込む。  

    サイト階層がセキュリティの境界です。サイトは単なる管理の境界であると考えてください。  

    管理ユーザーのすべてのアクティビティを監査し、定期的に監査ログを調べます。 すべての Configuration Manager 管理ユーザーについて、採用前に経歴を確認し、定期的に勤務状況を再確認することが必要です。  

-   登録ポイントが侵害された場合、攻撃者が認証用の証明書を取得して、モバイル デバイスを登録しているユーザーの資格情報を盗み出す可能性があります。  

    登録ポイントは証明機関と通信します。また、Active Directory オブジェクトを作成、変更、および削除することができます。 境界ネットワークに登録ポイントをインストールしないでください。また、異常なアクティビティを監視してください。  

-   インターネットベースのクライアント管理にユーザー ポリシーを許可したり、インターネット上にあるユーザー用にアプリケーション カタログ Web サイト ポイントを構成したりすると、攻撃プロファイルが増加します。  

    クライアントとサーバー間の接続に PKI 証明書を使用するだけでなく、これらの構成では Windows 認証が必要ですが、Kerberos ではなく NTLM 認証を使用するように切り替わることがあります。 NTLM 認証は、なりすましや再生攻撃に対して脆弱です。 インターネット上のユーザーを正しく認証するためには、インターネットベースのサイト システム サーバーからドメイン コントローラーへの接続を許可する必要があります。  

-   Admin$ 共有がサイト システム サーバーで必要です。  

    Configuration Manager サイト サーバーでは、サイト システムのサービスへの接続とサービスの実行に Admin$ 共有を使用します。 Admin$ 共有は無効化したり削除したりしないでください。  

-   Configuration Manager は、名前解決サービスを使用して他のコンピューターに接続します。この名前解決サービスを、スプーフィング、改ざん、否認、情報開示、サービス拒否、権限の昇格などのセキュリティ攻撃から保護することは困難です。  

    名前解決に使用する DNS と WINS のバージョンのセキュリティのベストプラクティスに従います。  

##  <a name="a-namebkmkprivacycliientsa-privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a> 探索のプライバシー情報  
 探索によって、ネットワーク リソースのレコードが作成され、System Center Configuration Manager データベースに保存されます。 探索データ レコードには、IP アドレス、オペレーティング システム、コンピューター名などのコンピューター情報が含まれます。 Active Directory 探索方法を Active Directory ドメイン サービスに保存されている情報を探索するように構成することもできます。  

 既定で有効になっている探索方法は定期探索だけですが、この方法では System Center Configuration Manager クライアント ソフトウェアが既にインストールされているコンピューターのみ探索されます。  

 探索情報がマイクロソフトに送信されることはありません。 探索情報は、Configuration Manager データベースに保存されます。 情報は、90 日ごとに実行されるサイトの保守タスク [期限切れの探索データの削除] によって削除されるまでデータベースに保持されます。 **** 削除間隔は構成できます。  

 追加の探索方法を構成したり、Active Directory 探索を拡張したりする前に、プライバシー要件を検討してください。  



<!--HONumber=Nov16_HO1-->

