---
title: Technical Preview 1801 | Microsoft Docs
titleSuffix: Configuration Manager
description: System Center Configuration Manager の Technical Preview バージョン 1801 で使用できる機能について説明します。
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: dc4fcea93da9edfd781d80f5db3c4dfe104b118b
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897884"
---
# <a name="capabilities-in-technical-preview-1801-for-system-center-configuration-manager"></a>System Center Configuration Manager の Technical Preview 1801 の機能

「オブジェクトの*適用対象: System Center Configuration Manager (Technical Preview)*

この記事では、System Center Configuration Manager の Technical Preview バージョン 1801 で使用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 

このバージョンの Technical Preview をインストールする前に、「[System Center Configuration Manager の Technical Preview](/sccm/core/get-started/technical-preview)」を確認してください。 この記事により、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、フィードバックを提供する方法についての理解を深めることができます。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**この Technical Preview の既知の問題:**
- **サイト サーバーがパッシブ モードの場合、新しいプレビュー バージョンへの更新に失敗します**。 [プライマリ サイト サーバーがパッシブ モード](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability)の場合は、この新しいプレビュー バージョンに更新する前にパッシブ モードのサイト サーバーをアンインストールする必要があります。 パッシブ モードのサイト サーバーは、サイトの更新を完了したあとに再インストールできます。

  パッシブ モードのサイト サーバーをアンインストールするには、次の手順を実行します。
  1. Configuration Manager コンソールで **[管理]** > **[概要]** > **[サイトの構成]** > **[サーバーとサイト システムの役割]** の順に移動し、パッシブ モードのサイト サーバーを選択します。
  2. **[サイト システムの役割]** ウィンドウで、**[サイト サーバー]** の役割を右クリックし、**[役割の削除]** を選択します。
  3. パッシブ モードのサイト サーバーを右クリックし、**[削除]** を選択します。
  4. サイト サーバーのアンインストール後に、アクティブなプライマリ サイト サーバーで **CONFIGURATION_MANAGER_UPDATE** のサービスを再起動します。
  <!--sms 489412-->


**このバージョンでお試しいただける新機能を次に示します。**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>段階的展開の作成
<!-- 1357405 --> 段階的展開では、複数の展開を作成せずに、調整して順序付けしたソフトウェアのロールアウトを自動化します。 この Technical Preview バージョンでは、管理コンソールでタスク シーケンスの段階的展開ウィザードを完了できます。 ただし、展開は作成されません。 

