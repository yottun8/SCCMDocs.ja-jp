---
title: 探索方法の選択
titleSuffix: Configuration Manager
description: 使用する方法とそれらを実行するサイトの選択に関する考慮事項を確認します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0eec065c9b5d4f75e6a66260760ba08e7bb2c481
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422557"
---
# <a name="select-discovery-methods-to-use-for-system-center-configuration-manager"></a>System Center Configuration Manager に使用する探索方法の選択

*適用対象:System Center Configuration Manager (Current Branch)*

Center Configuration Manager の探索を正常かつ効率的に使用するには、使用する方法とそれらを実行するサイトについて検討する必要があります。  

 探索によって大量のネットワーク トラフィックが発生し、生成された探索データ レコード (DDR) の処理に大量の CPU リソースが消費される可能性があるので、目的に合った探索方法だけを使用してください。 始めは 1 つまたは 2 つの探索方法だけを使用するようにして、後で追加的な方法を慎重に有効にして、環境での探索レベルを拡張してください。 このトピックの情報は、情報に基づいて判断するのに役立ちます。  

 各探索方法の詳細については、「[System Center Configuration Manager の探索方法について](../../../../core/servers/deploy/configure/about-discovery-methods.md)」を参照してください。  

## <a name="select-methods-to-discover-different-things"></a>使用する探索方法の決定  
 Configuration Manager で管理することになるクライアント コンピューターやユーザー リソースを見つけるには、適切な探索方法を有効にしなければなりません。 さまざまな探索方法を使って、各種リソースと、そのリソースに関する他の情報を見つけることができます。 使用する探索方法によって、検出されるリソースの種類、および探索プロセスで使用される Configuration Manager サービスとエージェントが決まります。 また、リソースに関するどのような情報を検出できるかも、探索方法によって異なります。  

### <a name="discover-computers"></a>コンピュータの検出   
コンピューターを見つけたい場合は、**Active Directory システム探索**、または**ネットワーク探索**を使用できます。  

 たとえば、Configuration Manager クライアントをプッシュ インストールする前に、クライアントをインストール可能なリソースを見つけるために、Active Directory システムの探索を実行します。 この方法を使用すると、リソースだけでなく、リソースの基本的な情報と、Active Directory ドメイン サービスにある、リソースの詳しい情報を検出することもできます。 この情報は、クライアント設定の割り当てやコンテンツの展開で使用する複雑なクエリとコレクションを構築するのに便利です。

または、ネットワーク探索でリソースのオペレーティング システム (後でクライアントをプッシュ インストールするときに必要) を検出するオプションを指定してから、探索を実行することもできます。 ネットワーク探索では、他の探索方法では見つからないネットワーク トポロジの情報を得ることができます。 ただし、この方法では、Active Directory 環境に関する情報は何も得られません。

 **定期探索**と呼ばれる方法もあります。 定期探索だけを使って、プッシュ方式以外の方法でインストールされたクライアントを見つけることも可能です。 ただし、他の探索方法とは異なり、定期探索では、アクティブな Configuration Manager クライアントのないコンピューターを見つけることはできません。 そのレコードの基礎ではなく、既存のデータベース レコードを維持するための情報の限られたセットが返されます。 したがって、定期探索で返された情報は、複雑なクエリやコレクションの構築用には不十分な場合があります。  

 **Active Directory グループの探索**方法で、特定のグループのメンバーシップを探索するときに、システムまたはコンピューターの限られた情報を検出することができます。 これは、コンピューターの完全な探索の代わりにはなりませんが、基本的な情報を得ることができます。 ただし、この情報は、クライアントのプッシュ インストール用に使うのには不十分です。  

### <a name="discover-users"></a>ユーザーを探索する   
ユーザーに関する情報を見つけたい場合は、**Active Directory ユーザー探索**を使用します。 Active Directory システム探索と同様に、この方法は、Active Directory からユーザーを検出します。 これには拡張された Active Directory 情報だけでなく、基本的な情報も含まれています。 この情報は、前述したコンピューターの探索の場合と同じように、複雑なクエリとコレクションを構築するのに使えます。  

