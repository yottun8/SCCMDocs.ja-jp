---
title: SCAP 拡張機能
titleSuffix: Configuration Manager
description: Configuration Manager の Security Content Automation Protocol (SCAP) 拡張機能について説明します。
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e42027663f06bff715cb7e9087ececbc421cc495
ms.sourcegitcommit: 013ca76d5a3c07306de7b5bfd985b0289d1be599
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "55482454"
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>Security Content Automation Protocol (SCAP) 拡張機能について

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager の SCAP 拡張機能は、Security Content Automation Protocol (SCAP) に準拠するためにネットワーク環境の分析と評価を実行するのに役立ちます。 SCAP は、米国標準技術研究所 (NIST) によって定義および管理されています。 詳細については、[SCAP プロジェクトの概要](https://csrc.nist.gov/projects/security-content-automation-protocol)を参照してください。

> [!Note]  
> このバージョンのツールは、バージョン 1806 でのみ利用できるプレリリース機能です。 このバージョンは、NIST に認定されていません。 <!--SCCMDocs-pr issue 3323-->
> 
> 認定されたツールが必要な場合、または別のバージョンの Configuration Manager Current Branch を使っている場合は、次のバージョンの SCAP 拡張機能を使います。
> - [System Center Configuration Manager の SCAP 拡張機能のダウンロード](https://www.microsoft.com/download/details.aspx?id=48741)
> - [SCAP 拡張機能バージョン 3.0 に関するドキュメント](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/mt228311\(v%3dtechnet.10\))

Configuration Manager の SCAP 拡張機能では、コンプライアンス設定機能を使用して、まず環境内のコンピューターをスキャンします。 次に、United States Government Configuration Baseline (USGCB) へのコンプライアンスのレベルを文書化します。

拡張機能は、Configuration Manager が SCAP データ ストリームを使用して、システムの対応状態を評価し、レポートの結果を SCAP 形式で生成できるようにします。 組織では、既存の Configuration Manager インフラストラクチャを使用して、管理するコンピューターがこの連邦政府のコンプライアンス要件を満たすようにすることができます。 Configuration Manager を使用して、NIST および米国行政管理予算局 (OMB) が要求する USGCB レポートも生成します。

この記事では、Configuration Manager インフラストラクチャでの SCAP 拡張機能のインストール、構成、実行に役立つ情報を提供します。



## <a name="whats-new"></a>新機能

このバージョンの Configuration Manager の SCEP 拡張機能には、次の機能が含まれ、サポートされています。  

- コンプライアンス設定基準への SCAP コンテンツの変換をサポートする Configuration Manager コンソール拡張機能。  

- 次のコンポーネントを含む SCAP バージョン 1.2。  

  - 拡張可能な構成のチェックリストの説明形式 (XCCDF) バージョン 1.2
  - Open Vulnerability and Assessment Language (OVAL) バージョン 5.10 まで
  - 資産レポート形式 (ARF) 1.1 のレポートの生成
  - 共通プラットフォーム一覧 (CPE) 2.3
  - 共通脆弱性識別子 (CVE)
  - 共通セキュリティ設定一覧 (CCE) バージョン 5
  - USGCB Internet Explorer 8、USGCB Windows 7、USGCB Windows 7 Firewall  

- SCAP バージョン 1.1 および 1.0 との下位互換性。  

- 構成基準に変換するための SCAP 1.2/1.1/1.0 および OVAL コンテンツをインポートするためのコンソール ウィザード。  

  - SCAP ソース データ ストリーム、および XCCDF ベンチマークと変換用プロファイルを選択できます。

- 構成評価の結果を SCAP 形式 XML レポートにエクスポートするためのコンソール ウィザード。  

  - 基準の生成に使用されるソース ファイル、SCAP データ ストリーム、XCCDF ベンチマーク、XCCDF プロファイルが表示されます。
  - Cyberscope Lightweight Asset Summary Results (LASR) レポートが生成されます。  

- 構成基準の展開に基づいて SCAP レポートを生成します。 このコンポーネントには、クライアント コンプライアンスと XCCDF ルール コンプライアンスを視覚化するための新しいダッシュボードが含まれます。 このダッシュボードでは、さらに詳しいレポートに移動し、そこで検索したり、フィルターを適用したりできます。  

- OVAL テストから変換したいくつかの種類の構成アイテムのパフォーマンスを改善し、評価を速く行えるようにします。  

- Windows 10 DISA v1r3 コンテンツで見つかったいくつかの問題を修正します。  



## <a name="terms"></a>用語

- **OVAL ID**:特定の OVAL を定義する識別子であり、OVAL ID の形式に準拠します。  

- **SCAP 結果データ ストリーム**:出力 (結果) コンテンツを保持する SCAP コンポーネントの集合に SCAP コンポーネント間の参照マッピングが追加されたもの。  

- **SCAP ソース データ ストリーム**:入力 (ソース) コンテンツを保持する SCAP コンポーネントの集合に SCAP コンポーネント間の参照マッピングが追加されたもの。



## <a name="deployment-process"></a>デプロイのプロセス

全体的な展開プロセスの概要を次に示します。  

- 拡張機能を使用するための[インフラストラクチャの準備](#bkmk_prepare)  

- Configuration Manager の [SCAP 拡張機能のインストールと構成](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_install)  

- NIST からの [SCAP データ ストリーム ファイルのダウンロードとインストール](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_scap-data-stream-files)  

- SCAP データ ストリーム ファイルを Configuration Manager のコンプライアンス設定基準に変換およびインポートします。 次のいずれかの操作を行います。   

    - Configuration Manager コンソールのインポート ウィザードを使用した[手動プロセス](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import)  

    - Microsoft.Sces.ScapToDcm.exe コマンドライン ツールを使用した[自動プロセス](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_auto-convert-and-import)  

- コレクションへの構成基準の[展開](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_deploy)  

- コンプライアンス データの[監視](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_monitor)  

- 次の 2 つの方法のいずれかを使用して、SCAP 形式にコンプライアンス結果をエクスポートします。  

    - コンソールのエクスポート ウィザードを使用した[手動プロセス](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_export)  

    - Microsoft.Sces.DcmToScap.exe コマンドライン ツールを使用した[自動プロセス](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_auto-export)  



## <a name="bkmk_prepare"></a> インフラストラクチャの準備

### <a name="software-requirements"></a>ソフトウェア要件

Configuration Manager の SCAP 拡張機能をインストール、構成、および実行するには、次のソフトウェアを使用しているコンピューターが必要です。

- Configuration Manager Current Branch コンソールの[サポートされているバージョン](/sccm/core/servers/manage/current-branch-versions-supported)。  

- Configuration Manager コンソールと互換性のある OS バージョン。 詳細については、[Configuration Manager コンソールのサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-consoles)に関する記事を参照してください。  

SCAP 拡張機能を実行しているコンピューターに加えて、次のアイテムも必要になります。

- Configuration Manager Current Branch インフラストラクチャ。 Configuration Manager の展開要件の詳細については、「[Configuration Manager のサポートされている構成](/sccm/core/plan-design/configs/supported-configurations)」という記事を参照してください。  

SCAP コンプライアンスを評価するコンピューターには、次のようなソフトウェアおよび構成が必要です。

- Configuration Manager クライアント。  

- Windows PowerShell 2.0 またはそれ以降。  

- **バイパス** に設定された Configuration Manager の PowerShell 実行ポリシー。 詳細については、「[PowerShell 実行ポリシー](/sccm/core/clients/deploy/about-client-settings#computer-agent)」という記事を参照してください。  

- 次のいずれかのオペレーティング システム  
  - Windows 7 SP1、32 ビットまたは 64 ビット
  - Windows 10、32 ビットまたは 64 ビット
  - Windows Server 2012 R2

### <a name="hardware-requirements"></a>ハードウェア要件

Configuration Manager の最小システム要件について詳しくは、[Configuration Manager のハードウェア構成の計画](/sccm/core/plan-design/configs/recommended-hardware)に関する記事をご覧ください。



## <a name="accessibility-features"></a>ユーザー補助機能

Configuration Manager の SCAP 拡張機能には、Windows コマンドライン ツールが含まれます。 これらのツールは、Windows のユーザー補助機能とツールを利用できます。

- Microsoft.Sces.ScapToDcm.exe と Microsoft.Sces.DcmToScap.exe のコマンドライン パラメーターが記載されています。 詳細については、[Microsoft.Sces.ScapToDcm.exe コマンドライン パラメーター](/sccm/compliance/plan-design/scap/install-configure-scap#microsoftscesscaptodcmexe-command-line-parameters)および [Microsoft.Sces.DcmToScap.exe コマンドライン パラメーター](/sccm/compliance/plan-design/scap/import-scap-compliance-settings#microsoftscesdcmtoscapexe-command-line-parameters)に関するページを参照してください。  

- 各ツールのコマンドライン パラメーター `-help` と `-?` は、画面に使用方法を出力します。 これらの使用方法の詳細は、スクリーン リーダーやその他の支援技術で利用できます。  

- 詳細については、[Windows のユーザー補助](http://windows.microsoft.com/windows/help/accessibility)に関するページを参照してください。

SCAP 拡張機能では、Configuration Manager ユーザー補助機能能も利用されます。 詳細については、[Configuration Manager のユーザー補助機能](/sccm/core/understand/accessibility-features)に関する記事を参照してください。

マイクロソフト のアクセシビリティおよびサービスについて詳しくは、[マイクロソフトのユーザー補助 Web サイト](http://go.microsoft.com/fwlink/p/?LinkId=9212)をご覧ください。



## <a name="next-step"></a>次のステップ
> [!div class="nextstepaction"]
> [SCAP 拡張機能のインストールと構成](/sccm/compliance/plan-design/scap/install-configure-scap)
