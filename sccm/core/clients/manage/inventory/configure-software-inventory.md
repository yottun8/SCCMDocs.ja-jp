---
title: ソフトウェア インベントリを構成する
titleSuffix: Configuration Manager
description: System Center Configuration Manager でソフトウェア インベントリを構成し、でソフトウェア インベントリからフォルダーを除外します。
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e3b6e1ab2962cec7891501ec6b19f081631e187
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421129"
---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager でソフトウェア インベントリを構成する方法

*適用対象:System Center Configuration Manager (Current Branch)*

この手順により、ソフトウェア インベントリの既定のクライアント設定を構成し、階層内のすべてのデバイスに適用します。 これらの設定を一部のクライアントにのみ適用する場合は、カスタムのデバイス クライアント設定を作成して、それをコレクションに割り当てます。 カスタムのデバイス設定の作成方法の詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../../core/clients/deploy/configure-client-settings.md)」を参照してください。   

## <a name="to-configure-software-inventory"></a>ソフトウェア インベントリを構成するには  

1. Configuration Manager コンソールで、**[管理]** > **[クライアント設定]** > **[既定のクライアント設定]** の順に選択します。  

2. **[ホーム]** タブの **[プロパティ]** グループで、**[プロパティ]** を選択します。  

3. **[既定の設定]** ダイアログ ボックスで、**[ソフトウェア インベントリ]** を選択します。  

4. [デバイスの設定] **** 一覧で、次の値を構成します。  

   -   **クライアントのソフトウェア インベントリを有効にする** - ドロップダウン リストから、**[True]** を選択します。  

   -   **ソフトウェア インベントリおよびファイル収集をスケジュールする** - クライアントがソフトウェア インベントリとファイルを収集する間隔を構成します。   

5. 必要なクライアント設定を構成します。 「[System Center Configuration Manager のクライアント設定について](../../../../core/clients/deploy/about-client-settings.md)」の記事の「[ソフトウェア インベントリ](../../../../core/clients/deploy/about-client-settings.md#software-inventory)」セクションに、クライアント設定の一覧があります。  

   クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始する場合は、「 [System Center Configuration Manager でクライアントを管理する方法](../../../../core/clients/manage/manage-clients.md)」を参照してください。  

   > [!TIP]
   >   inventoryprovider.log 内のエラー コード 80041006 は、WMI プロバイダーのメモリ不足を意味します。 つまり、プロバイダーのメモリ クォータが上限に達しており、インベントリ プロバイダーを続行できません。
   > この場合、インベントリ エージェントがエントリ 0 のレポートを作成するため、インベントリ項目が報告されません。 <br/>
   > このエラーの考えられる解決方法は、ソフトウェア インベントリ コレクションのスコープを縮小することです。 インベントリ スコープを制限した後もエラーが発生する場合は、[_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671) クラスで定義されている [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/) プロパティを増やすことが、解決策となります。

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>ソフトウェア インベントリからフォルダーを除外するには  

1.  Notepad.exe を使用して、 **Skpswi.dat**という名前の空のファイルを作成します。  

2.  **Skpswi.dat** ファイルを右クリックして、**[プロパティ]** をクリックします。 SkpSwi.dat ファイルのプロパティで、**[非表示]** 属性を選択します。  

3.  ソフトウェア インベントリから除外する各クライアントのハード ドライブまたはフォルダーのルートに Skpswi.dat ファイルを配置します。 ****  

> [!NOTE]  
>  このファイルがクライアント コンピューターのドライブから削除されない限り、ソフトウェア インベントリによってクライアントのドライブが以後インベントリされることはありません。