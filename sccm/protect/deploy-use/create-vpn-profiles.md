---
title: "System Center Configuration Manager で VPN プロファイルを作成する方法 | Microsoft Docs"
description: "System Center Configuration Manager で VPN プロファイルを作成する方法を説明します。"
ms.custom: 
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: 15
author: nbigman
caps.handback.revision: 0
ms.author: nbigman
ms.manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8a5dc7361da34f3e6b926acd35c72c0c0767ce70
ms.openlocfilehash: 73b8d28deb6e2c57c92ead2f0fee4d7a2d92f5d4


---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager で VPN プロファイルを作成する方法

*適用対象: System Center Configuration Manager (Current Branch)*

さまざまなデバイス プラットフォームで使用可能な接続の種類については、「[System Center Configuration Manager の VPN プロファイル](../../protect/deploy-use/vpn-profiles.md)」を参照してください。  

サード パーティの VPN 接続の場合は、VPN プロファイルを展開する前に VPN アプリを配布します。 アプリを展開しないと、ユーザーが VPN に接続しようとしたときに、アプリを展開するように求められます。 アプリの展開方法については、「[System Center Configuration Manager でアプリケーションを展開する方法](../../apps/deploy-use/deploy-applications.md)」を参照してください。

### <a name="create-a-vpn-profile"></a>VPN プロファイルの作成   

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[会社のリソースへのアクセス]** > **[VPN プロファイル]** の順に選択します。  

3.  **[ホーム]** タブの **[作成]** グループで、**[VPN プロファイルの作成]** を選択します。  


1.  **[全般]** ページに入力します。 」を参照し、次のことに注意してください。  

    - VPN プロファイル名には、\\/:*?<>&#124; などの文字や空白文字は使用しないでください。 Windows Server VPN プロファイルでは、これらの文字はサポートされていません。  

     -   **[ファイルから既存の VPN プロファイルの項目をインポートする]** を選択し、XML ファイルにエクスポートされた VPN プロファイルの情報をインポートします (Windows 8.1 および Windows RT のみ)。  

