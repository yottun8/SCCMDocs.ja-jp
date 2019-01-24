---
title: サイト サーバーの非推奨機能
titleSuffix: Configuration Manager
description: Configuration Manager でサポートされなくなったサイト サーバーの製品およびオペレーティング システムについて説明します。
ms.date: 01/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c8ea24e141d0e01512ed81ca96e88f2f0f2d07bc
ms.sourcegitcommit: d5c013a29f53b975fe3a6cb0a41f1e817bd7b235
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54342722"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Configuration Manager サイト サーバーで削除され、非推奨となったもの

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、Configuration Manager サイト サーバーのサポート対象から削除されたか、今後の更新で削除される予定 (非推奨) の製品およびオペレーティング システムについて説明します。 Configuration Manager の使用に影響する可能性のある将来の変更について早期に注意するものです。  

この情報は将来、変更される可能性があります。 非推奨の機能、製品、オペレーティング システムにはここで取り上げられていないものもある可能性があります。  



## <a name="server-os"></a>サーバー OS  

|**オペレーティング システム**|**最初に非推奨と発表**|**サポートの削除** |  
|-|-|-| 
|Windows Server 2008 R2 SP1|2015 年 7 月 10 日| バージョン 1702 <sup>[注 1](#bkmk_note1)</sup>| 
|Windows Server 2008 SP2|2015 年 7 月 10 日|バージョン 1511 <sup>[注 2](#bkmk_note2)</sup>|  

#### <a name="bkmk_note1"></a> 注 1:Windows Server 2008 R2 SP1
Windows Server 2008 R2 SP1 は、サイト サーバーやほとんどのサイト システムの役割に対してサポートされていません。 配布ポイントの役割に対しては、この OS は引き続きサポートされます。 このサポートには、プル配布ポイント、PXE、マルチキャストが含まれます。 

> [!Important]  
> Windows Server 2008 R2 SP1 の延長サポート終了日は、2020 年 1 月 14 日です。 この日以降、Configuration Manager はサイト システムの役割としてこの OS をサポートしません。 

サイト サーバー OS は、Windows Server 2008 R2 から Windows Server 2012 R2 にアップグレードできます。 詳細については、「[Windows Server 2008 R2 を実行するサイト サーバーのオペレーティング システムのインプレース アップグレード](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2)」を参照してください。  


#### <a name="bkmk_note2"></a> 注 2:Windows Server 2008 SP2
Windows Server 2008 SP2 は、サイト サーバーやほとんどのサイト システムの役割に対してサポートされていません。 配布ポイントの役割に対しては、この OS は引き続きサポートされます。 このサポートには、プル配布ポイント、PXE、マルチキャストが含まれます。 

> [!Important]  
> Windows Server 2008 SP2 の延長サポート終了日は、2020 年 1 月 14 日です。 この日以降、Configuration Manager はサイト システムの役割としてこの OS をサポートしません。  



## <a name="sql-server"></a>SQL Server   

|**SQL Server バージョン**|**最初に非推奨と発表**|**サポートの削除**|   
|-|-|-| 
|SQL Server 2008 R2|2015 年 7 月 10 日|バージョン 1702| 
|SQL Server 2008|2015 年 7 月 10 日|バージョン 1511|  


使用している SQL Server のバージョンをアップグレードする必要がある場合は、次の方法 (簡単な方法から順に示されています) を使用することをお勧めします。

1. [SQL Server をインプレースでアップグレードします](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (推奨)。  

2. 新しいコンピューターに新バージョンの SQL Server をインストールします。 次に、Configuration Manager セットアップの[データベースの移動オプションを使用](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration)し、サイト サーバーを新しい SQL Server にポイントします。  

3. [バックアップと回復](/sccm/protect/understand/backup-and-recovery)を使用します。  



## <a name="more-information"></a>説明

詳細については、以下の記事を参照してください。 

- [削除と非推奨](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)  

- [マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)  

- [Configuration Manager の Current Branch バージョンのサポート](/sccm/core/servers/manage/current-branch-versions-supported)  

