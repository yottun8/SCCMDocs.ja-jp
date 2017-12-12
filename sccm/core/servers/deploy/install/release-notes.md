---
title: "リリース ノート "
titleSuffix: Configuration Manager
description: "製品でまだ修正されていないまたは Microsoft サポート技術情報の記事で説明されていない緊急の問題については以下のメモを参照してください。"
ms.custom: na
ms.date: 11/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 8030ce7f98ebb34d9581ad036513b9b1c879c0ad
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2017
---
# <a name="release-notes-for-system-center-configuration-manager"></a>System Center Configuration Manager リリース ノート

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の製品リリース ノートは、この製品でまだ修正されていない緊急の問題 (コンソール内更新から入手可能)、または Microsoft サポート技術情報の記事で詳しく説明している緊急の問題のみに限定されています。  

主要なシナリオに影響を与える既知の問題については、System Center Configuration Manager ドキュメント ライブラリのオンライン製品ドキュメントをご覧ください。  

> [!TIP]  
>  このトピックには、System Center Configuration Manager の現在のブランチのリリース ノートが含まれています。 System Center Configuration Manager の Technical Preview の場合は、「[System Center Configuration Manager の Technical Preview](../../../../core/get-started/technical-preview.md)」を参照してください。  

異なるバージョンで導入された新しい機能については、次をご覧ください。
- [バージョン 1706 の新機能](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [バージョン 1702 の新機能](/sccm/core/plan-design/changes/whats-new-in-version-1702)
- [バージョン 1610 の新機能](/sccm/core/plan-design/changes/whats-new-in-version-1610)



## <a name="setup-and-upgrade"></a>セットアップとアップグレード  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>バージョン 1606 を使用して Long-Term Service Branch をインストールすると、Current Branch サイトがインストールされる
<!-- Consider move to core content  -->
2016 年 10 月リリースのバージョン 1606 ベースライン メディアを使用して Long-Term Servicing Branch (LTSB) サイトをインストールすると、代わりに Current Branch サイトがインストールされます。 この問題は、サイトのインストールでサービス接続ポイントをインストールするオプションがオフのために発生します。

 - サービス接続ポイントは必須ではありませんが、LTSB サイトをインストールするには、セットアップ時にインストールするオプションをオンにする必要があります。

セットアップが完了したら、サービス接続ポイントをアンインストールすることができます。  ただし、Current Branch サイトと LTSB サイトの両方でテレメトリ データを送信し、セキュリティ更新プログラムを取得するには、オフライン モードまたはオンライン モードのサービス接続ポイントが存在する必要があります。

既に Current Branch サイトとしてサイトがインストールされていて、LTSB をインストールする場合は、サイトをアンインストールしてから再インストールします。 不明な点については、[Microsoft ヘルプおよびサポート](http://go.microsoft.com/fwlink/?LinkId=243064)で検索または問い合わせてください。  

インストールされているブランチを確認するには、コンソールで **[管理]** > **[サイトの構成]** > **[サイト]** を選択し、**[階層設定]** を開きます。 サイトを Current Branch サイトに変換するオプションは、サイトが LTSB を実行している場合にのみ使用できます。  

**回避策:**  なし。   


### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>更新プログラムが Configuration Manager コンソールの更新プログラムとサービス ノードでダウンロード中の状態でスタックする  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
オンライン サービス接続ポイントによる更新プログラムの自動ダウンロード中には、更新プログラムがダウンロード中の状態でスタックする場合があります。 更新プログラムのダウンロードがスタックしている場合、指定されたログ ファイルに、次のようなエントリが表示されます。  

DMPdownloader ログ:  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log:  

-   Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**回避策**: サイト サーバーで、次に一致するように次のレジストリ キーを変更し、SMS_Executive サービスを再起動するか、次回の自動ダウンロード サイクルを最大で 24 時間待機します。  

-   **編集するキー**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **状態の値**: **146944** の 10 進数または **0x00023e00** の 16 進数に設定  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>CD.Latest フォルダーの再頒布可能ファイルを使用するとマニフェストの検証エラーのためにセットアップが失敗します。
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

バージョン 1606 用に作成された CD.Latest フォルダーからセットアップを実行し、その CD.Latest フォルダーに含まれている再頒布可能ファイルを使用すると、Configuration Manager のセットアップ ログに次のエラーが記録されてセットアップが失敗します。

  - エラー: File hash check failed for defaultcategories.dll (defaultcategories.dll のファイル ハッシュのチェックが失敗しました)
  - エラー: Manifest verification failed. (マニフェストの検証に失敗しました) Wrong version of manifest? (マニフェストのバージョンが正しくない可能性があります)

**回避策:** 次のいずれかを使用します。
 - セットアップ中には、CD.Latest フォルダーに含まれているファイルの代わりに、Microsoft から最新の再頒布可能ファイルをダウンロードすることを選択します。
 - *cd.latest\redist\languagepack\zhh* フォルダーを手動で削除してから、セットアップを再実行します。



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>クライアントの展開とアップグレード  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>クライアントのインストールが失敗し、エラー コード 0x8007064c が返される
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*次のものは、アクティブなすべてのバージョンの Configuration Manager に適用されます。*   
アクティブなすべてのバージョンで、Windows コンピューターにクライアントを展開すると、インストールが失敗します。 ccmsetup.log ファイルには、"ファイル 'C:\WINDOWS\ccmsetup\Silverlight.exe' がエラー終了コード 1612 を返しました。 インストールに失敗しました" というエントリに続き、"0x8007064c で InstallFromManifest のエラーが発生しました" というエントリが含まれます。

**回避策**: 以前にインストールしたバージョンの Silverlight の破損が原因です。 影響を受けたコンピューターで次のツールを試すと、この問題を解決できる場合があります。[https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>オペレーティング システムの展開  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>既定で、サービス プランが多くの重複したソフトウェア更新プログラム グループと展開を作成する  
現在の既定では、サービス プランの作成ウィザードが、すべてのソフトウェア更新プログラムの同期後に実行されます。 ウィザードを実行するたびに新しいソフトウェア更新プログラム グループと展開が作成されます。 1 日に複数回実行するソフトウェア更新プログラムの同期スケジュールがある場合、たとえば、サービス プランの作成ウィザードが複数の同一であるソフトウェア更新プログラム グループと展開を毎日作成します。  

**回避策**:    
サービス プランを作成した後で、サービス プランのプロパティを開き、**[評価スケジュール]** タブに移動し、**[スケジュールに基づいて規則を実行する]** を選んで、**[カスタマイズ]** をクリックし、カスタム スケジュールを作成します。 たとえば、60 日おきに実行するサービス プランを作成できます。  



## <a name="software-updates"></a>ソフトウェア更新プログラム

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>サポートされていない言語が含まれている場合、構成ファイルからの Office 365 クライアント設定のインポートが失敗する
<!-- 489258  Fixed in 1706  -->
*次のものは、バージョン 1702 以前のバージョンに適用されます。*   
既存の XML 構成ファイルから Office 365 クライアント設定をインポートするときに、ファイルに Office 365 ProPlus クライアントでサポートされていない言語が含まれている場合は、エラーが発生します。 詳細については、[Office 365 クライアント管理ダッシュボードからのクライアントへの Office 365 アプリの展開](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard)に関するページを参照してください。

**回避策**:    
XML 構成ファイルに、[Office 365 ProPlus クライアントでサポートされる言語](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx)のみを含めます。  



## <a name="mobile-device-management"></a>モバイル デバイス管理  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>バージョン 1710 以降、Windows Phone 8.1 の VPN プロファイルを Windows 10 に展開できなくなりました   <!-- 503274  Should be fixed by 1802, if not sooner -->
1710 では、Windows 10 デバイスにも適用可能な Windows Phone 8.1 ワークフローを使用して、VPN プロファイルを作成することができなくなりました。 これらのプロファイルの場合は、作成ウィザードに [サポートされているプラットフォーム] ページが表示されなくなり、Windows Phone 8.1 はバックエンドで自動的に選択されます。プロパティ ページでは、[サポートされているプラットフォーム] ページを利用できますが、Windows 10 のオプションは表示されません。

**回避策**: Windows 10 デバイス用の Windows 10 VPN プロファイル ワークフローを使用してください。 ご利用の環境でそれが実行不可能な場合は、サポートにお問い合わせください。 サポートは、必要に応じて、Windows 10 のターゲット設定の追加を支援することができます。


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>フル ワイプを実行すると 4 GB RAM 未満の Windows 10 デバイスが無効になる
RAM が 4 GB 未満の Windows 10 RTM デバイスでフル ワイプを実行すると (バージョン 1511 より前のバージョン)、デバイスが使用不可のままになる場合があります。 ワイプを試みた後、デバイスは起動できなくなり、応答しなくなります。

**回避策**: デバイスのフル ワイプを実行する前に、Windows 10 RTM PC が 4 GB 以上の RAM を搭載していることを確認します。 Windows 10 デバイスのバージョン番号を表示するには、コマンド プロンプトで 'winver' と入力します。 既にデバイスをワイプして応答しなくなった場合は、起動可能な Windows 10 の USB ドライブを使用して起動し、デバイスへのアクセスを回復します。


### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>1 人のユーザーが、使用条件ポリシーが展開されている複数のユーザー コレクションに属する場合は、同じ条項が複数表示されます。  
<!-- 454394    -->
管理者が複数のユーザー コレクションに一連の条項を展開し、ユーザーがその中の複数のコレクションのメンバーである場合、ユーザーが会社のポータルを開くと、同じ条項のコピーが複数表示されます。  たとえば、"SampleUser" という名前のユーザーが 2 つの別のユーザー コレクション ("CompanyEmployeesFTE" と "CompanyEmployeesNA") のメンバーであり、"CompanyTerms" と呼ばれる使用条件が CompanyEmployeesFTE と CompanyEmployeesNA の両方に展開されている場合、SampleUser の使用条件への同意ページには、2 つの同じ CompanyTerms が表示されます。 ユーザーが同意または拒否できるのはすべての条項に関してのみであるため、(ユーザーが同意と拒否の両方を行って) 条件に関してあいまいな状態になるという危険はありません。 使用条件への同意レポートには、ユーザーごとにそれぞれの条件セットに対して 1 行ずつしか含まれません。レポートにエラーは含まれません。 唯一の影響は、同意ページに 2 セットの条項が表示されることです。  

**回避策**: 各ユーザーが、条項が展開される 1 つのコレクションにのみ含まれていることを確認します。  


### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>証明書の認証を使用する Android for Work の電子メール プロファイルは、デバイスには適用されません
<!--  487657      -->
Android for Work の電子メール プロファイルを作成する場合、認証には 2 つのオプションがあります。 1 つはユーザー名とパスワード、もう 1 つは証明書です。 この時点で、証明書のオプションは動作していません。 **証明書**に設定する認証方法でプロファイルを作成する場合、プロファイルはデバイスに適応されず、ユーザーは電子メール アカウントの詳細を手動で入力することを要求されます。

**回避策**: ありません。 管理者は、**ユーザー名とパスワード**のオプションを使用するか、この問題が解決するまで待つ必要があります。



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
