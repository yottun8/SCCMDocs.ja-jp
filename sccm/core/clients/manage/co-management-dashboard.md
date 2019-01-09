---
title: 共同管理ダッシュボード
titleSuffix: Configuration Manager
description: 共同管理ダッシュボードを使用して、共同管理デバイスに関する情報を確認します。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5e20985ac8fc39f2384cee5d202e19fc69e2b348
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414686"
---
# <a name="co-management-dashboard-in-configuration-manager"></a>Configuration Manager の共同管理ダッシュボード

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

バージョン 1802 から、共同管理に関する情報を示すダッシュボードが表示されるようになりました。 ダッシュボードを利用すれば、お使いの環境で共同管理しているコンピューターを確認できます。 各種グラフを見ることで、対処が必要なデバイスを特定できます。<!--1356648-->

Configuration Manager コンソールで **[監視]** ワークスペースに移動し、**[共同管理]** ノードを選択します。

バージョン 1810 から、共同管理ダッシュボードが機能強化され、さらに詳細な情報が表示されるようになりました。 <!--1358980-->



## <a name="dashboard-tiles"></a>ダッシュボード タイル 

共同管理ダッシュボードには、サイトのバージョンに応じて、さまざまなタイルが表示されます。 


### <a name="co-managed-devices"></a>共同管理デバイス

*適用対象: バージョン 1802 および 1806*

環境全体の共同管理デバイスの割合が示されます。
 ![共同管理デバイス タイル](media/co-management-dashboard/Percent-Co-managed-graph.PNG)


### <a name="client-os-distribution"></a>クライアント OS ディストリビューション

*すべてのバージョンに適用* 

OS ごとのクライアント デバイスの数がバージョン別に表示されます。 ここでは以下のグループが使用されます。  
- Windows 7 と 8.x  
- 1709 より前の Windows 10  
- Windows 10 1709 以降  

    > [!Tip]  
    > Windows 10 バージョン 1709 以降が共同管理の前提条件となります。  

グラフ セクションにカーソルを合わせると、OS グループ内のデバイスの割合が表示されます。
 ![クライアント OS ディストリビューション タイル](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)


### <a name="co-management-status-donut"></a>共同管理の状態 (ドーナツ)

*適用対象: バージョン 1802 および 1806*

次のカテゴリのデバイスの成功または失敗の内訳が表示されます。
- 成功、ハイブリッド Azure AD 参加済み  
- 成功、Azure AD 参加済み  
- 失敗しました:自動登録に失敗しました  

グラフ セクションにカーソルを合わせると、そのカテゴリ内のデバイスの割合が表示されます。 
 ![共同管理の状態 (ドーナツ) タイル](media/co-management-dashboard/Co-management-status-graph.PNG)

グラフ セクションを選択すると、そのカテゴリのデバイスの一覧が表示されます。
 ![登録エラー デバイス リスト](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)


### <a name="co-management-status-funnel"></a>共同管理の状態 (じょうご)

*適用対象: バージョン 1810 以降*

登録プロセスから、次の状態にあるデバイスの数を示すじょうごグラフ。  
- 対象デバイス  
- スケジュール済み  
- 登録開始済み  
- 登録済み  

![共同管理の状態 (じょうご) タイル](media/co-management-dashboard/1358980-status-funnel.png)


### <a name="co-management-enrollment-status"></a>共同管理の登録状態

*適用対象: バージョン 1810 以降*

次のカテゴリのデバイスの状態の内訳が表示されます。
- 成功、ハイブリッド Azure AD 参加済み  
- 成功、Azure AD 参加済み  
- 登録中、ハイブリッド Azure AD 参加済み  
- エラー、ハイブリッド Azure AD 参加済み  
- エラー、Azure AD 参加済み  
- ユーザー サインインの保留中  

タイルで状態を選択すると、その状態のデバイスが一覧表示されます。  

![共同管理の登録状態タイル](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="enrollment-errors"></a>登録エラー

*適用対象: バージョン 1810 以降*

デバイスからの登録エラーの数を示す表。  


### <a name="workload-transition"></a>ワークロードの切り替え

*すべてのバージョンに適用*

使用可能なワークロードのために、Microsoft Intune に切り替えたデバイスの数を示す棒グラフが表示されます  (ワークロードのリストは、Configuration Manager のバージョンによって異なります。 詳細については、「[Intune に切り替えられるワークロード](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune)」を参照してください)。

グラフ セクションにカーソルを合わせると、ワークロードのために切り替えたデバイスの数が表示されます。 
 ![ワークロードの切り替えを示す棒グラフ](media/co-management-dashboard/Workload-Transition.PNG)


## <a name="next-steps"></a>次のステップ

共同管理の詳細については、以下を参照してください。
 - [Windows 10 デバイスの共同管理](/sccm/core/clients/manage/co-management-overview)
 - [共同管理用に Windows 10 デバイスを準備する](/sccm/core/clients/manage/co-management-prepare)

    
