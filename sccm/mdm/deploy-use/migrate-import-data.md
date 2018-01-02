---
title: "Microsoft Intune へのデータのインポート"
titleSuffix: Configuration Manager
description: 
keywords: 
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.openlocfilehash: d42a5fd64b5baead8ef87d8c08a99ec659f94633
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2017
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Configuration Manager のデータの Microsoft Intune へのインポート 

*適用対象: System Center Configuration Manager (Current Branch)*    

[ハイブリッド MDM のユーザーとデバイスを、クラウド専用構成の Intune スタンドアロンに移行する](migrate-hybridmdm-to-intunesa.md)プロセスの推奨される最初のフェーズは、Intune Data Importer ツールを使用することです。 このフェーズをスキップして [Intune でのユーザーの移行を準備する](migrate-prepare-intune.md)フェーズに進むこともできます。 ただし、このツールは、次のフェーズでの時間を大幅に節約できる、次の機能を実行します。 
1.  Configuration Manager 階層から選択したオブジェクトに関するデータを収集する。 
2.  インポートに選択できるオブジェクトに関する詳細と、一部のオブジェクトがインポートできない理由に関する情報を提供する。
3.  選択したオブジェクトを Microsoft Intune テナントにインポートする。 

Data Importer ツールがご使用の Configuration Manager 環境を変更することはありません。そのため、ハイブリッド MDM デバイスを管理されていない状態のままにするリスクを冒さずに、Intune にオブジェクトをインポートし、すべてが期待どおりに機能していることを検証することができます。 

## <a name="what-objects-can-this-tool-import"></a>このツールでインポートできるオブジェクト
インポート ツールは Configuration Manager で次のオブジェクト タイプに関する情報を収集し、収集されたオブジェクトがインポートできるかどうかに関する情報を提供します。 
- 構成項目
- 証明書プロファイル
- 電子メール プロファイル
- VPN プロファイル
- Wi-Fi プロファイル
- コンプライアンス ポリシー
- アプリ
- 展開

> [!Note]    
> デプロイのインポートは、インポートするその他のオブジェクトの種類にのみ役立ちます。 たとえば、VPN プロファイルとデプロイをインポートすると、選択した VPN プロファイルのデプロイのみをインポートできます。 Intune でのデプロイは、割り当てと呼ばれます。 以前にインポートしたオブジェクトのデプロイをインポートする場合は、そのオブジェクトをもう一度インポートするか、Azure の Intune で割り当てを手動で作成する必要があります。 たとえば、VPN プロファイルをインポートしてデプロイをインポートしない場合は、ツールを再度実行し、VPN プロファイルとデプロイを選択するか、Azure の Intune で割り当てを手動で作成する必要があります。  ツールを再実行すると、重複するオブジェクトが作成される場合があります。これは後で Azure の Intune で削除できます。  

> [!Important]    
> デプロイのコレクションが Azure Active Directory (AAD) にレプリケートされた Active Directory グループに基づいている場合、ツールを実行するときに、適切なデプロイを選択すると、ツールは移行されたオブジェクトを自動的にグループ化の対象にします。 より複雑なコレクションまたはダイレクト メンバーシップ コレクションがある場合は、AAD でそれらを手動で再作成し、Azure の Intune でそれらを手動でオブジェクトの割り当て対象にする必要があります。


## <a name="things-to-know-before-you-run-the-tool"></a>ツールを実行する前に知っておくべきこと
- ツールを実行しても、Configuration Manager 環境は変更されません。
- 最初に試用版テナントを使用して、データ インポート プロセスをテストすることをお勧めします。 そして、意図したデータがインポートされていることを確認したら、実稼働の Intune テナントで同じプロセスを実行できます。
- Data Importer は、Configuration Manager データを 1 回だけインポートすることを意図しています。 Configuration Manager または Intune 内のオブジェクトは追跡しません。 ただし、以前と同じコンピューターでインポーターを再度実行すると、以前にどのオブジェクトをインポートしたかがわかります。 ツールでは、オブジェクトがまだ Intune に存在しているかどうか、またはオブジェクトが変更されているかどうかはわかりません。 Intune にデータを複数回インポートすると、オブジェクトが重複する場合があります。
- すべてのプロファイル設定をインポートすることはできません。 たとえば、キオスク モードまたは PFX 設定をインポートすることはできません。 
- 選択したプラットフォームに適用できない設定を持つ Configuration Manager ポリシーがある場合、インポート時にツールでこれらの設定が無視される可能性があります。 設定を無視することで、ポリシーをインポートして Intune でサポートされるようにすることができます。 
- ツールは、オブジェクトをインポートできない理由を提供しようとします。 場合によっては、Intune にオブジェクトをインポートする前に、Configuration Manager コンソールに戻って、問題を修正し、Configuration Manager オブジェクトの検出スキャンをもう一度開始してから、オブジェクトをインポートすることができます。 Intune でこれらのオブジェクトを手動で再作成する必要がある場合があります。
- 他のオブジェクトに依存しているいくつかのプロファイルがあります。 証明書に依存している電子メール プロファイルのように、別のオブジェクトに依存しているプロファイルをインポートする場合は、以前に一方のオブジェクトを同じコンピューターから同じユーザーでインポートしたことがない限り、同時に両方のオブジェクトをインポートする必要があります。  
- このツールの実行後、手動で追加の手順を実行する必要がある場合があります。 たとえば、アプリとポリシーを AAD グループの対象とする場合などです。 

