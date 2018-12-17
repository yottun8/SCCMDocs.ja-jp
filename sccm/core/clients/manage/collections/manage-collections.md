---
title: コレクションを管理する
titleSuffix: Configuration Manager
description: Configuration Manager で一般的なコレクション管理タスクを実行します。
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03b34c09a5fef63316bb1d9d1a94dbbfc3ccf69f
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456262"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Configuration Manager でコレクションを管理する方法

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager でコレクションの管理タスクを行う際は、この記事の概要情報を参考にしてください。  

> [!NOTE]  
>  Configuration Manager コレクションを作成する方法については、「[コレクションを作成する方法](/sccm/core/clients/manage/collections/create-collections)」をご覧ください。  



## <a name="bkmk_device"></a> デバイス コレクションを管理する方法  

 **[資産とコンプライアンス]** ワークスペースで **[デバイス コレクション]** を選択し、管理するコレクションと管理タスクを選択します。  


#### <a name="show-members"></a>メンバーの表示
 **[デバイス]** ノードの一時ノードで選択されたコレクションのメンバーであるすべてのリソースを表示します。


#### <a name="add-selected-items"></a>選択された項目の追加
 次のオプションを使用できます。 

 - **[選択した項目を既存のデバイス コレクションに追加する]**: **[コレクションの選択]** ダイアログ ボックスを開きます。 選択したコレクションのメンバーを追加するコレクションを選択します。 **[コレクションを含める]** のメンバーシップ規則を使用すると、選択されたコレクションは、このコレクションに含められます。  

 - **[選択した項目を新しいデバイス コレクションに追加する]**: 新しいコレクションを作成できる**デバイス コレクションの作成ウィザード**を開きます。 **[コレクションを含める]** のメンバーシップ規則を使用すると、選択されたコレクションは、このコレクションに含められます。  


 詳しくは、「[コレクションを作成する方法](/sccm/core/clients/manage/collections/create-collections)」をご覧ください。


#### <a name="install-client"></a>クライアントのインストール
 **クライアントのインストール ウィザード**を開きます。 このウィザードでは、クライアント プッシュのインストールを使用して、選択したコレクションのすべてのコンピューターに Configuration Manager クライアントがインストールされます。 詳しくは、「[クライアント プッシュ インストール](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush)」をご覧ください。


#### <a name="run-script"></a>スクリプトを実行する
 **スクリプトの実行**ウィザードを開き、コレクション内のすべてのクライアントで PowerShell スクリプトを実行します。 詳しくは、「[PowerShell スクリプトの作成と実行](/sccm/apps/deploy-use/create-deploy-scripts)」をご覧ください。


#### <a name="manage-affinity-requests"></a>アフィニティ要求の管理
 **[ユーザーとデバイスのアフィニティ要求の管理]** ダイアログ ボックスを開きます。 保留中の要求を承認または拒否して、選択したコレクションのデバイスに対するユーザーとデバイスのアフィニティを確立します。 詳しくは、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)」をご覧ください。


#### <a name="clear-required-pxe-deployments"></a>必須の PXE 展開の消去
 選択されたコレクションのすべてのメンバーから必要な PXE ブート展開を消去します。 詳細については、「[PXE を使用したネットワーク経由での Windows の展開](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network)」を参照してください。


#### <a name="update-membership"></a>メンバーシップの更新
 選択されたコレクションのメンバーシップを評価します。 多くのメンバーからなるコレクションでは、更新の完了には時間がかかることがあります。 更新が完了したら、**[リフレッシュ]** アクションを使用して、新しいコレクションのメンバーで画面を更新します。


#### <a name="add-resources"></a>リソースの追加
 **[コレクションへのリソースの追加]** ダイアログ ボックスを開きます。 選択したコレクションに追加する新しいリソースを検索します。 更新中は選択されたコレクションで砂時計のアイコンが表示されます。


