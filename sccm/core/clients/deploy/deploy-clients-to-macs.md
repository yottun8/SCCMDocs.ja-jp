---
title: "Mac クライアントの展開 | System Center Configuration Manager"
description: "System Center Configuration Manager でクライアントを Mac コンピューターに展開する方法を説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: eae9e76085a95cb09fe01a32fd4b57294bc1cc20


---
# <a name="how-to-deploy-clients-to-macs-in-system-center-configuration-manager"></a>How to deploy clients to Macs in System Center Configuration Manager

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager で Mac コンピューターにクライアントをインストールして管理するには、公開キー基盤 (PKI) 証明書が必要です。 Configuration Manager では、Microsoft 証明書サービスを使用して、エンタープライズ証明機関 (CA) と、Configuration Manager 登録ポイントおよび登録プロキシ ポイント サイト システムの役割に、ユーザー クライアント証明書を要求してインストールできます。 または、証明書が Configuration Manager の要件を満たしている場合、Configuration Manager とは独立して、コンピューター証明書を要求してインストールできます。 PKI 証明書は、相互認証と暗号化データ転送を使用して、Mac コンピューターと Configuration Manager サイト間の通信を保護します。  

> [!IMPORTANT]  
>  Configuration Manager の Mac クライアントは、常に証明書失効チェックを実行します。Windows で実行される構成マネージャー クライアントとは異なり、この証明書失効リスト (CRL) チェック機能を無効にすることはできません。  
>   
>  Mac クライアントで、CRL の場所を特定できないことが原因でサーバー証明書の証明書失効ステータスを確認できない場合、クライアントは、管理ポイントや配布ポイントなどの Configuration Manager サイト システムに正常に接続できなくなります。 特に、Mac クライアントが発行側の証明機関とは別のフォレストにある場合、CRL の設計を確認して、サイト システム サーバーに接続するために、Mac クライアントが CRL 配布ポイント (CDP) の場所を特定し、接続できるようにしてください。  

 Mac コンピューターに構成マネージャー クライアントをインストールする前に、クライアント証明書をインストールする方法を決定します。  

-   CMEnroll ツールを使用して Configuration Manager 登録を使用し、このトピックの次のセクションの手順に従う。 登録プロセスでは自動証明書更新がサポートされていないため、インストールされている証明書が期限切れになる前に、Mac コンピューターを再登録する必要があります。  

-   Configuration Manager とは独立した証明書の要求およびインストール方法を使用する。 このインストール方法については、このトピックの「 [Use a certificate request and installation method that is independent from Configuration Manager](#BKMK_ManualCertifcateInstallation) 」セクションを参照してください。  

> [!NOTE]  
>  Mac クライアントの証明書の要件と、Mac コンピューターのサポートに必要なその他の PKI 証明書の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../../core/plan-design/network/pki-certificate-requirements.md)」をご覧ください。  

 Mac クライアントは、クライアントを管理する Configuration Manager サイトに自動的に割り当てられます。 Mac クライアントは、通信がイントラネットに制限されている場合でも、インターネット専用クライアントとしてインストールされます。 割り当てられているサイトのサイト システムの役割 (管理ポイントおよび配布ポイント) がインターネットからのクライアント接続を許可するように構成されている場合に、それらのサイト システムと通信します。 Mac コンピューターは、割り当てられたサイト以外のサイト システムの役割と通信しません。  

> [!IMPORTANT]  
>  Configuration Manager の Mac クライアントを使用して、データベース レプリカを使用するように構成されている管理ポイントに接続することはできません。 データベース レプリカについては、「[System Center Configuration Manager の管理ポイントのデータベース レプリカ](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)」をご覧ください。  

 以降のセクションの手順に従って、Configuration Manager 用に Mac コンピューターをインストール、構成、および管理します。  

