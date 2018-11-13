---
title: コンテンツ管理の基礎
titleSuffix: Configuration Manager
description: Configuration Manager のツールとオプションを使用して、展開するコンテンツを管理します。
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b73ead1492b143260d327f428db5a6183f84434c
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411342"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Configuration Manager でのコンテンツ管理の基本的な概念

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager では、ソフトウェア コンテンツを管理するためのツールとオプションの信頼性の高いシステムがサポートされます。 アプリケーション、パッケージ、ソフトウェア更新プログラム、OS の展開などのソフトウェアの展開にはすべてコンテンツが必要です。 Configuration Manager は、サイト サーバーと配布ポイントの両方にコンテンツを格納します。 このコンテンツを地点間で転送するときに、大きなネットワーク帯域幅が必要になります。 コンテンツ管理インフラストラクチャを効果的に計画および使用するには、まず、利用可能なオプションと構成を理解します。 その後、ネットワーク環境やコンテンツ展開ニーズに最適な使い方を検討します。  

> [!TIP]    
> コンテンツ配布プロセスの詳細、およびコンテンツ配布に関する一般的な問題の診断と解決に役立つ情報の探し方については、「[Understanding and Troubleshooting Content Distribution in Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm)」(Microsoft Configuration Manager でのコンテンツ配布の理解とトラブルシューティング) をご覧ください。

以下のトピックでは、コンテンツ管理の主要概念について説明します。 概念について追加情報または複雑な情報が必要な場合は、該当する詳細情報へのリンクが示されています。



## <a name="accounts-used-for-content-management"></a>コンテンツ管理に使用されるアカウント  
 コンテンツ管理では、次のアカウントを使用できます。  

#### <a name="network-access-account"></a>ネットワーク アクセス アカウント
クライアントが配布ポイントに接続してコンテンツにアクセスするために使用します。 既定では、コンピューター アカウントが最初に試行されます。  

このアカウントは、リモート フォレスト内のソース配布ポイントからコンテンツをダウンロードするためにプル配布ポイントによっても使われます  

バージョン 1806 以降では、一部のシナリオでネットワーク アクセス アカウントが不要になりました。 サイトで Azure Active Directory 認証を使用した拡張 HTTP の使用を有効にすることができます。<!--1358228--> 

