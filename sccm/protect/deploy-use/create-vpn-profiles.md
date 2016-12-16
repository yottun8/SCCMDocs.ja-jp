---
title: "System Center Configuration Manager で VPN プロファイルを作成する方法"
description: "System Center Configuration Manager で VPN プロファイルを作成する方法を説明します。"
ms.custom: na
ms.date: 10/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: 15
caps.handback.revision: 0
ms.author: nbigman
ms.manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a65de5feae2ff44f938ce8b7e3c8d23d560bb180
ms.openlocfilehash: bcea8676c163a8aba1bc7f3364fde52375f52429


---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager で VPN プロファイルを作成する方法

*適用対象: System Center Configuration Manager (Current Branch)*


> [!NOTE]  
>
> - 各デバイス プラットフォームの種類に対して利用可能な接続タイプの詳細については、「[System Center Configuration Manager の VPN プロファイル](../../protect/deploy-use/vpn-profiles.md)」を参照してください。  
> - サード パーティの VPN 接続の場合は、VPN プロファイルを展開する前に VPN アプリを配布します。 アプリを展開しないと、ユーザーが VPN に接続しようとしたときに、アプリを展開するように求められます。 アプリの展開方法については、「[System Center Configuration Manager でアプリケーションを展開する方法](../../apps/deploy-use/deploy-applications)」を参照してください。

### <a name="start-the-create-vpn-profile-wizard"></a>VPN プロファイルの作成ウィザードを開始する  

1.  System Center Configuration Manager コンソールで、[**資産とコンプライアンス**] をクリックします。  

2.  System Center Configuration Manager コンソールの [**資産とコンプライアンス**] ワークスペースで、[**コンプライアンス設定**]、[**会社リソースのアクセス**] の順に展開してから、[**VPN プロファイル**] をクリックします。  

3.  [ホーム **** ] タブの [作成 **** ] グループで、[VPN プロファイルの作成 ****] をクリックします。  

### <a name="provide-general-information-about-the-vpn-profile"></a>VPN プロファイルに関する全般情報を指定する  

1.  VPN プロファイルの作成ウィザード **** の [全般 ****] ページで、次の情報を指定します。  

    -   **[名前]** - 一意の VPN プロファイル名を入力します (256 文字以内)。  

        > [!IMPORTANT]  
        >  VPN プロファイル名に \\/:*?<>&#124;, やスペースを含めないでください。これらの文字は、Windows Server VPN プロファイルでサポートされていません。  

    -   **説明**: System Center Configuration Manager コンソールでプロファイルを検索するのに役立つ説明を入力します (256 文字以内)。  

    -   **ファイルから既存の VPN プロファイルの項目をインポートする**: [**VPN プロファイルのインポート**] ページを表示するにはこのオプションを選択します。 このページでは、XML ファイルにエクスポート済みの Windows 8.1 と Windows RT オペレーティング システムの VPN プロファイル情報をインポートできます。  

### <a name="provide-connection-information-for-the-vpn-profile"></a>VPN プロファイルの接続情報を指定する  

