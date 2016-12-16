---
title: "サイトの前提条件 | System Center Configuration Manager"
description: "Windows コンピューターを System Center Configuration Manager サイト システム サーバーとして構成する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0f24fd912b3e65dc0c0074ef1c8f76cc128a716c

---
# <a name="site-and-site-system-prerequisites-for-system-center-configuration-manager"></a>System Center Configuration Manager のサイトとサイト システムの前提条件

*適用対象: System Center Configuration Manager (Current Branch)*


 Windows コンピューターでは、System Center Configuration Manager サイト システム サーバーとしての使用をサポートするために、特定の構成が必要です。  


 ソフトウェア更新ポイント用の Windows Server Update Services (WSUS) など、一部の製品では、その製品のドキュメントで、その製品を使用するための追加の前提条件と制限を確認する必要があります。 ここでは、Configuration Manager と共に使用するために直接適用する構成についてのみ説明します。   

> [!NOTE]  
>  2016 年 1 月 12 日に、.NET 4.0、4.5、および 4.5.1 のサポートが期限切れになります。 詳細については、support.microsoft.com の [Microsoft .NET Framework のサポート ライフサイクル ポリシーに関する FAQ](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) を参照してください。  

## <a name="a-namebkmkgeneralprerewqa-general-site-server-requierments-and-limitations"></a><a name="bkmk_generalprerewq"></a> 全般的なサイト サーバーの要件と制限:
**すべてのサイト システム サーバーに適用される内容:**

-   各サイト システム サーバーでは、64 ビットのオペレーティング システムを使用する必要があります。 唯一の例外は、配布ポイント サイト システムの役割です。これは、一部の 32 ビット版のオペレーティング システムにインストール可能です。  

-   サイト システムは、オペレーティング システムの Server Core インストールではサポートされません。 この例外は、PXE やマルチキャストのサポートなしで、配布ポイント サイト システムの役割に対して、Server Core インストールがサポートされていることです。  

-   サイト システム サーバーのインストールされると、次の項目の変更がサポートされなくなります。  

    -   サイト システム コンピューターが配置されているドメインのドメイン名 (**ドメイン名の変更**と呼ぶこともあります)  

    -   コンピューターのドメイン メンバーシップ  

    -   コンピューターの名前  

  これらのいずれかの変更が必要な場合は、最初にコンピューターからサイト システムの役割を削除して、変更の完了後に役割を再インストールする必要があります。 これがサイト サーバー コンピューターに影響する場合は、サイトをアンインストールして、変更の完了後にサイトを再インストールする必要があります。  

-   サイト システムの役割は、Windows Server クラスターのインスタンスではサポートされません。 唯一の例外は、サイト データベース サーバーです。  

-   Configuration Manager サービスについては、スタートアップの種類やログオン方法の設定の変更はサポートされていません。 そのようにすると、主要なサービスが正しく実行できなくなる可能性があります。  

##  <a name="a-namebkmk2012prereqa-prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a> Windows Server 2012 以降のオペレーティング システムの前提条件  
###  <a name="a-namebkmk2012sspreqa-site-server---central-administration-site-and-primary-site"></a><a name="bkmk_2012sspreq"></a> サイト サーバー - 中央管理サイトおよびプライマリ サイト  
  **Windows Server の役割と機能:**  

-   .NET Framework 3.5 SP1 (またはそれ以降)  

-   .NET Framework 4.5.2  

-   Remote Differential Compression  

**Windows ADK:**  

-   中央管理サイトまたはプライマリ サイトをインストールまたはアップグレードする前に、インストールまたはアップグレードする Configuration Manager のバージョンで必要な Windows ADK のバージョンをインストールする必要があります。  

    -   1511 バージョンの Configuration Manager では、Windows ADK の Win10 RTM (10.0.10240) バージョンが必要です。  

-   この要件の詳細については、「オペレーティング システムの展開」を参照してください。  

**Visual C++ 再頒布可能ファイル:**  

-   Configuration Manager はサイト サーバーをインストールするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能ファイルをインストールします。  

-   中央管理サイトとプライマリ サイトには、該当する再頒布可能ファイルの x86 および x64 バージョンの両方が必要です。  

