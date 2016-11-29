---
title: "Wi-Fi プロファイルの概要 | System Center Configuration Manager"
description: "System Center Configuration Manager の Wi-Fi プロファイルを使用して、ワイヤレス ネットワーク設定を組織内のユーザーに展開する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 86725460-c2f3-49ed-90aa-6b2724d34d69
caps.latest.revision: 8
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 30fefb291a6fccb630d5e3272ce7266339c9139c


---
# <a name="introduction-to-wi-fi-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager の Wi-Fi プロファイルの概要

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の Wi-Fi プロファイルを使用して、ワイヤレス ネットワーク設定を組織内のユーザーに展開します。 これらの設定を展開すれば、ワイヤレス ネットワークに接続するために必要なエンド ユーザーの作業を最小限に抑えられます。  

 たとえば、 **Contoso Wi-Fi**という名前の新しい Wi-Fi ネットワークを設置したとします。 iOS オペレーティング システムを実行しているすべてのデバイスに、このネットワークへの接続に必要な設定をプロビジョニングしようとしています。 まず、 **Contoso Wi-Fi** ワイヤレス ネットワークへの接続に必要な設定が含まれている Wi-Fi プロファイルを作成します。 このプロファイルを、iOS を実行するデバイスを持つ階層内のすべてのユーザーに展開できます。 iOS デバイスのユーザーは、ワイヤレス ネットワークの一覧で会社のネットワークを参照し、このネットワークに簡単に接続できるようになります。  

 Wi-Fi プロファイルを使用して、次のデバイスの種類を構成できます。  

-   Windows 8.1 32 ビットを実行するデバイス  

-   Windows 8.1 64 ビットを実行するデバイス  

-   Windows RT 8.1 を実行するデバイス  

-   Windows Phone 8.1 を実行するデバイス  

-   Windows 10 デスクトップまたは Windows 10 Mobile を実行するデバイス  

-   iOS 5、iOS 6、iOS 7 および iOS 8 を実行する iPhone デバイス  

-   iOS 5、iOS 6、iOS 7 および iOS 8 を実行する iPad デバイス  

-   バージョン 4 を実行する Android デバイス  

> [!IMPORTANT]  
>  プロファイルを Android、iOS、Windows Phone、および登録されている Windows 8.1 以降の各デバイスに展開するには、これらのデバイスを Microsoft Intune に登録する必要があります。 デバイスの登録方法については、「 [Microsoft Intune を使用したモバイル デバイスの管理](https://technet.microsoft.com/library/dn646962.aspx)」を参照してください。  

 Wi-Fi プロファイルを作成するときに、さまざまなセキュリティ設定を含めることができます。 たとえば、Configuration Manager の証明書プロファイルを使ってプロビジョニングしている、サーバー評価用の証明書やクライアント認証用の証明書を使えます。 証明書プロファイルの詳細については、「[System Center Configuration Manager の証明書プロファイル](introduction-to-certificate-profiles.md)」を参照してください。  



<!--HONumber=Nov16_HO1-->


