---
title: "System Center Configuration Manager でのセキュリティの計画"
description: "System Center Configuration Manager のセキュリティのベスト プラクティスとその他の情報を取得する。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
caps.latest.revision: 6
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f38d7275a39d16f9e6cf90334a46668fcc860bc1


---
# <a name="plan-for-security-in-system-center-configuration-manager"></a>System Center Configuration Manager でのセキュリティの計画

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、System Center Configuration Manager のセキュリティの計画について説明します。  

   Configuration Manager による証明書と暗号化の管理の使用の詳細については、「[System Center Configuration Manager の暗号化コントロールのテクニカル リファレンス](../../../protect/deploy-use/cryptographic-controls-technical-reference.md)」を参照してください。  


##  <a name="a-namebkmkplanningforcertificatesa-planning-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> 証明書の計画 (自己署名および PKI)  
 Configuration Manager は、自己署名入り証明書と公開キー基盤 (PKI) 証明書の組み合わせを使用します。  

 セキュリティの運用方法として、できるかぎり PKI 証明書を使用することをお勧めします。 PKI 証明書の要件の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../../core/plan-design/network/pki-certificate-requirements.md)」を参照してください。 モバイル デバイスの登録中や AMT プロビジョニング中などに Configuration Manager が PKI 証明書を要求する場合、Active Directory Domain Services およびエンタープライズ証明機関を使用する必要があります。 他のすべての PKI 証明書の場合、Configuration Manager とは別にそれらの証明書を展開および管理する必要があります。  

 PKI 証明書は、クライアント コンピューターがインターネットベースのサイト システムに接続するときにも要求されるため、インターネット インフォメーション サービス (IIS) を実行しているサイト システムにクライアントが接続する場合は PKI 証明書を使用することをお勧めします。 クライアント通信の詳細については、「[System Center Configuration Manager でのクライアント通信ポートの構成方法](../../../core/clients/deploy/configure-client-communication-ports.md)」を参照してください。  

 PKI を使用するときは、IPsec も使用して、サイト内および異なるサイト間のサイト システムのサーバー同士の通信や、他のコンピューター間でデータを転送する場合にセキュリティで保護することができます。 IPsec は、Configuration Manager とは別に構成および実装する必要があります。  

 Configuration Manager では、PKI 証明書が使用できない場合、自己署名入り証明書を自動的に作成できます。また、Configuration Manager の一部の証明書は常に自己署名が入っています。 ほとんどの場合、Configuration Manager で自己署名入り証明書が自動的に管理されるため、他の操作を行う必要はありません。 考えられる 1 つの例外は、サイト サーバー署名証明書です。 サイト サーバー署名証明書は常に自己署名が入っているため、管理ポイントからクライアントがダウンロードするクライアント ポリシーがサイト サーバーから送信されたものであり、改ざんされていないことが保証されます。  

### <a name="planning-for-the-site-server-signing-certificate-self-signed"></a>サイト サーバー署名証明書の計画 (自己署名)  
 クライアントは、Active Directory ドメイン サービスおよびクライアント プッシュ インストールからサイト サーバー署名証明書のコピーを安全に取得できます。 これらのメカニズムのいずれかを使用してクライアントがサイト サーバー署名証明書のコピーを取得できない場合、セキュリティ運用方法として、クライアントのインストール時にサイト サーバー署名証明書のコピーをインストールすることをお勧めします。 これは、クライアントとサイトの最初の通信がインターネットからの場合に特に重要です。管理ポイントが信頼されていないネットワークに接続されることから、攻撃の危険にさらされるためです。 この追加の手順を実行しないと、管理ポイントからクライアントにサイト サーバー署名証明書のコピーが自動的にダウンロードされます。  

 次のような場合は、クライアントがサイト サーバー署名証明書のコピーを安全に取得できません。  

