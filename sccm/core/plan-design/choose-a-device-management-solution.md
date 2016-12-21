---
title: "System Center Configuration Manager のデバイス管理ソリューションの選択 | Microsoft Docs"
description: "PC、サーバー、およびデバイスを管理するために System Center Configuration Manager で提供されるソリューションについて説明します。"
ms.custom: na
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: 14
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 099e0001c01713224988e5b49d02cb358e3015d6
ms.openlocfilehash: f4f0a8e8b1b5aae2586cc885734f405f7e7f9ff5


---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>System Center Configuration Manager のデバイス管理ソリューションの選択

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager (ConfgMgr または SCCM とも呼ばれます) には、PC、サーバー、およびデバイスを管理するためのさまざまなソリューションが備わっています。 管理する必要のあるデバイス プラットフォームや、必要な管理機能に基づいて、適切なソリューションを選択できます。  


##  <a name="overview-of-device-management-solutions"></a>デバイス管理ソリューションの概要  
 この概要セクションの後には、各管理ソリューションを[サポートされているモバイル デバイス プラットフォーム別](#compare-device-management-solutions-based-on-supported-mobile-device-platforms)と[管理機能別](#compare-mobile-device-management-solutions-based-on-management-functionality)に比較した 2 つの表があります。
  

-   **Configuration Manager クライアントを使用したデバイスの管理**  

     このオプションでは、デバイスに Configuration Manager クライアント アプリケーションをインストールする必要はありますが、環境内の PC、サーバー、およびその他のデバイスを管理するための機能が最も多く提供されます。   

     詳細については、「[System Center Configuration Manager でのクライアントのインストール方法](/sccm/core/client/deploy/plan/client-installation-methods)」を参照してください。  

-   **オンプレミス Configuration Manager インフラストラクチャでのモバイル デバイスの管理**  

     このオプションでは、一部のデバイス プラットフォームのオペレーティング システムに組み込まれているデバイス管理機能を使用します。 オンプレミス モバイル デバイス管理では、クライアント ベースの管理とは異なりフル機能は提供されませんが、管理するための簡略化された方法が提供されます。この方法では、オンプレミス Configuration Manager リソースを使用して、デバイスのアクセスと管理を行います。 オンプレミス モバイル デバイス管理は、現在、Windows 10 PC と Windows 10 Mobile デバイスのみでサポートされています。  

     このソリューションの詳細については、「[モバイル デバイスを管理するには、System Center Configuration Manager でオンプレミス インフラストラクチャを使用します。](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」を参照してください。  

-   **Microsoft Intune を使用してモバイル デバイスを管理する (ハイブリッド)**  

     このオプションでは、Configuration Manager のオンプレミス リソースを使用する代わりに、Microsoft Intune を使用してデバイスを登録し、管理します。 Intune でデバイスが管理されている場合でも、Configuration Manager コンソールで管理タスクにアクセスできます。 このオプションは、Windows 10 Mobile、Windows Phone、iOS、Mac OS X、Android を含む主要なモバイル デバイス オペレーティング システムをすべてサポートします。 また、組織内の Windows 8.1 と Windows 10 のコンピューターの管理も提供します。  

     このソリューションの詳細については、「[System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM)](../../mdm/understand/hybrid-mobile-device-management.md)」を参照してください。  

-   **Exchange によるモバイル デバイスの管理**  

     このオプションでは、Exchange Server コネクタを使用して複数の Exchange サーバーを Configuration Manager に接続し、Exchange ActiveSync に接続可能なデバイスの管理を一元化します。 Configuration Manager コンソールから、複数の Exchange サーバー向けにリモート デバイス ワイプおよび設定コントロールといった、Exchange モバイル デバイス管理機能を構成できます。  

     このソリューションの詳細については、「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください。  

 これらのデバイス管理ソリューションは、単独で使用することも、相互に組み合わせて使用することもできます。 たとえば、クライアントベースの管理方法を使用して組織内のコンピューターとサーバーの管理を行いつつ、Intune を使用してモバイル デバイスを管理することができます。 このようにアプローチを組み合わせることによって、Configuration Manager コンソールでデバイス管理のすべてのニーズに対応することができます。  

## <a name="compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a>サポートされているモバイル デバイス プラットフォームに基いたデバイス管理ソリューションの比較  

|プラットフォーム|Configuration Manager クライアントを使用|Configuration Manager と Microsoft Intune の併用 (ハイブリッド)|オンプレミス モバイル デバイス管理|Configuration Manager と Exchange の併用|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||○||○|  
|iOS||○||○|  
|Mac OS X|○|||○|  
|UNIX/Linux|○|||○|  
|Windows 10|○|[はい]|[はい]|○|  
|Windows 10 Mobile||○|[はい]|○|  
|Windows (以前のバージョン)|○|[はい]||○|  
|Windows CE|○ (モバイル デバイス レガシ クライアントを使用)|||○|  
|Windows Embedded|○||||  
|Windows Phone||○||○|  
|Windows Server|○|||○|  

 サポート対象プラットフォームの一覧については、「[Supported operating systems for clients and devices for System Center Configuration Manager](configs\supported-operating-systems-for-clients-and-devices.md)」 (System Center Configuration Manager のクライアントとデバイスでサポートされるオペレーティング システム) を参照してください。

##  <a name="a-namebkmkcomp2a-compare-mobile-device-management-solutions-based-on-management-functionality"></a><a name="bkmk_comp2"></a> 管理機能に基づいたモバイル デバイス管理ソリューションの比較  

|管理機能|Configuration Manager クライアントを使用|Configuration Manager と Microsoft Intune の併用 (ハイブリッド)|オンプレミス モバイル デバイス管理|Configuration Manager と Exchange の併用|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|相互認証と SSL によるデータ転送暗号化を使用した、モバイル デバイスと Configuration Manager 間の公開キー基盤 (PKI) セキュリティ|○|[はい]|○||  
|クライアントのインストール|○||||  
|インターネット経由のサポート|○||||  
|探索|○|||○|  
|ハードウェア インベントリ|○|[はい]|[はい]|○|  
|ソフトウェア インベントリ|○|||○|  
|設定|○|[はい]|[はい]|○|  
|ソフトウェアの展開|○|[はい]|○||  
|フォールバック ステータス ポイントによる監視|○||||  
|管理ポイントへの接続|○||○||  
|配布ポイントへの接続|○|[はい]|○||  
|Configuration Manager からのブロック|○|[はい]|○||  
|Exchange Server (および Configuration Manager) からの検疫とブロック||||○|  
|リモート ワイプ|○|[はい]|[はい]|○|  



<!--HONumber=Dec16_HO3-->


