---
title: "System Center Configuration Manager の Technical Preview | Microsoft Docs"
description: "System Center Configuration Manager の新機能を体験できるテクニカル プレビュー リリースについて説明します。"
ms.custom: na
ms.date: 2/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0d1f8eb9274dde96eb4295c007c0f49036d1a3de
ms.openlocfilehash: e140ef9daad9fb4105cea543115af19a4378c903
ms.lasthandoff: 02/27/2017


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

-   スタンドアロンのプライマリ サイトのみがサポートされます。 中央管理サイト、複数のプライマリ サイト、またはセカンダリ サイトはサポートされません。  

-   次のバージョンの SQL Server のみがサポートされます。  

    -   SQL Server 2016 (Service Pack なし、およびそれ以降)
    -   SQL Server 2014 (Service Pack なし、およびそれ以降)
    -   SQL Server 2012 (Service Pack 2、またはそれ以降)


-   サイトは最大 10 台のクライアントをサポートします。各クライアントは次のいずれかを実行している必要があります。  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  


-   次のインストール フラグ (スイッチ) のみがサポートされます。  

    -   **/silent**  
    -   **/testdbupgrade**  

-   当てはまる場合には、Technical Preview の特定バージョンごとの詳細情報に、追加の制限または要件が含まれています。  

-   このプレビュー ビルドへの移行、またはこのプレビュー ビルドからの移行はサポートされません。  

-   このプレビュー ビルドへのアップグレードはサポートされません。  

