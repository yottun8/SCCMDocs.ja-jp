---
title: "リリース ノート | Microsoft Docs"
description: "製品でまだ修正されていないまたは Microsoft サポート技術情報の記事で説明されていない緊急の問題については以下のメモを参照してください。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: ea723a6694feb2c9584b35498aa9c3519383f08d
ms.openlocfilehash: a9dc046a54c15d9d299664cd1f2a149383f53489


---
# <a name="release-notes-for-system-center-configuration-manager"></a>System Center Configuration Manager リリース ノート

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の製品リリース ノートは、この製品でまだ修正されていない緊急の問題 (コンソール内更新から入手可能)、または Microsoft サポート技術情報の記事で詳しく説明している緊急の問題のみに限定されています。  

 主要なシナリオに影響を与える既知の問題については、System Center Configuration Manager ドキュメント ライブラリのオンライン製品ドキュメントを参照してください。  

> [!TIP]  
>  このトピックには、System Center Configuration Manager の現在のブランチのリリース ノートが含まれています。 System Center Configuration Manager の Technical Preview の場合は、「[System Center Configuration Manager の Technical Preview](../../../../core/get-started/technical-preview.md)」を参照してください。  

## <a name="setup-and-upgrade"></a>セットアップとアップグレード  

### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>バージョン 1606 を使用して Long-Term Service Branch をインストールすると、Current Branch サイトがインストールされる
2016 年 10 月リリースのバージョン 1606 ベースライン メディアを使用して Long-Term Servicing Branch (LTSB) サイトをインストールすると、代わりに Current Branch サイトがインストールされます。 この問題は、サイトのインストールでサービス接続ポイントをインストールするオプションがオフのために発生します。

 - サービス接続ポイントは必須ではありませんが、LTSB サイトをインストールするには、セットアップ時にインストールするオプションをオンにする必要があります。

セットアップが完了したら、サービス接続ポイントをアンインストールすることができます。  ただし、Current Branch サイトと LTSB サイトの両方でテレメトリ データを送信し、セキュリティ更新プログラムを取得するには、オフライン モードまたはオンライン モードのサービス接続ポイントが存在する必要があります。

