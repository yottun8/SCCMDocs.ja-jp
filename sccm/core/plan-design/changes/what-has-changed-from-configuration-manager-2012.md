---
title: "Configuration Manager 2012 からの変更点 | Microsoft Docs "
description: "System Center 2012 Configuration Manager と比較した System Center Configuration Manger の新機能と変更をご確認いただけます。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: 51
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 828e2ac9a3f9bcea1571d24145a1021fdf1091f3
ms.openlocfilehash: 3ede76bd60372dcef2b1b3230577ee3c3f1e2dcd


---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>System Center 2012 Configuration Manager からの System Center Configuration Manager の変更点

*適用対象: System Center Configuration Manager (Current Branch)*


 System Center Configuration Manager Current Branch には、System Center 2012 Configuration Manager からの重要な変更点があります。 このトピックでは、System Center Configuration Manager の基準バージョン 1511 における重要な変更点と新機能について紹介します。 System Center Configuration Manager の後続の更新で導入された追加の変更点については、「[System Center Configuration Manager 増分バージョンの新機能](/sccm/core/plan-design/changes/whats-new-incremental-versions)」を参照してください。



 2015 年 12 月リリースの System Center Configuration Manager (バージョン 1511) が、Microsoft から提供される Configuration Manager の最新の製品リリースです。   これは一般に System Center Configuration Manager の Current Branch と呼ばれます。 *Current Branch* は、製品に対する増分更新をサポートするバージョンであることを示しており、Configuration Manager の今回のリリースと過去のリリースとの間の重要な境界となります。  

 System Center Configuration Manager の今回のリリースの特徴:  

-   Configuration Manager 2007 や System Center 2012 Configuration Manager などの過去のバージョンとは異なり、製品名に年や製品識別子を使用していません。

-   製品組み込みの増分更新をサポートしているため、更新プログラム バージョンとも呼ばれます。 初回リリースはバージョン 1511 です。 後続のバージョンは、バージョン 1602 や 1606 のように、コンソール内の更新プログラムとして年に数回リリースされます。




##  <a name="a-namebkmkupdatesa-in-console-updates-for-configuration-manager"></a><a name="bkmk_updates"></a> Configuration Manager のコンソール内更新  
 System Center Configuration Manager では、**更新とサービス**と呼ばれるコンソール内でのサービス提供方式が採られています。この方式により、Configuration Manager 向けの推奨される更新プログラムを簡単に特定し、インストールすることができます。  

 バージョンによっては、(Configuration Manager コンソール内から) 既存のサイトに対する更新プログラムとしてのみ使用できて、新規 Configuration Manager サイトのインストールに使用できないものがあります。   
たとえば、1602 更新プログラムは Configuration Manager コンソール内からのみ使用可能で、基準バージョンの 1511 を実行しているサイトをバージョン 1602 に更新するために使用されます。  

更新プログラム バージョンは、新しい基準バージョン (更新プログラム 1606 など) としても定期的にリリースされます。新しい基準バージョンを使用すれば、古い基準バージョン (1511 など) から開始して最新バージョンまでアップグレードしなくても、新しい階層をインストールできます。


 更新プログラムの使用の詳細については、「[System Center Configuration Manager の更新プログラム](../../../core/servers/manage/updates.md)」を参照してください。  

##  <a name="a-namebkmkservicepointa-service-connection-point-replaces-microsoft-intune-connector"></a><a name="bkmk_servicepoint"></a> サービス接続ポイントは、Microsoft Intune コネクタに置き換わるものです。  
 **Microsoft Intune コネクタ**は新しいサイト システムの役割に置き換えられ、新たに追加された**サービス接続ポイント**機能が有効になります。 サービス接続ポイント:  

-   Intune を System Center Configuration Manager オンプレミス モバイル デバイス管理と統合するときに、Microsoft Intune コネクタに置き換わります  

-   管理するデバイスのコンタクト ポイントとして使用します  

-   展開に関する使用状況データを、Microsoft クラウド サービスにアップロードします  

-   対象の展開に適用する更新プログラムを Configuration Manager 内から利用できるようにします  

