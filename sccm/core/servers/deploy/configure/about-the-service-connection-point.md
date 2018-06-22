---
title: '[サービス接続ポイント]'
titleSuffix: Configuration Manager
description: この Configuration Manager サイト システムの役割について学習し、その使用範囲を理解し計画します。
ms.date: 1/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7328d7053d1fb06487e255fe4a24d6955c99c4b0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338052"
---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>System Center Configuration Manager のサービス接続ポイントについて

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager サービス接続ポイントは、階層のいくつかの重要な機能を提供するサイト システムの役割です。 サービス接続ポイントを設定する前に、その使用範囲を理解し、計画を立ててください。  使用計画によっては、このサイト システムの役割の設定方法に影響がある可能性があります。  

-   **Microsoft Intune を使用してモバイル デバイスを管理する** – この役割は、Configuration Manager の前のバージョンによって使用される Windows Intune コネクタを置き換え、Intune のサブスクリプションの詳細で構成することができます。 「[System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM)](../../../../mdm/understand/hybrid-mobile-device-management.md)」をご覧ください。  

-   **オンプレミス MDM を使用してモバイル デバイスを管理する** – この役割は、インターネットに接続しない管理対象オンプレミス デバイスのサポートを提供します。 「[System Center Configuration Manager でオンプレミス インフラストラクチャを使用したモバイル デバイスの管理](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」をご覧ください。  

-   **Configuration Manager インフラストラクチャからの使用データのアップロード** – アップロードする詳細のレベルと量を制御することができます。 アップロードされるデータは、次の点で役立ちます。  

    -   問題の早期識別とトラブルシューティング  

    -   Microsoft の製品やサービスの向上  

    -   使用する Configuration Manager のバージョンに適用する Configuration Manager の更新プログラムの識別  

  各レベルで収集されるデータ、および役割をインストールした後で収集レベルを変更する方法については、「[診断結果と使用状況データ](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)」を参照してください。 その後、使う Configuration Manager のバージョンに対応するリンクをご覧ください。  

  詳細については、「[使用状況データのレベルと設定](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage)」を参照してください。  

-   **Configuration Manager インフラストラクチャに適用される更新プログラムのダウンロード** – アップロードする使用データに基づいて、インフラストラクチャに関連する更新プログラムのみを入手することができます。  

- **各階層は、この役割の単一インスタンスをサポートします。**  

 -   このサイト システムの役割は、階層の最上位層サイト (中央管理サイトまたはスタンドアロン プライマリ サイト) のみにインストールできます。  

  -   スタンドアロン プライマリ サイトをより大きな階層に拡張する場合、この役割をアンインストールする必要があり、その後、中央管理サイトにインストールすることができます。  


##  <a name="bkmk_modes"></a> 操作モード  
 サービス接続ポイントは、操作の 2 つのモードをサポートしています。  

-   **オンライン モード**では、サービス接続ポイントは 24 時間ごとに更新プログラムを自動的にチェックします。 そして、現在のインフラストラクチャおよび製品バージョンで使用可能な新しい更新プログラムをダウンロードし、Configuration Manager コンソールで使用できるようにします。  

-   **オフライン モード**では、サービス接続ポイントは、Microsoft クラウド サービスに接続しません。 使用可能な更新プログラムを手動でインポートするには、[System Center Configuration Manager のサービス接続ツールを使います](../../../../core/servers/manage/use-the-service-connection-tool.md)。  

サービス接続ポイントをインストールした後でオンライン モードとオフライン モードを変更する場合は、Configuration Manager SMS_Executive サービスの SMS_DMP_DOWNLOADER スレッドを再起動する必要があります。これにより、この変更が有効になります。 Configuration Manager の Service Manager を使って、SMS_Executive サービスの SMS_DMP_DOWNLOADER スレッドのみを再起動できます。 また、Configuration Manager の SMS_Executive サービスを再起動することもでき、それによりほとんどのサイト コンポーネントが再起動されます。 または、サイトのバックアップなどのスケジュールされたタスクを待つこともできます。そうすると、SMS_Executive サービスが自動的に停止されて後で再起動されます。  

Configuration Manager サービス マネージャーを使用するには、コンソールで **[監視]** > **[システムのステータス]** > **[コンポーネントのステータス]** に移動して **[開始]** を選択してから、**[Configuration Manager サービス マネージャー]** を選択します。 サービス マネージャー:  

-   ナビゲーション ウィンドウで、サイトを展開してから **[コンポーネント]** を展開し、再起動するコンポーネントを選択します。  

-   詳細ウィンドウで、コンポーネントを右クリックして、**[クエリ]** を選択します。  

-   コンポーネントのステータスを確認したら、コンポーネントを再び右クリックして、**[停止]** を選択します。  

-   コンポーネントを再び**クエリ**して停止していることを確認します。 コンポーネントをもう一度右クリックし、**[開始]** を選びます。  

> [!IMPORTANT]  
>  サービス接続ポイントに Microsoft Intune サブスクリプションを追加するプロセスで、サイト システムの役割が自動的にオンラインに設定されます。 サービス接続ポイントは Intune サブスクリプションで設定されている場合にオフライン モードをサポートしません。  

**サイト サーバーからリモートにあるコンピューターに役割をインストールする場合:**  

-   サイト サーバーのコンピューター アカウントは、リモート サービス接続をホストするコンピューターのローカル管理者である必要があります。

-   役割をホストするサイト システム サーバーをサイト システムのインストール アカウントで設定する必要があります。  

-   サイト サーバー上の配布マネージャーは、サイト システムのインストール アカウントを使って、サービス接続ポイントから更新プログラムを転送します。

##  <a name="bkmk_urls"></a> インターネット アクセス要件  
操作を有効にするには、サービス接続ポイントをホストするコンピューター、およびそのコンピューターとインターネットの間のファイアウォールが、HTTPS の場合は送信ポート **TCP 443**、HTTP の場合は送信ポート **TCP 80** を通して、次のインターネット上の場所に通信が届くようにする必要があります。 サービス接続ポイントから、これらの場所を利用する際は、Web プロキシ (認証あり、または認証なし) を使用することもできます。  Web プロキシ アカウントを構成する必要がある場合は、「[System Center Configuration Manager でのプロキシ サーバーのサポート](/sccm/core/plan-design/network/proxy-server-support)」を参照してください。

**更新プログラムとサービス**  

-   *.akamaiedge.net  

-   *.akamaitechnologies.com 

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

-   download.windowsupdate.com

-   sccmconnected-a01.cloudapp.net  

**Microsoft Intune**  

-   *manage.microsoft.com  
-   https://bspmts.mp.microsoft.com/V
-   https://login.microsoftonline.com/{TenantID}


**Windows 10 サービス**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  

## <a name="install-the-service-connection-point"></a>サービス接続ポイントをインストールする
**[セットアップ]** を実行して階層の最上位サイトをインストールする場合、サービス接続ポイントをインストールするオプションがあります。

[セットアップ] を実行した後、またはサイト システムの役割を再インストールする場合は、**サイト システムの役割の追加**ウィザード、または**サイト システム サーバーの作成**ウィザードを使用して、サーバー上のサイト システムを階層の最上位サイト (中央管理サイトまたはスタンドアロン プライマリ サイト) にインストールします。 どちらのウィザードも、コンソールの **[ホーム]** タブの、**[管理]** > **[サイトの構成]** > **[サーバーとサイト システムの役割]** にあります。

## <a name="log-files-used-by-the-service-connection-point"></a>サービス接続ポイントにより使用されるログ ファイル
Microsoft へのアップロードに関する情報については、サービス接続ポイントを実行するコンピューターの **Dmpuploader.log** をご覧ください。  更新プログラムのダウンロード進捗状況など、ダウンロードについては、**Dmpdownloader.log** をご覧ください。 サービス接続ポイント関連のログの完全な一覧については、Configuration Manager ログ ファイルの記事の「[サービス接続ポイント](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog)」を参照してください。

更新プログラムをダウンロードするプロセスと更新プログラムを他のサイトに複製するプロセスの流れや重要なログ エントリについては、次のフローチャートを使用して理解に役立てることもできます。
 - [フローチャート - 更新プログラムのダウンロード](/sccm/core/servers/manage/download-updates-flowchart)
 - [フローチャート - レプリケーションの更新](/sccm/core/servers/manage/update-replication-flowchart)
