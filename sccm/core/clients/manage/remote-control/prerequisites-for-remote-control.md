---
title: "リモート コントロールの前提条件 | Microsoft Docs"
description: "System Center Configuration Manager のリモート コントロールの前提条件を確認します。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 12c602ddfa237768af497324440091e17e597ae9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-remote-control-in-system-center-configuration-manager"></a>System Center Configuration Manager のリモート コントロールの前提条件

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のリモート コントロールには、外部依存関係と製品内部依存関係があります。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|コンピューター ビデオ カード ドライバー|リモート コントロールのパフォーマンスを最適化するため、最新のビデオ ドライバーがクライアント コンピューターにインストールされていることを確認します。|  

 Windows Embedded、Windows Embedded for Point of Service (POS)、および Windows Fundamentals for Legacy PCs を実行しているデバイスは、リモート コントロール ビューアーをサポートしませんが、リモート コントロール クライアントはサポートします。  

 Configuration Manager のリモート コントロールは、Systems Management Server 2003 または Configuration Manager 2007 を実行しているクライアント コンピューターのリモート管理には使用できません。  

> [!NOTE]  
>  リモート コントロールの外部の依存要素として Windows サービスは不要です。  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>リモート コントロール ビューアーでサポートされるオペレーティング システム  
リモート コントロール ビューアーは、Configuration Manager コンソールでサポートされるすべてのオペレーティング システムでサポートされています。 詳しくは、[System Center Configuration Manager コンソールのサポートされている構成](../../../../core/plan-design/configs/supported-operating-systems-consoles.md)に関する記事をご覧ください。   

## <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|クライアントでリモート コントロールが有効になっている必要があります。|既定では、Configuration Manager をインストールする場合にリモート コントロールは有効化されていません。 電源管理を有効化して構成する方法の詳細については、「[Configuring remote control in System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md)」(System Center Configuration Manager でリモート コントロールを構成する) を参照してください。|  
|レポート サービス ポイント|リモート コントロールに対してレポートを実行するには、事前に Reporting Services ポイント サイト システムの役割がインストールされている必要があります。 詳細については、「[System Center Configuration Manager のレポート](../../../../core/servers/manage/reporting.md)」を参照してください。|  
|リモート コントロールを管理するためのセキュリティのアクセス許可|Configuration Manager コンソールからコレクション リソースにアクセスしてリモート コントロール セッションを開始する場合: **コレクション** オブジェクトに対する **読み取り**、**リソースの読み取り**、**リモート コントロール**のアクセス許可。<br /><br /> [**リモート ツール オペレーター**] セキュリティ ロールには、Configuration Manager でリモート コントロールを管理するのに必要な、これらのアクセス許可が含まれます。<br /><br /> 詳細については、「[Configure role-based administration for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md)」(System Center Configuration Manager の役割ベースの管理の構成) を参照してください。<br /><br /> さらに、許可されたビューアーには、リモート コントロールを使用するアクセス許可を付与する必要があります。この操作を行うには、[**リモート ツール**] クライアント設定の [**リモート コントロールとリモート アシスタンス セッションを表示できるユーザー**] の一覧に該当ユーザーを追加します。
