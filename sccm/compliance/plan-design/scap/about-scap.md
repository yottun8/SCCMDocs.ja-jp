---
title: Security Content Automation Protocol (SCAP) 拡張機能について
titleSuffix: System Center Configuration Manager
description: Security Content Automation Protocol (SCAP) 拡張機能について説明します
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: fc986e2175583124377ccb7c080df4b219ea8df0
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>Security Content Automation Protocol (SCAP) 拡張機能について

*適用対象: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> この機能は、Technical Preview バージョン 1803 で[プレリリース機能](/sccm/core/servers/manage/pre-release-features)として初めて導入されました。 プレリリース版の SCAP 拡張機能は、現在サポートされているバージョンの Configuration Manager Current Branch と LTSB 1606 にインストールできます。 1803 Technical Preview 以降のインストール ファイルは cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi にあります。 

Microsoft System Center Configuration Manager の SCAP 拡張機能は、Security Content Automation Protocol (SCAP) に準拠するためにネットワーク環境の分析と評価を実行するのに役立ちます。 SCAP は、米国標準技術研究所 (NIST) によって定義および管理されています。

Microsoft System Center Configuration Manager の SCAP 拡張機能では、Microsoft System Center Configuration Manager のコンプライアンス設定を使用して、環境内のコンピューターをスキャンしてから、United States Government Configuration Baseline (USGCB) 命令の遵守レベルを文書化します。

拡張機能は、Configuration Manager が Security Content Automation Protocol (SCAP) データ ストリームを使用して、システムの対応状態を評価し、レポートの結果を SCAP 形式で生成します。 組織で既存の Configuration Manager のインフラストラクチャを利用し、確実に管理対象のコンピューターがこの連邦政府の対応要件を満たし、National Institute of Standards and Technology (NIST) と米国行政管理予算局 (OMB) に必要な USGCB レポートを生成できるようになりました。

このガイドでは、System Center Configuration Manager インフラストラクチャでの SCAP 拡張機能のインストール、構成、実行に役立つ情報を提供します。



# <a name="what39s-new-in-scap-extensions-prerelease-for-microsoft-system-center-configuration-manager"></a>Microsoft System Center Configuration Manager の SCAP 拡張機能の新機能

このセクションでは、最新版の新機能について説明します。

System Center Configuration Manager の SCAP 拡張機能プレリリース:

- System Center Configuration Manager Current Branch のコンプライアンス設定基準に SCAP コンテンツを完全に変換できる Configuration Manager コンソール拡張機能が含まれます。
- SCAP バージョン 1.2 をサポートし、SCAP バージョン 1.1 および 1.0 と下位互換性があります。


  - 拡張可能な構成のチェックリストの説明形式 (XCCDF) バージョン 1.2 をサポートしています。
  - Open Vulnerability and Assessment Language (OVAL) をバージョン 5.10 までサポートしています。
  - 資産レポート形式 (ARF) 1.1 のレポートの生成をサポートしています。
  - 共通プラットフォーム一覧 (CPE) 2.3 をサポートしています。
  - 共通脆弱性識別子 (CVE) をサポートしています。
  - 共通セキュリティ設定一覧 (CCE) バージョン 5 をサポートしています。
  - USGCB Internet Explorer 8、USGCB Windows 7、USGCB Windows 7 Firewall をサポートしています。

- 構成基準に変換するための SCAP 1.2/1.1/1.0 および OVAL コンテンツをインポートするための UI ウィザードが含まれます。


  - SCAP ソース データ ストリーム、および XCCDF ベンチマークと変換用のプロファイルを選択できます。

- 構成評価の結果を SCAP 形式 XML レポートにエクスポートするための UI ウィザードが含まれます。


  - 基準の生成に使用されるソース ファイル、SCAP データストリーム、XCCDF ベンチマーク、XCCDF プロファイルが表示されます。
  - Cyberscope Lightweight Asset Summary Results (LASR) レポートの生成をサポートしています。

- 構成基準の展開に基づいて SCAP レポートを生成できます。 クライアント コンプライアンスと XCCDF ルール コンプライアンスを視覚化するための新しいダッシュボードが含まれます。 このダッシュボードでは、さらに詳しいレポートに移動し、そこで検索したり、フィルターを適用したりできます。
- OVAL テストから変換した中で、いくつかの構成アイテムのパフォーマンスを改善し、評価を速くします。

- Windows 10 DISA v1r3 コンテンツで見つかったいくつかの問題を修正します。

# <a name="scap-extensions-for-microsoft-system-center-configuration-manager-deployment-process"></a>Microsoft System Center Configuration Manager 配置プロセスの SCAP 拡張機能

このガイドでは、Microsoft System Center Configuration Manager の SCAP 拡張機能を使用した SCAP コンプライアンスの分析、評価、およびレポートの方法について説明します。 実行する手順の概要を次に示します。

