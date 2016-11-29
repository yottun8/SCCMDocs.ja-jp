---
title: "仮想化のサポート | System Center Configuration Manager"
description: "仮想化環境で System Center Configuration Manager クライアントとサイト システムの役割をインストールするための要件を取得します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: be32ccee17bc4829888d42dfff3f2818f4fc2810


---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>System Center Configuration Manager の仮想環境のサポート

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager は、次に示す仮想環境内でバーチャル マシンとして実行するサポート対象オペレーティング システムに、クライアントの役割およびサイト システムの役割をインストールすることをサポートしています。 このサポートは、バーチャル マシンのホスト (仮想環境) が、クライアントまたはサイト サーバーとしてサポートされていない場合でも存続します。  

 **たとえば**、Microsoft Hyper-V Server 2012 を使用して、Windows Server 2012 を実行するバーチャル マシンをホストする場合は、そのバーチャル マシン (Windows Server 2012) にクライアントの役割またはサイト システムの役割をインストールできますが、それらをホスト (Microsoft Hyper-V Server 2012) にインストールすることはできません。  

|仮想化環境|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|  

 使用する各バーチャル コンピューターのハードウェアおよびソフトウェア構成は、物理的な Configuration Manager のコンピューターに使用する構成と同じか、それ以上にする必要があります。  

 サーバー仮想化検証プログラムと、そのオンライン版の Virtualization Program Support Policy ウィザードを使用すると、Configuration Manager が仮想化環境をサポートしているかどうか検証できます。 サーバー仮想化検証プログラムの詳細については、「[Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx)」(Windows サーバーの仮想化検証プログラム) を参照してください。  

> [!NOTE]  
>  Configuration Manager では、Mac 上で実行されるバーチャル PC またはバーチャル サーバー ゲスト オペレーティング システムはサポートしていません。  

Configuration Manager では、バーチャル マシンがオンラインでない限り、そのマシンを管理できません。 ホスト コンピューター上の Configuration Manager クライアントを使用して、オフラインのバーチャル マシン イメージを更新したり、インベントリを収集したりすることはできません。  

バーチャル マシンについて特別に考慮する事項はありません。 たとえば、更新が適用されたバーチャル マシンの状態を保存せずにバーチャル マシンを停止して再起動した場合、Configuration Manager はバーチャル マシン イメージに更新を再適用する必要があるかどうかを判断できない可能性があります。  

##  <a name="a-namebkmkazurea-microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Microsoft Azure 仮想マシン  
 Configuration Manager は、物理的な企業ネットワーク内でオンプレミス実行する場合と同様に、Microsoft Azure の仮想マシンでの実行がサポートされます。 Microsoft Azure の仮想マシンでは、次のシナリオで Configuration Manager を使用できます。  

-   **シナリオ 1:** Microsoft Azure 仮想マシンで Configuration Manager を実行し、それを使用して他の Microsoft Azure 仮想マシンにインストールされたクライアントを管理することができます。  

-   **シナリオ 2:** Microsoft Azure 仮想マシンで Configuration Manager を実行し、それを使用して Microsoft Azure で実行されていないクライアントを管理することができます。  

-   **シナリオ 3:** Microsoft Azure 仮想マシンで複数の Configuration Manager サイト システムの役割を実行しながら、(通信のための適切なネットワーク接続がある) 物理的な企業ネットワークで他の役割を実行することができます。  

ネットワーク、サポート構成、ハードウェアには、物理的な企業ネットワークにオンプレミスで Configuration Manager をインストールするときと同じ System Center Configuration Manager の要件が、Microsoft Azure へのインストールにも適用されます。  

> [!IMPORTANT]  
>  Azure 仮想マシンで実行している Configuration Manager サイトおよびクライアントには、オンプレミス インストールと同じライセンス要件が課されます。  



<!--HONumber=Nov16_HO1-->


