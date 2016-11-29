---
title: "オペレーティング システム以外の展開用タスク シーケンスを作成する | Configuration Manager"
description: "ソフトウェアの配布、ドライバーの更新、ユーザー状態の編集などのオペレーティング システムの展開に関連していないタスク シーケンスを作成します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
caps.latest.revision: 6
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bc8ef5912f753031191a677d58d5e88f62b8d36a


---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>System Center Configuration Manager でオペレーティング システム以外の展開用タスク シーケンスを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のタスク シーケンスは、お客様の環境でさまざまなタスクを自動化するために使用します。 これらのタスクは、主にオペレーティング システムの展開のために設計され、テストされます。  Configuration Manager には、[アプリケーションのインストール](../../apps/understand/introduction-to-application-management.md)、[ソフトウェアの更新プログラムのインストール](../../sum/understand/software-updates-introduction.md)、[構成の設定](../../compliance/understand/ensure-device-compliance.md)、またはカスタム オートメーションなどのシナリオに使用する主要なテクノロジとなる、他の数多くの機能があります。 Microsoft System Center の他の自動化テクノロジとして、 [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) と [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) などもご検討ください。  

 タスク シーケンスの機能には柔軟性があり、タスク シーケンスを使用して、クライアント設定の構成、ソフトウェアの配布、ドライバーの更新、ユーザー状態の編集など、オペレーティング システムの展開とは独立した他のタスクを実行できます。 カスタム タスク シーケンスを作成して、タスクをいくつでも追加できます。 オペレーティング システム以外の展開用にカスタム タスク シーケンスの基本的な使用がサポートされているものの、可能な構成すべてをテストする方法はなく、より複雑なタスク シーケンスを開発すると問題が発生する機会は増加します。  

 オペレーティング システム以外の展開用のカスタム タスク シーケンスでは、以下のステップを使用できます。  

-   [準備の確認](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [ネットワーク フォルダーへの接続](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [パッケージ コンテンツのダウンロード](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [アプリケーションのインストール](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [パッケージのインストール](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [ソフトウェア更新プログラムのインストール](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [コンピューターの再起動](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)  

-   [コマンド ラインの実行](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [PowerShell スクリプトの実行](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [動的変数の設定](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [タスク シーケンス変数の設定](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>次のステップ
[タスク シーケンスの展開](manage-task-sequences-to-automate-tasks.md#a-namebkmkdeploytsa-deploy-a-task-sequence)



<!--HONumber=Nov16_HO1-->


