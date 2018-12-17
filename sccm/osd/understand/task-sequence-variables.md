---
title: タスク シーケンス変数リファレンス
titleSuffix: Configuration Manager
description: Configuration Manager のタスク シーケンスを制御およびカスタマイズするための変数について説明します。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cde62242fc4db99d762d670037aad22bd25d6c00
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456738"
---
# <a name="task-sequence-variables-in-configuration-manager"></a>Configuration Manager でのタスク シーケンス変数

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、使用できるすべての変数をアルファベット順で示します。 特定の変数を探すには、ブラウザーの**検索**機能 (通常は **Ctrl** + **F**) を使用してください。 変数では、特定のステップに固有かどうかが示されています。 [タスク シーケンスのステップ](/sccm/osd/understand/task-sequence-steps)に関する記事には、各ステップに固有の変数の一覧が含まれます。 

詳しくは、[タスク シーケンス変数の使用](/sccm/osd/understand/using-task-sequence-variables)に関するページをご覧ください。



## <a name="bkmk_tsvar"></a> タスク シーケンス変数リファレンス


### <a name="OSDDetectedWinDir"></a> _OSDDetectedWinDir

 Windows PE の起動時に、タスク シーケンスでコンピューターのハード ドライブの以前のオペレーティング システムのインストールがスキャンされます。 Windows フォルダーの場所は、この変数に格納されます。 タスク シーケンスを構成して、環境からこの値を取得して使用し、新しいオペレーティング システムのインストールに使用する同じ Windows フォルダーの場所を指定できます。


### <a name="OSDDetectedWinDrive"></a> _OSDDetectedWinDrive

 Windows PE の起動時に、タスク シーケンスでコンピューターのハード ドライブの以前のオペレーティング システムのインストールがスキャンされます。 オペレーティング システムがインストールされるハード ドライブの場所は、この変数に格納されます。 タスク シーケンスを構成して、環境からこの値を取得して使用し、新しいオペレーティング システムに使用する同じハード ドライブの場所を指定できます。


