---
title: "特定のユーザー (混在 MDM 機関) の MDM 機関を変更する"
titleSuffix: Configuration Manager
description: "一部のユーザーに対し、MDM 機関をハイブリッド MDM から Intune スタンドアロンに変更する方法について説明します。"
keywords: 
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 643b33810c2862e2d1c602bfe941c36605ad2631
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2017
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>特定のユーザー (混在 MDM 機関) の MDM 機関を変更する 

*適用対象: System Center Configuration Manager (Current Branch)*    

一部のユーザーを Intune で管理し、それ以外のユーザーをハイブリッド MDM (Intune と Configuration Manager の統合) で管理するように選択することで、同じテナントで混在 MDM 機関を構成できます。 この記事では、Intune スタンドアロンへのユーザーの移動を開始する方法について説明します。次の手順を完了していることを前提としています。
- データ インポート ツールを使用して [Configuration Manager オブジェクトを Intune にインポート](migrate-import-data.md)した (省略可能)。
- ユーザーとユーザーのデバイスを移行した後も管理が継続されていることを確認するには、「[Prepared Intune for user migration (Intune でのユーザーの移行の準備)](migrate-prepare-intune.md)」をご覧ください。

> [!Note]    
> テナントの完全なリセット (すべてのポリシー、アプリ、およびデバイスの登録を削除) を実行する場合は、サポートにお問い合わせください。

移行されたユーザーとそのデバイスは Intune で管理され、その他のデバイスは引き続き Configuration Manager で管理されます。 最初に小規模なテスト ユーザー グループを使用して、すべてが適切に機能していることを確認します。 次に、テナントレベル MDM 機関を Configuration Manager から Intune スタンドアロンに切り替える準備ができるまで、追加のユーザー グループを段階的に移行します。 

## <a name="things-to-know-before-you-migrate-users"></a>ユーザーを移行する前に知っておくべきこと
- 段階的な移行中に、Configuration Manager の既存の MDM ポリシーまたはアプリは、ハイブリッド MDM デバイスに引き続き適用されます。
- Intune サブスクリプションに関連付けられているコレクション内のユーザーのデバイスをハイブリッド MDM に登録できます。 コレクション内にないユーザーに関連付けられているすべてのデバイスは、そのユーザーが Intune/EMS ライセンスを持っている限り、Intune で管理されます。 
- ユーザーを Intune に移行すると、約 15 分後にそのユーザーとデバイスが Azure Portal の Intune に表示されます。  
- ユーザーを Intune スタンドアロンに移行するときに、Intune スタンドアロンとハイブリッド MDM デバイスの両方の Configuration Manager から次の設定を引き続き管理します。
    - [Apple Push Notification (APN) サービス証明書](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)
    - [Device Enrollment Program](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)
    - 登録プロファイル
    - [Volume Purchase Program (VPP) ライセンス](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)
    - 企業 ID 
    - [コード署名証明書](/sccm/mdm/deploy-use/enroll-hybrid-windows)
    - [デバイス カテゴリ](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)
    - [登録マネージャー](/sccm/mdm/plan-design/device-enrollment-methods)
    - Terms and conditions
    - Windows SLK
    - ポータル サイトのブランド化    
      
  > [!Important]    
  > Configuration Manager コンソールを使用してテナント レベルのポリシーの編集を続行します。 [テナントレベルの MDM 機関を Intune に変更](change-mdm-authority.md)したら、これらのポリシーを Azure の Intune で管理します。 
