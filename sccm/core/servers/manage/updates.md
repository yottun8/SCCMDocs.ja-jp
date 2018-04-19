---
title: 更新プログラムとサービス
titleSuffix: Configuration Manager
description: 推奨更新プログラムを簡単に特定してインストールできる、更新とサービスと呼ばれるコンソール内サービス方式について説明します。
ms.custom: na
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
caps.latest.revision: 51
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7660736dbacebb7167cb6bd19d7590d7f774e17c
ms.sourcegitcommit: aed99ba3c5e9482199cb3fc5c92f6f3a160cb181
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2018
---
# <a name="updates-for-system-center-configuration-manager"></a>System Center Configuration Manager の更新プログラム

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager では、**更新とサービス**と呼ばれるコンソール内でのサービス提供方式が採られています。 このコンソール内での方式により、使用している Configuration Manager インフラストラクチャに推奨される更新プログラムを簡単に特定し、インストールすることができます。 コンソール内でのサービス提供は、環境固有の問題を解決する必要があるお客様向けの修正プログラムなど、アウトオブバンドの更新プログラムによって補完されます。  

> [!TIP]  
> System Center Configuration Manager のサイトと階層のインフラストラクチャの管理において、*アップグレード*、*更新*、および*インストール* という用語は 3 つの異なる概念を説明するものです。 各用語の使用方法については、「[サイトと階層のインフラストラクチャでのアップグレード、更新、およびインストールについて](/sccm/core/understand/upgrade-update-install)」を参照してください。


 **次のトピックは、System Center Configuration Manager 向けのさまざまな更新プログラムを探してインストールする方法を理解するうえで役立ちます。**  

-   [System Center Configuration Manager のコンソール内の更新プログラムのインストール](../../../core/servers/manage/install-in-console-updates.md)  

-   [System Center Configuration Manager のサービス接続ツールの使用](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [更新登録ツールを使用して修正プログラムを System Center Configuration Manager にインポートする](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [修正プログラム インストーラーを使用して、System Center Configuration Manager の更新プログラムをインストールする](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


Technical Preview ブランチを使用する場合は、「[System Center Configuration Manager の Technical Preview](/sccm/core/get-started/technical-preview)」でブランチに固有の追加情報を参照してください。


##  <a name="bkmk_Baselines"></a> 基準バージョンと更新プログラムのバージョン  
 System Center Configuration Manager の現在のブランチの最初のリリースは、バージョン 1511 です。これが基準バージョンです。 最新の基準バージョンにはバージョン 1702 と 1802 が含まれています。

-   新しい階層に新しいサイトをインストールするときは、最新の基準バージョンを使用してください。  

-   System Center 2012 Configuration Manager からアップグレードする際には基準バージョンを使用します。 System Center Configuration Manager にアップグレードしたら、最新状態を維持するために基準バージョンを使用できなくなり、代わりに[コンソール内更新](/sccm/core/servers/manage/install-in-console-updates)のみを使用して、最新バージョンに更新できます。  

-   新しい基準バージョンは定期的にリリースされます。 最新の基準バージョンを使用して新しい階層をインストールする場合、古いバージョンの Configuration Manager をインストールした後に、インフラストラクチャの追加のアップグレードを実行して最新の状態にしないでください。  

基準バージョンのインストール後、Configuration Manager の新バージョンはコンソール内の更新プログラムとして提供されます。 コンソール内の更新プログラムにより、インフラストラクチャは最新バージョンの Configuration Manager に更新されます。  

-   最上位サイトのバージョンを更新するには、コンソール内の更新プログラムをインストールしてください。  

-   中央管理サイトにインストールした更新プログラムは、子のプライマリ サイトに自動的にインストールされます。ただし、プライマリ サイトで構成してあるメンテナンス期間によりブロックされる場合は除きます。  

-   セカンダリ サイトについては、コンソールから手動で新しい更新プログラムのバージョンに更新する必要があります。  

更新プログラムをインストールすると、サイト サーバーの CD.Latest という名前のフォルダーにそのバージョンのインストール ファイルが格納されます。 これらのファイルの詳細については、「[System Center Configuration Manager の CD.Latest フォルダー](../../../core/servers/manage/the-cd.latest-folder.md)」を参照してください。  

-   CD.Latest フォルダー内のファイルは、サイトの回復中と、基準バージョンが実行されない階層に別のサイトをインストールする際に使用します。  

-   CD.Latest 内のインストール ファイルを使用して新しい階層の最初のサイトをインストールしたり、サイトを System Center 2012 Configuration Manager からアップグレードしたりすることはできません。  

Configuration Manager の一部の更新プログラムは、既存のインフラストラクチャ向けのコンソール内の更新バージョンとして使用することも、新しい基準バージョンとして使用することもできます。  

Configuration Manager の次のバージョンは、基準バージョンと更新バージョンのどちらか一方または両方として利用できます。  

|バージョン |公開日|[サポート終了日](/sccm/core/servers/manage/current-branch-versions-supported) |Baseline|コンソール内の更新プログラム|  
|-------------|-----------|------------|--------------|------------------------|  
|[1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)<br /><br /> 5.00.8634.1000|2018 年 3 月 22 日|2019 年 9 月 22 日|はい|はい|
|[1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)<br /><br /> 5.00.8577.1000|2017 年 11 月 20 日|2019 年 5 月 20日|いいえ|はい|
|[1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)<br /><br /> 5.00.8540.1000|2017 年 7 月 31 日|2018 年 7 月 31 日|いいえ|はい|
|[1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)<br /><br /> 5.00.8498.1000|2017 年 3 月 27 日| 2018 年 3 月 27 日|はい|はい|
|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)<br /><br /> 5.00.8458.1000|2016 年 11 月 18 日| 2017 年 11 月 18 日|いいえ|はい|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)<br /><br /> 5.00.8412.1000|2016 年 7 月 22 日| 2017 年 7 月 22 日|いいえ|はい|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606) と 1606 修正プログラム ロールアップ (KB3186654) </br></br>5.00.8412.1307 *(注 1)* |2016 年 10 月 12 日| 2017 年 10 月 12 日|はい|いいえ|
| 1602<br /><br /> 5.00.8355.1000|2016 年 3 月 11 日| 2017 年 3 月 11 日|いいえ|はい|
| 1511 <br /><br /> 5.00.8325.1000|2015 年 12 月 8 日| 2016 年 12 月 8 日|はい|いいえ|  