1.  ウィザードの **[接続]** ページで、次の情報を指定します。  

    -   **接続タイプ:** ドロップダウン リストから、VPN 接続の種類を選択します。 サポートするプラットフォームを示す次の表にある接続の種類から選択できます。  

        > [!IMPORTANT]  
        >  デバイスに展開された VPN プロファイルを使用するには、事前に必要なサード パーティ製 VPN のアプリをインストールする必要があります。 「[System Center Configuration Manager でのアプリケーションの作成方法](../../apps/deploy-use/create-applications.md)」トピックの情報を参考にして、System Center Configuration Manager を使ってアプリを展開してください。  

    -   **サーバーの一覧:** **[追加]** をクリックして、VPN 接続に使用する新しいサーバーを追加します。 接続の種類によっては、1 つまたは複数の VPN サーバーを追加して、どのサーバーを既定のサーバーにするかを指定することもできます。  

        > [!NOTE]  
        >  iOS を実行するデバイスは、複数の VPN サーバーの使用をサポートしていません。 複数の VPN サーバーを構成して VPN プロファイルを iOS デバイスに展開すると、既定のサーバーだけが使用されます。  

     選択した接続の種類によっては、次の表にあるオプションが表示される場合があります。 詳細については、VPN サーバーのマニュアルを参照してください。  

    |オプション|説明|接続の種類|  
    |------------|----------------------|---------------------|  
    |**領域**|使用する認証領域の名前を指定します。 認証領域とは、"Pulse Secure" 接続の種類で使用される認証リソースのグループを表します。|Pulse Secure|  
    |**ロール**|この接続に対するアクセス権を持つユーザー ロールの名前を指定します。|Pulse Secure|  
    |**ログイン グループまたはドメイン**|接続するログイン グループまたはドメインの名前を指定します。|Dell SonicWALL Mobile Connect|  
    |**指紋**|VPN サーバーが信頼できることを確認するために使用する文字列を指定します (たとえば、"Contoso 指紋コード")。<br /><br /> 指紋:<br /><br /> - 指紋をクライアントに送信することにより、クライアントは、接続するときに同じ指紋を示すすべてのサーバーを信頼できます。<br /><br /> - デバイスが指紋を持たない場合、デバイスは、指紋を表示すると共に、接続先の VPN サーバーを信頼するようにユーザーを促します (ユーザーは、手動で指紋を検証し、[信頼する] をクリックして接続する必要があります)。|チェック ポイント モバイル VPN|  
    |**VPN 接続を介してすべてのネットワーク トラフィックを送信する**|このオプションが選択されていない場合、( **Microsoft SSL (SSTP)**、 **Microsoft Automatic**、 **IKEv2**、 **PPTP** 、および **L2TP** の各接続の種類に対して) 接続の追加のルートを指定することができます。これを分割または VPN のトンネリングといいます。<br /><br /> 企業ネットワークへの接続だけが VPN トンネル経由で送信されます。 インターネット上のリソースに接続するときは、VPN トンネリングは使用されません。|すべて|  
    |**接続専用 DNS サフィックス**|必要に応じて、接続に固有のドメイン ネーム システム (DNS) サフィックスを指定します。|- <br />                            Microsoft SSL (SSTP)<br /><br /> - Microsoft 自動<br /><br /> - <br />                            IKEv2<br /><br /> - <br />                            PPTP<br /><br /> - <br />                            L2TP|  
    |**企業の Wi-Fi ネットワークに接続しているときは VPN をバイパスする**|デバイスが企業の Wi-Fi ネットワークに接続しているときは VPN 接続を使用しないことを指定します。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - チェック ポイント モバイル VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft 自動<br /><br /> - IKEv2<br /><br /> - L2TP|  
    |**家庭の Wi-Fi ネットワークに接続しているときは VPN をバイパスする**|デバイスが家庭の Wi-Fi ネットワークに接続しているときは VPN 接続を使用しないことを指定します。|すべて|  
    |**アプリ VPN ごと (iOS 7 以降、Mac OS X 10.9 以降)**|VPN 接続を iOS アプリに関連付けて、アプリを実行すると接続が開かれるようにする場合は、このオプションを選択します。 アプリを展開するときに VPN プロファイルをアプリに関連付けることができます。|- <br />                        Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - チェック ポイント モバイル VPN|  
    |**カスタム XML (省略可能)**|VPN 接続を構成するカスタムの XML コマンドを指定することができます。<br /><br /> 次に例を示します。<br /><br /> **Pulse Secure**の場合:<br /><br /> **<pulse-schema><isSingleSignOnCredential\>true</isSingleSignOnCredential\></pulse-schema>**<br /><br /> **チェックポイント モバイル VPN**の場合:<br /><br /> **&lt;CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" /\>**<br /><br /> **Dell SonicWALL Mobile Connect**の場合:<br /><br /> **<MobileConnect\><Compression\>false</Compression\><debugLogging\>True</debugLogging\><packetCapture\>False</packetCapture\></MobileConnect\>**<br /><br /> **F5 Edge Client**の場合:<br /><br /> **&lt;f5-vpn-conf&gt;&lt;single-sign-on-credential /&gt;&lt;/f5-vpn-conf&gt;**<br /><br /> カスタムの XML コマンドの記述方法については、各製造元の VPN に関するマニュアルを参照してください。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - チェック ポイント モバイル VPN|  

