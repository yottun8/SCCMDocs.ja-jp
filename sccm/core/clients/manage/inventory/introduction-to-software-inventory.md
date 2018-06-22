---
title: ソフトウェア インベントリ
titleSuffix: Configuration Manager
description: System Center Configuration Manager のソフトウェア インベントリの概要について説明します。
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4fe27423391cbdc4767e18a06c73b23cbb302ab5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332512"
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

**モバイル デバイス:** モバイル デバイスにインストールされているアプリのインベントリの収集に関しては、「[Software inventory for mobile devices enrolled with Microsoft Intune (Microsoft Intune に登録されているモバイル デバイスのソフトウェア インベントリ)](../../../../mdm/deploy-use/software-inventory-mobile-devices.md)」を参照してください。