## <a name="prerequisites"></a>必要条件
- Configuration Manager バージョン 1610 以降。最上位サイトを指定し、サイト階層内のすべてのオブジェクトへのアクセス権を持つユーザーでツールを実行することをお勧めします。 ツールは、ツールを実行しているユーザーがアクセスできるオブジェクトのみを検出します。 
- グローバル管理者が最初に、次の ***intunedataimporter.exe - GlobalConsent*** パラメーターを使用して、Data Importer ツールを実行する必要があります。 その後、グローバル管理者または Intune 管理者がツールを実行できます。  


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->

## <a name="download-the-data-importer-tool"></a>Data Importer ツールのダウンロード
Data Importer ツールは、GitHub の ConfigMgrTools/Intune-Data-Importer リポジトリからダウンロードして入手できます。 次の手順に従ってツールをダウンロードします。

1. [Intune Data Importer GitHub リリース](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases)のページに移動します。
2. 最新のリリースについては、**Microsoft.Intune.Data.Importer.exe** をクリックします。
3. .exe ファイルを保存して実行 (または単に実行) してから、Intune Data Importer ツールを展開するフォルダーを選択します。

## <a name="run-the-data-importer-tool"></a>Data Importer ツールの実行
Data Importer ツールのウィザードは、次の 3 つの主要なステップに分割できます。 このセクションでは、ウィザードの各セクションを完了し、Intune に Configuration Manager データを正常にインポートするのに役立つ情報を提供します。 各ステップは前のステップが終了したところからの続きです。

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>リソースにアクセスするために Data Importer ツールにアクセス許可を付与する
Data Importer ツールを実行するには、事前にグローバル管理者アカウントを使用して、リソースにアクセスするためのアクセス許可を Azure の Data Importer ツールに付与する必要があります。 その後は、グローバル管理者アカウントまたは Intune 管理者アカウントを使用してツールを実行できます。   

1.  グローバル管理者は、最初に ***intunedataimporter.exe - GlobalConsent*** パラメーターを使用してツールを実行する必要があります。 
2. ツールが起動すると、ログイン画面が表示されます。ここで Azure でグローバル管理者ロールを持つアカウントを使用してサインインする必要がありますます。 
3. **[同意]** をクリックして Microsoft Graph で適切な権限を持つ Azure にアプリケーションを作成します。 Data Importer ツールでは、オブジェクトを Microsoft Intune にインポートするためにこれらの権限が必要です。   

   > [!Important]
   > **[同意]** をクリックすると、ツールに以下の操作を行うことを許可します。
   > - すべてのグループを読み取る
   > - サインインしてユーザー プロファイルを読み取る
   > - Intune デバイスの構成とポリシーの読み書き
   > - Intune アプリの読み書き
   > - Intune ロール ベース管理制御ポリシーの読み書き
   > - Intune デバイスの読み書き
   > - Intune 構成の読み書き
1. 同意すると、他のグローバル管理者または Intune 管理者がツールを実行して、Configuration Manager からデータを Azure の Intune にインポートできます。    
        
    > [!Note]
    > グローバル管理者が最初に同意していない場合、Intune 管理者が Data Importer ツールを実行し、Intune サブスクリプションにログインすると、ツールで「**このアプリケーションにアクセスできません**」と表示される場合があります。

