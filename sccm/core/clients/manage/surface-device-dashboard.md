---
title: Surface デバイス ダッシュボード
titleSuffix: System Center Configuration Manager
description: ダッシュボードを使用して Surface デバイスに関する情報を確認します。
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-other
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: 8c9171ed5b239091b7f77b534368422575c0f2f4
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2018
---
# <a name="surface-device-dashboard-in-system-center-configuration-manager"></a>System Center Configuration Manager の Surface デバイス ダッシュボード

*適用対象: System Center Configuration Manager (Current Branch)*

バージョン 1802 以降の Surface デバイス ダッシュボードでは、ご利用の環境で検出された Surface デバイスに関する情報がひとめでわかります。 <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Surface デバイス ダッシュボードを開く

Surface デバイス ダッシュボードを開くには、次の手順を使用します。 

1. Configuration Manager コンソールを開きます。 
2. **[監視]** ノードをクリックします。 
3. ダッシュボードを読み込むには、**[Surface デバイス]** をクリックします。

**Surface デバイス ダッシュボード**
![Surface デバイス ダッシュボード](media\Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Surface デバイス ダッシュボードでの情報の確認

Surface デバイス ダッシュボードには、ご利用の環境の 3 つのグラフが表示されます。 

- **Surface デバイスの割合** - 環境全体の Surface デバイスの割合が示されます。

    ![Surface デバイスの割合のグラフ](media\Percent-Surface-Devices.PNG)
- **Surface モデル** - Surface モデルごとのデバイスの数が表示されます。 
    - グラフ セクションにカーソルを合わせると、選択されたモデルである Surface デバイスの割合が表示されます。 

         ![Surface モデルのグラフ](media\Surface-Models-Hover.PNG)
    - グラフ セクションをクリックすると、モデルのデバイス リストが表示されます。 
        ![Surface モデル デバイスのリスト](media\Surface-Model-Device-List.PNG)

- **上位 5 つのファームウェア バージョン** - 環境内の上位 5 つのファームウェア モデルを示すグラフが表示されます。 
    - グラフ セクションにカーソルを合わせると、選択されたファームウェア バージョンである Surface デバイスの数が表示されます。 
       ![Surface モデル デバイスのリスト](media\Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>説明

Surface デバイスの詳細については、以下を参照してください。
 - [Surface]( https://go.microsoft.com/fwlink/?linkid=861998) Web サイト。
    
Configuration Manager に Surface のファームウェアの更新プログラムを配布する方法については、次を参照してください。
 - [How to manage Surface driver updates in Configuration Manager]( https://support.microsoft.com/help/4098906)(Configuration Manager で Surface のドライバーの更新プログラムを管理する方法)



