---
title: "クラウドベースの配布ポイントのインストール | Microsoft Docs"
description: "Microsoft Azure でクラウドベース配布ポイントの使用を開始するために必要なことについて説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: aba573b2822568236c006e7af19b421639faa8bc

---
# <a name="install-cloud-based-distribution-points-in-microsoft-azure-for-system-center-configuration-manager"></a>Microsoft Azure for System Center Configuration Manager のクラウド ベース配布ポイントのインストール

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Azure では、System Center Configuration Manager のクラウドベース配布ポイントをインストールできます。 クラウドベースの配布ポイントに関する詳細については、「[クラウドベースの配布ポイントの使用](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)」を参照してください。

 インストールを開始する前に、必要な証明書ファイルがあることを確認します。  

-   .cer ファイルと .pfx ファイルにエクスポートされた Microsoft Azure 管理証明書  

-   .pfx ファイルにエクスポートされた、Configuration Manager のクラウドベースの配布ポイントのサーバー証明書  

    > [!TIP]
    >   これらの証明書の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../../../core/plan-design/network/pki-certificate-requirements.md)」トピックのクラウドベースの配布ポイントの部分を参照してください。 クラウドベースの配布ポイントのサービス証明書を展開する例については、「[Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)」 (System Center Configuration Manager: Windows Server 2008 証明機関の PKI 証明書の展開手順例) トピックの「*クラウドベースの配布ポイント用のサービス証明書の展開*」を参照してください。  


 クラウドベースの配布ポイントをインストールすると、Microsoft Azure によって自動的にサービスの GUID が生成され、 **cloudapp.net**の DNS サフィックスに追加されます。 この GUID を使用して、Configuration Manager のクラウドベースの配布ポイントのサービス証明書に定義しているサービス名を自動的に生成された GUID にマップするように、DNS エイリアス (CNAME レコード) を使って DNS を構成する必要があります。  

 プロキシ Web サーバーを使用する場合は、配布ポイントをホストするクラウド サービスとの通信を有効にするように、プロキシ設定を構成することが必要になる可能性があります。  

##  <a name="a-namebkmkconfigwindowsazureandinstalldpa-configure-microsoft-azure-and-install-cloud-based-distribution-points"></a><a name="BKMK_ConfigWindowsAzureandInstallDP"></a> Microsoft Azure の構成とクラウドベースの配布ポイントのインストール  
 配布ポイントをサポートするように Microsoft Azure を構成してから、Configuration Manager でクラウドベースの配布ポイントをインストールするには、次の手順に従います。  

#### <a name="to-configure-a-cloud-service-in-microsoft-azure-for-a-distribution-point"></a>配布ポイント用に Microsoft Azure にクラウド サービスを構成するには  

1.  Web ブラウザーを開いて Microsoft Azure 管理ポータル (https://manage.windowsazure.com) に移動し、Microsoft Azure アカウントにアクセスします。  

2.  **[ホステッド サービス、ストレージ アカウント、CDN]** をクリックしてから、**[管理証明書]** を選択します。  

3.  サブスクリプションを右クリックしてから、[証明書の追加] を選択します。 ****  

4.  [ **証明書ファイル**] に、このクラウド サービスに使用するためにエクスポートした Microsoft Azure 管理証明書が含まれる .cer ファイルを指定してから、[ **OK**] をクリックします。  

 管理証明書が Microsoft Azure に読み込まれて、クラウドベースの配布ポイントをインストールできるようになります。  

#### <a name="to-install-a-cloud-based-distribution-point-for-configuration-manager"></a>Configuration Manager 用にクラウドベースの配布ポイントをインストールするには  

1.  管理証明書を使って Microsoft Azure にクラウド サービスを構成する、前述の手順を完了します。  

2.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]** を展開して **[クラウド配布ポイント]** を選択してから、**[ホーム]** タブで **[クラウド配布ポイントの作成]** をクリックします。  