- Configuration Manager でデバイス登録マネージャーとして追加されているユーザー アカウントは、いずれも移行しないことをお勧めします。 これらのユーザー アカウントは、後でテナントレベル MDM 機関を Intune に変更するときに正しく移行されます。 テナント レベル MDM 機関の変更前にデバイス登録マネージャーのユーザー アカウントを移行する場合、Azure の Intune でデバイス登録マネージャーとしてユーザーを手動で追加する必要があります。 ただし、デバイス登録マネージャーを使用して登録されたデバイスは正常に移行されません。 これらのデバイスを移行するには、サポートに連絡する必要があります。 詳細については、「[デバイス登録マネージャーの追加](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager)」を参照してください。
- デバイス登録マネージャーを使用して登録されたデバイスと、[ユーザー アフィニティ](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices)のないデバイスは、新しい MDM 機関に自動的には移行されません。 これらのMDM デバイスの管理機関を切り替えるには、「[ユーザー アフィニティなしのデバイスの移行](#migrate-devices-without-user-affinity)」をご覧ください。

## <a name="migrate-users-to-intune"></a>Intune にユーザーを移行する
Intune の構成が期待どおりに機能していることをテストするため、最初にごく少数のユーザーとそのデバイスを移行します。 そして期待どおりに機能していることを確認したら、より多くのユーザーとデバイスを含むより多くの AAD グループの移行を開始できます。

## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Intune スタンドアロンにテスト ユーザー グループを移行する
Intune サブスクリプションに関連付けられているコレクション内のユーザーのデバイスをハイブリッド MDM に登録できます。 コレクションからユーザーを削除するときに、このユーザーに Intune ライセンスが割り当てられている場合、このユーザーの登録済みデバイスは Intune スタンドアロンに移行されます。 移行を計画しているユーザーにまだライセンスが割り当てられていない場合は、「[ユーザー アカウントに Intune のライセンスを割り当てる](https://docs.microsoft.com/intune/licenses-assign)」を参照してください。 Intune サブスクリプションのコレクションで、メイン コレクションからユーザー コレクションを除外して、除外したコレクション内のユーザーを移行することができます。 

次の例では、ハイブリッド ユーザー コレクションに、すべてのユーザー コレクションのすべてのメンバーが含まれています。 これにより、任意のユーザーがデバイスをハイブリッド MDM に登録することができます。 Intune スタンドアロンにユーザーを移行するには、[コレクションを除外する] を選択して、移行するユーザーを含むコレクションを追加します。 追加のユーザーを移行する準備ができたら、これらのユーザーを含む別の除外されたコレクションを追加できます。 

![コレクションを除外する](../media/migrate-excludecollections.png)

> [!Note] 
> Intune サブスクリプションに **[すべてのユーザー]** を選択している場合、ルールを追加してコレクションを除外することはできません。 **[すべてのユーザー]** コレクションに基づいて新しいコレクションを作成し、そのコレクションに想定しているユーザーが含まれていることを確認し、新しいコレクションを使用するように Intune サブスクリプションを編集します。 新しいコレクションからユーザー コレクションを除外してユーザーを移行することができます。 

テスト ユーザー グループを Intune に移行するには、移行するユーザーを含むユーザー コレクションを作成し、そのユーザー コレクションを Intune サブスクリプションで使用されるコレクションから除外します。   

次の図に、ユーザーの移行のしくみの概要を示します。

 ![混合機関の概要](../media/migrate-mixedauthority.svg)

1. ユーザーが Intune/EMS ライセンスを持っていることを確認します。 
2. Intune サブスクリプションのコレクションから除外するコレクションを作成します。 この例では、**すべてのハイブリッド ユーザー** コレクションに**移行パイロット** コレクション内のユーザーを除外するルールが含まれています。 **User1** は**移行パイロット** コレクションのメンバーで、**すべてのハイブリッド ユーザー** コレクションから除外されます。 
3. **User1** のデバイスが、Azure Portal で Intune から管理されるようになりました。 
4. 他のデバイスはすべて、引き続き Configuration Manager コンソールから管理されます。 

## <a name="verify-intune-standalone-functionality"></a>Intune スタンドアロンの機能を確認する
少数のユーザーを移行した後、これらのユーザーのデバイスが Intune に一覧表示されていることを確認します。 **[デバイス]** ブレードに移動して、**[すべてのデバイス]** を選択します。 

次に、ポリシー、プロファイル、アプリなどがユーザーのデバイスで問題なく機能していることを確認します。

## <a name="migrate-additional-users"></a>他のユーザーを移行する
Intune スタンドアロンが期待どおりに機能していることを確認したら、他のユーザーの移行を開始できます。 一連のテスト ユーザーでコレクションを作成したのと同じく、移行するユーザーが含まれるコレクションを作成し、これらのコレクションを Intune サブスクリプションに関連付けられているコレクションから除外します。 詳細については、「[Collection associated with your Intune subscription](#collection-associated-with-your-intune-subscription)」 (Intune サブスクリプションに関連付けられたコレクション) を参照してください。

## <a name="migrate-devices-without-user-affinity"></a>ユーザー アフィニティなしのデバイスの移行
デバイス登録マネージャーを使用して登録されたデバイスと、[ユーザー アフィニティ](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices)のないデバイスは、新しい MDM 機関に自動的には移行されません。 次のようなシナリオで、*Switch-MdmDeviceAuthority* PowerShell コマンドレットを使用して、Intune と Configuration Manager 管理機関を切り替えることができます。 

-   シナリオ 1: *Switch-MdmDeviceAuthority* コマンドレットを使用して、選択したデバイスを移行し、それらを Azure で Intune を使って管理できることを検証します。 準備ができたら、[テナントのMDM 機関を Intune に変更](migrate-change-mdm-authority.md)して、デバイスの移行を完了することができます。 
-   シナリオ 2: テナントの MDM 機関を Intune に変更する準備ができている場合、次の操作を行ってユーザー アフィニティのないデバイスを移行できます。
    - [テナントの MDM 機関を Intune に変更](migrate-change-mdm-authority.md)する前に、コマンドレットを使用して、ユーザー アフィニティのないデバイスの MDM 機関を変更します。    
    - テナントの MDM 機関を Intune に変更した後で、サポートに連絡してユーザー アフィニティのないデバイスを切り替えてもらいます。

これらの MDM デバイスの管理機関を切り替えるには、*Switch-MdmDeviceAuthority* コマンドレットを使用して、Intune と Configuration Manager を切り替えることができます。 

### <a name="cmdlet-switch-mdmdeviceauthority"></a>コマンドレット *Switch-MdmDeviceAuthority*

#### <a name="synopsis"></a>概要
このコマンドレットは、ユーザー アフィニティのない MDM デバイス (たとえば、一括登録したデバイス) の管理機関を切り替えます。 このコマンドレットは指定したデバイスについて、コマンドレット実行時の管理機関に基づき、Intune と Configuration Manager を切り替えます。

### <a name="syntax"></a>構文
`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>パラメータ
``` powershell
-Credential <PSCredential>
Credential for Intune Tenant Admin or Service Admin account to use when switching device management authorities. The user is prompted for credentials if the parameter is not specified.

-DeviceIds <Guid[]>
The ids of the MDM devices that need to have their management authority switched. The device ids are unique identifiers for the devices displayed by the Configuration Manager console.

-Force [<SwitchParameter>]
Specify parameter to disable the Should Continue prompt.<br>
 
-LogFilePath <string>
Path to log file location.
 
-LoggingLevel <SourceLevels>
The log level used to determine the type of logs that need to be written to the log file.
 
The following are the possible values for LoggingLevel:

  - ActivityTracing
  - All
  - Critical
  - Error
  - Information
  - Off
  - Verbose
  - Warning
 
-Confirm [<SwitchParameter>]
Prompts you for confirmation before executing the command.
 
-WhatIf [<SwitchParameter>]
Describes what would happen if you executed the command without actually executing the command.
 
<CommonParameters>
This cmdlet supports the common parameters: Verbose, Debug,
ErrorAction, ErrorVariable, WarningAction, WarningVariable,
OutBuffer, PipelineVariable, and OutVariable. For more information, see
[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).
```

### <a name="example-1"></a>例 1

``` powershell
C:\PS>Switch-MdmDeviceAuthority -Credential $creds -DeviceIds $deviceIds
 
  DeviceId       : 62e6ea43-18f8-4278-bcd4-a4baed2c6d24
  Success        : True
  FailureReason  :
  NewAuthority   : Intune
  CompletionTime : 11/15/2017 8:00:11 PM
 
Description
 
-----------
 
Successfully switched the management authority of the device from Configuration Manager to Intune.
```
### <a name="remarks"></a>備考
``` powershell
To see the examples, type: "get-help Switch-MdmDeviceAuthority -examples".
For more information, type: "get-help Switch-MdmDeviceAuthority -detailed".
For technical information, type: "get-help Switch-MdmDeviceAuthority -full".
For online help, type: "get-help Switch-MdmDeviceAuthority -online".
```

## <a name="next-steps"></a>次のステップ
ユーザーを移行して、Intune の機能をテストしたら、Configuration Manager から Intune にご利用の Intune テナントの [MDM 機関を変更](migrate-change-mdm-authority.md)する準備ができているかどうかを検討します。 