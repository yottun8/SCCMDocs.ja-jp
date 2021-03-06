---
title: 推奨ハードウェア
titleSuffix: Configuration Manager
description: 基本的な展開だけでなく、System Center Configuration Manager 環境を拡張するために役立つハードウェアの推奨事項を確認します。
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b773696d5967d9ed1779ee822168d7177f10f585
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130447"
---
# <a name="recommended-hardware-for-system-center-configuration-manager"></a>System Center Configuration Manager の推奨ハードウェア

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

以下の推奨事項は、サイト、サイト システム、およびクライアントのごく基本的な展開以上のものをサポートするために、System Center Configuration Manager 環境を拡張する場合に役立つガイドラインです。 考えられるすべてのサイトと階層構成について説明することを意図したものではありません。  

 以下の各セクションの情報は、既定の構成で利用できる Configuration Manager 機能を使用するクライアントとサイトについて、その処理負荷に対応できるようにハードウェアを計画する場合のガイドとして使用してください。  



##  <a name="bkmk_ScaleSieSystems"></a> サイト システム  
 このセクションでは、最大数のクライアントをサポートし、大部分、あるいはすべての Configuration Manager 機能を使用する展開のための Configuration Manager サイト システムのお勧めのハードウェア構成を示します。 展開でサポートするクライアントが最大数よりも少なく、使用可能な機能をすべて使用するわけではない場合、必要なコンピューター リソースはより少なくて済む場合があります。 一般的に、システム全体のパフォーマンスを制限する主な要因を順に挙げます。  

1.  ディスク I/O のパフォーマンス  

2.  使用可能なメモリ  

3.  CPU  

最適なパフォーマンスを得るには、すべてのデータ ドライブを RAID 10 構成にし、1 Gbps イーサネット ネットワークを使用します。  

###  <a name="bkmk_ScaleSiteServer"></a> サイト サーバー  

