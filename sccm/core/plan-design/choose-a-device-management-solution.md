---
title: デバイス管理ソリューションの選択
titleSuffix: Configuration Manager
description: PC、サーバー、およびデバイスを管理するために Configuration Manager で提供されるソリューションについて説明します。
ms.date: 01/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1214a5b73b3e6b1bddab8a3918ddd32af0cacb68
ms.sourcegitcommit: f7b2fe522134cf102a3447505841cee315d3680c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2019
ms.locfileid: "55570202"
---
# <a name="choose-a-device-management-solution-for-configuration-manager"></a>Configuration Manager のデバイス管理ソリューションの選択

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager は、PC、サーバー、デバイスを管理するためのさまざまなソリューションを提供します。 ご自身の組織に最適な管理ソリューションを選択します。 管理する必要のあるデバイス プラットフォームや、必要な管理機能に基づいて判断します。  


> [!Important]  
> 2018 年 8 月 14 日の時点では、ハイブリッド モバイル デバイス管理は[非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)です。 詳細については、[ハイブリッド MDM の概要](/sccm/mdm/understand/hybrid-mobile-device-management)に関するページを参照してください。<!--Intune feature 2683117-->  
<!-- SCCMDocs issue 1197 -->



## <a name="overview"></a>概要

この記事は、次の 4 つのデバイス管理ソリューションを対象としています。 
- [構成マネージャー クライアント](#bkmk_sccm)
- [Configuration Manager でのオンプレミス モバイル デバイス管理 (MDM)](#bkmk_opmdm)
- [Microsoft Intune での共同管理](#bkmk_intune)
- [Microsoft Exchange](#bkmk_opmdm)

これらのデバイス管理ソリューションは、単独で使用することも、相互に組み合わせて使用することもできます。 たとえば、クライアントベースの管理方法を使用して組織内のコンピューターとサーバーの管理を行いつつ、共同管理を使用してインターネット ベースのラップトップを管理することができます。 このようにアプローチを組み合わせることによって、デバイス管理のすべてのニーズに対応することができます。  

また、この記事には、次の要因で管理ソリューションを比較した 2 つの表も含まれています。 
- [サポートされているプラットフォームによる比較](#bkmk_comp1)
- [管理機能による比較](#bkmk_comp2)


### <a name="bkmk_sccm"></a> 構成マネージャー クライアント  

このオプションを使うには、デバイス上に Configuration Manager クライアントをインストールする必要があります。 これにより、環境内の PC、サーバー、およびその他のデバイスを管理するための機能のほとんどが提供されます。 

詳細については、[クライアントのインストール方法](/sccm/core/clients/deploy/plan/client-installation-methods)に関する記事をご覧ください。  


### <a name="bkmk_opmdm"></a> オンプレミス MDM  

このオプションでは、Windows 10 に組み込まれているデバイス管理機能が使われます。 クライアント ベースの管理と同様のフル機能は提供されませんが、オンプレミスのモバイル デバイス管理では簡略化された方法で管理することができます。 デバイスを管理するために、オンプレミスの Configuration Manager リソースが使われます。  

詳しくは、「[オンプレミス インフラストラクチャを使用したモバイル デバイスの管理](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure)」をご覧ください。  


### <a name="bkmk_comanage"></a> Microsoft Intune での共同管理

共同管理は、既存の Configuration Manager の展開を Microsoft 365 のクラウドにアタッチするための主要な方法の 1 つです。 これによって、Configuration Manager と Microsoft Intune の両方を使って Windows 10 デバイスを同時に管理することができます。 共同管理を使うと、新しい機能を追加して、Configuration Manager 内の既存の投資をクラウドにアタッチできます。 

詳細については、「[共同管理とは](/sccm/comanage/overview)」をご覧ください。  


### <a name="bkmk_exchange"></a> Microsoft Exchange  

このオプションでは、Exchange Server コネクタを使用して、Configuration Manager に複数の Exchange サーバーを接続します。 これにより、Exchange ActiveSync に接続できるデバイスが一元的に管理されます。 Configuration Manager コンソールから Exchange のモバイル デバイス管理機能を構成できます。 機能の例としては、複数の Exchange サーバー向けのリモート デバイス ワイプや設定コントロールなどがあります。

詳しくは、「[Configuration Manager と Exchange によるモバイル デバイスの管理](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)」をご覧ください。  



## <a name="bkmk_comp1"></a> サポートされているプラットフォームでソリューションを比較する  

|プラットフォーム|Configuration Manager クライアント|オンプレミス MDM|Configuration Manager と Exchange の併用|  
|--------|----------------------------|---------------|-----------------------------------|  
|Android| | |はい|  
|iOS| | |はい|  
|Mac OS X|はい| |はい|  
|UNIX/Linux|はい| |はい|  
|Windows 10|はい|はい|はい|  
|Windows 10 Mobile| |はい|はい|  
|Windows (以前のバージョン)|はい| |はい|  
|Windows Server|はい| |はい|  
|Windows CE|○ (モバイル デバイス レガシ クライアントを使用)| |はい|  
|Windows Embedded|はい| | |  
|Windows Mobile| | |はい|  

サポート対象プラットフォームの一覧については、「[Supported operating systems for clients and devices for System Center Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md)」 (System Center Configuration Manager のクライアントとデバイスでサポートされるオペレーティング システム) を参照してください。

Microsoft では、Intune を使って Android、iOS、および Windows 10 モバイル デバイスを管理することをお勧めします。 詳細については、「[Microsoft Intune とは](https://docs.microsoft.com/intune/what-is-intune)」をご覧ください。



##  <a name="bkmk_comp2"></a> 管理機能でソリューションを比較する  

|管理機能|Configuration Manager クライアント|オンプレミス MDM|Configuration Manager と Exchange の併用|  
|--------|----------------------------|---------------|-----------------------------------|  
|モバイル デバイスと Configuration Manager 間の公開キー基盤 (PKI) セキュリティ (相互認証と SSL によるデータ転送暗号化を使用)|はい|はい| |  
|クライアントのインストール|はい| | |  
|インターネット経由のサポート|はい| | |  
|探索|はい| |はい|  
|ハードウェア インベントリ|はい|はい|はい|  
|ソフトウェア インベントリ|はい| |はい|  
|設定|はい|はい|はい|  
|ソフトウェアの展開|はい|はい| |  
|フォールバック ステータス ポイントによる監視|はい| | |  
|管理ポイントへの接続|はい|はい| |  
|配布ポイントへの接続|はい|はい| |  
|Configuration Manager からのブロック|はい|はい| |  
|Exchange Server (および Configuration Manager) からの検疫とブロック| | |はい|  
|リモート ワイプ| |はい|はい|  


