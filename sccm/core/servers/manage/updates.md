---
title: 更新プログラムとサービス
titleSuffix: Configuration Manager
description: 推奨される更新プログラムを簡単に検索してインストールできる、更新とサービスと呼ばれるコンソール内サービス方式について説明します。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1acc1bd6a6ccbd010308d026933a371f9e8227d8
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456551"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>Configuration Manager の更新とサービス

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager では、**更新とサービス**と呼ばれるコンソール内でのサービス提供方式が採られています。 このコンソール内での方式により、使用している Configuration Manager インフラストラクチャに推奨される更新プログラムを簡単に特定し、インストールすることができます。 コンソール内でのサービス提供は、修正プログラムなどのアウトオブバンド更新プログラムによって補完されます。 アウトオブバンド更新プログラムは、環境固有である可能性がある問題を解決する必要があるお客様向けです。  

> [!TIP]  
> *アップグレード*、*更新*、*インストール*という言葉は、Configuration Manager における 3 つの異なる概念を表すために使用されています。 各用語の使用方法については、[アップグレード、更新、インストール](/sccm/core/understand/upgrade-update-install)に関するページを参照してください。  



##  <a name="bkmk_Baselines"></a> 基準バージョンと更新プログラムのバージョン  

新しい階層に新しいサイトをインストールするときは、最新の基準バージョンを使用してください。 
- また、System Center 2012 Configuration Manager からアップグレードする際には基準バージョンを使用してください。  

- Configuration Manager Current Branch にアップグレードした後は、最新の状態に維持する目的で基準バージョンを使用しないでください。 代わりに、[コンソール内の更新プログラム](/sccm/core/servers/manage/install-in-console-updates)を使用し、最新バージョンに更新してください。  

- 新しい基準バージョンは定期的にリリースされます。 最新の基準バージョンを使用して新しい階層をインストールする場合、古い (サポートされていない) バージョンの Configuration Manager をインストールした後に、インフラストラクチャの追加のアップグレードを実行して最新の状態にしないでください。  

基準バージョンのインストール後、Configuration Manager の新バージョンはコンソール内の更新プログラムとして提供されます。 コンソール内の更新プログラムにより、インフラストラクチャは最新バージョンの Configuration Manager に更新されます。  

-   最上位サイトのバージョンを更新するには、コンソール内の更新プログラムをインストールしてください。  

-   中央管理サイトに更新プログラムをインストールすると、子プライマリ サイトにも自動的にインストールされます。 このタイミングを変更するには、プライマリ サイトのメンテナンス期間を利用します。  

-   セカンダリ サイトについては、コンソール内から手動で新しい更新プログラム バージョンに更新します。  

更新プログラムをインストールすると、サイト サーバーの **CD.Latest** という名前のフォルダーにそのバージョンのインストール ファイルが格納されます。 CD.Latest フォルダーの詳細については、[CD.Latest フォルダー](/sccm/core/servers/manage/the-cd.latest-folder)に関するページを参照してください。  

-   サイト回復のとき、CD.Latest フォルダーに入っているファイルを使用します。 また、階層で基準バージョンを実行しなくなった場合、CD.Latest フォルダーのファイルで追加サイトをインストールします。  

-   CD.Latest 内のインストール ファイルを使用して新しい階層の最初のサイトをインストールしたり、サイトを System Center 2012 Configuration Manager からアップグレードしたりすることはできません。  


### <a name="version-details"></a>バージョンの詳細

Configuration Manager の一部の更新プログラムは、既存のインフラストラクチャ向けのコンソール内の更新バージョンとして使用することも、新しい基準バージョンとして使用することもできます。  

#### <a name="supported-versions"></a>サポートされるバージョン
Configuration Manager の次のサポート対象バージョンは、現在、基準と更新バージョンのどちらか一方または両方として利用できます。  

