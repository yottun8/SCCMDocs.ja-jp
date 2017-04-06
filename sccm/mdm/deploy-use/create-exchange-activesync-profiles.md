---
title: "Exchange ActiveSync 電子メール プロファイルを作成する | Microsoft Docs"
description: "Microsoft Intune と連携して機能する System Center Configuration Manager で電子メール プロファイルを作成および構成する方法について説明します。"
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: 4
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: c90e5ebc2aca3f2133227fa59057aad8db3713f4
ms.lasthandoff: 03/27/2017


---

# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager で Exchange ActiveSync 電子メール プロファイルを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

電子メール プロファイルと Microsoft Intune を組み合わせて使えば、Exchange ActiveSync を利用して、電子メール プロファイルと制限をデバイスにプロビジョニングできます。 これにより、ユーザーは最小限の設定で自分のデバイスから会社の電子メールにアクセスできるようになります。  

 次の種類のデバイスに電子メール プロファイルを構成できます。  

- Windows 10
- Windows Phone 8.1
- Windows Phone 8.0
- iPhone (iOS 5、iOS 6、iOS 7、iOS 8)  
- iPad (iOS 5、iOS 6、iOS 7、iOS 8)  
- Samsung KNOX Standard (4 以降)
- Android for Work

電子メール プロファイルをデバイスに展開するには、デバイスが Intune に登録されている必要があります。 デバイスの登録方法については、「 [Microsoft Intune を使用したモバイル デバイスの管理](https://technet.microsoft.com/en-us/library/dn646962.aspx)」を参照してください。

>[!NOTE]
>Intune には Android for Work 電子メール プロファイルが 2 つあります。Gmail 用と Nine Work 電子メール アプリ用です。 これらのアプリは Google Play ストアで入手できます。また、Exchange への接続をサポートしています。 電子メール接続を有効にするには、いずれかの電子メール アプリをユーザーのデバイスに展開し、適切なプロファイルを作成して展開します。 Nine Work などの電子メール アプリは無料とは限りません。 アプリケーションのライセンスの詳細を確認するか、アプリの会社に問い合わせてください。

 デバイスに電子メール アカウントを構成するだけでなく、アドレス帳、予定表と仕事の同期の設定を構成することもできます。  

 電子メール プロファイルを作成するときに、System Center Configuration Manager 証明書プロファイルを使用してプロビジョニングされた ID、暗号化および署名に関する証明書などの幅広いセキュリティ設定を含めることができます。 証明書プロファイルの詳細については、「[System Center Configuration Manager の証明書プロファイル](/sccm/protect/deploy-use/introduction-to-certificate-profiles)」を参照してください。    

## <a name="create-a-new-exchange-activesync-email-profile"></a>新しい Exchange ActiveSync 電子メール プロファイルを作成する  

[Exchange ActiveSync 電子メール プロファイルの作成ウィザード] を開始する  

1.  Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。  

2.  [ **資産とコンプライアンス** ] ワークスペースで、[ **コンプライアンス設定**]、[ **会社リソースのアクセス**] の順に展開してから、[ **電子メール プロファイル**] をクリックします。  

3.  **[ホーム]** タブの **[作成]** グループで、**[Exchange ActiveSync 電子メール プロファイルの作成]** をクリックします。
4.  ウィザードの [全般] ページで、次のように構成します。
    - **[名前]** - 電子メール プロファイルにわかりやすい名前を指定します。
    - **[説明]** - 必要に応じて、Configuration Manager コンソールで識別するのに役立つ電子メール プロファイルの説明を指定します。
    - **[これは Android for Work に関するメール プロファイルです]** - この電子メール プロファイルを Android for Work デバイスのみに展開する場合は、このオプションを選びます。 このチェック ボックスをオンにした場合、**サポートされているプラットフォーム** ウィザードのページは表示されません。 Android for Work の電子メール プロファイルのみが構成されます。
4.  Exchange ActiveSync 電子メール プロファイルの作成ウィザードの [ **Exchange ActiveSync** ] ページで、次の情報を指定します。  

    -   **Exchange ActiveSync ホスト:** Exchange ActiveSync サービスをホストする社内 Exchange Server のホスト名を指定します。  

    -   **アカウント名:** ユーザーのデバイスに表示する、電子メール アカウントの表示名を指定します。  

    -   **アカウントのユーザー名:** クライアント デバイスで電子メール アカウントのユーザー名を構成する方法を選択します。 ドロップダウン リストから次のオプションのいずれかを選択できます。  

        -   [**ユーザー プリンシパル名** ] 完全ユーザー プリンシパル名を使用し、Exchange にログオンします。  

        -   **[アカウント名]** Active Directory の完全なユーザー アカウント名を使います

        -   [**プライマリ SMTP アドレス** ] ユーザーのプライマリ SMTP アドレスを使用し、Exchange にログオンします。  

    -   **電子メール アドレス:** 各クライアント デバイスでユーザーの電子メール アドレスを生成する方法を選択します。 ドロップダウン リストから次のオプションのいずれかを選択できます。  

        -   [**プライマリ SMTP アドレス** ] ユーザーのプライマリ SMTP アドレスを使用し、Exchange にログオンします。  

        -   [**ユーザー プリンシパル名** ] 電子メール アドレスとして完全ユーザー プリンシパル名を使用します。  

    -   **アカウント ドメイン:** 次のいずれかのオプションを選択します。  

        -   **Active Directory から取得する**  

        -   **カスタム**  

         このフィールドは、[ **sAMAccountName** ] が [ **アカウントのユーザー名** ] ドロップボックス リストで選択されている場合にのみ該当します。  

    -   **認証方法:** Exchange ActiveSync への接続の認証に使用する認証方法を次から 1 つ選択します。  

        -   [**証明書** ] ID 証明書を Exchange ActiveSync 接続の認証に使用します。  

        -   [**ユーザー名とパスワード** ] Exchange ActiveSync に接続するには、デバイス ユーザーはパスワードを入力する必要があります (ユーザー名は電子メール プロファイルの一部として構成されます)。  

    -   **ID 証明書:** **[選択]** をクリックし、ID として使用する証明書を選択します。  

        > [!NOTE]  
        >  ID 証明書を選択する前に、それを Simple Certificate Enrollment Protocol (SCEP) の証明書プロファイルとして最初に構成する必要があります。 証明書プロファイルの詳細については、「[System Center Configuration Manager の証明書プロファイル](/sccm/protect/deploy-use/introduction-to-certificate-profiles)」を参照してください。  

         このオプションは、[ **認証方法** ] の下で [ **証明書**] を選択した場合にのみ利用できます。  

    -   **[S/MIME を使用する]** (iOS デバイスの場合のみ) - S/MIME 暗号化を使って電子メールを送信します。 次のオプションを選択します。

        -   **署名証明書:** **[選択]** をクリックし、署名に使用する証明書を選択します。 このオプションは iOS デバイスにのみ適用されます。  

            > [!NOTE]  
            >  署名証明書を選ぶ前に、それを Simple Certificate Enrollment Protocol (SCEP) または PFX の証明書プロファイルとして最初に構成する必要があります。 証明書プロファイルの詳細については、「[System Center Configuration Manager の証明書プロファイル](/sccm/protect/deploy-use/introduction-to-certificate-profiles)」を参照してください。  

        -   **暗号化証明書:** **[選択]** をクリックし、暗号化に使用する証明書を選択します。 このオプションは iOS デバイスにのみ適用されます。 暗号化証明書として使うことができるのは、PFX 証明書だけです。

        暗号化証明書と署名証明書の両方を選ぶ場合は、どちらも PFX 形式でなければなりません。

        > [!NOTE]  
        >  証明書を選ぶ前に、それを Simple Certificate Enrollment Protocol (SCEP) または PFX の証明書プロファイルとして最初に構成する必要があります。 証明書プロファイルの詳細については、「[System Center Configuration Manager の証明書プロファイル](/sccm/protect/deploy-use/introduction-to-certificate-profiles)」を参照してください。  




###   <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Exchange ActiveSync 電子メール プロファイルの同期設定を構成します。  

1.  Exchange ActiveSync 電子メール プロファイルの作成ウィザードの [ **同期設定の構成** ] ページで、次の情報を指定します。  

    -   **スケジュール:** デバイスが Exchange Server からデータを同期するスケジュールを選択します。 このオプションは Windows Phone デバイスにのみ適用できます。 次の中から選択します。  

        -   [**未設定** ] 同期スケジュールは強制されません。 独自の同期スケジュールを構成できます。  

        -   [**メッセージが到着したとき** ] 電子メールや予定表アイテムなどのデータが到着したとき、自動的に同期します。  

        -   **15 分** Data such as emails and calendar items will be automatically synchronized every 15 分.  

        -   **30 分** Data such as emails and calendar items will be automatically synchronized every 30 分.  

        -   **60 分** Data such as emails and calendar items will be automatically synchronized every 60 分.  

        -   [**手動** ] デバイス ユーザーが同期を手動で開始する必要があります。  

    -   **同期する電子メールの日数:** ドロップダウン リストから、同期する電子メールの日数を選択します。 次のいずれかの値を選択します。  

        -   [**未設定** ] 設定は強制されません。 デバイスに電子メールをダウンロードする程度を構成できます。  

        -   [**無制限** ] 使用可能なすべての電子メールを同期します。  

        -   **1 日**  

        -   **3 日間**  

        -   **1 週間**  

        -   **2 週間**  

        -   **1 か月**  

    -   [**他の電子メール アカウントにメッセージを移動することを許可する** ] デバイスで構成されている複数のアカウント間で電子メール メッセージを移動するには、このオプションを選択します。 このオプションは iOS デバイスにのみ適用されます。  

    -   [**サードパーティ製のアプリケーションから電子メールの送信を許可する** ] 既定ではないサード パーティ製の電子メール アプリケーションからの電子メール送信を許可するには、このオプションを選択します。 このオプションは iOS デバイスにのみ適用されます。  

    -   [**最近使用した電子メール アドレスを同期する** ] デバイスで最近使用された電子メール アドレスのリストを同期するには、このオプションを選択します。 このオプションは iOS デバイスにのみ適用されます。  

    -   [**SSL の使用** ] 電子メールの送受信と Exchange Server との通信に Secure Sockets Layer (SSL) 通信を使用するには、このオプションを選択します。  

    -   **同期するコンテンツの種類:** デバイスに同期するコンテンツの種類を選択します。 このオプションは Windows Phone デバイスにのみ適用できます。 次の中から選択します。  

        -   **電子メール**  

        -   **連絡先**  

        -   **カレンダー**  

        -   **タスク**  

###  <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Exchange ActiveSync 電子メール プロファイルにサポートされているプラットフォームを指定します。  

1.  Exchange ActiveSync 電子メール プロファイルの作成ウィザードの [ **サポートされているプラットフォーム** ] ページで、電子メール プロファイルをインストールするオペレーティング システムを選択します。使用できるすべてのオペレーティング システムに電子メール プロファイルをインストールするには、[ **すべて選択** ] をクリックします。  

2.  ウィザードを完了します。

Exchange ActiveSync 電子メール プロファイルを展開する方法については、「[How to Deploy Email Profiles in Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)」(System Center Configuration Manager でプロファイルを展開する方法) を参照してください。  

