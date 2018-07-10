---
title: Technical Preview リリース
titleSuffix: Configuration Manager
description: Configuration Manager の新機能を体験するテクニカル プレビュー リリースについて説明します。
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1fd848c3e0ed663e0731eb86d39c930db3af7819
ms.sourcegitcommit: d1bf26bcf0d78b37ac7598fab36eb58ca69b1dc5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2018
ms.locfileid: "37066285"
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager の Technical Preview

*適用対象: System Center Configuration Manager (Technical Preview)*

**System Center Configuration Manager Technical Preview へようこそ**。 この記事では、最新のプレビュー リリースについて詳しく説明します。プレビュー リリースには、現在開発中の新しい機能と可能性が含まれます。 Technical Preview の各バージョンでは、そのバージョンが公開された時点において Configuration Manager の Current Branch に組み込まれていない新しい機能が導入されます。 これらの機能は、最終的に現在のブランチのリリースに対する更新プログラムに組み込まれる場合がありますが、最終版として追加される前に、これらの機能をお試しいただき、フィードバックをご提供いただければと思います。  

 このリリースはテクニカル プレビューであるため、詳細や機能は変更されることがあります。  

 この記事には、Technical Preview のすべてのバージョンに適用される情報が含まれています。 また、新しい各機能 (またはフィーチャー) とそれが初めて導入された Technical Preview のバージョン (たとえば、2018 年 6 月であればバージョン 1806) がリストされます。 これらの機能の詳細は、各プレビュー バージョンに特化した個別のトピックで説明されています。  

 Configuration Manager の現在のブランチの新機能については、「[What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)」 (System Center Configuration Manager の新機能) を参照してください。



##  <a name="bkmk_reqs"></a> Technical Preview の要件と制限事項  

> [!IMPORTANT]     
>  Technical Preview はラボ環境での使用目的に限定してライセンスされます。 Microsoft はサポート サービスを提供しない場合があり、また、プレビュー ソフトウェアでは特定の機能が使用できない場合があります。 さらに、プレビュー ソフトウェアは、製品版ソフトウェアに比べて、セキュリティ、プライバシー、アクセシビリティ、可用性および信頼性の基準が低いか、または異なる場合があります。  

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