| バージョン | 公開日 | [サポート終了日](/sccm/core/servers/manage/current-branch-versions-supported) | Baseline | コンソール内の更新プログラム |  
|-------------|-----------|------------|--------------|------------------------|  
| [1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)<br /><br /> 5.00.8740.1000 | 2018 年 11 月 27 日 | 2020 年 5 月 27 日 | いいえ | はい |
| [1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)<br /><br /> 5.00.8692.1000 | 2018 年 7 月 31 日 | 2020 年 1 月 31 日 | いいえ | はい |
| [1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)<br /><br /> 5.00.8634.1000 | 2018 年 3 月 22 日 | 2019 年 9 月 22 日 | はい<sup>[注 1](#bkmk_note1)</sup> | はい |
| [1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)<br /><br /> 5.00.8577.1000 | 2017 年 11 月 20 日 | 2019 年 5 月 20日 | いいえ | はい |

<a name="bkmk_note1"></a> 

> [!Note]  
> <sup>**注 1**</sup>: 1802 基準メディアは、[ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC) で次のリリースの一部として利用できます。
> - System Center Config Mgr (Current Branch)
> - System Center 2016 Datacenter
> - System Center 2016 Standard  
> 
> たとえば、`System Center Config Mgr (current branch)` という VLSC を探してみてください。 ファイルの一覧で 1802 基準メディアを見つけ、そのリリースでダウンロードしてください。  

#### <a name="historical-versions"></a>過去のバージョン
次の表に、サポート対象外である Configuration Manager Current Branch の過去のバージョンを一覧表示します。

| バージョン | 公開日 | サポート終了日 | Baseline | コンソール内の更新プログラム |  
|-------------|-----------|------------|--------------|------------------------|  
| 1706 <br /><br /> 5.00.8540.1000 | 2017 年 7 月 31 日 | 2018 年 7 月 31 日 | いいえ | はい |
| 更新プログラム 1702 を含む <br /><br /> 5.00.8498.1000 | 2017 年 3 月 27 日 | 2018 年 3 月 27 日 | はい | はい |
| 1610 <br /><br /> 5.00.8458.1000 | 2016 年 11 月 18 日 | 2017 年 11 月 18 日 | いいえ | はい |
| 1606 <br /><br /> 5.00.8412.1000 | 2016 年 7 月 22 日 | 2017 年 7 月 22 日 | いいえ | はい |
| 1606 と 1606 修正プログラム ロールアップ (KB3186654) <br><br>5.00.8412.1307 | 2016 年 10 月 12 日 | 2017 年 10 月 12 日 | はい | いいえ |
| 1602<br /><br /> 5.00.8355.1000 | 2016 年 3 月 11 日 | 2017 年 3 月 11 日 | いいえ | はい |
| 1511 <br /><br /> 5.00.8325.1000 | 2015 年 12 月 8 日 | 2016 年 12 月 8 日 | はい | いいえ |  

#### <a name="how-to-check-the-version"></a>バージョンの確認方法
Configuration Manager サイトのバージョンを確認するには、コンソールの左上隅にある **[System Center Configuration Manager のバージョン情報]** を選択します。 このダイアログには、サイトとコンソールのバージョンが表示されます。  

 > [!Note]  
 > バージョン 1802 以降、コンソール バージョンがサイト バージョンと若干異なります。 コンソールのマイナー バージョンは、Configuration Manager リリース バージョンに対応するようになりました。 たとえば、Configuration Manager バージョン 1802 では、初回のサイト バージョンは 5.0.8634.1000 で、初回のコンソール バージョンは 5.**1802**.1082.1700 です。 ビルド (1082) とリビジョン (1700) の番号は、1802 リリースの今後の修正プログラムによって変わることがあります。



##  <a name="bkmk_inconsole"></a> コンソール内の更新プログラムとサービス  

Configuration Manager の運用環境対応バージョン (Current Branch) を使用する場合、更新プログラムのほとんどは**更新プログラムとサービス** チャネルを通じて入手できます。 この方式では、現在のインフラストラクチャ バージョンと構成に適用される更新プログラムが特定され、ダウンロードの上、利用可能になります。 Microsoft がすべてのお客様にお勧めする更新プログラムのみが対象となります。   

そのような更新プログラムには次が含まれます。  

-   新しいバージョン (バージョン 1802、1806、1810 など)。  

-   現在のバージョンに対する新機能が含まれる更新プログラム。

-   すべてのお客様にインストールしていただく必要のある、使用中の Configuration Manager のバージョン向けの修正プログラム。

コンソール内の更新プログラムにより、安定性が向上し、一般的な問題が解決します。 コンソール内の更新プログラムは、Service Pack、累積的な更新プログラム、すべてのお客様が対象の修正プログラム、Microsoft Intune 向けの拡張機能など、以前の製品バージョンで利用されていた種類の更新プログラムの代わりになるものです。 

コンソール内の更新プログラムは次のシステムに適用できます。  

-   プライマリおよび中央管理サイト サーバー  

-   サイト システムの役割とサイト システム サーバー  

-   SMS プロバイダーのインスタンス  

-   Configuration Manager コンソール  

-   Configuration Manager クライアント  

Configuration Manager によって新しい更新プログラムが自動検出されます。 Configuration Manager サービス接続ポイントと Microsoft クラウド サービスを同期します。次の動作にご留意ください。  

-   サービス接続ポイントがオンライン モードのとき、サイトは Microsoft と毎日同期します。 お使いのインフラストラクチャに適用される新しい更新プログラムが自動的に特定されます。 更新プログラムと再頒布ファイルをダウンロードするために、サービス接続ポイントのサイト システムの役割をホストするコンピューターは、**System** コンテキストを使用して、インターネット上の go.microsoft.com と download.microsoft.com にアクセスします。 サービス接続ポイントによって使用される追加の場所については、「[インターネット アクセス要件](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)」をご覧ください。  

-   サービス接続ポイントがオフライン モードになっている場合は、サービス接続ツールを使って Microsoft クラウドと手動で同期してください。 詳細については、[サービス接続ツールの使用](/sccm/core/servers/manage/use-the-service-connection-tool)に関するページを参照してください。  

-   コンソール内の更新プログラムを利用すれば、個々の更新プログラム、Service Pack、新しい機能を個別に特定してインストールする必要がなくなります。  

-   選択したコンソール内更新プログラムのみをインストールします。 一部の更新プログラムをインストールするとき、有効にして使用する個々の機能を選択できます。 詳細については、「[Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」 (更新プログラムのオプション機能の有効化) を参照してください。  

コンソール内更新プログラムをインストールするとき、次のプロセスが行われます。  

-   前提条件の確認が自動的に実行されます。 この確認は、インストールの開始前にも手動で実行できます。  

-   お使いの環境の最上位サイトにインストールされます。 中央管理サイトがある場合、それが最上位サイトとなります。 階層では、更新プログラムは自動的にプライマリ サイトでインストールされます。 [サイト サーバーのサービス ウィンドウ](/sccm/core/servers/manage/service-windows)を利用することで、各プライマリ サイト サーバーで更新するタイミングを制御します。  

-   サイト サーバーが更新されると、関係するサイト システムの役割がすべて自動的に更新されます。 これらのロールには、SMS プロバイダーのインスタンスが含まれます。 また、サイトに更新プログラムがインストールされた後で、Configuration Manager コンソールからコンソール ユーザーに対してコンソールの更新を求めるメッセージが表示されます。  

-   更新プログラムに構成マネージャー クライアントが含まれている場合は、運用前に更新プログラムをテストするか、すべてのクライアントに更新プログラムをすぐに適用するかを選べます。  

-   プライマリ サイトが更新されても、セカンダリ サイトは自動的には更新されません。 そのため、セカンダリ サイトの更新を手動で開始する必要があります。  

> [!NOTE]  
>  Configuration Manager の Current Branch、Long-Term Servicing Branch、Technical Preview Branch は異なるリリースです。 そのため、あるブランチに適用される更新プログラムは、他のブランチのコンソール内更新プログラムとして利用できません。 使用可能なブランチの詳細については、「[適切な Configuration Manager のブランチを選択する](/sccm/core/understand/which-branch-should-i-use)」を参照してください。



##  <a name="bkmk_outofband"></a> アウトオブバンドの修正プログラム  

修正プログラムには、特定の問題に対処する目的で利用対象が限られるものがあります。 それ以外の修正プログラムはすべてのお客様がご利用いただけますが、コンソール内の方式ではインストールできません。 これらの修正プログラムはアウトオブバンドで提供され、Microsoft クラウド サービスでは検出されません。  

通常、アウトオブバンドの修正プログラムについては、Configuration Manager の展開に伴う問題を解決する方法を探しているときに、Microsoft カスタマー サポート サービス、サポート技術情報の記事、Enterprise Mobility + Security ブログでの [System Center Configuration Manager チームからの投稿](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager)を通じて調べることができます。 

このような更新プログラムは、以下の 2 つの方法のいずれかを利用して手動でインストールします。  

#### <a name="update-registration-tool"></a>更新登録ツール
このツールでは、Configuration Manager コンソールに修正プログラムを手動でインポートします。 その後、自動的に検出されたコンソール内更新プログラムの場合と同じように更新プログラムをインストールします。  

この方式は、次のファイル名構造を使用する修正プログラムに使用されます。  
  `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`    

詳細については、[更新登録ツールを使用して修正プログラムをインポートする](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)方法に関するページを参照してください。  

#### <a name="hotfix-installer"></a>修正プログラム インストーラー
このツールを使用して、コンソール内の方式を使用してインストールできない修正プログラムを手動でインストールします。  

この方式は、次のファイル名構造を使用する修正プログラムに使用されます。   
   `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

詳細については、[修正プログラム インストーラーを使用して更新プログラムをインストールする](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates)方法に関するページを参照してください。  



## <a name="next-steps"></a>次のステップ

次の記事は、Configuration Manager 向けのさまざまな更新プログラムを見つけてインストールする方法を理解する上で役立ちます。  

-   [コンソール内の更新プログラムのインストール](/sccm/core/servers/manage/install-in-console-updates)  

-   [サービス接続ツールの使用](/sccm/core/servers/manage/use-the-service-connection-tool)  

-   [更新登録ツールを使用して修正プログラムをインポートする](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

-   [修正プログラム インストーラーを使用して更新プログラムをインストールする](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates)  


Technical Preview Branch の詳細については、[Technical Preview](/sccm/core/get-started/technical-preview) に関するページを参照してください。
