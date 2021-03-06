---
title: Technical Preview リリース
titleSuffix: Configuration Manager
description: Configuration Manager の新機能を体験する Technical Preview Branch について説明します。
ms.date: 02/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 69fd77df25465910776eb413601efef5d87842aa
ms.sourcegitcommit: 4317bd20050f582a068d0a813e71c449d655e4b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2019
ms.locfileid: "55971899"
---
# <a name="technical-preview-for-configuration-manager"></a>Configuration Manager の Technical Preview

*適用対象:System Center Configuration Manager (Technical Preview)*

この記事では、Configuration Manager の毎月の Technical Preview Branch の詳細を説明します。 Technical Preview では、マイクロソフトが取り組んでいる新しい機能が紹介されます。 Configuration Manager の Current Branch にまだ組み込まれていない新機能が導入されています。 これらの機能は、最終的に Current Branch の更新プログラムに組み込まれる可能性があります。 機能が最終的に確定する前に実際に試してみて、フィードバックを提供してください。  

このリリースはテクニカル プレビューであるため、詳細や機能は変更されることがあります。  

この情報は、Configuration Manager Technical Preview Branch のすべてのバージョンに適用されます。 この記事では、各新機能とそれが最初に組み込まれる Technical Preview バージョンの一覧を示します。 たとえば、2019 年 (19) 1 月 (01) のバージョンは **1901** です。 個々の機能の詳細については、Preview バージョンごとの記事で説明します。  

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

    -   SQL Server 2017 (累積的な更新プログラム 2 以降) 
    -   SQL Server 2016 (Service Pack なし、またはそれ以降)
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

-  **Technical Preview バージョン 1810.2**:Configuration Manager Technical Preview バージョン 1810.2 は、コンソール内更新と、新しいベースライン バージョンの両方として使用できます。 ベースライン バージョンを [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) からダウンロードします。



##  <a name="BKMK_TPFeedback"></a> フィードバックについて  