###  <a name="a-namebkmk2012secpreqa-site-server--secondary-site"></a><a name="bkmk_2012secpreq"></a> サイト サーバー - セカンダリ サイト  
**Windows Server の役割と機能:**  

-   .NET Framework 3.5 SP1 (またはそれ以降)  

-   .NET Framework 4.5.2  

-   Remote Differential Compression  

**Visual C++ 再頒布可能ファイル:**  

-   Configuration Manager はサイト サーバーをインストールするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能ファイルをインストールします。  

-   セカンダリ サイトには x64 バージョンのみが必要です。  

**既定のサイト システムの役割:**  

-   既定では、セカンダリ サイトに**管理ポイント**と**配布ポイント**がインストールされます。  

-   セカンダリ サイト サーバーが、それらのサイト システムの役割に対する前提条件を満たしていることを確認します。  

###  <a name="a-namebkmk2012dbpreqa-database-server"></a><a name="bkmk_2012dbpreq"></a> データベース サーバー  
**リモート レジストリ サービス:**  

-   Configuration Manager サイトのインストール時には、サイト データベースをホストするコンピューターで、リモート レジストリ サービスが有効化されている必要があります。  

 **SQL Server**  

-   中央管理サイトまたはプライマリ サイトをインストールする前に、サイト データベースをホストする SQL Server のサポートされているバージョンをインストールする必要があります。  

-   セカンダリ サイトをインストールする前に、サポートされているバージョンの SQL Server をインストールすることができます。  

-   セカンダリ サイトのインストールの一環として Configuration Manager によって SQL Server Express をインストールする場合は、コンピューターが SQL Server Express を実行する要件を満たしていることを確認します。  

###  <a name="a-namebkmk2012smsprovpreqa-sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a> SMS プロバイダー サーバー  
**Windows ADK:**  

-   SMS プロバイダーのインスタンスをインストールするコンピューターには、インストールまたはアップグレードする Configuration Manager のバージョンで必要な Windows ADK のバージョンが必要です。  

    -   1511 バージョンの Configuration Manager では、Windows ADK の Win10 RTM (10.0.10240) バージョンが必要です。  

-   この要件の詳細については、「オペレーティング システムの展開」を参照してください。  

###  <a name="a-namebkmk2012acwspreqa-application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a> アプリケーション カタログ Web サイト ポイント  
**Windows Server の役割と機能:**  

-   .NET Framework 3.5 SP1 (またはそれ以降)  

-   .NET Framework 4.5.2  

    -   ASP.NET 4.5  

**IIS の構成:**  

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

###  <a name="a-namebkmk2012acwsitepreqa-application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a> アプリケーション カタログ Web サービス ポイント  
**Windows Server の役割と機能:**  

-   .NET Framework 3.5 SP1 (またはそれ以降)  

-   .NET Framework 4.5.2  

    -   ASP.NET 4.5  

        -   HTTP アクティブ化 (および、自動的に選択されるオプション)  

**IIS の構成:**  

-   共通の HTTP 機能:  

    -   既定のドキュメント  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

-   アプリケーションの開発:  

    -   ASP.NET 3.5 (および、自動的に選択されるオプション)  

    -   .NET 拡張機能 3.5  

    -   ASP.NET 4.5 (および、自動的に選択されるオプション)  

    -   .NET 拡張機能 4.5  

**コンピューターのメモリ:**  

-   このサイト システムの役割をホストするコンピューターは、サイト システムの役割が要求を処理できるようにするために、コンピューターの使用可能メモリの最低 5% は空けておく必要があります。  

-   このサイト システムの役割が同じ要件の別のサイト システムの役割と併置される場合、このコンピューターに対するメモリの要件は増加しませんが、最低 5% の要件は維持されます。  

###  <a name="a-namebkmk2012aipreqa-asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a> 資産インテリジェンス同期ポイント  
**Windows Server の役割と機能:**  

-   .NET Framework 4.5.2  

###  <a name="a-namebkmk2012crppreqa-certificate-registration-point"></a><a name="bkmk_2012crppreq"></a> 証明書登録ポイント  
**Windows Server の役割と機能:**  

