---
title: MDT リリース ノート
description: Microsoft Deployment Toolkit のサポートされているプラットフォーム、前提条件、および制限事項について説明します。
ms.date: 06/04/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 6e32ce6d-585d-4801-a345-ff0f6f2d90ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7cb287a17322af8069708268a18d638bd04dddcf
ms.sourcegitcommit: 10b3a571e2a822bbd7b58a25840ee1e6f703a7a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814282"
---
# <a name="microsoft-deployment-toolkit-release-notes"></a>Microsoft Deployment Toolkit リリース ノート  

この記事では、Microsoft Deployment Toolkit (MDT) の最新リリースの詳細について説明します。 これらの詳細には、サポートされているプラットフォーム、前提条件、制限事項が含まれます。 この記事では、MDT バージョンの概念、特徴、および機能を理解していることを前提としています。



## <a name="latest-release"></a>最新のリリース

**MDT ビルド 8450**は、[Microsoft ダウンロード センター](https://aka.ms/mdtdownload)で入手できる最新のバージョンです。 

この更新プログラムでは、Windows 10 バージョン 1709 用の Windows アセスメント & デプロイメント キット (ADK) のサポートが開始されます。 

***更新プログラム***: 2018 年 5 月の時点で、このビルドは Windows 10 バージョン 1803 もサポートしています。

詳細については、「[サポートされているプラットフォーム](#supported-platforms)」セクションを参照してください。


### <a name="significant-changes"></a>重要な変更
この MDT のビルドで加えられた重要な変更を次に概説します。

#### <a name="supported-configuration-updates"></a>サポートされる構成の更新
- Windows 10 バージョン 1709 用 Windows ADK
- Windows 10 バージョン 1709
- Configuration Manager バージョン 1710

#### <a name="quality-updates"></a>品質に関する更新
このリリースでのバグ修正のタイトルを次に示します。
- Win10 でサイドロードされたアプリの依存関係とライセンスがインストールされません
- CaptureOnly タスク シーケンスでイメージのキャプチャが許可されません
- MDT タスク シーケンスを開始すると、"指定された DeploymentType 値 "" は無効です" というエラーが返されます。 展開は続行されません。
- ZTIMoveStateStore は誤った場所で状態ストア フォルダーを探すため、それを移動することができません
- xml には、望ましくない動作を引き起こす単純な入力ミスが含まれています
- Windows Server 2016 IIS 管理コンソール機能で、"ロールと機能のインストール" が動作しません
- フォルダーを使用する際に、アップグレード タスク シーケンスで OS イメージの参照が動作しません
- MDT ツールによって、TPM が誤って機能制限状態にプロビジョニングされます。 詳細については、サポート技術情報 [KB 4018657](https://support.microsoft.com/help/4018657/tpm-is-in-reduced-functionality-mode-after-successful-deployment-of-wi) を参照してください。
- ZTIGather シャーシ タイプの検出ロジックに対する更新プログラム
- OS のアップグレード手順が実行されると SetupComplete.cmd が残り、今後の展開に影響を与えます
- 一部のハードウェア上で発生する Windows 10 ADK 1607 以降の UEFI ブートの問題
- 更新された Configuration Manager タスク シーケンス バイナリが含まれます



## <a name="supported-platforms"></a>[サポートされているプラットフォーム]

MDT のリリースは、年または更新プログラムのバージョンでタグ付けされなくなります。 Windows 10 および Configuration Manager の現在のブランチにより的確に合わせ、ブランド化およびリリースのプロセスを簡略化するために、**Microsoft Deployment Toolkit** はシンプルになりました。 ビルド番号を使用して各リリースを区別します。 たとえば、ダウンロード可能な最新のビルドは 8450 です。

リリース スケジュールがあらかじめ決められている Configuration Manager とは異なり、MDT は、Windows 10、Windows ADK、または Configuration Manager の現在のブランチの新しいバージョンをサポートするために必要に応じてリリースされるだけです。 これらのコンポーネントに関する既知の問題については、必要に応じて、この記事に記載します。

MDT での展開がサポートされる OS バージョンは次のとおりです。
- Windows 10 バージョン 1803
- Windows 10 バージョン 1709
- [サポートされている Windows 10 の他のバージョン](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)
- Windows 8.1
- Windows 7
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2



## <a name="prerequisites"></a>[前提条件]

MDT では次のコンポーネントが必要です。これらは Windows に含まれています。
- Microsoft .NET Framework 4.0
- Windows PowerShell バージョン 3.0

最新の [Windows ADK for Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install) を使用してください。 

> [!Note]  
> Windows では、展開している Windows のバージョンに合う Windows ADK を使用することをお勧めします。 たとえば、Windows 10 バージョン 1703 を展開している場合は、Windows 10 バージョン 1703 用 Windows ADK を使用します。 Windows ADK コンポーネントのサポートについては、「[DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)」(DISM でサポートされているプラットフォーム) および「[USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1)」(USMT の要件) を参照してください。

ZTI および UDI のシナリオに合わせて MDT を Configuration Manager と統合する場合は、Configuration Manager の現在のブランチの最新バージョンを使用します。



## <a name="upgrading-mdt"></a>MDT のアップグレード

MDT のインストール プロセスを実行すると、同じコンピューターにインストールされている MDT の既存のインスタンスが削除されます。 このプロセス中に、既存の展開共有、配布ポイント、およびデータベースは保持されます。 インストールが完了したら、それらをアップグレードする必要があります。

MDT の現在のリリースでは、MDT の次のバージョンからのアップグレードをサポートしています。
- MDT ビルド 8443

> [!Tip]  
> アップグレードを試みる前に、既存の MDT インフラストラクチャのバックアップを作成します。

### <a name="lti"></a>LTI
MDT をインストールしたら、Deployment Workbench の [展開共有] ノードから **[Open Deployment Share Wizard]\(展開共有を開くウィザード\)** を実行して既存の展開共有をアップグレードします。 既存の展開共有ディレクトリへのパスを指定し、**[アップグレード]** チェック ボックスをオンにします。 このプロセスでは既存のネットワーク展開共有とメディア展開共有もアップグレードされます。そのため、それらの共有はアクセス可能である必要があります。 使用中のファイルはアップグレードの問題を引き起こす可能性があるため、展開の実行中には、このアップグレードを実行しないでください。

### <a name="zti"></a>ZTI
MDT のインストール プロセス中には、Configuration Manager 内に既に存在する MDT タスク シーケンスは変更されません。 それらは引き続き問題なく動作するはずです。 これらのタスク シーケンスをアップグレードするメカニズムは用意されていません。 MDT の新機能のいずれかを使用する場合は、Configuration Manager で新しい MDT 統合タスク シーケンスを作成します。

アップグレード プロセスが終了したら、次のことを行います。  

- アップグレード後に **[Configure ConfigMgr Integration Wizard]\(ConfigMgr 統合の構成ウィザード\)** を実行します。 新しいコンポーネントが登録され、更新された ZTI タスク シーケンス テンプレートがインストールされます。  

- 新規に作成した ZTI タスク シーケンス用に新しい **Microsoft Deployment Toolkit ファイル** パッケージを作成します。 アップグレードの前に作成された ZTI タスク シーケンスには既存の Microsoft Deployment Toolkit ファイル パッケージを使用できますが、新しい ZTI タスク シーケンスに対しては新しい Microsoft Deployment Toolkit ファイル パッケージを作成する必要があります。



<!--
## Known issues
-->



## <a name="frequently-asked-questions"></a>よく寄せられる質問

#### <a name="whats-the-mdt-support-life-cycle"></a>MDT のサポート ライフ サイクルとは何ですか?  
詳細については、「[Microsoft Deployment Toolkit support life cycle](https://support.microsoft.com/help/2872000/microsoft-deployment-toolkit-support-life-cycle)」 (Microsoft Deployment Toolkit のサポート ライフ サイクル) を参照してください。

#### <a name="is-this-release-only-supported-with-windows-10-windows-adk-or-configuration-manager-version-x"></a>このリリースは Windows 10、Windows ADK、または Configuration Manager バージョン *X* でのみサポートされますか?
Microsoft では、主に上に一覧した構成でこの MDT のビルドをテストしました。 既知の問題があることが明示されていない限り、上記の構成以外でも高い可能性で機能します。 Microsoft では他の組み合わせを明示的にテストしていないため、得られる利点は異なる場合があります。

#### <a name="how-do-i-get-help-with-mdt"></a>MDT のヘルプを取得するにはどうすればよいですか?
次のいずれかの方法を使用して、MDT のヘルプを取得します (優先度順)。

1. [MDT フォーラム](https://social.technet.microsoft.com/Forums/en/home?forum=mdt)に投稿します。 コミュニティ内の MVP や他のユーザーが投稿を見て、応答してくれます。 おそらく、ヘルプを得るには最も効率的な方法です。
2. Microsoft サポートに問い合わせます。 サポート ケースが開かれ、何らかの専門的なヘルプが得られます。
3. 問題が常に再現され、製品のバグであると考えられる場合は、Windows 10 の[フィードバック ハブ](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)に問題を送信します。 報告されたすべての内容が製品チームによって調査されます。 フィードバックを送信する場合は、**[エンタープライズ管理]** カテゴリと **[OS の展開]** サブカテゴリを使用します。 このカテゴリ化は、フィードバックを分類し、MDT チームに転送するのに役立ちます。
     - またフィードバック ハブを使用して、製品に関する提案 (デザインの変更要求や DCR) も送信できます。
     - 以前に Connect を介してフィードバックを送信してある場合は、フィードバック ハブで再度送信する必要はありません。