### <a name="manually-map-collections-to-azure-ad-groups"></a>Azure AD グループにコレクションを手動でマップする
Data Importer ツールを実行すると、1 つの AD グループを対象とする 1 つの規則を使用して、コレクションから AD グループの名前が抽出されます。 Intune で割り当てが作成されると、Data Importer は AD グループと同じ名前の Azure AD グループを検索し、存在する場合は、インポートしたオブジェクトをその Azure AD グループに割り当てます。 Data Importer が検出したコレクションの AD グループ名を上書きして、そのコレクションに使用する 1 つまたは複数の Azure AD グループを指定できます。 コレクション マッピング ファイルを使用すると、通常 Data Importer ではインポートできないコレクションを Azure AD グループにマップできます。
#### <a name="find-the-collections-that-cannot-be-imported"></a>インポートできないコレクションを検索する
インポートできないすべてのコレクションの一覧を取得して、それらをコレクション マッピングの .csv ファイルに追加できます。 
1. Data Importer ツールを実行し、インポートするオブジェクトを選択します。 「[フェーズ 1: Configuration Manager オブジェクトの検出とデータの収集](#phase-1:-discover-configuration-manager-objects-and-collect-data)」および「[フェーズ 2: 問題を解決し、インポートするオブジェクトを選択する](#phase-2:-resolve-issues-and-select-the-objects-to-import)」の手順に従って、オブジェクトを検出し選択します。 次に **[概要]** ページで、**[エクスポートの詳細]** を選択して .csv ファイルを作成します。このファイルには、インポートできないオブジェクトやデプロイなどの、インポートに選択したすべての詳細が含まれます。 
2. Microsoft Excel で .csv ファイルを開き、**[種類]** 列に **[デプロイ]**、**[Importable]\(インポート可能\)** 列に **[いいえ]** を指定してデータをフィルター処理します。 コレクション名の列には、デプロイをインポート可能にするためにコレクション マッピング ファイルに追加する必要があるすべてのコレクションが示されます。

#### <a name="create-the-collection-mapping-file"></a>コレクション マッピング ファイルを作成する
コレクション マッピング ファイルはコンマ区切り値 (CSV) ファイルで、最初の列が Configuration Manager コレクションの名前で、2 番目の列がそのコレクションに使用する Azure AD グループの名前です。 1 つの Configuration Manager コレクションに複数の Azure AD グループを指定するには、そのコレクション名の CSV ファイルに複数の行を作成します。 次の例は、2 つのコレクションを含む CSV ファイルです。 最初のコレクションは 1 つの Azure AD グループにマップされ、2 つ目のコレクションは 2 つの Azure AD グループにマップされます。

![コレクション マッピング CSV ファイルの例](..\media\migrate-collectionmapping.png)

#### <a name="start-the-data-importer-tool-using-collection-mapping"></a>コレクション マッピングを使用して Data Importer ツールを起動する
コレクション マッピング ファイルを使用するには、*-CollectionMappingFile* コマンド ライン パラメーターおよび作成するコレクション マッピング .csv ファイルへの完全パスを使用して、Data Importer ツールを起動する必要があります。 たとえば、

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]
> Data Importer では、どのウィザード ページにも、コレクション マッピング ファイルが読み込まれたことを示すものは何も表示されません。 ただし、.csv ファイルの読み取り中に発生したエラーはすべて表示されます。 また、ウィザードの **[概要]** ページで、**[デプロイ]** の種類を確認できます。 ツールでは、インポート可能な列に **[はい]** が表示され、**[備考]** 列にはオブジェクトに割り当てる Azure AD グループが一覧表示されます。

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>フェーズ 1: Configuration Manager オブジェクトの検出とデータの収集
フェーズ 1 では、検出するオブジェクトを選択し、選択したオブジェクトに関する情報をツールに収集させます。 
1. ツールを開き、**[開始]** をクリックします。  
2. 情報を読み、**[次へ]** をクリックします。 
3. 以前にエクスポートされたデータ セットをインポートする、または、インポートするオブジェクトの種類を選択する、のいずれかを選択します。
   - **以前にエクスポートされたデータ セットをインポートする**: **[Import data set exported from a previous run of Intune Data Importer]\(Intune Data Importer の以前の実行でエクスポートされたデータ セットのインポート\)** を選択し、**[Exported data folder]\(エクスポートされたデータのフォルダー\)** で **[参照]** をクリックして、以前 Data Importer ツールでエクスポートしたデータ セットを選択します。 データ セットをインポートするユーザーは、そのデータをエクスポートしたユーザーと同じである必要があります。 データをインポートしたら、オブジェクトの概要がウィザードの **[概要]** ページに一覧表示されます。 概要の内容が正しければ、「[フェーズ 3: 選択したオブジェクトを Intune にインポートする](phase-3:-import-selected-object-to-intune)」までスキップします。
 
      > [!Note]
      > インポートするサイト内のオブジェクトを検出および選択したら、ウィザードの **[Sign-in to Intune]\(Intune にサインイン\)** ページでデータ セットにオブジェクトをエクスポートできます。 それが終わるとこのページでデータ セットをインポートできます。 データ セットはログイン ユーザーの Windows ユーザー資格情報 を使用して暗号化されているため、データ セットをエクスポートしたユーザーだけが、ツールでデータ セットをインポートできます。 
   - **インポートするオブジェクトの種類を選択**: **[Select object types to import]\(インポートするオブジェクトの種類を選択\)** を選択して、ご自分の環境内でインポートし検出するオブジェクトの種類を選択します。 ご自分のサイトおよびインポートするオブジェクトに関する次の情報を指定します。
      - **サイト サーバー名**: オブジェクトをインポートするサイト サーバーの完全修飾ドメイン名を指定します。 ツールは、ツールを実行しているユーザーがアクセスできるオブジェクトのみを検出します。 通常、最上位サイトを指定し、サイト階層内のすべてのオブジェクトへのアクセス権を持つユーザーでツールを実行します。
      - **サイト コード**: サイト サーバーのサイト コードを指定します。 この 3 文字のコードは、Configuration Manager コンソールの上部にあります。
      - **インポートするオブジェクトの種類**: ツールに収集させるオブジェクトを選択します。 **[すべて選択]** を選択してすべてのオブジェクトを選択するか、個々のオブジェクトの種類を選択することができます。 
