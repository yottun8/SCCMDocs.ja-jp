---
title: "MDM 機関を Intune に変更する"
titleSuffix: Configuration Manager
description: "MDM 機関を Configuration Manager (ハイブリッド) から Intune スタンドアロンに変更する方法について説明します。"
keywords: 
author: dougeby
manager: angrobe
ms.date: 12/05/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.openlocfilehash: 8884883c6e4e82cf38d83b9b7843002be3742bf1
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2017
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更する

*適用対象: System Center Configuration Manager (Current Branch)*    

Configuration Manager コンソール (ハイブリッド MDM) から構成された既存の Microsoft Intune テナントを Intune スタンドアロンに変更できます。 テナント レベルの MDM 機関を Intune に変更するのは、[ハイブリッド MDM のユーザーとデバイスを、クラウド専用構成の Intune スタンドアロンに移行する](migrate-hybridmdm-to-intunesa.md) プロセスの最後のフェーズです。    

> [!Important]    
> ハイブリッド MDM ユーザーを最初に Intune に移行せずに MDM 機関を変更する場合は、「[MDM 機関を変更する](change-mdm-authority.md)」をご覧ください。

この記事では、Configuration Manager コンソールから構成された既存の Microsoft Intune テナント (ハイブリッド) を Intune スタンドアロンに変更する方法について情報を提供しますが、次の手順が既に完了していることを前提としています。
- Configuration Manager オブジェクトを Intune にインポートするには、[Intune データ インポート ツール](migrate-import-data.md)を使用します。 
- ユーザーとユーザーのデバイスを移行した後も管理が継続されていることを確認するには、「[Prepared Intune for user migration (Intune でのユーザーの移行の準備)](migrate-prepare-intune.md)」をご覧ください。
- Azure Portal からユーザー デバイスの管理を開始するには、「[Changed the MDM authority for specific users (mixed MDM authority) (特定のユーザーの MDM 機関 (混合 MDM 機関) の変更)](migrate-mixed-authority.md)」をご覧ください。


## <a name="users-and-devices-that-have-not-been-migrated"></a>移行されていないユーザーとデバイス
既に多数のユーザーを移行し、Intune の機能が正常に動作することをテストしました。 したがって、ご使用のポリシー、プロファイル、アプリなどは Intune で構成され、デバイス上のオブジェクトは十分にテストされたことになります。 MDM 機関の変更後、テナント レベルのポリシーに新しい構成は必要ありません。 ただし、あらかじめ移行されていないユーザーとデバイスについては、MDM 機関の変更後に予想されることに関する次の情報を確認します。    
- 多くの場合、デバイスがチェックインしてサービスと同期するまでに、移行時間 (最大 8 時間) が発生します。
- デバイスの既存の設定が新しい MDM 機関の設定 (Intune スタンドアロン) に置き換わるように、変更後にご使用のデバイスをサービスに接続する必要があります。
- 最大 7 日間は、以前の MDM 機関 (ハイブリッド) の基本的な設定 (プロファイルなど) の一部がデバイスに残ります。 
- 関連付けられているユーザーがいない (通常は iOS Device Enrollment Program または一括登録シナリオの場合) デバイスは、新しい MDM 機関に移行されません。 これらのデバイスでは、新しい MDM 機関への移行を支援してもらうためにサポートを要請する必要があります。

## <a name="prerequisites"></a>必要条件
MDM 機関の変更に備えて、次の情報を確認します。
- MDM 機関を変更するオプションを使用するには、Configuration Manager バージョン 1610 以降が必要です。
- MDM 機関の変更前に、ハイブリッド MDM で現在管理されているすべてのユーザーに、Intune/EMS ライセンスが割り当てられていることを確認しておきます。 ライセンスがあることで、MDM 機関の変更後も、ユーザーとそのデバイスが Intune スタンドアロンで管理されます。 詳細については、「[ユーザー アカウントに Intune のライセンスを割り当てる](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4)」を参照してください。
- 管理者ユーザー アカウントに Intune/EMS ライセンスが割り当てられていることを確認します。

## <a name="change-the-mdm-authority-to-intune"></a>MDM 機関を Intune に変更する
次の手順を使用して、テナント レベルの MDM 機関を Intune に変更します。

