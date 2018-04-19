---
title: Security Content Automation Protocol (SCAP) 拡張機能をインストールし、構成する
titleSuffix: System Center Configuration Manager
description: Security Content Automation Protocol (SCAP) 拡張機能をインストールし、構成する
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 03fc9fa9f82aeae8ab22d6b4c3fa7858e93401cc
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-configure-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Microsoft System Center Configuration Manager の SCAP 拡張機能をインストールして構成します

*適用対象: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> この機能は、Technical Preview バージョン 1803 で[プレリリース機能](/sccm/core/servers/manage/pre-release-features)として初めて導入されました。 プレリリース版の SCAP 拡張機能は、現在サポートされているバージョンの Configuration Manager Current Branch と LTSB 1606 にインストールできます。 1803 Technical Preview 以降のインストール ファイルは cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi にあります。   

前提条件となるインフラストラクチャの準備ができたら、このプロセスを実行するコンピューターに Microsoft System Center Configuration Manager の SCAP 拡張機能をインストールして構成できます。

## <a name="install-scap-extensions-configuration-manager"></a>SCAP 拡張機能 Configuration Manager のインストール

1. ConfigMgr\_Extensions\_for\_SCAP.msi を実行してツールをインストールします。
2. Windows エクスプローラーで、**ConfigMgr\_Extensions\_for\_SCAP.msi** ファイルをダウンロードしたフォルダーに移動して、**ConfigMgr\_Extensions\_for\_SCAP.msi** ファイルをダブルクリックします。 Microsoft System Center Configuration Manager の SCAP 拡張機能のインストール ウィザードが起動します。

次の表内の情報を使用し、指定する必要がない場合はウィザードの既定値をそのまま選択し、**Microsoft System Center Configuration Manager の SCAP 拡張機能のインストール ウィザード**を完了します。

**表 1.0** Microsoft System Center Configuration Manager の SCAP 拡張機能のインストール ウィザード プロセス

| ウィザードのページ名 | ユーザーの操作 |
| --- | --- |
| ようこそとエンド ユーザー使用許諾契約 |1.使用許諾契約書を確認します|
| ようこそとエンド ユーザー使用許諾契約|2.**[使用許諾契約書に同意します]** をクリックします。|
| ようこそとエンド ユーザー使用許諾契約|3.**[インストール]** をクリックします。|
| Microsoft System Center Configuration Manager の SCAP 拡張機能のインストール ウィザードを実行します。 |4.**[完了]**をクリックします。|
 



Microsoft System Center Configuration Manager の SCAP 拡張機能のインストール ウィザードは、既定で、Configuration Manager コンソール インストール フォルダーに拡張機能をインストールします。



## <a name="download-and-install-the-scap-data-stream-files"></a>SCAP データ ストリーム ファイルのダウンロードとインストール

