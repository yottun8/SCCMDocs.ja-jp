---
title: サイト システムの役割オプション
titleSuffix: Configuration Manager
description: この記事では、必ずしも説明の必要がないとは言えない、Configuration Manager サイト システム役割の詳細を示します。
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 379fa3637d1634caf4797b1f1b7029e3531158cc
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893527"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Configuration Manager でのサイト システムの役割の構成オプション

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager のサイト システムの役割のほとんどの構成オプションについては、説明の必要がないか、構成時にウィザードかダイアログ ボックスで説明されます。 以下のセクションでは、追加情報を必要とする設定があるサイト システムの役割について説明します。  



##  <a name="BKMK_ApplicationCatalog_Website"></a> アプリケーション カタログ Web サイト ポイント  

> [!Note]  
> バージョン 1806 以降、アプリケーション カタログ Web サイト ポイントは "*必要*" ではなくなりましたが、まだ "*サポートされています*"。 詳しくは、「[ソフトウェア センターの構成](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex)」をご覧ください。  
> 
> アプリケーション カタログ Web サイト ポイントの **Silverlight ユーザー エクスペリエンス**は現在サポートされていません。 詳細については、[削除された機能と非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)に関するページを参照してください。  

 アプリケーション カタログ Web サイト ポイントの設定方法について詳しくは、「[アプリケーション管理の計画と構成](/sccm/apps/plan-design/plan-for-and-configure-application-management)」をご覧ください。  

 #### <a name="client-connections"></a>クライアント接続
 セキュリティを高めた接続設定を使用し、クライアントがインターネットから接続してきているかどうかをチェックするには、**[HTTPS]** を選択します。 このオプションでは、クライアントに対してサーバーを認証し、Secure Socket Layer (SSL) を介してデータを暗号化するために、PKI 証明書がサーバー上にあることが必要とされます。 詳細については、「[PKI 証明書の要件](/sccm/core/plan-design/network/pki-certificate-requirements)」を参照してください。  

 サーバー証明書の展開例と、それをインターネット インフォメーション サービス (IIS) で構成する方法については、「[IIS を実行するサイト システム用の Web サーバー証明書の展開](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)」をご覧ください。  

 #### <a name="add-application-catalog-website-to-trusted-sites-zone"></a>アプリケーション カタログ Web サイトを信頼済みサイト ゾーンに追加する  
 メッセージに既定のクライアント設定の値が表示され、**[Add Application Catalog website to Internet Explorer trusted sites zone (アプリケーション カタログ Web サイトを、Internet Explorer の信頼済みサイト ゾーンに追加する)]** クライアント設定が現在 **[True]** と **[False]** のどちらに設定されているかが示されます。 カスタム クライアント設定を使用してこの設定を構成した場合は、この設定を有効にします。  

 このサイト システムが完全修飾ドメイン名 (FQDN) 用に設定されていて、Web サイトが Internet Explorer の信頼済みサイト ゾーンに追加されていない場合は、ユーザーがアプリケーション カタログに接続する際に資格情報を入力するようにプロンプトが表示されます。  

 #### <a name="organization-name"></a>組織名  

 アプリケーション カタログのユーザーに表示される名称を入力します。 ユーザーがこの Web サイトを信頼されるソースとして認識する際に、この組織情報が役立ちます。  



##  <a name="BKMK_ApplicationCatalog_WebService"></a> アプリケーション カタログ Web サービス ポイント  

> [!Note]  
> バージョン 1806 以降、アプリケーション カタログ Web サービス ポイントは "*必要*" ではなくなりましたが、まだ "*サポートされています*"。 詳しくは、「[ソフトウェア センターの構成](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex)」をご覧ください。  

 アプリケーション カタログ Web サービス ポイントの設定方法について詳しくは、「[アプリケーション管理の計画と構成](/sccm/apps/plan-design/plan-for-and-configure-application-management)」をご覧ください。  

 #### <a name="https"></a>HTTPS

 アプリケーション カタログ Web サイト ポイントをこのアプリケーション カタログ Web サービス ポイントに対して認証するには、**[HTTPS]** を選択します。 このオプションでは、サーバーを認証し、SSL を介してデータを暗号化するために、アプリケーション カタログ Web サイト ポイントを実行するサーバー上に PKI 証明書があることが必要とされます。 詳細については、「[PKI 証明書の要件](/sccm/core/plan-design/network/pki-certificate-requirements)」を参照してください。  

 サーバー証明書の展開例と、それをインターネット インフォメーション サービス (IIS) で構成する方法については、「[IIS を実行するサイト システム用の Web サーバー証明書の展開](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)」をご覧ください。  



