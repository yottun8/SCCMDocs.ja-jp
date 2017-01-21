---
title: "サポートされている構成 | Microsoft Docs"
description: "機能的な System Center Configuration Manager 展開を計画、展開、および管理するための主要な構成および要件を特定します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 041ad6cb585028ecd64bd03feb44250fea0286b0


---
# <a name="supported-configurations-for-system-center-configuration-manager"></a>System Center Configuration Manager のサポートされている構成

*適用対象: System Center Configuration Manager (Current Branch)*

オンプレミス ソリューションとして、System Center Configuration Manager は、サーバー、クライアント、ネットワーク構成、および Microsoft Intune、SQL Server および Azure などのその他の製品を使用します。

このドキュメントおよび次のトピックの情報では、機能的な Configuration Manager 展開を計画、展開、および管理するための主要な構成および要件、または制限事項を識別するために不可欠です。  この情報は、Configuration Manager サイト、階層、および管理対象デバイスのインフラストラクチャに固有です。 Configuration Manager 機能に、さらに明確な構成が必要な場合、その情報は機能固有のドキュメントに含められ、これらのより一般的なサポートされている構成の詳細を補足します。  

 次のトピックで説明する製品とテクノロジが、Configuration Manager でサポートされています。 ただし、このコンテンツにそれらが含まれていても、その製品の個別のサポート ライフサイクルを超える製品サポートの延長を表すものではありません。 既にサポート ライフサイクルが終了している製品は、Configuration Manager ではサポートされません。 マイクロソフト サポート ライフサイクルの詳細については、 [「マイクロソフト サポート ライフサイクル」](http://go.microsoft.com/fwlink/p/?LinkId=208270) Web サイトを参照してください。  

> [!NOTE]  
>  マイクロソフトのサポート ライフサイクル ポリシーについては、[マイクロソフト サポートの「ライフサイクル ポリシー FAQ」](http://go.microsoft.com/fwlink/p/?LinkId=31976)Web サイトを参照してください。  

 さらに、次のトピックに示されていない製品および製品バージョンは、[Enterprise Mobility および Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/)で告知されていない限り、System Center Configuration Manager でサポートされません。  このブログのコンテンツは、このドキュメントの本文よりも先に更新される場合があります。


-  [サイジングとスケールの数値](../../../core/plan-design/configs/size-and-scale-numbers.md)  
サイトの数、サイトごとのサイト システムの役割、クライアントまたはデバイスに関する詳細は、Configuration Manager のさまざまな階層設計でサポートされます。

-  [サイトとサイト システムの前提条件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Windows Server でさまざまな種類のサイトの種類とサイト システムの役割をサポートするために必要な構成です。

-  [サイト システム サーバーのサポートされるオペレーティング システム](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
サイト サーバーまたはサイト システム サーバーとして使用できるオペレーティング システムについて説明します。

-  [クライアントとデバイスのサポートされるオペレーティング システム](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Windows、Linux および UNIX、Mac、埋め込みオペレーティング システム、およびモバイル デバイスを含む Configuration Manager で管理できるオペレーティング システムについて説明します。

-  [コンソールでサポートされているオペレーティング システム](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
展開を管理するためのアクセス ポイントを提供する Configuration Manager コンソールをホストできるオペレーティング システムについて説明します。  

-  [SQL Server バージョンのサポート](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
サイト データベースとレポート データベースだけでなく、使用することを選択できる必要な構成およびオプションの構成をホストできる SQL Server のバージョンを示します。

-  [高可用性オプション](../../../protect/understand/high-availability-options.md)  
Configuration Manager 展開の高可用性サービスを維持するために、環境の設計時に実装できるオプションについて説明します。

-  [推奨ハードウェア](../../../core/plan-design/configs/recommended-hardware.md)  
Configuration Manager サイトと主要なサービスをホストするための適切なハードウェアおよび構成の識別に役立つガイドライン。

-  [Active Directory ドメインのサポート](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Configuration Manager が必要とする Active Directory ドメインのサポートされている構成、およびサポートについて説明します。

-  [Windows の機能とネットワークのサポート](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Configuration Manager は、BranchCache およびデータ重複除去などのいくつかの Windows テクノロジをサポートします。 Configuration Manager で使用するための、サポートされているテクノロジと制限事項について説明します。

-  [仮想環境のサポート](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
サポートされている仮想マシン テクノロジを使用できるようにするための情報。



<!--HONumber=Dec16_HO3-->