この Configuration Manager のブランチでは、次の製品とテクノロジがサポートされています。 ただし、これは製品またはバージョンの各サポート ライフサイクルが過ぎてもサポートを延長するという意味ではありません。 既にサポート ライフサイクルが終了している製品は、Configuration Manager ではサポートされません。 マイクロソフト サポート ライフサイクルの詳細については、 [「マイクロソフト サポート ライフサイクル」](https://go.microsoft.com/fwlink/p/?LinkId=208270) Web サイトを参照してください。  

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
-  **Technical Preview 1806** - Configuration Manager Technical Preview 1806 は、コンソール内更新と、新しいベースライン バージョンの両方として使用できます。 ベースライン バージョンを [TechNet Evaluation Center から](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)ダウンロードします。


##  <a name="BKMK_TPFeedback"></a> フィードバックについて  
 Technical Preview の機能に関するフィードバックをお寄せください。 詳細については、「[製品に関するフィードバック](../understand/find-help.md#product-feedback)」を参照してください。

希望する新しい機能のアイデアがありましたら、その内容もお知らせください。 新しいアイデアを提出する、または、他の人が提出したアイデアに投票するには、 [ユーザー ボイスのページにアクセス](https://configurationmanager.uservoice.com)してください。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> 最新の Technical Preview で提供される機能  
以下は、最新の Configuration Manager Technical Preview リリースで提供される機能です。 Technical Preview の以前のバージョンで利用できるようになった機能は、以降のバージョンでも利用できます。 同様に、Configuration Manager の Current Branch に追加された機能は、後続の Technical Preview でも引き続き利用できます。 特定の機能の詳細については、各プレビュー バージョンのコンテンツをクリックします。  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-18062"></a>Technical Preview バージョン 1806.2
- [段階的展開の機能強化](capabilities-in-technical-preview-1806-2.md#bkmk_pod) <!--1358577,1358147,1358578-->
- [新しい Windows アプリケーション パッケージ形式のサポート](capabilities-in-technical-preview-1806-2.md#bkmk_msix) <!--1357427-->
- [クライアント プッシュ セキュリティの機能改善](capabilities-in-technical-preview-1806-2.md#bkmk_client-push) <!--1358204-->
- [プロアクティブ メンテナンスの管理分析情報](capabilities-in-technical-preview-1806-2.md#bkmk_insights) <!--1352184,et al-->
- [共同管理されたデバイスのモバイル アプリ ワークロードの移行](capabilities-in-technical-preview-1806-2.md#bkmk_comgmt) <!--1357892-->
- [ピアのダウンロードの境界グループのオプション](capabilities-in-technical-preview-1806-2.md#bkmk_bgoptions) <!--1356193-->
- [カスタム カタログ用のサード パーティ製ソフトウェアの更新プログラムのサポート](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate) <!--1358714-->
- [クラウド管理機能の改善](capabilities-in-technical-preview-1806-2.md#bkmk_cloud) <!--511980,515854-->
- [新しいソフトウェア更新プログラムのコンプライアンス レポート](capabilities-in-technical-preview-1806-2.md#bkmk_report) <!--1357775-->



## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>サポートされている最新の Technical Preview で提供される機能
以下は、Configuration Manager Technical Preview の以前のリリースで提供され、引き続きサポートされている機能です。 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |機能 |Technical Preview バージョン |Current Branch バージョン|  
 |----------------|---------------------|--------------------|
 | サード パーティ製ソフトウェアの更新プログラム <!--1352101--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)  | ![追加されていません](media/Red_X.gif) |  
 | Microsoft Edge 用に Windows Defender SmartScreen 設定を構成する <!--1353701--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#configure-windows-defender-smartscreen-settings-for-microsoft-edge)  | ![追加されていません](media/Red_X.gif) |  
 | 共同管理されたデバイスのために MDM ポリシーを Microsoft Intune から同期する <!--1357377--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device)  | ![追加されていません](media/Red_X.gif) |  
 | 共同管理を使用して Intune に Office 365 ワークロードを移行する <!--1357841--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#transition-office-365-workload-to-intune-using-co-management)  | ![追加されていません](media/Red_X.gif) |  
 | Package Conversion Manager <!--1357861--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#package-conversion-manager)  | ![追加されていません](media/Red_X.gif) |  
 | コンテンツなしのソフトウェア更新プログラムの展開 <!--1357933--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#deploy-software-updates-without-content)  | ![追加されていません](media/Red_X.gif) |  
 | Office 365 インストーラーと Office カスタマイズ ツールの統合 <!--1358149--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#office-customization-tool-integration-with-the-office-365-installer)  | ![追加されていません](media/Red_X.gif) |  
 | クラウド管理ゲートウェイの機能改善 <!--1358215,1358651,503899--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-cloud-management-gateway)   | ![追加されていません](media/Red_X.gif) |  
 | セキュアなクライアント通信の改善 <!--1358278,1358279--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-secure-client-communications)  | ![追加されていません](media/Red_X.gif) |  
 | ソフトウェア センターのインフラストラクチャの改善 <!--1358309--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#software-center-infrastructure-improvements)  | ![追加されていません](media/Red_X.gif) |  
 | デバイス上のすべてのユーザーに対して Windows アプリ パッケージをプロビジョニングする <!--1358310--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#provision-windows-app-packages-for-all-users-on-a-device)  | ![追加されていません](media/Red_X.gif) |  
 | Surface ダッシュボードの改善 <!--1358654--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-the-surface-dashboard)  | ![追加されていません](media/Red_X.gif) |  
 | ハードウェア インベントリの既定の単位のリビジョン <!--514442--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#hardware-inventory-default-unit-revision)  | ![追加されていません](media/Red_X.gif) |  
 | タスク シーケンスに手動で構成されたフェーズを使用して段階的展開を作成する <!--1358148--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence)  | ![追加されていません](media/Red_X.gif) |  
 | Azure Resource Manager のためのクラウド配布ポイントのサポート <!--1322209--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  | ![追加されていません](media/Red_X.gif) |  
 | 管理の洞察に基づいて対策する <!--1357930--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights)  | ![追加されていません](media/Red_X.gif) |  
 | 共同管理を使用して Intune にデバイス構成ワークロードを移行する <!--1357903--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management)  | ![追加されていません](media/Red_X.gif) |  
 | ネットワークの輻そう制御を使用する配布ポイントを有効にする <!--1358112--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control)  | ![追加されていません](media/Red_X.gif) |  
 | クラウド管理ダッシュボード <!--1358461--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-management-dashboard)  | ![追加されていません](media/Red_X.gif) |  
 | CMPivot <!--1358456--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmpivot)  | ![追加されていません](media/Red_X.gif) |  
 | 改善されたセキュアなクライアント通信 <!--1356889,1358228,1358460--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)  | ![追加されていません](media/Red_X.gif) |  
 | サード パーティ製のソフトウェア更新プログラムのサポートを有効にするための機能強化 <!--1357605--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)  | ![追加されていません](media/Red_X.gif) |  
 | Windows 10 一括アップグレード タスク シーケンスの機能強化 <!--1358500--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence)  | ![追加されていません](media/Red_X.gif) |  
 | クライアントと共にインストールされる CMTrace <!--1357971--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client)  | ![追加されていません](media/Red_X.gif) |  
 | Configuration Manager コンソールの機能強化 <!--1358202--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console)  | ![追加されていません](media/Red_X.gif) |  
 | コンソール フィードバックの機能強化 <!--1357542--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback)  | ![追加されていません](media/Red_X.gif) |  
 | PXE 対応の配布ポイントの機能強化 <!--1357580--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points)  | ![追加されていません](media/Red_X.gif) |  
 | 大きな整数値でのハードウェア インベントリの機能強化 <!--1357880--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)  | ![追加されていません](media/Red_X.gif) |  
 | WSUS メンテナンスの機能強化 <!--1357898--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance)  | ![追加されていません](media/Red_X.gif) |  
 | CNG 証明書のサポートの強化 <!--1357314--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates)  | ![追加されていません](media/Red_X.gif) |  
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
 
  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>以前の Technical Preview で提供される機能
以下は、Configuration Manager Technical Preview リリースの以前のバージョンで提供された特定の機能です。 これらの機能は、以降のバージョンでも使用できますが、Current Branch リリースではまだ提供されていません。 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |機能 |Technical Preview バージョン |  
 |----------------|---------------------|
 | PXE 対応の配布ポイントの機能強化 <!-- 1357580 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | 
 | 製品ライフサイクル ダッシュボード <!--1319632 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | 
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

