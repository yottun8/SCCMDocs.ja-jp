---
title: タスク シーケンス アクション変数
titleSuffix: Configuration Manager
description: ネットワーク設定変数などのシーケンス アクション変数を使用して、Configuration Manager のタスク シーケンスでシングル ステップの構成設定を指定します。
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e2269031-0977-4f01-a274-420e00630575
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f66203e335524fa922ec1b6ab3dd4dc5fb917b0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>System Center Configuration Manager でのタスク シーケンス アクション変数

*適用対象: System Center Configuration Manager (Current Branch)*

タスク シーケンス アクション変数では、System Center Configuration Manager タスク シーケンスの単一ステップで使用される構成設定を指定します。 既定では、タスク シーケンス ステップでその設定を初期化してから実行します。 これらの設定は、関連付けられているタスク シーケンス ステップの実行中にのみ使用できます。 つまり、タスク シーケンスではタスク シーケンス ステップの実行前に、タスク シーケンス環境にアクション変数値が追加されます。 タスク シーケンスではステップの実行後に環境から値が削除されます。  

## <a name="action-variable-example"></a>アクション変数の例  
 たとえば、**[コマンド ラインの実行]** タスク シーケンスのステップを使用して、コマンド ライン操作の開始ディレクトリを指定できます。 このステップには、既定値がタスク シーケンス環境に **WorkingDirectory** 変数として格納される **[開始]** プロパティが含まれます。 **WorkingDirectory** 環境変数は、**[コマンド ラインの実行]** タスク シーケンス アクションの実行前に初期化されます。 **[コマンド ラインの実行]** ステップの実行中に、**[開始]** プロパティを使用して **WorkingDirectory** の値にアクセスできます。 ステップの完了後、タスク シーケンスでは環境から **WorkingDirectory** 変数の値が削除されます。 シーケンスに別の **[コマンド ラインの実行]** タスク シーケンス ステップが含まれている場合、そのタスク シーケンスで新しい **WorkingDirectory** 変数が初期化され、現在のステップの開始値に設定されます。  

 タスク シーケンス アクション変数の*既定* 値は、タスク シーケンス ステップの実行時に示されます。 *新しい* 値を設定した場合、タスク シーケンスの複数のステップで使用できます。 タスク シーケンス変数の作成方法のいずれかを使用して、組み込み変数値を上書きすると、新しい値が環境に残り、タスク シーケンスの他のステップの既定値が上書きされます。 たとえば、**[タスク シーケンス変数の設定]** ステップをタスク シーケンスの最初のステップとして追加し、**[WorkingDirectory]** 変数を **C:\\** に設定した場合は、タスク シーケンスの **[コマンド ラインの実行]** ステップで新しい開始ディレクトリ値が使用されます。  