詳細については、「[ネットワーク アクセス アカウント](/sccm/core/plan-design/hierarchy/accounts#network-access-account)」を参照してください。

#### <a name="package-access-account"></a>［パッケージ アクセス アカウント］
既定では、Configuration Manager は、汎用アクセス アカウントである Users および Administrators に対して配布ポイント上のコンテンツへのアクセスを許可します。 ただし、追加のアクセス許可を構成してアクセスを制限することができます。   

詳細については、「[パッケージ アクセス アカウント](/sccm/core/plan-design/hierarchy/accounts#package-access-account)」をご覧ください。



## <a name="bandwidth-throttling-and-scheduling"></a>帯域幅調整とスケジュール  
 調整とスケジュールのどちらも、コンテンツをサイト サーバーから配布ポイントに配布する処理を管理するためのオプションです。 これらの機能は、サイト間のファイルベースのレプリケーションに関する帯域幅の制御に似ていますが、直接の関係はありません。  

 詳細については、「[ネットワーク帯域幅の管理](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)」を参照してください。



## <a name="binary-differential-replication"></a>バイナリ差分レプリケーション  
 バイナリ差分レプリケーション (BDR) は、配布ポイントの前提条件です。 これは、デルタ レプリケーションとも呼ばれます。 以前に他のサイトまたはリモート配布ポイントに展開したコンテンツに更新プログラムを配布すると、帯域幅を減らすために BDR が自動的に使われます。  

 BDR は、配布されたコンテンツの更新プログラムの送信に使われるネットワーク帯域幅を最小限に抑えます。 ファイルを変更するたびにコンテンツ ソース ファイルのセット全体が送信される代わりに、新しいまたは変更されたコンテンツのみが再送信します。  

 BDR が使われていると、Configuration Manager は、以前に配布された各コンテンツ セットについて、ソース ファイルに対して行われた変更を識別します。  

-   ソース コンテンツ内のファイルが変更されると、サイトではコンテンツの新しい増分バージョンが作成されます。 その後、変更されたファイルのみがレプリケーション先サイトと配布ポイントにレプリケートします。 ファイルは、名前が変更された場合、移動された場合、またはファイルの内容が変更された場合に、変更されたものと見なされます。 たとえば、以前に複数のサイトに配布したドライバー パッケージの 1 つのドライバー ファイルを置き換えた場合は、変更されたドライバー ファイルのみがレプリケートされます。  

-   Configuration Manager は、全体のコンテンツ セットを再送信するまでに、最大 5 つの増分バージョンのコンテンツ セットを保持できます。 5 番目の更新の後で、コンテンツ セットを次に変更すると、サイトはコンテンツ セットの新しいバージョンを作成します。 Configuration Manager はその後、コンテンツ セットの新しいバージョンを配布し、前のセットとその増分バージョンを置き換えます。 新しいコンテンツ セットが配布された後は、BDR によって、またソース ファイルの増分の変更がレプリケートされます。  

BDR は、同じ階層内の親サイトと子サイト間でサポートされます。 また、BDR は、サイト内のサイト サーバーとその定期的な配布ポイント間でサポートされます。 しかし、プル配布ポイントとクラウドの配布ポイントでは、BDR によるコンテンツの転送はサポートされません。 プル配布ポイントは、ファイル レベルのデルタをサポートしており、新しいファイルは転送されますが、ファイル内のブロックは転送されません。

アプリケーションは、常にバイナリ差分レプリケーションを使用します。 パッケージの BDR はオプションであり、既定では有効になりません。 パッケージに BDR を使うには、パッケージごとにこの機能を有効にします。 パッケージを作成または編集するときに、**[バイナリ差分レプリケーションを有効にする]** オプションを有効にします。   



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



## <a name="windows-ledbat"></a>Windows LEDBAT
<!--1358112--> Windows Low Extra Delay Background Transport (LEDBAT) は、バックグラウンド ネットワーク転送の管理に役立つ、Windows Server のネットワークの輻そう制御機能です。 サポートされている Windows Server のバージョンで実行される配布ポイントに対して、ネットワーク トラフィックの調整に役立つオプションを有効にします。 その後、クライアントでは利用可能な場合にのみ、ネットワーク帯域幅が使用されます。 

一般的な Windows LEDBAT の詳細については、[新しいトランスポートの発展](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/)に関するブログ投稿を参照してください。

Configuration Manager 配布ポイントで Windows LEDBAT を使用する方法の詳細については、[配布ポイントの全般設定を構成する](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-general)際に **[Adjust the download speed to use the unused network bandwidth (Windows LEDBAT)]\(未使用のネットワーク帯域幅を使用するようにダウンロード速度を調整する (Windows LEDBAT)\)** の設定を確認してください。



## <a name="peer-cache"></a>ピア キャッシュ
クライアントのピア キャッシュは、リモートの場所にあるクライアントへのコンテンツの展開を管理するのに役立ちます。 ピア キャッシュとは、クライアントがローカル キャッシュで他のクライアントとコンテンツを直接共有できるようにするための組み込みの Configuration Manager ソリューションです。

まず、コレクションにピア キャッシュを有効にするクライアント設定を展開します。 これにより、そのコレクションのメンバーは、同じ境界グループ内の他のクライアント用のピア コンテンツ ソースとして機能できます。

バージョン 1806 以降では、クライアント ピア キャッシュ ソースのコンテンツを分割できます。 これにより、ネットワーク転送が最小限に抑えられ、WAN の使用率が減ります。 管理ポイントでは、コンテンツの各パートをより詳細に追跡することができます。 境界グループごとに同じコンテンツが複数回ダウンロードされないようにします。<!--1357346-->

詳細については、「[Configuration Manager クライアントのピア キャッシュ](/sccm/core/plan-design/hierarchy/client-peer-cache)」を参照してください。



## <a name="windows-pe-peer-cache"></a>Windows PE ピア キャッシュ
Configuration Manager で新しい OS を展開するとき、タスク シーケンスを実行しているコンピューターは Windows PE ピア キャッシュを使うことができます。 このようなコンピューターは、配布ポイントの代わりに、ピア キャッシュ ソースからコンテンツをダウンロードします。 この動作により、ローカル配布ポイントが存在しないブランチ オフィス シナリオで WAN のトラフィックが最小限に抑えられます。

詳細については、「[Windows PE ピア キャッシュ](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic)」を参照してください。



## <a name="client-locations"></a>クライアントの場所  
 クライアントは、次の場所にあるコンテンツにアクセスします。  

-   **イントラネット** (オンプレミス):  

    -   配布ポイントでは、HTTP または HTTPS を使用できます。  

    -   オンプレミスの配布ポイントを使用できない場合、フォールバックとしてクラウドの配布ポイントのみを使用します。  

-   **インターネット**:  

    -   HTTPS を受け入れるには、インターネットに接続されている配布ポイントが必要です。  

    -   クラウドの配布ポイントを使用することができます。  

-   **ワークグループ**:  

    -   HTTPS を受け入れるには配布ポイントが必要です。  

    -   クラウドの配布ポイントを使用することができます。  



## <a name="content-source-priority"></a>コンテンツ ソースの優先順位

クライアントでコンテンツが必要な場合は、コンテンツの場所の要求を管理ポイントに対して行います。 管理ポイントからは、要求されたコンテンツで有効なソースの場所の一覧が返されます。 この一覧は、特定のシナリオ、使用されているテクノロジ、サイト設計、境界グループ、展開の設定によって異なります。 次の一覧には、クライアントで使用できる、利用可能なコンテンツ ソースの場所がすべて含まれており、優先順に示されています。  

1.  クライアントと同じコンピューター上の配布ポイント
2.  同じネットワーク サブネット内のピア ソース
3.  同じネットワーク サブネット内の配布ポイント
4.  同じ境界グループ内のピア ソース
5.  現在の境界グループ内の配布ポイント
6.  フォールバック用に構成された近隣境界グループ内の配布ポイント
9.  既定のサイト境界グループ内の配布ポイント 
10. Windows Update クラウド サービス
11. インターネットに接続されている配布ポイント
12. Azure 内のクラウド配布ポイント



## <a name="content-library"></a>コンテンツ ライブラリ  
 コンテンツ ライブラリは、Configuration Manager でのコンテンツの単一インスタンス ストアです。 このライブラリにより、配布されるコンテンツの全体的なサイズが減ります。  

- [コンテンツ ライブラリ](/sccm/core/plan-design/hierarchy/the-content-library)の詳細を確認してください。
- コンテンツがもはやアプリケーションに関連していない場合は、[コンテンツ ライブラリのクリーンアップ ツール](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) を使用して、コンテンツを削除します。  



## <a name="distribution-points"></a>配布ポイント  
 Configuration Manager は、配布ポイントを使用して、クライアント コンピューターで実行するソフトウェアに必要なファイルを格納します。 クライアントは、展開するコンテンツのファイルがダウンロード可能な 1 つ以上の配布ポイントにアクセスできる必要があります。  

 基本的な (特殊化されていない) 配布ポイントは、標準配布ポイントとも呼ばれます。 標準配布ポイントには次の 2 つのバリエーションがあることに注目してください。  

-   **プル配布ポイント**: 配布ポイントが他の配布ポイント (ソース配布ポイント) からコンテンツを取得する、配布ポイントのバリエーションの 1 つ。 このプロセスは、クライアントが配布ポイントからコンテンツをダウンロードするのと同じです。 プル配布ポイントを使用すると、サイト サーバーが各配布ポイントにコンテンツを直接配布する必要があるときに発生するネットワーク帯域幅のボトルネックを解消することができます。 [プル配布ポイントを使う](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)。

-   **クラウド配布ポイント**: Microsoft Azure にインストールされている配布ポイントのバリエーションの 1 つ。 クラウド配布ポイントの使い方については、[こちら](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)を参照してください。  


標準配布ポイントは、さまざまな構成と機能をサポートします。  

- この転送を制御するには、**スケジュール**や**帯域幅調整**などのコントロールを使います。  

- ネットワークの消費量を最小限にして制御するには、**事前設定されたコンテンツ**や**プル配布ポイント**などのコントロールを使います。  

- **BranchCache**、**ピア キャッシュ**、および**配信の最適化**は、コンテンツを展開するときに使われるネットワーク帯域幅を削減するためのピア ツー ピア テクノロジです。  

- OS の展開には、**[PXE](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_PXEDistributionPoint)** や**[マルチキャスト](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_DPMulticast)** など、さまざまな構成があります  

- **モバイル デバイス**のオプション   
  
クラウドおよびプル配布ポイントでは、これらの同じ構成の多くがサポートされますが、各配布ポイントのバリエーションに固有の制限事項があります。  



## <a name="distribution-point-groups"></a>配布ポイント グループ  
 配布ポイント グループは、コンテンツ配布の簡素化に役立つ、配布ポイントの論理的グループです。  

 詳細については、「[配布ポイント グループの管理](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_manage)」を参照してください。



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



## <a name="network-bandwidth"></a>ネットワークの帯域幅  
 コンテンツを配布するときに使用されるネットワーク帯域幅を管理するために、次のオプションを使用できます。  

-   **事前設定されたコンテンツ**: ネットワーク経由でコンテンツを配布せずに、配布ポイントにコンテンツを転送。  

-   **スケジュールと調整**: 配布ポイントにコンテンツを配布するタイミングと方法を制御するための構成。  

詳細については、「[ネットワーク帯域幅の管理](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)」を参照してください。



## <a name="network-connection-speed-to-content-source"></a>コンテンツ ソースへのネットワーク接続の速度  
 Configuration Manager の Current Branch では、クライアントがコンテンツを含む配布ポイントを検索する方法について、いくつかのことが変更されています。 これらの変更には、コンテンツ ソースへのネットワーク速度が含まれます。 

配布ポイントを **[高速]** または **[低速]** として定義するネットワーク接続速度は使用されなくなりました。 代わりに、境界グループに関連付けられている各サイト システムが同じように処理されます。

詳細については、「[境界グループ](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups)」を参照してください。



## <a name="on-demand-content-distribution"></a>オンデマンドのコンテンツ配布  
 オンデマンド コンテンツ配布は、個々のアプリケーションおよびパッケージの展開のオプションです。 このオプションは、優先サーバーへのオンデマンドのコンテンツ配布を有効にします。  

-   展開に対してこの設定を有効にするには、**[このパッケージのコンテンツを優先配布ポイントに配布する]** を有効にします。  

-   このオプションを展開に対して有効にしており、クライアントでコンテンツが要求されたものの、そのコンテンツがクライアントの優先配布ポイントのいずれかで利用できない場合、Configuration Manager によって、そのコンテンツが自動的にクライアントの優先配布ポイントに配布されます。  

-   このオプションが有効になっていると、Configuration Manager によってクライアントの優先配布ポイントにコンテンツが自動的に配布されますが、クライアントの優先配布ポイントが展開を受け取る前にクライアントが他の配布ポイントからコンテンツを取得する可能性があります。 この動作が発生した場合、コンテンツは、その展開を必要とする他のクライアントで利用できるように、その配布ポイント上に保持されます。  

詳細については、「[境界グループ](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups)」を参照してください。



## <a name="package-transfer-manager"></a>パッケージ転送マネージャー  
 パッケージ転送マネージャーは、他のコンピューター上の配布ポイントにコンテンツを転送するサイト サーバー コンポーネントです。  

 詳細については、「[パッケージ転送マネージャー](/sccm/core/plan-design/hierarchy/package-transfer-manager)」をご覧ください。  



## <a name="prestage-content"></a>コンテンツの事前設定  
 事前設定されたコンテンツは、ネットワーク経由でコンテンツを配布せずに、配布ポイントにコンテンツを転送するプロセスです。  

 詳細については、「[ネットワーク帯域幅の管理](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)」を参照してください。
