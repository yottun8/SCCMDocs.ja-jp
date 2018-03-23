---
title: "クラウド管理ゲートウェイの設定"
titleSuffix: Configuration Manager
description: 
author: arob98
ms.author: angrobe
manager: angrobe
ms.date: 09/26/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 7463cd7199098b21843fd5b99ed284a12ff91e00
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2017
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configuration Manager のクラウド管理ゲートウェイを設定する

*適用対象: System Center Configuration Manager (Current Branch)* Configuration Manager でクラウド管理ゲートウェイを設定するプロセスには、次の手順が含まれます。

## <a name="step-1-configure-required-certificates"></a>手順 1: 必要な証明書を構成する

> [!TIP]  
> 証明書を要求する前に、希望する Azure ドメイン名 (例: GraniteFalls.CloudApp.Net) が一意であることを確認します。 これを行うには、[Microsoft Azure Portal](https://manage.windowsazure.com) にログオンして、**[新規]** をクリックし、**[クラウド サービス]**、**[カスタム作成]** の順に選択します。 **[URL]** フィールドに希望するドメイン名を入力します (サービスを作成するチェックマークはクリックしないでください)。 ドメイン名が使用できるか、またはすでに別のサービスで使用されているかがポータルに表示されます。

### <a name="option-1-preferred---use-the-server-authentication-certificate-from-a-public-and-globally-trusted-certificate-provider-like-verisign"></a>オプション 1 (推奨): 一般のグローバルに信頼された証明書プロバイダー (VeriSign など) からのサーバー認証証明書を使用します。

この方式を使用する場合、クライアントは証明書を自動的に信頼することになり、管理者が自分でカスタム SSL 証明書を作成する必要はありません。

1. 組織のパブリック ドメイン ネーム サービス (DNS) に正規名レコード (CNAME) を作成して、パブリック証明書で使用されることになる、クラウド管理ゲートウェイ サービスに対するわかりやすい名前のエイリアスを作成します。
たとえば、Contoso 社では、同社のクラウド管理ゲートウェイ サービスに **GraniteFalls** という名前を付けています。Azure では、**GraniteFalls.CloudApp.Net** となります。 Contoso 社のパブリック DNS である contoso.com 名前空間内に DNS 管理者が、実際のホスト名 **GraniteFalls.CloudApp.net** に対する **GraniteFalls.Contoso.com** 用の新しい CNAME レコードを作成します。
2. 次に CNAME エイリアスの共通名 (CN) を使用してパブリック プロバイダーからのサーバー認証証明書を要求します。
たとえば、Contoso 社では、証明書の CN 用に **GraniteFalls.Contoso.com** を使用しています。
3. この証明書を使用して、Configuration Manager コンソールでクラウド管理ゲートウェイ サービスを作成します。
    - クラウド管理ゲートウェイの作成ウィザードの **[設定]** ページで、このクラウド サービスのサーバー証明書を追加するとき (**証明書ファイル**から)、ウィザードはサービス名として証明書の CN からホスト名を抽出し、**cloudapp.net** (Azure US Government クラウドの場合は **usgovcloudapp.net**) にサービスの FQDN としてこれを追加することで、Azure にサービスを作成します。
たとえば、Contoso 社でクラウド管理ゲートウェイを作成するときは、ホスト名 **GraniteFalls** が証明書の CN から抽出されます。そのため Azure での実際のサービスは **GraniteFalls.CloudApp.net** として作成されます。

### <a name="option-2---create-a-custom-ssl-certificate-for-cloud-management-gateway-in-the-same-way-as-for-a-cloud-based-distribution-point"></a>オプション 2: クラウドベースの配布ポイントで行うのと同じ方法でクラウド管理ゲートウェイのカスタム SSL 証明書を作成する

クラウド管理ゲートウェイのカスタム SSL 証明書は、クラウドベースの配布ポイントで行うのと同じ方法で作成できます。 次の操作以外は、「[クラウドベースの配布ポイント用のサービス証明書の展開](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)」の指示に従います。

- カスタムの Web サーバー証明書を要求する場合、クラウド管理ゲートウェイを Azure パブリック クラウド上で使用するときは **cloudapp.net** で終わる証明書の共通名の FQDN を入力し、Azure Government Cloud で使用するときは **usgovcloudapp.net** で終わる証明書の共通名の FQDN を入力します。


## <a name="step-2-export-the-client-certificates-root"></a>手順 2: クライアント証明書のルートをエクスポートする

ネットワークで使用されているクライアント証明書のルートをエクスポートする最も簡単な方法は、クライアント証明書を含むドメインに参加しているいずれかのコンピューター上でクライアント証明書を開いてコピーすることです。

> [!NOTE]
>
> クライアント証明書は、クラウド管理ゲートウェイで管理するコンピューター上およびクラウド管理ゲートウェイ コネクタ ポイントをホストしているサイト システム サーバー上で必要です。 これらの任意のコンピューターにクライアント証明書を追加する必要がある場合は、「[Windows コンピューター用のクライアント証明書の展開](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012)」をご覧ください。

1.  [実行] ウィンドウで、「**mmc**」を入力して Return キーを押します。

2.  [ファイル] メニューで **[スナップインの追加と削除]** を選択します。

3.  [スナップインの追加と削除] ダイアログ ボックスで、**[証明書]** > **[追加&gt;]** > **[コンピューター アカウント]** > **[次へ]** > **[ローカル コンピューター]** > **[完了]** の順に選択します。

4.  **[証明書]** &gt; **[個人用]** &gt; **[証明書]** に移動します。

5.  コンピューターでクライアント認証用の証明書をダブルクリックして、[証明のパス] タブを選択し、ルート証明機関 (パスの先頭) をダブルクリックします。

6.  [詳細] タブで、**[ファイルにコピー...]** を選択します。

7.  既定の証明書形式を使用して証明書のエクスポート ウィザードを完了します。 作成したルート証明書の名前と場所をメモします。 この情報は、[後の手順](#step-4-set-up-cloud-management-gateway)でクラウド管理ゲートウェイを構成する際に必要になります。

>[!NOTE]
>クライアント証明書が下位証明機関によって発行されている場合は、チェーン内の各証明書でこの手順を繰り返す必要があります。

## <a name="step-3-upload-the-management-certificate-to-azure"></a>手順 3: 管理証明書を Azure にアップロードする

Azure 管理証明書は、Configuration Manager が Azure API にアクセスして、クラウド管理ゲートウェイを構成するために必要です。 管理証明書をアップロードする方法の詳細と手順については、Azure のドキュメントの次の記事を参照してください。

- [Azure Cloud Services の証明書の概要](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [Azure Management API 管理証明書のアップロード](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>管理証明書に関連付けられているサブスクリプション ID を必ずコピーしてください。 これは、[次の手順](#step-4-set-up-cloud-management-gateway)で、Configuration Manager コンソールでクラウド管理ゲートウェイを構成する際に必要になります。



## <a name="step-4-set-up-cloud-management-gateway"></a>手順 4: クラウド管理ゲートウェイを設定する

>[!NOTE]
>バージョン 1610 では、クラウド管理ゲートウェイはプレリリース機能です。 有効にするには、「[更新プログラムからのプレリリース機能の使用](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)」をご覧ください。

1. Configuration Manager コンソールで、**[管理]** > **[クラウド サービス]** > **[クラウド管理ゲートウェイ]** の順に進みます。
2. **[クラウド管理ゲートウェイの作成]** を選択します。

3. クラウド管理ゲートウェイの作成ウィザードで、(Azure 管理ポータルからコピーした) Azure サブスクリプション ID を入力し、Azure の管理証明書としてアップロードする証明書ファイルを参照します。 **[次へ]** を選択し、コンソールが Azure に接続されるまでしばらく待機します。

4. ウィザードで追加の詳細を入力します。

    - Azure で実行するサービスの名前を指定します。 サービス名には英数字のみを使用し、3 文字から 24 文字の長さにする必要があります。

    - サービスを実行する Azure リージョンを選択します。

    - サービスで使用する仮想マシンの台数を指定します。 既定値は 1 ですが、サービスでは最大 16 台の仮想マシンを実行することができます。

    >[!NOTE]
    >クラウド管理ゲートウェイの接続ポイントにインターネット プロキシを使用する場合は、ポート 10124 から始めて、使用する仮想マシンの台数だけプロキシのポートの数を増やす必要があります。

    - カスタム SSL 証明書からエクスポートした秘密キー (.pfx ファイル) を指定します。

    - クライアント証明書からエクスポートしたルート証明書 (および下位証明書) を指定します。 ウィザードには、最大で 2 つのルート証明書と 4 つの下位証明書を指定できます。

    -   新しい証明書テンプレートを作成するときに使用したのと同じサービス名の FQDN を指定します。 使用している Azure クラウドに基づいて、FQDN サービス名の次のサフィックスのいずれかを指定する必要があります。

    Azure クラウド | FQDN のサフィックス
    --------------|-------------
    パブリック (商用) クラウド | .cloudapp.net    
    政府のクラウド | .usgovcloudapp.net

  - **[クライアント証明書の失効状態を検証する]** の横のボックスをオフにします (CRL 情報をパブリックに発行している場合を除く)。

  - 完了したら、**[次へ]** を選択します。

5. クラウド管理ゲートウェイ トラフィックを 14 日間のしきい値で監視する場合は、チェック ボックスをオンにしてしきい値のアラートを有効にします。 次に、しきい値と、別のアラート レベルを上げる割合を指定します。 完了したら、**[次へ]** を選択します。

6. 設定を確認して、**[次へ]** を選択します。 Configuration Manager がサービスの設定を開始します。 ウィザードを閉じた後に、Azure でサービスが完全にプロビジョニングされるまで 5 分から 15 分かかります。 新しいクラウド管理ゲートウェイの **[状態]** 列を確認して、サービスの準備が完了するタイミングを判断します。

## <a name="step-5-configure-primary-site-for-client-certification-authentication"></a>手順 5: クライアント証明書の認証用にプライマリ サイトを構成する

1. Configuration Manager コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** の順に移動します。

2. クラウド管理ゲートウェイを使用して管理するクライアントのプライマリ サイトを選択し、**[プロパティ]** を選択します。

3. プライマリ サイトのプロパティ シートの 「Client Computer Communications」 (クライアント コンピューターの通信方法) タブで、**「使用可能な場合は PKI クライアント証明書 (クライアント認証機能) を使用する」** をオンにします。

4. **[サイト システムの証明書失効リスト (CRL) をチェックする]** がオフになっていることを確認します。 このオプションは、CRL をパブリックに公開した場合にのみ必要になります。


## <a name="step-6-add-the-cloud-management-gateway-connector-point"></a>手順 6: クラウド管理ゲートウェイ コネクタ ポイントを追加する

クラウド管理ゲートウェイ コネクタ ポイントは、クラウド管理ゲートウェイと通信するための新しいサイト システムの役割です。 クラウド管理ゲートウェイ コネクタ ポイントを追加するには、「[System Center Configuration Manager のサイト システム役割の追加](/sccm/core/servers/deploy/configure/add-site-system-roles)」の手順に従います。

## <a name="step-7-configure-roles-for-cloud-management-gateway-traffic"></a>手順 7: クラウド管理ゲートウェイ トラフィック向けに役割を構成する

クラウド管理ゲートウェイを設定する最後のステップは、クラウド管理ゲートウェイ トラフィックを受け入れるサイト システムの役割を構成することです。 クラウド管理ゲートウェイでは、管理ポイントとソフトウェアの更新ポイントの役割のみがサポートされています。 各役割を個別に構成します。

1. Configuration Manager コンソールで、**[管理]** > **[サイトの構成]** > **[サーバーとサイト システムの役割]** の順に移動します。

2. クラウド管理ゲートウェイ トラフィック向けに構成する役割のサイト システム サーバーを選択します。

3. 役割を選択し、**[プロパティ]** を選択します。

4. 役割のプロパティ シートの [クライアント接続] で、**[Configuration Manager のクラウド管理ゲートウェイ トラフィックを許可する]** の横のチェック ボックスをオンにして **[OK]** を選択します。 残りの役割にこれらの手順を繰り返します。 セキュリティのベスト プラクティスとして、**HTTPS** オプションを有効にすることもお勧めしますが、必須ではありません。

## <a name="step-8-configure-clients-for-cloud-management-gateway"></a>手順 8: クラウド管理ゲートウェイ向けにクライアントを構成する

クラウド管理ゲートウェイおよびサイト システムの役割が構成され実行されると、次回の場所の要求で、クライアントがクラウド管理ゲートウェイ サービスの場所を自動的に取得します。 クラウド管理ゲートウェイ サービスの場所を受信するには、クライアントは企業ネットワーク上にある必要があります。 場所の要求のポーリング サイクルは 24 時間ごとです。 通常にスケジュール設定された場所の要求を待機したくない場合は、コンピューターで SMS Agent Host サービス (ccmexec.exe) を再起動することによって、要求を強制できます。

クライアントは、クライアントで構成されたクラウド管理ゲートウェイ サービスの場所から、イントラネットまたはインターネット上のいずれにあるかを自動的に判別できます。 クライアントがドメイン コントローラーまたはオンプレミスの管理ポイントに接続できる場合は、Configuration Manager との通信にこれらを使用します。 それ以外の場合は、インターネット上にあると見なして、クラウド管理ゲートウェイ サービスの場所を通信に使用します。

>[!NOTE]
> クライアントがイントラネットまたはインターネット上のどちらにあるかにかかわらず、クラウド管理ゲートウェイを常に使用するように強制することができます。 このためには、クライアント コンピューターで次のレジストリ キーを設定します。
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`

クライアントが Configuration Manager に接続できることを確認するには、クライアント コンピューターで次の PowerShell コマンドを実行します。

`gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate`

このコマンドによって、クラウド管理ゲートウェイ サービスを含む、クライアントが接続できる管理ポイントが表示されます。

## <a name="next-steps"></a>次のステップ

[クラウド管理ゲートウェイのクライアントの監視](monitor-clients-cloud-management-gateway.md)