### <a name="try-it-out"></a>試してみましょう。  
  タスクを実行してみます。 その後、**[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。
 
**タスク シーケンスの段階的展開の作成** </br>
1. **[ソフトウェア ライブラリ]** ワークスペースで **[オペレーティング システム]** を展開して、**[タスク シーケンス]** を選択します。
2. 既存のタスク シーケンスを右クリックして、**[Create Phased Deployment]\(段階的展開の作成\)** を選択します。 
3. **[全般]** タブで、段階的展開の名前と説明 (省略可能) を入力し、**[Automatically create default pilot and production phases]\(既定のパイロットと実稼働フェーズの自動作成\)** を選択します。 
4. **[パイロット コレクション]** フィールドと **[実稼働コレクション]** フィールドを設定します。 **[次へ]** を選択します。
5. **[設定]** タブで、スケジュール設定ごとに 1 つのオプションを選択し、完了したら **[次へ]** を選択します。 
6. **[Phases]\(フェーズ\)** タブで、必要に応じて、フェーズのいずれかを編集してから **[次へ]** をクリックします。
7. **[概要]** タブで選択内容を確認してから、**[次へ]** をクリックして続行します。

## <a name="co-management-reporting"></a>共同管理レポート
<!-- 1356648 --> [共同管理](/sccm/core/clients/manage/co-management-overview)機能を使用する場合、ご利用の環境での共同管理に関する情報を示すダッシュボードを表示できるようになりました。 Configuration Manager コンソールで、**[監視]** ワークスペースに移動し、**[Upgrade Readiness]** を展開して **[共同管理]** ダッシュボードを選択します。 ダッシュボードには次のタイルが含まれています。
- **共同管理デバイス**: 共同管理に対して有効にした、環境におけるデバイスの割合
- **OS ディストリビューション**: バージョンごとのオペレーティング システム (OS) の詳細。 このグラフでは以下のグループを使用します。
  - Windows 7 と 8.x
  - 1709 より前の Windows 10
  - Windows 10 1709 以降
    > [!NOTE] 
    > Windows 10 バージョン 1709 以降が共同管理の前提条件となります。
- **共同管理状態**: 次のカテゴリのデバイスの成功または失敗の詳細。
   - 成功、ハイブリッド Azure AD 参加済み
   - 成功、Azure AD 参加済み
   - 失敗しました:自動登録に失敗しました
- **ワークロードの移行**: 次の 3 つの使用可能なワークロードに関する、Microsoft Intune に移行したデバイスの数を示す棒グラフ。 
   - コンプライアンス ポリシー
   - リソース アクセス
   - Windows Update for Business

### <a name="prerequisites"></a>[前提条件]
- Configuration Manager コンソールを実行するコンピューターには、Internet Explorer 9 以降が必要です。



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>自動展開規則の評価スケジュールの機能拡張
<!-- 1357133 --> [皆さまからのフィードバック](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling)を基に、基準日からのオフセットを指定して自動展開規則 (ADR) の評価をスケジュールできるようになりました。 たとえば、月の第 2 火曜日の 2 日後のオフセットの場合、木曜日に規則が評価されます。 

### <a name="try-it-out"></a>試してみましょう。  
 タスクを実行してみます。 その後、**[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。 <br/>

**基準日からのオフセットを指定して ADR を評価するカスタム スケジュールを作成する** </br>
1.  **[ソフトウェア ライブラリ]** ワークスペースで、**[ソフトウェア更新プログラム]** を展開し、**[自動展開規則]** を選択します。
2. **[自動展開規則]** を右クリックして、**[自動展開規則の作成]** を選択します。 
3. 画面の指示に従って、**[全般]**、**[展開設定]**、**[ソフトウェアの更新]** の各タブに入力します。 
4. **[評価スケジュール]** タブで、**[スケジュールに基づいて規則を実行する]** と **[カスタマイズ]** を選択します。
5. カスタム スケジュールでは、**[毎月]** を選択し、第 2 火曜日などの基準日を指定します。 
6. **[オフセット (日)]** とオフセットの日数を確認し、完了したら **[OK]** をクリックします。  
7. **自動展開規則の作成ウィザード**の残りの部分を完了します。 



## <a name="reassign-distribution-point"></a>配布ポイントの再割り当て
<!-- 1306937 --> 多くのお客様が大きな Configuration Manager インフラストラクチャを持っており、環境を簡素化するためにプライマリ サイトまたはセカンダリ サイトを減らしています。 それでも、管理されたクライアントにコンテンツを提供するためにブランチ オフィスの所在地で配布ポイントを保持する必要があります。 多くの場合、これらの配布ポイントには数テラバイト以上のコンテンツが含まれています。 これらのリモート サーバーに配布するための時間とネットワーク帯域幅を考えると、このコンテンツにはコストがかかります。 

この機能を使用することで、コンテンツを再配布せずに配布ポイントを別のプライマリ サイトに再割り当てできます。 この操作により、サーバー上のすべてのコンテンツを保持したままで、サイト システムの割り当てが更新されます。 複数の配布ポイントを再割り当てする必要がある場合は、まず、単一の配布ポイントでこの操作を実行してから、一度に 1 つずつ追加のサーバーで操作を続行します。

> [!IMPORTANT]
> サイト システム サーバーでホストできるのは配布ポイントの役割のみです。 サイト システム サーバーで、状態移行ポイントなどの別の Configuration Manager サーバーの役割をホストする場合、配布ポイントを再割り当てすることはできません。 また、クラウド配布ポイントを再割り当てすることはできません。 

単一のプライマリ サイトに関する Technical Preview の制限により、このリリースではこのオプションは機能しません。 シナリオを検討し、リボンの **[ホーム]** タブから、この操作の機能について**フィードバック**を送信します。
1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動して、**[配布ポイント]** ノードを選択します。
2. ターゲットの配布ポイントを右クリックして、**[配布ポイントの再割り当て]** を選択します。 
  ![配布ポイントの再割り当て](media/1306937-reassign-dp.png)
3. この配布ポイントを再割り当てするサイト サーバーとサイト コードを選択します。 
  ![サイト サーバーの選択](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>ハードウェア インベントリの機能拡張
<!-- 1357389 --> 新しく追加されたクラスでは、キーではないハードウェア インベントリ プロパティに対して、255 文字より長い文字列を指定することができます。

### <a name="try-it-out"></a>試してみましょう。  
タスクを実行してみます。 その後、**[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。<br/>

1. **[管理]** ワークスペースで、**[クライアント設定]** をクリックして、編集するクライアント デバイス設定を強調表示し、右クリックして **[プロパティ]** を選択します。 
2. **[ハードウェア インベントリ]**、**[クラスの設定]**、**[追加]** の順に選択します。
3. **[接続]** ボタンをクリックします。
4. **[コンピューター名]**、**[WMI 名前空間]** を入力し、必要に応じて **[再帰]** を選択します。 接続するために必要な場合は、資格情報を指定します。 **[接続]** をクリックして、名前空間クラスを表示します。
5. 新しいクラスを選択してから **[編集]** をクリックします。
6. キー以外の、文字列である 1 つ以上のプロパティの **[長さ]** を変更し、255 より大きい値になるようにします。 **[OK]** をクリックします。 
7. **[ハードウェア インベントリ クラスの追加]** で編集したプロパティが選択されていることを確認して、**[OK]** をクリックします。 
8. 255 文字より長いプロパティを含むクラスが新しく追加されたハードウェア インベントリを収集します。 



## <a name="improvements-to-client-settings-for-software-center"></a>ソフトウェア センターのクライアント設定の機能拡張
<!-- 1351224 & 1355146 --> このバージョンの Technical Preview では、クライアント設定でソフトウェア センターのカスタマイズ機能が拡張されました。 

1. ソフトウェア センターのクライアント設定では、**[カスタマイズ]** ボタンが表示されるようになりました。
2. プレビューが追加され、ソフトウェア センターのバナーの外観が表示されるようになりました。<!--1351224-->
    - ロゴが選択されていない場合、プレビューでは会社名のテキストと色が表示されます。
    - ロゴが選択されている場合、プレビューではロゴと会社名のテキストが表示されます。  
3.  **[Hide unapproved applications in Software Center]\(ソフトウェア センターで承認されていないアプリケーションを非表示にする\)** は、ソフトウェア センターの新しい設定です。 このオプションを有効にすると、承認を必要とするユーザーの使用可能なアプリケーションがソフトウェア センターでは非表示になります。<!--1355146-->

### <a name="try-it-out"></a>試してみましょう。  
 タスクを実行してみます。 その後、**[ホーム]** タブから**フィードバック**を送信して、どのように動作したかを報告します。

1. **[管理]** ワークスペースで **[クライアント設定]** をクリックします。 編集するクライアント デバイス設定を選択します。 これを右クリックし、**[プロパティ]**、**[ソフトウェア センター]** の順に選択します。
2.  **[カスタマイズ]** ボタンをクリックします。 プレビューを含むさまざまなカスタマイズ設定を試してみます。
3. **[Hide unapproved applications in Software Center]\(ソフトウェア センターで承認されていないアプリケーションを非表示にする)** 設定を有効にします。 ソフトウェア センターで変更を確認します。 



## <a name="new-settings-for-windows-defender-application-guard"></a>Windows Defender Application Guard の新しい設定
<!-- 1356256 --> Windows 10 バージョン 1709 以降のデバイスには、[Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy) の新しい 2 つのホスト対話設定があります。 
1. Web サイトに、ホストの仮想グラフィック プロセッサへのアクセスを許可することができます。 
2. コンテナー内にダウンロードされたファイルをホストで保持することができます。 </br>



## <a name="improvements-to-run-scripts"></a>スクリプトの実行の改善
<!-- 1236459 --> [**スクリプトの実行**機能](/sccm/apps/deploy-use/create-deploy-scripts)を使用することで、署名済みの PowerShell スクリプトをインポートして実行できるようになりました。 
- スクリプトの整合性を保つには、コピー/貼り付けを使用せずに、署名済みスクリプトをインポートする必要があります。 
- 署名済みスクリプトをインポートした後で編集することはできません。
    
>[!IMPORTANT]
>この Technical Preview には、一時的な制限が 2 つあります。
>- スクリプトはスクリプトの実行機能でのみインポートでき、コンソールから直接編集することはできません。
>- 非 Unicode エンコードでインポートされたスクリプトは、コンソールに正しく表示されない可能性があります。 それでも、スクリプトは最初に書き込まれたとおり実行されます。





## <a name="next-steps"></a>次のステップ
Technical Preview ブランチのインストールまたは更新については、「[System Center Configuration Manager の Technical Preview](/sccm/core/get-started/technical-preview)」をご覧ください。    