*(注 1)* この 1802 および 1702 基準メディアは、Microsoft System Center 2016 または System Center Configuration Manager (Current Branch および Long-Term Servicing Branch) リリースの一部として[ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC) で使用できます。 たとえば、VLSC で、*System Center Config Mgr (current branch および LTSB)* を検索すると、1802 と 1702 の両方のバージョンの構成基準メディアが返され、ダウンロードできます。

お使いの Configuration Manager サイトのバージョンを確認するには、コンソールの左上隅にある **[System Center Configuration Manager について]** に移動してください。ここに新しいサイトとコンソールのバージョンが表示されます。  

 > [!Note]  
 > バージョン 1802 以降、コンソール バージョンがサイト バージョンと若干異なります。 コンソールのマイナー バージョンは、Configuration Manager リリース バージョンに対応するようになりました。 たとえば、Configuration Manager バージョン 1802 では、初回のサイト バージョンは 5.0.8634.1000 で、初回のコンソール バージョンは 5.**1802**.1082.1700 です。 ビルド (1082) とリビジョン (1700) の番号は、1802 リリースの今後の修正プログラムによって変わることがあります。


##  <a name="bkmk_inconsole"></a> コンソール内の更新プログラムとサービス  
 System Center Configuration Manager の運用環境対応バージョン (Current Branch とも呼ばれます) を使用する場合、インストールする更新プログラムのほとんどは、更新プログラムとサービス チャネルを通じて入手できます。 この方式では、現在のインフラストラクチャ バージョンと構成に適用される更新プログラムが特定され、ダウンロードのうえ、利用可能になります。また、Microsoft がすべてのお客様にお勧めする更新プログラムのみが対象となります。   
 次の設定があります。  

-   新しいバージョン (バージョン 1702、1706、1710、1802 など)。  

-   現在のバージョンに対する新機能が含まれる更新プログラム。

-   すべてのお客様にインストールしていただく必要のある、使用中の Configuration Manager のバージョン向けの修正プログラム。

コンソール内の更新プログラムにより、安定性が向上し、一般的な問題が解決します。 コンソール内の更新プログラムは、以前の製品バージョンの Service Pack で利用されていた種類の更新プログラムや、累積的な更新プログラム、すべてのお客様が対象の修正プログラム、Microsoft Intune 向けの拡張機能の代わりになるものです。 こうした更新プログラムは以下のものに適用できます。  

-   プライマリおよび中央管理サイト サーバー  

-   サイト システムの役割とサイト システム サーバー  

-   SMS プロバイダーのインスタンス  

-   Configuration Manager コンソール  

-   Configuration Manager クライアント  

サービス接続ポイントのサイト システムの役割を Microsoft クラウド サービスおよびダウンロード センターと同期すると、Configuration Manager によって新しい更新プログラムが自動的に検出されます。  

-   サービス接続ポイントがオンライン モードになっているとき、サイトは Microsoft と毎日同期され、自分のインフラストラクチャに適用される新しい更新プログラムが自動的に特定されます。  更新プログラムと更新プログラムの再頒布ファイルをダウンロードするために、サービス接続ポイントのサイト システムの役割をホストするコンピューターは、**System** コンテキストを使用して、インターネット上の go.microsoft.com と download.microsoft.com にアクセスします。サービス接続ポイントが接続するその他の場所については、「[System Center Configuration Manager のサービス接続ポイントについて](../../../core/servers/deploy/configure/about-the-service-connection-point.md)」の「[インターネット アクセス要件](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls)」を参照してください。  

