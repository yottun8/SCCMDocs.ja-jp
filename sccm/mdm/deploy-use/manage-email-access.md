---
title: 電子メールへのアクセスの管理
titleSuffix: Configuration Manager
description: Configuration Manager 条件付きアクセスを使用して、Exchange 電子メールへのアクセスを管理する方法について説明します。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f976b63b4580b5df9c6e609ff6b361538860c41c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137645"
---
# <a name="manage-email-access-in-configuration-manager"></a>Configuration Manager での電子メール アクセスを管理します。

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

指定した条件に基づいて Exchange 電子メールへのアクセスを管理する条件付きアクセスを構成マネージャーを使用します。  

以下のものへのアクセスを管理できます。  

- Microsoft Exchange On-premises  

- Microsoft Exchange Online  

- Exchange Online Dedicated  

次のプラットフォームでは、組み込みの電子メール クライアントから Exchange Online と Exchange On-premises へのアクセスを制御できます。  

- Android 4.0 以降、Samsung KNOX Standard 4.0 以降  

- iOS 9.0 以降  

- Windows Phone 8.1 以降  

- Windows 8.1 以降でのメール アプリケーション  

以下を実行している PC で、Office デスクトップ アプリケーションから Exchange Online にアクセスできます。  

- [最新の認証](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) が有効にされた Office デスクトップ 2013 以降。  

- Windows 7.0 または Windows 8.1  

> [!NOTE]  
> Pc をドメインに参加しているまたは、Intune で設定されたポリシーに対応します。  


## <a name="device-requirements"></a>デバイスの要件
条件付きアクセスを構成すると、ユーザーが電子メールに接続するには、使用するデバイスが以下の条件を満たさなくてはならなくなります。  

- Intune に登録されているか、ドメインに参加する PC である。  

- デバイスが Azure Active Directory に登録されている (デバイスが Intune に登録されている場合は、自動的に登録されます) (Exchange Online のみ)。 また、クライアントの Exchange ActiveSync ID が Azure Active Directory に登録されている必要があります (Exchange On-premises に接続している Windows および Windows Phone デバイスには該当しません)。  

    ドメインに参加している PC の場合、Azure Active Directory に自動的に登録するように設定する必要があります。 **Pc の条件付きアクセス**セクション、[サービスへのアクセスを管理](../../protect/deploy-use/manage-access-to-services.md)記事には、Pc の条件付きアクセスを有効にするための要件の完全なセットが一覧表示されます。  

- そのデバイスに展開されているすべての Configuration Manager コンプライアンス ポリシーを遵守している。  

    条件付きアクセス条件が満たされない場合にログインするときに、次のメッセージのいずれかで、ユーザーが表示されます。  

- デバイスが Intune に登録されていないか、Azure Active Directory に登録されていない場合、ポータル サイト アプリをインストール、デバイスの登録 (Android および iOS デバイス用)、電子メールで、関連付けるをアクティブ化する方法についての指示と共に、メッセージが表示されます、。デバイスの Exchange ActiveSync ID と Azure Active Directory 内のデバイス レコード。  

- デバイスが準拠していない場合は、問題に関する情報とその修復方法を確認できます、Intune web ポータルにユーザーを誘導するメッセージが表示されます。  

#### <a name="for-mobile-devices"></a>モバイル デバイスの場合

**iOS** および **Android** デバイスのブラウザーからアクセスされるときの Exchange Online 上の **Outlook Web Access (OWA)** へのアクセスを制限することができます。 準拠デバイスでの、サポートされる以下のブラウザーからのアクセスのみ許可されます。  

- Safari (iOS)  
- Chrome (Android)  
- 管理対象ブラウザー (iOS と Android)  

サポートされていないブラウザーはブロックされます。 IOS および Android 用の OWA アプリはサポートされていません。 ADFS 要求規則を介してこれらをブロックする必要があります。  

