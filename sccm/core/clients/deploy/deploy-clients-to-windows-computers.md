---
title: "Windows クライアントの展開 | Microsoft Docs"
description: "System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法を説明します。"
ms.custom: na
ms.date: 08/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
caps.latest.revision: "13"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: f03102c170e1e7de3a11349f4a66380c4291dcac
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2017
---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager クライアントをインストールする前に、すべての[前提条件](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)を満たしており、必要なすべての展開構成を完了していることを確認します。   

##  <a name="BKMK_ClientPush"></a> クライアント プッシュを使用したクライアントのインストール方法  

クライアント プッシュ インストールはサイトに対して構成でき、サイトの境界が境界グループとして構成されている場合、クライアント インストールはこれらの構成済みの境界内で検出されたコンピューターで自動的に実行されます。 特定のコレクションまたはコレクション内のリソースでクライアント プッシュ インストール ウィザードを実行して、クライアント プッシュ インストールを開始することもできます。  

また、クライアント プッシュ インストール ウィザードを使用して、[クエリ](../../../core/servers/manage/queries-technical-reference.md)の結果に Configuration Manager クライアントをインストールすることもできます。 インストールが成功するには、クエリで返されるいずれかのアイテムが、クラス **System Resource** からの属性 **ResourceID** である必要があります。   

サイト サーバーがクライアント コンピューターにアクセスできない場合やセットアップ プロセスを開始できない場合は、自動的に最大 7 日間、1 時間置きにインストールが試みられます。  

クライアントのインストール プロセスを追跡するには、クライアントをインストールする前に、フォールバック ステータス ポイント サイト システムをインストールします。 インストールしたフォールバック ステータス ポイントは、クライアント プッシュ インストール方法でクライアントをインストールするときに、自動的にクライアントに割り当てられます。 クライアントのインストールの進行状況は、クライアント展開レポートとクライアントの割り当てレポートで確認します。 

クライアント ログ ファイルにはトラブルシューティングに役立つ詳しい情報が記録されるため、フォールバック ステータス ポイントは必要ありません。 たとえば、サイト サーバー上の CCM.log ファイルには、サイト サーバーがコンピューターに接続するときに発生したすべての問題が記録され、クライアント上の CCMSetup.log ファイルには、インストール プロセスが記録されます。  

> [!IMPORTANT]  
>  クライアント プッシュが正常に実行されるように、前提条件がすべて満たされていることを確認してください。 その一覧は、「[System Center Configuration Manager で Windows コンピューターにクライアントを展開するための前提条件](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)」の「インストール方法の依存関係」というセクションに示されています。  

### <a name="to-configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>検出されたコンピューターに対して、サイトが自動的にクライアント プッシュ インストールを使用するように構成するには

1.  Configuration Manager コンソールで、[**管理**] > [**サイトの構成**] > [**サイト**] の順に選択します。  

3.  サイト全体の自動クライアント プッシュ インストールを構成するサイトを選択します。  

4.  [**ホーム**] タブの [**設定**] グループで、[**クライアント インストール設定**] > [**クライアント プッシュ インストール**] の順にクリックします。  

5.  [**クライアント プッシュ インストールのプロパティ**] ダイアログ ボックスの [**全般**] タブで、[**サイト全体にクライアントを自動的にプッシュ インストールする**] を選択します。 Configuration Manager でクライアント ソフトウェアをプッシュするシステムの種類を選択します。  

6.  ドメイン コント ローラーにクライアントをインストールするかどうかを選択します。  

7.  **[アカウント]** タブで、クライアント ソフトウェアをインストールするためにコンピューターに接続するときに Configuration Manager が使用するアカウントを 1 つまたは複数指定します。 [**作成**] アイコンをクリックし、[**ユーザー名**] と 「**パスワード**」 (38 文字以内) を入力して、パスワードを確認入力してから、[**OK**] をクリックします。 少なくとも 1 つのクライアント プッシュ インストール アカウントを指定する必要があります。このアカウントは、クライアントをインストールするすべてのコンピューターのローカル管理者権限を持っている必要があります。 クライアント プッシュ インストール アカウントを指定しないと、Configuration Manager はサイト システムのコンピューター アカウントを使おうとします。これにより、ドメイン間のクライアント プッシュが失敗します。  
    > [!NOTE]  
    >  クライアント プッシュ インストール方法をセカンダリ サイトから使用する場合、クライアント プッシュを開始するセカンダリ サイトでアカウントを指定する必要があります。  
    >   
    >  クライアント プッシュ インストール アカウントの詳細については、次の手順「クライアント プッシュ インストール ウィザードを使用するには」をご覧ください。  
8.  [**インストールのプロパティ**] タブを完了します。

     スキーマが Configuration Manager 向けに拡張されており、インストール プロパティを指定せずに CCMSetup を実行するクライアント インストールで読み取られる場合は、このタブで指定した[クライアント インストール プロパティ](../../../core/clients/deploy/about-client-installation-properties.md)は、Active Directory Domain Services に発行されます。  

    > [!NOTE]  
    >  セカンダリ サイトでクライアント プッシュ インストールを有効にする場合は、SMSSITECODE プロパティがその親プライマリ サイトの Configuration Manager サイト名に設定されていることを確認してください。 Active Directory スキーマが Configuration Manager 用に拡張されている場合は、これを AUTO を設定して、正しいサイトの割り当てを自動的に検索することもできます。  

