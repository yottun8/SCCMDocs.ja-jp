---
title: "System Center Configuration Manager の Technical Preview"
description: "System Center Configuration Manager の新機能を体験できるテクニカル プレビュー リリースについて説明します。"
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 39a9cde3bd955c84f301d25258b413fecaa4393b
ms.openlocfilehash: 2aa78c20c919d04401f663063860df06c5262048


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager の Technical Preview

*適用対象: System Center Configuration Manager (Technical Preview)*

**System Center Configuration Manager Technical Preview へようこそ**。 このトピックでは、最新のプレビュー リリースについて詳しく説明します。プレビュー リリースには、現在開発中の新しい機能と可能性が含まれます。 Technical Preview の各バージョンでは、そのバージョンが公開された時点において System Center Configuration Manager のブランチに組み込まれていない新しい機能が導入されます。 これらの機能は、最終的に現在のブランチのリリースに対する更新プログラムに組み込まれる場合がありますが、最終版として追加される前に、これらの機能をお試しいただき、フィードバックをご提供いただければと思います。  

 これはテクニカル プレビューであるため、詳細や機能は変更されることがあります。  

 このトピックでは、Technical Preview のすべてのバージョンに適用される情報を説明し、さらに、新しい機能 (またはフィーチャー) とそれが初めて導入された Technical Preview のバージョン (たとえば、2015 年 12 月であればバージョン 1512) を一覧に示します。 これらの機能の詳細は、各プレビュー バージョンに特化した個別のトピックで説明されています。  

 Configuration Manager の現在のブランチの新機能については、「[What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)」 (System Center Configuration Manager の新機能) を参照してください。



##  <a name="a-namebkmkreqsa-requirements-and-limitations-for-the-technical-preview"></a><a name="bkmk_reqs"></a> Technical Preview の要件と制限事項  

> [!IMPORTANT]  
>  Technical Preview はラボ環境での使用目的に限定してライセンスされます。  Microsoft はサポート サービスを提供しない場合があり、また、プレビュー ソフトウェアでは特定の機能が使用できない場合があります。 さらに、プレビュー ソフトウェアは、製品版ソフトウェアに比べて、セキュリティ、プライバシー、アクセシビリティ、可用性および信頼性の基準が低いか、または異なる場合があります。  

 ほとんどの製品の前提条件については、「[Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)」 (System Center Configuration Manager でサポートされる構成) を参照してください。 次の例外がテクニカル プレビュー リリースに適用されます。  

-   各インストールは 90 日後に使用期限が切れるまでアクティブです。  

-   サポートされる言語は英語のみです。  

-   スタンドアロンのプライマリ サイトのみがサポートされます。 中央管理サイト、複数のプライマリ サイト、またはセカンダリ サイトはサポートされません。  

-   次のバージョンの SQL Server のみがサポートされます。  

    -   累積的な更新プログラム 2 以降が適用された SQL Server 2012  

    -   SQL Server 2014  

-   サイトは最大 10 台のクライアントをサポートします。各クライアントは次のいずれかを実行している必要があります。  

    -   Windows 7  

    -   Windows 8  

    -   Windows 8.1  

    -   Windows 10  

-   次のインストール フラグ (スイッチ) のみがサポートされます。  

    -   **/silent**  

    -   **/testdbupgrade**  

-   当てはまる場合には、Technical Preview の特定バージョンごとの詳細情報に、追加の制限または要件が含まれています。  

-   このプレビュー ビルドへの移行、またはこのプレビュー ビルドからの移行はサポートされません。  

-   このプレビュー ビルドへのアップグレードはサポートされません。  

