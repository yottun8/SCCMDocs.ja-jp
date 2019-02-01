---
title: MDT のトラブルシューティング
titleSuffix: Microsoft Deployment Toolkit
description: 'Microsoft Deployment Toolkit のトラブルシューティング リファレンス '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 91a7a69a-deac-4b0f-aac9-b7bd187c53fb
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: efb65086878a46bfb3485fdd8b0be6f613225261
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2018
ms.locfileid: "27821016"
---
# <a name="troubleshooting-reference-for-the-microsoft-deployment-toolkit"></a>Microsoft Deployment Toolkit のトラブルシューティング リファレンス
 オペレーティング システムやアプリケーションの展開、およびユーザー状態の移行は、適切なツールとガイダンスを利用できる場合でも、困難な作業になることがあります。 Microsoft® Deployment Toolkit (MDT) 2013 に付属するこのリファレンスでは、現時点でわかっている問題、それらについて可能な回避策、およびトラブルシューティングのガイダンスを提供します。  

> [!NOTE]
>  このドキュメントでは、特に指定がない限り、*Windows* という表記は、Windows 8.1、Windows 8、Windows 7、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 の各オペレーティング システムを示します。 MDT では、ARM プロセッサ ベースのバージョンの Windows はサポートされていません。 同様に、特に指定がない限り、*MDT* は MDT 2013 を示します。  

> [!NOTE]
>  Microsoft Diagnostics and Recovery Toolset (DaRT) には、起動しないクライアント コンピューターまたは不安定になったクライアント コンピューターを復旧してトラブルシューティングを行うための強力なツールが含まれています。 DaRT を使うと、クラッシュの原因の特定、失われたファイルの復元などを行うことができます。 また、Windows オペレーティング システムを開発して展開するときのトラブルシューティング ツールとして DaRT を使うこともできます。 たとえば、ビルドされたイメージが正常に起動しない場合は、診断環境である ERD コマンダーを使うことによって、イメージが存在するクライアント コンピューターを起動できます。 その後、クライアント コンピューターのハード ディスクを調べたり、イベント ログを見たり、更新プログラムを削除したり、オペレーティング システムの設定を変更したりできます。 DaRT は、Microsoft Desktop Optimization Pack for Software Assurance の一部です。 DaRT の詳細については、[http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx](http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx) をご覧ください。  

## <a name="understanding-logs"></a>ログの理解  
 MDT の効果的なトラブルシューティングを始める前に、オペレーティング システムの展開時に使用される多数の .log ファイルについて明確に理解しておく必要があります。 どのログ ファイルで、どの時点のどのようなエラー状態を調べればよいかがわかっていれば、不可解で理解しにくかった問題が、明確でわかりやすくなる可能性があります。  

 MDT のログ ファイルの形式は、Trace32 で読み取るように設計されています。Trace32 は、System Center Configuration Manager 2007 Toolkit V2 に付属し、[Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=9257) からダウンロードできます。 また、System Center 2012 Configuration Manager 以降のバージョンで利用できる Configuration Manager Trace Log Tool (CMTrace) でログを読むこともできます。 エラーの検索がずっと簡単になるので、ログ ファイルを読むときはできる限りこれらのツールを使ってください。  

 このセクションではこの後、展開および Windows のセットアップの間に作成されるログ ファイルについて詳しく説明します。 このセクションでは、トラブルシューティングにログ ファイルを使うときの例も示します。  

### <a name="mdt-logs"></a>MDT のログ  
 各 MDT スクリプトは、実行するとログ ファイルを自動的に作成します。 これらのログ ファイルの名前は、スクリプトの名前と一致します。たとえば、ZTIGather.wsf は *ZTIGather.log* という名前のログ ファイルを作成します。 また、各スクリプトは、MDT スクリプトが作成するログ ファイルの内容を集約する共通マスター ログ ファイル (BDD.log) も更新します。 MDT のログ ファイルは、展開プロセスの間は C:\MININT\SMSOSD\OSDLOGS に存在します。 実施されている展開の種類に応じて、ログ ファイルは展開の完了時に %WINDIR%\SMSOSD または %WINDIR%\TEMP\SMSOS に移動されます。 Lite Touch Installation (LTI) 展開の場合は、ログは最初に C:\MININT\SMSOSD\OSDLogs に作成されます。 タスク シーケンスの処理が完了すると、%WINDIR%\TEMP\DeploymentLogs に移動されます。  

 MDT は次のログ ファイルを作成します。  

-   **BDD.log**。 集約された MDT ログ ファイルであり、Customsettings.ini ファイルで **SLShare** プロパティが指定されていると展開の終了時にネットワークの場所にコピーされます。  

-   **LiteTouch.log**。 このファイルは、LTI 展開の間に作成されます。 **/debug:true** オプションを指定しないと、%WINDIR%\TEMP\DeploymentLogs に格納されます。  

-   **Scriptname*.log**。 このファイルは、各 MDT スクリプトによって作成されます。 *Scriptname* は、対象のスクリプトの名前を表します。  

-   **SMSTS.log**。 このファイルはタスク シーケンサーによって作成され、タスク シーケンサーのすべてのトランザクションが記述されています。 展開のシナリオに応じて、%TEMP%、%WINDIR%\System32\ccm\logs、C:\\\_SMSTaskSequence、または C:\SMSTSLog に格納されます。  

-   **Wizard.log**。 このファイルは展開ウィザードによって作成および更新されます。  

-   **WPEinit.log**。 このファイルは、Windows PE の初期化プロセス中に作成され、Windows PE の起動中に発生したエラーのトラブルシューティングに役立ちます。  

-   **DeploymentWorkbench_*id*.log**。 このログ ファイルは、Deployment Workbench を開始するときに **a /debug** を指定すると、%temp% フォルダーに作成されます。  

