---
title: オペレーティング システム以外の展開用タスク シーケンスの作成
titleSuffix: Configuration Manager
description: ソフトウェアの配布、ドライバーの更新、ユーザー状態の編集などのオペレーティング システムの展開に関連していないタスク シーケンスを作成します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42c56b048afe768cd04cd5c91d659535ad5ffc9e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347486"
---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>System Center Configuration Manager でオペレーティング システム以外の展開用タスク シーケンスを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のタスク シーケンスは、お客様の環境でさまざまなタスクを自動化するために使用します。 これらのタスクは、主にオペレーティング システムの展開のために設計され、テストされます。  Configuration Manager には、[アプリケーションのインストール](../../apps/understand/introduction-to-application-management.md)、[ソフトウェアの更新プログラムのインストール](../../sum/understand/software-updates-introduction.md)、[構成の設定](../../compliance/understand/ensure-device-compliance.md)、またはカスタム オートメーションなどのシナリオに使用する主要なテクノロジとなる、他の数多くの機能があります。 Microsoft System Center の他の自動化テクノロジとして、 [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) と [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) などもご検討ください。  

タスク シーケンスの機能には柔軟性があり、タスク シーケンスを使用して、クライアント設定の構成、ソフトウェアの配布、ドライバーの更新、ユーザー状態の編集など、オペレーティング システムの展開とは独立した他のタスクを実行できます。 カスタム タスク シーケンスを作成して、タスクをいくつでも追加できます。 Configuration Manager では、オペレーティング システム以外の展開用のカスタム タスク シーケンスの使用がサポートされています。 ただし、タスク シーケンスで好ましくない結果や矛盾する結果が生じる場合は、操作を簡略化する方法を考えてください。 より簡単なステップを使用するか、操作を複数のタスク シーケンスに分けるか、あるいは段階的にタスク シーケンスを作成してテストすることで、これを行うことができます。

 オペレーティング システム以外の展開用のカスタム タスク シーケンスの使用では、以下のステップがサポートされています。  

-   [準備の確認](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [ネットワーク フォルダーへの接続](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [パッケージ コンテンツのダウンロード](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [アプリケーションのインストール](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [パッケージのインストール](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [ソフトウェア更新プログラムのインストール](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [コンピューターの再起動](../understand/task-sequence-steps.md#BKMK_RestartComputer)   

-   [コマンド ラインの実行](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [PowerShell スクリプトの実行](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [動的変数の設定](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [タスク シーケンス変数の設定](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>次のステップ 
[タスク シーケンスの展開](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
