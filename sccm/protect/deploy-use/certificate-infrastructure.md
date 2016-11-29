---
title: "証明書インフラストラクチャの構成 | System Center Configuration Manager"
description: "System Center Configuration Manager で証明書の登録を構成する方法を説明します。"
ms.custom: na
ms.date: 10/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
caps.latest.revision: 7
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: 9af69a813a1fe2a07e3b7b289e258b2d0b51a6f7

---
# <a name="certificate-infrastructure"></a>証明書インフラストラクチャ

*適用対象: System Center Configuration Manager (Current Branch)*


 ここでは、System Center Configuration Manager で証明書の登録を構成する方法の手順、説明、詳細情報を示します。 また、作業を始める前に、「[System Center Configuration Manager での証明書プロファイルの前提条件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)」にある前提条件を確認してください。  

 以下の作業が終わり、正常にインストールされていることを確認したら、証明書プロファイルの構成と展開を行うことができます。 詳細については、「[System Center Configuration Manager で証明書プロファイルを作成する方法](../../protect/deploy-use/create-certificate-profiles.md)」をご覧ください。  


**手順 1:** ネットワーク デバイス登録サービスおよび依存する要素をインストールして構成します。 Active Directory 証明書サービス (AD CS) 用のネットワークデバイス登録サービスの役割サービスは、Windows Server 2012 R2 オペレーティング システムで実行する必要があります。
     **重要:** System Center Configuration Manager でネットワーク デバイス登録サービスを使用するには、さらに構成手順を実行する必要があります。
**手順 2:** 証明書登録ポイントをインストールして構成します。 証明書登録ポイントを少なくとも 1 つインストールする必要があります。 この登録ポイントは、中央管理サイトとプライマリ サイトのどちらにあってもかまいません。
**手順 3:** System Center Configuration Manager ポリシー モジュールをインストールします。 ネットワーク デバイス登録サービスを実行するサーバーにポリシー モジュールをインストールします。

## <a name="supplemental-procedures-to-configure-certificate-enrollment-in-configuration-manager"></a>Configuration Manager で証明書の登録を構成するための補足手順  
 前の表の手順で補足手順が必要な場合は、次の情報を参考にしてください。  

###  <a name="step-1-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>手順 1: ネットワーク デバイス登録サービスおよび依存する要素をインストールおよび構成する  
 Active Directory 証明書サービス (AD CS) 用のネットワーク デバイス登録サービスの役割サービスをインストールして構成し、証明書テンプレートのセキュリティ アクセスを変更し、公開キー基盤 (PKI) クライアント認証証明書を展開して、レジストリでインターネット インフォメーション サービス (IIS) の既定の URL サイズの制限を上げます。 必要に応じて、証明書の発行元証明機関 (CA) でカスタムの有効期限を使えるように構成します。  

> [!IMPORTANT]  
>  System Center Configuration Manager でネットワーク デバイス登録サービスを使用するように構成する前に、ネットワーク デバイス登録サービスがインストールされ、構成されていることを確認してください。 サービスに依存する要素が正しく動作しないと、System Center Configuration Manager による証明書登録のトラブルシューティングが難しくなります。  

##### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>ネットワーク デバイス登録サービスおよび依存する要素をインストールして構成するには  

