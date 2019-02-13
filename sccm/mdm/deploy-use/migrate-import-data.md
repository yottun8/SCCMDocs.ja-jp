---
title: Microsoft Intune へのデータのインポート
titleSuffix: Configuration Manager
description: Configuration Manager のデータの Microsoft Intune へのインポート
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.collection: M365-identity-device-management
ms.openlocfilehash: 46b5034cb95193a07421fe79a445dac0f5b28503
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124263"
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Configuration Manager のデータの Microsoft Intune へのインポート 

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*    

[ハイブリッド MDM のユーザーとデバイスを、クラウド専用構成の Intune スタンドアロンに移行する](migrate-hybridmdm-to-intunesa.md)プロセスの推奨される最初のフェーズは、Intune Data Importer ツールを使用することです。 このフェーズをスキップして [Intune でのユーザーの移行を準備する](migrate-prepare-intune.md)フェーズに進むこともできます。 ただし、このツールは、次のフェーズでの時間を大幅に節約できる、次の機能を実行します。  

1.  Configuration Manager 階層から選択したオブジェクトに関するデータを収集する。  

2.  インポートに選択できるオブジェクトに関する詳細と、一部のオブジェクトがインポートできない理由に関する情報を提供する。  

3.  選択したオブジェクトを Microsoft Intune テナントにインポートする。  

Data Importer ツールは、任意の方法で、Configuration Manager 環境に変更されません。 Intune にオブジェクトをインポートし、リスク、管理されていない状態で、ハイブリッド MDM のデバイスを保持するためのせず、期待どおりの動作をすべて確認できます。 


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
> デプロイのインポートは、インポートするその他のオブジェクトの種類にのみ役立ちます。 たとえば、VPN プロファイルとデプロイをインポートすると、選択した VPN プロファイルのデプロイのみをインポートできます。 Intune でのデプロイは、割り当てと呼ばれます。 以前にインポートしたオブジェクトのデプロイをインポートする場合は、そのオブジェクトをもう一度インポートするか、Azure の Intune で割り当てを手動で作成する必要があります。 たとえば、VPN プロファイルをインポートしてデプロイをインポートしない場合は、ツールを再度実行し、VPN プロファイルとデプロイを選択するか、Azure の Intune で割り当てを手動で作成する必要があります。 ツールを再実行すると、重複するオブジェクトが作成される場合があります。これは後で Azure の Intune で削除できます。  

> [!Important]  
> デプロイのコレクションは、Azure Active Directory (Azure AD) にレプリケートされた Active Directory グループに基づいている場合、ツールでツールを実行するときに、適切な展開を選択した場合、グループに移行されたオブジェクトが自動的に対象とします。 複雑なコレクションまたはダイレクト メンバシップのコレクションがある場合は、Azure AD で手動で再作成して手動でそれらを Azure での Intune でのオブジェクトの割り当てを対象する必要があります。  


## <a name="things-to-know-before-you-run-the-tool"></a>ツールを実行する前に知っておくべきこと

- ツールを実行すると、任意の方法で、Configuration Manager 環境は変更されません。  

- まず、試用版のテナントを使用して、データ インポート プロセスをテストします。 後にすることがインポートされているはずのデータ、進んでと同じプロセスで、実稼働の Intune テナントを確認します。  

- Data Importer は、Configuration Manager データを 1 回だけインポートすることを意図しています。 これの追跡も行いません Configuration Manager または Intune 内のオブジェクト。 ただし、実行する場合、インポーターもう一度同じコンピューターにする前に、確認しているオブジェクトを以前にインポートします。 ツールには、Intune にオブジェクトがまだ存在する場合、またはオブジェクトが変更された場合を認識しません。 Intune にデータを複数回インポートすると、オブジェクトが重複する場合があります。  

- すべてのプロファイル設定をインポートすることはできません。 たとえば、キオスク モードまたは PFX 設定をインポートすることはできません。  

- 、選択したプラットフォームに該当しない設定に Configuration Manager ポリシーがある場合、ツールは、インポート中にこれらの設定を無視する場合があります。 設定を無視することで、ポリシーをインポートして Intune でサポートされるようにすることができます。  

