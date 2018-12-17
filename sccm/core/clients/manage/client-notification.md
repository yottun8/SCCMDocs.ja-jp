---
title: クライアント通知
titleSuffix: Configuration Manager
description: 中央の Configuration Manager コンソールから早急な対応を行うことで、クライアントを管理します。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8aa38217c3e9456a074a984b66feb83bdb192801
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52458138"
---
# <a name="client-notification-in-configuration-manager"></a>Configuration Manager のクライアント通知

*適用対象: System Center Configuration Manager (Current Branch)*

リモート クライアントで早急な対応を行うには、Configuration Manager コンソールからクライアント通知アクションを送信します。 個別のデバイスまたはデバイスのコレクションでこれらのアクションを開始します。 



## <a name="actions"></a>操作

次のアクションは、[ホーム] タブの [デバイス] または [コレクション] グループのリボンにあります。 


### <a name="install-client"></a>クライアントのインストール

**クライアントのインストール ウィザード**を開きます。 このウィザードでは、クライアント プッシュ インストールを使用して、Configuration Manager クライアントをインストールします。 詳しくは、「[クライアント プッシュ インストール](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush)」をご覧ください。

#### <a name="permissions"></a>アクセス許可
このアクションには、**コレクション** オブジェクトに対する**リソースの変更**と**読み取り**のアクセス許可が必要です。 

次の組み込みロールには、既定でこれらのアクセス許可があります。
- アプリケーション管理者  
- 完全な権限を持つ管理者  
- インフラストラクチャ管理者  
- オペレーション管理者  
- OS 展開マネージャー  

これらのアクセス許可を、クライアントをプッシュする必要がある任意のカスタム ロールに追加します。


### <a name="run-script"></a>スクリプトの実行

**スクリプトの実行**ウィザードを開き、コレクション内のすべてのクライアントで PowerShell スクリプトを実行します。 詳しくは、「[PowerShell スクリプトの作成と実行](/sccm/apps/deploy-use/create-deploy-scripts)」をご覧ください。

#### <a name="permissions"></a>アクセス許可
このアクションには、**コレクション** オブジェクトに対する**スクリプトの実行**アクセス許可が必要です。 

次の組み込みロールには、既定でこのアクセス許可があります。
- 完全な権限を持つ管理者  
- インフラストラクチャ管理者  
- オペレーション管理者  

このアクセス許可を、スクリプトを実行する必要があるカスタム ロールに追加します。


### <a name="start-cmpivot"></a>CMPivot の開始

対象のデバイスに対してリアルタイムでクエリを実行する **CMPivot** を開始します。 詳細については、[CMPivot](/sccm/core/servers/manage/cmpivot) に関するページを参照してください。

