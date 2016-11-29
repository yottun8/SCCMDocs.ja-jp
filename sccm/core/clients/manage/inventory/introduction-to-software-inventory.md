---
title: "ソフトウェア インベントリ | System Center Configuration Manager"
description: "System Center Configuration Manager のソフトウェア インベントリの概要について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8d664616e222119f7821a70a7c8f9cdbfca38538


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager のソフトウェア インベントリの概要

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のソフトウェア インベントリを使用して、組織内のクライアント デバイスに格納されているファイルに関する情報を収集します。 また、ソフトウェア インベントリはクライアント デバイスからファイルを収集し、サイト サーバーに格納することができます。 ソフトウェア インベントリは、クライアント設定で [クライアントのソフトウェア インベントリを有効にする] が、有効になっているときに収集されます。 ****  

 ソフトウェア インベントリが有効化され、クライアントがソフトウェア インベントリを実行した後で、クライアントはインベントリ情報をクライアント サイトの管理ポイントに送信します。 インベントリ情報は、さらに管理ポイントによって Configuration Manager サイト サーバーに転送され、ここでサイト データベースに保存されます。 ソフトウェア インベントリは、クライアント設定で指定されたスケジュールに従って、クライアントに対して実行されます。  

 Configuration Manager が収集するソフトウェア インベントリ データは、各種の方法で表示することができます。 リポジトリには、次のものが含まれます。  

-   デバイス上で検出される、指定されたファイルを使用するデバイスを返すクエリを作成する。 詳細については、「[Configuration Manager のクエリ](../../../../core/servers/manage/queries-technical-reference.md)」を参照してください。  

-   デバイス上で検出される、指定されたファイルを使用する、クエリベースのコレクションを作成する。 クエリベースのコレクションのメンバーシップは、スケジュールに従って自動的に更新されます。 コレクションは、ソフトウェアの展開など各種のタスクに使用できます。 詳細については、「[Configuration Manager のコレクション](../../../../core/clients/manage/collections/collections-technical-reference.md)」を参照してください。  

-   組織内のデバイス上のファイルに関する特定の詳細情報を表示するレポートを実行する。 詳細については、「[System Center Configuration Manager のレポート](../../../../core/servers/manage/reporting.md)」を参照してください。  

-   リソース エクスプローラーを使用して、クライアント デバイスから収集され、インベントリされたファイルに関する詳細情報を表示する。 詳細については、「[How to use Resource Explorer to view software inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)」(System Center Configuration Manager でリソース エクスプローラーを使用してソフトウェア インベントリを表示する方法) を参照してください。  

 ソフトウェア インベントリをクライアント デバイス上で実行するときは、最初に返されるインベントリ レポートは必ず、完全なインベントリとなります。 その後のインベントリ レポートは差分のデルタ インベントリ情報のみを含みます。 サイト サーバーは受け取った順番に、デルタ インベントリ情報を処理します。 クライアントに関するデルタ インベントリ情報がない場合は、サイト サーバーはその後のデルタ インベントリ情報を拒否し、クライアントに完全なインベントリ サイクルを実行するように指示します。  

 Configuration Manager のデュアル ブート コンピューターに対するサポートは限定的です。 Configuration Manager でデュアル ブート コンピューターを検出することはできますが、返す情報はインベントリ実行時にアクティブだったオペレーティング システムのインベントリ情報のみです。  

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Microsoft Intune に登録されているモバイル デバイスのソフトウェア インベントリ  
 モバイル デバイスにインストールされているアプリのインベントリを収集できます。 インベントリに収集されるアプリは、デバイスが会社所有か個人所有かによって異なります。 個人用デバイスの場合、インベントリに収集されるアプリは、Microsoft Intune で管理されているアプリのみです。  

> [!NOTE]  
>  モバイル デバイスにインストールされているアプリのインベントリが、Configuration Manager のハードウェア インベントリ プロセスの一部として収集されます。 詳細については、「[Configuration Manager と Microsoft Intune で登録されたモバイル デバイスのハードウェア インベントリを構成する方法](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md)」を参照してください。  

 次の表は、個人所有のデバイスまたは会社所有のデバイスに対してインベントリされるアプリの一覧を示しています。  

|プラットフォーム|個人所有のデバイス|会社所有のデバイス|  
|--------------|---------------------------------|--------------------------------|  
|Windows 8.1 (Configuration Manager クライアントを使用しない)|管理対象アプリのみ|管理対象アプリのみ|  
|Windows Phone 8|管理対象アプリのみ|管理対象アプリのみ|  
|Windows RT|管理対象アプリのみ|管理対象アプリのみ|  
|iOS|管理対象アプリのみ|デバイスにインストールされているすべてのアプリ|  
|Android|管理対象アプリのみ|デバイスにインストールされているすべてのアプリ|  



<!--HONumber=Nov16_HO1-->


