---
title: SCAP コンプライアンス設定のインポート
titleSuffix: Configuraton Manager
description: 構成基準として SCAP コンプライアンス設定をインポートし、結果をエクスポートする
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 1f6b1fa0dd0775083eff9925a65509083b3f47d3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="import-the-compliance-settings-compliant-cab-files-into-system-center-configuration-manager"></a>System Center Configuration Manager へのコンプライアンス設定に準拠した .cab ファイルのインポート

*適用対象: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> この機能は、Technical Preview バージョン 1803 で[プレリリース機能](/sccm/core/servers/manage/pre-release-features)として初めて導入されました。 プレリリース版の SCAP 拡張機能は、現在サポートされているバージョンの Configuration Manager Current Branch と LTSB 1606 にインストールできます。 1803 Technical Preview 以降のインストール ファイルは cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi にあります。 

プロセスの次のステップは、Configuration Manager コンソールを使用して、コンプライアンス設定に準拠した .cab ファイルを Configuration Manager にインポートすることです。 このプロセスの前半で作成した .cab ファイルをインポートするときに、1 つ以上の構成項目と構成基準が Configuration Manager データベースに作成されています。 このプロセスの後半では、Configuration Manager で構成基準のそれぞれをコンピューター コレクションに割り当てることができます。

## <a name="to-import-the-compliance-settings-compliant-cab-files-into-configuration-manager"></a>コンプライアンス設定に準拠した .cab ファイルを Configuration Manager にインポートするには

1. **Configuration Manager コンソール**を開きます。
2. **Configuration Manager コンソールのナビゲーション ウィンドウで、**[資産とコンプライアンス]**> **[コンプライアンス設定]** > **[構成基準]** に移動します。

3. 操作ウィンドウで、**[構成データのインポート]** をクリックして構成データのインポート ウィザードを起動します。

1. 次の表内の情報を使用して、それ以外の値を指定しない場合は既定値を受け入れながら、**構成データのインポート ウィザード**を完了します。



構成データのインポート ウィザードのプロセス

| ウィザードのページ名 | ユーザーの操作 |
| --- | --- |
| **ファイルの選択** |1.**[追加]** をクリックします。 </br>[開く] ダイアログ ボックスが表示されます。|
||2.**[開く]** ダイアログ ボックスで、**&lt;compliant cab output\_folder&gt;** に移動します。 **&lt; compliant\_cab&gt;**.cab ファイルをクリックします。ここで、_compliant cab **output\_folder** は、Sces.ScapToDcm.exe ツールの実行時に –output スイッチの後に指定されたフォルダーです。 **compliant\_file** は、プロセスの前半に作成した .cab ファイルの名前です。 次に、**[開く]** をクリックします。 </br> Configuration Manager コンソールの [セキュリティの警告] ダイアログ ボックスが表示されます。|
||3.**Configuration Manager コンソールの [セキュリティの警告]** ダイアログ ボックスで、**[実行]** をクリックします。 [ファイルの選択] ページで、インポートする基準の一覧に構成データが表示されます。|
||3.**[次へ]** をクリックします。|
| **概要** |5.**[次へ]** をクリックします。 |
| **構成データのインポート ウィザードの完了** |6.**[閉じる]** をクリックします。 |

新しい構成基準が Configuration Manager コンソールの情報ウィンドウに表示されます。

>[!IMPORTANT]
> このプロセスの前半で作成した .cab ファイルごとに、このプロセスを繰り返す必要があります。 NVD Web サイトからダウンロードした XCCDF/DataStream XML ファイル内の選択されたプロファイルごとに .cab ファイルが存在します。それらは、Microsoft.Sces.ScapToDcm.exe ツールを実行して処理することができます。

インポートした構成基準は読み取り専用であり、&#39;[有効]&#39; というステータスと &#39;[いいえ]&#39; という初期展開状態が割り当てられます。  &#39;[更新日]&#39; プロパティは、基準がインポートされた時刻を示します。  構成基準の名前は、XCCDF/Datastream XML の表示名セクションから取得されます。 この名前は次の規則を使用して構築されます。