-   クライアントをクライアント プッシュでインストールしておらず、次のいずれかの条件が当てはまる。  

    -   Active Directory スキーマが Configuration Manager 用に拡張されていない。  

    -   クライアントのサイトが Active Directory Domain Services に発行されていない。  

    -   クライアントが、信頼されていないフォレストまたはワークグループに属している。  

-   クライアントがインターネット上にあるときに、クライアントをインストールしている。  

クライアントと共にサイト サーバー署名証明書のコピーをインストールするには、次の手順に従います。  

##### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>クライアントと共にサイト サーバー署名証明書のコピーをインストールするには  

1.  クライアントのプライマリ サイト サーバーで、サイト サーバー署名証明書を見つけます。 証明書は、 **SMS** 証明書ストアに保存されています。サブジェクト名は **Site Server** 、フレンドリ名は **Site Server Signing Certificate**です。  

2.  秘密キーなしに証明書をエクスポートし、ファイルを安全な場所に保存し、このファイルにはセキュリティで保護されたチャネルからのみアクセスします (SMB 署名や IPsec を使用するなど)。  

3.  Client.msi のプロパティ **SMSSIGNCERT=***&lt;フル パスおよびファイル名\>* と CCMSetup.exe を使用して、クライアントをインストールします。  

###  <a name="a-namebkmkplanningforcrlsa-planning-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> PKI 証明書失効の計画  
PKI 証明書を Configuration Manager で使用する場合、接続するコンピューターの証明書をクライアントとサーバーが証明書失効リスト (CRL) を使用して検証する方法、およびクライアントとサーバーがその方法で検証するかどうかを計画します。 証明書失効リスト (CRL) は証明機関 (CA) が作成して署名したファイルであり、これには発行後に失効した証明書のリストが含まれます。 CA 管理者は、発行した証明書が侵害された場合、または侵害が疑われる場合などに、証明書を失効できます。  

> [!IMPORTANT]  
>  CRL の場所は、CA が証明書を発行したときに証明書に追加されるため、Configuration Manager で使用する PKI 証明書を展開する前に CRL を計画してください。  

既定では、IIS では常にクライアント証明書の CRL がチェックされ、Configuration Manager でこの構成を変更することはできません。 既定では、Configuration Manager クライアントは常にサイト サーバーの CRL をチェックしますが、サイト プロパティを設定し、CCMSetup プロパティを指定して、この設定を無効にすることができます。 帯域外の Intel AMT 搭載コンピューターを管理している場合、帯域外サービス ポイントの CRL チェック、および帯域外管理コンソールを実行しているコンピューターの CRL チェックを有効にすることもできます。  

コンピューターが証明書の失効確認を使用していても、CRL を検出できない場合、コンピューターは、証明書がリストにないことを確認できないので、証明チェーンのすべての証明書が失効しているかのように動作します。 この場合は、証明書が必要な、CRL を使用するすべての接続が失敗します。  

証明書を使用するたびに CRL を確認すると、失効した証明書の使用に対するセキュリティが高くなりますが、接続が遅くなり、クライアントで別の処理が発生します。 このような追加のセキュリティ チェックは、クライアントがインターネットまたは信頼されていないネットワーク上にある場合に必要になる可能性が高いです。  

CRL を Configuration Manager クライアントでチェックするかどうかを決める前に、PKI 管理者と相談してから、次の両方の条件が当てはまる場合、Configuration Manager でこのオプションを有効にすることを考慮してください。  

-   PKI インフラストラクチャが CRL サポートをしており、すべての Configuration Manager が検出可能な場所に CRL が公開されている。 インターネットベースのクライアント管理を使用しており、クライアントが信頼されていないフォレストに含まれている場合、この条件にはインターネット上のクライアントが含まれる可能性があります。  

-   PKI 証明書を使用するように構成されているサイト システムに接続するたびに CRL を確認する必要性が、クライアントの高速接続および効率的な処理の必要性より高く、クライアントが CRL を検出できない場合にサーバーに接続できないリスクより高い。  

