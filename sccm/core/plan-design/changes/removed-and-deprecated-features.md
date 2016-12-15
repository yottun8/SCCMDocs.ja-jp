---
title: "非推奨の機能 |Microsoft Docs"
description: "System Center Configuration Manager でサポートされなくなった機能、製品、およびオペレーティング システムについて説明します。"
ms.custom: na
ms.date: 12/05/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c899b4beaa2aae4eb609291dca0e23f3c266627a
ms.openlocfilehash: 294166af3d5c6062e3508249c767779876b23931


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>System Center Configuration Manager から削除された機能と非推奨の機能

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、System Center Configuration Manager のサポート対象から削除されたか、今後の更新で削除される予定 (非推奨) の機能、製品、およびオペレーティング システムについて説明します。 これは、Configuration Manager の使用に影響する可能性のある将来の変更について早期に警告することを目的としています。  

 この情報は、今後のリリースで変更される可能性があります。また、非推奨の機能、製品、またはオペレーティング システムをすべて記載しているわけではありません。  

## <a name="how-to-use-this-information"></a>この情報の使用方法  
機能またはオペレーティング システムが非推奨と最初に示されるとき、それは今後の Configuration Manager のバージョンで、それの Configuration Manager での使用がサポートされなくなることを意味します。 この情報は、その機能またはオペレーティング システムの代わりとなるものを計画できるよう、提供しています。  それがサポート対象外となる Configuration Manager の最初のバージョンがリリースされると、そのバージョンを具体的に示すよう、このトピックは更新されます。  

機能またはオペレーティング システムがサポート対象外となった場合でも、前のバージョンのサポート対象の Configuration Manager を使用する場合、その機能またはオペレーティング システムはサポートされます。 ただし、それ以降の日付にリリースされたまたは記載されているバージョンの Configuration Manager を使用する場合、そのバージョンの Configuration Manager ではサポートされません。

**例:** ある機能が 2016年 9 月以降にリリースされる更新プログラムからサポート対象外となる予定の場合、これは、その機能は 2016 年 10 月にリリースされる更新 1610 には含まれないことを意味します。
-  更新 1610 では、この機能はサポートされません。
-  この記事は更新され、バージョン 1610 でサポート対象外となることが明記されます。
ただし、その機能をサポートする 1602 や 1606 などの以前のバージョンを使用する場合、使用しているバージョンがサポート対象外となるまで、その機能は使用し続けられます。

詳細については、次をご覧ください。
 - [マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle) Web サイト
 - [Configuration Manager の Current Branch バージョンのサポート](/sccm/core/servers/manage/current-branch-versions-supported)

**非推奨の機能:**  


|**機能**|**最初に非推奨と発表**|**サポートの削除**|  
|-|-|-|  
|ネットワーク アクセス保護 (NAP) - System Center 2012 Configuration Manager の機能|2015/7/10|バージョン 1511|  
|帯域外管理 - System Center 2012 Configuration Manager の機能|2015/10/16|バージョン 1511|
|タスク シーケンス: <br /> - ディスクをダイナミックに変換 <br /> - 展開ツールのインストール |11/18/2016|2017 年 6 月 1 日以降にリリースされた最初の更新プログラムでこれらのタスク シーケンスのサポートは終了します|  

 **非推奨のサーバー オペレーティング システム:**  

 |**オペレーティング システム**|**最初に非推奨と発表**|**サポートの削除** |  
|-|-|-|  
|Windows Server 2008|2015/7/10|サポートは、2016 年 12 月 31 日より後にリリースされる最初の更新プログラムで終了します *(注 1 をご覧ください)*|  
|Windows Server 2008 R2|2015/7/10|サポートは、2016 年 12 月 31 日より後にリリースされる最初の更新プログラムで終了します *(注 2 をご覧ください)*|  

-   *注 1*: サポート終了後は、サイト サーバーやほとんどのサイト システムの役割に対してこのオペレーティング システムはサポートされなくなります。 ただし、このサポートの廃止が発表されるまで、またはこのオペレーティング システムの延長サポート期間が終了するまで、配布ポイントのサイト システムの役割 (プル配布ポイントなど) に対してこのオペレーティング システムは引き続きサポートされます。  