####   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Intune と Configuration Manager を使用するときに使用できる Windows 10 の VPN 機能  


> [!NOTE]  
> Windows 10 の VPN 機能を使用する VPN プロファイルの名前は、Unicode にしたり、特殊文字を含めたりすることはできません。


|オプション|説明|接続の種類|  
|------------|----------------------|---------------------|  
|**企業の Wi-Fi ネットワークに接続しているときは VPN をバイパスする**|デバイスが企業の Wi-Fi ネットワークに接続しているときは VPN 接続を使用しないことを指定します。 デバイスが会社のネットワークに接続されているかどうかを判断するために使用する信頼されたネットワーク名を入力します。|すべて|  
|**ネットワーク トラフィック規則**|VPN 接続に対して有効にするプロトコル、ローカルおよびリモートのポート、およびアドレス範囲を設定します。<br /><br /> **メモ:** ネットワーク トラフィック規則を作成しない場合は、すべてのプロトコル、ポート、およびアドレス範囲が有効になります。 規則を作成すると、その規則または追加の規則で指定したプロトコル、ポート、およびアドレス範囲だけが、VPN 接続で使用されます。|すべて|  
|**ルート**|VPN 接続を使用するルートを指定します。 60 を超えるルートを作成すると、ポリシーが機能しなくなる場合があることに注意してください。 |すべて|  
|**DNS サーバー**|接続の確立後に VPN 接続で使用する DNS サーバーを指定します。|すべて|  
|**自動的に VPN に接続するアプリ**|自動的に VPN 接続を使用するアプリを追加したり、アプリのリストをインポートしたりすることができます。 アプリの種類によってアプリの識別子が決まります。 デスクトップ アプリの場合、アプリのファイル パスを提供します。 ユニバーサル アプリの場合、パッケージ ファミリ名 (PFN) を提供します。 アプリの PFN を検索する方法については、「[Find a package family name for per-app VPN](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md)」(アプリごとの VPN のパッケージ ファミリ名を検索する) を参照してください。 |すべて|

> [!IMPORTANT]
> アプリごとの VPN の構成で使用するためにコンパイルする関連付けられたアプリのすべてのリストをセキュリティで保護することをお勧めします。 承認されていないユーザーによって変更されたリストを、アプリごとの VPN のアプリのリストにインポートすると、アクセスが許可されていないアプリへの VPN アクセスを認証してしまう可能性があります。 アプリのリストをセキュリティで保護できる 1 つの方法は、アクセス制御リスト (ACL) を使用することです。


### <a name="configure-the-authentication-method-for-the-vpn-profile"></a>VPN プロファイルの認証方法を構成する  