3.  クラウドの配布ポイントの作成ウィザードの [全般] タブで、次のように構成します。 ****  

    -   Microsoft Azure アカウントの [ **サブスクリプション ID** ] を指定します。  

        > [!TIP]  
        >  Microsoft Azure のサブスクリプション ID は、Microsoft Azure 管理ポータルで確認できます。  

    -   [管理証明書 ****] を指定します。 [ **参照** ] をクリックして、エクスポートされた Microsoft Azure 管理証明書が含まれている .pfx ファイルを指定してから、証明書のパスワードを入力します。 必要に応じて、Microsoft Azure SDK 1.7 のバージョン 1 の .publishsettings ファイルを指定できます  

4.  **[次へ]** をクリックします。すると、Configuration Manager が Microsoft Azure に接続して管理証明書を検証します。  

5.  [ **設定** ] ページで、次の構成を完了してから [ **次へ**] をクリックします。  

    -   [ **地域**] で、この配布ポイントをホストするクラウド サービスを作成する、Microsoft Azure の地域を選択します。  

    -   **[証明書ファイル]** に、エクスポートされた Configuration Manager クラウドベースの配布ポイント サービス証明書を含む .pfx ファイルを指定し、パスワードを入力します。  

        > [!NOTE]  
        >  [サービスの FQDN] ボックスには、証明書のサブジェクト名から自動的に入力されます。ほとんどの場合、編集する必要はありません。 **** テスト環境でワイルドカード証明書を使用しており、同じ DNS サフィックスを持つ複数のコンピューターが証明書を使用できるようにホスト名を指定していない場合は、例外となります。 このシナリオでは、証明書のサブジェクトには **CN=\*.contoso.com** のような値が含まれており、Configuration Manager によって、正しい FQDN を指定する必要があることを示すメッセージが表示されます。 [OK] をクリックしてメッセージを閉じてから、DNS サフィックスの前に特定の名前を入力して、完全な FQDN を指定します。 **** たとえば、 **clouddp1** を追加して、 **clouddp1.contoso.com**のサービスの完全な FQDN を指定します。 サービスの FQDN は、ドメインの中で固有である必要があり、ドメインに参加している他のデバイスと同じ FQDN は使用できません。  
        >   
        >  ワイルドカード証明書は、テスト環境でのみサポートされています。  

6.  **[アラート]** ページで、記憶域クォータ、転送クォータを構成し、Configuration Manage にアラートを生成させるそれぞれのクォータの使用率を指定して、**[次へ]** をクリックします。  

7.  ウィザードを完了します。  

 クラウドベースの配布ポイントの新しいホステッド サービスが作成されます。 ウィザードを閉じたら、Configuration Manage コンソールを使用して、またはプライマリ サイト サーバーの **CloudMgr.log** ファイルを監視して、クラウドベースの配布ポイントのインストールの進行状況を監視できます。 また、Microsoft Azure 管理ポータルでクラウド サービスのプロビジョニングを監視することもできます。  

> [!NOTE]  
>  Microsoft Azure に新しい配布ポイントをプロビジョニングするのに最大 30 分かかる可能性があります。 ストレージ アカウントがプロビジョニングされるまで、**CloudMgr.log** ファイルに次のメッセージが繰り返し出力されます。**コンテナーが存在するかどうかのチェックを待機しています。10 秒後にもう一度確認します**。 その後、サービスが作成されて構成されます。  

 次の方法を使用すると、クラウドベースの配布ポイントのインストールが完了したことを確認できます。  

-   Microsoft Azure 管理ポータルに、クラウドベースの配布ポイントの [ **展開** ] のステータスが **準備完了**として表示されます。  

-   **[管理]** ワークスペースで、Configuration Manager コンソールの **[階層の構成]**、**[クラウド]** ノードに、クラウドベースの配布ポイントのステータスが**準備完了**として表示されます。  

-   Configuration Manager に、SMS_CLOUD_SERVICES_MANAGER コンポーネントのステータス メッセージ ID **9409** が表示されます。  

