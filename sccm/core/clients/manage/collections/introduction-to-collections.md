---
title: "コレクションの概要 | System Center Configuration Manager"
description: "System Center Configuration Manager のコレクションの使用方法について概要を説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
caps.latest.revision: 8
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 47574218dec5069205f9dba5608c6f136fb032bc


---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager のコレクションの概要

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のコレクションを使用すると、管理しやすい単位にリソースを整理して、実行するタスクの種類を論理的に表す構造を作成できます。 コレクションは、一度に複数のリソースに対して Configuration Manager 操作を実行するためにも使用されます。 Configuration Manager でコレクションを使用する方法に関するいくつかの例を次の表に示します。  

|操作|例|  
|---------|-------|  
|リソースのグループ化|組織の階層に基づいた、リソースを論理的にグループ化するコレクションを作成できます。<br /><br /> たとえば、"ロンドン本社" Active Directory 組織単位 (OU) にあるすべてのコンピューターのコレクションを作成することができます。 この種類のコレクションを作成する方法の詳細については、「[Configuration Manager でのコレクションの作成方法](../../../../core/clients/manage/collections/create-collections.md)」を参照してください。<br /><br /> このコレクションを使用して、Endpoint Protection の設定やデバイスの電源管理設定の構成、Configuration Manager クライアントのインストールなどの操作を実行することができます。|  
|アプリケーションの展開|Microsoft Office 2013 がインストールされていないすべてのコンピューターのコレクションを作成し、このソフトウェアをそのコレクションのすべてのコンピューターにインストールすることができます。<br /><br /> アプリケーションの要件を使用してこのタスクを実行することもできます。 詳細については、「[System Center Configuration Manager でアプリケーションを作成する方法](../../../../apps/deploy-use/create-applications.md)」を参照してください。|  
|クライアント設定の管理|Configuration Manager の既定のクライアント設定はすべてのデバイスとすべてのユーザーに適用されますが、デバイスのコレクションまたはユーザーのコレクションに適用されるカスタム クライアント設定を作成することもできます。<br /><br /> たとえば、リモート コントロールを一部のデバイスを除くすべてのデバイスで使用可能にする場合、リモート コントロールを許可するよう既定のクライアント設定を構成し、その後、リモート コントロールを許可しないカスタム クライアント設定を構成することができます。 リモート コントロールを使用しないコンピューターが含まれるコレクションにこれらのカスタム クライアント設定を展開します。<br /><br /> クライアント設定のコレクションの使用方法については、「[Configuration Manager のクライアント設定について](../../../../core/clients/deploy/about-client-settings.md)」を参照してください。|  
|電源管理|作成するコレクションごとに、コレクションのコンピューターが非アクティブになってからスリープ モードになるまでの時間などの電源設定を構成することができます。<br /><br /> コレクションを電源管理に使用する方法の詳細については、「[Introduction to power management](../power/introduction-to-power-management.md)」(電源管理の概要) を参照してください。|  
|役割に基づいた管理|役割ベースの管理にコレクションを使用して、Configuration Manager コンソールの各種機能にアクセスできるユーザーのグループを制御することができます。<br /><br /> ロール ベース管理のコレクションを構成する方法については、「[Configure role-based administration for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md)」(System Center Configuration Manager のロールベース管理の構成) を参照してください。|  
|メンテナンス期間|メンテナンス期間を使用すると、Configuration Manager の各種の操作がデバイス コレクションのメンバーに実行できる期間を管理ユーザーが定義できます。 メンテナンス期間を使用すると、クライアントの構成に対する変更が、組織の生産性に影響しない時間帯に行なわれるようにできます。<br /><br /> メンテナンス期間の詳細については、「[System Center Configuration Manager でメンテナンス期間を使用する方法](../../../../core/clients/manage/collections/use-maintenance-windows.md)」を参照してください。|  

 管理タスクのほとんどは、1 つ以上のコレクションを使用することによって行います。 たとえば、デバイスにソフトウェア更新を展開するには、事前にソフトウェア更新を展開するコレクションを識別しておく必要があります。 組み込みのコレクションである [すべてのシステム] を使用することもできますが、管理タスクでこのコレクションを使用することはお勧めしません。 テスト環境を除くすべての環境で、独自のカスタム コレクションを作成して管理対象のデバイスまたはユーザーをより具体的に識別する方がメリットがあります。  

 組み込みコレクションおよびカスタム コレクションは、Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースの **[ユーザー コレクション]** ノードと **[デバイス コレクション]** ノードに表示されます。  

 最近表示されたコレクションは、Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースの **[ユーザー]** ノードと **[デバイス]** ノードに表示されます。  

## <a name="collection-types-in-configuration-manager"></a>Configuration Manager のコレクションの種類について  
 Configuration Manager には、一般的な操作で使用できるいくつかの組み込みコレクションがあります。 さらに、お客様のビジネス要件に固有のリソースをグループ化する、独自のコレクションを作成できます。  

### <a name="built-in-collections"></a>組み込みコレクション  
 既定では、Configuration Manager は、次の変更できないコレクションを含みます。  

