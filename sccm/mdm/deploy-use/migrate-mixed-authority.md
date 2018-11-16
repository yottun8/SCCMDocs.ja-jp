---
title: MDM 機関を変更する
titleSuffix: Configuration Manager
description: ハイブリッド MDM から Intune スタンドアロンの特定のユーザー (混在 MDM 機関) の MDM 機関を変更する方法について説明します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 79cf4c2ec217a245bb5c4abbad40aad7188e0ac0
ms.sourcegitcommit: 3772ece83823714b2aae46ec20523cc094701760
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/15/2018
ms.locfileid: "51688467"
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>特定のユーザー (混在 MDM 機関) の MDM 機関を変更する 

*適用対象します。System Center Configuration Manager (Current Branch)*    

同じテナントで混在 MDM 機関を構成できます。 一部のユーザーをハイブリッド MDM. でおよびその他の Microsoft Intune の管理します。 この記事では、ユーザーを Intune スタンドアロンに移行を開始する方法について説明します。 これにより、次の手順を完了したことを前提としています。  

- データ インポート ツールを使用して [Configuration Manager オブジェクトを Intune にインポート](migrate-import-data.md)した (省略可能)。  

- ユーザーとユーザーのデバイスを移行した後も管理が継続されていることを確認するには、「[Intune でのユーザーの移行を準備する](migrate-prepare-intune.md)」をご覧ください。  

> [!Note]    
> テナントの完全なリセットは、すべてのポリシー、アプリ、およびデバイスの登録を削除します。 このプロセスを実行する場合は、サポートにお問い合わせください。  

移行されたユーザーと Intune でデバイスを管理します。 Configuration Manager での他のデバイスの管理を継続します。 すべて、正しく動作することを確認するには、ユーザーの小規模なテスト グループを起動します。 他のユーザー グループを段階的に移行します。 準備ができたら、Intune スタンドアロンに Configuration Manager からテナント レベル MDM 機関を切り替えます。 

> [!Important]  
> 2018 年 8 月 13 日の時点では、ハイブリッド モバイル デバイス管理は[非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)です。 詳細については、[ハイブリッド MDM の概要](/sccm/mdm/understand/hybrid-mobile-device-management)に関するページを参照してください。<!--Intune feature 2683117-->  



## <a name="things-to-know-before-you-migrate-users"></a>ユーザーを移行する前に知っておくべきこと

- 段階的な移行中に、Configuration Manager の既存の MDM ポリシーまたはアプリは、ハイブリッド MDM デバイスに引き続き適用されます。  

- Intune サブスクリプションに関連付けられているコレクション内のユーザーのデバイスをハイブリッド MDM に登録できます。 コレクション内にないユーザーに関連付けられているすべてのデバイスは、そのユーザーが Intune/EMS ライセンスを持っている限り、Intune で管理されます。   

    > [!Note]  
    > ユーザーは、Configuration Manager コンソールでブロックされている場合でも、Intune スタンドアロンに登録できます。 ユーザーを登録から完全にブロックするには、Intune に望ましくないユーザーにはライセンスを与えないようにします。 ライセンスがなくては登録できません。<!--SCCMDocs issue 738-->  

- ユーザーを Intune に移行すると、約 15 分後にそのユーザーとデバイスが Azure Portal の Intune に表示されます。   

- ユーザーを Intune スタンドアロンに移行するときに、Intune スタンドアロンとハイブリッド MDM デバイスの両方の Configuration Manager から次の設定を引き続き管理します。  

    - [Apple Push Notification (APN) サービス証明書](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)  

    - [Device Enrollment Program](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)  

        > [!Note]  
        > Configuration Manager から削除したりする、DEP トークンを再作成する必要はありません。 Intune に Configuration Manager からテナントの MDM 機関を変更した後、Intune の 24 時間に自動的に移行されます。 この変更は、移行の最後の手順です。 (24 時間以内に DEP トークンを移行しない場合は、Microsoft サポートに問い合わせてください。)  

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
  > Configuration Manager コンソールを使用してテナント レベルのポリシーの編集を続行します。 したら[、テナント レベル MDM 機関を変更](/sccm/mdm/deploy-use/change-mdm-authority)を Intune に Configuration Manager では自動的に管理されたテナント レベルのポリシーは Azure での Intune に移行します。 このようなポリシーの例は、Apple Push Notification service (APNs) 証明書です。<!--SCCMDocs issue #971-->  

-   コード署名証明書を使用する場合、段階的にユーザーを移行することをお勧めします。 モバイル デバイスを移行すると、新しい証明書の証明書機関要求が行われます。 ユーザー (とそのデバイス) を移行する段階的なアプローチを使用して、同時の証明機関要求の数を制限します。  