-   .NET Framework 4.5.2  

    -   HTTP アクティブ化  

**IIS の構成:**  

-   アプリケーションの開発:  

    -   ASP.NET 3.5 (および、自動的に選択されるオプション)  

    -   ASP.NET 4.5 (および、自動的に選択されるオプション)  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

    -   IIS 6 WMI 互換  

###  <a name="a-namebkmk2012dppreqa-distribution-point"></a><a name="bkmk_2012dppreq"></a> 配布ポイント  
**Windows Server の役割と機能:**  

-   Remote Differential Compression  

**IIS の構成:**  

-   アプリケーションの開発:  

    -   ISAPI 拡張機能  

-   セキュリティ:  

    -   Windows 認証  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

    -   IIS 6 WMI 互換  

**PowerShell:**  

-   Windows Server 2012 以降では、配布ポイントをインストールする前に、PowerShell 3.0 または 4.0 が必要になります。  

**Visual C++ 再頒布可能ファイル:**  

-   Configuration Manager は配布ポイントをホストするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

-   インストールされるバージョンは、コンピューターのプラットフォーム (x86 または x64) によって異なります。  

**Microsoft Azure**  

-   Microsoft Azure のクラウド サービスを使用して、配布ポイントをホストできます。  

**PXE またはマルチキャストをサポートするには:**  

-   Windows 展開サービス (WDS) の Windows の役割をインストールして構成します。  

    > [!NOTE]  
    >  WDS は、PXE またはマルチキャストをサポートするように配布ポイントを構成するときに、Windows Server 2012 以降を実行するサーバーに自動的にインストールされ構成されます。  

> [!NOTE]  
>  配布ポイント サイト システムの役割に、バックグラウンド インテリジェント転送サービス (BITS) は必要ありません。 配布ポイントのコンピューターに BITS が構成されている場合、BITS を使用するクライアントによるコンテンツのダウンロードを効率化するために、配布ポイントのコンピューターの BITS は使用されません。  

###  <a name="a-namebkmk2012epppreqa-endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a> Endpoint Protection ポイント  
**Windows Server の役割と機能:**  

-   .NET Framework 3.5 SP1 (またはそれ以降)  

###  <a name="a-namebkmk2012enrollpreqa-enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a> 登録ポイント  
**Windows Server の役割と機能:**  

-   .NET framework 3.5 (またはそれ以降)  

-   .NET Framework 4.5.2  

     このサイト システムの役割のインストール時に Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework に関連して再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

    -   HTTP アクティブ化 (および、自動的に選択されるオプション)  

    -   ASP.NET 4.5  


**IIS の構成:**  

-   共通の HTTP 機能:  

    -   既定のドキュメント  

-   アプリケーションの開発:  

    -   ASP.NET 3.5 (および、自動的に選択されるオプション)  

    -   .NET 拡張機能 3.5  

    -   ASP.NET 4.5 (および、自動的に選択されるオプション)  

    -   .NET 拡張機能 4.5  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

**コンピューターのメモリ:**  

-   このサイト システムの役割をホストするコンピューターは、サイト システムの役割が要求を処理できるようにするために、コンピューターの使用可能メモリの最低 5% は空けておく必要があります。  

-   このサイト システムの役割が同じ要件の別のサイト システムの役割と併置される場合、このコンピューターに対するメモリの要件は増加しませんが、最低 5% の要件は維持されます。  

###  <a name="a-namebkmk2012enrollproxpreqa-enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a> 登録プロキシ ポイント  
**Windows Server の役割と機能:**  

-   .NET framework 3.5 (またはそれ以降)  

-   .NET Framework 4.5.2  

     このサイト システムの役割のインストール時に Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework に関連して再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

**IIS の構成:**  

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

**コンピューターのメモリ:**  

-   このサイト システムの役割をホストするコンピューターは、サイト システムの役割が要求を処理できるようにするために、コンピューターの使用可能メモリの最低 5% は空けておく必要があります。  

