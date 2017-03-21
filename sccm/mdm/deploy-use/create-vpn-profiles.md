---
title: "System Center Configuration Manager の VPN プロファイル | Microsoft Docs"
description: "System Center Configuration Manager のモバイル デバイスの VPN プロファイルです。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 32190ec39af2cf1568b3d57c2c2f25d9ff2f9e20
ms.lasthandoff: 03/06/2017

---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>System Center Configuration Manager のモバイル デバイスの VPN プロファイル

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の VPN プロファイルを使用して、VPN 設定を組織内のモバイル デバイス ユーザーに展開します。 これらの設定を展開して、企業ネットワーク上のリソースに接続するために必要なエンド ユーザーの作業を最小化します。  

 たとえば、iOS オペレーティング システムを実行するすべてのデバイスに対して、企業ネットワーク上のファイル共有に接続するために必要な設定をプロビジョニングできます。 企業ネットワークに接続するために必要な設定が含まれている VPN プロファイルを作成した後、階層内で iOS を実行するデバイスを持つすべてのユーザーにこのプロファイルを展開することができます。 iOS デバイスのユーザーに対して使用可能なネットワークの一覧で VPN 接続が表示されるため、最小限の作業でこのネットワークに接続できます。  

 VPN プロファイルを作成するときに、System Center Configuration Manager 証明書プロファイルを使用してプロビジョニングされた、サーバー検証用の証明書、クライアント認証用の証明書などの幅広いセキュリティ設定を含めることができます。 証明書プロファイルの詳細については、「[System Center Configuration Manager の証明書プロファイル](../../protect/deploy-use/introduction-to-certificate-profiles.md)」を参照してください。  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Configuration Manager と Intune を併用する場合の VPN プロファイル 
 
 プロファイルを iOS、Android、Windows Phone、Windows 8.1 の各デバイスに展開するには、これらのデバイスを Microsoft Intune に登録する必要があります。 その他のプラットフォームのデバイスも、Intune に登録できます。 登録方法については、「[Microsoft Intune を使用したモバイル デバイスの管理](https://technet.microsoft.com/en-us/library/dn646962.aspx)」を参照してください。 次の表は、各デバイス プラットフォームでサポートされている接続の種類を示しています。  

 |接続の種類|iOS および Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop および Mobile|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|○|○|いいえ|いいえ|いいえ|いいえ|はい (OMA-URI)|  
 |Pulse Secure|[はい]|[はい]|○|×|[はい]|[はい]|○|  
 |F5 Edge Client|[はい]|[はい]|○|×|[はい]|[はい]|○|  
 |Dell SonicWALL Mobile Connect|[はい]|[はい]|○|×|[はい]|[はい]|[はい]|  
 |チェック ポイント モバイル VPN|○|[はい]|○|×|[はい]|[はい]|○|  
 |Microsoft SSL (SSTP)|×|いいえ|[はい]|[はい]|○|いいえ|いいえ|  
 |Microsoft 自動|いいえ|いいえ|[はい]|[はい]|○|×|はい (OMA-URI)|  
 |IKEv2|はい (カスタム ポリシー)|いいえ|[はい]|[はい]|[はい]|○|はい (OMA-URI)|  
 |PPTP|○|×|[はい]|[はい]|○|×|はい (OMA-URI)|  
 |L2TP|[はい]|×|[はい]|[はい]|○|×|はい (OMA-URI)|  

## <a name="create-vpn-profiles"></a>VPN プロファイルの作成
VPN プロファイルの作成に関する一般情報は、「[System Center Configuration Manager で VPN プロファイルを作成する方法](../../protect/deploy-use/create-vpn-profiles.md)」を参照してください。

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

         ![VPN に条件付きアクセスを構成する](media/vpn-conditional-access.png)


> [!NOTE]  
> 認証方法によっては、**[構成]** をクリックして Windows のプロパティ ダイアログ ボックスを開くことができます (Configuration Manager コンソールを実行している Windows のバージョンで、この認証方法がサポートされている場合)。そこで、認証方法のプロパティを構成できます。  


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


**展開:** VPN プロファイルの展開については、[Wi-Fi、VPN、電子メール、および証明書プロファイルの展開](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)に関する記事を参照してください。

### <a name="next-steps"></a>次のステップ  
 Configuration Managerで VPN プロファイルの計画、構成、操作、およびメンテナンスを行うときに、次のトピックを参考にしてください。  

-   [System Center Configuration Manager の VPN プロファイルの前提条件](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [System Center Configuration Manager の VPN プロファイルのセキュリティとプライバシー](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