### <a name="discover-group-information"></a>グループの情報を探索する   
グループとグループのメンバーシップに関する情報が必要な場合は、**Active Directory グループ探索**を使用できます。 この方法では、セキュリティ グループ用のリソース レコードが作成されます。  

 この探索方法を使って、特定の Active Directory グループを検索し、そのグループ、およびネストされているグループのメンバーを見つけることができます。 また、Active Directory の特定の場所でグループを検索したり、Active Directory ドメイン サービスの特定の場所にある各子コンテナーを繰り返し検索することもできます。  

 この探索方法では、配布グループのメンバーシップを検索することもできます。 ユーザーとコンピューターの両方のグループの関係がわかります。  

 グループを探索するときに、そのメンバーに関する限られた情報を検出することもできます。 ただし、Active Directory システムまたはユーザーの探索方法は置き換えられません。 通常、複雑なクエリやコレクションの構築、またはクライアント プッシュ インストールの基礎として使用するには不十分です。  

### <a name="discover-infrastructure"></a>インフラストラクチャを探索する   
ネットワーク インフラストラクチャを探索する方法には、**Active Directory フォレスト探索**と**ネットワーク探索**の 2 通りあります。  

 Active Directory フォレストの探索では、Active Directory のフォレストで、サブネットと Active Directory サイトの構成に関する情報を検索します。 これらの構成は、Configuration Manager に、境界の場所として自動的に挿入されます。  

 ネットワーク トポロジを検出したい場合は、ネットワーク探索方法を使います。 他の探索方法では、Active Directory Domain Services に関係のある情報が返され、クライアントのネットワークでの現在の場所が識別されますが、ネットワークのサブネットやルーターのトポロジに基づいたインフラストラクチャの情報は返されません。  

##  <a name="bkmk_shared"></a> 探索データは複数のサイトで共有される  
 探索データがいったん Configuration Manager のデータベースに挿入されると、すぐに階層内のすべてのサイトで共有されます。 一般的に階層内の複数のサイトで同じ情報を検出しても意味がないので、1 つの探索方法を 1 つのサイトで実行するように設定することを検討してください。 その方が、1 つの方法の複数のインスタンスを異なる複数のサイトで実行するよりも有効です。  

 ただし、環境によっては、同じ方法の探索をサイトごとに別々の構成とスケジュールにして、複数のサイトで定期的に実行すると便利な場合があります。 たとえば、ネットワーク探索を使用するときに、WAN 経由ですべてのネットワークの場所の検出を実行する代わりに、各サイトがローカルネットワークを検出するように指定することができます。

同じ探索方法の複数のインスタンスを異なるサイトで実行するように構成しない場合は、各サイトの構成を慎重に計画します。 複数のサイトでネットワークまたは Active Directory から同じリソースを探索することを避ける必要があります。 これにより、追加のネットワーク帯域幅が消費され、重複する DDR が作成されます。

次の表に、探索方法ごとに実行可能な場所を示します。  

|探索方法|実行可能な場所|  
|----------------------|-------------------------|  
|Active Directory フォレストの探索|中央管理サイト<br /><br /> プライマリ サイト|  
|Active Directory グループの探索|プライマリ サイト|  
|Active Directory システムの探索|プライマリ サイト|  
|Active Directory ユーザー検出|プライマリ サイト|  
|定期探索<sup>1</sup>|プライマリ サイト|  
|ネットワーク探索|プライマリ サイト<br /><br /> セカンダリ サイト|  

 <sup>1</sup> セカンダリ サイトでは定期探索を実行できませんが、クライアントから定期探索の DDR を受信することはできます。  

 セカンダリ サイトでネットワーク探索を実行するか、定期探索の DDR を受信すると、DDR がファイルベースのレプリケーションによって、その親プライマリ サイトに転送されます。 これは、DDR を処理できるのは、プライマリ サイトと中央管理サイトだけだからです。 DDR がどのように処理されるかについては、「[探索データ レコードについて](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs)」を参照してください。  

## <a name="considerations-for-different-discovery-methods"></a>さまざまな探索方法に関する考慮事項  
 各サイト サーバーおよびネットワーク環境が異なるため、探索の初期構成を制限することをお勧めします。 その後で、各サイト サーバーで生成される探索データを処理する機能を厳密に監視します。  

**Active Directory** システムの探索、Active Directory ユーザーの探索、または Active Directory グループの探索方法を使用する場合:  

-   ドメイン コントローラーと高速ネットワークで接続されているサイトで実行します。  

