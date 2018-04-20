---
title: VPN プロファイル
titleSuffix: Configuration Manager
description: System Center Configuration Manager の VPN プロファイルを使用して、VPN 設定を組織内のユーザーに展開する方法について説明します。
ms.custom: na
ms.date: 04/10/2018
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
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d30e7cc834f1693f2cbcf2db840d650421062a19
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2018
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager の VPN プロファイル

*適用対象: System Center Configuration Manager (Current Branch)*

<!--1283610-->
組織内のユーザーに VPN 設定を展開するには、Configuration Manager の VPN プロファイルを使用します。 これらの設定を展開して、企業ネットワーク上のリソースに接続するために必要なエンド ユーザーの作業を最小化します。  

 たとえば、企業ネットワーク上のファイル共有に接続するために必要な設定をすべての Windows 10 デバイスに構成したいとします。 企業ネットワークに接続するのに必要な設定が含まれる VPN プロファイルを作成します。 次いで、Windows 10 を実行しているデバイスを使用するすべてのユーザーに、このプロファイルを展開します。 VPN 接続は、これらのユーザーに、使用できるネットワークの一覧として表示されるので、ユーザーは最小限の労力で接続できます。  

 VPN プロファイルを作成するときに、さまざまなセキュリティ設定を含めることができます。 これらの設定には、Configuration Manager の証明書プロファイルを使ってプロビジョニングする、サーバー評価用の証明書やクライアント認証用の証明書があります。 詳細については、「[Certificate profiles](introduction-to-certificate-profiles.md)」 (証明書プロファイル) をご覧ください。  

> [!Note]  
> Configuration Manager では、このオプション機能は既定で無効です。 この機能は、使用する前に有効にする必要があります。 詳細については、「[更新プログラムのオプション機能の有効化](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」を参照してください。<!--505213-->  


 [モバイル デバイスの VPN プロファイル](/sccm/mdm/deploy-use/create-vpn-profiles)に関する記事を参照して、Microsoft Intune で Configuration Manager を使用する場合に構成できるデバイスを確認してください。  

## <a name="vpn-profiles-when-using-configuration-manager"></a>Configuration Manager を使用する場合の VPN プロファイル  
 次の表では、さまざまなデバイス プラットフォームに対して構成できる VPN プロファイルについて説明します。  

|接続の種類|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|いいえ|いいえ|いいえ|いいえ|  
|**Pulse Secure**|はい|いいえ|はい|はい|  
|**F5 Edge Client**|はい|いいえ|はい|はい|  
|**Dell SonicWALL Mobile Connect**|はい|いいえ|はい|はい|  
|**チェック ポイント モバイル VPN**|はい|いいえ|はい|はい|  
|**Microsoft SSL (SSTP)**|はい|はい|はい|いいえ|  
|**Microsoft 自動**|はい|はい|はい|いいえ|  
|**IKEv2**|はい|はい|はい|いいえ|  
|**PPTP**|はい|はい|はい|いいえ|  
|**L2TP**|はい|はい|はい|いいえ|  

### <a name="next-steps"></a>次のステップ  
 Configuration Managerで VPN プロファイルの計画、構成、操作、およびメンテナンスを行うときに、次のトピックを参考にしてください。  

-   [System Center Configuration Manager の VPN プロファイルの前提条件](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [System Center Configuration Manager の VPN プロファイルのセキュリティとプライバシー](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
