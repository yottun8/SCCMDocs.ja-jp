---
title: ユーザーの状態をキャプチャおよび復元する
titleSuffix: Configuration Manager
description: Configuration Manager のタスク シーケンスを使用して、OS の展開シナリオでユーザー状態のデータをキャプチャして復元します。
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9888bbcc0468356b55216491d8599ebb5f42818
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420432"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>Configuration Manager でユーザー状態をキャプチャおよび復元するためのタスク シーケンスを作成する

 「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

 Configuration Manager のタスク シーケンスを使用して、OS の展開シナリオでユーザー状態のデータをキャプチャして復元します。 これらのシナリオでは、現在の OS のユーザー状態を維持することが望まれます。 作成するタスク シーケンスの種類によっては、タスク シーケンスの一部として、キャプチャの作成と復元のステップが自動的に追加されることがあります。 他のシナリオでは、タスク シーケンスにキャプチャと復元のステップを手動で追加する必要があります。 この記事では、ユーザー状態データをキャプチャして復元するために、既存のタスク シーケンスに追加する必要があるステップを示します。  



## <a name="task-sequence-steps"></a>タスク シーケンスのステップ  

 ユーザー状態をキャプチャして復元するには、タスク シーケンスに次のステップを追加します。  

 - [状態ストアの要求](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore)状態移行ポイントにユーザー状態を格納する場合、このステップが必要です。  

- [ユーザー状態のキャプチャ](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState): このステップでは、ユーザー状態データがキャプチャされます。 その後、状態移行ポイントに、またはハードリンクを使用してローカル ディスクに、そのデータが格納されます。  

