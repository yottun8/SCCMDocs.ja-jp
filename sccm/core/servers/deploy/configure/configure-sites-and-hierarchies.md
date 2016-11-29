---
title: "サイトの構成 | System Center Configuration Manager"
description: "このチェックリストを利用し、サイトと階層の両方に影響を与える最も一般的な構成を考慮してください。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: 15
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 470efc428045398588345f4546eb27831837715c


---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>System Center Configuration Manager のサイトと階層の構成

*適用対象: System Center Configuration Manager (Current Branch)*

最初の System Center Configuration Manager サイトのインストールまたは階層へのサイトの追加後に、次のチェック リストを使用して、サイトと階層の両方に影響する最も一般的な構成を検討しているか確認します。  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>新規および追加のサイト用の一般的な構成のチェック リスト  
 ほとんどの展開では、以下のオプションを特定の順序で構成する必要はありません。  

-   Active Directory フォレストの探索、境界、境界グループなどのように、互いに依存しているオプションもあります。  

-   一部の構成には、当面は構成の変更を必要とせずに使用できる既定値が設定されています。  

-   境界グループや配布ポイント グループなどのその他の構成は、使用前に構成が必要となります。  

|操作|説明|  
|------------|-------------|  
|ロール ベース管理の構成|ロール ベース管理は、Configuration Manager 環境でさまざまなオブジェクトやデータを表示および管理できる管理ユーザーを制御するために、管理の割り当て区分を設定する方法です。<br /><br /> ロール ベース管理の構成は、階層内のすべてのサイトで共有されます。   <br />「[System Center Configuration Manager のロール ベース管理の構成](../../../../core/servers/deploy/configure/configure-role-based-administration.md)」を参照してください|  
|サイト データを Active Directory ドメイン サービス (AD DS) に発行する|サイト データを AD DS に発行すると、クライアントでサービスを検索しやすくなり、サイト リソースを効率的に利用できるようになります。<br /><br /> まず、[System Center Configuration Manager 向けに Active Directory スキーマを拡張し](../../../../core/plan-design/network/extend-the-active-directory-schema.md)、次に、各サイトがそれぞれ [System Center Configuration Manager のサイト データを発行する](../../../../core/servers/deploy/configure/publish-site-data.md)ように構成する必要があります。|  
|サービス接続ポイントを構成する|階層の最上位層で、サービス接続ポイントをインストールおよび構成する計画を作成する必要があります。 詳細については、「[System Center Configuration Manager のサービス接続ポイントについて](../../../../core/servers/deploy/configure/about-the-service-connection-point.md)」を参照してください。|  
|サイト システムの役割を追加する|個々のサイトに追加のサイト システムの役割を 1 つ以上インストールします。  「 [Add site system roles for System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md)」を参照してください。|  
|サイト境界と境界グループを構成する|管理対象のデバイスを含むことができる、イントラネット上のネットワークの場所を定義する境界を指定した後、そのネットワークの場所にあるクライアントで Configuration Manager サービス リソースを検索できるように、境界グループを構成します。 「[System Center Configuration Manager のサイト境界と境界グループの定義](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)」を参照してください|  
|配布ポイント グループを構成する|展開を管理しやすくするために配布ポイントの論理グループを構成します。 「[Install and configure distribution points for System Center Configuration Manager (System Center Configuration Manager の配布ポイントのインストールと構成)](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md)」の「[Manage distribution point groups (配布ポイント グループの管理)](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)」を参照してください。|  
|検出を実行する|検出を実行して、ネットワーク インフラストラクチャ、デバイス、ユーザーなどのネットワーク上のリソースを見つけます。<br /><br /> 「 [Run discovery for System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md)」を参照してください。|  
|インフラストラクチャの管理者向けに冗長性と容量を追加する|追加の SMS プロバイダーと Configuration Manager コンソールをインストールすると、管理者がインフラストラクチャの管理に使用する容量を拡張することができます。<br /><br /> **追加の SMS プロバイダーをインストール** して、サイトや階層を管理するための接続ポイントに冗長性を与えます。 「 [Modify your System Center Configuration Manager 」の「frastructure](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) 」の「 [Modify your System Center Configuration Manager 」の「frastructure](../../../../core/servers/manage/modify-your-infrastructure.md)」を参照してください<br /><br /> **追加の Configuration Manager コンソールをインストール** して、追加の管理ユーザーに対して同時にアクセス許可を与えます。 「[Install Configuration Manager consoles (Configuration Manager コンソールのインストール)](../../../../core/servers/deploy/install/install-consoles.md)」を参照してください|  
|サイト コンポーネントを構成する|各サイトでサイト コンポーネントを構成すると、サイト システムの管理およびサイト ステータス レポートの動作を変更することができます。 「 [Site components for System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md)」を参照してください。|  
|カスタム コレクションを作成する|デバイスとユーザーについて検出された情報を使用し、将来の管理タスクを単純化するために、オブジェクトのカスタム コレクションを作成します。 [「System Center Configuration Manager でコレクションを作成する方法](../../../../core/clients/manage/collections/create-collections.md)」を参照してください|  
|危険度の高い展開を管理するための設定を構成する|管理ユーザーが危険度の高いタスク シーケンスの展開を作成すると警告が表示されるように、サイトの設定を構成します。  「 [Settings to manage high-risk deployments for System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md)」を参照してください。|  
|管理ポイントのデータベース レプリカを構成する|管理ポイントがクライアントからの要求を供給することでサイト データベース サーバーに加えられた CPU 負荷を軽減するように、データベース レプリカを構成します。 「 [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)」を参照してください。|  
|サイト データベースをホストする SQL Server AlwaysOn 可用性グループの構成|バージョン 1602 以降では、プライマリ サイトと中央管理サイトでサイト データベースをホストするための高可用性と障害復旧ソリューションとして可用性グループを構成できます。 「[System Center Configuration Manager の高可用性サイト データベースの SQL Server AlwaysOn](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)」を参照してください|  
|サイト間のレプリケーションを変更する|「[System Center Configuration Manager のサイト間でのデータの転送](../../../../core/servers/manage/data-transfers-between-sites.md)」をご覧になり、次に挙げる事項についてお読みください。<br /><br /> セカンダリ サイト間の [File-based replication](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) を構成する<br /><br /> [Database replication links](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)を構成する<br /><br /> [Distributed views](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)を構成する|  



<!--HONumber=Nov16_HO1-->


