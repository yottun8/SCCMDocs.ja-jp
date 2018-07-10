---
title: VPN プロファイル
titleSuffix: Configuration Manager
description: Configuration Manager のモバイル デバイスの VPN プロファイルについて説明します。
ms.date: 06/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9409b6cc71ea238755f40baf75e6211c447b547f
ms.sourcegitcommit: 826e9ec385d6a1c1f3aa86ac202883154e0c1285
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2018
ms.locfileid: "37116498"
---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>System Center Configuration Manager のモバイル デバイスの VPN プロファイル

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager の VPN プロファイルを使用して、VPN 設定を組織内のモバイル デバイス ユーザーに展開します。 これらの設定を展開して、企業ネットワーク上のリソースに接続するために必要なエンド ユーザーの作業を最小化します。  

たとえば、すべての iOS デバイスを、企業ネットワーク上のファイル共有に接続するように設定します。 必要な接続の設定を含む VPN プロファイルを作成します。 次に、iOS デバイスを使用するすべてのユーザーにこのプロファイルを展開します。 VPN 接続は、これらのユーザーに、使用できるネットワークの一覧として表示されるので、ユーザーは少しの労力でこのネットワークに接続できます。  

VPN プロファイルを作成するときに、さまざまなセキュリティ設定を含めることができます。 たとえば、Configuration Manager の証明書プロファイルを使用してセットアップされたサーバー評価用の証明書とクライアント認証用の証明書を指定できます。 詳細については、「[Certificate profiles](../../protect/deploy-use/introduction-to-certificate-profiles.md)」 (証明書プロファイル) をご覧ください。  



## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Configuration Manager と Intune を併用する場合の VPN プロファイル

プロファイルを iOS、Android、Windows Phone、Windows 8.1 の各デバイスに展開するには、これらのデバイスを Microsoft Intune に登録する必要があります。 その他のプラットフォームのデバイスも、Intune に登録できます。 登録方法については、[Microsoft Intune でのデバイスの登録](/intune/device-enrollment)に関するページを参照してください。 

次の表は、各デバイス プラットフォームでサポートされている接続の種類を示しています。  

 |接続の種類|iOS と macOS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop および Mobile|  
 |---------------|---------------|-------|-----------|----------|--------------|-----------------|-----------------------------|  
 |Cisco AnyConnect|○<sup>1</sup>|はい|いいえ|いいえ|いいえ|いいえ|いいえ|
 |Cisco (IPSec)|iOS のみ|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|  
 |Pulse Secure|はい|はい|はい|いいえ|はい|はい|はい|  
 |F5 Edge Client|はい|はい|はい|いいえ|はい|はい|はい|  
 |Dell SonicWALL Mobile Connect|はい|はい|はい|いいえ|はい|はい|はい|  
 |チェック ポイント モバイル VPN|はい|はい|はい|いいえ|はい|はい|はい|  
 |Microsoft SSL (SSTP)|いいえ|いいえ|はい|はい|はい|いいえ|いいえ|  
 |Microsoft 自動|いいえ|いいえ|はい|はい|はい|いいえ|はい|  
 |IKEv2|はい (カスタム ポリシー、iOS 9 以降)|いいえ|はい|はい|はい|はい|はい|  
 |PPTP|はい|いいえ|はい|はい|はい|いいえ|はい|  
 |L2TP|はい|いいえ|はい|はい|はい|いいえ|はい (OMA-URI)|  

