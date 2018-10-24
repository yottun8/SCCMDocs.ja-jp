---
title: Technical Preview リリース
titleSuffix: Configuration Manager
description: Configuration Manager の新機能を体験する Technical Preview Branch について説明します。
ms.date: 10/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c43b501e8305f97f178d2eba9d3ab64fa9efe2a7
ms.sourcegitcommit: 3dfe3f4401651afa9dc65d14a8944ae4e4198b3e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2018
ms.locfileid: "48862449"
---
# <a name="technical-preview-for-configuration-manager"></a>Configuration Manager の Technical Preview

*適用対象: System Center Configuration Manager (Technical Preview)*

この記事では、Configuration Manager の毎月の Technical Preview Branch の詳細を説明します。 Technical Preview では、マイクロソフトが取り組んでいる新しい機能が紹介されます。 Configuration Manager の Current Branch にまだ組み込まれていない新機能が導入されています。 これらの機能は、最終的に Current Branch の更新プログラムに組み込まれる可能性があります。 機能が最終的に確定する前に実際に試してみて、フィードバックを提供してください。  

このリリースはテクニカル プレビューであるため、詳細や機能は変更されることがあります。  

この情報は、Configuration Manager Technical Preview Branch のすべてのバージョンに適用されます。 この記事では、各新機能とそれが最初に組み込まれる Technical Preview バージョンの一覧を示します。 たとえば、2018 年 (18) 9 月 (09) のバージョンは **1809** です。 個々の機能の詳細については、Preview バージョンごとの記事で説明します。  

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

### <a name="technical-preview-version-1810"></a>Technical Preview バージョン 1810

- [ クライアント インストールの改善](capabilities-in-technical-preview-1810.md#bkmk_ccmsetup) <!--1358840-->
- [ 共同管理デバイスに必要なアプリ コンプライアンス ポリシー](capabilities-in-technical-preview-1810.md#bkmk_app-compliance) <!--1358196-->
- [ 共同管理ダッシュボードの改善](capabilities-in-technical-preview-1810.md#bkmk_comgmt-report) <!--1358980-->
- [新しい境界グループのオプション](capabilities-in-technical-preview-1810.md#bkmk_bgoptions) <!--1358749-->
- [Windows クラスター ノード上のサイト システム](capabilities-in-technical-preview-1810.md#bkmk_cluster) <!--1359132-->
- [CMPivot の改善](capabilities-in-technical-preview-1810.md#bkmk_cmpivot) <!--1359068-->
- [スクリプトの改善](capabilities-in-technical-preview-1810.md#bkmk_scripts) <!--1358239-->
- [デバイスを復帰させる新しいクライアント通知アクション](capabilities-in-technical-preview-1810.md#bkmk_wakeup) <!--1317364-->
- [境界グループのタスク シーケンス サポート](capabilities-in-technical-preview-1810.md#bkmk_bgr-osd) <!--1359025-->
- [管理分析情報ダッシュボード](capabilities-in-technical-preview-1810.md#bkmk_insights) <!--1357979-->
- [コンソール内ドキュメント ダッシュボード](capabilities-in-technical-preview-1810.md#bkmk_doc-dashboard) <!--1357546-->
- [ドライバーのメンテナンスの機能強化](capabilities-in-technical-preview-1810.md#bkmk_drivers)<!--1358270-->  


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
 | CMPivot の改善 <!--1359068--> | [Tech Preview 1809](capabilities-in-technical-preview-1809.md#bkmk_cmpivot) | ![追加されていません](media/Red_X.gif) | 
 | ライフサイクル ダッシュボードの改善 <!--1358702--> | [Tech Preview 1809](capabilities-in-technical-preview-1809.md#bkmk_lifecycle) | ![追加されていません](media/Red_X.gif) | 
 | データ ウェアハウスの機能強化 <!--1358870--> | [Tech Preview 1809](capabilities-in-technical-preview-1809.md#bkmk_dataw) | ![追加されていません](media/Red_X.gif) | 
 | ソフトウェア更新プログラムのメンテナンス期間の改善 <!--vso2839307--> | [Tech Preview 1809](capabilities-in-technical-preview-1809.md#bkmk_sum-mw) | ![追加されていません](media/Red_X.gif) | 
 | ソフトウェア更新プログラムの段階的展開 <!--1358146--> | [Tech Preview 1808](capabilities-in-technical-preview-1808.md#bkmk_pod) | ![追加されていません](media/Red_X.gif) | 
 | アプリケーション修復の機能強化 <!--1357866--> | [Tech Preview 1808](capabilities-in-technical-preview-1808.md#bkmk_repair) | ![追加されていません](media/Red_X.gif) | 
 | コミュニティ ハブ <!--1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | ![追加されていません](media/Red_X.gif) | 
 | オフライン OS イメージ サービス用のドライブを指定する <!--1358924--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_osd) | ![追加されていません](media/Red_X.gif) | 
 | Intune での共同管理されたデバイス同期アクティビティ <!--1358565--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | ![追加されていません](media/Red_X.gif) | 
 | アプリケーションの修復 <!--1357866--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_app-repair) | ![追加されていません](media/Red_X.gif) | 
 | 電子メールでアプリケーション要求を承認する <!--1321550--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_email-approve) | ![追加されていません](media/Red_X.gif) | 
 | スクリプトの出力の改良 <!--1236459--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_script) | ![追加されていません](media/Red_X.gif) | 
 | サード パーティ製ソフトウェアの更新プログラムの改良 <!--1358714--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_3pupdate) | ![追加されていません](media/Red_X.gif) | 



## <a name="features-in-previous-technical-previews"></a>以前の Technical Preview の機能

以下の機能は、Configuration Manager Technical Preview Branch の以前のバージョンでリリースされました。 これらの機能は、以降のバージョンでも使用できますが、Current Branch ではまだ使用できません。 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

|機能 |Technical Preview バージョン |  
|----------------|---------------------|
|サポート センター <!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | 
|クライアント ベースの PXE レスポンダー サービス <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
|PXE ネットワーク ブートでの IPv6 のサポート<!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
|Azure Active Directory の使用 <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
|Windows Update for Business 更新プログラムのコンプライアンス評価<!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
|OData エンドポイントのデータ アクセス<!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
|資産インテリジェンスの改善 <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
|エンド ユーザーはポータル サイトからアプリをインストールできる<!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>関連項目  

詳細については、以下の記事を参照してください。  

- [ラボでの Configuration Manager の評価](/sccm/core/get-started/evaluate-with-lab-environment)
- [Configuration Manager の増分バージョンの新機能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Configuration Manager の概要](/sccm/core/understand/introduction)

> [!Tip]  
> 有効化に同意が必要な最新のブランチ機能の詳細については、[プレリリース機能](/sccm/core/servers/manage/pre-release-features)に関するページを参照してください。  
> 
> 最初に有効にする必要があるプレリリース版以外の最新のブランチ機能の詳細については、「[更新プログラムのオプション機能の有効化](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」を参照してください。  
