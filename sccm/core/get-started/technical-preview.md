---
title: Technical Preview リリース
titleSuffix: Configuration Manager
description: Configuration Manager の新機能を体験するテクニカル プレビュー リリースについて説明します。
ms.date: 05/11/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a6a4faff728b14fae198f9709ca9ce9ca5d04455
ms.sourcegitcommit: 021272d5858e5dbb650b95644736d1de3dab7d8a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager の Technical Preview

*適用対象: System Center Configuration Manager (Technical Preview)*

**System Center Configuration Manager Technical Preview へようこそ**。 この記事では、最新のプレビュー リリースについて詳しく説明します。プレビュー リリースには、現在開発中の新しい機能と可能性が含まれます。 Technical Preview の各バージョンでは、そのバージョンが公開された時点において Configuration Manager の Current Branch に組み込まれていない新しい機能が導入されます。 これらの機能は、最終的に現在のブランチのリリースに対する更新プログラムに組み込まれる場合がありますが、最終版として追加される前に、これらの機能をお試しいただき、フィードバックをご提供いただければと思います。  

 このリリースはテクニカル プレビューであるため、詳細や機能は変更されることがあります。  

 この記事には、Technical Preview のすべてのバージョンに適用される情報が含まれています。 また、新しい各機能 (またはフィーチャー) とそれが初めて導入された Technical Preview のバージョン (たとえば、2018 年 5 月であればバージョン 1805) がリストされます。 これらの機能の詳細は、各プレビュー バージョンに特化した個別のトピックで説明されています。  

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
-  **Technical Preview 1804** - Configuration Manager Technical Preview 1804 は、コンソール内更新と、新しいベースライン バージョンの両方として使用できます。 ベースライン バージョンを [TechNet Evaluation Center から](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)ダウンロードします。