-   サービス接続ポイントがオフライン モードになっている場合は、サービス接続ツールを使って Microsoft クラウドと手動で同期してください。 詳細については、「 [System Center Configuration Manager のサービス接続ツールの使用](../../../core/servers/manage/use-the-service-connection-tool.md)」を参照してください。  

-   コンソール内の更新プログラムを利用すれば、個々の更新プログラム、Service Pack、新しい機能を個別に特定してインストールする必要がなくなります。  

-   選んだコンソール内の更新プログラムだけをインストールすれば済みます。一部の更新プログラムをインストールする際には、有効にして使用する個別の機能を選ぶことができます。 詳細については、「[Enable optional features from updates](../../../core/servers/manage/install-in-console-updates.md#bkmk_options)」 (更新プログラムのオプション機能の有効化) を参照してください。  

コンソール内の更新プログラムをインストールする際には、次の処理が行われます。  

-   前提条件の確認が自動的に実行されます。 この確認は、インストールの開始前にも実行できます。  

-   更新プログラムは中央管理サイト (このサイトが存在する場合) とプライマリ サイトに自動的にインストールされます。 [サイト サーバーのサービス期間](../../../core/servers/manage/service-windows.md)を利用することで、各プライマリ サイト サーバーでインフラストラクチャを更新するタイミングを制御できます。  

-   サイト サーバーが更新されると、関係するサイト システムの役割がすべて自動的に更新されます (SMS プロバイダーのインスタンスを含む)。 サイトに更新プログラムがインストールされた後で、Configuration Manager コンソールからコンソール ユーザーに対してコンソールの更新を求めるメッセージが表示されます。  

-   更新プログラムに Configuration Manager クライアントが含まれている場合は、運用前に更新プログラムをテストするか、すべてのクライアントに更新プログラムを即座に適用するかを選べます。  

-   プライマリ サイトが更新されても、セカンダリ サイトは自動的には更新されません。 そのため、セカンダリ サイトの更新を手動で開始する必要があります。  

> [!NOTE]  
>  System Center Configuration Manager (Current Branch) の実稼働リリース、Long-Term Servicing Branch、および System Center Configuration Manager の Technical Preview は、異なるリリースです。 したがって、1 つのブランチに適用される更新プログラムでは、他のブランチのコンソール内の更新プログラムには使用できません。 使用可能なブランチの詳細については、「[適切な Configuration Manager のブランチを選択する](/sccm/core/understand/which-branch-should-i-use)」を参照してください。

##  <a name="bkmk_outofband"></a> アウトオブバンドの修正プログラム  
修正プログラムによっては、特定の問題に対処するために対象を限定してリリースされるものや、すべてのお客様に適用可能であるものの、コンソール内の方式でインストールできないものもあります。 これらの修正プログラムはアウトオブバンドで提供され、Microsoft クラウド サービスでは検出されません。  

通常、アウトオブバンドの修正プログラムについては、Configuration Manager の展開に伴う問題を解決する方法を探しているときに、Microsoft カスタマー サポート サービス、サポート技術情報の記事、[System Center Configuration Manager チーム ブログ](https://blogs.technet.microsoft.com/configmgrteam)を通じて調べることができます。  

こうした更新プログラムは、以下の 2 つの方法のどちらかを使用して手動でインストールします。  

-   **更新登録ツール:** このツールを使うと、修正プログラムを手動で Configuration Manager コンソールにインポートできます。その後、自動的に検出されるコンソール内の更新プログラムと同様に、コンソールで更新プログラムをインストールできます。 この方式は、 **.update.exe**というファイル名の構造を持つ更新プログラムに使用されます。  この種の修正プログラムの完全なファイル名は、**&lt;製品\>-&lt;製品バージョン\>-&lt;サポート技術情報の記事 ID\>-ConfigMgr.Update.exe** となります。  

     詳細については、「[修正プログラムを System Center Configuration Manager にインポートするには、更新登録ツールを使用します](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)」を参照してください。  

-   **修正プログラムのインストーラー:** このツールは、コンソール内の方式でインストールできない修正プログラムをインストールするために使用されます。 この方式は、**&lt;製品\>-&lt;製品バージョン\>-&lt;サポート技術情報の記事 ID\>-&lt;プラットフォーム\>-&lt;言語\>.exe** というファイル名の構造を持つ更新プログラムに使用されます。

     詳細については、「[Use the Hotfix Installer to install updates for System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)」 (修正プログラム インストーラーを使用して、System Center Configuration Manager の更新プログラムをインストールする) を参照してください。
