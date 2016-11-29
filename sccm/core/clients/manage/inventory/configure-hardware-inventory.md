---
title: "ハードウェア インベントリの構成 | System Center Configuration Manager"
description: "System Center Configuration Manager ですべてのクライアントまたは 1 つのコレクションに対してハードウェア インベントリを設定します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 41bf42228e41785a05359c08e8dfedae48d50e30


---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のハードウェア インベントリを構成するには、次の手順に従います。  

 この手順により、ハードウェア インベントリの既定のクライアント設定を構成し、階層内のすべてのクライアントに適用します。 いくつかのクライアントにのみこの設定を適用するには、カスタムのデバイス クライアント設定を作成し、ハードウェア インベントリを使用するデバイスが含まれるコレクションにそれを割り当てます。 カスタムのデバイス設定の作成方法の詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../../core/clients/deploy/configure-client-settings.md)」を参照してください。  

> [!NOTE]  
>  クライアント デバイスが複数のクライアント設定をハードウェア インベントリを受信した場合は、各設定のハードウェア インベントリのクラスは、クライアントがハードウェア インベントリをレポートするときに結合されます。  

### <a name="to-configure-hardware-inventory"></a>ハードウェア インベントリを構成するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [ **管理** ] ワークスペースで [ **クライアント設定**] をクリックします。  

3.  [既定のクライアント設定 ****] をクリックします。  

4.  **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]**をクリックします。  

5.  [既定の設定] **** ダイアログ ボックスで、[ハードウェア インベントリ] ****をクリックします。  

6.  [デバイスの設定] **** 一覧で、次を構成します。  

    -   **クライアントのハードウェア インベントリを有効にする** – ドロップダウン リストから、 **[True]**を選択します。  

    -   **ハードウェア インベントリのスケジュール** - クライアントがハードウェア インベントリを収集する間隔を指定します。 規定値は [7 日] **** です。カスタムの間隔を構成するには、[スケジュール] **** をクリックします。  

7.  必要な他のクライアント設定を構成します。 構成できるハードウェア インベントリのクライアント設定の一覧については、「[System Center Configuration Manager のクライアント設定について](../../../../core/clients/deploy/about-client-settings.md#BKMK_HardwareInventoryDeviceSettings)」トピックの「[ハードウェア インベントリ](../../../../core/clients/deploy/about-client-settings.md)」セクションを参照してください。  

8.  [OK] **** をクリックして [既定の設定] **** ダイアログ ボックスを閉じます。  

 クライアント デバイスは、次の機会にクライアント ポリシーをダウンロードしたときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始する場合は、「 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)」を参照してください。  



<!--HONumber=Nov16_HO1-->


