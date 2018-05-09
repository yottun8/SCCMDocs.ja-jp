---
title: Windows にクライアントを展開する
titleSuffix: Configuration Manager
description: 構成マネージャー クライアントを Windows コンピューターに展開する方法を説明します。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5efca393afe2fc6441d074f987549228e7d0418f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager クライアントをインストールする前に、すべての[前提条件](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)を満たしており、必要なすべての展開構成を完了していることを確認します。   



##  <a name="BKMK_ClientPush"></a> クライアント プッシュを使用したクライアントのインストール方法  

サイトへのクライアント プッシュ インストールを構成することができます。 クライアント インストールは、サイトの境界が境界グループとして構成されている場合、これらの構成済みの境界内で検出されたコンピューターで自動的に実行されます。 特定のコレクションまたはコレクション内のリソースでクライアント プッシュ インストール ウィザードを実行して、クライアント プッシュ インストールを開始することもできます。  

また、クライアント プッシュ インストール ウィザードを使用して、[クエリ](../../../core/servers/manage/queries-technical-reference.md)の結果に Configuration Manager クライアントをインストールすることもできます。 インストールが成功するには、クエリで返されるいずれかのアイテムが、クラス **System Resource** からの属性 **ResourceID** である必要があります。   

サイト サーバーは、クライアント コンピューターにアクセスできない場合やセットアップ プロセスを開始できない場合、1 時間ごとに自動的にインストールを再試行します。 サーバーは、最大 7 日間再試行を続けます。  

クライアントのインストール プロセスを追跡するには、クライアントをインストールする前に、フォールバック ステータス ポイントをインストールします。 インストールしたフォールバック ステータス ポイントは、クライアント プッシュ インストール方法でクライアントをインストールするときに、自動的にクライアントに割り当てられます。 クライアントのインストールの進行状況を追跡するには、クライアント展開レポートとクライアント割り当てレポートを確認します。 

クライアント ログ ファイルは、トラブルシューティングに関する詳細な情報を提供します。 ログ ファイルには、フォールバック ステータス ポイントは不要です。 たとえば、サイト サーバー上の **CCM.log** ファイルには、コンピューターに接続するときのサイト サーバーからの問題がすべて記録されます。 クライアント上の **CCMSetup.log** ファイルには、インストール プロセスが記録されます。  

> [!IMPORTANT]  
>  クライアント プッシュが正常に実行されるように、前提条件がすべて満たされていることを確認してください。 詳細については、「[インストール方法の依存関係](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies)」をご覧ください。  

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>検出されたコンピューターに対してクライアント プッシュを自動的に使用するようにサイトを構成する

1.  Configuration Manager コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** を選択します。  

3.  サイト全体の自動クライアント プッシュ インストールを構成するサイトを選択します。  

4.  **[ホーム]** タブの **[設定]** グループで、**[クライアント インストール設定]** > **[クライアント プッシュ インストール]** の順にクリックします。  

5.  **[クライアント プッシュ インストールのプロパティ]** ダイアログ ボックスの **[全般]** タブで、**[サイト全体にクライアントを自動的にプッシュ インストールする]** を選択します。 Configuration Manager でクライアント ソフトウェアをプッシュするシステムの種類を選択します。  

6.  ドメイン コント ローラーにクライアントをインストールするかどうかを選択します。  

