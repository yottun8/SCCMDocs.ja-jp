---
title: "Intune でのユーザーの移行を準備する"
titleSuffix: Configuration Manager
description: "ハイブリッド MDM. からユーザーを移行するため、Azure で Intune を準備する方法について説明します。"
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/14/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.openlocfilehash: 7addb69ff0336b82d0e59e2288110ebb7c074af3
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2017
---
# <a name="prepare-intune-for-user-migration"></a>Intune でのユーザーの移行を準備する 

*適用対象: System Center Configuration Manager (Current Branch)*    

ハイブリッド MDM (Configuration Manager と統合された Intune) から Intune スタンドアロンにユーザーを移行する前に、Intune を準備する手順を実行する必要があります。 これらの手順は、移行されたユーザーとそのデバイスが引き続き管理されることを確認するのに役立ちます。 これらの手順を完了して、Intune への移行を開始するときに、ユーザーに対して透過的にする必要があります。  

## <a name="fix-issues-found-during-data-collection-and-import"></a>データの収集とインポート中に見つかった問題の修正
[Configuration Manager のデータを Microsoft Intune にインポートする](migrate-import-data.md)ための処理を実行すると、Intune Data Importer ツールによってインポートできなかったすべてのオブジェクトの概要が提供されます。 発生する可能性のある一般的な問題の一部と、Intune での問題を修正するために実行できる手順を次の表に示します。 

|問題  |修正  |
|---------|---------|
|ダイレクト メンバーシップまたは複合に基づくコレクションが自動的に移行されない|Azure で Azure Active Directory (AAD) グループを作成して、インポートされなかったコレクションを置き換える必要があります。 その後、オブジェクトをそのグループに割り当てる必要があります。|
|ポリシーがインポートできなかった |Intune でポリシーを再作成する必要があります。|
|インポートされないオブジェクトのデプロイ|グループにオブジェクトを割り当てる必要があります。 グループには、デプロイのコレクションから同じユーザーを含める必要があります。|

## <a name="create-intune-objects"></a>Intune オブジェクトの作成 
[Configuration Manager のデータを Microsoft Intune にインポートする](migrate-import-data.md)ための処理を実行し、インポート プロセス中に問題を修正した場合は、インポートしたオブジェクトが正しく構成されたことを確認する必要があります。 さらに、組織で必要な任意のオブジェクト (ポリシー、プロファイル、アプリなど) を Intune で作成します。 

