---
title: 'Intune サブスクリプションをセットアップする '
titleSuffix: Configuration Manager
description: System Center Configuration Manager でのオンプレミス モバイル デバイス管理のためのライセンスを追跡するように、Intune サブスクリプションをセットアップします。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: aa931c848bc3a25df452f8034530b6c740659e12
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347418"
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>System Center Configuration Manager でのオンプレミスのモバイル デバイス管理のための Microsoft Intune サブスクリプションをセットアップする

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のオンプレミス モバイル デバイス管理では、ライセンスを追跡するために Microsoft Intune サブスクリプションが必要です。 Intune サービスは、デバイスの管理または管理情報の保存には使用されません。 オンプレミス モバイル デバイス管理の場合、すべてのデバイス管理は、Configuration Manager インフラストラクチャによって処理されます。  

> [!NOTE]  
> バージョン 1610 以降の Configuration Manager では、Microsoft Intune とオンプレミスの Configuration Manager インフラストラクチャの両方で同時にモバイル デバイスを管理できます。   

> [!TIP]  
>  サイト システムの役割をインストールする前に、オンプレミス モバイル デバイス管理用の Intune サブスクリプションをセットアップすることによって、新しくインストールされたサイト システムの役割が機能するまでにかかる時間を最小限に抑えることをお勧めします。  

##  <a name="sign-up-for-microsoft-intune"></a>Microsoft Intune のセットアップ  
 オンプレミス モバイル デバイス管理が機能するには、Intune が必要です。 試用版または有料のサブスクリプションに[サインアップ](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/)し、次の手順に進んでサブスクリプションを Configuration Manager に追加します。  

##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Configuration Manager に Intune サブスクリプションを追加する  
 サブスクリプションを Configuration Manager に追加するには、Intune でモバイル デバイス管理のサブスクリプションを追加する場合と同じ基本的な手順に従います。 具体的な違いに関する以下のメモを参照して、[Intune サブスクリプションの構成](../deploy-use/configure-intune-subscription.md)に関するページに記載されている手順を使用します。  

> [!NOTE]  
>  Intune サブスクリプションを追加する場合は、次の点に注意してください。  
>   
>  -   Microsoft Intune サブスクリプションの追加ウィザードで指定したコレクションは、オンプレミス モバイル デバイス管理のユーザー権限の委任には使用されません。 これは、Intune でのモバイル デバイス管理にのみ使用されます。 ただし、ウィザードを先に進めるためには、コレクションを指定する必要があります。  
> -   ウィザードで指定したサイト コードの設定は、オンプレミス モバイル デバイス管理では無視されます。 使用されるのは、ユーザーに対してデバイスの登録の許可を与える登録プロファイルで指定されているサイト コードです。  
> -   多要素認証を有効にしないでください。 オンプレミス モバイル デバイス管理ではサポートされていません。  

##  <a name="configure-the-intune-subscription-for-on-premises-mobile-device-management"></a>オンプレミス モバイル デバイス管理用の Intune サブスクリプションを構成する  

1.  Configuration Manager コンソールで、**[Microsoft Intune サブスクリプション]** を右クリックし、**[プロパティ]** をクリックします。  

2.  [オンプレミス モバイル デバイス管理] ボックスで、次のいずれかを選択します。

  - オンプレミスのみでデバイスを管理する場合は、**[オンプレミスのデバイスのみを管理する]** の横にあるチェック ボックスをオンにして、**[OK]** をクリックします。  

      > [!NOTE]  
      >  このチェック ボックスをオンにすると、すべての管理情報をオンプレミスで保持し、データをクラウドにレプリケートしないように Intune サブスクリプションが構成されます。  

    - Intune とオンプレミス Configuration Manager の両方でデバイスを管理する場合は、ボックスをオフのままにします。

3.  Windows 10 Mobile デバイスを管理する場合は、 **[Microsoft Intune サブスクリプション]** を右クリックし、 **[プラットフォームの構成]**、  **[Windows Phone]** の順にクリックします。  

4.  **[Windows Phone 8.1 および Windows 10 Mobile]** の横にあるチェック ボックスをオンにして、 **[OK]** をクリックします。  

5.  Windows 10 のデスクトップ コンピューターを管理する場合は、 **[Microsoft Intune サブスクリプション]** を右クリックし、 **[プラットフォームの構成]**、 **[Windows の登録を有効にする]** の順にクリックします。  

6.  **[Windows の登録を有効にする]** の横にあるチェック ボックスをオンにして、 **[OK]** をクリックします。  
