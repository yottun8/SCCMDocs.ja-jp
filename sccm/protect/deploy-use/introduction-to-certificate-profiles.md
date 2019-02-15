---
title: 証明書プロファイルの概要
titleSuffix: Configuration Manager
description: System Center Configuration Manager の証明書プロファイルと Active Directory 証明書サービスの使用方法について説明します。
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5872a6a8ee69e50d0abfe5840a087aaf83ab7aa5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156612"
---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager における証明書プロファイルの概要

*適用対象: System Center Configuration Manager (Current Branch)*


証明書プロファイルは、Active Directory 証明書サービスおよびネットワーク デバイス登録サービス (NDES) ロールと共に使用されます。 ユーザーが会社のリソースに簡単にアクセスできるように、マネージド デバイスに証明書認証を作成して展開します。 たとえば、証明書プロファイルを作成して展開し、ユーザーが VPN 接続およびワイヤレス接続に必要な証明書を提供することができます。

証明書プロファイルでは、ユーザー デバイスを自動的に構成できます。 ユーザーは、証明書を手動でインストールしたり、帯域外のプロセスを使用したりすることなく、Wi-Fi ネットワークや VPN サーバーなどの会社のリソースにアクセスします。 エンタープライズ公開キー基盤 (PKI) でサポートされているさらに安全な設定を使用できるため、証明書プロファイルは会社のリソースをセキュリティで保護した状態で維持するために役立ちます。 たとえば、マネージド デバイスに必要な証明書を展開しているため、すべての Wi-Fi 接続と VPN 接続に対してサーバー認証を要求します。   

証明書プロファイルが提供する管理機能:  

-   iOS、Windows 8.1、Windows RT 8.1、Windows 10 Desktop および Mobile、Android を実行するデバイスにおける、エンタープライズ証明機関 (CA) の証明書の登録と更新。 これらの証明書を Wi-Fi 接続と VPN 接続に使用できます。  

-   信頼されたルート CA 証明書と中間 CA 証明書の展開。 これらの証明書では、サーバー認証が必要な場合に VPN 接続のデバイスと Wi-Fi 接続のデバイスで信頼関係のチェーンを構成します。  

-   インストールされている証明書を監視してレポートします。  

**例:** すべての従業員が、企業内の複数の場所で Wi-Fi ホットスポットに接続できる必要があります。 簡単なユーザー接続を有効にするには、最初に Wi-Fi への接続に必要な証明書を展開します。 次に、証明書を参照する Wi-Fi プロファイルを展開します。  

**例:** PKI が設置されています。 より柔軟でセキュリティで保護された方法で証明書を展開する必要があります。 セキュリティを低下させることなく、ユーザーが個別のデバイスから会社のリソースにアクセスできるようにする必要があります。 特定のデバイス プラットフォーム用にサポートされている設定とプロトコルを使用して、証明書プロファイルを構成します。 デバイスは、インターネットに接続された登録サーバーに対してこれらの証明書を自動的に要求することができます。 それから、デバイスが会社のリソースにアクセスできるように、これらの証明書を使用するように VPN プロファイルを構成します。  



## <a name="types-of-certificate-profiles"></a>証明書プロファイルの種類  
 次の 3 種類の証明書プロファイルがあります。  

-   **信頼された CA 証明書** - 信頼されたルート CA 証明書と中間 CA 証明書を展開します。 デバイスでサーバーを認証する必要がある場合、これらの証明書で信頼関係のチェーンが形成されます。  

-   **Simple Certificate Enrollment Protocol (SCEP)** - SCEP プロトコルを使用して、デバイスまたはユーザーの証明書を要求します。 この種類には、Windows Server 2012 R2 以降を実行するサーバー上のネットワーク デバイス登録サービス (NDES) ロールが必要です。

    **Simple Certificate Enrollment Protocol (SCEP)** の証明書プロファイルを作成するには、最初に**信頼された CA 証明書**プロファイルを作成します。

