---
title: "セットアップ リファレンス | System Center Configuration Manager"
description: "Configuration Manager サイトまたは階層をインストールするための準備をするには、このリファレンスを参照してください。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 06bab7e01fee2c0b030a2879fa67fd455bf668fe


---
# <a name="reference-for-system-center-configuration-manager-setup"></a>System Center Configuration Manager のセットアップのリファレンス

*適用対象: System Center Configuration Manager (Current Branch)*

「System Center Configuration Manager のセットアップ」には、他のトピックへのリンクが掲載されています。詳細については、以下のセクションを参照してください。 以下のセクションの情報は、Configuration Manager サイトまたは階層のインストールの準備、およびインストール中に決定する必要があるいくつかの事項についての準備に役立ちます。  

-   [始める前に](#bkmk_start)  

-   [サーバーの準備状態の評価](#bkmk_assess)  

-   [追加のオペレーティング システム用のクライアント](#bkmk_Addclients)  

-   [System Center Configuration Manager の診断結果と使用状況データ](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)  

##  <a name="a-namebkmkstarta-before-you-begin"></a><a name="bkmk_start"></a> 始める前に  
 新しい Configuration Manager サイトをインストールする前に、展開を正常に設計するためのステージの設定に役立つ次の情報を必ずご確認ください。  

-   [System Center Configuration Manager の基本](../../../../core/understand/fundamentals.md)  

-   [System Center Configuration Manager インフラストラクチャの計画](../../../plan-design/network/configure-firewalls-ports-domains.md)  

-   [System Center Configuration Manager サイトのインストールを準備する](prepare-to-install-sites.md)  

##  <a name="a-namebkmkassessa-assess-server-readiness"></a><a name="bkmk_assess"></a> サーバーの準備状態の評価  
 新しいサイトのインストールを開始する前に、サイトに使用しようとしているサイト サーバーとリモート サイト システム サーバー (サイト データベースをホストするサーバーなど) がすべての前提条件の構成を満たしていることを確認します。 ドキュメント ライブラリの以下のトピックは、次の対象に役立ちます。  

-   [System Center Configuration Manager のサポートされている構成](../../../../core/plan-design/configs/supported-configurations.md)  

-   [前提条件チェッカー](https://technet.microsoft.com/library/mt590813.aspx#bkmk_PreqChk)  

##  <a name="a-namebkmkaddclientsa-clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> 追加のオペレーティング システム用のクライアント  
 Microsoft ダウンロード センターから、次のオペレーティング システム向けの Configuration Manager のクライアント ソフトウェアをダウンロードできます。  

-   Mac (Apple)  

-   UNIX  

-   Linux  

**次のリンクを使用して、使用する Configuration Manager のバージョンのクライアントをダウンロードします。**  

-   [System Center Configuration Manager (現在のブランチ)](http://www.microsoft.com/download/details.aspx?id=47719)  

-   [System Center 2012 R2 Configuration Manager SP1 および System Center 2012 Configuration Manager SP2](http://go.microsoft.com/fwlink/?LinkID=626550)  

-   [System Center 2012 R2 Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=316448)  

-   [System Center 2012 Configuration Manager SP1](http://www.microsoft.com/en-pk/download/details.aspx?id=36212)  

##  <a name="a-namebkmkusagea-usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> 使用状況データのレベルと設定  
最初の System Center Configuration Manager サイトをインストールすると、次の既定設定でサイト サーバーの**サービス接続ポイント**に新しいサイト システムの役割が自動的にインストールされ、構成されます。  

-   **オンライン** モード (オフライン モードもサポートされています)  

-   **拡張** のデータ コレクション レベル (2 つの他のデータ コレクションのレベルとして基本と完全がサポートされています)  

この役割がオンラインの場合、Microsoft が自動的にインターネット経由で診断と使用状況の情報を収集することができます。 収集された情報は次のことに役立ちます。  

-   問題の識別とトラブルシューティング  

-   Microsoft の製品やサービスの向上  

-   使用する Configuration Manager のバージョンに適用する Configuration Manager の更新プログラムの識別  

データ コレクションの 3 つのレベルは次のとおりです。  

-   **基本** には、サイトの数や有効になる Configuration Manager 機能など、セットアップとアップグレードに関するデータが含まれます。 個人を特定できる情報は送信されません。  

-   **拡張** には、基本設定内のデータが含まれるだけでなく、階層に関するデータ、各機能の使用方法 (頻度と期間)、システムまたはアプリのクラッシュが発生した場合のサーバーのメモリ状態などの詳細な診断情報が送信されます。 個人を特定できるデータは送信されません。  

-   **完全** には、基本設定と拡張設定内のデータが含まれるだけでなく、システム ファイルやメモリ スナップショットなどの高度な診断情報も送信されます。 このオプションには個人を特定できる情報が含まれる場合がありますが、その情報を使用して個人を特定して連絡したり、広告のターゲットにしたりすることはありません。  

各レベルで収集した詳細情報の漏えいを含む詳細については、「[System Center Configuration Manager の診断結果と使用状況データ](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)」を参照してください。  

[System Center Configuration Manager のプライバシーに関する声明](http://go.microsoft.com/fwlink/?LinkID=626527)



<!--HONumber=Nov16_HO1-->