-   *注 2*: サポート終了後は、サイト サーバーやほとんどのサイト システムの役割に対してこのオペレーティング システムはサポートされなくなります。 ただし、このサポートの廃止が発表されるまで、またはこのオペレーティング システムの延長サポート期間が終了するまで、状態移行ポイントおよび配布ポイントのサイト システムの役割 (プル配布ポイント、PXE およびマルチキャストの場合を含む) に対してこのオペレーティング システムは引き続きサポートされます。  バージョン 1602 より、サイト サーバーのオペレーティング システムを Windows Server 2008 R2 から Windows Server 2012 R2 にインプレース アップグレードできます。  

     サイト サーバーのオペレーティング システムのインプレース アップグレードに関する詳細については、「[System Center Configuration Manager の変更点](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)」の「[Windows Server 2008 R2 を実行するサイト サーバーのオペレーティング システムのインプレース アップグレード](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS)」セクションを参照してください。



 **非推奨クライアント オペレーティング システム:**  

 特に明記しない限り、Configuration Manager クライアントとしてサポートされている各オペレーティング システムは、[マイクロソフト サポート ライフ サイクル](https://support.microsoft.com/lifecycle)に詳述されているオペレーティングシステムの延長サポート終了日までサポートされます。  延長サポート終了日より前にオペレーティング システムの Configuration Manager のサポートが終了する場合は、そのオペレーティング システムの廃止日とサポート削除日がここに表示されます。  

|**オペレーティング システム**|**最初に非推奨と発表**|**サポートの削除**|  
|-|-|-|  
|Windows XP|2015/7/10|バージョン 1511|  
|Windows XP Embedded|2015/7/10|サポートは、2016 年 12 月 31 日より後にリリースされた最初の更新プログラムで終了します|  
|Windows Server 2003|2015/7/10|バージョン 1511|  
|Windows Server 2003 R2|2015/7/10|バージョン 1511|  
|Windows Vista|2015/7/10|バージョン 1511|  
|Mac OS X  10.6 - 10.8|2015/7/10|バージョン 1511|  
|Windows Mobile 6.0 - 6.5|2015/7/10|バージョン 1511|  
|Nokia Symbian Belle|2015/7/10|バージョン 1511|  
|Windows CE 5.0 - 6.0|2015/7/10|バージョン 1511|  


 **サイト データベースとしてのサポートが廃止された SQL Server バージョン**  

|**SQL Server バージョン**|**最初に非推奨と発表**|**サポートの削除**|   
|-|-|-|  
|SQL Server 2008|2015/7/10|バージョン 1511|  
|SQL Server 2008 R2|2015/7/10|サポートは、2016 年 12 月 31 日より後にリリースされた最初の更新プログラムで終了します|  

## <a name="features-removed-in-system-center-configuration-manager"></a>System Center Configuration Manager で削除された機能  
 初期 System Center Configuration Manager リリース以降、削除された機能は次のとおりです。

###  <a name="a-namebkmkamta-out-of-band-management"></a><a name="bkmk_amt"></a> 帯域外管理  
 Configuration Manager では、Configuration Manager コンソール内からの AMT ベースのコンピューターに対するネイティブ サポートは削除されました。  

-    [Microsoft System Center Configuration Manager 用 Intel SCS アドオン](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)を使用すれば、AMT ベースのコンピューターは引き続き完全に管理されます。  

-   アドオンを使用することで、最新の機能にアクセスして AMT を管理できます。Configuration Manager にこれらの変更が組み込まれるまでに適用されていた制限は解除されます。  

-   System Center 2012 Configuration Manager での帯域外管理は、この変更の影響を受けません。  

###  <a name="a-namebkmknapa-network-access-protection"></a><a name="bkmk_nap"></a> ネットワーク アクセス保護  
 System Center Configuration Manager では、ネットワーク アクセス保護のサポートが削除されました。 この機能は Windows Server 2012 R2 で非推奨となり、Windows 10 からは削除されています。  

 ネットワーク アクセス保護の代替方法については、「 **ネットワーク ポリシーとアクセス サービスの概要** 」で [非推奨の機能](https://technet.microsoft.com/library/hh831683.aspx)に関する説明を参照してください。  



<!--HONumber=Dec16_HO1-->


