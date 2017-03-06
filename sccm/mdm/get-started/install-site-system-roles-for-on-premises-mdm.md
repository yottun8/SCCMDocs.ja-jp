---
title: "オンプレミス MDM の役割のインストール - Configuration Manager | Microsoft Docs"
description: "System Center Configuration Manager でのオンプレミス モバイル デバイス管理のサイト システムの役割のインストール"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
caps.latest.revision: 9
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3743c80b0c2b5142f3a537ba3855ffd14794d42b
ms.openlocfilehash: 916b971f851f968f6534ac834bd3182cc61614aa
ms.lasthandoff: 01/24/2017


---
# <a name="install-site-system-roles-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>System Center Configuration Manager でのオンプレミス モバイル デバイス管理のサイト システムの役割のインストール

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のオンプレミス モバイル デバイス管理では、Configuration Manager サイト インフラストラクチャに次のサイト システムの役割を必要とします。  

-   登録ポイント  

-   登録プロキシ ポイント  

-   配布ポイント  

-   デバイス管理ポイント  

-   [サービス接続ポイント]  

 ほとんどの PC とデバイスを Configuration Manager クライアント ソフトウェアを使用して管理している組織にオンプレミス モバイル デバイス管理を追加する場合、ほとんどのサイト システムの役割が既存のインフラストラクチャの一部として既にインストールされている可能性があります。 インストールされていない場合、「[System Center Configuration Manager のサイト システム役割の追加](../../core/servers/deploy/configure/add-site-system-roles.md)」を参照してください。サイトに追加する方法をご確認いただけます。  

> [!NOTE]  
>  デバイス管理ポイント サイト システムの役割を持つデータベース レプリカを使用する場合、新しく登録されたデバイスは、データベース レプリカがデバイス管理ポイントと同期するまでの間、デバイス管理ポイントへの接続に失敗します。 この接続エラーは、正常に接続するために必要な、新しく登録されたデバイスに関する情報が、データベース レプリカにないために発生します。 レプリカは 5 分ごとに同期するため、デバイスが接続に失敗するのは、登録後の最初の 5 分間です (通常、2 回の接続試行)。その後、デバイスは正常に接続します。  

 既存のサイト システムを使用するか、新しいサイト システムを追加するかに関係なく、最新のデバイスを管理するために使用するようそれらを構成する必要があります。 以下の手順に従って、オンプレミスのモバイル デバイス管理で正しく機能するように配布ポイントとデバイス管理ポイントを構成します。  

> [!NOTE]  
>  Configuration Manager の現在のブランチは、デバイスからオンプレミス モバイル デバイス管理の配布ポイントとデバイス管理ポイントへのイントラネット接続のみをサポートしています。 ただし、Mac OS X コンピューターも管理している場合は、それらのクライアントにはこれらのサイト システムの役割へのインターネット接続が必要となります。 その場合、配布ポイントとデバイス管理ポイントのプロパティを構成するときに、代わりに **[イントラネットとインターネットの接続を許可する]** 設定を使用する必要があります。  

### <a name="to-configure-site-system-roles-to-manage-modern-devices"></a>最新のデバイスを管理するようサイト システムの役割を構成するには:  

1.  Configuration Manager コンソールで、**[管理]**、**[概要]**、**[サイトの構成]**、**[サーバーとサイト システムの役割]** の順にクリックします。  

2.  構成する配布ポイントまたはデバイス管理ポイントとともにサイト システムのサーバーを選択し、**[サイト システム]** のプロパティを開き、FQDN が指定されていることを確認します。 **[OK]**をクリックします。  

3.  配布ポイント サイト システムの役割のプロパティを開きます。 [全般] タブで、**[HTTPS]** が選択されていることを確認し、**[イントラネットのみのクライアント接続を許可する]** を選択します。  

     Configuration Manager クライアントとともに Mac コンピューターも別に管理している場合、代わりに **[イントラネットとインターネットの接続を許可する]** を使用します。  

    > [!NOTE]  
    >  イントラネット接続用に構成された配布ポイントに対しては、サイトの境界を構成する必要があります。 Configuration Manager の現在のブランチは、オンプレミス モバイル デバイス管理に関して、IPv4 境界のみをサポートしています。 サイト境界構成については、「[System Center Configuration Manager のサイト境界と境界グループの定義](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)」を参照してください。  

4.  **[モバイル デバイスがこの配布ポイントに接続するのを許可する]** の横にあるチェック ボックスをクリックし、**[OK]** をクリックします。  

5.  管理ポイント サイト システムの役割のプロパティを開きます。 [全般] タブで、**[HTTPS]** が選択されていることを確認し、**[イントラネットのみのクライアント接続を許可する]** を選択します。  

     Configuration Manager クライアントとともに Mac コンピューターも別に管理している場合、代わりに **[イントラネットとインターネットの接続を許可する]** を使用します。  

6.  **[モバイル デバイスおよび Mac コンピューターでこの管理ポイントを使用できるようにする]** の横にあるチェック ボックスをクリックします。 **[OK]**をクリックします。  

     これにより実際、管理ポイントがデバイス管理ポイントに変換されます。  

 最新のデバイスを管理するためのサイト システムの役割を追加して構成したら、管理対象のデバイスを登録して通信するために、信頼されるエンドポイントとしてそれらの役割をホストするサーバーを構成する必要があります。 詳細については、「[System Center Configuration Manager でのオンプレミスのモバイル デバイス管理のために信頼された通信用の証明書をセットアップする](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)」を参照してください。  