1.  **[接続]** ページで、次のように指定します。  

    -   **接続の種類**: VPN 接続の種類を選択します。 次の表にある接続の種類から選択できます。  

    -   **サーバーの一覧**: VPN 接続に使用する新しいサーバーを追加します。 接続の種類によっては、1 つ以上の VPN サーバーを追加して、既定のサーバーを指定することもできます。  

        > [!NOTE]  
        >  iOS を実行するデバイスは、複数の VPN サーバーの使用をサポートしていません。 複数の VPN サーバーを構成して VPN プロファイルを iOS デバイスに展開すると、既定のサーバーだけが使用されます。  

     次の表に、接続の種類のオプションを示します。 詳細については、VPN サーバーのマニュアルを参照してください。  

    |オプション|説明|接続の種類|  
    |------------|----------------------|---------------------|  
    |**領域**|使用する認証領域です。 認証領域とは、"Pulse Secure" 接続の種類で使用される認証リソースのグループを表します。|Pulse Secure|  
    |**ロール**|この接続に対するアクセス権を持つユーザー ロールです。|Pulse Secure|  
    |**ログイン グループまたはドメイン**|接続するログイン グループまたはドメインの名前です。|Dell SonicWALL Mobile Connect|  
    |**指紋**|VPN サーバーが信頼できることを確認するために使用される文字列 ("Contoso 指紋コード" など) です。<br /><br /> 指紋:<br /><br /> - 指紋をクライアントに送信することにより、クライアントは、接続するときに同じ指紋を示すすべてのサーバーを信頼できます。<br /><br /> - デバイスにまだ指紋がない場合、指紋を表示すると共に、接続先の VPN サーバーを信頼するようにユーザーを促します (ユーザーは、手動で指紋を検証し、**[信頼する]** を選択して接続する必要があります)。|チェック ポイント モバイル VPN|  
    |**VPN 接続を介してすべてのネットワーク トラフィックを送信する**|このオプションが選択されていない場合、( **Microsoft SSL (SSTP)**、 **Microsoft Automatic**、 **IKEv2**、 **PPTP** 、および **L2TP** の各接続の種類に対して) 接続の追加のルートを指定することができます。これを分割または VPN のトンネリングといいます。<br /><br /> 企業ネットワークへの接続だけが VPN トンネル経由で送信されます。 インターネット上のリソースに接続するときは、VPN トンネリングは使用されません。|すべて|  
    |**接続専用 DNS サフィックス**|接続専用のドメイン ネーム システム (DNS) サフィックスです。|- <br />                            Microsoft SSL (SSTP)<br /><br /> - Microsoft 自動<br /><br /> - <br />                            IKEv2<br /><br /> - <br />                            PPTP<br /><br /> - <br />                            L2TP|  
    |**企業の Wi-Fi ネットワークに接続しているときは VPN をバイパスする**|デバイスが企業の Wi-Fi ネットワークに接続されている場合、VPN 接続は使用されません。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - チェック ポイント モバイル VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft 自動<br /><br /> - IKEv2<br /><br /> - L2TP|  
    |**家庭の Wi-Fi ネットワークに接続しているときは VPN をバイパスする**|デバイスが家庭の Wi-Fi ネットワークに接続されている場合、VPN 接続は使用されません。|すべて|  
    |**アプリ VPN ごと (iOS 7 以降、Mac OS X 10.9 以降)**|VPN 接続を iOS アプリに関連付けて、アプリを実行すると接続が開かれるようにします。 アプリを展開するときに VPN プロファイルをアプリに関連付けることができます。|- <br />                        Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - チェック ポイント モバイル VPN|  
    |**カスタム XML (省略可能)**|VPN 接続を構成するカスタムの XML コマンドを指定します。<br /><br /> 例:<br /><br /> **Pulse Secure**の場合:<br /><br /> **<pulse-schema><isSingleSignOnCredential\>true</isSingleSignOnCredential\></pulse-schema>**<br /><br /> **チェックポイント モバイル VPN**の場合:<br /><br /> **&lt;CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" /\>**<br /><br /> **Dell SonicWALL Mobile Connect**の場合:<br /><br /> **<MobileConnect\><Compression\>false</Compression\><debugLogging\>True</debugLogging\><packetCapture\>False</packetCapture\></MobileConnect\>**<br /><br /> **F5 Edge Client**の場合:<br /><br /> **&lt;f5-vpn-conf&gt;&lt;single-sign-on-credential /&gt;&lt;/f5-vpn-conf&gt;**<br /><br /> カスタムの XML コマンドの記述方法については、各製造元の VPN に関するマニュアルを参照してください。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - チェック ポイント モバイル VPN|  

    ###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Intune と Configuration Manager を使用するときに使用できる Windows 10 の VPN 機能  


    > [!NOTE]  
    > Windows 10 の VPN 機能を使用する VPN プロファイルの名前は、Unicode にしたり、特殊文字を含めたりすることはできません。


    |オプション|説明|接続の種類|  
    |------------|----------------------|---------------------|  
    |**企業の Wi-Fi ネットワークに接続しているときは VPN をバイパスする**|デバイスが企業の Wi-Fi ネットワークに接続されている場合、VPN 接続は使用されません。 デバイスが会社のネットワークに接続されているかどうかを判断するために使用する、信頼されたネットワーク名を入力します。|すべて|  
    |**ネットワーク トラフィック規則**|VPN 接続に対して有効にするプロトコル、ローカルおよびリモートのポート、およびアドレス範囲を設定します。<br /><br /> **メモ:** ネットワーク トラフィック規則を作成しない場合は、すべてのプロトコル、ポート、およびアドレス範囲が有効になります。 規則を作成すると、その規則または追加の規則で指定したプロトコル、ポート、およびアドレス範囲だけが、VPN 接続で使用されます。|すべて|  
    |**ルート**|VPN 接続を使用するルートを指定します。 60 を超えるルートを作成すると、ポリシーが機能しなくなる場合があることに注意してください。 |すべて|  
    |**DNS サーバー**|接続の確立後に VPN 接続で使用する DNS サーバーを指定します。|すべて|  
    |**自動的に VPN に接続するアプリ**|自動的に VPN 接続を使用するアプリを追加したり、アプリのリストをインポートしたりすることができます。 アプリの種類によってアプリの識別子が決まります。 デスクトップ アプリの場合、アプリのファイル パスを提供します。 ユニバーサル アプリの場合、パッケージ ファミリ名 (PFN) を提供します。 アプリの PFN を検索する方法については、「[Find a package family name for per-app VPN](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md)」(アプリごとの VPN のパッケージ ファミリ名を検索する) を参照してください。 |すべて|

    > [!IMPORTANT]
    > アプリごとの VPN の構成で使用するためにコンパイルする関連付けられたアプリのすべてのリストをセキュリティで保護することをお勧めします。 承認されていないユーザーによって変更されたリストを、アプリごとの VPN のアプリのリストにインポートすると、アクセスが許可されていないアプリへの VPN アクセスを認証してしまう可能性があります。 アプリのリストをセキュリティで保護できる&1; つの方法は、アクセス制御リスト (ACL) を使用することです。