#### <a name="permissions"></a>アクセス許可
このアクションには、[スクリプトの実行](#run-script)アクションと同じアクセス許可が必要です。 



## <a name="client-notification"></a>クライアント通知

これらのアクションは、[ホーム] タブの [デバイス] または [コレクション] グループのリボンにある、**[クライアント通知]** メニューにあります。


#### <a name="permissions"></a>アクセス許可
<!--SCCMDocs-pr issue #2972--> バージョン 1810 以降では、クライアント通知アクションに、コレクション オブジェクトに対する**リソースの通知**アクセス許可が必要になりました。 このアクセス許可は、**[クライアント通知]** メニューの下のすべてのアクションに適用されます。 

次の組み込みロールには、既定でこのアクセス許可があります。
- 完全な権限を持つ管理者  
- インフラストラクチャ管理者  

クライアント通知アクションを使用する必要があるカスタム ロールには、このアクセス許可を追加してください。


### <a name="download-computer-policy"></a>コンピューター ポリシーのダウンロード

デバイス ポリシーを更新します。 詳細については、「[Configuration Manager クライアントのポリシーの取得開始](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval)」を参照してください。  


### <a name="download-user-policy"></a>ユーザー ポリシーのダウンロード

ユーザー ポリシーを更新します。  


### <a name="collect-discovery-data"></a>検出データの収集

クライアントによる探索データ レコード (DDR) の送信をトリガーします。 詳しくは、「[定期探索](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat)」をご覧ください。  


### <a name="collect-software-inventory"></a>ソフトウェア インベントリの収集

クライアントによるソフトウェア インベントリ サイクルの実行をトリガーします。 詳しくは、「[ソフトウェア インベントリの概要](/sccm/core/clients/manage/inventory/introduction-to-software-inventory)」をご覧ください。  


### <a name="collect-hardware-inventory"></a>ハードウェア インベントリの収集

クライアントによるハードウェア インベントリ サイクルの実行をトリガーします。 詳しくは、「[ハードウェア インベントリの概要](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory)」をご覧ください。  


### <a name="evaluate-application-deployments"></a>アプリケーション展開の評価

クライアントによるアプリケーション展開評価サイクルの実行をトリガーします。 詳しくは、「[展開の再評価スケジュールを指定する](/sccm/core/clients/deploy/about-client-settings#schedule-re-evaluation-for-deployments)」をご覧ください。  


### <a name="evaluate-software-update-deployments"></a>ソフトウェア更新プログラム展開の評価

クライアントによるソフトウェア更新プログラム展開の評価サイクルの実行をトリガーします。 詳しくは、「[ソフトウェア更新プログラムの概要](/sccm/sum/understand/software-updates-introduction)」をご覧ください。  


### <a name="switch-to-the-next-software-update-point"></a>次のソフトウェアの更新ポイントに切り替える

クライアントによる次の利用可能なソフトウェア更新ポイントへの切り替えをトリガーします。 詳しくは、「[ソフトウェアの更新ポイントの切り替え](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching)」をご覧ください。  


### <a name="evaluate-device-health-attestation"></a>デバイス正常性構成証明の評価

Windows 10 クライアントによる最新のデバイスの正常性状態の確認と送信をトリガーします。 詳細については、[正常性構成証明書](/sccm/core/servers/manage/health-attestation)に関するページを参照してください。  


### <a name="check-conditional-access-compliance"></a>条件付きアクセス コンプライアンスを確認する

クライアントによる条件付きアクセスへの準拠の確認をトリガーします。 詳しくは、[PC の O365 サービスへのアクセスの管理](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)に関するページをご覧ください。  


### <a name="wake-up"></a>ウェイク アップ

バージョン 1810 以降では、スリープ状態のデバイスのフルパワーの状態への切り替えをトリガーします。


### <a name="restart"></a>再起動

選択したデバイスの再起動をトリガーします。 



## <a name="endpoint-protection"></a>Endpoint Protection

次のアクションは、**[Endpoint Protection]** メニューの下にあります。 このメニューは、[ホーム] タブの [コレクション] グループのリボンにあります。1 つまたは複数のデバイスを選択すると、これらのアクションがリボンの **[選択したオブジェクト]** タブに表示されます。

詳細については、[Configuration Manager のエンドポイント保護](/sccm/protect/deploy-use/endpoint-protection)に関するページを参照してください。

#### <a name="permissions"></a>アクセス許可
このアクションには、**コレクション** オブジェクトに対する**セキュリティ ポリシーの実施**アクセス許可が必要です。 

次の組み込みロールには、既定でこのアクセス許可があります。
- 完全な権限を持つ管理者  
- Endpoint Protection マネージャー  
- オペレーション管理者  

Endpoint Protection アクションをトリガーする必要があるカスタム ロールには、このアクセス許可を追加してください。


### <a name="full-scan"></a>フル スキャン

Endpoint Protection または Windows Defender によるマルウェア対策の*フル* スキャンの実行をトリガーします。  


### <a name="quick-scan"></a>クイック スキャン

Endpoint Protection または Windows Defender によるマルウェア対策の*クイック* スキャンの実行をトリガーします。  


### <a name="download-definition"></a>定義のダウンロード

Endpoint Protection または Windows Defender による最新のマルウェア対策定義のダウンロードをトリガーします。  



## <a name="see-also"></a>関連項目

- [クライアントを管理する方法](/sccm/core/clients/manage/manage-clients)
- [コレクションを管理する方法](/sccm/core/clients/manage/collections/manage-collections)