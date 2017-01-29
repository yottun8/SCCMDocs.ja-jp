---
title: "Configuration Manager の評価 | Microsoft Docs"
description: "組織で使用するために System Center Configuration Manager を評価するラボ環境を作成します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: 25
caps.handback.revision: 0
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 35e48666f4d1a2363304650f960531fd0630a291
ms.openlocfilehash: ad3c849bd3ebfc6c0aa795e5b49a4850371cda47


---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>独自のラボ環境を構築して System Center Configuration Manager を評価する

*適用対象: System Center Configuration Manager (Current Branch)*

組織で使用するために System Center Configuration Manager を評価するラボ環境を作成する方法について説明します。  

## <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>独自のラボ環境を構築して System Center Configuration Manager を評価する  
 System Center Configuration Manager は、ユーザー、デバイス、およびソフトウェアを管理するための、複雑で強力なツールです。 概念の理解を現場での実践に結び付けることができるように、完全な展開の前に System Center Configuration Manager の詳細な評価を完了することをお勧めします。  

 このガイドは、主に、企業環境内で Configuration Manager の使用を評価する管理者を対象にしています。  

-   PC、サーバー、およびモバイル デバイスを完全に管理するソリューションを求めている管理者  

-   オンプレミス デバイス管理のセキュリティと、クラウドベースのデバイス管理の柔軟性を必要とする高セキュリティ業界の管理者  

-   オンプレミス サーバー アーキテクチャのスケールアップに関心のある管理者  

### <a name="what-this-lab-does"></a>このラボの実行内容  
 この環境を作成する主な目的は、Configuration Manager の使用を開始するための一般的な知識を提供すること、および、作業を通じて Configuration Manager についての理解を深めることです。 ここでは、最新バージョンの Configuration Manager で&2; 台のサーバーを使用する、拡張された構成を例として説明します。  

-   1 つ目のサーバーは、Active Directory、ドメイン コントローラー、および DNS サーバーをホストします。  

-   2 つ目のサーバーは、Configuration Manager と、関連するすべての SQL Server コンポーネントをホストします。  

-   クライアント コンピューターは Hyper-V 内にインストールされます。 ラボ自体は、単一のサーバーで完全に仮想化されたシステムとして実行することもできます。  

### <a name="what-this-lab-does-not-do"></a>このラボで実行しないこと  
 このラボでは、すべての Configuration Manager シナリオは紹介せず、すぐにアクティブな環境に移行することは想定されていません。  

 このラボを構築すると、機能し、作業できる環境が整います。 ただし、この環境は、システム パフォーマンス、ハード ディスク領域の管理、SQL Server の記憶域などに関して最適化されません。  

###  <a name="a-namebkmkevalreca-recommended-reading-prior-to-beginning-the-lab"></a><a name="BKMK_EvalRec"></a> ラボを開始する前の推奨資料  
 「[System Center Configuration Manager のドキュメント](http://docs.microsoft.com/sccm/)」には豊富なコンテンツがあります。 このライブラリから選んだいくつかのトピックを次に示します。ラボで作業するすべての管理者が、演習を開始する前にこれらを参照することをお勧めします。  

-   「[System Center Configuration Manager の概要](../../core/understand/introduction.md)」。Configuration Manager コンソール、エンドユーザー ポータル、およびシナリオ例の主要な概念について説明しています。  

-   「[System Center Configuration Manager の特徴と機能](../../core/plan-design/changes/features-and-capabilities.md)」。Configuration Manager の主な管理機能について説明しています。  

-   「[System Center Configuration Manager の基本](../../core/understand/fundamentals.md)」。知識を強化します。  

-   「[System Center Configuration Manager のロール ベース管理の基礎](../../core/understand/fundamentals-of-role-based-administration.md)」。セキュリティ ロールの重要性について説明しています。  

-   「[コンテンツ管理の概念](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)」。これらを理解することによって、コンテンツ管理に関連する特定の概念を得ることができます。  

-   「[クライアントが System Center Configuration Manager のサイト リソースやサービスを検索する方法を理解する](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)」。展開全体での日常操作を適切にサポートします。  



<!--HONumber=Jan17_HO4-->


