---
title: "UNIX/Linux クライアントのコンポーネント サービスとコマンド | Microsoft Docs"
description: "System Center Configuration Manager での Linux クライアントおよび UNIX クライアントに対するコンポーネント サービスとコマンドについて説明します。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
caps.latest.revision: "6"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: f11795b05f1b422e97fd32e7457c44b708fa93e4
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2017
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-system-center-configuration-manager"></a>System Center Configuration Manager 用の Linux クライアントおよび UNIX クライアントのコンポーネント サービスとコマンド

*適用対象: System Center Configuration Manager (Current Branch)*


 Linux および UNIX 用 Configuration Manager クライアントのクライアント コンポーネント サービスを次の表に示します。  

|ファイル名|説明|  
|---------------|----------------------|  
|ccmexec.bin|このサービスは、Windows ベースのクライアントの ccmexc サービスに相当します。 Configuration Manager サイト システムの役割とのすべての通信を担当します。また、ローカル コンピューターからハードウェア インベントリを収集するために omiserver.bin サービスとも通信します。<br /><br /> サポートされているコマンド ライン引数を確認するには、 **ccmexec -h**を実行してください。|  
|omiserver.bin|このサービスは、CIM サーバーです。 CIM サーバーでは、プロバイダーと呼ばれるプラグ可能なソフトウェア モジュールのフレームワークを提供します。 プロバイダーは、Linux および UNIX コンピューターのリソースと対話し、ハードウェア インベントリ データを収集します。 たとえば、 **プロセス プロバイダー** Linux のコンピューターは Linux オペレーティング システムのプロセスに関連付けられているデータを収集します。|  

 開始するには、使用できる次のテーブル一覧のコマンドでは、停止、または、Linux または UNIX のバージョンごとに、クライアント サービス (ccmexec.bin および omiserver.bin) を再起動します。 ccmexec サービスを開始または停止すると、omiserver サービスも開始または停止します。  

|オペレーティング システム|コマンド|  
|----------------------|--------------|  
|Universal Agent<br /><br /> RHEL 4 および SLES 9|開始: **/etc/init d/ccmexecd start**<br /><br /> 停止: **/etc/init d/ccmexecd stop**<br /><br /> 再開: **/etc/init d/ccmexecd restart**|  
|Solaris 9|開始: **/etc/init d/ccmexecd start**<br /><br /> 停止: **/etc/init d/ccmexecd stop**<br /><br /> 再開: **/etc/init d/ccmexecd restart**|  
|Solaris 10|開始:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> 停止:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|Solaris 11|開始:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> 停止:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|AIX|開始:<br /><br /> **startsrc -s omiserver**<br /><br /> **startsrc -s ccmexec**<br /><br /> 停止:<br /><br /> **stopsrc -s ccmexec**<br /><br /> **stopsrc -s omiserver**|  
|HP-UX|開始: **/sbin/init.d/ccmexecd start**<br /><br /> 停止: **/sbin/init.d/ccmexecd stop**<br /><br /> 再開: **/sbin/init.d/ccmexecd restart**|  