SCAP 拡張機能を実行して SCAP データ ストリーム ファイルを変換してから、それらをコンプライアンス設定機能にインポートするには、Web サイトの National Vulnerability Database (NVD) [ダウンロード ページ](http://nvd.nist.gov/fdcc/download_fdcc.cfm)から SCAP データ ストリーム ファイルをダウンロードする必要があります。 次に、それらを SCAP 拡張機能をインストールしたフォルダーにコピーします。

環境によっては、ダウンロード ページに一覧表示された SCAP データ ストリーム ファイルのすべてが必要ではない場合があります。

SCAP データ ストリームをインストールするには:

1. [NVD Web サイト](http://nvd.nist.gov/) にアクセスして、組織に必要な SCAP データ ストリームを特定します。
NIST によって発行された SCAP データ ストリームは、_チェックリスト_とも呼ばれる複数のバンドルに編成されます。

2. [NVD Web サイト](http://nvd.nist.gov/home.cfm)から SCAP データ ストリームをダウンロードします。このデータ ストリームは、.zip ファイル名拡張子付きの圧縮ファイルに保存されているか、DataStream XML ファイルとしてマークされています。

    >[!IMPORTANT] 
    >NVD からダウンロード可能な .xml 拡張子付きの SCAP データ ストリーム ファイルは数多くあります。 ただし、XCCDF (SCAP1.0 と 1.1)/DataStream (SCAP1.2) コンテンツを含む .xml ファイルだけが SCAP 拡張機能での使用に適しています。

3. SCAP 拡張機能をインストールしたフォルダーと同じフォルダーに、ダウンロードした SCAP データ ストリーム .zip ファイル/DataStream XML を解凍します。

## <a name="convert-and-import-the-scap-data-stream-files-using-the-import-scap-content-wizard"></a>SCAP コンテンツのインポート ウィザードを利用し、SCAP データ ストリーム ファイルを変換し、インポートする

SCAP データ ストリームを取得したら、データ ストリームを構成基準にインポートし、変換する準備は完了です。 NIST によって発行された SCAP データ ストリームは複数のバンドルに編成されます。 NIST の指示に従って、環境内で使用するバンドルを確認します。 たとえば、Windows の各バージョン固有のバンドル、ファイアウォール構成用の別のバージョン固有のバンドルや Internet Explorer 8.0 用のバンドルがあります。 次の手順を使用してこのタスクを完了します。

### <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>SCAP データ ストリームを Configuration Manager にインポートするには

1. 構成基準のリボンから SCAP コンテンツのインポート ウィザードを起動します。

     ![CI 基準リボンから SCAP コンテンツのインポート ウィザードを起動する](./media/import-scap-content.png)

2. コンテンツの種類を選択します。

      ![コンテンツの種類を選択する](./media/import-new-scap-content.png)

3. SCAP データストリーム ファイル、XCCDF、CPE ディクショナリ ファイル、または OVAL コンテンツ ファイルを選択します。

     ![SCAP データストリーム ファイルを選択する](./media/select-datastream-file.png)

4. SCAP 1.2 の場合、データストリームを選択します。 次に、SCAP 1.x のベンチマークとプロファイルを選択します。  **[次へ]** を選択し、コンテンツを変換します。 進行状況バーが表示されます。

      ![SCAP 1.2 のベンチマークとプロファイルを選択する](./media/select-benchmark-and-profile.png)

5. インポートする構成データを確認します。

      ![構成確認のスクリーンショット](./media/confirm-configuration.png)

6. **[次へ]** をクリックし、構成データをインポートします。

      ![インポートの完了](./media/complete-import.png)

## <a name="alternate-method-convert-and-import-the-scap-data-stream-files-using-the-cmd-line-tool"></a>(代替方法) コマンド ライン ツールを利用し、SCAP データ ストリーム ファイルを変換し、インポートします。

SCAP データ ストリームを取得したら、Microsoft.Sces.ScapToDcm.exe ツールを利用し、SCAP データ ストリームをコンプライアンス設定準拠の .cab ファイルに変換できます。 次に、.cab ファイルを Configuration Manager にインポートします。 Microsoft.Sces.ScapToDcm.exe ツールによって、Configuration Manager のコンプライアンス設定機能を使用してアクセス可能な構成項目と構成基準に SCAP データ ストリームが変換されます。 Microsoft.Sces.ScapToDcm.exe ツールによって、SCAP データ ストリームが XML マニフェストに変換されます。 それから、XML マニフェストがパッケージ化され、Configuration Manager にインポートできる .cab ファイルが生成されます。

NIST によって発行された SCAP データ ストリームは複数のバンドルに編成されます。 NIST の指示に従って、環境内で使用するバンドルを確認します。 たとえば、Windows の各バージョン固有のバンドル、ファイアウォール構成用の別のバージョン固有のバンドルや Internet Explorer 8.0 用のバンドルがあります。 次の手順を使用してこのタスクを完了します。





## <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>SCAP データ ストリームを Configuration Manager にインポートするには

1. SCAP データ ストリームをコンプライアンス設定に準拠した .cab ファイルに変換します。
2. .cab ファイルを Configuration Manager にインポートします。

### <a name="convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files"></a>SCAP データ ストリームからコンプライアンス設定に準拠した .cab ファイルへの変換

システムのコンプライアンスを分析して評価する前に、XML 形式の SCAP データ ストリームをコンプライアンス設定の構成項目と構成基準に準拠している XML マニフェストに変換する必要があります。 Microsoft.Sces.ScapToDcm.exe ツールによって、SCAP データ ストリームが XML マニフェストに変換されます。 それから、XML マニフェストがパッケージ化され、後で Configuration Manager にインポートできる .cab ファイルが生成されます。

#### <a name="to-convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files-using-the-microsoftscesscaptodcmexe-tool"></a>**Microsoft.Sces.ScapToDcm.exe ツールを使用して、SCAP データ ストリームをコンプライアンス設定に準拠した .cab ファイルに変換するには**

コマンド プロンプトで、AdminConsole\Bin フォルダーに移動し、Microsoft.Sces.ScapToDcm.exe を実行してコンプライアンス設定に準拠した cab を生成し、それを Configuration Manager サイトにインポートします。

   >[!NOTE] 
   > 出力フォルダーの読み取り/書き込みアクセス許可をアカウントに与える必要があります

**SCAP 1.0/1.1 コンテンツ (USGCB や DISA コンテンツなどの XCCDF XML ファイル) の場合:**

 Microsoft.Sces.ScapToDcm.exe –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt; -out &lt;outputFolder&gt; [-select benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   >–select パラメーターを使用してベンチマーク/プロファイルを指定しなかった場合は、ツールがコンテンツ ファイル内のベンチマークごとに DCM cab を生成します。

**SCAP1.2 コンテンツ (最新の USGCB コンテンツなどの DataStream XML ファイル) の場合:**

Microsoft.Sces.ScapToDcm.exe –scap &lt;scapdatastreamfile.xml&gt; -out &lt;outputFolder&gt; [-select datastream/benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   > –select パラメーターを使用してデータストリーム/ベンチマーク/プロファイルを指定しなかった場合は、ツールがコンテンツ ファイル内のベンチマークごとに DCM cab を生成します。

**外部変数を含む単一の OVAL ファイルの場合:**

Microsoft.Sces.ScapToDcm.exe –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;] -out &lt;outputFolder&gt; [-log LogFileName]

   >[!NOTE] 
   > 外部変数ファイル内で 1 つの変数に対して複数の値が存在する場合、Microsoft.Sces.ScapToDcm.exe ツールは値をこの変数の配列として扱います。



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Microsoft.Sces.ScapToDcm.exe. コマンドライン パラメーター

| **パラメーター** | **使用方法** | **必須** |
| --- | --- | --- |
| -scap [scap data stream file] | SCAP データ ストリームのファイルを指定します。 | はい (SCAP 1.2 データ ストリームの場合、-xccdf と -oval / -variable で相互に排他的) |
| -xccdf [xccdf file] | XCCDF ファイルを指定します。 | はい (SCAP 1.0/1.1 XCCDF の場合、-scap と -oval / -variable で相互に排他的) |
| -cpe [cpe file] | CPE ファイルを指定します。 | はい (SCAP 1.0/1.1 XCCDF の場合、-scap と -oval / -variable で相互に排他的) |
| -oval [oval file] | OVAL ファイルを指定します。 | はい (スタンドアロン OVAL ファイルの場合、-xccdf と -scap で相互に排他的) |
| -variable [oval external variable file] | OVAL 外部変数ファイルを指定します。 | いいえ (外部 OVAL 変数ファイルが存在する場合のスタンドアロン OVAL ファイルに対しては任意、-xccdf と -scap で相互に排他的) |
| -select [xccdf benchmark/profile] | SCAP データ ストリームと XCCDF ファイルのどちらかから、XCCDF ベンチマークまたはプロファイルを選択します。 | いいえ (このスイッチを指定することをお勧めします。 指定しなかった場合、ツールはすべての組み込みデータ ストリーム/ベンチマークですべてのプロファイルに対して 1 つの cab を生成します) |
| -out [output directory] | DCM cab ファイルを出力する場所を指定します。 | いいえ (指定しなかった場合、ツールは変換せずにコンテンツを一覧表示するだけです) |
| -log [log file] | ログ ファイルを指定します。 | いいえ (指定しなかった場合、Microsoft.Sces.ScapToDcm.log ファイルにログが書き込まれます) |
| -help / -? | ツールの使用方法を出力します。 | いいえ |





#### <a name="the-following-command-lines-are-samples-for-the-microsoftscesscaptodcmexe-tool"></a>次のコマンド ラインは、Microsoft.Sces.ScapToDcm.exe ツールのサンプルです。

**SCAP1.2 Content:**

  Microsoft.Sces.ScapToDcm.exe –scap scap\_gov.nist\_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID

**SCAP1.0/1.1 Content:**

   Microsoft.Sces.ScapToDcm.exe–xccdf scap\_gov.nist\_Test-WinXP\_xccdf.xml –cpe scap\_gov.nist\_Test-WinXP\_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID

**SCAP OVAL Content:**

  Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder

**次の出力は Microsoft.Sces.ScapToDcm.exe ツールからのサンプルです。**

  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Process XCCDF Benchmark xccdf\_tst.bvt\_benchmark\_Windows-F

  Process XCCDF Profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0-BVT Profile #1

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml Process SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip SCAP Data Stream: [scap\_tst.bvt\_datastream\_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml] Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf\_tst.bvt\_benchmark\_Windows-F]

  Version:       [v1.0.0.0] Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf\_tst.bvt\_profile\_version\_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip

  Processing CPE dictionary: scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0 into DCM baseline xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

## <a name="next-step"></a>次のステップ
> [!div class="nextstepaction"]
> [SCAP コンプライアンス設定をインポートし、コンプライアンス結果をエクスポートする](/sccm/compliance/plan-design/scap/import-scap-compliance-settings)
