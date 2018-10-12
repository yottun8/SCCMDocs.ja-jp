---
title: プレリリース機能
titleSuffix: Configuration Manager
description: プレリリース機能は、運用環境での初期テスト用の Current Branch に含まれている機能です。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7b82bdfcbe69c7e9d59185fc6af20a85e65a6e7d
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893568"
---
# <a name="pre-release-features-in-configuration-manager"></a>Configuration Manager のプレリリース機能

*適用対象: System Center Configuration Manager (Current Branch)*

プレリリース機能は、運用環境での初期テスト用の Current Branch に含まれている機能です。 これらの機能は完全にサポートされていますが、現在開発中です。 プレリリース カテゴリから移動するまでは変更が行われる可能性があります。



## <a name="give-consent"></a>同意する  

プレリリース機能を使用する前に、プレリリース機能を使用することに同意します。 同意することは階層ごとに 1 回限りの操作であり、元に戻すことはできません。 同意するまでは、更新プログラムに含まれている新しいプレリリース機能を有効にすることはできません。 プレリリース機能を有効にした後で無効にすることはできません。

1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[サイトの構成]** を展開して **[サイト]** ノードを選択します。  

2. リボンの **[階層設定]** をクリックします。  

3. [階層設定のプロパティ] の **[全般]** タブで、**[プレリリース機能を使用することに同意する]** オプションを有効にします。 **[OK]** をクリックします。  



## <a name="enabling-pre-release-features"></a>プレリリース機能の有効化

プレリリース機能を含む更新プログラムをインストールすると、これらの機能は、更新プログラムに含まれる標準の機能と一緒に、[更新とサービス] ウィザードに表示されます。

#### <a name="if-you-have-given-consent"></a>同意した場合
更新とサービス ウィザードで、プレリリース機能を有効にします。 他の機能の場合と同じように、プレリリース機能を選択します。     

必要に応じて、後で **[管理]** ワークスペース内の **[更新とサービス]** の下にある **[機能]** ノードからプレリリース機能を有効にします。 機能を選択し、リボンの **[有効にする]** をクリックします。 同意するまで、このオプションは利用できません。

#### <a name="if-you-havent-given-consent"></a>同意していない場合
更新とサービス ウィザードに、プレリリース機能は表示されますが、有効にすることはできません。 更新プログラムがインストールされた後、**[機能]** ノードにこれらの機能が表示されます。 しかし、同意するまでそれらを有効することはできません。


> [!Important]  
> 複数サイトの階層では、中央管理サイトからオプション機能またはプレリリース機能のみを有効にできます。 この動作によって、階層全体で競合が発生しないようにします。 <!--507197-->  
> 
> スタンドアロン プライマリ サイトで同意し、新しい中央管理サイトをインストールして階層を拡張する場合、中央管理サイトでもう一度同意する必要があります。  

プレリリース機能を有効にすると、Configuration Manager の階層マネージャー (HMAN) は機能が利用可能になる前に変更を処理する必要があります。 多くの場合、変更の処理はすぐに行われます。 HMAN の処理サイクルによっては、完了までに最大 30 分かかることがあります。 変更が処理された後、その機能を使用するには、まずコンソールを再起動します。



## <a name="pre-release-features"></a>プレリリース機能

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  


> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1706, this feature is no longer a pre-release feature.  

-->


| 機能          | プレリリース版として追加 | 完全機能として追加 |  
|------------------|----------------------|-------------------------|
| 拡張 HTTP サイト システム<!--1356889,1358228-->|バージョン 1806|![未追加](media/red_x.png)|
| 共同管理デバイス向けのモバイル アプリ<!--1357892-->|[バージョン 1806](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune)|![未追加](media/red_x.png)|
| パッケージ変換マネージャー<!--1357861-->|[バージョン 1806](/sccm/apps/pcm/package-conversion-manager)|![未追加](media/red_x.png)|
| iOS 向け Cisco AnyConnect 4.0.07x 以降のサポート<!--1357393-->|[バージョン 1802](/sccm/mdm/deploy-use/create-vpn-profiles)| [バージョン 1802 (更新プログラム 4163547 適用)](/sccm/mdm/deploy-use/create-vpn-profiles) |
| 段階的展開<!--1356837-->|[バージョン 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|[バージョン 1806](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|
| タスク シーケンス ステップの実行<!-- 1261338 --> |  [バージョン 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |[バージョン 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence)|
| Windows Defender Exploit Guard <!-- 1355468 --> |  [バージョン 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |[バージョン 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)|
| 条件付きアクセス コンプライアンス ポリシーに対するデバイス正常性構成証明の評価 <!-- 1235616 --> |  [バージョン 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |[バージョン 1802](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)|
| Configuration Manager コンソールから PowerShell スクリプトを作成して実行する<!-- 1236459 --> |  [バージョン 1706](/sccm/apps/deploy-use/create-deploy-scripts)|[バージョン 1802](/sccm/apps/deploy-use/create-deploy-scripts)|
| Microsoft Surface ドライバーの更新プログラムの管理 <!-- 1098490 --> |  [バージョン 1706](/sccm/sum/get-started/configure-classifications-and-products) | [バージョン 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| Configuration Manager を使用した Device Guard 管理<!-- 1319346 --> |  [バージョン 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![未追加](media/red_x.png)|
| タスク シーケンス コンテンツの事前キャッシュ<!-- 1021244 --> |  [バージョン 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [バージョン 1710](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| アプリケーションをインストールする前に実行中の実行可能ファイルを確認する<!-- 1284624 --> |   [バージョン 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[バージョン 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| データ ウェアハウス サービス ポイント<!-- 1277922 --> |  [バージョン 1702](/sccm/core/servers/manage/data-warehouse) |[バージョン 1706](/sccm/core/servers/manage/data-warehouse)|
| クライアントへのコンテンツ配布のピア キャッシュ<!-- 1101436 --> |  [バージョン 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [バージョン 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| クラウド管理ゲートウェイ<!-- 1101764 --> |  [バージョン 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |[バージョン 1802](/sccm/core/clients/manage/plan-cloud-management-gateway)|
| Log Analytics コネクタ <!-- 1236739 --> | [バージョン 1606](/sccm/core/clients/manage/sync-data-log-analytics) |[バージョン 1802](/sccm/core/clients/manage/sync-data-log-analytics)|
| クラスター対応のコレクションのサービス (サーバー グループの提供)<!-- 1081776 --> | [バージョン 1602](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_ServerGroups)|![未追加](media/red_x.png)|
| System Center Configuration Manager が管理する PC の条件付きアクセス<!--  --> | [バージョン 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [バージョン 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> 最初に有効にする必要があるプレリリース版以外の機能の詳細については、「[更新プログラムのオプション機能の有効化](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」を参照してください。  
> 
> Technical Preview Branch でのみ利用できる機能の詳細については、[Technical Preview](/sccm/core/get-started/technical-preview) に関するページを参照してください。  