##  <a name="BKMK_CertificateRegistrationPoint"></a> 証明書登録ポイント  

 証明書登録ポイントの設定方法の詳細については、「[証明書プロファイルの概要](/sccm/protect/deploy-use/introduction-to-certificate-profiles)」を参照してください。  



##  <a name="BKMK_Distribution_Point"></a> 配布ポイント  

 コンテンツ展開の配布ポイントの構成方法については、[コンテンツとコンテンツ インフラストラクチャの管理](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)に関するページをご覧ください。  

 PXE 展開の配布ポイントの設定方法については、[PXE を使用したネットワーク経由での Windows の展開](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network)に関するページをご覧ください。  

 マルチキャスト展開の配布ポイントの設定方法については、[マルチキャストを使用したネットワーク経由での Windows の展開](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network)に関するページをご覧ください。  

 #### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Configuration Manager で必要な場合は IIS をインストールして構成する
 IIS がまだインストールされていない場合に、Configuration Manager で自動的に IIS をインストールして設定するには、このオプションを選択します。 IIS はすべての配布ポイントにインストールする必要があり、ウィザードを続行するにはこの設定を選択する必要があります。  

 #### <a name="site-system-installation-account"></a>サイト システムのインストール アカウント
 サイト サーバーにインストールされている配布ポイントでは、サイト システムのインストール アカウントとしての使用がサポートされているのは、サイト サーバーのコンピューター アカウントだけです。 詳細については、[アカウント](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account)に関するページを参照してください。  

 #### <a name="create-a-self-signed-certificate-or-import-a-pki-client-certificate"></a>自己署名入り証明書を作成するか、PKI クライアント証明書をインポートします
 この証明書には、次の 2 つの目的があります。  

1.  配布ポイントがステータス メッセージを管理ポイントに送信する前に、管理ポイントから認証を受けるようにします。  

2.  **[クライアントの PXE サポートを有効にする]** を選択すると、証明書が PXE ブート用にコンピューターに送信されます。 コンピューターは OS の展開の間、この証明書を使用して管理ポイントに接続します。  

サイトのすべての管理ポイントが HTTP 用に設定されている場合は、自己署名証明書を作成します。 管理ポイントが HTTPS 用に設定されている場合は、PKI クライアント証明書をインポートします。  

証明書をインポートするには、次の Configuration Manager の要件を満たす PKI 証明書を含む公開キー暗号化標準 #12 (PKCS #12) ファイルを見つけます。  

-   使用目的にクライアント認証が含まれている。  

-   秘密キーがエクスポートできるように設定されている。  

証明書のサブジェクト名またはサブジェクトの別名 (SAN) に関する要件は特にありません。 同じ証明書を複数の配布ポイントで使用できます。  

証明書の要件のについては、「[PKI 証明書の要件](/sccm/core/plan-design/network/pki-certificate-requirements)」をご覧ください。 

この証明書の展開の例については、「[配布ポイント用のクライアント証明書の展開](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012)」を参照してください。  

#### <a name="enable-this-distribution-point-for-prestaged-content"></a>事前設定されたコンテンツ用にこの配布ポイントを有効にする
事前設定されたコンテンツ用にこの配布ポイントを有効にするには、このチェック ボックスをオンにします。 このオプションを有効にすると、コンテンツの配布時の動作を設定できます。 配布ポイントで常にコンテンツを事前設定するか、パッケージの初期コンテンツを事前設定するかを選択できますが、コンテンツに更新がある場合には標準のコンテンツ配布プロセスを使用するか、パッケージ内のコンテンツに対して常に標準コンテンツ配布プロセスを使用するようにします。 詳細については、「[事前設定されたコンテンツ](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent)」を参照してください。  

#### <a name="boundary-groups"></a>境界グループ
 境界グループを配布ポイントに関連付けることができます。 コンテンツを展開するときに、クライアントがコンテンツ ソースの場所として配布ポイントを使用するには、クライアントは、その配布ポイントに関連付けられた境界グループ内になければなりません。 境界グループ間の関係を設定してください。有効なコンテンツ ソースの場所を追加の境界グループからクライアントが検索できるようになるタイミングが、その関係によってチェックされるようにします。 詳細については、「[境界グループ](/sccm/core/servers/deploy/configure/boundary-groups)」を参照してください。



##  <a name="BKMK_Enrollment_Point"></a> 登録ポイント  

登録ポイントは、macOS コンピューターをインストールし、オンプレミスのモバイル デバイス管理で管理するデバイスを登録するために使用します。 詳細については、以下の記事を参照してください。  

-   [Mac にクライアントを展開する方法](/sccm/core/clients/deploy/deploy-clients-to-macs)  

-   [ユーザーがオンプレミス MDM にデバイスを登録する方法](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm)  