|**コレクション名**|説明|  
|-------------------------|-----------------|  
|**すべてのユーザー グループ**|Active Directory セキュリティ グループの探索を使用して検出されたユーザー グループを含みます。|  
|**すべてのユーザー**|Active Directory ユーザー探索を使用して検出されたユーザーを含みます。|  
|**すべてのユーザーおよびユーザー グループ**|すべてのユーザーとすべてのユーザー グループのコレクションを含みます。 このコレクションは変更できず、ユーザーとユーザー グループのリソースの最大スコープを含みます。|  
|**すべてのデスクトップ クライアントおよびサーバー クライアント**|Configuration Manager クライアントをインストールした、サーバー デバイスとデスクトップ デバイスを含みます。 メンバーシップは、定期探索で保守されます。|  
|**すべてのモバイル デバイス**|Configuration Manager が管理するモバイル デバイスが含まれます。 メンバーシップは、正常にサイトに割り当てられている、あるいは Exchange Server コネクタ によって検出されたモバイル デバイスに制限されます。|  
|**すべてのシステム**|すべてのデスクトップ クライアントおよびサーバー クライアントのコレクション、すべてのモバイル デバイスのコレクション、すべての不明なコンピューターのコレクション、および Microsoft Intune によって登録されているすべてのモバイル デバイスを含みます。<br /><br /> このコレクションは変更できず、デバイス リソースの最大スコープを含みます。|  
|**すべての不明なコンピューター**|複数のコンピューター プラットフォームの一般的コンピューター レコードを含みます。 このコレクションを使用すると、タスク シーケンスと、PXE ブート、起動可能メディア、または事前設定されたメディアを使用して、オペレーティング システムを展開することができます。|  

### <a name="custom-collections"></a>カスタム コレクション  
 Configuration Manager にカスタム コレクションを作成すると、そのコレクションのメンバーシップは 1 つ以上のコレクション ルールによって決定されます。 コレクションの規則を構成する方法については、「[How to create collections in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)」(System Center Configuration Manager でコレクションを作成する方法) を参照してください。 使用できる規則は 4 つです。  

#### <a name="direct-rule"></a>ダイレクト規則  
 ダイレクト規則は、コレクションのメンバーに加えるユーザーまたはコンピューターを選択します。 この規則では、どのリソースがコレクションのメンバーかを直接制御することができます。 このメンバーシップはリソースが Configuration Manager から削除されない限り、自動的に変更されることはありません。 Configuration Manager はリソースを探知するか、ダイレクト規則のコレクションに追加する前にリソースをインポートする必要があります。 ダイレクト規則のコレクションは、コレクションの種類を手動で変更する必要があるため、クエリ規則のコレクションよりも管理オーバーヘッドが高くなります。  

#### <a name="query-rule"></a>クエリ規則  
 クエリ規則は、Configuration Manager がスケジュールに従って実行するクエリに基づいて、コレクションのメンバーシップを動的に更新します。 たとえば、Active Directory ドメイン サービスで人事部のメンバーであるユーザーのコレクションを作成することができます。 ダイレクト規則のコレクションとは異なり、このコレクションのメンバーシップは、人事部に新しいユーザーが追加または削除されると、自動的に更新されます。 クエリ規則は、ダイレクト規則を使用することで、コレクションに手動で追加するというデバイス管理のオーバーヘッドをなくします。 ただし、コレクションに追加されるコンピューターを管理者が細かく制御することがいくらか難しくなります。 クエリ ベースの規則の例として、次のものがあります。  

-   指定された OU のすべてのユーザー  

-   Windows 8 を実行しているすべてのコンピューター  

-   空きディスク領域が 20GB を超えるすべてのコンピューター  

#### <a name="include-collections-rule"></a>コレクションを含める規則  
 [コレクションを含める] 規則を使用すると、Configuration Manager における他のコレクションのメンバーを含めることができます。 含められるコレクションのメンバーシップに変更があった場合、Configuration Manager は現在のコレクションのメンバーシップはスケジュールで更新します。  

#### <a name="exclude-collections-rule"></a>コレクションを除外する規則  
 [コレクションを除外する] 規則を使用すると、Configuration Manager における他のコレクションのメンバーを除外することができます。 除外されるコレクションのメンバーシップに変更があった場合、Configuration Manager は現在のコレクションのメンバーシップはスケジュールで更新します。  

> [!NOTE]  
>  コレクションが、コレクションを含める規則とコレクションを除外する規則の両方を含み、競合が生じた場合は、除外する規則が含む規則を優先します。  

## <a name="incremental-collection-updates"></a>コレクションの増分更新  
 コレクションの増分更新を有効にすると、Configuration Manager は、以前のコレクションの評価から新しいリソースや変更されたリソースがないかどうかを定期的にスキャンして、コレクションのメンバーシップを、更新します。この増分更新は、コレクションの完全な評価とは独立して行われます。 既定では、コレクションの増分更新を有効にすると、5 分間隔でメンバーが更新されます。完全な評価とは異なり、オーバーヘッドを発生させずに、コレクションのデータを最新に保つことができます。  

> [!NOTE]  
>  新しく作成されたコレクションでは、増分更新は、既定で無効になっています。  



<!--HONumber=Nov16_HO1-->