###  <a name="a-namebkmkplanningforrootcasa-planning-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> PKI 信頼されたルート証明書と証明書発行者リストの計画  
IIS サイト システムで HTTP 経由のクライアント認証または HTTPS 経由のクライアント認証と暗号化に PKI クライアント証明書を使用する場合、ルート CA 証明書をサイト プロパティとしてインポートする必要があります。 次の 2 通りの方法があります。  

-   Configuration Manager を使用してオペレーティング システムを展開し、管理ポイントで HTTPS クライアント接続のみを受け入れる。  

-   管理ポイントによって信頼されているルート証明機関 (CA) 証明書にチェーンされない、PKI クライアント証明書を使用する。  

    > [!NOTE]  
    >  管理ポイントに使用するサーバー証明書を発行するのと同じ CA 階層からクライアント PKI 証明書を発行する場合、このルート CA 証明書を指定する必要はありません。 ただし、複数の CA 階層を使用しており、それらの階層が相互に信頼関係にあるかどうかが不明な場合は、クライアントの CA 階層用にルート CA をインポートします。  

Configuration Manager 用にルート CA 証明書をインポートする必要がある場合は、発行元の CA またはクライアント コンピューターからルート CA 証明書をエクスポートします。 証明書をエクスポートする発行元の CA がルート CA でもある場合、秘密キーがエクスポートされていないことを確認します。 改ざんを防ぐため、エクスポートした証明書ファイルを安全な場所に保存します。 サイトを構成するときにこのファイルにアクセスできる必要があるため、ネットワーク経由でファイルにアクセスする場合は、SMB 署名または IPsec を使用して通信が改ざんから保護されていることを確認します。  

インポートしたルート CA 証明書のいずれかが更新された場合、更新された証明書をインポートする必要があります。  

これらのインポートしたルート CA 証明書および各管理ポイントのルート CA 証明書では、証明書発行者リストが作成され、Configuration Manager コンピューターで次のように使用されます。  

-   クライアントが管理ポイントに接続すると、管理ポイントは、クライアント証明書がサイトの証明書発行者リストの信頼されたルート証明書にチェーンされていることを確認します。 チェーンされていない場合、証明書が拒否されて、PKI 接続は失敗します。  

