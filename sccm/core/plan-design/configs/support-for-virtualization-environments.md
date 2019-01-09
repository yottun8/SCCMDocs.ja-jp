---
title: 仮想化のサポート
titleSuffix: Configuration Manager
description: 仮想化環境で System Center Configuration Manager クライアントとサイト システムの役割をインストールするための要件を取得します。
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec7db94635bcc03b21392db19eb668917f38de6d
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417219"
---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>System Center Configuration Manager の仮想環境のサポート

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager は、この記事で説明する仮想環境内で仮想マシンとして実行するサポート対象オペレーティング システムに、クライアントの役割およびサイト システムの役割をインストールすることをサポートしています。 このサポートは、バーチャル マシンのホスト (仮想環境) が、クライアントまたはサイト サーバーとしてサポートされていない場合でも存続します。  

 たとえば、Microsoft Hyper-V Server 2012 を使用して、Windows Server 2012 を実行する仮想マシンをホストする場合は、その仮想マシン (Windows Server 2012) にクライアントの役割またはサイト システムの役割をインストールできますが、それらをホスト (Microsoft Hyper-V Server 2012) にインストールすることはできません。  


|            仮想化環境             |
|---------------------------------------------------|
|              Windows Server 2008 R2               |
|         Microsoft Hyper-V Server 2008 R2          |
|                Windows Server 2012                |
|           Microsoft Hyper-V Server 2012           |
|              Windows Server 2012 R2               |
|   Windows Server 2016 <sup>(「*注 1*」を参照してください)</sup>   |
| Microsoft Hyper-V Server 2016 <sup>(「*注 1*」を参照してください) |

-  *注 1*:Configuration Manager は、Windows Server 2016 の新機能である[入れ子の仮想化](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/what-s-new-in-hyper-v-on-windows#a-namebkmknestedanested-virtualization-new)をサポートしていません。


 使用する各バーチャル コンピューターのハードウェアおよびソフトウェアの要件は、物理的な Configuration Manager のコンピューターに使用する構成と同じか、それ以上にする必要があります。  

 サーバー仮想化検証プログラムと、そのオンライン版の Virtualization Program Support Policy ウィザードを使用すると、Configuration Manager が仮想化環境をサポートしているかどうか検証できます。 サーバー仮想化検証プログラムの詳細については、「[Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx)」(Windows サーバーの仮想化検証プログラム) を参照してください。  

> [!NOTE]  
>  Configuration Manager では、Mac コンピューター上で実行されるバーチャル PC またはバーチャル サーバー ゲスト オペレーティング システムはサポートしていません。  

Configuration Manager では、仮想マシンがオンラインでない限り、そのマシンを管理できません。 ホスト コンピューター上の Configuration Manager クライアントを使用して、オフラインの仮想マシン イメージを更新したり、インベントリを収集したりすることはできません。  

バーチャル マシンについて特別に考慮する事項はありません。 たとえば、更新が適用された仮想マシンの状態を保存せずに仮想マシンを停止して再起動した場合、Configuration Manager は仮想マシン イメージに更新を再適用する必要があるかどうかを判断できない可能性があります。  

##  <a name="bkmk_Azure"></a> Microsoft Azure 仮想マシン  
 Configuration Manager は、物理的な企業ネットワーク内のオンプレミスで実行されるコンピューターと同じように、Azure の仮想マシンで実行できます。 Azure Virtual Machines では、次のシナリオで Configuration Manager を使用できます。  

-   **シナリオ 1 :** Azure Virtual Machines で Configuration Manager を実行し、それを使用して他の Azure Virtual Machines にインストールされたクライアントを管理することができます。  

-   **シナリオ 2 :** Azure Virtual Machines で Configuration Manager を実行し、それを使用して Azure で実行されていないクライアントを管理することができます。  

-   **シナリオ 3:** Azure Virtual Machines で複数の Configuration Manager サイト システムの役割を実行しながら、(通信のための適切なネットワーク接続がある) 物理的な企業ネットワークで他の役割を実行することができます。  

ネットワーク、サポート構成、ハードウェアには、物理的な企業ネットワークにオンプレミスで Configuration Manager をインストールするときと同じ System Center Configuration Manager の要件が、Azure Virtual Machines へのインストールにも適用されます。  

詳細については、「[Azure の Configuration Manager - よく寄せられる質問](/sccm/core/understand/configuration-manager-on-azure)」を参照してください。

> [!IMPORTANT]  
>  Azure Virtual Machines で実行している Configuration Manager サイトおよびクライアントには、オンプレミス インストールと同じライセンス要件が課されます。  
