---
title: コンテンツ管理の基礎
titleSuffix: Configuration Manager
description: Configuration Manager のツールとオプションを使用して、展開するコンテンツを管理します。
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4419a563a65ab9d98a76dcf58b48ae00e0763dab
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2018
ms.locfileid: "36260736"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Configuration Manager でのコンテンツ管理の基本的な概念

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager は、アプリケーション、パッケージ、ソフトウェア更新プログラム、および OS の展開として展開するコンテンツを管理するための、信頼性の高いツールとオプションのシステムをサポートしています。 Configuration Manager は、サイト サーバーと配布ポイントの両方にコンテンツを格納します。 このコンテンツを地点間で転送するときに、大きなネットワーク帯域幅が必要になります。 コンテンツ管理インフラストラクチャを効果的に計画および使用するには、使用可能なオプションと構成を理解することをお勧めします。 その後、ネットワーク環境やコンテンツ展開ニーズに最適な使い方を検討します。  

> [!TIP]    
> コンテンツ配布プロセスの詳細、およびコンテンツ配布に関する一般的な問題の診断と解決に役立つ情報の探し方については、「[Understanding and Troubleshooting Content Distribution in Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm)」(Microsoft Configuration Manager でのコンテンツ配布の理解とトラブルシューティング) をご覧ください。

以下のトピックでは、コンテンツ管理の主要概念について説明します。 概念について追加情報または複雑な情報が必要な場合は、該当する詳細情報へのリンクが示されています。



## <a name="accounts-used-for-content-management"></a>コンテンツ管理に使用されるアカウント  
 コンテンツ管理では、次のアカウントを使用できます。  

-   **ネットワーク アクセス アカウント**: クライアントが配布ポイントに接続してコンテンツにアクセスするために使用します。 既定では、コンピューター アカウントが最初に試行されます。  

     このアカウントは、リモート フォレスト内のソース配布ポイントからコンテンツをダウンロードするためにプル配布ポイントによっても使われます  

-   **パッケージ アクセス アカウント**: 既定では、Configuration Manager は、汎用アクセス アカウントである Users および Administrators に対して配布ポイント上のコンテンツへのアクセスを許可します。 ただし、追加のアクセス許可を構成してアクセスを制限することができます。   

-   **マルチキャスト接続アカウント**: OS の展開に使われます。  

これらのアカウントの詳細については、「[コンテンツにアクセスするためのアカウントの管理](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md)」を参照してください。



## <a name="bandwidth-throttling-and-scheduling"></a>帯域幅調整とスケジュール  
 調整とスケジュールのどちらも、コンテンツをサイト サーバーから配布ポイントに配布する処理を管理するためのオプションです。 これらの機能は、サイト間のファイルベースのレプリケーションに関する帯域幅の制御に似ていますが、直接の関係はありません。  

 詳細については、「[ネットワーク帯域幅の管理](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)」を参照してください。



## <a name="binary-differential-replication"></a>バイナリ差分レプリケーション  
 バイナリ差分レプリケーション (BDR) は、配布ポイントの前提条件です。 これは、デルタ レプリケーションとも呼ばれます。 以前に他のサイトまたはリモート配布ポイントに展開したコンテンツに更新プログラムを配布すると、帯域幅を減らすために BDR が自動的に使われます。  

 BDR は、配布されたコンテンツの更新プログラムの送信に使われるネットワーク帯域幅を最小限に抑えます。 ファイルを変更するたびにコンテンツ ソース ファイルのセット全体が送信される代わりに、新しいまたは変更されたコンテンツのみが再送信します。  

 BDR が使われていると、Configuration Manager は、以前に配布された各コンテンツ セットについて、ソース ファイルに対して行われた変更を識別します。  

