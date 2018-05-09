---
title: Configuration Manager サイト サーバーで非推奨とされた項目
titleSuffix: Configuration Manager
description: System Center Configuration Manager でサポートされなくなったサイト サーバーの製品およびオペレーティング システムについて説明します。
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b92eb8083ce886fcab4d9957b2a79999d72a1a5a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="removed-and-deprecated-for-system-center-configuration-manager-site-servers"></a>System Center Configuration Manager サイト サーバーから削除された項目と非推奨の項目

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、System Center Configuration Manager サイト サーバーのサポート対象から削除されたか、今後の更新で削除される予定 (非推奨) の製品およびオペレーティング システムについて説明します。 この記事は、Configuration Manager の使用に影響する可能性のある将来の変更について早期に注意するものです。  

この情報は、今後のリリースで変更される可能性があります。また、非推奨の機能、製品、またはオペレーティング システムをすべて記載しているわけではありません。  


## <a name="deprecated-server-operating-systems"></a>非推奨のサーバー オペレーティング システム  

|**オペレーティング システム**|**最初に非推奨と発表**|**サポートの削除** |  
|-|-|-| 
|Windows Server 2008 R2|2015 年 7 月 10 日| バージョン 1702 (注 1 を参照)| 
|Windows Server 2008|2015 年 7 月 10 日|バージョン 1511 </br></br>サイト システムとしてのサポートは削除されています  (注 2 を参照)。|  

>[!NOTE]
>-   バージョン 1702 以降、Windows Server 2008 R2 はサイト サーバーまたはほとんどのサイト システムの役割に対してサポートされません。 ただし、1702 より前のバージョンでは、その使用は引き続きサポートされます。 このサポートの廃止が発表されるまで、またはこのオペレーティング システムの延長サポート期間が終了するまで、配布ポイントのサイト システムの役割 (プル配布ポイント、PXE およびマルチキャストの場合を含む) に対してこのオペレーティング システムは引き続きサポートされます。 バージョン 1602 より、サイト サーバーのオペレーティング システムを Windows Server 2008 R2 から Windows Server 2012 R2 にインプレース アップグレードできます。  
>- サイト サーバーのオペレーティング システムのインプレース アップグレードにについては、「[System Center Configuration Manager をサポートするオンプレミス インフラストラクチャのアップグレード](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)」の「[Windows Server 2008 R2 を実行するサイト サーバーのオペレーティング システムのインプレース アップグレード](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2)」セクションを参照してください。

>[!NOTE]
>-   Windows Server 2008 は、サイト サーバーとして、または配布ポイントとプル配布ポイントを除くサイト システムの役割としてはサポートされていません。 サポートの廃止が発表されるまで、またはこのオペレーティング システムの拡張サポート期間が終了するまでは、このオペレーティング システムを配布ポイントとして使用し続けることができます。 詳細については、「[Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095)」 (Windows Server 2008 で System Center Configuration Manager CB および LTSB のインストールに失敗する) を参照してください。

## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>サイト データベースとしてのサポートが非推奨とされた SQL Server バージョン  

|**SQL Server バージョン**|**最初に非推奨と発表**|**サポートの削除**|   
|-|-|-| 
|SQL Server 2008 R2|2015 年 7 月 10 日|バージョン 1702| 
|SQL Server 2008|2015 年 7 月 10 日|バージョン 1511|  


使用している SQL Server のバージョンをアップグレードする必要がある場合は、次の方法 (簡単な方法から順に示されています) を使用することをお勧めします。
1. [SQL Server をインプレースでアップグレードします](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (推奨)。
2. 新しいコンピューターに新バージョンの SQL Server をインストールします。 次に、Configuration Manager セットアップの[データベースの移動オプションを使用](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration)して、サイト サーバーを新しい SQL Server にポイントします。
3. [バックアップと回復](/sccm/protect/understand/backup-and-recovery)を使用します。


## <a name="more-information"></a>説明
詳細については、次をご覧ください。
 - [削除と非推奨](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - [Microsoft サポート ライフサイクル](https://support.microsoft.com/lifecycle) Web サイト
 - [Configuration Manager の Current Branch バージョンのサポート](/sccm/core/servers/manage/current-branch-versions-supported)