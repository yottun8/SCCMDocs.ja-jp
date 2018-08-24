---
title: Technical Preview リリース
titleSuffix: Configuration Manager
description: Configuration Manager の新機能を体験する Technical Preview Branch について説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b60ebcf0ce94dfdc25466b31c9a64d0d556e1ac6
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385390"
---
# <a name="technical-preview-for-configuration-manager"></a>Configuration Manager の Technical Preview

*適用対象: System Center Configuration Manager (Technical Preview)*

この記事では、Configuration Manager の毎月の Technical Preview Branch の詳細を説明します。 Technical Preview では、マイクロソフトが取り組んでいる新しい機能が紹介されます。 Configuration Manager の Current Branch にまだ組み込まれていない新機能が導入されています。 これらの機能は、最終的に Current Branch の更新プログラムに組み込まれる可能性があります。 機能が最終的に確定する前に実際に試してみて、フィードバックを提供してください。  

このリリースはテクニカル プレビューであるため、詳細や機能は変更されることがあります。  

この情報は、Configuration Manager Technical Preview Branch のすべてのバージョンに適用されます。 この記事では、各新機能とそれが最初に組み込まれる Technical Preview バージョンの一覧を示します。 たとえば、2018 年 (18) 6 月 (06) のバージョンは **1806** です。 個々の機能の詳細については、Preview バージョンごとの記事で説明します。  

Configuration Manager の *Current Branch* の新機能については、「[System Center Configuration Manager の増分バージョンの新機能](/sccm/core/plan-design/changes/whats-new-incremental-versions)」をご覧ください。



##  <a name="bkmk_reqs"></a> 要件と制限事項  

> [!IMPORTANT]     
>  Technical Preview はラボ環境での使用目的に限定してライセンスされます。 Microsoft はサポート サービスを提供しない場合があり、また、プレビュー ソフトウェアでは特定の機能が使用できない場合があります。 さらに、プレビュー ソフトウェアは、製品版ソフトウェアに比べて、セキュリティ、プライバシー、アクセシビリティ、可用性および信頼性の基準が低いか、または異なる場合があります。  

ほとんどの製品の前提条件については、[サポートされている構成](/sccm/core/plan-design/configs/supported-configurations)に関するページの情報をご覧ください。 Technical Preview Branch には次の例外が適用されます。  

-   各インストールは 90 日後に使用期限が切れるまでアクティブです。  

-   サポートされる言語は英語のみです。  

-   次のセットアップ コマンド ライン パラメーターのみをサポートしています。  
    -   `/silent`  
    -   `/testdbupgrade`    

-   サービス接続ポイントはオンライン モードでインストールされます。 オフライン モードはサポートされません。  

-   Technical Preview の特定バージョンごとの個別の記事には、追加の制限または要件が含まれています。

-   Technical Preview Branch では、次の機能はサポートされません。  

    - この Preview Branch への、またはこの Preview Branch からの[移行](/sccm/core/migration/migrate-data-between-hierarchies)。  

    - この Preview Branch への[アップグレード](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)。  

    - cd.latest フォルダーからの[サイトの回復](/sccm/core/servers/manage/recover-sites)。  <!--507106-->

-   この Preview Branch から Current Branch への更新はサポートされていません。  

    > [!Note]  
    > Preview バージョンから更新プログラムが使用できる場合は、Configuration Manager コンソールの **[更新とサービス]** ノードから検索してからインストールできます。 コンソール内アップグレード プロセスについては、youtube.com のビデオ「[Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8)」(Configuration Manager 更新プログラム パッケージのインストール) をご覧ください。  

-   スタンドアロン プライマリ サイトのみをサポートします。 中央管理サイト、複数のプライマリ サイト、またはセカンダリ サイトはサポートされません。  

Configuration Manager の Technical Preview Branch では、次の製品とテクノロジがサポートされています。 