1.  Windows Server 2012 R2 を実行しているサーバーに、ネットワーク デバイス登録サービスの役割サービスをインストールし、Active Directory 証明書サービス サーバーの役割用に構成します。 詳細については、TechNet の Active Directory 証明書サービスの「 [Network Device Enrollment Service Guidance (ネットワーク デバイス登録サービス ガイド)](http://go.microsoft.com/fwlink/p/?LinkId=309016) 」を参照してください。  

2.  必要に応じて、ネットワーク デバイス登録サービスが使用している証明書テンプレートのセキュリティ アクセス許可を変更します。  

    -   System Center Configuration Manager コンソールを実行するアカウントの場合: **[読み取り]** アクセス許可。  

         このアクセス許可は、証明書プロファイルの作成ウィザードを実行して、SCEP 設定プロファイルの作成に使用する証明書テンプレートを参照して選択するときに必要です。 証明書テンプレートを選択すると、ウィザードのページに設定値がいくつか自動的に挿入されます。そのため、手動で入力する手間が省けるだけでなく、ネットワーク デバイス登録サービスが使用している証明書テンプレートと適合しない設定を選択する危険性が低くなります。  

    -   ネットワーク デバイス登録サービスのアプリケーション プールで使用する SCEP サービス アカウントの場合:[読み取り **** ] および [登録 **** ] のアクセス許可  

         この要件は System Center Configuration Manager に固有ではありませんが、ネットワーク デバイス登録サービスの構成に含まれます。 詳細については、TechNet の Active Directory 証明書サービスの「 [Network Device Enrollment Service Guidance (ネットワーク デバイス登録サービス ガイド)](http://go.microsoft.com/fwlink/p/?LinkId=309016) 」を参照してください。  

    > [!TIP]  
    >  どの証明書テンプレートをネットワーク デバイス登録サービスで使用しているかを調べるには、ネットワーク デバイス登録サービスを実行しているサーバーの「HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP」というレジストリ キーを開きます。  

    > [!NOTE]  
    >  これらは、ほとんどの環境に適した既定のセキュリティ アクセス許可です。 ただし、別のセキュリティ構成を使用することもできます。 詳細については、「[System Center Configuration Manager の証明書プロファイルに関する証明書テンプレート アクセス許可の計画](../../protect/plan-design/planning-for-certificate-template-permissions.md)」を参照してください。  

3.  このサーバーに、クライアント認証をサポートするPKI 証明書を展開します。 使用するコンピューターに、既に適切な証明書がインストールされている場合もあれば、この目的専用の証明書を展開しなければならない (または展開したい) 場合もあります。 この証明書の要件の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../core/plan-design/network/pki-certificate-requirements.md)」トピックの「**サーバー用の PKI 証明書**」セクションに記載されているネットワーク デバイス登録サービスの役割サービスが設定された Configuration Manager ポリシー モジュールを実行するサーバーに関する詳細を参照してください。  

    > [!TIP]  
    >  この証明書の展開について不明な点がある場合は、「[配布ポイント用のクライアント証明書の展開](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012)」の手順を参照してください。次の 1 つの例外を除き、証明書の要件は同じです。  
    >   
    >  -   証明書テンプレートのプロパティの [要求処理 **** ] タブにある [プライベート キーのエクスポートを許可する **** ] チェック ボックスをオンにしないでください。  
    >   
    >  System Center Configuration Manager ポリシー モジュールを構成するときに、ローカルのコンピューター ストアを参照して選択できるので、プライベート キーを使用してこの証明書をエクスポートする必要はありません。  

4.  クライアント認証証明書が関連付けられているルート証明書を探します。 そのルート CA 証明書を証明書ファイル (.cer) にエクスポートします。 このファイルを、後で証明書登録ポイント サイト システム サーバーのインストールと構成を行うときに安全にアクセスできる場所に保存します。  

5.  同じサーバーでレジストリ エディターを使って IIS の既定の URL サイズの制限を上げます。このためには、HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters のレジストリ キー DWORD 値を次のように設定します。  

    -   **MaxFieldLength** キーを **65534**に設定します。  

    -   **MaxRequestBytes** キーを **16777216**に設定します。  

     詳細については、Microsoft サポート技術情報の記事「 [820129: Windows 用 Http.sys レジストリ設定](http://go.microsoft.com/fwlink/?LinkId=309013) 」を参照してください。  

6.  同じサーバーでインターネット インフォーメーション サービス (IIS) マネージャーを開き、/certsrv/mscep アプリケーションの要求のフィルタリング設定を変更してサーバーを再起動します。 [要求フィルター設定の編集 **** ] ダイアログ ボックスの [要求制限 **** ] 設定は次のように設定されています。  

    -   **許可されたコンテンツ最大長 (バイト)**: **30000000**  

    -   **URL の最大長 (バイト)**: **65534**  

    -   **クエリ文字列の最大長 (バイト)**: **65534**  

     これらの設定とその構成方法の詳細については、IIS リファレンス ライブラリの「 [Requests Limits (要求の制限)](http://go.microsoft.com/fwlink/?LinkId=309014) 」を参照してください。  

7.  使用している証明書テンプレートよりも有効期間が短い証明書を要求できるようにしたい場合があります。この設定は、エンタープライズ CA では既定で無効になっています。 エンタープライズ CA でこのオプションを有効にするには、次のように、Certutil コマンドライン ツールを使って設定を変更してから、証明書サービスをいったん停止して再開します。  

    1.  **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

    2.  **net stop certsvc**  

    3.  **net start certsvc**  

     詳細については、TechNet ライブラリの PKI Technologies セクションの「 [Certificate Services Tools and Settings (証明書サービスのツールと設定)](http://go.microsoft.com/fwlink/p/?LinkId=309015) 」を参照してください。  

8.  次のようなリンクを使用して、ネットワーク デバイス登録サービスが動作していることを確認してください。例: **https://server.contoso.com/certsrv/mscep/mscep.dll**。 組み込まれているネットワーク デバイス登録サービスの Web ページが表示されるはずです。 この Web ページには、登録サービスの紹介と、ネットワーク デバイスが証明書要求を送信する URL の説明が記載されています。  

 ネットワーク デバイス登録サービスと依存する要素の構成が完了したら、証明書登録ポイントをインストールおよび構成することができます。  

###  <a name="step-2-install-and-configure-the-certificate-registration-point"></a>手順 2:証明書登録ポイントをインストールおよび構成する  
 System Center Configuration Manager の階層に証明書登録ポイントを少なくとも 1 つインストールして構成する必要があります。このサイト システムの役割は、中央管理サイトまたはプライマリ サイトにインストールできます。  

> [!IMPORTANT]  
>  証明書登録ポイントをインストールする前に、「 **サイト システムの要件** 」の「 [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) 」で、証明書登録ポイントに必要なオペレーティング システムとその他の条件を確認してください。  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>証明書登録ポイントをインストールおよび構成するには  

1.  System Center Configuration Manager コンソールで、**[管理]** をクリックします。  

2.  [管理 **** ] ワークスペースで [サイトの構成 ****] を展開し、[サーバーとサイト システムの役割 ****] をクリックしてから、証明書登録ポイントに使用するサーバーを選択します。  

3.  **[ホーム]** タブの **[サーバー]** グループで、 **[サイト システムの役割の追加]**をクリックします。  

4.  **[全般]** ページで、サイト システムの全般設定を指定し、 **[次へ]**をクリックします。  

5.  [プロキシ **** ] ページで [次へ ****] をクリックします。 証明書登録ポイントでは、インターネット プロキシ設定を使用しません。  

6.  [システムの役割の選択 **** ] ページで、利用可能な役割の一覧から [証明書登録ポイント **** ] を選択してから、[次へ ****] をクリックします。  

7.  [証明書登録ポイント **** ] ページで、既定の設定をそのまま使用するか変更して、[追加 ****] をクリックします。  

8.  [URL とルート CA 証明書の追加 **** ] ダイアログ ボックスで、次の項目を指定し、[OK ****] をクリックします。  

    1.  **ネットワーク デバイス登録サービスの URL**: https://*<server_FQDN>*/certsrv/mscep/mscep.dll たとえば、ネットワーク デバイス登録サービスを実行している FQDN が「server1.contoso.com」の場合は、「 **https://server1.contoso.com/certsrv/mscep/mscep.dll**」と入力します。  

    2.  **ルート CA 証明書**:証明書 (.cer) ファイルを参照して選択します。これは、 **手順 1: ネットワーク デバイス登録サービスおよび依存する要素をインストールして構成する**で作成および保存したファイルです。 このルート CA 証明書を使用することで、証明書登録ポイントで、System Center Configuration Manager ポリシー モジュールが使用するクライアント認証証明書を検証できます。  

    > [!NOTE]  
    >  ネットワーク デバイス登録サービスを実行するサーバーが複数ある場合は、[追加 **** ] をクリックして、他のサーバーの詳細を指定します。  

9. **[次へ]** をクリックして、ウィザードを完了します。  

10. インストールが完了するまで待ち、次のいずれかの方法を使用して、証明書登録ポイントが正常にインストールされたことを確認します。  

    -   [監視 **** ] ワークスペースで [システムのステータス ****] を展開し、[コンポーネントのステータス ****] をクリックし、[SMS_CERTIFICATE_REGISTRATION_POINT **** ] コンポーネントからのステータス メッセージを参照します。  

    -   サイト システム サーバーで、*<ConfigMgr インストール パス\>*\Logs\crpsetup.log ファイルおよび *<ConfigMgr インストール パス\>*\Logs\crpmsi.log ファイルを使用します。 インストールが成功した場合、0 の終了コードを返します。  

    -   ブラウザーを使用して、証明書登録ポイントの URL (https://server1.contoso.com/CMCertificateRegistration など) に接続できることを確認します。 アプリケーション名のサーバー エラー ページが開き、 **** HTTP 404 の説明が表示されます。  

11. 証明書登録ポイントが自動的に作成してエクスポートしたルート CA 証明書ファイルを、プライマリ サイト サーバー コンピューターの *<ConfigMgr Installation Path\>*\inboxes\certmgr.box フォルダーで見つけます。 このファイルを、後でネットワーク デバイス登録サービスを実行しているサーバーに System Center Configuration Manager ポリシー モジュールをインストールするときに安全にアクセスできる場所に保存します。  

    > [!TIP]  
    >  この証明書ファイルは、上に示されているフォルダー内にすぐに格納されません。 System Center Configuration Manager がこの場所にファイルをコピーするまで、しばらく (30 分ほど) 待つ必要がある場合があります。  

 証明書登録ポイントのインストールと構成が完了したら、ネットワーク デバイス登録サービスの System Center Configuration Manager ポリシー モジュールをインストールできます。  

###  <a name="step-3-install-the-configuration-manager-policy-module"></a>手順 3:Configuration Manager ポリシー モジュールをインストールする  
 「**手順 2: 証明書登録ポイントをインストールおよび構成する **」で指定した各サーバーに、System Center Configuration Manager ポリシー モジュールをインストールして、証明書登録ポイントのプロパティの **[ネットワーク デバイス登録サービスの URL]** として構成する必要があります。  

##### <a name="to-install-the-policy-module"></a>ポリシー モジュールをインストールするには  

1.  ネットワーク デバイス登録サービスを実行するサーバーで、ドメイン管理者としてログオンし、次のファイルを System Center Configuration Manager インストール メディアの <ConfigMgrInstallationMedia\>\SMSSETUP\POLICYMODULE\X64 フォルダーから一時フォルダーにコピーします。  

    -   PolicyModule.msi  

    -   PolicyModuleSetup.exe  

     さらに、インストール メディアのに LanguagePack フォルダーがある場合、そのフォルダーとフォルダーの内容をコピーします。  

2.  一時フォルダーから PolicyModuleSetup.exe を実行して、System Center Configuration Manager ポリシー モジュールのセットアップ ウィザードを起動します。  

3.  ウィザードの最初のページで [次へ ****] をクリックしてライセンス条項に同意し、[次へ ****] ボタンをクリックします。  

4.  [インストール先フォルダー **** ] ページで、ポリシー モジュールの既定のインストール先フォルダーをそのまま使用するか、別のフォルダーを指定し、[次へ ****] をクリックします。  

5.  [証明書登録ポイント **** ] ページで、サイト システム サーバーの FQDN と証明書登録ポイントのプロパティで指定した仮想アプリケーション名から成る、証明書登録ポイントの URL を指定します。 既定の仮想アプリケーション名は CMCertificateRegistration です。 たとえば、サイト システム サーバーの FQDN が server1.contoso.com で、既定の仮想アプリケーション名を使用した場合、「 **https://server1.contoso.com/CMCertificateRegistration**」と指定します。  

6.  [443 **** ] という既定のポートをそのまま使用するか、証明書登録ポイントが使用する別のポート番号を指定して、[次へ ****] をクリックします。  

7.  **[ポリシー モジュールのクライアント証明書]**ページで、「 **手順 1: ネットワーク デバイス登録サービスおよび依存する要素をインストールして構成する**」で展開したクライアント認証証明書を参照して指定し、 **[次へ]**をクリックします。  

8.  **[証明書登録ポイント証明書]** ページで **[参照]** をクリックし、「 **手順 2: 証明書登録ポイントをインストールおよび構成する**」の最後で見つけて保存した、ルート CA にエクスポートされた証明書ファイルを選択します。  

    > [!NOTE]  
    >  この証明書ファイルを以前に保存していない場合は、サイト サーバー コンピューターの <ConfigMgr インストール パス\>\inboxes\certmgr.box にあります。  

9. **[次へ]** をクリックして、ウィザードを完了します。  

 これでネットワーク デバイス登録サービスと依存する要素、証明書登録ポイント、および System Center Configuration Manager ポリシー モジュールをインストールする構成手順が完了しました。証明書プロファイルを作成し、展開することで、証明書をユーザーとデバイスに展開できます。 証明書プロファイルの作成方法の詳細については、「[System Center Configuration Manager で証明書プロファイルを作成する方法](../../protect/deploy-use/create-certificate-profiles.md)」を参照してください。  

 System Center Configuration Manager ポリシー モジュールをアンインストールする場合は、コントロール パネルの **[プログラムと機能]** を使用します。  



<!--HONumber=Nov16_HO1-->


