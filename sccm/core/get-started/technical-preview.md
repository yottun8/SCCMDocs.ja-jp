---
title: "Technical Preview リリース"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager の新機能を体験できるテクニカル プレビュー リリースについて説明します。"
ms.custom: na
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 975bd66bb86efb133ccd7017295e8108558f633d
ms.sourcegitcommit: db9978135d7a6455d83dbe4a5175af2bdeaeafd8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager の Technical Preview

*適用対象: System Center Configuration Manager (Technical Preview)*

**System Center Configuration Manager Technical Preview へようこそ**。 この記事では、最新のプレビュー リリースについて詳しく説明します。プレビュー リリースには、現在開発中の新しい機能と可能性が含まれます。 Technical Preview の各バージョンでは、そのバージョンが公開された時点において Configuration Manager の Current Branch に組み込まれていない新しい機能が導入されます。 これらの機能は、最終的に現在のブランチのリリースに対する更新プログラムに組み込まれる場合がありますが、最終版として追加される前に、これらの機能をお試しいただき、フィードバックをご提供いただければと思います。  

 このリリースはテクニカル プレビューであるため、詳細や機能は変更されることがあります。  

 この記事には、Technical Preview のすべてのバージョンに適用される情報が含まれています。 さらに、新しい機能 (またはフィーチャー) とそれが初めて導入された Technical Preview のバージョン (たとえば、2018 年 1 月であればバージョン 1801) を一覧に示します。 これらの機能の詳細は、各プレビュー バージョンに特化した個別のトピックで説明されています。  

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
>  Technical Preview への更新をインストールするときに、プレビュー インストール環境を対象の新しい Technical Preview バージョンに更新します。    Technical Preview インストールでは、現在のブランチ インストールにアップグレードすることも、現在のブランチ リリースから更新を受け取ることもできません。  

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