4.  **[次へ]** をクリックして、サイトでオブジェクトの検出を開始します。 ツールに各オブジェクトの種類の進行状況が表示されます。 
    - ツールで選択したオブジェクトの種類のデータが検出されない場合は、進行状況バーにすぐにそのオブジェクトの種類に対して完了が表示されます。
    - 選択していないオブジェクトは、**データ収集**ページには表示されません。 
    - 収集されなかったオブジェクトまたは収集プロセス中に取り消したオブジェクトに対し、もう一度ツールを実行することができます。

### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>フェーズ 2: 問題を解決し、インポートするオブジェクトを選択する  
フェーズ 2 では、ツールで検出されたオブジェクトを確認し、オブジェクトが Intune にインポートされることを妨げている問題を解決し、インポートするオブジェクトを選択します。 問題を修正したら、ウィザードの **[Discover environment]\(検出環境\)** ページに戻り、オブジェクトを再検出します。 
5.  **[次へ]** をクリックして、収集されたオブジェクトを確認します。 項目の選択ページは、収集されたオブジェクトの種類ごとに使用できます。 
 <!--   > [!Tip]     
    > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
    > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
    > - Objects are always grouped under their parent item even when you sort or filter the objects.
-->
6.  項目の選択の各ページで、[Importable]\(インポート可能\) の列でオブジェクトを並べ替えて、インポートできないオブジェクトを確認します。 [Notes]\(備考\) 列の情報では、ツールがオブジェクトをインポートできない理由の詳細を提供します。 
7.  この時点で、インポートできないオブジェクトの問題を修正するかどうかを決定する必要があります。 1 つまたは複数の問題を修正する場合は、[Select data from Configuration Manager]\(Configuration Manager からデータを選択する\) ページに到達するまで [前へ] をクリックして、データを再度収集し、問題が解決したかどうかを確認します。 インポートできないオブジェクトを解決するまで、問題の修正を続行することができます。 
8.  項目の選択の各ページで、インポートするオブジェクトを選択します。 次の列が一覧表示されます。
    - **[名前]**: Configuration Manager オブジェクトの名前。 
    - **[Importable]\(インポート可能\)**: オブジェクトがインポート可能かどうかを指定します。 [Importable]\(インポート可能\) 列が [はい] になっているオブジェクトのみを選択できます。 
    - **[プラットフォーム]**: オブジェクトでサポートされるプラットフォームを指定します。
    - **[Already imported]\(インポート済み\)**: このコンピューターのツールを使用して、オブジェクトが既にインポートされているかどうかを指定します。 
    - **[Is superseded]\(置き換え\)** (アプリ): アプリが別のアプリに置き換えられるかどうかを指定します。 置き換え済みのアプリを表示するには、ページ上部にある **[Show superseded apps]\(置き換え済みのアプリを表示\)** チェック ボックスをオンにします。
    - **[Notes]\(備考\)**: オブジェクトをインポートできない理由に関する情報を提供します。 **[備考]** 列には、設定に関する無視された情報も表示されます (一部の種類のオブジェクトについて) が、オブジェクトはそれらの設定がなくてもインポート可能です。
    - **[構成基準]** (構成項目用): 構成項目に関連付けられている構成基準を指定します。
    - **[Required certificate]\(必要な証明書\)** (プロファイルとポリシー用): 証明書がオブジェクトに関連付けられているかどうかを指定します。 証明書がオブジェクトに関連付けられている場合は、証明書もインポートする必要があります。
