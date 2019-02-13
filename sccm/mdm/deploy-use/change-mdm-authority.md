---
title: MDM 機関を変更する
titleSuffix: Configuration Manager
description: MDM 機関を Configuration Manager (ハイブリッド) から Intune スタンドアロンに変更する方法について説明します
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0420113feaaf9c9485b8d1e3d488b07878c61b5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131967"
---
# <a name="change-your-mdm-authority"></a>MDM 機関を変更する

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft サポートに問い合わせずに、また、既存のマネージド デバイスの登録解除と再登録を行わずに、MDM 機関を変更できます。 この記事では、Configuration Manager コンソール (ハイブリッド) から構成された既存の Microsoft Intune テナントを Intune スタンドアロンに変更する手順を説明します。 この記事の手順を完了すると、デバイスが [Azure Portal](https://portal.azure.com) の Microsoft Intune で管理されます。 

この記事では、ユーザーをまだ移行していない場合に、MDM 機関を変更します。 [ユーザーのサブセットを移行](migrate-hybridmdm-to-intunesa.md)した後で MDM 機関を変更するには、[MDM 機関の変更](migrate-change-mdm-authority.md)に関するページをご覧ください。

> [!Important]  
> 2018 年 8 月 13 日の時点では、ハイブリッド モバイル デバイス管理は[非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)です。 詳細については、[ハイブリッド MDM の概要](/sccm/mdm/understand/hybrid-mobile-device-management)に関するページを参照してください。<!--Intune feature 2683117-->  



## <a name="key-considerations"></a>主な考慮事項

MDM 機関を変更した後の切り替え時間は、最大 8 時間と予想されます。 デバイスがサービスにチェックインして同期される前に、これだけの時間がかかる可能性があります。 変更後も登録済みデバイスが管理および保護されるように、Intune で直接設定を構成します。 以下は、注意事項です。

- デバイスの既存の設定が新しい MDM 機関の設定 (Intune スタンドアロン) に置き換わるように、変更後にご使用のデバイスをサービスに接続する必要があります。  

- MDM 機関を変更した後、最大 7 日間は、以前の MDM 機関 (ハイブリッド) の基本的な設定 (プロファイルなど) の一部がデバイスに残ります。 できるだけ早く、新しい MDM 機関でアプリと設定 (ポリシー、プロファイル、アプリなど) を構成することをお勧めします。 さらに、既存の登録済みデバイスを持っているユーザーが含まれるユーザー グループに設定を展開します。 MDM 機関の変更後にデバイスがサービスに接続するときに、新しい MDM 機関から新しい設定を受信します。 新しいターゲットのポリシーがある場合は、デバイス上の既存のポリシーがオーバーライドされます。  

- 新しい MDM 機関に変更すると、[Azure Portal](https://portal.azure.com) のコンプライアンス データが正確に報告されるまでに最大 1 週間かかる場合があります。 ただし、Azure Active Directory とデバイスのコンプライアンス状態は正確です。 デバイスは引き続き保護されます。  

- 関連付けられているユーザーが存在しないデバイスは、新しい MDM 機関に移行されません。 この動作は、iOS Device Enrollment Program や一括登録のシナリオの場合に一般的です。 これらのデバイスでは、新しい MDM 機関への移行を支援してもらうためにサポートを要請します。  



## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更する準備

MDM 機関の変更に備えて、次の情報を確認します。

- 新しい MDM 機関に変更した後に、デバイスがサービスに接続できるようになるまでに最大 8 時間かかります。  

- MDM 機関の変更前に、ハイブリッドで現在管理されているすべてのユーザーに、Intune/EMS ライセンスが割り当てられていることを確認しておきます。 このライセンスによって、MDM 機関の変更後も、ユーザーとそのデバイスが Intune スタンドアロンで管理されるようにします。 詳細については、「[ユーザー アカウントに Intune のライセンスを割り当てる](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4)」を参照してください。  

- 管理者ユーザー アカウントに Intune/EMS ライセンスが割り当てられていることを確認します。 MDM 機関への変更の前に、管理者ユーザー アカウントが Intune にサインインできることを確認します。 [Azure Portal](https://portal.azure.com) の Intune で、MDM 機関に **[Configuration Manager に設定]** (ハイブリッド テナント) と表示されることを確認してから、MDM 機関を変更します。  

- MDM 機関の変更中に、エンドユーザーへの影響はあまりありません。 



## <a name="change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更する

MDM 機関を Intune スタンドアロンに変更するプロセスには、概要として次のような手順が含まれます。  

- Configuration Manager コンソールで **[MDM 機関を Microsoft Intune に変更]** オプションを使用して既存の Microsoft Intune サブスクリプションを削除します。  

- [Azure Portal](https://portal.azure.com) の Intune で、新しい MDM 機関 (Intune) から、新しい設定とアプリを構成し、展開します。  

- 次にデバイスをサービスに接続すると、新しい MDM 機関と同期し、新しい設定を受信します。  

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更するには
1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動します。 **[クラウド サービス]** を展開し、**[Microsoft Intune サブスクリプション]** ノードを選択します。 既存の Intune サブスクリプションを削除します。  

2. **[MDM 機関を Microsoft Intune に変更]** を選択し、**[次へ]** をクリックします。  

   ![Microsoft Intune サブスクリプションの削除ウィザードの [概要] ページ](./media/mdm-change-delete-subscription.png)

3. Configuration Manager で MDM 機関を設定したときに元々使用していた Intune テナントにサインインします。  

4. **[次へ]** をクリックして、ウィザードを完了します。  

5. MDM 機関が **Microsoft Intune** に設定されます。 Configuration Manager コンソールの [Microsoft Intune サブスクリプション] ノードに Intune サブスクリプションは表示されません。  

6. MDM 機関が設定されていることを確認するには、次の手順を実行します。  

    1. 以前に使用したのと同じ Intune テナントを使用して、[Azure Portal](https://portal.azure.com) にサインインします。  

    2. **[すべてのサービス]** > **[Intune]** > **[デバイスの登録]** の順に選択します。 MDM 機関は、**[概要]** の右上のセクションに表示されます。  



## <a name="next-steps"></a>次のステップ

MDM 機関の変更が完了したら、次の手順を実行します。  

- テナントの MDM 機関が変更されたことを Intune サービスが検出すると、登録されているすべてのデバイスに、サービスにチェックインして同期するように促す通知メッセージが送信されます。 この動作は定期的にスケジュールされているチェックインとは別です。 そのため、テナントの MDM 機関がハイブリッドから Intune スタンドアロンに変更された後は、電源を入れてオンラインになったすべてのデバイスはサービスに接続し、新しい MDM 機関を受信し、Intune スタンドアロンで管理されます。 これらのデバイスの管理と保護は中断されません。  

- MDM 機関の変更中 (または変更直後) に電源を切っていたかオフラインだったデバイスは、電源を入れ、オンラインになったときに新しい MDM 機関のサービスに接続し、同期します。   

- ユーザーが新しい MDM 機関にすぐに変更するには、デバイスからサービスへのチェックインを手動で開始します。 ポータル サイト アプリを使用して、デバイス コンプライアンス チェックを開始することで、ユーザーはこのアクションを簡単に実行できます。  

- MDM 機関の変更後に、デバイスがサービスにチェックインして同期した後に、正常に動作していることを確認するには、[Azure Portal](https://portal.azure.com) でそのデバイスを探します。 Configuration Manager (ハイブリッド) で以前に管理されていたデバイスは、マネージド デバイスとして Intune に表示されます。    

- MDM 機関の変更中にデバイスがオフラインだったときから、デバイスがサービスにチェックインするまでは中間期間があります。 この中間期間にも確実にデバイスが保護され利用できるように、次のプロファイルが最大 7 日間 (またはデバイスが新しい MDM 機関に接続し、新しい設定を受信して既存の設定が上書きされるまで)、デバイスに残ります。  
    - 電子メール プロファイル
    - VPN プロファイル
    - 証明書プロファイル
    - Wi-Fi プロファイル
    - 構成プロファイル  

- 古い設定を上書きするには、新しい設定は、既存の設定が確実に上書きされるように、前の設定と同じ名前にする必要があります。 そうしないと、デバイスのプロファイルとポリシーが重複する可能性があります。    

  > [!TIP]   
  > MDM 機関の変更が完了した直後に、すべての管理設定、構成、展開を作成します。 このアクションは、中間期間にもデバイスを保護し、アクティブに管理するのに役立ちます。   

-  MDM 機関を変更した後に、次の手順を実行して、新しいデバイスが新しい機関に正常に登録されたことを確認します。   

    - 新しいデバイスを登録する  

    - 新しく登録したデバイスが、[Azure Portal](https://portal.azure.com) に表示されることを確認します。  

    - [Azure Portal](https://portal.azure.com) からデバイスに対して、リモート ロックなどのアクションを実行します。 成功した場合、そのデバイスは新しい MDM 機関で管理されていることを示します。  
    
- 特定のデバイスに問題がある場合は、デバイスの登録解除と再登録を行います。 このアクションは新しい機関に接続され、できるだけ迅速に管理されます。  

- ハイブリッド テナントなどの [Android for Work](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client) を有効にして、テナントを Intune スタンドアロンに移行する場合は、登録制限の下での Android for Work の設定は、許可ではなくブロックとして示される可能性があります。 手動で **[許可]** に設定して、もう一度 Android for Work の登録を有効にします。<!--512117-->  

- MDM 機関を変更した後、Apple VPP トークンとそれに関連付けられている[ボリューム購入された iOS アプリ](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)は、自動的に削除されません。 この情報をクリーンアップするには、「[Apple VPP トークンを削除する](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps#delete-an-apple-vpp-token)」の手順に従います。 操作が完了すると、サイトでトークンが削除されます。 また、ライセンスされたストア アプリのノードから、そのトークンのアプリケーション メタデータも削除されます。<!--SCCMDocs issue 579-->  

    まれに、サイトで管理オブジェクトを削除できなかったというエラーが表示されることがあります。  

    - トークンが表示されない場合は、エラーを無視してください  

    - トークンがまだ一覧に表示される場合は、削除を再試行します  

