---
title: サポートされるサイト システム サーバー
titleSuffix: Configuration Manager
description: Configuration Manager サイトまたはサイト システムの役割をホストできる Windows バージョンについて説明します。
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fd8e815ab57730ad2186a7e75cd51f21012383a
ms.sourcegitcommit: 265d38d55ca0db043e3a7131a56f123e1d98aa5b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2018
ms.locfileid: "48236176"
---
# <a name="supported-operating-systems-for-configuration-manager-site-system-servers"></a>Configuration Manager サイト システム サーバーでサポートされるオペレーティング システム

*適用対象: System Center Configuration Manager (Current Branch)*


この記事では、Configuration Manager サイトまたはサイト システムの役割をホストできる Windows バージョンについて説明します。


この記事の情報は、次の記事の情報とともに使用します。
-   [Configuration Manager の推奨ハードウェア](/sccm/core/plan-design/configs/recommended-hardware)
-   [Configuration Manager のサイトとサイト システムの前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
-   [Configuration Manager のサイズとスケール番号](/sccm/core/plan-design/configs/size-and-scale-numbers)



## <a name="bkmk_2016"></a> Windows Server 2016: Standard、Datacenter

Configuration Manager バージョン 1606 用の更新プログラムのロールアップ 1 ([KB3186654](https://support.microsoft.com/help/3186654)) により、この OS バージョンは次の役割でサポートされます。

#### <a name="site-servers"></a>サイト サーバー

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト  

#### <a name="site-system-servers"></a>サイト システム サーバー

-   アプリケーション カタログ Web サービス ポイント  
-   アプリケーション カタログ Web サイト ポイント  
-   資産インテリジェンス同期ポイント  
-   証明書登録ポイント  
-   クラウド管理ゲートウェイ コネクション ポイント  
-   データ ウェアハウス サービス ポイント  
-   配布ポイント<sup>[注 1](#bkmk_note1)</sup>  
-   Endpoint Protection ポイント  
-   登録ポイント  
-   登録プロキシ ポイント  
-   フォールバック ステータス ポイント  
-   管理ポイント
-   レポート サービス ポイント  
-   [サービス接続ポイント]  
-   サイト データベース サーバー<sup>[注 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   ソフトウェアの更新ポイント  
-   状態移行ポイント



## <a name="bkmk_stor2016"></a> Windows Storage Server 2016

#### <a name="site-system-server"></a>サイト システム サーバー

-   配布ポイント<sup>[注 1](#bkmk_note1)</sup>  



## <a name="bkmk_2012r2"></a> Windows Server 2012 R2 (x64): Standard、Datacenter  

#### <a name="site-servers"></a>サイト サーバー

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト  

#### <a name="site-system-servers"></a>サイト システム サーバー

-   アプリケーション カタログ Web サービス ポイント  
-   アプリケーション カタログ Web サイト ポイント  
-   資産インテリジェンス同期ポイント  
-   証明書登録ポイント  
-   クラウド管理ゲートウェイ コネクション ポイント  
-   データ ウェアハウス サービス ポイント  
-   配布ポイント<sup>[注 1](#bkmk_note1)</sup>  
-   Endpoint Protection ポイント  
-   登録ポイント  
-   登録プロキシ ポイント  
-   フォールバック ステータス ポイント  
-   管理ポイント
-   レポート サービス ポイント  
-   [サービス接続ポイント]  
-   サイト データベース サーバー<sup>[注 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   ソフトウェアの更新ポイント  
-   状態移行ポイント  



## <a name="bkmk_2012"></a> Windows Server 2012 (x64): Standard、Datacenter  

#### <a name="site-servers"></a>サイト サーバー

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト  

#### <a name="site-system-servers"></a>サイト システム サーバー

-   アプリケーション カタログ Web サービス ポイント  
-   アプリケーション カタログ Web サイト ポイント  
-   資産インテリジェンス同期ポイント  
-   証明書登録ポイント  
-   クラウド管理ゲートウェイ コネクション ポイント  
-   データ ウェアハウス サービス ポイント  
-   配布ポイント<sup>[注 1](#bkmk_note1)</sup>  
-   Endpoint Protection ポイント  
-   登録ポイント  
-   登録プロキシ ポイント  
-   フォールバック ステータス ポイント  
-   管理ポイント
-   レポート サービス ポイント  
-   [サービス接続ポイント]  
-   サイト データベース サーバー<sup>[注 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   ソフトウェアの更新ポイント  
-   状態移行ポイント  



## <a name="bkmk_2008r2sp1"></a> Windows Server 2008 R2 SP1 (x64): Standard、Enterprise、Datacenter  

[マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)で詳述するように、Windows Server 2008 R2 が延長サポートになり、メインストリーム サポートが終了しました。 Configuration Manager を使用したサイト システム サーバーとしてのこれらのオペレーティング システムの将来のサポートについては、「[非推奨のサーバー オペレーティング システム](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems)」を参照してください。  

この OS は、サイト サーバーやほとんどのサイト システムの役割に対してサポートされていません。 プル配布ポイント、PXE およびマルチキャストを含む配布ポイントのサイト システムの役割に対しては引き続きサポートされます。

#### <a name="site-system-servers"></a>サイト システム サーバー
-   配布ポイント<sup>[注 1](#bkmk_note1)</sup>  

    - この OS の配布ポイントでは、PXE およびマルチキャストをサポートします。  



## <a name="bkmk_2008sp2"></a> Windows Server 2008 SP2 (x86, x64): Standard、Enterprise、Datacenter  

[マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)で詳述するように、Windows Server 2008 が延長サポートになり、メインストリーム サポートが終了しました。 Configuration Manager を使用したサイト システム サーバーとしてのこれらのオペレーティング システムの将来のサポートについては、「[非推奨のサーバー オペレーティング システム](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems)」を参照してください。  

この OS は、サイト サーバーとして、または配布ポイントとプル配布ポイントを除くサイト システムの役割としてはサポートされていません。 このサポートの廃止が発表されるまで、またはこの OS の拡張サポート期間が終了するまでは、この OS を配布ポイントとして引き続き使用してください。 詳細については、「[Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095)」 (Windows Server 2008 で System Center Configuration Manager CB および LTSB のインストールに失敗する) を参照してください。

#### <a name="site-system-servers"></a>サイト システム サーバー
-   配布ポイント<sup>[注 1](#bkmk_note1)</sup>  

    -   この OS の配布ポイントでは、PXE およびマルチキャストをサポートします。  

    -   この OS の配布ポイントは、EFI モードでのクライアント コンピューターのネットワーク ブートはサポートしません。 クライアント コンピューターのレガシ モードでの BIOS ブートまたは EFI ブートはサポートされます。  



## <a name="bkmk_win10"></a> Windows 10 (x86, x64): Pro、Enterprise  

#### <a name="site-system-servers"></a>サイト システム サーバー

-   配布ポイント<sup>[注 1](#bkmk_note1)</sup>  

    -   この OS の配布ポイントは、既定の Windows 展開サービスによる PXE ではサポートされません。 バージョン 1806 より、この OS の配布ポイントを **Windows 展開サービスなしで PXE レスポンダーを有効にする**オプションで PXE 対応にすることができます。 詳細については、[配布ポイントのインストールと構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)に関するページを参照してください。  

    -   この OS バージョンの配布ポイントでは、マルチキャストをサポートしません。  



## <a name="bkmk_win81"></a> Windows 8.1 (x86、x64): Professional、Enterprise  

#### <a name="site-system-servers"></a>サイト システム サーバー

-   配布ポイント<sup>[注 1](#bkmk_note1)</sup>  

    -   この OS の配布ポイントは、既定の Windows 展開サービスによる PXE ではサポートされません。 バージョン 1806 より、この OS の配布ポイントを **Windows 展開サービスなしで PXE レスポンダーを有効にする**オプションで PXE 対応にすることができます。 詳細については、[配布ポイントのインストールと構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)に関するページを参照してください。  

    -   この OS バージョンの配布ポイントでは、マルチキャストをサポートしません。  



## <a name="bkmk_win7sp1"></a> Windows 7 SP1 (x86、x64): Professional、Enterprise、Ultimate  

#### <a name="site-system-servers"></a>サイト システム サーバー

-   配布ポイント<sup>[注 1](#bkmk_note1)</sup>  

    -   この OS の配布ポイントは、既定の Windows 展開サービスによる PXE ではサポートされません。 バージョン 1806 より、この OS の配布ポイントを **Windows 展開サービスなしで PXE レスポンダーを有効にする**オプションで PXE 対応にすることができます。 詳細については、[配布ポイントのインストールと構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)に関するページを参照してください。  

    -   この OS バージョンの配布ポイントでは、マルチキャストをサポートしません。  



## <a name="bkmk_core1803"></a> Windows Server バージョン 1803 の Server Core インストール
<!--503702--> Configuration Manager 1802 以降では、[Windows Server バージョン 1803](https://docs.microsoft.com/windows-server/get-started/get-started-with-1803) が、次の制限付きの配布ポイントとしての使用でサポートされます。  

  -   64 ビット バージョンのみがサポートされています。  

  -   この OS の配布ポイントでは、既定の Windows 展開サービスによる PXE またはマルチキャストをサポートしません。 バージョン 1806 より、この OS の配布ポイントを **Windows 展開サービスなしで PXE レスポンダーを有効にする**オプションで PXE 対応にすることができます。 詳細については、[配布ポイントのインストールと構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)に関するページを参照してください。  



## <a name="bkmk_core1709"></a> Windows Server バージョン 1709 の Server Core インストール

Configuration Manager 1710 以降では、[Windows Server バージョン 1709](https://docs.microsoft.com/windows-server/get-started/get-started-with-1709) が、次の制限付きの配布ポイントとしての使用でサポートされます。  

  -   64 ビット バージョンのみがサポートされています。  

  -   この OS の配布ポイントでは、既定の Windows 展開サービスによる PXE またはマルチキャストをサポートしません。 バージョン 1806 より、この OS の配布ポイントを **Windows 展開サービスなしで PXE レスポンダーを有効にする**オプションで PXE 対応にすることができます。 詳細については、[配布ポイントのインストールと構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)に関するページを参照してください。  



## <a name="bkmk_core2016"></a> Windows Server 2016 の Server Core のインストール

Configuration Manager バージョン 1606 用の更新プログラムのロールアップ 1 ([KB3186654](https://support.microsoft.com/help/3186654)) により、この OS バージョンは次の制限付きの配布ポイントとしての使用でサポートされます。  

  -   64 ビット バージョンのみがサポートされています。  

  -   この OS の配布ポイントでは、既定の Windows 展開サービスによる PXE またはマルチキャストをサポートしません。 バージョン 1806 より、この OS の配布ポイントを **Windows 展開サービスなしで PXE レスポンダーを有効にする**オプションで PXE 対応にすることができます。 詳細については、[配布ポイントのインストールと構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)に関するページを参照してください。  



## <a name="bkmk_core2012r2"></a> Windows Server 2012 R2 の Server Core のインストール  

Windows Server 2012 R2 の Server Core インストールが、次の制限付きの配布ポイントとしての使用でサポートされます。  

-   64 ビット バージョンのみがサポートされています。

-   この OS の配布ポイントでは、既定の Windows 展開サービスによる PXE またはマルチキャストをサポートしません。 バージョン 1806 より、この OS の配布ポイントを **Windows 展開サービスなしで PXE レスポンダーを有効にする**オプションで PXE 対応にすることができます。 詳細については、[配布ポイントのインストールと構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)に関するページを参照してください。  



## <a name="bkmk_core2012"></a> Windows Server 2012 の Server Core のインストール  

Windows Server 2012 の Server Core インストールが、次の制限付きの配布ポイントとしての使用でサポートされます。  

-   64 ビット バージョンのみがサポートされています。  

-   この OS の配布ポイントでは、既定の Windows 展開サービスによる PXE またはマルチキャストをサポートしません。 バージョン 1806 より、この OS の配布ポイントを **Windows 展開サービスなしで PXE レスポンダーを有効にする**オプションで PXE 対応にすることができます。 詳細については、[配布ポイントのインストールと構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)に関するページを参照してください。



## <a name="general-notes"></a>一般的な注意事項

#### <a name="bkmk_note1"></a> 注 1: 配布ポイント
配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 詳細については、「[コンテンツ管理インフラストラクチャの展開と管理](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)」をご覧ください。  

#### <a name="bkmk_note2"></a> 注 2: サイト データベース サーバー
サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート記事の「[You may encounter problems when installing SQL Server on a domain controller](https://support.microsoft.com/help/2032911)」(ドメイン コント ローラーに SQL Server をインストールするときに問題が発生する可能性があります) を参照してください。 

さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  