-   このサイト システムの役割が同じ要件の別のサイト システムの役割と併置される場合、このコンピューターに対するメモリの要件は増加しませんが、最低 5% の要件は維持されます。  

###  <a name="a-namebkmk2012fsppreqa-fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a> フォールバック ステータス ポイント  
**次の追加内容を含む既定の IIS 構成が必要です。**  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

###  <a name="a-namebkmk2012mppreqa-management-point"></a><a name="bkmk_2012MPpreq"></a> 管理ポイント  
**Windows Server の役割と機能:**  

-   .NET Framework 4.5.2  

-   BITS サーバー拡張 (および自動的に選択されるオプション)、またはバックグラウンド インテリジェント転送サービス (BITS) (および自動的に選択されるオプション)  

**IIS の構成:**  

-   アプリケーションの開発:  

    -   ISAPI 拡張機能  

-   セキュリティ:  

    -   Windows 認証  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

    -   IIS 6 WMI 互換  

###  <a name="a-namebkmk2012rspointa-reporting-services-point"></a><a name="bkmk_2012RSpoint"></a> レポート サービス ポイント  
**Windows Server の役割と機能:**  

-   .NET Framework 4.5.2  

**SQL Server Reporting Services:**  

-   レポート サービス ポイントをインストールする前に、SQL Server Reporting Services をサポートするために、SQL Server の 1 つ以上のインスタンスをインストールして構成する必要があります。  

-   SQL Server Reporting Services に使用するインスタンスは、サイト データベースに使用するインスタンスと同じものにすることができます。  

-   さらに、そのインスタンスを別の System Center 製品と共有して使用することもできます。ただし、他の System Center 製品に SQL Server のインスタンスの共有に対する制限がない場合に限ります。  

###  <a name="a-namebkmkscppreqa-service-connection-point"></a><a name="bkmk_SCPpreq"></a> サービス接続ポイント  
**Windows Server の役割と機能:**  

-   .NET Framework 4.5.2  

     このサイト システムの役割のインストール時に Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework に関連して再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

**Visual C++ 再頒布可能ファイル:**  

-   Configuration Manager は配布ポイントをホストするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

-   サイト システムの役割では、x64 バージョンが必要です。  

###  <a name="a-namebkmk2012suppreqa-software-update-point"></a><a name="bkmk_2012SUPpreq"></a> ソフトウェアの更新ポイント  
**Windows Server の役割と機能:**  

-   .NET Framework 3.5 SP1 (またはそれ以降)  

-   .NET Framework 4.5.2  

**既定の IIS 構成が必要です。**  

**Windows Server Update Services:**  

-   ソフトウェアの更新ポイントをインストールする前に、コンピューターに Windows サーバーの役割の Windows Server Update Services をインストールする必要があります。  

-   詳細については、「[System Center Configuration Manager でのソフトウェア更新プログラムの計画](../../../sum/plan-design/plan-for-software-updates.md)」を参照してください。  

### <a name="state-migration-point"></a>状態移行ポイント  
**既定の IIS 構成が必要です。**  

##  <a name="a-namebkmk2008a-prerequisites-for-windows-server-2008-r2-and-windows-server-2008"></a><a name="bkmk_2008"></a> Windows Server 2008 R2 および Windows Server 2008 の前提条件  
[マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)で詳述するように、Windows Server 2008 および Windows Server 2008 R2 が延長サポートになり、メインストリーム サポートが終了しました。 Configuration Manager を使用したサイト システム サーバーとしてのこれらのオペレーティング システムの将来のサポートの詳細については、「[System Center Configuration Manager から削除された機能と非推奨の機能](../../../core/plan-design/changes/removed-and-deprecated-features.md)」を参照してください。  

**次は、すべての .NET Framework の要件に適用されます。**  

