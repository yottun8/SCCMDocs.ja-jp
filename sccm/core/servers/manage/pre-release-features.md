---
title: "プレリリース機能 | Microsoft Docs"
description: "System Center Configuration Manager のプレリリース機能"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: c164ae7ca17a3a7d96b010f41b5ecf72ab34976b
ms.lasthandoff: 03/04/2017


---
# <a name="pre-release-feaures-in-system-center-configuration-manager"></a>System Center Configuration Manager のプレリリース機能
*適用対象: System Center Configuration Manager (Current Branch)*

 プレリリース機能は、実稼働環境での初期テストの Current Branch に含まれている機能です。 これらの機能は実稼働の準備ができていると見なすべきではありませんが、実稼働環境で使用することはできます。

 プレリリース機能を使用できるようになる前に、Configuration Manager コンソールのプレリリース機能を使用することに同意してはじめて、その機能を選択して使用を有効にすることができます。  

同意する操作は階層ごとに&1; 回限りの操作であり、元に戻すことはできません 同意するまでは、更新プログラムに含まれている新しいプレリリース機能を有効にすることはできません。

同意するには、コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** に移動してから、**[階層設定]** を選択します。 **[全般]** タブで、**[プレリリース機能を使用することに同意する]** を選択します。

 > [!NOTE]
 > 1602 より後の更新バージョンをインストールする前に更新プログラム 1602 のプレリリース機能の使用を有効にしていた場合は、プレリリース機能を使用する同意をしなくても、それらの機能は有効のままになります。

プレリリース機能を含む更新プログラムをインストールすると、これらの機能は、更新プログラムに含まれる標準の機能と一緒に、[更新とサービス] ウィザードに表示されます。
  - **既に同意した場合:** 更新プログラムのインストール時に、[更新とサービス] ウィザード内でプレリリース機能を有効にすることができます。 これを行うには、その他の機能の場合と同様に、プレリリース機能を選択します。     

    必要に応じて、後でコンソールの **[管理]** > **[クラウド サービス]** > **[更新とサービス]** > **[機能]** ノードからプレリリース機能を有効にすることもできます。 **[機能]** ノードで、機能を選択し、**[有効にする]** を選択します (このオプションは同意するまで灰色表示のままです)。  
  -   **まだ同意していない場合:** 更新プログラムのインストール時に、プレリリース機能は [更新とサービス] ウィザードに表示されますが、灰色表示になっていて、有効にすることはできません。 更新プログラムをインストールした後は、**[機能]** ノードにこれらの機能が表示されますが、**[階層設定]** で同意するまで有効にすることはできません。

スタンドアロン プライマリ サイトで同意し、新しい中央管理サイトをインストールして階層を拡張する場合、中央管理サイトでもう一度同意する必要があります。

**利用できるプレリリース機能:**

 |機能          |プレリリース版として追加 | 完全機能として追加|  
|------------------|---------------------|---------------------|
| データ ウェアハウス サービス ポイント  |  [バージョン 1702](/sccm/core/servers/manage/data-warehouse) |![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| クライアントへのコンテンツ配布のピア キャッシュ |  [バージョン 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| クラウド管理ゲートウェイ |  [バージョン 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| クライアント データ ソース ダッシュボード |  [バージョン 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Microsoft Operations Management Suite コネクタ  | [バージョン 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| クラスター対応のコレクションのサービス (サーバー グループの提供)| [バージョン 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|System Center Configuration Manager が管理する PC の条件付きアクセス | [バージョン 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     |![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)                        |

