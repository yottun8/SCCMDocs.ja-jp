---
title: "特定のユーザー (混在 MDM 機関) の MDM 機関を変更する"
titleSuffix: Configuration Manager
description: "一部のユーザーに対し、MDM 機関をハイブリッド MDM から Intune スタンドアロンに変更する方法について説明します。"
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/14/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 31d1d84c225d041f644669f0d3279e6bcd3f75ba
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2017
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>特定のユーザー (混在 MDM 機関) の MDM 機関を変更する 

*適用対象: System Center Configuration Manager (Current Branch)*    

一部のユーザーを Intune で管理し、それ以外のユーザーをハイブリッド MDM (Intune と Configuration Manager の統合) で管理するように選択することで、同じテナントで混在 MDM 機関を構成できます。 このトピックでは、Intune スタンドアロンへのユーザーの移動を開始する方法について説明します。次の手順を完了していることを前提としています。
- データ インポート ツールを使用して [Configuration Manager オブジェクトを Intune にインポート](migrate-import-data.md)した (省略可能)。
- ユーザーとユーザーのデバイスを移行した後も管理が継続されていることを確認するには、「[Prepared Intune for user migration (Intune でのユーザーの移行の準備)](migrate-prepare-intune.md)」をご覧ください。

> [!Note]    
> すべてのポリシー、アプリ、およびデバイスの登録を削除する、テナントの完全なリセットを実行する場合は、サポートにお問い合わせください。

移行されたユーザーとそのデバイスは Intune で管理され、その他のデバイスは引き続き Configuration Manager で管理されます。 最初に小規模なテスト ユーザー グループを使用して、すべてが期待どおりに機能していることを確認します。 次に、テナント レベル MDM 機関を Configuration Manager から Intune スタンドアロンに切り替える準備ができるまで、追加のユーザーのグループを段階的に移行します。 

## <a name="things-to-know-before-you-migrate-users"></a>ユーザーを移行する前に知っておくべきこと
- 段階的な移行中に、Configuration Manager の既存の MDM ポリシーまたはアプリは、ハイブリッド MDM デバイスに引き続き適用されます。
- ユーザーは、移行グループとして指定した AAD グループに追加されます。 移行グループ内のユーザーに関連付けられているすべてのデバイスは、Intune で管理されます。
- デバイスが AAD グループに追加された場合、関連付けられているユーザーがいなければ、これらのデバイスは無視されます。
- 移行のためにマーク付けされた AAD グループに属していないユーザーは、テナント レベル MDM 機関 (Configuration Manager) を自動的に継承します。
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
  > Configuration Manager コンソールを使用してテナント レベルのポリシーの編集を続行します。 [テナント レベルの MDM 機関を Intune に変更](change-mdm-authority.md)したら、これらのポリシーを Azure の Intune で管理します。 
- Configuration Manager でデバイス登録マネージャーとして追加されているユーザー アカウントは、いずれも移行しないことをお勧めします。 これらのユーザー アカウントは、後でテナント レベル MDM 機関を Intune に変更するときに正しく移行されます。 テナント レベル MDM 機関の変更前にデバイス登録マネージャーのユーザー アカウントを移行する場合、Azure の Intune でデバイス登録マネージャーとしてユーザーを手動で追加する必要があります。 ただし、デバイス登録マネージャーを使用して登録されたデバイスは正常に移行されません。 これらのデバイスを移行するには、サポートに連絡する必要があります。 詳細については、「[デバイス登録マネージャーの追加](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager)」を参照してください。
- デバイス登録マネージャーを使用して登録されたデバイスと、関連付けられているユーザーがないデバイスは、新しい MDM 機関には移行されません。 これらのデバイスについては、サポートに連絡して、これらの個別のデバイスのサポートを依頼する必要があります。 サポートに MDM 機関のリセットを実行させないようにしてください。実行すると、Intune 内のデータがワイプされます。 [MDM 機関の変更](migrate-change-mdm-authority.md)は、Configuration Manager コンソールから行う必要があります。

## <a name="migrate-users-to-intune"></a>Intune にユーザーを移行する
Intune の構成が期待どおりに機能していることをテストするため、最初にごく少数のユーザーとそのデバイスを移行します。 そして期待どおりに機能していることを確認したら、より多くのユーザーとデバイスを含むより多くの AAD グループの移行を開始できます。

## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Intune スタンドアロンにテスト ユーザー グループを移行する
Intune サブスクリプションに関連付けられているコレクション内のユーザーのデバイスをハイブリッド MDM に登録できます。 コレクションからユーザーを削除するときに、このユーザーに Intune ライセンスが割り当てられている場合、このユーザーの登録済みデバイスは Intune スタンドアロンに移行されます。 移行を計画しているユーザーにまだライセンスが割り当てられていない場合は、「[ユーザー アカウントに Intune のライセンスを割り当てる](https://docs.microsoft.com/intune/licenses-assign)」を参照してください。 Intune サブスクリプションのコレクションで、メイン コレクションからユーザー コレクションを除外して、除外したコレクション内のユーザーを移行することができます。 

次の例では、ハイブリッド ユーザー コレクションに、すべてのユーザー コレクションのすべてのメンバーが含まれています。 これにより、任意のユーザーがデバイスをハイブリッド MDM に登録することができます。 Intune スタンドアロンにユーザーを移行するには、[コレクションを除外する] を選択して、移行するユーザーを含むコレクションを追加します。 追加のユーザーを移行する準備ができたら、これらのユーザーを含む別の除外されたコレクションを追加できます。 

![コレクションを除外する](../media/migrate-excludecollections.png)

> [!Note] 
> Intune サブスクリプションに **[すべてのユーザー]** を選択している場合、ルールを追加してコレクションを除外することはできません。 **[すべてのユーザー]** コレクションに基づいて新しいコレクションを作成し、そのコレクションに想定しているユーザーが含まれていることを確認し、新しいコレクションを使用するように Intune サブスクリプションを編集します。 新しいコレクションからユーザー コレクションを除外してユーザーを移行することができます。 

テスト ユーザー グループを Intune に移行するには、移行するユーザーが含まれるユーザー コレクションを作成し、そのユーザー コレクションを Intune サブスクリプションで使用されるコレクションから除外します。   

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

## <a name="next-steps"></a>次のステップ
ユーザーを移行して、Intune の機能をテストしたら、Configuration Manager から Intune にご利用の Intune テナントの [MDM 機関を変更](migrate-change-mdm-authority.md)する準備ができているかどうかを検討します。 