9.  インポートするオブジェクトを選択すると、それらが [概要] ページに表示されます。 次の操作を実行できます。 
    - **[エクスポートの詳細]**: 画面に表示されている情報を含む .csv ファイルを作成します。 インポートできないオブジェクトとインポートできない理由も示します。 記録のため、このファイルを保持できます。 
    - **エラー データのエクスポート**: ツールが変換またはインポートできなかったデータに関する情報を含む圧縮ファイルをエクスポートします。 

### <a name="phase-3-import-selected-objects-to-intune"></a>フェーズ 3: 選択したオブジェクトを Intune にインポートする
フェーズ 3 では、Intune にサインインして、選択したオブジェクトをインポートします。 
10. **[次へ]** をクリックし、**[Sign in to Intune]\(Intune にサインインする\)** をクリックして、データ インポートのために Intune テナントにサインインするか、データのエクスポートを選択します。

    - **[エクスポート]**: インポートするサイト内のオブジェクトを検出および選択したら、データ セットにオブジェクトをエクスポートできます。 これにより、インターネットにアクセスできないコンピューターからオブジェクトを検出し、データをエクスポートした後で、そのデータをインターネットにアクセスできるコンピューターからインポートできます。 データ セットはログイン ユーザーの Windows ユーザー資格情報 を使用して暗号化されているため、データ セットをエクスポートしたユーザーだけが、ツールでデータ セットをインポートできます。 このオプションを選択する場合、エクスポートするデータへのパスを選択します。 
      1. **[Sign in to Intune]\(Intune にサインイン\)** ページにある **[エクスポート]** をクリックします。 
      2. **[参照]** をクリックして、エクスポート先のフォルダーを選択します。 フォルダーは空でなければいけません。 
      3. **[開始]** をクリックしてデータをエクスポートし、エクスポートが完了したら **[閉じる]** をクリックしてウィザードを完了して Data Importer を閉じます。
      4. インターネットにアクセスできる別のコンピューターから同じ資格情報を使用して Data Importer を開始し、ウィザードの 2 ページ目で **[Import previously exported data set]\(以前エクスポートされたデータ セットをインポート\)** を選択します。 データがインポートされたら、ウィザードは **[Sign in to Intune]\(Intune にサインイン\)** ページに移動します。 
    - **[Sign in to Intune]\(Intune にサインイン\)**: グローバル管理者アカウントまたは Intune 管理者アカウントでサインインする必要があります。 サインインすると、インポート プロセスが開始します。
    
      > [!Important]
      > 最初に試用版テナントを使用して、データ インポート プロセスをテストすることをお勧めします。 そして、意図したデータがインポートされていることを確認したら、実稼働の Intune テナントで同じプロセスを実行できます。
12. [進行状況] ページでは、オブジェクトのインポートの進行状況が提供されます。 インポートが完了したら、**[次へ]** をクリックします。 
13. [完了] ページに、インポートされたオブジェクトの一覧が表示されます。 インポート処理中にエラーが発生したすべてのオブジェクトの状態を確認します。 次の操作を実行できます。 
    - **詳細のエクスポート**: 画面に表示されている情報を含む .csv ファイルを作成します。 記録のため、このファイルを保持できます。 
    - **エラー データのエクスポート**: ツールが変換またはインポートできなかったデータに関する情報を含む圧縮ファイルをエクスポートします。

## <a name="next-steps"></a>次のステップ
Intune にデータをインポートしたら、[Intune でのユーザーの移行を準備する](migrate-prepare-intune.md)ステップを実行する必要があります。 