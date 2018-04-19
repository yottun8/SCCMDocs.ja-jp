---
title: Technical Preview リリース
titleSuffix: Configuration Manager
description: Configuration Manager の新機能を体験するテクニカル プレビュー リリースについて説明します。
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 753503fd8c59ef8f93c0968c3d5c386cec35f88e
ms.sourcegitcommit: a19e12d5c3198764901d44f4df7c60eb542e765f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager の Technical Preview

*適用対象: System Center Configuration Manager (Technical Preview)*

**System Center Configuration Manager Technical Preview へようこそ**。 この記事では、最新のプレビュー リリースについて詳しく説明します。プレビュー リリースには、現在開発中の新しい機能と可能性が含まれます。 Technical Preview の各バージョンでは、そのバージョンが公開された時点において Configuration Manager の Current Branch に組み込まれていない新しい機能が導入されます。 これらの機能は、最終的に現在のブランチのリリースに対する更新プログラムに組み込まれる場合がありますが、最終版として追加される前に、これらの機能をお試しいただき、フィードバックをご提供いただければと思います。  

 このリリースはテクニカル プレビューであるため、詳細や機能は変更されることがあります。  

 この記事には、Technical Preview のすべてのバージョンに適用される情報が含まれています。 また、新しい各機能 (またはフィーチャー) とそれが初めて導入された Technical Preview のバージョン (たとえば、2018 年 3 月であればバージョン 1803) がリストされます。 これらの機能の詳細は、各プレビュー バージョンに特化した個別のトピックで説明されています。  

 Configuration Manager の現在のブランチの新機能については、「[What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)」 (System Center Configuration Manager の新機能) を参照してください。



##  <a name="bkmk_reqs"></a> Technical Preview の要件と制限事項  

> [!IMPORTANT]     
>  Technical Preview はラボ環境での使用目的に限定してライセンスされます。  Microsoft はサポート サービスを提供しない場合があり、また、プレビュー ソフトウェアでは特定の機能が使用できない場合があります。 さらに、プレビュー ソフトウェアは、製品版ソフトウェアに比べて、セキュリティ、プライバシー、アクセシビリティ、可用性および信頼性の基準が低いか、または異なる場合があります。  

 ほとんどの製品の前提条件については、「[Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)」 (System Center Configuration Manager でサポートされる構成) を参照してください。 次の例外がテクニカル プレビュー リリースに適用されます。  

-   各インストールは 90 日後に使用期限が切れるまでアクティブです。  

-   サポートされる言語は英語のみです。


-   次のインストール フラグ (スイッチ) のみがサポートされます。  

    -   **/silent**  
    -   **/testdbupgrade**    


-   既定では、Technical Preview を使用すると、サービス接続ポイントがオンライン モードにインストールされます。 オフライン モードへの変更はサポートされていません。

-   Technical Preview の特定バージョンごとの個別の記事には、追加の制限または要件が含まれています。

-   このプレビュー ビルドへの移行、またはこのプレビュー ビルドからの移行はサポートされません。  

-   このプレビュー ビルドへのアップグレードはサポートされません。 

-   cd.latest フォルダーからのサイトの回復はサポートされません。  <!--507106-->