-   クライアントは、PKI 証明書を選択するときに証明書発行者リストがある場合、証明書発行者リストの信頼されたルート証明書にチェーンされている証明書を選択します。 一致するものがない場合、クライアントは PKI 証明書を選択しません。 クライアント証明書の処理の詳細については、このトピックの「 [Planning for PKI client certificate selection](#BKMK_PlanningForClientCertificateSelection) 」を参照してください。  

モバイル デバイスまたは Mac コンピューターを登録する際、および Intel AMT 搭載コンピューターをワイヤレス ネットワーク用にプロビジョニングする際に、サイト構成とは関係なく、ルート CA 証明書をインポートすることが必要になる場合があります。  

###  <a name="a-namebkmkplanningforclientcertificateselectiona-planning-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> Planning for PKI client certificate selection  
 IIS サイト システムで、HTTP 経由のクライアント認証または HTTPS 経由のクライアント認証と暗号化に PKI クライアント証明書を使用する場合、Configuration Manager に対して使用する証明書を、Windows ベースのクライアントが選択する方法を計画します。  

> [!NOTE]  
>  すべてのデバイスで証明書の選択方法がサポートされるわけではなく、その場合、証明書の条件を満たす最初の証明書が自動的に選択されます。 たとえば、Mac コンピューターのクライアントやモバイル デバイスでは、証明書の選択方法がサポートされません。  

ほとんどの場合、既定の構成と動作で十分です。 Windows ベースのコンピューターの Configuration Manager クライアントは、次の条件を使用して複数の証明書をフィルタリングします。  

1.  証明書発行者リスト: 証明書が管理ポイントによって信頼されているルート CA に至るまでチェーンされている。  

2.  証明書が既定の証明書ストア [個人用] に保存されている。 ****  

3.  証明書が有効であり、失効しておらず、期限切れになっていない。 有効性の確認には、秘密キーがアクセスできること、および Configuration Manager と互換性がないバージョン 3 の証明書テンプレートを使用して証明書が作成されないことの検証が含まれます。  

4.  証明書にクライアント認証機能がある、または証明書がコンピューター名に対して発行されている。  

5.  証明書に最長の有効期間が設定されている。  

次のメカニズムを使用して証明書発行者リストを使用するように、クライアントを構成できます。  

-   Configuration Manager サイト情報として Active Directory Domain Services に発行されている。  

-   クライアント プッシュを使用してクライアントがインストールされている。  

-   クライアントが、サイトに正常に割り当てられた後に、管理ポイントから証明書の発行元リストをダウンロードする。  

-   クライアントのインストール時に、CCMSetup の client.msi の CCMCERTISSUERS プロパティで証明書の発行元リストを指定する。  

クライアントがまずインストールされ、サイトにまだ割り当てられていないときに、クライアントに証明書の発行元リストがない場合は、クライアントはこのチェックをスキップします。 クライアントに証明書発行者リストがあり、証明書発行者リストの信頼されたルート証明書にチェーンしている PKI 証明書がない場合、証明書の選択は失敗し、他の証明書選択条件を使用してクライアントが選択を続行することはありません。  

ほとんどの場合、Configuration Manager クライアントは、使用する適切な一意の PKI 証明書を正しく識別します。 ただし、そうでない場合、クライアント認証機能に基づいて証明書を選択する方法の代わりに、別の 2 つの選択方法を構成できます。  

-   部分文字列を使用した、クライアント証明書のサブジェクト名との一致。 この方法では大文字小文字を区別しません。サブジェクト フィールドでコンピューターの完全修飾ドメイン名 (FQDN) を使用していて、 **contoso.com**などのドメイン サフィックスに基づいて証明書を選択する場合に便利です。 しかし、この選択方法を使用すれば、クライアントの証明書ストア内で証明書を他の証明書と区別する、証明書のサブジェクト名の任意の連続した文字を識別することができます。  

    > [!NOTE]  
    >  サイト設定のサブジェクトの別名 (SAN) に、部分文字列の照合を指定することはできません。 CCMSetup を使用して SAN の部分文字列の照合を指定できますが、次の場合は、サイトのプロパティによって上書きされます。  
    >   
    >  -   クライアントが、Active Directory ドメイン サービスに発行されているサイト情報を取得する。  
    > -   クライアント プッシュ インストールを使用してクライアントがインストールされている。  
    >   
    >  クライアントを手動でインストールしており、クライアントが Active Directory ドメイン サービスからサイト情報を取得しない場合のみ、SAN で部分文字列の一致を使用してください。 たとえば、これらの条件はインターネットのみのクライアントに当てはまります。  

-   クライアント証明書のサブジェクト名属性値またはサブジェクトの別名 (SAN) 属性値との一致。 この方法では大文字小文字を区別します。RFC 3280 に対応し、X500 識別名または同等の OID (オブジェクト ID) を使用していて、属性値に基づいて証明書を選択したい場合に便利です。 証明書ストアの他の証明書の中から特定の証明書を一意に識別する (検証して選別する) のに必要な属性と値のみを指定できます。  

次の表に、クライアント証明書の選択条件で Configuration Manager がサポートしている属性値を示します。  

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

選択条件を適用すると該当する証明書が複数検出される場合、有効期間が最長の証明書を選択するように既定の構成を上書きして、その代わりに、証明書が選択されていないことを指定できます。 この場合は、クライアントは、PKI 証明書を使用して IIS サイト システムと通信することはできません。 クライアントは、割り当てられたフォールバック ステータス ポイントにエラー メッセージを送信し、証明書の選択に失敗したことを通知します。これにより、証明書選択条件の変更や改善が可能になります。 クライアントの動作は、失敗した接続が HTTPS 経由または HTTP 経由のいずれであるのかによって異なります。  

-   失敗した接続が HTTPS 経由の場合: クライアントは、クライアントの自己署名証明書を使用して HTTP 経由で接続を試みます。  

-   失敗した接続が HTTP 経由の場合: クライアントは、自己署名のクライアント証明書を使用して HTTP 経由で別の接続を試みます。  

一意の PKI クライアント証明書を識別できるように、 **コンピューター** ストア内に既定の [ **個人用** ] 以外のカスタム ストアを指定することもできます。 ただし、このストアは Configuration Manager とは別に作成する必要があります。また、このカスタム ストアに証明書を展開して、有効期間が切れる前に証明書を更新できる必要があります。  

クライアント証明書の設定を構成する方法については、「[System Center Configuration Manager でのセキュリティの構成](../../../core/plan-design/security/configure-security.md)」のトピックの「[クライアント PKI 証明書の設定の構成](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI)」セクションを参照してください。  

###  <a name="a-namebkmkplanningforpkitransitiona-planning-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> PKI 証明書とインターネットベースのクライアント管理の移行戦略の計画  
Configuration Manager の柔軟な構成オプションを使用すると、PKI 証明書を使用するようにクライアントとサイトを徐々に移行して、クライアント エンドポイントをセキュリティで保護することができます。 PKI 証明書を使用すると、セキュリティが向上し、クライアントがインターネット上にあるときにクライアントを管理できます。  

Configuration Manager の構成オプションと選択肢の数のために、すべてのクライアントが HTTPS 接続を使用するようにサイトを移行する方法は 1 つではありません。 ただし、ガイダンスとして、次の手順に従うことができます。  

1.  Configuration Manager サイトをインストールし、サイト システムが HTTPS 経由および HTTP 経由でクライアント接続を受け入れるようにサイトを構成します。  

2.  サイト プロパティの [ **クライアント コンピューターの通信** ] タブで、[ **サイト システム設定** ] が **HTTP または HTTPS**になるように構成し、[ **使用可能な場合は PKI クライアント証明書 (クライアント認証機能) を使用する** ] チェック ボックスをオンします。 このタブで必要な他の設定を構成します。 詳細については、「[System Center Configuration Manager でのセキュリティの構成](../../../core/plan-design/security/configure-security.md)」のトピックの「[クライアント PKI 証明書の設定の構成](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI)」のセクションを参照してください。  

3.  PKI クライアント証明書の展開を試験的に行います。 展開の例については、「[System Center Configuration Manager PKI 証明書の展開手順の例: Windows Server 2008 証明機関](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)」のトピックの「*Windows コンピューター用のクライアント証明書の展開*」セクションを参照してください。  

4.  クライアント プッシュ インストール方法を使用してクライアントをインストールします。 詳細については、「[System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)」のトピックの「[クライアント プッシュを使用した Configuration Manager クライアントのインストール方法](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)」のセクションを参照してください。  

5.  Configuration Manager コンソールのレポートと情報を使用して、クライアントの展開とステータスを監視します。  

6.  [ **資産とコンプライアンス** ] ワークスペースの [ **デバイス** ] ノードで [ **クライアント証明書** ] 列を表示して、クライアント PKI 証明書を使用しているクライアントの数を追跡します。  

     コンピューターに Configuration Manager HTTPS 準備評価ツール (**cmHttpsReadiness.exe**) を展開し、レポートを使用して、Configuration Manager でクライアント PKI 証明書を使用できるコンピューターの数を表示することもできます。  

    > [!NOTE]  
    >  クライアント コンピューターに Configuration Manager クライアントをインストールすると、**cmHttpsReadiness.exe** ツールが *%windir%***\CCM** フォルダーにインストールされます。 このツールをクライアントで実行する際、次のオプションを指定できます。  
    >   
    >  -   /Store:&lt;name\>  
    > -   /Issuers:&lt;list\>  
    > -   /Criteria:&lt;criteria\>  
    > -   /SelectFirstCert  
    >   
    >  これらのオプションは、 **CCMCERTSTORE**、 **CCMCERTISSUERS**、 **CCMCERTSEL**、および **CCMFIRSTCERT** Client.msi プロパティにそれぞれマップされます。 これらのオプションの詳細については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」を参照してください。  

7.  十分な数のクライアントが HTTP 経由での認証にクライアント PKI 証明書を正しく使用している場合は、次の操作を行います。  

    1.  PKI Web サーバー証明書を、サイトの追加の管理ポイントを実行するメンバー サーバーに展開し、この証明書を IIS に構成します。 詳細については、「[System Center Configuration Manager PKI 証明書の展開手順の例: Windows Server 2008 証明機関](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)」のトピックの「*IIS を実行するサイト システム用のWeb サーバー証明書の展開*」のセクションを参照してください。  

    2.  このサーバーに管理ポイントの役割をインストールし、[ **HTTPS** ] の管理ポイントのプロパティで [ **クライアント接続**] オプションを構成します。  

8.  PKI 証明書があるクライアントが HTTPS 経由で新しい管理ポイントを使用していることを、監視および確認します。 IIS ログまたはパフォーマンス カウンターを使用して、これを確認できます。  

9. HTTPS クライアント接続を使用するように、他のサイト システムの役割を再構成します。 インターネット上のクライアントを管理する場合は、サイト システムにインターネット FQDN があることを確認し、インターネットからのクライアント接続を受け入れるように個々の管理ポイントと配布ポイントを構成します。  

    > [!IMPORTANT]  
    >  インターネットからの接続を受け入れるようにサイト システムの役割を構成する前に、インターネットベースのクライアント管理の計画情報と前提条件を確認してください。 詳細については、「[System Center Configuration Manager でのエンドポイント間の通信](../../../core/plan-design/hierarchy/communications-between-endpoints.md)」を参照してください。  

10. 必要に応じて、IIS を実行しているクライアントとサイト システムに PKI 証明書の展開を拡張し、HTTPS クライアント接続とインターネット接続用にサイト システムの役割を構成します。  

11. セキュリティを最大限に高めるため、すべてのクライアントが認証と暗号化にクライアント PKI 証明書を使用している場合は、HTTPS のみを使用するようにサイト プロパティを変更します。  

 この計画に従って PKI 証明書をまず HTTP 経由での認証にのみ導入し、次に HTTPS 経由での認証と暗号化に導入すると、クライアントが管理不能になるリスクが軽減されます。 また、セキュリティを Configuration Manager がサポートしている最大限のレベルにまで高めることができます。  

##  <a name="a-namebkmkplanningforrtka-planning-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> 信頼されたルート キーの計画  
Configuration Manager の信頼されたルート キーは、サイト システムが階層に属していることを Configuration Manager クライアントが確認するメカニズムを提供します。 すべてのサイト サーバーが、他のサイトと通信するためにサイト交換キーを生成します。 階層内の最上位のサイトのサイト交換キーは、信頼されたルート キーと呼ばれます。  

Configuration Manager の信頼されたルート キーの機能は、信頼されたルート キーの秘密キーによって署名されたすべてのものが階層の下位で信頼されるという点で、公開キー基盤のルート証明書に似ています。 たとえば、信頼されたルート キー ペアの秘密キーで管理ポイントの証明書に署名し、クライアントで使用できる信頼されたルート キー ペアの公開キーをコピーすると、クライアントは階層内の管理ポイントと階層内にない管理ポイントを区別できます。 クライアントは、WMI を使用して、信頼されたルート キーのコピーを名前空間 **root\ccm\locationservices**に保存します。  

次の 2 つのメカニズムを使用すると、信頼されたルート キーの公開コピーをクライアントが自動的に取得できます。  

-   Active Directory スキーマが Configuration Manager 向けに拡張されており、サイトが Active Directory Domain Services に公開されており、クライアントがグローバル カタログ サーバーからこのサイト情報を取得できる。  

-   クライアント プッシュを使用してクライアントがインストールされている。  

これらのメカニズムのいずれかを使用して、クライアントが信頼されたルート キーを取得できない場合、クライアントは、通信している最初の管理ポイントが提供する信頼されたルート キーを信頼します。 この場合は、偽の管理ポイントからポリシーを受け取る攻撃者の管理ポイントにクライアントが誘導される可能性があります。 これは、巧妙な攻撃者の操作である可能性が高く、有効な管理ポイントから信頼されたルート キーをクライアントが取得する前の限られた時間内のみに発生することがあります。 ただし、攻撃者がクライアントを偽の管理ポイントに誘導するリスクを軽減するために、信頼されたルート キーをクライアントに事前に準備できます。  

Configuration Manager クライアントに信頼されたルート キーを事前に準備および検証するには、次の手順に従います。  

-   ファイルを使用して信頼されたルート キーをクライアントに事前に準備する  

-   ファイルを使用せずに信頼されたルート キーをクライアントに事前に準備する  

-   クライアントの信頼されたルート キーを検証する  

> [!NOTE]  
>  クライアントが Active Directory ドメイン サービスから信頼されたルート キーを取得できる場合や、クライアント プッシュを使用してクライアントがインストールされている場合は、信頼されたルート キーをクライアントに事前に準備する必要はありません。 また、クライアントが管理ポイントに対して HTTPS 通信を使用している場合、PKI 証明書を使用して信頼が確立されるため、クライアントに事前に準備する必要はありません。  

Client.msi プロパティ **RESETKEYINFORMATION = TRUE** と CCMSetup.exe を共に使用すると、クライアントから信頼されたルート キーを削除できます。 信頼されたルート キーを置き換えるには、クライアント プッシュを使用するか、CCMSetup.exe を使用して Client.msi **SMSPublicRootKey** プロパティを指定し、クライアントを新しい信頼されたルート キーと共に再インストールします。  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a>ファイルを使用して信頼されたルート キーをクライアントに事前に準備するには  

1.  テキスト エディターで、ファイル *&lt;Configuration Manager ディレクトリ\>***\bin\mobileclient.tcf** を開きます。  

2.  エントリ **SMSPublicRootKey=**を検索し、その行のキーをコピーし、変更せずにファイルを閉じます。  

3.  新しいテキスト ファイルを作成し、mobileclient.tcf ファイルからコピーしたキー情報を貼り付けます。  

4.  ファイルを保存して、すべてのコンピューターがアクセスでき、改ざんできないようにファイルがセキュリティで保護される場所に配置します。  

5.  Client.msi プロパティを使用できる任意のインストール方法を使用してクライアントをインストールし、Client.msi プロパティ **SMSROOTKEYPATH=***&lt;フル パスとファイル名\>* を指定します。  

    > [!IMPORTANT]  
    >  クライアントのインストール時にセキュリティを向上するために信頼できるルート キーを指定する場合、Client.msi のプロパティ **SMSSITECODE=&lt;サイト コード\>** を使用して、サイト コードも指定する必要があります。  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a>ファイルを使用せずに信頼されたルート キーをクライアントに事前に準備するには  

1.  テキスト エディターで、ファイル *&lt;Configuration Manager ディレクトリ\>***\bin\mobileclient.tcf** を開きます。  

2.  エントリ SMSPublicRootKey= を検索し、その行のキーを書き留めるかクリップボードにコピーし、変更せずにファイルを閉じます。  

3.  Client.msi プロパティを使用できるインストール方法でクライアントをインストールし、Client.msi プロパティ **SMSPublicRootKey=***&lt;キー\>* を指定します。ここで、*&lt;キー\>* は mobileclient.tcf からコピーした文字列です。  

    > [!IMPORTANT]  
    >  クライアントのインストール時にセキュリティを向上するために信頼できるルート キーを指定する場合、Client.msi のプロパティ **SMSSITECODE=&lt;サイト コード\>** を使用して、サイト コードも指定する必要があります。  

#### <a name="to-verify-the-trusted-root-key-on-a-client"></a>クライアントの信頼されたルート キーを検証するには  

1.  **[スタート]** メニューの **[ファイル名を指定して実行]**をクリックし、「 **Wbemtest**」と入力します。  

2.  [ **Windows Management Instrumentation テスト** ] ダイアログ ボックスで、[ **接続**] をクリックします。  

3.  **[接続]** ダイアログ ボックスで、 **[名前空間]** ボックスに「 **root\ccm\locationservices**」と入力してから、 **[接続]**をクリックします。  

4.  [ **Windows Management Instrumentation テスト** ] ダイアログ ボックスの [ **IWbemServices** ] セクションで、[ **クラスの列挙**] をクリックします。  

5.  [ **スーパークラス情報** ] ダイアログ ボックスで、[ **再帰**] を選択してから [ **OK**] をクリックします。  

6.  [ **クエリ結果** ] ウィンドウで、リストの末尾までスクロールし、[ **TrustedRootKey ()**] をダブルクリックします。  

7.  [ **TrustedRootKey のオブジェクト エディタ** ] ダイアログ ボックスで、[ **インスタンス**] をクリックします。  

8.  新しい [ **クエリ結果** ] ウィンドウに、[ **TrustedRootKey**] のインスタンスが表示されるので、[ **TrustedRootKey=@**  

9. [**TrustedRootKey=@ のオブジェクト エディター**] ダイアログ ボックスの [**プロパティ**] セクションで、[**TrustedRootKey CIM_STRING**] までスクロールダウンします。 右側の列の文字列が信頼されたルート キーです。 この文字列が、*&lt;Configuration Manager ディレクトリ\>***\bin\mobileclient.tcf** ファイルの **SMSPublicRootKey** 値と一致することを確認します。  

##  <a name="a-namebkmkplanningforsigningencryptiona-planning-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> 署名と暗号化の計画  
 すべてのクライアント通信に PKI 証明書を使用する場合は、クライアント データの通信をセキュリティで保護するために、署名と暗号化を計画する必要はありません。 ただし、HTTP クライアント接続を許可するように IIS を実行しているサイト システムを構成する場合は、サイトのクライアント接続をどのようにセキュリティで保護するのかを決める必要があります。  

 管理ポイントにクライアントが送信するデータを保護するために、データに署名することを要求できます。 また、HTTP を使用するクライアントからのすべての署名入りデータが SHA-256 アルゴリズムを使用して署名されるように要求することもできます。 これはより安全な設定ですが、すべてのクライアントが SHA-256 をサポートしているのでない限り、このオプションを有効にしないでください。 多くのオペレーティング システムは SHA-256 をネイティブにサポートしていますが、以前のオペレーティング システムには更新または修正プログラムが必要になる場合があります。 たとえば、Windows Server 2003 SP2 を実行しているコンピューターでは、 [サポート技術情報 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666)に示されている修正プログラムをインストールする必要があります。  

 署名によって改ざんからデータを保護できますが、暗号化によって情報公開からデータを保護できます。 サイト内の管理ポイントにクライアントが送信するインベントリ データと状態メッセージに対して、3DES 暗号化を有効にすることができます。 このオプションをサポートするために、クライアントに更新をインストールする必要はありませんが、暗号化と復号化を実行するためにクライアントと管理ポイントで必要になる、追加の CPU 使用率を考慮してください。  

 署名と暗号化の設定を構成する方法については、「[System Center Configuration Manager でのセキュリティの構成](../../../core/plan-design/security/configure-security.md)」のトピックの「[署名と暗号化の構成](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption)」セクションを参照してください。  

##  <a name="a-namebkmkplanningforrbaa-planning-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> 役割に基づいた管理の計画  
 詳細については、「[System Center Configuration Manager のロール ベース管理の基礎](../../../core/understand/fundamentals-of-role-based-administration.md)」を参照してください。  



<!--HONumber=Nov16_HO1-->


