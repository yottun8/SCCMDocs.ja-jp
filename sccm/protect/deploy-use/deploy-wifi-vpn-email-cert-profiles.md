---
title: Wi-Fi、VPN、電子メール、および証明書プロファイルの展開
titleSuffix: Configuration Manager
description: System Center Configuration Manager で Wi-Fi、VPN、電子メール、および証明書のプロファイルを展開する方法について説明します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63b52b42a9957ed8728d0942988067fef2be6271
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129716"
---
# <a name="deploy-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager でのプロファイルの展開

*適用対象: System Center Configuration Manager (Current Branch)*

プロファイルを使用するには、1 つまたは複数のコレクションに展開する必要があります。  

 **[Wi-Fi プロファイルの展開]**、**[VPN プロファイルの展開]**、**[Exchange ActiveSync プロファイルの展開]**、または **[Deploy Certificate Profile]** (証明書プロファイルの展開) ダイアログ ボックスを使用して、これらのプロファイルの展開を構成します。 この構成には、プロファイルの展開先のコレクションの定義と、プロファイルのコンプライアンスを評価する頻度の指定が含まれます。  

> [!NOTE]
>  同じユーザーに複数の会社リソース アクセス プロファイルを展開する場合は、次の動作が発生します。  
> 
> - 競合している設定にオプションの値が含まれている場合、その値はデバイスに送信されません。  
>   -   競合する設定に必須の値が含まれている場合、既定値がデバイスに送信されます。 既定値がない場合は、全体の会社リソース アクセス プロファイルは失敗します。 たとえば、同じユーザーに 2 つの電子メール プロファイルを展開し、**[Exchange ActiveSync ホスト]** または **[電子メール アドレス]** に指定した値が異なる場合、その両方の設定は必須のため、電子メール プロファイルは失敗します。  
> 
> - 証明書プロファイルを展開する前に、まず、インフラストラクチャを構成して証明書プロファイルを作成する必要があります。 詳細については、以下のトピックを参照してください。  
> 
>   -   [System Center Configuration Manager での証明書インフラストラクチャの構成](certificate-infrastructure.md)  
> - [System Center Configuration Manager で証明書プロファイルを作成する方法](create-certificate-profiles.md)    
> 
> [!IMPORTANT]
>  VPN プロファイルの展開を削除するときに、VPN プロファイルはクライアント デバイスから削除されません。 デバイスからプロファイルを削除する場合、手動で削除する必要があります。

## <a name="deploying--profiles"></a>プロファイルの展開  


1.  System Center Configuration Manager コンソールで、**[資産とコンプライアンス]** を選択します。  

2.  **[資産とコンプライアンス]** ワークスペースで、**[コンプライアンス設定]**、**[会社リソースのアクセス]** の順に展開してから、**[Wi-Fi プロファイル]** などの適切なプロファイル タイプを選択します。  

3.  プロファイルの一覧で、展開するプロファイルを選択してから、**[ホーム]** タブの **[展開]** グループで、**[展開]** をクリックします。  

4.  プロファイルの展開ダイアログ ボックスで、次の情報を指定します。  

    -   **コレクション**: **[参照]** をクリックして、プロファイルを展開するコレクションを選択します。  

    -   **アラートを生成する**: このオプションを有効にすると、プロファイルのコンプライアンスが、指定した日付と時刻までに指定した割合に達しなかった場合に生成されるアラートを構成できます。 アラートを System Center Operations Manager に送信するかどうかも指定できます。  

    -   -   **ランダム遅延 (時間)**: (Simple Certificate Enrollment Protocol 設定を含む証明書プロファイルのみ) ネットワーク デバイス登録サービスの処理量が多くなりすぎないように、処理を延期できる期間を指定します。 既定値は **64** 時間です。  

    -   **この <type> プロファイルのコンプライアンス評価スケジュールを指定してください**: 展開されたプロファイルをクライアント コンピューターで評価するスケジュールを指定します。 単純なスケジュールとカスタム スケジュールの 2種類あります。  

        > [!NOTE]  
        >  プロファイルは、ユーザーがログオンしたときにクライアント コンピューターによって評価されます。  

5.  **[OK]** をクリックしてダイアログ ボックスを閉じると、展開が作成されます。

### <a name="see-also"></a>関連項目  

[System Center Configuration Manager で Wi-Fi、VPN、および電子メールのプロファイルを監視する方法](monitor-wifi-email-vpn-profiles.md)

[System Center Configuration Manager で証明書プロファイルを監視する方法](monitor-certificate-profiles.md)
