---
title: サポートされるサイト システム サーバー
titleSuffix: Configuration Manager
description: System Center Configuration Manager サイトまたはサイト システムの役割をホストできる Windows バージョンについて説明します。
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: aa933186e95f084bd4e3e518e167a1cd301a4484
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2018
ms.locfileid: "34474294"
---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>System Center Configuration Manager サイト システム サーバーのサポートされるオペレーティング システム

*適用対象: System Center Configuration Manager (Current Branch)*


この記事では、Configuration Manager サイトまたはサイト システムの役割をホストできる Windows バージョンについて説明します。


この記事の情報は、次の記事の情報とともに使用します。
-   [Configuration Manager の推奨ハードウェア](../../../core/plan-design/configs/recommended-hardware.md)
-   [Configuration Manager のサイトとサイト システムの前提条件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Configuration Manager のサイズとスケール番号](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-standard-and-datacenter"></a>Windows Server 2016: Standard、Datacenter
KB3186654 からの修正プログラムのロールアップで、次の役割に対してこの OS がサポートされています。

**サイト サーバー:**  

-   中央管理サイト  

-   プライマリ サイト  

-   セカンダリ サイト  

**サイト システム サーバー:**  

-   アプリケーション カタログ Web サービス ポイント  

-   アプリケーション カタログ Web サイト ポイント  

-   資産インテリジェンス同期ポイント  

-   証明書登録ポイント  

-   配布ポイント  

     配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

-   Endpoint Protection ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

-   フォールバック ステータス ポイント  

-   管理ポイント

-   レポート サービス ポイント  

-   [サービス接続ポイント]  

-   サイト データベース サーバー  

     サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート技術情報の「 [You may encounter problems when installing SQL Server on a domain controller (ドメイン コントローラーに SQL Server をインストールすると問題が発生する)](https://go.microsoft.com/fwlink/p/?LinkId=264856) 」を参照してください。 さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  

-   SMS_Provider  

-   ソフトウェアの更新ポイント  

-   状態移行ポイント



## <a name="windows-storage-server-2016"></a>Windows Storage Server 2016

**サイト システム サーバー:**  

-   配布ポイント  



## <a name="windows-server-2012-r2-x64-standard-and-datacenter"></a>Windows Server 2012 R2 (x64): Standard、Datacenter  
**サイト サーバー:**  

-   中央管理サイト  

-   プライマリ サイト  

-   セカンダリ サイト  

**サイト システム サーバー:**  

-   アプリケーション カタログ Web サービス ポイント  

-   アプリケーション カタログ Web サイト ポイント  

-   資産インテリジェンス同期ポイント  

-   証明書登録ポイント  

-   配布ポイント  

     配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

-   Endpoint Protection ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

-   フォールバック ステータス ポイント  

-   管理ポイント

-   レポート サービス ポイント  

-   [サービス接続ポイント]  

-   サイト データベース サーバー  

     サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート技術情報の「 [You may encounter problems when installing SQL Server on a domain controller (ドメイン コントローラーに SQL Server をインストールすると問題が発生する)](https://go.microsoft.com/fwlink/p/?LinkId=264856) 」を参照してください。 さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  

-   SMS_Provider  

-   ソフトウェアの更新ポイント  

-   状態移行ポイント  

## <a name="windows-server-2012-x64-standard-and-datacenter"></a>Windows Server 2012 (x64): Standard、Datacenter  
**サイト サーバー:**  

-   中央管理サイト  

-   プライマリ サイト  

-   セカンダリ サイト  

**サイト システム サーバー:**  

-   アプリケーション カタログ Web サービス ポイント  

-   アプリケーション カタログ Web サイト ポイント  

-   資産インテリジェンス同期ポイント  

-   証明書登録ポイント  

-   配布ポイント  

     配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

-   Endpoint Protection ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

-   フォールバック ステータス ポイント  

-   管理ポイント

-   レポート サービス ポイント  

-   [サービス接続ポイント]  

-   サイト データベース サーバー  

     サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート技術情報の「 [You may encounter problems when installing SQL Server on a domain controller (ドメイン コントローラーに SQL Server をインストールすると問題が発生する)](https://go.microsoft.com/fwlink/p/?LinkId=264856) 」を参照してください。 さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  

-   SMS_Provider  

-   ソフトウェアの更新ポイント  

-   状態移行ポイント  



## <a name="windows-server-2008-r2-with-sp1-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 R2 SP1 (x64): Standard、Enterprise、Datacenter  
 [マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)で詳述するように、Windows Server 2008 R2 が延長サポートになり、メインストリーム サポートが終了しました。 Configuration Manager を使用したサイト システム サーバーとしてのこれらのオペレーティング システムの将来のサポートについては、「[非推奨のサーバー オペレーティング システム](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems)」を参照してください。  

 この OS は、サイト サーバーやほとんどのサイト システムの役割に対してサポートされていません。 プル配布ポイント、PXE およびマルチキャストを含む配布ポイントのサイト システムの役割に対しては引き続きサポートされます。

**サイト システム サーバー:**  
-   配布ポイント  

    -   この OS の配布ポイントでは、マルチキャストをサポートしません。  

    -   この OS の配布ポイントは、PXE に対してサポートされています。

    -   配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  



## <a name="windows-server-2008-with-sp2-x86-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 SP2 (x86, x64): Standard、Enterprise、Datacenter  
 [マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)で詳述するように、Windows Server 2008 が延長サポートになり、メインストリーム サポートが終了しました。 Configuration Manager を使用したサイト システム サーバーとしてのこれらのオペレーティング システムの将来のサポートについては、「[非推奨のサーバー オペレーティング システム](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems)」を参照してください。  

この OS は、サイト サーバーとして、または配布ポイントとプル配布ポイントを除くサイト システムの役割としてはサポートされていません。 このサポートの廃止が発表されるまで、またはこの OS の拡張サポート期間が終了するまでは、この OS を配布ポイントとして使用し続けることができます。 詳細については、「[Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095)」 (Windows Server 2008 で System Center Configuration Manager CB および LTSB のインストールに失敗する) を参照してください。

**サイト システム サーバー:**  
-   配布ポイント  

    -   この OS の配布ポイントでは、マルチキャストをサポートしません。  

    -   この OS の配布ポイントは、PXE ではサポートされますが、EFI モードでのクライアント コンピューターのネットワーク ブートはサポートしません。 クライアント コンピューターのレガシ モードでの BIOS ブートまたは EFI ブートはサポートされます。  

    -   配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  



## <a name="windows-10-x86-x64-pro-and-enterprise"></a>Windows 10 (x86, x64): Pro、Enterprise  
**サイト システム サーバー:**  

-   配布ポイント  

    -   この OS の配布ポイントは、PXE に対してサポートされていません。 

    -   この OS の配布ポイントでは、マルチキャストをサポートしません。  

    -   配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  



## <a name="windows-81-x86-x64-professional-and-enterprise"></a>Windows 8.1 (x86、x64): Professional、Enterprise  
**サイト システム サーバー:**  

-   配布ポイント  

    -   この OS の配布ポイントは、PXE に対してサポートされていません。  

    -   この OS の配布ポイントでは、マルチキャストをサポートしません。  

    -   配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  



## <a name="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate"></a>Windows 7 SP1 (x86、x64): Professional、Enterprise、Ultimate  
**サイト システム サーバー:**  

-   配布ポイント  

    -   この OS の配布ポイントは、PXE に対してサポートされていません。  

    -   この OS の配布ポイントでは、マルチキャストをサポートしません。  

    -   配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

## <a name="the-server-core-installation-of-windows-server-version-1803"></a>Windows Server バージョン 1803 の Server Core インストール
<!--503702--> Configuration Manager 1802 以降では、[Windows Server バージョン 1803](https://docs.microsoft.com/windows-server/get-started/get-started-with-1803) が、次の制限付きの配布ポイントとしての使用でサポートされます。  
  -   64 ビット バージョンのみがサポートされています。
  -   この OS の配布ポイントでは、PXE またはマルチキャストをサポートしません。  

## <a name="the-server-core-installation-of-windows-server-version-1709"></a>Windows Server バージョン 1709 の Server Core インストール
Configuration Manager 1710 以降では、[Windows Server バージョン 1709](https://docs.microsoft.com/windows-server/get-started/get-started-with-1709) が、次の制限付きの配布ポイントとしての使用でサポートされます。  
  -   64 ビット バージョンのみがサポートされています。
  -   この OS の配布ポイントでは、PXE またはマルチキャストをサポートしません。  

## <a name="the-server-core-installation-of-windows-server-2016"></a>Windows Server 2016 の Server Core インストール
KB3186654 からの修正プログラムのロールアップを適用すると、この OS が次の制限付きの配布ポイントとしてサポートされます。  
  -   64 ビット バージョンのみがサポートされています。
  -   この OS の配布ポイントでは、PXE またはマルチキャストをサポートしません。  



## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>Windows Server 2012 R2 の Server Core のインストール  
 Windows Server 2012 R2 の Server Core インストールが、次の制限付きの配布ポイントとしての使用でサポートされます。  

-   64 ビット バージョンのみがサポートされています。

-   この OS の配布ポイントでは、PXE またはマルチキャストをサポートしません。  



## <a name="the-server-core-installation-of-windows-server-2012"></a>Windows Server 2012 の Server Core のインストール  
 Windows Server 2012 の Server Core インストールが、次の制限付きの配布ポイントとしての使用でサポートされます。  

-   64 ビット バージョンのみがサポートされています。  

-   この OS の配布ポイントでは、PXE またはマルチキャストをサポートしません。