##  <a name="BKMK_TPFeedback"></a> フィードバックについて  
 Technical Preview の機能に関するフィードバックをお寄せください。 詳細については、「[製品に関するフィードバック](../understand/find-help.md#product-feedback)」を参照してください。

希望する新しい機能のアイデアがありましたら、その内容もお知らせください。 新しいアイデアを提出する、または、他の人が提出したアイデアに投票するには、 [ユーザー ボイスのページにアクセス](http://configurationmanager.uservoice.com)してください。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> 最新の Technical Preview で提供される機能  
以下は、最新の Configuration Manager Technical Preview リリースで提供される機能です。  Technical Preview の以前のバージョンで利用できるようになった機能は、以降のバージョンでも利用できます。 同様に、Configuration Manager の Current Branch に追加された機能は、後続の Technical Preview でも引き続き利用できます。  特定の機能の詳細については、各プレビュー バージョンのコンテンツをクリックします。  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1805"></a>Technical Preview バージョン 1805
- [タスク シーケンスに手動で構成されたフェーズを使用して段階的展開を作成する](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence) <!--1358148--> 
- [Azure Resource Manager のためのクラウド配布ポイントのサポート](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager) <!--1322209--> 
- [管理の洞察に基づいて対策する](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights) <!--1357930--> 
- [共同管理を使用して Intune にデバイス構成ワークロードを移行する](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management) <!--1357903--> 
- [ネットワークの輻そう制御を使用する配布ポイントを有効にする](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control) <!--1358112--> 
- [クラウド管理ダッシュボード](capabilities-in-technical-preview-1805.md#cloud-management-dashboard) <!--1358461--> 
- [CMPivot](capabilities-in-technical-preview-1805.md#cmpivot) <!--1358456--> 
- [改善されたセキュアなクライアント通信](capabilities-in-technical-preview-1805.md#improved-secure-client-communications) <!--1356889,1358228,1358460--> 
- [サード パーティ製のソフトウェア更新プログラムのサポートを有効にする場合の機能強化](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support) <!--1357605--> 
- [Windows 10 一括アップグレード タスク シーケンスの機能強化](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence) <!--1358500--> 
- [クライアントを使ってインストールされた CMTrace](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client) <!--1357971--> 
- [Configuration Manager コンソールの機能強化](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console) <!--1358202--> 
- [コンソール フィードバックの機能強化](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback) <!--1357542--> 
- [PXE 対応の配布ポイントの機能強化](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points) <!--1357580--> 
- [大きな整数値でのハードウェア インベントリの機能強化](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values) <!--1357880--> 
- [WSUS メンテナンスの機能強化](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance) <!--1357898--> 
- [CNG 証明書のサポートの強化](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates) <!--1357314--> 






## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>サポートされている最新の Technical Preview で提供される機能
以下は、Configuration Manager Technical Preview の以前のリリースで提供され、引き続きサポートされている機能です。 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |機能 |Technical Preview バージョン |Current Branch バージョン|  
 |----------------|---------------------|--------------------|
 | サイト サーバーのリモート コンテンツ ライブラリを構成する <!--1357525--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)  | ![追加されていません](media/Red_X.gif) | 
 | Configuration Manager コンソールからフィードバックを送信する<!--1357542--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#bkmk_feedback)  | ![追加されていません](media/Red_X.gif) | 
 | サポート センター <!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | ![追加されていません](media/Red_X.gif) | 
 | Configuration Manager Toolkit <!--1357145--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit)  | ![追加されていません](media/Red_X.gif) | 
 | 承認を取り消したときにアプリケーションをアンインストールする <!--1357891--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation)  | ![追加されていません](media/Red_X.gif) | 
 | 探索から Active Directory コンテナーを除外する <!--1358143--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery)  | ![追加されていません](media/Red_X.gif) | 
 | ソフトウェア センターのアプリケーション カタログ Web サイト リンクの表示を指定する <!--1358214--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center)  | ![追加されていません](media/Red_X.gif) | 
 | ソフトウェア更新アーキテクチャを使用した自動展開規則のフィルター処理 <!--1322266--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture)  | ![追加されていません](media/Red_X.gif) | 
 | OS 展開の機能強化 <!--1358330,1358493--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) | ![追加されていません](media/Red_X.gif) | 
 | ソースとしてのクラウド配布ポイントのプル配布ポイントのサポート <!--1321554--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | ![追加されていません](media/Red_X.gif) | 
 | WAN の使用率を減らすためのクライアント ピア キャッシュでの部分的なダウンロードのサポート <!--1357346--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | ![追加されていません](media/Red_X.gif) | 
 | ソフトウェア センターのメンテナンス期間 <!--1358131--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | ![追加されていません](media/Red_X.gif) | 
 | ソフトウェア センターの Web ページのカスタム タブ <!--1358132--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | ![追加されていません](media/Red_X.gif) | 
 | クライアントでサード パーティ製ソフトウェア更新プログラムを有効にするサポート <!--1357605--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | ![追加されていません](media/Red_X.gif) | 
 | 監視ビューからの資産の詳細のコピー/貼り付けを有効にする <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | ![追加されていません](media/Red_X.gif) | 
 | SCAP 拡張機能 <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | ![追加されていません](media/Red_X.gif) | 
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
 
  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>以前の Technical Preview で提供される機能
以下は、Configuration Manager Technical Preview リリースの以前のバージョンで提供された特定の機能です。 これらの機能は、以降のバージョンでも使用できますが、Current Branch リリースではまだ提供されていません。 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |機能 |Technical Preview バージョン |  
 |----------------|---------------------|
 | クライアント ベースの PXE レスポンダー サービス <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
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

> [!Tip]  
> 有効化に同意が必要な最新のブランチ機能の詳細については、[プレリリース機能](/sccm/core/servers/manage/pre-release-features)に関するページを参照してください。  
> 最初に有効にする必要があるプレリリース版以外の最新のブランチ機能の詳細については、「[更新プログラムのオプション機能の有効化](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」を参照してください。  