#### <a name="client-notification"></a>クライアント通知
 詳細については、[クライアント通知](/sccm/core/clients/manage/client-notification)に関するページをご覧ください。


#### <a name="endpoint-protection"></a>Endpoint Protection
 詳細については、[クライアント通知](/sccm/core/clients/manage/client-notification)に関するページをご覧ください。


#### <a name="export"></a>エクスポート
 このコレクションを管理オブジェクト フォーマット (MOF) ファイルにエクスポートできる**コレクションのエクスポート** ウィザードを開きます。 このファイルを別の Configuration Manager サイトでアーカイブまたはインポートできます。 コレクションをエクスポートするとき、参照されているコレクションはエクスポートされません。 参照されているコレクションは、**[含む]** 規則または **[除外する]** 規則を使用することによって、選択したコレクションで参照されています。


#### <a name="copy"></a>コピー
 選択したコレクションのコピーを作成します。 新しいコレクションは選択したコレクションを限定コレクションとして使用します。


#### <a name="refresh"></a>最新の情報に更新
 ビューに表示されている情報を更新します。


#### <a name="delete"></a>削除
 選択したコレクションを削除します。 コレクションのすべてのリソースをサイト データベースから削除することもできます。 

 Configuration Manager に構築されたコレクションは削除することができません。 組み込みコレクションの一覧については、「[コレクションの概要](/sccm/core/clients/manage/collections/introduction-to-collections#built-in-collections)」をご覧ください。


#### <a name="simulate-deployment"></a>展開のシミュレート
 **アプリケーション展開のシミュレーション ウィザード**を開きます。 このウィザードでは、アプリケーションをインストールしたりアンインストールしたりせずにアプリケーションの結果をテストできます。 詳しくは、「[アプリケーションの展開をシミュレーションする方法](/sccm/apps/deploy-use/simulate-application-deployments)」をご覧ください。


#### <a name="deploy"></a>[展開]
 次のオプションを表示します。  

 - **[アプリケーション]**: **ソフトウェアの展開ウィザード**を開きます。 選択したコレクションに対するアプリケーションの展開を選択して構成します。 詳しくは、「[アプリケーションを展開する方法](/sccm/apps/deploy-use/deploy-applications)」をご覧ください。  

 - **[プログラム]**: **ソフトウェアの展開ウィザード**を開きます。 選択したコレクションに対するパッケージとプログラムの展開を選択して構成します。 詳細については「[Packages and programs](/sccm/apps/deploy-use/packages-and-programs)」(パッケージとプログラム) を参照してください。  

 - **[構成基準]**: **[構成基準の展開]** ダイアログ ボックスを開きます。 選択したコレクションに対する 1 つ以上の構成基準の展開を構成します。 詳細については、[構成基準を展開する方法](/sccm/compliance/deploy-use/deploy-configuration-baselines)に関するページを参照してください。  

 - **[タスク シーケンス]**: **ソフトウェアの展開ウィザード**を開きます。 選択したコレクションに対するタスク シーケンスの展開を選択して構成します。 詳細については、「[タスクを自動化するためのタスク シーケンスの管理](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)」をご覧ください。  

 - **[ソフトウェア更新プログラム]**: **ソフトウェアの更新の展開ウィザード**を開きます。 選択したコレクション内のリソースへのソフトウェア更新プログラムの展開を構成します。 詳しくは、「[ソフトウェア更新プログラムの管理](/sccm/sum/understand/software-updates-introduction)」をご覧ください。  


#### <a name="clear-server-group-deployment-locks"></a>サーバー グループ展開のロックを解除
 コレクションに対するすべてのサーバー グループ展開のロックを手動で解放します。 詳しくは、「[サーバー グループの提供](/sccm/sum/deploy-use/service-a-server-group)」をご覧ください。


#### <a name="move"></a>移動
 選択したコレクションを **[デバイス コレクション]** ノードの別のフォルダーに移動します。 


#### <a name="properties"></a>プロパティ
 詳しくは、「[コレクションのプロパティ](#BKMK_CollProp)」をご覧ください。  



## <a name="bkmk_user"></a> ユーザー コレクションを管理する方法  

 **[資産とコンプライアンス]** ワークスペースで **[ユーザー コレクション]** を選択し、管理するコレクションと管理タスクを選択します。  

 > [!Note]  
 > ユーザー コレクションでは次のアクションを使用できますが、動作はデバイス コレクションと同じです。 それ以外では、アクションはユーザー コレクションとその中のユーザーに適用されます。 詳しくは、「[デバイス コレクションを管理する方法](#bkmk_device)」の対応するアクションをご覧ください。  

 - **メンバーの表示**  
 - **選択された項目の追加**  
     - **選択した項目を既存のユーザー コレクションに追加する**  
     - **選択した項目を新しいユーザー コレクションに追加する**  
 - **アフィニティ要求の管理**  
 - **メンバーシップの更新**  
 - **リソースの追加**  
 - **エクスポート**  
 - **コピー**  
 - **更新**  
 - **削除**  
 - **展開のシミュレート**  
 - **展開**  
     - **アプリケーション**。  
     - **プログラム**  
     - **構成基準**   
 - **移動**  
 - **プロパティ**



##  <a name="BKMK_CollProp"></a> コレクションのプロパティ  

 コレクションの **[プロパティ]** ダイアログ ボックスを開くと、次のオプションを表示し構成することができます。  

#### <a name="general"></a>全般
 コレクション名や限定コレクションを含め選択されたコレクションに関する概要を表示し構成します。

#### <a name="membership-rules"></a>メンバーシップの規則
 このコレクションのメンバーシップを定義するメンバーシップ規則を構成します。 詳しくは、「[コレクションを作成する方法](/sccm/core/clients/manage/collections/create-collections)」をご覧ください。  

#### <a name="power-management"></a>電源管理
 選択したコレクションのコンピューターに割り当てられた電源管理の計画を構成します。 詳細については、「[電源管理の概要](/sccm/core/clients/manage/power/introduction-to-power-management)」を参照してください。  

#### <a name="deployments"></a>展開
 選択したコレクションのメンバーに展開したソフトウェアが表示されます。  

#### <a name="maintenance-windows"></a>メンテナンス期間
 選択されたコレクションのメンバーに適用されたメンテナンス期間を表示し構成します。 詳細については、「[メンテナンス期間を使用する方法](/sccm/core/clients/manage/collections/use-maintenance-windows)」を参照してください。

#### <a name="collection-variables"></a>コレクション変数
 コレクションに適用され、タスク シーケンスで使用することができる変数を構成します。 詳しくは、「[How to set task sequence variables](/sccm/osd/understand/using-task-sequence-variables#bkmk_set)」(タスク シーケンス変数の設定方法) をご覧ください。  

#### <a name="distribution-point-groups"></a>配布ポイント グループ
 1 つ以上の配布ポイント グループを選択されたコレクションのメンバーに関連付けます。 詳細については、「[コンテンツ管理インフラストラクチャの展開と管理](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)」をご覧ください。

#### <a name="security"></a>セキュリティ
 関連付けられた役割やセキュリティの範囲で選択されたコレクションへの権限を持つ管理者ユーザーを表示します。 詳細については、「[ロール ベース管理の基礎](/sccm/core/understand/fundamentals-of-role-based-administration)」を参照してください。  

#### <a name="alerts"></a>アラート 
 クライアント ステータスや Endpoint Protection に関するアラートが生成されるタイミングを構成します。 詳しくは、「[クライアント ステータスを構成する方法](/sccm/core/clients/deploy/configure-client-status)」および「[Endpoint Protection を監視する方法](/sccm/protect/deploy-use/monitor-endpoint-protection)」をご覧ください。  
