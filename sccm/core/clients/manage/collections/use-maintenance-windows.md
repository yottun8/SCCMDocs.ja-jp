---
title: メンテナンス期間を使用する
titleSuffix: Configuration Manager
description: コレクションおよびメンテナンス ウィンドウを使用して、System Center Configuration Manager でクライアントを効果的に管理します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8e81c1b5f5898c00d004cbf903bee2eff41fdd4e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421112"
---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>System Center Configuration Manager でメンテナンス期間を使用する方法

*適用対象:System Center Configuration Manager (Current Branch)*

メンテナンス期間を使用すると、デバイス コレクションに対して Configuration Manager の各種の操作を実行できる期間を定義できます。 メンテナンス期間を使用して、クライアントの構成に対する変更が、生産性に影響しない時間帯に行われるようにします。 Configuration Manager バージョン 1806 以降では、ユーザーは **[ソフトウェア センター]** の **[インストールの状態]** タブから次のメンテナンス期間を確認できます。 <!--1358131-->

 次の操作では、メンテナンス期間がサポートされています。  

- ソフトウェアの展開  

- ソフトウェア更新プログラムの展開  

- コンプライアンス設定の展開と評価  

- オペレーティング システムの展開  

- タスク シーケンスの展開  

  メンテナンス期間の開始日、開始時刻、終了時刻、および繰り返しパターンを構成します。 期間の最長時間は、24 時間未満にする必要があります。 既定では、展開によって実行されるコンピューターの再起動はメンテナンス期間以外では許可されませんが、既定の設定をオーバーライドできます。 メンテナンス期間は展開プログラムの実行時間のみに影響を与えます。ダウンロードしてローカルで実行するように構成されたアプリケーションは、メンテナンス期間以外でもコンテンツをダウンロードできます。  

  クライアント コンピューターが、メンテナンス期間が構成されているデバイス コレクションのメンバーである場合は、許容最長実行時間がそのメンテナンス期間に構成されている期間を超えない場合にのみ、展開プログラムが実行されます。 プログラムの実行が失敗すると、アラートが生成され、次のスケジュールされたメンテナンス期間に利用可能な時間があれば、その展開が再実行されます。  

## <a name="using-multiple-maintenance-windows"></a>複数のメンテナンス期間の使用  
 クライアント コンピューターが、メンテナンス期間が構成されている複数のデバイス コレクションのメンバーである場合は、次の規則が適用されます。  

- メンテナンス期間が重なっていない場合は、2 つの独立したメンテナンス期間として扱われます。  

- メンテナンス期間が重なっている場合は、両方のメンテナンス期間が対象とする期間をすべて含む単一のメンテナンス期間として扱われます。 たとえば、2 つのメンテナンス期間があり、それぞれ期間が 1 時間でそのうち 30 分が重なっている場合、メンテナンス期間の実際の期間は 90 分になります。  

  アプリケーションのインストールをソフトウェア センターから開始すると、メンテナンス期間に関係なく、アプリケーションは直ちにインストールされます。  

  目的が **[必須]** であるアプリケーション展開が、ソフトウェア センターのユーザーによって構成された勤務時間外にインストールの期限に達した場合、アプリケーションはインストールされます。 

### <a name="how-to-configure-maintenance-windows"></a>メンテナンス期間を構成する方法  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]**>  **[デバイス コレクション]** の順に選択します。  

3.  **[デバイス コレクション]** の一覧で、コレクションを選択します。 **[すべてのシステム]** コレクションにメンテナンス期間を作成することはできません。  

4.  **[ホーム]** タブの **[プロパティ]** グループで、**[プロパティ]** を選択します。  

5.  **[&lt;コレクション名\> のプロパティ]** ダイアログ ボックスの **[メンテナンス期間]** タブで、**[新規]** アイコンをクリックします。  

6.  **[&lt;新しい\>スケジュール]** ダイアログ ボックスに入力します。  

7.  **[このスケジュールの適用対象]** ドロップダウン リストから選択します。  

8.  **[OK]** を選択し、**[&lt;コレクション名\>のプロパティ]** ダイアログ ボックスを閉じます。  