-   このプレビュー ビルドから、製品版 (現在のブランチ) へのアップグレードはサポートされません。 ただし、プレビュー バージョンから更新プログラムが使用できる場合は、Configuration Manager コンソールの **[更新とサービス]** ノードから検索してからインストールできます。 コンソール内アップグレード プロセスに関する「 [ConfigMgr 更新プログラム パッケージをインストールする](https://www.youtube.com/embed/KBd_EGFbUT8) 」というビデオを youtube.com でご覧ください。  

##  <a name="a-namebkmkinstalla-install-and-update-the-technical-preview"></a><a name="bkmk_install"></a> Technical Preview のインストールと更新  
 System Center Configuration Manager の Technical Preview は、System Center Configuration Manager の最新リリースとは異なります。  

 テクニカル プレビューを使用するには、テクニカル プレビュー ビルドの **ベースライン バージョン** を最初にインストールする必要があります。 ベースライン バージョンをインストールしたら、 **コンソール内更新** を使用して、最新のプレビュー バージョンでインストール環境を最新のものにできます。     通常、Technical Preview の新バージョンは毎月使用可能です。  

> [!TIP]  
>  Technical Preview への更新をインストールするときに、プレビュー インストール環境を対象の新しい Technical Preview バージョンに更新します。    Technical Preview インストールでは、現在のブランチ インストールにアップグレードすることも、現在のブランチ リリースから更新を受け取ることもできません。  

 **Technical Preview のアクティブ ベースライン バージョン:**  
 リリース後、最長 1 年間、ベースライン バージョンをインストールできます。

-   **Technical Preview 1610** - Configuration Manager Technical Preview 1610 は、Configuration Manager Technical Preview のコンソール内更新と、[TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) Web サイトから入手できる新しいベースライン バージョンの両方として使用できます。

-   **System Center Technical Preview 5** の一部としての **Technical Preview 1603** - Configuration Manager Technical Preview 1603 は、Configuration Manager Technical Preview のコンソール内更新と、System Center Technical Preview 5 に含まれている新しいベースライン バージョンの両方として使用できます。    ベースライン インストールには、System Center Technical Preview 5 に含まれているバージョンのみを使用できます。  

     [System Center Technical Preview 5 からの Configuration Manager Technical Preview](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) のベースライン バージョンの概要:  

    -   セットアップと Configuration Manager コンソールの両方は、System Center Configuration Manager Technical Preview 1603 としてバージョンが表示されます。  

    -   このベースライン バージョンは、コンソール内更新のサポートなど、Configuration Manager Technical Preview 1603 と同様に機能します。  


##  <a name="a-namebkmktpfeedbacka-providing-feedback"></a><a name="BKMK_TPFeedback"></a> フィードバックについて  
 テクニカル プレビューに対するフィードバックをお待ちしています。 各プレビューで提供される機能に対するフィードバックを提出するには、Microsoft Connect サイトの「 [Configuration Manager フィードバック プログラム](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) 」ページでフィードバック フォームへのリンクを辿ってください。  

 また、希望する新しい機能のアイデアがありましたら、その内容もお知らせください。 新しいアイデアを提出する、または、他の人が提出したアイデアに投票するには、 [ユーザー ボイスのページにアクセス](http://configurationmanager.uservoice.com)してください。  

##  <a name="a-namebdmktpknownissuesa-general-changes-introduced-in-technical-previews"></a><a name="bdmk_tpknownissues"></a> Technical Preview に導入された一般的な変更  

-   **Technical Preview 1603:**  

    -   Technical Preview 1603 以降では、クライアントがソフトウェア更新プログラムのインストールと再起動の直後に、ソフトウェア更新プログラムのコンプライアンス対応スキャンを実行するように、ソフトウェア更新プログラムの展開を構成できます。 これにより、クライアントは、クライアントの再起動後に適用可能になる追加のソフトウェア更新プログラムをチェックして、同じメンテナンス期間中にそれらをインストール (およびコンプライアンスに準拠) できます。  

         展開に対してこれを構成するには、ソフトウェア更新プログラムの展開ウィザードの **[ユーザー エクスペリエンス]** ページで、オプション **[この展開の更新プログラムでシステムの再起動が必要な場合は、再起動後に更新プログラムの展開評価サイクルを実行する]**をオンにします。  

    -   Technical Preview 1603 以降では、SMSTSRebootDelay タスク シーケンス変数の動作が変更されました。 SMSTSRebootDelay 変数は、コンピューターが再起動するまでの待機時間を秒単位で指定します。 この変数を 0 以外に設定すると、タスク シーケンス マネージャーは再起動の前に通知ダイアログ ボックスを表示します。  
        この変数の値を構成すると、その値は、新しい値を構成するまで保持されます。 すべての後続のコンピューターの再起動の遅延は、同じ値になります。 Configuration Manager バージョン 1602 以前では、コンピューターの再起動後に変数が既定値 (30 秒) にリセットされます。   詳細については、「 [Task sequence built-in variables in System Center Configuration Manager](../../osd/understand/task-sequence-built-in-variables.md)」をご覧ください。

-   **Technical Preview 1602:** Technical Preview 1602 以降、Windows 2008 Server R2 から Windows 2012 Server R2 を実行するサイト システム サーバーのオペレーティング システムを一括アップグレードできます。  Windows Server 2012 R2 のアップグレード手順を使用する場合、アップグレード後に Configuration Manager サイト サーバーの復元を実行する必要はありません。  アップグレード手順については、「 [Windows Server 2012 R2 のアップグレード オプション](https://technet.microsoft.com/library/dn303416.aspx)」をご覧ください。  

    > [!WARNING]  
    >  Windows Server 2012 R2 にアップグレードする前に、サーバーから **WSUS 3.2 をアンインストールする必要があります** 。  
    >   
    >  この重要な手順の詳細については、Windows Server ドキュメントの「 [Windows Server Update Services の概要](https://technet.microsoft.com/library/hh852345.aspx) 」の「新機能と変更された機能」セクションを参照してください。  

-   **Technical Preview 1601:** 既定では、インストール時はサービス接続ポイントがオンライン モードに設定されており、オフライン モードへの変更はサポートされていません。  





##  <a name="a-namebkmktpcapsa-capabilities-delivered-in-technical-previews"></a><a name="bkmk_tpCaps"></a> Technical Preview で提供される機能  
 以下は、それぞれの Configuration Manager Technical Preview リリースで提供される機能です。  Technical Preview のバージョンで利用できるようになった機能は、以降のバージョンでも利用できます。 同様に、System Center Configuration Manager リリース (Current Branch) に追加された機能は、後続の Technical Preview でも引き続き利用できます。  特定の機能の詳細については、各プレビュー バージョンのコンテンツをクリックします。  

 |機能|Technical Preview バージョン|Current Branch バージョン|  
 |----------------|---------------------|--------------------|
 |自動展開規則でコンテンツのサイズでフィルター処理する|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|![追加されていません](media/Red_X.gif)|
 |必要なソフトウェア ダイアログの機能向上|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|![追加されていません](media/Red_X.gif)|
 |以前に承認されたアプリケーションの要求を拒否する|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|![追加されていません](media/Red_X.gif)|
 |自動アップグレードからクライアントを除外する|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|![追加されていません](media/Red_X.gif)|
 |Endpoint Protection の機能強化|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|![追加されていません](media/Red_X.gif)|
 |登録されるデバイス数の増加|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#increased-number-of-enrolled-devices)|![追加されていません](media/Red_X.gif)|
 |Apple DEP 設定の追加|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|![追加されていません](media/Red_X.gif)|
 |ビジネス向け Windows ストアと Configuration Manager のとの統合の強化|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|![追加されていません](media/Red_X.gif)|
 |構成アイテムの新しいコンプライアンス設定|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|![追加されていません](media/Red_X.gif)|
 |Upgrade Analytics との統合|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|![追加されていません](media/Red_X.gif)|
 |Windows 10 VPN ハイブリッド プロファイルのネイティブ接続の種類|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![追加されていません](media/Red_X.gif)|
 |境界グループの機能強化|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|![追加されていません](media/Red_X.gif)|
 |Office 365 クライアント管理ダッシュボード|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|![追加されていません](media/Red_X.gif)|
 |クライアントに Office 365 アプリを展開する|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#ceploy-office-365-apps-to-clients)|![追加されていません](media/Red_X.gif)|
 |BIOS から UEFI への変換の改善|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-bios-to-uefi-conversion)|![追加されていません](media/Red_X.gif)|
 |Intune 準拠チャート|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|![追加されていません](media/Red_X.gif)|
 |ConfigMgr クライアントのキャプチャの準備タスク シーケンス ステップの向上|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|![追加されていません](media/Red_X.gif)|
 |ソフトウェア センターの機能強化|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|![追加されていません](media/Red_X.gif)|
 |資産インテリジェンスの改善|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![追加されていません](media/Red_X.gif)|
 |リモート コントロール キーボードの変換|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![追加されていません](media/Red_X.gif)|
 |Windows 10 のエディションのアップグレード ポリシーの改善|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|![追加されていません](media/Red_X.gif)|
 |ソフトウェア センター ダイアログにおけるカスタマイズ可能なブランド|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-denter-dialogs)|![追加されていません](media/Red_X.gif)|  
 |オンプレミス モバイル デバイス管理のための複数のデバイス管理ポイント|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |デバイスを自動的にコレクションごとに分類|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[バージョン 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |必要なアプリケーションとソフトウェア更新プログラムを展開するための適用猶予期間|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|![追加されていません](media/Red_X.gif)|
 |デバイス ガードにより Configuration Manager を管理インストーラーとして使用|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![追加されていません](media/Red_X.gif)|
 |クラウド プロキシ サービス|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | ![追加されていません](media/Red_X.gif)|  
 |Configuration Manager で Office 365 のクライアント エージェントを管理|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |OSDPreserveDriveLetter タスク シーケンス変数は使用されなくなった|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[バージョン 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |更新プログラムとサービス ノードの変更|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |Windows 10 デバイス向けのアプリごとの VPN|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[バージョン 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |ソフトウェア更新プログラムのインストール タスク シーケンスの向上|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |ConfigMgr クライアントのキャプチャの準備タスク シーケンス ステップの向上 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|![追加されていません](media/Red_X.gif) |
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
 |クライアント キャッシュ設定とクライアント ピア キャッシュを管理するためのクライアント設定 |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)|  
 |KSP としての Passport for Work のサポート |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[バージョン 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |オンプレミスのデバイス正常性構成証明書|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[バージョン 1606](/sccm/core/servers/manage/health-attestation)|  
 |Android デバイスの SmartLock 設定|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[バージョン 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |ソフトウェア センターの機能強化|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |リモート制御の機能強化|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |PXE 対応配布ポイント上の RamDisk TFTP ブロック サイズとウィンドウ サイズのカスタマイズ|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[バージョン 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |モバイル デバイス管理の機能強化|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_MDM)|[バージョン 1602](/sccm/mdm/deploy-use/manage-ios-activation-lock) |  
 |バージョン 1602 でのソフトウェア センターの機能強化|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_SC1601)| [バージョン 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#client-management)|  
 |Windows 10 サービスの機能強化|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_Win10Servicing)|[バージョン 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#operating-system-deployment) |  
 |Microsoft Intune の統合の機能強化|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_hybrid1)|[バージョン 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#conditional-access)|  
 |クライアントのオンライン状態|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_clientStatus)|[バージョン 1602](/sccm/core/clients/manage/monitor-clients)|
 |アプリケーション管理の機能強化|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_appmgmt1601)|[バージョン 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#application-management)|  
 |コンプライアンス設定の機能強化|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_compliance1601)|[バージョン 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#compliance-settings)|  
 |デバイス正常性構成証明書|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_devicehealth)|[バージョン 1602](/sccm/core/servers/manage/health-attestation)|
 |使用条件のコンソール内での監視|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_viewterms)|[バージョン 1602](/sccm/mdm/deploy-use/terms-and-conditions)|  
 |Endpoint Protection のポリシー設定の機能強化|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_EPpolicy)|[バージョン 1602](/sccm/protect/deploy-use/endpoint-antimalware-policies)|  
 |Windows 10 における Windows Update for Business との統合|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_WUfB)|[バージョン 1602](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|  
 |System Center Configuration Manager を使用した Office 365 ProPlus クライアント更新プログラムの管理|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_Office365ProPlus)|[バージョン 1602](/sccm/sum/deploy-use/manage-office-365-proplus-updates)|  
 |高可用性データベース用の SQL Server AlwaysOn のサポート|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_AlwasyOn)|[バージョン 1602](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)|  
 |サーバー クラスターの提供|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_ClusterServerUpdates)|[バージョン 1606](/sccm/sum/deploy-use/service-a-server-group)|  
## <a name="see-also"></a>関連項目  
[System Center Configuration Manager の新機能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [System Center Configuration Manager の概要](../../core/understand/introduction.md)



<!--HONumber=Nov16_HO1-->


