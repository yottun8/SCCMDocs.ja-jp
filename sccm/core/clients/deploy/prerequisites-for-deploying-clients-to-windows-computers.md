---
title: Windows クライアント展開の前提条件
titleSuffix: Configuration Manager
description: Windows コンピューターに Configuration Manager クライアントを展開するための前提条件について説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11474f54aaf7a9afe13d411b0dd469abb1eef963
ms.sourcegitcommit: c2c44329f1f9a2e6c14095360b4fc4aafabc27f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/15/2018
ms.locfileid: "51694945"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Configuration Manager で Windows コンピューターにクライアントを展開するための前提条件

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager クライアントを環境で展開するには、次の外部の依存関係、および製品内の依存関係が必要となります。 それぞれのクライアント展開方法に固有の依存関係もあり、それを満たさないとクライアント インストールを正常に実行できません。  

Configuration Manager クライアントのハードウェアおよび OS の最小要件について詳しくは、「[サポートされている構成](/sccm/core/plan-design/configs/supported-configurations)」をご覧ください。  

> [!NOTE]  
>  この記事に示されているソフトウェア バージョンの番号は、必要な最小のバージョン番号のみを示します。  



##  <a name="BKMK_prereqs_computers"></a> Windows クライアントの前提条件  

Windows デバイスに Configuration Manager クライアントをいつインストールするかの前提条件を判断するには次の情報を使用します。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  

|コンポーネント|説明|  
|---|---|  
|Windows インストーラー バージョン 3.1.4000.2435|Windows インストーラーの更新 (.msp) ファイルを、パッケージおよびソフトウェアの更新に使用できるようにするために必要となります。|  
|Microsoft バックグラウンド インテリジェント転送サービス (BITS) バージョン 2.5|クライアント コンピューターと Configuration Manager サイト システムの間でデータが転送されるときのネットワーク負荷を軽減するために必要となります。 BITS は、クライアント インストール中に自動的にはダウンロードされません。 BITS がコンピューターにインストールされると通常、インストールを完了するために再起動が必要となります。<br /><br /> ほとんどのオペレーティング システムに BITS が含まれています。 そうでない場合は、Configuration Manager クライアントをインストールする前に BITS をインストールします。|  
|Microsoft タスク スケジューラ|クライアントのインストールを完了するために、クライアントでこのサービスを有効にします。|  


### <a name="bkmk_ExternalDependencies"></a> Configuration Manager の外部の依存関係、およびインストール中の自動ダウンロードされる外部の依存関係  

Configuration Manager クライアントには外部の依存関係があります。 これらの依存関係は、クライアント コンピューターの OS バージョンやインストールされたソフトウェアによります。  

インストールを完了するためにクライアントにこれらの依存関係が必要な場合は、それらが自動的にインストールされます。  