<sup>1</sup> バージョン 1802 以降では、Cisco AnyConnect 接続の種類の使用法が異なります。<!--1357393-->  
   - 次のバージョンの VPN プロファイルには **Cisco Legacy AnyConnect** オプションを使用します。
       - バージョン 4.0.5 以前の Cisco AnyConnect を適用した iOS
       - 任意のバージョンの Cisco AnyConnect を適用した macOS
   - 次のバージョンの VPN プロファイルには **Cisco AnyConnect** オプションを使用します。
       - バージョン 4.0.7 以降の Cisco AnyConnect を適用した iOS

     > [!Tip]  
     > iOS 向け Cisco AnyConnect 4.0.07x 以降は、最初はバージョン 1802 で[プレリリース機能](/sccm/core/servers/manage/pre-release-features)として導入されました。 バージョン 1802 に対する[更新 4163547](https://support.microsoft.com/help/4163547) 以降、この機能はプレリリース機能ではなくなりました。  
  
  
> [!Note]  
> F5 Access 2018 はハイブリッド MDM の VPN プロファイルではサポートされません。  


## <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Intune と Configuration Manager を使用するときに使用できる Windows 10 の VPN 機能  

Windows 10 では、すべての接続の種類に次のオプションを使用できます。

- **[企業の Wi-Fi ネットワークに接続しているときは VPN をバイパスする]**: デバイスが会社の Wi-Fi ネットワークに接続されている場合、VPN 接続は使用されません。 デバイスが会社のネットワークに接続されているかどうかを判断するために使用する、信頼されたネットワーク名を入力します。  

- **[ネットワーク トラフィック規則]**: VPN 接続に対して有効にするプロトコル、ローカル ポート、リモート ポート、アドレス範囲を設定します。  

     > [!Note]  
     > ネットワーク トラフィック規則を作成しない場合は、すべてのプロトコル、ポート、およびアドレス範囲が有効になります。 規則を作成すると、その規則または追加の規則で指定したプロトコル、ポート、アドレス範囲のみが VPN 接続で使用されます。  
  
- **[ルート]**: VPN 接続を使用するルート。 60 を超えるルートを作成すると、ポリシーが機能しなくなる場合があります。  

- **[DNS サーバー]**: 接続の確立後に VPN 接続で使用する DNS サーバー。  

- **[自動的に VPN に接続するアプリ]**: 自動的に VPN 接続を使用するアプリを追加したり、アプリのリストをインポートしたりすることができます。 アプリの種類によってアプリの識別子が決まります。 デスクトップ アプリの場合、アプリのファイル パスを提供します。 ユニバーサル アプリの場合、パッケージ ファミリ名 (PFN) を提供します。 アプリの PFN を検索する方法については、「[Find a package family name for per-app VPN](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md)」(アプリごとの VPN のパッケージ ファミリ名を検索する) を参照してください。  

     > [!IMPORTANT]  
     > アプリごとの VPN の構成で使用するためにコンパイルする関連付けられたアプリのすべてのリストをセキュリティで保護してください。 承認されていないユーザーによって変更されたリストを、アプリごとの VPN のアプリのリストにインポートすると、アクセスが許可されていないアプリへの VPN アクセスを認証してしまう可能性があります。 アプリのリストをセキュリティで保護できる 1 つの方法は、アクセス制御リスト (ACL) を使用することです。  



## <a name="create-vpn-profiles"></a>VPN プロファイルの作成


1. Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースで、**[コンプライアンス設定]**、**[会社リソースのアクセス]** の順に展開して、**[VPN プロファイル]** を選択します。 

2. リボンの **[VPN プロファイルの作成]** をクリックします。  

3. **[全般]** ページで、**[名前]** を指定してから、**[VPN プロファイルの種類]** を選択します。   
     > [!NOTE]  
     > Windows 10 の VPN 機能を使用する VPN プロファイルの名前は、Unicode にしたり、特殊文字を含めたりすることはできません。


4. **[サポートされているプラットフォーム]** ページが利用可能な場合は、以前に指定した VPN プロファイルの種類の OS バージョンを選択します。 利用可能なすべての OS バージョンに VPN プロファイルをインストールする場合は、**[すべて選択]** を選びます。  

5. **[接続]** ページで VPN 接続を構成します。 これらのオプションの詳細については、「[VPN プロファイルの作成](/sccm/protect/deploy-use/create-vpn-profiles#create-a-vpn-profile)」の [接続] ページの手順を参照してください。  

6.  **[認証方法]** ページで、次の設定を指定します。  

    -   **[認証方法]**: VPN 接続で使用する認証方法を選択します。 使用可能な方法は、この表に示されている接続の種類によって異なります。  

        |[認証方法]|サポートされる&nbsp;接続&nbsp;の種類|  
        |---------------------------|--------------------------------|  
        |**証明書**<br /><br /> **注:**<ul><li>RADIUS サーバー (ネットワーク ポリシー サーバーなど) での認証にクライアント証明書を使用する場合は、証明書のサブジェクトの別名をユーザーのプリンシパル名に設定します。</li><li>Android 向けに展開する場合は、EKU 識別子と証明書発行者の拇印のハッシュ値を選択します。 それ以外の場合は、ユーザーは適切な証明書を手動で選択する必要があります。</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Cisco Legacy AnyConnect</li><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> チェック ポイント モバイル VPN</li></ul>|  
        |**ユーザー名とパスワード**|<ul><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> チェック ポイント モバイル VPN</li></ul>|  
        |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft 自動</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
        |**Microsoft 保護された EAP (PEAP)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft 自動</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Microsoft セキュリティで保護されたパスワード (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft 自動</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**スマート カードまたはその他の証明書**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft 自動</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft 自動</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**RSA SecurID** (iOS のみ)|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft 自動</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**コンピューターの証明書を使う**|<ul><li>IKEv2</li></ul>|  

         選択したオプションに応じて、次のような詳細情報の指定を求められることがあります。  

        -   **[ログオンごとにユーザー資格情報を保存する]**: ユーザーが接続するたびに入力しなくても済むように、ユーザーの資格情報が記憶されます。  

        -   **[クライアント認証用のクライアント証明書の選択]**: 事前に作成した、VPN 接続の認証に使用するクライアント [SCEP 証明書](create-pfx-certificate-profiles.md)を選択します。   

            > [!NOTE]  
            >  iOS デバイスの場合、選択する SCEP プロファイルは VPN プロファイルに埋め込まれます。 その他のプラットフォームでは、証明書が存在しないか準拠していない場合に VPN プロファイルがインストールされないようにする適用規則が追加されます。  
            >   
            >  指定した SCEP 証明書が準拠していない、または展開されていない場合、VPN プロファイルはデバイスにインストールされません。
            >  
            >  IOS を実行するデバイスは、接続種類が PPTP の場合に認証方法として RSA SecurID と MSCHAP v2のみをサポートします。 エラーの報告を回避するには、iOS を実行するデバイスに、個別に PPTP VPN プロファイルを展開します。   

        - **条件付きアクセス**  
            - VPN に接続するデバイスについて、接続前に条件付きアクセスのコンプライアンスのためにテストするには、**[この VPN 接続に対して条件付きアクセスを有効にする]** をオンにします。 詳細については、「[デバイス コンプライアンス ポリシー](/sccm/protect/deploy-use/device-compliance-policies)」を参照してください。  

            - デバイスのコンプライアンスのために VPN 認証証明書以外の証明書を選択するには、**[別の証明書でのシングル サインオン (SSO) を有効にする]** をオンにします。 このオプションをオンにする場合は、VPN クライアントを特定できる正しい証明書の **[EKU]** (コンマ区切りリスト) と **[発行元ハッシュ]** を指定します。  

         - **[Windows 情報保護]** には、企業が管理する企業 ID を指定します。通常、これは組織のプライマリ ドメインです (*contoso.com* など)。 組織が所有している複数のドメインを指定するには、"|" 文字で区切ります。 たとえば、「*contoso.com|newcontoso.com*」と指定します。 詳細については、「[Intune で Windows 情報保護 (WIP) アプリ保護ポリシーを作成して展開する](/intune/windows-information-protection-policy-create)」を参照してください。   

         ![VPN プロファイルの作成ウィザードの [認証方法] ページ](media/vpn-conditional-access.png)

         Windows クライアント バージョンでサポートされている場合は、認証方法を**構成**するためのオプションを使用できます。 このオプションを選択すると、認証方法を構成するための Windows のプロパティ ダイアログ ボックスが開きます。 **[構成]** が無効になっている場合は、別の方法で認証方法のプロパティを構成してください。  

3.  VPN 接続でプロキシ サーバーを使用する場合は、**[VPN プロファイルの作成ウィザード]** の **[プロキシの設定]** ページで、**[この VPN プロファイルのプロキシ設定の構成]** チェック ボックスをオンにします。 次に、プロキシ サーバーの情報を指定します。 詳細については、Windows Server のドキュメントを参照してください。  

    > [!NOTE]  
    >  Windows 8.1 コンピューターでは、そのコンピューターを VPN に接続するまで、VPN プロファイルにプロキシ情報は表示されません。  


4. 必要に応じて、詳細な DNS 設定を構成します。  

5. ウィザードを終了します。 新しい VPN プロファイルは、**[資産とコンプライアンス]** ワークスペースの **[VPN プロファイル]** ノードに表示されます。  



## <a name="next-steps"></a>次のステップ  
VPN プロファイルの展開方法の詳細については、[Wi-Fi、VPN、電子メール、証明書プロファイルの展開](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)に関する記事を参照してください。

 VPN プロファイルの計画、設定、操作、メンテナンスを行うときは、次の記事を参考にしてください。  

-   [VPN プロファイルの前提条件](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [VPN プロファイルのセキュリティとプライバシー](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