##  <a name="a-namebkmkconfigdnsforclouddpsa-configure-name-resolution-for-cloud-based-distribution-points"></a><a name="BKMK_ConfigDNSforCloudDPs"></a> クラウドベースの配布ポイントの名前解決の構成  
 クライアントは、クラウドベースの配布ポイントにクライアントがアクセスするためには、クラウドベースの配布ポイントの名前を Microsoft Azure で管理される IP アドレスに解決できる必要があります。 クライアントでは、これを 2 段階で行います。  

1.  クライアントは、Configuration Manager のクラウドベースの配布ポイントのサービス証明書に指定されているサービス名を Microsoft Azure サービスの FQDN にマップします。 この FQDN には、 **cloudapp.net**の GUID と DNS サフィックスが含まれています。 GUID は、クラウドベースの配布ポイントがインストールされると自動的に生成されます。 Microsoft Azure 管理ポータルで完全な FQDN を確認するには、クラウド サービスのダッシュボードにある [ **サイトの URL** ] を参照します。 サイトの URL の例として、 **http://d1594d4527614a09b934d470.cloudapp.net**があります。  

2.  クライアントは、Microsoft Azure サービスの FQDN を Microsoft Azure によって割り当てられる IP アドレスに解決します。 この IP アドレスも、Microsoft Azure ポータルのクラウド サービスのダッシュボードで確認できます。名前は、[ **公開仮想 IP アドレス (VIP)**] です。  

Configuration Manager のクラウドベースの配布ポイントのサービス証明書に指定されているサービス名 (たとえば **clouddp1.contoso.com**) を Microsoft Azure サービスの FQDN (たとえば **d1594d4527614a09b934d470.cloudapp.net**) にマップするためには、インターネット上の DNS サーバーに DNS エイリアス (CNAME レコード) が構成されている必要があります。 これにより、クライアントでは、インターネット上の DNS サーバーを使用して、Microsoft Azure サービスの FQDN を IP アドレスに解決できます。  

##  <a name="a-namebkmkconfigproxyforclouda-configure-proxy-settings-for-primary-sites-that-manage-cloud-services"></a><a name="BKMK_ConfigProxyforCloud"></a> クラウド サービスを管理するプライマリ サイトのプロキシ設定の構成  
 Configuration Manager でクラウド サービスを使用するときに、クラウドベースの配布ポイントを管理するプライマリ サイトが、プライマリ サイト コンピューターの **System** アカウントを使用して Microsoft Azure 管理ポータルに接続できる必要があります。 この接続は、プライマリ サイト サーバー コンピューターの既定の Web ブラウザーを使用して行われます。  

 クラウドベースの配布ポイントを管理するプライマリ サイト サーバーで、プライマリ サイトがインターネットと Microsoft Azure にアクセスできるように、プロキシ設定を構成することが必要になる場合があります。  

 Configuration Manager コンソールでプライマリ サイト サーバーのプロキシ設定を構成するには、次の手順に従います。  

> [!TIP]  
>  プライマリ サイト サーバーに新しいサイト システムの役割をインストールするときに、 **サイト システムの役割の追加ウィザード**を使用してプロキシ サーバーを構成することもできます。  

#### <a name="to-configure-proxy-settings-for-the-primary-site-server"></a>プライマリ サイト サーバーのプロキシ設定を構成するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [ **管理** ] ワークスペースで、[ **サイトの構成**] を展開し、[ **サーバーとサイト システムの役割**] をクリックしてから、クラウドベースの配布ポイントを管理するプライマリ サーバーを選択します。  

3.  詳細ウィンドウで、[ **サイト システム**] を右クリックし、[ **プロパティ**] をクリックします。  

4.  **[サイト システムのプロパティ]** で **[プロキシ]** タブを選択し、そのプライマリ サイト サーバーのプロキシ設定を構成します。  

5.  [OK **** ] をクリックして新しいプロキシ サーバー構成を保存します。  



<!--HONumber=Dec16_HO3-->


