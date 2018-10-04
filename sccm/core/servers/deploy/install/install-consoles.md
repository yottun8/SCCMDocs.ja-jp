---
title: コンソールをインストールする
titleSuffix: Configuration Manager
description: Configuration Manager コンソールをインストールし、中央管理サイトまたはプライマリ サイトに接続します。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a8d1d0a727f0a4ad4a2bfc25141f7e2982494080
ms.sourcegitcommit: b596d944e49f3c4912c6ca91915ed1418c17a1a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "42584403"
---
# <a name="install-the-system-center-configuration-manager-console"></a>System Center Configuration Manager コンソールをインストールする

*適用対象: System Center Configuration Manager (Current Branch)*

管理者は Configuration Manager コンソールを利用し、Configuration Manager 環境を管理します。 各 Configuration Manager コンソールで中央管理サイトまたはプライマリ サイトに接続できます。 Configuration Manager コンソールをセカンダリ サイトに接続することはできません。

> [!NOTE]  
>  管理者は、そのユーザー アカウントに割り当てられたアクセス許可に基づいて、コンソール内のオブジェクトを表示できます。 ロールベース管理の詳細については、「[ロール ベース管理の基礎](../../../../core/understand/fundamentals-of-role-based-administration.md)」を参照してください。  

 サイト サーバーをインストールするときに、同時に、Configuration Manager コンソールをインストールできます。 サイト サーバーのインストールとは別にコンソールをインストールするには、スタンドアロンのインストーラーを実行します。  

 スタンドアロンのインストーラーを使用して Configuration Manager コンソールをインストールするには、次の手順に従います。  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>セットアップ ウィザードを使用して Configuration Manager コンソールをインストールするには  

1.  次の要件を満たすことを確認してください。  

    -  コンソールのインストール先のコンピューターの**ローカル管理者**権限が与えられていること。  

    -   コンソールのインストール ファイルのある場所の **読み取り** 権限が与えられていること。  

2.  次のいずれかの場所に移動します。  

    -   サイト サーバー上で次の場所に移動します: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   Configuration Manager ソース メディアで次の場所に移動します: `<Configuration Manager source files>\Smssetup\Bin\I386`  

    > [!TIP]  
    >  ベスト プラクティスとして、Configuration Manager コンソールのインストーラーは、System Center Configuration Manager のインストール メディアではなく、サイト サーバーから開始することをお勧めします。 サイト サーバーをインストールするときには、Configuration Manager コンソールのインストール ファイル、およびサイト用にサポートされている言語パックが **Tools\ConsoleSetup** サブフォルダーにコピーされます。 インストール メディアから Configuration Manager コンソールをインストールすると、常に英語バージョンがインストールされます。 この動作は、サイト サーバーがさまざまな言語をサポートしているか、ターゲット コンピューターの OS が別の言語に設定されている場合でも発生します。 **ConsoleSetup** フォルダーを別の場所にコピーして、その場所からインストールを開始することもできます。

3.  Configuration Manager コンソールのセットアップ ウィザードを開くには、**consolesetup.exe** をダブルクリックします。  

    > [!IMPORTANT]  
    >  Configuration Manager コンソールのインストールには、常に、**consolesetup.exe** を使用します。 Adminconsole.msi を実行して、Configuration Manager コンソールをインストールできますが、このメソッドは前提条件や依存関係のチェックを実行しません。 インストールが正しくインストールされない可能性があります。  

4.  ウィザードで、**[次へ]** を選択します。  

5.  **[サイト サーバー]** ページで、Configuration Manager コンソールが接続するサイト サーバーの完全修飾ドメイン名 (FQDN) を入力します。  

6.  **[インストール先フォルダー]** ページで、Configuration Manager コンソールのインストール先フォルダーを入力します。 フォルダーのパスに Unicode 文字を含めたり、末尾にスペースを付けたりすることはできません。  

7.  **[カスタマー エクスペリエンス向上プログラム]** ページで、カスタマー エクスペリエンス向上プログラム (CEIP) に参加するかどうかを選択します。  
    > [!Note]  
    > Configuration Manager バージョン 1802 以降では、CEIP 機能が製品から削除されます。

8.  **[インストールの準備完了]** ページで、**[インストール]** を選択して Configuration Manager コンソールをインストールします。  



## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>コマンド プロンプトから Configuration Manager コンソールをインストールするには  

1.  Configuration Manager コンソールのインストールを開始するサーバーでコマンド プロンプト ウィンドウを開き、次のいずれかの場所に移動します。  

    -   `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    > [!TIP]  
    >  コマンド プロンプトから Configuration Manager コンソールをインストールすると、常に英語バージョンがインストールされます。 この動作は、ターゲット コンピューターの OS が別の言語に設定されている場合でも発生します。 英語以外の言語で Configuration Manager コンソールをインストールするには、[セットアップ ウィザードを利用して Configuration Manager コンソールをインストールする](#to-install-the-configuration-manager-console-by-using-the-setup-wizard)必要があります。  

2.  コマンド プロンプトで「**consolesetup.exe**」と入力します。 次のコマンド ライン オプションから選択します。  

|  コマンド ライン オプションを使用します     | 説明     |
  |-------------|-------------|
  |/q|Configuration Manager コンソールを無人インストールします。 **EnableSQM**、 **TargetDir**、 **DefaultSiteServerName** の各オプションは、このオプションを使用する場合に指定する必要があります。|  
  |/uninstall|Configuration Manager コンソールをアンインストールします。 **/q** オプションと共に使用する場合は、このオプションを先に指定します。|  
  |LangPackDir|言語ファイルが含まれているフォルダーのパスを指定します。 **セットアップ ダウンローダー** を使用して言語ファイルをダウンロードできます。 このオプションを指定しないと、現在のフォルダー内で言語フォルダーが検索されます。 言語フォルダーが見つからなかった場合は、英語版だけがインストールされます。 詳細については、「[セットアップ ダウンローダー](setup-downloader.md)」を参照してください。|  
  |TargetDir|Configuration Manager コンソールをインストールするインストール先フォルダーを指定します。 このオプションは、 **/q** オプションを使用する場合に指定する必要があります。|  
  |EnableSQM|カスタマー エクスペリエンス向上プログラム (CEIP) に参加するかどうかを指定します。 値として **1** を指定すると、CEIP に参加します。**0** を指定すると、参加しません。 このオプションは、 **/q** オプションを使用する場合に指定する必要があります。</br></br>注: Configuration Manager バージョン 1802 以降、CEIP 機能が製品から削除されます。  パラメーターを使用すると、インストールが失敗します。|  
  |DefaultSiteServerName|コンソールを開いたときに接続されるサイト サーバーの FQDN を指定します。 このオプションは、 **/q** オプションを使用する場合に指定する必要があります。|  


  ### <a name="examples"></a>例
  **バージョン 1802 以降の場合は、EnableSQM パラメーターを指定しないでください**
  -  `ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

  -  `ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com EnableSQM=1  LangPackDir=C:\Downloads\ConfigMgr`  

  -  `ConsoleSetup.exe /uninstall /q`  
