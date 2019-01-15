---
title: 'Device Enrollment Program (DEP) を使用して iOS デバイスを登録する '
titleSuffix: Configuration Manager
description: Configuration Manager と Intune のハイブリッド展開に対応するために、iOS Device Enrollment Program (DEP) 登録を有効にします。
ms.date: 09/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 78d44adc-9b1c-4bc6-b72d-e93873916ea6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4628dd18ed865088c68cf38810e984a18f0ba0ad
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422217"
---
# <a name="ios-device-enrollment-program-dep-enrollment-for-hybrid-deployments-with-configuration-manager"></a>Configuration Manager とのハイブリッド展開に対応する iOS Device Enrollment Program (DEP) 登録

*適用対象します。System Center Configuration Manager (Current Branch)*

企業は、Apple のデバイス登録プログラムで iOS デバイスを購入してから、Microsoft Intune を使用してそのデバイスを管理することができます。 Apple Device Enrollment Program (DEP) を使用して企業所有の iOS デバイスを管理するには、企業は Apple の手順を実行してプログラムに参加し、そのプログラムを使用してデバイスを取得する必要があります。 そのプロセスの詳細については、[https://deploy.apple.com](https://deploy.apple.com) を参照してください。 このプログラムの利点として、各デバイスをコンピューターに USB 接続することなく、デバイスを楽に設定できる点があります。  

 DEP を使用して企業所有の iOS デバイスを登録するには、Apple の DEP トークンが必要です。 このトークンにより、Intune は企業所有の DEP 参加デバイスに関する情報を同期できるようになります。 また、Intune は Apple に登録プロファイルをアップロードし、デバイスをそれらのプロファイルに割り当てられるようになります。  

## <a name="apple-dep-enrollment-for-ios-devices"></a>iOS デバイスの Apple DEP 登録  
 次に、Apple DEP で購入した iOS デバイスを、Intune が管理する企業所有のデバイスに指定する手順について説明します。 ユーザーがデバイスの電源を初めて入れると、DEP 管理プロファイルを受信し、セットアップ アシスタントが実行され、管理対象になります。  

##  <a name="enable-dep-enrollment-in-configuration-manager-with-intune"></a>Configuration Manager と Intune で DEP 登録を有効にする  

1. **Configuration Manager を使用して iOS デバイス管理を開始する**   
   iOS Device Enrollment Program (DEP) デバイスを登録する前に、[iOS の登録をサポートする手順](../deploy-use/enroll-hybrid-ios-mac.md)を含む「[Set up Hybrid mobile device management](../../mdm/deploy-use/setup-hybrid-mdm.md)」(ハイブリッド モバイル デバイス管理のセットアップ) の手順を完了する必要があります。
2. **DEP トークン要求の作成**   
   Configuration Manager コンソールの **[管理]** ワークスペースで、**[階層の構成]**、**[クラウド サービス]** の順に展開してから、**[Microsoft Intune サブスクリプション]** をクリックします。 **[ホーム]** タブの **[DEP トークン要求の作成]** 、 **[参照]** の順にクリックして、DEP トークン要求をダウンロードする場所を指定してから、 **[ダウンロード]** をクリックします。 DEP トークン要求 (.pem) ファイルをローカルに保存します。 .pem ファイルは、Apple Device Enrollment Program ポータルから信頼されたトークン (.p7m) を要求するために使用します。  
3. **Device Enrollment Program トークンを取得する**   
   [Device Enrollment Program ポータル](https://deploy.apple.com) (https://deploy.apple.com) に移動し、会社の Apple ID でサインインします。 この Apple ID は、将来 DEP トークンを更新するために使用する必要があります。  
   1. [Device Enrollment Program ポータル](https://deploy.apple.com)で **[Device Enrollment Program]** > **「Manage Servers」 (サーバーの管理)** に移動して、**[Add MDM Server]** (MDM サーバーの追加) をクリックします。  
      ![Device Enrollment Program ポータルへの MDM サーバーの追加のスクリーンショット](../media/enrollment-program-token-add-server.png)
   2. **MDM サーバー名**を入力し、 **[Next]** をクリックします。 サーバー名は、自分が MDM サーバーを識別できるようにするための名前です。 Intune または Configuration Manager サーバーの名前または URL ではありません。  
   3. **[Add <サーバー名\>]** (<サーバー名> の追加) ダイアログ ボックスが開きます。 **[ファイルの選択…] をクリックして、** 前の手順で作成した .pem ファイルをアップロードしてから、**[Next]** (次へ) をクリックします。  
   4. **[Add <サーバー名\>]** (<サーバー名> の追加) ダイアログ ボックスに、**[Your Server Token]** (サーバー トークン) リンクが表示されます。 サーバー トークン (で管理することができます。p7m) ファイルをコンピューターにダウンロードしたら、 **[完了]** で管理することができます。  

      この証明書 (.p7m) ファイルは、Intune と Apple の Device Enrollment Program サーバーとの間に信頼関係を確立するために使用されます。  
4. **DEP トークンの Configuration Manager への追加**   
   Configuration Manager コンソールの **[管理]** ワークスペースで、**[階層の構成]** を展開してから、**[Windows Intune サブスクリプション]** をクリックします。 **[ホーム]** タブの **[プラットフォームの構成]** をクリックし、 **[iOS]** をクリックします。 **[デバイスの登録プログラムを有効にする]** を選択して、証明書 (.p7m) ファイルを参照してから、 **[開く]**、 **[アップロード]**、 **[OK]** の順にクリックします。  

## <a name="add-a-corporate-device-enrollment-policy"></a>業務用デバイスの登録ポリシーを追加する  

1. Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースで、**[概要]**、**[すべての企業所有のデバイス]**、**[iOS]** の順に展開してから、**[登録プロファイル]** をクリックします。 **[ホーム]** タブの **[プロファイルの作成]** をクリックして、プロファイルの作成ウィザードを開きます。 次の各ページで、設定を構成します。  
2. **[全般]** ページで、次の情報を指定してから、 **[次へ]** をクリックします。  
   - **名前** – デバイス登録プロファイルの名前を指定します。 (この機能は、ユーザーに表示されません)  
   - **説明** - デバイス登録プロファイルの説明。 (この機能は、ユーザーに表示されません)  
   - **[ユーザー アフィニティ]** – デバイスの登録方法を指定します。 「[User affinity for hybrid managed devices in Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md)」(Configuration Manager でのハイブリッド管理のデバイス向けユーザー アフィニティ) を参照してください。  

     - **ユーザー アフィニティのプロンプト**:デバイスは、初期セットアップ時にユーザーに関連付ける必要があり、会社のデータとそのユーザーとしての電子メールにアクセスが許可されますできます。  ユーザーに属していて (アプリケーションをインストールするために) ポータル サイトを利用する必要がある DEP 管理対象デバイスのユーザー アフィニティを構成する必要があります。  
       > [!NOTE]
       > ユーザー アフィニティが設定された DEP でユーザー トークンを要求するには、ADFS WS-Trust 1.3 Username/Mixed エンドポイントを有効にする必要があります。

     - **ユーザー アフィニティなし**:デバイスは、ユーザーと関連付けられません。 このデバイス関連付け情報を使用すると、ローカルのユーザー データにアクセスしなくてもタスクを実行できます。 ユーザーへの関連付けが必要なアプリが動作しません。  
       ![DEP プロファイル名、説明、ユーザー アフィニティ プロンプトのスクリーンショット](../media/dep-general.png)

3. **[Device Enrollment Program の設定]** ページで、以下の情報を指定し、**[次へ]** をクリックします。  
    -   **部門**:この情報は、ユーザーがアクティブ化時に構成について をタップすると表示されます。  
    -   **サポートの電話番号**:ユーザーがクリックしたときに表示される、**ヘルプが必要です**アクティブ化中にボタンをクリックします。
       ![iOS デバイスへの DEP プロファイルの割り当てのスクリーンショット](../media/dep-settings.png)

    - **準備モード**:この状態がアクティブ化時に設定され、工場出荷時のデバイスをリセットせずに変更することはできません。  
        -   **監督解除済み** - 管理機能が制限されます  
        -   **監督下** - より多くの管理オプションが使用可能になり、既定で [アクティブ化ロック] は無効になります  
    - **登録プロファイルをデバイスのロック**:この状態は、アクティブ化時に設定され、工場出荷時設定せずに変更することはできません。  
      -   **無効** - **[設定]** メニューから管理プロファイルを削除できます  
      -   **有効** - (**[準備モード]** = **[監督下]** にする必要があります) 管理プロファイルの削除を許可する iOS 設定を無効にします  

4. **[セットアップ アシスタント]** ページで、デバイスの電源が初めてオンになったときに起動する iOS セットアップ アシスタントをカスタマイズする設定を構成してから、 **[次へ]** をクリックします。 設定は次のとおりです。  
   -   **パスコード** - アクティブ化時にパスコードの入力を求めます。 デバイスがセキュリティで保護される場合や、他の何らかの方法 (デバイスを 1 つのアプリに制限するキオスク モードなど) でアクセスが制御されている場合を除き、パスコードは常に必須にしてください。  
   -   **位置情報サービス** - 有効にすると、アクティブ化時に、セットアップ アシスタントによってサービスがプロンプトされます  
   -   **復元** - 有効にすると、アクティブ化時に、セットアップ アシスタントによって iCloud バックアップがプロンプトされます  
   -   **Apple ID** - Intune でインストールされるアプリを含め、iOS App Store アプリをダウンロードする際に Apple ID が必須になります。 有効にして、Intune で ID を指定せずにアプリをインストールしようとすると、Apple ID の入力が求められます。  
   -   **使用条件** - 有効にすると、アクティブ化時に、セットアップ アシスタントによって Apple の使用条件に同意するように求められます  
   -   **タッチ ID** - 有効にすると、アクティブ化時に、セットアップ アシスタントによってこのサービスがプロンプトされます
   -   **Apple Pay** - 有効にすると、アクティブ化時に、セットアップ アシスタントによってこのサービスがプロンプトされます
   -   **ズーム** - 有効にすると、アクティブ化時に、セットアップ アシスタントによってこのサービスがプロンプトされます
   -   **Siri** - 有効にすると、アクティブ化時に、セットアップ アシスタントによってこのサービスがプロンプトされます  
   -   **Apple に診断データを送信する** - 有効にすると、アクティブ化時に、セットアップ アシスタントによってこのサービスがプロンプトされます  
   ![iOS デバイスへの DEP プロファイルの割り当てのスクリーンショット](../media/dep-setup-assistant.png)
5. **[追加の管理]** ページで、追加の管理設定のために USB 接続の使用を許可するかどうかを指定します。 **[証明書が必要]** を選択する場合、このプロファイルに使用する Apple Configurator 管理証明書をインポートする必要があります。  **[許可しない]** に設定すると、ファイルの iTunes との同期と Apple Configurator 経由の管理が実行されなくなります。 **[許可しない]** を使用して証明書ありまたは証明書なしの手動の展開を許可するのではなく、[許可しない] を選択して、Apple Configurator からその他の構成をエクスポートし、カスタム iOS 構成プロファイルとして展開することをお勧めします。  

   -   **許可しない** - デバイスの USB 経由の通信を禁止します (ペアリングを無効にします)  
   -   **許可する** - デバイスに PC または Mac との USB 接続での通信を許可します  
   -   **証明書が必要** - 登録プロファイルにインポートされた証明書を使用した Mac とのペアリングを許可します  

## <a name="assign-dep-devices-for-management"></a>DEP デバイスを管理対象にする

1. [Device Enrollment Program ポータル](https://deploy.apple.com) (https://deploy.apple.com) に移動し、会社の Apple ID でサインインします。
2. **[Deployment Program]** > **[Device Enrollment Program]** > **[デバイスの管理]** で管理することができます。 **デバイスの選択**方法を指定し、デバイス情報を入力して、デバイスの **シリアル番号**、 **注文番号**、または **CSV ファイルのアップロード**で詳細を指定します。 次に、**[Assign to Server]** (サーバーに割り当て) を選択し、手順 3 で指定した <*サーバー名*> を選択して、**[OK]** をクリックします。  
![Apple Device Enrollment Program ポータルへのデバイスの追加のスクリーンショット](../media/enrollment-program-token-specify-serial.png)

3.  **DEP で管理されたデバイスの同期**   
    **[資産とコンプライアンス]** ワークスペースで、**[会社が所有しているすべてのデバイス]**、**[事前に宣言されたデバイス]** の順に進みます。 **[ホーム]** タブの **[DEP の同期]** をクリックします。同期要求が Apple に送信されます。 同期が完了すると、DEP で管理されたデバイスが表示されます。

    > [!NOTE]
    > ハイブリッド構成では、Configuration Manager コンソールで **[DEP 同期]** をクリックすると、DEP の同期操作が手動でトリガーされます。

4.  **DEP プロファイルを割り当てる**<br>**[資産とコンプライアンス]** ワークスペースで、**[会社が所有しているすべてのデバイス]** > **[iOS]** > **[登録プロファイル]** の順に進みます。 DEP 登録プロファイルを選択し、**[ホーム]** タブで **[デバイスに割り当て]** をクリックします。 この登録プロファイルを使用するデバイスを選択し、**[追加]** をクリックし、**[OK]** をクリックします。

    > [!NOTE]
    > DEP プロファイルがデバイスに割り当てられると、別の DEP プロファイルでのみ、プロファイルを置き換えることができます。 ただし、DEP プロファイルの割り当てを削除することはできません。 DEP プロファイルをデバイスから削除するには、デバイスの登録を解除する必要があります。  
     ![iOS デバイスへの DEP プロファイルの割り当てのスクリーンショット](../media/dep-assign-profile.png)

## <a name="distribute-devices-to-users"></a>デバイスのユーザーへの配布
これで、会社が所有するデバイスをユーザーに付与できるようになりました。 マネージド デバイスの **登録状態** は、デバイスの電源がオンになり、セットアップ アシスタントを実行してデバイスを登録するまでは **[未接続]** となります。 iOS デバイスの電源をオンにすると、iOS デバイスが Intune の管理対象として登録されます。