1.  ウィザードの **[認証方法]** ページで、次の情報を指定します。  

    -   **認証方法:** ドロップダウン リストから、VPN 接続で使用する認証方法を選択します。 ドロップダウン リストに表示される項目は、前の手順で選択した接続の種類によって異なります。 次の表に、使用できる認証方法とサポートされている接続の種類を示します。  

        |[認証方法]|サポートされる接続の種類|  
        |---------------------------|--------------------------------|  
        |**証明書**<br /><br /> **メモ:** RADIUS サーバー (ネットワーク ポリシー サーバーなど) への認証にクライアント証明書を使用する場合は、証明書のサブジェクトの別名をユーザー プリンシパル名に設定する必要があります。|- <br />                            Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - チェック ポイント モバイル VPN|  
        |**ユーザー名とパスワード**|- <br />                            Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - チェック ポイント モバイル VPN|  
        |**Microsoft EAP-TTLS**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft 自動<br /><br /> - PPTP<br /><br /> - IKEv2<br /><br /> - L2TP|  
        |**Microsoft 保護された EAP (PEAP)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft 自動<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Microsoft セキュリティで保護されたパスワード (EAP-MSCHAP v2)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft 自動<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**スマート カードまたはその他の証明書**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft 自動<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**MSCHAP v2**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft 自動<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**RSA SecurID** (iOS のみ)|- Microsoft SSL (SSTP)<br /><br /> - Microsoft 自動<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**コンピューターの証明書を使う**|IKEv2|  

         選択したオプションに応じて、次のような詳細情報の指定を求められることがあります。  

        -   **ログオンごとにユーザーの資格情報を記憶**:ユーザーの資格情報を記憶し、接続が確立されるたびにユーザーが資格情報を入力する必要を省くには、このオプションを選択します。  

        -   **クライアント認証用のクライアント証明書を選択** - 事前に作成した、VPN 接続の認証に使用するクライアント SCEP 証明書を選択します。 System Center Configuration Manager で証明書プロファイルを使用する方法の詳細については、「[System Center Configuration Manager の証明書プロファイル](introduction-to-certificate-profiles.md)」を参照してください。  

            > [!NOTE]  
            >  iOS デバイスの場合、選択する SCEP プロファイルは VPN プロファイルに埋め込まれます。 その他のプラットフォームでは、証明書が存在しないか準拠していない場合に VPN プロファイルがインストールされないようにする適用規則が追加されます。  
            >   
            >  指定した SCEP 証明書が準拠していないか展開されていない場合、VPN プロファイルはデバイスにインストールされません。
            >  
            >  IOS を実行するデバイスは、接続種類が PPTP の場合に認証方法として RSA SecurID と MSCHAP v2のみをサポートします。 エラーの報告を回避するには、iOS を実行するデバイスに、個別に PPTP VPN プロファイルを展開します。  

               - Intune なしで Configuration Manager を使用する場合にのみサポートされる [**条件付きアクセス**] と [**エンタープライズ データ保護のプライマリ ドメイン**] の設定は、[**詳細**] を選ぶとアクセスできます。 エンタープライズ データ保護については、「[Microsoft Intune を使用して Windows 情報保護 (WIP) ポリシーを作成する](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune)」を参照してください。
        
        ![VPN に条件付きアクセスを構成する](../media/vpn-conditional-access.png)

        -   認証方法によっては、[**構成**] をクリックして [Windows のプロパティ] ダイアログ ボックスを開きます (System Center Configuration Manager コンソールを実行している Windows のバージョンがこの認証方法をサポートしている場合)。ここで、ユーザーは認証方法のプロパティを構成できます。  

### <a name="configure-proxy-settings-for-the-vpn-profile"></a>VPN プロファイルのプロキシ設定を構成する  

1.  VPN 接続でプロキシ サーバーを使用する場合は、VPN プロファイルの作成ウィザード **** の [プロキシの設定 ****] ページで、[この VPN プロファイルのプロキシ設定の構成 **** ] チェック ボックスをオンにします。  

2.  プロキシ サーバーとその設定について詳細を指定します。 詳細については、Windows Server のドキュメントを参照してください。  

> [!NOTE]  
>  Windows 8.1 コンピューターでは、VPN とそのコンピューターを接続するまで、VPN プロファイルにプロキシ情報は表示されません。  


### <a name="configure-further-dns-settings-if-required"></a>詳細な DNS 設定を構成する (必要な場合)  
 ウィザードの **[自動 VPN 接続の構成]** ページで、次の設定を構成することができます。  

-   **要求に応じて VPN を有効にする** - Windows Phone 8.1 デバイス用のウィザードのこのページで DNS の詳細設定を構成する場合は、このオプションを選択します。