|サイトの構成|CPU (コア)|メモリ (GB)|SQL Server のメモリの割り当て (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|同じサーバー上でデータベース サイトの役割を持つスタンドアロン プライマリ サイト サーバー<sup>1</sup>|16|96|80|  
|リモート サイトのデータベースを使用するスタンドアロン プライマリ サイト サーバー|8|16|-|  
|スタンドアロン プライマリ サイトのリモート データベース サーバー|16|72|90|  
|同じサーバー上でデータベース サイトの役割を持つ中央管理サイト サーバー<sup>1</sup>|20|128|80|  
|リモート サイトのデータベースを使用する中央管理サイト サーバー|8|16|-|  
|中央管理サイトのリモート データベース サーバー|16|96|90|  
|同じサーバー上でデータベース サイトの役割を持つ子プライマリ サイト|16|96|80|  
|リモート サイトのデータベースを使用する子プライマリ サイト サーバー|8|16|-|  
|子プライマリ サイトのリモート データベース サーバー|16|72|90|  
|セカンダリ サイト サーバー|8|16|-|  

 <sup>1</sup> サイト サーバーと SQL Server が同じコンピューターにインストールされている場合、展開はサイトとクライアントの最大の [Sizing and scale numbers](/sccm/core/plan-design/configs/size-and-scale-numbers) をサポートします。 ただし、この構成により [System Center Configuration Manager の高可用性オプション](/sccm/protect/understand/high-availability-options) (SQL Server クラスターの使用など) が制限されることがあります。 また、SQL Server と Configuration Manager サイト サーバーの両方を同じコンピューターで実行する場合、その両方をサポートするためには高い I/O 要件が必要になるため、大規模な展開を使用するユーザーはリモート SQL Server コンピューターでの構成を使用することをお勧めします。  

###  <a name="bkmk_RemoteSiteSystem"></a> リモート サイト システム サーバー  
 以下のガイダンスは、1 つのサイト システムの役割を保有しているコンピューター用です。 複数のサイト システムの役割を同じコンピューターにインストールする場合は、調整を計画します。  

|サイト システムの役割|CPU (コア)|メモリ (GB)|ディスク領域 (GB)|  
|----------------------|---------------|---------------|--------------------|  
|管理ポイント|4|8|50|  
|配布ポイント|2|8|オペレーティング システムで必要とされ、展開するコンテンツを保存するために使用する|  
|サイト システム コンピューター上の Web サービスと Web サイトによるアプリケーション カタログ|4|16|50|  
|ソフトウェアの更新ポイント<sup>1</sup>|8|16|オペレーティング システムで必要とされ、展開する更新プログラムを保存するために使用する|  
|その他すべてのサイト システムの役割|4|8|50|  

 <sup>1</sup> ソフトウェアの更新ポイントをホストするコンピューターには、IIS アプリケーション プールの次の構成が必要です。  

-   **WsusPool キューの長さ** を **2000**に増やす  

-   **WsusPool プライベート メモリの制限** を 4 倍に増やすか、**0** (無制限) に設定する  

###  <a name="bkmk_DiskSpace"></a> サイト システムのディスク領域  
 ディスク割り当てと構成によって、Configuration Manager のパフォーマンスが向上します。 Configuration Manager 環境はそれぞれ異なるため、実装することの価値が以下のガイダンスとは異なる場合もあります。  

 最高のパフォーマンスを実現するには、個々の専用 RAID ボリュームに各オブジェクトを配置します。 また、最高のパフォーマンスを実現するには、すべてのデータ ボリューム (Configuration Manager およびそのデータベース ファイル) に RAID 10 を使用します。  

|データの使用|最小限のディスク領域|クライアント数 25,000|クライアント数 50,000|クライアント数 100,000|クライアント数 150,000|クライアント数 700,000 (中央管理サイト)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|オペレーティング システム|オペレーティング システムのガイダンスを参照してください。|オペレーティング システムのガイダンスを参照してください。|オペレーティング システムのガイダンスを参照してください。|オペレーティング システムのガイダンスを参照してください。|オペレーティング システムのガイダンスを参照してください。|オペレーティング システムのガイダンスを参照してください。|  
|Configuration Manager のアプリケーションおよびログ ファイル|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|サイト データベース .mdf ファイル|25,000 クライアントごとに 75 GB|75 GB|150 GB|300 GB|500 GB|2 TB|  
|サイト データベース .ldf ファイル|25,000 クライアントごとに 25 GB|25 GB|50 GB|100 GB|150 GB|100 GB|  
|一時データベース ファイル (.mdf および .ldf)|必要に応じて|必要に応じて|必要に応じて|必要に応じて|必要に応じて|必要に応じて|  
|コンテンツ (共有されている配布ポイント)|必要に応じて <sup>1</sup>|必要に応じて <sup>1</sup>|必要に応じて <sup>1</sup>|必要に応じて <sup>1</sup>|必要に応じて <sup>1</sup>|必要に応じて <sup>1</sup>|  

 <sup>1</sup> ディスク領域の指標には、サイト サーバーまたは配布ポイントのコンテンツ ライブラリに格納されるコンテンツに必要な領域は含まれません。 コンテンツ ライブラリの計画については、[コンテンツ ライブラリ](../../../core/plan-design/hierarchy/the-content-library.md)のトピックを参照してください。  

 ディスク領域の要件を計画する場合は、前述のガイダンスに加え、次のガイドラインを考慮してください。  

-   各クライアントには、約 5 MB の領域が必要です。  

-   プライマリ サイトの一時データベースのサイズを計画する場合、サイト データベース .mdf ファイルの 25% から 30% の合計サイズを計画します。 サイト サーバーのパフォーマンスや、短期および長期にわたって受信するデータのサイズに応じて、実際のサイズは大幅に小さく、または大きくなる可能性があります。  

    > [!NOTE]  
    >  サイトで 50,000 以上のクライアントを使用している場合は、4 つ以上の一時データベースの .mdf ファイルを使用するよう計画してください。  

-   中央管理サイトの一時データベース サイズは、通常、プライマリ サイトのサイズよりも大幅に小さくなります。  

-   セカンダリ サイトのデータベースには、次のサイズ制限があります。  

    -   SQL Server 2012 Express:10 GB  

    -   SQL Server 2014 Express:10 GB  

##  <a name="bkmk_ScaleClient"></a> クライアント  
 このセクションでは、Configuration Manager クライアント ソフトウェアを使用して管理するコンピューター用の推奨ハードウェア構成を示します。  

### <a name="client-for-windows-computers"></a>Windows コンピューターのクライアント  
 組み込みオペレーティング システムなど、Configuration Manager で管理する Windows ベースのコンピューターの最小要件は次のとおりです。  

-   **プロセッサとメモリ:** コンピューターのオペレーティング システムのプロセッサと RAM に関する要件を参照してください。  

-   **ディスク領域:** 500MB の空きディスク領域。Configuration Manager クライアントのキャッシュには、5 GB の空きディスク領域をお勧めします。 次に示すように、カスタマイズした設定を使用して Configuration Manager クライアントをインストールすると、必要とされるディスク領域が少なくなります。  

    -   CCMSetup のコマンドライン プロパティ /skipprereq を使用して、クライアントには不要なファイルがインストールされないようにします。 たとえば、クライアントがアプリケーション カタログを使用しない場合は、`CCMSetup.exe /skipprereq:silverlight.exe` を実行します。 Configuration Manager 1802 以降では、Silverlight は自動的にインストールされなくなりました。  

    -   Client.msi のプロパティ SMSCACHESIZE を使用して、既定の 5120 MB よりも小さいキャッシュ ファイルを設定します。 最小サイズは 1 MB です。 たとえば、`CCMSetup.exe SMSCachesize=2` ではサイズが 2 MB のキャッシュが作成されます。  

    クライアント インストールの設定について詳しくは、「[クライアント インストールのプロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」をご覧ください。  

    > [!TIP]  
    >  一般に、標準の Windows コンピューターよりもディスク サイズが小さい Windows Embedded デバイスの場合は、最小のディスク領域を使用するクライアントのインストールが実用的です。  



 Configuration Manager のオプション機能のための追加的な最小ハードウェア要件は、次のとおりです。  

-   **オペレーティング システムの展開:** 384 MB の RAM  

-   **ソフトウェア センター:** 500 MHz のプロセッサ  

-   **リモート コントロール:** Pentium 4 ハイパー スレッド 3 GHz (シングル コア) または同等の CPU。最適な結果を得るには少なくとも 1 GB の RAM が必要です  

### <a name="client-for-linux-and-unix"></a>Linux および UNIX 用のクライアント  
 以下は、Configuration Manager で管理する Linux および UNIX サーバーの最小要件です。  

|要件|詳細|  
|-----------------|-------------|  
|プロセッサとメモリ|コンピューターのオペレーティング システムのプロセッサと RAM に関する要件を参照してください。|  
|ディスク領域|500MB の空きディスク領域。Configuration Manager クライアントのキャッシュには、5 GB の空きディスク領域をお勧めします。|  
|ネットワーク接続|Configuration Manager のクライアント コンピューターには、管理を可能にするための、Configuration Manager サイト システムへのネットワーク接続が必要です。|  

##  <a name="bkmk_ScaleConsole"></a> Configuration Manager コンソール  
 次の表に示された要件は、Configuration Manager コンソールを実行する各コンピューターに適用されます。  

 **最小ハードウェア構成:**  

-   Intel i3 または同等の CPU  

-   2 GB の RAM  

-   2 GB のディスク領域  

|DPI 設定|最小解像度|  
|-----------------|------------------------|  
|96/100%|1024 x 768|  
|120/125%|1280 x 960|  
|144/150%|1600 x 1200|  
|196/200%|2500 x 1600|  

 **PowerShell のサポート:**  

 Configuration Manager コンソールを実行するコンピューターに PowerShell のサポートをインストールすると、そのコンピューターで Configuration Manager を管理するために PowerShell のコマンドレットを実行できるようになります。

 - PowerShell 3.0 以降がサポートされています。

PowerShell のほかに、Windows Management Framework (WMF) Version 3.0 以降もサポートされます。   


##  <a name="bkmk_ScaleLab"></a> ラボ展開  
 Configuration Manager のラボ展開とテストの展開には、次の最小ハードウェア推奨事項を使用します。 これらの推奨事項はすべてのサイトの種類に適用され、最大 100 のクライアントで使用する場合のものです。  

|ロール|CPU (コア)|メモリ (GB)|ディスク領域 (GB)|  
|----------|---------------|-------------------|-----------------------|  
|サイトとデータベース サーバー|2 - 4|8 - 12|100|  
|サイト システム サーバー|1 - 4|2 - 4|50|  
|クライアント|1 - 2|1 - 3|30|  
