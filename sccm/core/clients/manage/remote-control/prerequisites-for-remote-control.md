---
title: "リモート コントロールの前提条件 | System Center Configuration Manager"
description: "System Center Configuration Manager のリモート コントロールの前提条件を確認します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5e15fc7359787b40ebd138fd79dd72081dd8fb36


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
 次の表は、リモート コントロール ビューアーでサポートされるオペレーティング システムについて説明します。 サポートされるクライアント オペレーティング システムに関する詳細については、「[System Center Configuration Manager のサポートされている構成](../../../../core/plan-design/configs/supported-configurations.md)」を参照してください。  

|オペレーティング システム|ビューアーのサポート|説明|  
|----------------------|--------------------|----------------------|  
|Windows XP (32 ビット)|○|このオペレーティング システム上でリモート コントロール ビューアーを実行するには、まず Microsoft ダウンロード センターから [リモート デスクトップ接続 (RDC) 7.0 クライアント更新プログラム (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) をダウンロードして、インストールする必要があります。|  
|Windows XP (64 ビット)|×|詳細情報はありません。|  
|Windows Vista (32 ビット)|○|このオペレーティング システム上でリモート コントロール ビューアーを実行するには、まず Microsoft ダウンロード センターから [リモート デスクトップ接続 (RDC) 7.0 クライアント更新プログラム (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) をダウンロードして、インストールする必要があります。|  
|Windows Vista (64 ビット)|○|このオペレーティング システム上でリモート コントロール ビューアーを実行するには、まず Microsoft ダウンロード センターから [リモート デスクトップ接続 (RDC) 7.0 クライアント更新プログラム (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) をダウンロードして、インストールする必要があります。|  
|Windows 7 (32 ビット)|○|詳細情報はありません。|  
|Windows 7 (64 ビット)|○|詳細情報はありません。|  
|Windows Server 2003 (32 ビット)|×|詳細情報はありません。|  
|Windows Server 2003 (64 ビット)|×|詳細情報はありません。|  
|Windows Server 2008 (32 ビット)|×|詳細情報はありません。|  
|Windows Server 2008 (64 ビット)|×|詳細情報はありません。|  
|Windows Server 2008 R2 (64 ビット)|○|詳細情報はありません。|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|クライアントでリモート コントロールが有効になっている必要があります。|既定では、Configuration Manager をインストールする場合にリモート コントロールは有効化されていません。 電源管理を有効化して構成する方法の詳細については、「[Configuring remote control in System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md)」(System Center Configuration Manager でリモート コントロールを構成する) を参照してください。|  
|レポート サービス ポイント|リモート コントロールに対してレポートを実行するには、事前に Reporting Services ポイント サイト システムの役割がインストールされている必要があります。 詳細については、「[System Center Configuration Manager のレポート](../../../../core/servers/manage/reporting.md)」を参照してください。|  
|リモート コントロールを管理するためのセキュリティのアクセス許可|Configuration Manager コンソールからコレクション リソースにアクセスしてリモート コントロール セッションを開始する場合: **コレクション** オブジェクトに対する **AMT の制御**、**読み取り**、**リソースの読み取り**、**リモート コントロール** のアクセス許可<br /><br /> [**リモート ツール オペレーター**] セキュリティ ロールには、Configuration Manager でリモート コントロールを管理するのに必要な、これらのアクセス許可が含まれます。<br /><br /> 詳細については、「[Configure role-based administration for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md)」(System Center Configuration Manager の役割ベースの管理の構成) を参照してください。<br /><br /> さらに、オプションを使用して、リモート_コントロールとリモート アシスタンスをリモート制御の許可されているビューの一覧を使用するためのアクセス許可を付与するユーザーを追加する必要があります **リモート_コントロールとリモート アシスタンスのあるユーザーが許可されている** で、 **リモート ツール** クライアント設定します。|  



<!--HONumber=Nov16_HO1-->


