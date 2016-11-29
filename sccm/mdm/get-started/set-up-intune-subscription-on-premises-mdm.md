---
title: "Intune サブスクリプションをセットアップする | オンプレミス | System Center Configuration Manager"
description: "System Center Configuration Manager でのオンプレミス モバイル デバイス管理のためのライセンスを追跡するように、Intune サブスクリプションをセットアップします。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
caps.latest.revision: 8
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4daf5d6ea30aa1fb4aa189ef6da9b364fe197805


---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>System Center Configuration Manager でのオンプレミスのモバイル デバイス管理のための Microsoft Intune サブスクリプションをセットアップする

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のオンプレミス モバイル デバイス管理では、ライセンスを追跡するために Microsoft Intune サブスクリプションが必要です。 Intune サービスは、デバイスの管理または管理情報の保存には使用されません。 オンプレミス モバイル デバイス管理の場合、すべてのデバイス管理は、Configuration Manager インフラストラクチャによって処理されます。  

> [!IMPORTANT]  
>  Configuration Manager では、Microsoft Intune とオンプレミスの Configuration Manager インフラストラクチャの両方を管理機関として同時に使用することはできません。 そのため、オンプレミス管理のために Intune サブスクリプションをセットアップする場合は、結果的に Intune での管理を無効にすることになります。  

 オンプレミス モバイル デバイス管理で動作するように Intune サービスをセットアップするには、次の概要手順のようにします。  

-   [Microsoft Intune のセットアップ](#bkmk_signup)  

-   [Configuration Manager に Intune サブスクリプションを追加する](#bkmk_addSub)  

-   [オンプレミス モバイル デバイス管理用の Intune サブスクリプションを構成する](#bkmk_configure)  

> [!TIP]  
>  サイト システムの役割をインストールする前に、オンプレミス モバイル デバイス管理用の Intune サブスクリプションをセットアップすることによって、新しくインストールされたサイト システムの役割が機能するまでにかかる時間を最小限に抑えることをお勧めします。  

##  <a name="a-namebkmksignupa-sign-up-for-microsoft-intune"></a><a name="bkmk_signup"></a> Microsoft Intune のセットアップ  
 オンプレミス モバイル デバイス管理が機能するには、Intune が必要です。 試用版または有料のサブスクリプションに[サインアップ](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/)し、次の手順に進んでサブスクリプションを Configuration Manager に追加します。  

##  <a name="a-namebkmkaddsuba-add-the-intune-subscription-to-configuration-manager"></a><a name="bkmk_addSub"></a> Configuration Manager に Intune サブスクリプションを追加する  
 サブスクリプションを Configuration Manager に追加するには、Intune でモバイル デバイス管理のサブスクリプションを追加する場合と同じ基本的な手順に従います。 以下の注意事項で具体的な違いを確認した後、「[System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM)](../../mdm/plan-design/hybrid-mobile-device-management.md)」の「[Microsoft Intune サブスクリプションを作成するには](../../mdm/plan-design/hybrid-mobile-device-management.md#bkmk_subscription)」の手順に従ってください。  

> [!NOTE]  
>  Intune サブスクリプションを追加する場合は、次の点に注意してください。  
>   
>  -   Microsoft Intune サブスクリプションの追加ウィザードで指定したコレクションは、オンプレミス モバイル デバイス管理のユーザー権限の委任には使用されません。 これは、Intune でのモバイル デバイス管理にのみ使用されます。 ただし、ウィザードを先に進めるためには、コレクションを指定する必要があります。  
> -   ウィザードで指定したサイト コードの設定は、オンプレミス モバイル デバイス管理では無視されます。 使用されるのは、ユーザーに対してデバイスの登録の許可を与える登録プロファイルで指定されているサイト コードです。  
> -   多要素認証を有効にしないでください。 オンプレミス モバイル デバイス管理ではサポートされていません。  

##  <a name="a-namebkmkconfigurea-configure-the-intune-subscription-for-on-premises-mobile-device-management"></a><a name="bkmk_configure"></a> オンプレミス モバイル デバイス管理用の Intune サブスクリプションを構成する  

1.  Configuration Manager コンソールで、**[Microsoft Intune サブスクリプション]** を右クリックし、**[プロパティ]** をクリックします。  

2.  オンプレミス モバイル デバイス管理のボックスで、 **[オンプレミスのデバイスのみを管理する]**の横にあるチェック ボックスをオンにして、 **[OK]**をクリックします。  

    > [!NOTE]  
    >  このチェック ボックスをオンにすると、すべての管理情報をオンプレミスで保持し、データをクラウドにレプリケートしないように Intune サブスクリプションが構成されます。  

3.  Windows 10 Mobile デバイスを管理する場合は、 **[Microsoft Intune サブスクリプション]**を右クリックし、 **[プラットフォームの構成]**、  **[Windows Phone]**の順にクリックします。  

4.  **[Windows Phone 8.1 および Windows 10 Mobile]**の横にあるチェック ボックスをオンにして、 **[OK]**をクリックします。  

5.  Windows 10 のデスクトップ コンピューターを管理する場合は、 **[Microsoft Intune サブスクリプション]**を右クリックし、 **[プラットフォームの構成]**、 **[Windows の登録を有効にする]**の順にクリックします。  

6.  **[Windows の登録を有効にする]**の横にあるチェック ボックスをオンにして、 **[OK]**をクリックします。  



<!--HONumber=Nov16_HO1-->


