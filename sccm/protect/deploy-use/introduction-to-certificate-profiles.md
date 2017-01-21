---
title: "証明書プロファイルの概要 | Microsoft Docs"
description: "System Center Configuration Manager の証明書プロファイルと Active Directory 証明書サービスの使用方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: 7
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 25d57d25ca683608bbe9a0695b2463ad5b9a0833


---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager における証明書プロファイルの概要

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager では、Active Directory 証明書サービスとネットワーク デバイス登録サービスの役割と連携し、証明書プロファイルを使って管理対象のデバイスに認証証明書をプロビジョニングして、ユーザーが会社のリソースにシームレスにアクセスできるようにします。 たとえば、証明書プロファイルを作成し、展開して、ユーザーが VPN 接続およびワイヤレス接続を開始するために必要な証明書を提供することができます。  

 System Center Configuration Manager の証明書プロファイルには、次の管理機能があります。  

-   iOS、Windows 8.1、Windows RT 8.1、Windows 10 Desktop および Mobile、Android を実行するデバイスにおける、エンタープライズ証明機関 (CA) の証明書の登録と更新。これらの証明書を Wi-Fi 接続と VPN 接続に使用できます。  

-   サーバー認証が必要な場合に VPN 接続のデバイスと Wi-Fi 接続のデバイスで信頼関係のチェーンを構成するための、信頼されたルート CA 証明書と中間 CA 証明書の展開。  

-   インストールされている証明書を監視してレポートします。  

 証明書プロファイルでは、Wi-Fi ネットワークや VPN サーバーなどの会社のリソースにアクセスできるように、ユーザー デバイスを自動的に構成でき、証明書を手動でインストールしたり帯域外プロセスを使用する必要がありません。 エンタープライズ公開キー基盤 (PKI) でサポートされているさらに安全な設定を使用できるため、証明書プロファイルは会社のリソースをセキュリティで保護した状態で維持するためにも役立ちます。 たとえば、管理対象のデバイスに必要な証明書がプロビジョニングされるため、すべての Wi-Fi 接続と VPN 接続にサーバー認証を要求できます。  

 **例:** すべての従業員が、企業内の複数の場所で Wi-Fi ホットスポットに接続できる必要があります。 これを実現するには、Wi-Fi 接続に必要な証明書を展開するだけでなく、ユーザーが Wi-Fi 接続をシームレスに利用するための正しい証明書を参照する Wi-Fi プロファイルを System Center Configuration Manager で展開します。  

 **例:** PKI を使用中の場合に、セキュリティを損なうことなく、ユーザーの個人のデバイスから会社のリソースへのアクセスを可能にする証明書をプロビジョニングする方法として、セキュリティで保護されたさらに柔軟なメソッドに移行する必要がある場合。 これを実現するには、特定のデバイス プラットフォーム用にサポートされている設定とプロトコルを使用して、証明書プロファイルを構成することができます。 デバイスは、インターネットに接続された登録サーバーに対してこれらの証明書を自動的に要求することができます。 さらに、デバイスが会社のリソースにアクセスできるように、これらの証明書を使用するように VPN プロファイルを構成することができます。  

## <a name="types-of-certificate-profile"></a>証明書プロファイルの種類  
 System Center Configuration Manager では、3 種類の証明書プロファイルを作成できます。  

-   **信頼された CA 証明書** - デバイスがサーバーを認証する必要があるときに信頼できる証明書チェーンを形成するために、信頼されたルート CA または中間 CA 証明書を展開することができます。  

-   **Simple Certificate Enrollment Protocol (SCEP)** - Windows Server 2012 R2 を実行するサーバーで、SCEP プロトコルおよびネットワーク デバイス登録サービスを使用して、デバイス用やユーザー用の証明書を要求することができます。
-   -   **Personal information exchange (.pfx)** - Windows Server 2012 R2 を実行するサーバーで、SCEP プロトコルおよびネットワーク デバイス登録サービスを使用して、デバイス用やユーザー用の証明書を要求することができます。

    > [!NOTE]  
    >  証明書プロファイルの種類 [Simple Certificate Enrollment Protocol (SCEP) 設定 **** ] を作成するには、証明書プロファイルの種類 [信頼された証明機関証明書 ****] を作成する必要があります。  

