---
title: "コンソールのインストール | Microsoft Docs"
description: "Configuration Manager コンソールをインストールし、中央管理サイトまたはプライマリ サイトに接続する方法についてご確認ください。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e3bc8341b384be975098d1b9d7824ef117a47ccb

---
# <a name="install-system-center-configuration-manager-consoles"></a>System Center Configuration Manager コンソールをインストールする

*適用対象: System Center Configuration Manager (Current Branch)*


管理ユーザーは System Center Configuration Manager コンソールを利用し、Configuration Manager 環境を管理します。 各 Configuration Manager コンソールで中央管理サイトまたはプライマリ サイトに接続できます。 Configuration Manager をセカンダリ サイトに接続することはできません。


> [!NOTE]  
>  コンソールを実行している管理ユーザーに表示されるオブジェクトは、管理ユーザーに割り当てられた権限によって異なります。 ロール ベース管理について詳しくは、「[System Center Configuration Manager のロール ベース管理の基礎](../../../../core/understand/fundamentals-of-role-based-administration.md)」を参照してください。  

 Configuration Manager コンソールは、サイト サーバーのインストール時にセットアップ ウィザードでインストールすることも、スタンドアロンのアプリケーションを実行してインストールすることもできます。  

 スタンドアロンのアプリケーションを使用して Configuration Manager コンソールをインストールするには、次の手順に従います。  

## <a name="to-install-a-configuration-manager-console"></a>Configuration Manager コンソールをインストールするには  

1.  Configuration Manager コンソール アプリケーションを実行する管理ユーザーが、次のセキュリティ権限を持っていることを確認します。  

    -   コンソールを実行するコンピューターの**ローカル管理者** 権限  

    -   コンソールのインストール ファイルのある場所の **読み取り** 権限  

2.  次の場所のいずれかに移動します。  

    -   Configuration Manager のソース メディアから **&lt;ConfigMgrSourceFiles\>\Smssetup\Bin\I386** に移動します。  

    -   サイト サーバーで、**&lt;ConfigMgrSiteServerInstallationPath\>\Tools\ConsoleSetup** に移動します。  

    > [!TIP]  
    >  ベスト プラクティスとして、Configuration Manager コンソールのインストールは、System Center Configuration Manager のインストール メディアではなく、サイト サーバーから開始することをお勧めします。 サイト サーバーからインストールする方法では、Configuration Manager コンソールのインストール ファイル、およびサイト用にサポートされている言語パックが **Tools\ConsoleSetup** サブフォルダーにコピーされます。 一方、インストール メディアから Configuration Manager コンソールをインストールする場合は、サイト サーバーでサポートされている言語や、コンピューターのオペレーティング システムの言語設定には関係なく、常に英語版をインストールすることになります。 **ConsoleSetup** フォルダーを別の場所にコピーして、その場所からインストールを開始することもできます。  

3.  **consolesetup.exe**をダブルクリックします。 Configuration Manager コンソールのセットアップ ウィザードが開きます。  

    > [!IMPORTANT]  
    >  Configuration Manager コンソールのインストールには、常に、consolesetup.exe を使用します。 AdminConsole.msi を実行しても Configuration Manager コンソールをインストールできますが、前提条件や依存関係のチェックは行われず、正しくインストールされない可能性があります。  

4.  ウィザードの最初のページで [ **次へ**] をクリックします。  

5.  **[サイト サーバー]** ページで、Configuration Manager コンソールが接続するサイト サーバーの完全修飾ドメイン名 (FQDN) を指定します。  

6.  **[インストール先フォルダー]** ページで、Configuration Manager コンソールのインストール先フォルダーを指定します。 フォルダーのパスに Unicode 文字を含めたり、末尾にスペースを付けたりすることはできません。  

7.  **[カスタマー エクスペリエンス向上プログラム]** ページで、カスタマー エクスペリエンス向上プログラムに参加するかどうかを選びます。  

8.  **[インストールの準備完了]** ページで、**[インストール]** をクリックして Configuration Manager コンソールをインストールします。  

## <a name="to-install-a-configuration-manager-console-from-a-command-prompt"></a>コマンド プロンプトから Configuration Manager コンソールをインストールするには  

1.  Configuration Manager コンソールのインストールを開始するサーバーでコマンド プロンプト ウィンドウを開き、次のいずれかの場所に移動します。  

    -   **&lt;Configuration Manager サイト サーバーのインストール パス\>\Tools\ConsoleSetup**  

    -   **&lt;Configuration Manager のインストール メディア\>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  コマンド プロンプトから Configuration Manager コンソールをインストールすると、コンピューターのオペレーティング システムの言語設定に関係なく、常に英語版がインストールされます。 Configuration Manager コンソールを別の言語でインストールするには、前述の方法を使う必要があります。  

2.  「 **consolesetup.exe** 」と、必要に応じて、次のコマンド ライン オプションを入力します。  

|  コマンド ライン オプションを使用します     | [説明]     |
  | :------------- | :------------- |
  |/q|Configuration Manager コンソールを無人インストールします。 **EnableSQM**、 **TargetDir**、 **DefaultSiteServerName** の各オプションは、このオプションを使用する場合に指定する必要があります。|  
  |/uninstall|Configuration Manager コンソールをアンインストールします。 **/q** オプションと共に使用する場合は、このオプションを先に指定する必要があります。|  
  |LangPackDir|言語ファイルが含まれているフォルダーのパスを指定します。 **セットアップ ダウンローダー** を使用して言語ファイルをダウンロードできます。 このオプションを指定しないと、現在のフォルダー内で言語フォルダーが検索されます。 言語フォルダーが見つからなかった場合は、英語版だけがインストールされます。 詳細については、「[セットアップ ダウンローダー](/sccm/core/servers/deploy/install/setup-downloader)」を参照してください。|  
  |TargetDir|Configuration Manager コンソールをインストールするインストール先フォルダーを指定します。 このオプションは、 **/q** オプションを使用する場合に指定する必要があります。|  
  |EnableSQM|カスタマー エクスペリエンス向上プログラム (CEIP) に参加するかどうかを指定します。 参加する場合は 1 に、参加しない場合は 0 に設定します。 このオプションは、 **/q** オプションを使用する場合に指定する必要があります。|  
  |DefaultSiteServerName|コンソールを開いたときに接続されるサイト サーバーの FQDN を指定します。 このオプションは、 **/q** オプションを使用する場合に指定する必要があります。|  


  **使用例:**  
  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  



<!--HONumber=Dec16_HO3-->