- 拡張機能を活用するために、前提条件となるインフラストラクチャを準備します。
- Microsoft System Center Configuration Manager の SCAP 拡張機能をインストールして構成します。
- [国家脆弱性データベース](http://nvd.nist.gov) (NVD) から SCAP データのストリーム ファイルをダウンロード、インストール、構成します。
- インポート ウィザードを使用して、**あるいは**コマンドライン Microsoft.Sces.ScapToDcm.exe ツールを利用したキャビネット (.cab) ファイルを介して、System Center Configuration Manager コンプライアンス設定基準に直接、SCAP データ ストリーム ファイルを変換し、インポートします。
- エクスポート ウィザードまたはコマンドライン Microsoft.Sces.DcmToScap.exe ツールを使用して SCAP 形式にコンプライアンス結果をエクスポートします。

# <a name="terms"></a>用語

**OVAL ID:** 特定の OVAL を定義する識別子であり、OVAL ID の形式に準拠します。

**SCAP 結果データ ストリーム:** 出力 (結果) コンテンツを保持する SCAP コンポーネントの集合に SCAP コンポーネント間の参照マッピングが追加されたもの。

**SCAP ソース データ ストリーム:** 入力 (ソース) コンテンツを保持する SCAP コンポーネントの集合に SCAP コンポーネント間の参照マッピングが追加されたもの。

# <a name="prepare-the-prerequisite-infrastructure"></a>前提条件となるインフラストラクチャの準備

Microsoft System Center Configuration Manager の SCAP 拡張機能を利用するために、次のソフトウェアとハードウェアの要件が満たされていることを確認します。

## <a name="software-requirements"></a>ソフトウェア要件

Microsoft System Center Configuration Manager の SCAP 拡張機能をインストール、構成、および実行するには、次のソフトウェアを使用しているコンピューターが必要です。

- System Center Configuration Manager Current Branch コンソールのサポートされている[バージョン](/sccm/core/servers/manage/current-branch-versions-supported)。
- System Center Configuration Manager コンソールと互換性のあるオペレーティング システム。 互換性のあるオペレーティング システムの一覧は、「[System Center Configuration Manager コンソールのサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-consoles)」という記事でご確認ください。

SCAP 拡張機能を実行しているコンピューターに加えて、次のアイテムも必要になります。

- System Center Configuration Manager Current Branch インフラストラクチャ。 Configuration Manager の展開要件の詳細については、「[Configuration Manager のサポートされている構成](/sccm/core/plan-design/configs/supported-configurations)」という記事を参照してください。

SCAP コンプライアンスを評価するコンピューターには、次のようなソフトウェアおよび構成が必要です。

- Configuration Manager クライアントで有効なコンプライアンスと設定の管理コンポーネント。
- Windows PowerShell 2.0 またはそれ以降。
- **バイパス** に設定された Configuration Manager の PowerShell 実行ポリシー。 詳細については、「[PowerShell 実行ポリシー](/sccm/core/clients/deploy/about-client-settings#computer-agent)」という記事を参照してください。
- 次のいずれかのオペレーティング システム
  - Windows 7 リリース バージョンまたは SP1、32 ビットまたは 64 ビット
  - Windows 10 の 32 ビットまたは 64 ビット
  - Windows Server 2012 R2

## <a name="hardware-requirements"></a>ハードウェア要件

最小システム要件はこちらにあります。

[Configuration Manager のハードウェア構成の計画](/sccm/core/plan-design/configs/recommended-hardware)



## <a name="accessibility-features"></a>ユーザー補助機能

System Center Configuration Manager の SCAP 拡張機能には、Windows のユーザー補助機能とツールを活用できる Windows コマンド ライン ツールが含まれます。

- Microsoft.Sces.ScapToDcm.exe と Microsoft.Sces.DcmToScap.exe については、このユーザー ガイドにコマンドライン パラメーターが記載されています。
- -help と -? により、ツールの使用法がスクリーンに出力され、スクリーン リーダーやその他の補助的な技術によって使用可能です。
- Windows [ユーザー補助](http://windows.microsoft.com/windows/help/accessibility)

SCAP 拡張機能では、System Center Configuration Manager の機能も利用されます。  System Center Configuration Manager には、障碍のあるユーザーに製品を利用してもらうための機能があります。

- [System Center Configuration Manager のユーザー補助機能](/sccm/core/understand/accessibility-features)

マイクロソフト アクセシビリティ製品およびサービスの一般的な情報については、[マイクロソフト アクセシビリティ Web サイト](http://go.microsoft.com/fwlink/p/?LinkId=9212)を参照してください。

## <a name="next-step"></a>次のステップ
> [!div class="nextstepaction"]
> [SCAP 拡張機能のインストールと構成](/sccm/compliance/plan-design/scap/install-configure-scap)
