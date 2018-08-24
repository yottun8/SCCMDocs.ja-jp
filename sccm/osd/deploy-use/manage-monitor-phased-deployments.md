---
title: 段階的な展開の管理と監視
titleSuffix: Configuration Manager
description: Configuration Manager でソフトウェアの段階的な展開を管理および監視する方法について説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1889ba3ea19d27676089f2a9a24cef812c9f526c
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385863"
---
# <a name="manage-and-monitor-phased-deployments"></a>段階的な展開の管理と監視

この記事では、段階的な展開を管理および監視する方法について説明します。 管理タスクには、手動で次のフェーズを開始することと、フェーズを中断または再開することが含まれます。 

まず、[段階的な展開を作成](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)する必要があります。 



## <a name="bkmk_move"></a> 次のフェーズに移行する

設定 **[Manually begin the second phase of deployment]\(展開の第 2 フェーズを手動で開始する\)** を選択すると、成功の条件に基づいて自動的に次のフェーズが開始されません。 段階的な展開を次のフェーズに移行する必要があります。  

1. このアクションを開始する方法は、展開されているソフトウェアの種類に応じて変わります。  

    - **アプリケーション** (バージョン 1806 以降のみ): **[ソフトウェア ライブラリ]** に移動し、**[アプリケーション管理]** を展開して **[アプリケーション]** を選択します。   

    - **タスク シーケンス**: **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開して、**[タスク シーケンス]** を選択します。   

2. 段階的な展開を使用するソフトウェアを選択します。  

3. 詳細ウィンドウで、**[段階的な展開]** タブに切り替えます。  

4. 段階的な展開を選択し、リボンの **[次のフェーズに移動]** をクリックします。  

    ![段階的な展開に関するアクションが表示された右クリック メニュー](media/Suspend-phased-deployment.PNG)



## <a name="bkmk_suspend"></a> フェーズの中断と再開 

段階的な展開は、手動で中断または再開する必要があります。 たとえば、タスク シーケンスの段階的な展開を作成するとします。 パイロット グループのフェーズを監視している間、多数の障害が発生していることに気づきます。 そこで段階的な展開を中断し、以降、デバイスのタスク シーケンスの実行を停止します。 問題を解決したら、段階的な展開を再開してロールアウトを続行します。 

1. このアクションを開始する方法は、展開されているソフトウェアの種類に応じて変わります。  

    - **アプリケーション** (バージョン 1806 以降のみ): **[ソフトウェア ライブラリ]** に移動し、**[アプリケーション管理]** を展開して **[アプリケーション]** を選択します。   

    - **タスク シーケンス**: **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開して、**[タスク シーケンス]** を選択します。 既存のタスク シーケンスを選択して、リボンの **[段階的な展開の作成]** をクリックします。  

2. 段階的な展開を使用するソフトウェアを選択します。  

3. 詳細ウィンドウで、**[段階的な展開]** タブに切り替えます。  

4. 段階的な展開を選択し、リボンの **[中断]** または **[再開]** をクリックします。  

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="bkmk_monitor"></a> 監視
<!--1358577-->

バージョン 1806 以降、ネイティブの監視機能が段階的な展開に追加されました。 **[監視]** ワークスペースの **[展開]** ノードから段階的な展開を選択し、リボンで **[段階的な展開の状態]** をクリックします。

![2 つのフェーズの状態を示す段階的な展開の状態ダッシュボード](media/1358577-phased-deployment-status.png)

このダッシュボードには、展開の各フェーズに対して次の情報が表示されます。  

- **[デバイスの総数]**: このフェーズの対象となるデバイスの数です。  

- **[状態]**:このフェーズの現在の状態です。 各フェーズは次の状態のいずれかになります。  

    - **[展開の作成完了]**: 段階的な展開によって、このフェーズのコレクションにソフトウェアの展開が作成されました。 このソフトウェアではアクティブにクライアントを対象とします。  

    - **[待機中]**: 前のフェーズは、展開をこのフェーズに移行するための成功基準にまだ達していません。  

    - **[中断]**: 管理者が展開を中断しました。  

- **[進行状況]**: クライアントからの色分けされた展開の状態。 例: 成功、実行中、エラー、要件が満たされていません、不明。 

#### <a name="success-criteria-tile"></a>[成功の条件] タイル

**[Select Phase]\(フェーズの選択\)** ドロップダウン リストを使用して、**[成功の条件]** タイルの表示を変更します。 このタイルには、**[Phase Goal]\(フェーズ目標\)** と展開の現在のコンプライアンスとの比較が表示されます。 既定の設定では、フェーズ目標は 95% です。 この値は、展開が次のフェーズに移行するには 95% のコンプライアンスが必要であることを意味します。 

この例では、フェーズ目標は 65% であり、現在のコンプライアンスは 66.7% です。 第 1 段階が成功の条件を満たしていたため、段階的な展開は自動的に第 2 段階に移行しました。
![段階的な展開状況の [成功の条件] タイルの例](media/pod-status-success-criteria-tile.png)

フェーズ目標は、*次の*フェーズの [フェーズの設定] の **[展開の成功率]** と同じです。 段階的な展開が次の段階を開始するために、この第 2 段階で第 1 段階の成功の条件を定義します。 この設定を表示するには: 

1. ソフトウェアの段階的な展開オブジェクトに移動し、[段階的な展開のプロパティ] を開きます。  

2. **[フェーズ]** タブに切り替えます。**[フェーズ 2]** を選択し、**[表示]** をクリックします。  

3. フェーズの [プロパティ] ウィンドウで、**[フェーズの設定]** タブに切り替えます。  

4. *[前のフェーズが成功したかどうかの基準]* グループの **[展開の成功率]** の値を確認します。  

たとえば、以下のプロパティは、前述した条件が 65% の [成功の条件] タイルと同じフェーズのプロパティです。  
![フェーズのプロパティの [プロパティの設定] タブ](media/phase-properties-phase-settings.png)

