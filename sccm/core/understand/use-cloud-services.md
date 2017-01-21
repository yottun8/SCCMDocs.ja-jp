---
title: "クラウド サービスの使用 | Microsoft Docs"
description: "オンプレミスのインフラストラクチャを補足するための System Center Configuration Manager 用クラウド リソースをプロビジョニングします。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 539ad555b85b7517507c21718dab0b79fdf4dfb8


---
# <a name="use-cloud-services-with-system-center-configuration-manager"></a>クラウド サービスを System Center Configuration Manager と一緒に使う

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager は、クラウドベースのオプションをいくつかサポートしています。オンプレミス インフラストラクチャを補完し、次のようなビジネス上の問題を解決することができます。  

-   BYOD を管理する (Intune をモバイル デバイス管理に使用する)  

-   企業ファイアウォール外部のイントラネット上の隔離されたクライアントやリソースに対し、コンテンツ リソースを提供する (クラウドベースの配布ポイントを使用する)  

-   物理ハードウェアを利用できない事情があるときや、個別のニーズに対応するために論理ハードウェアを導入するとき、インフラストラクチャをスケールアウトする (Microsoft Azure Virtual Machines を使用する)  

クラウド リソースのプロビジョニングは、Configuration Manager を展開する前に必ず実行しなければならないものではありませんが、階層の設計プランの基礎段階でこれらのオプションを理解しておくと役に立つ場合があります。 クラウド リソースを使用することによって、オンプレミスのインフラストラクチャでは解決できないビジネスの課題に対応すると共に、コストを削減し、時間を短縮することができます。  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Configuration Manager で使用できるクラウド ベースのリソース  
 選択肢によって要件は異なりますが、それぞれの要件を詳しく調査し、前提条件や制限、使用に応じて発生する追加コストなどを把握してください。  

-   クラウドベースの配布ポイントの詳細については、「[クラウドベースの配布ポイントのインストール](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)」を参照してください。

-   Windows Azure の詳細については、MSDN ライブラリの [Windows Azure](http://go.microsoft.com/fwlink/p/?LinkId=262965) を参照してください。  

### <a name="microsoft-azure-virtual-machines-for-cloud-based-infrastructure"></a>Microsoft Azure 仮想マシン (クラウドベースのインフラストラクチャ用)  
 Configuration Manager は、物理的な企業ネットワーク内でオンプレミスで実行されるコンピューターと同じように、Azure の仮想マシン内で動作するコンピューターの使用をサポートします。 次のシナリオで Azure Virtual Machines を使うことができます。  

-   **シナリオ 1:** ある仮想マシンで Configuration Manager を実行し、それを使用して、別の仮想マシンにインストールされたクライアントを管理することができます。  

-   **シナリオ 2:** 仮想マシンで Configuration Manager を実行し、それを使用して Azure で実行されていないクライアントを管理することができます。  

-   **シナリオ 3:** 仮想マシンで複数の Configuration Manager サイト システムの役割を実行しながら、(通信のための適切なネットワーク接続がある) 物理的な企業ネットワークで他の役割を実行することができます。  

物理的な企業ネットワークに Configuration Manager をインストールするときと同じネットワーク、オペレーティング システム、ハードウェアの要件が、Microsoft Azure での Configuration Manager のインストールにも適用されます。  

Azure の仮想マシンを使用するためには、Azure サブスクリプションが必要です。また、仮想マシンの使用台数や構成、クラウドベースのリソースの使用に応じた料金が発生します。  

加えて、Azure Virtual Machines で実行している Configuration Manager サイトおよびクライアントには、オンプレミス インストールと同じライセンス要件が課されます。  

### <a name="microsoft-azure-services-for-cloud-based-distribution-points"></a>Microsoft Azure サービス (クラウドベースの配布ポイント用)  
 Azure サービスを Configuration Manager 配布ポイントのホストとして使用することができます。これをクラウドベースの配布ポイントと呼びます。  オンプレミスの配布ポイントや、Azure Virtual Machines に展開されている配布ポイントと一緒に、[System Center Configuration Manager でクラウド ベースの配布ポイントを使用](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)できます。  

 これは、サイト システムの役割の展開先の Azure の仮想マシンを使うこととは異なります。 クラウドベースの配布ポイント:  

-   仮想マシン上ではなく Microsoft Azure でサービスとして実行される  

-   クライアントからのコンテンツ要求の増加に対応するように自動的に拡張する  

-   インターネットとイントラネット上のクライアントをサポートする  

Azure を使って配布ポイントをホストするためには、Azure サブスクリプションが必要です。また、サービスとのやり取りで転送されるデータの量に応じた料金が発生します。  

### <a name="microsoft-intune-for-mobile-device-management"></a>Microsoft Intune (モバイル デバイス管理用)  
 Microsoft Intune サブスクリプションを Configuration Manager に統合することによって、Intune サービスを使用したデバイスの管理が可能になります。 この統合は:  

-   ハイブリッド構成と呼ばれます。また、Configuration Manager (または、見方によっては Intune) を拡張してさまざまなデバイスに対応することができます。  

-   Microsoft Intune コネクタ サイト システムの役割が必要です。  

-   別途 Intune サブスクリプションと、Intune を使って管理するデバイス分のライセンスが必要です。  

Intune は Microsoft Azure を使用しますが、個別に Azure を構成する必要はなく、また Intune サブスクリプションの料金以外で別途コストが発生することもありません。  

### <a name="additional-configuration-manager-capabilities"></a>その他の Configuration Manager の機能  
 Configuration Manager の一部の機能は、次のようなクラウドベースのサービスに接続することができます。  

-   Windows Server Update Services (WSUS)  

-   Configuration Manager の更新プログラムをダウンロードする Configuration Manager サービスのクラウド  

これらの追加機能については、Azure サブスクリプションは不要です。クラウドに特定の接続や証明書、サービスを構成する必要もありません。 これらは Configuration Manager によって自動的に管理されます。  必要なのは、対象となるサイト システムとデバイスからインターネット ベースの URL にアクセスできることを確認するだけです。  

##  <a name="a-namebkmkcloudseca-security-for-cloud-based-services"></a><a name="BKMK_CloudSec"></a> クラウドベースのサービスのセキュリティ  
 Configuration Manager は証明書を使用して、Microsoft Azure 内のコンテンツのプロビジョニングとアクセスを行い、使用するサービスを管理します。 Configuration Manager は Azure に保存されるデータを暗号化しますが、Azure が提供する機能以外のセキュリティ機能やデータ制御機能を提供しません。  

 詳細については、クラウドベースのリソースの各種シナリオを参照してください。 Microsoft Azure のセキュリティについては、次のトピックも参考になります。  

-   [Microsoft Azure: Microsoft Azure におけるセキュリティ アカウントの管理を理解する](http://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Windows Azure のセキュリティの概要](http://go.microsoft.com/fwlink/p/?LinkId=262970)  

-   [クラウド移行をセキュリティの問題で中断しない](http://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [Azure におけるデータのセキュリティ、パート 1/2](http://go.microsoft.com/fwlink/p/?LinkId=262974)  



<!--HONumber=Dec16_HO3-->


