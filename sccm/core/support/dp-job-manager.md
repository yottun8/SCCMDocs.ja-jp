---
title: DP Job Queue Manager
titleSuffix: Configuration Manager
description: DP Job Queue Manager を使用して、Configuration Manager 配布ポイントに対するコンテンツ配布ジョブのトラブルシューティングと管理を行います。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5218d47ae8699ee0feb0cf59405833ec4cc49569
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385833"
---
# <a name="dp-job-queue-manager"></a>DP Job Queue Manager

*適用対象: System Center Configuration Manager (Current Branch)*

Distribution Point (DP) Job Queue Manager は、[Configuration Manager ツール](/sccm/core/support/tools)の 1 つです。 このツールを使用して、Configuration Manager 配布ポイントに対する実行中のコンテンツ配布ジョブのトラブルシューティングと管理を行います。 

このツールには、パッケージ転送マネージャー コンポーネントのキュー内にあるジョブの一覧が表示されます。 また、ジョブの状態 (実行の準備完了、実行中、または再試行中) も表示されます。 このツールでは、キュー内のジョブを操作する、一覧内でジョブを上に移動する、ジョブを取り消す、または手動でジョブの実行を開始することができます。

また、配布ポイントがジョブを実行しているサイト サーバーからも情報を取得します。 このツールは、プロバイダーを介してサイト サーバーに接続します。 この情報を収集するために、すべてのリモート配布ポイントに接続するわけではありません。 アクションをトリガーし、プロバイダーを介して情報を取得するため、リモートの配布ポイントからの変更が反映されるまでに遅延があります。



## <a name="usage"></a>使用方法

**DPJobMgr.exe** を実行します。 このツールのメイン メニューには、次のタブがあります。 

