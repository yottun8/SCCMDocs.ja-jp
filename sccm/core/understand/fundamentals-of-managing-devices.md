---
title: "デバイスの管理の基礎 | Microsoft ドキュメント"
description: "System Center Configuration Manager を使用してデバイスを管理する方法について説明します。"
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: 6
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 17b36eae97272c408fce20e1f88812dafc984773
ms.openlocfilehash: b907975db5b5ffa6fefef58902319b987e57dca6


---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>System Center Configuration Manager を使用したデバイス管理の基礎

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager は、大きく分けて 2 つのカテゴリのデバイスを管理できます。

**クライアント**は、Configuration Manager クライアント ソフトウェアがインストールされているデバイス (ワークステーション、ノート PC、サーバー、モバイル デバイスなど) です。 ハードウェア インベントリなどの一部の管理関数では、このクライアント ソフトウェアが必要です。  

**管理対象デバイス**は、*クライアント*を含めることができますが、通常は Configuration Manager クライアント ソフトウェアをインストールしないモバイル デバイスであり、Microsoft Intune または Configuration Manager の組み込み型オンプレミス モバイル デバイス管理を使用して管理するモバイル デバイスを意味します。

デバイスをグループ化および識別する場合は、クライアントの種類だけでなくユーザーも使用できます。

## <a name="managing-devices-with-the-configuration-manager-client"></a>Configuration Manager クライアントを使用したデバイスの管理

Configuration Manager クライアント ソフトウェアを使用してデバイスを管理するには、ネットワーク上のデバイスを探索して、そのデバイスにクライアント ソフトウェアを展開するか、または新しいコンピューターにクライアント ソフトウェアを手動でインストールしてから、そのコンピューターをネットワークに参加させるときに、サイトにも参加させます。 クライアント ソフトウェアがまだインストールされていないデバイスを探索するには、組み込まれた探索方法のうちの 1 つまたは複数を実行します。 デバイスが探索されたら、いくつかの方法のいずれかで、クライアント ソフトウェアをインストールします。 探索の使用の詳細については、「[System Center Configuration Manager 用の探索の実行](../../core/servers/deploy/configure/run-discovery.md)」をご覧ください。  

 構成マネージャー クライアント ソフトウェアを実行するためにサポートされているデバイスを探索したら、いくつかの方法のうちの 1 つを使用して、ソフトウェアをインストールできます。 ソフトウェアがインストールされて、クライアントがプライマリ サイトに割り当てられたら、デバイスの管理を開始できます。  一般的なインストール方法としては、クライアント プッシュ インストール、ソフトウェア更新プログラムを利用するインストール、グループ ポリシーの使用、コンピューターへの手動インストール、展開するオペレーティング システム イメージの一部としてのクライアントの追加などがあります。  

 クライアントがインストールされたら、コレクションを使用して、デバイス管理タスクを簡略化できます。 コレクションは、デバイスやユーザーをグループとして管理できるように作成されたデバイスまたはユーザーのグループです。 たとえば、Configuration Manager に登録されているすべてのモバイル デバイスに、モバイル デバイス アプリケーションをインストールすることができます。 この場合は、**[すべてのモバイル デバイス]** コレクションを使用することが可能です。  

 詳細については、次のトピックを参照してください。  

-   [System Center Configuration Manager のデバイス管理ソリューションの選択](../../core/plan-design/choose-a-device-management-solution.md)  

-   [System Center Configuration Manager でのクライアントのインストール方法](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [System Center Configuration Manager のコレクションの概要](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>クライアント設定  
 Configuration Manager を最初にインストールすると、階層内のすべてのクライアントは既定のクライアント設定で構成されます (これは変更可能です)。 これらのクライアント設定には、デバイスがサイトと通信する頻度、クライアントがソフトウェア更新プログラムとその他の管理操作の対象であるかどうか、ユーザーがモバイル デバイスを Configuration Manager による管理対象として登録できるかどうかなどの構成オプションが含まれます。  

カスタム クライアント設定を作成し、コレクションに割り当てることができます。  カスタム設定が適用されるようにコレクションのメンバーに構成されます。指定する (番号) 順序で適用されるように複数のカスタム クライアントを作成できます。  競合する設定がある場合は、順序番号が最も小さい設定がその他の設定に優先します。  

次の図は、カスタム クライアント設定を作成および適用する方法の例を示します。  

 ![クライアント設定](media/ClientSettings.gif)  

 クライアント設定の詳細については、  
「                [System Center Configuration Manager でクライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)」および「[System Center Configuration Manager のクライアント設定について](../../core/clients/deploy/about-client-settings.md)」をご覧ください。

## <a name="managing-devices-without-the-configuration-manager-client"></a>Configuration Manager クライアントを使用しないデバイス管理  
 Configuration Manager では、クライアント ソフトウェアがインストールされていないデバイスの管理 (および Microsoft Intune によって管理されないデバイスの管理) をサポートします。 詳細については、「[System Center Configuration Manager でのオンプレミス インフラストラクチャによるモバイル デバイスの管理](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」および「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」をご覧ください。  

## <a name="user-based-management"></a>ユーザー ベースの管理  
 Active Directory Domain Services ユーザーの Configuration Manager コレクション。 ユーザー コレクションを使用するときには、展開するソフトウェアがユーザーのプライマリ デバイスとして指定されているデバイスのみにインストールされるように、コレクションのメンバーがログインするすべてのコンピューターにソフトウェアをインストールして、 **ユーザーとデバイスのアフィニティ** を構成できます。 ユーザーは 1 つまたは複数のプライマリ デバイスを持つことができます。  

 ユーザーがソフトウェア展開の操作を制御できる 1 つの方法は、コンピューター クライアント インターフェイスである **ソフトウェア センター**を使用することです。 ソフトウェア センターは、クライアント コンピューターに自動的にインストールされ、ユーザーの [スタート] メニューからアクセスします。 ユーザーはソフトウェア センターを使用して自分のソフトウェアを管理できるだけでなく、次の機能を実行できます。  

-   ソフトウェアのインストール  

-   勤務時間外にソフトウェアが自動的にインストールされるようにスケジュールする  

-   Configuration Manager がデバイスにソフトウェアをインストールできるタイミングを構成する  

-   Configuration Manager でリモート コントロールが有効な場合に、リモート コントロールのアクセス設定を構成する  

-   電源管理のオプションの構成 (管理ユーザーがこれを有効にしている場合)  

 ソフトウェア センター内のリンクを使用すると、ユーザーは **アプリケーション カタログ**に接続して、ソフトウェアの参照、インストール、および要求を行えます。 さらに、アプリケーション カタログにより、ユーザーは優先設定を構成したり、モバイル デバイスをワイプしたり、(この構成が許可されている場合に) ユーザーとデバイスのアフィニティのプライマリ デバイスを指定したりできます。   

 アプリケーション カタログは、IIS でホストされる Web サイトであるため、ブラウザー、イントラネット、またはインターネットから直接アクセスすることもできます。  



<!--HONumber=Dec16_HO3-->