ABC[XYZ]。ここで、ABC は XCCDF ベンチマーク ID で、XYZ は XCCDF プロファイル ID (プロファイルが選択されている場合) です。



## <a name="assign-configuration-baselines-to-the-computer-collections"></a>コンピューター コレクションへの構成基準の割り当て

SCAP コンプライアンスを評価するコンピューターに適切なコンピューター コレクションを作成したら、そのコンピューター コレクションを関連付ける、インポートした構成基準を割り当てることができます。 このセクションでは、Configuration Manager コンソールを使用して構成基準をコンピューター コレクションに割り当てる方法について説明します。

構成基準をコンピューター コレクションに割り当てるには、次の操作を行います。

1. **Configuration Manager** **コンソール**を開きます。

2. **Configuration Manager コンソールのナビゲーション ウィンドウで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** >**[構成基準]** に移動します。
3. ナビゲーション ウィンドウで、&lt; **configuration\_baseline> をクリックします。ここで、&lt;_configuration\_baseline&gt;_ はコンピューター コレクションに割り当てる構成基準の名前です。

    構成基準の構成項目の一覧が Configuration Manager の情報ウィンドウに表示されます。

4. 操作ウィンドウで、 **[展開]** をクリックします。

5. 次の表内の情報を使用して、それ以外の値を指定しない場合は既定値を受け入れながら、[**構成基準**の**展開**] **ダイアログ**を完了します。

### <a name="deploy-configuration-baseline-dialog-process"></a>[構成基準の展開] ダイアログのプロセス

| ウィザードのページ名 | ユーザーの操作 |
| --- | --- |
| **コレクションの選択** | 1.**[参照]** をクリックします。|
||2.**[コレクションの選択]** ダイアログ ボックスで、**[デバイス コレクション]** を選択します。 次に、**&lt;computer\_collection&gt;** をクリックします。ここで、&lt;_computer\_collection&gt;_ は、プロセスの前半で作成したコンピューター コレクションの名前です。 **[OK]** をクリックします。|
| **スケジュールの設定** |3.組織に適切なスケジュールを選択します。|
 
>[!IMPORTANT]
> 各構成基準に割り当てるコンピューター コレクションごとに、このプロセスを繰り返します。 各構成基準を 1 つ以上のコンピューター コレクションに割り当てます。

## <a name="verify-that-the-compliance-data-has-been-collected"></a>コンプライアンス データが収集済みであることを確認する

コンプライアンス データを SCAP 形式にエクスポートする前に、そのデータが収集済みであることを確認する必要があります。 構成基準をコンピューター コレクションに割り当てた後、コレクション内の各コンピューター上の Configuration Manager クライアントが自動的にコンプライアンス情報を収集します。 その後、コンプライアンス情報が Configuration Manager データベースに格納されます。

Configuration Manager で構成基準展開のステータスを表示して、適切なデータが Configuration Manager クライアントによって収集済みであることを確認します。 Configuration Manager で適切なコンプライアンス データが収集済みであることを確認することは重要です。これは、プロセスの後半で作成する XCCDF/DataStream 結果ファイルの検証に役立つためです。



### <a name="verify-that-the-compliance-data-has-been-collected"></a>コンプライアンス データが収集済みであることを確認します。

1. Configuration Manager コンソールを開きます。
2. Configuration Manager コンソールのナビゲーション ウィンドウで、**[監視]** > **[展開]** に移動します。
3. **[機能の種類]** をクリックして展開の種類を並べ替え、一覧内で種類が **[基準]** になっている項目を探します。
4. 一覧でコレクションに展開したばかりの &lt;configuration\_baseline&gt; を右クリックして、**[ステータスの表示]** をクリックします。
5. その後、&lt;configuration\_baseline&gt; ノードに移動して準拠ステータスを確認します。不明な状態のコンピューターが存在する場合は、そのコンピューターのコンプライアンス データ コレクションがまだ完了していないことを意味します。

### <a name="validate-the-xccdfdatastream-results"></a>XCCDF/Datastream 結果の検証