-   **Personal information exchange (.pfx)** - デバイスまたはユーザーの .pfx (別名、PKCS #12) 証明書を要求します。<!--1321368-->  

    要求を処理するために既存の証明書から[証明書をインポート](/sccm/mdm/deploy-use/import-pfx-certificate-profiles)するか、[証明機関を定義](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)して、PFX の証明書プロファイルを作成できます。

    > [!Note]  
    > Configuration Manager では、このオプション機能は既定で無効です。 この機能は、使用する前に有効にする必要があります。 詳細については、「[更新プログラムのオプション機能の有効化](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」を参照してください。<!--505213-->  

    バージョン 1706 以降、**Personal information exchange (.pfx)** 証明書の証明機関として Microsoft または Entrust を使用できます。


## <a name="requirements-and-supported-platforms"></a>要件とサポートされるプラットフォーム  
SCEP を使用する証明書プロファイルを展開するには、証明書登録ポイントをサイト システム サーバーにインストールします。 また、NDES 用のポリシー モジュール (Configuration Manager ポリシー モジュール) を Windows Server 2012 R2 以降を実行するサーバーにインストールします。 このサーバーには、Active Directory 証明書サービス ロールおよび証明書が必要なデバイスにアクセスできる動作中の NDES が必要です。 Microsoft Intune によって登録されたデバイスの場合、NDES にインターネットからアクセスできる必要があります。 たとえば、スクリーン サブネット (DMZ) 内です。  

PFX 証明書には、証明書登録ポイントも必要です。 また、証明書の証明機関 (CA) と関連するアクセス資格情報も指定します。 バージョン 1706 以降、証明機関として Microsoft または Entrust のいずれかを指定できます。  

Configuration Manager で証明書を展開するためのネットワーク デバイス登録サービスとポリシー モジュールのしくみについては、「[ポリシー モジュールとネットワーク デバイス登録サービスの使用](http://go.microsoft.com/fwlink/p/?LinkId=328657)」を参照してください。  

要件に応じて、Configuration Manager では、さまざまなデバイスの種類やオペレーティング システム上で異なる証明書ストアへの証明書の展開をサポートします。 次のデバイスとオペレーティング システムがサポートされています。  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop および Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  プロファイルを Android、iOS、Windows Phone、および登録されている Windows 8.1 以降の各デバイスに展開するには、これらのデバイスを [Microsoft Intune に登録する](/intune/device-enrollment)必要があります。   

Configuration Manager の一般的なシナリオとして、接続に EAP-TLS、EAP-TTLS、PEAP の認証プロトコル、IKEv2、L2TP/IPsec、Cisco IPsec VPN のトンネリング プロトコルを使用する場合に、Wi-Fi サーバーと VPN サーバーを認証するために、信頼されるルート CA 証明書をインストールするというものがあります。  

デバイスが SCEP 証明書プロファイルを使用して証明書を要求するには、そのデバイスにエンタープライズ ルート CA 証明書がインストールされている必要があります。  

さまざまな環境や接続要件に合わせてカスタマイズされた証明書を要求するように、SCEP 証明書プロファイルに設定を指定できます。 **証明書プロファイルの作成ウィザード** には、登録パラメーター用のページが 2 つあります。 1 つ目の **[SCEP 登録]** には、登録要求の設定と証明書のインストール先の場所が含まれています。 もう 1 つの **[証明書のプロパティ]** は、要求する証明書自体を説明するページです。  

## <a name="deploying-certificate-profiles"></a>証明書プロファイルの展開  
 証明書プロファイルを展開すると、プロファイル内の証明書ファイルがクライアント デバイスにインストールされます。 SCEP パラメーターも展開されて、SCEP 要求がクライアント デバイス上で処理されます。 証明書プロファイルをユーザー コレクションまたはデバイス コレクションに展開して、各証明書の保存先のストアを指定できます。 適用規則によって、証明書をデバイスにインストールできるかどうかが決まります。 証明書プロファイルをユーザー コレクションに展開する場合は、ユーザーとデバイスのアフィニティによって、証明書をインストールするユーザーのデバイスが決まります。 ユーザー証明書が含まれた証明書プロファイルをデバイス コレクションに展開すると、既定では、証明書はユーザーの各プライマリ デバイスにインストールされます。 この動作を変更して、**証明書プロファイルの作成ウィザード** の **[SCEP 登録]** のページにあるユーザーの任意のデバイス上に証明書をインストールできます。 デバイスがワークグループのコンピューターの場合、ユーザーの証明書は展開されません。  

## <a name="monitoring-certificate-profiles"></a>証明書プロファイルの監視  

コンプライアンスの結果やレポートを表示し、証明書プロファイルの展開を監視できます。 これらの手法の説明は、「[証明書プロファイルを監視する方法](/sccm/protect/deploy-use/monitor-certificate-profiles)」にあります。


## <a name="automatic-revocation-of-certificates"></a>証明書の自動失効  
 System Center Configuration Manager で証明書プロファイルを使用して展開したユーザー証明書とデバイス証明書は、次のような場合に自動的に失効します。  

- デバイスが System Center Configuration Manager の管理下のインベントリから削除された場合。  

- デバイスの特定のコンテンツがワイプされた場合。  

- デバイスが System Center Configuration Manager の階層からブロックされた場合。  

  証明書を失効させるために、サイト サーバーが、証明書の発行元の証明機関に失効コマンドを送信します。 この失効の理由は、「 **運用停止** 」です。  