### <a name="OSDMigrateUsmtPackageID"></a> _OSDMigrateUsmtPackageID

 *[ユーザー状態のキャプチャ](task-sequence-steps.md#BKMK_CaptureUserState) ステップに適用されます。*

 (入力)

 USMT ファイルを含む Configuration Manager パッケージのパッケージ ID を指定します。 この変数は必須です。


### <a name="OSDMigrateUsmtRestorePackageID"></a> _OSDMigrateUsmtRestorePackageID

 *[ユーザー状態の復元](task-sequence-steps.md#BKMK_RestoreUserState)ステップに適用されます。*

 (入力)

 USMT ファイルを含む Configuration Manager パッケージのパッケージ ID を指定します。 この変数は必須です。


### <a name="SMSTSAdvertID"></a> _SMSTSAdvertID

 現在実行中のタスク シーケンスの一意の ID を格納します。 Configuration Manager のソフトウェア配布展開 ID と同じフォーマットを使用します。 タスク シーケンスがスタンドアロン メディアから実行されている場合は、この変数は未定義になります。

 #### <a name="example"></a>例
 `ABC20001`


### <a name="SMSTSAssetTag"></a> _SMSTSAssetTag

 *[動的変数の設定](task-sequence-steps.md#BKMK_SetDynamicVariables)ステップに適用されます。*

 コンピューターの資産タグを指定します。


### <a name="SMSTSBootImageID"></a> _SMSTSBootImageID

 現在実行中のタスク シーケンスでブート イメージ パッケージを参照する場合は、この変数でブート イメージ パッケージ ID が格納されます。 タスク シーケンスでブート イメージ パッケージを参照しない場合、この変数は設定されません。

 #### <a name="example"></a>例
 `ABC00001`  


### <a name="SMSTSBootUEFI"></a> _SMSTSBootUEFI

 タスク シーケンスは、UEFI モードのコンピューターを検出すると、この変数を設定します。


### <a name="SMSTSClientGUID"></a> _SMSTSClientGUID

 Configuration Manager クライアント GUID の値を格納します。 タスク シーケンスがスタンドアロン メディアから実行されている場合、この変数は設定されません。

 #### <a name="example"></a>例
 `0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`


### <a name="SMSTSCurrentActionName"></a> _SMSTSCurrentActionName

 現在実行中のタスク シーケンス ステップの名前です。 この変数は、タスク シーケンス マネージャーが個々のステップを実行する前に設定されます。

 #### <a name="example"></a>例
 `run command line`


### <a name="SMSTSDefaultGateways"></a> _SMSTSDefaultGateways

 *[動的変数の設定](task-sequence-steps.md#BKMK_SetDynamicVariables)ステップに適用されます。*

 コンピューターで使用される既定のゲートウェイを指定します。


### <a name="SMSTSDownloadOnDemand"></a> _SMSTSDownloadOnDemand

 現在のタスク シーケンスがオン デマンド ダウンロード モードで実行されている場合、この変数は `true` です。 オン デマンド ダウンロード モードでは、コンテンツへのアクセスが必要になった場合にのみ、タスク シーケンス マネージャーがコンテンツをローカルにダウンロードします。


### <a name="SMSTSInWinPE"></a> _SMSTSInWinPE

 現在のタスク シーケンス ステップが Windows PE で実行されている場合、この変数は `true` です。 このタスク シーケンス変数をテストして、現在の OS 環境を特定します。


### <a name="SMSTSIPAddresses"></a> _SMSTSIPAddresses

 *[動的変数の設定](task-sequence-steps.md#BKMK_SetDynamicVariables)ステップに適用されます。*

 コンピューターで使用される IP アドレスを指定します。


### <a name="SMSTSLastActionName"></a> _SMSTSLastActionName
 *バージョン 1810 以降*  

 最後に実行された操作の名前を格納します。 この変数は **_SMSTSLastActionRetCode** に関連します。 タスク シーケンスで、これらの値が smsts.log ファイルに記録されます。 この変数は、タスク シーケンスのトラブルシューティングを行うときに役立ちます。 ステップが失敗した場合、カスタム スクリプトにリターン コードと共にステップ名を含めることができます。


### <a name="SMSTSLastActionRetCode"></a> _SMSTSLastActionRetCode

 最後に実行されたアクションからのリターン コードを格納します。 この変数は、次の手順が実行されるかどうかを決定するための条件として使用できます。

 #### <a name="example"></a>例
 `0`


### <a name="SMSTSLastActionSucceeded"></a> _SMSTSLastActionSucceeded

 - 最後のステップが成功した場合、この変数は `true` です。  

 - 最後のステップが失敗した場合は `false` です。  

 - ステップが無効になっているか、関連する条件が **false** に評価されたためにタスク シーケンスで最後のアクションがスキップされた場合、この変数はリセットされません。 引き続き、前のアクションの値が保持されます。  

 
### <a name="SMSTSLaunchMode"></a> _SMSTSLaunchMode

 次のいずれかの方法でタスク シーケンスが開始したことを指定します。  

 - **SMS**: Configuration Manager クライアント (ユーザーがソフトウェア センターから開始した場合など)
 - **UFD**: レガシ USB メディア
 - **UFD+FORMAT**: 新しい USB メディア
 - **CD**: 起動可能な CD
 - **DVD**: 起動可能な DVD
 - **PXE**: PXE によるネットワーク ブート
 - **HD**: ハード ディスク上の事前設定されたメディア


### <a name="SMSTSLogPath"></a> _SMSTSLogPath

 ログ ディレクトリへの完全なパスを格納します。 タスク シーケンスのステップがそのアクションをログに記録しているかどうかを確認するには、この値を使用します。 ハード ドライブが利用できない場合、この値は設定されません。


### <a name="SMSTSMacAddresses"></a> _SMSTSMacAddresses

 *[動的変数の設定](task-sequence-steps.md#BKMK_SetDynamicVariables)ステップに適用されます。*

 コンピューターで使用される MAC アドレスを指定します。


### <a name="SMSTSMachineName"></a> _SMSTSMachineName

 コンピューター名を格納します。 タスク シーケンスですべてのステータス メッセージを記録するために使用するコンピューターの名前を格納します。 新しい OS で使用するコンピューター名を変更するには、[OSDComputerName](#OSDComputerName) 変数を使用します。


### <a name="SMSTSMake"></a> _SMSTSMake

 *[動的変数の設定](task-sequence-steps.md#BKMK_SetDynamicVariables)ステップに適用されます。*

 コンピューターのメーカーを指定します。


### <a name="SMSTSMDataPath"></a> _SMSTSMDataPath

 [SMSTSLocalDataDrive](#SMSTSLocalDataDrive) 変数で定義されているパスを指定します。 コレクション変数の設定などのように、タスク シーケンスが起動する前に SMSTSLocalDataDrive を定義すると、Configuration Manager はそのタスク シーケンスが起動された後で _SMSTSMDataPath 値を定義します。


### <a name="SMSTSMediaType"></a> _SMSTSMediaType

 インストールを開始するために使用するメディアの種類を指定します。 メディアの種類の例としては、ブート メディア、フル メディア、PXE、事前設定されたメディアなどがあります。


### <a name="SMSTSModel"></a> _SMSTSModel

 *[動的変数の設定](task-sequence-steps.md#BKMK_SetDynamicVariables)ステップに適用されます。*

 コンピューターのモデルを指定します。


### <a name="SMSTSMP"></a> _SMSTSMP

 Configuration Manager の管理ポイントの URL または IP アドレスを格納します。


### <a name="SMSTSMPPort"></a> _SMSTSMPPort

 Configuration Manager の管理ポイントのポート番号を格納します。


### <a name="SMSTSOrgName"></a> _SMSTSOrgName

 タスク シーケンスの進行状況ダイアログに表示されるブランド タイトル名を格納します。


### <a name="SMSTSOSUpgradeActionReturnCode"></a> _SMSTSOSUpgradeActionReturnCode

 *[オペレーティング システムのアップグレード](task-sequence-steps.md#BKMK_UpgradeOS) ステップに適用されます。*

 Windows セットアップで返される終了コード値 (成功または失敗を示す値) を格納します。 この変数は、`/Compat` コマンド ライン オプションで使用すると便利です。

 #### <a name="example"></a>例
 コンパクトのみのスキャンが完了すると、終了コードが失敗か成功かに応じて、以降のステップのアクションが実行されます。 成功の場合は、アップグレードを開始します。 または、ハードウェア インベントリで収集するためのマーカーを環境に設定します。 たとえば、ファイルを追加したり、レジストリ キーを設定したりします。 このマーカーを使用して、アップグレードの準備ができているコンピューターや、アップグレード前にアクションが必要なコンピューターのコレクションを作成します。


### <a name="SMSTSPackageID"></a> _SMSTSPackageID

 現在実行中のタスク シーケンス ID を格納します。 この ID では Configuration Manager のパッケージ ID と同じ形式が使用されます。 

 #### <a name="example"></a>例
 `HJT00001`


### <a name="SMSTSPackageName"></a> _SMSTSPackageName

 現在実行中のタスク シーケンスの名前を格納します。 Configuration Manager の管理者が、タスク シーケンスを作成するときに、この名前を指定します。

 #### <a name="example"></a>例
 `Deploy Windows 10 task sequence`


### <a name="SMSTSRunFromDP"></a> _SMSTSRunFromDP

 現在のタスク シーケンスが配布ポイントからの実行モードで実行されている場合、`true` に設定されます。 このモードでは、タスク シーケンス マネージャーは、配布ポイントから必要なパッケージ共有を取得します。


### <a name="SMSTSSerialNumber"></a> _SMSTSSerialNumber

 *[動的変数の設定](task-sequence-steps.md#BKMK_SetDynamicVariables)ステップに適用されます。*

 コンピューターのシリアル番号を指定します。


### <a name="SMSTSSetupRollback"></a> _SMSTSSetupRollback

 Windows セットアップが、インプレース アップグレードの間にロールバック操作を実行したかどうかを指定します。 変数の値は `true` または `false` です。


### <a name="SMSTSSiteCode"></a> _SMSTSSiteCode

 Configuration Manager サイトのサイト コードを格納します。

 #### <a name="example"></a>例
 `ABC`


### <a name="SMSTSTimezone"></a> _SMSTSTimezone

 この変数は、次の形式でタイム ゾーン情報を格納します。 

 ```
 Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName
 ```

 #### <a name="example"></a>例
 タイム ゾーンが**東部標準時 (米国およびカナダ)** の場合: 

 ```
 300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time
 ```


### <a name="SMSTSType"></a> _SMSTSType

 現在実行中のタスク シーケンスの種類です。 次のいずれかの値になります。  

 - **1**: 一般タスク シーケンス
 - **2**: OS 展開のタスク シーケンス


### <a name="SMSTSUseCRL"></a> _SMSTSUseCRL

 タスク シーケンスで管理ポイントとの通信に HTTPS を使用する場合、この変数は証明書失効リスト (CRL) を使用するかどうかを指定します。


### <a name="SMSTSUserStarted"></a> _SMSTSUserStarted

 ユーザーがタスク シーケンスを開始したかどうかを指定します。 この変数は、タスク シーケンスがソフトウェア センターから開始された場合にのみ設定されます。 たとえば、[_SMSTSLaunchMode](#SMSTSLaunchMode) が `SMS` に設定されている場合などです。 

 この変数は次の値のいずれかを取ります。  

 - `true`: タスク シーケンスがユーザーによってソフトウェア センターから手動で開始されたことを示します。  

 - `false`: タスク シーケンスが Configuration Manager スケジューラによって自動的に開始されたことを示します。


### <a name="SMSTSUseSSL"></a> _SMSTSUseSSL

 タスク シーケンスが Configuration Manager 管理ポイントとの通信に SSL を使用するかどうかを表します。 HTTPS 用にサイト システムを構成する場合、値を `true` に設定します。


### <a name="SMSTSUUID"></a> _SMSTSUUID

 *[動的変数の設定](task-sequence-steps.md#BKMK_SetDynamicVariables)ステップに適用されます。*

 コンピューターの UUID を指定します。


### <a name="SMSTSWTG"></a> _SMSTSWTG

 コンピューターが Windows To Go デバイスとして動作しているかどうかを指定します。


### <a name="TSAppInstallStatus"></a> _TSAppInstallStatus

 タスク シーケンスで、[アプリケーションのインストール](task-sequence-steps.md#BKMK_InstallApplication) ステップでのアプリケーションのインストール状態がこの変数に設定されます。 次のいずれかの値に設定されます。  

 - **Undefined**: アプリケーションのインストール ステップは実行されていません。  

 - **エラー**: [アプリケーションのインストール] ステップで、エラーのために少なくとも 1 つのアプリケーションが失敗しました。  

 - **Warning**: アプリケーションのインストール ステップでエラーは発生していません。 要件が満たされなかったため、1 つ以上のアプリケーション、または必要な依存関係がインストールされませんでした。  

 - **成功**: [アプリケーションのインストール] ステップで、エラーや警告は検出されていません。  


### <a name="OSDAdapter"></a> OSDAdapter

 *[ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)ステップに適用されます。*

 (入力)

 このタスク シーケンス変数は、"*配列*" 変数です。 配列内の各要素は、コンピューター上の単一ネットワーク アダプターの設定を表します。 各アダプターの設定にアクセスするには、配列変数名にゼロから始まるネットワーク アダプター インデックスとプロパティ名を組み合わせます。

 ネットワーク設定の適用ステップで複数のネットワーク アダプターを構成する場合、変数名のインデックス **1** を使用して、"*2 番目*" のネットワーク アダプターのプロパティが定義されます。 たとえば、OSDAdapter1EnableDHCP、OSDAdapter1IPAddressList、OSDAdapter1DNSDomain のようになります。

 次の変数名を使用して、ステップで構成する "*1 番目*" のネットワーク アダプターのプロパティを定義します。

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP
 この設定は必須です。 指定できる値は `True` または `False` です。 次に例を示します。

 `true`: アダプターの動的ホスト構成プロトコル (DHCP) を有効にします。

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList
 アダプターの IP アドレスを示すコンマ区切りの一覧。 このプロパティは **EnableDHCP** が `false`に設定されている場合を除き、無視されます。 この設定は必須です。

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask
 サブネット マスクのコンマ区切りの一覧。 このプロパティは **EnableDHCP** が `false`に設定されている場合を除き、無視されます。 この設定は必須です。

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways
 IP ゲートウェイ アドレスのコンマ区切りの一覧。 このプロパティは **EnableDHCP** が `false`に設定されている場合を除き、無視されます。 この設定は必須です。

#### <a name="osdadapter0dnsdomain"></a>OSDAdapter0DNSDomain
 アダプターのドメイン ネーム システム (DNS) ドメイン。

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList
 アダプターの DNS サーバーを示すコンマ区切りの一覧。 この設定は必須です。

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration
 DNS でアダプターの IP アドレスを登録するには、`true` に設定します。

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration
 アダプターの IP アドレスを コンピューターのフル DNS 名で DNS に登録するには、`true` に設定します。

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering
 アダプターで IP プロトコルのフィルター処理を有効にするには、`true` に設定します。

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList
 IP での実行を許可されたプロトコルのコンマ区切りの一覧。 このプロパティは、**EnableIPProtocolFiltering** が `false`に設定されている場合、無視されます。

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering
 アダプターの TCP ポート フィルター処理を有効にするには、`true` に設定します。

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList
 TCP へのアクセス許可を付与するポートのコンマ区切りの一覧。 このプロパティは、**EnableTCPFiltering** が `false`に設定されている場合、無視されます。

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions
 NetBIOS over TCP/IP のオプションです。 使用できる値は次のとおりです。  

 - `0`: DHCP サーバーから NetBIOS 設定を使用します  
 - `1`: NetBIOS over TCP/IP を有効にします  
 - `2`: NetBIOS over TCP/IP を無効にします  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS
 名前解決に WINS を使用するには、`true` に設定します。

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList
 WINS サーバー IP アドレスのコンマ区切りの一覧。 このプロパティは、**EnableWINS** が `true`に設定されている場合を除き、無視されます。

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress
 設定を物理ネットワーク アダプターに合わせるために使用する MAC アドレス。

#### <a name="osdadapter0name"></a>OSDAdapter0Name
 ネットワーク接続のコントロール パネル プログラムに表示されるネットワーク接続の名前。 名前の長さは 0 ～ 255 文字の範囲です。

#### <a name="osdadapter0index"></a>OSDAdapter0Index
 設定の配列内にあるネットワーク アダプター設定のインデックス。

#### <a name="example"></a>例
 - **OSDAdapterCount** = `1`  
 - **OSDAdapter0EnableDHCP** = `FALSE`  
 - **OSDAdapter0IPAddressList** = `192.168.0.40`  
 - **OSDAdapter0SubnetMask** = `255.255.255.0`  
 - **OSDAdapter0Gateways** = `192.168.0.1`  
 - **OSDAdapter0DNSSuffix** = `contoso.com`  


### <a name="OSDAdapterCount"></a> OSDAdapterCount

 *[ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)ステップに適用されます。*

 (入力)

 対象のコンピューターにインストールされているネットワーク アダプターの数を指定します。 **OSDAdapterCount** の値を設定するときは、各アダプターのすべての構成オプションも設定します。 

 たとえば、1 番目のアダプターの **OSDAdapter0TCPIPNetbiosOptions** の値を設定する場合は、そのアダプターのすべての値を構成する必要があります。

 この値を指定しないと、タスク シーケンスは **OSDAdapter** のすべての値を無視します。


### <a name="OSDApplyDriverBootCriticalContentUniqueID"></a> OSDApplyDriverBootCriticalContentUniqueID

 *[ドライバー パッケージの適用](task-sequence-steps.md#BKMK_ApplyDriverPackage)ステップに適用されます。*

 (入力)

 ドライバー パッケージからインストールする大容量記憶装置デバイス ドライバーのコンテンツ ID を指定します。 この変数を指定しない場合、大容量記憶装置ドライバーはインストールされません。


### <a name="OSDApplyDriverBootCriticalHardwareComponent"></a> OSDApplyDriverBootCriticalHardwareComponent

 *[ドライバー パッケージの適用](task-sequence-steps.md#BKMK_ApplyDriverPackage)ステップに適用されます。*

 (入力)

 大容量記憶装置デバイス ドライバーをインストールするかどうかを指定します。この変数は **scsi** にする必要があります。

 [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) が設定されている場合、この変数は必須です。


### <a name="OSDApplyDriverBootCriticalID"></a> OSDApplyDriverBootCriticalID

 *[ドライバー パッケージの適用](task-sequence-steps.md#BKMK_ApplyDriverPackage)ステップに適用されます。*

 (入力)

 インストールする大容量記憶装置デバイス ドライバーの起動に必要な ID を指定します。 この ID は、デバイス ドライバーの txtsetup.oem ファイルの **scsi** セクションに一覧表示されます。

 [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) が設定されている場合、この変数は必須です。

### <a name="OSDApplyDriverBootCriticalINFFile"></a> OSDApplyDriverBootCriticalINFFile

 *[ドライバー パッケージの適用](task-sequence-steps.md#BKMK_ApplyDriverPackage)ステップに適用されます。*

 (入力)

 インストールする大容量記憶装置ドライバーの INF ファイルを指定します。

 [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) が設定されている場合、この変数は必須です。


### <a name="OSDAutoApplyDriverBestMatch"></a> OSDAutoApplyDriverBestMatch

 *[ドライバーの自動適用](task-sequence-steps.md#BKMK_AutoApplyDrivers)ステップに適用されます。*

 (入力)

 ハードウェア デバイスと互換性のある複数のデバイス ドライバーがドライバー カタログにある場合は、この変数でステップのアクションが決定します。 

 #### <a name="valid-values"></a>有効な値
 - `true` (既定): 最適なデバイス ドライバーのみをインストールします。  

 - `false`: 互換性のあるすべてのデバイス ドライバーをインストールし、Windows で使用に最適なドライバーが選択されます。  


### <a name="OSDAutoApplyDriverCategoryList"></a> OSDAutoApplyDriverCategoryList

 *[ドライバーの自動適用](task-sequence-steps.md#BKMK_AutoApplyDrivers)ステップに適用されます。*

 (入力)

 ドライバー カタログ カテゴリの一意の ID を記載するカンマ区切りの一覧です。 **[ドライバーの自動適用]** ステップでは、指定されたカテゴリの少なくとも 1 つのドライバーのみが考慮されます。 この値は省略可能であり、既定では設定されていません。 利用可能なカテゴリ ID は、サイトの **SMS_CategoryInstance** オブジェクトの一覧を列挙して取得します。


### <a name="OSDBitLockerRecoveryPassword"></a> OSDBitLockerRecoveryPassword

 *[BitLocker の有効化](task-sequence-steps.md#BKMK_EnableBitLocker)ステップに適用されます。*

 (入力)

 **BitLocker の有効化**ステップは、ランダムな回復パスワードを生成する代わりに、指定された値を回復パスワードとして使用します。 有効な数値の BitLocker 回復パスワードを指定する必要があります。


### <a name="OSDBitLockerStartupKey"></a> OSDBitLockerStartupKey

 *[BitLocker の有効化](task-sequence-steps.md#BKMK_EnableBitLocker)ステップに適用されます。*

 (入力)

 **[BitLocker の有効化]** ステップでは、キー管理オプション **[USB 上のスタートアップ キーのみ]** のランダムなスタートアップ キーを生成する代わりに、信頼されたプラットフォーム モジュール (TPM) をスタートアップ キーとして使用します。 有効な 256 ビット の Base64 エンコードされた BitLocker スタートアップ キーを指定する必要があります。


### <a name="OSDCaptureAccount"></a> OSDCaptureAccount

 *[オペレーティング システム イメージのキャプチャ](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) ステップに適用されます。*

 (入力)

 キャプチャしたイメージをネットワーク共有 ([OSDCaptureDestination](#OSDCaptureDestination)) に格納するためのアクセス許可を持つ Windows アカウント名を指定します。 [OSDCaptureAccountPassword](#OSDCaptureAccountPassword) も指定します。

 OS イメージ キャプチャのアカウントについて詳しくは、[アカウント](/sccm/core/plan-design/hierarchy/accounts#capture-operating-system-image-account)に関するページをご覧ください。


### <a name="OSDCaptureAccountPassword"></a> OSDCaptureAccountPassword

 *[オペレーティング システム イメージのキャプチャ](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) ステップに適用されます。*

 (入力)

 キャプチャしたイメージをネットワーク共有 ([OSDCaptureDestination](#OSDCaptureDestination)) に格納するのに使用される Windows アカウント ([OSDCaptureAccount](#OSDCaptureAccount)) のパスワードを指定します。


### <a name="OSDCaptureDestination"></a> OSDCaptureDestination

 *[オペレーティング システム イメージのキャプチャ](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) ステップに適用されます。*

 (入力)

 タスク シーケンスがキャプチャされた OS イメージを保存する場所を指定します。 ディレクトリ名の最大長は 255 文字です。 ネットワーク共有で認証が必要な場合は、[OSDCaptureAccount](#OSDCaptureAccount) 変数と [OSDCaptureAccountPassword](#OSDCaptureAccountPassword) 変数を指定します。


### <a name="OSDComputerName-input"></a> OSDComputerName (入力)

 *[Windows 設定の適用](task-sequence-steps.md#BKMK_ApplyWindowsSettings)ステップに適用されます。*

 対象のコンピューターの名前を指定します。

 #### <a name="example"></a>例
 `%_SMSTSMachineName%` (既定)


### <a name="OSDComputerName-output"></a> OSDComputerName (出力)

 *[Windows 設定のキャプチャ](task-sequence-steps.md#BKMK_CaptureWindowsSettings) ステップに適用されます。*

 コンピューターの NetBIOS 名に設定します。 この値は、[OSDMigrateComputerName](#OSDMigrateComputerName) 変数が `true` に設定されている場合にのみ設定されます。


### <a name="OSDConfigFileName"></a> OSDConfigFileName

 *[オペレーティング システム イメージの適用](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)ステップに適用されます。*

 (入力)

 OS の展開イメージ パッケージに関連付けられている OS の展開の応答ファイルの名前を指定します。  


### <a name="OSDDataImageIndex"></a> OSDDataImageIndex

 *[データ イメージの適用](task-sequence-steps.md#BKMK_ApplyDataImage)ステップに適用されます。*

 (入力)

 対象のコンピューターに適用されるイメージのインデックス値を指定します。


### <a name="OSDDiskIndex"></a> OSDDiskIndex

 *[ディスクのフォーマットとパーティション作成](task-sequence-steps.md#BKMK_FormatandPartitionDisk)ステップに適用されます。*

 (入力)

 パーティションを作成する物理ディスク番号を指定します。


### <a name="OSDDNSDomain"></a> OSDDNSDomain

 *[ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)ステップに適用されます。*

 (入力)

 対象のコンピューターによって使用されるプライマリ DNS サーバーを指定します。


### <a name="OSDDNSSuffixSearchOrder"></a> OSDDNSSuffixSearchOrder

 *[ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)ステップに適用されます。*

 (入力)

 対象のコンピューターの DNS 検索順序を指定します。


### <a name="OSDDomainName"></a> OSDDomainName

 *[ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)ステップに適用されます。*

 (入力)

 対象コンピューターを参加させる Active Directory ドメインの名前を指定します。 指定する値は Active Directory ドメイン サービスの有効なドメイン名でなければなりません。


### <a name="OSDDomainOUName"></a> OSDDomainOUName

 *[ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)ステップに適用されます。*

 (入力)

 対象コンピューターを参加させる組織単位 (OU) の RFC 1779 形式の名前を指定します。 指定する場合の値は、完全なパスを含む必要があります。

 #### <a name="example"></a>例
 `LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`


### <a name="OSDDoNotLogCommand"></a> OSDDoNotLogCommand
 <!--1358493--> *バージョン 1806 以降*  
 *[コマンド ラインの実行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)ステップに適用されます。*

 (入力)

 機密性が高い可能性のあるデータが表示または記録されないようにするには、この変数を `TRUE` に設定します。 この変数は、[コマンド ラインの実行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)タスク シーケンス ステップの間に、**smsts.log** のプログラム名をマスキングします。   


### <a name="OSDEnableTCPIPFiltering"></a> OSDEnableTCPIPFiltering

 *[ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)ステップに適用されます。*

 (入力)

 TCP/IP フィルタリングを有効にするかどうかを指定します。

 #### <a name="valid-values"></a>有効な値
 - `true`  
 - `false` (既定)  


### <a name="OSDGPTBootDisk"></a> OSDGPTBootDisk

 *[ディスクのフォーマットとパーティション作成](task-sequence-steps.md#BKMK_FormatandPartitionDisk)ステップに適用されます。*

 (入力)

 GPT ハード ディスク上で EFI パーティションを作成するかどうかを指定します。 EFI ベースのコンピューターでは、スタートアップ ディスクとしてこのパーティションを使用します。

 #### <a name="valid-values"></a>有効な値
 - `true`  
 - `false` (既定)


### <a name="OSDImageCreator"></a> OSDImageCreator

 *[オペレーティング システム イメージのキャプチャ](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) ステップに適用されます。*

 (入力)

 イメージを作成したユーザーのオプションの名前。 この名前は WIM ファイルに保存されます。 ユーザー名の最大長は 255 文字です。


### <a name="OSDImageDescription"></a> OSDImageDescription

 *[オペレーティング システム イメージのキャプチャ](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) ステップに適用されます。*

 (入力)

 キャプチャされた OS イメージの、オプションのユーザー定義の説明。 この説明は WIM ファイルに保存されます。 この説明の最大長は 255 文字です。


### <a name="OSDImageIndex"></a> OSDImageIndex

 *[オペレーティング システム イメージの適用](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)ステップに適用されます。*

 (入力)

 対象のコンピューターに適用される WIM イメージのイメージ インデックス値を指定します。


### <a name="OSDImageVersion"></a> OSDImageVersion

 *[オペレーティング システム イメージのキャプチャ](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) ステップに適用されます。*

 (入力)

 キャプチャした OS イメージに割り当てる、ユーザーが任意に定義したバージョン番号。 このバージョン番号は WIM ファイルに保存されます。 この値は、英数字の任意の組み合わせにすることができ、最大長は 32 文字です。


### <a name="OSDInstallDriversAdditionalOptions"></a> OSDInstallDriversAdditionalOptions
<!--516679/2840016--> *バージョン 1806 以降*  
 *[ドライバー パッケージの適用](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage)ステップに適用されます。*

 (入力)

 ドライバー パッケージを適用するときに、DISM コマンドラインに追加する追加オプションを指定します。 タスク シーケンスではコマンド ライン オプションは検証されません。 

 この変数を使用するには、**ドライバー パッケージの適用**ステップで、**[再帰処理オプションを指定して DISM を実行し、ドライバー パッケージをインストール]** の設定を有効にします。 

 詳しくは、「[Windows 10 DISM Command-Line Options](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options)」(Windows 10 DISM のコマンド ライン オプション) をご覧ください。


### <a name="OSDJoinAccount"></a> OSDJoinAccount

 *次のステップに適用されます。*  
 - [ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)   
 - [ドメインまたはワークグループに参加](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  


 (入力)

 対象のコンピューターをドメインに追加するために使用するドメイン ユーザー アカウントを指定します。 この変数はドメインに参加するときに必要になります。

 タスク シーケンスのドメイン参加アカウントについて詳しくは、[アカウント](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account)に関するページをご覧ください。


### <a name="OSDJoinDomainName"></a> OSDJoinDomainName

 *[ドメインまたはワークグループに参加](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)ステップに適用されます。*

 (入力)

 対象コンピューターを参加させる Active Directory ドメインの名前を指定します。 ドメイン名の長さは 1 文字から 255 文字の範囲である必要があります。


### <a name="OSDJoinDomainOUName"></a> OSDJoinDomainOUName

 *[ドメインまたはワークグループに参加](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)ステップに適用されます。*

 (入力)

 対象コンピューターを参加させる組織単位 (OU) の RFC 1779 形式の名前を指定します。 指定する場合の値は、完全なパスを含む必要があります。 OU 名の長さは 0 文字から 32,767 文字の範囲である必要があります。 [OSDJoinType](#OSDJoinType) 変数が `1` (ワークグループに参加) に設定されている場合、この値は設定されません。

 #### <a name="example"></a>例
 `LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

  
### <a name="OSDJoinPassword"></a> OSDJoinPassword

 *次のステップに適用されます。*  
 - [ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
 - [ドメインまたはワークグループに参加](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  


 (入力)

 対象コンピューターが Active Directory ドメインに参加するために使用する [OSDJoinAccount](#OSDJoinAccount) のパスワードを指定します。 タスク シーケンス環境にこの変数が含まれていない場合、Windows セットアップでは空白のパスワードが試行されます。 [OSDJoinType](#OSDJoinType) 変数が `0` (ドメインに参加) に設定されている場合は、この値が必要になります。


### <a name="OSDJoinSkipReboot"></a> OSDJoinSkipReboot

 *[ドメインまたはワークグループに参加](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)ステップに適用されます。*

 (入力)

 対象コンピューターがドメインまたはワークグループに参加した後、再起動をするかどうかを指定します。

 #### <a name="valid-values"></a>有効な値
 - `true`  
 - `false`  


### <a name="OSDJoinType"></a> OSDJoinType

 *[ドメインまたはワークグループに参加](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)ステップに適用されます。*

 (入力)

 対象コンピューターを Windows ドメインに参加させるか、ワークグループに参加させるかを指定します。 

 #### <a name="valid-values"></a>有効な値
 - `0`: 対象コンピューターを Windows ドメインに参加させます  
 - `1`: 対象コンピューターをワークグループに参加させます  


### <a name="OSDJoinWorkgroupName"></a> OSDJoinWorkgroupName

 *[ドメインまたはワークグループに参加](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)ステップに適用されます。*

 (入力)

 対象コンピューターを参加させるワークグループの名前を指定します。 ワークグループ名の長さは 1 ～ 32 文字の範囲であることが必要です。


### <a name="OSDKeepActivation"></a> OSDKeepActivation

 *[Windows のキャプチャの準備](task-sequence-steps.md#BKMK_PrepareWindowsforCapture)ステップに適用されます。*

 (入力)

 sysprep がプロダクト アクティベーション フラグをリセットするかどうかを指定します。

 #### <a name="valid-values"></a>有効な値
 - `true`
 - `false` (既定)


### <a name="OSDLocalAdminPassword"></a> OSDLocalAdminPassword

 *[Windows 設定の適用](task-sequence-steps.md#BKMK_ApplyWindowsSettings)ステップに適用されます。*

 (入力)

 ローカル管理者アカウントのパスワードを指定します。 **[ローカルの管理者パスワードをランダムに生成し、サポートされているすべてのプラットフォームのアカウントを無効にする]** オプションを有効にした場合は、ステップでこの変数が無視されます。 値は 1 ～ 255 文字の範囲で指定する必要があります。


### <a name="OSDMigrateAdapterSettings"></a> OSDMigrateAdapterSettings

 *[ネットワーク設定のキャプチャ](task-sequence-steps.md#BKMK_CaptureNetworkSettings) ステップに適用されます。*

 (入力)

 タスク シーケンスがネットワーク アダプターの情報をキャプチャするかどうかを指定します。 この情報には、TCP/IP、DNS、WINS の構成設定が含まれます。

 #### <a name="valid-values"></a>有効な値
 - `true` (既定)
 - `false`


### <a name="OSDMigrateAdditionalCaptureOptions"></a> OSDMigrateAdditionalCaptureOptions

 *[ユーザー状態のキャプチャ](task-sequence-steps.md#BKMK_CaptureUserState) ステップに適用されます。*

 (入力)

 タスク シーケンスでユーザー状態をキャプチャするために使用されるユーザー状態移行ツール (USMT) 用の追加のコマンド ライン オプションを指定します。 ステップでは、タスク シーケンス エディターでこれらの設定が公開されません。 タスク シーケンスで ScanState に対して自動生成された USMT コマンド ラインに付加される、文字列としてこれらのオプションを指定します。

 タスク シーケンスを実行するまで、このタスク シーケンス変数で指定される USMT オプションの正確性は検証されません。

 使用可能なオプションについて詳しくは、「[ScanState Syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax)」(ScanState の構文) をご覧ください。


### <a name="OSDMigrateAdditionalRestoreOptions"></a> OSDMigrateAdditionalRestoreOptions

 *[ユーザー状態の復元](task-sequence-steps.md#BKMK_RestoreUserState)ステップに適用されます。*

 (入力)

 タスク シーケンスでユーザー状態を復元するときに使用されるユーザー状態移行ツール (USMT) 用の追加のコマンド ライン オプションを指定します。 タスク シーケンスで LoadState に対して自動生成された USMT コマンド ラインに付加される、文字列として追加オプションを指定します。 

 タスク シーケンスを実行するまで、このタスク シーケンス変数で指定される USMT オプションの正確性は検証されません。

 使用可能なオプションについて詳しくは、「[LoadState Syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax)」(LoadState の構文) をご覧ください。


### <a name="OSDMigrateComputerName"></a> OSDMigrateComputerName

 *[Windows 設定のキャプチャ](task-sequence-steps.md#BKMK_CaptureWindowsSettings) ステップに適用されます。*

 (入力)

 コンピューター名を移行するかどうかを指定します。

 #### <a name="valid-values"></a>有効な値
 - `true` (既定)。 [OSDComputerName (出力)](#OSDComputerName-output) 変数は、コンピューターの NetBIOS 名に設定されます。  
 - `false`   


### <a name="OSDMigrateConfigFiles"></a> OSDMigrateConfigFiles

 *[ユーザー状態のキャプチャ](task-sequence-steps.md#BKMK_CaptureUserState) ステップに適用されます。*

 (入力)

 ユーザー プロファイルのキャプチャの制御に使用される構成ファイルを指定します。 この変数は、[OSDMigrateMode](#OSDMigrateMode) が `Advanced` に設定されている場合にのみ使用されます。 カスタマイズされたユーザー プロファイル移行を実行するためには、このカンマ区切りの一覧の値を設定します。

 #### <a name="example"></a>例
 `miguser.xml,migsys.xml,migapps.xml`  


### <a name="OSDMigrateContinueOnLockedFiles"></a> OSDMigrateContinueOnLockedFiles

 *[ユーザー状態のキャプチャ](task-sequence-steps.md#BKMK_CaptureUserState) ステップに適用されます。*

 (入力)

 USMT で一部のファイルをキャプチャできない場合、この変数を使用することで、ユーザー状態のキャプチャを続行できます。 

 #### <a name="valid-values"></a>有効な値
 - `true` (既定)  
 - `false`   


### <a name="OSDMigrateContinueOnRestore"></a> OSDMigrateContinueOnRestore

 *[ユーザー状態の復元](task-sequence-steps.md#BKMK_RestoreUserState)ステップに適用されます。*

 (入力)

 USMT で一部のファイルを復元できない場合でも、プロセスを続行します。

 #### <a name="valid-values"></a>有効な値
 - `true` (既定)  
 - `false`  


### <a name="OSDMigrateEnableVerboseLogging"></a> OSDMigrateEnableVerboseLogging

 *次のステップに適用されます。*  
 - [ユーザー状態のキャプチャ](task-sequence-steps.md#BKMK_CaptureUserState)  
 - [ユーザー状態の復元](task-sequence-steps.md#BKMK_RestoreUserState)  


 (入力)

 USMT の詳細ログ記録を有効にします。 ステップではこの値が必要です。

 #### <a name="valid-values"></a>有効な値
 - `true`  
 - `false` (既定)  


### <a name="OSDMigrateLocalAccounts"></a> OSDMigrateLocalAccounts

 *[ユーザー状態の復元](task-sequence-steps.md#BKMK_RestoreUserState)ステップに適用されます。*

 (入力)

 ローカル コンピューター アカウントを復元するかどうかを指定します。

 #### <a name="valid-values"></a>有効な値
 - `true`  
 - `false` (既定)  


### <a name="OSDMigrateLocalAccountPassword"></a> OSDMigrateLocalAccountPassword

 *[ユーザー状態の復元](task-sequence-steps.md#BKMK_RestoreUserState)ステップに適用されます。*

 (入力)

 [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) 変数が `true` の場合、この変数には移行された "*すべての*" ローカル アカウントに割り当てるパスワードが含まれる必要があります。 USMT は、移行されたすべてのローカル アカウントに同じパスワードを割り当てます。 このパスワードは一時的なものと考え、後で他の方法で変更してください。


### <a name="OSDMigrateMode"></a> OSDMigrateMode

 *[ユーザー状態のキャプチャ](task-sequence-steps.md#BKMK_CaptureUserState) ステップに適用されます。*

 (入力)

 USMT によってキャプチャされたファイルをカスタマイズできます。 

 #### <a name="valid-values"></a>有効な値
 - `Simple`: タスク シーケンスでは標準の USMT 構成ファイルのみが使用されます  

 - `Advanced`: タスク シーケンス変数 [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) により、USMT が使用する構成ファイルが指定されます  


### <a name="OSDMigrateNetworkMembership"></a> OSDMigrateNetworkMembership

 *[ネットワーク設定のキャプチャ](task-sequence-steps.md#BKMK_CaptureNetworkSettings) ステップに適用されます。*

 (入力)

 タスク シーケンスがワークグループまたはドメインのメンバーシップ情報を移行するかどうかを指定します。

 #### <a name="valid-values"></a>有効な値
 - `true` (既定)
 - `false`


### <a name="OSDMigrateRegistrationInfo"></a> OSDMigrateRegistrationInfo

 *[Windows 設定のキャプチャ](task-sequence-steps.md#BKMK_CaptureWindowsSettings) ステップに適用されます。*

 (入力)

 ステップでユーザーと組織の情報を移行するかどうかを指定します。

 #### <a name="valid-values"></a>有効な値
 - `true` (既定)。 [OSDRegisteredOrgName (出力)](#OSDRegisteredOrgName-output) 変数はコンピューターの登録組織名に設定されます。  
 - `false`   


### <a name="OSDMigrateSkipEncryptedFiles"></a> OSDMigrateSkipEncryptedFiles

 *[ユーザー状態のキャプチャ](task-sequence-steps.md#BKMK_CaptureUserState) ステップに適用されます。*

 (入力)

 暗号化ファイルをキャプチャするかどうかを指定します。

 #### <a name="valid-values"></a>有効な値
 - `true`  
 - `false` (既定)  


### <a name="OSDMigrateTimeZone"></a> OSDMigrateTimeZone

 *[Windows 設定のキャプチャ](task-sequence-steps.md#BKMK_CaptureWindowsSettings) ステップに適用されます。*

 (入力)

 コンピューターのタイム ゾーンを移行するかどうかを指定します。

 #### <a name="valid-values"></a>有効な値
 - `true` (既定)。 変数 [OSDTimeZone (出力)](#OSDTimeZone-output) はコンピューターのタイム ゾーンに設定されます。  
 - `false`   


### <a name="OSDNetworkJoinType"></a> OSDNetworkJoinType

 *[ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)ステップに適用されます。*

 (入力)

 対象コンピューターを Active Directory ドメインに参加させるか、ワークグループに参加させるかを指定します。

 #### <a name="value-values"></a>値
 - `0`: Active Directory ドメインに参加します  
 - `1`: ワークグループに参加します


### <a name="OSDPartitions"></a> OSDPartitions

 *[ディスクのフォーマットとパーティション作成](task-sequence-steps.md#BKMK_FormatandPartitionDisk)ステップに適用されます。*

 (入力)

 このタスク シーケンス変数は、パーティション設定の配列変数です。 配列内の各要素は、ハード ディスクの単一パーティションの設定を表します。 各パーティションに定義された設定にアクセスするには、配列変数名にゼロから始まるディスク パーティション番号とプロパティ名を結合します。

次の変数名は、このステップでハード ディスクに作成される "*最初の*" パーティションに対して、プロパティを定義するときに使用します。

 #### <a name="osdpartitions0type"></a>OSDPartitions0Type
 パーティションの種類を指定します。 このプロパティは必須です。 有効な値は、`Primary`、`Extended`、`Logical`、`Hidden` です。

 #### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem
 パーティションをフォーマットするときに使用するファイル システムの種類を指定します。 このプロパティは省略可能です。 ファイル システムを指定しない場合、ステップではパーティションはフォーマットされません。 有効な値は、`FAT32`、`NTFS` です。

 #### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable
 パーティションが起動可能かどうかを指定します。 このプロパティは必須です。 MBR ディスクでこの値が `TRUE` に設定されている場合、ステップではこのパーティションがアクティブとしてマークされます。

 #### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat
 使用されるフォーマットの種類を指定します。 このプロパティは必須です。 この値が `TRUE` に設定されている場合、ステップではクイック フォーマットが実行されます。 それ以外の場合、ステップではフル フォーマットが実行されます。

 #### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName
 フォーマット時にボリュームに割り当てられる名前を指定します。 このプロパティは省略可能です。

 #### <a name="osdpartitions0size"></a>OSDPartitions0Size
 パーティションのサイズを指定します。 このプロパティは省略可能です。 このプロパティを指定しない場合、残りの空き領域すべてを使用してパーティションが作成されます。 単位は **OSDPartitions0SizeUnits** 変数で指定します。

 #### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits
 ステップではこれらの単位を使用して、**OSDPartitions0Size** 変数が解釈されます。 このプロパティは省略可能です。 有効な値は、`MB` (既定)、`GB`、`Percent` です。

 #### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable
 このステップでパーティションを作成するときに、Windows PE で次に利用可能なドライブ文字が常に使用されます。 別のタスク シーケンス変数の名前を指定する場合は、この省略可能なプロパティを使用します。 ステップではこの変数を使用して、今後の参照用に新しいドライブ文字を保存します。

 このタスク シーケンス ステップで複数のパーティションを定義する場合、"*2 番目*" のパーティションのプロパティは変数名でインデックス **1** を使用して定義されます。 たとえば、**OSDPartitions1Type**、**OSDPartitions1FileSystem**、**OSDPartitions1Bootable**、**OSDPartitions1QuickFormat**、**OSDPartitions1VolumeName** のようになります。


### <a name="OSDPartitionStyle"></a> OSDPartitionStyle

 *[ディスクのフォーマットとパーティション作成](task-sequence-steps.md#BKMK_FormatandPartitionDisk)ステップに適用されます。*

 (入力)

 ディスクをパーティション分割するときに使用するパーティション スタイルを指定します。 

 #### <a name="valid-values"></a>有効な値
 - `GPT`: GUID パーティション テーブル スタイルを使用します
 - `MBR`: マスター ブート レコード パーティション スタイルを使用します


### <a name="OSDProductKey"></a> OSDProductKey

 *[Windows 設定の適用](task-sequence-steps.md#BKMK_ApplyWindowsSettings)ステップに適用されます。*

 (入力)

 Windows のプロダクト キーを指定します。 値は 1 ～ 255 文字の範囲で指定する必要があります。


### <a name="OSDRandomAdminPassword"></a> OSDRandomAdminPassword

 *[Windows 設定の適用](task-sequence-steps.md#BKMK_ApplyWindowsSettings)ステップに適用されます。*

 (入力)

 新しい OS のローカル管理者アカウントにランダム生成パスワードを使用するかどうかを指定します。 

 #### <a name="valid-values"></a>有効な値
 - `true` (既定): Windows セットアップで対象コンピューターのローカル管理者アカウントが無効になります  

 - `false`: Windows セットアップで対象コンピューターのローカル管理者アカウントが有効になり、アカウント パスワードが [OSDLocalAdminPassword](#OSDLocalAdminPassword) の値に設定されます  


### <a name="OSDRegisteredOrgName-input"></a> OSDRegisteredOrgName (input)

 *[Windows 設定の適用](task-sequence-steps.md#BKMK_ApplyWindowsSettings)ステップに適用されます。*

 新しい OS に既定で登録する組織名を指定します。 値は 1 ～ 255 文字の範囲で指定する必要があります。


### <a name="OSDRegisteredOrgName-output"></a> OSDRegisteredOrgName (出力)

 *[Windows 設定のキャプチャ](task-sequence-steps.md#BKMK_CaptureWindowsSettings) ステップに適用されます。*

 コンピューターの登録組織名に設定します。 この値は、[OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) 変数が `true` に設定されている場合にのみ設定されます。


### <a name="OSDRegisteredUserName"></a> OSDRegisteredUserName

 *[Windows 設定の適用](task-sequence-steps.md#BKMK_ApplyWindowsSettings)ステップに適用されます。*

 (入力)

 新しい OS に既定で登録するユーザー名を指定します。 値は 1 ～ 255 文字の範囲で指定する必要があります。


### <a name="OSDServerLicenseConnectionLimit"></a> OSDServerLicenseConnectionLimit

 *[Windows 設定の適用](task-sequence-steps.md#BKMK_ApplyWindowsSettings)ステップに適用されます。*

 (入力)

 最大接続許可数を指定します。 接続数は 5 ～ 9999 の範囲で指定する必要があります。


### <a name="OSDServerLicenseMode"></a> OSDServerLicenseMode

 *[Windows 設定の適用](task-sequence-steps.md#BKMK_ApplyWindowsSettings)ステップに適用されます。*

 (入力)

 使用する Windows Server ライセンス モードを指定します。

 #### <a name="valid-values"></a>有効な値
 - `PerSeat`
 - `PerServer`


### <a name="OSDSetupAdditionalUpgradeOptions"></a> OSDSetupAdditionalUpgradeOptions

 *[オペレーティング システムのアップグレード](task-sequence-steps.md#BKMK_UpgradeOS) ステップに適用されます。*

 (入力)

 Windows 10 へのアップグレードの際に Windows セットアップに追加されるコマンド ライン オプションを指定します。 タスク シーケンスではコマンド ライン オプションは検証されません。 

 詳細については、「 [Windows セットアップ コマンド ライン オプション](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)」を参照してください。


### <a name="OSDStateFallbackToNAA"></a> OSDStateFallbackToNAA

 *[状態ストアの要求](task-sequence-steps.md#BKMK_RequestStateStore)ステップに適用されます。*

 (入力)

 コンピューター アカウントが状態移行ポイントに接続できない場合に、タスク シーケンスでネットワーク アクセス アカウント (NAA) を使用するようにフォールバックするかどうかをこの変数で指定します。 

 ネットワーク アクセス アカウントについて詳しくは、[アカウント](/sccm/core/plan-design/hierarchy/accounts#network-access-account)に関するページをご覧ください。

 #### <a name="valid-values"></a>有効な値
 - `true`  
 - `false` (既定)  


### <a name="OSDStateSMPRetryCount"></a> OSDStateSMPRetryCount

 *[状態ストアの要求](task-sequence-steps.md#BKMK_RequestStateStore)ステップに適用されます。*

 (入力)

 タスク シーケンス ステップが状態移行ポイントの検索を試行する回数を指定します。この回数を超えるとこの手順は失敗します。 回数は 0 ～ 600 の範囲で指定する必要があります。


### <a name="OSDStateSMPRetryTime"></a> OSDStateSMPRetryTime

 *[状態ストアの要求](task-sequence-steps.md#BKMK_RequestStateStore)ステップに適用されます。*

 (入力)

 タスク シーケンス ステップが再試行間に待機する秒数を指定します。 最大秒数は 30 文字です。


### <a name="OSDStateStorePath"></a> OSDStateStorePath

 *次のステップに適用されます。*  
 - [ユーザー状態のキャプチャ](task-sequence-steps.md#BKMK_CaptureUserState)  
 - [状態ストアのリリース](task-sequence-steps.md#BKMK_ReleaseStateStore)  
 - [状態ストアの要求](task-sequence-steps.md#BKMK_RequestStateStore)  
 - [ユーザー状態の復元](task-sequence-steps.md#BKMK_RestoreUserState)  


 (入力)

 タスク シーケンスがユーザー状態を保存または復元するフォルダーのネットワーク共有またはローカル パス名です。 既定値はありません。


### <a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive

 *[オペレーティング システム イメージの適用](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)ステップに適用されます。*

 (出力)

 イメージが適用された後で OS ファイルが含まれているパーティションのドライブ文字を示します。


### <a name="OSDTargetSystemRoot-input"></a> OSDTargetSystemRoot (入力)

 *[オペレーティング システム イメージのキャプチャ](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) ステップに適用されます。*

 参照コンピューター上にインストールされた OS の Windows ディレクトリへのパスを指定します。 タスク シーケンスは、Configuration Manager によるキャプチャにサポートされている OS として、これを確認します。


### <a name="OSDTargetSystemRoot-output"></a> OSDTargetSystemRoot (出力)

 *[Windows のキャプチャの準備](task-sequence-steps.md#BKMK_PrepareWindowsforCapture)ステップに適用されます。*

 参照コンピューター上にインストールされた OS の Windows ディレクトリへのパスを指定します。 タスク シーケンスは、Configuration Manager によるキャプチャにサポートされている OS として、これを確認します。


### <a name="OSDTimeZone-input"></a> OSDTimeZone (入力)

 *[Windows 設定の適用](task-sequence-steps.md#BKMK_ApplyWindowsSettings)ステップに適用されます。*

 新しい OS で使用する既定のタイム ゾーン設定を指定します。


### <a name="OSDTimeZone-output"></a> OSDTimeZone (出力)

 *[Windows 設定のキャプチャ](task-sequence-steps.md#BKMK_CaptureWindowsSettings) ステップに適用されます。*

 コンピューターのタイム ゾーンに設定します。 この値は、[OSDMigrateTimeZone](#OSDMigrateTimeZone) 変数が `true` に設定されている場合にのみ設定されます。


### <a name="OSDWipeDestinationPartition"></a> OSDWipeDestinationPartition

 *[データ イメージの適用](task-sequence-steps.md#BKMK_ApplyDataImage)ステップに適用されます。*

 (入力)

 対象のパーティションにあるファイルを削除するかどうかを指定します。

 #### <a name="valid-values"></a>有効な値
 - `true` (既定)
 - `false`


### <a name="OSDWorkgroupName"></a> OSDWorkgroupName

 *[ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)ステップに適用されます。*

 (入力)

 対象のコンピューターを参加させるワークグループの名前を指定します。

 この変数または [OSDDomainName](#OSDDomainName) 変数を指定します。 ワークグループの名前は 32 文字までの長さにできます。 


### <a name="SMSClientInstallProperties"></a> SMSClientInstallProperties

 *[Windows と ConfigMgr のセットアップ](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) ステップに適用されます。*

 (入力)

 タスク シーケンスが Configuration Manager クライアントをインストールするときに使用するクライアント インストール プロパティを指定します。

 詳しくは、[クライアント インストールのパラメーターとプロパティ](/sccm/core/clients/deploy/about-client-installation-properties)に関するページをご覧ください。


### <a name="SMSConnectNetworkFolderAccount"></a> SMSConnectNetworkFolderAccount

 *[ネットワーク フォルダーへの接続](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)ステップに適用されます。*

 (入力)

 [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath) のネットワーク共有に接続するために使用するユーザー アカウントを指定します。 [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword) の値でアカウントのパスワードを指定します。

 タスク シーケンスのネットワーク フォルダー接続アカウントについて詳しくは、[アカウント](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-network-folder-connection-account)に関するページをご覧ください。


### <a name="SMSConnectNetworkFolderDriveLetter"></a> SMSConnectNetworkFolderDriveLetter

 *[ネットワーク フォルダーへの接続](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)ステップに適用されます。*

 (入力)

 接続先のネットワーク ドライブ文字を指定します。 この値は省略可能です。 指定しない場合、ネットワーク接続はドライブ文字にマップされません。 この値を指定する場合は、値は D から Z までの範囲でなければなりません。X は、Windows PE フェーズの間に Windows PE によって使用されるドライブ文字なので使用しないでください。

 #### <a name="examples"></a>例
 - `D:`  
 - `E:`  


### <a name="SMSConnectNetworkFolderPassword"></a> SMSConnectNetworkFolderPassword

 *[ネットワーク フォルダーへの接続](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)ステップに適用されます。*

 (入力)

 [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath) のネットワーク共有に接続するために使用する [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) のパスワードを指定します。 


### <a name="SMSConnectNetworkFolderPath"></a> SMSConnectNetworkFolderPath

 *[ネットワーク フォルダーへの接続](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)ステップに適用されます。*

 (入力)

 接続に使用するネットワーク パスを指定します。 このパスをドライブ文字にマップする必要がある場合は、[SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter) の値を使用します。

 #### <a name="example"></a>例
 `\\server\share`


### <a name="SMSInstallUpdateTarget"></a> SMSInstallUpdateTarget

 *[ソフトウェア更新プログラムのインストール](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) ステップに適用されます。*

 (入力)

 すべての更新プログラムをインストールするのか、必須の更新プログラムのみインストールするのかを指定します。

 #### <a name="valid-values"></a>有効な値
 - `All`  
 - `Mandatory`  


### <a name="SMSRebootMessage"></a> SMSRebootMessage

 *[コンピューターの再起動](task-sequence-steps.md#BKMK_RestartComputer)ステップに適用されます。*

 (入力)

 対象コンピューターの再起動前にユーザーに表示されるメッセージを指定します。 この変数を設定しなかった場合、既定のメッセージ テキストが表示されます。 メッセージは、512 文字以内で指定する必要があります。

 #### <a name="example"></a>例
 `Save your work before the computer restarts.`  


### <a name="SMSRebootTimeout"></a> SMSRebootTimeout

 *[コンピューターの再起動](task-sequence-steps.md#BKMK_RestartComputer)ステップに適用されます。*

 (入力)

 コンピューターが再起動される前にユーザーに警告を表示する秒数を指定します。 

 #### <a name="examples"></a>例
 - `0` (既定): 再起動メッセージを表示しません  
 - `60`: 1 分間の警告を表示します  


### <a name="SMSTSAssignmentsDownloadInterval"></a> SMSTSAssignmentsDownloadInterval

 ポリシーが返されなかった前回の試行から、ポリシーのダウンロードをクライアントが試行するまで待機する秒数。 既定では、クライアントは **0** 秒待機してから再試行します。 

 この変数は、メディアまたは PXE から起動前コマンドを使用して設定できます。


### <a name="SMSTSAssignmentsDownloadRetry"></a> SMSTSAssignmentsDownloadRetry

 初回の試行でポリシーが見つからなかった場合に、ポリシーのダウンロードをクライアントが試行する回数。 既定では、クライアントは **0** 回再試行します。

 この変数は、メディアまたは PXE から起動前コマンドを使用して設定できます。


### <a name="SMSTSAssignUsersMode"></a> SMSTSAssignUsersMode

 タスク シーケンスがユーザーを対象コンピューターと関連付ける方法を示します。 変数に次のいずれかの値を設定します。  

 - **Auto**: タスク シーケンスは、対象のコンピューターに OS を展開するとき、指定されたユーザーと対象のコンピューターの間に関係を作成します。  

 - **Pending**: タスク シーケンスは、指定されたユーザーと対象のコンピューターの間に関係を作成します。 管理者は関係を承認して設定する必要があります。  

 - **Disabled**: タスク シーケンスは、OS の展開時にユーザーを対象のコンピューターに関連付けません。


### <a name="SMSTSDisableStatusRetry"></a> SMSTSDisableStatusRetry
 <!--512358--> 切断されたシナリオでは、タスク シーケンス エンジンが管理ポイントへのステータス メッセージの送信を繰り返し試行します。 このシナリオのこの動作によって、タスク シーケンスの処理に遅延が発生します。 

 バージョン 1802 以降では、この変数を `true` に設定すると、タスク シーケンス エンジンは最初のメッセージの送信に失敗した後でステータス メッセージの送信を試行しません。 この最初の試行には複数回の再試行が含まれます。

 タスク シーケンスの再開時に、この変数の値は保持されます。 ただし、タスク シーケンスでは初期ステータス メッセージの送信が試行されます。 この最初の試行には複数回の再試行が含まれます。 成功した場合、この変数の値に関係なく、タスク シーケンスではステータスの送信が続行されます。 ステータスの送信に失敗した場合、タスク シーケンスではこの変数の値が使用されます。

 > [!NOTE]  
 > [タスク シーケンス状態レポート](/sccm/core/servers/manage/list-of-reports#task-sequence---deployment-status)は、これらのステータス メッセージに基づいて、各ステップの進捗、履歴、詳細を表示します。


### <a name="SMSTSDisableWow64Redirection"></a> SMSTSDisableWow64Redirection

 *[コマンド ラインの実行](task-sequence-steps.md#BKMK_RunCommandLine)ステップに適用されます。*

 (入力)

 64 ビット OS の場合、既定では、タスク シーケンスで WOW64 ファイル システム リダイレクターを使用して、コマンド ラインでプログラムを見つけて実行します。 この動作では、コマンドを使用して、32 ビット バージョンの OS のプログラムや DLL を見つけることができます。 この変数を `true` に設定すると、WOW64 ファイル システム リダイレクターの使用が無効になります。 ネイティブの 64 ビット バージョンの OS のプログラムと DLL は、コマンドを使用して見つけることができます。 32 ビット OS 上で実行している場合は、この変数は影響を及ぼしません。


### <a name="SMSTSDownloadAbortCode"></a> SMSTSDownloadAbortCode

 この変数には、外部プログラム ダウンローダーの中止コード値が含まれます。 このプログラムは、[SMSTSDownloadProgram](#SMSTSDownloadProgram) 変数で指定されています。 プログラムが SMSTSDownloadAbortCode 変数の値と等しいエラー コードを返した場合、コンテンツのダウンロードは失敗し、他のダウンロード方法は試されません。


### <a name="SMSTSDownloadProgram"></a> SMSTSDownloadProgram

 この変数を使用して、代替コンテンツ プロバイダー (ACP) を指定します。 ACP は、コンテンツのダウンロードに使用されるダウンローダー プログラムです。 タスク シーケンスは、既定の Configuration Manager ダウンローダーの代わりに、ACP を使用します。 コンテンツのダウンロード プロセスの一部として、タスク シーケンスはこの変数を確認します。 指定されている場合、タスク シーケンスはそのプログラムを実行してコンテンツをダウンロードします。


### <a name="SMSTSDownloadRetryCount"></a> SMSTSDownloadRetryCount

 Configuration Manager が配布ポイントからのコンテンツのダウンロードを試行する回数。 既定では、クライアントは **2** 回再試行します。


### <a name="SMSTSDownloadRetryDelay"></a> SMSTSDownloadRetryDelay

 配布ポイントからのコンテンツのダウンロードを再試行する前に Configuration Manager が待機する秒数。 既定では、クライアントは **15** 秒待機してから再試行します。


### <a name="SMSTSDriverRequestConnectTimeOut"></a> SMSTSDriverRequestConnectTimeOut

 *[ドライバーの自動適用](task-sequence-steps.md#BKMK_AutoApplyDrivers)ステップに適用されます。*

 ドライバー カタログを要求する場合、この変数は、タスク シーケンスで HTTP サーバーの接続を待機する秒数となります。 タイムアウトの設定値よりも接続に時間がかかる場合は、タスク シーケンスで要求がキャンセルされます。 既定では、タイムアウトは **60** 秒に設定されます。


### <a name="SMSTSDriverRequestReceiveTimeOut"></a> SMSTSDriverRequestReceiveTimeOut

 *[ドライバーの自動適用](task-sequence-steps.md#BKMK_AutoApplyDrivers)ステップに適用されます。*

 ドライバー カタログを要求する場合、この変数は、タスク シーケンスで応答を待機する秒数となります。 タイムアウトの設定値よりも接続に時間がかかる場合は、タスク シーケンスで要求がキャンセルされます。 既定では、タイムアウトは **480** 秒に設定されます。


### <a name="SMSTSDriverRequestResolveTimeOut"></a> SMSTSDriverRequestResolveTimeOut

 *[ドライバーの自動適用](task-sequence-steps.md#BKMK_AutoApplyDrivers)ステップに適用されます。*

 ドライバー カタログを要求する場合、この変数は、タスク シーケンスで HTTP 名前解決を待機する秒数となります。 タイムアウトの設定値よりも接続に時間がかかる場合は、タスク シーケンスで要求がキャンセルされます。 既定では、タイムアウトは **60** 秒に設定されます。


### <a name="SMSTSDriverRequestSendTimeOut"></a> SMSTSDriverRequestSendTimeOut

 *[ドライバーの自動適用](task-sequence-steps.md#BKMK_AutoApplyDrivers)ステップに適用されます。*

 ドライバー カタログの要求を送信する場合、この変数は、タスク シーケンスで要求の送信を待機する秒数となります。 タイムアウトの設定値より要求に時間がかかる場合は、タスク シーケンスで要求がキャンセルされます。 既定では、タイムアウトは **60** 秒に設定されます。


### <a name="SMSTSErrorDialogTimeout"></a> SMSTSErrorDialogTimeout

 タスク シーケンスでエラーが発生すると、エラーを示すダイアログ ボックスが表示されます。 タスク シーケンスでは、この変数で指定された秒数の経過後にダイアログ ボックスが自動的に閉じられます。 既定では、この値は **900** 秒 (15 分) です。


### <a name="SMSTSLanguageFolder"></a> SMSTSLanguageFolder

 言語に依存しないブート イメージの表示言語を変更するときに使用します。


### <a name="SMSTSLocalDataDrive"></a> SMSTSLocalDataDrive

 タスク シーケンスの実行中に一時ファイルを対象コンピューターに格納する場所を指定します。

 この変数は、コレクション変数の設定によって行うなど、タスク シーケンスが開始する前に設定します。 タスク シーケンスが開始された後で、Configuration Manager は [_SMSTSMDataPath](#SMSTSMDataPath) 変数を定義します。


### <a name="SMSTSMP"></a> SMSTSMP

 この変数を使用して、Configuration Manager の管理ポイントの URL または IP アドレスを指定します。


### <a name="SMSTSMPListRequestTimeoutEnabled"></a> SMSTSMPListRequestTimeoutEnabled

 *次のステップに適用されます。*  
 - [アプリケーションのインストール](task-sequence-steps.md#BKMK_InstallApplication)  
 - [ソフトウェア更新プログラムのインストール](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  


 (入力) 

 クライアントがイントラネット上にない場合に、繰り返しの MPList 要求を有効にしてクライアントを更新するには、この変数を使用します。 既定では、この変数は `True` に設定されます。 

 クライアントがインターネット上にある場合は、不必要な遅延を回避するためにこの変数を `False` に設定します。 


### <a name="SMSTSMPListRequestTimeout"></a> SMSTSMPListRequestTimeout

 *次のステップに適用されます。*  
 - [アプリケーションのインストール](task-sequence-steps.md#BKMK_InstallApplication)  
 - [ソフトウェア更新プログラムのインストール](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  


 (入力) 

 タスク シーケンスがロケーション サービスから管理ポイント リスト (MPList) を取得できなかった場合、この変数はステップを再試行する前に待機するミリ秒数を指定します。 再試行前の既定の待ち時間は `60000` ミリ秒 (60 秒) です。 最大で 3 回再試行します。


### <a name="SMSTSPeerDownload"></a> SMSTSPeerDownload

 この変数を使用して、クライアントに Windows PE ピア キャッシュの使用を許可します。 この変数を `true` に設定すると、この機能が有効になります。


### <a name="SMSTSPeerRequestPort"></a> SMSTSPeerRequestPort

 Windows PE ピア キャッシュで初期ブロードキャストに使用されるカスタム ネットワーク ポート。 クライアント設定で構成されている既定のポートは **8004** です。


### <a name="SMSTSPersistContent"></a> SMSTSPersistContent

 コンテンツをタスク シーケンス キャッシュに一時的に保存するときに使用します。 この変数は、タスク シーケンスが完了した後も Configuration Manager クライアント キャッシュの内容を保持する [SMSTSPreserveContent](#SMSTSPreserveContent) とは異なります。 SMSTSPersistContent ではタスク シーケンス キャッシュを使用し、SMSTSPreserveContent では Configuration Manager クライアント キャッシュを使用します。 


### <a name="SMSTSPostAction"></a> SMSTSPostAction

 タスク シーケンスの完了後に実行されるコマンドを指定します。 たとえば、タスク シーケンスが OS をデバイスに展開した後に、埋め込まれたデバイスで書き込みフィルターを有効にするスクリプトを指定します。


### <a name="SMSTSPreferredAdvertID"></a> SMSTSPreferredAdvertID

 タスク シーケンスで対象コンピューターでの特定の展開が実行されるように強制します。 この変数は、メディアまたは PXE から起動前コマンドを使用して設定します。 この変数が設定されると、タスク シーケンスは要求されたすべての展開をオーバーライドします。


### <a name="SMSTSPreserveContent"></a> SMSTSPreserveContent

 この変数は、展開後に Configuration Manager クライアント キャッシュに残すタスク シーケンス内のコンテンツにフラグを設定します。 この変数は、タスク シーケンスの持続期間だけコンテンツを保持する、[SMSTSPersistContent](#SMSTSPersistContent) とは異なります。 SMSTSPersistContent ではタスク シーケンス キャッシュを使用し、SMSTSPreserveContent では Configuration Manager クライアント キャッシュを使用します。 この機能を有効にするには、SMSTSPreserveContent を `true` に設定します。


### <a name="SMSTSRebootDelay"></a> SMSTSRebootDelay

 コンピューターが再起動するまでの待機時間を秒単位で指定します。 この変数がゼロ (0) の場合、タスク シーケンス マネージャーは再起動の前に通知ダイアログを表示しません。

 #### <a name="example"></a>例
 - `0`: 通知を表示しません  

 - `60`: 1 分間通知を表示します  


### <a name="SMSTSRebootMessage"></a> SMSTSRebootMessage

 再起動通知ダイアログに表示するメッセージを指定します。 この変数を設定しない場合、既定のメッセージが表示されます。

 #### <a name="example"></a>例
 `The task sequence is restarting this computer`


### <a name="SMSTSRebootRequested"></a> SMSTSRebootRequested

 現在のタスク シーケンスのステップを完了した後で再起動が必要であることを示します。 再起動が必要な場合は、この変数を `true` に設定すると、このタスク シーケンス ステップの後で、タスク シーケンス マネージャーが自動的にコンピューターを再起動します。 タスク シーケンス ステップでアクションを完了するために再起動が必要な場合は、この変数を設定します。 コンピューターの再起動後、タスク シーケンスは次のタスク シーケンス ステップから続行されます。


### <a name="SMSTSRetryRequested"></a> SMSTSRetryRequested

 現在のタスク シーケンスのステップを完了した後で再試行を要求します。 このタスク シーケンス変数を設定する場合は、[SMSTSRebootRequested](#SMSTSRebootRequested) も `true` に設定します。 コンピューターの再起動後、タスク シーケンス マネージャーは同じタスク シーケンスのステップを再実行します。


### <a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName

 *[コマンド ラインの実行](task-sequence-steps.md#BKMK_RunCommandLine)ステップに適用されます。*

 (入力)

 コマンド ラインを実行するアカウントを指定します。 この値は、ユーザー名 または ドメイン\ユーザー名 という形式の文字列になります。 [SMSTSRunCommandLinePassword](#SMSTSRunCommandLinePassword) 変数でアカウントのパスワードを指定します。

 タスク シーケンスの実行アカウントについて詳しくは、[アカウント](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account)に関するページをご覧ください。


### <a name="SMSTSRunCommandLinePassword"></a> SMSTSRunCommandLinePassword

 *[コマンド ラインの実行](task-sequence-steps.md#BKMK_RunCommandLine)ステップに適用されます。*

 (入力)

 [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName) 変数で指定されたアカウントのパスワードを指定します。


### <a name="SMSTSSoftwareUpdateScanTimeout"></a> SMSTSSoftwareUpdateScanTimeout

 *[ソフトウェア更新プログラムのインストール](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) ステップに適用されます。*

 (入力)

 このステップにおけるソフトウェア更新プログラムのスキャンのタイムアウトを制御します。 たとえば、スキャン中に多数の更新プログラムが予想される場合は、この値を増やします。 既定値は `1800` 秒 (30 分) です。 変数値は秒単位で設定されます。


### <a name="SMSTSUDAUsers"></a> SMSTSUDAUsers

 `<DomainName>\<UserName>` の形式を使用して、対象コンピューターのプライマリ ユーザーを指定します。 複数のユーザーは、コンマ (`,`) で区切ります。 詳細については、「[System Center Configuration Manager でユーザーをセットアップ先のコンピューターに関連付ける](/sccm/osd/get-started/associate-users-with-a-destination-computer)」を参照してください。

 #### <a name="example"></a>例
 `contoso\jqpublic, contoso\megb, contoso\janedoh`


### <a name="SMSTSWaitForSecondReboot"></a> SMSTSWaitForSecondReboot

 *[ソフトウェア更新プログラムのインストール](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) ステップに適用されます。*

 (入力)

 ソフトウェア更新プログラムのインストールで 2 回再起動が必要な場合に、この省略可能なタスク シーケンス変数でクライアントの動作を制御します。 この変数は、ソフトウェア更新プログラムのインストールからの 2 つ目の再起動によってタスク シーケンスが失敗するのを防ぐために、このステップの前に設定します。

 コンピューターの再起動中にこのステップでタスク シーケンスが一時停止する時間を指定する場合は、SMSTSWaitForSecondReboot の値を秒単位で設定します。 2 つ目の再起動がある場合には十分な時間を取るようにしてください。 

たとえば、SMSTSWaitForSecondReboot を `600` に設定した場合、再起動してから追加のステップが実行されるまで、タスク シーケンスが 10 分間一時停止します。 この変数は、何百ものソフトウェア更新プログラムが 1 つのソフトウェア更新プログラムのインストール タスク シーケンス ステップでインストールされる場合に便利です。


### <a name="TSDisableProgressUI"></a> TSDisableProgressUI
 <!-- 1354291 --> この変数を使って、タスク シーケンスが進行状況をエンド ユーザーに表示するタイミングを制御します。 異なる時点で進行状況の非表示または表示を切り替えるには、タスク シーケンス内で複数回この変数を設定します。  

 - `true`: タスク シーケンスの進行状況を非表示にします  

 - `false`: タスク シーケンスの進行状況を表示します  


### <a name="TSErrorOnWarning"></a> TSErrorOnWarning 

 *[アプリケーションのインストール](task-sequence-steps.md#BKMK_InstallApplication) ステップに適用されます。*

 (入力) 

 タスク シーケンス エンジンがこのステップで検出された警告をエラーと見なすかどうかを指定します。 1 つ以上のアプリケーション、または必要な依存関係がインストールされていない場合、要件を満たしていないため、タスク シーケンスでは [_TSAppInstallStatus](#TSAppInstallStatus) 変数を `Warning` に設定します。 この変数を `True` に設定したときに、タスク シーケンスでは **_TSAppInstallStatus** が `Warning` に設定されている場合、結果はエラーとなります。 値 `False` が既定の動作です。


### <a name="WorkingDirectory"></a> WorkingDirectory

 *[コマンド ラインの実行](task-sequence-steps.md#BKMK_RunCommandLine)ステップに適用されます。*

 (入力)

 コマンド ラインのアクションの開始ディレクトリを指定します。 ディレクトリ名は、255 文字以内で指定する必要があります。

 #### <a name="examples"></a>例
 - `C:\`  
 - `%SystemRoot%`  



## <a name="deprecated-variables"></a>非推奨の変数

以下の変数は非推奨です。

- **OSDAllowUnsignedDriver**: Windows Vista 以降のオペレーティング システムの展開時には使用されません
- **OSDBuildStorageDriverList**: Windows XP および Windows Server 2003 にのみ適用されます
- **OSDDiskpartBiosCompatibilityMode**: Windows XP または Windows Server 2003 を展開する場合にのみ必要です
- **OSDInstallEditionIndex**: Windows Vista より後では必要ありません
- **OSDPreserveDriveLetter**: 詳しくは、「[OSDPreserveDriveLetter](#OSDPreserveDriveLetter)」をご覧ください

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

 > [!Important]
 > このタスク シーケンス変数は非推奨とされます。 
 >
 > 既定では、OS の展開中に、Windows セットアップが、使用する最適なドライブ文字を決定します (通常は C:)。 

 *以前の動作*: イメージの適用時に、OSDPreverveDriveLetter 変数で、タスク シーケンスがイメージ ファイル (WIM) にキャプチャされたドライブ文字を使用するかどうかを判断します。 この変数の値を `false` に設定して、**オペレーティング システムの適用**タスク シーケンス ステップの **[適用先]** 設定で指定した場所を使用します。 詳しくは、「[オペレーティング システム イメージの適用](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)」をご覧ください。



## <a name="see-also"></a>関連項目

- [タスク シーケンスのステップ](/sccm/osd/understand/task-sequence-steps)
- [タスク シーケンス変数の使用](/sccm/osd/understand/using-task-sequence-variables)
- [タスクの自動化計画に関する考慮事項](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