1. Configuration Manager コンソールを開きます。
2. Configuration Manager コンソールのナビゲーション ウィンドウで、**[コンプライアンス設定]** > **[SCAP ダッシュボード]** に移動します。
3. 構成基準、割り当て、SCAP ファイル、データストリーム、ベンチマーク、プロファイル (該当する場合) を選択します。
4. **[レポートの表示]**
 ![[SCAP レポート]](./media/scap-report.png) をクリックします。



## <a name="export-compliance-results-to-scap-format"></a>SCAP 形式へのコンプライアンス結果のエクスポート

プロセス内の次のタスクは、コンプライアンス設定コンプライアンス データを SCAP 形式にエクスポートすることです。その結果、XML/人間が読める形式の ARF レポート ファイルが生成されます。 SCAP 拡張機能のエクスポート ウィザードおよび Microsoft.Sces.DcmToScap.exe ツールは、コンプライアンス設定構成基準ごとに別々の XCCDF/DataStream ARF 結果ファイルをエクスポートします。 これらのファイルは、Microsoft.Sces.ScapToDcm.exe ツールで各コンプライアンス設定構成基準を作成するときに使用される各 XCCDF/DataStream 入力ファイルに対応します。

### <a name="export-the-compliance-settings-compliance-data-using-the-export-scap-report-wizard"></a>SCAP レポートのエクスポート ウィザードを使用するコンプライアンス設定コンプライアンス データのエクスポート

1. SCAP ダッシュボードの右クリック メニューから、SCAP レポートのエクスポート ウィザードを起動します。
![SCAP ダッシュボードからのインポート](./media/import-from-scap-dashboard.png)

2. 構成基準と割り当ての選択 ![ベースラインの選択](./media/select-ci-baseline.png)

3. SCAP データストリーム ファイル、XCCDF/CPE ファイル、または Oval コンテンツと変数ファイルの場所を選択します。
![データストリームの選択](./media/export-scap-report-datastream.png)

4. 組織名を指定し、SCAP レポートをエクスポートするフォルダーの場所を選択します。
 ![データストリームの選択](./media/specify-org-export.png)

5. 設定を確認します。
 ![データストリームの選択](./media/confirm-export.png)

6. **[次へ] を選択して、レポートをエクスポートします。  進行状況バーに続いて、完了ページが表示されます。
 ![エクスポートの完了](./media/complete-report-export.png)



### <a name="alternate-method-export-the-compliance-settings-compliance-data-using-the-microsoftscesdcmtoscapexe-tool"></a>(代替方法) Microsoft.Sces.DcmToScap.exe ツールを使用するコンプライアンス設定コンプライアンス データのエクスポート

1. コマンド プロンプトで、AdminConsole\Bin フォルダーに移動して、次の表に一覧表示されたコマンド ライン パラメーターを入力してから、**ENTER キーを押します。

    >[!NOTE] 
    >使用するアカウントは、Configuration Manager プロバイダーに対する読み取りアクセス許可だけでなく、コマンド ラインの -out パラメーターで指定された出力フォルダーに対する書き込みアクセス許可も持っている必要があります。

**SCAP 1.0/1.1 コンテンツ (USGCB や DISA コンテンツなど) の場合:**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt;  -select &lt;xccdfBenchmark/profile&gt; -out &lt;outputResultFolder&gt;  [-log logFileName]

  >[!NOTE] 
    >コンテンツ内に複数のベンチマーク/プロファイルが存在する場合は、–select パラメーターを使用して、クライアントで評価済みのベンチマーク/プロファイルを指定する必要があります。

**SCAP1.2 コンテンツ (最新の USGCB コンテンツなど) の場合:**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID  -select &lt;datastream/xccdfBenchmark/profile&gt; -out &lt;outputResultFolder&gt;  [-log logFileName]

   >[!NOTE] 
   >コンテンツ内に複数のデータストリーム/ベンチマーク/プロファイルが存在する場合は、–select パラメーターを使用して、クライアントで評価済みのデータストリーム/ベンチマーク/プロファイルを指定する必要があります。

**外部変数を含む単一の OVAL ファイルの場合:**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;]  -out &lt;outputResultFolder&gt;  [-log logFileName]

   >[!NOTE] 
    >Microsoft.Sces.DcmToScap.exe は、各ターゲット コンピューターの OVAL 定義結果レポートしか生成しないため、ARF レポートは生成されません。