### <a name="technical-preview-version-1801"></a>Technical Preview バージョン 1801
- [段階的展開の作成](capabilities-in-technical-preview-1801.md#create-phased-deployments) <!-- 1357405 --> 
- [共同管理レポート](capabilities-in-technical-preview-1801.md#co-management-reporting) <!-- 1356648 --> 
- [自動展開規則の評価スケジュールの機能拡張](capabilities-in-technical-preview-1801.md#improvements-to-automatic-deployment-rule-evaluation-schedule) <!-- 1357133 --> 
- [配布ポイントの再割り当て](capabilities-in-technical-preview-1801.md#reassign-distribution-point) <!-- 1306937 --> 
- [ハードウェア インベントリの機能拡張](capabilities-in-technical-preview-1801.md#improvements-to-hardware-inventory) <!-- 1357389 --> 
- [ソフトウェア センターのクライアント設定の機能拡張](capabilities-in-technical-preview-1801.md#improvements-to-client-settings-for-software-center) <!-- 1355146 --> 
- [Windows Defender Application Guard の新しい設定](capabilities-in-technical-preview-1801.md#new-settings-for-windows-defender-application-guard) <!-- 1356256 --> 
- [スクリプトの実行の改善](capabilities-in-technical-preview-1801.md#improvements-to-run-scripts) <!-- 1236459 --> 




## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>サポートされている最新の Technical Preview で提供される機能
以下は、Configuration Manager Technical Preview の以前のリリースで提供され、引き続きサポートされている機能です。 

<!-- This is the full list of new features in the past three TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |機能 |Technical Preview バージョン |Current Branch バージョン|  
 |----------------|---------------------|--------------------|
 |置き換えられたアプリケーションを自動的にアップグレードしない <!-- 1351266 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#do-not-automatically-upgrade-superseded-applications)  |![追加されていません](media/Red_X.gif)    | 
 |ソフトウェア センターで複数のアプリケーションをインストールする <!-- 1357126 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#install-multiple-applications-in-software-center)  |![追加されていません](media/Red_X.gif)    |
 |Configuration Manager クライアント インストールにおける変更 <!-- 1356195 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-in-the-configuration-manager-client-install)  |![追加されていません](media/Red_X.gif)    | 
 |Surface デバイス ダッシュボードに対する変更 <!-- 1355788 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-to-the-surface-device-dashboard)  |![追加されていません](media/Red_X.gif)    | 
 |Office 365 クライアント管理ダッシュボードの機能拡張 <!-- 1357281 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-office-365-client-management-dashboard)  |![追加されていません](media/Red_X.gif)    | 
 |Configuration Manager コンソールの機能拡張 <!-- 1357280,1357282 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-the-configuration-manager-console)  |![追加されていません](media/Red_X.gif)    | 
 |オペレーティング システムの展開に関する機能拡張 <!-- SMS 500897 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-operating-system-deployment)  |![追加されていません](media/Red_X.gif)    | 
 |タスク シーケンス ステップの実行<!-- 1261338 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |[バージョン 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence)    |
 |アプリケーションをインストールするときに、ユーザー操作を許可する <!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |![追加されていません](media/Red_X.gif)    |
 |Windows Analytics デバイスの正常性に関する Windows 10 のテレメトリ<!--1356148 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health) |[バージョン 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#reporting)    |
 |ソフトウェア センター アイコンの機能強化<!-- 1356194 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#software-center-no-longer-distorts-icons-larger-than-250x250) |[バージョン 1710](/sccm/apps/plan-design/plan-for-and-configure-application-management#supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center)    |
 |ソフトウェア センターから共同管理対象デバイスのコンプライアンスを確認する<!-- 1356374 -->|[Tech Preview 1710](capabilities-in-technical-preview-1710.md#check-compliance-from-software-center-for-co-managed-devices)|[バージョン 1710](/sccm/core/clients/manage/co-management-overview)    |
 |CNG 証明書の制限付きサポート<!-- 1356191 -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md#limited-support-for-cng-certificates)|[バージョン 1710](/sccm/core/plan-design/network/cng-certificates-overview)    |
 |Exploit Guard のサポート<!--1355468 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#support-for-exploit-guard) |[バージョン 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)    |
 |再起動を待機しているコンピューターに関する説明を改善   <!-- 1356283  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[バージョン 1710](/sccm/core/clients/manage/manage-clients)    |
 |Device Guard ポリシーの変更<!-- 1355092  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[バージョン 1710](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)    |
 |Windows Defender Application Guard ポリシーの構成と展開<!-- 1351960  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[バージョン 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)    |
 |Configuration Manager から PowerShell スクリプトを展開するための機能強化 <!-- 1236459 -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md#improvements-for-deploying-powershell-scripts-from-configuration-manager) | [バージョン 1710](/sccm/apps/deploy-use/create-deploy-scripts)
 

## <a name="capabilities-delivered-in-previous-technical-previews"></a>以前の Technical Preview で提供される機能
以下は、Configuration Manager Technical Preview リリースの以前のバージョンで提供された特定の機能です。 これらの機能は、以降のバージョンでも使用できますが、Current Branch リリースではまだ提供されていません。 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |機能 |Technical Preview バージョン |  
 |----------------|---------------------|
 |Configuration Manager コンソールの向上した VPN プロファイル エクスペリエンス <!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |
 |管理分析情報 <!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|
 |Surface デバイス ダッシュボード<!-- 1355788 --> |[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|
 |サイト サーバーの役割の高可用性<!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |PXE ネットワーク ブートでの IPv6 のサポート<!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |条件付きアクセスのコンプライアンス ポリシーに対するデバイス正常性構成証明の評価<!-- 1235616 -->|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|
 |Azure Active Directory の使用 <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Windows Update for Business 更新プログラムのコンプライアンス評価<!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |OData エンドポイントのデータ アクセス<!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |資産インテリジェンスの改善 <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |エンド ユーザーはポータル サイトからアプリをインストールできる<!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>関連項目  
[System Center Configuration Manager の新機能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [System Center Configuration Manager の概要](../../core/understand/introduction.md)
