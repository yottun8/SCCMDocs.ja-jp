---
title: "ソフトウェア インベントリ | Microsoft Docs"
description: "System Center Configuration Manager のソフトウェア インベントリの概要について説明します。"
ms.custom: na
ms.date: 12/26/2016
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
ms.sourcegitcommit: 9206b82eca02877c30eebf146d42bcca7290eb42
ms.openlocfilehash: c9956dd4ef94a1b109d761e44e42f512c42eb8d2


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager のソフトウェア インベントリの概要

*適用対象: System Center Configuration Manager (Current Branch)*

ソフトウェア インベントリを利用し、クライアント デバイスでファイルに関する情報を収集します。 また、ソフトウェア インベントリはクライアント デバイスからファイルを収集し、サイト サーバーに格納することができます。 ソフトウェア インベントリは、クライアント設定で **[クライアントのソフトウェア インベントリを有効にする]** 設定を選択すると収集されます。この設定では、操作をスケジュールすることもできます。  

ソフトウェア インベントリが有効化され、クライアントがソフトウェア インベントリを実行した後で、クライアントは情報をクライアント サイトの管理ポイントに送信します。 インベントリ情報は、さらに管理ポイントによって Configuration Manager サイト サーバーに転送され、そこでサイト データベースに保存されます。   

 ソフトウェア インベントリ データの表示方法:  

-   指定のファイルとデバイスを返す[クエリを作成](../../../../core/servers/manage/queries-technical-reference.md)する。   

-   指定のファイルとデバイスを含む[クエリベース コレクション](../../../../core/clients/manage/collections/introduction-to-collections.md)を作成する。   

-   デバイスでファイルに関する詳細を提供する[レポートを実行](../../../../core/servers/manage/reporting.md)する。 

-   [リソース エクスプローラー](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)を使用して、クライアント デバイスから収集され、インベントリされたファイルに関する詳細情報を表示する。   

 ソフトウェア インベントリをクライアント デバイス上で実行するとき、最初のレポートは完全なインベントリとなります。 その後のレポートは差分のデルタ インベントリ情報のみを含みます。 サイト サーバーは受け取った順番にデルタ情報を処理します。 クライアントに関するデルタ情報がない場合は、サイト サーバーはその後のデルタ情報を拒否し、クライアントに完全インベントリを実行するように指示します。  

 Configuration Manager でデュアル ブート コンピューターを検出することはできますが、返す情報はインベントリ実行時にアクティブだったオペレーティング システムのインベントリ情報のみです。  

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Microsoft Intune に登録されているモバイル デバイスのソフトウェア インベントリ  
 モバイル デバイスにインストールされているアプリのインベントリを収集できます。 インベントリに収集されるアプリは、デバイスが会社所有か個人所有かによって異なります。 個人用デバイスの場合、インベントリに収集されるアプリは、Microsoft Intune で管理されているアプリのみです。  

> [!NOTE]  
>  モバイル デバイスにインストールされているアプリのインベントリが[ハードウェア インベントリ](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md) プロセスの一部として収集されます。  

 個人所有のデバイスまたは会社所有のデバイスのインベントリに次のアプリが収集されます。  

|プラットフォーム|個人所有のデバイス|会社所有のデバイス|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (Configuration Manager クライアントを使用しない)|管理対象アプリのみ|管理対象アプリのみ| 
|Windows 8.1 (Configuration Manager クライアントを使用しない)|管理対象アプリのみ|管理対象アプリのみ|  
|Windows Phone 8|管理対象アプリのみ|管理対象アプリのみ|  
|Windows RT|管理対象アプリのみ|管理対象アプリのみ|  
|iOS|管理対象アプリのみ|デバイスにインストールされているすべてのアプリ|  
|Android|管理対象アプリのみ|デバイスにインストールされているすべてのアプリ|  





<!--HONumber=Dec16_HO5-->


