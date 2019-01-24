---
title: サイトの前提条件
titleSuffix: Configuration Manager
description: Windows コンピューターを Configuration Manager サイト システム サーバーとして構成する方法について説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e8f575fc609dea662688ed10a76733467784a5b9
ms.sourcegitcommit: d5c013a29f53b975fe3a6cb0a41f1e817bd7b235
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54342807"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Configuration Manager のサイトとサイト システムの前提条件

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Windows ベースのコンピューターを Configuration Manager サイト システム サーバーとして使用するには、特定の構成が必要です。 

この記事では、[Windows Server 2012 以降](#bkmk_2012Prereq)を中心に説明しています。 配布ポイント サイト システムの役割に対しては、[Windows Server 2008 R2 および Windows Server 2008](#bkmk_2008) がサポートされます。 詳細については、[サイト システム サーバーでサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)に関するページを参照してください。 

ソフトウェア更新ポイント用の Windows Server Update Services (WSUS) など、一部の製品では、その製品のドキュメントで、使用に関する追加の前提条件と制限を確認する必要があります。 ここでは、Configuration Manager で使用するために行う必要のある構成についてのみ説明します。   

> [!NOTE]  
>  2016 年 1 月に .NET Framework 4.0、4.5、および 4.5.1 のサポートは終了しました。 詳細については、[Microsoft .NET Framework のサポート ライフサイクル ポリシーに関する FAQ](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) を参照してください。  



## <a name="bkmk_generalprerewq"></a> 一般的な要件と制限事項

すべてのサイト システム サーバーに以下の要件が適用されます。

- 各サイト システム サーバーでは、64 ビットの OS を使用する必要があります。 唯一の例外は、配布ポイント サイト システムの役割です。これは、一部の 32 ビット版のオペレーティング システムにインストール可能です。  

- サイト システムは、オペレーティング システムの Server Core インストールではサポートされません。 例外は、配布ポイント サイト システムの役割に対して、Server Core インストールがサポートされていることです。 詳細については、「[Configuration Manager サイト システム サーバーでサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)」を参照してください。  

- サイト システム サーバーは、インストール後、次を変更できません。  

    - サイト システム コンピューターが配置されているドメインのドメイン名 (**ドメイン名の変更**とも呼ばれます)。  

    - コンピューターのドメイン メンバーシップ。  

    - コンピューターの名前です。  

  これらの項目のいずれかを変更する必要がある場合は、まず、コンピューターからサイト システムの役割を削除します。 変更が完了した後、役割を再インストールします。 サイト サーバーに影響する変更の場合は、まず、サイトをアンインストールします。 変更が完了した後、サイトを再インストールします。  

- サイト システムの役割は、Windows Server クラスターのインスタンスではサポートされません。 唯一の例外は、サイト データベース サーバーです。 詳細については、[Configuration Manager サイト データベースでの SQL Server クラスターの使用](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database)に関するページを参照してください。  

- Configuration Manager サービスについては、スタートアップの種類やログオン方法の設定の変更はサポートされていません。 そのようにすると、主要なサービスが正しく実行できなくなる可能性があります。  


###  <a name="bkmk_2012Prereq"></a> Windows Server 2012 以降のオペレーティング システムの前提条件  

Windows Server 2012 以降のサイト システム サーバーと役割に関する特定の前提条件については、この記事の主要なセクションを参照してください。

- [中央管理サイトおよびプライマリ サイト サーバー](#bkmk_2012sspreq)
- [セカンダリ サイト サーバー](#bkmk_2012secpreq)
- [データベース サーバー](#bkmk_2012dbpreq)
- [SMS プロバイダー サーバー](#bkmk_2012smsprovpreq)
- [アプリケーション カタログ Web サイト ポイント](#bkmk_2012acwspreq)
- [アプリケーション カタログ Web サービス ポイント](#bkmk_2012ACwsitepreq)
- [資産インテリジェンス同期ポイント](#bkmk_2012AIpreq)
- [証明書登録ポイント](#bkmk_2012crppreq)
- [配布ポイント](#bkmk_2012dppreq)
- [Endpoint Protection ポイント](#bkmk_2012EPPpreq)
- [登録ポイント](#bkmk_2012Enrollpreq)
- [登録プロキシ ポイント](#bkmk_2012EnrollProxpreq)
- [フォールバック ステータス ポイント](#bkmk_2012FSPpreq)
- [管理ポイント](#bkmk_2012MPpreq)
- [レポート サービス ポイント](#bkmk_2012RSpoint)
- [サービス接続ポイント](#bkmk_SCPpreq)
- [ソフトウェアの更新ポイント](#bkmk_2012SUPpreq)
- [状態移行ポイント](#bkmk_2012SMPpreq)

##  <a name="bkmk_2012sspreq"></a> 中央管理サイトおよびプライマリ サイト サーバー 

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

- .NET Framework 3.5 SP1 (またはそれ以降)  

- .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2  

    - .NET Framework のバージョンの詳細については、「[.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)」を参照してください。

- Remote Differential Compression  

#### <a name="windows-adk"></a>Windows ADK  

- 中央管理サイトまたはプライマリ サイトをインストールまたはアップグレードする前に、インストールまたはアップグレードする Configuration Manager のバージョンで必要な Windows アセスメント & デプロイメント キット (ADK) のバージョンをインストールします。 詳細については、「[Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)」を参照してください。  

- 要件の詳細については、「[オペレーティング システムの展開のインフラストラクチャ要件](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)」を参照してください。  

#### <a name="visual-c-redistributable"></a>Visual C++ 再頒布可能ファイル  

- Configuration Manager はサイト サーバーをインストールするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

- 中央管理サイトとプライマリ サイトには、該当する再頒布可能ファイルの x86 および x64 バージョンの両方が必要です。  



##  <a name="bkmk_2012secpreq"></a> セカンダリ サイト サーバー   

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

- .NET Framework 3.5 SP1 (またはそれ以降)  

- .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2  

    - .NET Framework のバージョンの詳細については、「[.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)」を参照してください。  

- Remote Differential Compression  

#### <a name="visual-c-redistributable"></a>Visual C++ 再頒布可能ファイル  

- Configuration Manager はサイト サーバーをインストールするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

- セカンダリ サイトには x64 バージョンのみが必要です。  

#### <a name="default-site-system-roles"></a>既定のサイト システムの役割  

- 既定では、セカンダリ サイトに**管理ポイント**と**配布ポイント**がインストールされます。  

- セカンダリ サイト サーバーが、それらのサイト システムの役割に対する前提条件を満たしていることを確認します。  



##  <a name="bkmk_2012dbpreq"></a> データベース サーバー  

#### <a name="remote-registry-service"></a>リモート レジストリ サービス  

- Configuration Manager サイトのインストール時には、サイト データベースをホストするコンピューターで、**リモート レジストリ** サービスを有効にします。  

#### <a name="sql-server"></a>SQL Server  

- 中央管理サイトまたはプライマリ サイトをインストールする前に、サイト データベースをホストする SQL Server のサポートされているバージョンをインストールします。 詳細については、[サポートされている SQL Server のバージョン](/sccm/core/plan-design/configs/support-for-sql-server-versions)に関するページを参照してください。  

- セカンダリ サイトをインストールする前に、サポートされているバージョンの SQL Server をインストールすることができます。  

- セカンダリ サイトのインストールの一環として Configuration Manager によって SQL Server Express をインストールする場合は、コンピューターが SQL Server Express を実行する要件を満たしていることを確認します。  



##  <a name="bkmk_2012smsprovpreq"></a> SMS プロバイダー サーバー  

#### <a name="windows-adk"></a>Windows ADK  

- SMS プロバイダーのインスタンスをインストールするコンピューターには、インストールまたはアップグレードする Configuration Manager のバージョンで必要な Windows ADK のバージョンが必要です。 詳細については、「[Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)」を参照してください。  

- 要件の詳細については、「[オペレーティング システムの展開のインフラストラクチャ要件](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)」を参照してください。  



##  <a name="bkmk_2012acwspreq"></a> アプリケーション カタログ Web サイト ポイント  

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

- .NET Framework 3.5 SP1 (またはそれ以降)  

- .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2  

    - ASP.NET 4.5  

    - .NET Framework のバージョンの詳細については、「[.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)」を参照してください。  


#### <a name="iis-configuration"></a>IIS の構成  

-   共通の HTTP 機能:  

    -   既定のドキュメント  

    -   静的コンテンツ  

-   アプリケーションの開発:  

    -   ASP.NET 3.5 (および、自動的に選択されるオプション)  

    -   ASP.NET 4.5 (および、自動的に選択されるオプション)  

    -   .NET 拡張機能 3.5  

    -   .NET 拡張機能 4.5  

-   セキュリティ:  

    -   Windows 認証  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  



##  <a name="bkmk_2012ACwsitepreq"></a> アプリケーション カタログ Web サービス ポイント  

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

-   .NET Framework 3.5 SP1 (またはそれ以降)  

-   .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2:  

    -   ASP.NET 4.5:  

        -   HTTP アクティブ化 (および、自動的に選択されるオプション)  

#### <a name="iis-configuration"></a>IIS の構成  

-   共通の HTTP 機能:  

    -   既定のドキュメント  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

-   アプリケーションの開発:  

    -   ASP.NET 3.5 (および、自動的に選択されるオプション)  

    -   .NET 拡張機能 3.5  

    -   ASP.NET 4.5 (および、自動的に選択されるオプション)  

    -   .NET 拡張機能 4.5  

#### <a name="computer-memory"></a>コンピューターのメモリ  

-   このサイト システムの役割をホストするコンピューターには、サイト システムの役割が要求を処理するために、コンピューターの使用可能メモリの最低 5% を空けておく必要があります。  

-   このサイト システムの役割が同じ要件の別のサイト システムの役割と併置される場合、このコンピューターに対するメモリの要件は増加しませんが、最低 5% の要件は維持されます。  



##  <a name="bkmk_2012AIpreq"></a> 資産インテリジェンス同期ポイント  

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

-   .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2 



##  <a name="bkmk_2012crppreq"></a> 証明書登録ポイント  

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

-   .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2:  

    -   HTTP アクティブ化  

#### <a name="iis-configuration"></a>IIS の構成  

-   アプリケーションの開発:  

    -   ASP.NET 3.5 (および、自動的に選択されるオプション)  

    -   ASP.NET 4.5 (および、自動的に選択されるオプション)  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

    -   IIS 6 WMI 互換  



##  <a name="bkmk_2012dppreq"></a> 配布ポイント  

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

-   Remote Differential Compression  

#### <a name="iis-configuration"></a>IIS の構成  

-   アプリケーションの開発:  

    -   ISAPI 拡張機能  

-   セキュリティ:  

    -   Windows 認証  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

    -   IIS 6 WMI 互換  

#### <a name="powershell"></a>PowerShell  

-   Windows Server 2012 以降では、配布ポイントをインストールする前に、PowerShell 3.0 または 4.0 が必要になります。  

#### <a name="visual-c-redistributable"></a>Visual C++ 再頒布可能ファイル  

-   Configuration Manager は配布ポイントをホストするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

-   インストールされるバージョンは、コンピューターのプラットフォーム (x86 または x64) によって異なります。  

#### <a name="microsoft-azure"></a>Microsoft Azure  

-   Microsoft Azure のクラウド サービスを使用して、配布ポイントをホストできます。  

#### <a name="to-support-pxe-or-multicast"></a>PXE またはマルチキャストをサポートするには  

-   Windows 展開サービス (WDS) の Windows サーバー ロールをインストールして構成します。  

    > [!NOTE]  
    >  WDS は、PXE またはマルチキャストをサポートするように配布ポイントを構成するときに、Windows Server 2012 以降を実行するサーバーに自動的にインストールされ構成されます。  

-   バージョン 1806 以降では、Windows 展開サービスなしで、配布ポイントで PXE レスポンダーを有効にします。  

詳細については、[配布ポイントのインストールと構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)に関するページを参照してください。

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> 配布ポイントではコンテンツを転送するときに、Windows に組み込まれた**バックグラウンド インテリジェント転送サービス** (BITS) が使用されます。 配布ポイントの役割では、オプションの BITS IIS サーバー拡張機能をインストールする必要はありません。これは、クライアントではそこに情報がアップロードされないためです。  



##  <a name="bkmk_2012EPPpreq"></a> Endpoint Protection ポイント  

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

-   .NET Framework 3.5 SP1 (またはそれ以降)  

-   Windows Defender の機能 (Windows Server 2016 以降)  



##  <a name="bkmk_2012Enrollpreq"></a> 登録ポイント  

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

-   .NET framework 3.5 (またはそれ以降)  

-   .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2:  

     このサイト システムの役割のインストール時に Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework の再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

    -   HTTP アクティブ化 (および、自動的に選択されるオプション)  

    -   ASP.NET 4.5  

#### <a name="iis-configuration"></a>IIS の構成  

-   共通の HTTP 機能:  

    -   既定のドキュメント  

-   アプリケーションの開発:  

    -   ASP.NET 3.5 (および、自動的に選択されるオプション)  

    -   .NET 拡張機能 3.5  

    -   ASP.NET 4.5 (および、自動的に選択されるオプション)  

    -   .NET 拡張機能 4.5  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

#### <a name="computer-memory"></a>コンピューターのメモリ  

-   このサイト システムの役割をホストするコンピューターには、サイト システムの役割が要求を処理するために、コンピューターの使用可能メモリの最低 5% を空けておく必要があります。  

-   このサイト システムの役割が同じ要件の別のサイト システムの役割と併置される場合、このコンピューターに対するメモリの要件は増加しませんが、最低 5% の要件は維持されます。  



##  <a name="bkmk_2012EnrollProxpreq"></a> 登録プロキシ ポイント  

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

-   .NET framework 3.5 (またはそれ以降)  

-   .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2 

     このサイト システムの役割のインストール時に Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework の再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

#### <a name="iis-configuration"></a>IIS の構成  

-   共通の HTTP 機能:  

    -   既定のドキュメント  

    -   静的コンテンツ  

-   アプリケーションの開発:  

    -   ASP.NET 3.5 (および、自動的に選択されるオプション)  

    -   ASP.NET 4.5 (および、自動的に選択されるオプション)  

    -   .NET 拡張機能 3.5  

    -   .NET 拡張機能 4.5  

-   セキュリティ:  

    -   Windows 認証  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

#### <a name="computer-memory"></a>コンピューターのメモリ  

-   このサイト システムの役割をホストするコンピューターには、サイト システムの役割が要求を処理するために、コンピューターの使用可能メモリの最低 5% を空けておく必要があります。  

-   このサイト システムの役割が同じ要件の別のサイト システムの役割と併置される場合、このコンピューターに対するメモリの要件は増加しませんが、最低 5% の要件は維持されます。  



##  <a name="bkmk_2012FSPpreq"></a> フォールバック ステータス ポイント 

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能 

-   BITS サーバー拡張 (および自動的に選択されるオプション)、またはバックグラウンド インテリジェント転送サービス (BITS) (および自動的に選択されるオプション) 

#### <a name="iis-configuration"></a>IIS の構成 

既定の IIS 構成に加え、次が必要です。  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  



##  <a name="bkmk_2012MPpreq"></a> 管理ポイント  

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

-   .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2 

-   BITS サーバー拡張 (および自動的に選択されるオプション)、またはバックグラウンド インテリジェント転送サービス (BITS) (および自動的に選択されるオプション)  

#### <a name="iis-configuration"></a>IIS の構成  

-   アプリケーションの開発:  

    -   ISAPI 拡張機能  

-   セキュリティ:  

    -   Windows 認証  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

    -   IIS 6 WMI 互換  



##  <a name="bkmk_2012RSpoint"></a> レポート サービス ポイント  

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

-   .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2 

#### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

-   レポート ポイントをインストールする前に、SQL Server Reporting Services をサポートするために、SQL Server の 1 つ以上のインスタンスをインストールして構成します。  

-   SQL Server Reporting Services に使用するインスタンスは、サイト データベースに使用するインスタンスと同じものにすることができます。  

-   さらに、そのインスタンスを別の System Center 製品と共有して使用することもできます。ただし、他の System Center 製品に SQL Server のインスタンスの共有に対する制限がない場合に限ります。  



##  <a name="bkmk_SCPpreq"></a> サービス接続ポイント  

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

-   .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2 

     このサイト システムの役割のインストール時に Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework の再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

#### <a name="visual-c-redistributable"></a>Visual C++ 再頒布可能ファイル  

-   Configuration Manager は配布ポイントをホストするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

-   サイト システムの役割には、x64 バージョンが必要です。  



##  <a name="bkmk_2012SUPpreq"></a> ソフトウェアの更新ポイント  

#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

-   .NET Framework 3.5 SP1 (またはそれ以降)  

-   .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2 

既定の IIS 構成が必要です。

#### <a name="windows-server-update-services"></a>Windows Server Update Services  

-   ソフトウェアの更新ポイントをインストールする前に、コンピューターに Windows サーバーの役割の Windows Server Update Services をインストールします。  

-   詳細については、[ソフトウェア更新プログラムの計画](/sccm/sum/plan-design/plan-for-software-updates)に関するページを参照してください。  



##  <a name="bkmk_2012SMPpreq"></a> 状態移行ポイント  
<!--SCCMDocs issue 645-->
#### <a name="windows-server-roles-and-features"></a>Windows Server の役割と機能  

-   .NET framework 3.5 (またはそれ以降)  

-   .NET Framework 4.5.2、4.6.1、4.6.2、4.7、4.7.1、4.7.2:  

     このサイト システムの役割のインストール時に Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework の再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

    -   HTTP アクティブ化 (および、自動的に選択されるオプション)  

    -   ASP.NET 4.5  

#### <a name="iis-configuration"></a>IIS の構成  

-   共通の HTTP 機能:  

    -   既定のドキュメント  

-   アプリケーションの開発:  

    -   ASP.NET 3.5 (および、自動的に選択されるオプション)  

    -   .NET 拡張機能 3.5  

    -   ASP.NET 4.5 (および、自動的に選択されるオプション)  

    -   .NET 拡張機能 4.5  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  



##  <a name="bkmk_2008"></a> Windows Server 2008 R2 および Windows Server 2008 の前提条件  

[マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)で詳述するように、Windows Server 2008 および Windows Server 2008 R2 が延長サポートになり、メインストリーム サポートが終了しました。 Configuration Manager を使用したサイト システム サーバーとしてのこれらのオペレーティング システムの将来のサポートについては、[削除されたり非推奨になったサーバー オペレーティング システム](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems)に関する説明をご覧ください。  

これらの OS バージョンは、サイト サーバーやほとんどのサイト システムの役割に対してサポートされていません。 プル配布ポイント、PXE およびマルチキャストを含む配布ポイントのサイト システムの役割に対しては引き続きサポートされます。


###  <a name="bkmk_2008dppreq"></a> 配布ポイント  

#### <a name="iis-configuration"></a>IIS の構成

既定の IIS 構成を使用することも、カスタム構成を使用することもできます。 カスタムの IIS 構成を使用するには、次に示す IIS のオプションを有効にする必要があります。  

-   アプリケーションの開発:  

    -   ISAPI 拡張機能  

-   セキュリティ:  

    -   Windows 認証  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

    -   IIS 6 WMI 互換  

カスタムの IIS 構成を使用する場合は、次に示すような不要な項目を削除できます。  

-   共通の HTTP 機能:  

    -   HTTP リダイレクト  

-   IIS 管理スクリプトおよびツール  

#### <a name="windows-feature"></a>Windows の機能  

-   Remote Differential Compression  

#### <a name="visual-c-redistributable"></a>Visual C++ 再頒布可能ファイル  

-   Configuration Manager は配布ポイントをホストするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

-   インストールされるバージョンは、コンピューターのプラットフォーム (x86 または x64) によって異なります。  

#### <a name="microsoft-azure"></a>Microsoft Azure  

-   Azure のクラウド サービスを使用して、配布ポイントをホストできます。  

#### <a name="to-support-pxe-or-multicast"></a>PXE またはマルチキャストをサポートするには  

-   Windows 展開サービス (WDS) の Windows サーバー ロールをインストールして構成します。  

    > [!NOTE]  
    >  WDS は、PXE またはマルチキャストをサポートするように配布ポイントを構成するときに、Windows Server 2012 以降を実行するサーバーに自動的にインストールされ構成されます。  

-   バージョン 1806 以降では、Windows 展開サービスなしで、配布ポイントで PXE レスポンダーを有効にします。  

詳細については、[配布ポイントのインストールと構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)に関するページを参照してください。

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> 配布ポイントはコンテンツを転送するときに、Windows オペレーティング システムに組み込まれた**バックグラウンド インテリジェント転送サービス** (BITS) を使用します。 配布ポイントの役割には、クライアントがそこに情報をアップロードしないため、オプションの BITS IIS サーバー拡張機能をインストールする必要はありません。   

