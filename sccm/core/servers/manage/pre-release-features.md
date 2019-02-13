---
title: プレリリース機能
titleSuffix: Configuration Manager
description: プレリリース機能は、運用環境での初期テスト用の Current Branch に含まれている機能です。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e1becb8cc719466edabfb55ce82f9aa5e3345e3f
ms.sourcegitcommit: 013ca76d5a3c07306de7b5bfd985b0289d1be599
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "55482437"
---
# <a name="pre-release-features-in-configuration-manager"></a>Configuration Manager のプレリリース機能

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

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
| SMS プロバイダー API <!--1359052--> | バージョン 1810 | ![未追加](media/red_x.png) |
| [拡張 HTTP サイト システム](/sccm/core/plan-design/hierarchy/enhanced-http) <!--1356889,1358228--> | バージョン 1806 | バージョン 1810 |
| [共同管理デバイス向けのクライアント アプリ](/sccm/comanage/workloads#client-apps) <!--1357892--> | バージョン 1806 | ![未追加](media/red_x.png) |
| [SCAP 拡張機能](/sccm/compliance/plan-design/scap/about-scap) <!--3607889--> | バージョン 1806 | ![未追加](media/red_x.png) |
| [パッケージ変換マネージャー](/sccm/apps/pcm/package-conversion-manager) <!--1357861--> | バージョン 1806 | バージョン 1810 |
| [iOS 向け Cisco AnyConnect 4.0.07x 以降のサポート](/sccm/mdm/deploy-use/create-vpn-profiles) <!--1357393--> | バージョン 1802 | バージョン 1802 <br>更新プログラム 4163547 適用 |
| [段階的展開](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) <!--1356837--> | バージョン 1802 | バージョン 1806 |
| [タスク シーケンス ステップの実行](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338--> |  バージョン 1710 | バージョン 1802 |
| [Windows Defender Exploit Guard](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468--> | バージョン 1710 | バージョン 1802 |
| [条件付きアクセス コンプライアンス ポリシーに対するデバイス正常性構成証明の評価](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616--> | バージョン 1710 | バージョン 1802 |
| [Windows PowerShell スクリプトの作成と実行](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459--> | バージョン 1706 | バージョン 1802 |
| [Microsoft Surface ドライバーの更新プログラムの管理](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490--> | バージョン 1706 | バージョン 1710 |
| [Device Guard 管理](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) <!--1355092 (1319346)--> | バージョン 1702 | ![未追加](media/red_x.png) |
| [タスク シーケンス コンテンツの事前キャッシュ](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244--> | バージョン 1702 | バージョン 1710 |
| [アプリケーションをインストールする前に実行中の実行可能ファイルを確認する](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) <!--1284624--> | バージョン 1702 | バージョン 1706 |
| [データ ウェアハウス サービス ポイント](/sccm/core/servers/manage/data-warehouse) <!--1277922--> | バージョン 1702 | バージョン 1706 |
| [クライアントへのコンテンツ配布のピア キャッシュ](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436--> | バージョン 1610 | バージョン 1710 |
| [クラウド管理ゲートウェイ](/sccm/core/clients/manage/plan-cloud-management-gateway) <!--1101764--> | バージョン 1610 | バージョン 1802 |
| [Azure Log Analytics コネクタ](/sccm/core/clients/manage/sync-data-log-analytics) <!--1236739--> | バージョン 1606 | バージョン 1802 |
| [クラスター対応のコレクションのサービス (サーバー グループの提供)](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_ServerGroups) <!--1081776--> | バージョン 1602 | ![未追加](media/red_x.png) |
| [Configuration Manager が管理する PC の条件付きアクセス](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--  --> | バージョン 1602 | バージョン 1702 |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> 最初に有効にする必要があるプレリリース版以外の機能の詳細については、「[更新プログラムのオプション機能の有効化](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」を参照してください。  
> 
> Technical Preview Branch でのみ利用できる機能の詳細については、[Technical Preview](/sccm/core/get-started/technical-preview) に関するページを参照してください。  