-   ソース コンテンツ内のファイルが変化すると、サイトはコンテンツ セットの新しい増分バージョンを作成します。 その後、変更されたファイルのみがレプリケーション先サイトと配布ポイントにレプリケートします。 ファイルは、名前が変更された場合、移動された場合、またはファイルの内容が変更された場合に、変更されたものと見なされます。 たとえば、以前に複数のサイトに配布したドライバー パッケージの 1 つのドライバー ファイルを置き換えた場合は、変更されたドライバー ファイルのみがレプリケートされます。  

-   Configuration Manager は、全体のコンテンツ セットを再送信するまでに、最大 5 つの増分バージョンのコンテンツ セットを保持できます。 5 番目の更新の後で、コンテンツ セットを次に変更すると、サイトはコンテンツ セットの新しいバージョンを作成します。 Configuration Manager はその後、コンテンツ セットの新しいバージョンを配布し、前のセットとその増分バージョンを置き換えます。 新しいコンテンツ セットが配布された後は、BDR によって、またソース ファイルの増分の変更がレプリケートされます。  

BDR は、同じ階層内の親サイトと子サイト間でサポートされます。 また、BDR は、サイト内のサイト サーバーとその定期的な配布ポイント間でサポートされます。 ただし、プル配布ポイントとクラウドベースの配布ポイントでは、BDR によるコンテンツの転送はサポートされません。 プル配布ポイントは、ファイル レベルのデルタをサポートしており、新しいファイルは転送されますが、ファイル内のブロックは転送されません。

アプリケーションは、常にバイナリ差分レプリケーションを使用します。 パッケージの BDR はオプションであり、既定では無効になっています。 パッケージに BDR を使うには、パッケージごとにこの機能を有効にします。 パッケージを作成または編集するときに、**[バイナリ差分レプリケーションを有効にする]** オプションを有効にします。   



## <a name="branchcache"></a>BranchCache  
 [BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) は Windows のテクノロジです。 BranchCache をサポートし、BranchCache 用に構成されている展開をダウンロードしたクライアントは、BranchCache が有効な他のクライアントに対するコンテンツ ソースとして機能します。  

 たとえば、Windows Server 2012 以降を実行する配布ポイントがあり、BranchCache サーバーとして構成されているものとします。 最初の BranchCache が有効なクライアントがこのサーバーのコンテンツを要求すると、クライアントはそのコンテンツをダウンロードしてキャッシュします。  

- その後、このクライアントは、同じサブネット上にあって BranchCache が有効であり、やはりコンテンツをキャッシュするようになっている他のクライアントが、コンテンツを利用できるようにします。  
- 同じサブネット上の他のクライアントは、配布ポイントからコンテンツをダウンロードする必要はありません。  
- コンテンツは、今後の転送に備えて複数のクライアントに分散されます。  

詳細については、[Windows BranchCache のサポート](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache)に関するページをご覧ください。