1.  Configuration Manager コンソールで **[管理]** &gt; **[概要]** &gt; **[クラウド サービス]** &gt; **[Microsoft Intune のサブスクリプション]** に移動し、既存の Intune サブスクリプションを削除します。
2.  **[MDM 機関を Microsoft Intune に変更]** を選択し、**[次へ]** をクリックします。

    ![Microsoft Intune サブスクリプションの削除ダイアログ](media/mdm-change-delete-subscription.png)
3.  Configuration Manager で MDM 機関を設定したときに元々使用していた Intune テナントにサインインします。
4.  **[次へ]** をクリックして、ウィザードを完了します。
5.  これで MDM 機関はリセットされました。 Configuration Manager コンソールの [Microsoft Intune サブスクリプション] ノードに Intune サブスクリプションは表示されなくなります。
6.  以前に使用したのと同じ Intune テナントを使用して、[Azure Portal で Intune](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade/overview) にログインします。    

  > [!Important]    
  > Intune のクラシック コンソールを使用しないでください。 Azure Portal で Intune にログインする必要があります。
7.  MDM 機関が **Microsoft Intune** に変更されたことを確認します。 

## <a name="next-steps"></a>次のステップ
MDM 機関の変更が完了したら、次の情報を確認します。
- MDM 機関の変更中に、エンドユーザーへの影響はあまりありません。 
- テナント レベルのポリシーを再構成する必要はありません。 
- MDM 機関の変更後に、Azure Portal で Intune からテナント レベルのポリシーを編集できます。
-  MDM 機関を変更した後に、次の手順を実行して、新しいデバイスが新しい機関に正常に登録されたことを確認します。   
    - 新しいデバイスを登録する
    - 新しく登録したデバイスが、Intune に表示されることを確認します。
    - 管理コンソールからデバイスに対して、リモート ロックなどのアクションを実行します。 成功した場合、そのデバイスは新しい MDM 機関で管理されていることを示します。
- 特定のデバイスで問題がある場合、できるだけ早くデバイスを新しい機関に接続し、管理対象にするには、そのデバイスの登録を解除してから再登録します。
- あらかじめ移行されていないユーザーとデバイスについて
    - デバイスが**デバイス** ブレードに、管理対象デバイスとして現在表示されていることを確認します。 MDM 機関の変更後、これらのデバイスが表示される前に、デバイスをサービスにチェックインして、同期する必要があります。 
    - テナントの MDM 機関が変更されたことを Intune サービスが検出すると、登録されているすべてのデバイスに、サービスにチェックインして同期するように促す通知メッセージが送信されます (定期的にスケジュールされているチェックインとは別です)。 そのため、テナントの MDM 機関がハイブリッドから Intune スタンドアロンに変更された後は、電源を入れてオンラインになったすべてのデバイスはサービスに接続し、新しい MDM 機関を受信し、以降は Intune スタンドアロンで管理されるようになります。 これらのデバイスの管理と保護は中断されません。
    - MDM 機関の変更中 (または変更直後) に電源を切っていたかオフラインだったデバイスは、電源を入れ、オンラインになったときに新しい MDM 機関のサービスに接続し、同期します。  
    - ユーザーが新しい MDM 機関にすぐに変更するには、デバイスからサービスへのチェックインを手動で開始します。 ポータル サイト アプリを使用して、デバイス コンプライアンス チェックを開始することで、簡単にチェックインを開始できます。
    - MDM 機関の変更中にデバイスがオフラインだったときから、デバイスがサービスにチェックインするまでは中間期間があります。 この中間期間にも確実にデバイスが保護され利用できるように、次のプロファイルが最大 7 日間 (またはデバイスが新しい MDM 機関に接続し、新しい設定を受信して既存の設定が上書きされるまで)、デバイスに残ります。
        - 電子メール プロファイル
        - VPN プロファイル
        - 証明書プロファイル
        - Wi-Fi プロファイル
        - 構成プロファイル
    - サポートに連絡して、ユーザーに関連付けられていないデバイスの MDM 機関の変更について支援を受けます。 
