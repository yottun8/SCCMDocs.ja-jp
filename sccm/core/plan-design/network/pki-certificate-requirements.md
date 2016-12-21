---
title: "PKI 証明書の要件 | System Center Configuration Manager"
description: "System Center Configuration Manager で必要な PKI 証明書の要件について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6a73e68-57d8-4786-842b-36669541d8ff
caps.latest.revision: 17
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fbc85f65e4ad952d40161e6f6282bb6c0796662b


---
# <a name="pki-certificate-requirements-for-system-center-configuration-manager"></a>System Center Configuration Manager での PKI 証明書の要件

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager で必要になる場合がある公開キー基盤 (PKI) 証明書の一覧を次に示します。 この情報は、PKI 証明書の基本的な知識があることを前提にしています。 展開の詳細な手順については、「[System Center Configuration Manager PKI 証明書の展開手順の例: Windows Server 2008 証明機関](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)」を参照してください。 Active Directory 証明書サービスの詳細については、次のドキュメントを参照してください。  

-   Windows Server 2012: [Active Directory 証明書サービスの概要](http://go.microsoft.com/fwlink/p/?LinkId=286744)  

-   Windows Server 2008: [Windows Server 2008 の Active Directory 証明書サービス](http://go.microsoft.com/fwlink/p/?LinkId=115018)  

> [!IMPORTANT]  
>  2017 年 1 月 1 日より、Windows は SHA-1 で署名された証明書を信頼しなくなります。  SHA-2 で署名された新しいサーバーおよびクライアント認証証明書を発行することをお勧めします。  
>   
>  この変更と、今後生じる可能性のある期日の更新の詳細については、このブログの投稿をご覧ください: [Windows Enforcement of Authenticode Code Signing and Timestamping (Windows の Authenticode コード署名とタイムスタンプ処理の実施)](http://social.technet.microsoft.com/wiki/contents/articles/32288.windows-enforcement-of-authenticode-code-signing-and-timestamping.aspx)  

 System Center Configuration Manager でモバイル デバイスと Mac コンピューターに登録するクライアント証明書、Microsoft Intune でモバイル デバイスの管理用に自動作成される証明書、および System Center Configuration Manager で AMT ベースのコンピューターにインストールされる証明書を除き、任意の PKI を使用して次の証明書を作成、展開、および管理できます。 ただし、Active Directory 証明書サービスと証明書テンプレートを使用する場合、この Microsoft PKI ソリューションを使用すると証明書の管理が簡単になります。 次の表の「 **使用する Microsoft 証明書テンプレート** 」列を確認し、証明書の要件に最も近い証明書テンプレートを特定してください。 テンプレート ベースの証明書を発行できるのは、Windows Server 2008 Enterprise や Windows Server 2008 Datacenter など、サーバー オペレーティング システムの Enterprise Edition または Datacenter Edition で実行されている企業証明機関だけです。  

> [!IMPORTANT]  
>  エンタープライズ証明機関と証明書テンプレートを使用する場合、バージョン 3 のテンプレートを使用しないでください。 これらの証明書テンプレートで作成される証明書は、System Center Configuration Manager と互換性がありません。 代わりに、次の手順に従って、バージョン 2 のテンプレートを使用してください。  
>   
>  -   Windows Server 2012 の CA の場合: 証明書テンプレートのプロパティの **[互換性]** タブで、 **[証明機関]** オプションに **[Windows Server 2003]** を指定し、 **[証明書の受信者]** オプションに **[Windows XP / Server 2003]** を指定します。  
> -   Windows Server 2008 の CA の場合: 証明書テンプレートを複製するときに、 **[テンプレートの複製]** ポップアップ ダイアログ ボックスで選択を求められたら、 **[Windows Server 2003 Enterprise]** を既定の選択のままにします。 [Windows Server 2008 Enterprise Edition ****] を選択しないでください。  

 次のセクションで証明書の要件を確認してください。  

##  <a name="a-namebkmkpkicertificatesforserversa-pki-certificates-for-servers"></a><a name="BKMK_PKIcertificates_for_servers"></a> サーバー向け PKI 証明書  

|System Center Configuration Manager コンポーネント|証明書の目的|使用する Microsoft 証明書テンプレート|証明書の固有情報|System Center Configuration Manager での証明書の使用方法|  
|-------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|Internet Information Services (IIS) を実行し、HTTPS クライアント接続用に構成されているサイト システム:<br /><br /> - 管理ポイント<br /><br /> - 配布ポイント<br /><br /> - ソフトウェアの更新ポイント<br /><br /> - 状態移行ポイント<br /><br /> - 登録ポイント<br /><br /> - 登録プロキシ ポイント<br /><br /> - アプリケーション カタログ Web サービス ポイント<br /><br /> - アプリケーション カタログ Web サイト ポイント<br /><br /> - 証明書登録ポイント|サーバー認証|**Web サーバー**|[拡張キー使用法] の値には「 サーバー認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。1)」をご覧ください。<br /><br /> サイト システムがインターネットからの接続を受け入れる場合は、サブジェクト名やサブジェクトの別名にインターネット完全修飾ドメイン名 (FQDN) が含まれる必要があります。<br /><br /> サイト システムがイントラネットからの接続を受け入れる場合は、サイト システムの構成方法に応じて、サブジェクト名やサブジェクトの別名にイントラネット FQDN (推奨) またはコンピューターの名前が含まれる必要があります。<br /><br /> サイト システムがインターネットとイントラネット両方からの接続を受け入れる場合は、インターネット FQDN とイントラネット FQDN (またはコンピューターの名前) の両方をアンパサンド (&) 記号で区切って指定する必要があります。<br /><br /> **注:** ソフトウェアの更新ポイントがインターネットからのみクライアント接続を受け入れる場合は、インターネット FQDN とイントラネット FQDN の両方が証明書に含まれている必要があります。<br /><br /> SHA-2 ハッシュ アルゴリズムがサポートされています。<br /><br /> System Center Configuration Manager では、この証明書でサポートされるキーの最大長が指定されません。 この証明書のキー サイズに関する問題については、使用している PKI および IIS のドキュメントを参照してください。|この証明書は、コンピューター証明書ストア内の個人用ストアに保存されている必要があります。<br /><br /> この Web サーバー証明書は、これらのサーバーをクライアントに対して認証するのに使用されます。また、クライアントとこれらのサーバーの間で転送されるすべてのデータを SSL (Secure Sockets Layer) で暗号化するのにも使用されます。|  
|クラウドベースの配布ポイント|サーバー認証|**Web サーバー**|[拡張キー使用法] の値には「 サーバー認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。1)」をご覧ください。<br /><br /> サブジェクト名には、クラウドベースの配布ポイントの特定のインスタンスについて、共通名としてユーザー定義のサービス名と FQDN 形式のドメイン名が含まれている必要があります。<br /><br /> 秘密キーはエクスポートできる必要があります。<br /><br /> SHA-2 ハッシュ アルゴリズムがサポートされています。<br /><br /> サポートされるキーの長さ: 2048 ビット。|このサービス証明書は、Configuration Manager クライアントに対するクラウドベースの配布ポイント サービスを認証するため、および Secure Sockets Layer (SSL) を使用してクライアント間で転送されるすべてのデータを暗号化するために使用されます。この証明書は、公開キー証明書標準 (PKCS #12) 形式でエクスポートする必要があります。パスワードは、クラウドベースの配布ポイントを作成するときにインポートできるように既知である必要があります。<br /><br /> **注:** この証明書は、Windows Azure 管理証明書と一緒に使用されます。 この証明書の詳細については、MSDN ライブラリの Windows Azure プラットフォーム セクションの「 [Windows Azure の管理証明書を作成する方法](http://go.microsoft.com/fwlink/p/?LinkId=220281) 」および「 [Windows Azure サブスクリプションへの管理証明書の追加方法](http://go.microsoft.com/fwlink/?LinkId=241722) 」をご覧ください。|  
|Microsoft SQL Server を実行するサイト システム サーバー|サーバー認証|**Web server**|[拡張キー使用法] の値には「 サーバー認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。1)」をご覧ください。<br /><br /> サブジェクト名にはイントラネット完全修飾ドメイン名 (FQDN) が含まれている必要があります。<br /><br /> SHA-2 ハッシュ アルゴリズムがサポートされています。<br /><br /> サポートされるキーの最大長は 2048 ビットです。|この証明書はコンピューター証明書ストア内の個人用ストアに保存されている必要があります。System Center Configuration Manager は、サーバーとの信頼関係を確立する必要がある System Center Configuration Manager 階層内のサーバーの信頼されたユーザー ストアにこの証明書を自動的にコピーします。<br /><br /> これらの証明書はサーバー間の認証に使用されます。|  
|SQL Server クラスター: Microsoft SQL Server を実行するサイト システム サーバー|サーバー認証|**Web server**|[拡張キー使用法] の値には「 サーバー認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。1)」をご覧ください。<br /><br /> サブジェクト名には、クラスターのイントラネット完全修飾ドメイン名 (FQDN) が含まれている必要があります。<br /><br /> 秘密キーはエクスポートできる必要があります。<br /><br /> SQL Server クラスターを使用するように System Center Configuration Manager を構成する時点で、証明書に 2 年間以上の有効期間が残っている必要があります。<br /><br /> SHA-2 ハッシュ アルゴリズムがサポートされています。<br /><br /> サポートされるキーの最大長は 2048 ビットです。|クラスターの 1 つのノードでこの証明書を要求してインストールしたら、証明書をエクスポートし、SQL Server クラスター内のその他の各ノードにインポートします。<br /><br /> この証明書はコンピューター証明書ストア内の個人用ストアに保存されている必要があります。System Center Configuration Manager は、サーバーとの信頼関係を確立する必要がある System Center Configuration Manager 階層内のサーバーの信頼されたユーザー ストアにこの証明書を自動的にコピーします。<br /><br /> これらの証明書はサーバー間の認証に使用されます。|  
|次のサイト システムの役割のサイト システム監視: <br /><br /> 管理ポイント<br /><br /> 状態移行ポイント|クライアント認証|**ワークステーション認証**|[拡張キー使用法] の値には「 クライアント認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。2)」をご覧ください。<br /><br /> コンピューターでは、[サブジェクト名] フィールドまたは [サブジェクトの別名] フィールドに一意の値が必要です。<br /><br /> **注:** サブジェクトの別名に複数の値を使用している場合は、最初の値のみが使用されます。<br /><br /> SHA-2 ハッシュ アルゴリズムがサポートされています。<br /><br /> サポートされるキーの最大長は 2048 ビットです。|System Center Configuration Manager クライアントがインストールされていない場合でも、これらのサイト システムの役割の正常性を監視しサイトに報告するため、この証明書は一覧のサイト システム サーバーで必要です。<br /><br /> これらのサイト システム用の証明書は、コンピューター証明書ストアの個人用ストアに保存されている必要があります。|  
|ネットワーク デバイス登録サービスのロール サービスが設定された System Center Configuration Manager ポリシー モジュールを実行するサーバー。|クライアント認証|ワークステーション認証|[拡張キー使用法] の値には「 クライアント認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。2)」をご覧ください。<br /><br /> 証明書のサブジェクトやサブジェクトの別名 (SAN) には、特定の要件はありません。ネットワークデバイス登録サービスを実行する複数のサーバーで、同じ証明書を使用できます。<br /><br /> SHA-2 および SHA-3 ハッシュ アルゴリズムがサポートされています。<br /><br /> サポートされるキーの長さ: 1024 ビットと 2048 ビット。||  
|配布ポイントがインストールされているサイト システム|クライアント認証|**ワークステーション認証**|[拡張キー使用法] の値には「 クライアント認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。2)」をご覧ください。<br /><br /> 証明書のサブジェクトやサブジェクトの別名 (SAN) には、特定の要件はありません。複数の配布ポイントで同じ証明書を使用することができます。 ただし、配布ポイントごとに異なる証明書を使用することをお勧めします。<br /><br /> 秘密キーはエクスポートできる必要があります。<br /><br /> SHA-2 ハッシュ アルゴリズムがサポートされています。<br /><br /> サポートされるキーの最大長は 2048 ビットです。|この証明書には、次の 2 つの目的があります。<br /><br /> - 配布ポイントがステータス メッセージを送信する前に、HTTPS に対応している管理ポイントに対して配布ポイントを認証します。<br /><br /> - **[クライアントの PXE サポートを有効にする]** 配布ポイント オプションが選択されている場合は、コンピューターに証明書が送信されます。これにより、オペレーティング システムを展開するときには、クライアント ポリシーの取得やインベントリ情報の送信といったクライアント アクションがオペレーティング システム展開プロセスのタスク シーケンスに含まれている場合に、クライアント コンピューターから HTTPS 対応管理ポイントに接続できるようになります。<br /><br /> この証明書は、オペレーティング システムの展開プロセス中にのみ使用され、クライアントにはインストールされません。 このように一時的に使用することで、複数のクライアント証明書を使用せずに、同じ証明書をすべてのオペレーティング システムの展開に使用できます。<br /><br /> この証明書は、公開キー証明書標準 (PKCS #12) 形式でエクスポートする必要があります。パスワードは、配布ポイントのプロパティにインポートできるように既知である必要があります。<br /><br /> **注:** この証明書の要件は、オペレーティング システムを展開するブート イメージのクライアント証明書と同じです。 要件が同じなので、同じ証明書ファイルを使用できます。|  
|帯域外サービス ポイント|AMT のプロビジョニング|**Web サーバー** (変更済み)|**[拡張キー使用法]** の値に " **サーバー認証 (1.3.6.1.5.5.7.3.1)** " とオブジェクト識別子 **2.16.840.1.113741.1.2.3**が含まれている必要があります。<br /><br /> [サブジェクト名] フィールドに、帯域外サービス ポイントをホストしているサーバーの FQDN が含まれている必要があります。<br /><br /> **注:** 独自の内部 CA ではなく外部 CA に AMT プロビジョニング証明書を要求する場合で、その CA が AMT プロビジョニング オブジェクト識別子である 2.16.840.1.113741.1.2.3 をサポートしていない場合は、証明書サブジェクト名の組織単位 (OU) 属性として、代わりに「 **Intel(R) Client Setup Certificate**」という文字列を指定できます。 この英語のテキスト文字列をそのまま (大文字小文字を区別、末尾にピリオドを付けない)、帯域外サービス ポイントをホストしているサーバーの FQDN に加えて使用する必要があります。<br /><br /> サポートされるキーの長さ: 1024 と 2048。 AMT 6.0 以降のバージョンでは、キーの長さとして 4096 ビットもサポートされます。|この証明書は、帯域外サービス ポイント サイト システム サーバーにあるコンピューター証明書ストア内の個人用ストアに保存されます。<br /><br /> この AMT プロビジョニング証明書は、帯域外管理用コンピューターを準備するために使用されます。<br /><br /> AMT プロビジョニング証明書を提供する CA から発行されるこの証明書を要求する必要があります。AMT ベースのコンピューターの BIOS 拡張は、このプロビジョニング証明書のルート証明書の拇印 (証明書ハッシュとも呼ばれる) を使用するように構成する必要があります。<br /><br /> VeriSign は、AMT プロビジョニング証明書を提供する外部 CA の一例ですが、独自の内部 CA を使用することもできます。<br /><br /> 帯域外サービス ポイントをホストするサーバーに証明書をインストールします。このサーバーは、証明書のルート CA に正常に連係できる必要があります (既定では、ルート CA 証明書と VeriSign に対する中間 CA 証明書は Windows のインストール時にインストールされます)。|  
|Microsoft Intune コネクタを実行するサイト システム サーバー|クライアント認証|該当なし: この証明書は Intune で自動作成されます。|[拡張キー使用法] の値には「クライアント認証 (1.3.6.1.5.5.7.3.2)」が含まれます。<br /><br /> 3 つのカスタム拡張機能で、ユーザーの Intune サブスクリプションが一意に識別されます。<br /><br /> キーのサイズは 2,048 ビットであり、SHA-1 ハッシュ アルゴリズムを使用します。<br /><br /> **注:** この設定は変更できません。この情報は参考のためにのみ提供されます。|Microsoft Intune をサブスクライブすると、この証明書は自動的に要求され、Configuration Manager データベースにインストールされます。 Microsoft Intune コネクタをインストールすると、Microsoft Intune コネクタを実行しているサイト システム サーバーにこの証明書がインストールされます。 また、コンピューターの証明書ストアにインストールされます。<br /><br /> この証明書は、Microsoft Intune コネクタを使用して、Microsoft Intune に対して Configuration Manager 階層を認証するために使用されます。 これらのコンポーネント間で転送されるすべてのデータは、Secure Sockets Layer (SSL) を使用します。|  

###  <a name="a-namebkmkpkicertificatesforproxyserversa-proxy-web-servers-for-internet-based-client-management"></a><a name="BKMK_PKIcertificates_for_proxyservers"></a> インターネット ベースのクライアント管理用のプロキシ Web サーバー  
 サイトがインターネット ベースのクライアント管理をサポートしており、SSL ターミネーションによるプロキシ Web サーバーを使用 (ブリッジング) してインターネット接続を受信している場合、プロキシ Web サーバーには次の表に示す証明書要件があります。  

> [!NOTE]  
>  SSL ターミネーション機能がないプロキシ Web サーバーを使用 (トンネリング) している場合は、プロキシ Web サーバー上に追加の証明書は必要ありません。  

|ネットワーク インフラストラクチャ コンポーネント|証明書の目的|使用する Microsoft 証明書テンプレート|証明書の固有情報|System Center Configuration Manager での証明書の使用方法|  
|--------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|インターネット経由のクライアント接続を受け入れるプロキシ Web サーバー|サーバー認証およびクライアント認証|1. <br />                        **Web サーバー**<br /><br /> 2. <br />                        **ワークステーション認証**|[サブジェクト名] フィールドまたは [サブジェクトの別名] フィールドにインターネット FQDN が必要です (Microsoft 証明書テンプレートを使用している場合は、サブジェクトの別名はワークステーション テンプレートでのみ利用可能です)。<br /><br /> SHA-2 ハッシュ アルゴリズムがサポートされています。|この証明書は、次のサーバーをインターネット クライアントに対して認証するのに使用されます。また、クライアントとこのサーバーの間で転送されるすべてのデータを SSL で暗号化するのにも使用されます。<br /><br /> - インターネット ベースの管理ポイント<br /><br /> - インターネット ベースの配布ポイント<br /><br /> - インターネット ベースのソフトウェアの更新ポイント<br /><br /> クライアント認証は、System Center Configuration Manager クライアントとインターネット ベースのサイト システムの間のクライアント接続のブリッジに使用されます。|  

##  <a name="a-namebkmkpkicertificatesforclientsa-pki-certificates-for-clients"></a><a name="BKMK_PKIcertificates_for_clients"></a> クライアント向け PKI 証明書  

|System Center Configuration Manager コンポーネント|証明書の目的|使用する Microsoft 証明書テンプレート|証明書の固有情報|System Center Configuration Manager での証明書の使用方法|  
|-------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|Windows クライアント コンピューター|クライアント認証|**ワークステーション認証**|[拡張キー使用法] の値には「 クライアント認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。2)」をご覧ください。<br /><br /> クライアント コンピューターでは、[サブジェクト名] フィールドまたは [サブジェクトの別名] フィールドに一意の値が必要です。<br /><br /> **注:** サブジェクトの別名に複数の値を使用している場合は、最初の値のみが使用されます。<br /><br /> SHA-2 ハッシュ アルゴリズムがサポートされています。<br /><br /> サポートされるキーの最大長は 2048 ビットです。|既定では、System Center Configuration Manager はコンピューター証明書ストア内の個人用ストアでコンピューターの証明書を検索します。<br /><br /> ソフトウェアの更新ポイントとアプリケーション カタログ Web サイト ポイントを除き、この証明書は、IIS を実行し HTTPS を使用するように構成されているサイト システム サーバーに対してクライアントを認証します。|  
|モバイル デバイス クライアント|クライアント認証|**認証されたセッション**|[拡張キー使用法] の値には「 クライアント認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。2)」をご覧ください。<br /><br /> SHA-1<br /><br /> サポートされるキーの最大長は 2048 ビットです。<br /><br /> **注:**<br /><br /> - これらの証明書は Distinguished Encoding Rules (DER) encoded binary X.509 形式である必要があります。<br /><br /> - Base64 encoded X.509 形式はサポートされません。|この証明書は、管理ポイントや配布ポイントなど、モバイル デバイス クライアントが通信するサイト システム サーバーに対して、モバイル デバイス クライアントを認証します。|  
|オペレーティング システムを展開するためのブート イメージ|クライアント認証|**ワークステーション認証**|[拡張キー使用法] の値には「 クライアント認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。2)」をご覧ください。<br /><br /> 証明書のサブジェクトやサブジェクトの別名 (SAN) には、特定の要件はありません。すべてのブート イメージで同じ証明書を使用することができます。<br /><br /> 秘密キーはエクスポートできる必要があります。<br /><br /> SHA-2 ハッシュ アルゴリズムがサポートされています。<br /><br /> サポートされるキーの最大長は 2048 ビットです。|オペレーティング システムの展開プロセスのタスク シーケンスに、クライアント ポリシーの取得やインベントリ情報の送信などのクライアントの操作が含まれる場合は、この証明書が使用されます。<br /><br /> この証明書は、オペレーティング システムの展開プロセス中にのみ使用され、クライアントにはインストールされません。 このように一時的に使用することで、複数のクライアント証明書を使用せずに、同じ証明書をすべてのオペレーティング システムの展開に使用できます。<br /><br /> この証明書は、公開キー証明書標準 (PKCS #12) 形式でエクスポートする必要があります。パスワードは、System Center Configuration Manager ブート イメージにインポートできるように既知である必要があります。<br /><br /> これは、タスク シーケンス用の一時的な証明書であり、クライアントのインストールには使用されません。 HTTPS の環境のみがある場合に、クライアントがサイトと通信して展開を続行するには、クライアントの有効な証明書が必要です。 クライアントが Active Directory に参加している場合は、クライアント証明書をクライアントで自動的に生成できます。あるいは、別のメソッドを使用して、クライアント証明書をインストールできます。<br /><br /> **注:** この証明書の要件は、配布ポイントがインストールされているサイト システムのサーバー証明書と同じです。 要件が同じなので、同じ証明書ファイルを使用できます。|  
|Mac クライアント コンピューター|クライアント認証|System Center Configuration Manager の登録の場合: **認証されたセッション**<br /><br /> System Center Configuration Manager とは独立した証明書のインストールの場合: **ワークステーション認証**|[拡張キー使用法] の値には「 クライアント認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。2)」をご覧ください。<br /><br /> System Center Configuration Manager でユーザー証明書を作成する場合、証明書のサブジェクト値には、Mac コンピューターを登録した個人のユーザー名が設定されます。<br /><br /> System Center Configuration Manager の登録を使用せず、System Center Configuration Manager とは独立してコンピューター証明書を展開する証明書のインストール方法の場合、証明書のサブジェクト値を一意にする必要があります。 たとえば、コンピューターの FQDN を指定します。<br /><br /> [サブジェクトの別名] フィールドはサポートされません。<br /><br /> SHA-2 ハッシュ アルゴリズムがサポートされています。<br /><br /> サポートされるキーの最大長は 2048 ビットです。|この証明書は、管理ポイントや配布ポイントなど、モバイル デバイス クライアントが通信するサイト システム サーバーに対して、Mac クライアント コンピューターを認証します。|  
|Linux および UNIX クライアント コンピューター|クライアント認証|**ワークステーション認証**|[拡張キー使用法] の値には「 クライアント認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。2)」をご覧ください。<br /><br /> [サブジェクトの別名] フィールドはサポートされません。<br /><br /> 秘密キーはエクスポートできる必要があります。<br /><br /> SHA-2 ハッシュ アルゴリズムは、クライアントオペレーティング システムが SHA-2 をサポートしている場合にサポートされます。 詳しくは、「[System Center Configuration Manager での Linux コンピューターおよび UNIX コンピューターへのクライアント展開の計画](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)」の「[SHA-256 をサポートしていない Linux および UNIX オペレーティング システムについて](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256)」セクションを参照してください。<br /><br /> サポートされるキーの長さ: 2048 ビット。<br /><br /> **注:** これらの証明書は Distinguished Encoding Rules (DER) encoded binary X.509 形式である必要があります。 Base64 encoded X.509 形式はサポートされません。|この証明書は、管理ポイントや配布ポイントなど、モバイル デバイス クライアントが通信するサイト システム サーバーに対して、Mac クライアント コンピューターを認証します。 この証明書は、公開キー証明書標準 (PKCS #12) 形式でエクスポートする必要があります。パスワードは、PKI 証明書を指定するときにクライアントに指定できるように既知である必要があります。<br /><br /> 詳しくは、「[System Center Configuration Manager での Linux コンピューターおよび UNIX コンピューターへのクライアント展開の計画](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)」の「[Linux および UNIX サーバーのセキュリティと証明書の計画](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_SecurityforLnU)」セクションを参照してください。|  
|- 次のシナリオで使用されるルート証明機関 (CA) 証明書:<br /><br /> - オペレーティング システムの展開<br /><br /> - モバイル デバイスの登録<br /><br /> - Intel AMT ベース コンピューターの RADIUS サーバー認証<br /><br /> - クライアント証明書認証|信頼できる発行元への証明書チェーン|該当なし。|標準のルート CA 証明書。|ルート CA 証明書は、クライアントが通信するサーバーの証明書を、信頼できる発行元にチェーンする必要があるときに指定する必要があります。 これは、次のようなシナリオに適用されます。<br /><br /> - オペレーティング システムを展開して、HTTPS を使用するように構成された管理ポイントにクライアント コンピューターを接続するタスク シーケンスを実行するとき。<br /><br /> - System Center Configuration Manager で管理されるようにモバイル デバイスを登録するとき。<br /><br /> - AMT ベースのコンピューターに対して 802.1X 認証を使用し、RADIUS サーバーのルート証明書用のファイルを指定するとき。<br /><br /> さらに、管理ポイント証明書を発行した CA 階層とは別の CA 階層によって、クライアント証明書が発行された場合は、クライアントのルート CA 証明書の提供が必要になります。|  
|Intel AMT ベースのコンピューター|サーバー認証|**Web サーバー** (変更済み)<br /><br /> **[Active Directory の情報から構築する]**で [サブジェクト名] を構成して、 **[サブジェクト名の形式]** で **[共通名]**を選択する必要があります。<br /><br /> 帯域外管理コンポーネントのプロパティで指定したユニバーサル セキュリティ グループに、 **読み取り** と **登録** の権限を付与する必要があります。|[拡張キー使用法] の値には「 サーバー認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。1)」をご覧ください。<br /><br /> サブジェクト名は、AMT ベース コンピューターの FQDN を含んでいる必要があります。これは Active Directory Domain Services によって自動的に提供されます。|この証明書は、コンピューターの管理コントローラーに搭載された不揮発性 RAM に格納され、Windows ユーザー インターフェイスからは参照できません。<br /><br /> Intel AMT ベースの各コンピューターは、AMT プロビジョニング中、およびその後の更新中にこの証明書を要求します。 これらのコンピューターから AMT プロビジョニング情報を削除すると、この証明書は失効します。<br /><br /> この証明書を Intel AMT ベースのコンピューターにインストールすると、ルート CA への証明書チェーンもインストールされます。 AMT ベースのコンピューターは、キーの長さが 2048 ビットを超える CA 証明書をサポートできません。<br /><br /> 証明書を Intel AMT ベースのコンピューターにインストールすると、AMT ベースのコンピューターは、この証明書によって、帯域外サービス ポイント サイト システム サーバーと帯域外管理コンソールを実行しているコンピューターに対して認証されます。また、Transport Layer Security (TLS) を使用して、これらのコンピューター間のデータ転送がすべて暗号化されます。|  
|Intel AMT 802.1X クライアント証明書|クライアント認証|**ワークステーション認証**<br /><br /> **[Active Directory の情報から構築する]**で [サブジェクト名] を構成し、 **[サブジェクト名の形式]** で **[共通名]**を選択して、DNS 名を消去し、サブジェクトの別名として [ユーザー プリンシパル名 (UPN)] を選択してください。<br /><br /> 帯域外管理コンポーネントのプロパティで指定したユニバーサル セキュリティ グループに、証明書テンプレートに対する **読み取り** と **登録** の権限を付与する必要があります。|[拡張キー使用法] の値には「 クライアント認証 (1」をご覧ください。3」をご覧ください。6」をご覧ください。1」をご覧ください。5」をご覧ください。5」をご覧ください。7」をご覧ください。3」をご覧ください。2)」をご覧ください。<br /><br /> サブジェクト名フィールドは、AMT ベース コンピューターの FQDN を含んでいる必要があります。また、サブジェクトの別名は UPN を含んでいる必要があります。<br /><br /> サポートされるキーの最大長: 2048 ビット。|この証明書は、コンピューターの管理コントローラーに搭載された不揮発性 RAM に格納され、Windows ユーザー インターフェイスからは参照できません。<br /><br /> Intel AMT ベースの各コンピューターは、AMT プロビジョニング中にこの証明書を要求しますが、AMT プロビジョニング情報が削除されたときに、この証明書を失効させません。<br /><br /> 証明書が AMT ベースのコンピューターにインストールされると、この証明書によって AMT ベースのコンピューターが RADIUS サーバーに対して認証され、その後でそのコンピューターによるネットワーク アクセスが認証されます。|  
|Microsoft Intune で登録されるモバイル デバイス|クライアント認証|該当なし: この証明書は Intune で自動作成されます。|[拡張キー使用法] の値には「クライアント認証 (1.3.6.1.5.5.7.3.2)」が含まれます。<br /><br /> 3 つのカスタム拡張機能で、ユーザーの Intune サブスクリプションが一意に識別されます。<br /><br /> ユーザーは登録時に証明書のサブジェクト値を指定できます。 ただし、この値は Intune がデバイスを識別するときに使用されません。<br /><br /> キーのサイズは 2,048 ビットであり、SHA-1 ハッシュ アルゴリズムを使用します。<br /><br /> **注:** この設定は変更できません。この情報は参考のためにのみ提供されます。|認証済みユーザーが Microsoft Intune を使用して自分のモバイル デバイスを登録すると、この証明書が自動的に要求され、インストールされます。 デバイスの結果の証明書はコンピューター ストアに保存され、Intune で管理できるように、登録されたモバイル デバイスを Intune に対して認証するために使用されます。<br /><br /> 証明書にはカスタム拡張機能があるため、認証は、この組織用に設定されている Intune サブスクリプションに制限されます。|



<!--HONumber=Nov16_HO1-->

