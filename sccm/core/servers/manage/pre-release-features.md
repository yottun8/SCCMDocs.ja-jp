---
title: プレリリース機能
titleSuffix: Configuration Manager
description: System Center Configuration Manager のプレリリース機能
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c30fbeaad87b18750f65f90427366044d30c6609
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2018
---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>System Center Configuration Manager のプレリリース機能
*適用対象: System Center Configuration Manager (Current Branch)*

プレリリース機能は、運用環境での初期テスト用の Current Branch に含まれている機能です。 これらの機能は完全にサポートされていますが、現在開発中のため、プレリリースのカテゴリから移動するまでは変更が行われる可能性があります。

 プレリリース機能を使用できるようになる前に、Configuration Manager コンソールのプレリリース機能を使用することに同意してはじめて、その機能を選択して使用を有効にすることができます。  

同意する操作は階層ごとに 1 回限りの操作であり、元に戻すことはできません 同意するまでは、更新プログラムに含まれている新しいプレリリース機能を有効にすることはできません。 プレリリース機能を有効にした後で無効にすることはできません。

同意するには、コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** に移動してから、**[階層設定]** を選択します。 **[全般]** タブで、**[プレリリース機能を使用することに同意する]** を選択します。

プレリリース機能を含む更新プログラムをインストールすると、これらの機能は、更新プログラムに含まれる標準の機能と一緒に、[更新とサービス] ウィザードに表示されます。
  - **既に同意した場合:** 更新プログラムのインストール時に、[更新とサービス] ウィザード内でプレリリース機能を有効にすることができます。 これを行うには、その他の機能の場合と同様に、プレリリース機能を選択します。     

    必要に応じて、後でコンソールの **[管理]** > **[更新とサービス]** > **[機能]** ノードからプレリリース機能を有効にすることもできます。 **[機能]** ノードで、機能を選択し、**[有効にする]** を選択します。 このオプションは同意するまで灰色表示のままです  (1702 より前のバージョンでは、[更新とサービス] は、**[管理]** > **[クラウド サービス]** にありました)。
  -   **まだ同意していない場合:** 更新プログラムのインストール時に、プレリリース機能は [更新とサービス] ウィザードに表示されますが、灰色表示になっていて、有効にすることはできません。 更新プログラムをインストールしたら、**[機能]** ノードでこれらの機能を表示できます。 ただし、**[階級設定]** で同意するまではこれらの機能を有効にすることはできません。

スタンドアロン プライマリ サイトで同意し、新しい中央管理サイトをインストールして階層を拡張する場合、中央管理サイトでもう一度同意する必要があります。

 プレリリース機能を有効にすると、Configuration Manager の階層マネージャー (HMAN) は機能が利用可能になる前に変更を処理する必要があります。 多くの場合、変更の処理はすぐに行われますが、HMAN の処理サイクルによっては完了までに最大で 30 分かかることがあります。 変更が処理された後、その機能に関連する新しい UI が表示されるようにするには、コンソールを再起動する必要があります。

**利用できるプレリリース機能:**

 |機能          |プレリリース版として追加 | 完全機能として追加|  
|------------------|---------------------|---------------------|
|段階的展開<!--1356837-->|[バージョン 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence.md)|![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| タスク シーケンス ステップの実行<!-- 1261338 --> |  [バージョン 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |[バージョン 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence)|
| Windows Defender Exploit Guard <!-- 1355468 --> |  [バージョン 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |[バージョン 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)|
| 条件付きアクセス コンプライアンス ポリシーに対するデバイス正常性構成証明の評価 <!-- 1235616 --> |  [バージョン 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |[バージョン 1802](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)|
| Configuration Manager コンソールから PowerShell スクリプトを作成して実行する<!-- 1236459 --> |  [バージョン 1706](/sccm/apps/deploy-use/create-deploy-scripts)|[バージョン 1802](/sccm/apps/deploy-use/create-deploy-scripts)|
| Microsoft Surface ドライバーの更新プログラムの管理 <!-- 1098490 --> |  [バージョン 1706](/sccm/sum/get-started/configure-classifications-and-products) | [バージョン 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| Configuration Manager を使用した Device Guard 管理<!-- 1319346 --> |  [バージョン 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| タスク シーケンス コンテンツの事前キャッシュ<!-- 1021244 --> |  [バージョン 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [バージョン 1706](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| アプリケーションをインストールする前に実行中の実行可能ファイルを確認する<!-- 1284624 --> |   [バージョン 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[バージョン 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| データ ウェアハウス サービス ポイント<!-- 1277922 --> |  [バージョン 1702](/sccm/core/servers/manage/data-warehouse) |[バージョン 1706](/sccm/core/servers/manage/data-warehouse)|
| クライアントへのコンテンツ配布のピア キャッシュ<!-- 1101436 --> |  [バージョン 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [バージョン 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| クラウド管理ゲートウェイ<!-- 1101764 --> |  [バージョン 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |[バージョン 1802](/sccm/core/clients/manage/plan-cloud-management-gateway)|
| Microsoft Operations Management Suite コネクタ<!-- 1236739 --> | [バージョン 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |[バージョン 1802](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md)|
| クラスター対応のコレクションのサービス (サーバー グループの提供)<!-- 1081776 --> | [バージョン 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| System Center Configuration Manager が管理する PC の条件付きアクセス<!--  --> | [バージョン 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [バージョン 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
<!--Image used = ![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif) -->