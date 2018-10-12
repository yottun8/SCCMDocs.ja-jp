---
title: Log Analytics にデータを同期する
titleSuffix: Configuration Manager
description: Configuration Manager から Azure Log Analytics にデータを同期します。
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0fd4c36ed03f0e0b158fe637a045553dab31ade
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43995357"
---
#  <a name="sync-data-from-configuration-manager-to-azure-log-analytics"></a>Configuration Manager から Azure Log Analytics にデータを同期する

*適用対象: System Center Configuration Manager (Current Branch)*

<!--1258052--> **Azure サービス ウィザード**を使用して、Configuration Manager から Azure Log Analytics クラウド サービスへの接続を構成します。 この接続は、デバイス コレクションのデータを Log Analytics に同期します。 

> [!Note]  
> Configuration Manager では、このオプション機能は既定で無効です。 この機能は、使用する前に有効にする必要があります。 詳細については、「[更新プログラムのオプション機能の有効化](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」を参照してください。<!--505213-->  

> [!TIP]
> Configuration Manager 1802 以降、Log Analytics コネクタはプレリリース機能ではなくなりました。 詳細については、「[更新プログラムからのプレリリース機能の使用](/sccm/core/servers/manage/pre-release-features)」を参照してください。



## <a name="prerequisites-for-the-log-analytics-connector"></a>Log Analytics コネクタの前提条件

> [!Note]  
> この記事で "*Log Analytics コネクタ*" と呼んでいるものは、以前は "*OMS コネクタ*" という名前でした。 機能に違いはありません。 詳しくは、[Azure 管理の監視](https://docs.microsoft.com/azure/monitoring/#operations-management-suite)に関するページをご覧ください。  

- Configuration Manager で Log Analytics コネクタをインストールする前に、Configuration Manager にアクセス許可を付与する必要があります。 Log Analytics ワークスペースを含む Azure "*リソース グループ*" への "*共同作成者アクセス許可*" を付与します。 詳細については、「[Configuration Manager に Log Analytics へのアクセス許可を付与する](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics)」をご覧ください。  

- オンライン モードの[サービス接続ポイント](/sccm/core/servers/deploy/configure/about-the-service-connection-point)をホストするコンピューターに Log Analytics コネクタをインストールします。  

- サービス接続ポイントに、コネクタと共に Log Analytics 用の Microsoft Monitoring Agent をインストールします。 同じ Log Analytics ワークスペースを使用するようにこのエージェントとコネクタを構成します。 このエージェントをインストールする方法について詳しくは、「[エージェントのダウンロードとインストール](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent)」をご覧ください。  

- コネクタとエージェントをインストールしたら、Configuration Manager データを使用するように Log Analytics を構成します。 詳細については、[Configuration Manager のコレクションのインポート](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections)に関する記事をご覧ください。  



## <a name="configure-the-connection-to-log-analytics"></a>Log Analytics への接続を構成する

**Azure サービス ウィザード**を使用して、Configuration Manager から Azure Log Analytics クラウド サービスへの接続を構成します。 このプロセスについて詳しくは、「[Azure サービスの構成](https://docs.microsoft.com/sccm/core/servers/deploy/configure/azure-services-wizard)」をご覧ください。 ウィザードで **OMS コネクタ**用のオプションを選択します。 

> [!Note]  
> この記事で "*Log Analytics コネクタ*" と呼んでいるものは、以前は "*OMS コネクタ*" という名前でした。 機能に違いはありません。 詳しくは、[Azure 管理の監視](https://docs.microsoft.com/azure/monitoring/#operations-management-suite)に関するページをご覧ください。  

その他の手順をすべて正常に完了すると、Web アプリのインポート後に **[接続の構成]** 画面上の情報が自動的に表示されます。 接続設定の情報は、**[Azure サブスクリプション]**、**[Azure リソース グループ]**、および **[Operations Management Suite ワークスペース]** に表示されます。

ウィザードは、入力した情報を使用して、Log Analytics サービスに接続します。 クラウド サービスと同期するデバイス コレクションを選択し、**[追加]** をクリックします。


## <a name="verify-the-connector-properties"></a>コネクタのプロパティを確認する

Configuration Manager を Log Analytics にリンクした後、接続のプロパティを確認してコレクションを追加または削除します。 

1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[Cloud Services]** を展開して **[Azure サービス]** ノードを選択します。  

2. Log Analytics の接続を選択します。 リボンで、**[プロパティ]** を選択します。  

[プロパティ] ページには、次の 2 つのタブがあります。  

#### <a name="azure-active-directory"></a>Azure Active Directory
このタブには、次の属性が表示されます。 
- **テナント**  
- **クライアント ID**  
- **クライアントのシークレット キーの有効期限**  

クライアントのシークレット キーがいつ期限切れになるのかも確認します。

#### <a name="connection-properties"></a>接続のプロパティ
このタブには、次の属性が表示されます。 
- **Azure サブスクリプション**  
- **Azure リソース グループ**  
- **Log Analytics ワークスペース**  

ここでは **[デバイス コレクション]** の一覧も表示されます。 **[追加]** と **[削除]** ボタンを使用して同期するコレクションを変更します。