既に Current Branch サイトとしてサイトがインストールされていて、LTSB をインストールする場合は、サイトをアンインストールしてから再インストールします。 不明な点については、[Microsoft ヘルプおよびサポート](http://go.microsoft.com/fwlink/?LinkId=243064)で検索または問い合わせてください。  

インストールされているブランチを確認するには、コンソールで **[管理]** > **[サイトの構成]** > **[サイト]** を選択し、**[階層設定]** を開きます。 サイトを Current Branch サイトに変換するオプションは、サイトが LTSB を実行している場合にのみ使用できます。  

**回避策:**  なし。   





### <a name="the--sql-server-backup-model-in-use-by-configuration-manager-can-change-from-full-to-simple"></a>Configuration Managerで使用されている SQL Server のバックアップ モデルが完全版から簡易版に変更されることがあります。  
 System Center Configuration Manager バージョン 1511 にアップグレードすると、Configuration Manager で使用されている SQL Server のバックアップ モデルが完全版から簡易版に変更されることがあります。  

-   Configuration Manager の組み込みバックアップ タスクを使用せずに、SQL Server のカスタム バックアップ タスクと完全バックアップ モデルを組み合わせて使用している場合、アップグレードを実行すると、バックアップ モデルが完全版から簡易版に変更されることがあります。  

**回避策**: バージョン 1511 にアップグレードした後、SQL Server の構成を確認し、必要であれば完全版に復元します。  

### <a name="when-you-add-a-service-window-to-a-new-site-server-service-windows-that-were---configured-for-another-site-server-are-deleted"></a>サービス ウィンドウを新しいサイト サーバーに追加すると、別のサイト サーバーに構成されているサービス ウィンドウが削除されます。  
 System Center Configuration Manager バージョン 1511 でサービス ウィンドウを使用すると、階層内の 1 つのサイト サーバーにのみサービス ウィンドウを構成できます。 1 つのサーバー上でサービス ウィンドウを構成した後に、2 つ目のサイト サーバーでサービス ウィンドウを構成すると、警告やエラーが表示されることなく、最初のサイト サーバーのサービス ウィンドウが削除されます。  

**回避策**: 修正プログラムを [Microsoft サポート技術情報の記事 3142341](http://support.microsoft.com/kb/3142341) からインストールします。 この問題は、System Center Configuration Manager の更新プログラム 1602 をインストールした場合にも解決されます。  

### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>更新プログラムが Configuration Manager コンソールの更新プログラムとサービス ノードでダウンロード中の状態でスタックする  
オンライン サービス接続ポイントによる更新プログラムの自動ダウンロード中には、更新プログラムがダウンロード中の状態でスタックする場合があります。 更新プログラムのダウンロードがスタックしている場合、指定されたログ ファイルに、次のようなエントリが表示されます。  

DMPdownloader ログ:  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log:  

-   Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**回避策**: サイト サーバーで、次に一致するように次のレジストリ キーを変更し、SMS_Executive サービスを再起動するか、次回の自動ダウンロード サイクルを最大で 24 時間待機します。  

-   **編集するキー**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **状態の値**: **146944** の 10 進数または **0x00023e00** の 16 進数に設定  

### <a name="pre-release-features-introduced-in-system-center-configuration-manager-1602"></a>System Center Configuration Manager 1602 で導入されたプレリリース機能  

プレリリース機能は、運用環境での早期テストのためにこの製品に含まれていますが、運用環境で使用することはできません。  

更新プログラム 1606 から開始する場合、プレリリース機能を使用する前に同意する必要があります。 詳細については、「[更新プログラムからプレリリース機能を使用する](../../../../core/servers/manage/install-in-console-updates.md)」を参照してください。

System Center Configuration Manager バージョン 1602 では 2 つのプレリリース機能が導入されました。  

-   System Center Configuration Manager が管理する PC の条件付きアクセス。 詳細については、「[System Center Configuration Manager で管理されている PC の O365 サービスへのアクセスを管理する](../../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)」を参照してください
    - 更新プログラム 1602 をインストールすると、プレリリース機能であっても機能の種類はリリース済みとして表示されます。
    - その後 1602 から 1606 に更新した場合、プレリリース機能のままですが、機能の種類はリリース済みとして表示されます。
    - バージョン 1511 から 1606 に直接更新した場合、機能の種類はプレリリースとして表示されます。


-   クラスター対応のコレクションのサービス。 詳細については、「[System Center Configuration Manager 向けテクニカル プレビュー 1605 の機能](../../../../core/get-started/capabilities-in-technical-preview-1605.md)」の「[サーバー グループのサービス](../../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)」を参照してください。  




### <a name="recovery-options-for-a-secondary-site-are-not-available-in-the-console"></a>セカンダリ サイトの回復オプションは、コンソールで利用不可  
セカンダリ サイトの回復が失敗した後、オプション **[セカンダリ サイトの回復]** が Configuration Manager コンソールで利用できなくなる場合があります。  

この問題は、System Center Configuration Manager バージョン 1511 および 1602 に影響し、今後の更新プログラムで解決される予定です。  

**回避策**: 次の方法のいずれかを使用して、セカンダリ サイトを回復 (再インストール) します。  

-   **Preinst.exe** および **/delsite** コマンドを使用して、セカンダリ サイトを削除してから、セカンダリ サイトを再インストールします。 preinst.exe の詳細については、「[System Center Configuration Manager の階層メンテナンス ツール (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)」を参照してください。  

-   セカンダリ サイトの回復を開始するには、次のスクリプトを実行します。 回復するセカンダリ サイトのプライマリ親サイトのデータベースでこのスクリプトを実行します。  

    ```  
    declare @SiteCode NVARCHAR(3)=N'<replace with secondary site code>'   

    UPDATE Sites SET Status = 9  
                    , DetailedStatus = 3  
    FROM Sites WHERE SiteCode = @SiteCode  

    UPDATE SCP SET SCP.Value1 = 9  
                    , SCP.Value2 = N'3'  
    FROM SC_SiteDefinition_Property SCP INNER JOIN SC_SiteDefinition SC ON SC.SiteNumber = SCP.SiteNumber  
    WHERE SC.SiteCode = @SiteCode AND SCP.[Name] = N'Requested Status'  
  ```  

###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>CD.Latest フォルダーの再頒布可能ファイルを使用するとマニフェストの検証エラーのためにセットアップが失敗します。
バージョン 1606 用に作成された CD.Latest フォルダーからセットアップを実行し、その CD.Latest フォルダーに含まれている再頒布可能ファイルを使用すると、Configuration Manager のセットアップ ログに次のエラーが記録されてセットアップが失敗します。

  - エラー: File hash check failed for defaultcategories.dll (defaultcategories.dll のファイル ハッシュのチェックが失敗しました)
  - エラー: Manifest verification failed. (マニフェストの検証に失敗しました) Wrong version of manifest? (マニフェストのバージョンが正しくない可能性があります)

**回避策:** 次のいずれかを使用します。
 - セットアップ中には、CD.Latest フォルダーに含まれているファイルの代わりに、Microsoft から最新の再頒布可能ファイルをダウンロードすることを選択します。
 - *cd.latest\redist\languagepack\zhh* フォルダーを手動で削除してから、セットアップを再実行します。

### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>SQL Server がリモートの場合、または共有メモリが無効な場合、サービス接続ツールから例外がスローされる
バージョン 1606 以降、次のいずれかの条件に該当する場合、サービス接続ツールから例外が生成されます。  
 -  サービス接続ポイントをホストし、標準以外のポート (1433 以外のポート) を使用しているコンピューターとは別のコンピューターにサイト データベースがある
 -  サイト データベースがサービス接続ポイントと同じサーバー上にあるが、SQL プロトコルの**共有メモリ**が無効

次のような例外がスローされます。
 - *未処理の例外が発生しました: System.Data.SqlClient.SqlException: SQL Server への接続を確立しているときにネットワーク関連またはインスタンス固有のエラーが発生しました。サーバーが見つからなかったか、アクセスできませんでした。インスタンス名が正しいことと、SQL Server がリモート接続を許可するように構成されていることを確認してください。(プロバイダー: 名前付きパイプのプロバイダー、エラー: 40 - SQL Server への接続を開けませんでした) --*

**回避策**: ツールの使用時に、サービス接続ポイントをホストするサーバーのレジストリを変更して、SQL Server ポートに関する情報を含める必要があります。

   1.   このツールの使用前に、次のレジストリ キーを編集し、使用しているポート番号を SQL Server 名に追加します。
    - キー: HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - 値: &lt;SQL Server 名>
    - 追加: **,&lt;ポート番号>**

    たとえば、ポート *15001* を *testserver.test.net* というサーバーに追加する場合、結果のキーは ***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001*** になります。

   2.   ポートをレジストリに追加すると、ツールは正常に動作するようになります。  

   3.   ツールの使用が完了したら、**-connect** ステップと **-import** ステップの両方について、レジストリ キーを元の値に変更します。  






## <a name="backup-and-recovery"></a>バックアップと回復
### <a name="pre-production-client-is-not-available-after-a-site-restore"></a>サイトの復元の後、実稼働前クライアントは利用不可
バージョン 1602 で実稼働前クライアントを使用してバックアップから最上階層のサイトを復元すると、サイトが復元された後、実稼働前クライアント バージョンは利用できなくなります。  

**回避策:** 最上階層のサイトを復元した後、実稼働前クライアント ファイルを手動でコピーする必要があります。そうすると、Configuration Manager がそれらのファイルを使用できるように処理と復元を行います。
1. 最上位サイト サーバー コンピューターで、*&lt;CM_Install_Location\>\\Client* フォルダーの内容を *&lt;CM_Install_Location\>\\StagingClient* フォルダーにコピーします。

2. **client.acu** という名前の空のファイルを作成し、このファイルをサイト サーバーの *&lt;CM_Install_Location\>\\Inboxes\\hman*.box フォルダーにコピーまたはペーストします。 (このファイルはテキスト ファイルを名前変更したものでもかまいません。ただし、txt 拡張子は除去します。) hman.box フォルダーにこのファイルを配置すると、サイト サーバーの階層マネージャーは起動してクライアント ファイルを処理し、実稼働前クライアント ファイルを使用できるように復元します。

この問題は、バージョン 1606 で解決されます。


## <a name="client-deployment-and-upgrade"></a>クライアントの展開とアップグレード  

### <a name="expansion-to-central-administration-site-stops-automatic-client-upgrades"></a>中央管理サイトに拡張すると自動クライアント アップグレードが停止する  
バージョン 1511 のみで、プライマリ サイトから中央管理サイトに拡張されたすべてのサイトで、自動クライアント アップグレードを実行することはできません。 サイトが拡張されると、クライアント アップグレード パッケージの権限を持つサイトが、新しい中央管理サイトに正しく設定されないため、自動クライアント アップグレードを正常に実行できなくなります。 この問題は、バージョン 1511 にのみ存在します。 1602 およびそれ以降のバージョンでは、この問題は修正されています。  

**回避策:** 中央管理サイト データベースで次の SQL スクリプトを実行します。 スクリプトを実行すると、自動クライアント アップグレードの実行が正常に開始されます。  

  ```  
  DECLARE @RootSite AS NVARCHAR(3)  
  DECLARE @SourceServer AS NVARCHAR(255)  
  DECLARE @FullClientPkgSource AS NVARCHAR(255)  
  DECLARE @UpgradePkgSource AS NVARCHAR(255)  

  SELECT @RootSite = SiteCode, @SourceServer = SiteServer  
  FROM sites  
  WHERE ISNULL(ReportToSite, N'') = N''  

  SELECT @FullClientPkgSource = N'\\' + @SourceServer + N'\SMS_' + @RootSite + N'\Client'  
  SELECT @UpgradePkgSource = N'\\' + @SourceServer + N'\SMS_' + @RootSite + N'\ClientUpgrade'  

  UPDATE SMSPackages_G  
  SET Source = @FullClientPkgSource, SourceSite = @RootSite  
  WHERE PkgID IN  
      (SELECT FullPackageID FROM ClientDeploymentSettings)  

  UPDATE SMSPackages_G  
  SET Source = @UpgradePkgSource, SourceSite = @RootSite  
  WHERE PkgID IN  
      (SELECT UpgradePackageID FROM ClientDeploymentSettings)  

  UPDATE ProgramOffers_G  
  SET SourceSite = @RootSite  
  WHERE OfferID IN  
      (SELECT UpgradeAdvertisementID FROM ClientDeploymentSettings)  
  ```  

## <a name="operating-system-deployment"></a>オペレーティング システムの展開  

### <a name="issue-with-the-windows-adk-for-windows-10-version-1511"></a>Windows ADK for Windows 10 バージョン 1511 の問題  
Windows ADK 10 バージョン 1511 の Windows PE v.10.0.10586 ブート イメージを使用するソフトウェア センターからタスク シーケンスを実行すると、コンピューターが再起動されて Windows PE に移行するとき、"ハードウェア デバイスの初期化" 時に、エラー: **エラー コード 0x80220014 が発生して Windows PE の初期化に失敗しました** が発生して失敗します。  

**回避策**: 元の Windows 10 ADK を使用します。 詳細については、System Center Configuration Manager チームのブログ「 [Issue with the Windows ADK for Windows 10](http://blogs.technet.com/b/configmgrteam/archive/2015/11/20/issue-with-the-windows-adk-for-windows-10-version-1511.aspx)」を参照してください。  

### <a name="dynamic-application-installation-fails-during-task-sequence-which-successfully-completes"></a>正常に完了するタスク シーケンス中に動的なアプリケーションのインストールが失敗する  
**[動的な変数一覧に従ってアプリケーションをインストールする]**オプションを使用するタスク シーケンスを展開し、何らかの理由でインストールするアプリケーションのいずれかが失敗した場合に、タスク シーケンスによって成功がレポートされます。 このことは、次のオプションをどのように構成するかに関係なく発生します。  

-   **エラー時に続行する** ([アプリケーションのインストール] ステップの [オプション] タブ)  

-   **アプリケーションのインストールに失敗した場合に、一覧にある他のアプリケーションのインストールを続行する** ([アプリケーションのインストール] ステップの [プロパティ] タブ)  

アプリケーションのインストールが失敗したかどうかを判断するには、smsts.log を確認します。  

**回避策**: いずれかの動的なアプリケーションにエラーが発生した場合にタスク シーケンスが失敗する条件が指定されたタスク シーケンスの後続ステップで **_TSAppInstallStatus** 変数を条件として使用します。  

### <a name="smb-might-not-work-properly-after-you-use-a-task-sequence-to-install-windows-10"></a>タスク シーケンスを使用して Windows 10 をインストールした後で、SMB が正しく動作しない場合がある  
Windows 10 のイメージをインストールするタスク シーケンスを使用すると、Configuration Manager クライアントをインストールした後で SMB が正しく動作しない場合があります。 たとえば、次のタスク シーケンス ステップが失敗する可能性があります。  

-   状態移行ポイントとの併用時のユーザー状態の復元  

-   ネットワーク フォルダへの接続  

F8 管理者のコマンド プロンプトから、たとえば、引き続きコンピューターに ping を実行できますが、いずれかの SMB ネットワーク トラフィック (コマンド プロンプトからの NET USE など) がエラー 1231 (ネットワークの場所に到達できない) で失敗する場合があります。  

**回避策**:  
Windows と ConfigMgr のセットアップ タスク シーケンス ステップの後でコマンド ラインの実行タスク シーケンス ステップを追加して停止し、次のように、ワークステーション サービスを開始します。    
**net stop workstation /y & net start workstation**  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>既定で、サービス プランが多くの重複したソフトウェア更新プログラム グループと展開を作成する  
現在の既定では、サービス プランの作成ウィザードが、すべてのソフトウェア更新プログラムの同期後に実行されます。 ウィザードを実行するたびに新しいソフトウェア更新プログラム グループと展開が作成されます。 1 日に複数回実行するソフトウェア更新プログラムの同期スケジュールがある場合、たとえば、サービス プランの作成ウィザードが複数の同一であるソフトウェア更新プログラム グループと展開を毎日作成します。  

**回避策**:    
サービス プランを作成した後で、サービス プランのプロパティを開き、**[評価スケジュール]** タブに移動し、**[スケジュールに基づいて規則を実行する]** を選んで、**[カスタマイズ]** をクリックし、カスタム スケジュールを作成します。 たとえば、60 日おきに実行するサービス プランを作成できます。  

## <a name="mobile-device-management"></a>モバイル デバイス管理  

### <a name="cannot-create-an-enrollment-profile-on-a-primary-site"></a>プライマリ サイトで登録プロファイルを作成できない  
管理者は、プライマリ サイトに接続する System Center Configuration Manager 管理コンソールで、登録プロファイルを作成できません。 登録時に、管理者に対して、登録プロファイル ウィザードでエラー "DEP トークンが更新されていません。 DEP トークンをアップロードしてください" が表示されます。 このエラーは、有効な DEP トークンが中央管理サイトにアップロードされている場合でも発生します。  

**回避策**: 中央管理サイトに接続する System Center Configuration Manager コンソールで、登録プロファイルを作成します。  

### <a name="dep-cannot-use-non-alpha-numeric-characters-in-enrollment-profiles"></a>DEP の登録プロファイルで英数字以外の文字が使用できない  
Apple のデバイス登録プロファイル (DEP) と関連付けられている登録プロファイルで、DEP が有効になっている場合に、登録プロファイルの **[名前]**、 **[説明]**、 **[部署]** 、および **[電話番号]** フィールドで英数字以外の文字を使用できません。 これらのフィールドに英数字以外の文字を使用すると、登録プロファイルが作成されますが、プロファイルを Apple にアップロードすることはできません。 Apple サーバーによってエラー メッセージまたは警告が表示されず、プロファイルは、DEP で管理されたデバイスに展開されません。  

**回避策:** なし。

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>フル ワイプを実行すると 4 GB RAM 未満の Windows 10 デバイスが無効になる

RAM が 4 GB 未満の Windows 10 RTM デバイスでフル ワイプを実行すると (バージョン 1511 より前のバージョン)、デバイスが使用不可のままになる場合があります。 ワイプを試みた後、デバイスは起動できなくなり、応答しなくなります。

**回避策**: デバイスのフル ワイプを実行する前に、Windows 10 RTM PC が 4 GB 以上の RAM を搭載していることを確認します。 Windows 10 デバイスのバージョン番号を表示するには、コマンド プロンプトで 'winver' と入力します。 既にデバイスをワイプして応答しなくなった場合は、起動可能な Windows 10 の USB ドライブを使用して起動し、デバイスへのアクセスを回復します。

### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>1 人のユーザーが、使用条件ポリシーが展開されている複数のユーザー コレクションに属する場合は、同じ条項が複数表示されます。  

管理者が複数のユーザー コレクションに一連の条項を展開し、ユーザーがその中の複数のコレクションのメンバーである場合、ユーザーが会社のポータルを開くと、同じ条項のコピーが複数表示されます。  たとえば、"SampleUser" という名前のユーザーが 2 つの別のユーザー コレクション ("CompanyEmployeesFTE" と "CompanyEmployeesNA") のメンバーであり、"CompanyTerms" と呼ばれる使用条件が CompanyEmployeesFTE と CompanyEmployeesNA の両方に展開されている場合、SampleUser の使用条件への同意ページには、2 つの同じ CompanyTerms が表示されます。 ユーザーが同意または拒否できるのはすべての条項に関してのみであるため、(ユーザーが同意と拒否の両方を行って) 条件に関してあいまいな状態になるという危険はありません。 使用条件への同意レポートには、ユーザーごとにそれぞれの条件セットに対して 1 行ずつしか含まれません。レポートにエラーは含まれません。 唯一の影響は、同意ページに 2 セットの条項が表示されることです。  

**回避策**: 各ユーザーが、条項が展開される 1 つのコレクションにのみ含まれていることを確認します。  

## <a name="reports-and-monitoring"></a>レポートおよび監視  

### <a name="the-health-attestation-report-is-empty-even-though-health-attestation-data-was-previously-collected"></a>正常性構成証明書のデータが以前に収集された場合でも、正常性構成証明書のレポートが空になる  
**正常性構成証明書**アクセス許可グループに対する**読み取り**アクセス許可を含むセキュリティ ロールを持つ管理ユーザーが正常性構成証明書のレポートを表示すると、レポートが空になり、データを表示できません。 これは、正常性構成証明書のレポートのデータを表示する権限が、正常性構成証明書アクセス許可グループではなく、**ユーザーとデバイスのアフィニティ** アクセス許可グループにリンクされているためです。  

この問題は、更新プログラム 1602 を適用した System Center Configuration Manager に影響し、今後の更新プログラムで解決される予定です。  

**回避策**: 管理ユーザーに、**ユーザーとデバイスのアフィニティ** アクセス許可グループに対する**読み取り**アクセス許可を含むセキュリティ グループを割り当てます。  

### <a name="conditional-access"></a>条件付きアクセス  

#### <a name="the-same-user-collection-is-not-blocked-from-being-added-to-both-exempted-and-targeted-collections"></a>同じユーザー コレクションは、例外コレクションと対象となるコレクションの両方への追加がブロックされません。  
これは、**対象となるコレクション** ページにユーザー コレクションを追加**する前に**、同じ**ユーザー コレクション**を**例外コレクション** ページに追加するときにのみ発生します。  最初に **対象となるコレクション** ページに**ユーザー コレクション**を追加して、同じ**ユーザー コレクション**を**例外コレクション** ページに追加しようとすると、通常のブロッキング メッセージが表示されます。  

この問題は、更新プログラム 1602 の **Exchange On-premises** の ystem Center Configuration Manager 条件付きアクセスに影響を与え、今後の更新プログラムでの解決を予定しています。  

**回避策:** **例外コレクション** ページで**ユーザー コレクション**を選ぶ前に**対象となるコレクション ページ**に**ユーザー コレクション**を追加して、例外コレクションと対象となるコレクションの両方に同じ**ユーザー コレクション**を追加していないことを確認します。



<!--HONumber=Dec16_HO3-->


