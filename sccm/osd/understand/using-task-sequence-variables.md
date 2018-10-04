---
title: タスク シーケンス変数の使用方法
titleSuffix: Configuration Manager
description: Configuration Manager のタスク シーケンスで変数を使用する方法について説明します。
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18305b26937c87cbdb4d5726bded571699416793
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2018
ms.locfileid: "42756272"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Configuration Manager でタスク シーケンス変数を使用する方法

*適用対象: System Center Configuration Manager (Current Branch)*

 Configuration Manager の OS 展開機能のタスク シーケンス エンジンでは、その動作を制御するために多くの変数が使用されます。 次の目的にこれらの変数を使用します。 
 - ステップでの条件を設定する  
 - 特定のステップの動作を変更する  
 - より複雑なアクションのためにスクリプトで使用する  


 使用可能なすべてのタスク シーケンス変数の参照については、「[タスク シーケンス変数](/sccm/osd/understand/task-sequence-variables)」をご覧ください。



## <a name="bkmk_types"></a> 変数の種類

 変数には複数の種類があります。  
 - [組み込み](#bkmk_built-in)  
 - [操作](#bkmk_action)  
 - [カスタム](#bkmk_custom)  
 - [読み取り専用](#bkmk_read-only)  
 - [配列](#bkmk_array)  


### <a name="bkmk_built-in"></a> 組み込み変数

 組み込み変数では、タスク シーケンスの実行環境に関する情報が提供されます。 これらの値は、タスク シーケンス全体で使用できます。 通常、組み込み変数はタスク シーケンス エンジンによってステップの実行前に初期化されます。 

 たとえば、**\_SMSTSLogPath** は、Configuration Manager コンポーネントがログ ファイルを書き込むパスを指定する環境変数です。 この環境変数には、すべてのタスク シーケンス ステップからアクセスできます。 

 タスク シーケンスでは、各ステップの前にいくつかの変数が評価されます。 たとえば、**\_SMSTSCurrentActionName** では現在のステップの名前がリストされています。 

### <a name="bkmk_action"></a> アクション変数

 タスク シーケンス アクション変数では、単一のタスク シーケンス ステップで使用される構成設定が指定されています。 既定では、ステップはその設定を初期化してから実行します。 これらの設定は、関連付けられているタスク シーケンス ステップの実行中にのみ使用できます。 タスク シーケンスでは、ステップを実行する前に、環境にアクション変数の値が追加されます。 ステップの実行後には、環境から値が削除されます。

 たとえば、**コマンド ラインの実行**ステップをタスク シーケンスに追加します。 このステップには、**作業フォルダー** プロパティが含まれます。 タスク シーケンスでは、このプロパティの既定値が **WorkingDirectory** 変数として格納されています。 タスク シーケンスは、**コマンド ラインの実行**ステップを実行する前に、この値を初期化します。 このステップの実行中は、**WorkingDirectory** の値から**作業フォルダー** プロパティの値にアクセスします。 ステップの完了後、タスク シーケンスでは環境から **WorkingDirectory** 変数の値が削除されます。 タスク シーケンスに別の**コマンド ラインの実行**ステップが含まれている場合は、新しい **WorkingDirectory** 変数が初期化されます。 その時点で、タスク シーケンスは現在のステップの開始値に変数を設定します。 詳しくは、「[WorkingDirectory](using-task-sequence-variables.md#WorkingDirectory)」をご覧ください。  

 ステップが実行すると、アクション変数の "*既定の*" 値が示されます。 "*新しい*" 値を設定した場合、タスク シーケンスの複数のステップで使用できます。 既定値をオーバーライドした場合、新しい値は環境内で維持されます。 この新しい値は、タスク シーケンス内の他のステップの既定値をオーバーライドします。 たとえば、タスク シーケンスの最初のステップとして、**タスク シーケンス変数の設定**ステップを追加します。 このステップで、**WorkingDirectory** 変数を `C:\` に設定します。 タスク シーケンス内のすべての**コマンド ラインの実行**ステップでは、新しい開始ディレクトリ値が使用されます。  

 一部のタスク シーケンス ステップでは、特定のアクション変数が "*出力*" としてマークされています。 タスク シーケンスの後続のステップでは、これらの出力変数が読み取られます。

 > [!Note]  
 > アクション変数を持たないタスク シーケンス ステップもあります。 たとえば、**BitLocker の有効化**アクションには関連付けれた変数がありますが、**BitLocker の無効化**アクションには関連付けられた変数はありません。  


### <a name="bkmk_custom"></a> カスタム変数

 カスタム変数は、Configuration Manager で作成されない変数です。 条件として使用するにはコマンド ラインまたはスクリプトで独自の変数を初期化します。 

 新しいタスク シーケンス変数の名前を指定する際、次のガイドラインに従います。  

 - タスク シーケンス変数名には、文字、数字、下線 (`_`)、およびハイフン (`-`) を含めることができます。  

 - タスク シーケンス変数名の最低の長さは 1 文字、最大の長さは 256 文字です。  

 - ユーザー定義変数は、文字 (`A-Z` または `a-z`) で始まる必要があります。  

 - ユーザー定義変数名を下線で始めることはできません。 読み取り専用タスク シーケンス変数のみを下線で始めることができます。  

 - タスク シーケンス変数名では大文字と小文字が区別されません。 たとえば、`OSDVAR` と `osdvar` は同じタスク シーケンス変数です。  

 - タスク シーケンス変数名をスペースで始めたり終わらせたりすることはできません。 また、変数名にスペースを埋め込むこともできません。 変数名の先頭または末尾のスペースは、タスク シーケンスでは無視されます。  


 作成できるタスク シーケンス変数の数に制限はありません。 ただし、タスク シーケンス環境のサイズによって制限されます。 タスク シーケンス環境の合計サイズの制限は、32 MB です。  


### <a name="bkmk_read-only"></a> 読み取り専用変数

 一部の変数の値は変更できず、読み取り専用です。 通常、そのような変数の名前は下線 (\_) で始まっています。 タスク シーケンスでは、操作に読み取り専用変数が使用されます。 読み取り専用変数は、タスク シーケンス環境内で可視です。 

 これらの変数はスクリプトまたはコマンド ラインで役に立ちます。 たとえば、コマンド ラインを実行し、**\_SMSTSLogPath** のログ ファイルに出力をパイプします。

 > [!NOTE]  
 >  読み取り専用タスク シーケンス変数は、タスク シーケンスのステップで読み取ることができますが、設定することはできません。 たとえば、**コマンド ラインの実行**ステップのコマンド ラインの一部として読み取り専用変数を使用します。 **タスク シーケンス変数の設定**ステップを使用して読み取り専用変数を設定することはできません。  



### <a name="bkmk_array"></a> 配列変数

 タスク シーケンスは、一部の変数を配列として格納します。 配列内の各要素は、1 つのオブジェクトに対する設定を表します。 デバイスに構成するオブジェクトが複数ある場合は、これらの変数を使用します。 次のタスク シーケンス ステップでは、配列変数が使用されます。

 - [ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

 - [ディスクのフォーマットとパーティション作成](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  



## <a name="bkmk_set"></a> 変数を設定する方法

 カスタム変数または読み取り専用ではない変数の場合は、変数の値を初期化および設定する方法がいくつかあります。  

 - [タスク シーケンス変数の設定](#bkmk_set-ts-step)  
 - [動的変数の設定](#bkmk_set-dyn-step)  
 - [コレクションとデバイスの変数](#bkmk_set-coll-var)  
 - [TSEnvironment COM オブジェクト](#bkmk_set-com)  
 - [起動前コマンド](#bkmk_set-prestart)  
 - [タスク シーケンス メディア ウィザード](#bkmk_set-media)  


 環境から変数を削除するには、変数の作成と同じ方法を使用します。 変数を削除するには、変数の値を空の文字列に設定します。  

 この方法を組み合わせて、同じシーケンスでタスク シーケンス変数をさまざまな値に設定できます。 たとえば、タスク シーケンス エディターを使用して既定値を設定し、スクリプトを使用してカスタム値を設定することができます。 

 異なる方法で同じ変数を設定する場合、タスク シーケンス エンジンでは次の順序が使用されます。  

 1. 最初にコレクション変数を評価します。  

 2. デバイス固有の変数は、コレクションで設定されている同じ変数をオーバーライドします。  

 3. タスク シーケンス中に何らかの方法によって設定された変数は、コレクションまたはデバイスの変数より優先されます。  


#### <a name="general-limitations-for-task-sequence-variable-values"></a>タスク シーケンス変数の値に関する一般的な制限事項  

 - タスク シーケンス変数の値は、4,000 文字を超えることはできません。  

 - 読み取り専用タスク シーケンス変数を変更することはできません。 読み取り専用変数の名前は、下線 (`_`) で始まっています。  

 - タスク シーケンス変数の値は、値の使用方法によっては、大文字と小文字が区別されることがあります。 ほとんどの場合、タスク シーケンス変数の値では、大文字と小文字が区別されません。 パスワードを含む変数は、大文字と小文字が区別されます。  


### <a name="bkmk_set-ts-step"></a> タスク シーケンス変数の設定

 1 つの変数を 1 つの値に設定するには、タスク シーケンスでこのステップを使用します。 

 詳しくは、「[タスク シーケンス変数の設定](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)」をご覧ください。 


### <a name="bkmk_set-dyn-step"></a> 動的変数の設定

 1 つまたは複数のタスク シーケンス変数を設定するには、タスク シーケンスでこのステップを使用します。 このステップでは使用する変数と値を決定する規則を定義します。 

 詳細については、「[動的変数の設定](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables)」を参照してください。


### <a name="bkmk_set-coll-var"></a> コレクション変数とデバイス変数

 コレクションまたは特定のデバイスのプロパティに変数を設定します。 

 詳しくは、「[コンピューターおよびコレクションのタスク シーケンスの変数の作成](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTSVariables)」をご覧ください。


### <a name="bkmk_set-com"></a> TSEnvironment COM オブジェクト

 スクリプトから変数を使用するには、**TSEnvironment** オブジェクトを使用します。 

 詳しくは、Configuration Manager SDK の「[How to use variables in a running task sequence](/sccm/develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence)」(実行中のタスク シーケンスで変数を使用する方法) をご覧ください。


### <a name="bkmk_set-prestart"></a> 起動前コマンド

 起動前コマンドは、ユーザーがタスク シーケンスを選択する前に Windows PE で実行されるスクリプトまたは実行可能ファイルです。 起動前コマンドでは、変数のクエリを行ったり、ユーザーに情報の指定を求めたりした後、それを環境に保存することができます。 起動前コマンドで変数を読み書きするには、[TSEnvironment](#bkmk_set-com) COM オブジェクトを使用します。 

 詳細については、「[タスク シーケンス メディアの起動前コマンド](/sccm/osd/understand/prestart-commands-for-task-sequence-media)」を参照してください。


### <a name="bkmk_set-media"></a> タスク シーケンス メディア ウィザード

 メディアから実行されるタスク シーケンスの変数を指定します。 メディアを使用して OS を展開する場合、メディアを作成するときに、タスク シーケンス変数を追加して値を指定します。 変数とその値はメディアに格納されます。  

 > [!NOTE]  
 >  タスク シーケンスは、スタンドアロン メディアに保存されます。 ただし、事前設定メディアなどのその他のすべての種類のメディアは、管理ポイントからタスク シーケンスを取得します。  

 メディアからタスク シーケンスを実行するときに、ウィザードの **[カスタマイズ]** ページで変数を追加することができます。 

 コレクションごとの変数またはコンピューターごとの変数の代わりに、メディア変数を使用してください。 タスク シーケンスをメディアから実行している場合、コンピューターごとの変数およびコレクションごとの変数は適用されず、使用されません。  

 > [!TIP]  
 >  タスク シーケンスは、パッケージ ID と起動前コマンド ラインを、Configuration Manager コンソールを実行しているコンピューターの **CreateTSMedia.log** ファイルに書き込みます。 このログ ファイルには、任意のタスク シーケンス変数の値が含まれています。 このログ ファイルで、タスク シーケンス変数の値を確認します。  

 詳しくは、「[タスク シーケンス メディアの作成](/sccm/osd/deploy-use/create-task-sequence-media)」をご覧ください。



## <a name="bkmk_access"></a> 変数にアクセスする方法

 前のセクションの方法のいずれかを使用して変数とその値を指定した後、タスク シーケンス内でそれを使用できます。 たとえば、組み込みタスク シーケンス変数の既定値にアクセスしたり、ステップを変数の値の条件に基づくようにしたりします。  

 タスク シーケンス環境の変数値にアクセスするには、次の方法を使用します。
 - [ステップでの使用](#bkmk_access-step)  
 - [ステップの条件](#bkmk_access-condition)  
 - [カスタム スクリプト](#bkmk_access-script)  
 - [Windows セットアップ応答ファイル](#bkmk_access-answer)  
  

### <a name="bkmk_access-step"></a> ステップでの使用

 タスク シーケンスのステップで設定に対して変数の値を指定します。 タスク シーケンス エディターで、ステップを編集し、フィールドの値として変数名を指定します。 変数名は、パーセント記号 (`%`) で囲みます。 

 たとえば、**コマンド ラインの実行**ステップの **[コマンド ライン]** フィールドの一部として変数名を使用します。 次のコマンド ラインは、コンピューター名をテキスト ファイルに書き込みます。 

 `cmd.exe /c %_SMSTSMachineName% > C:\File.txt`


### <a name="bkmk_access-condition"></a> ステップの条件

 ステップまたはグループの条件の一部として、組み込みまたはカスタムのタスク シーケンス変数を使用します。 タスク シーケンスは、ステップまたはグループを実行する前に、変数の値を評価します。

 変数値を評価する条件を追加するには、次の手順のようにします。  

 1. タスク シーケンス エディターで、条件を追加するステップまたはグループを選択します。  

 2. ステップまたはグループの **[オプション]** タブに切り替えます。 **[条件の追加]** をクリックし、**[タスク シーケンス変数]** を選択します。  

 3. **[タスク シーケンス変数]** ダイアログ ボックスで、次の設定を指定します。  

    - **[変数]**: 変数の名前です。 たとえば、`_SMSTSInWinPE` となります。  

    - **[条件]**: 変数の値を評価する条件です。 たとえば、**[が次の値と等しい]** などです。  

    - **[値]**: チェックする変数の値です。 たとえば、`false` となります。  


 上の 3 つの例では、タスク シーケンスが Windows PE のブート イメージから実行されているかどうかをテストする一般的な条件を設定しています。 

 > **タスク シーケンス変数** `_SMSTSInWinPE equals "false"`

 既存の OS イメージをインストールする既定のタスク シーケンス テンプレートの **[ファイルと設定のキャプチャ]** グループで、この条件を確認してください。


### <a name="bkmk_access-script"></a> カスタム スクリプト

 タスク シーケンスの実行中に、**Microsoft.SMS.TSEnvironment** COM オブジェクトを使用して、変数を読み書きします。

 次の Windows PowerShell の例では、**_SMSTSLogPath** 変数のクエリを行って、現在のログの場所を取得しています。 このスクリプトではカスタム変数も設定されます。

 ```PowerShell
 # Create an object to access the task sequence environment
 $tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment
 
 # Query the environment to get an existing variable
 # Set a variable for the task sequence log path
 $LogPath = $tsenv.Value("_SMSTSLogPath")

 # Or, convert all of the variables currently in the environment to PowerShell variables
 $tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

 # Write a message to a log file
 Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append
 
 # Set a custom variable "startTime" to the current time
 $tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
 ```


###  <a name="bkmk_access-answer"></a> Windows セットアップ応答ファイル

ユーザーが提供する Windows セットアップ応答ファイルには、タスク シーケンス変数を埋め込むことができます。 `%varname%` の形式を使用します。ここで、*varname* は変数の名前です。 **Windows と ConfigMgr のセットアップ** ステップでは、変数名の文字列が実際の変数値に置き換えられます。 これらの埋め込みタスク シーケンス変数は、unattend.xml 応答ファイルの数値のみのフィールドでは使うことができません。

詳細については、「[Setup Windows and ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr)」(Windows と ConfigMgr のセットアップ) を参照してください。



## <a name="see-also"></a>関連項目

- [タスク シーケンスのステップ](/sccm/osd/understand/task-sequence-steps)
- [タスク シーケンス変数](/sccm/osd/understand/task-sequence-variables)
- [タスクの自動化計画に関する考慮事項](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
