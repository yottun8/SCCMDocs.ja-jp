---
title: '準備手順 '
titleSuffix: Configuration Manager
description: System Center Configuration Manager でのオンプレミス モバイル デバイス管理でデバイスの管理を準備します。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 711af365353d68020a7bbbef8026f452d4203ce3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="preparation-steps-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>System Center Configuration Manager でのオンプレミス モバイル デバイス管理の準備手順

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager オンプレミス モバイル デバイス管理でデバイスを管理するには、Configuration Manager インフラストラクチャをセットアップして、必要なサイト システムの役割 (登録プロキシ ポイント、登録ポイント、デバイス管理ポイント、および配布ポイント) が信頼されたチャネル経由で管理対象のモバイル デバイスと通信できるようにする必要があります。\-  

 オンプレミス モバイル デバイス管理用に Configuration Manager システムを準備するには、次の高度なタスクを実行する必要があります。\-  

-   [System Center Configuration Manager でのオンプレミスのモバイル デバイス管理のための Microsoft Intune サブスクリプションをセットアップする](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)  

     このタスクでは、Microsoft Intune にサインアップし、し、Configuration Manager コンソールで、サブスクリプションを Configuration Manager に追加します。 この手順はライセンス付与のためにのみ必要となっています。 Intune はデバイスの管理にも、管理情報の保存にも使用されません。 デバイスの調整と管理のすべては、オンプレミスの Configuration Manager インフラストラクチャを使用して組織の計画に沿って行われます。  

-   [System Center Configuration Manager でのオンプレミス モバイル デバイス管理のサイト システムの役割のインストール](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     このタスクでは、オンプレミスの Configuration Manager インフラストラクチャによるデバイス管理に必要なサイト システムの役割をインストールして構成します。 オンプレミス モバイル デバイス管理には、登録プロキシ ポイント、登録ポイント、デバイス管理ポイント、および配布ポイントの各サイト システムの役割が最低限必要です。\-  

-   [System Center Configuration Manager でのオンプレミスのモバイル デバイス管理のために信頼された通信用の証明書をセットアップする](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

     このタスクでは、オンプレミスの Configuration Manager インフラストラクチャを構成して、管理対象のデバイスと、必要なサイト システムの役割をホストするサーバーとの間の信頼できる通信 (HTTPS) を許可します。  

-   [System Center Configuration Manager でのオンプレミスのモバイル デバイス管理のデバイス登録の設定](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

     このタスクでは、ユーザーにコンピューターとデバイスの登録の許可を与えます。またデバイス (通常は、ドメインに参加していないデバイス) に信頼されたルート証明書をインストールして、サイト システム サーバーへの HTTPS 接続を許可します。  