- [ユーザー状態の復元](/sccm/osd/understand/task-sequence-steps#BKMK_RestoreUserState): このステップでは、ユーザー データを展開先コンピューターに復元します。 状態移行ポイントから、またはハードリンクでローカル ディスクから、データを取得できます。  

- [状態ストアのリリース](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore): 状態移行ポイントにユーザー状態を格納する場合、このステップが必要です。 このステップでは、状態移行ポイントからデータが削除されます。  


 ユーザー状態のキャプチャと復元に必要なタスク シーケンスのステップを追加するには、次の手順のようにします。 タスク シーケンスの作成について詳しくは、「[タスクを自動化するためのタスク シーケンスの管理](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks)」をご覧ください。  



## <a name="capture-the-user-state"></a>ユーザー状態をキャプチャする  

 ユーザー状態をキャプチャするタスク シーケンスのステップを追加するには、次の手順を使用します。

1.  **[タスク シーケンス]** 一覧で、タスク シーケンスを選択し、**[編集]** をクリックします。  

2.  状態移行ポイントを使用してユーザー状態を保存するには、**[状態ストアの要求]** ステップをタスク シーケンスに追加します。 **タスク シーケンス エディター**で **[追加]** をクリックします。 **[ユーザー状態]** をポイントして、**[状態ストアの要求]** をクリックします。 このステップのオプションとプロパティを構成して、**[適用]** をクリックします。 使用できる設定について詳しくは、「[状態ストアの要求](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore)」をご覧ください。  

3.  **[ユーザー状態のキャプチャ]** ステップをタスク シーケンスに追加します。 **タスク シーケンス エディター**で **[追加]** をクリックします。 **[ユーザー状態]** をポイントして、**[ユーザー状態のキャプチャ]** をクリックします。 このステップのオプションとプロパティを構成して、**[適用]** をクリックします。 使用できる設定について詳しくは、「[ユーザー状態のキャプチャ](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState)」をご覧ください。  

    > [!IMPORTANT]  
    >  タスク シーケンスにこのステップを追加する場合、**OSDStateStorePath** タスク シーケンス変数も設定して、ユーザー状態データの保存場所を指定します。 ユーザー状態をローカルに保存する場合は、ルート フォルダーを指定しないでください。タスク シーケンスが失敗する可能性があります。 ユーザー データをローカルに保存する場合は、常にフォルダーまたはサブフォルダーを使用してください。 この変数について詳しくは、「[タスク シーケンス変数](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)」をご覧ください。  

4.  状態移行ポイントを使用する場合は、タスク シーケンスに **[状態ストアのリリース]** ステップを追加します。 **タスク シーケンス エディター**で **[追加]** をクリックします。 **[ユーザー状態]** をポイントして、**[状態ストアのリリース]** をクリックします。 このステップのオプションとプロパティを構成して、**[適用]** をクリックします。 使用できる設定について詳しくは、「[状態ストアのリリース](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore)」をご覧ください。  

    > [!IMPORTANT]  
    >  **状態ストアのリリース** ステップが開始する前に、**状態ストアのリリース**の開始前に実行するタスク シーケンス アクションが成功している必要があります。  


 このタスク シーケンスを展開し、展開先コンピューターでユーザー状態をキャプチャします。 タスク シーケンスの展開方法の詳細については、「[タスク シーケンスの展開](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)」を参照してください。  



## <a name="restore-the-user-state"></a>ユーザー状態を復元する  

 ユーザー状態を復元するタスク シーケンスのステップを追加するには、次の手順を使用します。

1. **[タスク シーケンス]** 一覧で、タスク シーケンスを選択し、**[編集]** をクリックします。  

2. **[ユーザー状態の復元]** ステップをタスク シーケンスに追加します。 **タスク シーケンス エディター**で **[追加]** をクリックします。 **[ユーザー状態]** をポイントして、**[ユーザー状態の復元]** をクリックします。 このステップでは、必要に応じて状態移行ポイントへの接続が確立されます。 このステップのオプションとプロパティを構成して、**[適用]** をクリックします。 使用できる設定について詳しくは、「[ユーザー状態の復元](/sccm/osd/understand/task-sequence-steps#BKMK_RestoreUserState)」をご覧ください。  

   > [!Important]  
   >  **[すべてのユーザー プロファイルを標準オプションでキャプチャする]** オプションを指定して[ユーザー状態のキャプチャ](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState) ステップを使用するときは、**ユーザー状態の復元**ステップで **[ローカル コンピューターのユーザー プロファイルを復元する]** 設定を選択する必要があります。 そうしないと、タスク シーケンスは失敗します。  

   > [!Note]  
   > ローカル ハードリンクを使用してユーザー状態を格納していて、復元が成功しない場合は、データを格納するために作成されたハードリンクを手動で削除することができます。 タスク シーケンスは、[コマンド ラインの実行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)ステップで USMTUtils ツールを実行してこのアクションを自動化できます。 USMTUtils を使用してハードリンクを削除する場合は、USMTUtils を実行した後に[コンピューターの再起動](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer)ステップを追加します。  

3. 状態移行ポイントを使用してユーザー状態を保存する場合は、タスク シーケンスに**状態ストアのリリース** ステップを追加します。 **タスク シーケンス エディター**で **[追加]** をクリックします。 **[ユーザー状態]** をポイントして、**[状態ストアのリリース]** をクリックします。 このステップのオプションとプロパティを構成して、**[適用]** をクリックします。 使用できる設定について詳しくは、「[状態ストアのリリース](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore)」をご覧ください。  

   > [!IMPORTANT]  
   >  **状態ストアのリリース** ステップが開始する前に、**状態ストアのリリース**の開始前に実行するタスク シーケンス アクションが成功している必要があります。  


 このタスク シーケンスを展開し、対象コンピューターでユーザー状態を復元します。 タスク シーケンスの詳細については、「[タスク シーケンスの展開](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)」を参照してください。  



## <a name="next-steps"></a>次のステップ

[タスク シーケンスの展開の監視](/sccm/osd/deploy-use/monitor-operating-system-deployments#BKMK_TSDeployStatus)