- ツールは、オブジェクトをインポートできない理由の理由を提供しようとします。 場合によっては、Intune にオブジェクトをインポートする前に、Configuration Manager コンソールに戻って、問題を修正し、Configuration Manager オブジェクトの検出スキャンをもう一度開始してから、オブジェクトをインポートすることができます。 Intune でこれらのオブジェクトを手動で再作成する必要がある場合があります。  

- 他のオブジェクトに依存しているいくつかのプロファイルがあります。 証明書に依存している電子メール プロファイルのように、別のオブジェクトに依存しているプロファイルをインポートする場合は、以前に一方のオブジェクトを同じコンピューターから同じユーザーでインポートしたことがない限り、同時に両方のオブジェクトをインポートする必要があります。  

- このツールの実行後、手動で追加の手順を実行する必要がある場合があります。 たとえば、アプリと Azure AD グループにポリシーを対象とします。  

- (Webclips とも呼ばれます) のすべての web アプリがユーザーに割り当てられている場合は、ユーザーを移行する前にこれらの web アプリを削除する必要があります。 移行が完了し、web アプリを再割り当てください。 この操作を実行しない場合は、web クリップが、移行後に管理できなくなります。  


## <a name="prerequisites"></a>[前提条件]

- 最上位サイトを指定し、サイト階層内のすべてのオブジェクトへのアクセスを持つユーザーでツールを実行します。 ツールは、ツールを実行しているユーザーがアクセスできるオブジェクトのみを検出します。  

- グローバル管理者は、初めて - GlobalConsent パラメーターを使用して Data Importer ツールを実行する必要があります。 グローバル管理者または Intune 管理者は、ツールを実行できます。 

- Windows 10 または Windows Server 2016 では、Data Importer ツールを実行します。


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->



## <a name="download-the-data-importer-tool"></a>Data Importer ツールのダウンロード

Data Importer ツールをからダウンロード、 **ConfigMgrTools/Intune-Data Importer** GitHub リポジトリ。 次の手順に従ってツールをダウンロードします。

1. [Intune Data Importer GitHub リリース](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases)のページに移動します。  

2. 最新のリリースについては、**Microsoft.Intune.Data.Importer.exe** をクリックします。  

3. 保存し、実行可能ファイルを実行します。 次に Intune Data Importer ツールを抽出する宛先フォルダーを選択します。  



## <a name="run-the-data-importer-tool"></a>Data Importer ツールの実行

Data Importer ツールのウィザードは、次の 3 つの主要なステップに分割できます。 このセクションでは、ウィザードの各セクションを完了し、Intune に Configuration Manager データを正常にインポートするのに役立つ情報を提供します。 各ステップは前のステップが終了したところからの続きです。


### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>リソースにアクセスするために Data Importer ツールにアクセス許可を付与する

Data Importer ツールを実行するには、事前にグローバル管理者アカウントを使用して、リソースにアクセスするためのアクセス許可を Azure の Data Importer ツールに付与する必要があります。 グローバル管理者または Intune 管理者アカウントを使用して、ツールを実行できます。   

1.  グローバル管理者では、次のパラメーターを使用して初めてツールを実行する必要があります。 `IntuneDataImporter.exe -GlobalConsent`  

2. ツールの開始時に、Azure でグローバル管理者ロールを持つアカウントを使用してサインインします。  

3. 選択**Accept** Microsoft Graph で適切な権限を持つ Azure でアプリケーションを作成します。 Data Importer ツールでは、オブジェクトを Microsoft Intune にインポートするためにこれらの権限が必要です。  

    > [!Important]  
    > このプロンプトに同意する場合は、次の操作を行うツールのアクセス許可を付与します。  
    > - すべてのグループを読み取る  
    > - サインインしてユーザー プロファイルを読み取る  
    > - Intune デバイスの構成とポリシーの読み書き  
    > - Intune アプリの読み書き  
    > - Intune ロール ベース管理制御ポリシーの読み書き  
    > - Intune デバイスの読み書き  
    > - Intune 構成の読み書き  

4. 同意すると、他のグローバル管理者または Intune 管理者がツールを実行して、Configuration Manager からデータを Azure の Intune にインポートできます。  

