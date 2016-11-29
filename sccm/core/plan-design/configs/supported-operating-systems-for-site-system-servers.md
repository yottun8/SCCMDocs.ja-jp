---
title: "サポートされているサイト システム サーバー | System Center Configuration Manager"
description: "System Center Configuration Manager サイトまたはサイト システムの役割をホストできる Windows バージョンについて説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 00d5d8d9ce90b2da79485250d25f943ca1c4547b


---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>System Center Configuration Manager サイト システム サーバーのサポートされるオペレーティング システム

*適用対象: System Center Configuration Manager (Current Branch)*


この記事では、System Center Configuration Manager サイトまたはサイト システムの役割をホストできる Windows バージョンについて説明します。


このトピックの情報は、次の記事の情報とともに使用します。
-   [Configuration Manager の推奨ハードウェア](../../../core/plan-design/configs/recommended-hardware.md)
-   [Configuration Manager のサイトとサイト システムの前提条件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Configuration Manager のサイズとスケール番号](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016---standard-datacenter"></a>Windows Server 2016   - Standard、Datacenter
Windows Server 2016 は、Configuration Manager バージョン 1606 以降および KB3186654 以降の修正プログラム ロールアップ (2016 年 10 月にリリースされた 1606 のベースライン バージョン) でサポートされています。

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

     配布ポイントは、それぞれに要件の異なる、数種類の構成をサポートします。また、サーバーへのインストールだけでなく、クライアント オペレーティング システムへのインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

-   Endpoint Protection ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

-   フォールバック ステータス ポイント  

-   レポート サービス ポイント  

-   サービス接続ポイント  

-   サイト データベース サーバー  

     サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート技術情報の「 [You may encounter problems when installing SQL Server on a domain controller (ドメイン コントローラーに SQL Server をインストールすると問題が発生する)](http://go.microsoft.com/fwlink/p/?LinkId=264856) 」を参照してください。 さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  

-   SMS_Provider  

-   ソフトウェアの更新ポイント  

-   状態移行ポイント

## <a name="windows-server-2012-r2-x64---standard-datacenter"></a>Windows Server 2012 R2 (x64) - Standard、Datacenter  
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

     配布ポイントは、それぞれに要件の異なる、数種類の構成をサポートします。また、サーバーへのインストールだけでなく、クライアント オペレーティング システムへのインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

-   Endpoint Protection ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

-   フォールバック ステータス ポイント  

-   レポート サービス ポイント  

-   サービス接続ポイント  

-   サイト データベース サーバー  

     サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート技術情報の「 [You may encounter problems when installing SQL Server on a domain controller (ドメイン コントローラーに SQL Server をインストールすると問題が発生する)](http://go.microsoft.com/fwlink/p/?LinkId=264856) 」を参照してください。 さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  

-   SMS_Provider  

-   ソフトウェアの更新ポイント  

-   状態移行ポイント  

## <a name="windows-server-2012-x64---standard-datacenter"></a>Windows Server 2012 (x64) - Standard、Datacenter  
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

     配布ポイントは、それぞれに要件の異なる、数種類の構成をサポートします。また、サーバーへのインストールだけでなく、クライアント オペレーティング システムへのインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

-   Endpoint Protection ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

-   フォールバック ステータス ポイント  

-   レポート サービス ポイント  

-   サービス接続ポイント  

-   サイト データベース サーバー  

     サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート技術情報の「 [You may encounter problems when installing SQL Server on a domain controller (ドメイン コントローラーに SQL Server をインストールすると問題が発生する)](http://go.microsoft.com/fwlink/p/?LinkId=264856) 」を参照してください。 さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  

-   SMS_Provider  

-   ソフトウェアの更新ポイント  

-   状態移行ポイント  

## <a name="windows-server-2008-r2-with-sp1-x64---standard-enterprise-datacenter"></a>Windows Server 2008 R2 SP1 (x64)   - Standard、Enterprise、Datacenter  
 [マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)で詳述するように、Windows Server 2008 R2 が延長サポートになり、メインストリーム サポートが終了しました。 Configuration Manager を使用したサイト システム サーバーとしてのこれらのオペレーティング システムの将来のサポートの詳細については、「[System Center Configuration Manager から削除された機能と非推奨の機能](../../../core/plan-design/changes/removed-and-deprecated-features.md)」を参照してください。  

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

     配布ポイントは、それぞれに要件の異なる、数種類の構成をサポートします。また、サーバーへのインストールだけでなく、クライアント オペレーティング システムへのインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

-   Endpoint Protection ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

-   フォールバック ステータス ポイント  

-   レポート サービス ポイント  

-   サービス接続ポイント  

-   サイト データベース サーバー  

     サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート技術情報の「 [You may encounter problems when installing SQL Server on a domain controller (ドメイン コントローラーに SQL Server をインストールすると問題が発生する)](http://go.microsoft.com/fwlink/p/?LinkId=264856) 」を参照してください。 さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  

-   SMS_Provider  

-   ソフトウェアの更新ポイント  

-   状態移行ポイント  

## <a name="windows-server-2008-with-sp2-x86-x64---standard-enterprise-datacenter"></a>Windows Server 2008 SP2 (x86、x64) - Standard、Enterprise、Datacenter  
 [マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)で詳述するように、Windows Server 2008 が延長サポートになり、メインストリーム サポートが終了しました。 Configuration Manager を使用したサイト システム サーバーとしてのこれらのオペレーティング システムの将来のサポートの詳細については、「[System Center Configuration Manager から削除された機能と非推奨の機能](../../../core/plan-design/changes/removed-and-deprecated-features.md)」を参照してください。  

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

    -   このオペレーティング システムの配布ポイントでは、マルチキャストをサポートしません。  

    -   このオペレーティング システムの配布ポイントは、PXE ではサポートされますが、EFI モードでのクライアント コンピューターのネットワーク ブートはサポートしません。 クライアント コンピューターのレガシ モードでの BIOS ブートまたは EFI ブートはサポートされます。  

    -   配布ポイントは、それぞれに要件の異なる、数種類の構成をサポートします。また、サーバーへのインストールだけでなく、クライアント オペレーティング システムへのインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

-   Endpoint Protection ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

-   フォールバック ステータス ポイント  

-   レポート サービス ポイント  

-   サービス接続ポイント  

-   サイト データベース サーバー  

     サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート技術情報の「 [You may encounter problems when installing SQL Server on a domain controller (ドメイン コントローラーに SQL Server をインストールすると問題が発生する)](http://go.microsoft.com/fwlink/p/?LinkId=264856) 」を参照してください。 さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  

-   SMS_Provider  

-   ソフトウェアの更新ポイント  

-   状態移行ポイント  

## <a name="windows-10-x86-x64---pro-enterprise"></a>Windows 10 (x86、x64) - Pro、Enterprise  
**サイト システム サーバー:**  

-   配布ポイント  

    -   このオペレーティング システムの配布ポイントは、PXE ではサポートされません。  

    -   このオペレーティング システムのバージョンの配布ポイントでは、マルチキャストをサポートしません。  

    -   配布ポイントは、それぞれに要件の異なる、数種類の構成をサポートします。また、サーバーへのインストールだけでなく、クライアント オペレーティング システムへのインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

## <a name="windows-81-x86-x64---professional-enterprise"></a>Windows 8.1 (x86、x64) - Professional、Enterprise  
**サイト システム サーバー:**  

-   配布ポイント  

    -   このオペレーティング システムの配布ポイントは、PXE ではサポートされません。  

    -   このオペレーティング システムのバージョンの配布ポイントでは、マルチキャストをサポートしません。  

    -   配布ポイントは、それぞれに要件の異なる、数種類の構成をサポートします。また、サーバーへのインストールだけでなく、クライアント オペレーティング システムへのインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

## <a name="windows-8-x86-x64---professional-enterprise-distribution-point"></a>Windows 8 (x86、x64) - Professional、Enterprise の配布ポイント  
**サイト システム サーバー:**  

-   配布ポイント  

    -   このオペレーティング システムの配布ポイントは、PXE ではサポートされません。  

    -   このオペレーティング システムのバージョンの配布ポイントでは、マルチキャストをサポートしません。  

    -   配布ポイントは、それぞれに要件の異なる、数種類の構成をサポートします。また、サーバーへのインストールだけでなく、クライアント オペレーティング システムへのインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

## <a name="windows-7-with-sp1-x86-x64---professional-enterprise-ultimate"></a>Windows 7 SP1 (x86、x64) - Professional、Enterprise、Ultimate  
**サイト システム サーバー:**  

-   配布ポイント  

    -   このオペレーティング システムの配布ポイントは、PXE ではサポートされません。  

    -   このオペレーティング システムのバージョンの配布ポイントでは、マルチキャストをサポートしません。  

    -   配布ポイントは、それぞれに要件の異なる、数種類の構成をサポートします。また、サーバーへのインストールだけでなく、クライアント オペレーティング システムへのインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

## <a name="the-server-core-installation-of-windows-server-2012"></a>Windows Server 2012 の Server Core のインストール  
 前のオペレーティング システムだけでなく、Windows Server 2012 の Server Core インストールが、次の制限付きの配布ポイントとしての使用でサポートされます。  

-   X64 のみがサポートされています。  

-   このオペレーティング システムの配布ポイントでは、PXE またはマルチキャストをサポートしません。  

## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>Windows Server 2012 R2 の Server Core のインストール  
 前のオペレーティング システムだけでなく、Windows Server 2012 R2 の Server Core インストールが、次の制限付きの配布ポイントとしての使用でサポートされます。  

-   X64 のみがサポートされています。  

-   このオペレーティング システムの配布ポイントでは、PXE またはマルチキャストをサポートしません。  



<!--HONumber=Nov16_HO1-->


