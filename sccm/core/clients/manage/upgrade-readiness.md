---
title: Upgrade Readiness
titleSuffix: Configuration Manager
description: Upgrade Readiness と Configuration Manager を統合して Windows 10 アップグレードの互換性データにアクセスし、アップグレードまたは修復対象のデバイスを指定します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/04/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 0ba5a484fe11185b46125de0d8764bce153f577d
ms.sourcegitcommit: a2ecd84d93f431ee77848134386fec14031aed6a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2019
ms.locfileid: "55230853"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>Upgrade Readiness と Configuration Manager の統合

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Upgrade Readiness は [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness) の一部です。 これを使用すると、Windows 10 にアップグレードするため、環境内のデバイスの対応性を評価および分析することができます。 Upgrade Readiness と Configuration Manager を統合することで、Configuration Manager コンソールでクライアントのアップグレードの互換性データにアクセスできます。 次にこのデータを使用してコレクションを作成し、アップグレードまたは修復対象のデバイスを指定します。



## <a name="configure-clients"></a>クライアントを構成する

Upgrade Readiness は Windows Analytics のデータに依存しています。 Upgrade Readiness が十分なデータを受信するためには、次の前提条件を構成する必要があります。

- "*商用 ID キー*" を使用してすべてのクライアントを構成する  

- Windows Analytics で少なくとも基本レベルのデータを報告できるように Windows 10 クライアントを構成する  

- Windows 7 または 8.1 を稼働しているクライアントの場合:  

    - 「[Get started with Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs)」 (Upgrade Readiness の概要) の説明に従って更新プログラムをインストールする  

    - Windows Analytics クライアント設定を有効にする  

Configuration Manager クライアント設定を使用してこれらの設定を構成します。 詳細については、「[Windows Analytics の使用](/sccm/core/clients/manage/monitor-windows-analytics)」をご覧ください。

> [!NOTE]  
> ほとんどの環境では、前提条件となる適切な更新プログラムを展開し、クライアント設定を構成すれば十分です。 Upgrade Readiness が環境内のデバイスからデータを受信しない問題が発生する場合、一部の問題は [Upgrade Readiness 展開スクリプト](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script)を使用して対処できる場合があります。 



## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Configuration Manager と Upgrade Readiness の接続

[Azure サービス ウィザード](/sccm/core/servers/deploy/configure/azure-services-wizard)を使用して、Configuration Manager で使用する Azure サービスを構成するプロセスを簡略化します。 Configuration Manager と Upgrade Readiness を接続するには、[Azure portal](https://portal.azure.com) で *[Web アプリ/API]* タイプの Azure Active Directory (Azure AD) アプリ登録を作成します。 アプリ登録の作成方法について詳しくは、「[Azure Active Directory テナントにアプリケーションを登録する](/azure/active-directory/active-directory-app-registration)」をご覧ください。 

Azure portal で、新しく登録した Web アプリに次のアクセス許可を付与します。
- Log Analytics ワークスペースと Upgrade Readiness データを含むリソース グループに対して、"*閲覧者*" アクセス許可
- Upgrade Readiness データをホストしている Log Analytics ワークスペースに対して、"*共同作成者*" アクセス許可

Azure サービス ウィザードは、このアプリ登録を使用して、Configuration Manager が Azure AD と安全に通信し、インフラストラクチャを Upgrade Readiness データに接続できるようにします。

> [!IMPORTANT]  
> Azure AD ユーザー ID ではなく、アプリ自体にアクセス許可を付与します。 Configuration Manager インフラストラクチャの代わりにデータにアクセスするのは、登録済みアプリです。 アクセス許可を与えるには、アクセス許可を割り当てるときに **[ユーザーの追加]** ブレードでアプリ登録名を検索します。 
> 
> このプロセスは、Log Analytics へのアクセス許可を Configuration Manager に提供する場合と同じです。 これらの手順は、*Azure サービス ウィザード*を使用してアプリ登録が Configuration Manager にインポートされる前に完了する必要があります。
> 
> 詳細については、「[Configuration Manager を Log Analytics に接続する](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm)」をご覧ください。


### <a name="use-the-azure-wizard-to-create-the-connection"></a>Azure ウィザードを使用して、接続を作成する

「[Azure サービスの構成](/sccm/core/servers/deploy/configure/azure-services-wizard)」の指示に従い、上記で作成した Web アプリ登録をインポートすることで、Upgrade Readiness への接続を作成します。 

Web アプリが正常にインポートされ、Azure portal で適切なアクセス許可が割り当てられると、*[構成]* ページに次の値があらかじめ設定されます。   
-  Azure サブスクリプション  
-  Azure リソース グループ  
-  Windows Analytics ワークスペース  

次の状況では、複数のリソース グループまたはワークスペースを使用できます。 
- 登録された Azure AD Web アプリが複数のリソース グループに対して "*共同作成者*" アクセス許可を持っている場合   
- 選択したリソース グループに複数の Log Analytics ワークスペースが含まれる場合  



## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Configuration Manager で Upgrade Readiness の情報を表示および使用する

Upgrade Readiness と Configuration Manager を統合したら、クライアントでのアップグレード準備の分析を表示できます。

1. Configuration Manager コンソールで **[監視]** ワークスペースに移動し、**[アップグレードの準備]** ノードを選択します。  

2. データを確認します。 次に例を示します。  
    - アップグレードの準備状態  
    - データを報告している Windows デバイスの割合  

3. 特定のコレクションでデバイス用のデータを表示するためにダッシュボードをフィルター処理します。  

4. 特定の準備状態のデバイスを表示し、それらのデバイス用に動的コレクションを作成します。 次にそのコレクションを使用して、各デバイスをアップグレードするか、ブロックされた状態のデバイスを修復するためのアクションを実行します。  

> [!Note]  
> サイトは、週に 1 回 Upgrade Readiness とデータを同期します。<!--SCCMDocs issue 732--> 同期を手動でトリガーする場合:
> 1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[Cloud Services]** を展開して **[Azure サービス]** ノードを選択します。  
> 2. 一覧から Upgrade Readiness の接続を選択します。  
> 3. リボンで、同期するオプションを選択します。  



## <a name="next-steps"></a>次のステップ

- [Windows を最新バージョンにアップグレードする](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)  
- [OS をアップグレードするタスク シーケンスの作成](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)  
- [段階的展開を作成する](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  
