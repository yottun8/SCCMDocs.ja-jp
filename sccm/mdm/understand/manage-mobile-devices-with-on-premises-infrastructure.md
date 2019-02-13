---
title: オンプレミス モバイル デバイス管理 (MDM)
titleSuffix: Configuration Manager
description: System Center Configuration Manager のデバイス管理ソリューション、オンプレミス モバイル デバイス管理について説明します。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63a82c6b81d5a2e09c6f73b79c39372c96ed4e07
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56143658"
---
# <a name="on-premises-mobile-device-management-mdm-in-system-center-configuration-manager"></a>System Center Configuration Manager でのオンプレミス モバイル デバイス管理 (MDM)

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のオンプレミス モバイル デバイス管理 は、デバイスのオペレーティング システムの組み込み管理機能 (Open Mobile Alliance Device Management や OMA DM 標準に基づく機能) を利用するデバイス管理ソリューションです。デバイス自体は、会社の Configuration Manager インフラストラクチャを使用して管理および維持します。 オンプレミス モバイル デバイス管理では、Microsoft Intune で管理機能を設定する必要がありますが、これはサブスクリプションのため (およびポリシー変更のためにチェックインするようにデバイスに通知するとき) にのみ必要であり、デバイスの管理や、デバイスに関するデータの格納に使用されることはありません。  

 ![オンプレミスの概念](media/On-premises-conceptual.png)  

 オンプレミス モバイル デバイス管理これは、同じく組み込みの OMA DM 機能を利用する Microsoft Intune とは異なりますが、すべての管理機能はクラウド サービス経由で提供されます。  オンプレミス モバイル デバイス管理 は、これまで Configuration Manager によって提供されてきたクライアント ベースの管理ソリューションとも異なります。具体的には、同じような企業インフラストラクチャを利用しますが、管理対象コンピューターとデバイスに個別にインストールされたクライアント ソフトウェアを使用しません。  

 次の表は、オンプレミス モバイル デバイス管理と従来のクライアント ベースの管理の長所と短所を比較した一覧です。  

|長所|短所|  
|----------------|-------------------|  
|**簡素化されたインフラストラクチャ** - 必要になるサイト システムの役割が少なくなります。<br /><br /> **管理が容易** - 管理機能がデバイスのオペレーティング システムに組み込まれているため、新しい管理機能を Configuration Manager システムに導入するときに、新しいバージョンのクライアント ソフトウェアが必要ありません。<br /><br /> **オンプレミス** - すべての管理とデータをオンプレミスに保持します。|**クライアント管理機能が少ない** - オーケストレーション、ソフトウェア使用状況測定、サード パーティ統合、タスク シーケンス、およびソフトウェア センター サポートがありません。<br /><br /> **デバイス サポートの制限** - 現時点で、オンプレミス モバイル デバイス管理は Windows 10 および Windows 10 Mobile を実行しているデバイスのみをサポートしています。|  

 次のトピックでは、オンプレミス モバイル デバイス管理用にデバイスを計画、準備、および登録する際に使用できる情報を提供します。  

-   [System Center Configuration Manager でのオンプレミス モバイル デバイス管理の計画](../plan-design/plan-on-premises-mdm.md)  

     Configuration Manager インフラストラクチャを設定し、オンプレミス モバイル デバイス管理でのデバイス登録を計画するときに考慮すべき事項について確認します。  

-   [System Center Configuration Manager でのオンプレミス モバイル デバイス管理の準備手順](../get-started/preparation-steps-for-on-premises-mdm.md)  

     Microsoft Intune サブスクリプションの設定、証明書の設定、サイト システムの役割のインストール、およびデバイス登録の設定を行うことで、Configuration Manager システムをオンプレミス モバイル デバイス管理用に準備する方法について確認します。  

-   [System Center Configuration Manager でのオンプレミス モバイル デバイス管理の対象となるデバイスの登録](../deploy-use/enroll-devices-on-premises-mdm.md)  

     登録を行う方法、ユーザーが自分のデバイスを登録する方法、および登録パッケージを使用してデバイスを一括登録する方法について確認します。  
