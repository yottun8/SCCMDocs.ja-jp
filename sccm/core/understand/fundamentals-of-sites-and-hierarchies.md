---
title: "サイトおよび階層の基礎 | System Center Configuration Manager"
description: "System Center Configuration Manager サイトと階層の基本情報について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 07e10ead8d4b147a4a96b1e5189597e1ac4d4f52


---
# <a name="fundamentals-of-sites-and-hierarchies-for-system-center-configuration-manager"></a>System Center Configuration Manager のサイトおよび階層の基礎

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 展開は、Active Directory ドメインにインストールする必要があり、その基盤はサイトの階層を形成する 1 つ以上の Configuration Manager サイトです。 1 つのサイトからマルチサイト階層まで、インストールするサイトの種類と場所では、必要に応じて展開をスケールアップ (拡張) して、キー サービスを管理されているユーザーとデバイスに配信できます。

## <a name="hierarchies-of-sites"></a>サイトの階層
System Center Configuration Manager を初めてインストールするときに最初にインストールする Configuration Manager サイトによって、階層のスコープが決まります。これは、社内のデバイスとユーザーを管理する基礎となります。 この最初のサイトは、中央管理サイトまたはスタンドアロンのプライマリ サイトのいずれかです。  

 **中央管理サイト**は大規模な展開に適しています。中央管理サイトは、管理の中心点となり、グローバルなネットワーク インフラストラクチャ全体に配布されるデバイスの柔軟なサポートを可能にします。 中央管理サイトのインストール後に、子サイトとして 1 つまたは複数のプライマリ サイトをインストールする必要があります。  これは、プライマリ サイトの機能であるデバイス管理は中央管理サイトによって直接サポートされないためです。 中央管理サイトは複数の子プライマリ サイトをサポートします。管理対象デバイスがさまざまな地理的な場所にある場合に、管理者は子プライマリ サイトを使用して、デバイスを直接管理したり、ネットワーク帯域幅を制御したりします。  

 **スタンドアロン プライマリ サイト**は小規模な展開に適しています。追加サイトをインストールせずにデバイスを管理するには、スタンドアロン プライマリ サイトを使用できます。 スタンドアロン プライマリ サイトは、展開のサイズを制限できますが、後で新しい中央管理サイトをインストールすることによって階層を拡張するシナリオもサポートします。 このサイト拡張シナリオで、スタンドアロン プライマリ サイトが子プライマリ サイトになったら、管理者は新しい中央管理サイトの下に追加の子プライマリ サイトをインストールできます。  この方法で、初期の展開を会社の将来の成長に合わせて拡張できます。  

> [!TIP]  
>  スタンドアロン プライマリ サイトと子プライマリ サイトは実際には同じ種類のサイト、つまりプライマリ サイトです。 名前の違いは、中央管理サイトも使用する場合に作成される階層関係に基づいています。  また、この階層関係では、Configuration Manager の機能を拡張する特定のサイト システムの役割のインストールを制限することもできます。 特定のサイト システムの役割は、階層の最上位層サイト、中央管理サイト、またはスタンドアロン プライマリ サイトのみにインストールできるからです。  

 最初のサイトをインストールした後に、追加サイトをインストールできます。  最初のサイトが中央管理サイトの場合は、1 つまたは複数の子プライマリ サイトをインストールできます。  プライマリ サイト (スタンドアロンまたは子プライマリ) をインストールした後に、1 つまたは複数のセカンダリ サイトをインストールできます。  

 **セカンダリ サイト** はプライマリ サイトの下に子サイトとしてのみインストールできます。 このサイトの種類は、プライマリ サイトへのネットワーク接続が低速な場所のデバイスを管理するために、プライマリ サイトの範囲を拡張します。   セカンダリ サイトによってプライマリ サイトが拡張されても、クライアントは引き続きプライマリ サイトによって管理されます。 セカンダリ サイトは、ネットワーク経由でクライアントに送信 (展開) される情報とクライアントからサイトに返信される情報を圧縮して、情報の転送を管理することにより、離れた場所のデバイスをサポートします。  

 次の図に、サイト設計のいくつかの例を示します。  

 ![階層の例](media/Hierarchy_examples.png)  

 詳細については、以下のトピックを参照してください。  

-   [System Center Configuration Manager の概要](../../core/understand/introduction.md)  

-   [System Center Configuration Manager のサイト階層の設計](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [System Center Configuration Manager サイトをインストールする](/sccm/core/servers/deploy/install/installing-sites)  

## <a name="site-system-servers-and-site-system-roles"></a>サイト システム サーバーとサイト システムの役割  
 各 Configuration Manager サイトは、管理操作をサポートする**サイト システムの役割**をインストールします。  **サイト サーバー**の役割 (サイトをインストールするコンピューターに割り当てられる) や、サイト データベース サーバーの役割 (サイト データベースをホストする SQL Server に割り当てられる) など、一部の役割はサイトのインストール時に既定でインストールされます。 その他のサイト システムの役割は、オプションであり、サイト システムの役割によって有効になる機能の使用時にのみ使用されます。  サイト システムの役割をホストするコンピューターは、サイト システム サーバーと呼ばれます。  

 Configuration Manager の小規模展開の初期には、すべてのサイト システムの役割をサイト サーバーのコンピューターで直接実行することがあります。 その後に、管理対象環境が拡大して、要件が増えたら、増加するデバイスにサービスを提供するサイトの効率を改善するために、追加のサイト システム サーバーをインストールして、追加のサイト システムの役割をホストできます。  

 さまざまなサイト システムの役割については、「[System Center Configuration Manager のサイト システム サーバーとサイト システムの役割の計画](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)」の「[サイト システムの役割](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)」を参照してください  

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Active Directory ドメイン サービスへのサイト情報の発行  
 Configuration Manager の管理を簡素化するには、Configuration Manager で使用される詳細情報をサポートするように Active Directory スキーマを拡張してから、サイトのキー情報が Active Directory Domain Services (AD DS) に公開されるようにします。 これにより、管理対象コンピューターが AD DS の信頼されたソースからサイト関連情報を安全に取得できるようになります。 クライアントが取得できる情報は、使用可能なサイト、サイト システム サーバー、およびそれらのサイト システム サーバーが提供するサービスを識別します。  

 **Active Directory スキーマの拡張**は、フォレストごとに 1 回だけ実行され、Configuration Manager のインストールの前または後に実行できます。   スキーマを拡張するときには、クライアントが検索するデータを公開する Configuration Manager サイトを含む各ドメインで、**System Management** という名前の新しい Active Directory コンテナーを作成する必要があります。 詳細については、「[System Center Configuration Manager 向けに Active Directory スキーマを拡張する](../../core/plan-design/network/extend-the-active-directory-schema.md)」を参照してください。  

 **サイト データの発行**は、Configuration Manager 階層のセキュリティを強化して、管理オーバーヘッドを削減しますが、基本的な Configuration Manager 機能には必要ありません。  



<!--HONumber=Nov16_HO1-->


