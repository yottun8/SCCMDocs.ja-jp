---
title: Windows クライアント展開の前提条件
titleSuffix: Configuration Manager
description: Windows コンピューターに Configuration Manager クライアントを展開するための前提条件について説明します。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf929e605a7d44ac2f29226177d3ab962eb8fba0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-system-center-configuration-manager"></a>System Center Configuration Manager で Windows コンピューターにクライアントを展開するための前提条件

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager クライアントを環境で展開するには、次の外部の依存関係、および製品内の依存関係が必要となります。 それぞれのクライアント展開方法に固有の依存関係もあり、それを満たさないとクライアント インストールを正常に実行できません。  

  また、「[サポートされている構成](../../../core/plan-design/configs/supported-configurations.md)」を参照し、デバイスが Configuration Manager クライアントのハードウェアおよび OS の最小要件を満たしていることを確認してください。  

 Linux および UNIX 用の Configuration Manager クライアントの前提条件については、[Linux および UNIX コンピューターへのクライアント展開の計画](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)に関するページを参照してください。  

> [!NOTE]  
>  この記事に示されているソフトウェア バージョンの番号は、必要な最小のバージョン番号のみを示します。  



##  <a name="BKMK_prereqs_computers"></a> コンピューター クライアントの前提条件  
 コンピューターに Configuration Manager クライアントをいつインストールするかの前提条件を判断するには次の情報に従います。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  