-   次のバージョンの **SQL Server** のみをサポートします。  

    -   Configuration Manager バージョン 1710 以降の SQL Server 2017 (累積的な更新プログラム 2 以降適用済み)
    -   SQL Server 2016 (Service Pack なし、およびそれ以降)
    -   SQL Server 2014 (Service Pack 1 以降)
    -   SQL Server 2012 (Service Pack 3 以降)  


-   サイトは最大 10 台のクライアントをサポートします。各クライアントは次のいずれかの Windows バージョンを実行している必要があります。  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

> [!Note]  
> ここに製品が記載されていても、そのサポート ライフサイクルを超えてサポートが延長されることを意味するものではありません。 Configuration Manager では、サポート ライフサイクルが終了している製品はサポートされません。 詳しくは、「[Microsoft ライフサイクル ポリシー](https://go.microsoft.com/fwlink/p/?LinkId=208270)」をご覧ください。  



##  <a name="bkmk_install"></a> インストールと更新  

ラボ用の Configuration Manager Technical Preview Branch は、運用環境用の Configuration Manager Current Branch とは異なります。  

最初に、Technical Preview Branch のベースライン バージョンをインストールします。 ベースライン バージョンをインストールした後、コンソール内更新を使用して、最新のプレビュー バージョンでインストール環境を最新の状態にします。 通常、Technical Preview の新バージョンは毎月使用可能になります。

各 Technical Preview Branch は、それより後の 3 つの連続するバージョンが利用可能になるまでサポートされます。 たとえば、バージョン 1708 がリリースされた時点で、バージョン 1704 はサポートされなくなります。 バージョン 1705、1706、1707 はまだサポートされています。 ベースラインがサポートされなくなったときも、すぐにサポートされるバージョンに更新するのであれば、新しい Technical Preview サイトのインストール用にサポートされます。 古いベースラインは、新しいベースライン バージョンが使用できるようになるまでサポートされます。 ベースラインから使用可能な最新のバージョンに更新した後、最新の Technical Preview バージョンをインストールするまで更新プロセスを繰り返します。

> [!TIP]  
>  Technical Preview の更新プログラムをインストールするときに、プレビュー インストール環境を対象の新しい Technical Preview バージョンに更新します。 Technical Preview のインストールでは、Current Branch のインストールにはアップグレードできません。 また、Current Branch リリースから更新プログラムを受け取ることもありません。 
> 
> 1 年の間に何回か、Technical Preview Branch と Current Branch のバージョン番号が同じになることがあります。 たとえば、Technical Preview バージョン 1802 と Current Branch バージョン 1802 が存在します。 


### <a name="active-baseline-versions"></a>アクティブなベースライン バージョン
   
リリース後、最長 1 年間、ベースライン バージョンをインストールできます。 新しい Technical Preview サイトをインストールする時点で、使用できるベースライン バージョンが複数ある場合は、最新のベースライン バージョンを使用します。

-  **Technical Preview バージョン 1806**: Configuration Manager Technical Preview バージョン 1806 は、コンソール内更新と、新しいベースライン バージョンの両方として使用できます。 ベースライン バージョンを [TechNet Evaluation Center から](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)ダウンロードします。



##  <a name="BKMK_TPFeedback"></a> フィードバックについて  

Technical Preview の新機能に関するフィードバックをお寄せください。 詳細については、「[製品に関するフィードバック](/sccm/core/understand/find-help#product-feedback)」を参照してください。

希望する新しい機能のアイデアがありましたら、その内容もお知らせください。 新しいアイデアを提出する、または、他の人が提出したアイデアに投票するには、[UserVoice ページにアクセス](https://configurationmanager.uservoice.com)してください。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> 最新バージョンの機能  

最新の Configuration Manager Technical Preview バージョンでは、以下の機能を使用できます。 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1807"></a>Technical Preview バージョン 1807

- [コミュニティ ハブ](capabilities-in-technical-preview-1807.md#bkmk_hub) <!--1357766-->
- [オフライン OS イメージ サービス用のドライブを指定する](capabilities-in-technical-preview-1807.md#bkmk_osd) <!--1358924-->
- [Intune での共同管理されたデバイス同期アクティビティ](capabilities-in-technical-preview-1807.md#bkmk_comgmt) <!--1358565-->
- [アプリケーションの修復](capabilities-in-technical-preview-1807.md#bkmk_app-repair) <!--1357866-->
- [電子メールでアプリケーション要求を承認する](capabilities-in-technical-preview-1807.md#bkmk_email-approve) <!--1321550-->
- [スクリプトの出力の改良](capabilities-in-technical-preview-1807.md#bkmk_script) <!--1236459-->
- [サード パーティ製ソフトウェアの更新プログラムの改良](capabilities-in-technical-preview-1807.md#bkmk_3pupdate) <!--1358714-->


> [!Note]  
> Technical Preview の以前のバージョンで利用できるようになった機能は、以降のバージョンでも利用できます。 同様に、Configuration Manager の Current Branch に追加された機能は、Technical Preview Branch でも引き続き利用できます。   



## <a name="features-in-recent-supported-technical-previews"></a>サポートされている最近の Technical Preview での機能

Configuration Manager Technical Preview Branch の以前のバージョンでリリースされた以下の機能は、まだサポートされています。 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |機能 |Technical Preview のバージョン |Current Branch のバージョン|  
 |----------------|---------------------|--------------------|
 | 段階的な展開の機能強化 <!--1358577,1358147,1358578--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_pod)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | 新しい Windows アプリケーション パッケージ形式のサポート <!--1357427--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_msix)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | クライアント プッシュ セキュリティの機能改善 <!--1358204--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_client-push)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | プロアクティブ メンテナンスの管理分析情報 <!--1352184,et al--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_insights)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | 共同管理されたデバイスのモバイル アプリ ワークロードの移行 <!--1357892--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_comgmt)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | ピアのダウンロードの境界グループのオプション <!--1356193--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_bgoptions)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | カスタム カタログ用のサード パーティ製ソフトウェアの更新プログラムのサポート <!--1358714--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | クラウド管理機能の改善 <!--511980,515854--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_cloud)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | 新しいソフトウェア更新プログラムのコンプライアンス レポート <!--1357775--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_report)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | サード パーティ製ソフトウェアの更新プログラム <!--1352101--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Microsoft Edge 用に Windows Defender SmartScreen 設定を構成する <!--1353701--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#configure-windows-defender-smartscreen-settings-for-microsoft-edge)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | 共同管理されたデバイスのために MDM ポリシーを Microsoft Intune から同期する <!--1357377--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | 共同管理を使用して Intune に Office 365 ワークロードを移行する <!--1357841--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#transition-office-365-workload-to-intune-using-co-management)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Package Conversion Manager <!--1357861--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#package-conversion-manager)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | コンテンツなしのソフトウェア更新プログラムの展開 <!--1357933--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#deploy-software-updates-without-content)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Office 365 インストーラーと Office カスタマイズ ツールの統合 <!--1358149--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#office-customization-tool-integration-with-the-office-365-installer)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | クラウド管理ゲートウェイの機能改善 <!--1358215,1358651,503899--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-cloud-management-gateway)   | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | セキュアなクライアント通信の改善 <!--1358278,1358279--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-secure-client-communications)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | ソフトウェア センターのインフラストラクチャの改善 <!--1358309--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#software-center-infrastructure-improvements)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | デバイス上のすべてのユーザーに対して Windows アプリ パッケージをプロビジョニングする <!--1358310--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#provision-windows-app-packages-for-all-users-on-a-device)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Surface ダッシュボードの改善 <!--1358654--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-the-surface-dashboard)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | ハードウェア インベントリの既定の単位のリビジョン <!--514442--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#hardware-inventory-default-unit-revision)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | タスク シーケンスに手動で構成されたフェーズを使用して段階的展開を作成する <!--1358148--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Azure Resource Manager のためのクラウド配布ポイントのサポート <!--1322209--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | 管理の洞察に基づいて対策する <!--1357930--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | 共同管理を使用して Intune にデバイス構成ワークロードを移行する <!--1357903--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | ネットワークの輻そう制御を使用する配布ポイントを有効にする <!--1358112--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | クラウド管理ダッシュボード <!--1358461--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-management-dashboard)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | CMPivot <!--1358456--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmpivot)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | 改善されたセキュアなクライアント通信 <!--1356889,1358228,1358460--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | サード パーティ製のソフトウェア更新プログラムのサポートを有効にするための機能強化 <!--1357605--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Windows 10 一括アップグレード タスク シーケンスの機能強化 <!--1358500--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | クライアントと共にインストールされる CMTrace <!--1357971--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Configuration Manager コンソールの機能強化 <!--1358202--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | コンソール フィードバックの機能強化 <!--1357542--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | PXE 対応の配布ポイントの機能強化 <!--1357580--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | 大きな整数値でのハードウェア インベントリの機能強化 <!--1357880--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | WSUS メンテナンスの機能強化 <!--1357898--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | CNG 証明書のサポートの強化 <!--1357314--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | サイト サーバーのリモート コンテンツ ライブラリを構成する <!--1357525--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Configuration Manager コンソールからフィードバックを送信する<!--1357542--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#bkmk_feedback)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | サポート センター <!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | ![追加されていません](media/Red_X.gif) | 
 | Configuration Manager Toolkit <!--1357145--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | 承認を取り消したときにアプリケーションをアンインストールする <!--1357891--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | 探索から Active Directory コンテナーを除外する <!--1358143--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | ソフトウェア センターのアプリケーション カタログ Web サイト リンクの表示を指定する <!--1358214--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | ソフトウェア更新アーキテクチャを使用した自動展開規則のフィルター処理 <!--1322266--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | OS 展開の機能強化 <!--1358330,1358493--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | ソースとしてのクラウド配布ポイントのプル配布ポイントのサポート <!--1321554--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | WAN の使用率を減らすためのクライアント ピア キャッシュでの部分的なダウンロードのサポート <!--1357346--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | ソフトウェア センターのメンテナンス期間 <!--1358131--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | ソフトウェア センターの Web ページのカスタム タブ <!--1358132--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | クライアントでサード パーティ製ソフトウェア更新プログラムを有効にするサポート <!--1357605--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | 監視ビューからの資産の詳細のコピー/貼り付けを有効にする <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | SCAP 拡張機能 <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | [バージョン 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 
  

## <a name="features-in-previous-technical-previews"></a>以前の Technical Preview の機能

以下の機能は、Configuration Manager Technical Preview Branch の以前のバージョンでリリースされました。 これらの機能は、以降のバージョンでも使用できますが、Current Branch ではまだ使用できません。 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

|機能 |Technical Preview バージョン |  
|----------------|---------------------|
| クライアント ベースの PXE レスポンダー サービス <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
|PXE ネットワーク ブートでの IPv6 のサポート<!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
|Azure Active Directory の使用 <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
|Windows Update for Business 更新プログラムのコンプライアンス評価<!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
|OData エンドポイントのデータ アクセス<!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
|資産インテリジェンスの改善 <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
|エンド ユーザーはポータル サイトからアプリをインストールできる<!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|

<!--Removed for 1806 CB:
 |Site server role high availability <!-- 1128774  |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 | Product lifecycle dashboard <!--1319632  | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | 
 | Improvements to PXE-enabled distribution points <!-- 1357580  | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | 
-->



## <a name="see-also"></a>関連項目  

詳細については、以下の記事を参照してください。  

- [ラボでの Configuration Manager の評価](/sccm/core/get-started/evaluate-with-lab-environment)
- [Configuration Manager の増分バージョンの新機能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Configuration Manager の概要](/sccm/core/understand/introduction)

> [!Tip]  
> 有効化に同意が必要な最新のブランチ機能の詳細については、[プレリリース機能](/sccm/core/servers/manage/pre-release-features)に関するページを参照してください。  
> 
> 最初に有効にする必要があるプレリリース版以外の最新のブランチ機能の詳細については、「[更新プログラムのオプション機能の有効化](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」を参照してください。  