1.  ウィザードの **[認証方法]** ページで、次のように指定します。  

    -   **認証方法**: VPN 接続で使用する認証方法を選択します。 使用可能な方法は、この表に示されている接続の種類によって異なります。  

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

        -   **ログオンのたびにユーザーの資格情報を記憶する**: ユーザーが接続するたびに入力しなくても済むように、ユーザーの資格情報が記憶されます。  

        -   **クライアント認証用のクライアント証明書を選択** - 事前に作成した、VPN 接続の認証に使用するクライアント [SCEP 証明書](introduction-to-certificate-profiles.md)を選択します。   

            > [!NOTE]  
            >  iOS デバイスの場合、選択する SCEP プロファイルは VPN プロファイルに埋め込まれます。 その他のプラットフォームでは、証明書が存在しないか準拠していない場合に VPN プロファイルがインストールされないようにする適用規則が追加されます。  
            >   
            >  指定した SCEP 証明書が準拠していないか展開されていない場合、VPN プロファイルはデバイスにインストールされません。
            >  
            >  IOS を実行するデバイスは、接続種類が PPTP の場合に認証方法として RSA SecurID と MSCHAP v2のみをサポートします。 エラーの報告を回避するには、iOS を実行するデバイスに、個別に PPTP VPN プロファイルを展開します。  

        - **条件付きアクセス**
            - VPN に接続するデバイスについて、接続前に条件付きアクセスのコンプライアンスのためにテストするには、**[この VPN 接続に対して条件付きアクセスを有効にする]** をオンにします。 コンプライアンス ポリシーについては、「[Device compliance policies in System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md)」(System Center Configuration Manager でのデバイス コンプライアンス ポリシー) を参照してください。
            - デバイスのコンプライアンスのために VPN 認証証明書以外の証明書を選択するには、**[別の証明書でのシングル サインオン (SSO) を有効にする]** をオンにします。 このオプションをオンにする場合は、VPN クライアントを特定できる正しい証明書の **EKU** (コンマ区切りリスト) と**発行元ハッシュ**を指定します。

         - **[Windows Information Protection]** - 企業が管理する企業 ID を指定します。通常、これは組織のプライマリ ドメインです (*contoso.com* など)。 組織が使用している複数のドメインを指定するには、"|" 文字で区切ります。 たとえば、「*contoso.com|newcontoso.com*」と指定します。   
            Windows Information Protection については、「[Microsoft Intune を使用して Windows 情報保護 (WIP) ポリシーを作成する](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune)」を参照してください。   

         ![VPN に条件付きアクセスを構成する](../media/vpn-conditional-access.png)


        > [!NOTE]  
        >
        >認証方法によっては、**[構成]** をクリックして Windows のプロパティ ダイアログ ボックスを開くことができます (Configuration Manager コンソールを実行している Windows のバージョンで、この認証方法がサポートされている場合)。そこで、認証方法のプロパティを構成できます。  