## <a name="delivery-optimization"></a>配信の最適化
<!-- 1324696 --> Configuration Manager の境界グループを使って、企業ネットワークおよびリモート オフィスへのコンテンツ配布を定義して調整します。 [Windows の配信最適化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)は、Windows 10 デバイス間でコンテンツを共有するための、クラウド ベースのピア ツー ピア テクノロジです。 バージョン 1802 以降、ピア間でコンテンツを共有するときは、境界グループを使うように配信の最適化を構成します。 クライアントの設定は、クライアントでの配信最適化グループの識別子として境界グループ識別子を適用します。 クライアントは、配信の最適化クラウド サービスと通信するとき、この識別子を使って目的のコンテンツを含むピアを探します。 詳細については、「[配信の最適化](/sccm/core/clients/deploy/about-client-settings#delivery-optimization)」のクライアント設定をご覧ください。

配信の最適化は、Windows 10 品質更新プログラム用の高速インストール ファイルの [Windows 10 更新プログラムの配信を最適化](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)するために推奨されるテクノロジです。



## <a name="peer-cache"></a>ピア キャッシュ
クライアントのピア キャッシュは、リモートの場所にあるクライアントへのコンテンツの展開を管理するのに役立ちます。 ピア キャッシュとは、クライアントがローカル キャッシュで他のクライアントとコンテンツを直接共有できるようにするための組み込みの Configuration Manager ソリューションです。

ピア キャッシュを有効にするクライアント設定をコレクションに展開すると、そのコレクションのメンバーは同じ境界グループ内の他のクライアントのピア コンテンツ ソースとして動作できます。

詳細については、「[Configuration Manager クライアントのピア キャッシュ](/sccm/core/plan-design/hierarchy/client-peer-cache)」を参照してください。



## <a name="windows-pe-peer-cache"></a>Windows PE ピア キャッシュ
Configuration Manager で新しい OS を展開するとき、タスク シーケンスを実行しているコンピューターは Windows PE ピア キャッシュを使うことができます。 このようなコンピューターは、配布ポイントの代わりに、ピア キャッシュ ソースからコンテンツをダウンロードします。 この動作により、ローカル配布ポイントが存在しないブランチ オフィス シナリオで WAN のトラフィックが最小限に抑えられます。

詳細については、「[Windows PE ピア キャッシュ](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)」を参照してください。



## <a name="client-locations"></a>クライアントの場所  
 クライアントは、次の場所にあるコンテンツにアクセスします。  

-   **イントラネット** (オンプレミス):  

    -   配布ポイントでは、HTTP または HTTPS を使用できます。  

    -   オンプレミスの配布ポイントを使用できない場合、フォールバックとしてクラウドベースの配布ポイントのみを使用します。  

-   **インターネット**:  

    -   HTTPS を受け入れるには配布ポイントが必要です。  

    -   フォールバックとしてクラウドベースの配布ポイントを使用できます。  

-   **ワークグループ**:  

    -   HTTPS を受け入れるには配布ポイントが必要です。  

    -   フォールバックとしてクラウドベースの配布ポイントを使用できます。  



## <a name="content-library"></a>コンテンツ ライブラリ  
 コンテンツ ライブラリは、Configuration Manager でのコンテンツの単一インスタンス ストアです。 このライブラリにより、配布されるコンテンツの全体的なサイズが減ります。  

- [コンテンツ ライブラリ](../../../core/plan-design/hierarchy/the-content-library.md)の詳細を確認してください。
- コンテンツがもはやアプリケーションに関連していない場合は、[コンテンツ ライブラリのクリーンアップ ツール](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) を使用して、コンテンツを削除します。  



## <a name="distribution-points"></a>配布ポイント  
 Configuration Manager は、配布ポイントを使用して、クライアント コンピューターで実行するソフトウェアに必要なファイルを格納します。 クライアントは、展開するコンテンツのファイルがダウンロード可能な 1 つ以上の配布ポイントにアクセスできる必要があります。  

 基本的な (特殊化されていない) 配布ポイントは、標準配布ポイントとも呼ばれます。 標準配布ポイントには次の 2 つのバリエーションがあることに注目してください。  

-   **プル配布ポイント**: 配布ポイントが他の配布ポイント (ソース配布ポイント) からコンテンツを取得する、配布ポイントのバリエーションの 1 つ。 このプロセスは、クライアントが配布ポイントからコンテンツをダウンロードするのと同じです。 プル配布ポイントを使用すると、サイト サーバーが各配布ポイントにコンテンツを直接配布する必要があるときに発生するネットワーク帯域幅のボトルネックを解消することができます。 [プル配布ポイントを使う](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)。

-   **クラウドベースの配布ポイント**: Microsoft Azure にインストールされている配布ポイントのバリエーションの 1 つ。 クラウドベースの配布ポイントの使い方については[こちら](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)を参照してください。  


標準配布ポイントは、さまざまな構成と機能をサポートします。  

- この転送を制御するには、**スケジュール**や**帯域幅調整**などのコントロールを使います。  
- ネットワークの消費量を最小限にして制御するには、**事前設定されたコンテンツ**や**プル配布ポイント**などのコントロールを使います。 
- **BranchCache**、**ピア キャッシュ**、および**配信の最適化**は、コンテンツを展開するときに使われるネットワーク帯域幅を削減するためのピア ツー ピア テクノロジです。  
- OS の展開には、**[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** や**[マルチキャスト](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** など、さまざまな構成があります
- **モバイル デバイス**のオプション   
  
  
クラウドベースのプル配布ポイントは、これらの同じ構成の多くをサポートしますが、各配布ポイントのバリエーションに固有の制限事項があります。  



## <a name="distribution-point-groups"></a>配布ポイント グループ  
 配布ポイント グループは、コンテンツ配布の簡素化に役立つ、配布ポイントの論理的グループです。  

 詳細については、「[配布ポイント グループの管理](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)」を参照してください。



## <a name="distribution-point-priority"></a>配布ポイントの優先順位  
 配布ポイントの優先順位値は、以前の展開をその配布ポイントに転送するのに要した時間に基づきます。  

-   この値は、自動的に調整されます。 Configuration Manager がより多くの配布ポイントにいっそう速くコンテンツを転送できるように、各配布ポイントで設定されます。  

-   同時に複数の配布ポイントに、または配布ポイント グループに、コンテンツを配布するとき、サイトは優先順位が最も高いサーバーに最初にコンテンツを送信します。 その後、その同じコンテンツを優先順位の低い配布ポイントに送信します。  

-   配布ポイントの優先順位によって、パッケージ配布の優先順位が置き換わることはありません。 パッケージの優先順位は、サイトが異なるコンテンツを送信するときの決定因子のままです。  

たとえば、パッケージの優先順位が高いパッケージがあるものとします。 それを、配布ポイントの優先順位が低いサーバーに配布します。 この優先順位の高いパッケージは、常に、優先順位の低いパッケージより前に転送されます。 パッケージの優先順位は、サイトが低い優先順位のパッケージを配布ポイントの優先順位の高いサーバーに配布する場合であっても、適用されます。

つまり、Configuration Manager では、優先順位の高いパッケージのコンテンツは、優先順位の低いパッケージより前に配布ポイントに配布されることが保証されます。  

> [!NOTE]  
>  また、プル配布ポイントは、優先順位の概念を使用して、ソース配布ポイントのシーケンスを決定しています。  
>   
>  -   サーバーへのコンテンツ転送に対する配布ポイントの優先順位は、プル配布ポイントが使う優先順位とは異なります。 プル配布ポイントは、ソース配布ポイントからコンテンツを検索するとき、プル配布ポイントの優先順位を使います。  
>  -   詳細については、「[プル配布ポイントの使用](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)」をご覧ください。  



## <a name="fallback"></a>フォールバック  
 Configuration Manager の Current Branch では、クライアントによる (フォールバックを含めた) コンテンツを含む配布ポイントの検索方法について、いくつかのことが変更されています。 

現在の境界グループに関連付けられた配布ポイントのコンテンツが見つからないクライアントは、近隣の境界グループに関連付けられたコンテンツ ソースの場所を使うようにフォールバックします。 フォールバックとして使用するには、近隣の境界グループにクライアントの現在の境界グループとの関係が定義されている必要があります。 このリレーションシップには、コンテンツがローカルで見つからないクライアントが検索により近隣の境界グループのコンテンツ ソースを含めることができるまでに経過しなければならない時間が構成されています。

優先配布ポイントの概念は使用されなくなりました。また、**[代替のコンテンツ ソースの場所の使用を許可する]** の設定も使用または適用されなくなりました。

詳細については、「[境界グループ](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups)」を参照してください。

<!--
**Version 1511, 1602, and 1606**   
Fallback settings are related to the use of **preferred distribution points** and to content source locations that are used by clients.

-   By default, clients only download content from a preferred distribution point (one that is associated with the client's boundary groups).  

-   However, when a distribution point is configured with **Allow clients to use this site system as a fallback source location for content**, that distribution point is only offered as a valid content source to any client that can't get a deployment from one of its preferred distribution points.  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="network-bandwidth"></a>ネットワークの帯域幅  
 コンテンツを配布するときに使用されるネットワーク帯域幅を管理するために、次のオプションを使用できます。  

-   **事前設定されたコンテンツ**: ネットワーク経由でコンテンツを配布せずに、配布ポイントにコンテンツを転送。  

-   **スケジュールと調整**: 配布ポイントにコンテンツを配布するタイミングと方法を制御するための構成。  

詳細については、「[ネットワーク帯域幅の管理](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)」を参照してください。



## <a name="network-connection-speed-to-content-source"></a>コンテンツ ソースへのネットワーク接続の速度  
 Configuration Manager の Current Branch では、クライアントがコンテンツを含む配布ポイントを検索する方法について、いくつかのことが変更されています。 これらの変更には、コンテンツ ソースへのネットワーク速度が含まれます。 

配布ポイントを **[高速]** または **[低速]** として定義するネットワーク接続速度は使用されなくなりました。 代わりに、境界グループに関連付けられている各サイト システムが同じように処理されます。

詳細については、「[境界グループ](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups)」を参照してください。

<!--
**Version 1511, 1602, and 1606**   
 You can configure the network connection speed of each distribution point in a boundary group:  

-   Clients use this value when they connect to the distribution point.

-   By default, the network connection speed is configured as **Fast**, but it can also be set as **Slow**.  

-   The **network connection speed**, along with the configuration of a deployment, determine if a client can download content from a distribution point when the client is in an associated boundary group  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="on-demand-content-distribution"></a>オンデマンドのコンテンツ配布  
 オンデマンド コンテンツ配布は、個々のアプリケーションおよびパッケージの展開のオプションです。 このオプションは、優先サーバーへのオンデマンドのコンテンツ配布を有効にします。  

-   展開に対してこの設定を有効にするには、**[このパッケージのコンテンツを優先配布ポイントに配布する]** を有効にします。  

-   このオプションが展開で有効になっていて、クライアントがこのコンテンツを要求したときにコンテンツがクライアントの優先配布ポイントのいずれかで利用できない場合、Configuration Manager は、このコンテンツを自動的にクライアントの優先配布ポイントに配布します。  

-   このオプションが有効になっていると、Configuration Manager によってクライアントの優先配布ポイントにコンテンツが自動的に配布されますが、クライアントの優先配布ポイントが展開を受け取る前にクライアントが他の配布ポイントからコンテンツを取得する可能性があります。 この動作が発生した場合、コンテンツは、その展開を必要とする他のクライアントで利用できるように、その配布ポイント上に保持されます。  

詳細については、「[境界グループ](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups)」を参照してください。

<!--
If you use version 1511, 1602, or 1606, see  [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) for information about the different content location and fallback scenarios.
-->



## <a name="package-transfer-manager"></a>パッケージ転送マネージャー  
 パッケージ転送マネージャーは、他のコンピューター上の配布ポイントにコンテンツを転送するサイト サーバー コンポーネントです。  

 詳細については、「[パッケージ転送マネージャー](../../../core/plan-design/hierarchy/package-transfer-manager.md)」をご覧ください。  



<!--
## Preferred distribution point  
 A preferred distribution point includes any distribution points that are associated with a client's current boundary groups.  

 You have the option to associate each distribution point with one or more boundary groups:  

-   This association helps the client identify distribution points from which it can download content.  
-   By default, clients can only download content from a preferred distribution point.  


For more information:
 - If you use version 1610 or later, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - If you use version 1511, 1602, or 1606, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).
-->



## <a name="prestage-content"></a>コンテンツの事前設定  
 事前設定されたコンテンツは、ネットワーク経由でコンテンツを配布せずに、配布ポイントにコンテンツを転送するプロセスです。  

 詳細については、「[ネットワーク帯域幅の管理](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)」を参照してください。