> [!Note]  
> この設定は Windows Phone 8.1 デバイスのみに適用され、Windows Phone 8.1 デバイスに展開することになっている VPN プロファイルでのみ有効にします。


-   DNS サフィックス リスト (Windows Phone 8.1 デバイスのみ) - VPN 接続を確立するドメインを構成します。 指定するドメインごとに、DNS サフィックス、DNS サーバーのアドレス、および次のいずれかのオンデマンド操作を追加します。  

    -   **確立しない** – VPN 接続を開くことはありません。  

    -   **必要に応じて確立する** – デバイスがリソースに接続する必要がある場合にのみ VPN 接続を開きます。  

    -   **常に確立する** – 常時 VPN 接続を開きます。  

-   **結合** – [**信頼されたネットワーク一覧**] に構成した任意の DNS サフィックスをコピーします。  

-   **信頼されたネットワーク一覧** (Windows Phone 8.1 デバイスのみ) – 各行に 1 つの DNS サフィックスを指定します。 デバイスが信頼されたネットワークにある場合、VPN 接続は開かれません。  

-   **サフィックス検索一覧** (Windows Phone 8.1 デバイスのみ) – 各行に 1 つの DNS サフィックスを指定します。 短い名前を使用して Web サイトに接続するときに、指定した各 DNS サフィックスが検索されます。  

     たとえば、 **domain1.contoso.com** と **domain2.contoso.com** の DNS サフィックスを指定した後、URL **http://mywebsite**にアクセスしたとします。 次のアドレスが検索されます。  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

> [!NOTE]  
>  Windows Phone 8.1 デバイスのみ  
>   
>  **[VPN 接続を介してすべてのネットワーク トラフィックを送信する]** オプションの選択がオンで、かつ VPN 接続が完全トンネリングを使用している場合、デバイスに最初にプロビジョニングされるプロファイルで、VPN 接続が自動的に開きます。 別のプロファイルで自動的に接続を開く場合は、そのプロファイルをデバイス上で既定のプロファイルに指定する必要があります。  
>   
>  **[VPN 接続を介してすべてのネットワーク トラフィックを送信する]** オプションの選択がオフで、かつ VPN 接続が分割トンネリングを使用している場合、VPN 接続は、ルート、または接続固有の DNS サフィックスを構成している場合に自動的に開きます。  


### <a name="configure-supported-platforms-for-the-vpn-profile"></a>VPN プロファイルのサポートされるプラットフォームを構成する  
 サポートされるプラットフォームとは、VPN プロファイルがインストールされるオペレーティング システムのことです。  

VPN プロファイルの作成ウィザード **** の [サポートされているプラットフォーム ****] ページで、VPN プロファイルをインストールするオペレーティング システムを選択します。使用できるすべてのオペレーティング システムに VPN プロファイルをインストールするには、[すべて選択 **** ] をクリックします。  

### <a name="complete-the-wizard"></a>ウィザードを完了します。  
 このウィザードの [**概要**] ページで実行される操作を確認し、[**完了**] をクリックします。 新しい VPN プロファイルは、[資産とコンプライアンス **** ] ワークスペースの [VPN プロファイル **** ] ノードに表示されます。  

### <a name="next-steps"></a>次のステップ

- サード パーティの VPN 接続の場合は、VPN プロファイルを展開する前に VPN アプリを配布します。 アプリを展開しないと、ユーザーが VPN に接続しようとしたときに、アプリを展開するように求められます。 アプリの展開方法については、「[System Center Configuration Manager でアプリケーションを展開する方法](../../apps/deploy-use/deploy-applications)」を参照してください。

- 「[System Center Configuration Manager でのプロファイルの展開](deploy-wifi-vpn-email-cert-profiles.md)」に記載されているとおりに、VPN プロファイルを展開します。  



<!--HONumber=Nov16_HO1-->


