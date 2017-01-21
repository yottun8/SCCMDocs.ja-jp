---
title: "サイト データベースの計画 | Microsoft Docs"
description: "System Center Configuration Manager の階層を計画するとき、サイト データベースとサイト データベース サーバーの役割を考える必要があります。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 012d5b313487640faeebe5b49064c74d41a7edb9


---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>System Center Configuration Manager のサイト データベースの計画

*適用対象: System Center Configuration Manager (Current Branch)*

サイト データベース サーバーとは、サポートされている Microsoft SQL Server のバージョンを実行し、Configuration Manager サイトの情報を格納するコンピューターです。 Configuration Manager 階層内の各サイトには、サイト データベースと、サイト データベース サーバーの役割を持つサーバーがあります。  

-   中央管理サイトとプライマリ サイトでは、SQL Server をサイト サーバーにインストールすることも、サイト サーバー以外のサーバーにインストールすることもできます。  

-   一方、セカンダリ サイトでは、SQL Server の完全版の代わりに SQL Server Express を使えるものの、データベース サーバーは、セカンダリ サイト サーバーで実行されていなければなりません。  

リモート データベース サーバーのコンピューターを使用する場合は、介在するネットワーク接続が可用性の高い広帯域のネットワーク接続であることを確認します。 これは、サイト サーバーとサイト システムの役割のいくつかは、サイト データベースをホストしている SQL Server と継続的に通信する必要があるからです。  


**リモート データベース サーバーの場所を決めるときは、次のことに注意してください。**  

-   データベース サーバーとの通信に必要な帯域幅は、サイトとクライアントの構成によって異なります。そのため、実際に必要な帯域幅を的確に予想することはできません。  

-   SMS プロバイダーを実行し、サイト データベースに接続するコンピューターが多いほど、必要なネットワーク帯域幅が大きくなります。  

-   SQL Server を実行するコンピューターは、サイト サーバー、および SMS プロバイダーを実行しているすべてのコンピューターとの双方向の信頼関係があるドメインになければなりません。  

-   サイト データベースとサイト サーバーを併置する場合は、クラスター化された SQL Server をサイト データベース サーバーにすることはできません。  


通常、1 つのサイト システム サーバーには、1 つの Configuration Manager サイトだけの役割を割り当てます。しかし、SQL Server クラスターのインスタンスごと、またはクラスター化されていない SQL Server のインスタンスごとに、異なる Configuration Manager サイトのデータベースをホストするように構成することができます。 この場合は、SQL Server の各インスタンスが、通信用に別々のポートを使用するように構成する必要があります。  


**次の SQL Server 構成を使用して、サイト データベースをホストできます。**  

-   SQL Server の既定のインスタンス  

-   SQL Server を実行している 1 台のコンピューターの名前付きインスタンス  

-   SQL Server のクラスター化されたインスタンスの名前付きインスタンス  

-   SQL Server AlwaysOn 可用性グループ (バージョン 1602 以降)


**サイト データベースの前提条件:**  

-   サイト データベースをホストするには、SQL Server が「[System Center Configuration Manager の SQL Server バージョンのサポート](../../../core/plan-design/configs/support-for-sql-server-versions.md)」に記載されている要件を満たしている必要があります。  



<!--HONumber=Dec16_HO3-->