### <a name="to-use-the-client-push-installation-wizard"></a>クライアント プッシュ インストール ウィザードを使用するには

1.  Configuration Manager コンソールで、[**管理**] >  [**サイトの構成**] > [**サイト**] の順に選択します。  

3.  サイト全体の自動クライアント プッシュ インストールを構成するサイトを選択します。  

4.  [**ホーム**] タブの [**設定**] グループで、[**クライアント インストール設定**] > [**クライアント プッシュ インストール**] の順にクリックします。  

5.  [**インストールのプロパティ**] タブを完了します。  

     スキーマが Configuration Manager 向けに拡張されており、インストール プロパティを指定せずに CCMSetup を実行するクライアント インストールで読み取られる場合は、このタブで指定した[クライアント インストール プロパティ](../../../core/clients/deploy/about-client-installation-properties.md)は、Active Directory Domain Services に発行されます。  

6.  Configuration Manager コンソールで、**[資産とコンプライアンス]** を選択します。  

7.  [**資産とコンプライアンス**] ワークスペースで、1 つ以上のコンピューター、またはコンピューターのコレクションを選択します。  

8.  [**ホーム**] タブで、次のいずれかを選択します。  

    -   単一のコンピューターまたは複数のコンピューターにクライアントをインストールする場合は、[**デバイス**] グループで [**クライアントのインストール**] を選択します。  

    -   コンピューターのコレクションにクライアントをインストールする場合は、[**コレクション**] グループで [**クライアントのインストール**] を選択します。  

9. **クライアントのインストール ウィザード**の [**開始する前に**] ページで情報を確認してから、[**次へ**] を選択します。  

10. [**インストール オプション**] ページを完了します。  

11. インストール設定を確認してから、ウィザードを閉じます。  

> [!NOTE]  
>  サイトがクライアント プッシュ用に構成されていない場合でも、ウィザードを使用してクライアントをインストールできます。  

##  <a name="BKMK_ClientSUP"></a> ソフトウェアの更新に基づいたインストールを使用したクライアントのインストール方法  
 ソフトウェアの更新に基づいたクライアント インストールでは、クライアントをソフトウェア更新プログラムとしてソフトウェアの更新ポイントに発行します。 初回のインストールまたはアップグレードには、この方法を使用します。  

 コンピューターに Configuration Manager クライアントがインストールされている場合は、Configuration Manager により、ソフトウェア更新プログラムを取得するソフトウェアの更新ポイントのサーバー名とポートを含むクライアント ポリシーがクライアントに提供されます。   

> [!IMPORTANT]  
>  ソフトウェアの更新に基づいたインストールを使用するには、クライアントのインストールとソフトウェア更新プログラムに同じ Windows Server Update Services (WSUS) サーバーを使用する必要があります。 このサーバーは、プライマリ サイトでアクティブなソフトウェアの更新ポイントである必要があります。 詳細については、「[Install a software update point](../../../sum/get-started/install-a-software-update-point.md)」 (ソフトウェアの更新ポイントのインストール) をご覧ください。  

コンピューターに Configuration Manager クライアントがインストールされていない場合は、ソフトウェアの更新ポイントのサーバー名を指定するように Active Directory Domain Services のグループ ポリシー オブジェクト (GPO) を構成して割り当てる必要があります。  

ソフトウェアの更新に基づいたクライアント インストールに、コマンド ライン プロパティを追加することはできません。 Configuration Manager 用に Active Directory スキーマを拡張した場合、クライアント コンピューターはインストール時に、自動的に Active Directory Domain Services にインストール プロパティを照会します。  