### <a name="configuration-manager-operating-system-deployment-logs"></a>Configuration Manager のオペレーティング システム展開ログ  
 Microsoft System Center 2012 R2 Configuration Manager によって作成されるオペレーティング システム展開ログ ファイルについては、「[Configuration Manager のログ ファイルのテクニカル リファレンス](http://technet.microsoft.com/library/hh427342.aspx)」をご覧ください。  

 Windows ユーザー状態移行ツール (USMT) を実行すると、MDT は USMT のログ ファイルを MDT のログ ファイルの場所に保存するログ オプションを自動的に追加します。 作成されるログ ファイルと作成されるタイミングは次のとおりです。  

-   **USMTEstimate.log**。 USMT の要件を推定するときに作成されます。  

-   **USMTCapture.log**。 データをキャプチャするときに USMT によって作成されます。  

-   **USMTRestore.log**。 データを復元するときに USMT によって作成されます。  

 ZeroTouchInstallation.vbs スクリプトは、USMT の進行状況ログ ファイルで、エラーと警告を自動的にスキャンします。 このスクリプトは、Microsoft System Center Operations Manager に対して次のようなサマリーでイベント ID 41010 を生成します (*usmt_type* は **ESTIMATE**、**SCANSTATE**、または **LOADSTATE**、*error_count* は見つかったエラーの総数、*warning_count* は見つかった警告の総数です)。  

```  
ZTI USMT <usmt_type> reported <error_count> errors and <warning_count> warnings  
```  

 エラーの数が 0 より多い場合、このイベントは Error 型です。 警告の数が 0 より多く、エラーがない場合、このイベントは Warning 型です。 それ以外の場合、このイベントは Informational 型です。  

## <a name="identifying-error-codes"></a>エラー コードの識別  
表 1 は、MDT のスクリプトが作成するエラー コードとその説明の一覧です。 これらのエラー コードは、BDD.log ファイルに記録されます。  

### <a name="table-1-error-codes-and-their-description"></a>表 1. エラー コードとその説明  

|**エラー コード**|**説明**|  
|-|-|  
|5201|展開共有に接続できませんでした。 展開は続行されません。|  
|5203|展開共有に接続できませんでした。 展開は続行されません。|  
|5205|展開共有に接続できませんでした。 展開は続行されません。|  
|5206|展開ウィザードは取り消されたか、または正常に完了しませんでした。 展開は続行されません。|  
|5207|展開共有に接続できませんでした。 展開は続行されません。|  
|5208|**DeploymentType** が設定されていません。 **SkipWizard** に対する何らかの値を設定する必要があります。|  
|5208|SMS タスク シーケンサーが見つかりません。 展開は続行されません。|  
|5400|オブジェクトを作成します: **Set *class_instance* = New *class_name***|  
|5490|MSXML2.DOMDocument を作成してください。|  
|5495|MSXML2.DOMDocument.ParseErr.ErrCode を作成してください。|  
|5496|LoadControlFile.FindFile: *ConfigFile*|  
|5601|OS の GUID: %OSGUID% が存在することを確認してください。|  
|5602|OSGUID: %OSGUID% で XML を開いてください。|  
|5610|ファイルを確認してください。|  
|5630|ファイルを確認してください: *ImagePath*。|  
|5640|ファイルを確認してください: *ImagePath*。|  
|5641|FindFile: ImageX.exe。|  
|5643|BootSect.exe を検索してください。|  
|5650|ディレクトリを確認してください: *SourcePath*。|  
|5651|ディレクトリを確認してください: *SourcePath*\Platform。|  
|5652|FindFile: bootsect.exe。|  
|6001|ドライブを確認してください。|  
|6002|ドライブを確認してください。|  
|6010|TSGUID をテストしてください。|  
|6020|Robocopy によって返された値: *Value*。|  
|6021|Robocopy によって返された値: *Value*。|  
|6101|ファイルを確認してください: *DeployCab*。|  
|6102|Sysprep ファイルを DEPLOY.CAB から展開してください。|  
|6111|Sysprep.exe を実行してください。|  
|6121|Sysprep を実行してください。|  
|6191|レジストリの **CloneTag** をテストして、Sysprep が完了したことを確認してください。|  
|6192|レジストリの **SystemSetupInProgress** をテストして、Sysprep が完了したことを確認してください。|  
|6401|承認された DHCP サーバー。|  
|6501|コンピューターのバックアップを実行できません。ネットワーク パス (**BackupShare**、**BackupDir**) が指定されていません。|  
|6502|エラー - IMAGEX が見つかりません、バックアップを実行できません。|  
|6601|GetObject(... root/wmi:BCDStore)。|  
|6602|BCD.OpenStore (*BCDStore*)。|  
|6701|保護機能を構成しました。|  
|6702|ブート ファイルを移動しました。|  
|6703|BDE パーティションを作成してください。|  
|6704|ドライブを最適化してください。|  
|6705|ドライブを圧縮してください。|  
|6706|複数のパーティションをテストしています。|  
|6707|ブート ファイルを作成してください。|  
|6708|ディスクを暗号化してください。|  
|6709|MicrosoftVolumeEncryption WMI プロバイダーに接続してください。|  
|6710|ディスクを暗号化しています。|  
|6711|**ProtectKeyWithTPM**。|  
|6712|**ProtectKeyWithTPMAndPIN**。|  
|6713|**ProtectKeyWithTPMAndStartupKey**。|  
|6714|外部キーをファイルに保存してください。|  
|6715|外部キーで保護してください。|  
|6716|外部キーをファイルに保存してください。|  
|6717|数値パスワードでキーを保護してください。|  
|6718|**GetKeyProtectorNumberialP@ssword。**|  
|6718|パスワードをファイルに保存してください。|  
|6719|*PasswordFile* を開いてください。|  
|6720|ドライブを暗号化してください。|  
|6721|*DiskPartFile* を開いてください。|  
|6722|パーティションを作成してください。|  
|6723|既存の BDE ドライブを取得してください。|  
|6724|*DiskPartFile* を開いてください。|  
|6727|*DiskPartFile* を開こうとしています。|  
|6729|テキスト ファイル *DiskPartFile* を作成します。|  
|6730|**cmd /c DISKPART.EXE /s *DiskPartFile* >> *LogPath*\ZTIMarkActive_diskpart.log 2>&1** を実行します|  
|6731|bcdboot.exe を検索します。|  
|6732|Microsoft TPM プロバイダーに接続してください。|  
|6733|プロバイダー クラスで TPM のインスタンスを取得してください。|  
|6734|TPM のインスタンスを取得してください。|  
|6735|TPM が有効になっているかどうかを確認してください。|  
|6736|TPM がアクティブになっているかどうかを確認してください。|  
|6737|TPM が所有されているかどうかを確認してください。|  
|6738|TPM の所有権が許可されているかどうかを確認してください。|  
|6739|TPM が有効になっているかどうかを確認してください。|  
|6740|TPM がアクティブになっているかどうかを確認してください。|  
|6741|TPM が所有されていて所有権が許可されているかどうかを確認してください。|  
|6741|TPM 所有者パスワードの設定|  
|6742|TPM 所有者 P@ssword が **AdminP@ssword** に設定されています。|  
|6743|TPM 所有者 P@ssword を値に設定してください。|  
|6744|TPM が有効になっているかどうかを確認してください。|  
|6745|TPM の所有者を確認してください。|  
|6746|承認キー ペアを確認してください。|  
|6747|TPM がアクティブになっているかどうかを確認してください。|  
|6748|TPM の所有権が許可されているかどうかを確認してください。|  
|6749|所有者 p@ssword を所有者の承認に変換してください。|  
|6750|承認キー ペアを作成してください。|  
|6751|所有者の承認を変更してください。|  
|6752|**Cmd** を実行してください。|  
|6753|TPM を検証してください。|  
|6754|BDE のインスタンスを取得してください。|  
|6755|TPM でキーを保護してください。|  
|6756|構成するリムーバブル メディアを確認してください。 **ProtectKeyWithTpmAndStartupKey**。|  
|6757|TPM と起動キーでキーを保護してください。|  
|6758|BDE PIN を検索してください。|  
|6759|TPM と PIN でキーを保護してください。|  
|6760|**BDEKeyLocation** のリムーバブル メディアを検索してください。|  
|6761|外部キーで保護してください。|  
|6762|*PasswordFile* に保存されている P@ssword を復旧してください。|  
|6764|BitLocker ポリシーを構成してください。|  
|7000|ZTIConfigure.xml が見つかりません。中止しています。|  
|7001|無人応答ファイルを検索しています。|  
|7100|エラー - このスクリプトは、完全な OS でのみ実行する必要があります。|  
|7101|エラー - DCPromo 応答ファイルの生成に十分な値が指定されていません。|  
|7102|エラー - 新しいレプリカ DC の作成に必須のプロパティが指定されませんでした。|  
|7103|エラー - 新しい子ドメインの作成に必須のプロパティが指定されませんでした。|  
|7104|エラー - 新しいフォレストの作成に必須のプロパティが指定されませんでした。|  
|7105|エラー - 新しいフォレストの作成に必須のプロパティが指定されませんでした。|  
|7200|サービスがインストールされていないため、DHCP サーバーを構成できません。|  
|7201|スコープの詳細を読み取れません。`GetScopeDetails()` は失敗しました。|  
|7202|スコープを作成するための十分な値が指定されていません。|  
|7203|このスコープの IP 範囲を設定するのに十分な値が指定されていません。|  
|7204|スコープの除外範囲に値が指定されていません。|  
|7300|DNS コマンドを発行できません。|  
|7700|新しいコンピューター シナリオではありません。ディスク パーティションを終了しています。|  
|7701|システムおよび BDE パーティションに十分な大きさのディスクではありません。1.5 GB が必要です。|  
|7702|システムおよび WinRE パーティションに十分な大きさのディスクではありません。10 GB が必要です。|  
|7703|DeployRoot がディスク # *DiskIndex* 上にあります。 OEM シナリオを実行しています。スキップします。|  
|7704|OEM シナリオを実行しています。スキップします。|  
|7704|BitLocker では、拡張パーティションと論理パーティションは許可されません。|  
|7712|Drive/<*ボリューム ドライブ*> が存在することを確認してください。 フォーマットします。|  
|7900|Findfile: Microsoft.BDD.PnpEnum.exe。|  
|7901|**AllDrivers.Exists("*GUID*")。**|  
|7904|**AllDrivers.Exists("*GUID*")。**|  
|9200|Findfile(PkgMgr.exe)。|  
|9601|エラー - ZTITatoo 状態復元タスクは、完全な OS で実行する必要があります。中止しています。|  
|9701|USMT の見積もりからのリターン コードがゼロではありません。リターン コード = *Error*。|  
|9702|ユーザー状態をキャプチャできません。ローカル空間が十分ではなく、ネットワーク パス (UDShare、UDDir) が指定されていません。|  
|9703|USMT のキャプチャからのリターン コードがゼロではありません。リターン コード = *Error*。|  
|9704|有効なコマンド ライン オプションが指定されませんでした。|  
|9801|エラー - サーバー オペレーティング システムを実行しているマシンにクライアント オペレーティング システムを展開しようとしています。|  
|9802|エラー - クライアント オペレーティング システムを実行しているマシンにサーバー オペレーティング システムを展開しようとしています。|  
|9803|エラー - マシンはアップグレードを承認されていません (OSInstall=*OSInstall*)。中止しています。|  
|9804|エラー - メモリの *Memory* MB が十分ではありません。 少なくとも *Memory* MB のメモリが必要です。|  
|9805|エラー - プロセッサ速度 *ProcessorSpeed* MHz では不十分です。  少なくとも *ProcessorSpeed* MHz のプロセッサが必要です。|  
|9806|エラー - *Drive* の空き領域が十分ではありません。 さらに *Size* MB が必要です。|  
|9807|エラー - *Drive* の空き領域が十分ではありません。 さらに *Size* MB が必要です。|  
|9901|ZTIWindowsUpdate スクリプトは Windows PE では実行できません。|  
|9902|ZTIWindowsUpdate を実行して失敗した回数が多すぎます。 回数 = *Count*。|  
|9903|更新された Windows Update エージェントのインストール中に予期しない問題が発生しました。リターン コード = *Error*。|  
|9904|オブジェクトの作成が失敗しました: **Microsoft.Update.Session**。|  
|9905|オブジェクトの作成が失敗しました: **Microsoft.Update.UpdateColl**。|  
|9906|重要なファイル *File* が見つかりませんでした。中止しています。|  
|10000|オブジェクトを作成してください。**Set oLTICleanup = New LTICleanup**。|  
|10201|ドメイン *Domain* に参加できません。 インストールを停止します。|  
|10203|FindFile(LTISuspend.wsf)。|  
|10204|プログラム *LTISuspend* を実行してください。|  
|41024|ImageX を実行してください。|  
|52012|ウィザードのすべてのパラメーターが設定されていません。|  

 リスト 1 では、エラー コードを検索する方法を示すログ ファイルからの抜粋を提供します。 この抜粋で報告されているエラー コードは 5001 です。  

 **リスト 1.エラー コード 5001 を含む SMSTS.log ファイルからの抜粋**  

```  
.  
.  
.  
The operating system installation failed. Please contact your system administrator for assistance.  

The action "Zero Touch Installation - Validation" failed with exit code 5001  
.  
.  
.  

```  

### <a name="converting-error-codes"></a>エラー コードの変換  
 ログ ファイルで示される多くのエラー コードはわかりにくく、実際のエラー状態と関連付けるのが困難です。 以下のプロセスでは、エラー コードを変換し、問題の解決に役立つ可能性のある意味のある情報を取得する方法を示します。  

 **問題**: イメージのキャプチャがエラー コード 0x80070040 で失敗する。  

 **解決方法 1**: 示されているエラー コードは 16 進形式なので、10 進形式に変換する必要があります。 そのためには、関数電卓が必要であり、Windows オペレーティング システムに含まれる電卓はこの作業に適しています。  

 **エラー コードを変換するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[アクセサリ]** をポイントして、**[電卓]** をクリックします。  

2.  **[表示]** メニューをクリックして、**[関数電卓]** をクリックします。  

3.  **[16 進]** を選び、コードの最後の 4 桁を入力します。この例では、図 1 に示すように **0040** です。  

     ![TroubleshootingReference1](media/TroubleshootingReference1.jpg "TroubleshootingReference1")  
図 1 エラーの変換  

     **図 1.エラーの変換**  

     電卓が 16 進モードのときは、先頭のゼロが表示されないことに注意してください。  

4.  **[10 進]** を選びます。  

     16 進値 *40* が 10 進値 *64* に変換されます。  

5.  コマンド プロンプト ウィンドウを開き、「**NET HELPMSG 64**」と入力して、Enter キーを押します。  

     **NET HELPMSG** コマンドは、数値のエラー コードをわかりやすいテキストに変換します。 ここで指定したエラー コードの場合、"指定されたネットワーク名は利用できません" に変換されます。  

 この情報は、ターゲット コンピューター上、またはターゲット コンピューターと展開の共有が存在するサーバーの間に、ネットワークの問題が存在する可能性があることを示します。 このような問題としては、ネットワーク ドライバーが正しくインストールされていない、速度と二重化の設定が一致していない、などが考えられます。  

 **解決方法 2:** Microsoft Exchange Server Error Code Look-up ユーティリティを使います。 このコマンド ライン ユーティリティは、エラー コードの変換に役立ちます。 [Microsoft ダウンロード センター](http://www.microsoft.com/download/details.aspx?id=985)からダウンロードできます。  

### <a name="review-of-sample-logs"></a>サンプル ログの確認  
 MDT で作成されるログ ファイルを使って、MDT の展開プロセスでの問題のトラブルシューティングを行うことができます。 以下のセクションでは、MDT のログ ファイルを使って展開プロセスのトラブルシューティングを行う方法の例を示します。  

-   「[データベースへのアクセスの失敗](#FailuretoAccesstheDatabase)」で説明されている、MDT データベース (MDT DB) へのアクセスの失敗に関する問題  

####  <a name="FailuretoAccesstheDatabase"></a> データベースへのアクセスの失敗  
 **問題:** 多くのセクションが含まれ、**Priority** プロパティで各セクションの処理の優先順位が指定されている CustomSettings.ini ファイルを使用した展開の実行中に、エラーが発生します。 BDD.log には、次のエラー メッセージが含まれています。  

-   ```  
    ERROR - Opening Record Set (Error Number = -2147217911) (Error Description: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'.)  
    ```  

-   ```  
    ADO error: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'. (Error #-2147217911; Source: Microsoft OLE DB Provider for SQL Server; SQL State: 42000; NativeError: 229  
    ```  

-   ```  
    ERROR - Unhandled error returned by ZTIGather: Object required (424)  
    ```  

> [!NOTE]
>  わかりやすくするため、上記のログ ファイルの内容は、Trace32 プログラムを使用して表示したものを示してあります。  

 **解決方法:** ログ ファイル サンプルの最初の行で指摘されているように、問題はデータベースにアクセスするためのアクセス許可が拒否されたことです。 したがって、おそらくユーザー ID とパスワードを使用できなかったために、スクリプトはデータベースへのセキュリティで保護された接続を確立できません。 その結果、データベースへのアクセスはコンピューター アカウントを使って試みられました。 この問題を解決する最も簡単な方法は、すべてのユーザーにデータベースへの読み取りアクセスを許可することです。  

## <a name="troubleshooting"></a>トラブルシューティング  
 詳細なトラブルシューティング プロセスに着手する前に、次の項目を検討し、関連する要件が満たされていることを確認します。  

-   インストールに関する問題は、ソフトウェアとハードウェアのすべての前提条件が満たされていない場合に発生することがあります。  

### <a name="application-installation"></a>アプリケーションのインストール  
 アプリケーションのインストールに関する問題と解決策を確認します。  

-   セキュリティ上の理由からブロックされたインストール ソース ファイル (「[ブロックされた実行可能ファイル](#BlockedExecutables)」の説明を参照)  

-   ネットワーク接続の喪失 (「[失われたネットワーク接続](#LostNetworkConnections)」の説明を参照)  

-   2007 Microsoft Office system または関連ファイルのインストール時のインストール エラー 30029 (「[2007 Microsoft Office system](#MicrosoftOfficeSystem)」の説明を参照)  

####  <a name="BlockedExecutables"></a> ブロックされた実行可能ファイル  
 **問題:** インストール ソース ファイルがインターネットからダウンロードされる場合、1 つまたは複数の NTFS ファイル システム データ ストリームとマークされる可能性があります。 NTFS データ ストリームの詳細については、「[File Streams](http://msdn2.microsoft.com/library/aa364404\(VS.85\).aspx)」(ファイル ストリーム) をご覧ください。 NTFS ファイル システム データ ストリームが存在すると、"**ファイルを開く – セキュリティの警告**" というプロンプトが表示される場合があります。 プロンプトで **[実行]** をクリックするまで、インストールは続行されません。  

 図 2 では、**More** コマンドと [Streams ユーティリティ](http://technet.microsoft.com/sysinternals/bb897440.aspx)を使って NTFS ファイル システム データ ストリームを表示できることが示されています。  

 ![TroubleshootingReference2](media/TroubleshootingReference2.jpg "TroubleshootingReference2")  
図 2. NTFS データ ストリーム  

 **図 2.NTFS データ ストリーム**  

 **解決方法 1:** インストール ソース ファイルを右クリックして、**[プロパティ]** をクリックします。 **[ブロック解除]** をクリックし、**[OK]** をクリックして、NTFS ファイル システム データ ストリームをファイルから削除します。 1 つまたは複数の NTFS ファイル システム データ ストリームの存在によってブロックされているインストール ソース ファイルごとに、このプロセスを繰り返します。  

 **解決方法 2:** 図 2 で示されているように、Streams ユーティリティを使って、インストール ソース ファイルから NTFS ファイル システム データ ストリームを削除します。 Streams ユーティリティは、1 つまたは複数のファイルまたはフォルダーから、NTFS ファイル システム データ ストリームを削除できます。  

####  <a name="LostNetworkConnections"></a> 失われたネットワーク接続  
 **問題:** デバイス ドライバーをインストールする場合、またはデバイスとネットワークの構成を変更する場合に、インストールが失敗する可能性があります。 これらの変更によってネットワーク接続が失われて、インストールが失敗する原因になる場合があります。  

 **解決方法:** ZTICacheUtil.vbs スクリプトを実装して、インストールのためのダウンロードと実行を可能にします。 このスクリプトは、アドバタイズを調整してダウンロードと実行を可能にするように設計されています。 Configuration Manager 配布ポイントが Web 分散オーサリングとバージョン管理で、バックグラウンド インテリジェント転送サービス \(BITS\) 対応の場合、ダウンロードは BITS を使います。 同時に、ZTICache.vbs script を最初に実行するように Configuration Manager を変更します。これにより、プログラムは展開プロセスの間に自分自身を削除しないようになります。  

####  <a name="MicrosoftOfficeSystem"></a> 2007 Microsoft Office system  
 **問題:** 2007 Office system を展開するときに、Windows インストーラー修正プログラム \(MSP\) ファイルを含んでいると、インストールはエラー コード 30029 で失敗する可能性があります。  

 さらに ZTIApplications.log を調査すると、次のようなメッセージが見つかります。  

-   ```  
    About to run command: \\Server\Deployment$\Tools\X86\bddrun.exe \\Server\Share\Microsoft\Office\2007\Professional\setup.exe /adminfile \\Server\Share\Microsoft\Office\2007\Professional\file.msp  
    ```  

-   ```  
    ZTI Heartbeat: command has been running for 12 minutes (process ID 1600) Return code from command = 30029  
    ```  

-   ```  
    Application Microsoft Office 2007 Professional returned an unexpected return code: 30029  
    ```  

 **解決方法 1:** MSP ファイルを Updates ディレクトリに再配置した後、**\/adminfile** オプションを指定しないで setup.exe を実行します。 インストール中の更新プログラムの展開については、「[2007 Office system を展開する](http://technet.microsoft.com/library/cc303395\(v=Office.12\).aspx)」をご覧ください。  

 **解決方法 2:** MSP ファイルで **[入力項目を表示しない]** チェック ボックスがオンになっていないことを確認します。 この設定を構成する方法については、「[2007 Office system 展開の概要](http://technet.microsoft.com/library/bb490141.aspx)」をご覧ください。  

### <a name="autologon"></a>自動ログオン  
 自動ログオンの問題と解決策を確認します。  

-   ログオン セキュリティ バナーによる、LTI およびゼロ タッチ インストール \(ZTI\) の展開プロセスの中断 (「[ログオン セキュリティ バナー](#LogonSecutiryBanners)」の説明を参照)  

-   ユーザー資格情報のプロンプトによる、LTI および ZTI の展開プロセスの中断 (「[ユーザー資格情報の入力要求](#PromtedforUserCredentials)」の説明を参照)  

####  <a name="LogonSecutiryBanners"></a> ログオン セキュリティ バナー  
 **問題:** MDT タスク シーケンスは対話式ユーザー セッションの間に処理され、ターゲット コンピューターは指定された管理者アカウントを使って自動的にログオンできる必要があります。 ログオン セキュリティ バナーを強制するグループ ポリシー オブジェクト \(GPO\) が適用されている場合、セキュリティ バナーはユーザーが示されたポリシーに同意するのを待機している間はログオン プロセスを停止するため、この自動ログオンの続行を許可されません。  

 **解決方法:** GPO が特定の組織単位 \(OU\) に適用され、既定のドメインの GPO に含まれないようにします。 ドメインにコンピューターを追加するときに、ログオン セキュリティ バナーを適用する GPO によって影響を受けない OU に追加されるように指定します。 タスク シーケンス エディターで、最後のタスク シーケンス ステップの 1 つとして、目的の OU にコンピューター アカウントを再配置するスクリプトを含めます。  

> [!NOTE]
>  既存の Active Directory® Domain Services \(AD DS\) アカウントを再利用している場合は、ターゲット コンピューターに展開する前に、セキュリティ ログオン バナーを適用する GPO によって影響を受けない OU に、ターゲット コンピューターのアカウントを再配置したことを確認します。  

####  <a name="PromtedforUserCredentials"></a> ユーザー資格情報の入力要求  
 **問題:** ドメインに参加しているコンピューターのイメージを作成しました。 ターゲット コンピューターに新しいイメージを展開するときに、自動ログオンが行われず、ユーザーに適切な資格情報の入力が要求されるため、展開プロセスが停止します。 資格情報が入力されて、ユーザーがログオンすると、展開プロセスは再開します。  

 **解決方法:** イメージをキャプチャするとき、ソース コンピューターがドメインに参加していてはなりません。 コンピューターがドメインに参加していた場合は、ワークグループにコンピューターを参加させ、イメージをキャプチャし直してから、ターゲット コンピューターに展開してみて、問題が解決するかどうかを判断します。  

### <a name="bios"></a>BIOS  
 **問題:** Intel vPro テクノロジが搭載されているターゲット コンピューターへの展開中に、展開が停止エラーで終了する場合があります。 更新されたすべてのドライバーが非インボックス ドライバーとして Deployment Workbench に含まれている場合でも、ターゲット コンピューターは起動しません。   

 解決方法: ターゲット コンピューターの基本入力\/出力システム \(BIOS\) の設定を調べて、既定のシリアル ATA (Serial Advanced Technology Attachment) モードが Advanced Host Controller Interface \(AHCI\) として構成されているかどうかを確認します。 残念ながら、特定の Windows オペレーティング システムは既定では AHCI をサポートしていません。  

### <a name="database-problems"></a>データベースの問題  
 データベース関連の問題と解決策を確認します。  

-   データベース サーバーで不適切に構成されたファイアウォールの結果として生成されるエラー (「[ブロックされた SQL Server ブラウザー要求](#BlockedSQLServerBrowserRequests)」の説明を参照)  

-   データベース サーバーとの接続が切断された結果として生成されるエラー (「[名前付きパイプによる接続](#NamedPipeConnections)」の説明を参照)  

####  <a name="BlockedSQLServerBrowserRequests"></a> ブロックされた SQL Server ブラウザー要求  
 **問題:** MDT 展開プロセスの間に、Microsoft SQL Server® データベースから情報を取得できます。 ただし、データベース サーバーでの不適切なファイアウォール構成に関するエラーが生成される場合があります。  

 **解決方法:** Windows Server の Windows ファイアウォールは、コンピューター リソースへの不正アクセスを防止するのに役立ちます。 ただし、ファイアウォールが正しく構成されていない場合、SQL Server インスタンスへの接続の試行がブロックされることがあります。 ファイアウォールの内側にある SQL Server のインスタンスにアクセスするには、SQL Server を実行しているコンピューターでファイアウォールを構成します。 SQL Server のファイアウォール ポートの構成については、Microsoft サポート技術情報「[Windows Server 2008 で SQL Server のファイアウォール ポートを開く方法](http://support.microsoft.com/kb/968872)」をご覧ください。  

####  <a name="NamedPipeConnections"></a> 名前付きパイプによる接続  
 **問題:** MDT 展開プロセスの間に、SQL Server データベースから情報を取得できます。 ただし、SQL Server との接続の断絶に関するエラーが発生する場合があります。 Microsoft SQL Server で名前付きパイプ接続を有効にしていないことが原因である可能性があります。  

 **解決方法:** これらの問題を解決するには、SQL Server で名前付きパイプを有効にします。 また、**SQLShare** プロパティを指定します。これは、名前付きパイプを使って外部データベースに接続するときに必要です。 名前付きパイプを使って接続するには、統合セキュリティを使ってデータベースへの接続を行います。 LTI 展開の場合を、指定したユーザー アカウントがデータベースへの接続を行います。 Configuration Manager を使う ZTI 展開では、ネットワーク アクセス アカウントがデータベースに接続します。 Windows PE には既定ではセキュリティ コンテキストがないため、データベース サーバーへのネットワーク接続を作成して、接続するユーザーのためのセキュリティ コンテキストを確立する必要があります。  

 **SQLShare** プロパティで指定されているネットワーク共有は、サーバーに接続して適切なセキュリティ コンテキストを取得するための手段を提供します。 共有に対する読み取りアクセス権が必要です。 接続が行われるときに、データベースへの名前付きパイプ接続を確立できます。 データベースに TCP\/IP 接続を行うときは、**SQLShare** プロパティは必要なく、使わないようにする必要があります。  

 使っている SQL Server のバージョンに基づいて、次のタスクを実行することにより、名前付きパイプ接続を有効にします。  

-   SQL Server 2008 R2 への名前付きパイプ接続を有効にするには、「[SQL Server 2008 R2 で名前付きパイプ接続を有効にする](#EnableNamedPipeConnectionsinSQLServer)」で説明されているようにします。  

-   SQL Server 2005 への名前付きパイプ接続を有効にするには、「[SQL Server 2005 で名前付きパイプ接続を有効にする](#EnableNamedPipeConnectionsinSQL)」で説明されているようにします。  

#####  <a name="EnableNamedPipeConnectionsinSQLServer"></a> SQL Server 2008 R2 で名前付きパイプ接続を有効にする  
 SQL Server 2008 R2 で名前付きパイプ接続を有効にするには、次の手順を実行します。  

1.  クエリ対象のデータベースをホストする SQL Server 2008 R2 を実行するコンピューターで、**[スタート]** ボタンをクリックして **[すべてのプログラム]** をポイントします。 **[Microsoft SQL Server 2008 R2]** をポイントして、**[SQL Server Management Studio]** をクリックします。  

2.  **Microsoft SQL Server Management Studio** コンソールの**オブジェクト エクスプローラー**で、***sql\_server\_name*** を右クリックして、**[プロパティ]** をクリックします \(*sql\_server\_name* は、構成する SQL Server を実行しているコンピューターの名前です\)。  

3.  [サーバーのプロパティ \- ***sql\_server\_name***] ダイアログ ボックスが表示されます。  

4.  **[サーバーのプロパティ \- ***sql\_server\_name***]** ダイアログ ボックスの **[ページの選択]** で、**[接続]** をクリックします。  

5.  **[接続]** ページで、**[このサーバーへのリモート接続を許可する]** チェック ボックスをオンにして、**[OK]** をクリックします。  

6.  Microsoft SQL Server Management Studio コンソールを閉じます。  

7.  クエリ対象のデータベースをホストする SQL Server 2008 R2 を実行するコンピューターで、**[スタート]** ボタンをクリックして **[すべてのプログラム]** をポイントします。 **[Microsoft SQL Server 2008 R2]**、**[構成ツール]** の順にポイントして、**[SQL Server 構成マネージャー]** をクリックします。  

8.  **SQL Server 構成マネージャー** コンソールで、[SQL Server Configuration Manager \(Local\)]\(SQL Server 構成マネージャー (ローカル)\) \/ [SQL Server ネットワークの構成] \/ [*sql\_instance* のプロトコル] の順に移動します \(*sql\_instance* は構成する SQL Server インスタンスの名前です\)。  

9. 詳細ウィンドウで **[名前付きパイプ]** を右クリックして、**[有効化]** をクリックします。  

     [警告] ダイアログ ボックスが表示され、変更は保存されますが、サービスを停止して再起動するまで有効にならないことが示されます。  

10. **[警告]** ダイアログ ボックスで、**[OK]** をクリックします。  

11. **SQL Server 構成マネージャー** コンソールで、[SQL Server Configuration Manager \(Local\)]\(SQL Server 構成マネージャー (ローカル)\) \/ [SQL Server のサービス] に移動します。  

12. 詳細ウィンドウで **[SQL Server* \(sql\_instance\)*]** を右クリックし、**[再起動]** をクリックします \(ここで *sql\_instance* は、ステップ 2 で構成した SQL Server インスタンスの名前です\)。  

     SQL Server 構成マネージャーの進行状況バーが表示され、サービスの再起動の状態が示されます。 サービスが再起動すると、進行状況バーは閉じます。  

13. SQL Server 構成マネージャー コンソールを閉じます。  

 詳細については、「[How to enable remote connections in SQL Server 2008](http://blogs.msdn.com/b/walzenbach/archive/2010/04/14/how-to-enable-remote-connections-in-sql-server-2008.aspx)」(SQL Server 2008 でリモート接続を有効にする方法) をご覧ください。  

#####  <a name="EnableNamedPipeConnectionsinSQL"></a> SQL Server 2005 で名前付きパイプ接続を有効にする  
 SQL Server 2005 で名前付きパイプ接続を有効にするには、次の手順を実行します。  

1.  クエリ対象のデータベースをホストする SQL Server 2005 を実行するコンピューターで、**[スタート]** ボタンをクリックして **[すべてのプログラム]** をポイントします。 **[Microsoft SQL Server 2005]**、**[構成ツール]** の順にポイントして、**[SQL Server セキュリティ構成]** をクリックします。  

2.  **[SQL Server 2005 セキュリティ構成]** ダイアログ ボックスで、**[サービスと接続のセキュリティ構成]** をクリックします。  

3.  **[サービスと接続のセキュリティ構成 – *server\_name*]** ダイアログ ボックス \(*server\_name* は、SQL Server 2005 を実行しているコンピューターの名前です\) の **[コンポーネントを選択して、サービスおよび接続を構成してください]** で、[MSSQLSERVER]\\[データベース エンジン] に移動し、**[リモート接続]** をクリックします。  

4.  **[ローカル接続およびリモート接続]** をクリックし、**[TCP\/IP および名前付きパイプを使用する]** をクリックして、**[適用]** をクリックします。  

5.  **[サービスと接続のセキュリティ構成 – *server\_name*]** ダイアログ ボックス \(*server\_name* は、SQL Server 2005 を実行しているコンピューターの名前です\) の **[コンポーネントを選択して、サービスおよび接続を構成してください]** で、[MSSQLSERVER]\\[データベース エンジン] に移動し、**[サービス]** をクリックします。  

6.  **[停止]** をクリックします。  

     MSSQLSERVER サービスが停止します。  

7.  **[開始]** をクリックします。  

     MSSQLSERVER サービスが開始します。  

8.  **[OK]** をクリックします。  

9. [SQL Server 2005 セキュリティ構成] を閉じます。  

 詳細については、Microsoft サポート技術情報「[リモート接続が許可されるように SQL Server 2005 を構成する方法](http://support.microsoft.com/kb/914277)」をご覧ください。  

### <a name="deployment-scripts"></a>展開スクリプト  
 MDT 関連の問題と解決策を確認します。  

-   ユーザーの資格情報の入力を求められて、エラー 0x80070035 を受け取る可能性がある (「[Credentials_script](#Credentials_script)」の説明を参照)  

-   エラー メッセージ "Wuredist.cab が見つかりません" が表示される (「[ZTIWindowsUpdate](#ZTIWindowsUpdate)」の説明を参照)  

####  <a name="Credentials_script"></a> Credentials\_script  
 **問題:** 新しく展開されたコンピューターの最後の起動中に、ユーザーにユーザー資格情報の入力が要求され、ネットワーク パスが見つからなかったことを示すエラー 0x80070035 を受け取る場合があります。  

 **解決方法:** WIM ファイルに MININT または \_SMSTaskSequence フォルダーが含まれないことを確認します。 これらのフォルダーを削除するには、最初に ImageX ユーティリティを使って WIM ファイルをマウントしてから、フォルダーを削除します。  

> [!NOTE]
>  WIM ファイルからフォルダーを削除しようとするとアクセス拒否エラーが発生する場合は、コマンド プロンプト ウィンドウを開き、WIM ファイルに含まれるイメージのルートに切り替えて、**RD MININT** および **RD \_SMSTaskSequence** を実行します。  

####  <a name="ZTIWindowsUpdate"></a> ZTIWindowsUpdate  
 **問題:** ZTIWindowsUpdate.wsf スクリプトを使って展開の間にソフトウェア更新プログラムを適用する場合は、このスクリプトが、Microsoft Update Web サイトと直接通信して必要な Windows Update エージェント バイナリをダウンロードしてインストールし、適用可能なソフトウェア更新プログラムをスキャンし、適用可能なソフトウェア更新プログラムのバイナリ ファイルをダウンロードして、ダウンロードしたバイナリをインストールする可能性があることに注意してください。 このプロセスでは、ターゲット コンピューターが Microsoft Update Web サイトにアクセスできるようにネットワーク インフラストラクチャを構成する必要があります。  

 展開の共有に Windows Update エージェントのインストール ファイルが含まれず、ターゲット コンピューターに適切なインターネット アクセスが設定されていない場合は、ZTIWindowsUpdate.log ファイルと BDD.log ファイルでエラー "wuredist.cab が見つかりません" が報告されます。  

 **解決方法:** MDT "*ツールキット リファレンス*" に関するドキュメントの "ZTIWindowsUpdate.wsf" のセクションで説明されている手順に従います。  

### <a name="deployment-shares"></a>展開共有  
 展開共有に関連する問題と解決策を確認します。  

-   展開共有を更新すると WIM ファイルの更新が失敗する (「[WIM ファイルの更新の失敗](#FailuretoUpdateWIMFiles)」の説明を参照)  

####  <a name="FailuretoUpdateWIMFiles"></a> WIM ファイルの更新の失敗  
 "単純な" 環境の場合:  

-   MDT は、通常、WIMGAPI.DLL を C:\\Windows\\system32 から取得します \(常にパス内\)。 この WIMGAPI.DLL のバージョンは、オペレーティング システムのバージョン \(ビルド\) と一致する必要があります。  

-   64 ビットのオペレーティング システムでは、MDT は常に x64 WIMGAPI.DLL ファイルを使います。システムの PATH には、そのファイルのみが存在していなければなりません。 32 ビットのオペレーティング システムでは、MDT は常に x86 WIMGAPI.DLL ファイルを使います。システムの PATH には、そのファイルのみが存在していなければなりません  \(Configuration Manager などの他の製品は 32 ビット版の WIMGAPI.DLL を使用し、64 ビットのオペレーティング システムであっても、32 ビット版を管理およびインストールします\)。  

 **問題:** 展開共有を更新しようとすると、.wim ファイルのマウントが成功しなかったことが通知されます。  

 **解決方法:** コマンド プロンプト ウィンドウを開き、**where WIMGAPI.DLL** を実行します。 一覧の最初のエントリ \(パスを検索して最初に見つかった場所\) について、**Version** プロパティが、インストールされている Windows アセスメント & デプロイメント キット \(Windows ADK\) のビルドと一致することを確認します。 また、プロパティがオペレーティング システムのビルド番号と一致することを確認します。  

### <a name="the-windows-deployment-wizard"></a>Windows 展開ウィザード  
 Windows 展開ウィザードに関連する問題と解決策を確認します。  

-   Windows 展開ウィザードのページをスキップするように LTI が構成されていても、ウィザードのページが表示される (「[ウィザードのページがスキップされない](#WizardPagesareNotSkipped)」の説明を参照)  

####  <a name="WizardPagesareNotSkipped"></a> ウィザードのページがスキップされない  
 **問題:** MDT DB または CustomSettings.ini ファイルでウィザードをスキップする必要があるように指定されていても、ウィザードのページが表示されます。  

 **解決方法:** ウィザードのページが正しくスキップされるようにするには、そのウィザードのページで指定されているすべてのプロパティを、MDT DB または CustomSettings.ini ファイルの適切な場所に、適切な値と供に含めます。 スキップするウィザード ページのプロパティが正しく構成されていない場合は、そのページが表示されます。 ウィザード ページをスキップするために必要なプロパティについては、MDT ドキュメント "*ツールキット リファレンス*" のスキップされる展開ウィザード ページのプロパティに関するセクションをご覧ください。  

### <a name="disks-and-partitioning"></a>ディスクとパーティション分割  
 ディスクのパーティション分割に関する問題と解決策を確認します。  

-   BitLocker® ドライブ暗号化の問題 (「[BitLocker ドライブ暗号化](#BitLockerDriveEncryption)」の説明を参照)  

-   ディスク パーティション分割のエラー (ディスク パーティション分割のエラーに関する説明を参照)  

-   論理ディスクまたはダイナミック ディスクが原因で発生するコンピューター更新の展開シナリオの間のエラー (「[論理ディスクとダイナミック ディスクのサポート](#SupportforLoogicalandDynamicDisks)」の説明を参照)  

####  <a name="BitLockerDriveEncryption"></a> BitLocker ドライブ暗号化  
 BitLocker を展開するには、適切な展開のための特定の構成が必要です。 以下の潜在的な問題は、ターゲット コンピューターの構成に関係する場合があります。  

-   ZTI および UDI の展開で、ZTIBde.wsf スクリプトがエラー "レジストリ キー 'HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName' を開いて読み取ることができません" で失敗する (「[ZTIBde.wsf スクリプトがエラー "レジストリ キー 'HKEY_CURRENT_USER\Control Panel\International\LocaleName' を開いて読み取ることができません" で失敗する](#ZTIBde.wsf)」の説明を参照)  

-   ターゲット コンピューター上の USB デバイス、CD ドライブ、DVD ドライブ、他のリムーバブル メディア デバイスが複数のドライブ文字として表示される (「[デバイスが複数のドライブ文字として表示される](#DevicesAppearasMultipleDriveLetters)」の説明を参照)  

-   未割り当ての十分なディスク領域を提供するためのターゲット コンピューター上のドライブ C の圧縮 (「[ディスクの圧縮に関する問題](#ProblemswithShrinkingDisks)」の説明を参照)  

#####  <a name="ZTIBde.wsf"></a> ZTIBde.wsf スクリプトがエラー "レジストリ キー 'HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName' を開いて読み取ることができません" で失敗する  
 **Problem:** ZTI または UDI でターゲット コンピューターに BitLocker を展開しようとすると、ZTIBde.wsf スクリプトがエラー "レジストリ キー 'HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName' を開いて読み取ることができません" で失敗します。  

 **解決方法:** **UILanguage** プロパティでロケールを指定します。 ZTI と UDI では、ZTIBde.wsf スクリプトはシステムの制御内で実行されるので、完全なユーザー プロファイルは読み込まれません。 ZTIBde.wsf スクリプトがロケール情報を読み取ろうとしても、レジストリ \(user profile\) は完全には読み込まれないので、ロケール情報はレジストリにありません。 回避策としては、**UILanguage** プロパティでロケールを指定します。  

#####  <a name="DevicesAppearasMultipleDriveLetters"></a> デバイスが複数のドライブ文字として表示される  
 **問題:** 一部のデバイスが、パーティション分割の方法によっては、複数の論理ドライブ文字で表示されます。 場合によっては、このようなデバイスは 1.44 メガバイト \(MB\) のフロッピー ディスク ドライブやメモリ ストレージ ドライブをエミュレートできます。 したがって、Windows は、同じデバイス ドライブ文字 A および B をフロッピー ディスク エミュレーション用に、F をメモリ ストレージ ドライブ用に割り当てることがあります。 既定では、MDT スクリプトはアルファベット順で最も早いドライブ文字を使います \(この例では A\)。  

 **解決方法:** Windows 展開ウィザードの **[Specify the BitLocker recovery details]\(BitLocker 復旧の詳細を指定する\)** ページで既定の設定を上書きします。 Windows 展開ウィザードの概要ページでは、BitLocker 復旧情報の格納に選択されたドライブ文字をユーザーに通知する警告が表示されます。 さらに、BDD.log および ZTIBDE.log ファイルには、検出されたリムーバブル メディア デバイスと、BitLocker 復旧情報の格納に選択されたデバイスが記録されます。  

#####  <a name="ProblemswithShrinkingDisks"></a> ディスクの圧縮に関する問題  
 **問題:** ターゲット コンピューターに、BitLocker を有効にするのに十分な未割り当てのディスク領域が存在しません。 ターゲット コンピューターに BitLocker を展開するには、システム ボリュームを作成するために、少なくとも 2 ギガバイト \(GB\) の未割り当てディスク領域が必要です。 "*システム ボリューム*" は、BIOS がコンピューターを起動した後で Windows を読み込むために必要なハードウェア固有のファイルを含むボリュームです。  

 **解決方法 1:** 既存のコンピューターで Diskpart ツールを使ってドライブ C を圧縮し、システム ボリュームを作成できるようにします。 ただし、一部のインスタンスでは、おそらくドライブ C 内の断片化されたディスク領域のために、Diskpart ツールを使用しても、2 GB の未割り当てディスク領域を提供できるほど十分にドライブ C を縮小できないことがあります。  

 この問題に対して考えられる 1 つの解決策は、ドライブ C を最適化することです。そのためには次の手順のようにします。  

1.  Diskpart の **shrink querymax** コマンドを実行して、未割り当てにできるディスク領域の最大量を確認します。  

2.  ステップ 1 で返された値が 2 GB 未満の場合は、ドライブ C で不要なファイルを削除してから最適化します。  

3.  Diskpart の **shrink querymax** コマンドを再び実行して、2 GB より多くのディスク領域を未割り当てにできることを確認します。  

4.  ステップ 3 で返される値が 2 GB より小さい場合は、次のいずれかのようにします。  

    -   ドライブ C を複数回最適化して、完全に最適化されるようにします。  

    -   ドライブ C 上のデータをバックアップし、既存のパーティションを削除し、新しいパーティションを作成して、新しいパーティションにデータを復元します。  

 **解決方法 2:** ZTIBDE.wsf スクリプトは、ディスク準備ツール \(bdehdcfg.exe\) を実行し、システム ボリュームのパーティション サイズを既定の 2 GB に構成します。 必要な場合は、ZTIBDE.wsf スクリプトをカスタマイズして既定値を変更できます。 ただし、MDT スクリプトを変更することは推奨されません。  

####  <a name="SupportforLoogicalandDynamicDisks"></a> 論理ディスクとダイナミック ディスクのサポート  
 **問題:** コンピューター更新の展開シナリオを実行するとき、論理ドライブまたはダイナミック ディスクを使っているターゲット コンピューターに展開すると、展開プロセスが失敗することがあります。  

 **解決方法:** MDT は、論理ドライブまたはダイナミック ディスクへのオペレーティング システムの展開はサポートしていません。  

### <a name="domain-join"></a>ドメイン参加  
 **問題:** 展開時には、Windows 展開ウィザードを使って、資格情報、ドメイン参加情報、静的 IP 構成などの必要なすべての情報をターゲット コンピューターに提供します。 セットアップが完了すると、システムがドメインに参加しておらず、まだワークグループ内にあるように表示されることがあります。  

 **解決方法:** MDT の LTI 展開は、オペレーティング システムが稼働状態になった後で、静的 IP の情報を構成します。 ターゲット コンピューターが動的ホスト構成プロトコル \(DHCP\) のないネットワーク セグメント上にある場合、Unattend.xml で指定されている自動ドメイン参加は、DHCP が存在しない場合は失敗します。  

 ワークグループに参加するように Unattend.xml を構成します。 その後、組み込みの**ドメインからの復旧**タスク シーケンス ステップを使って、静的 IP が適用された後でドメインに参加するステップをタスク シーケンスに追加します。  

### <a name="driver-installation"></a>ドライバーのインストール  
 できるだけ最適なユーザー エクスペリエンスにするには、ハードウェア デバイスとソフトウェア ドライバーのインストールが、ユーザーの介入がほとんど、またはまったくなしに、可能な限りシームレスに実行されるようにする必要があります。 Microsoft からは、この目標を達成するインストール パッケージの作成に役立つツールとガイドラインが提供されています。 ドライバーのインストールに関する一般的な情報については、「[Device and Driver Installation](http://www.microsoft.com/whdc/driver/install/default.mspx)」(デバイスとドライバーのインストール) をご覧ください。  

 デバイス ドライバーのインストールに関連した問題と解決策を確認します。  

-   $OEM$ 大容量記憶装置ドライバーを MDT で使用すると発生する問題 ($OEM$ 大容量記憶装置ドライバーと MDT 大容量記憶装置ロジックの組み合わせに関する説明を参照)  

-   SetupAPI.log を使用したデバイス ドライバーのインストールの問題のトラブルシューティング (「[SetupAPI.log でのデバイスのインストールのトラブルシューティング](#TroubleshootDeviceInstallationwithSetupAPI.log)」の説明を参照)  

####  <a name="TroubleshootDeviceInstallationwithSetupAPI.log"></a> SetupAPI.log でのデバイスのインストールのトラブルシューティング  
 ホワイト ペーパー「[Troubleshooting Device Installation with the SetupAPI Log File](http://msdn.microsoft.com/windows/hardware/gg463393.aspx)」(SetupAPI ログ ファイルでのデバイスのインストールのトラブルシューティング) では、Windows デバイスのインストールに関する情報が提供されています。 具体的には、SetupAPI ログ ファイルの解釈に関するドライバーの開発者とテスト担当者に対するガイドラインが示されています。  

 デバッグの目的に最も役に立つログ ファイルの 1 つは、SetupAPI.log ファイルです。 このプレーンテキスト ファイルには、デバイスのインストール、サービス パックのインストール、更新プログラムのインストールに関して SetupAPI が記録する情報が保持されています。 具体的には、デバイスとドライバーの変更、および最新の Windows インストール以降に行われた主要なシステム変更の記録が保持されます。 このホワイト ペーパーの焦点は、SetupAPI ログ ファイルを使用したデバイスのインストールのトラブルシューティングです。サービス パックおよび更新プログラムのインストールに関連付けられているログ ファイルのセクションについては説明されていません。  

### <a name="new-computer-deployments"></a>新しいコンピューターの展開  
 コンピューターの新規展開シナリオに関連する問題と解決策を確認します。  

-   Preboot Execution Environment \(PXE\) ブートを使用する展開プロセスの開始に関する問題 (「[PXE ブート](#PXEBoot)」の説明を参照)  

####  <a name="PXEBoot"></a> PXE ブート  
 簡単に説明すると、PXE プロトコルは次のように動作します。クライアント コンピューターは、PXE プロトコルを実装するクライアント コンピューターから送信された要求を識別する拡張機能を含む DHCP 検出パケットをブロードキャストすることによって、プロトコルを開始します。 この拡張プロトコルを実装しているブート サーバーを利用できるものとすると、ブート サーバーはクライアントにサービスを提供するサーバーの IP アドレスを含むオファーを送信します。 クライアントは、簡易ファイル転送プロトコルを使って、ブート サーバーから実行可能ファイルをダウンロードします。 最後に、クライアント コンピューターは、ダウンロードしたブートストラップ プログラムを実行します。  

 このプロトコルの最初のフェーズは、DHCP メッセージのサブセットにピギーバックして、クライアントがブート サーバー \(つまり、新しいコンピューターのセットアップ用の実行可能ファイルを配信するサーバー\) を検出できるようにします。 クライアント コンピューターは、IP アドレスを取得する機会を使用できますが \(これが期待される動作です\)、それを行わなくてもかまいません。  

 このプロトコルの 2 番目のフェーズはクライアント コンピューターとブート サーバーの間で行われ、通信の便利な形式として DHCP メッセージ形式を使います。 この 2 番目のフェーズは、それ以外については、標準的な DHCP サービスと関係ありません。 以下では、PXE クライアント コンピューターの初期化プロセスの手順の概要を説明します。  

 レガシ モードまたは混合モードで実行している Windows 展開サービスでの PXE ブートに関連する問題のトラブルシューティングについては、Microsoft サポート技術情報「[Description of PXE Interaction Among PXE Client, DHCP, and RIS Server](http://support.microsoft.com/kb/244036)」(PXE クライアント、DHCP、RIS サーバーの間で行われる PXE のやり取りの説明) をご覧ください。  

 PXE ブートの問題について次の解決策を確認します。  

-   SetupAPI.log への Windows PE のログ記録を無効にする (「[Windows 展開サービスで Windows PE のログ記録を無効にする](#DisableWindowsPELogginginWindowsDeploymentServices)」の説明を参照)  

-   DHCP が正しく構成されていることを確認する (「[適切な DHCP の構成を確認する](#EnsuretheProperDHCPConfiguration)」の説明を参照)  

-   PXE クライアント コンピューターへの IP アドレス割り当ての応答時間を短縮する (「[PXE の IP アドレス割り当て応答時間を短縮する](#ImprovePXEIPAddressAssignmentResponseTime)」の説明を参照)  

#####  <a name="DisableWindowsPELogginginWindowsDeploymentServices"></a> Windows 展開サービスで Windows PE のログ記録を無効にする  
 推奨される最初の手順は、setupapi.log へのログ記録が無効になっていることを確認することです。  

#####  <a name="EnsuretheProperDHCPConfiguration"></a> 適切な DHCP の構成を確認する  
 使われているルーターのモデルによっては、DHCP ブロードキャスト転送の特定のルーター構成が、サブネット \(またはルーター インターフェイス\) または特定のホストに対してサポートされている場合があります。 DHCP サーバーと Windows 展開サービスを実行するコンピューターが異なるコンピューターの場合は、DHCP サーバーと Windows 展開サービス サーバーの両方がクライアント ブロードキャストを受信するように、DHCP ブロードキャストを転送するルーターが設計されていることを確認します。そうでない場合、クライアント コンピューターは、リモート ブート要求への応答を受信しません。  

 クライアント コンピューターとリモート インストール サーバーの間に、DHCP ベースの要求または応答の通過を許可しないルーターが存在しますか。 Windows 展開サービス クライアント コンピューターと Windows 展開サービス サーバーが異なるサブネット上にある場合は、Windows 展開サービス サーバーに DHCP パケットを転送するように、2 つのシステムの間のルーターを構成します。 Windows 展開サービス クライアント コンピューターは DHCP ブロードキャスト メッセージを使って Windows 展開サービス サーバーを検出するので、このように設定する必要があります。 ルーターに DHCP 転送が設定されていないと、クライアント コンピューターの DHCP ブロードキャストは、Windows 展開サービス サーバーに到達できません。 この DHCP 転送プロセスは、ルーターの構成マニュアルでは "*DHCP プロキシ*" または "*IP ヘルパー アドレス*" と呼ばれることもあります。 特定のルーターでの DHCP 転送の設定については、ルーターの説明をご覧ください。  

#####  <a name="ImprovePXEIPAddressAssignmentResponseTime"></a> PXE の IP アドレス割り当て応答時間を短縮する  
 PXE クライアント コンピューターが IP アドレスを取得するまでに長い時間 \(15 - 20 秒\) がかかる場合は、次の要素をチェックします。  

-   ターゲット コンピューターのネットワーク アダプターと、スイッチまたはルーターが、同じ速度に設定されているか \(自動、二重、完全など\)。  

-   Windows 展開サービス サーバーの IP アドレスが、接続が経由するルーターの IP ヘルパー ファイルに含まれるか。 IP ヘルパー ファイルの IP アドレスのリストが長い場合、Windows 展開サービス サーバーのアドレスを上の方に移動できるか。  

### <a name="restarting-the-deployment-process"></a>展開プロセスを開始し直す  
 **問題:** 新しいまたは変更したタスク シーケンスをテストおよびトラブルシューティングするとき、展開プロセスを最初からやり直すことができるように、ターゲット コンピューターの再起動が必要になることがあります。 このとき、MDT はハード ディスクにデータを書き込むことによって進行状況を追跡しているため、予期しない結果が発生することがあります。ターゲット コンピューターを再起動すると、MDT は前回の再起動で終了したところから再開します。  

 **解決方法:** 展開プロセスを先頭から再び開始するには、ターゲット コンピューターを再起動する前に、C:\\MININT and C:\\\_SMSTaskSequence フォルダーを削除します。  

### <a name="sysprep"></a>Sysprep  
 Sysprep 関連の問題と解決策を確認します。  

-   ターゲット コンピューターが正しい AD DS OU に表示されない (「[コンピューター アカウントの OU が正しくない](#ComputerAccountisintheWrongOU)」の説明を参照)  

####  <a name="ComputerAccountisintheWrongOU"></a> コンピューター アカウントの OU が正しくない  
 **問題:** ターゲット コンピューターは正しくドメインに参加していますが、コンピューター アカウントは正しくない OU に存在します。  

 **解決方法 1:** アカウントがターゲット コンピューターに事前に存在している場合、アカウントは元の OU に残ります。 アカウントを指定した OU に移動するには、Microsoft Visual Basic® Scripting Edition などの自動化ツールを使うタスク シーケンス ステップを追加して、アカウントを移動します。  

 **解決方法 2:** 指定した OU が正しい形式であり、存在することを確認します。 OU の正しい形式は `OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com` です。  

### <a name="configuration-manager"></a>Configuration Manager  
 **問題:** **[自己署名入り PXE 証明書を作成する]** オプションを使って Configuration Manager PXE サービス ポイントを作成しようとすると、図 3 のようなエラー メッセージが表示されます。  

 ![TroubleshootingReference3](media/TroubleshootingReference3.jpg "TroubleshootingReference3")  
図 SEQ 図 \\\* アラビア語 3. PXE サービス ポイント エラー  

 **図 SEQ 図 \\\* アラビア語 3.PXE サービス ポイント エラー**  

 **解決方法:** 構成しているサーバーに PXE サービス ポイントが以前存在した場合、それをアンインストールしたときに、PXE サービス ポイントが自己作成した証明書を削除していない可能性があります。 PXE 証明書フォルダーを、C:\\Documents and Settings\\*user\_name*\\Application Data\\Microsoft\\Crypto\\RSA から削除します。*user\_name* は、現在の構成を実行しているユーザーまたは以前に構成を実行したユーザーの名前です。 フォルダーを削除すると、Configuration Manager コンソールのサイトの役割の新規作成ウィザードは正常に完了するはずです。  

### <a name="task-sequences"></a>タスク シーケンス  
 タスク シーケンスに関連した問題と解決策を確認します。  

-   タスク シーケンスが正常に完了しないか、予期しない動作を示す (「[タスク シーケンスが正常に完了しない](#TaskSequenceDoesNotFinishSuccessfully)」の説明を参照)。  

-   LTI の相手先ブランド供給 \(OEM\) タスク シーケンスが、異なるプロセッサ アーキテクチャのブート イメージで一覧表示される (「[OEM タスク シーケンスが異なるプロセッサ アーキテクチャに作成されたブート イメージに誤って表示される](#OEMTaskSequenceIncorrectlyAppearsforBootImage)」の説明を参照)。  

-   Windows 展開ウィザードでエラー メッセージ "Bad Task Sequence Item \(Invalid OS GUID\)" (不正なタスク シーケンス項目 (無効な OS GUID)) が表示される ([Windows 展開ウィザードでの不正なタスク シーケンス項目 (無効な OS GUID) というメッセージ](#BadTaskSequenceItem)の説明を参照)。  

-   ネットワーク接続名を構成するときに、"Please enter a valid name for the network adapter" (ネットワーク アダプターの有効な名前を入力してください) というメッセージが表示される (「[ネットワークの設定の適用](#ApplyNetworkSettings)」の説明を参照)。  

-   タスク シーケンス ステップの [エラー時に続行する] 構成設定の不適切な構成の結果として発生する可能性がある問題 (「[[エラー時に続行する] の使用](#UseContinueonError)」の説明を参照)。  

####  <a name="TaskSequenceDoesNotFinishSuccessfully"></a> タスク シーケンスが正常に完了しない  
 **問題:** タスク シーケンスが正常に完了しないか、予期しない動作を示す可能性があります。  

 **解決方法:** **オペレーティング システムのインストール** タスク シーケンス ステップ \(LTI の場合\) または**オペレーティング システム イメージの適用**タスク シーケンス ステップ \(UDI および ZTI の場合\) がタスク シーケンス ステップの作成後に変更された場合、予期しない結果になる可能性があります。 たとえば、32 ビットの Windows 8.1 イメージを展開するタスク シーケンスを作成した後、**オペレーティング システムのインストール**または**オペレーティング システム イメージの適用**タスク シーケンス ステップが、64 ビットの Windows 8.1 イメージを参照するように変更した場合、タスク シーケンスの実行が成功しない可能性があります。  

 異なるオペレーティング システム イメージを展開する場合は、新しいタスク シーケンスを作成することをお勧めします。  

####  <a name="OEMTaskSequenceIncorrectlyAppearsforBootImage"></a> OEM タスク シーケンスが異なるプロセッサ アーキテクチャに作成されたブート イメージに誤って表示される  
 **問題:** LTI OEM タスク シーケンス テンプレートに基づくタスク シーケンスが、異なるプロセッサ アーキテクチャのブート イメージに表示されます。 たとえば、64 ビットのオペレーティング システムを展開する OEM タスク シーケンスが、32 ビットのブート イメージに表示されます。  

 **解決方法:** LTI の OEM タスク シーケンスは "プラットフォーム固有" と見なされないので、ブート イメージのプロセッサ アーキテクチャに関係なく、常に一覧に表示されるのは想定される動作です。  

####  <a name="BadTaskSequenceItem"></a> Windows 展開ウィザードでの不正なタスク シーケンス項目 \(無効な OS GUID\) というメッセージ  
 **問題:** Windows 展開ウィザードを実行すると、ウィザードに "Bad Task Sequence Item \(Invalid OS GUID\)" (不正なタスク シーケンス項目 (無効な OS GUID)) というエラー メッセージが表示されます。 オペレーティング システムは OperatingSystem.xml ファイルの一覧に含まれますが、Deployment Workbench には表示されません。  

 **解決方法:** 元のオペレーティング システム ソースに、複数の WIM ファイルが関連付けられています。 タスク シーケンスに関連付けられている SKU は削除されますが、オペレーティング システム ソースのそれ以外の SKU はまだ存在します。 Windows 展開ウィザードの **[Select a task sequence to execute on this computer]\(このコンピューターで実行するタスク シーケンスの選択\)** ウィザード ページで、削除された SKU を参照するタスク シーケンスを選ぶと、ウィザード ページの **[次へ]** をクリックした後で、"Bad Task Sequence Item \(Invalid OS GUID\)" (不正なタスク シーケンス項目 (無効な OS GUID)) というエラー メッセージが表示されます。  

 この問題を解決するには、次のいずれかを実行します。  

-   オペレーティング システム ソースからすべての SKU を削除します。 Windows 展開ウィザードは通常どおり動作し、エラー メッセージは表示されません。  

-   別のオペレーティング システム イメージを使うようにタスク シーケンスを変更します。  

####  <a name="ApplyNetworkSettings"></a> ネットワーク設定の適用  
 **問題:** Deployment Workbench でネットワーク接続名を構成するとき、検証エラーで "Please enter a valid name for the network adapter" (ネットワーク アダプターの有効な名前を入力してください) というメッセージが表示されます。  

 **解決方法:** 指定した接続名からスペースと無効な文字を削除します。  

####  <a name="UseContinueonError"></a> [エラー時に続行する] の使用  
 MDT タスク シーケンスがエラー時に続行しないように構成されていて、そのタスク シーケンスがエラーを返した場合、そのタスク シーケンス グループ内の残りのタスク シーケンスはすべてスキップされます。 ただし、残りのタスク シーケンス グループは処理されます。 次の点を考慮します。  

 2 つのタスク シーケンス グループが作成されていて、どちらのグループにも複数のタスク シーケンス ステップが含まれます。  

-   グループ A  

    -   ステップ A  

    -   ステップ B  

-   グループ B  

    -   ステップ A  

    -   ステップ B  

 グループ A\\ステップ A がエラー時に続行しないように構成されていると、グループ A\\ステップ B は処理されません。 ただし、グループ B のすべてのタスク シーケンス ステップは処理されます。  

### <a name="the-user-state-migration-tool"></a>ユーザー状態移行ツール  
 USMT 関連の問題と解決策を確認します。  

-   ネットワーク共有フォルダーに格納されているドキュメントを参照するショートカットが正しく復元されない場合がある (「[見つからないデスクトップ ショートカット](#MissingDesktopShortcuts)」の説明を参照)  

####  <a name="MissingDesktopShortcuts"></a> 見つからないデスクトップ ショートカット  
 **問題:** USMT を使ってユーザー データを移行しているとき、ネットワーク ドキュメントを参照しているショートカットが復元されないことがあります。 Scanstate の間にショートカットはキャプチャされますが、Loadstate の間にターゲット コンピューターに復元されません。  

 **解決方法:** MigUser.xml ファイルを編集して、次の行をコメントにします。  

 変更前:  

```  
<include> filter='MigXmlHelper.IgnoreIrrelevantLinks()'>  
```  

 変更後:  

```  
<include> <!-- filter='MigXmlHelper.IgnoreIrrelevantLinks()'> -->  
```  

### <a name="windows-imaging-format-files"></a>Windows イメージング形式ファイル  
 WIM 関連の問題と解決策を確認します。  

-   LTI および ZTI の展開が失敗し、WIM ファイル エラーが BDD.log ファイルに記録される (「[壊れた WIM ファイル](#CorruptWIMFile)」の説明を参照)  

####  <a name="CorruptWIMFile"></a> 壊れた WIM ファイル  
 **問題:** イメージを展開するとき、展開が失敗して、BDD.log ファイルに次のエントリが作成されます。  

-   ```  
    The image \\Server\Deployment$\Operating Systems\Windows\version1.wim was not applied successfully by ImageX, rc = 2  
    ```  

-   ```  
    LTIApply COMPLETED.  Return Value = 2  
    ```  

-   ```  
    ZTI ERROR - Non-zero return code by LTIApply, rc = 2  
    ```  

 "データが無効です" というエラーに含まれる ImageX の結果を使って WIM ファイルをマウントすることにより、問題を調査します。 さらに調査すると、.wim ファイルの日付スタンプが、現在の日付より何年も前であることがわかります。 ウイルス検索プログラムなどの別のプロセスが、以前に読み取りまたは書き込みプロセスの終了時に .wim ファイルを開いたままにしていた可能性があります。  

 **解決方法:** .wim ファイルをバックアップ メディアから復元します。  

### <a name="windows-pe"></a>Windows PE  
 Windows PE 関連の問題と解決策を確認します。  

-   RAM またはワイヤレス ネットワーク アダプターの不足のために、LTI または ZTI の展開プロセスが開始されない (「[展開プロセスが開始しない — RAM またはワイヤレス ネットワーク アダプターの制限](#LimitedRamorWirelessNetworkAdapter)」の説明を参照)。  

-   Windows PE コンポーネントが見つからないために、LTI または ZTI の展開プロセスが開始されない (「[展開プロセスが開始しない — 見つからないコンポーネント](#MissingComponents)」の説明を参照)  

-   デバイス ドライバーが見つからないか正しくないために、LTI または ZTI の展開プロセスが開始されない (「[展開プロセスが開始しない — 見つからないか正しくないドライバー](#MissingorIncorrectDrivers)」の説明を参照)  

####  <a name="LimitedRamorWirelessNetworkAdapter"></a> 展開プロセスが開始しない — RAM またはワイヤレス ネットワーク アダプターの制限  
 **問題:** 特定のターゲット コンピューターにイメージを展開するときに、Windows PE が起動し、**wpeinit** を実行して、コマンド プロンプト ウィンドウを開きますが、実際には展開プロセスを開始しません。 ターゲット コンピューターからネットワーク ドライブをマッピングすることによって問題のトラブルシューティングを行うと、ネットワーク アダプター ドライバーが読み込まれていないことを示します。  

 **解決方法 1:** RAM が不足しているため、展開ウィザードが開始しません。 ターゲット コンピューターに少なくとも 512 MB の RAM があること、および 512 MB のうち 64 MB より多くが共有ビデオ メモリによって消費されていないことを確認します。  

 MDT がサポートする Windows PE のバージョンは、RAM が 512 MB 未満のターゲット コンピューターでは実行できません。  

 **解決方法 2:** ワイヤレス ドライバーを Windows PE イメージに含めないようにします。  

####  <a name="MissingComponents"></a> 展開プロセスが開始しない — 見つからないコンポーネント  
 **問題:** 失敗した展開のトラブルシューティングで BDD.log ファイルを確認すると、次のエントリが一覧に表示されます。  

```  
ERROR - Unable to create ADODB.Connection object, impossible to query SQL Server: ActiveX component can't create object (429).  
```  

 **解決方法:** このエラーは、Windows PE のイメージが MDT を使用して作成されなかったことを示す可能性があります。 Configuration Manager を使っている場合は、Configuration Manager が作成した既存の Windows PE イメージの 1 つを使わないでください。代わりに、インポート Microsoft 展開タスク シーケンス ウィザードを使ってイメージを作成します。  

> [!NOTE]
>  Configuration Manager が作成する Windows PE イメージには、スクリプト、XML、および Windows Management Instrumentation (WMI) をサポートするコンポーネントは含まれますが、Microsoft ActiveX® Data オブジェクト (ADO) をサポートするコンポーネントは含まれません。  

####  <a name="MissingorIncorrectDrivers"></a> 展開プロセスが開始しない — 見つからないか正しくないドライバー  
 **問題:** 特定のターゲット コンピューターに展開するときに、Windows PE が起動し、**wpeinit** を実行して、コマンド プロンプト ウィンドウを開きますが、実際には展開プロセスを開始しません。 ターゲット コンピューターからネットワーク ドライブをマッピングすることによってトラブルシューティングを行うと、ネットワーク アダプター ドライバーが読み込まれていないことを示します。 *X*:\Windows\System32\Inf にある SetupAPI.log ファイルを調べると、Windows PE がネットワーク アダプターを構成しているときにエラーを生成していることがわかり、そのうちの 1 つが "This driver is not meant for this platform" (このドライバーはこのプラットフォームのものではありません) です。 **[Out-of-Box Drivers]\(Out-of-Box ドライバー\)** の一覧のドライバーが、イメージに取り込まれています。  

 **解決方法:** Windows PE に別のドライバーとのドライバーの競合がある可能性があります。 Deployment Workbench で Windows PE イメージの設定を構成するときに、ネットワーク アダプターとストレージ ドライバーのみを含む Windows PE のドライバー グループを作成し、Windows PE のドライバー グループのみを使うように展開共有を構成します。  

## <a name="deployment-process-flow-charts"></a>展開プロセスのフロー チャート  
 このセクションでは、2 セットの MDT フロー チャートを提供します。1 つは LTI 展開のもので、もう 1 つは Configuration Manager での ZTI 展開のものです。 各フロー チャートでは、その展開の種類の間に実行されるタスクを示します。  

 次のようにして、展開プロセスのフロー チャートをよく理解してください。  

-   「[LTI 展開プロセスのフローチャート](#LTIDeploymentProcessFlowcharts)」で説明されている LTI 展開プロセスのフローチャートを確認します  

-   「[ZTI 展開プロセスのフローチャート](#ZTIDevelopmentProcessFlowcharts)」で説明されている ZTI 展開プロセスのフローチャートを確認します  

###  <a name="LTIDeploymentProcessFlowcharts"></a> LTI 展開プロセスのフローチャート  
 次のフェーズのフロー チャートが提供されています。  

-   検証 (図 4)  

-   状態キャプチャ (図 5、図 6)  

-   インストール前 (図 7、図 8、図 9)  

-   インストール (図 10)  

-   インストール後 (図 11、図 12)  

-   状態復元 (図 13、図 14、図 15、図 16)  

 ![TroubleshootingReference4](media/TroubleshootingReference4.jpg "TroubleshootingReference4")  
図 4: 検証フェーズのフローチャート  

 **図 4.検証フェーズのフローチャート**  

 ![TroubleshootingReference5](media/TroubleshootingReference5.jpg "TroubleshootingReference5")  
図 5. 状態キャプチャ フェーズのフローチャート (1/2)  

 **図 5.状態キャプチャ フェーズのフローチャート (1/2)**  

 ![TroubleshootingReference6](media/TroubleshootingReference6.jpg "TroubleshootingReference6")  
図 6. 状態キャプチャ フェーズのフローチャート (2/2)  

 **図 6.状態キャプチャ フェーズのフローチャート (2/2)**  

 ![TroubleshootingReference7](media/TroubleshootingReference7.jpg "TroubleshootingReference7")  
図 7. インストール前フェーズのフローチャート (1/3)  

 **図 7.インストール前フェーズのフローチャート (1/3)**  

 ![TroubleshootingReference8](media/TroubleshootingReference8.jpg "TroubleshootingReference8")  
図 8. インストール前フェーズのフローチャート (2/3)  

 **図 8.インストール前フェーズのフローチャート (2/3)**  

 ![TroubleshootingReference9](media/TroubleshootingReference9.jpg "TroubleshootingReference9")  
図 9. インストール前フェーズのフローチャート (3/3)  

 **図 9.インストール前フェーズのフローチャート (3/3)**  

 ![TroubleshootingReference10](media/TroubleshootingReference10.jpg "TroubleshootingReference10")  
図 10. インストール フェーズのフローチャート  

 **図 10.インストール フェーズのフローチャート**  

 ![TroubleshootingReference11](media/TroubleshootingReference11.jpg "TroubleshootingReference11")  
図 11. インストール後フェーズのフローチャート (1/2)  

 **図 11.インストール後フェーズのフローチャート (1/2)**  

 ![TroubleshootingReference12](media/TroubleshootingReference12.jpg "TroubleshootingReference12")  
図 12. インストール後フェーズのフローチャート (2/2)  

 **図 12. インストール後フェーズのフローチャート (2/2)**  

 ![TroubleshootingReference13](media/TroubleshootingReference13.jpg "TroubleshootingReference13")  
図 13. 状態復元フェーズのフローチャート (1/4)  

 **図 13.状態復元フェーズのフローチャート (1/4)**  

 ![TroubleshootingReference14](media/TroubleshootingReference14.jpg "TroubleshootingReference14")  
図 14. 状態復元フェーズのフローチャート (2/4)  

 **図 14.状態復元フェーズのフローチャート (2/4)**  

 ![TroubleshootingReference15](media/TroubleshootingReference15.jpg "TroubleshootingReference15")  
図 15. 状態復元フェーズのフローチャート (3/4)  

 **図 15.状態復元フェーズのフローチャート (3/4)**  

 ![TroubleshootingReference16](media/TroubleshootingReference16.jpg "TroubleshootingReference16")  
図 16. 状態復元フェーズのフローチャート (4/4)  

 **図 16.状態復元フェーズのフローチャート (4/4)**  

###  <a name="ZTIDevelopmentProcessFlowcharts"></a> ZTI 展開プロセスのフローチャート  
 Configuration Manager を使用した ZTI 展開の以下のフェーズについてのフローチャートが提供されています。  

-   初期化 (図 17)  

-   検証 (図 18)  

-   状態キャプチャ (図 19)  

-   インストール前 (図 20)  

-   インストール (図 21)  

-   インストール後 (図 22)  

-   状態復元 (図 23、図 24)  

-   キャプチャ (図 25)  

 ![TroubleshootingReference17](media/TroubleshootingReference17.jpg "TroubleshootingReference17")  
図 17. 初期化フェーズのフローチャート  

 **図 17.初期化フェーズのフローチャート**  

 ![TroubleshootingReference18](media/TroubleshootingReference18.jpg "TroubleshootingReference18")  
図 18. 検証フェーズのフローチャート  

 **図 18.検証フェーズのフローチャート**  

 ![TroubleshootingReference19](media/TroubleshootingReference19.jpg "TroubleshootingReference19")  
図 19. 状態キャプチャ フェーズのフローチャート  

 **図 19.状態キャプチャ フェーズのフローチャート**  

 ![TroubleshootingReference20](media/TroubleshootingReference20.jpg "TroubleshootingReference20")  
図 20. インストール前フェーズのフローチャート  

 **図 20.インストール前フェーズのフローチャート**  

 ![TroubleshootingReference21](media/TroubleshootingReference21.jpg "TroubleshootingReference21")  
図 21. インストール フェーズのフローチャート  

 **図 21.インストール フェーズのフローチャート**  

 ![TroubleshootingReference22](media/TroubleshootingReference22.jpg "TroubleshootingReference22")  
図 22. インストール後フェーズのフローチャート  

 **図 22.インストール後フェーズのフローチャート**  

 ![TroubleshootingReference23](media/TroubleshootingReference23.jpg "TroubleshootingReference23")  
図 23. 状態復元フェーズのフローチャート (1/2)  

 **図 23.状態復元フェーズのフローチャート (1/2)**  

 ![TroubleshootingReference24](media/TroubleshootingReference24.jpg "TroubleshootingReference24")  
図 24. 状態復元フェーズのフローチャート (2/2)  

 **図 24.状態復元フェーズのフローチャート (2/2)**  

 ![TroubleshootingReference25](media/TroubleshootingReference25.jpg "TroubleshootingReference25")  
図 25. キャプチャ フェーズのフローチャート  

 **図 25.キャプチャ フェーズのフローチャート**  

## <a name="finding-additional-help"></a>その他のヘルプの検索  
 MDT の展開の問題の解決に関するその他のヘルプ情報は、次のようにして探します。  

-   Microsoft のサポートに問い合わせる (「[Microsoft サポート](#MicrosoftSupport)」を参照)  

-   ブログや他のインターネット リソースを利用する (「[インターネットのサポート](#InternetSupport)」を参照)  

###  <a name="MicrosoftSupport"></a> Microsoft サポート  
 Microsoft では、Microsoft Deployment Toolkit に対して Premier レベルと Professional レベルのサポートが提供されています。  

 Professional レベルのサポート: [http://support.microsoft.com/](http://support.microsoft.com/)  

 Premier レベルのサポート: [https://premier.microsoft.com/](https://premier.microsoft.com/)  

> [!NOTE]
>  サポートに問い合わせるときは、MDT の特定のバージョンに関する問題であることを明確に伝えてください。  

###  <a name="InternetSupport"></a> インターネットのサポート  
 MDT のトラブルシューティングに関しては、このリファレンスでは説明されていない多くの情報が、オンライン ソースで提供されています。 次のようなオンライン ソースがあります。  

-   Microsoft がホストするブログ  

    -   [MDT チームのブログ](http://blogs.technet.com/b/msdeployment/)  

    -   [Configuration Manager チームのブログ](http://blogs.technet.com/b/configmgrteam/)  

    -   [Michael Niehaus のブログ](http://blogs.technet.com/b/mniehaus/) (Michael Niehaus は Windows および Microsoft Office の展開について書いています)  

-   Microsoft がホストするニュースグループとフォーラム:  

     以下のニュースグループとフォーラムでは、Microsoft 従業員、同業者、Microsoft Valued Professionals からのサポートが得られます。  

    -   [Configuration Manager - オペレーティング システムの展開](http://social.technet.microsoft.com/Forums/home?forum=configmanagerosd)  

    -   [Windows 8 のインストール、セットアップ、展開](http://social.technet.microsoft.com/Forums/windows/home?forum=w8itproinstall)  

-   Microsoft 以外による展開関連の情報ソース:  

    -   [DeployVista.com](http://www.deployvista.com/)  

    -   [myITforum.com](http://www.myitforum.com/)
