---
title: SCAP コンプライアンスの展開と監視
titleSuffix: Configuration Manager
description: 構成基準として SCAP コンプライアンス設定を展開し、コンプライアンスを監視して、結果をエクスポートします。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7b59b7414ad2095d053b1121ba936281559aa5e2
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386003"
---
# <a name="deploy-and-monitor-scap-compliance-in-configuration-manager"></a>Configuration Manager での SCAP コンプライアンスの展開と監視

*適用対象: System Center Configuration Manager (Current Branch)*

SCAP データ ストリーム ファイルを[変換してインポート](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import)した後、次の手順を参照してください。  

- 構成基準をコレクションに[展開](#bkmk_deploy)して、デバイスの SCAP コンプライアンスを評価する  

- 対象のクライアントから返されたコンプライアンス データを[監視](#bkmk_monitor)する  

- SCAP 形式にコンプライアンス結果を[エクスポート](#bkmk_export)する  



## <a name="bkmk_deploy"></a> SCAP 構成基準を展開する

まず、SCAP コンプライアンスを評価するコンピューターのデバイス コレクションを作成します。 詳細については、[コレクションの作成](/sccm/core/clients/manage/collections/create-collections)に関するページを参照してください。  

これで、これらのデバイス コレクションにインポートした構成基準を展開する準備ができました。 詳細については、[構成基準を展開する方法](/sccm/compliance/deploy-use/deploy-configuration-baselines)に関するページを参照してください。  

> [!Tip]  
> 各デバイス コレクションに展開する構成基準ごとに、このプロセスを繰り返します。 少なくとも、各構成基準を 1 つ以上のデバイス コレクションに展開します。



## <a name="bkmk_monitor"></a> SCAP コンプライアンス データを監視する 

コンプライアンス データを SCAP 形式にエクスポートする前に、そのサイトでデータを収集済みであることを確認する必要があります。 構成基準をデバイス コレクションに展開した後、コレクション内の各コンピューター上の Configuration Manager クライアントが自動的にコンプライアンス情報を収集します。 その後、コンプライアンス情報が Configuration Manager データベースに格納されます。

Configuration Manager で構成基準展開の状態を表示して、適切なデータが Configuration Manager クライアントによって収集済みであることを確認します。 Configuration Manager で適切なコンプライアンス データが収集済みであることを確認することは重要です。これは、プロセスの後半で作成する XCCDF/DataStream 結果ファイルの検証に役立つためです。

詳細については、「[コンプライアンス設定を監視する](/sccm/compliance/deploy-use/monitor-compliance-settings)」を参照してください。


### <a name="validate-the-xccdfdatastream-results"></a>XCCDF/Datastream 結果の検証

1. Configuration Manager コンソールで **[資産とコンプライアンス]** ワークスペースに移動し、**[コンプライアンス設定]** を展開して、**[SCAP Dashboard]\(SCAP ダッシュボード\)** を選択します。  

2. 構成基準、割り当て、SCAP ファイル、データストリーム、ベンチマーク、プロファイル (該当する場合) を選択します。  

3. **[レポートの表示]** をクリックします。
 ![SCAP レポートの例](./media/scap-report.png)



## <a name="bkmk_export"></a> SCAP 形式へのコンプライアンス結果のエクスポート

プロセス内の次の手順では、コンプライアンス データを SCAP 形式にエクスポートします。この形式は、XML/人間が判読できる形式の ARF レポート ファイルです。 SCAP 拡張機能のエクスポート ウィザードおよび Microsoft.Sces.DcmToScap.exe コマンドライン ツールでは、構成基準ごとに個別の XCCDF/DataStream ARF 結果ファイルがエクスポートされます。 これらのファイルは、Microsoft.Sces.ScapToDcm.exe ツールで各構成基準を作成するときに使用される各 XCCDF/DataStream 入力ファイルに対応します。


### <a name="manually-export-with-the-console-wizard"></a>コンソール ウィザードを使って手動でエクスポート

> [!Note]  
> このセクションでは、Configuration Manager コンソールを使ってコンプライアンスの結果をエクスポートする手動プロセスについて説明します。 このプロセスを自動化するには、次のセクションの「[コマンドライン ツールを使用して自動的にエクスポート](#bkmk_auto-export)」を参照してください。  


1. **[SCAP Dashboard]\(SCAP ダッシュボード\)** を右クリックして、**[Export SCAP Report]\(SCAP レポートのエクスポート\)** ウィザードを開始します。  
![SCAP ダッシュボードから SCAP レポートのエクスポート ウィザードを開始する](./media/import-from-scap-dashboard.png)

2. 構成基準、割り当て、および SCAP コンテンツの種類を選択します。  
![ベースラインの選択](./media/select-ci-baseline.png)

3. SCAP データストリーム ファイル、XCCDF/CPE ファイル、または Oval コンテンツと変数ファイルの場所を選択します。  
![データストリームの選択](./media/export-scap-report-datastream.png)

4. 組織名を指定し、SCAP レポートをエクスポートするフォルダーの場所を選びます。  
 ![データストリームの選択](./media/specify-org-export.png)
   > [!Tip]  
   > ウィザードのこのページには、同じプロセスを自動化する **DcmToScap.exe** ツールで使用するコマンドラインが表示されます。  

5. 設定を確認します。  
 ![データストリームの選択](./media/confirm-export.png)

6. **[次へ]** を選択して、レポートをエクスポートします。 ウィザードを完了します。  
 ![エクスポートの完了](./media/complete-report-export.png)


### <a name="bkmk_auto-export"></a> コマンドライン ツールを使用して自動的にエクスポート

コマンド プロンプトを開いて、Configuration Manager の **AdminConsole\Bin** フォルダーに移動します。 次のコマンドラインの例のいずれかを使用します。  

> [!NOTE]  
> ご利用のアカウントに Configuration Manager プロバイダーに対する読み取りアクセス許可がある必要があります。 また、コマンドラインの `–out` パラメーターで指定したフォルダーに対する書き込みアクセス許可も必要です。

**SCAP 1.0/1.1 コンテンツ (USGCB や DISA コンテンツなど) の場合:**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf <xccdf.xml> -cpe <cpe.xml>  -select <xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

  > [!NOTE]  
  > コンテンツ内に複数のベンチマーク/プロファイルが存在する場合は、`–select` パラメーターを使用して、クライアントで評価済みのベンチマーク/プロファイルを指定します。  

**SCAP1.2 コンテンツ (最新の USGCB コンテンツなど) の場合:**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID -select <datastream/xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > コンテンツ内に複数のデータストリーム/ベンチマーク/プロファイルが存在する場合は、`–select` パラメーターを使用して、クライアントで評価済みのデータストリーム/ベンチマーク/プロファイルを指定します。  

**外部変数を含む単一の OVAL ファイルの場合:**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > Microsoft.Sces.DcmToScap.exe では、各ターゲット コンピューターの OVAL 定義結果レポートのみが生成されます。 ARF レポートは生成されません。  


#### <a name="how-to-get-the-baselineciid-and-assignmentid"></a>BaselineCIID と AssignmentID を取得する方法

Configuration Manager コンソールで **[資産とコンプライアンス]** ワークスペースに移動し、**[コンプライアンス設定]** を展開して、**[構成基準]** を選択します。 `BaselineCIID` は構成基準の識別子 (ID) です。  
![CI ID と割り当て ID の取得](./media/get-to-baselines.png)

必要な構成基準を選択して、**[展開]** タブをクリックします。`AssignmentID` は、デバイス コレクションに対する構成基準の識別子 (ID) です。 割り当て ID が表示されない場合は、列ヘッダーを右クリックして、**[割り当て ID]** を選択します。  
![CI ID と割り当て ID の取得](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Microsoft.Sces.DcmToScap.exe コマンドライン パラメーター

| パラメーター | 使用方法 | 必須 |
| --- | --- | --- |
| `-baseline [Baseline CI ID]` | 構成基準を指定します。 | はい |
| `-assignment [Assignment ID]` | 構成基準の展開を指定します。 | はい |
| `-organization [organization name]` | レポートに表示される組織名を指定します。 複数行の組織名を指定するには、`;` で区切ることができます。 | いいえ |
| `-type [thin/full/fullnosc]` | OVAL 結果の種類 (簡潔な結果、完全な結果、またはシステム特性を含まない完全な結果) を指定します。 | いいえ (指定されていない場合、既定値は full です) |
| `-scap [scap data stream file]` | SCAP データ ストリームのファイルを指定します。 | はい (SCAP 1.2 データ ストリームの場合、-xccdf と -oval / -variable で相互に排他的) |
| `-xccdf [xccdf file]` | XCCDF ファイルを指定します。 | はい (SCAP 1.0/1.1 XCCDF の場合、-scap と -oval / -variable で相互に排他的) |
| `-cpe [cpe file]` | CPE ファイルを指定します。 | はい (SCAP 1.0/1.1 XCCDF の場合、-scap と -oval / -variable で相互に排他的) |
| `-oval [oval file]` | OVAL ファイルを指定します。 | はい (スタンドアロン OVAL ファイルの場合、-xccdf と -scap で相互に排他的) |
| `-variable [oval external variable file]` | OVAL 外部変数ファイルを指定します。 | いいえ (外部 OVAL 変数ファイルが存在する場合のスタンドアロン OVAL ファイルに対しては任意、-xccdf と -scap で相互に排他的) |
| `-select [xccdf benchmark/profile]` | SCAP データ ストリームと XCCDF ファイルのどちらかから、XCCDF ベンチマークまたはプロファイルを選択します。 | はい (Configuration Manager データベース内の対応する DCM 基準を照合できるように、レポートの生成を選択する必要があります) |
| `-out [output directory]` | コンプライアンス設定 cab ファイルを出力する場所を指定します。 | いいえ (指定しなかった場合、ツールは変換せずにコンテンツを一覧表示するだけです) |
| `-log [log file]` | ログ ファイルを指定します。 | いいえ (指定しなかった場合、Microsoft.Sces.DcmToScap.log ファイルにログが書き込まれます) |
| `-help` または `-?` | ツールの使用方法を出力します。 | いいえ |

 > [!TIP]  
 > `-?`、`–h`、または `–help` パラメーターを指定して、Microsoft.Sces.DcmToScap.exe ツールの構文とパラメーターの一覧を表示できます。

既定で、Microsoft.Sces.DcmToScap.exe ツールはユーザーの資格情報を使用して、Configuration Manager データベースにアクセスします。 Microsoft.Sces.DcmToScap.exe ツールには、少なくとも Configuration Manager データベースへの読み取りアクセス権が必要です。

ツールを実行した後、次のファイルが存在することを確認します。 
- **ARF** レポート: `_ARF_xxxx.xml_` かつ/または **人間が判読できる**レポート: `xxx.txt`
- **Cyberscope** レポート: `LASR_xxx.xml`
- **ConsumedOval** レポート: `xx-oval-<machineName>.xml`
- **XCCDF ベンチマークの結果**レポート: `xccdf_xxx.xml` 



## <a name="next-step"></a>次のステップ
> [!div class="nextstepaction"]
> [トラブルシューティング](/sccm/compliance/plan-design/scap/troubleshooting-scap)
