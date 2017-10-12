---
title: "Configuration Manager の Technical Preview | Microsoft Docs"
description: "System Center Configuration Manager の新機能を体験できるテクニカル プレビュー リリースについて説明します。"
ms.custom: na
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: "157"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 429e20185bd23519f78c37ded39f2638d0c80ced
ms.sourcegitcommit: 8ac9c2c9ba1fdcbb7cc8d5be898586865fcf67c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2017
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager の Technical Preview

*適用対象: System Center Configuration Manager (Technical Preview)*

**System Center Configuration Manager Technical Preview へようこそ**。 このトピックでは、最新のプレビュー リリースについて詳しく説明します。プレビュー リリースには、現在開発中の新しい機能と可能性が含まれます。 Technical Preview の各バージョンでは、そのバージョンが公開された時点において System Center Configuration Manager のブランチに組み込まれていない新しい機能が導入されます。 これらの機能は、最終的に現在のブランチのリリースに対する更新プログラムに組み込まれる場合がありますが、最終版として追加される前に、これらの機能をお試しいただき、フィードバックをご提供いただければと思います。  

 これはテクニカル プレビューであるため、詳細や機能は変更されることがあります。  

 このトピックでは、Technical Preview のすべてのバージョンに適用される情報を説明し、さらに、新しい機能 (またはフィーチャー) とそれが初めて導入された Technical Preview のバージョン (たとえば、2017 年 1 月であればバージョン 1701) を一覧に示します。 これらの機能の詳細は、各プレビュー バージョンに特化した個別のトピックで説明されています。  

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


-   既定では、Technical Preview を使用する場合、インストール時はサービス接続ポイントがオンライン モードに設定されており、オフライン モードへの変更はサポートされていません。

-   当てはまる場合には、Technical Preview の特定バージョンごとの詳細情報に、追加の制限または要件が含まれています。  

-   このプレビュー ビルドへの移行、またはこのプレビュー ビルドからの移行はサポートされません。  

-   このプレビュー ビルドへのアップグレードはサポートされません。  