-   このプレビュー ビルドから、製品版 (現在のブランチ) へのアップグレードはサポートされません。 ただし、プレビュー バージョンから更新プログラムが使用できる場合は、Configuration Manager コンソールの **[更新とサービス]** ノードから検索してからインストールできます。 コンソール内アップグレード プロセスに関する「 [ConfigMgr 更新プログラム パッケージをインストールする](https://www.youtube.com/embed/KBd_EGFbUT8) 」というビデオを youtube.com でご覧ください。  

##  <a name="bkmk_install"></a> Technical Preview のインストールと更新  
 System Center Configuration Manager の Technical Preview は、System Center Configuration Manager の最新リリースとは異なります。  

 テクニカル プレビューを使用するには、テクニカル プレビュー ビルドの **ベースライン バージョン** を最初にインストールする必要があります。 ベースライン バージョンをインストールしたら、 **コンソール内更新** を使用して、最新のプレビュー バージョンでインストール環境を最新のものにできます。     通常、Technical Preview の新バージョンは毎月使用可能です。

各プレビュー リリースは、3 つの連続したリリースが使用可能になるまでサポートされます。 つまり、バージョン 1702 がリリースされると、バージョン 1610 はサポートされなくなりますが、バージョン 1611、1612、1701 は引き続きサポートされます。 ただし、最終ベースラインが (バージョン 1610 のように) サポート対象でなくなっても、そのインストールをサポートされるバージョンに更新すれば新しい Technical Preview サイトのインストールがサポートされます。

> [!TIP]  
>  Technical Preview への更新をインストールするときに、プレビュー インストール環境を対象の新しい Technical Preview バージョンに更新します。    Technical Preview インストールでは、現在のブランチ インストールにアップグレードすることも、現在のブランチ リリースから更新を受け取ることもできません。  

 **Technical Preview のアクティブ ベースライン バージョン:**  
 リリース後、最長 1 年間、ベースライン バージョンをインストールできます。

-   **Technical Preview 1610** - Configuration Manager Technical Preview 1610 は、Configuration Manager Technical Preview のコンソール内更新と、[TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) Web サイトから入手できる新しいベースライン バージョンの両方として使用できます。




##  <a name="BKMK_TPFeedback"></a> フィードバックについて  
 テクニカル プレビューに対するフィードバックをお待ちしています。 各プレビューで提供される機能に対するフィードバックを提出するには、Microsoft Connect サイトの「 [Configuration Manager フィードバック プログラム](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) 」ページでフィードバック フォームへのリンクを辿ってください。  

 また、希望する新しい機能のアイデアがありましたら、その内容もお知らせください。 新しいアイデアを提出する、または、他の人が提出したアイデアに投票するには、 [ユーザー ボイスのページにアクセス](http://configurationmanager.uservoice.com)してください。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Technical Preview で提供される機能  
 以下は、それぞれの Configuration Manager Technical Preview リリースで提供される機能です。  Technical Preview のバージョンで利用できるようになった機能は、以降のバージョンでも利用できます。 同様に、System Center Configuration Manager リリース (Current Branch) に追加された機能は、後続の Technical Preview でも引き続き利用できます。  特定の機能の詳細については、各プレビュー バージョンのコンテンツをクリックします。  

 |機能|Technical Preview バージョン|Current Branch バージョン|  
 |----------------|---------------------|--------------------|
 |iOS デバイスの新しいコンプライアンス設定|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|![追加されていません](media/Red_X.gif)|
 |S/MIME サポートを含む PFX 証明書を作成する|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|![追加されていません](media/Red_X.gif)|
 |アプリケーションをインストールする前に実行中の実行可能ファイルを確認する|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|![追加されていません](media/Red_X.gif)|
 |Configuration Manager コンソールからフィードバックを送信する | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |![追加されていません](media/Red_X.gif)  |
 |更新プログラムとサービスの変更  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |![追加されていません](media/Red_X.gif) |
 |ピア キャッシュの改善  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |![追加されていません](media/Red_X.gif)|
 |Azure Active Directory の使用  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![追加されていません](media/Red_X.gif)|
 |条件付きアクセス デバイス コンプライアンス ポリシーの改善 | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |![追加されていません](media/Red_X.gif)|
 |マルウェア対策クライアントのバージョンのアラート | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |![追加されていません](media/Red_X.gif)|
 |Windows Update for Business 更新プログラムのコンプライアンス評価 | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![追加されていません](media/Red_X.gif)|
 |ソフトウェア センターの設定と影響の大きいタスク シーケンスの通知メッセージの改善| [Tech Preview 1702](capabilities-in-technical-preview-1702.md#improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences) |![追加されていません](media/Red_X.gif)|
 |Android for Work のサポート| [Tech Preview 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |![追加されていません](media/Red_X.gif)|
 |ソフトウェア更新ポイントの境界グループの改善 | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |![追加されていません](media/Red_X.gif)  |
 |ハードウェア インベントリでの UEFI 情報の収集 | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|![追加されていません](media/Red_X.gif)  |
 |オペレーティング システムの展開に関する機能拡張| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|![追加されていません](media/Red_X.gif)  |
 |クラウドベースの配布ポイントでソフトウェアの更新をホストする| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|![追加されていません](media/Red_X.gif) |
 |管理ポイント経由でデバイス正常性構成証明データを検証する| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)|![追加されていません](media/Red_X.gif) |
 |Microsoft Azure Government クラウドの OMS コネクタ |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |![追加されていません](media/Red_X.gif) |
 |作成ウィザードで Android と iOS のバージョン指定が不要に |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |![追加されていません](media/Red_X.gif) |
 |OData エンドポイントのデータ アクセス |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![追加されていません](media/Red_X.gif)|
 |データ ウェアハウス サービス ポイント |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|![追加されていません](media/Red_X.gif)|
 |コンテンツ ライブラリのクリーンアップ ツール |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|![追加されていません](media/Red_X.gif)|
 |コンソール内検索の機能強化 |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|![追加されていません](media/Red_X.gif)|
 |指定したプログラムが実行されている場合、アプリケーションのインストールはできない|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|![追加されていません](media/Red_X.gif)|
 |エンド ユーザーを対象とした新しい Windows Hello for Business 通知|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|![追加されていません](media/Red_X.gif)|
 |Configuration Manager でのビジネス向け Windows ストアのサポート|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|![追加されていません](media/Red_X.gif)|
 |タスク シーケンスが失敗した場合に前のページに戻る|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|![追加されていません](media/Red_X.gif)|
 |Windows 10 更新プログラムに対する高速インストール ファイルのサポート|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|![追加されていません](media/Red_X.gif)|
 |Azure Active Directory のオンボーディング|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|![追加されていません](media/Red_X.gif)|
|デバイス登録のための多要素認証の構成の変更|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![追加されていません](media/Red_X.gif)|
|展開とタスク シーケンスのコンテンツの事前キャッシュ |[Tech Preview 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|![追加されていません](media/Red_X.gif)|
 |Windows Defender の構成設定|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[バージョン 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |管理者コンソールからのポリシー同期の要求|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[バージョン 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |[すべての企業所有のデバイス] ノードの追加セキュリティ ロールのサポート|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[バージョン 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Windows 10 VPN プロファイルの条件付きアクセス|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[バージョン 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |自動展開規則でコンテンツのサイズでフィルター処理する|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[バージョン 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |必要なソフトウェア ダイアログの機能向上|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[バージョン 1610](/sccm/apps/deploy-use/deploy-applications)|
 |以前に承認されたアプリケーションの要求を拒否する|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[バージョン 1610](/sccm/apps/deploy-use/deploy-applications)|
 |自動アップグレードからクライアントを除外する|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[バージョン 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Endpoint Protection の機能強化|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|![追加されていません](media/Red_X.gif)|
 |登録されるデバイス数の増加|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#increased-number-of-enrolled-devices)|![追加されていません](media/Red_X.gif)|
 |Apple DEP 設定の追加|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[バージョン 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |ビジネス向け Windows ストアと Configuration Manager のとの統合の強化|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[バージョン 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |構成アイテムの新しいコンプライアンス設定|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[バージョン 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Upgrade Analytics との統合|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[バージョン 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Windows 10 VPN ハイブリッド プロファイルのネイティブ接続の種類|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![追加されていません](media/Red_X.gif)|
 |境界グループの機能強化|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[バージョン 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Office 365 クライアント管理ダッシュボード|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[バージョン 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |クライアントに Office 365 アプリを展開する|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|![追加されていません](media/Red_X.gif)|
 |BIOS から UEFI への変換の改善|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[バージョン 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Intune 準拠チャート|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[バージョン 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |ConfigMgr クライアントのキャプチャの準備タスク シーケンス ステップの向上|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[バージョン 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |ソフトウェア センターの機能強化|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |資産インテリジェンスの改善|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![追加されていません](media/Red_X.gif)|
 |リモート コントロール キーボードの変換|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![追加されていません](media/Red_X.gif)|
 |Windows 10 のエディションのアップグレード ポリシーの改善|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[バージョン 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |ソフトウェア センター ダイアログにおけるカスタマイズ可能なブランド|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|![追加されていません](media/Red_X.gif)|  
 |オンプレミス モバイル デバイス管理のための複数のデバイス管理ポイント|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |デバイスを自動的にコレクションごとに分類|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[バージョン 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |必要なアプリケーションとソフトウェア更新プログラムを展開するための適用猶予期間|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[バージョン 1610](/sccm/apps/deploy-use/deploy-applications)|
 |デバイス ガードにより Configuration Manager を管理インストーラーとして使用|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![追加されていません](media/Red_X.gif)|
 |クラウド管理ゲートウェイ (旧クラウド プロキシ サービス)|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [バージョン 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Configuration Manager で Office 365 のクライアント エージェントを管理|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |OSDPreserveDriveLetter タスク シーケンス変数は使用されなくなった|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[バージョン 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |更新プログラムとサービス ノードの変更|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |Windows 10 デバイス向けのアプリごとの VPN|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[バージョン 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |ソフトウェア更新プログラムのインストール タスク シーケンスの向上|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |ConfigMgr クライアントのキャプチャの準備タスク シーケンス ステップの向上 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[バージョン 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |必要なアプリケーション展開の猶予期間 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![追加されていません](media/Red_X.gif)|  
 |リモート デバイスの操作の新しいエクスペリエンス |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |ビジネス向け Windows ストアのアプリ |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[バージョン 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |ボリューム購入アプリの全般的な向上|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |エンタープライズ データ保護 (EDP)|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |エンド ユーザーはポータル サイトからアプリをインストールできる |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![追加されていません](media/Red_X.gif)|  
 |ソフトウェア センターの更新プログラムおよびオペレーティング システムの新しいタブ|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[バージョン 1606 ](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |サーバー グループの提供 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[バージョン 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Windows Defender Advanced Threat Protection サービスのサポート |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[バージョン 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |Windows 10 クライアントにおけるソフトウェア更新プログラムのインストール後の新しい再起動オプション|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[バージョン 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |オンプレミスのデバイス正常性構成証明書 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[バージョン 1606](/sccm/core/servers/manage/health-attestation)|  
 |IMEI または iOS シリアル番号を持つ会社所有のデバイスの事前宣言|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[バージョン 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |ビジネス向け Windows ストアからの一括購入アプリの管理| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[バージョン 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Microsoft Passport for Work 管理の機能強化|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |クライアントが新しいソフトウェア更新ポイントに切り替えるためのオプション|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[バージョン 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |クライアント キャッシュ設定とクライアント ピア キャッシュを管理するためのクライアント設定 |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|クライアント設定: [バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>ピア キャッシュ: [バージョン 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |KSP としての Passport for Work のサポート |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[バージョン 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |オンプレミスのデバイス正常性構成証明書|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[バージョン 1606](/sccm/core/servers/manage/health-attestation)|  
 |Android デバイスの SmartLock 設定|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[バージョン 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |ソフトウェア センターの機能強化|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |リモート制御の機能強化|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |PXE 対応配布ポイント上の RamDisk TFTP ブロック サイズとウィンドウ サイズのカスタマイズ|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  


 Technical Preview リリースのすべての機能が Current Branch でサポートされる最小バージョンで使用可能になると、そのプレビュー バージョンの詳細がこのテーブルから削除されます。


## <a name="see-also"></a>関連項目  
[System Center Configuration Manager の新機能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [System Center Configuration Manager の概要](../../core/understand/introduction.md)

