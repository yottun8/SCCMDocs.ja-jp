---
title: SCAP 拡張機能のインストールと構成
titleSuffix: Configuration Manager
description: Configuration Manager の Security Content Automation Protocol (SCAP) 拡張機能をインストールし、構成します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4fd440905bb736dfbfac01de804373d29c9fbb59
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384616"
---
# <a name="install-and-configure-the-scap-extensions-for-configuration-manager"></a>Configuration Manager の SCAP 拡張機能のインストールと構成

*適用対象: System Center Configuration Manager (Current Branch)*

[インフラストラクチャの準備](/sccm/compliance/plan-design/scap/about-scap#bkmk_prepare)ができたら、このプロセスを実行するコンピューターに Configuration Manager の SCAP 拡張機能をインストールして構成できます。



## <a name="bkmk_install"></a> SCAP 拡張機能のインストール

インストール ファイルは、Configuration Manager サイト サーバーのインストール ディレクトリ内の次のパスにあります。  
`cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi`

1. このプロセスを実行する Configuration Manager コンソールがあるコンピューターに **ConfigMgrExtensionsforSCAP.msi** をコピーします。  

2. Windows エクスプローラーで、**ConfigMgrExtensionsforSCAP.msi** をコピーしたフォルダーに移動します。 ファイルをダブルクリックして開き、Configuration Manager のインストール ウィザードの SCAP 拡張機能を開始します。  

3. 使用許諾契約書を確認します。 **[使用許諾契約書に同意します]** をクリックし、**[インストール]** をクリックします。  

4. インストールが完了したら、**[完了]** をクリックしてインストール ウィザードを終了します。  

インストール ウィザードでは、Configuration Manager コンソールのインストール フォルダーに SCAP 拡張機能がインストールされます。 既定では、コンソールのインストール フォルダーは `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole` です。  



## <a name="bkmk_scap-data-stream-files"></a> SCAP データ ストリーム ファイルのダウンロードとインストール

SCAP 拡張機能を実行する前に、National Vulnerability Database (NVD) の[ダウンロード ページ](https://csrc.nist.gov/Projects/United-States-Government-Configuration-Baseline)から SCAP データ ストリーム ファイルをダウンロードする必要があります。 次に、SCAP 拡張機能をインストールしたフォルダーにそれらをコピーします。

環境によっては、ダウンロード ページに一覧表示された SCAP データ ストリーム ファイルのすべてが必要ではない場合があります。

### <a name="install-the-scap-data-streams"></a>SCAP データ ストリームのインストール

1. [NVD Web サイト](http://nvd.nist.gov/) にアクセスして、組織に必要な SCAP データ ストリームを特定します。
NIST によって発行された SCAP データ ストリームは、_チェックリスト_とも呼ばれる複数のバンドルに編成されます。  

2. [NVD Web サイト](http://nvd.nist.gov/home.cfm)から SCAP データ ストリームをダウンロードします。このデータ ストリームは、.zip ファイル名拡張子付きの圧縮ファイルに保存されているか、DataStream XML ファイルとしてマークされています。  

    > [!IMPORTANT]  
    > NVD からダウンロード可能な .xml 拡張子付きの SCAP データ ストリーム ファイルは数多くあります。 ただし、XCCDF (SCAP1.0 と 1.1)/DataStream (SCAP1.2) コンテンツを含む .xml ファイルだけが SCAP 拡張機能での使用に適しています。  

3. SCAP 拡張機能をインストールしたフォルダーと同じフォルダーに、ダウンロードした SCAP データ ストリーム .zip ファイル/DataStream XML ファイルを抽出します。  



## <a name="bkmk_convert-and-import"></a> SCAP データ ストリーム ファイルの手動での変換とインポート 

SCAP データ ストリームを取得したら、データ ストリームを構成基準にインポートし、変換する準備は完了です。 NIST によって発行された SCAP データ ストリームは複数のバンドルに編成されます。 NIST の指示に従って、環境内で使用するバンドルを確認します。 たとえば、Windows の各バージョン固有のバンドル、ファイアウォール構成用の別のバージョン固有のバンドルや Internet Explorer 用のバンドルがあります。 次の手順を使用してこのタスクを完了します。  

> [!Note]  
> このセクションでは、Configuration Manager コンソールを使ってデータ ストリーム ファイルを変換およびインポートする手動プロセスについて説明します。 このプロセスを自動化するには、次の「[SCAP データ ストリーム ファイルの自動での変換とインポート](#bkmk_auto-convert-and-import)」のセクションを参照してください。  

1. 構成基準グループのリボンで **[SCAP コンテンツのインポート]** ウィザードをクリックします。

     ![コンソールのリボンの [SCAP コンテンツのインポート]](./media/import-scap-content.png)

2. SCAP コンテンツのオプションを選択します。

      ![インポート ウィザードの SCAP コンテンツ オプションの選択ページ](./media/import-new-scap-content.png)

3. SCAP データストリーム ファイル、XCCDF、CPE ディクショナリ ファイル、または OVAL コンテンツ ファイルを選択します。

     ![SCAP データストリーム ファイルを選択する](./media/select-datastream-file.png)

4. SCAP 1.2 の場合は、データストリームを選択します。 次に、SCAP 1.x のベンチマークとプロファイルを選択します。 **[次へ]** をクリックしてコンテンツを変換します。 

      ![SCAP 1.2 のベンチマークとプロファイルを選択する](./media/select-benchmark-and-profile.png)

      > [!Tip]  
      > ウィザードのこのページには、同じプロセスを自動化する **ScapToDcm.exe** ツールで使用するコマンド ラインが表示されます。  

5. インポートする構成データを確認します。

      ![構成確認のスクリーンショット](./media/confirm-configuration.png)

6. **[次へ]** をクリックして構成データをインポートします。

      ![インポートの完了](./media/complete-import.png)



## <a name="bkmk_auto-convert-and-import"></a> SCAP データ ストリーム ファイルの自動での変換とインポート 

### <a name="import-with-the-command-line-tool"></a>コマンドライン ツールを使用してエクスポートする

SCAP データ ストリームを取得したら、**Microsoft.Sces.ScapToDcm.exe** ツールを利用し、SCAP データ ストリームをコンプライアンス設定準拠の .cab ファイルに変換できます。 次に、.cab ファイルを Configuration Manager にインポートします。 Microsoft.Sces.ScapToDcm.exe ツールによって、Configuration Manager で使用できる構成項目と構成基準に SCAP データ ストリームが変換されます。 Microsoft.Sces.ScapToDcm.exe ツールによって、SCAP データ ストリームが XML マニフェストに変換されます。 それから、XML マニフェストがパッケージ化され、Configuration Manager にインポートできる .cab ファイルが生成されます。

> [!Tip]  
> 前のセクションの手動プロセスの手順 4 では、同じプロセスを自動化する **ScapToDcm.exe** ツールで使用するコマンド ラインを表示するウィザードのページが示されています。  


#### <a name="use-microsoftscesscaptodcmexe-to-convert-scap-data-streams-into-cab-files"></a>Microsoft.Sces.ScapToDcm.exe を使用して、SCAP データ ストリームを .cab ファイルに変換します

コマンド プロンプトで、**AdminConsole\Bin** フォルダーに移動し、**Microsoft.Sces.ScapToDcm.exe** を実行します。 このツールは、コンプライアンスの設定に準拠した .cab ファイルを生成し、Configuration Manager サイトにインポートします。

   > [!NOTE]  
   > 出力フォルダーに対する読み取り/書き込みアクセス許可がアカウントに必要です。

**SCAP 1.0/1.1 コンテンツ (USGCB や DISA コンテンツなどの XCCDF XML ファイル) での使用方法:**  

`Microsoft.Sces.ScapToDcm.exe –xccdf <xccdf.xml> -cpe <cpe.xml> -out <outputFolder> [-select benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > `–select` パラメーターを使用してベンチマーク/プロファイルを指定しなかった場合は、ツールがコンテンツ ファイル内のベンチマークごとに .cab ファイルを生成します。  

**SCAP1.2 コンテンツ (最新の USGCB コンテンツなどの DataStream XML ファイル) での使用方法:**  

`Microsoft.Sces.ScapToDcm.exe –scap <scapdatastreamfile.xml> -out <outputFolder> [-select datastream/benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > `–select` パラメーターを使用してデータストリーム/ベンチマーク/プロファイルを指定しなかった場合は、ツールがコンテンツ ファイル内のベンチマークごとに .cab ファイルを生成します。

**外部変数を含む単一の OVAL ファイルでの使用方法:**  

`Microsoft.Sces.ScapToDcm.exe –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputFolder> [-log LogFileName]`  

   > [!NOTE]  
   > 外部変数ファイル内で 1 つの変数に対して複数の値が存在する場合、Microsoft.Sces.ScapToDcm.exe ツールは値をこの変数の配列として扱います。  



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Microsoft.Sces.ScapToDcm.exe コマンド ライン パラメーター

| パラメーター | 使用方法 | 必須 |
| --- | --- | --- |
| `-scap [scap data stream file]` | SCAP データ ストリームのファイルを指定します。 | はい (SCAP 1.2 データ ストリームの場合、-xccdf と -oval / -variable で相互に排他的) |
| `-xccdf [xccdf file]` | XCCDF ファイルを指定します。 | はい (SCAP 1.0/1.1 XCCDF の場合、-scap と -oval / -variable で相互に排他的) |
| `-cpe [cpe file]` | CPE ファイルを指定します。 | はい (SCAP 1.0/1.1 XCCDF の場合、-scap と -oval / -variable で相互に排他的) |
| `-oval [oval file]` | OVAL ファイルを指定します。 | はい (スタンドアロン OVAL ファイルの場合、-xccdf と -scap で相互に排他的) |
| `-variable [oval external variable file]` | OVAL 外部変数ファイルを指定します。 | いいえ (外部 OVAL 変数ファイルが存在する場合のスタンドアロン OVAL ファイルに対しては任意、-xccdf と -scap で相互に排他的) |
| `-select [xccdf benchmark/profile]` | SCAP データ ストリームと XCCDF ファイルのどちらかから、XCCDF ベンチマークまたはプロファイルを選択します。 | いいえ (このパラメーターは必要ではありませんがお勧めします。 指定しなかった場合、ツールはすべての組み込みデータストリーム/ベンチマークですべてのプロファイルに対して 1 つの cab を生成します) |
| `-out [output directory]` | DCM cab ファイルを出力する場所を指定します。 | いいえ (指定しなかった場合、ツールはコンテンツを変換せずに一覧表示するだけです) |
| `-log [log file]` | ログ ファイルを指定します。 | いいえ (指定しなかった場合、Microsoft.Sces.ScapToDcm.log ファイルにログが書き込まれます) |
| `-help` または `-?` | ツールの使用方法を出力します。 | いいえ |


#### <a name="microsoftscesscaptodcmexe-examples"></a>Microsoft.Sces.ScapToDcm.exe の例

**SCAP 1.2 のコンテンツ:**  

`Microsoft.Sces.ScapToDcm.exe –scap scap_gov.nist_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID`  

**SCAP 1.0/1.1 のコンテンツ:**  

`Microsoft.Sces.ScapToDcm.exe–xccdf scap_gov.nist_Test-WinXP_xccdf.xml –cpe scap_gov.nist_Test-WinXP_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID`  

**SCAP OVAL のコンテンツ:**  

`Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder`  


#### <a name="sample-output-from-microsoftscesscaptodcmexe"></a>Microsoft.Sces.ScapToDcm.exe からのサンプル出力

```
  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Process XCCDF Benchmark xccdf_tst.bvt_benchmark_Windows-F

  Process XCCDF Profile: xccdf_tst.bvt_profile_version_1.0.0.0-BVT Profile #1

  Process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml
   Process SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip
    SCAP Data Stream: [scap_tst.bvt_datastream_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml]
  Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf_tst.bvt_benchmark_Windows-F]

  Version:       [v1.0.0.0]
   Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf_tst.bvt_profile_version_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip

  Processing CPE dictionary: scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf_tst.bvt_profile_version_1.0.0.0 into DCM baseline xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab
```


### <a name="import-the-cab-file"></a>.cab ファイルのインポート

プロセスの次のステップは、Configuration Manager コンソールを使用して、コンプライアンス設定に準拠した .cab ファイルを Configuration Manager にインポートすることです。 このプロセスの前半で作成した .cab ファイルをインポートするときに、1 つ以上の構成項目と構成基準が Configuration Manager データベースに作成されています。 プロセスの後半では、デバイス コレクションに構成基準を展開できます。 詳細については、「[構成データのインポート](/sccm/compliance/deploy-use/import-configuration-data)」を参照してください。

以前に作成した .cab ファイルの場所は、Microsoft.Sces.ScapToDcm.exe ツールの `–output` パラメーターによって指定されたフォルダーです。

> [!IMPORTANT]  
> このプロセスの前半で作成した .cab ファイルごとに、このプロセスを繰り返します。 NVD Web サイトからダウンロードした XCCDF/DataStreamXML ファイルに選択した各プロファイルの .cab ファイルがあります。 これらのファイルを処理するには、Microsoft.Sces.ScapToDcm.exe ツールを実行します。  

インポートした構成基準は読み取り専用であり、その状態は *[有効]* で、初期展開状態は *[いいえ]* です。 **[更新日]** プロパティは、基準をインポートした時刻を示します。 構成基準の名前は、XCCDF/Datastream XML の表示名セクションから取得されます。 この名前は、`ABC[XYZ]` という規則を使用して作成されます。**ABC** は XCCDF ベンチマーク ID で、**XYZ** は XCCDF プロファイル ID (プロファイルが選択されている場合) です。



## <a name="next-step"></a>次のステップ
> [!div class="nextstepaction"]
> [SCAP コンプライアンスを展開および監視し、コンプライアンス結果をエクスポートする](/sccm/compliance/plan-design/scap/deploy-monitor-export)