-   このプレビュー ビルドから、製品版 (現在のブランチ) へのアップグレードはサポートされません。 ただし、プレビュー バージョンから更新プログラムが使用できる場合は、Configuration Manager コンソールの **[更新とサービス]** ノードから検索してからインストールできます。 コンソール内アップグレード プロセスに関する「 [ConfigMgr 更新プログラム パッケージをインストールする](https://www.youtube.com/embed/KBd_EGFbUT8) 」というビデオを youtube.com でご覧ください。  
-   スタンドアロンのプライマリ サイトのみがサポートされます。 中央管理サイト、複数のプライマリ サイト、またはセカンダリ サイトはサポートされません。  

この Configuration Manager のブランチでは、次の製品とテクノロジがサポートされています。 ただし、これは製品またはバージョンの各サポート ライフサイクルが過ぎてもサポートを延長するという意味ではありません。 既にサポート ライフサイクルが終了している製品は、Configuration Manager ではサポートされません。 マイクロソフト サポート ライフサイクルの詳細については、 [「マイクロソフト サポート ライフサイクル」](http://go.microsoft.com/fwlink/p/?LinkId=208270) Web サイトを参照してください。  

-   次のバージョンの SQL Server のみがサポートされます。  

    -   SQL Server 2016 (Service Pack なし、およびそれ以降)
    -   SQL Server 2014 (Service Pack 1 以降)
    -   SQL Server 2012 (Service Pack 3 以降)


-   サイトは最大 10 台のクライアントをサポートします。各クライアントは次のいずれかを実行している必要があります。  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> Technical Preview のインストールと更新  
 System Center Configuration Manager の Technical Preview は、System Center Configuration Manager の最新リリースとは異なります。  

 テクニカル プレビューを使用するには、テクニカル プレビュー ビルドの **ベースライン バージョン** を最初にインストールする必要があります。 ベースライン バージョンをインストールしたら、 **コンソール内更新** を使用して、最新のプレビュー バージョンでインストール環境を最新のものにできます。     通常、Technical Preview の新バージョンは毎月使用可能です。

各プレビュー リリースは、3 つの連続したリリースが使用可能になるまでサポートされます。 つまり、バージョン 1708 がリリースされると、バージョン 1704 はサポートされなくなりますが、バージョン 1705、1706、1707 は引き続きサポートされます。 ベースラインが (バージョン 1703 のように) サポート対象でなくなっても、そのインストールをサポートされるバージョンに更新すれば、(新しいベースライン バージョンが使用できるようになるまでは) 新しい Technical Preview サイトのインストールがサポートされます。 更新時に利用可能な最新バージョンがコンソールに表示されない場合、提供されている最新のバージョンに更新した後、最新バージョンのテクニカル プレビューをインストールできるようになるまでそのプロセスを繰り返します。

> [!TIP]  
>  Technical Preview への更新をインストールするときに、プレビュー インストール環境を対象の新しい Technical Preview バージョンに更新します。    Technical Preview インストールでは、現在のブランチ インストールにアップグレードすることも、現在のブランチ リリースから更新を受け取ることもできません。  

**Technical Preview のアクティブ ベースライン バージョン:**  
リリース後、最長 1 年間、ベースライン バージョンをインストールできます。 ただし、新しい Technical Preview サイトをインストールする場合は、利用可能な最新のベースライン バージョンを使用することをお勧めします。
-  **Technical Preview 1703** - Configuration Manager Technical Preview 1703 は、Configuration Manager Technical Preview のコンソール内更新と、[TechNet Evaluation Center Web サイトから入手できる](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)新しいベースライン バージョンの両方として使用できます。

<!-- out of support. Use baseline 1703
-  **Technical Preview 1610** - The Configuration Manager Technical Preview 1610 was available as both an in-console update for the Configuration Manager Technical Preview, and as a baseline version. If you have media for installing 1610, we recommend you download version 1703 and install that version instead.
-->



##  <a name="BKMK_TPFeedback"></a> フィードバックについて  
 テクニカル プレビューに対するフィードバックをお待ちしています。 各プレビューで提供される機能に対するフィードバックを提出するには、Microsoft Connect サイトの「 [Configuration Manager フィードバック プログラム](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) 」ページでフィードバック フォームへのリンクを辿ってください。  

 また、希望する新しい機能のアイデアがありましたら、その内容もお知らせください。 新しいアイデアを提出する、または、他の人が提出したアイデアに投票するには、 [ユーザー ボイスのページにアクセス](http://configurationmanager.uservoice.com)してください。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> 最新の Technical Preview で提供される機能  
 以下は、それぞれの Configuration Manager Technical Preview リリースで提供される機能です。  Technical Preview のバージョンで利用できるようになった機能は、以降のバージョンでも利用できます。 同様に、System Center Configuration Manager リリース (Current Branch) に追加された機能は、後続の Technical Preview でも引き続き利用できます。  特定の機能の詳細については、各プレビュー バージョンのコンテンツをクリックします。  

 |機能 |Technical Preview バージョン |Current Branch バージョン|  
 |----------------|---------------------|--------------------|
 |Configuration Manager コンソールの向上した VPN プロファイル エクスペリエンス <!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |![追加されていません](media/Red_X.gif)    |
 |Windows 10 デバイスの共同管理|[Tech Preview 1709](capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices)|![追加されていません](media/Red_X.gif)    |


## <a name="capabilities-delivered-in-previous-technical-previews"></a>以前の Technical Preview で提供される機能
 Technical Preview リリースのすべての機能が Current Branch でサポートされる最小バージョンで使用可能になると、そのプレビュー バージョンの詳細は次の表から削除されます。  

 |機能 |Technical Preview バージョン |Current Branch バージョン|  
 |----------------|---------------------|--------------------|
 |Configuration Manager から PowerShell スクリプトを展開するときのスクリプト パラメーターの指定を改善 <!-- 1236459 -->|[Tech Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|![追加されていません](media/Red_X.gif)|
 |管理分析情報 <!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|![追加されていません](media/Red_X.gif)|
 |Configuration Manager コンソールからコンピューターを再起動 <!-- 1356283 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console)|![追加されていません](media/Red_X.gif)|
 |ソフトウェア センターのカスタマイズ <!-- 1351224 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#software-center-customization)|![追加されていません](media/Red_X.gif)|
|クライアント ピア キャッシュで、Windows 10 と Office 365 の高速インストール ファイルに対応|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365)|![追加されていません](media/Red_X.gif)|
 |Surface デバイス ダッシュボード|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|![追加されていません](media/Red_X.gif)|
 |Windows Defender Application Guard ポリシーの構成と展開|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#configure-and-deploy-windows-defender-application-guard-policies)|![追加されていません](media/Red_X.gif)|
 |Configuration Manager から PowerShell スクリプトを展開するときにパラメーターを追加する|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|![追加されていません](media/Red_X.gif)|
 |新しいモバイル アプリケーション管理ポリシーの設定|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-mobile-application-management-policy-settings)|![追加されていません](media/Red_X.gif)|
 |ソフトウェアの更新ポイントのための境界グループの改善|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#improved-boundary-groups-for-software-update-points)|[バージョン 1706](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)|
 |サイト サーバーの役割の高可用性|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |![追加されていません](media/Red_X.gif)|
 |Device Guard ポリシーに特定のファイルとフォルダーの信頼を含める|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#include-trust-for-specific-files-and-folders-in-a-device-guard-policy)|[バージョン 1706](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|
 |タスク シーケンスの進行状況の非表示|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#hide-task-sequence-progress)|![追加されていません](media/Red_X.gif)|
 |コンテンツのインストールとコンテンツのアンインストール用に別のコンテンツの場所を指定する|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#specify-a-different-content-location-for-install-content-and-uninstall-content)|[バージョン 1706](/sccm/core/get-started/capabilities-in-technical-preview-1706#hide-task-sequence-progress)|
 |ユーザー補助の機能強化 |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#accessibility-improvements)|[バージョン 1706](/sccm/core/understand/accessibility-features)|
 |Azure サービス ウィザードでの Upgrade Readiness のサポート |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#changes-to-the-azure-services-wizard-to-support-upgrade-readiness)|[バージョン 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |クラウド サービスの新しいクライアント設定|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-client-settings-for-cloud-services)|[バージョン 1706](/sccm/core/clients/deploy/deploy-clients-cmg-azure)|
 |Configuration Manager コンソールから PowerShell スクリプトを作成して実行する|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)|[バージョン 1706](/sccm/apps/deploy-use/create-deploy-scripts)|
 |PXE ネットワーク ブートでの IPv6 のサポート |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|![追加されていません](media/Red_X.gif)|
 |Microsoft Surface ドライバーの更新プログラムの管理 |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#manage-microsoft-surface-driver-updates)|[バージョン 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#manage-microsoft-surface-driver-updates)|
 |Windows Update for Business 遅延ポリシーの構成 |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#configure-windows-update-for-business-deferral-policies)|[バージョン 1706](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)|
 |iOS の登録制限|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|[バージョン 1706](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions)|
 |Android の登録制限|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|[バージョン 1706](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)|
 |コピー/貼り付け用の Android for Work アプリケーション管理ポリシー|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-for-work-application-management-policy-for-copy-paste)|[バージョン 1706](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client#android-for-work-configuration-item-settings-reference)|
 |新しい Windows 構成アイテムの設定|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-windows-configuration-item-settings)|[バージョン 1706](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |新しいデバイス コンプライアンス ポリシー ルール|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-device-compliance-policy-rules)|[バージョン 1706](/sccm/mdm/deploy-use/create-compliance-policy)|
 |条件付きアクセスのコンプライアンス ポリシーに対するデバイス正常性構成証明の評価|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|![追加されていません](media/Red_X.gif)|
 |Entrust 証明機関のサポート|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#support-for-entrust-certification-authorities)|[バージョン 1706](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |macOS VPN プロファイルの Cisco (IPsec) のサポート|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#cisco-ipsec-support-for-macos-vpn-profiles)|[バージョン 1706](/sccm/protect/deploy-use/vpn-profiles)|
 |Azure AD の新機能とクラウド管理|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management)|[バージョン 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#azure-ad-integration-with-configuration-manager)|
 |Windows Defender Application Guard ポリシーの構成と展開|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#configure-and-deploy-windows-defender-application-guard-policies)|![追加されていません](media/Red_X.gif)|
 |更新のリセット ツール  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#update-reset-tool)|[バージョン 1706](/sccm/core/servers/manage/update-reset-tool)|
 |高 DPI コンソールのサポート  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#high-dpi-console-support)|[バージョン 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#high-dpi-console-support)|
 |ピア キャッシュの改善  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#peer-cache-improvements) |[バージョン 1706](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache)|
 |SQL Server Always On 可用性グループの機能強化 |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#improvements-for-sql-server-always-on-availability-groups) |[バージョン 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#improvements-for-sql-server-always-on-availability-groups)|
 |Office 365 更新プログラムのユーザーへの通知の改善|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#improved-user-notifications-for-office-365-updates) |[バージョン 1706](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates)|
 |Azure サービス ウィザードを使用して、OMS への接続を構成する|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) |[バージョン 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |アプリ構成ポリシーを使用した Android アプリの構成  |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#configure-android-apps-with-app-configuration-policies)|![追加されていません](media/Red_X.gif)|
 |ハードウェア インベントリでのセキュア ブート情報の収集 |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#hardware-inventory-collects-secure-boot-information)|[バージョン 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#hardware-inventory-collects-secure-boot-information)|
 |子タスク シーケンスをタスク シーケンスに追加する|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#add-child-task-sequences-to-a-task-sequence)|![追加されていません](media/Red_X.gif)|
 |最新バージョンの Windows PE を使用してブート イメージを再読み込みする |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#reload-boot-images-with-current-windows-pe-version)|[バージョン 1706](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image)|
 |オペレーティング システムの展開に関する機能拡張<!-- This item does not track to be added to the Current Branch. It is covered by various other incremental work. --> |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#improvements-to-operating-system-deployment)|![追加されていません](media/Red_X.gif)|
 |ボリューム購入 iOS アプリをデバイス コレクションに展開する|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[バージョン 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |ソフトウェア センターでのアプリケーションへの直接リンク|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|[バージョン 1706](/sccm/apps/deploy-use/share-applications)
 |Configuration Manager の Windows クライアント コンピューター用の PFX 証明書|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|[バージョン 1706](/sccm/protect/deploy-use/create-certificate-profiles)|
 |Azure サービスの構成ウィザード|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|[バージョン 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |オペレーティング システムのアップグレード タスク シーケンスでの BIOS から UEFI への変換| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[バージョン 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |折りたたみ可能なタスク シーケンス グループ| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |[バージョン 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#collapsible-task-sequence-groups)|
 |Windows Analytics for Upgrade Readiness を構成するためのクライアント設定 | [Tech Preview 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |[バージョン 1706](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics)|
 |iOS デバイスの新しいコンプライアンス設定|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[バージョン 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |S/MIME サポートを含む PFX 証明書を作成する|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[バージョン 1706](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |アプリケーションをインストールする前に実行中の実行可能ファイルを確認する|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[バージョン 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Configuration Manager コンソールからフィードバックを送信する | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[バージョン 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |更新プログラムとサービスの変更  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[バージョン 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |ピア キャッシュの改善  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[バージョン 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |Azure Active Directory の使用 <!-- This item does not track to be added to the Current Branch. It is covered by various other incremental work. --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![追加されていません](media/Red_X.gif)|
 |条件付きアクセス デバイス コンプライアンス ポリシーの改善 | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[バージョン 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |マルウェア対策クライアントのバージョンのアラート | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[バージョン 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Windows Update for Business 更新プログラムのコンプライアンス評価 | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![追加されていません](media/Red_X.gif)|
 |ソフトウェア センターの設定と影響の大きいタスク シーケンスの通知メッセージの改善|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[バージョン 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Android for Work のサポート| [Tech Preview 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[バージョン 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |ソフトウェア更新ポイントの境界グループの改善 | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[バージョン 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |ハードウェア インベントリでの UEFI 情報の収集 | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[バージョン 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |オペレーティング システムの展開に関する機能拡張| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[バージョン 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |クラウドベースの配布ポイントでソフトウェアの更新をホストする| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|[バージョン 1702](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#plan-to-use-a-cloud-based-distribution-point) |
 |管理ポイント経由でデバイス正常性構成証明データを検証する| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [バージョン 1702](/sccm/core/servers/manage/health-attestation) |
 |Microsoft Azure Government クラウドの OMS コネクタ |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[バージョン 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |作成ウィザードで Android と iOS のバージョン指定が不要に |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |[バージョン 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |
 |OData エンドポイントのデータ アクセス |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![追加されていません](media/Red_X.gif)|
 |データ ウェアハウス サービス ポイント |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[バージョン 1702](/sccm/core/servers/manage/data-warehouse)|
 |コンテンツ ライブラリのクリーンアップ ツール |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[バージョン 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |コンソール内検索の機能強化 |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[バージョン 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |指定したプログラムが実行されている場合、アプリケーションのインストールはできない|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[バージョン 1702](/sccm/apps/deploy-use/deploy-applications)|
 |エンド ユーザーを対象とした新しい Windows Hello for Business 通知|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|[バージョン 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#new-windows-hello-for-business-notification-for-end-users)|
 |Configuration Manager でのビジネス向け Windows ストアのサポート|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|[バージョン 1702](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |タスク シーケンスが失敗した場合に前のページに戻る|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[バージョン 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Windows 10 更新プログラムに対する高速インストール ファイルのサポート|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[バージョン 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Azure Active Directory のオンボーディング|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|[バージョン 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |デバイス登録のための多要素認証の構成の変更|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![追加されていません](media/Red_X.gif)|
 |展開とタスク シーケンスのコンテンツの事前キャッシュ |[Tech Preview 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|[バージョン 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
 |Windows Defender の構成設定|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[バージョン 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |管理者コンソールからのポリシー同期の要求|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[バージョン 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |[すべての企業所有のデバイス] ノードの追加セキュリティ ロールのサポート|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[バージョン 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Windows 10 VPN プロファイルの条件付きアクセス|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[バージョン 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |自動展開規則でコンテンツのサイズでフィルター処理する|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[バージョン 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |必要なソフトウェア ダイアログの機能向上|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[バージョン 1610](/sccm/apps/deploy-use/deploy-applications)|
 |以前に承認されたアプリケーションの要求を拒否する|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[バージョン 1610](/sccm/apps/deploy-use/deploy-applications)|
 |自動アップグレードからクライアントを除外する|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[バージョン 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Endpoint Protection の機能強化|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|[バージョン 1610](/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)|
 |登録されるデバイス数の増加|[Tech Preview 1609](/sccm/mdm/deploy-use/enable-platform-enrollment)|[バージョン 1610](/sccm/mdm/deploy-use/enable-platform-enrollment)|
 |Apple DEP 設定の追加|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[バージョン 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |ビジネス向け Windows ストアと Configuration Manager のとの統合の強化|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[バージョン 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |構成アイテムの新しいコンプライアンス設定|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[バージョン 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Upgrade Analytics との統合|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[バージョン 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Windows 10 VPN ハイブリッド プロファイルのネイティブ接続の種類|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![追加されていません](media/Red_X.gif)|
 |境界グループの機能強化|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[バージョン 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Office 365 クライアント管理ダッシュボード|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[バージョン 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |クライアントに Office 365 アプリを展開する|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|[バージョン 1702](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)|
 |BIOS から UEFI への変換の改善|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[バージョン 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Intune 準拠チャート|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[バージョン 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|


 <!--  TP 1608 and earlier have aged out of support. Features from these previews are either in the minimum supported Current Branch version, or are not scheduled for inclusion.
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Improvements to Software Center|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Improvements to Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|N/A|
 |Remote control keyboard translation|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|[Version 1702](/sccm/core/clients/manage/remote-control/configuring-remote-control#enable-keyboard-translation)|
 |Improvements to the Windows 10 Edition Upgrade Policy|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Version 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Customizable Branding for Software Center Dialogs|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#customizable-branding-for-software-center-dialogs)|  
 |Multiple device management points for On-premises Mobile Device Management|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Automatically categorize devices into collections|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Version 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Enforcement grace period for required application and software update deployments|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Using Configuration Manager as a Managed Installer with Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|[Version 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|
 |Cloud management gateway (formerly Cloud Proxy Service)|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Manage the Office 365 client agent in Configuration Manager|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |The OSDPreserveDriveLetter task sequence variable has been deprecated|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Version 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Changes for the Updates and Servicing Node|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |Per-app VPN for Windows 10 devices|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Version 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Improvements to the Install software updates task sequence|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |Grace period for required application deployments |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|N/A|  
 |New experience for remote device actions |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Windows Store for Business apps |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |General improvements for volume-purchased apps|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Enterprise Data Protection (EDP)|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |End users can install apps from the Company Portal |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|N/A|  
 |New tabs for Updates and Operating Systems in Software Center|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Version 1606 ](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Service a server group |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Version 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Support for Windows Defender Advanced Threat Protection service |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Version 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |New restart options for Windows 10 clients after software update installation|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |On-premises Device Health Attestation |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |Pre-declare corporate-owned devices with IMEI or iOS serial number|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Version 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |Manage volume-purchased apps from the Windows Store for Business| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Improvements to Microsoft Passport for Work management|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Option for clients to switch to a new software update point|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Client settings to manage Client Cache Settings and client Peer Cache |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|Client Settings: [Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>Peer Cache: [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |Support for Passport for Work as a KSP |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Version 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |On-premises Device Health Attestation|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |SmartLock setting for Android devices|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Version 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |Improvements to Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Improvements to remote control|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
-->



## <a name="see-also"></a>関連項目  
[System Center Configuration Manager の新機能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [System Center Configuration Manager の概要](../../core/understand/introduction.md)