|||  
|-|-|  
|Windows インストーラー バージョン 3.1.4000.2435|Windows インストーラーの更新 (.msp) ファイルを、パッケージおよびソフトウェアの更新に使用できるようにするために必要となります。|  
|[KB2552033](https://go.microsoft.com/fwlink/p/?LinkId=240048)|クライアント プッシュ インストールが有効な場合は、Windows Server 2008 R2 を実行するサイト サーバーに修正プログラムをインストールします。|  
|Microsoft バックグラウンド インテリジェント転送サービス (BITS) バージョン 2.5|クライアント コンピューターと Configuration Manager サイト システムの間でデータが転送されるときのネットワーク負荷を軽減するために必要となります。 BITS は、クライアント インストールで自動的にダウンロードされません。 BITS がコンピューターにインストールされると通常、インストールを完了するために再起動が必要となります。<br /><br /> ほとんどのオペレーティング システムには BITS が含まれいますが、含まれていない場合は (たとえば、Windows Server 2003 R2 SP2)、Configuration Manager クライアントをインストールする前に BITS をインストールする必要があります。|  
|Microsoft タスク スケジューラ|クライアントのインストールを完了するために、クライアントでこのサービスを有効にします。|  

### <a name="bkmk_ExternalDependencies"></a> Configuration Manager の外部の依存関係、およびインストール中の自動ダウンロードされる外部の依存関係  
 Configuration Manager クライアントには潜在的な外部の依存関係があります。 これらの依存関係は、クライアント コンピューターのオペレーティング システムやインストールされたソフトウェアによります。  

 クライアントのインストールの完了にこの依存関係が必要である場合は、クライアント ソフトウェアと共に自動的にインストールされます。  

|||  
|-|-|  
|Windows Update エージェント バージョン 7.0.6000.363|更新プログラムの検出および展開のサポートに Windows で必要となります。|  
|Microsoft Core XML Services (MSXML) バージョン 6.20.5002 以降|Windows で XML ドキュメントを処理できるようにするために必要となります。|  
|Microsoft Remote Differential Compression (RDC)|ネットワークのデータ転送を最適化するために必要となります。|  
|Microsoft Visual C++ 2013 再頒布可能パッケージ バージョン 12.0.21005.1|クライアントのオペレーションをサポートするために必要となります。 クライアント コンピューターにこの更新プログラムがインストールされていると、インストールを完了するために再起動が必要になる可能性があります。|  
|Microsoft Visual C++ 2005 再頒布可能バージョン 8.0.50727.42|1606 以前のバージョンの場合、Microsoft SQL Server Compact オペレーションをサポートするために必要です。|  
|Windows Imaging APIs 6.0.6001.18000|Configuration Manager が Windows イメージ (.wim) ファイルを管理するのを許可するために必要となります。|  
|Microsoft Policy Platform 1.2.3514.0|クライアントがコンプライアンス設定を評価するのを許可するために必要となります。|  
|Microsoft Silverlight 5.1.41212.0|アプリケーション カタログ ウェブサイトのユーザー エクスペリエンスをサポートするために必要となります。 Configuration Manager 1802 以降では、Silverlight は自動的にインストールされなくなりました。 アプリケーション カタログの主な機能はソフトウェア センターに含まれるようになりました。 アプリケーション カタログの Web サイトは、2018 年 6 月 1 日以降にリリースされる最初の更新プログラムでサポートが終了します。<!--1356195-->|  
|Microsoft .NET Framework バージョン 4.5.2|クライアントのオペレーションをサポートするために必要となります。 Microsoft .NET Framework バージョン 4.5 以降がインストールされていない場合は、クライアント コンピューターに自動的にインストールされます。 詳細については、「[Microsoft .NET Framework バージョン 4.5.2 に関する追加情報](#dotNet)」を参照してください。|  
|Microsoft SQL Server Compact 3.5 SP2 コンポーネント|クライアント オペレーションに関連した情報を保存するために必要となります。|  
|Microsoft Windows Imaging Component|Microsoft .NET Framework 4.0 で、64 ビット コンピューター向け Windows Server 2003 または Windows XP SP2 に必要となります。|
|Microsoft Intune PC ソフトウェア クライアント|Intune PC ソフトウェア クライアントと Configuration Manager クライアントを同じ PC で実行することはできません。 Configuration Manager クライアントをインストールする前に、必ず、Intune クライアントを削除してください。|

####  <a name="dotNet"></a> Microsoft .NET Framework バージョン 4.5.2 に関する追加情報  

> [!NOTE]  
>  2016 年 1 月 12 日に、.NET 4.0、4.5、および 4.5.1 のサポートが期限切れになりました。 詳細については、[Microsoft .NET Framework のサポート ライフサイクル ポリシーに関する FAQ](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) を参照してください。  

 Microsoft .NET Framework バージョン 4.5.2 のインストールの完了に再起動が必要な場合があります。 システム トレイに **[再起動が必要]** 通知が表示されます。 クライアント コンピューターの再起動が必要な一般的なシナリオは、次のとおりです。  

-   .NET アプリケーションまたはサービスがコンピューター上で実行されている。  

-   .NET インストールに必要な 1 つ以上 のソフトウェア更新プログラムが不足している。  

-   コンピューターで、.NET Framework のソフトウェア更新プログラムの以前のインストールからの再起動が保留されている。  

 .NET Framework 4.5.2 をインストールした後に、追加の更新プログラムをインストールすると、追加のコンピューターの再起動が必要になる場合がある。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  
 詳細については、[クライアントのサイト システムの役割の決定](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)に関するページを参照してください。  

|||  
|-|-|  
|管理ポイント|Configuration Manager クライアントの展開に管理ポイントは必要ありませんが、クライアント コンピューターと Configuration Manager サーバーの間で情報を転送するには管理ポイントが必要です。 管理ポイントがないと、クライアント コンピューターを管理できません。|  
|配布ポイント|配布ポイントはオプションですが、クライアント展開において推奨されるサイト システムの役割です。 すべての配布ポイントはクライアント ソース ファイルをホストします。それによりコンピューターは、最も近い配布ポイントからクライアント展開中にクライアント ソース ファイルをダウンロードできます。 サイトに配布ポイントがない場合は、クライアントは管理ポイントからクライアント ソース ファイルをダウンロードします。|  
|フォールバック ステータス ポイント|フォールバック ステータス ポイントはオプションですが、クライアント展開において推奨されるサイト システムの役割です。 フォールバック ステータス ポイントにより、Configuration Manager サイトのコンピューターは、管理ポイントとやり取りできないときに状態メッセージを送信できます。|  
|レポート サービス ポイント|レポート サービス ポイントはオプションですが、クライアントの展開や管理に関するレポートを表示できる、推奨されるサイト システムの役割です。 詳細については、「[System Center Configuration Manager のレポート](../../../core/servers/manage/reporting.md)」を参照してください。|  

### <a name="installation-method-dependencies"></a>インストール方法の依存関係  
 次の前提条件は、クライアント インストールのさまざまな方法に固有です。  

#### <a name="client-push-installation"></a>クライアント プッシュ インストール  

   -   クライアント プッシュ インストールのアカウントは、コンピューターを接続してクライアントをインストールするのに使用され、 **[クライアント プッシュ インストールのプロパティ]** ダイアログ ボックスの **[アカウント]** タブで指定されます。 アカウントは、展開先のコンピューターでローカルの管理者グループのメンバーである必要があります。  

         クライアント プッシュ インストール アカウントを指定しない場合は、サイト サーバー コンピューター アカウントが使用されます。  

   -   クライアントをインストールしているコンピューターは、少なくとも 1 つの Configuration Manager 探索方法で見つかっている必要があります。  

   -   コンピューターに ADMIN$ 共有が必要です。  

   -   検出されたリソースに Configuration Manager クライアントを自動的にプッシュする場合は、**[クライアント プッシュ インストールのプロパティ]** ダイアログ ボックスで **[割り当てられたリソースへのクライアント プッシュ インストールを有効にする]** を選択する必要があります。  

   -   クライアント コンピューターは、配布ポイントまたは管理ポイントにアクセスし、サポート ファイルをダウンロードできる必要があります。  


クライアント プッシュを使用して、Configuration Manager クライアントをインストールするには次のセキュリティのアクセス許可が必要です。  

   -   クライアント プッシュ インストール アカウントを構成する: **サイト** オブジェクトの **変更** と読み取りアクセス許可。  

   -   コレクション、デバイス、クエリにクライアントをインストールするためのクライアント プッシュの使用: コレクション オブジェクトの **リソースの変更** と **読み取り** アクセス許可。  


**[インフラストラクチャの管理者]** のセキュリティの役割には、クライアント プッシュ インストールを管理するのに必要な許可が含まれています。  


#### <a name="software-update-point-based-installation"></a>ソフトウェアの更新ポイント経由のインストール  

   -   Active Directory スキーマを拡張していない場合、または別のフォレストからのクライアントをインストールする場合は、グループ ポリシーを使用して、CCMSetup.exe のインストール プロパティをコンピューターのレジストリで準備する必要があります。 詳細については、「[クライアント インストールのプロパティの準備方法 (グループ ポリシーおよびソフトウェア更新ベースのクライアント インストール)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision)」を参照してください。  

   -   Configuration Manager クライアントをソフトウェアの更新ポイントに発行する必要があります。  

   -   クライアント コンピューターは、サポート ファイルをダウンロードするために配布ポイントまたは管理ポイントにアクセスできる必要があります。  


Configuration Manager ソフトウェア更新プログラムの管理に必要なセキュリティのアクセス許可については、[ソフトウェア更新プログラムの前提条件](../../../sum/plan-design/prerequisites-for-software-updates.md)に関するページを参照してください。  


#### <a name="group-policy-based-installation"></a>グループ ポリシーを使用したインストール  

   -   Active Directory スキーマを拡張していない場合、または別のフォレストからのクライアントをインストールする場合は、グループ ポリシーを使用して、CCMSetup.exe のインストール プロパティをコンピューターのレジストリで準備する必要があります。 詳細については、「[クライアント インストールのプロパティの準備方法 (グループ ポリシーおよびソフトウェア更新ベースのクライアント インストール)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision)」を参照してください。  

   -   クライアント コンピューターは、サポート ファイルをダウンロードするために管理ポイントへアクセスできる必要があります。  


#### <a name="logon-script-based-installation"></a>ログオン スクリプトを使用したインストール  

クライアント コンピューターは、サポート ファイルをダウンロードするために配布ポイントまたは管理ポイントにアクセスできる必要があります。 ただし、CCMSetup.exe をコマンド ライン プロパティの **ccmsetup /source** で指定した場合を除きます。  


#### <a name="manual-installation"></a>手動インストール  

クライアント コンピューターは、サポート ファイルをダウンロードするために配布ポイントまたは管理ポイントにアクセスできる必要があります。 ただし、CCMSetup.exe をコマンド ライン プロパティの **ccmsetup /source** で指定した場合を除きます。  


#### <a name="microsoft-intune-mdm-installation"></a>Microsoft Intune MDM のインストール

 - Microsoft Intune サブスクリプションと適切なライセンスが必要です。  

 - デバイスは、インター ネット ベースでない場合でもインターネットにアクセスできる必要があります。  

 - ユース ケースに応じて、次のテクノロジのいずれか、または両方が必要になる場合もあります。  

     - Azure Active Directory  

     - クラウド管理ゲートウェイ  


#### <a name="workgroup-computer-installation"></a>ワークグループ コンピューターのインストール  

Configuration Manager サイト サーバー ドメイン内のリソースにアクセスするには、このサイト用にネットワーク アクセス アカウントを構成する必要があります。  

ネットワーク アクセス アカウントの構成方法の詳細については、[コンテンツ管理の基本的な概念](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)に関するページを参照してください。  


#### <a name="software-distribution-based-installation-for-upgrades-only"></a>ソフトウェアの配布を使用したインストール (アップグレードのみ)  

   -   Active Directory スキーマを拡張していない場合、または別のフォレストからのクライアントをインストールする場合は、グループ ポリシーを使用して、CCMSetup.exe のインストール プロパティをコンピューターのレジストリで準備する必要があります。 詳細については、「[クライアント インストールのプロパティの準備方法 (グループ ポリシーおよびソフトウェア更新ベースのクライアント インストール)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision)」を参照してください。  

   -   クライアント コンピューターは、配布ポイントまたは管理ポイントにアクセスし、サポート ファイルをダウンロードできる必要があります。  


アプリケーション管理を使用して Configuration Manager クライアントをアップグレードするのに必要なセキュリティのアクセス許可については、「[アプリケーション管理に関するセキュリティとプライバシー](../../../apps/plan-design/security-and-privacy-for-application-management.md)」を参照してください。  


#### <a name="automatic-client-upgrades"></a>自動のクライアント アップグレード  

自動のクライアント アップグレードを構成するには、セキュリティの役割である **[完全な権限を持つ管理者]** のメンバーである必要があります。  


### <a name="firewall-requirements"></a>ファイアウォールの要件  

サイト システム サーバーと Configuration Manager クライアントをインストールするコンピューターとの間にファイアウォールがある場合は、[クライアントの Windows ファイアウォールとポートの設定](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md)に関するページを参照してください。  



##  <a name="BKMK_prereqs_mobiledevices"></a> モバイル デバイス クライアントの前提条件  

Configuration Manager クライアントをモバイル デバイスにインストールして登録する場合は、以下の情報を使用して前提条件を判断します。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  

-   モバイル デバイスに必要な証明書の展開と管理を行う Microsoft 企業証明機関 (CA) と証明書テンプレート。  

     発行する証明機関は、登録プロセス中モバイル デバイスのユーザーからの証明書要求を自動的に承認する必要があります。  

     証明書の要件の詳細については、[証明書プロファイルのセキュリティとプライバシー](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md)に関するページを参照してください。  

-   モバイル デバイスを登録できるユーザーを含んだセキュリティ グループ。  

     このセキュリティ グループは、モバイル デバイスの登録中に使用される証明書テンプレートを構成するのに使用されます。  

-   省略可能ですがお勧めします: **ConfigMgrEnroll** という名前の DNS エイリアス (CNAME レコード)。 登録プロキシ ポイントのサーバー名用にこのエイリアスを構成します。  

     この DNS エイリアスは登録サービスの自動検出をサポートするために必要になります。 この DNS レコードを構成しない場合は、ユーザーが登録プロセスの一環として登録プロキシ ポイントの名前を手動で指定する必要があります。  

-   登録ポイントと登録プロキシ ポイント サイト システムの役割を実行するコンピューター用サイト システムの役割の依存関係。  

     「[サイト システム サーバーでサポートされるオペレーティング システム](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)」を参照してください。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  
 詳細については、[クライアントのサイト システムの役割の決定](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)に関するページを参照してください。  

-   HTTPS クライアント接続用に構成され、モバイル デバイスが有効な管理ポイント  

     管理ポイントは、Configuration Manager クライアントをモバイル デバイスをインストールするのに常に必要となります。 HTTPS の構成要求とモバイル デバイス用の有効化に加えて、管理ポイントはインターネット FQDN で構成され、インターネットからのクライアント接続を許可する必要があります。  

-   登録ポイントおよび登録プロキシ ポイント  

     登録プロキシ ポイントはモバイル デバイスからの登録要求を管理し、登録ポイントは登録プロセスを完了します。 登録ポイントはサイト サーバーと同じ Active Directory フォレストにある必要がありますが、登録プロキシ ポイントは別のフォレストに設けることができます。  

-   モバイル デバイス登録用のクライアント設定  

     ユーザーがモバイル デバイスを登録し、少なくとも 1 つの登録プロファイルを構成できるようにクライアント設定を構成します。  

-   レポート サービス ポイント  

     レポート サービス ポイントはオプションですが、モバイル デバイスの登録やクライアント管理に関するレポートを表示できる、推奨されるサイト システムの役割です。  

     詳細については、「[System Center Configuration Manager のレポート](../../../core/servers/manage/reporting.md)」を参照してください。  

-   モバイル デバイス用に登録を構成するには、次のセキュリティのアクセス許可が必要です。  

    -   登録サイト システムの役割を追加、変更、削除する: **サイト** オブジェクトの **変更** のアクセス許可。  

    -   登録用にクライアント設定を構成する: 既定のクライアント設定には **サイト** オブジェクトの **変更** のアクセス許可、カスタムのクライアント設定には **クライアント エージェント**  のアクセス許可が必要です。  

     **[完全な権限を持つ管理者]** のセキュリティの役割には、登録サイト システムの役割を構成するのに必要な許可が含まれています。  

     登録されたモバイル デバイスを管理するには、次のセキュリティのアクセス許可が必要です。  

    -   モバイル デバイスをワイプまたはインベントリから削除する: **コレクション** オブジェクトの **リソースの削除**  

    -   [ワイプ] または [インベントリから削除] コマンドを取り消す: **コレクション** オブジェクトの **リソースの削除**  

    -   モバイル デバイスを許可またはブロックする: **コレクション** オブジェクトの **リソースの変更**  

    -   モバイル デバイスでリモート ロック、またはパスコードのリセットを実行する: **コレクション** オブジェクトのリソースの **変更** 。  

     **[オペレーションの管理者]** のセキュリティの役割には、モバイル デバイスを管理するのに必要な許可が含まれています。  

     セキュリティのアクセス許可を構成する方法の詳細については、[ロール ベース管理の基礎](../../../core/understand/fundamentals-of-role-based-administration.md)と、[ロール ベース管理の構成](../../../core/servers/deploy/configure/configure-role-based-administration.md)に関するページを参照してください。  

### <a name="firewall-requirements"></a>ファイアウォールの要件  
ルーターやファイアウォール、および該当する場合は Windows ファイアウォールなど、介在するネットワーク デバイスは、モバイル デバイスの登録に関連付けられたトラフィックを許可する必要があります。  

-   モバイル デバイスと登録プロキシ ポイント間では: HTTPS (既定では、TCP 443)  

-   登録プロキシ ポイントと登録ポイント間では: HTTPS (既定では、TCP 443)  


プロキシの Web サーバーを使用している場合は、SSL トンネリング用に構成されている必要があります。モバイル デバイスは SSL ブリッジに対応しません。  