このサイト システムの役割は、オンライン モードとオフライン モードの両方の操作をサポートしており、これらは付加的な用途に影響を及ぼします。 詳細については、「[System Center Configuration Manager のサービス接続ポイントについて](../../../core/servers/deploy/configure/about-the-service-connection-point.md)」を参照してください。  

##  <a name="a-namebkmkusagea-usage-data-collection"></a><a name="bkmk_usage"></a> 使用状況データの収集  
 System Center Configuration Manager は、サイトとインフラストラクチャに関する使用状況データを収集します。 この情報は、サービス接続ポイント (新しいサイト システムの役割) によってコンパイルされ、Microsoft クラウド サービスに送信されます。また、使用している Configuration Manager のバージョンに適用する展開の更新プログラムを Configuration Manager がダウンロードできるようにするには、この情報が必要になります。 サービス接続ポイントを構成するときには、収集するデータのレベルと、そのデータを自動的に送信するか (オンライン モード)、手動で送信するか (オフライン モード) の両方を構成できます。  

 詳細については、「 [Usage data levels and settings](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage)」をご覧ください。  

##  <a name="a-namebkmkamta-support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Intel Active Management Technology (AMT) のサポート  
 System Center Configuration Manager では、Configuration Manager コンソール内からの AMT ベースのコンピューターに対するネイティブ サポートは削除されました。  

-   [Microsoft System Center Configuration Manager 用 Intel SCS アドオン](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)を使用すれば、AMT ベースのコンピューターは引き続き完全に管理されます。  

-   アドオンを使用することで、最新の機能にアクセスして AMT を管理できます。Configuration Manager にこれらの変更が組み込まれるまでに適用されていた制限は解除されます。  

-   System Center 2012 Configuration Manager での帯域外管理は、この変更の影響を受けません。  

System Center Configuration Manager での統合 AMT の削除には、次の内容が含まれています。  

-   帯域外管理ポイント サイト システムの役割は、もう使用されず、使用できなくなります。  