- [接続](#bkmk_connect): プライマリ サイト サーバーへの最初の接続を確立します  

- [概要](#bkmk_overview): すべての配布ポイントで実行されているすべてのジョブが単一のビューにまとめて表示されます  

- [Distribution Point Info (配布ポイントの情報)](#bkmk_dp-info): 追跡する複数の配布ポイントを追跡し、関心のある単一のジョブを管理します  

- [ジョブの管理](#bkmk_manage-jobs): すべてのジョブとその状態の一覧が 1 つのフラット ビューで表示されます。 ジョブを操作する、上に移動する、取り消す、または手動で開始することができます。  


### <a name="bkmk_connect"></a> [接続] タブ

このタブを使用して、プライマリ サイト サーバーへの最初の接続を確立します。 現在サインインしているユーザーの資格情報を使用します。 中央管理サイトまたはセカンダリ サイトに接続することはできません。 接続には、**完全な権限を持つ管理者**セキュリティ ロールが必要です。

ツールが正常に接続を確立すると、ツールの下部に表示される通知で、サイト サーバーに接続されていることを確認できます。 


### <a name="bkmk_overview"></a> [概要] タブ

すべての配布ポイントのすべてのジョブの概要が表示されます。 次の列を参照してください。  

- **配布ポイント**: 配布ポイントの名前が一覧表示されます  

- **実行中のジョブ**: 特定の配布ポイントで実行されている同時ジョブの数が表示されます。  

    > [!Tip]  
    > 同時実行ソフトウェア配布の数はサイト設定です。 この設定は、[ソフトウェアの配布コンポーネントのプロパティ] で変更されます。  

- **合計ジョブ数**: 特定の配布ポイントを対象とするすべてのジョブの数が表示されます。 この数には、実行中、再試行中、または実行待ちのジョブが含まれます。  

- **Total Retries (合計試行回数)**: ジョブが特定の配布ポイントで再試行された回数が表示されます。 数値が大きいほど、その配布ポイントに関する一般的な問題が発生する可能性が高いことを示します。  


> [!Tip]  
> - このタブの各列を並べ替えるには、列名をクリックします  
> 
> - このタブの情報を手動で更新するには、**[更新]** をクリックします  
> 
> - このタブの情報を自動的に更新するには、**[Start Auto Refresh]\(自動更新の開始\)** をクリックして、自動更新間隔を設定します。 既定の更新間隔は 2 分間です。  


### <a name="bkmk_dp-info"></a> [配布ポイントの情報] タブ

接続されたサイト以下のすべての配布ポイントの一覧が表示されます。 左側のウィンドウにすべての配布ポイントが表示されます。 必要に応じて **[すべて選択]** または **[すべて選択解除]** をクリックするか、この一覧内の特定の配布ポイントを複数選択します。 右側のウィンドウには、選択した配布ポイントのジョブが表示されます。

次の 8 つの列があります。  

- **状態アイコン**: 次の 3 つの状態アイコンがあります。  

    - **準備完了**: 特定のジョブがすべての検証手順を完了したことを示します。 同時実行中のジョブに追加する準備が整っています。 通常、この状態のジョブは待機段階です。 現在の実行中のプロセスが完了し、その領域が空くまで待ちます。  

    - **実行中**: 特定のジョブが現在配布ポイントで実行されていることを示します。 長時間実行ジョブ (大きいパッケージ) の場合、通常は、完了までの進行状況 (%) を取得する時間があります。 この割合はこのビューの **[進行状況]** 列に表示されます。 小さいパッケージの場合、**[進行状況]** 列が空のままになることがあります。 リモートの配布ポイントから状態を受け取る前に、ジョブが既に完了している可能性があります。  

    - **再試行**: 特定のジョブが失敗し、現在再試行状態であることを示します。 このジョブは、再試行間隔後に再試行されます。 この間隔は構成可能であり、既定では 30 分に設定されています。  

- **ソフトウェア**: 特定の配布ポイントを対象とするパッケージの名前  

- **パッケージ ID**: 特定の配布ポイントを対象とするパッケージのパッケージ ID  

- **サイズ**: パッケージのサイズ (KB 単位)  

- **進行状況**: ジョブの完了率。 詳細については、**実行中**状態アイコンの説明を参照してください。  

- **Start/Restart Time (開始/再開時刻)**: 実行中のジョブの場合、この値は開始時刻 (緑色) です。 再試行ジョブの場合、この値はジョブを再試行する時刻です。  

- **再試行**: このパッケージを再試行した回数。  

- **配布ポイント名**: 配布ポイントの完全修飾ドメイン名 (FQDN)  

> [!Tip]  
> - このタブの各列を並べ替えるには、列名をクリックします  
> 
> - このタブの情報を手動で更新するには、**[更新]** をクリックします  
> 
> - このタブの情報を自動的に更新するには、**[Start Auto Refresh]\(自動更新の開始\)** をクリックして、自動更新間隔を設定します。 既定の更新間隔は 2 分間です。  
> 
> - 特定のジョブを変更する必要がある場合は、このビューでジョブを右クリックし、**[ジョブの管理]** を選択します。 この操作で [[ジョブの管理] タブ](#bkmk_manage-jobs)が開きます。  


### <a name="bkmk_manage-jobs"></a> [ジョブの管理] タブ

すべてのジョブとその状態の一覧が 1 つのフラット ビューで表示されます。 [[Distribution Point Info]\(配布ポイントの情報\) タブ](#bkmk_dp-info)と同じ 8 つの列があります。このビューでは、ジョブを右クリックすると次のアクションが表示されます。  

- **実行**: 実行中ではない任意の状態のジョブを開始します  

- **先頭へ移動**: 1 つまたは複数のジョブをキューの一番上に移動します。 このアクションで、すぐにジョブが実行されることがあります。 優先度の低いジョブは、このアクションのために一時停止されることがあります。  

- **上へ移動**: 特定のジョブを 1 行上に移動します。 優先度の低いジョブは、このアクションのために実行が一時停止されることがあります。  

- **下へ移動**: 特定のジョブを 1 行下に移動します。  

- **一番下へ移動**: 1 つまたは複数のジョブをキューの一番下に移動します。  

    > [!Tip]  
    > 一覧のジョブをドラッグ アンド ドロップして移動することもできます。  

- **キャンセル**: 1 つまたは複数のジョブの取り消しを試行します。  

    > [!Note]  
    > 最終的な完了時刻に近づいたジョブを取り消すことはできません。 サイト サーバーが配布ポイントでもある場合は、サイト サーバー上のジョブを取り消すことはできません。  



## <a name="see-also"></a>関連項目

- [コンテンツ管理の基本的な概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [パッケージ転送マネージャー](/sccm/core/plan-design/hierarchy/package-transfer-manager)