#### <a name="how-to-get-baseline-ci-id-and-assignment-id"></a>基準 CI ID と割り当て ID を取得する方法

管理コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[構成基準]** に移動します。 CI ID は構成基準の CI ID です。

![CI ID と割り当て ID の取得](./media/get-to-baselines.png)

必要な構成基準を選択して、[展開] タブをクリックします。割り当て ID が表示されない場合は、列ヘッダーを右クリックし、[割り当て ID] をクリックして有効にします。
![CI ID と割り当て ID の取得](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Microsoft.Sces.DcmToScap.exe コマンド ライン パラメーター

| **パラメーター** | **使用方法** | **必須** |
| --- | --- | --- |
| -baseline [Baseline CI ID] | 構成基準を指定します。 | はい |
| -assignment [Assignment ID] | 構成基準の展開を指定します。 | はい |
| -organization [organization name] | レポートに表示される組織名を指定します。 複数行の組織名を指定する場合は、&#39;;&#39; で区切ることができます。 | いいえ |
| -type [thin/full/fullnosc] | OVAL 結果の種類 (簡潔な結果、完全な結果、またはシステム特性を含まない完全な結果) を指定します。 | いいえ (指定されていない場合、既定値は full です) |
| -scap [scap data stream file] | SCAP データ ストリームのファイルを指定します。 | はい (SCAP 1.2 データ ストリームの場合、–xccdf と –oval / -variable で相互に排他的) |
| -xccdf [xccdf file] | XCCDF ファイルを指定します。 | はい (SCAP 1.0/1.1 XCCDF の場合、–scap と –oval / -variable で相互に排他的) |
| -cpe [cpe file] | CPE ファイルを指定します。 | はい (SCAP 1.0/1.1 XCCDF の場合、–scap と –oval / -variable で相互に排他的) |
| -oval [oval file] | OVAL ファイルを指定します。 | はい (スタンドアロン OVAL ファイルの場合、–xccdf と -scap で相互に排他的) |
| -variable [oval external variable file] | OVAL 外部変数ファイルを指定します。 | いいえ (外部 OVAL 変数ファイルが存在する場合のスタンドアロン OVAL ファイルに対しては任意、–xccdf と -scap で相互に排他的) |
| -select [xccdf benchmark/profile] | SCAP データ ストリームと XCCDF ファイルのどちらかから、XCCDF ベンチマークまたはプロファイルを選択します。 | はい (Configuration Manager データベース内の対応する DCM 基準を照合できるように、レポートの生成を選択する必要があります) |
| -out [output directory] | コンプライアンス設定 cab ファイルを出力する場所を指定します。 | いいえ (指定しなかった場合、ツールは変換せずにコンテンツを一覧表示するだけです) |
| -log [log file] | ログ ファイルを指定します。 | いいえ (指定しなかった場合、Microsoft.Sces.DcmToScap.log ファイルにログが書き込まれます) |
| -help / -? | ツールの使用方法を出力します。 | いいえ |



 >[!TIP] 
 >-?、 –h、または –help パラメーターを指定して、Microsoft.Sces.DcmToScap.exe ツールの構文とパラメーターの一覧を表示できます。

既定で、Microsoft.Sces.DcmToScap.exe ツールはユーザーの資格情報を使用して、Configuration Manager データベースにアクセスします。 Microsoft.Sces.DcmToScap.exe ツールには、少なくとも Configuration Manager データベースへの読み取りアクセス権が必要です。

適切な **ARF** レポート: _ARF\_xxxx.xml_ および/または**人間が判読できる**レポート: xxx.txt、**Cyberscope** レポート: LASR\_xxx.xml、**ConsumedOval** レポート: xx-oval-&lt;machineName&gt;.xml、**XCCDF ベンチマーク結果**レポート: xccdf\_xxx.xml ファイルが存在することを確認したら、「exit」と入力し、**ENTER** キーを押してコマンド プロンプトを終了します。

## <a name="next-step"></a>次のステップ
> [!div class="nextstepaction"]
> [トラブルシューティング](/sccm/compliance/plan-design/scap/troubleshooting-scap)
