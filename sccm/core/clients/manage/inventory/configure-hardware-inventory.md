---
title: ハードウェア インベントリを構成する
titleSuffix: Configuration Manager
description: System Center Configuration Manager ですべてのクライアントまたは 1 つのコレクションに対してハードウェア インベントリを設定します。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 7b282fdb2f7cf3a200950484e4da5b9505c5b71c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332157"
---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager でハードウェア インベントリを構成する方法

*適用対象: System Center Configuration Manager (Current Branch)*

この手順により、ハードウェア インベントリの既定のクライアント設定を構成し、階層内のすべてのクライアントに適用します。 いくつかのクライアントにのみこの設定を適用するには、カスタムのデバイス クライアント設定を作成し、ハードウェア インベントリを使用するデバイスが含まれるコレクションにそれを割り当てます。 「[System Center Configuration Manager でクライアント設定を構成する方法](../../../../core/clients/deploy/configure-client-settings.md)」を参照してください。  

> [!NOTE]  
>  クライアント デバイスが複数のクライアント設定をハードウェア インベントリを受信した場合は、各設定のハードウェア インベントリのクラスは、クライアントがハードウェア インベントリをレポートするときに結合されます。  

### <a name="to-configure-hardware-inventory"></a>ハードウェア インベントリを構成するには  

1.  Configuration Manager コンソールで、**[管理]** > **[クライアント設定]** > **[既定のクライアント設定]** の順に選択します。  

4.  **[ホーム]** タブの **[プロパティ]** グループで、**[プロパティ]** を選択します。  

5.  **[既定の設定]** ダイアログ ボックスで、**[ハードウェア インベントリ]** を選択します。  

6.  **[デバイスの設定]** 一覧で、次を構成します。  

    -   **クライアントのハードウェア インベントリを有効にする** - **[True]** を選択します。  

    -   **ハードウェア インベントリのスケジュール** - **[スケジュール]** をクリックしてクライアントがハードウェア インベントリを収集する間隔を指定します。  

7.  必要なその他の[ハードウェア インベントリのクライアント設定](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory)を構成します。  

クライアント デバイスは、次の機会にクライアント ポリシーをダウンロードしたときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始する場合は、「 [System Center Configuration Manager でクライアントを管理する方法](../../../../core/clients/manage/manage-clients.md)」を参照してください。  