-   [Mac 用のクライアントのインストールと構成の手順](#InstallSteps)  

-   [Uninstalling the Mac client](#uninstallMacClient)  

-   [Renewing the Mac client certificate](#BKMK_Renew)  

-   [Use a certificate request and installation method that is independent from Configuration Manager](#BKMK_ManualCertifcateInstallation)  

##  <a name="a-nameinstallstepsa-steps-to-install-and-configure-the-client-for-macs"></a><a name="InstallSteps"></a> Mac 用のクライアントのインストールと構成の手順  

> [!IMPORTANT]  
>  これらの手順を実行する前に、Mac コンピューターが前提条件を満たしていることをご確認ください。 詳細については、「[Supported operating systems for Macs](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)」 (Mac でサポートされているオペレーティング システム) をご覧ください。  

### <a name="step-1-deploy-a-web-server-certificate-to-site-system-servers"></a>手順 1: Web サーバー証明書をサイト システム サーバーに展開する  
 これらのサイト システムには、その他の構成マネージャー クライアント用に、この証明書が既に存在していることがあります。 証明書がない場合、Web サーバー証明書を、次のサイト システムの役割を持つコンピューターに展開します。  

-   管理ポイント  

-   配布ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

> [!IMPORTANT]  
>  Web サーバー証明書には、サイト システム プロパティで指定されるインターネット FQDN が含まれていなければなりません。  
>   
>  これは、Mac コンピューターをサポートするために、インターネットからサーバーにアクセスできる必要があるということではありません。 インターネットベースのクライアント管理が不要な場合、インターネット FQDN にイントラネット FQDN 値を指定できます。  

 この Web サーバー証明書を作成してインストールする展開の例については、「[IIS を実行するサイト システム用の Web サーバー証明書の展開](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)」をご覧ください。  

> [!IMPORTANT]  
>  管理ポイント、配布ポイント、および登録プロキシ ポイントの Web サーバー証明書に、サイト システムのインターネット FQDN 値が指定されていることを確認してください。  

### <a name="step-2-deploy-a-client-authentication-certificate-to-site-system-servers"></a>手順 2: クライアント認証証明書をサイト システム サーバーに展開する  
 これらのサイト システムには、Configuration Manager 機能用に、この証明書が既に存在していることがあります。 証明書がない場合、クライアント認証証明書を、次のサイト システムの役割を持つコンピューターに展開します。  

-   管理ポイント  

-   配布ポイント  

 管理ポイントのクライアント証明書を作成してインストールする展開の例については、「[Windows コンピューター用のクライアント証明書の展開](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)」をご覧ください。  

 配布ポイントのクライアント証明書を作成してインストールする展開の例については、「[配布ポイント用のクライアント証明書の展開](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)」をご覧ください。  

### <a name="step-3-prepare-the-client-certificate-template-for-macs"></a>手順 3: Mac 用のクライアント証明書テンプレートを準備する  

> [!NOTE]  
>  Configuration Manager 登録ツールを実行するには、Active Directory ユーザー アカウントが必要です。  

 証明書テンプレートには、Mac コンピューターに証明書を登録するユーザー アカウントに対する **読み取り** と **登録** の権限が必要です。  

 「[Mac コンピューター用のクライアント証明書の展開](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1)」をご覧ください。  

### <a name="step-4-configure-the-management-point-and-distribution-point"></a>手順 4: 管理ポイントおよび配布ポイントを構成する  
 次のオプションを指定して、管理ポイントを構成します。  

-   HTTPS  

-   インターネットからクのライアント接続を許可する  

    > [!NOTE]  
    >  この構成値は、Mac コンピューターの管理に必要です。 ただし、インターネットからサイト システム サーバーにアクセスする必要があるということではありません。  

-   モバイル デバイスおよび Mac コンピューターでこの管理ポイントを使用できるようにする  

 Mac コンピューターへのクライアントのインストールに配布ポイントは必要ありませんが、構成マネージャー クライアントをインストールした後で、これらの Mac コンピューターにソフトウェアを展開する場合は、インターネットからのクライアント接続を許可するように配布ポイントを構成する必要があります。  

 この手順では、既存の管理ポイントと配布ポイントで Mac コンピューターのサポートを構成します。 この手順を開始する前に、管理ポイントおよび配布ポイントを実行するサイト システム サーバーがインターネット FQDN を指定して構成されていることを確認してください。 このようなサイト システム サーバーがインターネットベースのクライアント管理をサポートしない場合、インターネット FQDN 値としてイントラネット FQDN を指定できます。 また、これらのサイト システムの役割はプライマリ サイト内になければなりません。  

##### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>管理ポイントと配布ポイントで Mac のサポートを構成するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [管理 **** ] ワークスペースで [サイトの構成 ****] を展開し、[サーバーとサイト システムの役割 ****] を選択して、構成対象のサイト システムの役割を保有しているサーバーを選択します。  

3.  詳細ウィンドウで、[管理ポイント ****] を右クリックし、[役割のプロパティ ****] をクリックして、[管理ポイントのプロパティ **** ] ダイアログ ボックスで次のオプションを構成し、[OK ****] をクリックします。  

    1.  [HTTPS ****] を選択します。  

    2.  [インターネットのみのクライアント接続を許可する **** ] または [イントラネットとインターネット両方のクライアント接続を許可する ****] を選択します。 これらのオプションを使用するには、サイト システム サーバーにインターネットからアクセスできない場合でも、インターネット FQDN をサイト システムのプロパティに指定する必要があります。  

    3.  [モバイル デバイスおよび Mac コンピューターでこの管理ポイントを使用できるようにする ****] を選択します。  

4.  詳細ウィンドウで、[管理ポイント ****] を右クリックし、[役割のプロパティ ****] をクリックして、[配布ポイントのプロパティ **** ] ダイアログ ボックスで次のオプションを構成し、[OK ****] をクリックします。  

    -   [HTTPS ****] を選択します。  

    -   [インターネットのみのクライアント接続を許可する **** ] または [イントラネットとインターネット両方のクライアント接続を許可する ****] を選択します。 これらのオプションを使用するには、サイト システム サーバーにインターネットからアクセスできない場合でも、インターネット FQDN をサイト システムのプロパティに指定する必要があります。  

    -   [証明書をインポートする ****] をクリックし、エクスポートされているクライアント配布ポイント証明書ファイルを参照して、パスワードを指定します。  

5.  Mac コンピューターで使用するプライマリ サイトのすべての管理ポイントと配布ポイントについて、手順 2 ～ 4 を繰り返します。  

### <a name="step-5-configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>手順 5: 登録プロキシ ポイントおよび登録ポイントを構成する  
 これらのサイト システムの役割は同じサイトにインストールする必要がありますが、同じサイト システム サーバーや同じ Active Directory フォレストにインストールする必要はありません。  

 サイト システムの役割の配置と考慮事項について詳しくは、「[System Center Configuration Manager のサイト システム サーバーとサイト システムの役割の計画](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)」の「[サイト システムの役割](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)」をご覧ください。  

 これらの手順では、サイト システム サーバーで Mac コンピューターのサポートを構成します。 Mac コンピューターのサポート用に新しいサイト システム サーバーをインストールするか、既存のサイト システム サーバーを使用するかによって、次の手順のいずれかを選択します。  

-   [登録サイト システムをインストールして構成するには (新しいサイト システム サーバーの場合)](#BKMK_HowtoInstallEnrollmentSiteSystems_new)  

-   [登録サイト システムをインストールして構成するには (既存のサイト システム サーバーの場合)](#BKMK_HowtoInstallEnrollmentSiteSystems_existing)  

####  <a name="a-namebkmkhowtoinstallenrollmentsitesystemsnewa-to-install-and-configure-the-enrollment-site-systems-new-site-system-server"></a><a name="BKMK_HowtoInstallEnrollmentSiteSystems_new"></a> 登録サイト システムをインストールして構成するには (新しいサイト システム サーバーの場合)  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [管理 **** ] ワークスペースで、[サイトの構成 ****] を展開して [サーバーとサイト システムの役割 ****  

3.  [ **ホーム** ] タブの [ **作成** ] グループで、[ **サイト システム サーバーの作成**] をクリックします。  

4.  **[全般]** ページで、サイト システムの全般設定を指定し、 **[次へ]**をクリックします。  

    > [!IMPORTANT]  
    >  サイト システム サーバーがインターネットからアクセスできない場合でも、インターネット FQDN には値を指定してください。 インターネットからサイト システム サーバーにアクセスできないようにするために、インターネット FQDN を指定しない場合は、インターネット FQDN としてイントラネット FQDN 値を指定できます。 Mac コンピューターは、イントラネット上にあっても、常にインターネット FQDN に接続します。  

5.  [システムの役割の選択 **** ] ページの利用可能な役割の一覧で、[登録プロキシ ポイント **** ] および [登録ポイント **** ] を選択して、[次へ ****] をクリックします。  

6.  [登録プロキシ ポイント **** ] ページで、設定を確認し、必要な変更を加えて、[次へ ****] をクリックします。  

7.  [登録ポイントの設定 **** ] ページで、設定を確認し、必要な変更を加えて、[次へ ****] をクリックします。  

8.  ウィザードを完了します。  

####  <a name="a-namebkmkhowtoinstallenrollmentsitesystemsexistinga-to-install-and-configure-the-enrollment-site-systems-existing-site-system-server"></a><a name="BKMK_HowtoInstallEnrollmentSiteSystems_existing"></a> 登録サイト システムをインストールして構成するには (既存のサイト システム サーバーの場合)  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [管理 **** ] ワークスペースで [サイトの構成 ****] を展開し、[サーバーとサイト システムの役割 ****] を選択して、Mac コンピューターのサポートに使用するサーバーを選択します。  

3.  [ホーム **** ] タブの [作成 **** ] グループで、[サイト システムの役割の追加 ****] をクリックします。  

4.  **[全般]** ページで、サイト システムの全般設定を指定し、 **[次へ]**をクリックします。  

    > [!IMPORTANT]  
    >  サイト システム サーバーがインターネットからアクセスできない場合でも、インターネット FQDN には値を指定してください。 インターネットからサイト システム サーバーにアクセスできないようにするために、インターネット FQDN を指定しない場合は、インターネット FQDN としてイントラネット FQDN 値を指定できます。 Mac コンピューターは、イントラネット上にあっても、常にインターネット FQDN に接続します。  

5.  [システムの役割の選択 **** ] ページの利用可能な役割の一覧で、[登録プロキシ ポイント **** ] および [登録ポイント **** ] を選択して、[次へ ****] をクリックします。  

6.  [登録プロキシ ポイント **** ] ページで、設定を確認し、必要な変更を加えて、[次へ ****] をクリックします。  

7.  [登録ポイントの設定 **** ] ページで、設定を確認し、必要な変更を加えて、[次へ ****] をクリックします。  

8.  ウィザードを完了します。  

### <a name="step-6-optional-install-the-reporting-services-point"></a>手順 6: オプション: レポート サービス ポイントをインストールする  
 Mac コンピューターのレポートを実行する場合は、レポート サービス ポイントをインストールします。  

 レポート サービス ポイントのインストールと構成方法の詳細については、「[System Center Configuration Manager におけるレポートの構成](../../../core/servers/manage/configuring-reporting.md)」をご覧ください。  

### <a name="step-7-configure-client-settings-for-enrollment"></a>手順 7: 登録のためのクライアント設定を構成する  
 Mac コンピューターの登録を構成するには、既定のクライアント設定を使用する必要があります。カスタムのクライアント設定は使用できません。  

 クライアント設定の詳細については、「 [About client settings in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md)」を参照してください。  

 この手順は、Configuration Manager が Mac コンピューターで証明書を要求してインストールするために必要です。  

##### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>Mac に証明書を登録する Configuration Manager の既定のクライアント設定を構成するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [ **管理** ] ワークスペースで [ **クライアント設定**] をクリックします。  

3.  [既定のクライアント設定 ****] をクリックします。  

    > [!IMPORTANT]  
    >  登録の構成にカスタムのクライアント設定を使用することはできません。既定のクライアント設定を使用する必要があります。  

4.  **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]**をクリックします。  

5.  [モバイル デバイス **** ] セクションを選択し、次のユーザー設定を構成します。  

    1.  **ユーザーがモバイル デバイスと Mac コンピューターを登録できるようにする: はい**  

    2.  **[登録プロファイル]:** **[プロファイルの設定]**をクリックします。  

6.  [モバイル デバイス登録プロファイル **** ] ダイアログ ボックスで、[作成 ****] をクリックします。  

7.  [登録プロファイルの作成 **** ] ダイアログ ボックスで、この登録プロファイルの名前を入力し、[管理サイト コード ****] を構成します。 Mac コンピューターを管理する管理ポイントを含む Configuration Manager プライマリ サイトを選択します。  

    > [!NOTE]  
    >  サイトを選択できない場合は、そのサイト内で少なくとも 1 つの管理ポイントがモバイル デバイスをサポートするように構成されていることを確認してください。  

8.  [ **追加**] をクリックします。  

9. [モバイル デバイスの証明機関の追加 **** ] ダイアログ ボックスで、Mac コンピューターに証明書を発行する認証機関 (CA) サーバーを選択し、[OK ****] をクリックします。  

10. [登録プロファイルの作成 **** ] ダイアログ ボックスで、手順 3 で作成した Mac コンピューター証明書テンプレートを選択し、[OK ****] をクリックします。  

11. [OK **** ] をクリックして [登録プロファイル **** ] ダイアログ ボックスを閉じ、[OK **** ] をクリックして [既定のクライアント設定 **** ] ダイアログ ボックスを閉じます。  

    > [!TIP]  
    >  クライアント ポリシーの間隔を変更する場合、[クライアント ポリシー **** ] クライアント設定グループの [クライアント ポリシーのポーリング間隔 **** ] クライアント設定を使用します。  

 すべてのユーザーは、次回クライアント ポリシーをダウンロードしたときに、これらの設定を使用して構成されます。 1 つのクライアントのポリシーの取得を開始するには、「[構成マネージャー クライアントのポリシーの取得開始](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)」をご覧ください。  

 登録クライアント設定の他に、次の構成マネージャー クライアント デバイス設定が構成されていることを確認します。  

-   **[ハードウェア インベントリ]**: Mac および Windows クライアント コンピューターからハードウェア インベントリを収集する場合、このクライアント設定を有効にして構成します。 詳細については、「[System Center Configuration Manager でのハードウェア インベントリの拡張方法](../../../core/clients/manage/inventory/extend-hardware-inventory.md)」をご覧ください。  

-   **[コンプライアンス設定]**: Mac および Windows クライアント コンピューターの設定を評価して修復する場合、このクライアント設定を有効にして構成します。 詳細については、「[コンプライアンス設定の計画と構成](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)」をご覧ください。  

> [!NOTE]  
>  構成マネージャー クライアント設定の詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../core/clients/deploy/configure-client-settings.md)」をご覧ください。  

### <a name="step-8-download-the-client-source-files-for-macs"></a>手順 8: Mac 用のクライアント ソース ファイルをダウンロードする  
 Mac に構成マネージャー クライアントをインストールして管理する前に、次のプログラムをダウンロードしてインストールする必要があります。  

-   **Ccmsetup**: 組織の Mac コンピューターに構成マネージャー クライアントをインストールするには、このアプリケーションを使用します。  

-   **CMDiagnostics**: 組織の Mac コンピューターの構成マネージャー クライアントに関連する診断情報を収集するには、このツールを使用します。  

-   **CMUninstall**: 組織の Mac コンピューターから構成マネージャー クライアントをアンインストールするには、このツールを使用します。  

-   **CMAppUtil**: Apple アプリケーション パッケージを Configuration Manager アプリケーションとして展開できる形式に変換するには、このツールを使用します。  

-   **CMEnroll**: Mac コンピューター用のクライアント証明書を要求してインストールし、構成マネージャー クライアントをインストールできるようにするには、このツールを使用します。  

> [!IMPORTANT]  
>  Mac コンピューター用の新しいクライアントをインストールする場合は、Configuration Manager の更新プログラムをインストールして、Configuration Manager コンソールで新しいクライアント情報を反映する必要もあります。  

##### <a name="to-download-and-install-the-mac-os-x-client-files"></a>Mac OS X クライアント ファイルをダウンロードしてインストールするには  

1.  Mac OS X クライアント ファイル パッケージ ( **ConfigmgrMacClient.msi**) をダウンロードして、Windows を実行しているコンピューターに保存します。  

     このファイルは Configuration Manager インストール メディアに含まれていません。 このファイルは、 [Microsoft ダウンロード センター](http://go.microsoft.com/fwlink/?LinkID=525184)からダウンロードできます。  

2.  Windwos コンピューターで、ダウンロードした **ConfigmgrMacClient.msi** ファイルを実行し、Mac クライアント パッケージ (Macclient.dmg) をローカル ディスクのフォルダー (既定では、 **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**) に抽出します。  

3.  Macclient.dmg ファイルを Mac コンピューターのフォルダーにコピーします。  

4.  Mac コンピューターで、ダウンロードした Macclient.dmg ファイルを実行して、ローカル ディスクのフォルダーにファイルを抽出します。  

5.  フォルダーに Ccmsetup と CMClient.pkg ファイルが抽出されていることと、Tools という名前のフォルダーが作成され、CMDiagnostics、CMUninstall、CMAppUtil and CMEnroll ツールが含まれていることを確認します。  

### <a name="step-9-install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>手順 9: Mac にクライアントをインストールし、クライアント証明書を登録する  
 この手順では、クライアントをインストールし、CMEnroll ツールを使用して Mac コンピューター用にクライアント証明書を要求してインストールし、Configuration Manager を使用してこのコンピューターを管理できるようにします。  

 CMEnroll ツールを使用することなく、Mac コンピューターの登録ウィザードを使用してクライアントを登録できます。 詳細については、以下の手順を参照してください。  

##### <a name="to-install-the-client-and-enroll-the-certificate-by-using-the-cmenroll-tool"></a>CMEnroll ツールを使用して、クライアントをインストールし、証明書を登録するには  

1.  Mac コンピューターで、Microsoft ダウンロード センターからダウンロードした Macclient.dmg の内容を抽出したフォルダーに移動します。  

2.  次のコマンドラインを入力します。 **sudo ./ccmsetup**  

3.  「 **Completed installation (インストール完了)** 」メッセージが表示されるまで待ちます。 インストーラーでは、再起動が必要というメッセージが表示されますが、ここでは再起動せず、次の手順に進みます。  

4.  Mac コンピューターの Tools フォルダーで、次のコマンドを入力します: **sudo ./CMEnroll -s &lt;enrollment_proxy_server_name> -ignorecertchainvalidation -u &lt;user name'>**  

    > [!NOTE]  
    >  クライアントのインストール後に、Mac コンピューターの登録ウィザードを使用して Mac コンピューターを登録できます。 この方法でクライアントを登録する場合は、このトピックの「 [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) 」を参照してください。  

     Active Directory ユーザー アカウントのパスワードを入力するように求められます。  

    > [!IMPORTANT]  
    >  このコマンドを入力すると、実際には 2 つのパスワードの入力が求められます。最初のプロンプトは、コマンドを実行するスーパー ユーザー アカウント用です。 2 つ目のプロンプトは、Active Directory ユーザー アカウント用です。 プロンプトは似ているため、正しい順番で指定するように気を付けてください。  

     ユーザー名は、次の形式で入力できます。  

    -   'ドメイン\名前' (たとえば、'contoso\mnorth')  

    -   'user@domain'. たとえば、次のように入力します。 'mnorth@contoso.com'  

     ユーザー名と、対応するパスワードは、Mac クライアント証明書テンプレートに対する読み取り権限と登録権限が付与された Active Directory ユーザー アカウントと一致している必要があります。  

     例: 登録プロキシ ポイント サーバーの名前が **server02.contoso.com** で、ユーザー名が **contoso\mnorth**のユーザーに Mac クライアント証明書テンプレートに対するアクセス許可が付与されている場合、次のように入力します: **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!IMPORTANT]  
    >  ユーザー名に **&lt;>"+=** のいずれかの文字が含まれている場合、登録は失敗します。  
    >   
    >  この問題を解決するには、これらの文字が含まれていないユーザー名で帯域外証明書を取得します。  

    > [!NOTE]  
    >  ユーザー エクスペリエンスを単純化するには、インストール手順とコマンドをスクリプト化し、ユーザーがユーザー名とパスワードを指定するだけで済むようにします。  

5.  「 **Successfully enrolled (正常に登録されました)** 」メッセージが表示されるまで待ちます。  

6.  Mac コンピューターで、登録する証明書を Configuration Manager に制限するには、ターミナル ウィンドウを開き、次のように変更します。  

    1.  コマンド **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**を入力します。  

    2.  [Keychain Access **** ] ダイアログ ボックスの [Keychains **** ] セクションで、[System ****] をクリックし、[Category **** ] セクションの [Keys ****] をクリックします。  

    3.  キーを展開してクライアント証明書を表示します。 インストールした秘密キーの証明書を特定したら、そのキーをダブルクリックします。  

    4.  [アクセス制御 **** ] タブで、[アクセスを許可する前に確認する ****] を選択します。  

    5.  **/Library/Application Support/Microsoft/CCM**を参照し、 **[CCMClient]**を選択して **[追加]**をクリックします。  

    6.  [Save Changes **** ] をクリックし、[Keychain Access **** ] ダイアログ ボックスを閉じます。  

7.  Mac コンピューターを再起動します。  

 Mac コンピューターの [システム環境設定 **** ] で [Configuration Manager **** ] 項目を開いて、クライアントのインストールが正常に完了したことを確認します。 また、[すべてのシステム **** ] コレクションを更新して表示し、Mac コンピューターが管理されたクライアントとして、このコレクションに表示されていることを確認できます。  

> [!TIP]  
>  Mac クライアントに関する問題のトラブルシューティングを実行するには、Mac OS X クライアント パッケージに含まれている CMDiagnostics を使用して、次の診断情報を収集します。  
>   
>  -   実行中のプロセスの一覧  
> -   Mac OS X オペレーティング システムのバージョン  
> -   構成マネージャー クライアントに関連する Mac OS X のクラッシュ レポート (**CCM\*.crash** と **System Preference.crash** を含む)  
> -   構成マネージャー クライアントのインストールで作成される Bill of Materials (BOM) ファイルとプロパティ一覧 (.plist) ファイル  
> -   /Library/Application Support/Microsoft/CCM/Logs フォルダーの内容  
>   
>  CmDiagnostics で収集された情報は、コンピューターのデスクトップに保存される zip ファイルに追加され、cmdiag-*<ホスト名\>***-***<日付と時刻\>*.zip という名前が付けられます。  

####  <a name="a-namebkmkenrollr2a-to-enroll-the-client-by-using-the-mac-computer-enrollment-wizard"></a><a name="BKMK_EnrollR2"></a> To enroll the client by using the Mac Computer Enrollment Wizard  

1.  クライアントのインストールを完了したら、コンピューターの登録ウィザードが開きます。 [次へ **** ] をクリックして、ようこそページの次に進みます。  

    > [!NOTE]  
    >  ウィザードが表示されなかった場合や、間違ってウィザードを閉じてしまった場合は、 **Configuration Manager** の環境設定ページで **[登録]** をクリックして、ウィザードを開いてください。  

2.  ウィザードの次のページで、次の情報を指定します。  

    -   **ユーザー名** : 次の形式で入力できます。  

        -   'ドメイン\名前' (たとえば、'contoso\mnorth')  

        -   'user@domain'. たとえば、次のように入力します。 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  電子メール アドレスを使用して **[ユーザー名]** フィールドを指定すると、Configuration Manager により、電子メール アドレスのドメイン名と登録プロキシ ポイント サーバーの既定の名前を使用して **[サーバー名]** フィールドが自動的に指定されます。 このドメイン名とサーバー名が登録プロキシ ポイント サーバーの名前と一致しない場合、使用する正しい名前をユーザーに知らせて、Mac コンピューターを登録するときにその情報を入力できるようにする必要があります。  

         ユーザー名と、対応するパスワードは、Mac クライアント証明書テンプレートに対する読み取り権限と登録権限が付与された Active Directory ユーザー アカウントと一致している必要があります。  

    -   **パスワード**: 指定したユーザー名に対応するパスワードを入力します。  

    -   **サーバー名**: 登録プロキシ ポイント サーバーの名前を入力します。  

3.  [次へ **** ] をクリックして、ウィザードを完了します。  

##  <a name="a-nameuninstallmacclienta-uninstalling-the-mac-client"></a><a name="uninstallMacClient"></a> Uninstalling the Mac client  
 Mac クライアントをアンインストールする場合、Web からダウンロードした Mac クライアント ファイルに含まれている CMUninstall スクリプトを使用します。 次の手順に従って、Configuration Manager クライアントを Mac コンピューターからアンインストールします。  

#### <a name="to-uninstall-the-mac-client"></a>Mac クライアントをアンインストールするには  

1.  Mac コンピューターでターミナル ウィンドウを開き、Microsoft ダウンロード センターからダウンロードした macclient.dmg の内容を抽出したフォルダーに移動します。  

2.  ツール フォルダーに移動し、次のコマンドラインを入力します。  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  **-c** プロパティは、クライアントのアンインストールで、クライアントのクラッシュ ログとログ ファイルも削除するように指示します。 このプロパティは省略できますが、後でクライアントを再インストールする場合の混乱を防ぐために推奨されます。  

3.  必要に応じて、Configuration Manager が使用していたクライアント認証証明書を手動で削除するか、失効させます。 CMUnistall では、この証明書は削除または失効されません。  

##  <a name="a-namebkmkrenewa-renewing-the-mac-client-certificate"></a><a name="BKMK_Renew"></a> Renewing the Mac client certificate  
 Mac クライアント証明書を更新する方法は、次の 2 通りあります。  

-   [Renewing the Mac client certificate by using the Renew Certificate Wizard](#BKMK_UI)  

-   [Renewing the Mac client certificate manually](#BKMK_Man)  

###  <a name="a-namebkmkuia-renewing-the-mac-client-certificate-by-using-the-renew-certificate-wizard"></a><a name="BKMK_UI"></a> Renewing the Mac client certificate by using the Renew Certificate Wizard  
 Configuration Manager の証明書の更新ウィザードを構成して使用するには、次の手順に従います。  

##### <a name="to-renew-the-mac-client-certificate-by-using-the-renew-certificate-wizard"></a>証明書の更新ウィザードを使用して Mac クライアント証明書を更新するには  

1.  ccmclient.plist ファイルで次の値を構成して、証明書の更新ウィザードがいつ開くかを制御します。  

    > [!IMPORTANT]  
    >  以下の値は、必ず文字列として指定してください。 **-int** プロパティを使って整数として指定すると、値が読み取られません。  

    -   **RenewalPeriod1**: ユーザーが証明書を更新できる 1 番目の更新期間を秒単位で指定します。 既定値は 3,888,000 秒 (45 日) です。  

        > [!NOTE]  
        >  **RenewalPeriod1** を 300 秒以上に設定した場合は、その値が使われます。  0 ～ 300 秒の値に設定した場合は、既定の 45 日が使われます。  

    -   **RenewalPeriod2**: ユーザーが証明書を更新できる 2 番目の更新期間を秒単位で指定します。 既定値は 259,200 秒 (3 日) です。  

        > [!NOTE]  
        >  **RenewalPeriod2** を 300 秒以上、 **RenewalPeriod1**の値以下に設定した場合は、その値が使われます。 **RenewalPeriod1** の値が 3 日より大きい場合は、 **RenewalPeriod2**の値として 3 日が使われます。  **RenewalPeriod1** の値が 3 日より小さい場合は、 **RenewalPeriod2** が **RenewalPeriod1**と同じ値に設定されます。  

    -   **RenewalReminderInterval1**: 1 番目の更新期間中に、証明書の更新ウィザードがユーザーに表示される頻度を秒単位で指定します。 既定値は 86,400 秒 (1 日) です。  

        > [!NOTE]  
        >  **RenewalReminderInterval1** を 300 秒以上、 **RenewalPeriod1**の値未満に設定した場合は、その値が使われます。 それ以外の場合は、既定値の 1 日が使われます。  

    -   **RenewalReminderInterval2**: 2 番目の更新期間中に、証明書の更新ウィザードがユーザーに表示される頻度を秒単位で指定します。 既定値は 28,800 秒 (8 時間) です。  

        > [!NOTE]  
        >  **RenewalReminderInterval2** を 300 秒以上、 **RenewalReminderInterval1** の値以下、且つ **RenewalPeriod2**の値以下に設定した場合は、その値が使われます。 それ以外の場合は、8 時間が使われます。  

     **例:** すべて既定値のままにすると、証明書が失効する 45 日前から、24 時間に 1 回の割合でウィザードが開きます。  証明書が失効する 3 日前になると、8 時間に 1 回ウィザードが開くようになります。  

     **例:** 1 回目の更新期間を 20 日に設定するには、次のコマンドライン (またはスクリプト) を使用します。  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  証明書の更新ウィザードが開いたときには、通常、 **[ユーザー名]** フィールドと **[サーバー名]** フィールドに既に値が挿入されており、ユーザーはパスワードを入力するだけで証明書を更新できます。  

    > [!NOTE]  
    >  ウィザードが表示されなかった場合や、間違ってウィザードを閉じてしまった場合は、 **Configuration Manager** の環境設定ページで **[更新]** をクリックして、ウィザードを開いてください。  

###  <a name="a-namebkmkmana-renewing-the-mac-client-certificate-manually"></a><a name="BKMK_Man"></a> Renewing the Mac client certificate manually  
 Mac クライアント証明書の一般的な有効期間は 1 年間です。 Configuration Manager への登録時に必要なユーザー証明書は、自動的に更新されません。そのため、次の手順に従って証明書を手動で更新する必要があります。  

> [!IMPORTANT]  
>  証明書が期限切れになった場合、Mac クライアントのアンインストール、再インストール、および再登録を行う必要があります。  

 この手順で SMSID が削除されます。SMSID は、同じ Mac コンピューターの新しい証明書を要求するために必要です。 新しい証明書を要求すると、その証明書が Configuration Manager で自動的に使用されます。  

> [!IMPORTANT]  
>  クライアント SMSID を削除して置き換えると、Configuration Manager コンソールからクライアントが削除された後に、インベントリなどの保存されているクライアント履歴も削除されます。  

##### <a name="to-renew-the-mac-client-certificate-manually"></a>Mac クライアント証明書を手動で更新するには  

1.  ユーザー証明書を更新する必要がある Mac コンピューターのデバイス コレクションを作成してから、Mac コンピューターをコレクションに追加します。  

    > [!WARNING]  
    >  Configuration Manager は、Mac コンピューター用に登録されている証明書の有効期間を監視しません。 Configuration Manager とは関係なく有効期間を監視して、このコレクションに追加する Mac コンピューターを特定する必要があります。  

2.  [資産とコンプライアンス **** ] ワークスペースで、構成項目の作成ウィザード ****を開始します。  

3.  ウィザードの [全般 **** ] ページで、次の情報を指定します。  

    -   **[名前]:Mac の SMSID の削除**  

    -   **[種類]:Mac OS X**  

4.  ウィザードの [サポートされているプラットフォーム **** ] ページで、すべての Mac OS X バージョンが選択されていることを確認します。  

5.  ウィザードの [設定 **** ] ページで [新規作成 **** ] をクリックし、[設定の作成 **** ] ダイアログ ボックスで次の情報を指定します。  

    -   **[名前]:Mac の SMSID の削除**  

    -   **[設定の種類]:スクリプト**  

    -   **[データ型]:文字列**  

6.  **[設定の作成]** ダイアログ ボックスの **[検索スクリプト]**で **[スクリプトの追加]** をクリックし、SMSID が構成されている Mac コンピューターを検出するスクリプトを指定します。  

7.  [探索スクリプトの編集 **** ] ダイアログ ボックスで、次のシェル スクリプトを入力します。  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  [OK **** ] をクリックして、[探索スクリプトの編集 **** ] ダイアログ ボックスを閉じます。  

9. [設定の作成 **** ] ダイアログ ボックスの [修復スクリプト (オプション) ****] で、[スクリプトの追加 **** ] をクリックして、Mac コンピューターで見つかった SMSID を削除するスクリプトを指定します。  

10. [修復スクリプトの作成 **** ] ダイアログ ボックスで、次のシェル スクリプトを入力します。  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. [OK **** ] をクリックして [修復スクリプトの作成 **** ] ダイアログ ボックスを閉じます。  

12. ウィザードの [コンプライアンス規則 **** ] ページで [新規作成 ****] をクリックし、[規則の作成 **** ] ダイアログ ボックスで次の情報を指定します。  

    -   **[名前]:Mac の SMSID の削除**  

    -   **[選択した設定]:** **[参照]** をクリックし、前に指定した探索スクリプトを選びます。  

    -   **[次の値]** フィールドに「 **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**」と入力します。  

    -   オプション [この設定が対応していない場合に指定した修復スクリプトを実行する ****] を有効にします。  

13. 構成項目の作成ウィザードを完了します。  

14. 作成した構成項目を含む構成基準を作成し、それを手順 1 で作成したデバイス コレクションに展開します。  

     構成基準の作成方法と展開方法の詳細については、「[System Center Configuration Manager で構成基準を作成する方法](../../../compliance/deploy-use/create-configuration-baselines.md)」および「[System Center Configuration Manager で構成基準を展開する方法](../../../compliance/deploy-use/deploy-configuration-baselines.md)」をご覧ください。  

15. SMSID を削除した Mac コンピューターで、次のコマンドを実行して新しい証明書をインストールします。  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     プロンプトが表示されたら、コマンドを実行するスーパー ユーザー アカウントのパスワードを指定し、Active Directory ユーザー アカウントのパスワードを指定します。  

16. Mac コンピューターで、登録する証明書を Configuration Manager に制限するには、ターミナル ウィンドウを開き、次のように変更します。  

    1.  コマンド **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**を入力します。  

    2.  [Keychain Access **** ] ダイアログ ボックスの [Keychains **** ] セクションで、[System ****] をクリックし、[Category **** ] セクションの [Keys ****] をクリックします。  

    3.  キーを展開してクライアント証明書を表示します。 インストールした秘密キーの証明書を特定したら、そのキーをダブルクリックします。  

    4.  [アクセス制御 **** ] タブで、[アクセスを許可する前に確認する ****] を選択します。  

    5.  **/Library/Application Support/Microsoft/CCM**を参照し、 **[CCMClient]**を選択して **[追加]**をクリックします。  

    6.  [Save Changes **** ] をクリックし、[Keychain Access **** ] ダイアログ ボックスを閉じます。  

17. Mac コンピューターを再起動します。  

##  <a name="a-namebkmkmanualcertifcateinstallationa-use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a><a name="BKMK_ManualCertifcateInstallation"></a> Use a certificate request and installation method that is independent from Configuration Manager  
 Configuration Manager の登録を使用せず、Configuration Manager とは独立したクライアント証明書を要求およびインストールする場合、一部の構成手順が異なります。  

1.  手順 1、2、4、6 (省略可能)、および 8 を実行します。  

2.  手順 3、5、7、および 9 は実行しないでください。  

3.  次の指示に従ってクライアントをインストールします。  

#### <a name="to-install-the-client-certificate-independently-from-configuration-manager-and-install-the-client"></a>Configuration Manager とは独立してクライアント証明書をインストールし、クライアントをインストールするには  

1.  Configuration Manager とは独立してクライアント証明書をインストールするには、選択した証明書の展開方法で指定されている指示に従い、クライアント証明書を要求して、Mac コンピューターにインストールします。  

2.  Microsoft ダウンロード センターからダウンロードした macclient.dmg ファイルのコンテンツを抽出したフォルダーに移動します。  

3.  次のコマンドラインを入力します: **sudo ./ccmsetup -MP <management point Internet FQDN\> -SubjectName <certificate subject value\>**  

    > [!IMPORTANT]  
    >  証明書のサブジェクト値は大文字と小文字が区別されるので、証明書の詳細に表示されるとおりに入力してください。  

     例: サイト システムのプロパティのインターネット FQDN が **server03.contoso.com** であり、Mac クライアント証明書が証明書のサブジェクトで共通名として **mac12.contoso.com** という FQDN を持っている場合、次のように入力します: **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  "Completed installation **** " というメッセージが表示されるまで待ってから、Mac コンピューターを再起動します。  

5.  Mac コンピューターで、この証明書から Configuration Manager にアクセスできるようにするには、ターミナル ウィンドウを開き、次のように変更します。  

    1.  コマンド **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**を入力します。  

    2.  [Keychain Access **** ] ダイアログ ボックスの [Keychains **** ] セクションで、[System ****] をクリックし、[Category **** ] セクションの [Keys ****] をクリックします。  

    3.  キーを展開してクライアント証明書を表示します。 インストールした秘密キーの証明書を特定したら、そのキーをダブルクリックします。  

    4.  [アクセス制御 **** ] タブで、[アクセスを許可する前に確認する ****] を選択します。  

    5.  **/Library/Application Support/Microsoft/CCM**を参照し、 **[CCMClient]**を選択して **[追加]**をクリックします。  

    6.  [Save Changes **** ] をクリックし、[Keychain Access **** ] ダイアログ ボックスを閉じます。  

6.  同じサブジェクト値を含む証明書が複数ある場合、構成マネージャー クライアントに使用する証明書を特定するには、証明書のシリアル番号を指定する必要があります。 このためには、次のコマンドを使用します: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<シリアル番号\>"**  

     たとえば、次のように入力します。 **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Mac コンピューターの [システム環境設定 **** ] で [Configuration Manager **** ] 項目を開いて、クライアントのインストールが正常に完了したことを確認します。 また、[すべてのシステム **** ] コレクションを更新して表示し、Mac コンピューターが管理されたクライアントとして、このコレクションに表示されていることを確認できます。  

### <a name="renewing-the-mac-client-certificate"></a>Mac クライアント証明書の更新  
 Mac コンピューターのコンピューター証明書を更新する前に、次の手順を実行します。  

 この手順で SMSID を削除します。SMSID は、クライアントが Mac コンピューターで新規または更新された証明書を使用するときに必要です。  

> [!IMPORTANT]  
>  クライアント SMSID を削除して置き換えると、Configuration Manager コンソールからクライアントが削除された後に、インベントリなどの保存されているクライアント履歴も削除されます。  

##### <a name="to-renew-the-mac-client-certificate"></a>Mac クライアント証明書を更新するには  

1.  コンピューター証明書を更新する必要がある Mac コンピューターのデバイス コレクションを作成してから、Mac コンピューターをコレクションに追加します。  

2.  [資産とコンプライアンス **** ] ワークスペースで、構成項目の作成ウィザード ****を開始します。  

3.  ウィザードの [全般 **** ] ページで、次の情報を指定します。  

    -   **[名前]:Mac の SMSID の削除**  

    -   **[種類]:Mac OS X**  

4.  ウィザードの [サポートされているプラットフォーム **** ] ページで、すべての Mac OS X バージョンが選択されていることを確認します。  

5.  ウィザードの [設定 **** ] ページで [新規作成 **** ] をクリックし、[設定の作成 **** ] ダイアログ ボックスで次の情報を指定します。  

    -   **[名前]:Mac の SMSID の削除**  

    -   **[設定の種類]:スクリプト**  

    -   **[データ型]:文字列**  

6.  **[設定の作成]** ダイアログ ボックスの **[検索スクリプト]**で **[スクリプトの追加]** をクリックし、SMSID が構成されている Mac コンピューターを検出するスクリプトを指定します。  

7.  [探索スクリプトの編集 **** ] ダイアログ ボックスで、次のシェル スクリプトを入力します。  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  [OK **** ] をクリックして、[探索スクリプトの編集 **** ] ダイアログ ボックスを閉じます。  

9. [設定の作成 **** ] ダイアログ ボックスの [修復スクリプト (オプション) ****] で、[スクリプトの追加 **** ] をクリックして、Mac コンピューターで見つかった SMSID を削除するスクリプトを指定します。  

10. [修復スクリプトの作成 **** ] ダイアログ ボックスで、次のシェル スクリプトを入力します。  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. [OK **** ] をクリックして [修復スクリプトの作成 **** ] ダイアログ ボックスを閉じます。  

12. ウィザードの [コンプライアンス規則 **** ] ページで [新規作成 ****] をクリックし、[規則の作成 **** ] ダイアログ ボックスで次の情報を指定します。  

    -   **[名前]:Mac の SMSID の削除**  

    -   **[選択した設定]:** **[参照]** をクリックし、前に指定した探索スクリプトを選びます。  

    -   **[次の値]** フィールドに「 **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**」と入力します。  

    -   オプション [この設定が対応していない場合に指定した修復スクリプトを実行する ****] を有効にします。  

13. 構成項目の作成ウィザードを完了します。  

14. 作成した構成項目を含む構成基準を作成し、それを手順 1 で作成したデバイス コレクションに展開します。  

     構成基準の作成方法と展開方法の詳細については、「[System Center Configuration Manager で構成基準を作成する方法](../../../compliance/deploy-use/create-configuration-baselines.md)」をご覧ください。  

15. SMSID を削除した Mac コンピューターに新しい証明書をインストールしたら、次のコマンドを実行して、新しい証明書を使用するクライアントを構成します。  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. 同じサブジェクト値を含む証明書が複数ある場合、構成マネージャー クライアントに使用する証明書を特定するには、証明書のシリアル番号を指定する必要があります。 このためには、次のコマンドを使用します: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<シリアル番号\>"**  

     たとえば、次のように入力します。 **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Mac コンピューターを再起動します。  



<!--HONumber=Nov16_HO1-->


