---
title: "MDM 機関を変更する"
titleSuffix: Configuration Manager
description: "MDM 機関を Configuration Manager (ハイブリッド) から Intune スタンドアロンに変更する方法について説明します"
keywords: 
author: dougeby
manager: angrobe
ms.date: 10/04/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: cbf45c5f9f04affc65243fdc4c8410d4ff033c1e
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2017
---
# <a name="change-your-mdm-authority"></a>MDM 機関を変更する
Configuration Manager バージョン 1610 以降では、Microsoft サポートに連絡しなくても、また、既存の管理対象デバイスの登録を解除してから再登録しなくても、MDM 機関を変更できます。 このトピックでは、Configuration Manager コンソール (ハイブリッド) から構成された既存の Microsoft Intune テナントを Intune スタンドアロンに変更する手順を説明します。

> [!Note]    
> MDM 機関が Intune に設定された既存の Microsoft Intune テナントを Configuration Manager (ハイブリッド) に変更する場合は、「[MDM 機関を変更する](https://docs.microsoft.com/intune-classic/deploy-use/change-mdm-authority)」をご覧ください。

> [!Important]    
> このトピックでは、ユーザーをまだ移行していない場合に、MDM 機関を変更します。 [ユーザーのサブセットを移行](migrate-hybridmdm-to-intunesa.md)した後に ご使用の MDM 機関を変更するには、[MDM 機関の変更](migrate-change-mdm-authority.md)に関するページをご覧ください。

## <a name="key-considerations"></a>主な考慮事項
新しい MDM 機関に変更した後、多くの場合、デバイスがチェックインしてサービスと同期されるまでに移行時間 (最大 8 時間) があります。 新しい MDM 機関 (Intune スタンドアロン) で、変更後も登録済みデバイスが管理および保護されるように、設定を構成する必要があります。 以下は、注意事項です。
- デバイスの既存の設定が新しい MDM 機関 (Intune スタンドアロン) の設定に置き換わるように、変更後にデバイスをサービスに接続する必要があります。
- MDM 機関を変更した後、最大 7 日間は、以前の MDM 機関 (ハイブリッド) の基本的な設定 (プロファイルなど) の一部がデバイスに残ります。 できるだけ早く、新しい MDM 機関でアプリと設定 (ポリシー、プロファイル、アプリなど) を構成することをお勧めします。 さらに、既存の登録済みデバイスを持っているユーザーが含まれるユーザー グループに設定を展開します。 MDM 機関の変更後にデバイスがサービスに接続するときに、新しい MDM 機関から新しい設定を受信します。 新しいターゲットのポリシーがある場合は、デバイス上の既存のポリシーが上書きされます。
- 新しい MDM 機関に変更した後は、Microsoft Intune 管理コンソールのコンプライアンス データが正確に報告されるまでに最大 1 週間かかる可能性があります。 ただし、Azure Active Directory とデバイスのコンプライアンス状態は正確なので、デバイスは引き続き保護されます。
- 関連付けられているユーザーがいない (通常は iOS Device Enrollment Program または一括登録シナリオの場合) デバイスは、新しい MDM 機関に移行されません。 これらのデバイスでは、新しい MDM 機関への移行を支援してもらうためにサポートを要請する必要があります。

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更する準備
MDM 機関の変更に備えて、次の情報を確認します。
- MDM 機関を変更するオプションを使用するには、Configuration Manager バージョン 1610 以降が必要です。
- 新しい MDM 機関に変更した後に、デバイスがサービスに接続できるようになるまでに最大 8 時間かかります。
- MDM 機関の変更前に、ハイブリッドで現在管理されているすべてのユーザーに、Intune/EMS ライセンスが割り当てられていることを確認しておきます。 ライセンスがあることで、MDM 機関の変更後も、ユーザーとそのデバイスが Intune スタンドアロンで管理されます。 詳細については、「[ユーザー アカウントに Intune のライセンスを割り当てる](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4)」を参照してください。
- 管理者ユーザー アカウントに Intune/EMS ライセンスが割り当てられていること、管理者ユーザー アカウントが Intune にサインインできることを確認してから、MDM 機関を変更します。 Microsoft Intune 管理コンソールで、MDM 機関に **[Configuration Manager に設定]** (ハイブリッド テナント) と表示されることを確認してから、MDM 機関を変更します。
- Configuration Manager コンソールで、すべてのデバイス登録マネージャー ロールを削除します。 **[管理]** > **[クラウド サービス]** > **[Microsoft Intune サブスクリプション]** に移動し、Microsoft Intune サブスクリプションを選択し、**[プロパティ]**、**[デバイス登録マネージャー]** タブの順にクリックし、すべてのデバイス登録マネージャー ロールを削除します。
- Configuration Manager コンソールで既存のデバイス カテゴリを削除します。 **[資産とコンプライアンス]** > **[概要]** > **[デバイス コレクション]** の順に移動し、**[デバイス カテゴリの管理]** を選択し、既存のデバイス カテゴリを削除します。
- MDM 機関の変更中に、エンドユーザーへの影響はあまりありません。 
- Configuration Manager (ハイブリッド テナント) を使用して iOS デバイスを管理していて、MDM 機関を変更する予定の場合は、Configuration Manager で使用されていたものと同じ Apple Push Notification サービス (APNs) 証明書を更新し、Intune スタンドアロンでテナントのセットアップに使用する必要があります。

   > [!IMPORTANT]  
   > Intune スタンドアロンに別の APNs を使用する場合、以前に登録されていた iOS デバイスはすべて未登録になるので、デバイスを再登録するプロセスを実行する必要があります。 MDM 機関を変更する前に、Configuration Manager で iOS デバイスの管理に使用されていた APNs 証明書を正確に把握しておく必要があります。 Apple Push 証明書ポータル (https://identity.apple.com) に記載されているものと同じ証明書を検索し、元の APNs 証明書の作成に使用された Apple ID を持つユーザーを特定し、新しい MDM 機関を変更する際に同じ APNs 証明書を更新できることを確認します。  

## <a name="change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更する
MDM 機関を Intune スタンドアロンに変更するプロセスには、概要として次のような手順が含まれます。  
- Configuration Manager コンソールで **[MDM 機関を Microsoft Intune に変更]** オプションを使用して既存の Microsoft Intune サブスクリプションを削除します。
- Microsoft Intune 管理コンソールで新しい MDM 機関を **[Intune]** に設定します。
- 更新したものと同じ APNs 証明書を使用して、Apple APNs 証明書を構成します。
- 新しい MDM 機関 (Intune) から、Microsoft Intune 管理コンソールで新しい設定とアプリを構成し、展開します。
- 次にデバイスをサービスに接続すると、新しい MDM 機関と同期し、新しい設定を受信します。

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更するには
1. Configuration Manager コンソールで **[管理]** &gt; **[概要]** &gt; **[クラウド サービス]** &gt; **[Microsoft Intune のサブスクリプション]** に移動し、既存の Intune サブスクリプションを削除します。
2. **[MDM 機関を Microsoft Intune に変更]** を選択し、**[次へ]** をクリックします。
   ![APNs 証明書要求のダウンロード](./media/mdm-change-delete-subscription.png)
3. Configuration Manager で MDM 機関を設定したときに元々使用していた Intune テナントにサインインします。
4. **[次へ]** をクリックして、ウィザードを完了します。
5. これで MDM 機関はリセットされました。 Configuration Manager コンソールの [Microsoft Intune サブスクリプション] ノードに Intune サブスクリプションは表示されなくなります。
6. 前の手順で使用したものと同じ Intune テナントを使用して、[Microsoft Intune 管理コンソール](http://manage.microsoft.com)にログインします。
7. MDM 機関がリセットされたことを確認してから、MDM 機関を **[Microsoft Intune]** に設定します。 MDM 機関を変更すると、コンソールで反映されたことを確認できます。 詳細については、「[MDM 機関を設定する](https://docs.microsoft.com/en-us/intune/deploy-use/prerequisites-for-enrollment#step-2-set-mdm-authority)」を参照してください。
<!-- [Azure portal](https://docs.microsoft.com/en-us/intune-azure/enroll-devices/set-mdm-authority) -->


## <a name="configure-the-apns-certificate"></a>APNs 証明書を構成する
iOS デバイスがある場合は、Intune で APNs 証明書を構成する必要があります。

#### <a name="to-configure-the-apns-certificate"></a>APNs 証明書を構成するには
1. APNs 証明書要求をダウンロードします。
   <!--The process is different depending on how you connect to Intune:
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment** &gt; **Apple MDM Push Certificate**, and then select **Download your CSR** to download and save the .csr file locally.   
    <br/>
    **Microsoft Intune administration console**   -->
   [Microsoft Intune 管理コンソール](http://manage.microsoft.com)で、**[管理]** &gt; **[モバイル デバイス管理]** &gt; **[iOS と Mac OS X]** &gt; **[APNs 証明書のアップロード]** に移動し、**[APNs 証明書要求のダウンロード]** を選択します。 証明書署名要求 (.csr) ファイルをローカルに保存します。    
   > [!IMPORTANT]    
   > 新しい証明書署名要求をダウンロードします。 既存のファイルは使用しないでください。失敗します。

   ![APNs 証明書要求のダウンロード](./media/mdm-change-download-apns-certificate.png)

2. [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) にアクセスし、以前に作成したときに使用したものと**同じ** Apple ID でサインインし、Configuration Manager (ハイブリッド) で使用していた APNs 証明書を更新します。

   ![Apple Push Certificates Portal のサインイン ページ](./media/mdm-change-apns-portal.png)

3. Configuration Manager (ハイブリッド) で使用していた APNs 証明書を選択し、**[Renew]** をクリックします。   

    ![[Renew APNs] ダイアログ ボックス](./media/mdm-change-renew-apns.png)

4. ローカルにダウンロードした APNs 証明書署名要求 (.csr) ファイルを選択し、**[Upload]** をクリックします。

    ![Apple Push Certificates Portal のサインイン ページ](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)
 
5. 同じ APNs を選択し、**[Download]** をクリックします。 APNs (.pem) 証明書をダウンロードして、ファイルをローカルに保存します。  

   ![Apple Push Certificates Portal のサインイン ページ](./media/mdm-change-renew-apns-download.png)

6. 以前と同じ Apple ID を使用して、更新された APNs 証明書を Intune テナントにアップロードします。
<!--The process is different depending on how to connect to Intune:  
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment**  &gt; **Apple MDM Push Certificate**, enter your Apple ID in step 3, select the certificate (.pem) file in step 4, and then click **Upload**.     
    <br/>
    **Microsoft Intune administration console**    -->
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Upload the APNs certificate**. Go to the certificate (.pem) file, choose **Open**, and then enter your **Apple ID**.   

   ![APNs 証明書のアップロード](./media/mdm-change-upload-apns-certificate.png)

## <a name="next-steps"></a>次のステップ
MDM 機関の変更が完了したら、次の手順を実行します。
- テナントの MDM 機関が変更されたことを Intune サービスが検出すると、登録されているすべてのデバイスに、サービスにチェックインして同期するように促す通知メッセージを送信します (これは定期的にスケジュールされているチェックインとは別になります)。 そのため、テナントの MDM 機関がハイブリッドから Intune スタンドアロンに変更された後は、電源を入れてオンラインになったすべてのデバイスはサービスに接続し、新しい MDM 機関を受信し、以降は Intune スタンドアロンに管理されるようになります。 これらのデバイスの管理と保護は中断されません。
- MDM 機関の変更中 (または変更直後) に電源を切っていたかオフラインだったデバイスは、電源を入れ、オンラインになったときに新しい MDM 機関のサービスに接続し、同期します。  

  iOS デバイスの場合、APNs 証明書の更新とセットアップのためにさらに時間が必要です。 そのため、iOS デバイスは最初のチェックイン要求を受信しません。 MDM 機関の変更中 (または変更直後) に iOS デバイスの電源が入り、オンラインだった場合でも、iOS デバイスが新しい MDM 機関のサービスに登録されるまでに最大 8 時間の遅れがあります (次の定期的なチェックインのタイミングによって異なります)。    

  > [!IMPORTANT]
  > MDM 機関を変更してから、更新された APNs 証明書が新しい機関にアップロードされるまで、iOS デバイスの新しいデバイスの登録とデバイスのチェックインは失敗します。 そのため、MDM 機関を変更した後は、できるだけ早く APNs 証明書を確認し、新しい機関にアップロードすることが重要です。   

- ユーザーが新しい MDM 機関にすぐに変更するには、デバイスからサービスへのチェックインを手動で開始します。 ポータル サイト アプリを使用して、デバイス コンプライアンス チェックを開始することで、簡単にチェックインを開始できます。
- MDM 機関の変更後に、デバイスがサービスにチェックインして同期した後に、正常に動作していることを確認するには、[Microsoft Intune 管理コンソール](http://manage.microsoft.com)でそのデバイスを探します。 Configuration Manager (ハイブリッド) で管理されていたデバイスが、管理対象デバイスとして表示されるようになります。    
- MDM 機関の変更中にデバイスがオフラインだったときから、デバイスがサービスにチェックインするまでは中間期間があります。 この中間期間にも確実にデバイスを保護し、利用できるように、最大 7 日間 (またはデバイスが新しい MDM 機関に接続し、新しい設定を受信して既存の設定が上書きされるまで)、次のものがデバイスに残ります。
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
    - 新しく登録したデバイスが、Intune 管理コンソールに表示されることを確認します。
    - 管理コンソールからデバイスに対して、リモート ロックなどのアクションを実行します。 成功した場合、そのデバイスは新しい MDM 機関で管理されていることを示します。
- 特定のデバイスで問題がある場合、できるだけ早くデバイスを新しい機関に接続し、管理対象にするには、そのデバイスの登録を解除してから再登録します。

<!-- After the change in MDM authority and devices check in with the service, note the following:      - The updated compliance status of devices will only display in the Azure portal immediately.
- There will be a delay for compliance status of devices to display in the Intune administrative console.-->