1.  VPN 接続でプロキシ サーバーを使用する場合は、VPN プロファイルの作成ウィザード **** の [プロキシの設定 ****] ページで、[この VPN プロファイルのプロキシ設定の構成 **** ] チェック ボックスをオンにします。 次に、プロキシ サーバーの情報を指定します。 詳細については、Windows Server のドキュメントを参照してください。  

    > [!NOTE]  
    >  Windows 8.1 コンピューターでは、VPN とそのコンピューターを接続するまで、VPN プロファイルにプロキシ情報は表示されません。  


2. 詳細な DNS 設定を構成する (必要な場合)  
 **[自動 VPN 接続の構成]** ページで、次のように構成することができます。  

    -   **要求に応じて VPN を有効にする** - Windows Phone 8.1 デバイス用の DNS の詳細設定を構成する場合に使用します。 この設定は Windows Phone 8.1 デバイスのみに適用され、Windows Phone 8.1 デバイスに展開することになっている VPN プロファイルでのみ有効にします。

    -   DNS サフィックス リスト (Windows Phone 8.1 デバイスのみ) - VPN 接続を確立するドメインを構成します。 指定するドメインごとに、DNS サフィックス、DNS サーバーのアドレス、および次のいずれかのオンデマンド操作を追加します。  

        -   **確立しない** – VPN 接続を開くことはありません。  

        -   **必要に応じて確立する** – デバイスがリソースに接続する必要がある場合にのみ VPN 接続を開きます。  

        -   **常に確立する** – 常時 VPN 接続を開きます。  

    -   **結合** – [**信頼されたネットワーク一覧**] に構成した任意の DNS サフィックスをコピーします。  

    -   **信頼されたネットワーク一覧** (Windows Phone 8.1 デバイスのみ) - 各行に 1 つの DNS サフィックスを指定します。 デバイスが信頼されたネットワークにある場合、VPN 接続は開かれません。  

    -   **サフィックス検索一覧** (Windows Phone 8.1 デバイスのみ) - 各行に 1 つの DNS サフィックスを指定します。 短い名前を使用して Web サイトに接続するときに、各 DNS サフィックスが検索されます。  

     たとえば、 **domain1.contoso.com** と **domain2.contoso.com** の DNS サフィックスを指定した後、URL **http://mywebsite**にアクセスしたとします。 次のアドレスが検索されます。  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  Windows Phone 8.1 デバイスのみ  
    >   
    >  **[VPN 接続を介してすべてのネットワーク トラフィックを送信する]** オプションの選択がオンで、かつ VPN 接続が完全トンネリングを使用している場合、デバイスに最初にプロビジョニングされるプロファイルで、VPN 接続が自動的に開きます。 別のプロファイルで自動的に接続を開く場合は、そのプロファイルをデバイス上で既定のプロファイルに指定する必要があります。  
    >   
    >  **[VPN 接続を介してすべてのネットワーク トラフィックを送信する]** オプションの選択がオフで、かつ VPN 接続が分割トンネリングを使用している場合、VPN 接続は、ルート、または接続固有の DNS サフィックスを構成している場合に自動的に開きます。  


1. VPN プロファイルの作成ウィザード **** の [サポートされているプラットフォーム ****] ページで、VPN プロファイルをインストールするオペレーティング システムを選択します。使用できるすべてのオペレーティング システムに VPN プロファイルをインストールするには、[すべて選択 **** ] をクリックします。  

2. ウィザードを完了します。 新しい VPN プロファイルは、[資産とコンプライアンス **** ] ワークスペースの [VPN プロファイル **** ] ノードに表示されます。  

### <a name="next-steps"></a>次のステップ

- サード パーティの VPN 接続の場合は、VPN プロファイルを展開する前に VPN アプリを配布します。 アプリを展開しないと、ユーザーが VPN に接続しようとしたときに、アプリを展開するように求められます。 アプリの展開方法については、「[System Center Configuration Manager でアプリケーションを展開する方法](../../apps/deploy-use/deploy-applications.md)」を参照してください。

- 「[System Center Configuration Manager でのプロファイルの展開](deploy-wifi-vpn-email-cert-profiles.md)」に記載されているとおりに、VPN プロファイルを展開します。  



<!--HONumber=Dec16_HO5-->