##  <a name="a-namebkmkouta-deprecated-functionality"></a><a name="bkmk_out"></a> 非推奨機能  
 System Center Configuration Manager では、[Intel Active Management Technology (AMT)](#bkmk_AMT) ベースのコンピューターのネイティブ サポートなど、Configuration Manager コンソールから除外された機能や、ネットワーク アクセス保護のように完全に削除された機能があります。 さらに、Windows Vista、Windows Server 2008、SQL Server 2008 などの古い Microsoft 製品の一部はサポートされていません。  

 非推奨機能の一覧については、「[System Center Configuration Manager から削除された機能と非推奨の機能](../../../core/plan-design/changes/removed-and-deprecated-features.md)」を参照してください。  

 サポートされる製品、オペレーティング システム、および構成の詳細については、「[System Center Configuration Manager のサポートされている構成](../../../core/plan-design/configs/supported-configurations.md)」を参照してください。  

## <a name="client-deployment"></a>クライアント展開  
 System Center Configuration Manager では、Configuration Manager クライアントの新しいバージョンをテストしてから、この新しいソフトウェアでサイトの他の部分をアップグレードするようにするための新機能を導入しています。  この新しい機能により、新しいクライアントをパイロット運用するための実稼働前コレクションを設定できるようになります。 実稼働前環境で新しいクライアント ソフトウェアが正常に動作することを確認した後、その新しいバージョンでサイトの残りの部分を自動的にアップグレードするようにクライアントを昇格できます。  

 クライアントをテストする方法の詳細については、「[System Center Configuration Manager で実稼働前コレクションのクライアント アップグレードをテストする方法](../../../core/clients/manage/upgrade/test-client-upgrades.md)」を参照してください。  

## <a name="operating-system-deployment"></a>オペレーティング システムの展開  

-   タスク シーケンスの作成ウィザードで新しいタスク シーケンスの種類 (  **アップグレード パッケージからのオペレーティング システムのアップグレード**) を利用できるようになりました。これにより、コンピューターを Windows 7、Windows 8、または Windows 8.1 から Windows 10 にアップグレードするステップが作成されます。  詳細については、「 [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)」をご覧ください。  

-   オペレーティング システムを展開するときに、Windows PE ピア キャッシュを利用できるようになりました。 オペレーティング システムを展開するタスク シーケンスを実行しているコンピューターでは、配布ポイントからコンテンツをダウンロードするのではなく、Windows PE ピア キャッシュを使用してローカル ピア (ピア キャッシュ ソース) からコンテンツを取得できます。 これにより、ローカル配布ポイントが存在しないブランチ オフィス シナリオでワイド エリア ネットワーク (WAN) トラフィックが最小限に抑えられます。 詳細については、「 [Prepare Windows PE peer cache to reduce WAN traffic in System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic)」をご覧ください。  

-   環境内のサービスとして Windows の状態を確認したり、展開リングを形成するサービス プランを作成して、新しいビルドがリリースされたときに、Windows 10 の Current Branch コンピューターが最新の状態であることを確認したりできるようになりました。また、Windows 10 クライアントの Current Branch (CB) または Current Branch for Business (CBB) について、サポートの終了が近付いた場合にアラートを表示することもできます。 詳細については、「 [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md)」を参照してください。  

## <a name="application-management"></a>アプリケーション管理  

-   System Center Configuration Manager では、Windows 10 以降を実行しているデバイス用のユニバーサル Windows プラットフォーム (UWP) アプリを展開できます。 「[System Center Configuration Manager での Windows アプリケーションの作成](../../../apps/get-started/creating-windows-applications.md)」を参照してください。  

-   ソフトウェア センターは現代的な新しい外観へと一新され、これまではアプリケーション カタログにしか表示されなかったアプリ (ユーザーが利用できるアプリ) がソフトウェア センターの [アプリケーション] タブに表示されるようになりました。 これにより、ユーザーがこれらの展開を見つけやすくなり、アプリケーション カタログを使う必要がなくなります。 さらに、Silverlight 対応のブラウザーが必要なくなります。 「[System Center Configuration Manager のアプリケーション管理の計画と構成](../../../apps/plan-design/plan-for-and-configure-application-management.md)」を参照してください。  

-   MDM アプリケーションを介した新しい Windows インストーラーの種類では、Windows インストーラー ベースのアプリを作成して、Windows 10 を実行する登録済み PC に展開できます。 「[System Center Configuration Manager での Windows アプリケーションの作成](../../../apps/get-started/creating-windows-applications.md)」を参照してください。  

-   社内 iOS アプリとしてアプリケーションを作成するときは、アプリのインストーラー (.ipa) ファイルを指定することのみが必要になります。 対応するプロパティ リスト (.plist) ファイルを指定する必要はなくなりました。 「[System Center Configuration Manager での iOS アプリケーションの作成](../../../apps/get-started/creating-ios-applications.md)」を参照してください。  

-   Configuration Manager 2012 では、Windows ストアのアプリへのリンクを指定する場合、リンクを直接指定するか、またはアプリがインストールされているリモート コンピューターを参照します。 System Center Configuration Manager でも、引き続きリンクを直接入力できますが、参照コンピューターを参照するのではなく、Configuration Manager コンソールから直接アプリのストアを参照できるようになりました。  

## <a name="software-updates"></a>ソフトウェア更新プログラム  

-   System Center Configuration Manager で、ソフトウェアの更新管理のために Windows Update for Business (WUfB) に接続する Windows 10 コンピューターと、ソフトウェア更新管理のために WSUS に接続するコンピューターとを区別できるようになりました。 **UseWUServer** は新たに導入された属性で、WUfB でコンピューターを管理するかどうかを指定します。 コレクションでこの設定を使用すると、ソフトウェアの更新管理からこれらのコンピューターを除外できます。 詳細については、「 [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)」をご覧ください。  

-   Configuration Manager コンソールから WSUS クリーンアップ タスクをスケジュールし、実行できるようになりました。  
    ソフトウェアの更新ポイント コンポーネントのプロパティから、WSUS クリーンアップ タスクを手動で実行できるようになりました。 WSUS クリーンアップ タスクを実行することを選ぶと、次回、ソフトウェア更新プログラムを最新に保つときにこのタスクが実行されます。 期限切れのソフトウェアの更新プログラムは WSUS サーバー上で拒否状態に設定され、コンピューター上の Windows Update エージェントでこれらのソフトウェア更新プログラムをスキャンできなくなります。 詳細については、「 [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md)」をご覧ください。  

## <a name="compliance-settings"></a>コンプライアンス設定  

-   System Center Configuration Manager では、構成項目を作成するためのワークフローが改良されています。 これで、構成項目を作成し、サポートされているプラットフォームを選択するときに、そのプラットフォームに関連する設定のみが使用できるようになります。 「[System Center Configuration Manager のコンプライアンス設定を使ってみる](../../../compliance/get-started/get-started-with-compliance-settings.md)」を参照してください。  

-   構成項目の作成ウィザードでは、作成する構成項目の種類が選択しやすくなりました。 さらに、次のものに対して使用できる構成項目が追加および更新されています。  

    -   Configuration Manager クライアントを使用して管理されている Windows 10 デバイス  

    -   Configuration Manager クライアントを使用して管理されている Mac OS X デバイス  

    -   Configuration Manager クライアントを使用して管理されている Windows デスクトップおよびサーバー コンピューター  

    -   Configuration Manager クライアントを使用せずに管理されている Windows 8.1 および Windows 10 デバイス  

    -   Configuration Manager クライアントを使用せずに管理されている Windows Phone デバイス  

    -   Configuration Manager クライアントを使用せずに管理されている iOS および Mac OS X デバイス  

    -   Configuration Manager クライアントを使用せずに管理されている Android および Samsung KNOX Standard デバイス  

     「[System Center Configuration Manager で構成項目を作成する方法](../../../compliance/deploy-use/create-configuration-items.md)」を参照してください。  

-   Microsoft Intune に登録されているか、Configuration Manager クライアントを使用して管理されている、Mac OS X コンピューター上の設定を管理するためのサポート。 「[System Center Configuration Manager クライアントを使用せずに管理されている iOS デバイスと Mac OS X デバイスの構成項目を作成する方法](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)」を参照してください。  

## <a name="protect-data-and-site-infrastructure"></a>データとサイト インフラストラクチャの保護  
-   System Center Configuration Manager では、Windows Hello for Business (旧称 Microsoft Passport for Work) を統合できます。これは Active Directory や Azure Active Directory アカウントを使った代替サインイン方法であり、Windows 10 を実行しているデバイス上のパスワード、スマート カード、または仮想スマート カードに取って代わります。 「[System Center Configuration Manager における Windows Hello for Business 設定について](../../../protect/deploy-use/windows-hello-for-business-settings.md)」を参照してください。

## <a name="mobile-device-management-with-microsoft-intune"></a>Microsoft Intune を使用したモバイル デバイスの管理  
 System Center Configuration Manager では、次に挙げるように、モバイル デバイス管理エクスペリエンスが改良されています。  

-   ユーザーが登録できるデバイスの数を制限します。  

-   会社のポータルのユーザーがアプリを登録または使用するために事前に同意する必要がある使用条件を指定します。  

-   大量のデバイスを管理できるようにデバイス登録マネージャーの役割が追加されました。  

Configuration Manager および Intune によるモバイル デバイス管理機能の詳細については、「[System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM)](../../../mdm/understand/hybrid-mobile-device-management.md)」を参照してください。  

## <a name="on-premises-mobile-device-management"></a>オンプレミス モバイル デバイス管理  
 System Center Configuration Manager では、オンプレミスの Configuration Manager インフラストラクチャを使用してモバイル デバイスを管理できるようになりました。 すべてのデバイス管理と管理データはオンプレミスで処理され、Microsoft Intune またはその他のクラウド サービスの一部ではなくなります。 この種類のデバイス管理では、Configuration Manager がデバイスを管理するために使用する機能がデバイスのオペレーティング システムに組み込まれているため、クライアント ソフトウェアが必要ありません。  

 詳細については、「[System Center Configuration Manager でオンプレミス インフラストラクチャを使用したモバイル デバイスの管理](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」を参照してください。



<!--HONumber=Dec16_HO3-->


