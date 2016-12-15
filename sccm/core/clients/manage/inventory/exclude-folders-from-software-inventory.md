---
title: "ソフトウェア インベントリからフォルダーを除外する | Microsoft Docs"
description: "System Center Configuration Manager でソフトウェア インベントリからフォルダーを除外します。"
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6d1aabbde576f01de920468fd3ef372bd23be9df
ms.openlocfilehash: 7850b69cdccb0e897ee71b75255004bdc8d0ae97


---
# <a name="how-to-exclude-folders-from-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager でソフトウェア インベントリからフォルダーを除外する方法

*適用対象: System Center Configuration Manager (Current Branch)*

 この手順により、ソフトウェア インベントリの既定のクライアント設定を構成し、階層内のすべてのデバイスに適用します。 いくつかのコンピューターにのみこれらの設定を適用するには、カスタムのデバイス クライアント設定を作成し、ソフトウェア インベントリを使用するコンピューターが含まれるコレクションにそれを割り当てます。 カスタムのデバイス設定の作成方法の詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../../core/clients/deploy/configure-client-settings.md)」を参照してください。  

### <a name="to-configure-software-inventory"></a>ソフトウェア インベントリを構成するには  

1.  Configuration Manager コンソールで、[**管理**] > [**クライアント設定**] > [**既定のクライアント設定**] の順に選択します。  

4.  **[ホーム]** タブの **[プロパティ]** グループで、**[プロパティ]** を選択します。  

5.  [**既定の設定**] ダイアログ ボックスで、[**ソフトウェア インベントリ**] を選択します。  

6.  [デバイスの設定] **** 一覧で、次の値を構成します。  

    -   **クライアントのソフトウェア インベントリを有効にする** - ドロップダウン リストから、**[True]** を選択します。  

    -   **ソフトウェア インベントリおよびファイル収集をスケジュールする** - クライアントがソフトウェア インベントリとファイルを収集する間隔を構成します。   

7.  必要なクライアント設定を構成します。 構成できるソフトウェア インベントリ クライアント設定の一覧については、「[System Center Configuration Manager のクライアント設定について](../../../../core/clients/deploy/about-client-settings.md)」トピックの「[ソフトウェア インベントリ](../../../../core/clients/deploy/about-client-settings.md#software-inventory)」セクションをご覧ください。  

 クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始する場合は、「 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)」を参照してください。  



<!--HONumber=Dec16_HO1-->