> [!Note]  
> ツールのグローバル管理者が同意を受け入れて最初場合は、次のエラーが、Intune 管理者に表示可能性があります。**このアプリケーションにアクセスすることはできません**します。  


### <a name="manually-map-collections-to-azure-ad-groups"></a>Azure AD グループにコレクションを手動でマップする

Data Importer ツールを実行すると、1 つの Active Directory グループを対象とする単一のルールのコレクションから Active Directory のグループ名を抽出します。 Intune で割り当てが作成されると、Data Importer は、Active Directory グループと同じ名前で Azure AD グループを検索します。 存在する場合、ツールは、その Azure AD グループにインポートしたオブジェクトを割り当てます。 

コレクションの Data Importer を検索する Active Directory のグループ名をオーバーライドし、そのコレクションに使用する 1 つまたは複数の Azure AD グループを指定できます。 コレクション マッピング ファイルを使用すると、通常 Data Importer ではインポートできないコレクションを Azure AD グループにマップできます。 

#### <a name="find-the-collections-that-cant-be-imported"></a>インポートできないコレクションを検索します。
インポートできないすべてのコレクションの一覧を取得して、それらをコレクション マッピングの .csv ファイルに追加できます。 

1. Data Importer ツールを実行し、インポートするオブジェクトを選択します。 プロシージャを使用して[フェーズ 1。Configuration Manager オブジェクトを検出し、データを収集](#phase-1:-discover-configuration-manager-objects-and-collect-data)と[フェーズ 2。問題を解決し、インポートするオブジェクトを選択します。](#phase-2:-resolve-issues-and-select-the-objects-to-import)を検出し、オブジェクトを選択します。 次に **[概要]** ページで、**[エクスポートの詳細]** を選択して .csv ファイルを作成します。このファイルには、インポートできないオブジェクトやデプロイなどの、インポートに選択したすべての詳細が含まれます。  

2. Microsoft Excel で .csv ファイルを開き、**[種類]** 列に **[デプロイ]**、**[Importable]\(インポート可能\)** 列に **[いいえ]** を指定してデータをフィルター処理します。 コレクション名の列には、デプロイをインポート可能にするためにコレクション マッピング ファイルに追加する必要があるすべてのコレクションが示されます。  

#### <a name="create-the-collection-mapping-file"></a>コレクション マッピング ファイルを作成する
コレクション マッピング ファイルはコンマ区切り値 (CSV) ファイルで、最初の列が Configuration Manager コレクションの名前で、2 番目の列がそのコレクションに使用する Azure AD グループの名前です。 1 つの Configuration Manager コレクションに複数の Azure AD グループを指定するには、そのコレクション名の CSV ファイルに複数の行を作成します。 次の例は、2 つのコレクションを含む CSV ファイルです。 最初のコレクションは 1 つの Azure AD グループにマップされ、2 つ目のコレクションは 2 つの Azure AD グループにマップされます。

![コレクション マッピング CSV ファイルの例](../media/migrate-collectionmapping.png)

#### <a name="start-the-data-importer-tool-using-collection-mapping"></a>コレクション マッピングを使用して Data Importer ツールを起動する
コレクション マッピング ファイルを使用するには、**-CollectionMappingFile** コマンド ライン パラメーターおよび作成するコレクション マッピング .csv ファイルへの完全パスを使用して、Data Importer ツールを起動する必要があります。 次に例を示します。

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]  
> Data Importer は何もコレクション マッピング ファイルが読み込まれたことを示す任意のウィザード ページに表示されません。 ただし、.csv ファイルの読み取り中に発生したエラーはすべて表示されます。 
> 
> また、ウィザードの **[概要]** ページで、**[デプロイ]** の種類を確認できます。 ツールでは、インポート可能な列に **[はい]** が表示され、**[備考]** 列にはオブジェクトに割り当てる Azure AD グループが一覧表示されます。  


### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>フェーズ 1:Configuration Manager オブジェクトを検出して、データの収集

フェーズ 1 では、検出するオブジェクトを選択し、選択したオブジェクトに関する情報をツールに収集させます。 

1. ツールを開き、選択**開始**します。  

2. クリックして、情報を読んで**次**します。  