- Configuration Manager でデバイス登録マネージャー (DEM) として追加されているユーザー アカウントは、いずれも移行しないでください。 これらのユーザー アカウントは、後でテナントレベル MDM 機関を Intune に変更するときに正しく移行されます。 テナント レベル MDM 機関の変更の前に、DEM ユーザーのアカウントに移行する場合は、Azure での Intune での DEM としてユーザーを手動で追加する必要があります。 ただし、DEM を使用して登録されたデバイスは正常に移行しません。 これらのデバイスを移行するには、サポートに連絡してください。 詳しくは、「[デバイス登録マネージャーの追加](https://docs.microsoft.com/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager)」をご覧ください。  

    > [!Note]  
    > 混在機関モードの間は、ConfigMgr クラウド コレクションからアカウントを削除することで、アカウントを Intune に移動しないでください。 これを行うと、ユーザーは標準ユーザーになり、15 より多くのデバイスを登録できません。 そのような場合は代わりに、テナントに対する MDM 機関を完全に切り替えた後、ユーザーとそのデバイスを移行します。<!--Intune bug 2174210-->  

- デバイスを登録する DEM となしのデバイスを使用して[ユーザー アフィニティ](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices)新しい MDM 機関に自動的に移行されません。 これらのMDM デバイスの管理機関を切り替えるには、「[ユーザー アフィニティなしのデバイスの移行](#migrate-devices-without-user-affinity)」をご覧ください。  



## <a name="migrate-users-to-intune"></a>Intune にユーザーを移行する

Intune の構成が期待どおりに機能していることをテストするため、最初にごく少数のユーザーとそのデバイスを移行します。 そして期待どおりに機能していることを確認したら、より多くのユーザーとデバイスを含むより多くの AAD グループの移行を開始できます。



## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Intune スタンドアロンにテスト ユーザー グループを移行する

Intune サブスクリプションに関連付けられているコレクション内のユーザーのデバイスをハイブリッド MDM に登録できます。 ユーザーに Intune ライセンスが割り当てられている場合、コレクションからユーザーを削除するときに、登録済みデバイスは Intune スタンドアロンに移行します。 移行を参照して計画していない割り当て済みであるライセンスをユーザーにする場合[ユーザー アカウントにライセンスを割り当てる Intune](https://docs.microsoft.com/intune/licenses-assign)します。 Intune サブスクリプションのコレクションで、メイン コレクションからユーザー コレクションを除外して、除外したコレクション内のユーザーを移行することができます。 

次の例では、ハイブリッド ユーザー コレクションに、すべてのユーザー コレクションのすべてのメンバーが含まれています。 この構成により、任意のユーザーがデバイスをハイブリッド MDM に登録することができます。 Intune スタンドアロンにユーザーを移行するには、[コレクションを除外する] を選択して、移行するユーザーを含むコレクションを追加します。 追加のユーザーを移行する準備ができたら、これらのユーザーを含む別の除外されたコレクションを追加します。 

![コレクションを除外する](../media/migrate-excludecollections.png)

> [!Note]  
> ある場合、**すべてのユーザー** Intune サブスクリプションの選択したコレクションでは、許可されていないコレクションを除外するルールを追加します。 基づく新しいコレクションを作成、**すべてのユーザー**コレクション。 必要なユーザーが、コレクションに含まれていることを確認します。 新しいコレクションを使用する Intune サブスクリプションを編集します。 新しいコレクションからユーザー コレクションを除外してユーザーを移行することができます。  

テスト ユーザー グループを Intune に移行するには、移行するユーザーを含むユーザー コレクションを作成します。 Intune サブスクリプションに使用されるコレクションからユーザーのコレクションを除外します。   

次の図に、ユーザーの移行のしくみの概要を示します。

 ![混合機関の概要](../media/migrate-mixedauthority.svg)

1. ユーザーが Intune/EMS ライセンスを持っていることを確認します。   

2. Intune サブスクリプションのコレクションから除外するコレクションを作成します。 この例では、**すべてのハイブリッド ユーザー** コレクションに**移行パイロット** コレクション内のユーザーを除外するルールが含まれています。 **User1** は**移行パイロット** コレクションのメンバーで、**すべてのハイブリッド ユーザー** コレクションから除外されます。  

3. **User1** のデバイスが、Azure Portal で Intune から管理されるようになりました。   

4. 他のデバイスはすべて、引き続き Configuration Manager コンソールから管理されます。  



## <a name="verify-intune-standalone-functionality"></a>Intune スタンドアロンの機能を確認する

少数のユーザーを移行した後、これらのユーザーのデバイスが Intune に一覧表示されていることを確認します。 **[デバイス]** に移動して、**[すべてのデバイス]** を選択します。 

次に、ポリシー、プロファイル、アプリがユーザーのデバイスで問題なく機能していることを確認します。



## <a name="migrate-additional-users"></a>他のユーザーを移行する

Intune スタンドアロンが期待どおりに機能していることを確認したら、他のユーザーの移行を開始します。 一連のテスト ユーザーのコレクションを作成したのと同様に、移行するユーザーを含むコレクションを作成します。 Intune サブスクリプションに関連付けられているコレクションから、これらのコレクションを除外します。 詳細については、「[Collection associated with your Intune subscription](#collection-associated-with-your-intune-subscription)」 (Intune サブスクリプションに関連付けられたコレクション) を参照してください。



## <a name="migrate-devices-without-user-affinity"></a>ユーザー アフィニティなしのデバイスの移行

デバイス登録マネージャーを使用して登録されたデバイスと、[ユーザー アフィニティ](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices)のないデバイスは、新しい MDM 機関に自動的には移行されません。 次のようなシナリオで、*Switch-MdmDeviceAuthority* PowerShell コマンドレットを使用して、Intune と Configuration Manager 管理機関を切り替えることができます。 

-   シナリオ 1 :使用して、 *Switch-mdmdeviceauthority*コマンドレットを選択したデバイスの移行し、検証を管理できる Azure で Intune を使用します。 準備ができたら、[テナントのMDM 機関を Intune に変更](migrate-change-mdm-authority.md)して、デバイスの移行を完了します。  

-   シナリオ 2 :テナントの MDM 機関を Intune に変更する準備ができたらは、ユーザー アフィニティなしのデバイスを移行する次の措置を取ります。  

    - [テナントの MDM 機関を Intune に変更](migrate-change-mdm-authority.md)する前に、コマンドレットを使用して、ユーザー アフィニティのないデバイスの MDM 機関を変更します。     

    - テナントの MDM 機関を Intune に変更した後で、サポートに連絡してユーザー アフィニティのないデバイスを切り替えてもらいます。  

これらの MDM デバイスの管理機関を切り替えるには、*Switch-MdmDeviceAuthority* コマンドレットを使用して、Intune と Configuration Manager を切り替えることができます。 

### <a name="cmdlet-switch-mdmdeviceauthority"></a>コマンドレット *Switch-MdmDeviceAuthority*

#### <a name="synopsis"></a>概要
このコマンドレットは、ユーザー アフィニティのない MDM デバイス (たとえば、一括登録したデバイス) の管理機関を切り替えます。 コマンドレットは、管理機関を Intune と Configuration Manager の間で切り替わります。 コマンドレットを実行するときに、管理機関に基づき、指定したデバイスに切り替わります。

### <a name="syntax"></a>構文
`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>パラメータ
#### `-Credential <PSCredential>`
デバイスの管理機関を切り替えるときに使用される Azure AD ユーザー アカウントの PowerShell 資格情報オブジェクト。 パラメーターが指定されていない場合は、資格情報を求められます。 このユーザー アカウントのディレクトリ ロールは、**グローバル管理者**、または **Intuen 管理者**の管理者ロールのある**制限付き管理者**である必要があります。

#### `-DeviceIds <Guid[]>`
管理機関を切り替える必要がある MDM デバイスの ID。 デバイス ID は、Configuration Manager コンソールで表示されるデバイスの一意識別子です。

#### `-Force [<SwitchParameter>]`
続行を求めるプロンプトを無効にするパラメーターを指定します。<br>
 
#### `-LogFilePath <string>`
ログ ファイルの場所へのパス。
 
#### `-LoggingLevel <SourceLevels>`
ログ ファイルに書き込む必要があるログの種類を決定するために使用されるログ レベル。
 
LoggingLevel に指定できる値は次のとおりです。

  - ActivityTracing
  - すべて
  - 重要
  - エラー
  - 情報
  - オフ
  - 詳細
  - 警告
 
#### `-Confirm [<SwitchParameter>]`
コマンドを実行する前に確認を求められます。
 
#### `-WhatIf [<SwitchParameter>]`
実際にコマンドを実行せず、コマンドを実行した場合の動作について説明します。
 
#### `<CommonParameters>`
このコマンドレットは、共通のパラメーターをサポートしています。Verbose、Debug、ErrorAction、ErrorVariable、WarningAction、WarningVariable、OutBuffer、PipelineVariable、および OutVariable します。 詳細については、「[about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216)」を参照してください。

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

### <a name="remarks"></a>「解説」
- 例を表示するには、「`get-help Switch-MdmDeviceAuthority -examples`」と入力します。  
- 詳細については、「`get-help Switch-MdmDeviceAuthority -detailed`」と入力します。  
- 技術情報については、「`get-help Switch-MdmDeviceAuthority -full`」と入力します。  
- オンライン ヘルプについては、「`get-help Switch-MdmDeviceAuthority -online`」と入力します。   



## <a name="next-steps"></a>次のステップ

ユーザーを移行して、Intune の機能をテストしたら、Configuration Manager から Intune にご利用の Intune テナントの [MDM 機関を変更](migrate-change-mdm-authority.md)する準備ができているかどうかを検討します。 