|コンポーネント|説明|  
|---|---|  
|Windows Update エージェント バージョン 7.0.6000.363|更新プログラムの検出および展開のサポートに Windows で必要となります。|  
|Microsoft Core XML Services (MSXML) バージョン 6.20.5002 以降|Windows で XML ドキュメントを処理できるようにするために必要となります。|  
|Microsoft Remote Differential Compression (RDC)|ネットワークのデータ転送を最適化するために必要となります。|  
|Microsoft Visual C++ 2013 再頒布可能パッケージ バージョン 12.0.21005.1|クライアントのオペレーションをサポートするために必要となります。 クライアント コンピューターにこの更新プログラムをインストールする場合、インストールを完了するために再起動が必要になる可能性があります。|  
|Microsoft Visual C++ 2005 再頒布可能バージョン 8.0.50727.42|1606 以前のバージョンの場合、Microsoft SQL Server Compact オペレーションをサポートするために必要です。|  
|Windows Imaging APIs 6.0.6001.18000|Configuration Manager が Windows イメージ (.wim) ファイルを管理するのを許可するために必要となります。|  
|Microsoft Policy Platform 1.2.3514.0|クライアントがコンプライアンス設定を評価するのを許可するために必要となります。|  
|Microsoft Silverlight 5.1.41212.0|アプリケーション カタログ ウェブサイトのユーザー エクスペリエンスをサポートするために必要となります。 Configuration Manager 1802 以降では、クライアントは Silverlight を自動的にインストールしません。 アプリケーション カタログの主な機能はソフトウェア センターに含まれるようになりました。 アプリケーション カタログ Web サイトのサポートは、バージョン 1806 で終了します。<!--1356195-->|  
|Microsoft .NET Framework バージョン 4.5.2|クライアントのオペレーションをサポートするために必要となります。 Microsoft .NET Framework バージョン 4.5 以降がインストールされていない場合は、クライアント コンピューターに自動的にインストールされます。 詳細については、「[Microsoft .NET Framework バージョン 4.5.2 に関する追加情報](#dotNet)」を参照してください。|  
|Microsoft SQL Server Compact 4.0 SP1 コンポーネント|クライアント オペレーションに関連した情報を保存するために必要となります。|  


####  <a name="dotNet"></a> Microsoft .NET Framework バージョン 4.5.2 に関する追加情報  

> [!NOTE]  
>  .NET 4.0、4.5、4.5.1 はサポートされなくなりました。 詳細については、[Microsoft .NET Framework のサポート ライフサイクル ポリシーに関する FAQ](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework) を参照してください。  

インストールを完了するには、Microsoft .NET Framework バージョン 4.5.2 の再起動が必要な場合があります。 システム トレイに **[再起動が必要]** 通知が表示されます。 次の一般的なシナリオではクライアント コンピューターの再起動が必要です。  

-   .NET アプリケーションまたはサービスがコンピューター上で実行されている。  

-   .NET インストールに必要な 1 つ以上 のソフトウェア更新プログラムが不足している。  

-   コンピューターで、.NET Framework のソフトウェア更新プログラムの以前のインストールからの再起動が保留されている。  


.NET Framework 4.5.2 をインストールした後、追加の更新プログラムが必要な場合があります。 これらの追加の更新プログラムでは、コンピューターの再起動が追加で必要になることがあります。  


### <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  

詳細については、[クライアントのサイト システムの役割の決定](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients)に関するページを参照してください。  

|コンポーネント|説明|  
|---|---|  
|管理ポイント|Configuration Manager クライアントを展開するには、管理ポイントは必要ありません。 クライアントでは、サイト情報を転送するために管理ポイントが必要です。 管理ポイントがないと、クライアント コンピューターを管理できません。|  
|配布ポイント|配布ポイントはオプションですが、クライアントの展開および管理において推奨されるサイト システムの役割です。 すべての配布ポイントは、クライアント ソース ファイルをホストします。 クライアントは、クライアントの展開または更新中にソース ファイルをダウンロードする最寄りの配布ポイントを検索します。 サイトに配布ポイントがない場合、コンピューターは管理ポイントからクライアント ソース ファイルをダウンロードします。|  
|フォールバック ステータス ポイント|フォールバック ステータス ポイントはオプションですが、クライアント展開において推奨されるサイト システムの役割です。 フォールバック ステータス ポイントにより、クライアントの展開が追跡され、Configuration Manager サイトのコンピューターは、管理ポイントとやり取りできないときに状態メッセージを送信できるようになります。|  
|レポート サービス ポイント|レポート サービス ポイントはオプションですが、推奨されるサイト システムの役割です。 クライアントの展開と管理に関連するレポートが表示されます。 詳細については、[Configuration Manager のレポート](/sccm/core/servers/manage/reporting)に関する記事を参照してください。|  


### <a name="installation-method-dependencies"></a>インストール方法の依存関係  

次の前提条件は、クライアント インストールのさまざまな方法に固有です。  

#### <a name="client-push-installation"></a>クライアント プッシュ インストール  

   -   サイトでは、クライアント プッシュ インストール アカウントを使用してコンピューターに接続し、クライアントをインストールします。 これらのアカウントを [クライアント プッシュ インストールのプロパティ] の **[アカウント]** タブで指定します。 アカウントは、展開先のコンピューターでローカルの管理者グループのメンバーである必要があります。  

         クライアント プッシュ インストール アカウントを指定しない場合、サイト サーバーではそのコンピューター アカウントが使用されます。  

   -   クライアントをインストールしているコンピューターがサイトによって検出される必要があります。 少なくとも 1 つの Configuration Manager 探索方法が必要です。  

   -   コンピューターに ADMIN$ 共有が必要です。  

   -   検出されたリソースに Configuration Manager クライアントを自動的にプッシュするには、[クライアント プッシュ インストールのプロパティ] で **[割り当てられたリソースへのクライアント プッシュ インストールを有効にする]** オプションを選択します。  

   -   クライアント コンピューターは、配布ポイントまたは管理ポイントと通信してソース ファイルをダウンロードする必要があります。  

   -   バージョン 1806 以降、Kerberos の相互認証が必要な場合、クライアントは、信頼された Active Directory フォレスト内にある必要があります。 Windows の Kerberos は、相互認証を Active Directory に依存しています。<!--1358204-->  


クライアント プッシュを使用するには、次のセキュリティ アクセス許可が必要です。  

   -   クライアント プッシュ インストール アカウントを構成する: **サイト** オブジェクトの **変更**と**読み取り**アクセス許可。  

   -   コレクション、デバイス、クエリにクライアントをインストールするためのクライアント プッシュの使用: **コレクション** オブジェクトの**リソースの変更**と**読み取り**アクセス許可。  


**[インフラストラクチャの管理者]** の既定のセキュリティ ロールには、クライアント プッシュ インストールを管理するのに必要な許可が含まれています。  


#### <a name="software-update-point-based-installation"></a>ソフトウェアの更新ポイント経由のインストール  

   -   Active Directory スキーマを拡張していない場合、または別のフォレストからクライアントをインストールする場合は、グループ ポリシーを使用して CCMSetup.exe のインストール パラメーターをプロビジョニングします。 詳細については、[クライアント インストールのプロパティの準備方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision)に関するページを参照してください。  

   -   Configuration Manager クライアントをソフトウェアの更新ポイントに発行します。  

   -   ソース ファイルをダウンロードするには、クライアント コンピューターが配布ポイントまたは管理ポイントと通信する必要があります。  


Configuration Manager ソフトウェア更新プログラムの管理に必要なセキュリティのアクセス許可については、[ソフトウェア更新プログラムの前提条件](/sccm/sum/plan-design/prerequisites-for-software-updates)に関するページを参照してください。  


#### <a name="group-policy-based-installation"></a>グループ ポリシーを使用したインストール  

   -   Active Directory スキーマを拡張していない場合、または別のフォレストからクライアントをインストールする場合は、グループ ポリシーを使用して CCMSetup.exe のインストール パラメーターをプロビジョニングします。 詳細については、[クライアント インストールのプロパティの準備方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision)に関するページを参照してください。  

   -   ソース ファイルをダウンロードするには、クライアント コンピューターが配布ポイントまたは管理ポイントと通信する必要があります。  


#### <a name="logon-script-based-installation"></a>ログオン スクリプトを使用したインストール  

ソース ファイルをダウンロードするには、クライアント コンピューターが配布ポイントまたは管理ポイントと通信する必要があります。 ただし、CCMSetup.exe を次のコマンド ライン パラメーターで指定した場合を除きます: `ccmsetup /source`  


#### <a name="manual-installation"></a>手動インストール  

ソース ファイルをダウンロードするには、クライアント コンピューターが配布ポイントまたは管理ポイントと通信する必要があります。 ただし、CCMSetup.exe を次のコマンド ライン パラメーターで指定した場合を除きます: `ccmsetup /source`  


#### <a name="microsoft-intune-mdm-installation"></a>Microsoft Intune MDM のインストール

 - Microsoft Intune サブスクリプションと適切なライセンスが必要です。  

 - デバイスは、インターネット ベースでない場合でもインターネットにアクセスできる必要があります。  

 - ユース ケースに応じて、次のテクノロジのいずれか、または両方が必要になる場合もあります。  

     - Azure Active Directory  

     - クラウド管理ゲートウェイ  


#### <a name="workgroup-computer-installation"></a>ワークグループ コンピューターのインストール  

Configuration Manager サイト サーバーのドメイン内のリソースにアクセスするには、このサイト用にネットワーク アクセス アカウントを構成します。  

ネットワーク アクセス アカウントの構成方法の詳細については、[コンテンツ管理の基本的な概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)に関するページを参照してください。  


#### <a name="software-distribution-based-installation-for-upgrades-only"></a>ソフトウェアの配布を使用したインストール (アップグレードのみ)  

   -   Active Directory スキーマを拡張していない場合、または別のフォレストからクライアントをインストールする場合は、グループ ポリシーを使用して CCMSetup.exe のインストール パラメーターをプロビジョニングします。 詳細については、[クライアント インストールのプロパティの準備方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision)に関するページを参照してください。   

   -   ソース ファイルをダウンロードするには、クライアント コンピューターが配布ポイントまたは管理ポイントと通信する必要があります。  


アプリケーション管理を使用して Configuration Manager クライアントをアップグレードするのに必要なセキュリティのアクセス許可については、「[アプリケーション管理に関するセキュリティとプライバシー](/sccm/apps/plan-design/security-and-privacy-for-application-management)」を参照してください。  


#### <a name="automatic-client-upgrades"></a>自動のクライアント アップグレード  

自動のクライアント アップグレードを構成するには、セキュリティの役割である **[完全な権限を持つ管理者]** のメンバーである必要があります。  


### <a name="firewall-requirements"></a>ファイアウォールの要件  

サイト システム サーバーと Configuration Manager クライアントをインストールするコンピューターとの間にファイアウォールがある場合は、[クライアントの Windows ファイアウォールとポートの設定](/sccm/core/clients/deploy/windows-firewall-and-port-settings-for-clients)に関するページを参照してください。  



##  <a name="BKMK_prereqs_mobiledevices"></a> モバイル デバイス クライアントの前提条件  

Configuration Manager クライアントをモバイル デバイスにインストールして登録する場合は、以下の情報を使用して前提条件を判断します。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  

-   モバイル デバイスに必要な証明書の展開と管理を行う Microsoft 企業証明機関 (CA) と証明書テンプレート。  

     発行する証明機関は、登録プロセス中モバイル デバイスのユーザーからの証明書要求を自動的に承認する必要があります。  

     証明書の要件の詳細については、[証明書プロファイルのセキュリティとプライバシー](/sccm/protect/plan-design/security-and-privacy-for-certificate-profiles)に関するページを参照してください。  

-   モバイル デバイスを登録できるユーザーを含んだセキュリティ グループ。  

     このセキュリティ グループは、モバイル デバイスの登録中に使用される証明書テンプレートを構成するのに使用されます。  

-   省略可能ですがお勧めします: **ConfigMgrEnroll** という名前の DNS エイリアス (CNAME レコード)。 登録プロキシ ポイントのサーバー名用にこのエイリアスを構成します。  

     この DNS エイリアスは登録サービスの自動検出をサポートするために必要になります。 この DNS レコードを構成しない場合は、ユーザーが登録プロセスの一環として登録プロキシ ポイントの名前を手動で指定する必要があります。  

-   登録ポイントと登録プロキシ ポイント サイト システムの役割を実行するコンピューター用サイト システムの役割の依存関係。  

     詳細については、[サイト システム サーバーでサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)に関するページを参照してください。  


### <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  

詳細については、[クライアントのサイト システムの役割の決定](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients)に関するページを参照してください。  

-   HTTPS クライアント接続用に構成され、モバイル デバイスが有効な管理ポイント  

     管理ポイントは、Configuration Manager クライアントをモバイル デバイスをインストールするのに常に必要となります。 HTTPS の構成要求とモバイル デバイス用の有効化に加えて、管理ポイントはインターネット FQDN で構成され、インターネットからのクライアント接続を許可する必要があります。  

-   登録ポイントおよび登録プロキシ ポイント  

     登録プロキシ ポイントはモバイル デバイスからの登録要求を管理し、登録ポイントは登録プロセスを完了します。 登録ポイントはサイト サーバーと同じ Active Directory フォレストにある必要がありますが、登録プロキシ ポイントは別のフォレストに設けることができます。  

-   モバイル デバイス登録用のクライアント設定  

     ユーザーがモバイル デバイスを登録し、少なくとも 1 つの登録プロファイルを構成できるようにクライアント設定を構成します。  

-   レポート サービス ポイント  

     レポート サービス ポイントはオプションですが、モバイル デバイスの登録やクライアント管理に関するレポートを表示できる、推奨されるサイト システムの役割です。  

     詳細については、[Configuration Manager のレポート](/sccm/core/servers/manage/reporting)に関する記事を参照してください。  

-   モバイル デバイス用に登録を構成するには、次のセキュリティのアクセス許可が必要です。  

    -   登録サイト システムの役割を追加、変更、削除する: **サイト** オブジェクトの **変更** のアクセス許可。  

    -   登録用にクライアント設定を構成する: 既定のクライアント設定には **サイト** オブジェクトの **変更** のアクセス許可、カスタムのクライアント設定には **クライアント エージェント**  のアクセス許可が必要です。  

     **[完全な権限を持つ管理者]** の既定のセキュリティ ロールには、登録サイト システムの役割を構成するのに必要なアクセス許可が含まれています。  

     登録されたモバイル デバイスを管理するには、次のセキュリティのアクセス許可が必要です。  

    -   モバイル デバイスをワイプまたはインベントリから削除する: **コレクション** オブジェクトの **リソースの削除**  

    -   [ワイプ] または [インベントリから削除] コマンドを取り消す: **コレクション** オブジェクトの **リソースの削除**  

    -   モバイル デバイスを許可またはブロックする: **コレクション** オブジェクトの **リソースの変更**  

    -   モバイル デバイスでリモート ロック、またはパスコードのリセットを実行する: **コレクション** オブジェクトのリソースの **変更** 。  

     **[オペレーションの管理者]** の既定のセキュリティ ロールには、モバイル デバイスを管理するのに必要なアクセス許可が含まれています。  

     セキュリティのアクセス許可を構成する方法の詳細については、[ロール ベース管理の基礎](/sccm/core/understand/fundamentals-of-role-based-administration)と、[ロール ベース管理の構成](/sccm/core/servers/deploy/configure/configure-role-based-administration)に関するページを参照してください。  


### <a name="firewall-requirements"></a>ファイアウォールの要件  

ルーターやファイアウォール、および該当する場合は Windows ファイアウォールなど、介在するネットワーク デバイスは、モバイル デバイスの登録に関連付けられたトラフィックを許可する必要があります。  

-   モバイル デバイスと登録プロキシ ポイント間では: HTTPS (既定では、TCP 443)  

-   登録プロキシ ポイントと登録ポイント間では: HTTPS (既定では、TCP 443)  


プロキシ Web サーバーを使用する場合は、SSL トンネリング用に構成する必要があります。 モバイル デバイスでは SSL ブリッジングはサポートされません。  