3. 以前にエクスポートされたデータ セットをインポートする、または、インポートするオブジェクトの種類を選択する、のいずれかを選択します。  

    - **インポートのデータ セットは、Intune Data Importer の以前の実行からエクスポートされた**:選択**参照**の**エクスポートされたデータ フォルダー**します。 Data Importer ツールを使用して、以前エクスポートしたデータ セットを選択します。 データ セットをインポートするユーザーは、そのデータをエクスポートしたユーザーと同じである必要があります。 データをインポートしたら、オブジェクトの概要がウィザードの **[概要]** ページに一覧表示されます。 場合は、概要が正確で、[フェーズ 3。Intune を選択したオブジェクトをインポート](#phase-3-import-selected-objects-to-intune)します。  

        > [!Note]  
        > インポートするサイト内のオブジェクトを検出および選択したら、ウィザードの **[Sign-in to Intune]\(Intune にサインイン\)** ページでデータ セットにオブジェクトをエクスポートできます。 それが終わるとこのページでデータ セットをインポートできます。 そのため、サインイン ユーザーの Windows ユーザー資格情報を使用して、データ セットを暗号化だけで、データ セットをエクスポートするユーザーがツールでデータ セットをインポートできます。  

    - **インポートするオブジェクトの種類を選択します**:。インポートする、サイトとオブジェクトに関する次の情報を提供します。  

        - **サイト サーバー名**:オブジェクトをインポートするサイト サーバーの完全修飾ドメイン名を提供します。 ツールは、ツールを実行しているユーザーがアクセスできるオブジェクトのみを検出します。 通常、最上位サイトを指定し、サイト階層内のすべてのオブジェクトへのアクセス権を持つユーザーでツールを実行します。  

        - **サイト コード**:サイト サーバーのサイト コードを提供します。 この 3 文字のコードは、Configuration Manager コンソールの上部にあります。  

        - **インポートするオブジェクトの種類**:ツールに収集するオブジェクトを選択します。 **[すべて選択]** を選択してすべてのオブジェクトを選択するか、個々のオブジェクトの種類を選択することができます。  

4.  選択**次**サイトでオブジェクトの検出を開始します。 ツールに各オブジェクトの種類の進行状況が表示されます。  

    - ツールで選択したオブジェクトの種類のデータが検出されない場合は、進行状況バーにすぐにそのオブジェクトの種類に対して完了が表示されます。  

    - 選択していないオブジェクトを表示しない、**収集**データ ページ。  

    - 収集されなかったオブジェクト用にもう一度ツールまたはコレクションの処理中にキャンセルされたことを行うことができます。  


### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>フェーズ 2:問題を解決し、インポートするオブジェクトを選択します。  

フェーズ 2 では、ツールで検出されたオブジェクトを確認し、オブジェクトが Intune にインポートされることを妨げている問題を解決し、インポートするオブジェクトを選択します。 問題を修正した場合に戻って、 **Discover 環境**オブジェクトを検出し、ウィザードのページ。 

1. **[次へ]** をクリックして、収集されたオブジェクトを確認します。 項目の選択ページは、収集されたオブジェクトの種類ごとに使用できます。  
   <!--   > [!Tip]     
   > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
   > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
   > - Objects are always grouped under their parent item even when you sort or filter the objects.
   -->
2. 各項目の選択 ページで、オブジェクトを並べ替える、 **Importable**列とインポートできないオブジェクトを確認します。 内の情報、**ノート**列は、ツールが、オブジェクトをインポートできません理由の詳細を提供します。  

3. インポートを可能なオブジェクトの問題を修正するかどうかを決定します。 1 つまたは複数の問題を修正する場合は、選択**前**構成マネージャー ページから、データが表示されるまでです。 問題を解決するかどうかを確認するには、もう一度データを収集します。 移植性がないオブジェクトが完成したらまで問題を修正する続行することができます。  

4. 項目の選択の各ページで、インポートするオブジェクトを選択します。 次の列が一覧表示されます。  

    - **名前**:Configuration Manager オブジェクトの名前。  

    - **インポート可能な**:オブジェクトをインポートできるかどうかを指定します。 [Importable]\(インポート可能\) 列が [はい] になっているオブジェクトのみを選択できます。  

    - **プラットフォーム**:オブジェクトによってサポートされるプラットフォームを指定します。  

    - **既にインポート**:このコンピューターでツールを使用して、オブジェクトが既にインポートされているかどうかを指定します。  

    - **置き換えられる**(アプリ) 用。アプリが別のアプリに置き換えられるかどうかを指定します。 選択、**表示アプリの置き換え**置き換え済みのアプリを表示するページの上部にあるオプション。  

    - **ノート**:オブジェクトをインポートできない理由に関する情報を提供します。 **[備考]** 列には、設定に関する無視された情報も表示されます (一部の種類のオブジェクトについて) が、オブジェクトはそれらの設定がなくてもインポート可能です。  

    - **構成基準**(構成項目) の場合。構成項目に関連付けられている構成基準を指定します。  

    - **必要な証明書**(プロファイルとポリシー) 用。証明書は、オブジェクトに関連付けられているかどうかを指定します。 証明書がオブジェクトに関連付けられている場合は、証明書もインポートする必要があります。  

5. インポートするオブジェクトを選択すると、[概要] ページに表示されます。 次の操作を実行できます。  

    - **エクスポートの詳細**:画面に表示される情報を含む .csv ファイルを作成します。 示しますインポートできないオブジェクト、および理由を理由に、インポートできません。 記録のため、このファイルを保持できます。  

    - **エラー データのエクスポート**:ツールが変換またはインポートできなかったデータに関する情報を含む圧縮ファイルをエクスポートします。  


### <a name="phase-3-import-selected-objects-to-intune"></a>フェーズ 3:選択したオブジェクトを Intune にインポートします。

フェーズ 3 では、Intune にサインインし、選択したオブジェクトをインポートします。 

1. 選択**次**、次のオプションのいずれかを選択します。  

    - **エクスポート**:検出、インポートするサイト内のオブジェクトを選択して後、は、データ セットにオブジェクトをエクスポートできます。 これにより、データをエクスポートし、インターネットにアクセスできるコンピューターからデータをインポートし、インターネット アクセスがないコンピューターからオブジェクトを検出することができます。 そのため、サインイン ユーザーの Windows ユーザー資格情報を使用して、データ セットを暗号化だけで、データ セットをエクスポートするユーザーがツールでデータ セットをインポートできます。 このオプションを選択する場合、エクスポートするデータへのパスを選択します。  

        1. 選択**エクスポート**上、 **Intune にサインインする**ページ。  

        2. 選択**参照**エクスポート先のフォルダーを選択します。 フォルダーは空でなければいけません。  

        3. 選択**開始**にデータをエクスポートします。 エクスポートが完了したら、選択**閉じます**ウィザードを完了し、Data Importer を閉じます。  

        4. 別のコンピューターからインターネットにアクセスできる、同じ資格情報を使用して Data Importer を起動します。 選択**以前エクスポートされたデータ セットをインポート**ウィザードの 2 ページ目にします。 データがインポートされたら、ウィザードは **[Sign in to Intune]\(Intune にサインイン\)** ページに移動します。  

    - **Intune にサインインする**:グローバル管理者または Intune 管理者アカウントでサインインします。 サインインすると、インポート プロセスが開始します。  

        > [!Important]  
        > まず、試用版のテナントを使用して、データ インポート プロセスをテストします。 後にすることがインポートされているはずのデータ、進んでと同じプロセスで、実稼働の Intune テナントを確認します。  

2. [進行状況] ページでは、オブジェクトのインポートの進行状況が提供されます。 インポートが完了したら、**[次へ]** をクリックします。  

3. [完了] ページに、インポートされたオブジェクトの一覧が表示されます。 インポート処理中にエラーが発生したすべてのオブジェクトの状態を確認します。 次の操作を実行できます。  

    - **エクスポートの詳細**:画面に表示される情報を含む .csv ファイルを作成します。 記録のため、このファイルを保持できます。  

    - **エラー データのエクスポート**:ツールが変換またはインポートできなかったデータに関する情報を含む圧縮ファイルをエクスポートします。  



## <a name="next-steps"></a>次のステップ

Intune にデータをインポートした後[Intune ユーザーの移行を準備する](migrate-prepare-intune.md)します。 
