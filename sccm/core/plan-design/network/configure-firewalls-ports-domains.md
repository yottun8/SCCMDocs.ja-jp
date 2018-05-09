---
title: ファイアウォールとドメイン
titleSuffix: Configuration Manager
description: System Center Configuration Manager 通信の準備としてファイアウォール、ポート、ドメインを設定します。
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ee7494b582828014114d41eb6bb721a7e1fd5c16
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-firewalls-ports-and-domains-for-system-center-configuration-manager"></a>System Center Configuration Manager のファイアウォール、ポート、ドメインの設定

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager をサポートするためにネットワークを準備するには、Configuration Manager で使用される通信をファイアウォールで許可するなど、インフラストラクチャの設定を計画します。  

|考慮事項|詳細|  
|-------------------|-------------|  
|さまざまな Configuration Manager 機能で使用する**ポートとプロトコル**。 必須のポートと、カスタマイズできる**ドメインとサービス**があります。|ほとんどの Configuration Manager 通信では、HTTP 通信にポート 80、HTTPS 通信にポート 443 など、共通のポートを使用します。 ただし、[一部のサイト システムの役割では、カスタム Web サイトとカスタム ポートの使用をサポート](/sccm/core/plan-design/network/websites-for-site-system-servers)しています。<br /><br /> **Configuration Manager を展開する前に**、使用する予定のポートを特定し、ファイアウォールを適宜設定します。<br /><br /> **Configuration Manager をインストールした後でポートを変更する必要がある場合**、必ずデバイスとネットワークでファイアウォールを更新し、Configuration Manager 内からポートの構成を変更してください。<br /><br /> 詳細については、次をご覧ください。 </br>- [クライアント通信ポートを構成する方法](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [Configuration Manager で使用されるポート](../../../core/plan-design/hierarchy/ports.md) </br>- [サービス接続ポイントのインターネット アクセス要件](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|サイト サーバーとクライアントが使用する可能性のある**ドメインとサービス**。|Configuration Manager 機能では、サイト サーバーおよびクライアントが Windowsudpate.microsoft.com や Microsoft Intune サービスなどのインターネット上の特定のサービスおよびドメインにアクセスする必要がある場合があります。<br /><br /> Microsoft Intune を使用してモバイル デバイスを管理する場合は、[Intune で必要なポートとドメイン](https://docs.microsoft.com/en-us/intune/get-started/network-infrastructure-requirements-for-microsoft-intune)へのアクセスも設定する必要があります。|  
|サイト システム サーバーとクライアント通信用の**プロキシ サーバー** 。 異なるサイト システム サーバーとクライアントに対して別のプロキシ サーバーを指定することができます。|これらの構成はサイト システムの役割またはクライアントのインストール時に行われるため、サイト システムの役割とクライアントを構成するときに注意が必要なのは、後で参照するプロキシ サーバー構成のみです。<br /><br /> 展開でプロキシ サーバーを使用する必要があるかどうかがわからない場合は、「[System Center Configuration Manager でのプロキシ サーバーのサポート](../../../core/plan-design/network/proxy-server-support.md)」を確認し、プロキシ サーバーを使用できるサイト システムの役割とクライアントの動作についてご理解ください。|   
|  