- 最新ではない認証プロトコルをブロックするように ADFS 要求規則を設定します。 シナリオ 3 で詳細な手順が提供されている[O365 にブラウザー ベースのアプリケーションを除くすべてのアクセスをブロック](https://technet.microsoft.com/library/dn592182.aspx)します。  

#### <a name="for-pcs"></a>Pc の

- 条件付きアクセス ポリシーの要件が **[ドメインに参加する]** または **[準拠]** を許可することである場合、デバイスを登録する方法についての手順が示されているメッセージが表示されます。 PC がどちらの要件も満たさない場合、ユーザーはデバイスを Intune に登録するように求められます。  

- 条件付きアクセス ポリシーの要件がドメインに参加している Windows デバイスのみを許可するように設定されている場合は、デバイスはブロックされ、IT 管理者に問い合わせるようにメッセージが表示されます。  

Exchange ActiveSync 電子メール クライアントを組み込まれた、以下のプラットフォームのデバイスから Exchange 電子メールへのアクセスをブロックできます。  

- Android 4.0 以降、Samsung KNOX Standard 4.0 以降  

- iOS 9.0 以降  

- Windows Phone 8.1 以降  

- Windows 8.1 以降での **メール** アプリケーション  

iOS と Android 用の Outlook アプリ、Outlook デスクトップ 2013 以上がサポートされるのは、Exchange Online のみです。  

条件付きアクセスが機能するには、Configuration Manager と Exchange 間に **On-Premises Exchange Connector** が必要です。  

Configuration Manager コンソールから、Exchange On-premises の条件付きアクセス ポリシーを構成できます。 Exchange Online 用の条件付きアクセス ポリシーを構成する場合、Configuration Manager コンソールでプロセスを開始できます。これにより、Intune コンソールが起動し、そこでプロセスを完了することができます。  



## <a name="configure-conditional-access"></a>条件付きアクセスの構成

### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>手順 1:条件付きアクセス ポリシーの効果を評価します。  

構成した後、**オンプレミス Exchange connector**、Configuration Manager を使用することができます**条件付きアクセス状態ごとのデバイスの一覧**がブロックされるデバイスを識別するためにレポート条件付きアクセス ポリシーを構成した後、Exchange にアクセスします。 このレポートには以下も必要です。  

- Intune のサブスクリプション  

- サービス接続ポイントを構成して配置する必要があります。  

レポート パラメーターで、評価する Intune グループを選び、必要に応じて、ポリシーを適用するデバイス プラットフォームを選びます。  

レポートの実行方法の詳細については、「 [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting)」を参照してください。  

レポートを実行した後、ユーザーをブロックするかどうかを判断するために、次の 4 つの列を調べます。  

- **管理チャネル**:デバイスは、Intune、Exchange ActiveSync、またはその両方によって管理されます。  

- **AAD に登録されている**:Azure Active Directory (社内参加と呼ばれます) とデバイスが登録されます。  

- **対応**: デバイスがデプロイしたすべてのコンプライアンス ポリシーに準拠します。  

- **EAS アクティブ化**: iOS および Android デバイスが、Exchange ActiveSync ID が Azure Active Directory でのデバイス登録レコードに関連付けられているが必要です。 これは、ユーザーが検疫電子メールで **[電子メールのアクティブ化]** のリンクをクリックしたときに発生します。  

    > [!NOTE]  
    > Windows Phone デバイスは、常にこの列の値を表示します。  

対象グループまたはコレクションの一部であるデバイスは、列の値が以下の表に示されている値と一致しない限り、Exchange にアクセスできないようにブロックされます。  

|[管理チャネル]|AAD に登録済み|[準拠]|[EAS アクティブ化]|結果の動作|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**Microsoft Intune および Exchange ActiveSync による管理の対象**|はい|はい|**[はい]** または **[いいえ]** が表示されます|電子メール アクセスが許可される|  
|その他の値|いいえ|いいえ|値が表示されない|電子メール アクセスがブロックされる|  

レポートの内容をエクスポートし、 **[電子メール アドレス]** 列を使って、ブロックされることをユーザーに通知できます。  


### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>手順 2:ユーザー グループまたはコレクションを条件付きアクセス ポリシーを構成します。  

条件付きアクセス ポリシーは、ポリシーの種類に応じて、さまざまなユーザーのグループまたはコレクションを対象とします。 これらのグループには、ポリシーの対象となるユーザーや、ポリシーから除外されるユーザーが含まれます。 ユーザーがポリシーの対象となる場合、ユーザーに使用される各デバイスが電子メールにアクセスするには、ポリシーを遵守している必要があります。  

- **Exchange Online ポリシー**: Azure Active Directory セキュリティ ユーザー グループにします。 これらのグループは、 **Office 365 管理センター**または **Intune アカウント ポータル**で構成できます。  

- **Exchange on-premises ポリシー**: Configuration Manager ユーザー コレクションにします。 **[資産とコンプライアンス]** ワークスペースでこれらを構成できます。  

各ポリシーには、次の 2 つのグループの種類を指定できます。  

- **対象グループ**:ポリシーを適用するユーザー グループまたはコレクション  

- **例外グループ**:ユーザー グループまたは (省略可能) のポリシーから除外されるコレクション  

ユーザーが両方に含まれている場合は、ポリシーから除外されます。  

条件付きアクセス ポリシーの対象となるグループまたはコレクションだけが、Exchange アクセスのために評価されます。  


### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>手順 3:構成し、コンプライアンス ポリシーの展開  

コンプライアンス ポリシーを作成し、Exchange 条件付きアクセス ポリシーの対象となるすべてのデバイスに展開したことを確認します。  

コンプライアンス ポリシーを構成する方法の詳細については、[デバイス コンプライアンス ポリシーの管理](device-compliance-policies.md)に関するページを参照してください。  

> [!IMPORTANT]  
> コンプライアンス ポリシーを展開していないし、Exchange 条件付きアクセス ポリシーを有効にすると場合、すべての対象デバイスには、アクセスが許可されます。  


### <a name="step-4-configure-the-conditional-access-policy"></a>手順 4:条件付きアクセス ポリシーを構成します。  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>Exchange Online (および新しい Exchange Online Dedicated 環境のテナント) の場合

> [!NOTE]  
> Azure AD 管理コンソールで条件付きアクセス ポリシーを作成することもできます。 Azure AD の管理コンソールでは、Intune デバイス条件付きアクセス ポリシー (Azure AD のデバイスベースの条件付きアクセス ポリシーと呼ぶ) に加えて、多要素認証のような他の条件付きアクセス ポリシーを作成することができます。 また、Salesforce や Box など、Azure AD がサポートするサード パーティ製エンタープライズ アプリ用の条件付きアクセス ポリシーを設定することもできます。 詳細については、次を参照してください[How To:。条件付きアクセスのクラウド アプリへのアクセスの管理対象デバイスを必要と](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)します。  

Exchange Online の条件付きアクセス ポリシーは、次のフローを使用して、デバイスを許可するかブロックするかを評価します。  

![条件付きアクセス フロー](media/ConditionalAccess8-1.png)  

電子メールにアクセスするには、デバイスは以下の条件を満たす必要があります。  

- Intune に登録する。  

- Pc のドメインに参加しているか、Intune で設定されたポリシーで、登録されており準拠している必要があります。  

- Azure AD でデバイスを登録します。 デバイスが Intune で登録されている場合に自動的に発生します。 ドメインに参加する Pc、する必要がありますに設定する最大[自動的にデバイスを登録](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-manual-steps)と Azure AD。  

- アクティブ化された電子メールがある。これによって、デバイスの Exchange ActiveSync ID が Azure Active Directory のデバイス レコードに関連付けられます (iOS および Android デバイスのみに適用)。  

- 展開されているすべてのコンプライアンス ポリシーを遵守している。  

デバイスの状態は Azure Active Directory に格納され、条件の評価に基づいて、電子メールへのアクセスが許可されたりブロックされたりします。  

条件が満たされない場合にサインインしたときに、次のメッセージのいずれか、ユーザーが表示されます。  

- デバイスは登録されていないか、Azure AD に登録されている場合、ポータル サイト アプリをインストールして登録する方法についての指示と共に、メッセージが表示されます。  

- デバイスが準拠していない場合は、問題に関する情報とその修復方法を確認できます、Intune ポータル サイト web サイトまたはポータル サイト アプリにユーザーを誘導するメッセージが表示されます。  

- PC の場合:  

    - ドメインへの参加を要求するポリシーを設定し、PC がドメインに参加している場合、IT 管理者にお問い合わせに、メッセージが表示されます。  

    - ドメインへの参加を要求するポリシーが設定されている場合、または対応と、PC がいずれかの要件を満たしていない、ポータル サイト アプリをインストールして登録する方法についての指示と共にメッセージが表示されます。  

メッセージは、新しい Exchange Online Dedicated 環境の Exchange Online ユーザーおよびテナントのデバイスに表示され、Exchange On-premises および従来の Exchange Online Dedicated デバイスのユーザー受信トレイに配信されます。  

> [!NOTE]  
> Configuration Manager 条件付きアクセス規則は、Exchange Online 管理コンソールで定義された規則をオーバーライド、許可、ブロック、および検疫します。  
> 
> 条件付きアクセス ポリシーは、Intune コンソールで構成する必要があります。 Intune コンソールに Configuration Manager を介してアクセスし、次の手順を開始します。 メッセージが表示されたら、Configuration Manager と Intune 間のサービス接続ポイントを設定するために使用された同じ資格情報を使用してサインインします。  

##### <a name="to-enable-the-exchange-online-policy"></a>Exchange Online ポリシーを有効にするには  

1. Configuration Manager コンソールで選択**資産とコンプライアンス**します。  

2. 展開**コンプライアンス設定**、展開**条件付きアクセス**、し、 **Exchange Online**します。  

3. **ホーム**] タブで、**リンク**グループで、[ **Intune コンソールで条件付きアクセス ポリシーを構成する**します。 Configuration Manager を Intune サービスの全体管理者と結び付けるために使用したアカウントのユーザー名とパスワードの入力が必要になる場合があります。 Intune 管理コンソールが開きます。  

4. Microsoft Intune ポータルで選択**ポリシー** > **条件付きアクセス** > **Exchange Online ポリシー**します。  

    ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5. **[Exchange Online ポリシー]** ページで、 **[Exchange Online の条件付きアクセス ポリシーを有効にする]** を選択します。 これをチェックする場合、デバイスは準拠している必要があります。 これを確認しない場合、条件付きアクセスは適用されません。  

    > [!NOTE]  
    > コンプライアンス ポリシーを展開していないし、Exchange Online ポリシーを有効にすると場合、すべての対象デバイスは準拠として報告されます。  
   >   
   >  コンプライアンスの状態に関係なく、ポリシーの対象となっているすべてのユーザーがデバイスを Intune に登録する必要があります。  

6. **アプリケーションへのアクセス**Outlook、およびその他のアプリを最新の認証を使用して、各プラットフォームの準拠デバイスのみにアクセスを制限する選択できます。 Windows デバイスはドメインに参加しているか、Intune に登録または準拠している必要があります。  

    > [!TIP]  
    > **先進認証** では、Active Directory Authentication Library (ADAL) ベースのサインインが Office クライアントに提供されます。  
    > 
    > - ADAL ベースの認証を使用すると、Office クライアントでブラウザー ベースの認証 (パッシブ認証とも呼ばれます) を利用できます。 認証する際に、ユーザーはサインイン Web ページに転送されます。  
    > - この新しいサインイン方法では、 **デバイスのコンプライアンス** と、 **多要素認証** が実行されたかどうかに基づいて、条件付きのアクセスなどの新しいシナリオを実現できます。  
    > 
    >  詳細については、「[Office 2013 クライアント アプリと Office 2016 クライアント アプリでの先進認証のしくみ](https://docs.microsoft.com/office365/enterprise/modern-auth-for-office-2013-and-2016)」を参照してください。  

    Configuration Manager と Intune と共に Exchange Online を使用すると、条件付きアクセスでモバイル デバイスだけではなく、デスクトップ コンピューターも管理できます。 Pc では、ドメインに参加しているいずれか、Intune で登録された準拠している必要があります。 以下の要件を設定できます。  

    - **デバイスはドメインに参加しているか準拠デバイスである必要があります。** Pc には、ドメインに参加しているか、ポリシーに準拠してあること。 場合は、PC には、これらの要件のいずれかを満たしていない、Intune でデバイスを登録する入力が求められます。  

    - **デバイスはドメインに参加している必要があります** Exchange Online へのアクセスにドメインに参加している Pc がある必要があります。 電子メールへのアクセスがブロックされているし、ユーザーが IT 管理者にお問い合わせするように求めの場合は、PC では、ドメインに参加していない場合は、  

    - **デバイスは準拠デバイスである必要があります** PC は Intune に登録および準拠している必要があります。 PC が登録されていない場合は、登録する方法については、メッセージが表示されます。  

7. **Outlook web access (OWA)**、サポートされているブラウザーを通じてのみ、Exchange Online へのアクセスを許可することもできます。Safari (iOS) および Chrome (Android)。 その他のブラウザーからのアクセスはブロックされます。 Outlook のアプリケーション アクセス用に選択した、同じプラットフォーム制限もここで適用されます。  

    - **Android** デバイスで、ユーザーはブラウザー アクセスを有効にする必要があります。 この操作には、ユーザー必要がありますように有効に登録されたデバイスに「ブラウザー アクセスを有効にする」オプション。  

        1. **ポータル サイト アプリ**を起動します。  

        2. トリプル ドット (...) またはハードウェアのメニュー ボタンから、 **[設定]** ページに移動します。  

        3. **[ブラウザー アクセスを有効にする]** ボタンを押します。  

        4. Chrome ブラウザーでは、Office 365 からサインアウトし、Chrome を再起動します。  

    - **IOS と Android**プラットフォーム、サービス、Azure AD へのアクセスに使用されるデバイスを識別するためには、デバイスに TLS 証明書を発行します。 デバイスでは、次のスクリーン ショットに示すように、証明書を選択するユーザーにプロンプトが証明書を表示します。 ユーザーは、ブラウザーを使用して続行する前に、この証明書を選択する必要があります。  

        - **iOS**  

        ![iPad での証明書プロンプトのスクリーンショット](media/mdm-browser-ca-ios-cert-prompt_v2.png)  

        - **Outlook Web Access (OWA)**  

        ![Android デバイスでの証明書プロンプトのスクリーンショット](media/mdm-browser-ca-android-cert-prompt.png)  

8. **[Exchange ActiveSync メール アプリ]** では、デバイスがポリシーに準拠していない場合にメールによる Exchange Online へのアクセスをブロックすることを選択できます。Intune がデバイスを管理できない場合にメールへのアクセスを許可またはブロックすることも選択できます。  

9. **[対象グループ]** で、ポリシーを適用するユーザーの Active Directory セキュリティ グループを選択します。  

    > [!NOTE]  
    > 対象となるグループ内にあるユーザーの場合、Intune のポリシーには Exchange のルールとポリシーを置き換えます。  
    > 
    > 次の場合にのみ、Exchange の許可、ブロック、検疫のルールと、Exchange のポリシーが適用されます。  
    > 
    > - ユーザーが Intune のライセンスを取得していない。  
    > - ユーザーに、Intune のライセンスが、ユーザーは、条件付きアクセス ポリシーの対象となるすべてのセキュリティ グループに属していません。  

10. **[例外グループ]** で、このポリシーから除外するユーザーの Active Directory セキュリティ グループを選択します。 ユーザーが対象となると、例外の両方のグループにある場合、ポリシーから除外されは自分の電子メールにアクセスします。  

11. 操作が完了したら、 **[保存]** をクリックします。  


このポリシーの詳細については、次のノートを確認してください。  

- 条件付きアクセス ポリシーを展開する必要はありません。すぐに有効になります。  

- ユーザーが電子メール アカウントを作成すると、デバイスはすぐにブロックされます。  

- ブロックされたユーザーがデバイスを Intune に登録すると (または非準拠を修復すると)、メールのアクセスは 2 分以内にブロック解除されます。  

- ユーザーがデバイスの登録を解除した場合、メールは約 6 時間後にブロックされます。  


### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>Exchange On-premises (および従来の Exchange Online Dedicated 環境のテナント) の場合  
従来の Exchange Online Dedicated 環境の Exchange On-premises およびテナントの条件付きアクセス ポリシーは、次のフローを使用して、デバイスを許可するかブロックするかを評価します。  

![ConditionalAccess8&#45;2](media/ConditionalAccess8-2.png)  

#### <a name="to-enable-the-exchange-on-premises-policy"></a>Exchange On-premises ポリシーを有効にするには  

1. Configuration Manager コンソールで選択**資産とコンプライアンス**します。  

2. 展開**コンプライアンス設定**、展開**条件付きアクセス**、し、 **、オンプレミスの Exchange**します。  

3. **ホーム**] タブで、 **、オンプレミスの Exchange**グループで、[**条件付きアクセス ポリシーを構成する**します。  

4. **全般**のページ、**条件付きアクセス ポリシーの構成ウィザード**、Exchange Active Sync の既定のルールを上書きするかどうかを指定します。 登録して、既定のルールがブロックまたは検疫に設定されている場合でも、電子メールへのアクセスを常が準拠しているデバイスにアクセスする場合は、このオプションを選択します。  

    > [!NOTE]  
    > Android デバイスの既定の上書きに関する問題があります。 Exchange サーバーの既定のアクセス ルールが **[ブロック]** に設定されていて、既定のルールのオーバーライドオプションと Exchange 条件付きアクセス ポリシーが有効である場合は、対象ユーザーの Android デバイスが Intune に登録されて準拠したとしても、デバイスのブロックが解除されない可能性があります。 この問題を回避するには、既定の Exchange アクセス ルールを **[検疫]** に設定します。 デバイスは既定では、Exchange へのアクセスを取得しないし、管理者は検疫されているデバイスの一覧で、Exchange サーバーからレポートを取得できます。  

    いない場合はセットアップ通知の電子メール アカウントに Exchange connector をセットアップするときに、このページで、警告が表示されます、**次**ボタンが無効になります。  続行するには、最初に Exchange Connector で通知の電子メール設定を構成してから、 **条件付きアクセス ポリシーの構成ウィザード** に戻って、プロセスを完了する必要があります。  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

5. **[対象コレクション]** ページで、1 つまたは複数のユーザー コレクションを追加します。 Exchange にアクセスするには、これらのコレクション内のユーザーは、Intune にデバイスを登録し、展開されたすべてのコンプライアンス ポリシーに準拠する必要があります。  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

6. **[除外コレクション]** ページで、条件付きアクセス ポリシーから除外するすべてのユーザー コレクションを追加します。 これらのグループ内のユーザー、必要がありますしないおよび Intune でデバイスを登録する必要はありません Exchange にアクセスするために、展開されたコンプライアンス ポリシーに準拠します。  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

    ユーザーが対象リストと例外リストの両方に属している場合、ユーザーは条件付きアクセス ポリシーから除外されます。  

7. **[ユーザー通知の編集]** ページで、Intune がデバイスのブロックを解除する方法についての指示と共にユーザーに送信するメールを構成します (Exchange が送信するメールに加えて)。  

    既定のメッセージを編集したり、テキストの表示方法を HTML タグで書式設定したりすることができます。 変更の予定を通知し、デバイスを登録する手順を説明するメールを事前に従業員に送信することもできます。  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    > 修復手順が記載されている Intune 通知電子メールはユーザーの Exchange 受信トレイに送信されるため、電子メール メッセージを受信する前にユーザーのデバイスがブロックされた場合は、ブロックされていないデバイスや、Exchange にアクセスするその他の方法を使用して、メッセージを表示できます。  
    > 
    > Exchange が通知電子メールを送信するためには、通知電子メールの送信に使用されるアカウントを構成します。 Exchange Server コネクタのプロパティを構成する場合に、これを実行します。  
    >   
    > 詳しくは、「[Configuration Manager と Exchange によるモバイル デバイスの管理](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)」をご覧ください。  

8. **概要** ページでの設定を確認して、ウィザードを完了します。  


このポリシーの詳細については、次のノートを確認してください。  

- 条件付きアクセス ポリシーを展開する必要はありません。すぐに有効になります。  

- ユーザーが、Exchange ActiveSync のプロファイルを設定 (Intune で管理されていない) 場合にブロックされるデバイスの 1 ~ 3 時間かかる場合があります。  

- ブロックされたユーザー、デバイスを Intune に登録 (または非準拠の問題を修正) 場合、電子メールへのアクセスはブロック解除されます 2 分以内です。  

- 場合、ユーザー解除-がブロックされるデバイスの 1 ~ 3 時間がかかる場合があります Intune から登録します。  


## <a name="see-also"></a>関連項目  

[サービスへのアクセスの管理](/sccm/protect/deploy-use/manage-access-to-services)
