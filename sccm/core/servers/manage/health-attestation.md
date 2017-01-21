---
title: "正常性構成証明書 | Microsoft Docs"
description: "Configuration Manager コンソールに表示できるデバイス正常性構成証明書の機能について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: 17
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 937a168f79168b3e3a3a578513814abb2b368d9f


---
# <a name="health-attestation-for-system-center-configuration-manager"></a>System Center Configuration Manager の正常性構成証明書

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の現在のブランチであるバージョン 1602 以降では、管理者は Configuration Manager コンソールで [Windows 10 デバイス正常性構成証明書](https://technet.microsoft.com/library/mt592023.aspx)の状態を確認できます。  この機能は、Configuration Manager によって管理されている PC と内部設置型リソース、および Microsoft Intune で管理されているモバイル デバイスで利用できます。 管理者は、報告がクラウドを使用して行われるか、内部設置型インフラストラクチャを使用して行われるかを指定できます。 これにより、インターネット アクセスを使用しないクライアント PC が、正常性構成証明書を使用してデバイスを有効化および監視できるようになります。 デバイスの正常性構成証明で、管理者はクライアント コンピューターで次の信頼できる BIOS、TPM、およびブート ソフトウェアの構成が有効になっていることを確認できます。  

-   起動時マルウェア対策 - 起動時マルウェア対策 (ELAM) により、サードパーティのドライバーが初期化される前の起動時にコンピューターが保護されます。 [ELAM を有効にする方法](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  

-   BitLocker - Windows BitLocker ドライブ暗号化は、Windows オペレーティング システムのボリュームに格納されているすべてのデータを暗号化できるソフトウェアです。  [Bitlocker を有効にする方法](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  

-   セキュア ブート - セキュア ブートは、PC 業界のメンバーによって開発されたセキュリティ標準で、PC の製造元によって信頼されているソフトウェアのみを使用して PC が起動されるようにするのに役立ちます。 [セキュア ブートの詳細](https://technet.microsoft.com/library/hh824987.aspx)  

-   コードの整合性 - コードの整合性は、メモリに読み込まれるたびに、ドライバーまたはシステム ファイルの整合性を検証することによって、オペレーティング システムのセキュリティを強化する機能です。 [コードの整合性の詳細](https://technet.microsoft.com/library/dd348642.aspx)  



##  <a name="device-health-attestation"></a>デバイス正常性構成証明書  
 Configuration Manager デバイス正常性構成証明書には、次の情報が表示されます。  

-   **正常性構成証明書のステータス** - 対応、非対応、エラー、および不明な状態のデバイスの共有を表示します。  

-   **正常性構成証明書を報告するデバイス** - 正常性構成証明書のステータスを報告するデバイスの割合を示します。  

-   **クライアントの種類別の非対応のデバイス** - 非対応のモバイル デバイスとコンピューターの共有を表示します。  

-   **最も不足している正常性構成証明書の設定** - 正常性構成証明書の設定のないデバイスの数を設定ごとに表示します。  

 **要件:**  

-   Win10 を実行しているクライアント デバイス  

-   [デバイス正常性構成証明書が有効になっている](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation) Windows Server 2016 Technical Preview 5

-    TPM 2 が有効  

-   構成マネージャー クライアント エージェントと has.spserv.microsoft.com (ポート 443) の正常性構成証明書サービスとの間の通信のブロックを解除する

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Configuration Manager クライアント コンピューターの正常性構成証明書サービスの通信を有効にする方法  

1.  Configuration Manager コンソールで、**[管理]**  >  **[概要]**  >  **[クライアント設定]** を選択します。  **[コンピューター エージェント]** 設定のタブを選択します。  

2.  **[既定の設定]** ダイアログ ボックスで、 **[コンピューター エージェント]** を選択して、 **[正常性構成証明書サービスとの通信を有効にする]**まで下にスクロールします。  

3.  **[正常性構成証明書サービスとの通信を有効にする]** を **[はい]**に設定し、 **[OK]**をクリックします。  

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Configuration Manager クライアント コンピューターの内部設置型正常性構成証明書サービスの通信を有効にする方法


1. Configuration Manager コンソールで、**[管理]**  >  **[概要]**  >  **[クライアント設定]** に移動し、**[オンプレミスの正常性構成証明書サービスを使用]** を **[はい]** に設定します。


2. **[オンプレミスの正常性構成証明書サービスの URL]** を指定し、**[OK]** をクリックします。

## <a name="how-to-view-health-attestation"></a>正常性構成証明書を表示する方法  


1.  デバイス正常性構成証明書ビューを表示するには、Configuration Manager コンソールで **[監視]** ワークスペースに移動し、 **[セキュリティ]** ノードをクリックしてから **[正常性構成証明書]**をクリックします。  

2.  デバイス正常性構成証明書が表示されます。  

 クライアント デバイス正常性構成証明書のステータスは、Microsoft Intune を備えた Configuration Manager によって管理されるデバイスのコンプライアンス ポリシーに条件付きアクセスの規則を定義するために使用できます。 詳細については、「[System Center Configuration Manager でのデバイス コンプライアンス ポリシーの管理](/sccm/protect/deploy-use/device-compliance-policies)」をご覧ください。  



<!--HONumber=Dec16_HO3-->


