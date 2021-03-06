---
title: 更新のリセット ツール
titleSuffix: Configuration Manager
description: System Center Configuration Manager のコンソール内の更新のリセット ツールを使用します。
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de5c98e45c6f5d6dca1569de812825cce80d6f70
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417344"
---
# <a name="update-reset-tool"></a>更新のリセット ツール

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*  


バージョン 1706 以降、Configuration Manager のプライマリ サイトと中央管理サイトには、Configuration Manager 更新のリセット ツール **CMUpdateReset.exe** が含まれています。 このツールを使用して、コンソール内の更新プログラムのダウンロードやレプリケートに問題がある場合に、問題を修正します。 このツールはサイト サーバーの ***\cd.latest\SMSSETUP\TOOLS*** フォルダーにあります。

このツールは、サポートされている Current Branch のすべてのバージョンで使用できます。

このツールは、[コンソール内の更新プログラム](/sccm/core/servers/manage/install-in-console-updates)がまだインストールされておらず、失敗状態のときに使用することができます。 失敗状態とは、更新プログラムのダウンロードが進行中だが、スタックしているか、極端に長い時間がかかっていることを示します。 長時間とは、同様のサイズの更新プログラム パッケージの過去の予想よりも長い時間と見なされます。 また、更新プログラムの子プライマリ サイトへのレプリケートの失敗を意味している場合もあります。  

ツールを実行する際には、指定した更新プログラムに対して実行します。 既定では、このツールで正常にインストールまたはダウンロードされた更新プログラムが削除されることはありません。  

### <a name="prerequisites"></a>[前提条件]
ツールの実行に使用するアカウントには、次のアクセス許可が必要です。
-   中央管理サイトと階層の各プライマリ サイトのサイト データベースへの**読み取り**と**書き込み**アクセス許可。 これらのアクセス許可を設定するため、各サイトの Configuration Manager データベースで、ユーザー アカウントを **db_datawriter** および **db_datareader** の[固定データベース ロール](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles)のメンバーとして追加できます。 このツールは、セカンダリ サイトとは対話しません。
-   階層の最上位サイトの**ローカル管理者**。
-   サービス接続ポイントをホストするコンピューターの**ローカル管理者**。

リセットする更新プログラム パッケージの GUID が必要になります。 GUID の取得には、次の手順を実行します。
  1.   コンソールで、**[管理]** > **[更新とサービス]** の順に進みます。
  2.   表示ウィンドウでいずれかの列の見出し (**[状態]** など) を右クリックして、**[パッケージ GUID]** を選択し、その列を表示に追加します。
  3.   列に、更新プログラム パッケージの GUID が表示されます。

> [!TIP]  
> GUID をコピーするには、リセットする更新プログラム パッケージの行を選択し、CTRL + C キーを使用してその行をコピーします。 コピーした選択をテキスト エディターに貼り付けると、ツールを実行する際に、GUID のみをコピーしてコマンド ライン パラメーターとして使用できます。

### <a name="run-the-tool"></a>ツールを実行します。    
このツールは、階層の最上位サイトで実行する必要があります。

ツールを実行するときは、コマンドライン パラメーターを使用して、次を指定します。
  -   階層の最上位層サイトにある SQL Server。
  -   最上位層サイトにあるサイト データベース名。
  -   リセットする更新プログラム パッケージの GUID。

ツールは、更新プログラムの状態に基づいてアクセスする必要がある追加のサーバーを識別します。   

更新プログラム パッケージが*ダウンロード後*の状態にある場合、ツールはパッケージをクリーンアップしません。 オプションとして、強制削除パラメーター (このトピックで後述するコマンド ライン パラメーターを参照) を使用して、正常にダウンロードされた更新プログラムを強制的に削除できます。

ツールの実行後:
-   パッケージが削除された場合、最上位層サイトの SMS_Executive サービスを再起動します。 次に、再度パッケージをダウンロードするために更新プログラムを確認します。
-   パッケージが削除されていない場合は、何もする必要はありません。 更新プログラムが再初期化され、レプリケーションまたはインストールが再開されます。

**コマンドライン パラメーター:**  


|                        パラメーター                         |                                                       説明                                                        |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;最上位層サイトの SQL Server の FQDN>** | *必須* <br> 階層の最上位層サイトのサイト データベースをホストする SQL Server の FQDN を指定します。 |
|                **-D &lt;データベース名>**                 |                          *必須* <br> 最上位層サイトにあるデータベースの名前を指定します。                          |
|                 **-P &lt;パッケージ GUID>**                 |                        *必須* <br> リセットする更新プログラム パッケージの GUID を指定します。                        |
|           **-I &lt;SQL Server インスタンス名>**           |                    *省略可能* <br> サイト データベースをホストする SQL Server のインスタンスを識別します。                     |
|                       **-FDELETE**                       |                       *省略可能* <br> 正常にダウンロードした更新プログラム パッケージを強制的に削除します。                        |

 **例:**  
 一般的なシナリオで、ダウンロードに関する問題のある更新プログラムをリセットするとします。 SQL Server の FQDN が *server1.fabrikam.com* で、サイト データベースが *CM_XYZ*、パッケージ GUID が *61F16B3C-F1F6-4F9F-8647-2A524B0C802C* の場合、  次を実行します。***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 より極端なシナリオで、問題のある更新プログラム パッケージの削除を強制するとします。 SQL Server の FQDN が *server1.fabrikam.com* で、サイト データベースが *CM_XYZ*、パッケージ GUID が *61F16B3C-F1F6-4F9F-8647-2A524B0C802C* の場合、  次を実行します。***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***
