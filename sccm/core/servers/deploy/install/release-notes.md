---
title: "リリース ノート "
titleSuffix: Configuration Manager
description: "製品でまだ修正されていないまたは Microsoft サポート技術情報の記事で説明されていない緊急の問題については以下のメモを参照してください。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53685ef2647cfd87c2fcb603097186360f1c96a5
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2018
---
# <a name="release-notes-for-system-center-configuration-manager"></a>System Center Configuration Manager リリース ノート

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager 製品のリリース ノートには、緊急の問題のみが記載されています。 これらの問題はまだ、製品で修正されていないか、または Microsoft サポート技術情報の記事で詳しく説明されていません。  

機能固有のドキュメントには、主要なシナリオに影響を与える既知の問題に関する情報が含まれます。  

> [!TIP]  
>  このトピックには、Configuration Manager の現在のブランチのリリース ノートが含まれています。 Technical Preview ブランチについては、「[System Center Configuration Manager の Technical Preview](../../../../core/get-started/technical-preview.md)」をご覧ください。  

異なるバージョンで導入された新しい機能については、以下の記事をご覧ください。
- [バージョン 1710 の新機能](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [バージョン 1706 の新機能](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [バージョン 1702 の新機能](/sccm/core/plan-design/changes/whats-new-in-version-1702)



## <a name="setup-and-upgrade"></a>セットアップとアップグレード  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>バージョン 1606 を使用して Long-Term Service Branch をインストールすると、Current Branch サイトがインストールされる
<!-- Consider move to core content  -->
2016 年 10 月リリースのバージョン 1606 ベースライン メディアを使用して Long-Term Servicing Branch (LTSB) サイトをインストールすると、代わりに Current Branch サイトがインストールされます。 この動作は、サイトのインストールでサービス接続ポイントをインストールするオプションがオフのために発生します。

 - サービス接続ポイントは必須ではありませんが、LTSB サイトをインストールするには、セットアップ時にインストールするオプションをオンにする必要があります。

セットアップが完了したら、サービス接続ポイントをアンインストールすることができます。 ただし、Current Branch サイトと LTSB サイトの両方でテレメトリ データを送信し、セキュリティ更新プログラムを取得するには、オフライン モードまたはオンライン モードのサービス接続ポイントが存在する必要があります。

既に Current Branch サイトとしてサイトがインストールされていて、LTSB をインストールする場合は、サイトをアンインストールしてから再インストールします。 不明な点については、[Microsoft ヘルプおよびサポート](http://go.microsoft.com/fwlink/?LinkId=243064)で検索または問い合わせてください。  

インストールされているブランチを確認するには、コンソールで **[管理]** > **[サイトの構成]** > **[サイト]** を選択し、**[階層設定]** を開きます。 サイトを Current Branch サイトに変換するオプションは、サイトが LTSB を実行している場合にのみ使用できます。  

**対応策 :** なし。   


### <a name="an-update-persists-in-downloading-state-in-the-updates-and-servicing-node-of-the-console"></a>コンソールの [更新とサービス] ノードで更新プログラムがダウンロード中状態のままになる  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
オンライン サービス接続ポイントによる更新プログラムの自動ダウンロード中に、更新プログラムがダウンロード中の状態でスタックする場合があります。 更新プログラムのダウンロードがスタックしている場合、指定されたログ ファイルに、次のようなエントリが表示されます。  

DMPdownloader ログ:  
`ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"`  

ConfigMgrSetup.log:  
`Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.`  
`Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi`  

**回避策**: サイト サーバーで、次のレジストリ キーを次の値と一致するように変更します。  

-   **編集するキー**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **状態の値**: **146944** (10 進数) または **0x00023e00** (16 進数) に設定します  

その後、SMS_Executive サービスを開始し直すか、または次の自動ダウンロード サイクルまで最大 24 時間待ちます。

### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>CD.Latest フォルダーの再頒布可能ファイルを使用すると、マニフェスト検証エラーでセットアップが失敗する
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

バージョン 1606 用に作成された CD.Latest フォルダーからセットアップを実行し、その CD.Latest フォルダーに含まれている再頒布可能ファイルを使うと、Configuration Manager のセットアップ ログに次のエラーが記録されてセットアップが失敗します。

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

**回避策**: 次のいずれかのオプションを使います。
 - セットアップ中に、Microsoft から提供されている最新の再頒布可能ファイルのダウンロードを選びます。 CD.Latest フォルダーのファイルではなく、最新の再頒布可能ファイルを使います。
 - *cd.latest\redist\languagepack\zhh* フォルダーを手動で削除してから、セットアップを再実行します。



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>クライアントの展開とアップグレード  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>クライアントのインストールが失敗し、エラー コード 0x8007064c が返される
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*次の問題は、アクティブなすべてのバージョンの Configuration Manager に適用されます。*  

Windows コンピューターにクライアントを展開すると、インストールが失敗します。 ccmsetup.log ファイルには以下のエントリが含まれます。 

`File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation`  
`InstallFromManifest failed 0x8007064c`

**回避策**: 以前にインストールしたバージョンの Silverlight の破損がこの問題の原因です。 この問題を解決するには、影響を受けたコンピューターで「[プログラムのインストールまたは削除をブロックしている問題を解決する](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)」のツールを実行します。

## <a name="operating-system-deployment"></a>オペレーティング システムの展開  

### <a name="servicing-plans-create-many-duplicate-software-update-groups-and-deployments-by-default"></a>既定で、サービス プランが多くの重複したソフトウェア更新プログラム グループと展開を作成する  
現在の既定では、サービス プランの作成ウィザードが、すべてのソフトウェア更新プログラムの同期後に実行されます。 ウィザードを実行するたびに新しいソフトウェア更新プログラム グループと展開が作成されます。 1 日に複数回実行するソフトウェア更新プログラムの同期スケジュールがある場合、サービス プランの作成ウィザードが複数のソフトウェア更新プログラム グループと展開を毎日作成します。  

**回避策**: サービス プランを作成した後、サービス プランのプロパティを開き、**[評価スケジュール]** タブに移動し、**[スケジュールに基づいて規則を実行する]** を選んで、**[カスタマイズ]** をクリックし、カスタム スケジュールを作成します。 たとえば、60 日おきに実行するサービス プランを作成できます。  



## <a name="software-updates"></a>ソフトウェア更新プログラム

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>サポートされていない言語が含まれている場合、構成ファイルからの Office 365 クライアント設定のインポートが失敗する
<!-- 489258  Fixed in 1706  -->
*次の問題は、バージョン 1702 以前のバージョンに適用されます。*   

既存の XML 構成ファイルから Office 365 クライアント設定をインポートするときに、ファイルに Office 365 ProPlus クライアントでサポートされていない言語が含まれている場合は、エラーが発生します。 詳細については、[Office 365 クライアント管理ダッシュボードからのクライアントへの Office 365 アプリの展開](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard)に関するページを参照してください。

**回避策**: XML 構成ファイルに、[Office 365 ProPlus クライアントでサポートされる言語](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx)のみを含めます。  



## <a name="mobile-device-management"></a>モバイル デバイス管理  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>バージョン 1710 以降、Windows Phone 8.1 の VPN プロファイルを Windows 10 に展開できなくなりました   <!-- 503274  Should be fixed by 1802, if not sooner -->
1710 では、Windows 10 デバイスにも適用可能な Windows Phone 8.1 ワークフローを使用して、VPN プロファイルを作成することができなくなりました。 これらのプロファイルについては、[サポートされているプラットフォーム] ページが作成ウィザードに表示されなくなります。 バックエンドでは Windows Phone 8.1 が自動的に選択されます。 プロファイルのプロパティでは [サポートされているプラットフォーム] ページを使用できますが、Windows 10 のオプションは表示されません。

**回避策**: Windows 10 デバイス用の Windows 10 VPN プロファイル ワークフローを使用してください。 お使いの環境でこのオプションを実行できない場合は、サポートにお問い合わせください。 サポートは、Windows 10 のターゲット設定の追加を支援することができます。


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-of-memory"></a>フル ワイプを実行するとメモリが 4 GB 未満の Windows 10 デバイスが無効になる
Windows 10 バージョン 1507 を搭載している RAM が 4 GB 未満のデバイスでフル ワイプを実行すると、デバイスが使用不可のままになる場合があります。 ワイプを試みた後、デバイスは起動できなくなり、応答しなくなります。

**回避策**: フル ワイプを実行する前に、Windows 10 デバイスで少なくとも 4 GB のメモリを使用できることを確認してください。 Windows 10 デバイスのバージョン番号を表示するには、コマンド プロンプトで 'winver' と入力します。 既にデバイスをワイプして応答しなくなった場合は、起動可能な Windows 10 の USB ドライブを使って、デバイスを復旧します。


### <a name="when-a-user-belongs-to-two-or-more-user-collections-to-which-you-deploy-a-terms-and-conditions-policy-the-user-sees-multiple-sets-of-the-same-terms"></a>1 人のユーザーが、使用条件ポリシーが展開されている複数のユーザー コレクションに属する場合は、同じ条項が複数表示される  
<!-- 454394    -->
複数のユーザー コレクションに条項のセットを展開し、ユーザーがその中の複数のコレクションのメンバーである場合、会社のポータルで同じ条項のコピーが複数表示されます。 次に例を示します。
- ユーザー "SampleUser" は、2 つの異なるユーザー コレクション "CompanyEmployeesFTE" と "CompanyEmployeesNA" のメンバーです
- CompanyEmployeesFTE と CompanyEmployeesNA の両方に、"CompanyTerms" 使用条件を展開します
- SampleUser には、会社のポータルの条件同意ページで、2 つのまったく同じ companyterms が表示されます。 

ユーザーは、すべての条項に同意すること、またはすべてに同意しないことしかできません。 したがって、承諾状態があいまいになる危険はありません (ユーザーが同じ条項を承諾かつ拒否している状態)。 使用条件への同意レポートには、ユーザーごとにそれぞれの条件セットに対して 1 行ずつしか含まれません。レポートにエラーは含まれません。 唯一の影響は、同意ページに 2 セットの条項が表示されることです。  

**回避策**: 各ユーザーが、条項が展開される 1 つのコレクションにのみ含まれていることを確認します。  


<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
