---
title: 共同管理ダッシュボード
titleSuffix: Configuration Manager
description: ダッシュボードを使用して、共同管理に関する情報を確認します。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 72b42aec2b50e229b90e9a642343386e8588aab7
ms.sourcegitcommit: 2cc635835709fb8d86cdb63ea34233b36c94d4d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2018
ms.locfileid: "52259006"
---
# <a name="co-management-dashboard-in-system-center-configuration-manager"></a>System Center Configuration Manager の共同管理ダッシュボード
*適用対象: System Center Configuration Manager (Current Branch)*

バージョン 1802 以降では、共同管理に関する情報を示すダッシュボードを表示できます。 ダッシュボードを利用すれば、お使いの環境で共同管理しているコンピューターを確認できます。 各種グラフを見ることで、対処が必要なデバイスを特定できます。<!--1356648-->

## <a name="open-the-co-management-dashboard"></a>共同管理ダッシュボードを開く
共同管理ダッシュボードを開くには、次の手順を使用します。 

1. Configuration Manager コンソールを開きます。 
2. **[監視]** ノードをクリックします。 
3. ダッシュボードを読み込むには、**[共同管理]** をクリックします。

## <a name="reviewing-information-in-the-co-management-dashboard"></a>共同管理ダッシュボードでの情報の確認

共同管理ダッシュボードには、ご利用の環境に関する 4 つのグラフが表示されます。 

- **共同管理デバイス** - 環境全体の共同管理デバイスの割合が示されます。

    ![管理対象デバイスのグラフ](media\co-management-dashboard\Percent-Co-managed-graph.PNG)

- **クライアント OS ディストリビューション** - OS ごとのクライアント デバイスの数がバージョン別に表示されます。 以下のグループが使用されます。 </br>
    - Windows 7 と 8.x
    - 1709 より前の Windows 10
    - Windows 10 1709 以降

         > [!NOTE] 
         > Windows 10 バージョン 1709 以降が共同管理の前提条件となります。

     グラフ セクションにカーソルを合わせると、選択された OS グループのデバイスの割合が表示されます。

     ![クライアント OS ディストリビューションのグラフ](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)

- **共同管理状態** - 次のカテゴリのデバイスの成功または失敗の詳細。
    - 成功、ハイブリッド Azure AD 参加済み
    - 成功、Azure AD 参加済み
    - 失敗: 自動登録に失敗
    
     グラフ セクションにカーソルを合わせると、カテゴリのデバイスの割合が表示されます。 

     ![共同管理の状態グラフ](media\co-management-dashboard\Co-management-status-graph.PNG)

     グラフ セクションをクリックすると、カテゴリのデバイス リストが表示されます。
 
     ![登録エラー デバイス リスト](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


- **ワークロードの切り替え** - 次の 4 つの使用可能なワークロードに関する、Microsoft Intune に切り替えたデバイスの数を示す棒グラフが表示されます。
    - コンプライアンス ポリシー
    - リソース アクセス
    - Windows Update for Business
    - Endpoint Protection

     グラフ セクションにカーソルを合わせると、ワークロードに関する切り替えたデバイスの数が表示されます。 
     ![ワークロードの切り替えを示す棒グラフ](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>次のステップ

共同管理の詳細については、以下を参照してください。
 - [Windows 10 デバイスの共同管理](/sccm/core/clients/manage/co-management-overview)
 - [共同管理用に Windows 10 デバイスを準備する](/sccm/core/clients/manage/co-management-prepare)

    