## <a name="requirements-and-supported-platforms"></a>要件とサポートされるプラットフォーム  
 Simple Certificate Enrollment Protocol を使用する証明書プロファイルを展開するためには、中央管理サイトまたはプライマリ サイトで、サイト システム サーバーに証明書登録ポイントをインストールする必要があります。 また、Active Directory 証明書サービスの役割が配置され、証明書を必要とするデバイスからアクセス可能なネットワーク デバイス登録サービスが動作している Windows Server 2012 R2 サーバーに、ネットワーク デバイス登録サービス用のポリシー モジュール、つまり Configuration Manager ポリシー モジュールをインストールする必要があります。 Microsoft Intune によって登録されるデバイスでは、たとえば、スクリーン サブネット (境界ネットワーク とも呼ばれます) などで、インターネットからネットワーク デバイス登録サービスにアクセスできる必要があります。  

 System Center Configuration Manager で証明書を展開するためのネットワーク デバイス登録サービスとポリシー モジュールのしくみについては、「[ポリシー モジュールとネットワーク デバイス登録サービスの使用](http://go.microsoft.com/fwlink/p/?LinkId=328657)」を参照してください。  

 System Center Configuration Manager では、要件に加えて、デバイスの種類とオペレーティング システムにも応じて、異なる証明書ストアに証明書を展開することがサポートされています。 次のデバイスとオペレーティング システムがサポートされています。  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop および Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  プロファイルを Android、iOS、Windows Phone、および登録されている Windows 8.1 以降の各デバイスに展開するには、これらのデバイスを Microsoft Intune に登録する必要があります。 デバイスの登録方法については、「 [Microsoft Intune を使用したモバイル デバイスの管理](https://technet.microsoft.com/en-us/library/dn646962.aspx)」を参照してください。  

 System Center Configuration Manager の典型的なシナリオとして、接続に EAP-TLS、EAP-TTLS、および PEAP の認証プロトコル、IKEv2、L2TP/IPsec、および Cisco IPsec VPN のトンネリング プロトコルを使用する場合に、Wi-Fi サーバーと VPN サーバーを認証するために、信頼されるルート CA 証明書をインストールするというものがあります。  

 デバイスが SCEP 証明書プロファイルを使用して証明書を要求するためには、そのデバイスにエンタープライズ ルート CA 証明書がインストールされていなければなりません。  

 さまざまな環境や接続要件に合わせてカスタマイズされた証明書を要求するように、SCEP 証明書プロファイルにさまざまな設定を指定できます。 **** 証明書プロファイルの作成ウィザードには、登録パラメーター用のページが 2 つあります。 1 つ目の [SCEP 登録 ****] には、登録要求の設定と証明書のインストール先の設定が含まれています。 もう 1 つの [証明書のプロパティ] は、要求する証明書自体を説明するページです。 ****  

## <a name="deploying-certificate-profiles"></a>証明書プロファイルの展開  
 証明書プロファイルを展開すると、プロファイル内の証明書ファイルがクライアント デバイスにインストールされます。 SCEP パラメーターも展開されて、SCEP 要求がクライアント デバイス上で処理されます。 証明書プロファイルをユーザー コレクションまたはデバイス コレクションに展開して、各証明書の保存先のストアを指定できます。 適用規則によって、証明書をデバイスにインストールできるかどうかが決まります。 証明書プロファイルをユーザー コレクションに展開する場合は、ユーザーとデバイスのアフィニティによって、ユーザーのどのデバイスに証明書をインストールするのかが決まります。 ユーザー証明書が含まれた証明書プロファイルをデバイス コレクションに展開すると、既定では、証明書はユーザーの各プライマリ デバイスにインストールされます。 この動作を変更して、**証明書プロファイルの作成ウィザード**の **[SCEP 登録]** のページにあるユーザーの任意のデバイス上に証明書をインストールできます。 また、デバイスがワークグループ コンピューターの場合、デバイスにユーザー証明書は展開されません。  

## <a name="monitoring-certificate-profiles"></a>証明書プロファイルの監視  
 証明書プロファイルの展開は、System Center Configuration Manager コンソールの **[監視]** ワークスペースの **[展開]** ノードで監視できます。  

 また、次の System Center Configuration Manager レポートのいずれかを使用して証明書プロファイルを監視できます。  

-   **証明書登録ポイントによって発行される証明書の履歴。**  

-   **証明書登録ポイントで登録された証明書での、証明書の発行状態による資産の一覧**  

-   **証明書の有効期限日が近い資産の一覧**  

## <a name="automatic-revocation-of-certificates"></a>証明書の自動失効  
 System Center Configuration Manager で証明書プロファイルを使用して展開したユーザー証明書とデバイス証明書は、次のような場合に自動的に失効します。  

-   デバイスが System Center Configuration Manager の管理下のインベントリから削除された場合。  

-   デバイスの特定のコンテンツがワイプされた場合。  

-   デバイスが System Center Configuration Manager の階層からブロックされた場合。  

 証明書を失効させるために、サイト サーバーが、証明書の発行元の証明機関に失効コマンドを送信します。 この失効の理由は、「運用停止」です。 ****  



<!--HONumber=Dec16_HO3-->


