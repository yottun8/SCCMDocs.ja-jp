---
title: "System Center Configuration Manager の VPN プロファイル | System Center Configuration Manager"
description: "System Center Configuration Manager の VPN プロファイルを使用して、VPN 設定を組織内のユーザーに展開する方法について説明します。"
ms.custom: na
ms.date: 10/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: 6
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: dda572392884c54b63af09a9fae79c1e73eb3d95


---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager の VPN プロファイル

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager の VPN プロファイルを使用して、VPN 設定を組織内のユーザーに展開します。 これらの設定を展開して、企業ネットワーク上のリソースに接続するために必要なエンド ユーザーの作業を最小化します。  

 たとえば、iOS オペレーティング システムを実行するすべてのデバイスに対して、企業ネットワーク上のファイル共有に接続するために必要な設定をプロビジョニングできます。 企業ネットワークに接続するために必要な設定が含まれている VPN プロファイルを作成した後、階層内で iOS を実行するデバイスを持つすべてのユーザーにこのプロファイルを展開することができます。 iOS デバイスのユーザーに対して使用可能なネットワークの一覧で VPN 接続が表示されるため、最小限の作業でこのネットワークに接続できます。  

 VPN プロファイルを作成するときに、System Center Configuration Manager 証明書プロファイルを使用してプロビジョニングされた、サーバー検証用の証明書、クライアント認証用の証明書などの幅広いセキュリティ設定を含めることができます。 証明書プロファイルの詳細については、「[System Center Configuration Manager の証明書プロファイル](introduction-to-certificate-profiles.md)」を参照してください。  

 以下のセクションでは、Configuration Manager を使用する場合または Configuration Manager と Microsoft Intune を併用する場合に、VPN プロファイルを使用して構成できるデバイスについて説明します。  

## <a name="vpn-profiles-when-using-configuration-manager"></a>Configuration Manager を使用する場合の VPN プロファイル  
 次の表では、さまざまなデバイス プラットフォームに対して構成できる VPN プロファイルについて説明します。  

|接続の種類|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|いいえ|いいえ|いいえ|×|  
|**Pulse Secure**|○|×|[はい]|○|  
|**F5 Edge Client**|○|×|[はい]|○|  
|**Dell SonicWALL Mobile Connect**|○|×|[はい]|○|  
|**チェック ポイント モバイル VPN**|○|×|[はい]|○|  
|**Microsoft SSL (SSTP)**|○|[はい]|○|×|  
|**Microsoft 自動**|○|[はい]|○|×|  
|**IKEv2**|○|[はい]|○|いいえ|  
|**PPTP**|○|[はい]|○|いいえ|  
|**L2TP**|○|[はい]|○|いいえ|  

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

### <a name="next-steps"></a>次のステップ  
 Configuration Managerで VPN プロファイルの計画、構成、操作、およびメンテナンスを行うときに、次のトピックを参考にしてください。  

-   [System Center Configuration Manager の VPN プロファイルの前提条件](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [System Center Configuration Manager の VPN プロファイルのセキュリティとプライバシー](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)



<!--HONumber=Nov16_HO1-->