Active Directory スキーマを拡張していない場合は、グループ ポリシーを使用して、サイト内のコンピューターにクライアント インストール設定をプロビジョニングできます。 これらの設定は、ソフトウェアの更新に基づいたクライアント インストールに自動的に適用されます。 詳細については、「[クライアント インストールのプロパティの準備方法 (グループ ポリシーおよびソフトウェア更新ベースのクライアント インストール)](#BKMK_Provision)」および「[System Center Configuration Manager でクライアントをサイトに割り当てる方法](../../../core/clients/deploy/assign-clients-to-a-site.md)」を参照してください。  

Configuration Manager クライアントがインストールされていないコンピューターで、次の手順に従って、ソフトウェアの更新ポイントを使用してクライアントのインストールやソフトウェアの更新を行ったり、クライアントをソフトウェアの更新ポイントに発行したりするように構成します。  

> [!NOTE]  
>  コンピューターが前のソフトウェアのインストールの後に保留中の再起動の状態になると、ソフトウェア更新ベースのクライアント インストールによってコンピューターが再起動する可能性があります。  

### <a name="configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>クライアントのインストールおよびソフトウェア更新プログラム用のソフトウェアの更新ポイントを指定するように、Active Directory Domain Services のグループ ポリシー オブジェクトを構成するには  

1.  グループ ポリシー管理コンソールを使用して、新規または既存のグループ ポリシー オブジェクトを開きます。  

2.  コンソールで、[**コンピューターの構成**]、[**管理用テンプレート**]、[**Windows コンポーネント**] の順に展開し、[**Windows Update**] を選択します。  

3.  設定 [**イントラネットの Microsoft 更新サービスの場所を指定する**] のプロパティを開いてから、[**有効**] を選択します。  

4.  [**更新を検出するためのイントラネットの更新サービスを設定する**] ボックスで、ソフトウェアの更新ポイントのサーバー名とポートを指定します。  

    -   Configuration Manager サイト システムが完全修飾ドメイン名 (FQDN) を使用するように構成されている場合は、FQDN 形式を使用します。  

    -   Configuration Manager サイト システムが完全修飾ドメイン名 (FQDN) を使用するように構成されていない場合は、短い名前の形式を使用します。  

    > [!NOTE]  
    >  ポート番号を特定するには、「[System Center Configuration Manager において、WSUS で使用するポート設定を特定する方法](../../../sum/plan-design/plan-for-software-updates.md)」を参照してください。  

     例: **http://server1.contoso.com:8530**  

5.  [**イントラネット統計サーバーの設定**] ボックスで、イントラネット統計サーバーの名前を指定します。 このサーバーは、ソフトウェアの更新ポイント サーバーと同じである必要はありません。また、ソフトウェアの更新ポイントと同じサーバーである場合は、形式が一致しなくてもかまいません。  

6.  クライアントのインストール先とし、ソフトウェア更新プログラムを受け取るコンピューターに、グループ ポリシー オブジェクトを割り当てます。  

### <a name="to-publish-the-configuration-manager-client-to-the-software-update-point"></a>構成マネージャー クライアントをソフトウェアの更新ポイントに発行するには  

1.  Configuration Manager コンソールで、[**管理**] > [**サイトの構成**] > [**サイト**] の順にクリックします。  

3.  ソフトウェアの更新に基づいたクライアントのインストールを構成するサイトを選択します。  

4.  [**ホーム**] タブの [**設定**] グループで、[**クライアント インストール設定**] を選択し、[**ソフトウェアの更新に基づいたクライアントのインストール**] を選択します。  

5.  [**ソフトウェアの更新に基づいたクライアントのインストールを有効にする**] を選択します。  

6.  Configuration Manager サイト サーバー上のクライアント ソフトウェアのバージョンが、ソフトウェアの更新ポイントにあるクライアントのバージョンよりも新しい場合、**[新しいバージョンのクライアント パッケージが見つかりました]** ダイアログ ボックスが開きます。 [**はい**] をクリックして、最新バージョンを発行します。  

    > [!NOTE]  
    >  クライアント ソフトウェアがソフトウェアの更新ポイントに発行されていない場合、このボックスは空白になります。  

構成マネージャー クライアント用のソフトウェア更新プログラムは、新しいバージョンが存在する場合に自動的に更新されるわけではありません。 新しいクライアント バージョンが含まれるようにサイトをアップグレードするには、手順 6 でこの手順を繰り返して [**はい**] をクリックする必要があります。  

##  <a name="BKMK_ClientGP"></a> グループ ポリシーを使用したクライアントのインストール方法  
 Active Directory Domain Services のグループ ポリシーを使用して、企業内のコンピューターにインストールするように構成マネージャー クライアントを割り当てたり、発行したりできます。 クライアントは、コンピューターの起動時にインストールされます。 グループ ポリシーを使用すると、コントロール パネルの [**プログラムの追加と削除**] ダイアログ ボックスにクライアントが表示され、ユーザーがインストールできるようになります。  

 グループ ポリシーに基づいたインストールには、Windows インストーラー パッケージ (CCMSetup.msi) を使用します。 このファイルは、Configuration Manager サイト サーバーの **&lt;ConfigMgr インストール ディレクトリ\>\bin\i386** フォルダーにあります。 このファイルにプロパティを追加してインストールの動作を変更することはできません。  

> [!IMPORTANT]  
>  クライアント インストール ファイルにアクセスするためには、管理者権限を持っている必要があります。  

-   Active Directory スキーマが Configuration Manager 用に拡張されており、**[サイトのプロパティ]** ダイアログ ボックスの **[詳細設定]** タブで **[Active Directory Domain Services 内にこのサイトを発行する]** が選択されている場合、クライアント コンピューターは自動的に Active Directory Domain Services でインストール プロパティを検索します。 発行されるインストール プロパティの詳細については、「[System Center Configuration Manager で Active Directory Domain Services に発行されたクライアント インストールのプロパティについて](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)」を参照してください。  

-   Active Directory スキーマが拡張されていない場合は、このトピックの手順 ([クライアント インストールのプロパティの準備方法 (グループ ポリシーおよびソフトウェア更新ベースのクライアント インストール)](#BKMK_Provision)) を使用して、コンピューターのレジストリ内にインストール プロパティを格納できます。 これらのインストール プロパティは、クライアントのインストール時に使用されます。  

Active Directory Domain Services のグループ ポリシーを使用してソフトウェアをインストールする方法については、Windows Server のドキュメントを参照してください。  

##  <a name="BKMK_Manual"></a> クライアントの手動インストール方法  
 CCMSetup.exe プログラムを使用して、企業内のコンピューターにクライアント ソフトウェアを手動でインストールできます。 このプログラムとそのサポート ファイルは、サイト サーバー上の Configuration Manager インストール フォルダーの **Client** フォルダーおよびサイトの管理ポイントにあります。 このフォルダーは次のようにネットワークで共有されます。  

 \\\\*&lt;サイト サーバー名\>*\SMS_*&lt;サイト コード\>*\Client\  

 ここで *&lt;サイト サーバー名\>* は管理ポイントをホストするいずれかのサーバーの名前、*&lt;サイト コード\>* はクライアントが属するプライマリ サイトのコードです。  クライアントでコマンド ラインから CCMSetup.exe を実行するには、この場所にネットワーク ドライブをマップしてからコマンドを実行する必要があります。  

> [!IMPORTANT]  
>  クライアント インストール ファイルにアクセスするためには、管理者権限を持っている必要があります。  

 CCMSetup.exe は、必要なすべての前提条件をクライアント コンピューターにコピーし、Windows インストーラー パッケージ (Client.msi) を呼び出してクライアントをインストールします。 Client.msi を直接実行することはできません。  

 CCMSetup.exe および Client.msi の両方にコマンド ライン プロパティを指定して、クライアント インストールの動作を変更できます。 Client.msi のプロパティを指定する前に、CCMSetup のプロパティ (先頭が **/** のプロパティ) を指定する必要があります。 たとえば、  

```  
CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01  
```  
次のプロパティを使用して、クライアント インストールを指定します。  

|プロパティ|説明|  
|--------------|-----------------|  
|**/mp:SMSMP01**|CCMSetup のこのプロパティで、必要なクライアント インストール ファイルをダウンロードする管理ポイント SMSMP01 を指定します。|  
|**/logon**|CCMSetup のこのプロパティで、既存の構成マネージャー クライアントがコンピューターで見つかった場合はインストールを停止するように指定します。|  
|**SMSSITECODE=AUTO**|Client.msi のこのプロパティで、たとえば Active Directory Domain Services を使用して、使用する Configuration Manager サイト コードをクライアントが特定するように指定します。|  
|**FSP=SMSFP01**|Client.msi のこのプロパティで、SMSFP01 というフォールバック ステータス ポイントを使用して、クライアント コンピューターから送信される状態メッセージを受信するように指定します。|  

 すべての CCMSetup.exe プロパティの詳細については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」を参照してください  

### <a name="examples"></a>例
 これらの例は、イントラネット上の Active Directory クライアントを対象としており、次の値を使用してサイトのさまざまな側面を表しています。  

 **MPSERVER** = 管理ポイントをホストするサーバー   
**FSPSERVER** = フォールバック ステータス ポイントをホストするサーバー  
**ABC** = サイト コード  
**contoso.com** = ドメイン名  

 すべてのサイト システム サーバーはイントラネットの FQDN で構成され、サイトはクライアントの Active Directory フォレストに発行されます。  

 クライアント コンピューターで、ローカル管理者としてログオンします。ドライブ (z:) を \\\MPSERVER\SMS_ABC\Client にマップして、コマンド プロンプトを z ドライブに切り替えてから、次のいずれかのコマンドを実行します。  

 **例 1:**  

```  
CCMSetup.exe  
```  
この例では、Active Directory Domain Services に発行されたクライアント インストール プロパティを使ってクライアントが自動的に構成されるように、追加のプロパティを指定せずにクライアントをインストールしています。 たとえば、クライアントにサイト コード (クライアントのネットワークの場所を、クライアントの割り当て用に構成された境界グループ内に含める必要があります)、管理ポイント、およびフォールバック ステータス ポイントが自動的に構成され、クライアントが HTTPS のみを使用して通信する必要があるかどうかも自動的に構成されます。 Active Directory クライアント用に自動構成できるクライアント インストール プロパティの詳細については、「[System Center Configuration Manager で Active Directory Domain Services に発行されたクライアント インストールのプロパティについて](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)」を参照してください。  

 **例 2:**  

```  
CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com  
```  
この例では、Active Directory Domain Services で提供される自動構成を上書きしており、クライアントのネットワークの場所がクライアントの割り当て用に構成された境界グループに含まれている必要はありません。 代わりに、インストールで、サイト、イントラネットの管理ポイントとインターネットベースの管理ポイント、インターネットからの接続を受け入れるフォールバック ステータス ポイント、および有効期限の最も長い、使用するクライアント PKI 証明書 (使用可能な場合) を指定しています。  

##  <a name="BKMK_ClientLogonScript"></a> ログオン スクリプトを使用したクライアントのインストール方法  
 Configuration Manager では、構成マネージャー クライアント ソフトウェアをインストールするログオン スクリプトをサポートしています。 **CCMSetup.exe** プログラム ファイルをログオン スクリプトで使用して、クライアント インストールを開始できます。  

 ログオン スクリプト インストールの使用方法は、手動のクライアント インストールと同じです。 CCMSsetup.exe に **/logon** インストール プロパティを指定して、既にクライアントがコンピューターに存在する場合は、クライアントをインストールしないようにすることができます。 これにより、ログオン スクリプトが実行されるたびにクライアントの再インストールが発生することはなくなります。  

 **/Source** プロパティを使用しているインストール ソースが指定されておらず、インストールの取得元となる管理ポイントが **/MP** プロパティを使用して指定されていない場合に、Configuration Manager 用にスキーマが拡張されており、サイトが Active Directory Domain Services に発行されていれば、CCMSetup.exe は Active Directory Domain Services を検索して管理ポイントを特定できます。 または、クライアントが DNS または WINS を使用して管理ポイントを特定することもできます。  

##  <a name="BKMK_ClientApp"></a> パッケージとプログラムを使用したクライアントのインストール方法  
 Configuration Manager を使用し、階層内の選択したコンピューターのクライアント ソフトウェアをアップグレードするパッケージとプログラムを作成して展開できます。 Configuration Manager には、通常使用される値をパッケージ プロパティに適用する、パッケージ定義ファイルが付属しています。 追加のコマンド ライン プロパティを指定することで、クライアント インストールの動作をカスタマイズできます。  

> [!NOTE]  
>  この方法では、Configuration Manager 2007 クライアントをアップグレードすることはできません。 代わりに、最新バージョンのクライアントが含まれたパッケージを自動的に作成して展開する自動クライアント アップグレードを使用します。 詳細については、「[System Center Configuration Manager でのクライアントのアップグレード](../../../core/clients/manage/upgrade/upgrade-clients.md)」を参照してください。  
>   
>  旧バージョンの構成マネージャー クライアントから移行する方法について、詳しくは「[System Center Configuration Manager でのクライアント移行戦略の計画](../../../core/migration/planning-a-client-migration-strategy.md)」をご覧ください。  

 
###<a name="to-create-a-package-and-program-for-the-client-software"></a>クライアント ソフトウェア用のパッケージとプログラムを作成するには  

次の手順に従って、クライアント ソフトウェアをアップグレードするために構成マネージャー クライアント コンピューターに展開できる、Configuration Manager パッケージとプログラムを作成します。  

1.  Configuration Manager コンソールで、[**ソフトウェア ライブラリ**] > [**アプリケーション管理**] > [**パッケージ**] の順に選択します。  

3.  [**ホーム**] タブの [**作成**] グループで、[**定義に基づいたパッケージの作成**] を選択します。  

4.  ウィザードの [**パッケージの定義**] ページで、[**発行元**] ドロップダウン リストから [**Microsoft**] を選択し、[**パッケージ定義**] の一覧から [**Configuration Manager クライアントのアップグレード**] を選択します。  

5.  [**ソース ファイル**] ページで、[**常にソース フォルダーからファイルを取得する**] を選択します。  

6.  [**ソース フォルダー**] ページで、[**ネットワーク パス (UNC 名)**] を選択し、クライアント インストール ファイルが含まれているコンピューターとフォルダーへのネットワーク パスを入力します。  

    > [!NOTE]  
    >  Configuration Manager の展開を実行するコンピューターが、指定したネットワーク フォルダーへのアクセス権を持っている必要があります。持っていない場合、インストールは失敗します。  

    クライアント インストールのプロパティを変更する場合は、[**Configuration Manager エージェントのサイレント アップグレードのプロパティ**] プログラム ダイアログ ボックスの [**全般**] タブで CCMSetup.exe コマンド ライン パラメーターを変更できます。 既定のインストール プロパティは、 **/noservice SMSSITECODE=AUTO**です。  

9. クライアント アップグレード パッケージをホストする必要があるすべての配布ポイントにパッケージを配布します。 次に、アップグレードが必要なクライアントが含まれているコンピューターのコレクションにパッケージを展開できます。  

## <a name="how-to-install-clients-to-intune-mdm-managed-windows-devices"></a>Intune に登録されている MDM 管理対象 Windows デバイスへのクライアントのインストール方法

Microsoft Intune に登録されているコンピューターにクライアントのインストール ファイルを展開できます。 

クライアント ソフトウェアをインストールした後に、デバイスが管理状態にあることを確認するには、デバイスが企業ネットワーク上にあり、Configuration Manager サイトの境界内にある必要があります。 

> [!NOTE]
> クライアント ソフトウェアがインストールされると、デバイスが Intune から登録されます。

### <a name="to-install-clients-with-intune"></a>Intune を使用してクライアントをインストールするには

1. Intune で、構成マネージャー クライアントのインストール ファイル **ccmsetup.msi** を含む、[アプリを作成](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune)します。

2. ソフトウェア パブリッシャーでは、次のコマンド ラインのパラメーターを使用します。

  **CCMSETUPCMD="/MP:&lt;管理ポイントの FQDN> SMSMP=&lt;管理ポイントの FQDN> SMSSITECODE=&lt;サイト コード> DNSSUFFIX=&lt;管理ポイントの DNS サフィックス>"**

3. 登録済みの Windows コンピューターに[アプリを展開](/intune/deploy-use/deploy-apps-in-microsoft-intune)します。

##  <a name="BKMK_ClientImage"></a> コンピューター イメージングを使用したクライアントのインストール方法  
他のコンピューターをイメージ化するために使用するマスター イメージ コンピューターに Configuration Manager クライアント ソフトウェアをプレインストールできます。   

### <a name="to-prepare-the-client-computer-for-imaging"></a>クライアント コンピューターのイメージングを準備するには  

1.  マスター イメージ コンピューターに構成マネージャー クライアント ソフトウェアを手動でインストールします。 詳細については、「[Configuration Manager クライアントの手動インストール方法](#BKMK_Manual)」をご覧ください。  

    > [!IMPORTANT]  
    >  CCMSetup.exe コマンド ライン プロパティでクライアントに Configuration Manager サイト コードを指定しないでください。  

2.  コマンド プロンプトで「**net stop ccmexec**」と入力して、 **SMS Agent Host** サービス (Ccmexec.exe) がマスター イメージ コンピューターで実行されていないことを確認します。
3.  参照コンピューターの **Windows** フォルダーから、ファイル **SMSCFG.INI** を削除します。  
3.  マスター イメージ コンピューターのローカル コンピューター ストアに保存されている証明書を削除します。  たとえば、公開キー基盤 (PKI) 証明書を使用する場合、コンピューターをイメージ化する前に、[**コンピューター**] と [**ユーザー**] の [**個人用**] ストアの証明書を削除する必要があります。

4.  クライアントをマスター イメージ コンピューターとは別の Configuration Manager 階層にインストールする場合は、信頼されたルート キーをマスター イメージ コンピューターから削除します。  
    > [!NOTE]  
    >  クライアントは、Active Directory Domain Services に管理ポイントを照会できない場合、信頼されたルート キーを使用して信頼された管理ポイントを特定します。 イメージングされたすべてのクライアントをマスター コンピューターと同じ階層に展開する場合は、信頼されたルート キーを所定の場所に残しておきます。 クライアントを別の階層に展開する場合、信頼されたルート キーを削除し、ベスト プラクティスとして、これらのクライアントに信頼されたルート キーを事前準備することをお勧めします。 詳細については、「[Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)」を参照してください。 

5.  イメージング ソフトウェアを使用して、マスター コンピューターのイメージをキャプチャします。  

6.  イメージを対象コンピューターに展開します。  

##  <a name="BKMK_ClientWorkgroup"></a> ワークグループ コンピューターへのクライアントのインストール方法  
 Configuration Manager は、ワークグループ内のコンピューターへのクライアント インストールをサポートします。 「[Configuration Manager クライアントの手動インストール方法](#BKMK_Manual)」で指定された方法を使用して、ワークグループ コンピューターにクライアントをインストールします。  

 必要条件:  

-   クライアントは、各ワークグループ コンピューターに手動でインストールする必要があります。 インストール時に、ログオン ユーザーはローカル管理者権限を持っている必要があります。  

-   Configuration Manager サイト サーバー ドメイン内のリソースにアクセスするには、このサイト用にネットワーク アクセス アカウントを構成する必要があります。 このアカウントをソフトウェアの配布コンポーネントのプロパティとして指定します。 詳細については、「[Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md)」をご覧ください。  

 制限事項:  

-   ワークグループ クライアントは、Active Directory Domain Services から管理ポイントを特定できません。代わりに、DNS、WINS、または別の管理ポイントを使用する必要があります。  

-   クライアントは、Active Directory Domain Services にサイト情報を照会できないので、グローバル ローミングはサポートされません。  

-   Active Directory 探索方法では、ワークグループ内のコンピューターを探索できません。  

-   ワークグループ コンピューターのユーザーにソフトウェアを展開することはできません。  

-   クライアント プッシュ インストール方法を使用して、ワークグループ コンピューターにクライアントをインストールすることはできません。  

-   ワークグループ クライアントの場合は、認証に Kerberos を使用できないので、手動の承認が必要です。  

-   ワークグループ クライアントは、配布ポイントとして構成できません。 Configuration Manager では、配布ポイントであるコンピューターがドメインのメンバーに指定されている必要があります。  

### <a name="to-install-the-client-on-workgroup-computers"></a>ワークグループ コンピューターにクライアントインストールするには  

前提条件を確認し、セクション「[Configuration Manager クライアントの手動インストール方法](#BKMK_Manual)」の指示に従います。  

   この例では、イントラネットのクライアント管理用のクライアントをインストールし、サイト コードと DNS サフィックスを指定して管理ポイントを検索しています。`**CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com**`  

     

   この例では、サイトの自動割り当てが成功するように、境界グループ内に構成されたネットワークの場所にクライアントを配置する必要があります。 クライアントの展開を追跡すると共に、クライアントの通信の問題を特定できるように、コマンドにサーバー FSPSERVER のフォールバック ステータス ポイントを含めています。`**CCMSetup.exe FSP=fspserver.constoso.com**`  

      

##  <a name="BKMK_ClientInternet"></a> インターネット ベースのクライアント管理用クライアントのインストール方法  
 Configuration Manager サイトが、イントラネット上にある場合とインターネット上にある場合があるクライアントに対してインターネットベースのクライアント管理をサポートするときは、次の 2 つの方法のいずれかを使用して、イントラネット上のクライアントをインストールできます。  

-   たとえば、手動インストールやクライアント プッシュを使ってクライアントをインストールするときには、CCMHOSTNAME=*&lt;インターネットベースの管理ポイントのインターネット FQDN\>* という Client.msi プロパティを含めることができます。 この方法を使用するときには、クライアントをサイトに直接割り当てる必要があります。また、サイトの自動割り当ては使用できません。 このトピックの「[Configuration Manager クライアントの手動インストール方法](#BKMK_Manual)」セクションに、この構成方法の例を示します。  

-   イントラネットのクライアント管理用にクライアントをインストールしてから、コントロール パネルで構成マネージャー クライアントのプロパティを使用するかスクリプトを使用して、インターネット ベースのクライアント管理ポイントをクライアントに割り当てることができます。 この方法を使用するときに、自動クライアント割り当てを使用できます。 詳細については、このトピックの「[クライアント インストール後のインターネットベースのクライアント管理用のクライアント構成方法](#BKMK_ConfigureIBCM_MP)」セクションを参照してください。  

 クライアントがインターネットのみのクライアントであるか、またはイントラネットに戻る前にクライアントをインストールする必要があるために、インターネット上のクライアントをインストールする必要がある場合は、次のサポートされる方法のいずれかを選択します。  

-   仮想プライベート ネットワーク (VPN) を使用してこれらのクライアントが一時的にイントラネットに接続し、適切なクライアント インストール方法を使用してクライアントをインストールするメカニズムを提供します。  

-   リムーバブル メディアにクライアント インストール ソース ファイルをパッケージ化し、インストールするユーザーに指示と共に送るなど、Configuration Manager に依存しないインストール方法を使用します。 クライアント インストール ソース ファイルは、Configuration Manager サイト サーバーおよび管理ポイントの*&lt;インストール パス\>*\Client フォルダーにあります。 クライアント フォルダー経由とこのフォルダーから手動でコピーし、CCMSetup.exe と適切なすべての CCMSetup コマンド ライン プロパティを使用して、クライアントを手動でインストールするためのスクリプトをメディアに含めます。  

> [!NOTE]  
>  Configuration Manager では、インターネット ベースの管理ポイントまたはインターネット ベースのソフトウェア更新ポイントからクライアントを直接インストールすることはサポートしていません。  

 インターネット経由で管理されるクライアントはインターネット ベースのサイト システムと通信する必要があるため、インストールする前に、これらのクライアントに公開キー基盤 (PKI) 証明書がインストールされていることを確認します。 これらの証明書は Configuration Manager とは別にインストールする必要があります。 証明書の要件の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../../core/plan-design/network/pki-certificate-requirements.md)」を参照してください。  

### <a name="to-install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>CCMSetup コマンドライン プロパティを指定してインターネット上のクライアントをインストールするには  

1.  セクション「[Configuration Manager クライアントの手動インストール方法](#BKMK_Manual)」の指示に従い、常に以下を含めます。  

    -   CCMSetup のコマンド ライン プロパティ **/source:***&lt;コピーされた Client フォルダーへのローカル パス\>*  

    -   CCMSetup のコマンド ライン プロパティ **/UsePKICert**  

    -   Client.msi のプロパティ **CCMHOSTNAME=***&lt;インターネット ベースの管理ポイントの FQDN\>*  

    -   Client.msi のプロパティ **SMSSIGNCERT=***&lt;エクスポートされたサイト サーバー署名証明書へのローカル パス\>*  

    -   Client.msi のプロパティ **SMSSITECODE=***&lt;インターネット ベースの管理ポイントのサイト コード\>*  

    > [!NOTE]  
    >  サイトに複数のインターネット ベースの管理ポイントがある場合、どのインターネット ベースの管理ポイントを CCMHOSTNAME プロパティに指定してもかまいません。 Configuration Manager クライアントが指定したインターネット ベースの管理ポイントに接続するときに、サイト内で使用できるインターネット ベースの管理ポイントの一覧が管理ポイントからクライアントに送信され、クライアントは一覧から 1 つをランダムに選択します。  

2.  クライアントで証明書失効リスト (CRL) を確認しないようにする場合は、CCMSetup コマンドライン プロパティ「**/NoCRLCheck**」を指定します。  

3.  インターネット ベースのフォールバック ステータス ポイントを使用する場合は、Client.msi プロパティ **FSP=***&lt;インターネット ベースのフォールバック ステータス ポイントのインターネット FQDN\>* を指定します。  

4.  インターネットのみのクライアント管理用にクライアントをインストールする場合、Client.msi プロパティ「**CCMALWAYSINF=1**」を指定します。  

5.  その他の CCMSetup コマンドライン プロパティを指定する必要があるかどうかを確認します。 たとえば、クライアントに複数の有効な PKI 証明書がある場合は、場合によって証明書選択条件を指定する必要があります。 使用可能なプロパティの一覧については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」を参照してください。  

   例: `**CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1**`  

   この例では、クライアント PKI 証明書を使用するように設定された D ドライブのフォルダーからクライアント ソース ファイルをインストールし、インターネットのみのクライアント管理用の有効期限の最も長い証明書を選択し、SERVER1 というインターネットベースの管理ポイントおよび contoso.com domain 内のインターネットベースのフォールバック ステータス ポイントを使用するようにクライアントを割り当てて、ABC サイトにクライアントを割り当てています。  

###  <a name="BKMK_ConfigureIBCM_MP"></a> クライアント インストール後のインターネット ベースのクライアント管理用のクライアントを構成するには  
 クライアントのインストール後にインターネットベースの管理ポイントを割り当てるには、次のいずれかの手順に従います。 1 つ目の手順では手動で構成します。クライアントが少数の場合に適しています。 クライアントの数が多い場合は、2 つ目の手順が適しています。  

#### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>クライアントのインストール後に、Configuration Manager のプロパティでインターネットベースの管理ポイントを割り当てて、インターネットベースのクライアント管理用のクライアントを構成するには  

1.  クライアント コンピューターのコントロール パネルで [**Configuration Manager**] に移動してから、ダブルクリックしてプロパティを開きます。  

2.  [**インターネット**] タブで、[インターネット FQDN] ボックスにインターネットベースの管理ポイントの完全修飾ドメイン名を入力します。  

    > [!NOTE]  
    >  [**インターネット**] タブは、クライアントにクライアント PKI 証明書がある場合のみ使用できます。  

3.  プロキシ サーバーを使ってクライアントがインターネットにアクセスする場合は、プロキシ サーバー設定を入力します。  

#### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>クライアントのインストール後に、スクリプトを使用して、インターネットベースのクライアント管理用のクライアントを構成するには  

1.  メモ帳などのテキスト エディターを開きます。  

2.  次をコピーし、ファイルに挿入します。 *mp.contoso.com* を、使用するインターネットベースの管理ポイントのインターネット FQDN に置き換えます。  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the Internet-Based Management Point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  インターネットベースの管理ポイントを使用するようにはクライアントが構成されないように、指定のインターネットベースの管理ポイントを削除する必要がある場合は、引用符の内側の値を削除して、この行が **newInternetBasedManagementPointFQDN = ""**になるようにします。  

4.  ファイルを .vbs 拡張子で保存します。  

5.  スクリプトを使って、次のいずれかの方法でクライアント コンピューターでスクリプトを実行します。  

    -   パッケージとプログラムを使用して、既存の Configuration Manager クライアントにファイルを展開する  

    -   Windows エクスプローラーでスクリプトをダブルクリックして、既存の Configuration Manager クライアントでファイルをローカルに実行する  

 変更を適用するために、クライアントの再起動が必要になることがあります。  

##  <a name="BKMK_Provision"></a> クライアント インストールのプロパティの準備方法 (グループ ポリシーおよびソフトウェア更新ベースのクライアント インストール)  
 Windows グループ ポリシーを使用して、コンピューターに Configuration Manager クライアントのインストール プロパティを事前に準備しておくことができます。 これらのプロパティは、コンピューターのレジストリに格納され、クライアント ソフトウェアがインストールされるときに読み込まれます。 この手順は、通常必要ありませんが、次のような一部のクライアント インストール シナリオで必要となる場合があります。  

-   グループ ポリシー設定またはソフトウェア更新ベースのクライアント インストール方法を使用し、Active Directory スキーマを Configuration Manager 用に拡張していない場合。  

-   特定のコンピューターのクライアント インストール プロパティを上書きする場合。  

> [!NOTE]  
>  CCMSetup.exe コマンド ラインで何らかのインストール プロパティを指定した場合、コンピューターに準備されたインストール プロパティは使用されません。  

 Configuration Manager のインストール メディアには、ConfigMgrInstallation.adm というグループ ポリシー管理テンプレートが用意されており、クライアント コンピューターにインストール プロパティを準備するために使用できます。   

### <a name="to-configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>グループ ポリシー オブジェクトを使用してクライアント インストール プロパティの構成と割り当てを行うには  

1.  Windows グループ ポリシー オブジェクト エディターなどのエディターを使用し、新しいグループ ポリシー オブジェクトまたは既存のグループ ポリシー オブジェクトに、管理テンプレート ConfigMgrInstallation.adm をインポートします。 このファイルは、Configuration Manager インストール メディアの **TOOLS\ConfigMgrADMTemplates** フォルダーにあります。  

2.  インポートした設定 **[クライアント展開の設定を構成する]**のプロパティを開きます。  

3.  [**有効**] を選択します。  

4.  **[CCMSetup]** ボックスに、必要な CCMSetup コマンドライン プロパティを入力します。 すべての CCMSetup コマンド ライン プロパティのリストと使用例については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」を参照してください。  

5.  構成マネージャー クライアントのインストール プロパティを準備するコンピューターにグループ ポリシー オブジェクトを割り当てます。  

Windows グループ ポリシーの詳細については、Windows Server のマニュアルを参照してください。  

## <a name="next-steps"></a>次のステップ
構成マネージャー クライアントのインストール方法の詳細については、「[System Center Configuration Manager でのクライアントのインストール方法](../../../core/clients/deploy/plan/client-installation-methods.md)」をご覧ください。