#### <a name="allowed-connections"></a>許可される接続
 HTTPS 設定が自動的に選択されます。HTTPS 設定では、登録プロキシ ポイントと帯域外サービス ポイントに対してサーバーを認証し、SSL を介してデータを暗号化するために、サーバー上に PKI 証明書があることが必要とされます。 詳細については、「[PKI 証明書の要件](/sccm/core/plan-design/network/pki-certificate-requirements)」を参照してください。  

 サーバー証明書の展開例と、それをインターネット インフォメーション サービス (IIS) で構成する方法については、「[IIS を実行するサイト システム用の Web サーバー証明書の展開](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)」をご覧ください。  



##  <a name="BKMK_Enrollment_Proxy_Point"></a> 登録プロキシ ポイント  

モバイル デバイスの登録プロキシ ポイントの構成方法について詳しくは、「[ユーザーがオンプレミス MDM にデバイスを登録する方法](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm)」をご覧ください。  

#### <a name="client-connections"></a>クライアント接続
 HTTPS 設定が自動的に選択されます。 サーバーで次の PKI 証明書が必要です。 
- Configuration Manager で登録するモバイル デバイスおよび Mac コンピューターに対するサーバー認証用 
- Secure Sockets Layer (SSL) を介したデータの暗号化用

証明書の要件のについては、「[PKI 証明書の要件](/sccm/core/plan-design/network/pki-certificate-requirements)」をご覧ください。  

 サーバー証明書の展開例と、それをインターネット インフォメーション サービス (IIS) で構成する方法については、「[IIS を実行するサイト システム用の Web サーバー証明書の展開](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)」をご覧ください。  



##  <a name="BKMK_Fallback_Status_Point"></a> フォールバック ステータス ポイント  

#### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>状態メッセージの数と調整間隔 (秒)
これらのオプションの既定の設定は、状態メッセージ数が 10,000、調整間隔が 3,600 秒です。 これらの設定はほとんどの状況に十分に対応できますが、次の両方の条件に一致する場合は、変更が必要になることがあります。  

-   フォールバック ステータス ポイントがイントラネットからのみ接続を受け入れる。  

-   多数のコンピューターを対象としたクライアント展開のロールアウト中に、フォールバック ステータス ポイントを使用する。  

この場合は、状態メッセージの継続的なストリームのために状態メッセージのバックログが生成され、サイト サーバーのプロセッサ使用率が長時間高くなることがあります。 さらに、Configuration Manager コンソールとクライアント展開レポートに、クライアント展開の最新情報が表示されない場合もあります。  

これらのフォールバック ステータス ポイント設定は、クライアント展開中に生成される状態メッセージ用に設定するように設計されています。 これらの設定は、インターネット上のクライアントがインターネットベースの管理ポイントに接続できないなどの、クライアントの通信問題用に設定するようには設計されていません。 フォールバック ステータス ポイントは、クライアント展開中に生成された状態メッセージだけに設定を適用することができないため、フォールバック ステータス ポイントがインターネットからの接続を受け入れる場合には、これらの設定は構成しないでください。  

Configuration Manager クライアントを正常にインストールする各コンピューターは、次の 4 つの状態メッセージをフォールバック ステータス ポイントに送信します。  

-   クライアントの展開が開始されました  

-   クライアントの展開に成功しました  

-   クライアントの割り当てが開始されました  

-   クライアントの割り当てに成功しました  

インストールできないコンピューター、または Configuration Manager クライアントを割り当てることができないコンピューターは、追加の状態メッセージを送信します。  

たとえば、Configuration Manager クライアントを 20,000 台のコンピューターに展開する場合、フォールバック ステータス ポイントへの状態メッセージが 80,000 個送信されるとします。 既定のスロットル構成では、3,600 秒 (1 時間) ごとに 10,000 の状態メッセージをフォールバック ステータス ポイントに送信できるため、状態メッセージはフォールバック ステータス ポイント上でバックログされる可能性があります。 また、フォールバック ステータス ポイントとサイト サーバー間の利用可能なネットワーク帯域幅と、サイト サーバーが大量の状態メッセージを扱う処理能力も考慮します。  

このような問題を防止するため、状態メッセージの数を増やして、調整間隔を短くすることを検討してください。  

次の状態のいずれかが該当する場合は、フォールバック ステータス ポイントの調整値を再設定します。  

-   現在のスロットル値が、フォールバック ステータス ポイントからの状態メッセージの処理に必要な値より大きいことが計算される場合。  

-   現在の調整設定では、サイト サーバーのプロセッサ負荷が高くなる場合。  

結果について理解していない場合は、フォールバック ステータス ポイントの調整設定を変更しないでください。 たとえば、調整設定を高くすると、サイト サーバーのプロセッサ負荷が高くなり、すべてのサイト操作の速度が遅くなります。  
