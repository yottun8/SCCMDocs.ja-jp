---
title: "ハードウェア インベントリ | System Center Configuration Manager"
description: "System Center Configuration Manager のハードウェア インベントリの概要について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6a0addd31f6e8cd7ef91303cc664d9242c22e0f2


---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager のハードウェア インベントリの概要

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のハードウェア インベントリを使用して、組織内のクライアント デバイスのハードウェア構成に関する情報を収集することができます。 ハードウェア インベントリを収集するには、クライアント設定で [クライアントのハードウェア インベントリを有効にする] を有効にする必要があります。 ****  

 ハードウェア インベントリが有効化され、ハードウェア インベントリ サイクルが実行された後、クライアントは収集したインベントリ情報をクライアント サイトの管理ポイントに送信します。 インベントリ情報は、さらに管理ポイントによって Configuration Manager サイト サーバーに転送され、ここでサイト データベースに保存されます。 ハードウェア インベントリは、クライアント設定で指定されたスケジュールに従って、クライアントに対して実行されます。  

 Configuration Manager が収集するハードウェア インベントリ データは、各種の方法で見ることができます。 リポジトリには、次のものが含まれます。  

-   特定のハードウェア構成に基づいたデバイスを返すクエリを作成する。 詳細については、「[Configuration Manager のクエリ](../../../../core/servers/manage/queries-technical-reference.md)」を参照してください。  

-   特定のハードウェア構成に基づいたクエリベースのコレクションを作成する。 クエリベースのコレクションのメンバーシップは、スケジュールに従って自動的に更新されます。 コレクションは、ソフトウェアの展開など各種のタスクに使用できます。 詳細については、「[Configuration Manager のコレクション](../../../../core/clients/manage/collections/collections-technical-reference.md)」を参照してください。  

-   組織内のハードウェア構成に関する特定の詳細情報を表示するレポートを実行する。 詳細については、「[System Center Configuration Manager のレポート](../../../../core/servers/manage/reporting.md)」を参照してください。  

-   リソース エクスプローラーを使用して、クライアント デバイスから収集された、ハードウェア インベントリに関する詳細情報を表示する。 詳細については、「[System Center Configuration Manager でリソース エクスプローラーを使用してハードウェア インベントリを表示する方法](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)」を参照してください。  

 ハードウェア インベントリをクライアント デバイス上で実行するときは、最初に返されるインベントリ レポートは必ず、完全なインベントリとなります。 その後のインベントリ情報は差分のデルタ インベントリ情報のみを含みます。 サイト サーバーは受け取った順番に、デルタ インベントリ情報を処理します。 クライアントに関するデルタ インベントリ情報がない場合は、サイト サーバーはその後のデルタ インベントリ情報を拒否し、クライアントに完全インベントリ サイクルを実行するように指示します。  

 Configuration Manager のデュアル ブート コンピューターに対するサポートは限定的です。 Configuration Manager でデュアル ブート コンピューターを検出することはできますが、返す情報はインベントリ実行時にアクティブだったオペレーティング システムのインベントリ情報のみです。  

> [!NOTE]  
>  Linux および UNIX を実行しているクライアントでハードウェア インベントリを使用する方法については、「[Hardware inventory for Linux and UNIX in System Center Configuration Manager](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)」(System Center Configuration Manager における Linux および UNIX のハードウェア インベントリ) を参照してください。  

## <a name="extending-configuration-manager-hardware-inventory"></a>Configuration Manager のハードウェア インベントリの拡張  
 Configuration Manager に組み込まれたハードウェア インベントリに加えて、次の方法のうちの 1 つを使用して、ハードウェア インベントリを拡張し、追加の情報を収集することができます。  

|メソッド|説明|  
|------------|-----------------|  
|Configuration Manager コンソールにインベントリ クラスを追加したり、削除したりします。|Configuration Manager では、Configuration Manager コンソールから、ハードウェア インベントリのインベントリ クラスを有効化、無効化したり、追加や削除を行うことができます。|  
|NOIDMIF ファイル|NOIDMIF ファイルは、Configuration Manager ではインベントリできないクライアント デバイスに関する情報を収集するために使用します。 たとえば、デバイス上にラベルとしてのみ存在するデバイス資産番号情報を収集できます。 NOIDMIF のインベントリは、収集元のクライアント デバイスに自動的に関連付けられます。|  
|IDMIF ファイル|IDMIF ファイルは、プロジェクター、複写機、ネットワーク プリンターなどの、Configuration Manager クライアントに関連付けられていない組織内の資産に関する情報を収集するために使用します。|  

 これらの方法を使用して Configuration Manager ハードウェア インベントリを拡張する方法については、「[How to configure hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)」(System Center Configuration Manager でハードウェア インベントリを構成する方法) を参照してください。  



<!--HONumber=Nov16_HO1-->