-   このプレビュー ビルドから、製品版 (現在のブランチ) へのアップグレードはサポートされません。 ただし、プレビュー バージョンから更新プログラムが使用できる場合は、Configuration Manager コンソールの **[更新とサービス]** ノードから検索してからインストールできます。 コンソール内アップグレード プロセスに関する「 [ConfigMgr 更新プログラム パッケージをインストールする](https://www.youtube.com/embed/KBd_EGFbUT8) 」というビデオを youtube.com でご覧ください。  
-   スタンドアロンのプライマリ サイトのみがサポートされます。 中央管理サイト、複数のプライマリ サイト、またはセカンダリ サイトはサポートされません。  

この Configuration Manager のブランチでは、次の製品とテクノロジがサポートされています。 ただし、これは製品またはバージョンの各サポート ライフサイクルが過ぎてもサポートを延長するという意味ではありません。 既にサポート ライフサイクルが終了している製品は、Configuration Manager ではサポートされません。 マイクロソフト サポート ライフサイクルの詳細については、 [「マイクロソフト サポート ライフサイクル」](http://go.microsoft.com/fwlink/p/?LinkId=208270) Web サイトを参照してください。  

-   次のバージョンの SQL Server のみがサポートされます。  

    -   Configuration Manager バージョン 1710 以降の SQL Server 2017 (累積的な更新プログラム 2 以降適用済み)
    -   SQL Server 2016 (Service Pack なし、およびそれ以降)
    -   SQL Server 2014 (Service Pack 1 以降)
    -   SQL Server 2012 (Service Pack 3 以降)


-   サイトは最大 10 台のクライアントをサポートします。各クライアントは次のいずれかの Windows バージョンを実行している必要があります。  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

##  <a name="bkmk_install"></a> Technical Preview のインストールと更新  
 System Center Configuration Manager の Technical Preview は、System Center Configuration Manager の最新リリースとは異なります。  

 Technical Preview を使用するには、Technical Preview ビルドの **ベースライン バージョン** を最初にインストールする必要があります。 ベースライン バージョンをインストールしたら、**コンソール内更新**を使用して、最新のプレビュー バージョンでインストール環境を最新の状態にすることができます。 通常、Technical Preview の新バージョンは毎月使用可能です。

各プレビュー リリースは、3 つの連続したリリースが使用可能になるまでサポートされます。 つまり、バージョン 1708 がリリースされると、バージョン 1704 はサポートされなくなりますが、バージョン 1705、1706、1707 は引き続きサポートされます。 ベースラインがサポート対象でなくなっても、そのインストールをサポートされるバージョンに更新すれば、(新しいベースライン バージョンが使用できるようになるまでは) 新しい Technical Preview サイトのインストールがサポートされます。 提供されている最新のバージョンに更新した後、最新バージョンの Technical Preview をインストールできるようになるまでそのプロセスを繰り返します。

> [!TIP]  
>  Technical Preview の更新プログラムをインストールするときに、プレビュー インストール環境を対象の新しい Technical Preview バージョンに更新します。 Technical Preview のインストールでは、現在のブランチのインストールにアップグレードすることも、現在のブランチ リリースから更新を受け取ることもできません。  

**Technical Preview のアクティブ ベースライン バージョン:**
   
リリース後、最長 1 年間、ベースライン バージョンをインストールできます。 ただし、新しい Technical Preview サイトをインストールする場合は、利用可能な最新のベースライン バージョンを使用することをお勧めします。
-  **Technical Preview 1711** - Configuration Manager Technical Preview 1711 は、コンソール内更新と、新しいベースライン バージョンの両方として使用できます。 ベースライン バージョンを [TechNet Evaluation Center から](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)ダウンロードします。


##  <a name="BKMK_TPFeedback"></a> フィードバックについて  
 Technical Preview の機能に関するフィードバックをお寄せください。 詳細については、「[製品に関するフィードバック](../understand/find-help.md#product-feedback)」を参照してください。

希望する新しい機能のアイデアがありましたら、その内容もお知らせください。 新しいアイデアを提出する、または、他の人が提出したアイデアに投票するには、 [ユーザー ボイスのページにアクセス](http://configurationmanager.uservoice.com)してください。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> 最新の Technical Preview で提供される機能  
以下は、最新の Configuration Manager Technical Preview リリースで提供される機能です。  Technical Preview の以前のバージョンで利用できるようになった機能は、以降のバージョンでも利用できます。 同様に、Configuration Manager の Current Branch に追加された機能は、後続の Technical Preview でも引き続き利用できます。  特定の機能の詳細については、各プレビュー バージョンのコンテンツをクリックします。  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1803"></a>Technical Preview バージョン 1803
- [ソースとしてのクラウド配布ポイントのプル配布ポイントのサポート](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source) <!--1321554--> 
- [WAN の使用率を減らすためのクライアント ピア キャッシュでの部分的なダウンロードのサポート](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization) <!--1357346--> 
- [ソフトウェア センターのメンテナンス期間](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center) <!--1358131--> 
- [ソフトウェア センターの Web ページのカスタム タブ](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center) <!--1358132--> 
- [クライアントでサード パーティ製ソフトウェア更新プログラムを有効にするサポート](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients) <!--1357605-->
- [監視ビューからの資産の詳細のコピー/貼り付けを有効にする](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views) <!--1357552-->
- [SCAP 拡張機能](capabilities-in-technical-preview-1803.md#scap-extensions) <!--1357552-->



## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>サポートされている最新の Technical Preview で提供される機能
以下は、Configuration Manager Technical Preview の以前のリリースで提供され、引き続きサポートされている機能です。 

<!-- This is the full list of new features in the past three TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |機能 |Technical Preview バージョン |Current Branch バージョン|  
 |----------------|---------------------|--------------------|
 | 共同管理を使用して Intune に Endpoint Protection ワークロードを移行する <!-- 1357365 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#transition-endpoint-protection-workload-to-intune-using-co-management) | [バージョン 1802](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune) |  
 | Configuration Manager 境界グループを使用するように Windows の配信の最適化を構成する <!-- 1324696 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups) | [バージョン 1802](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization) |  
 | クラウド管理ゲートウェイ経由での Windows 10 一括アップグレード タスク シーケンス <!-- 1357149 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway) | [バージョン 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg) |  
 | Windows 10 一括アップグレード タスク シーケンスの機能強化 <!-- 1357425 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-windows-10-in-place-upgrade-task-sequence) | [バージョン 1802](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) |  
 | PXE 対応の配布ポイントの機能強化 <!-- 1357580 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | ![追加されていません](media/Red_X.gif) | 
 | タスク シーケンスの展開テンプレート <!-- 1357391 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#deployment-templates-for-task-sequences) | [バージョン 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) |  
 | 製品ライフサイクル ダッシュボード <!--1319632 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | ![追加されていません](media/Red_X.gif) | 
 | レポートの機能強化 <!--1357653 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-reporting) | [バージョン 1802](/sccm/core/servers/manage/list-of-reports#operating-system) |  
 | ソフトウェア センターの機能強化 <!--1357592 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-software-center) | [バージョン 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled) |  
 | 管理ポイントに対する境界グループのフォールバック <!-- 1324594 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#boundary-group-fallback-for-management-points) | [バージョン 1802](/sccm/core/servers/deploy/configure/boundary-groups#management-points) |  
 | CNG 証明書のサポートの強化 <!-- 1357314 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improved-support-for-cng-certificates) | [バージョン 1802](/sccm/core/plan-design/network/cng-certificates-overview) |  
 | Azure Resource Manager に対するクラウド管理ゲートウェイのサポート <!-- 1324735 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#cloud-management-gateway-support-for-azure-resource-manager) | [バージョン 1802](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager) |  
 | デバイスごとにユーザーのアプリケーション要求を承認する <!-- 1357015 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#approve-application-requests-for-users-per-device) | [バージョン 1802](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) |  
 | ソフトウェア センターを使用してユーザーが利用できるアプリケーションを参照し、Azure AD に参加しているデバイスにインストールする <!-- 1322613 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices) | [バージョン 1802](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices) |  
 | Windows AutoPilot のデバイス情報についてのレポート <!-- 1351442 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-on-windows-autopilot-device-information) | [バージョン 1802](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices) |  
 | Windows Defender Exploit Guard に対する Configuration Manager ポリシーの機能強化 <!-- 1356220 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard) | [バージョン 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |  
 | Microsoft Edge ブラウザーのポリシー <!-- 1357310 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#microsoft-edge-browser-policies) | [バージョン 1802](/sccm/compliance/deploy-use/browser-profiles) | 
 | 既定のブラウザー数についてのレポート <!-- 1357830 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-for-default-browser-counts) | [バージョン 1802](/sccm/core/servers/manage/list-of-reports#software---companies-and-products) | 
 | Windows 10 ARM64 デバイスのサポート <!-- 1353704 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#support-for-windows-10-arm64-devices) | [バージョン 1802](/sccm/core/plan-design/configs/support-for-windows-10) |  
 | 段階的展開を作成する <!-- 1356837 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#create-phased-deployments) | [バージョン 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) |
 | 共同管理のレポート <!-- 1356648 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#co-management-reporting) | [バージョン 1802](\sccm\core\clients\manage\client-management-dashboard) |
 | 自動展開規則の評価スケジュールの機能強化 <!-- 1357133 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-automatic-deployment-rule-evaluation-schedule) | [バージョン 1802](/sccm/sum/deploy-use/automatically-deploy-software-updates#BKMK_CreateAutomaticDeploymentRule) |
 | 配布ポイントの再割り当て <!-- 1306937 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#reassign-distribution-point) | [バージョン 1802](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign) |
 | ハードウェア インベントリの機能強化 <!-- 1357389 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-hardware-inventory) | [バージョン 1802](/sccm/core/clients/manage/inventory/extend-hardware-inventory#BKMK_GreaterThan255) |
 | ソフトウェア センターのクライアント設定の機能強化 <!-- 1355146 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-client-settings-for-software-center) | [バージョン 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideUnapproved) |
 | Windows Defender Application Guard の新しい設定 <!-- 1356256 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#new-settings-for-windows-defender-application-guard) | [バージョン 1802](/sccm/protect/deploy-use/create-deploy-application-guard-policy#BKMK_HIS) |
 | スクリプト実行の機能強化 <!-- 1236459 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-run-scripts) | [バージョン 1802](/sccm/apps/deploy-use/create-deploy-scripts) |
 | 置き換えられたアプリケーションを自動的にアップグレードしない <!-- 1351266 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#do-not-automatically-upgrade-superseded-applications) | [バージョン 1802](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) | 
 | ソフトウェア センターで複数のアプリケーションをインストールする <!-- 1357126 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#install-multiple-applications-in-software-center) | [バージョン 1802](/sccm/core/understand/software-center#install-multiple-applications) |
 | クライアント ベースの PXE レスポンダー サービス <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) | ![追加されていません](media/Red_X.gif) |
 | Configuration Manager クライアント インストールにおける変更 <!-- 1356195 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-in-the-configuration-manager-client-install) | [バージョン 1802](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.#BKMK_ExternalDependencies) | 
 | Surface デバイス ダッシュボードに対する変更 <!-- 1355788 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-to-the-surface-device-dashboard) | [バージョン 1802](/sccm/core/clients/manage/surface-device-dashboard) | 
 | Office 365 クライアント管理ダッシュボードの機能拡張 <!-- 1357281 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-office-365-client-management-dashboard) | [バージョン 1802](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard) | 
 | Configuration Manager コンソールの機能拡張 <!-- 1357280,1357282 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-the-configuration-manager-console) | バージョン 1802 | 
 | OS 展開の機能強化 <!-- SMS 500897 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-operating-system-deployment) | バージョン 1802 | 

  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>以前の Technical Preview で提供される機能
以下は、Configuration Manager Technical Preview リリースの以前のバージョンで提供された特定の機能です。 これらの機能は、以降のバージョンでも使用できますが、Current Branch リリースではまだ提供されていません。 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |機能 |Technical Preview バージョン |  
 |----------------|---------------------|
 |サイト サーバーの役割の高可用性<!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |PXE ネットワーク ブートでの IPv6 のサポート<!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Azure Active Directory の使用 <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Windows Update for Business 更新プログラムのコンプライアンス評価<!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |OData エンドポイントのデータ アクセス<!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |資産インテリジェンスの改善 <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |エンド ユーザーはポータル サイトからアプリをインストールできる<!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>関連項目  
[System Center Configuration Manager の新機能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [System Center Configuration Manager の概要](../../core/understand/introduction.md)
