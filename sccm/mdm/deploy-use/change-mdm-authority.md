---
title: "MDM 機関を変更する"
titleSuffix: Configuration Manager
description: "MDM 機関を Configuration Manager (ハイブリッド) から Intune スタンドアロンに変更する方法について説明します"
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/17/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: c61a44cce443a7ff210a626d114068691541aaae
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="change-your-mdm-authority"></a>MDM 機関を変更する
Configuration Manager バージョン 1610 以降では、Microsoft サポートに連絡しなくても、また、既存の管理対象デバイスの登録を解除してから再登録しなくても、MDM 機関を変更できます。 この記事では、Configuration Manager コンソール (ハイブリッド) から構成された既存の Microsoft Intune テナントを Intune スタンドアロンに変更する手順を説明します。 この記事の手順を完了すると、デバイスが [Azure Portal](https://portal.azure.com) の Microsoft Intune で管理されます。 

> [!Note]    
> MDM 機関が Intune に設定された既存の Microsoft Intune テナントを Configuration Manager (ハイブリッド) に変更する場合は、「[MDM 機関を変更する](https://docs.microsoft.com/intune-classic/deploy-use/change-mdm-authority)」をご覧ください。

> [!Important]    
> この記事では、ユーザーをまだ移行していない場合に、MDM 機関を変更します。 [ユーザーのサブセットを移行](migrate-hybridmdm-to-intunesa.md)した後に ご使用の MDM 機関を変更するには、[MDM 機関の変更](migrate-change-mdm-authority.md)に関するページをご覧ください。

## <a name="key-considerations"></a>主な考慮事項
新しい MDM 機関に変更した後、多くの場合、デバイスがチェックインしてサービスと同期されるまでに移行時間 (最大 8 時間) があります。 新しい MDM 機関 (Intune スタンドアロン) で、変更後も登録済みデバイスが管理および保護されるように、設定を構成する必要があります。 以下は、注意事項です。
- デバイスの既存の設定が新しい MDM 機関の設定 (Intune スタンドアロン) に置き換わるように、変更後にご使用のデバイスをサービスに接続する必要があります。
- MDM 機関を変更した後、最大 7 日間は、以前の MDM 機関 (ハイブリッド) の基本的な設定 (プロファイルなど) の一部がデバイスに残ります。 できるだけ早く、新しい MDM 機関でアプリと設定 (ポリシー、プロファイル、アプリなど) を構成することをお勧めします。 さらに、既存の登録済みデバイスを持っているユーザーが含まれるユーザー グループに設定を展開します。 MDM 機関の変更後にデバイスがサービスに接続するときに、新しい MDM 機関から新しい設定を受信します。 新しいターゲットのポリシーがある場合は、デバイス上の既存のポリシーが上書きされます。
- 新しい MDM 機関に変更すると、[Azure Portal](https://portal.azure.com) のコンプライアンス データが正確に報告されるまでに最大 1 週間かかる場合があります。 ただし、Azure Active Directory とデバイスのコンプライアンス状態は正確なので、デバイスは引き続き保護されます。
- 関連付けられているユーザーがいない (通常は iOS Device Enrollment Program または一括登録シナリオの場合) デバイスは、新しい MDM 機関に移行されません。 これらのデバイスでは、新しい MDM 機関への移行を支援してもらうためにサポートを要請する必要があります。

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更する準備
MDM 機関の変更に備えて、次の情報を確認します。
- MDM 機関を変更するオプションを使用するには、Configuration Manager バージョン 1610 以降が必要です。
- 新しい MDM 機関に変更した後に、デバイスがサービスに接続できるようになるまでに最大 8 時間かかります。
- MDM 機関の変更前に、ハイブリッドで現在管理されているすべてのユーザーに、Intune/EMS ライセンスが割り当てられていることを確認しておきます。 ライセンスがあることで、MDM 機関の変更後も、ユーザーとそのデバイスが Intune スタンドアロンで管理されます。 詳細については、「[ユーザー アカウントに Intune のライセンスを割り当てる](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4)」を参照してください。
- 管理者ユーザー アカウントに Intune/EMS ライセンスが割り当てられていること、管理者ユーザー アカウントが Intune にサインインできることを確認してから、MDM 機関を変更します。 [Azure Portal](https://portal.azure.com) の Intune で、MDM 機関に **[Configuration Manager に設定]** (ハイブリッド テナント) と表示されることを確認してから、MDM 機関を変更します。
- MDM 機関の変更中に、エンドユーザーへの影響はあまりありません。 

## <a name="change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更する
MDM 機関を Intune スタンドアロンに変更するプロセスには、概要として次のような手順が含まれます。  
- Configuration Manager コンソールで **[MDM 機関を Microsoft Intune に変更]** オプションを使用して既存の Microsoft Intune サブスクリプションを削除します。
- [Azure Portal](https://portal.azure.com) の Intune で、新しい MDM 機関 (Intune) から、新しい設定とアプリを構成し、展開します。
- 次にデバイスをサービスに接続すると、新しい MDM 機関と同期し、新しい設定を受信します。

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更するには
1. Configuration Manager コンソールで **[管理]** &gt; **[概要]** &gt; **[クラウド サービス]** &gt; **[Microsoft Intune のサブスクリプション]** に移動し、既存の Intune サブスクリプションを削除します。
2. **[MDM 機関を Microsoft Intune に変更]** を選択し、**[次へ]** をクリックします。
   ![APNs 証明書要求のダウンロード](./media/mdm-change-delete-subscription.png)
3. Configuration Manager で MDM 機関を設定したときに元々使用していた Intune テナントにサインインします。
4. **[次へ]** をクリックして、ウィザードを完了します。
5. MDM 機関が **Microsoft Intune** に設定されます。 Configuration Manager コンソールの [Microsoft Intune サブスクリプション] ノードに Intune サブスクリプションは表示されなくなります。 
6. MDM 機関が設定されていることを確認するには、次の手順を実行します。 a. 以前に使用したのと同じ Intune テナントを使用して、[Azure Portal](https://portal.azure.com) にサインインします。 
    b. **[その他のサービス]** > **[監視 + 管理]** > **[Intune]** > **[デバイスの登録]** の順に選択します。 MDM 機関は、**[概要]** ブレードの右上のセクションに表示されます。 

## <a name="next-steps"></a>次のステップ
MDM 機関の変更が完了したら、次の手順を実行します。
- テナントの MDM 機関が変更されたことを Intune サービスが検出すると、登録されているすべてのデバイスに、サービスにチェックインして同期するように促す通知メッセージを送信します (これは定期的にスケジュールされているチェックインとは別になります)。 そのため、テナントの MDM 機関がハイブリッドから Intune スタンドアロンに変更された後は、電源を入れてオンラインになったすべてのデバイスはサービスに接続し、新しい MDM 機関を受信し、以降は Intune スタンドアロンに管理されるようになります。 これらのデバイスの管理と保護は中断されません。
- MDM 機関の変更中 (または変更直後) に電源を切っていたかオフラインだったデバイスは、電源を入れ、オンラインになったときに新しい MDM 機関のサービスに接続し、同期します。  
- ユーザーが新しい MDM 機関にすぐに変更するには、デバイスからサービスへのチェックインを手動で開始します。 ポータル サイト アプリを使用して、デバイス コンプライアンス チェックを開始することで、簡単にチェックインを開始できます。
- MDM 機関の変更後に、デバイスがサービスにチェックインして同期した後に、正常に動作していることを確認するには、[Azure Portal](https://portal.azure.com) でそのデバイスを探します。 Configuration Manager (ハイブリッド) で管理されていたデバイスが、管理対象デバイスとして Intune に表示されるようになります。    
- MDM 機関の変更中にデバイスがオフラインだったときから、デバイスがサービスにチェックインするまでは中間期間があります。 この中間期間にも確実にデバイスを保護し、利用できるように、最大 7 日間 (またはデバイスが新しい MDM 機関に接続し、新しい設定を受信して既存の設定が上書きされるまで)、次のプロファイルがデバイスに残ります。
    - 電子メール プロファイル
    - VPN プロファイル
    - 証明書プロファイル
    - Wi-Fi プロファイル
    - 構成プロファイル
- 既存の設定を上書きするための新しい設定は、古い設定が確実に上書きされるように、古い設定と同じ名前にする必要があります。 そうしないと、デバイスのプロファイルとポリシーが重複する可能性があります。    

  > [!TIP]   
  > ベスト プラクティスとして、MDM 機関の変更が完了した直後に、すべての管理設定、構成、展開を作成することをお勧めします。 こうすることで、中間期間にもデバイスを保護し、アクティブに管理することができます。   
-  MDM 機関を変更した後に、次の手順を実行して、新しいデバイスが新しい機関に正常に登録されたことを確認します。   
    - 新しいデバイスを登録する
    - 新しく登録したデバイスが、[Azure Portal](https://portal.azure.com) に表示されることを確認します。
    - [Azure Portal](https://portal.azure.com) からデバイスに対して、リモート ロックなどのアクションを実行します。 成功した場合、そのデバイスは新しい MDM 機関で管理されていることを示します。
- 特定のデバイスで問題がある場合、できるだけ早くデバイスを新しい機関に接続し、管理対象にするには、そのデバイスの登録を解除してから再登録します。