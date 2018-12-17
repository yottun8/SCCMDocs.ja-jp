---
title: リリース ノート
titleSuffix: Configuration Manager
description: 製品でまだ修正されていないまたは Microsoft サポート技術情報の記事で説明されていない緊急の問題について説明します。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 41039ec31c11573424f044df009e9c364491b5f7
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456347"
---
# <a name="release-notes-for-configuration-manager"></a>Configuration Manager のリリース ノート

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager 製品のリリース ノートには、緊急の問題のみが記載されています。 これらの問題はまだ、製品で修正されていないか、または Microsoft サポート技術情報の記事で詳しく説明されていません。  

機能固有のドキュメントには、主要なシナリオに影響を与える既知の問題に関する情報が含まれます。  

> [!TIP]  
>  このトピックには、Configuration Manager の現在のブランチのリリース ノートが含まれています。 Technical Preview ブランチについては、「[Technical Preview](/sccm/core/get-started/technical-preview)」を参照してください。  

異なるバージョンで導入された新しい機能については、以下の記事をご覧ください。
- [バージョン 1810 の新機能](/sccm/core/plan-design/changes/whats-new-in-version-1810)
- [バージョン 1806 の新機能](/sccm/core/plan-design/changes/whats-new-in-version-1806)  
- [バージョン 1802 の新機能](/sccm/core/plan-design/changes/whats-new-in-version-1802)



## <a name="setup-and-upgrade"></a>セットアップとアップグレード  


### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>CD.Latest フォルダーの再頒布可能ファイルを使用すると、マニフェスト検証エラーでセットアップが失敗する
<!-- 510080, 490569  -->

バージョン 1606 用に作成された CD.Latest フォルダーからセットアップを実行し、その CD.Latest フォルダーに含まれている再頒布可能ファイルを使うと、Configuration Manager のセットアップ ログに次のエラーが記録されてセットアップが失敗します。

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

#### <a name="workaround"></a>回避策
次のいずれかのオプションを使用します。
 - セットアップ中に、Microsoft から提供されている最新の再頒布可能ファイルのダウンロードを選びます。 CD.Latest フォルダーのファイルではなく、最新の再頒布可能ファイルを使います。
 - *cd.latest\redist\languagepack\zhh* フォルダーを手動で削除してから、セットアップを再実行します。


### <a name="setup-command-line-option-joinceip-must-be-specified"></a>セットアップのコマンドライン オプション JoinCEIP を指定する必要がある
<!--510806-->
*適用対象: Configuration Manager バージョン 1802*

Configuration Manager バージョン 1802 以降では、カスタマー エクスペリエンス向上プログラム (CEIP) 機能が製品から削除されます。 コマンドラインまたは無人スクリプトから新しいサイトの[インストールを自動化する](/sccm/core/servers/deploy/install/command-line-options-for-setup)ときに、セットアップから必要なパラメーターが不足しているというエラーが返されます。 

#### <a name="workaround"></a>回避策
セットアップ プロセスの結果に影響しませんが、**JoinCEIP** パラメーターをセットアップのコマンドラインに含めます。

 > [!Note]  
 > [コンソールのセットアップ](/sccm/core/servers/deploy/install/install-consoles)の EnableSQM パラメーターは必要ありません。


### <a name="cloud-service-manager-component-stopped-on-site-server-in-passive-mode"></a>パッシブ モードのサイト サーバー上でクラウド サービス マネージャー コンポーネントが停止している
<!--VSO 2858826, SCCMDocs issue 772-->
*適用対象: Configuration Manager バージョン 1806*

[サービス接続ポイント](/sccm/core/servers/deploy/configure/about-the-service-connection-point)が[パッシブ モードのサイト サーバー](/sccm/core/servers/deploy/configure/site-server-high-availability)と同じ場所にある場合、[クラウド管理ゲートウェイ](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)の展開および監視は開始しません。 クラウド サービス マネージャー コンポーネント (SMS_CLOUD_SERVICES_MANAGER) は停止状態になります。

#### <a name="workaround"></a>回避策
サービス接続ポイントの役割を別のサーバーに移動します。



<!-- ## Backup and recovery  -->


<!--## Client deployment and upgrade-->



<!-- ## Operating system deployment  -->



## <a name="software-updates"></a>ソフトウェア更新プログラム

### <a name="changing-office-365-client-setting-doesnt-apply"></a>Office 365 クライアント設定の変更が適用されない 
<!--511551-->
*適用対象: Configuration Manager バージョン 1802*  

**[Enable Management of the Office 365 Client Agent]\(Office 365 クライアント エージェントの管理を有効にする\)** を `Yes` に構成した状態で、[クライアント設定](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent)をデプロイします。 その後で、その設定を `No` または `Not Configured` に変更します。 Office 365 更新プログラムは、ターゲットのクライアント上でポリシーを更新した後も、Configuration Manager によって管理されます。 

#### <a name="workaround"></a>回避策
次のレジストリ値を `0` に変更し、**Microsoft Office クイック実行サービス** (ClickToRunSvc) を再起動します。

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```



## <a name="mobile-device-management"></a>モバイル デバイス管理  

### <a name="you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10"></a>Windows Phone 8.1 の VPN プロファイルを Windows 10 に展開できなくなった
<!-- 503274  -->
*適用対象: Configuration Manager バージョン 1710*

Windows Phone 8.1 ワークフローを使用して、Windows 10 デバイスにも適用可能な VPN プロファイルを作成することができなくなりました。 これらのプロファイルについては、[サポートされているプラットフォーム] ページが作成ウィザードに表示されなくなります。 バックエンドでは Windows Phone 8.1 が自動的に選択されます。 プロファイルのプロパティでは [サポートされているプラットフォーム] ページを使用できますが、Windows 10 のオプションは表示されません。

#### <a name="workaround"></a>回避策
 Windows 10 デバイス用の Windows 10 VPN プロファイル ワークフローを使用してください。 お使いの環境でこのオプションを実行できない場合は、サポートにお問い合わせください。 サポートは、Windows 10 のターゲット設定の追加を支援することができます。



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
