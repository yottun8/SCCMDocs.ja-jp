---
title: 管理分析情報
titleSuffix: Configuration Manager
description: Configuration Manager コンソールで使用できるマネジメント インサイト機能について説明します。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cd2cee9de9f876f591145a12443b50d08349a451
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250750"
---
# <a name="management-insights-in-configuration-manager"></a>Configuration Manager でのマネジメント インサイト

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager のマネジメント インサイトからは、環境の現状に関する情報が提供されます。 この情報は、サイト データベースからのデータの分析に基づきます。 分析情報を利用することで、ご利用の環境についての理解を深め、その情報に基づいてアクションを実行できます。 この機能は、Configuration Manager バージョン 1802 でリリースされました。 <!--1353967-->



## <a name="review-management-insights"></a>マネジメント インサイトを確認する 

規則を表示するには、お使いのアカウントに**サイト** オブジェクトに対する**読み取り**アクセス許可が必要です。

1. Configuration Manager コンソールを開きます。  

2. **[管理]** ワークスペースに移動して、**[管理分析情報]** を展開し、**[すべての分析情報]** を選択します。  

    > [!Note]  
    > バージョン 1810 以降では、**[管理分析情報]** を選択すると、[管理分析情報ダッシュボード](#bkmk_insights)に表示されます。  

3. 確認する管理分析情報グループ名を開きます。 リボンで **[分析情報の表示]** を選択します。  

次の 4 つのタブを確認に使用できます。 

- **すべての規則**: 選択したマネジメント インサイト グループに対する規則をすべて一覧表示します。  

- **完了**: アクションが不要な規則を一覧表示します。  

- **進行中**: すべてではなく一部の前提条件が完了している規則を表示します。  

- **アクションが必要**: アクションを実行する必要がある規則が一覧表示されます。 **[詳細情報]** を選択し、アクションが必要な具体的な項目を取得します。  

**[前提条件]** ウィンドウには、規則の実行に必要な項目が一覧表示されます。

#### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>クラウド サービス グループのすべての規則と前提条件
![マネジメント インサイト - クラウド サービス グループのすべての規則と前提条件](./media/Management-insights-all-cloud-rules.png)


規則を選択し、**[詳細情報]** を選択して規則の詳細を表示します。



## <a name="operations"></a>オペレーション

マネジメント インサイト規則で、毎週のスケジュールで適用性が再評価されます。 必要に応じて規則を再評価するには、規則を右クリックして、**[再評価]** を選択します。

マネジメント インサイト規則のログ ファイルは、サイト サーバー上の **SMS_DataEngine.log** です。

<!--1357930--> バージョン 1806 以降では、一部の規則でアクションを実行できます。 規則を選択し、**[詳細情報]** を選択してから、**[アクションの実行]** を使用できる場合は選択します。 

規則に応じて、このアクションにより次のいずれかの動作が実行されます。  

- コンソールで、さらに詳細な対策を行うことが可能なノードへ、自動的に移動する。 たとえば、管理の洞察によって、クライアント設定の変更が推奨された場合、[クライアント設定] ノードへの移動という対策を行います。 その後、既定またはカスタムのクライアント設定オブジェクトを変更することにより、さらにアクションを実行します。  

- クエリに基づいてフィルター処理されたビューに移動する。 たとえば、空のコレクション ルールに対して対策を行うと、単にコレクションの一覧にこれらのコレクションが表示されるようになります。 その後、コレクションの削除やメンバーシップ規則の変更など、さらにアクションを実行します。  



## <a name="bkmk_insights"></a> 管理分析情報ダッシュボード
<!--1357979-->

バージョン 1810 以降では、**管理分析情報**ノードにグラフィック ダッシュボードが含まれています。 このダッシュボードにはルールの状態の概要が表示されるので、進捗状況を簡単に表示できます。 

ビューを絞り込むには、ダッシュボードの上部にある次のフィルターを使用します。
- 完了したタスクを表示
- オプション
- 推奨
- 重要

ダッシュボードには次のタイルが含まれています。  

- **管理分析情報インデックス**:管理分析情報ルールの全体的進捗状況を追跡記録します。 インデックスは加重平均です。 クリティカル ルールが最も重要です。 このインデックスは、任意のルールに最も軽い重みを与えます。  

- **管理分析情報グループ**: 各グループのルールがパーセント表示されます。フィルターが適用されます。 このグループで特定のルールにドリルダウンするグループを選択します。  

- **管理分析情報の優先順位**: 優先順位別のルールがパーセント表示されます。フィルターが適用されます。   

- **すべての分析情報**:優先順位と状態を含む、分析情報のテーブル。 使用可能な任意の列に文字列を一致させるには、テーブルの上部にある **[フィルター]** フィールドを使用します。 ダッシュボードでは、次の順序でテーブルが並べ替えられます。
    - ［ステータス］:アクションが必要、完了、不明  
    - 優先順位: クリティカル、推奨、オプション  
    - 最終更新: 古い日付順   

![管理分析情報ダッシュボードのスクリーンショット](media/1357979-management-insights-dashboard.png)



## <a name="groups-and-rules"></a>グループと規則

規則は、次の管理分析情報グループに編成されます。
- [アプリケーション](#applications)  
- [クラウド サービス](#cloud-services)  
- [コレクション](#collections)  
- [プロアクティブ メンテナンス](#proactive-maintenance)  
- [Security](#security)  
- [簡素化された管理](#simplified-management)  
- [ソフトウェア センター](#software-center)  
- [Windows 10](#windows-10)  


### <a name="applications"></a>アプリケーション

アプリケーション管理についての分析情報。

- **展開されていないアプリケーション**: ご利用の環境内でアクティブに展開されていないアプリケーションを一覧表示します。 この規則により、使用されていないアプリケーションの発見と削除が容易になり、コンソール上に表示されるアプリケーションの一覧を把握しやすくなります。 詳細については、「[アプリケーションの展開](/sccm/apps/deploy-use/deploy-applications)」をご覧ください。  


### <a name="cloud-services"></a>クラウド サービス

多くのクラウド サービスと統合できます。デバイスの最新の管理が可能になります。 

- **共同管理準備へのアクセス**: 共同管理を可能にするために必要な手順を理解するために役立ちます。 この規則には前提条件があります。 詳しくは、[共同管理の概要](/sccm/comanage/overview)に関するページをご覧ください。  

- **Configuration Manager で使用するように Azure サービスを構成する**: この規則は、Azure AD に Configuration Manager をオンボードするのに役に立ちます。これを行うと、Azure AD を使ってサイトでクライアントを認証できるようになります。 詳細については、「[Azure サービスの構成](/sccm/core/servers/deploy/configure/azure-services-wizard)」を参照してください。  

- **デバイスがハイブリッド Azure Active Directory に参加できるようにする**: Azure AD に参加しているデバイスの場合、ユーザーがドメインの資格情報でサインインできるだけでなく、デバイスが組織のセキュリティとコンプライアンスの基準を確実に満たすことができます。 詳しくは、「[Azure Active Directory ハイブリッド ID の設計上の考慮事項](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview)」をご覧ください。  

- **クライアントを最新の Windows 10 バージョンに更新する**: Windows 10 バージョン 1709 以降では、ユーザーのコンピューティング エクスペリエンスが向上し、新しくなります。 詳しくは、「[サービスとしての Windows の導入に関する主な記事](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service)」をご覧ください。  


### <a name="collections"></a>コレクション

コレクションを整理して再構成することで管理を簡易化できる分析情報。

- **空のコレクション**: ご利用の環境内でメンバーがいないコレクションを一覧表示します。 詳しくは、「[コレクションを管理する方法](/sccm/core/clients/manage/collections/manage-collections)」をご覧ください。  


### <a name="proactive-maintenance"></a>プロアクティブ メンテナンス
<!--1352184--> バージョン 1806 以降のこのグループの規則では、Configuration Manager オブジェクトの維持によって回避できる潜在的な構成上の問題が注目されています。    

- **割り当てられたサイト システムがない境界グループ**: 割り当てられたサイト システムがない境界グループは、サイトの割り当てにのみ使用できます。 詳細については、[境界グループの構成](/sccm/core/servers/deploy/configure/boundary-groups)に関するページを参照してください。  

- **メンバーを持たない境界グループ**: メンバーを持たない境界グループは、サイトの割り当てやコンテンツ ルックアップに適用されません。 詳細については、[境界グループの構成](/sccm/core/servers/deploy/configure/boundary-groups)に関するページを参照してください。  

- **コンテンツをクライアントに提供していない配布ポイント**: 過去 30 日以内にクライアントにコンテンツを提供していない配布ポイント。 このデータは、クライアントからのダウンロード履歴のレポートに基づきます。 詳細については、[配布ポイントのインストールと構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points)に関するページを参照してください。  

- **WSUS クリーンアップを有効にする**: ソフトウェアの更新ポイント コンポーネントのプロパティで WSUS のクリーンアップを実行するオプションを有効にしたことを確認します。 このオプションは、WSUS のパフォーマンスの向上に役立ちます。 詳しくは、「[ソフトウェア更新プログラムのメンテナンス](/sccm/sum/deploy-use/software-updates-maintenance)」をご覧ください。  

- **未使用のブート イメージ**: PXE ブートまたはタスク シーケンスの使用のために参照されていないブート イメージ。 詳細については、「[ブート イメージの管理](/sccm/osd/get-started/manage-boot-images)」をご覧ください。  

- **未使用の構成項目**: 構成基準の一部ではなく、30 日以上経過している構成項目。 詳細については、「[Create configuration baselines](/sccm/compliance/deploy-use/create-configuration-baselines)」 (構成基準を作成する) を参照してください。  

- **ピア キャッシュのソースを、Configuration Manager クライアントの最新バージョンにアップグレードします**: ピア キャッシュ ソースとして機能しているにもかかわらず、1806 より前のクライアント バージョンからアップグレードされていないクライアントを識別します。 1806 より前のクライアントは、1806 以降のバージョンを実行するクライアントに対するピア キャッシュ ソースとして使用できません。 **[対応策を取る]** を選択して、クライアントの一覧が表示されるデバイス ビューを開きます。<!--1358008-->  


### <a name="security"></a>セキュリティ
インフラストラクチャとデバイスのセキュリティを向上させるための分析情報。 

- **サポートされていないバージョンのマルウェア対策クライアント**: 10% を超えるクライアントが、サポートされていないバージョンの System Center Endpoint Protection を実行しています。 詳しくは、「[Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection)」をご覧ください。  


### <a name="simplified-management"></a>簡素化された管理

日常的に行う環境の管理の単純化に役立つ分析情報。 

- **CB 以外のクライアント バージョン**: バージョンが Current Branch (CB) のビルドではないすべてのクライアントを一覧表示します。 詳細については、「[クライアントをアップグレードする](/sccm/core/clients/manage/upgrade/upgrade-clients)」をご覧ください。  


### <a name="software-center"></a>ソフトウェア センター

ソフトウェア センターを管理するための分析情報。 

- **アプリケーション カタログの代わりに、ソフトウェア センターにユーザーを案内します**: 過去 14 日間にユーザーがアプリケーション カタログからアプリケーションをインストールまたは要求したかどうかを確認します。 アプリケーション カタログの主な機能はソフトウェア センターに含まれるようになりました。 アプリケーション カタログ Web サイトのサポートは、バージョン 1806 で終了します。 詳しくは、「[非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures#deprecated-features)」をご覧ください。  

- **ソフトウェア センターの新しいバージョンを使用する**: 前のバージョンのソフトウェア センターはサポートされなくなりました。 新しいソフトウェア センターを使用するようにクライアントを設定するには、**[コンピューター エージェント]** グループのクライアント設定 **[新しいソフトウェア センターを使用する]** を有効にします。 詳細については、「[クライアント設定について](/sccm/core/clients/deploy/about-client-settings#use-new-software-center)」を参照してください。  


### <a name="windows-10"></a>Windows 10

Windows 10 の展開とサービスに関連する分析情報を提供します。 Windows 10 のマネジメント インサイト グループは、半数を超えるクライアントが Windows 7、Windows 8、または Windows 8.1 を実行している場合にのみ利用できます。

- **Windows のテレメトリと商用 ID キーを構成します**: Upgrade Readiness のデータを使うには、商用 ID キーでデバイスを構成して、テレメトリを有効にします。 Windows 10 デバイスを、拡張 (制限付き) テレメトリ レベル以上に設定します。 詳しくは、「[Windows Analytics にデータをレポートするようにクライアントを構成する](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics)」をご覧ください。  

- **Configuration Manager を Upgrade Readiness に接続します**: Windows 7 がサポート対象外になる前に、Windows 10 の展開を促進するため、Upgrade Readiness を活用します。 詳しくは、[Upgrade Readiness の統合](/sccm/core/clients/manage/upgrade/upgrade-analytics)に関するページをご覧ください。   

#### <a name="windows-10-management-insights-rules"></a>Windows 10 のマネジメント インサイト規則
![マネジメント インサイト - Windows 10 の規則](./media/Windows-10-insights-group.png)