7.  **[アカウント]** タブで、ターゲット コンピューターに接続するときに Configuration Manager が使うアカウントを 1 つ以上指定します。 **[作成]** アイコンをクリックし、**[ユーザー名]** と 「**パスワード**」 (38 文字以内) を入力して、パスワードを確認入力してから、**[OK]** をクリックします。 クライアント プッシュ インストール アカウントを少なくとも 1 つ指定します。 クライアントをインストールするには、このアカウントにターゲット コンピューターでのローカル管理者権限が必要です。 クライアント プッシュ インストール アカウントを指定しないと、Configuration Manager はサイト システムのコンピューター アカウントを使います。 サイト システムのコンピューター アカウントを使った場合、クロス ドメインのクライアント プッシュは失敗します。  
    > [!NOTE]  
    >  セカンダリ サイトからのクライアント プッシュを使うには、クライアント プッシュを開始するセカンダリ サイトのアカウントを指定します。  
    >   
    >  クライアント プッシュ インストール アカウントについては、次の手順「[クライアント プッシュ インストール ウィザードを使用する](#use-the-client-push-installation-wizard)」をご覧ください。  

8.  **[インストールのプロパティ]** タブを完了します。

     スキーマが Configuration Manager 用に拡張されている場合、サイトは、このタブで指定する[クライアント インストール プロパティ](../../../core/clients/deploy/about-client-installation-properties.md)を Active Directory Domain Services に発行します。これらのプロパティは、CCMSetup がインストール プロパティなしで実行されるクライアント インストールによって読み込まれます。  

    > [!NOTE]  
    >  セカンダリ サイトでクライアント プッシュ インストールを有効にする場合は、**SMSSITECODE** プロパティがその親プライマリ サイトの Configuration Manager サイト名に設定されていることを確認してください。 Active Directory スキーマが Configuration Manager 用に拡張されている場合は、このプロパティを AUTO に設定して、正しいサイトの割り当てを自動的に検索することもできます。  

### <a name="use-the-client-push-installation-wizard"></a>クライアント プッシュ インストール ウィザードを使用する

1.  Configuration Manager コンソールで、**[管理]** >  **[サイトの構成]** > **[サイト]** を選択します。  

3.  サイト全体の自動クライアント プッシュ インストールを構成するサイトを選択します。  

4.  **[ホーム]** タブの **[設定]** グループで、**[クライアント インストール設定]** > **[クライアント プッシュ インストール]** の順にクリックします。  

5.  **[インストールのプロパティ]** タブを完了します。  

     スキーマが Configuration Manager 用に拡張されている場合、サイトは、このタブで指定する[クライアント インストール プロパティ](../../../core/clients/deploy/about-client-installation-properties.md)を Active Directory Domain Services に発行します。これらのプロパティは、CCMSetup がインストール プロパティなしで実行されるクライアント インストールによって読み込まれます。   

6.  Configuration Manager コンソールで、**[資産とコンプライアンス]** を選択します。  

7.  **[資産とコンプライアンス]** ワークスペースで、1 つ以上のコンピューター、またはコンピューターのコレクションを選択します。  

8.  **[ホーム]** タブで、以下のオプションのいずれかを選びます。  

    -   単一のコンピューターまたは複数のコンピューターにクライアントをインストールする場合は、**[デバイス]** グループで **[クライアントのインストール]** を選択します。  

    -   コンピューターのコレクションにクライアントをインストールする場合は、**[コレクション]** グループで **[クライアントのインストール]** を選択します。  

9. **クライアントのインストール ウィザード**の **[開始する前に]** ページで情報を確認してから、**[次へ]** を選択します。  

10. **[インストール オプション]** ページを完了します。  

11. インストール設定を確認してから、ウィザードを閉じます。  

> [!NOTE]  
>  サイトがクライアント プッシュ用に構成されていない場合でも、ウィザードを使ってクライアントをインストールできます。  



##  <a name="BKMK_ClientSUP"></a> ソフトウェアの更新に基づいたインストールを使用したクライアントのインストール方法  
 ソフトウェアの更新に基づいたクライアント インストールでは、クライアントをソフトウェア更新プログラムとしてソフトウェアの更新ポイントに発行します。 初回のインストールまたはアップグレードには、この方法を使用します。  

 コンピューターに構成マネージャー クライアントがインストールされている場合、クライアントはサイトからクライアント ポリシーを受け取ります。 このポリシーには、ソフトウェアの更新ポイントのサーバー名と、ソフトウェア更新プログラムの取得元のポートが含まれます。   

> [!IMPORTANT]  
>  ソフトウェアの更新に基づいたインストールを使用するには、クライアントのインストールとソフトウェア更新プログラムに同じ Windows Server Update Services (WSUS) サーバーを使用する必要があります。 このサーバーは、プライマリ サイトでアクティブなソフトウェアの更新ポイントである必要があります。 詳細については、「[Install a software update point](../../../sum/get-started/install-a-software-update-point.md)」 (ソフトウェアの更新ポイントのインストール) をご覧ください。  

コンピューターに構成マネージャー クライアントがインストールされていない場合は、ソフトウェアの更新ポイントのサーバー名を指定するように Active Directory Domain Services のグループ ポリシー オブジェクトを構成して割り当てます。  

ソフトウェア更新プログラムに基づいたクライアント インストールに、コマンド ライン プロパティを追加することはできません。 Configuration Manager 用に Active Directory スキーマを拡張した場合、クライアント コンピューターはインストール時に、自動的に Active Directory Domain Services にインストール プロパティを照会します。  

Active Directory スキーマを拡張していない場合は、グループ ポリシーを使用して、サイト内のコンピューターにクライアント インストール設定をプロビジョニングできます。 これらの設定は、ソフトウェアの更新に基づいたクライアント インストールに自動的に適用されます。 詳細については、「[クライアント インストールのプロパティの準備方法 (グループ ポリシーおよびソフトウェア更新ベースのクライアント インストール)](#BKMK_Provision)」および「[クライアントをサイトに割り当てる方法](../../../core/clients/deploy/assign-clients-to-a-site.md)」をご覧ください。  

Configuration Manager クライアントがインストールされていないコンピューターで、次の手順に従って、ソフトウェアの更新ポイントを使用してクライアントのインストールやソフトウェアの更新を行ったり、クライアントをソフトウェアの更新ポイントに発行したりするように構成します。  

> [!NOTE]  
>  コンピューターが前のソフトウェアのインストールの後に保留中の再起動の状態になると、ソフトウェア更新ベースのクライアント インストールによってコンピューターが再起動する可能性があります。  

### <a name="configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>クライアントのインストールおよびソフトウェア更新プログラム用のソフトウェアの更新ポイントを指定するように、Active Directory Domain Services のグループ ポリシー オブジェクトを構成する  

1.  グループ ポリシー管理コンソールを使って、新規または既存のグループ ポリシー オブジェクトを開きます。  

2.  コンソールで、**[コンピューターの構成]**、**[管理用テンプレート]**、**[Windows コンポーネント]** の順に展開し、**[Windows Update]** を選択します。  

3.  設定 **[イントラネットの Microsoft 更新サービスの場所を指定する]** のプロパティを開いてから、**[有効]** を選択します。  

4.  **[更新を検出するためのイントラネットの更新サービスを設定する]** ボックスで、ソフトウェアの更新ポイントのサーバー名とポートを指定します。  

    -   Configuration Manager サイト システムが完全修飾ドメイン名 (FQDN) を使用するように構成されている場合は、FQDN 形式を使用します。  

    -   Configuration Manager サイト システムが完全修飾ドメイン名 (FQDN) を使うように構成されていない場合は、短い名前の形式を使います。  

    > [!NOTE]  
    >  ポート番号を確認するには、[WSUS で使用するポート設定の特定方法](../../../sum/plan-design/plan-for-software-updates.md)に関するページをご覧ください。  

     例: **http://server1.contoso.com:8530**  

5.  **[イントラネット統計サーバーの設定]** ボックスで、イントラネット統計サーバーの名前を指定します。 ソフトウェアの更新ポイント サーバーと同じである必要はありません。 同じサーバーである場合、形式が一致している必要はありません。  

6.  クライアントをインストールしてソフトウェア更新プログラムを受け取るコンピューターに、グループ ポリシー オブジェクトを割り当てます。  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>構成マネージャー クライアントをソフトウェアの更新ポイントに発行する  

1.  Configuration Manager コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** の順にクリックします。  

3.  ソフトウェアの更新に基づいたクライアントのインストールを構成するサイトを選択します。  

4.  **[ホーム]** タブの **[設定]** グループで、**[クライアント インストール設定]** を選択し、**[ソフトウェアの更新に基づいたクライアントのインストール]** を選択します。  

5.  **[ソフトウェアの更新に基づいたクライアントのインストールを有効にする]** を選択します。  

6.  Configuration Manager サイト サーバー上のクライアント ソフトウェアのバージョンが、ソフトウェアの更新ポイントのバージョンより新しい場合、**[新しいバージョンのクライアント パッケージが見つかりました]** ダイアログ ボックスが開きます。 **[はい]** をクリックして、最新バージョンを発行します。  

    > [!NOTE]  
    >  クライアント ソフトウェアがソフトウェアの更新ポイントに発行されていない場合、このボックスは空白になります。  

構成マネージャー クライアント用のソフトウェア更新プログラムは、新しいバージョンが存在する場合に自動的に更新されるわけではありません。 新しいクライアント バージョンが含まれるようにサイトをアップグレードするには、手順 6 でこの手順を繰り返して **[はい]** をクリックします。  



##  <a name="BKMK_ClientGP"></a> グループ ポリシーを使用したクライアントのインストール方法  
 Active Directory Domain Services のグループ ポリシーを使って、企業内のコンピューターにインストールするように構成マネージャー クライアントを割り当てたり、発行したりできます。 クライアントは、コンピューターの起動時にインストールされます。 グループ ポリシーを使うと、コントロール パネルの **[プログラムの追加と削除]** ダイアログ ボックスにクライアントが表示され、ユーザーがインストールできるようになります。  

 グループ ポリシーに基づいたインストールには、Windows インストーラー パッケージ (CCMSetup.msi) を使います。 このファイルは、Configuration Manager サイト サーバーの **&lt;ConfigMgr インストール ディレクトリ\>\bin\i386** フォルダーにあります。 このファイルにプロパティを追加してインストールの動作を変更することはできません。  

> [!IMPORTANT]  
>  クライアント インストール ファイルにアクセスするためには、管理者権限を持っている必要があります。  

-   Active Directory スキーマが Configuration Manager 用に拡張されており、**[サイトのプロパティ]** ダイアログ ボックスの **[詳細設定]** タブで **[Active Directory Domain Services 内にこのサイトを発行する]** が選択されている場合、クライアント コンピューターは自動的に Active Directory Domain Services でインストール プロパティを検索します。 発行されるインストール プロパティについては、「[Active Directory Domain Services に発行されたクライアント インストールのプロパティについて](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)」をご覧ください。  

-   Active Directory スキーマが拡張されていない場合は、このトピックの手順「[クライアント インストールのプロパティの準備方法 (グループ ポリシーおよびソフトウェア更新ベースのクライアント インストール)](#BKMK_Provision)」を使って、コンピューターのレジストリ内にインストール プロパティを格納できます。 これらのインストール プロパティは、クライアントのインストール時に使われます。  

Active Directory Domain Services のグループ ポリシーを使ってソフトウェアをインストールする方法については、Windows Server のドキュメントをご覧ください。  



##  <a name="BKMK_Manual"></a> クライアントの手動インストール方法  
 CCMSetup.exe プログラムを使用して、企業内のコンピューターにクライアント ソフトウェアを手動でインストールできます。 このプログラムとそのサポート ファイルは、サイト サーバー上の Configuration Manager インストール フォルダーの **Client** フォルダーおよびサイトの管理ポイントにあります。 このフォルダーは次のようにネットワークで共有されます。  

 \\\\*&lt;サイト サーバー名\>* \SMS_*&lt;サイト コード\>* \Client\  

 ここで &lt;*サイト サーバー名*\> は管理ポイントをホストするいずれかのサーバーの名前、&lt;*サイト コード*\> はクライアントが割り当てられるプライマリ サイト コードです。 クライアントでコマンド ラインから CCMSetup.exe を実行するには、この場所にネットワーク ドライブをマップしてからコマンドを実行する必要があります。  

> [!IMPORTANT]  
>  クライアント インストール ファイルにアクセスするためには、管理者権限を持っている必要があります。  

 CCMSetup.exe は、必要なすべての前提条件をクライアント コンピューターにコピーし、Windows インストーラー パッケージ (Client.msi) を呼び出してクライアントをインストールします。 Client.msi を直接実行することはできません。  

 CCMSetup.exe および Client.msi の両方にコマンド ライン プロパティを指定して、クライアント インストールの動作を変更できます。 Client.msi のプロパティを指定する前に、CCMSetup のプロパティ (先頭が **/** のプロパティ) を指定する必要があります。 次に例を示します。  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`    

次のプロパティを使用して、クライアント インストールを指定します。  

|プロパティ|説明|  
|--------------|-----------------|  
|**/mp:SMSMP01**|CCMSetup のこのプロパティで、必要なクライアント インストール ファイルをダウンロードする管理ポイント SMSMP01 を指定します。|  
|**/logon**|CCMSetup のこのプロパティで、既存の構成マネージャー クライアントがコンピューターで見つかった場合はインストールを停止するように指定します。|  
|**SMSSITECODE=AUTO**|Client.msi のこのプロパティで、たとえば Active Directory Domain Services を使用して、使用する Configuration Manager サイト コードをクライアントが特定するように指定します。|  
|**FSP=SMSFP01**|Client.msi のこのプロパティで、SMSFP01 というフォールバック ステータス ポイントを使って、クライアント コンピューターから送信される状態メッセージを受信するように指定します。|  

 すべての CCMSetup.exe プロパティについては、「[クライアント インストールのプロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」をご覧ください  

> [!Tip]  
> Azure AD の ID を使って最新の Windows 10 デバイスに構成マネージャー クライアントをインストールする手順については、「[認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる](/sccm/core/clients/deploy/deploy-clients-cmg-azure)」をご覧ください。 その手順は、イントラネットまたはインターネット上のクライアントに対するものです。  


### <a name="examples"></a>例
 以下の例は、イントラネット上の Active Directory クライアントに関するものです。 これらは、次の値を使ってサイトのさまざまな側面を表します。  

 **MPSERVER** = 管理ポイントをホストするサーバー   
**FSPSERVER** = フォールバック ステータス ポイントをホストするサーバー  
**ABC** = サイト コード  
**contoso.com** = ドメイン名  

 すべてのサイト システム サーバーは、イントラネット FQDN で構成されます。 サイトは、クライアントの Active Directory フォレストに発行されます。  

 クライアント コンピューターで、ローカル管理者としてログオンします。ドライブ (z:) を \\\MPSERVER\SMS_ABC\Client にマップして、コマンド プロンプトを z ドライブに切り替えてから、次のいずれかのコマンドを実行します。  

 **例 1:**  

`CCMSetup.exe`  

この例では、追加プロパティなしでクライアントをインストールします。 クライアントは、Active Directory Domain Services に対して発行されたクライアント インストール プロパティで自動的に構成されます。 以下の設定に自動的に構成されます。 
- サイト コード。 この設定では、クライアントの割り当て用に構成されている境界グループに、クライアントのネットワークの場所が含まれる必要があります。 
- 管理ポイント
- フォールバック ステータス ポイント
- HTTPS のみを使って通信します  
  
詳細については、「[Active Directory Domain Services に発行されたクライアント インストールのプロパティについて](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)」をご覧ください。  

 **例 2:**  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
この例では、Active Directory Domain Services が提供する自動構成を上書きします。 クライアントの割り当て用に構成されている境界グループに、クライアントのネットワークの場所が含まれる必要はありません。 代わりに、インストールでは次の設定を指定します。
- サイト コード
- イントラネット管理ポイント 
- インターネット ベースの管理ポイント
- インターネットからの接続を受け入れるフォールバック ステータス ポイント
- 最長の有効期間を持つクライアント PKI 証明書 (該当する場合) を使います  



##  <a name="BKMK_ClientLogonScript"></a> ログオン スクリプトを使用したクライアントのインストール方法  
 Configuration Manager では、構成マネージャー クライアント ソフトウェアをインストールするログオン スクリプトをサポートしています。 **CCMSetup.exe** プログラム ファイルをログオン スクリプトで使用して、クライアント インストールを開始できます。  

 ログオン スクリプト インストールの使用方法は、手動のクライアント インストールと同じです。 CCMSsetup.exe には **/logon** インストール プロパティを指定することができます。 このプロパティを指定すると、クライアントのいずれかのバージョンがコンピューターに既に存在する場合、クライアントはインストールされません。 この動作により、ログオン スクリプトが実行されるたびにクライアントの再インストールが発生することはなくなります。  

 インストール ソース (**/Source** プロパティ) もインストール取得元の管理ポイント (**/MP** プロパティ) も指定されていない場合、CCMSetup.exe は Active Directory Domain Services を検索して管理ポイントを探します。 この動作は、スキーマが Configuration Manager 用に拡張されていて、サイトが Active Directory Domain Services に発行されている場合にのみ発生します。 または、クライアントが DNS または WINS を使用して管理ポイントを特定することもできます。  



##  <a name="BKMK_ClientApp"></a> パッケージとプログラムを使用したクライアントのインストール方法  
 Configuration Manager を使用し、階層内の選択したコンピューターのクライアント ソフトウェアをアップグレードするパッケージとプログラムを作成して展開できます。 Configuration Manager には、通常使用される値をパッケージ プロパティに適用する、パッケージ定義ファイルが付属しています。 追加のコマンド ライン プロパティを指定することで、クライアント インストールの動作をカスタマイズできます。  

> [!NOTE]  
>  この方法では、Configuration Manager 2007 クライアントをアップグレードすることはできません。 代わりに、最新バージョンのクライアントが含まれたパッケージを自動的に作成して展開する自動クライアント アップグレードを使用します。 詳細については、「[クライアントをアップグレードする](../../../core/clients/manage/upgrade/upgrade-clients.md)」をご覧ください。  
>   
>  旧バージョンの構成マネージャー クライアントから移行する方法については、「[System Center Configuration Manager でのクライアント移行戦略の計画](../../../core/migration/planning-a-client-migration-strategy.md)」をご覧ください。  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>クライアント ソフトウェア用のパッケージとプログラムを作成する  

次の手順に従って、クライアント ソフトウェアをアップグレードするために構成マネージャー クライアント コンピューターに展開できる、Configuration Manager パッケージとプログラムを作成します。  

1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]** > **[アプリケーション管理]** > **[パッケージ]** の順に選択します。  

3.  **[ホーム]** タブの **[作成]** グループで、**[定義に基づいたパッケージの作成]** を選択します。  

4.  ウィザードの **[パッケージの定義]** ページで、**[発行元]** ドロップダウン リストから **[Microsoft]** を選択し、**[パッケージ定義]** の一覧から **[Configuration Manager クライアントのアップグレード]** を選択します。  

5.  **[ソース ファイル]** ページで、**[常にソース フォルダーからファイルを取得する]** を選択します。  

6.  **[ソース フォルダー]** ページで、**[ネットワーク パス (UNC 名)]** を選びます。 その後、クライアント インストール ファイルが含まれているコンピューターとフォルダーへのネットワーク パスを入力します。  

    > [!NOTE]  
    >  Configuration Manager の展開を実行するコンピューターが、指定したネットワーク フォルダーへのアクセス権を持っている必要があります。持っていない場合、インストールは失敗します。  

    クライアント インストールのプロパティを変更するには、**[Configuration Manager エージェントのサイレント アップグレードのプロパティ]** プログラム ダイアログ ボックスの **[全般]** タブで CCMSetup.exe コマンド ライン パラメーターを変更します。 既定のインストール プロパティは、 **/noservice SMSSITECODE=AUTO**です。  

9. クライアント アップグレード パッケージをホストする必要があるすべての配布ポイントにパッケージを配布します。 次に、アップグレードが必要なクライアントが含まれているコンピューターのコレクションにパッケージを展開できます。  



## <a name="bkmk_mdm"></a>Intune に登録されている MDM 管理対象 Windows デバイスへのクライアントのインストール方法

Microsoft Intune に登録されているコンピューターにクライアントのインストール ファイルを展開できます。 

この手順では、イントラネットに接続されている従来のクライアントに対するものです。 従来のクライアント認証方法を使います。 クライアント ソフトウェアをインストールした後に、デバイスが管理状態にあることを確認するには、デバイスがイントラネット上にあり、Configuration Manager サイトの境界内にある必要があります。  

Azure AD の ID を使って最新の Windows 10 デバイスに構成マネージャー クライアントをインストールする手順については、「[認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる](/sccm/core/clients/deploy/deploy-clients-cmg-azure)」をご覧ください。

> [!NOTE]
> クライアント ソフトウェアがインストールされると、デバイスが Intune から登録されます。
> 
> バージョン 1710 以降では、クライアントは Intune から登録解除されません。 クライアントは、構成マネージャー クライアントと MDM の登録の両方を同時に持つことができます。 詳細については、[共同管理](/sccm/core/clients/manage/co-management-overview)に関するページをご覧ください。

###  <a name="install-clients-with-intune"></a>Intune でクライアントをインストールします。

1. Intune で、構成マネージャー クライアントのインストール ファイル **ccmsetup.msi** を含む、[アプリを作成](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune)します。 このファイルは、Configuration Manager サイト サーバーの **&lt;ConfigMgr インストール ディレクトリ\>\bin\i386** フォルダーにあります。

2. Intune ソフトウェア パブリッシャーで、コマンド ライン パラメーターを入力します。 たとえば、イントラネット上の従来のクライアントでは次のコマンド ラインを使います。

  `CCMSETUPCMD="/MP:&lt;FQDN of management point> SMSMP=&lt;FQDN of management point> SMSSITECODE=&lt;Your site code> DNSSUFFIX=&lt;DNS Suffix of management point>"`  

   > [!Note]  
   > Azure AD 認証を使う最新の Windows 10 クライアントで使うコマンド ラインの例については、「[共同管理用に Windows 10 デバイスを準備する](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)」をご覧ください。

3. 登録済みの Windows コンピューターに[アプリを展開](/intune/deploy-use/deploy-apps-in-microsoft-intune)します。



##  <a name="BKMK_ClientImage"></a> コンピューター イメージングを使用したクライアントのインストール方法  
OS イメージの作成に使う参照コンピューターに、構成マネージャー クライアント ソフトウェアをプレインストールできます。   

> [!Important]
> Configuration Manager のタスク シーケンスを使って OS イメージを展開するときに、[ConfigMgr クライアントの準備](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)タスク シーケンス ステップは、構成マネージャー クライアントを完全に削除します。 

### <a name="prepare-the-client-computer-for-imaging"></a>イメージング用にクライアント コンピューターを準備する  

1.  参照コンピューターに構成マネージャー クライアント ソフトウェアを手動でインストールします。 詳細については、「[Configuration Manager クライアントの手動インストール方法](#BKMK_Manual)」をご覧ください。  

    > [!IMPORTANT]  
    >  CCMSetup.exe コマンド ライン プロパティでクライアントに Configuration Manager サイト コードを指定しないでください。  

2.  コマンド プロンプトで「`net stop ccmexec`」と入力して、**SMS Agent Host** サービス (Ccmexec.exe) が参照コンピューターで実行されていないことを確認します。
3.  参照コンピューターの **Windows** フォルダーから、ファイル **SMSCFG.INI** を削除します。  
3.  参照コンピューターのローカル コンピューター ストアに保存されている証明書を削除します。 たとえば、公開キー基盤 (PKI) 証明書を使用する場合、コンピューターをイメージ化する前に、**[コンピューター]** と **[ユーザー]** の **[個人用]** ストアの証明書を削除する必要があります。

4.  クライアントを参照コンピューターとは別の Configuration Manager 階層にインストールする場合は、信頼されたルート キーを参照コンピューターから削除します。  
    > [!NOTE]  
    >  クライアントは、Active Directory Domain Services に管理ポイントを照会できない場合、信頼されたルート キーを使用して信頼された管理ポイントを特定します。 イメージングされたすべてのクライアントをマスター コンピューターと同じ階層に展開する場合は、信頼されたルート キーを所定の場所に残しておきます。 クライアントが別の階層に展開されている場合は、信頼されたルート キーを削除します。 また、信頼されたルート キーでクライアントをプロビジョニングします。 詳細については、「[信頼されたルート キーの計画](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)」を参照してください。 

5.  イメージング ソフトウェアを使用して、マスター コンピューターのイメージをキャプチャします。  

6.  イメージを対象コンピューターに展開します。  



##  <a name="BKMK_ClientWorkgroup"></a> ワークグループ コンピューターへのクライアントのインストール方法  
 Configuration Manager は、ワークグループ内のコンピューターへのクライアント インストールをサポートします。 「[Configuration Manager クライアントの手動インストール方法](#BKMK_Manual)」で指定された方法を使用して、ワークグループ コンピューターにクライアントをインストールします。  

 必要条件:  

-   クライアントは、各ワークグループ コンピューターに手動でインストールする必要があります。 インストール時に、ログオン ユーザーはローカル管理者権限を持っている必要があります。  

-   Configuration Manager サイト サーバー ドメイン内のリソースにアクセスするには、このサイト用にネットワーク アクセス アカウントを構成する必要があります。 このアカウントをソフトウェアの配布コンポーネントのプロパティとして指定します。 詳細については、「 [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md)」をご覧ください。  

 制限事項:  

-   ワークグループ クライアントは、Active Directory Domain Services から管理ポイントを特定できません。代わりに、DNS、WINS、または別の管理ポイントを使用する必要があります。  

-   クライアントは、Active Directory ドメイン サービスにサイト情報を照会できないので、グローバル ローミングはサポートされません。  

-   Active Directory 探索方法では、ワークグループ内のコンピューターを探索できません。  

-   ワークグループ コンピューターのユーザーにソフトウェアを展開することはできません。  

-   クライアント プッシュ インストール方法を使用して、ワークグループ コンピューターにクライアントをインストールすることはできません。  

-   ワークグループ クライアントの場合は、認証に Kerberos を使用できないので、手動の承認が必要です。  

-   ワークグループ クライアントは、配布ポイントとして構成できません。 Configuration Manager では、配布ポイントであるコンピューターがドメインのメンバーに指定されている必要があります。  

### <a name="install-the-client-on-workgroup-computers"></a>ワークグループ コンピューターにクライアントインストールする  

前提条件を確認し、セクション「[Configuration Manager クライアントの手動インストール方法](#BKMK_Manual)」の指示に従います。  

   この例では、イントラネットのクライアント管理用のクライアントをインストールし、サイト コードと DNS サフィックスを指定して管理ポイントを検索しています。 `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     

   この例では、境界グループ内に構成されたネットワークの場所にクライアントを配置する必要があります。 この要件は、サイトの自動割り当てを成功させるために必要です。 コマンドには、サーバー FSPSERVER 上のフォールバック ステータス ポイントが含まれます。 このプロパティは、クライアントの展開を追跡し、クライアントの通信の問題を識別するのに役立ちます。 
   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> インターネット ベースのクライアント管理用クライアントのインストール方法  
 
> [!Note]
> このセクションの内容は、[クラウド管理ゲートウェイ](/sccm/core/clients/manage/plan-cloud-management-gateway)を使うクライアントには適用されません。 クラウド管理ゲートウェイを使ってインターネット ベースのクライアントをインストールするには、「[認証のため Azure AD を使用して、Configuration Manager の Windows 10 クライアントをインストールして割り当てる](/sccm/core/clients/deploy/deploy-clients-cmg-azure)」をご覧ください。

Configuration Manager サイトが、イントラネット上にある場合とインターネット上にある場合があるクライアントに対して[インターネットベースのクライアント管理](/sccm/core/clients/manage/plan-internet-based-client-management)をサポートするときは、次の 2 つの方法のいずれかを使って、イントラネット上のクライアントをインストールできます。  

-   たとえば、手動インストールやクライアント プッシュを使ってクライアントをインストールするときには、"CCMHOSTNAME=&lt;*インターネットベースの管理ポイントのインターネット FQDN*\>" という Client.msi プロパティを含めることができます。 この方法を使用するときには、クライアントをサイトに直接割り当てる必要があります。また、サイトの自動割り当ては使用できません。 このトピックの「[Configuration Manager クライアントの手動インストール方法](#BKMK_Manual)」セクションに、この構成方法の例を示します。  

-   イントラネットのクライアント管理用にクライアントをインストールしてから、インターネット ベースのクライアント管理ポイントをクライアントに割り当てることができます。 コントロール パネルの構成マネージャー クライアントのプロパティを使うか、またはスクリプトを使って、管理ポイントを変更します。 この方法を使用するときに、自動クライアント割り当てを使用できます。 詳細については、このトピックの「[クライアント インストール後のインターネットベースのクライアント管理用のクライアント構成方法](#BKMK_ConfigureIBCM_MP)」セクションをご覧ください。  

 インターネット上のクライアントをインストールする必要がある場合は、以下のサポートされる方法の 1 つから選択します。  

-   これらのクライアントが VPN でイントラネットに一時的に接続するためのメカニズムを提供します。 その後、適切なクライアント インストール方法を使ってクライアントをインストールします。  

-   Configuration Manager に依存しないインストール方法を使います。 たとえば、リムーバブル メディアにクライアント インストール ソース ファイルをパッケージ化し、インストールするユーザーに指示と共に送ります。 クライアント インストール ソース ファイルは、Configuration Manager サイト サーバーおよび管理ポイントの*&lt;インストール パス\>* \Client フォルダーにあります。 クライアント フォルダー経由とこのフォルダーから手動でコピーし、CCMSetup.exe と適切なすべての CCMSetup コマンド ライン プロパティを使用して、クライアントを手動でインストールするためのスクリプトをメディアに含めます。  

> [!NOTE]  
>  Configuration Manager では、インターネット ベースの管理ポイントまたはインターネット ベースのソフトウェア更新ポイントからクライアントを直接インストールすることはサポートしていません。  

 インターネット経由で管理されるクライアントは、インターネット ベースのサイト システムと通信する必要があります。 クライアントをインストールする前に、これらのクライアントが公開キー基盤 (PKI) 証明書も持っていることを確認します。 これらの証明書は Configuration Manager とは別にインストールします。 証明書の要件のについては、「[PKI 証明書の要件](../../../core/plan-design/network/pki-certificate-requirements.md)」をご覧ください。  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>CCMSetup コマンドライン プロパティを指定してインターネット上のクライアントをインストールする  

1.  セクション「[Configuration Manager クライアントの手動インストール方法](#BKMK_Manual)」の指示に従い、常に以下を含めます。  

    -   CCMSetup のコマンド ライン プロパティ **/source:**&lt;*コピーされた Client フォルダーへのローカル パス*\>  

    -   CCMSetup のコマンド ライン プロパティ **/UsePKICert**  

    -   Client.msi のプロパティ **CCMHOSTNAME=**&lt;*インターネット ベースの管理ポイントの FQDN*\>  

    -   Client.msi のプロパティ **SMSSIGNCERT=**&lt;*エクスポートされたサイト サーバー署名証明書へのローカル パス*\>  

    -   Client.msi のプロパティ **SMSSITECODE=**&lt;*インターネット ベースの管理ポイントのサイト コード*\>  

    > [!NOTE]  
    >  サイトに複数のインターネット ベースの管理ポイントがある場合、どのインターネット ベースの管理ポイントを CCMHOSTNAME プロパティに指定してもかまいません。 構成マネージャー クライアントが指定したインターネット ベースの管理ポイントに接続するときに、サイト内で使用できるインターネット ベースの管理ポイントの一覧が管理ポイントからクライアントに送信されます。 クライアントは一覧から 1 つをランダムに選びます。  

2.  クライアントで証明書失効リスト (CRL) を確認しないようにする場合は、CCMSetup コマンドライン プロパティ「**/NoCRLCheck**」を指定します。  

3.  インターネット ベースのフォールバック ステータス ポイントを使用する場合は、Client.msi プロパティ「**FSP=**&lt;*インターネット ベースのフォールバック ステータス ポイントのインターネット FQDN*\>」を指定します。  

4.  インターネットのみのクライアント管理用にクライアントをインストールする場合、Client.msi プロパティ「**CCMALWAYSINF=1**」を指定します。  

5.  その他の CCMSetup コマンドライン プロパティを指定する必要があるかどうかを確認します。 たとえば、クライアントに複数の有効な PKI 証明書がある場合は、場合によって証明書選択条件を指定する必要があります。 使用可能なプロパティのリストについては、「[クライアント インストールのプロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」をご覧ください。  

   例:  
   `CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

   この例では、次の動作を持つクライアントがインストールされます。
   - D ドライブのフォルダーにあるソース ファイルを使う
   - クライアント PKI 証明書を使う 
   - 有効期限の最も長い証明書を選ぶ 
   - インターネットのみのクライアント管理
   - SERVER1 という名前のインターネット ベースの管理ポイントを使うようにクライアントを割り当てる
   - contoso.com ドメインのインターネット ベースのフォールバック ステータス ポイントを割り当てる
   - ABC サイトにクライアントを割り当てる  

###  <a name="BKMK_ConfigureIBCM_MP"></a> クライアント インストール後のインターネット ベースのクライアント管理用のクライアントを構成するには  
 クライアントのインストール後にインターネットベースの管理ポイントを割り当てるには、次のいずれかの手順に従います。 1 つ目の手順では手動で構成します。クライアントが少数の場合に適しています。 クライアントの数が多い場合は、2 つ目の手順が適しています。  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>クライアントのインストール後に、Configuration Manager のプロパティでインターネットベースの管理ポイントを割り当てて、インターネットベースのクライアント管理用のクライアントを構成する  

1.  クライアント コンピューターのコントロール パネルで **[Configuration Manager]** に移動してから、ダブルクリックしてプロパティを開きます。  

2.  **[インターネット]** タブで、[インターネット FQDN] ボックスにインターネットベースの管理ポイントの完全修飾ドメイン名を入力します。  

    > [!NOTE]  
    >  **[インターネット]** タブは、クライアントにクライアント PKI 証明書がある場合のみ使用できます。  

3.  クライアントがプロキシ サーバーを使ってインターネットにアクセスする場合は、プロキシ サーバーの設定を入力します。  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>クライアントのインストール後に、スクリプトを使用して、インターネットベースのクライアント管理用のクライアントを構成する  

1.  メモ帳などのテキスト エディターを開きます。  

2.  次の VBScript サンプルをコピーして、ファイルに挿入します。 *mp.contoso.com* を、使用するインターネットベースの管理ポイントのインターネット FQDN に置き換えます。  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the internet-based management point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  インターネットベースの管理ポイントを使うようにクライアントが構成されないように、指定のインターネットベースの管理ポイントを削除する必要がある場合は、引用符の内側の値を削除して、この行が `newInternetBasedManagementPointFQDN = ""` になるようにします。  

4.  ファイルを .vbs 拡張子で保存します。  

5.  cscript.exe を使って、次のいずれかの方法でクライアント コンピューターでスクリプトを実行します。  

    -   パッケージとプログラムを使用して、既存の Configuration Manager クライアントにファイルを展開する  

    -   Windows エクスプローラーでスクリプトをダブルクリックして、既存の Configuration Manager クライアントでファイルをローカルに実行する  

 変更を適用するために、クライアントの再起動が必要になることがあります。  



##  <a name="BKMK_Provision"></a> クライアント インストールのプロパティの準備方法 (グループ ポリシーおよびソフトウェア更新ベースのクライアント インストール)  
 Windows グループ ポリシーを使って、コンピューターに構成マネージャー クライアントのインストール プロパティを事前にプロビジョニングしておくことができます。 これらのプロパティは、コンピューターのレジストリに格納され、クライアント ソフトウェアがインストールされるときに読み込まれます。 この手順は、通常必要ありませんが、次のような一部のクライアント インストール シナリオで必要となる場合があります。  

-   グループ ポリシー設定またはソフトウェア更新ベースのクライアント インストール方法を使っていて、 Active Directory スキーマを Configuration Manager 用に拡張していない場合。  

-   特定のコンピューターのクライアント インストール プロパティを上書きする場合。  

> [!NOTE]  
>  CCMSetup.exe コマンド ラインで何らかのインストール プロパティを指定した場合、コンピューターにプロビジョニングされたインストール プロパティは使われません。  

 Configuration Manager のインストール メディアには、ConfigMgrInstallation.adm というグループ ポリシー管理テンプレートが用意されています。 このテンプレートを使って、インストール プロパティでクライアント コンピューターをプロビジョニングできます。   

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>グループ ポリシー オブジェクトを使用してクライアント インストール プロパティの構成と割り当てを行う  

1.  Windows グループ ポリシー オブジェクト エディターなどのエディターを使い、新しいグループ ポリシー オブジェクトまたは既存のグループ ポリシー オブジェクトに、管理テンプレート ConfigMgrInstallation.adm をインポートします。 このファイルは、Configuration Manager インストール メディアの **TOOLS\ConfigMgrADMTemplates** フォルダーにあります。  

2.  インポートした設定 **[クライアント展開の設定を構成する]** のプロパティを開きます。  

3.  **[有効]** を選択します。  

4.  **[CCMSetup]** ボックスに、必要な CCMSetup コマンドライン プロパティを入力します。 CCMSetup コマンド ライン プロパティの詳細と使用例については、「[クライアント インストールのプロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」をご覧ください。  

5.  構成マネージャー クライアントのインストール プロパティをプロビジョニングするコンピューターにグループ ポリシー オブジェクトを割り当てます。  

Windows グループ ポリシーについては、Windows Server のマニュアルをご覧ください。  



## <a name="next-steps"></a>次のステップ
構成マネージャー クライアントのインストール方法については、「[クライアント インストール方法](../../../core/clients/deploy/plan/client-installation-methods.md)」をご覧ください。