Technical Preview の新機能に関するフィードバックをお寄せください。 詳細については、「[製品に関するフィードバック](/sccm/core/understand/find-help#product-feedback)」を参照してください。

希望する新しい機能のアイデアがありましたら、その内容もお知らせください。 新しいアイデアを提出する、または、他の人が提出したアイデアに投票するには、[UserVoice ページにアクセス](https://configurationmanager.uservoice.com)してください。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> 最新バージョンの機能  

最新の Configuration Manager Technical Preview バージョンでは、以下の機能を使用できます。 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1902"></a>Technical Preview バージョン 1902

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor)<!--ID-->

- [ダイアログ ウィンドウでトースト通知を置き換える](/sccm/core/get-started/2019/technical-preview-1902#bkmk_impact)<!--3555947-->
- [インプレース アップグレード タスク シーケンスの進行状況](/sccm/core/get-started/2019/technical-preview-1902#bkmk_ipu)<!--3747129-->
- [Windows の既知のフォルダーを OneDrive にリダイレクト](/sccm/core/get-started/2019/technical-preview-1902#bkmk_odfb)<!--3556021-->
- [リモート制御中にのみ最初の画面を表示する](/sccm/core/get-started/2019/technical-preview-1902#bkmk_rcmulti)<!--3231732-->
- [PowerShell スクリプトの編集またはコピー](/sccm/core/get-started/2019/technical-preview-1902#bkmk_psedit)<!--3705507-->
- [クラウド管理ゲートウェイを境界グループに追加する](/sccm/core/get-started/2019/technical-preview-1902#bkmk_cmgbg)<!--3640932-->
- [ソフトウェア センターで既定のビューを構成する](/sccm/core/get-started/2019/technical-preview-1902#bkmk_swctr)<!--3612112-->
- [クライアントの正常性ダッシュボードの機能強化](/sccm/core/get-started/2019/technical-preview-1902#bkmk_health)<!--3599209-->



> [!Note]  
> Technical Preview の以前のバージョンで利用できるようになった機能は、以降のバージョンでも利用できます。 同様に、Configuration Manager の Current Branch に追加された機能は、Technical Preview Branch でも引き続き利用できます。   



## <a name="features-in-recent-supported-technical-previews"></a>サポートされている最近の Technical Preview での機能

Configuration Manager Technical Preview Branch の以前のバージョンでリリースされた以下の機能は、まだサポートされています。 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 | 機能 | Technical Preview のバージョン | Current Branch のバージョン |  
 |---------|---------------------------|------------------------|
 | クライアントの正常性ダッシュボード <!--3599209--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_health) | ![追加されていません](media/Red_X.gif) | 
 | Windows 10 サービスで機能更新プログラムの優先順位を指定する <!--3734525--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_neo) | ![追加されていません](media/Red_X.gif) | 
 | 段階的な展開に対する専用の監視 <!--3555949--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_pod) | ![追加されていません](media/Red_X.gif) | 
 | 中央管理サイトから CMPivot を実行する <!--3610960--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmpivot) | ![追加されていません](media/Red_X.gif) | 
 | PowerShell スクリプトの実行タスク シーケンス ステップの改善 <!--3556028--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_posh) | ![追加されていません](media/Red_X.gif) | 
 | ライフサイクル ダッシュボードでの Office 製品 <!--3556026--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_lifecycle) | ![追加されていません](media/Red_X.gif) | 
 | コレクションのマネジメント インサイト規則 <!--3555752--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_micoll) | ![追加されていません](media/Red_X.gif) | 
 | MAC アドレスを使用してデバイス ビューを検索する <!--3600878--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_mac) | ![追加されていません](media/Red_X.gif) | 
 | 配布ポイント メンテナンス モード <!--3555754--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_dpmaint) | ![追加されていません](media/Red_X.gif) | 
 | 最適化されたイメージ サービス <!--3555951--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_resetbase) | ![追加されていません](media/Red_X.gif) | 
 | OS イメージの 1 つのインデックスをインポートする <!--3719699--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_index) | ![追加されていません](media/Red_X.gif) | 
 | クラウド サービスに Azure Resource Manager を使用する <!--3605704--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_arm) | ![追加されていません](media/Red_X.gif) | 
 | コンソール フィードバックの確認 <!--3556010--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_feedback) | ![追加されていません](media/Red_X.gif) | 
 | Azure で Configuration Manager Technical Preview ラボを作成する <!--3556017--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_azurevm) | ![追加されていません](media/Red_X.gif) | 
 | ピア ウェイクアップ用のカスタム ポートを指定する <!--3605925--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_sleep) | ![追加されていません](media/Red_X.gif) | 
 | 最近接続されたコンソールを表示する <!--3699367--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_console) | ![追加されていません](media/Red_X.gif) | 
 | しきい値を超えたときにクラウド サービスを停止する <!--3735092--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmg) | ![追加されていません](media/Red_X.gif) | 
 | クライアント プロビジョニング モードのタイムアウト <!--3197824--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osdprov) | ![追加されていません](media/Red_X.gif) | 
 | OS 展開の機能強化 <!--3633146,3641475,3654172,3734270--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osd) | ![追加されていません](media/Red_X.gif) | 
 | PowerShell スクリプトの実行タスク シーケンス ステップの改善 <!--3556028 fka 1359389--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_posh) | ![追加されていません](media/Red_X.gif) | 
 | 電子メールを使用したアプリケーション承認の改善 <!--3594063--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_email) | ![追加されていません](media/Red_X.gif) | 
 | ソフトウェア センターでのユーザーとデバイスのアフィニティの構成 <!--3485366--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_uda) | ![追加されていません](media/Red_X.gif) | 
 | Configuration Manager コンソールの機能拡張 <!--3594151--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_console) | ![追加されていません](media/Red_X.gif) | 
 | コミュニティ ハブからレポートのダウンロード<!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) | ![追加されていません](media/Red_X.gif) | 
 | Windows PowerShell プロファイルを読み込まない <!--1359239--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_noprofile) | ![追加されていません](media/Red_X.gif) | 
 | オンプレミスの MDM に Intune 接続は不要になった <!--1359124--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_opmdm) | ![追加されていません](media/Red_X.gif) | 
 | Configuration Manager コンソールの通知 <!--1318035--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_notify) | ![追加されていません](media/Red_X.gif) | 
 | タスク シーケンス メディアの作成の改善 <!--1359388--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_tsmedia) | ![追加されていません](media/Red_X.gif) | 
 | PowerShell スクリプトの実行タスク シーケンス ステップの改善 <!--1359389--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_posh) | ![追加されていません](media/Red_X.gif) | 



## <a name="features-in-previous-technical-previews"></a>以前の Technical Preview の機能

以下の機能は、Configuration Manager Technical Preview Branch の以前のバージョンでリリースされました。 これらの機能は、以降のバージョンでも使用できますが、Current Branch ではまだ使用できません。 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| 機能        | Technical Preview のバージョン |  
|----------------|---------------------------|
| コンソール内ドキュメント ダッシュボード <!--1357546--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_doc-dashboard) | 
| コミュニティ ハブ <!--1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | 
| Intune での共同管理されたデバイス同期アクティビティ <!--1358565--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | 
| クライアント ベースの PXE レスポンダー サービス <!--1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| PXE ネットワーク ブートでの IPv6 のサポート<!--1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Azure Active Directory の使用 <!--1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Windows Update for Business 更新プログラムのコンプライアンス評価<!--1235390--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
| 資産インテリジェンスの改善 <!--1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| エンド ユーザーはポータル サイトからアプリをインストールできる<!--1037233?--> | [Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |



## <a name="see-also"></a>関連項目  

詳細については、以下の記事を参照してください。  

- [ラボでの Configuration Manager の評価](/sccm/core/get-started/evaluate-with-lab-environment)
- [Configuration Manager の増分バージョンの新機能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Configuration Manager の概要](/sccm/core/understand/introduction)

> [!Tip]  
> 有効化に同意が必要な最新のブランチ機能の詳細については、[プレリリース機能](/sccm/core/servers/manage/pre-release-features)に関するページを参照してください。  
> 
> 最初に有効にする必要があるプレリリース版以外の最新のブランチ機能の詳細については、「[更新プログラムのオプション機能の有効化](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」を参照してください。  