-   フル バージョンの Microsoft.NET Framework をインストールしてから、サイト システムの役割をインストールします。 たとえば、「[Microsoft .NET Framework 4 (スタンドアロンのインストーラー)](http://go.microsoft.com/fwlink/p/?LinkId=193048)」を参照してください。 Microsoft .NET Framework 4 Client Profile では、この要件は満たされません。  

**次は、すべての Windows Communication Foundation (WCF) の有効化の要件に適用されます。**  

-   WCF のアクティブ化は、サイト システム サーバーの .NET Framework Windows 機能の一部として構成できます。 たとえば、Windows Server 2008 R2 では、**機能の追加ウィザード**を実行して、追加の機能をサーバーにインストールします。 **[機能の選択]** ページで、**[NET Framework 3.5.1 の機能]** を展開してから **[WCF アクティブ化]** を展開します。**[HTTP アクティブ化]** と **[非 HTTP アクティブ化]** の両方のチェック ボックスをオンにして、これらのオプションを有効にします。  

###  <a name="a-namebkmk2008sspreqa-site-server---central-administration-site-and-primary-site"></a><a name="bkmk_2008sspreq"></a> サイト サーバー - 中央管理サイトおよびプライマリ サイト  
**.NET Framework:**  

-   3.5 SP1 (またはそれ以降)  

-   .NET Framework 4.5.2  

**Windows の機能:**  

-   Remote Differential Compression  

**Windows ADK:**  

-   中央管理サイトまたはプライマリ サイトをインストールまたはアップグレードする前に、インストールまたはアップグレードする Configuration Manager のバージョンで必要な Windows ADK のバージョンをインストールする必要があります。  

    -   1511 バージョンの Configuration Manager では、Windows ADK の Win10 RTM (10.0.10240) バージョンが必要です。  

-   この要件の詳細については、「オペレーティング システムの展開」を参照してください。  

**Visual C++ 再頒布可能ファイル:**  

-   Configuration Manager はサイト サーバーをインストールするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能ファイルをインストールします。  

-   中央管理サイトとプライマリ サイトには、該当する再頒布可能ファイルの x86 および x64 バージョンの両方が必要です。  

###  <a name="a-namebkmk2008secpreqa-site-server--secondary-site"></a><a name="bkmk_2008secpreq"></a> サイト サーバー - セカンダリ サイト  
**.NET Framework:**  

-   3.5 SP1 (またはそれ以降)  

-   .NET Framework 4.5.2  

**Visual C++ 再頒布可能ファイル:**  

-   Configuration Manager はサイト サーバーをインストールするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能ファイルをインストールします。  

-   セカンダリ サイトには x64 バージョンのみが必要です。  

**既定のサイト システムの役割:**  

-   既定では、セカンダリ サイトに**管理ポイント**と**配布ポイント**がインストールされます。  

-   セカンダリ サイト サーバーが、それらのサイト システムの役割に対する前提条件を満たしていることを確認します。  

###  <a name="a-namebkmk2008dbpreqa-database-server"></a><a name="bkmk_2008dbpreq"></a> データベース サーバー  
**リモート レジストリ サービス:**  

-   Configuration Manager サイトのインストール時には、サイト データベースをホストするコンピューターで、リモート レジストリ サービスが有効化されている必要があります。  

**SQL Server**  

-   中央管理サイトまたはプライマリ サイトをインストールする前に、サイト データベースをホストする SQL Server のサポートされているバージョンをインストールする必要があります。  

-   セカンダリ サイトをインストールする前に、サポートされているバージョンの SQL Server をインストールすることができます。  

-   セカンダリ サイトのインストールの一環として Configuration Manager によって SQL Server Express をインストールする場合は、コンピューターが SQL Server Express を実行する要件を満たしていることを確認します。  

###  <a name="a-namebkmk2008smsprovpreqa-sms-provider-server"></a><a name="bkmk_2008smsprovpreq"></a> SMS プロバイダー サーバー  
**Windows ADK:**  

-   SMS プロバイダーのインスタンスをインストールするコンピューターには、インストールまたはアップグレードする Configuration Manager のバージョンで必要な Windows ADK のバージョンが必要です。  

    -   1511 バージョンの Configuration Manager では、Windows ADK の Win10 RTM (10.0.10240) バージョンが必要です。  

-   この要件の詳細については、「オペレーティング システムの展開」を参照してください。  

###  <a name="a-namebkmk2008acwspreqa-application-catalog-website-point"></a><a name="bkmk_2008acwspreq"></a> アプリケーション カタログ Web サイト ポイント  
**.NET Framework:**  

-   .NET Framework 4.5.2  

**IIS 構成:** 次の追加内容を含む既定の IIS 構成が必要です。  

-   共通の HTTP 機能:  

    -   静的コンテンツ  

    -   既定のドキュメント  

-   アプリケーションの開発:  

    -   ASP.NET (および、自動的に選択されるオプション)\  

         .NET Framework バージョン 4.5.2 のインストール後に、IIS がインストールまたは再構成された場合など、一部のシナリオでは明示的に ASP.NET バージョン 4.5 をインストールする必要があります。 たとえば、.NET Framework バージョン 4.0.30319 を実行している 64 ビット コンピューターで、**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable** のコマンドを実行します。  

-   セキュリティ:  

    -   Windows 認証  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

###  <a name="a-namebkmk2008acwsitepreqa-application-catalog-web-service-point"></a><a name="bkmk_2008ACwsitepreq"></a> アプリケーション カタログ Web サービス ポイント  
**.NET Framework:**  

-   3.5 SP1 (またはそれ以降)  

-   .NET Framework 4.5.2  

**Windows Communication Foundation (WCF) アクティブ化:**  

-   HTTP アクティブ化  

-   非 HTTP アクティブ化  

**IIS 構成:** 次の追加内容を含む既定の IIS 構成が必要です。  

-   アプリケーションの開発:  

    -   ASP.NET (および、自動的に選択されるオプション)  

         .NET Framework バージョン 4.5.2 のインストール後に、IIS がインストールまたは再構成された場合など、一部のシナリオでは明示的に ASP.NET バージョン 4.5 をインストールする必要があります。 たとえば、.NET Framework バージョン 4.0.30319 を実行している 64 ビット コンピューターで、**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable** のコマンドを実行します。  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

**コンピューターのメモリ:**  

-   このサイト システムの役割をホストするコンピューターは、サイト システムの役割が要求を処理できるようにするために、コンピューターの使用可能メモリの最低 5% は空けておく必要があります。  

-   このサイト システムの役割が同じ要件の別のサイト システムの役割と併置される場合、このコンピューターに対するメモリの要件は増加しませんが、最低 5% の要件は維持されます。  

###  <a name="a-namebkmk2008aipreqa-asset-intelligence-synchronization-point"></a><a name="bkmk_2008AIpreq"></a> 資産インテリジェンス同期ポイント  
**.NET Framework:**  

-   .NET Framework 4.5.2  

###  <a name="a-namebkmk2008crppreqa-certificate-registration-point"></a><a name="bkmk_2008crppreq"></a> 証明書登録ポイント  
**.NET Framework:**  

-   .NET Framework 4.5.2  

-   HTTP アクティブ化  

**IIS 構成:** 次の追加内容を含む既定の IIS 構成が必要です。  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

    -   IIS 6 WMI 互換  

###  <a name="a-namebkmk2008dppreqa-distribution-point"></a><a name="bkmk_2008dppreq"></a> 配布ポイント  
**IIS 構成:** 既定の IIS 構成を使用することも、カスタム構成を使用することもできます。  カスタムの IIS 構成を使用するには、次に示す IIS のオプションを有効にする必要があります。  

-   アプリケーションの開発:  

    -   ISAPI 拡張機能  

-   セキュリティ:  

    -   Windows 認証  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

    -   IIS 6 WMI 互換  

カスタムの IIS 構成を使用する場合は、次に示すような不要なオプションを削除できます。  

-   共通の HTTP 機能:  

    -   HTTP リダイレクト  

-   IIS 管理スクリプトおよびツール  

**Windows の機能:**  

-   Remote Differential Compression  

**Visual C++ 再頒布可能ファイル:**  

-   Configuration Manager は配布ポイントをホストするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

-   インストールされるバージョンは、コンピューターのプラットフォーム (x86 または x64) によって異なります。  

**Microsoft Azure**  

-   Microsoft Azure のクラウド サービスを使用して、配布ポイントをホストできます。  

**PXE またはマルチキャストをサポートするには:**  

-   Windows 展開サービス (WDS) の Windows の役割をインストールして構成します。  

    > [!NOTE]  
    >  WDS は、PXE またはマルチキャストをサポートするように配布ポイントを構成するときに、Windows Server 2012 以降を実行するサーバーに自動的にインストールされ構成されます。  

> [!NOTE]  
>  配布ポイント サイト システムの役割に、バックグラウンド インテリジェント転送サービス (BITS) は必要ありません。 配布ポイントのコンピューターに BITS が構成されている場合、BITS を使用するクライアントによるコンテンツのダウンロードを効率化するために、配布ポイントのコンピューターの BITS は使用されません。  


###  <a name="a-namebkmk2008epppreqa-endpoint-protection-point"></a><a name="bkmk_2008EPPpreq"></a> Endpoint Protection ポイント  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (またはそれ以降)  

###  <a name="a-namebkmk2008enrollpreqa-enrollment-point"></a><a name="bkmk_2008Enrollpreq"></a> 登録ポイント  
**.NET Framework:**  

-   4.5.2  

     このサイト システムの役割をインストールすると、サーバーにサポートされているバージョンの .NET Framework がまだインストールされていない場合、Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework に関連して再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

**Windows Communication Foundation (WCF) アクティブ化:**  

-   HTTP アクティブ化  

-   非 HTTP アクティブ化  

**IIS 構成:** 次の追加内容を含む既定の IIS 構成が必要です。  

-   アプリケーションの開発:  

    -   ASP.NET (および、自動的に選択されるオプション)  

         .NET Framework バージョン 4.5.2 のインストール後に、IIS がインストールまたは再構成された場合など、一部のシナリオでは明示的に ASP.NET バージョン 4.5 をインストールする必要があります。 たとえば、.NET Framework バージョン 4.0.30319 を実行している 64 ビット コンピューターで、**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable** のコマンドを実行します。  

**コンピューターのメモリ:**  

-   このサイト システムの役割をホストするコンピューターは、サイト システムの役割が要求を処理できるようにするために、コンピューターの使用可能メモリの最低 5% は空けておく必要があります。  

-   このサイト システムの役割が同じ要件の別のサイト システムの役割と併置される場合、このコンピューターに対するメモリの要件は増加しませんが、最低 5% の要件は維持されます。  

###  <a name="a-namebkmk2008enrollproxpreqa-enrollment-proxy-point"></a><a name="bkmk_2008EnrollProxpreq"></a> 登録プロキシ ポイント  
**.NET Framework:**  

-   4.5.2  

     このサイト システムの役割をインストールすると、サーバーにサポートされているバージョンの .NET Framework がまだインストールされていない場合、Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework に関連して再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

**Windows Communication Foundation (WCF) アクティブ化:**  

-   HTTP アクティブ化  

-   非 HTTP アクティブ化  

**IIS 構成:** 次の追加内容を含む既定の IIS 構成が必要です。  

-   アプリケーションの開発:  

    -   ASP.NET (および、自動的に選択されるオプション)  

         .NET Framework バージョン 4.5.2 のインストール後に、IIS がインストールまたは再構成された場合など、一部のシナリオでは明示的に ASP.NET バージョン 4.5 をインストールする必要があります。 たとえば、.NET Framework バージョン 4.0.30319 を実行している 64 ビット コンピューターで、**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable** のコマンドを実行します。  

**コンピューターのメモリ:**  

-   このサイト システムの役割をホストするコンピューターは、サイト システムの役割が要求を処理できるようにするために、コンピューターの使用可能メモリの最低 5% は空けておく必要があります。  

-   このサイト システムの役割が同じ要件の別のサイト システムの役割と併置される場合、このコンピューターに対するメモリの要件は増加しませんが、最低 5% の要件は維持されます。  

###  <a name="a-namebkmk2008fsppreqa-fallback-status-point"></a><a name="bkmk_2008FSPpreq"></a> フォールバック ステータス ポイント  
**IIS 構成:** 次の追加内容を含む既定の IIS 構成が必要です。  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

###  <a name="a-namebkmk2008mppreqa-management-point"></a><a name="bkmk_2008MPpreq"></a> 管理ポイント  
**.NET Framework:**  

-   4.5.2  

**IIS 構成:** 既定の IIS 構成を使用することも、カスタム構成を使用することもできます。 モバイル デバイスのサポートを有効にした各管理ポイントでは、ASP.NET (および自動的に選択されるオプション) に対する追加の IIS 構成が必要になります。 .NET Framework バージョン 4.5.2 のインストール後に、IIS がインストールまたは再構成された場合など、一部のシナリオでは明示的に ASP.NET バージョン 4.5 をインストールする必要があります。 たとえば、.NET Framework バージョン 4.0.30319 を実行している 64 ビット コンピューターで、**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable** のコマンドを実行します。  


カスタムの IIS 構成を使用するには、次に示す IIS のオプションを有効にする必要があります。  

-   アプリケーションの開発:  

    -   ISAPI 拡張機能  

-   セキュリティ:  

    -   Windows 認証  

-   IIS 6 管理互換性:  

    -   IIS 6 メタベース互換  

    -   IIS 6 WMI 互換  


カスタムの IIS 構成を使用する場合は、次に示すような不要なオプションを削除できます。  

-   共通の HTTP 機能:  

    -   HTTP リダイレクト  

-   IIS 管理スクリプトおよびツール  

**Windows の機能:**  

-   BITS サーバー拡張 (および自動的に選択されるオプション)、またはバックグラウンド インテリジェント転送サービス (BITS) (および自動的に選択されるオプション)  

###  <a name="a-namebkmk2008rspointa-reporting-services-point"></a><a name="bkmk_2008RSpoint"></a> レポート サービス ポイント  
**.NET Framework:**  

-   4.5.2  

**SQL Server Reporting Services:**  

-   レポート サービス ポイントをインストールする前に、SQL Server Reporting Services をサポートするために、SQL Server の 1 つ以上のインスタンスをインストールして構成する必要があります。  

-   SQL Server Reporting Services に使用するインスタンスは、サイト データベースに使用するインスタンスと同じものにすることができます。  

-   さらに、そのインスタンスを別の System Center 製品と共有して使用することもできます。ただし、他の System Center 製品に SQL Server のインスタンスの共有に対する制限がない場合に限ります。  

###  <a name="a-namebkmk2008scppreqa-service-connection-point"></a><a name="bkmk_2008SCPpreq"></a> サービス接続ポイント  
**.NET Framework:**  

-   4.5.2  

     このサイト システムの役割をインストールすると、サーバーにサポートされているバージョンの .NET Framework がまだインストールされていない場合、Configuration Manager は自動的に .NET Framework 4.5.2 をインストールします。 このインストールでは、サーバーが再起動保留中の状態になる場合があります。 .NET Framework に関連して再起動が保留中である場合は、サーバーが再起動されて、インストールが完了するまで、.NET アプリケーションが失敗する可能性があります。  

**Visual C++ 再頒布可能ファイル:**  

-   Configuration Manager は配布ポイントをホストするコンピューターごとに、Microsoft Visual C++ 2013 再頒布可能パッケージをインストールします。  

-   サイト システムの役割では、x64 バージョンが必要です。  

###  <a name="a-namebkmk2008suppreqa-software-update-point"></a><a name="bkmk_2008SUPpreq"></a> ソフトウェアの更新ポイント  
**.NET Framework:**  

-   3.5 SP1 (またはそれ以降)  

-   .NET Framework 4.5.2  

**IIS 構成:** 既定の IIS 構成が必要です。  

**Windows Server Update Services:**  

-   ソフトウェアの更新ポイントをインストールする前に、コンピューターに Windows サーバーの役割の Windows Server Update Services をインストールする必要があります。  

-   詳細については、「[System Center Configuration Manager でのソフトウェア更新プログラムの計画](../../../sum/plan-design/plan-for-software-updates.md)」を参照してください。

###  <a name="a-namebkmk2008smppreqa-state-migration-point"></a><a name="bkmk_2008SMPpreq"></a> 状態移行ポイント  
**IIS 構成:** 既定の IIS 構成が必要です。  



<!--HONumber=Nov16_HO1-->