## <a name="assign-intune-licenses-to-migrated-users"></a>Intune ライセンスを移行されたユーザーに割り当てる
Configuration Manager で、Intune サブスクリプションにコレクションを追加します。コレクションのメンバーは、自分のデバイスを登録することができます。 Intune ライセンスは登録済みのデバイス用に予約されていますが、これらのライセンスはユーザーまたはデバイスに具体的に関連付けられていません。 たとえば、登録済みのデバイスを持つユーザーの AAD では、Intune ライセンスは見つかりません。 しかし、Intune スタンドアロンでは、ユーザーごとに Intune ライセンスを構成する必要があります。 MDM 機関の変更後も、ユーザーとそのデバイスが Intune で管理されるようにするには、Intune スタンドアロンにユーザーを移行する前に、これを行う必要があります。 詳細については、「[ユーザー アカウントに Intune のライセンスを割り当てる](https://docs.microsoft.com/intune/licenses-assign)」を参照してください。 

## <a name="verify-intune-user-groups"></a>Intune ユーザー グループの確認
ディレクトリ同期を構成したため、ユーザーとグループが AAD に既にある可能性があります。 ユーザーが適切なユーザー グループに含まれていることを確認するには、Intune ユーザー グループを確認することをお勧めします。 ポリシー、プロファイル、アプリなどをこれらのグループの対象にします。 Intune スタンドアロンに移行するユーザーが正しいグループに含まれていることを確認します。 

## <a name="configure-role-based-administration-control-rbac"></a>ロール ベースの管理制御 (RBAC) の構成
移行の一環として、Intune で必要なすべての RBAC ロールを構成して、これらのロールにユーザーを割り当てます。 Configuration Manager と Intune の RBAC には、リソースのスコープの設定など、いくつかの相違点があることに注意してください。 詳細については、「[Intune でのロール ベースの管理制御 (RBAC)](https://docs.microsoft.com/en-us/intune/role-based-access-control)」を参照してください。

## <a name="assign-apps-and-policies-to-aad-groups"></a>AAD グループにアプリとポリシーを割り当てる
移行プロセスの [Configuration Manager データの Microsoft Intune へのインポート](migrate-import-data.md) フェーズを実行して異なる Configuration Manager オブジェクトを Intune に移行した場合、オブジェクトの多くが既に AAD グループに割り当てられている可能性があります。 ただし、すべてのオブジェクト (アプリ、ポリシー、プロファイルなど) が正しい AAD グループに割り当てられていることを確認する必要があります。 オブジェクトを正しく割り当てると、ユーザーが移行された後にユーザーのデバイスが自動的に構成され、移行がユーザーに対して透過的になります。 AAD グループへのオブジェクトの割り当ての詳細については、次を参照してください。 
- [ポリシーの割り当て](https://docs.microsoft.com/intune/get-started-policies) 
- [プロファイルの割り当て](https://docs.microsoft.com/intune/device-profile-assign) 
- [アプリの割り当て](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>使用条件ポリシー
その他のテナント レベルのポリシーと同じように、ご利用のテナントに対して混在機関を有効にすると、使用条件ポリシーが Intune に自動的に移行されます。  ただし、移行したユーザーの同意について正確にレポートするには、移行したユーザーを含むグループに使用条件を割り当て、使用条件が将来の使用条件の更新またはデバイスの登録を対象としていることを確認する必要があります。 Configuration Manager コンソールで、ポリシーに変更が加えられない限り、ユーザーは使用条件に再度同意する必要はありません。 詳細については、「[使用条件を割り当てる](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions)」を参照してください。

## <a name="configure-the-exchange-connector"></a>Exchange Connector の構成
Exchange を使用して Configuration Manager で Exchange Connector を持つ場合は、Intune でオンプレミスの Exchange Connector を構成する必要があります。 詳細については、「[Microsoft Intune Azure で Intune のオンプレミス Exchange Connector をセットアップする](https://docs.microsoft.com/intune/exchange-connector-install)」を参照してください。

> [!Important]
> ユーザーを移行後、条件付きアクセスが正常に機能するため、およびユーザーが自分の電子メール サーバーに引き続きアクセスできるようにするには、次の条件に当てはまることを確認します。
> - Exchange ActiveSync の既定のアクセス レベルの設定 (DefaultAccessLevel) がブロックまたは検疫に設定されている場合、デバイスが電子メールへのアクセスを失う可能性があります。 
> - Configuration Manager が Exchange Connector にインストールされていて、**[モバイル デバイスをアクセス規則で管理しない場合のアクセス レベル]** 設定の値が **[アクセスを許可する]** になっている場合、ユーザーを移行する前に、Intune に [On-Premises Exchange Connector](https://docs.microsoft.com/en-us/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) をインストールする必要があります。 **[Exchange ActiveSync アクセスの詳細設定]** の **[Exchange on-premises]\(Exchange On-Premises\)** ブレードで、Intune に既定のアクセス レベルの設定を構成します。 詳細については、「[Exchange On-premises アクセスの構成](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access)」を参照してください。
> - 両方のコネクタに同じ構成を使用します。 構成した最後のコネクタにより、他のコネクタによって以前に書き込まれた ActiveSync の組織設定が上書きされます。 コネクタを異なる方法で構成すると、予期しない条件付きアクセスの変更が発生する可能性があります。
> - ユーザーが Intune スタンドアロンに移行されたら、Configuration Manager での条件付きアクセスの対象からそれらのユーザーを削除します。

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Microsoft Intune Certificate Connector の構成
NDES を使用して SCEP を使用する証明書を発行する場合は、Microsoft Intune Certificate Connector を構成する必要があります。 Intune で NDES コネクタをホストするコンピューターは、Configuration Manager で NDES コネクタをホストするのと同じコンピューターにすることはできません。 詳細については、「[Intune で SCEP 証明書を構成して管理する](https://docs.microsoft.com/en-us/intune/certificates-scep-configure)」を参照してください。 

> [!Important]    
> コネクタを構成した後に、インポートした SCEP プロファイルを新しいサーバーの URL を参照するように変更する必要があります。

## <a name="next-step"></a>次のステップ
移行のための Intune の準備が終ったら、一連のテスト ユーザーを Intune スタンドアロンに移行することができます。 詳細については、「[Change the MDM authority for specific users (mixed authority)](migrate-mixed-authority.md)」 (特定のユーザーの MDM 機関を変更する (混在機関)) を参照してください。