## <a name="action-variables-for-task-sequence-actions"></a>タスク シーケンス アクションのアクション変数  
 Configuration Manager タスク シーケンス変数は、関連付けられたタスク シーケンス アクションごとに分類されます。 特定のアクションに関連付けられているアクション変数の詳細については、次のリンク先を参照してください。 タスク シーケンス変数は、タスク シーケンスで何が行われるかを制御します。 タスク シーケンスの入力変数に指定した変数が、読み取られて使用されます。 または、[[タスク シーケンス変数の設定]](task-sequence-steps.md#BKMK_SetTaskSequenceVariable) ステップか TSEnvironment COM オブジェクトを使用して、実行時に変数を設定することもできます。 タスク シーケンス アクションでのみ、変数が出力変数と見なされます。 タスク シーケンスの後続のアクションでこれらの出力変数が読み取られます。  

> [!NOTE]  
>  すべてのタスク シーケンス アクションが、一連のタスク シーケンス変数に関連付けられているわけではありません。 たとえば、BitLocker の有効化アクションに関連付けれている変数はありますが、BitLocker の無効化アクションに関連付けられている変数はありません。  



###  <a name="BKMK_ApplyDataImage"></a> データ イメージの適用   
 詳細については、「[データ イメージの適用](task-sequence-steps.md#BKMK_ApplyDataImage)」を参照してください。 

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (入力)|対象のコンピューターに適用されるイメージのインデックス値を指定します。|  
|OSDWipeDestinationPartition<br /><br /> (入力)|対象のパーティションにあるファイルを削除するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **true** (既定)<br /><br /> **false**|  



###  <a name="BKMK_ApplyDriverPackage"></a> ドライバー パッケージの適用   
詳細については、「[ドライバー パッケージの適用](task-sequence-steps.md#BKMK_ApplyDriverPackage)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (入力)|ドライバー パッケージからインストールする大容量記憶装置デバイス ドライバーのコンテンツ ID を指定します。 この変数を指定しない場合、大容量記憶装置ドライバーはインストールされません。|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (入力)|インストールする大容量記憶装置ドライバーの INF ファイルを指定します。<br /><br /> <br /><br /> このタスク シーケンス変数は、OSDApplyDriverBootCriticalContentUniqueID が設定されている場合に必要です。|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (入力)|大容量記憶装置デバイス ドライバーをインストールするかどうかを指定します。この変数は **scsi** にする必要があります。<br /><br /> このタスク シーケンス変数は、OSDApplyDriverBootCriticalContentUniqueID が設定されている場合に必要です。|  
|OSDApplyDriverBootCriticalID<br /><br /> (入力)|インストールする大容量記憶装置デバイス ドライバーの起動に必要な ID を指定します。 この ID は、デバイス ドライバーの txtsetup.oem ファイルの **scsi** セクションに一覧表示されます。<br /><br /> このタスク シーケンス変数は、OSDApplyDriverBootCriticalContentUniqueID が設定されている場合に必要です。|  
|OSDAllowUnsignedDriver<br /><br /> (入力)|署名されていないデバイス ドライバーのインストールを許可するように Windows を構成するかどうかを指定します。 このタスク シーケンス変数は、Windows Vista 以降のオペレーティング システムの展開時には使用されません。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false** (既定)|  



###  <a name="BKMK_ApplyNetworkSettings"></a> ネットワーク設定の適用   
 詳細については、「[ネットワーク設定の適用](task-sequence-steps.md#BKMK_ApplyNetworkSettings)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (入力)|このタスク シーケンス変数は、配列変数です。 配列内の各要素は、コンピューター上の単一ネットワーク アダプターの設定を表します。 各アダプターの設定にアクセスするには、配列変数名にゼロから始まるネットワーク アダプター インデックスとプロパティ名を組み合わせます。<br /><br />このステップで複数のネットワーク アダプターを構成する場合、変数名でインデックスを使用して、2 番目のネットワーク アダプターのプロパティが定義されます。 たとえば、OSDAdapter1EnableDHCP、OSDAdapter1IPAddressList、OSDAdapter1DNSDomain、OSDAdapter1WINSServerList、OSDAdapter1EnableWINS のようになります。<br /><br />たとえば、次の変数名を使用して、このタスク シーケンス ステップで構成する最初のネットワーク アダプターのプロパティを定義します。<br /><br /> <ul><li>**OSDAdapter0EnableDHCP**: **true** の場合は、アダプターの動的ホスト構成プロトコル (DHCP) が有効になります。<br />    この設定は必須です。 使用できる値は **True** または **False** です。</li><li>**OSDAdapter0IPAddressList**: アダプターの IP アドレスを示すコンマ区切りの一覧。 このプロパティは **EnableDHCP** が **FALSE**に設定されている場合を除き、無視されます。<br />    この設定は必須です。</li><li>**OSDAdapter0SubnetMask**: サブネット マスクのコンマ区切りの一覧。 このプロパティは **EnableDHCP** が **FALSE**に設定されている場合を除き、無視されます。<br />    この設定は必須です。</li><li>**OSDAdapter0Gateways**: IP ゲートウェイ アドレスのコンマ区切りの一覧。 このプロパティは **EnableDHCP** が **FALSE**に設定されている場合を除き、無視されます。<br />    この設定は必須です。</li><li>**OSDAdapter0DNSDomain**: アダプターのドメイン ネーム システム (DNS) ドメイン。</li><li>**OSDAdapter0DNSServerList**: アダプターの DNS サーバーを示すコンマ区切りの一覧。<br />    この設定は必須です。</li><li>**OSDAdapter0EnableDNSRegistration**: **true** の場合は、アダプターの IP アドレスが DNS に登録されます。</li><li>**OSDAdapter0EnableFullDNSRegistration**: **true** の場合は、アダプターの IP アドレスがコンピューターのフル DNS 名で DNS に登録されます。</li><li>**OSDAdapter0EnableIPProtocolFiltering**: **true** の場合は、アダプターで IP プロトコル フィルターが有効になります。</li><li>**OSDAdapter0IPProtocolFilterList**: IP での実行を許可されたプロトコルのコンマ区切りの一覧。 このプロパティは **EnableIPProtocolFiltering** が **FALSE**に設定されている場合、無視されます。</li><li>**OSDAdapter0EnableTCPFiltering**: **true** の場合は、アダプターで TCP ポート フィルターが有効になります。</li><li>**OSDAdapter0TCPFilterPortList**: TCP へのアクセス許可を付与するポートのコンマ区切りの一覧。 このプロパティは **EnableTCPFiltering** が **FALSE**に設定されている場合、無視されます。</li><li>**OSDAdapter0TcpipNetbiosOptions**: NetBIOS over TCP/IP 用のオプション。 使用できる値は次のとおりです。<br /><br /> <ul><li>**0**: DHCP サーバーから NetBIOS 設定を使用します。</li><li>**1**: NetBIOS over TCP/IP を有効にします。</li><li>**2**: NetBIOS over TCP/IP を無効にします。</li></ul></li><li>**OSDAdapter0EnableWINS**: **true** の場合は、名前解決に WINS が使用されます。</li><li>**OSDAdapter0WINSServerList**: WINS サーバー IP アドレスのコンマ区切りの一覧。 このプロパティは **EnableWINS** が **TRUE**に設定されている場合を除き、無視されます。</li><li>**OSDAdapter0MacAddress**: 設定を物理ネットワーク アダプターに合わせるために使用する MAC アドレス。</li><li>**OSDAdapter0Name**: ネットワーク接続のコントロール パネル プログラムに表示されるネットワーク接続の名前。 名前は 0 ～ 255 文字の長さにしてください。</li><li>**OSDAdapter0Index**: 設定の配列内にあるネットワーク アダプター設定のインデックス。<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (入力)|対象のコンピューターにインストールされているネットワーク アダプターの数を指定します。 **OSDAdapterCount** 値が設定されている場合、各アダプターのすべての構成オプションを設定する必要があります。 たとえば、特定のアダプターの **OSDAdapterTCPIPNetbiosOptions** 値を設定したら、そのアダプターのすべての値を構成する必要があります。<br /><br />この値が指定されていない場合、すべての **OSDAdapter** 値が無視されます。|  
|OSDDNSDomain<br /><br /> (入力)|対象のコンピューターによって使用されるプライマリ DNS サーバーを指定します。|  
|OSDDomainName<br /><br /> (入力)|対象のコンピューターを参加させる Windows ドメインの名前を指定します。 指定する値は Active Directory ドメイン サービスの有効なドメイン名でなければなりません。|  
|OSDDomainOUName<br /><br /> (入力)|対象コンピューターを参加させる組織単位 (OU) の RFC 1779 形式の名前を指定します。 指定する場合の値は、完全なパスを含む必要があります。<br /><br /> 例:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (入力)|TCP/IP フィルタリングを有効にするかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false** (既定)|  
|OSDJoinAccount<br /><br /> (入力)|対象のコンピューターを Windows ドメインに追加するために使用するネットワーク アカウントを指定します。|  
|OSDJoinPassword<br /><br /> (入力)|対象のコンピューターを Windows ドメインに追加するために使用するネットワーク パスワードを指定します。|  
|OSDNetworkJoinType<br /><br /> (入力)|対象コンピューターを Windows ドメインに参加させるか、ワークグループに参加させるかを指定します。<br /><br /> **0** は、対象のコンピューターが Windows ドメインに参加することを示します。 **1** は、コンピューターがワークグループに参加することを示します。<br /><br /> 有効な値:<br /><br /> **0**<br /><br /> **1**|  
|OSDDNSSuffixSearchOrder<br /><br /> (入力)|対象のコンピューターの DNS 検索順序を指定します。|  
|OSDWorkgroupName<br /><br /> (入力)|対象のコンピューターを参加させるワークグループの名前を指定します。<br /><br /> この値または **OSDDomainName** の値を指定します。 ワークグループの名前は 32 文字までの長さにできます。<br /><br /> 例:<br /><br /> **会計**|  



###  <a name="BKMK_ApplyOperatingSystem"></a> オペレーティング システム イメージの適用   
 詳細については、「 [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (入力)|オペレーティング システムの展開パッケージに関連付けられているオペレーティング システムの展開の応答ファイルの名前を指定します。|  
|OSDImageIndex<br /><br /> (入力)|対象のコンピューターに適用される WIM イメージのイメージ インデックス値を指定します。|  
|OSDInstallEditionIndex<br /><br /> (入力)|インストールする Windows Vista 以降のオペレーティング システムのバージョンを指定します。 バージョンを指定しない場合、Windows セットアップでは参照されたプロダクト キーを使用してインストールするバージョンが判断されます。<br /><br /> 次の条件を満たす場合は、0 (ゼロ) のみを使用してください。<br /><br /> -   Windows Vista より前のオペレーティング システムをインストールしている<br />-   Windows Vista 以降のボリューム ライセンス版をインストールしており、プロダクト キーを指定していない<br /><br /> 有効な値:<br /><br /> **0** (既定)|  
|OSDTargetSystemDrive (出力)|オペレーティング システム ファイルが含まれているパーティションのドライブ文字を設定します。|  



###  <a name="BKMK_ApplyWindowsSettings"></a> Windows 設定の適用   
 詳細については、「[Windows 設定の適用](task-sequence-steps.md#BKMK_ApplyWindowsSettings)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (入力)|対象のコンピューターの名前を指定します。<br /><br /> 例:<br /><br /> **%_SMSTSMachineName%** (既定)|  
|OSDProductKey<br /><br /> (入力)|Windows のプロダクト キーを指定します。 値は 1 ～ 255 文字の範囲で指定する必要があります。|  
|OSDRegisteredUserName<br /><br /> (入力)|新しいオペレーティング システムに既定で登録するユーザー名を指定します。 値は 1 ～ 255 文字の範囲で指定する必要があります。|  
|OSDRegisteredOrgName<br /><br /> (入力)|新しいオペレーティング システムに既定で登録する組織名を指定します。 値は 1 ～ 255 文字の範囲で指定する必要があります。|  
|OSDTimeZone<br /><br /> (入力)|新しいオペレーティング システムで使用する既定のタイム ゾーン設定を指定します。|  
|OSDServerLicenseMode<br /><br /> (入力)|使用する Windows Server ライセンス モードを指定します。<br /><br /> 有効な値:<br /><br /> **PerSeat**<br /><br /> **PerServer**|  
|OSDServerLicenseConnectionLimit<br /><br /> (入力)|最大接続許可数を指定します。 接続数は 5 ～ 9999 の範囲で指定する必要があります。|  
|OSDRandomAdminPassword<br /><br /> (入力)|新しいオペレーティング システムの管理者アカウントにランダム生成パスワードを使用するかどうかを指定します。 **true** に設定した場合、Windows セットアップで対象コンピューターのローカル管理者アカウントが無効になります。 **false** に設定した場合、Windows セットアップで対象コンピューターのローカル管理者アカウントが有効になり、アカウント パスワードが **OSDLocalAdminPassword** の値に設定されます。<br /><br /> 有効な値:<br /><br /> **true** (既定)<br /><br /> **false**|  
|OSDLocalAdminPassword<br /><br /> (入力)|ローカルの管理者パスワードを指定します。 **[ローカルの管理者パスワードをランダムに生成し、サポートされているすべてのプラットフォームのアカウントを無効にする]** オプションを有効にした場合は、ステップでこの変数が無視されます。 値は 1 ～ 255 文字の範囲で指定する必要があります。|  



###  <a name="BKMK_AutoApplyDrivers"></a> ドライバーの自動適用   
 詳細については、「[Auto Apply Drivers](task-sequence-steps.md#BKMK_AutoApplyDrivers)」(ドライバーの自動適用) を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (入力)|ドライバー カタログ カテゴリの一意の ID を記載するカンマ区切りの一覧です。 **[ドライバーの自動適用]** ステップでは、指定されたカテゴリの少なくとも 1 つのドライバーのみが考慮されます。 この値は省略可能であり、既定では設定されていません。 利用可能なカテゴリ ID は、サイトの **SMS_CategoryInstance** オブジェクトの一覧を列挙して取得します。|  
|OSDAllowUnsignedDriver<br /><br /> (入力)|署名されていないデバイス ドライバーのインストールを許可するように Windows を構成するかどうかを指定します。 このタスク シーケンス変数は、Windows Vista 以降のオペレーティング システムの展開時には使用されません。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false** (既定)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (入力)|ハードウェア デバイスと互換性のある複数のデバイス ドライバーがドライバー カタログにある場合は、この変数でステップのアクションが決定します。 **true** に設定すると、ステップでは最適なデバイス ドライバーのみがインストールされます。 **false** の場合、ステップでは互換性のあるすべてのデバイス ドライバーがインストールされ、Windows で使用に最適なドライバーが選択されます。<br /><br /> 有効な値:<br /><br /> **true** (既定)<br /><br /> **false**|  
|SMSTSDriverRequestConnectTimeOut|ドライバー カタログを要求する場合、この変数は、タスク シーケンスで HTTP サーバーの接続を待機する秒数となります。 タイムアウトの設定値よりも接続に時間がかかる場合は、タスク シーケンスで要求がキャンセルされます。 既定では、タイムアウトは **60** 秒に設定されます。|  
|SMSTSDriverRequestReceiveTimeOut|ドライバー カタログを要求する場合、この変数は、タスク シーケンスで応答を待機する秒数となります。 タイムアウトの設定値よりも接続に時間がかかる場合は、タスク シーケンスで要求がキャンセルされます。 既定では、タイムアウトは **480** 秒に設定されます。|
|SMSTSDriverRequestResolveTimeOut|ドライバー カタログを要求する場合、この変数は、タスク シーケンスで HTTP 名前解決を待機する秒数となります。 タイムアウトの設定値よりも接続に時間がかかる場合は、タスク シーケンスで要求がキャンセルされます。 既定では、タイムアウトは **60** 秒に設定されます。|
|SMSTSDriverRequestSendTimeOut|ドライバー カタログの要求を送信する場合、この変数は、タスク シーケンスで要求の送信を待機する秒数となります。 タイムアウトの設定値より要求に時間がかかる場合は、タスク シーケンスで要求がキャンセルされます。 既定では、タイムアウトは **60** 秒に設定されます。|



###  <a name="BKMK_CaptureNetworkSettings"></a> ネットワーク設定のキャプチャ   
 詳細については、「[ネットワーク設定のキャプチャ](task-sequence-steps.md#BKMK_CaptureNetworkSettings)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (入力)|ネットワーク アダプター設定 (TCP/IP、DNS、WINS) の構成情報をキャプチャするかどうかを指定します。<br /><br /> 次に例を示します。<br /><br /> **true** (既定)<br /><br /> **false**|  
|OSDMigrateNetworkMembership<br /><br /> (入力)|ワークグループまたはドメインのメンバーシップ情報をオペレーティング システムの展開の一部として移行するかどうかを指定します。<br /><br /> 次に例を示します。<br /><br /> **true** (既定)<br /><br /> **false**|  



###  <a name="BKMK_CaptureOperatingSystemImage"></a> オペレーティング システム イメージのキャプチャ   
 詳細については、「[オペレーティング システム イメージのキャプチャ](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (入力)|キャプチャしたイメージをネットワーク共有に格納するためのアクセス許可を持つ Windows アカウント名を指定します。|  
|OSDCaptureAccountPassword<br /><br /> (入力)|キャプチャしたイメージをネットワーク共有に格納するのに使用される Windows アカウントのパスワードを指定します。|  
|OSDCaptureDestination<br /><br /> (入力)|キャプチャしたオペレーティング システム イメージを保存する場所を指定します。 ディレクトリ名の最大長は 255 文字です。|  
|OSDImageCreator<br /><br /> (入力)|イメージを作成したユーザーのオプションの名前。 この名前は WIM ファイルに保存されます。 ユーザー名の最大長は 255 文字です。|  
|OSDImageDescription<br /><br /> (入力)|キャプチャするオペレーティング システム イメージに関する、オプションのユーザー定義の説明。 この説明は WIM ファイルに保存されます。 この説明の最大長は 255 文字です。|  
|OSDImageVersion<br /><br /> (入力)|キャプチャしたオペレーティング システム イメージに割り当てる、ユーザーが任意に定義したバージョン番号。 このバージョン番号は WIM ファイルに保存されます。 この値は、文字の任意の組み合わせにすることができ、最大長は 32 文字です。|  
|OSDTargetSystemRoot<br /><br /> (入力)|参照コンピューター上にインストールされたオペレーティング システムの Windows ディレクトリへのパスを指定します。 このオペレーティング システムは Configuration Manager によるキャプチャをサポートするオペレーティング システムとして検証済みです。|  



###  <a name="BKMK_CaptureUserState"></a> ユーザー状態のキャプチャ   
 詳細については、「[ユーザー状態のキャプチャ](task-sequence-steps.md#BKMK_CaptureUserState)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (入力)|ユーザー状態を保存するフォルダーの UNC またはローカル パス名。 既定の設定はありません。|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (入力)|タスク シーケンスでユーザー状態をキャプチャするために使用する、追加のユーザー状態移行ツール (USMT) コマンド ライン オプション。 ステップでは、タスク シーケンス エディターでこれらの設定が公開されません。 タスク シーケンスで自動生成された USMT コマンド ラインに付加される、文字列としてこれらのオプションを指定します。<br /><br />タスク シーケンスを実行するまで、このタスク シーケンス変数で指定される USMT オプションの正確性は検証されません。|  
|OSDMigrateMode<br /><br /> (入力)|USMT によってキャプチャされたファイルをカスタマイズできます。 この変数が **Simple** に設定されている場合、タスク シーケンスでは標準の USMT 構成ファイルのみが使用されます。 この変数が **Advanced** に設定されている場合、タスク シーケンス変数 OSDMigrateConfigFiles により、USMT が使用する構成ファイルが指定されます。<br /><br /> 有効な値:<br /><br /> **Simple**<br /><br /> **Advanced**|  
|OSDMigrateConfigFiles<br /><br /> (入力)|ユーザー プロファイルのキャプチャの制御に使用される構成ファイルを指定します。 この変数は、OSDMigrateMode が Advanced に設定されている場合にのみ使用されます。 カスタマイズされたユーザー プロファイル移行を実行するためには、このカンマ区切りの一覧の値を設定します。<br /><br /> 例: miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (入力)|USMT で一部のファイルをキャプチャできない場合、この変数を使用することで、ユーザー状態のキャプチャを続行できます。<br /><br /> 有効な値:<br /><br /> **true** (既定)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (入力)|USMT の詳細ログ記録を有効にします。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false** (既定)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (入力)|暗号化ファイルをキャプチャするかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false** (既定)|  
|_OSDMigrateUsmtPackageID<br /><br /> (入力)|USMT ファイルを含む Configuration Manager パッケージのパッケージ ID を指定します。 この変数は必須です。|  



###  <a name="BKMK_CaptureWindowsSettings"></a> Windows 設定のキャプチャ   
 詳細については、「[Windows 設定のキャプチャ](task-sequence-steps.md#BKMK_CaptureWindowsSettings)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (入力)|コンピューター名を移行するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **true** (既定)<br /><br /> **false**<br /><br /> この値が **true** の場合、OSDComputerName 変数がコンピューターの NetBIOS 名に設定されます。|  
|OSDComputerName<br /><br /> (出力)|コンピューターの NetBIOS 名に設定します。 この値は、OSDMigrateComputerName 変数が **true** に設定されている場合にのみ設定されます。|  
|OSDMigrateRegistrationInfo<br /><br /> (入力)|ステップでユーザーと組織の情報を移行するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **true** (既定)<br /><br /> **false**<br /><br /> この値が **true** の場合、OSDRegisteredOrgName 変数がコンピューターの登録組織名に設定されます。|  
|OSDRegisteredOrgName<br /><br /> (出力)|コンピューターの登録組織名に設定します。 この値は、OSDMigrateRegistrationInfo 変数が **true** に設定されている場合にのみ設定されます。|  
|OSDMigrateTimeZone<br /><br /> (入力)|コンピューターのタイム ゾーンを移行するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **true** (既定)<br /><br /> **false**<br /><br /> この値が **true** の場合、変数 OSDTimeZone がコンピューターのタイム ゾーンに設定されます。|  
|OSDTimeZone<br /><br /> (出力)|コンピューターのタイム ゾーンに設定します。 この値は、OSDMigrateTimeZone 変数が **true** に設定されている場合にのみ設定されます。|  



###  <a name="BKMK_ConnecttoNetworkFolder"></a> ネットワーク フォルダーへの接続   
 詳細については、「[ネットワーク フォルダーへの接続](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (入力)|ネットワーク共有に接続するために使用する管理者アカウントを指定します。|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (入力)|接続先のネットワーク ドライブ文字を指定します。 この値は省略可能です。指定しない場合、ネットワーク接続はドライブ文字にマップされません。 値を指定する場合は、D: から Z: の範囲で指定する必要があります。 また、X: は使用しないでください。X: は、Windows PE 段階で Windows PE によって使用されるドライブ文字です。<br /><br /> 次に例を示します。<br /><br /> **D:**<br /><br /> **E:**|  
|SMSConnectNetworkFolderPassword<br /><br /> (入力)|ネットワーク共有に接続するために使用するネットワーク パスワードを指定します。|  
|SMSConnectNetworkFolderPath<br /><br /> (入力)|接続に使用するネットワーク パスを指定します。<br /><br /> 例:<br /><br /> **\\\servername\sharename**|  



###  <a name="BKMK_EnableBitLocker"></a> BitLocker の有効化   
 詳細については、「[BitLocker の有効化](task-sequence-steps.md#BKMK_EnableBitLocker)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (入力)|**[BitLocker の有効化]** タスク シーケンス アクションは、ランダムな回復パスワードを生成する代わりに、指定された値を回復パスワードとして使用します。 有効な数値の BitLocker 回復パスワードを指定する必要があります。|  
|OSDBitLockerStartupKey<br /><br /> (入力)|**[BitLocker の有効化]** ステップでは、キー管理オプション **[USB 上のスタートアップ キーのみ]** のランダムなスタートアップ キーを生成する代わりに、信頼されたプラットフォーム モジュール (TPM) をスタートアップ キーとして使用します。 有効な 256 ビット の Base64 エンコードされた BitLocker スタートアップ キーを指定する必要があります。|  



###  <a name="BKMK_FormatPartitionDisk"></a> ディスクのフォーマットとパーティション作成   
 詳細については、「[ディスクのフォーマットとパーティション作成](task-sequence-steps.md#BKMK_FormatandPartitionDisk)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (入力)|パーティションを作成する物理ディスク番号を指定します。|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (入力)|特定の種類の BIOS との互換性を保つため、ハード ディスクのパーティションを作成するときに、この変数でキャッシュ整合の最適化を無効にするかどうかを指定します。 これは、Windows XP または Windows Server 2003 オペレーティング システムの展開時に必要です。 詳細については、Microsoft サポート技術情報の [記事 931760](http://go.microsoft.com/fwlink/?LinkId=134081) および [記事 931761](http://go.microsoft.com/fwlink/?LinkId=134082) を参照してください。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false** (既定)| 
|OSDGPTBootDisk<br /><br /> (入力)|GPT ハード ディスク上で EFI パーティションを作成するかどうかを指定します。 EFI ベースのコンピューターでは、スタートアップ ディスクとしてこのパーティションを使用します。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false** (既定)|  
|OSDPartitions<br /><br /> (入力)|パーティション設定の配列を指定します。タスク シーケンス環境で配列変数にアクセスする方法については、SDK のトピックを参照してください。<br /><br /> このタスク シーケンス変数は、配列変数です。 配列内の各要素は、ハード ディスクの単一パーティションの設定を表します。 各パーティションに定義された設定にアクセスするには、配列変数名にゼロから始まるディスク パーティション番号とプロパティ名を結合します。<br /><br /> たとえば、次の変数名は、このステップでハード ディスクに作成される最初のパーティションに対して、プロパティを定義するときに使用します。<br /><br /> - **OSDPartitions0Type**: パーティションの種類を指定します。 このプロパティは必須です。 有効な値は、**Primary**、**Extended**、**Logical**、**Hidden** です。<br />-   **OSDPartitions0FileSystem**: パーティションをフォーマットするときに使用するファイル システムの種類を指定します。 このプロパティは省略可能です。 ファイル システムを指定しない場合、ステップではパーティションはフォーマットされません。 有効な値は **FAT32** と **NTFS** です。<br />-   **OSDPartitions0Bootable**: パーティションが起動可能かどうかを指定します。 このプロパティは必須です。 MBR ディスクでこの値が **TRUE** に設定されている場合、ステップではこのパーティションがアクティブとしてマークされます。<br />-   **OSDPartitions0QuickFormat**: 使用されるフォーマットの種類を指定します。 このプロパティは必須です。 この値が **TRUE** に設定されている場合、ステップではクイック フォーマットが実行されます。 それ以外の場合、ステップではフル フォーマットが実行されます。<br />-   **OSDPartitions0VolumeName**: フォーマット時にボリュームに割り当てられる名前を指定します。 このプロパティは省略可能です。<br />-   **OSDPartitions0Size**: パーティションのサイズを指定します。 単位は **OSDPartitions0SizeUnits** 変数で指定します。 このプロパティは省略可能です。 このプロパティを指定しない場合、残りの空き領域すべてを使用してパーティションが作成されます。<br />-   **OSDPartitions0SizeUnits**: ステップではこれらの単位を使用して、**OSDPartitions0Size** 変数が解釈されます。 このプロパティは省略可能です。 有効な値は、**MB** (既定)、**GB**、**Percent** です。<br />-   **OSDPartitions0VolumeLetterVariable**: このステップでパーティションを作成するときに、Windows PE で次に利用可能なドライブ文字が常に使用されます。 別のタスク シーケンス変数の名前を指定する場合は、この省略可能なプロパティを使用します。 ステップではこの変数を使用して、今後の参照用に新しいドライブ文字を保存します。<br /><br />このタスク シーケンス アクションで複数のパーティションを定義する場合、2 番目のパーティションのプロパティは変数名でそのインデックスを使用して定義されます。 たとえば、**OSDPartitions1Type**、**OSDPartitions1FileSystem**、**OSDPartitions1Bootable**、**OSDPartitions1QuickFormat**、**OSDPartitions1VolumeName** のようになります。|  
|OSDPartitionStyle<br /><br /> (入力)|ディスクをパーティション分割するときに使用するパーティション スタイルを指定します。 **MBR** はマスター ブート レコードのパーティション スタイルを示し、**GPT** は GUID パーティション テーブル スタイルを示します。<br /><br /> 有効な値:<br /><br /> **GPT**<br /><br /> **MBR**|  



###  <a name="BKMK_InstallApplication"></a> アプリケーションのインストール   
 詳細については、「[アプリケーションのインストール](task-sequence-steps.md#BKMK_InstallApplication)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名<br /><br /> (入力)|説明|  
|----------------------------------------|-----------------|  
| TSErrorOnWarning |タスク シーケンス エンジンがこのステップで検出された警告をエラーと見なすかどうかを指定します。 1 つ以上のアプリケーション、または必要な依存関係がインストールされていない場合、要件を満たしていないため、タスク シーケンスでは _TSAppInstallStatus 変数を**警告**に設定します。 この変数を **True** に設定したときに、タスク シーケンスでは _TSAppInstallStatus が警告に設定されている場合、結果はエラーとなります。 値 **False** が既定の動作です。| 
|SMSTSMPListRequestTimeoutEnabled|クライアントがイントラネット上にない場合に、繰り返しの MPList 要求を有効にしてクライアントを更新するには、この変数を使用します。 <br />既定では、この変数は **True** に設定されます。 クライアントがインターネット上にある場合は、不必要な遅延を回避するためにこの変数を **False** に設定することができます。 この変数の値は、[アプリケーションのインストール] および [ソフトウェア更新プログラムのインストール] タスク シーケンス ステップにのみ適用されます。|  
|SMSTSMPListRequestTimeout|タスク シーケンスでロケーション サービスから管理ポイント一覧を取得できなかった場合に、アプリケーションのインストールを再試行するまでの待ち時間をミリ秒単位で指定します。 既定では、タスク シーケンスは **60000** ミリ秒 (60 秒) 待機してからステップを再試行します。再試行は 3 回までです。|  



###  <a name="BKMK_InstallSoftwareUpdates"></a> ソフトウェア更新プログラムのインストール   
詳細については、「[ソフトウェア更新プログラムのインストール](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名<br /><br /> (入力)|説明|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (入力)|すべての更新プログラムをインストールするのか、必須の更新プログラムのみインストールするのかを指定します。<br /><br /> 有効な値:<br /><br /> **すべて**<br /><br /> **必須**|  
|SMSTSSoftwareUpdateScanTimeout| このステップにおけるソフトウェア更新プログラムのスキャンのタイムアウトを制御します。 たとえば、スキャン中に多数の更新プログラムが予想される場合は、この値を増やします。 既定値は **1800** 秒 (30 分) です。 変数値は秒単位で設定されます。 |
|SMSTSWaitForSecondReboot|ソフトウェア更新プログラムのインストールで 2 回再起動が必要な場合に、この省略可能なタスク シーケンス変数でクライアントの動作を制御します。 この変数は、ソフトウェア更新プログラムのインストールからの 2 つ目の再起動によってタスク シーケンスが失敗するのを防ぐために、このステップの前に設定します。<br /><br /> コンピューターの再起動中にこのステップでタスク シーケンスが一時停止する時間を指定する場合は、SMSTSWaitForSecondReboot の値を秒単位で設定します。 2 つ目の再起動がある場合には十分な時間を取るようにしてください。 <br />たとえば、SMSTSWaitForSecondReboot を 600 に設定した場合、再起動してから追加のステップが実行されるまで、タスク シーケンスが 10 分間一時停止します。 この変数は、何百ものソフトウェア更新プログラムが 1 つのソフトウェア更新プログラムのインストール タスク シーケンス ステップでインストールされる場合に便利です。| 
|SMSTSMPListRequestTimeoutEnabled|クライアントがイントラネット上にない場合に、繰り返しの MPList 要求を有効にしてクライアントを更新するには、この変数を使用します。 <br />既定では、この変数は **True** に設定されます。 クライアントがインターネット上にある場合は、不必要な遅延を回避するためにこの変数を **False** に設定することができます。 この変数の値は、[アプリケーションのインストール] および [ソフトウェア更新プログラムのインストール] タスク シーケンス ステップにのみ適用されます。|  
|SMSTSMPListRequestTimeout|タスク シーケンスでロケーション サービスから管理ポイント一覧を取得できなかった場合に、ソフトウェア更新プログラムのインストールを再試行するまでの待ち時間をミリ秒単位で指定します。 既定では、タスク シーケンスは **60000** ミリ秒 (60 秒) 待機してからステップを再試行します。再試行は 3 回までです。|  



###  <a name="BKMK_JoinDomainWorkgroup"></a> ドメインまたはワークグループへの参加   
 詳細については、「[ドメインまたはワークグループへの参加](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (入力)|対象コンピューターを Active Directory ドメインに参加させるために使用するアカウントを指定します。 この変数はドメインに参加するときに必要になります。|  
|OSDJoinDomainName<br /><br /> (入力)|対象コンピューターを参加させる Active Directory ドメインの名前を指定します。 ドメイン名の長さは 1 文字から 255 文字の範囲である必要があります。|  
|OSDJoinDomainOUName<br /><br /> (入力)|対象コンピューターを参加させる組織単位 (OU) の RFC 1779 形式の名前を指定します。 指定する場合の値は、完全なパスを含む必要があります。 OU 名の長さは 0 文字から 32,767 文字の範囲である必要があります。 **OSDJoinType** 変数が **1** (ワークグループに参加) に設定されている場合、この値は設定されません。<br /><br /> 例:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (入力)|対象コンピューターが Active Directory ドメインに参加するために使用するネットワーク パスワードを指定します。 タスク シーケンス環境にこの変数が含まれていない場合、Windows セットアップでは空白のパスワードが試行されます。 **OSDJoinType** 変数が **0** (ドメインに参加) に設定されている場合は、この値が必要になります。|  
|OSDJoinSkipReboot<br /><br /> (入力)|対象コンピューターがドメインまたはワークグループに参加した後、再起動をするかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false**|  
|OSDJoinType<br /><br /> (入力)|対象コンピューターを Windows ドメインに参加させるか、ワークグループに参加させるかを指定します。 対象コンピューターを Windows ドメインに参加させる場合は、**0** を指定します。 対象コンピューターをワークグループに参加させる場合は、**1** を指定します。<br /><br /> 有効な値:<br /><br /> **0**<br /><br /> **1**|  
|OSDJoinWorkgroupName<br /><br /> (入力)|対象コンピューターを参加させるワークグループの名前を指定します。 ワークグループ名の長さは 1 ～ 32 文字の範囲であることが必要です。<br /><br /> 例:<br /><br /> **会計**|  



###  <a name="BKMK_PrepareWindowsCapture"></a> Windows のキャプチャの準備   
 詳細については、「[Windows のキャプチャの準備](task-sequence-steps.md#BKMK_PrepareWindowsforCapture)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (入力)|Sysprep が大容量記憶装置のドライバー一覧を構築するかどうかを指定します。 この設定は、Windows XP および Windows Server 2003 にのみ適用されます。 この変数により、sysprep.inf の [SysprepMassStorage] セクションに、キャプチャするイメージでサポートされるすべての大容量記憶装置のドライバーに関する情報が入力されます。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false** (既定)|  
|OSDKeepActivation<br /><br /> (入力)|sysprep がプロダクト アクティベーション フラグをリセットするかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false** (既定)|  
|OSDTargetSystemRoot<br /><br /> (出力)|参照コンピューター上にインストールされたオペレーティング システムの Windows ディレクトリへのパスを指定します。 このオペレーティング システムは Configuration Manager によるキャプチャをサポートするオペレーティング システムとして検証済みです。|  



###  <a name="BKMK_ReleaseStateStore"></a> 状態ストアのリリース   
 詳細については、「[状態ストアのリリース](task-sequence-steps.md#BKMK_ReleaseStateStore)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (入力)|ユーザー状態の復元元となる場所への UNC またはローカル パス名。 この値は、**ユーザー状態のキャプチャ** タスク シーケンス アクションと**ユーザー状態の復元**タスク シーケンス アクションの両方で使用されます。|  



###  <a name="BKMK_RequestState"></a> 状態ストアの要求   
  詳細については、「[状態ストアのリリース](task-sequence-steps.md#BKMK_ReleaseStateStore)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (入力)|コンピューター アカウントが状態移行ポイントに接続できない場合に、タスク シーケンスでネットワーク アクセス アカウント (NAA) を使用するようにフォールバックするかどうかをこの変数で指定します。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false** (既定)|  
|OSDStateSMPRetryCount<br /><br /> (入力)|タスク シーケンス ステップが状態移行ポイントの検索を試行する回数を指定します。この回数を超えるとこの手順は失敗します。 回数は 0 ～ 600 の範囲で指定する必要があります。|  
|OSDStateSMPRetryTime<br /><br /> (入力)|タスク シーケンス ステップが再試行間に待機する秒数を指定します。 最大秒数は 30 文字です。|  
|OSDStateStorePath<br /><br /> (出力)|ユーザー状態が格納される状態移行ポイント上にあるフォルダーへの UNC パス。|  



###  <a name="BKMK_RestartComputer"></a> コンピューターの再起動   
 詳細については、「[コンピューターの再起動](task-sequence-steps.md#BKMK_RestartComputer)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (入力)|対象コンピューターの再起動前にユーザーに表示されるメッセージを指定します。 この変数を設定しなかった場合、既定のメッセージ テキストが表示されます。 メッセージは、512 文字以内で指定する必要があります。<br /><br /> 例:<br /><br /> **コンピューターの再起動前に、作業内容を保存します。**|  
|SMSRebootTimeout<br /><br /> (入力)|コンピューターが再起動される前にユーザーに警告を表示する秒数を指定します。 0 秒を指定すると、再起動されるというメッセージは表示されません。<br /><br /> 次に例を示します。<br /><br /> **0** (既定)<br /><br />  **60**|  



###  <a name="BKMK_RestoreUserState"></a> ユーザー状態の復元   
  詳細については、「[ユーザー状態の復元](task-sequence-steps.md#BKMK_RestoreUserState)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (入力)|ユーザー状態の復元元となるフォルダーの UNC またはローカル パス名。|  
|OSDMigrateContinueOnRestore<br /><br /> (入力)|USMT で一部のファイルを復元できない場合でも、プロセスを続行します。<br /><br /> 有効な値:<br /><br /> **true** (既定)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (入力)|USMT ツールの詳細ログ記録を有効にします。 この値はアクションに必要です。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false** (既定)|  
|OSDMigrateLocalAccounts<br /><br /> (入力)|ローカル コンピューター アカウントを復元するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **true**<br /><br /> **false** (既定)|  
|OSDMigrateLocalAccountPassword<br /><br /> (入力)|**OSDMigrateLocalAccounts** 変数が "true" の場合、この変数には移行されたすべてのローカル アカウントに割り当てるパスワードが含まれる必要があります。 USMT は、移行されたすべてのローカル アカウントに同じパスワードを割り当てます。 このパスワードは一時的なものと考え、後で他の方法で変更してください。|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (入力)|ユーザー状態の復元時に使用する、追加のユーザー状態移行ツール (USMT) コマンド ライン オプションを指定します。 追加のオプションは、自動生成された USMT コマンド ラインに付加される文字列の形式で指定されます。 タスク シーケンスを実行するまで、このタスク シーケンス変数で指定される USMT オプションの正確性は検証されません。|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (入力)|USMT ファイルを含む Configuration Manager パッケージのパッケージ ID を指定します。 この変数は必須です。|  



###  <a name="BKMK_RunCommand"></a> コマンド ラインの実行   
  詳細については、「[コマンド ラインの実行](task-sequence-steps.md#BKMK_RunCommandLine)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (入力)|64 ビット オペレーティング システムの場合、既定では、タスク シーケンスで WOW64 ファイル システム リダイレクターを使用して、コマンド ラインでプログラムを見つけて実行します。 この動作では、コマンドを使用して、32 ビット バージョンのオペレーティング システムのプログラムや DLL を見つけることができます。 この変数を **true** に設定すると、WOW64 ファイル システム リダイレクターの使用が無効になります。 ネイティブの 64 ビット バージョンのオペレーティング システムのプログラムと DLL は、コマンドを使用して見つけることができます。 32 ビット オペレーティング システム上で実行している場合は、この変数は影響を及ぼしません。|  
|WorkingDirectory<br /><br /> (入力)|コマンド ラインのアクションの開始ディレクトリを指定します。 ディレクトリ名は、255 文字以内で指定する必要があります。<br /><br /> 次に例を示します。<br /><br /> -   **C:\\**<br />-   **%SystemRoot%**|  
|SMSTSRunCommandLineUserName<br /><br /> (入力)|コマンド ラインを実行するアカウントを指定します。 この値は、ユーザー名 または ドメイン\ユーザー名 という形式の文字列になります。|  
|SMSTSRunCommandLinePassword<br /><br /> (入力)|SMSTSRunCommandLineUserName 変数で指定されたアカウントのパスワードを指定します。|  



### <a name="set-dynamic-variables"></a>動的変数の設定  
詳細については、「[動的変数の設定](task-sequence-steps.md#BKMK_SetDynamicVariables)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名<br /><br /> (入力)|説明|  
|----------------------------------------|-----------------|  
|_SMSTSMake|コンピューターのメーカーを指定します。|  
|_SMSTSModel|コンピューターのモデルを指定します。|  
|_SMSTSMacAddresses|コンピューターで使用される MAC アドレスを指定します。|  
|_SMSTSIPAddresses|コンピューターで使用される IP アドレスを指定します。|  
|_SMSTSSerialNumber|コンピューターのシリアル番号を指定します。|  
|_SMSTSAssetTag|コンピューターの資産タグを指定します。|  
|_SMSTSUUID|コンピューターの UUID を指定します。|  
|_SMSTSDefaultGateways|コンピューターで使用される既定のゲートウェイを指定します。|  



###  <a name="BKMK_SetupWindows"></a> Windows と ConfigMgr のセットアップ   
  詳細については、「[Setup Windows and ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)」(Windows と ConfigMgr のセットアップ) を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名<br /><br /> (入力)|説明|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (入力)|Configuration Manager クライアントをインストールするときに使用するクライアント インストール プロパティを指定します。|  



### <a name="upgrade-operating-system"></a>オペレーティング システムのアップグレード  
 詳細については、「[オペレーティング システムのアップグレード](task-sequence-steps.md#BKMK_UpgradeOS)」を参照してください。  

#### <a name="details"></a>詳細  

|アクション変数名<br /><br /> (入力)|説明|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (入力)|Windows 10 へのアップグレードの際に Windows セットアップに追加されるコマンド ライン オプションを指定します。 タスク シーケンスではコマンド ライン オプションは検証されません。<br /><br /> 詳細については、「 [Windows セットアップ コマンド ライン オプション](/windows-hardware/manufacture/desktop/windows-setup-command-line-options)」を参照してください。|  