-   Active Directory のレプリケーション トポロジを確認し、探索時に最新の情報にアクセスできるようにします。  

-   探索のスコープを構成して、検出する必要のある Active Directory の場所とグループだけが探索されるようにします。  

**ネットワーク探索**を使用する場合:  

-   初めてネットワーク探索を実行するときは、ネットワーク トポロジだけが識別されるように構成します。  

-   ネットワーク トポロジを検出したら、もっと詳しく探索したい領域の中央に位置する特定のサイトで、ネットワーク探索を実行します。  

**定期探索**では、実行するサイトを指定しないので、実行場所の計画をたてるときに考慮する必要はありません。  

##  <a name="bkmk_best"></a> 探索のベスト プラクティス  
探索で最適な結果を得るために、次のことをお勧めします。

- **[Active Directory グループの探索] を実行する前に [Active Directory システムの探索] および [Active Directory ユーザーの探索] を実行する**  

  [Active Directory グループの探索] で、グループのメンバーとして以前に探索されていないユーザーまたはコンピューターが特定されるときに、そのユーザーまたはコンピューターの基本情報の探索が試行されます。 [Active Directory グループの探索] はこの種類の探索用に最適化されていないため、このプロセスによって実行速度が低下する可能性があります。 さらに、[Active Directory グループの探索] では、ユーザーおよびコンピューターに関する基本情報のみが探索され、完全なユーザーまたはコンピューターの探索レコードは作成されません。 [Active Directory システムの探索] および [Active Directory ユーザーの探索] を実行すると、オブジェクトの種類ごとに追加の Active Directory 属性を使用できます。 結果として、[Active Directory グループの探索] がより効率的に実行されます。  

- **[Active Directory グループの探索] を設定する場合、Configuration Manager で使用するグループのみを指定する**  

  [Active Directory グループの探索] でリソースの使用を制御するには、Configuration Manager で使用する Active Directory グループのみを指定します。 これは、[Active Directory グループの探索] が、ユーザー、コンピューター、および入れ子のグループについて、探索する各グループを再帰的に検索するためです。 入れ子の各グループの検索で [Active Directory グループの探索] の範囲を拡張できますが、パフォーマンスは低下します。 さらに、[Active Directory グループの探索] で差分探索を設定すると、この探索方法では、各グループの変更が監視されます。 この方法では、不要なグループを検索する必要があるときに、パフォーマンスがさらに低下します。  

- **完全探索は長い間隔、差分探索は短い頻度で探索方法を設定する**  

  差分探索は完全探索サイクルよりも使用リソースが少なく、Active Directory で新規または変更されたリソースを特定できるため、完全探索サイクルの頻度を 1 週間に 1 度以下に減らすことができます。 [Active Directory システムの探索]、[Active Directory ユーザーの探索]、および [Active Directory グループの探索] の差分探索によって、Active Directory オブジェクトのほぼすべての変更が特定されます。また、リソースの正確な探索データが維持されます。  

- **Active Directory ドメイン コントローラーに最も近いネットワークの場所にあるプライマリ サイトで Active Directory の探索方法を実行する**  

  Active Directory の探索のパフォーマンスを改善するには、ドメイン コントローラーに対する高速なネットワーク接続があるプライマリ サイトで探索を実行することが推奨されます。 複数のサイトで同じ Active Directory の探索方法を実行する場合、重複を防ぐように各探索方法を設定してください。 これまでのバージョンの Configuration Manager とは異なり、探索データは複数のサイトで共有されます。 そのため、複数のサイトで同じ情報を探索する必要はありません。 詳細については、「[探索データは複数のサイトで共有される](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared)」を参照してください。  

- **探索データから境界を自動的に作成する予定の場合は、1 つのサイトでのみ [Active Directory フォレストの探索] を実行する**  

  階層内の複数のサイトで [Active Directory フォレストの探索] を実行する場合、1 つのサイトで境界を自動的に作成するオプションのみを有効にすることが推奨されます。 [Active Directory フォレストの探索] は各サイトで実行し、境界を作成するため、Configuration Manager ではこのような境界を 1 つの境界オブジェクトに結合できません。 複数のサイトで境界を自動的に作成するように [Active Directory フォレストの探索] を構成すると、Configuration Manager コンソールで境界オブジェクトが重複する結果になる可能性があります。  
