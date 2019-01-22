---
title: Windows クライアント コンピューターのリモート管理
titleSuffix: Configuration Manager
description: System Center Configuration Manager を使用してリモートの Windows クライアント コンピューターを管理します。
ms.date: 07/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ce6bf7c39e400a59188388ee162bc187b1683a7
ms.sourcegitcommit: 2687489aa409a050dcacd67f17b3dad3ab7f1804
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2019
ms.locfileid: "54316475"
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-system-center-configuration-manager"></a>System Center Configuration Manager を使用して Windows クライアント コンピューターをリモート管理する方法

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

リモート コントロールを開始する前に、次のトピックの情報を確認してください。  

-   [System Center Configuration Manager のリモート コントロールの前提条件](../../../../core/clients/manage/remote-control/prerequisites-for-remote-control.md)  

-   [System Center Configuration Manager でのリモート コントロールの構成](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

リモート コントロール ビューアーを起動するには、次の 3 つの方法があります。  

-   Configuration Manager コンソールを使用する。  

-   Windows のコマンド プロンプトを使用する。  

-   **Microsoft System Center** プログラム グループから、Configuration Manager コンソールを実行するコンピューターの Windows **スタート** メニューを使用する。  

### <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Configuration Manager コンソールからクライアント コンピューターをリモート管理するには  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[デバイス]** または **[ユーザー コレクション]** の順に選択します。  

3.  リモートで管理するコンピューターを選択し、**[ホーム]** タブの **[デバイス]** グループで、**[開始]** > **[リモート コントロール]** を選択します。  

    > [!IMPORTANT]  
    >  場合、クライアント設定 **リモート制御のプロンプトのユーザー** にアクセス許可が設定されている **True**, 、接続では、リモート コンピューターのユーザーがリモート コントロール プロンプトに同意するまでは開始されません。 詳しくは、「[System Center Configuration Manager でのリモート コントロールの構成](../../../../core/clients/manage/remote-control/configuring-remote-control.md)」を参照してください。  

4.  **[Configuration Manager リモート コントロール]** ウィンドウが開いたら、クライアント コンピューターをリモート管理できます。 接続を構成するには、次のオプションを使用します。  

    > [!NOTE]  
    >  接続するコンピューターに複数のモニターがある場合は、すべてのモニターの表示画面がリモート コントロール ウィンドウに表示されます。  

    -   **ファイル - 接続** – ほかのコンピューターに接続します。 このオプションはリモート コントロール セッションがアクティブな間は使用できません。  

    -   **ファイル - 切断** – アクティブなリモート コントロール セッションを切断しますが、**[Configuration Manager リモート コントロール]** ウィンドウは閉じません。  

    -   **ファイル - 終了** – アクティブなリモート コントロール セッションを切断し、**[Configuration Manager リモート コントロール]** ウィンドウを閉じます。  

        > [!NOTE]  
        >  リモート コントロール セッションを切断すると、見ているコンピューターの Windows クリップボードのコンテンツは削除されます。  

    -   **表示 - 全画面** - **[Configuration Manager リモート コントロール]** ウィンドウを最大化します。  

        > [!NOTE]  
        >  全画面表示モードを終了するには、Ctrl+Alt+Break を押します。  

    -   **表示 - 画面に合わせて拡大縮小** – リモート コンピューターの画面を、**[Configuration Manager リモート コントロール]** ウィンドウのサイズに合わせて拡大縮小します。  

    -   **表示 - ステータス バー** – **[Configuration Manager リモート コントロール]** ウィンドウ ステータス バーの表示を切り替えます。  

    -   **操作 - Ctrl+Alt+Del キーの送信** – Ctrl+Alt+Del キーの組み合わせをリモート コンピューターに送信します。  

    -   **操作 - クリップボードの共有** – リモート コンピューターとの間でコピーと貼り付けを可能にします。 この値を変えた場合は、その変更を有効にするには、リモート コントロールのセッションを再起動する必要があります  

        > [!NOTE]  
        >  Configuration Manager コンソールでクリップボードを共有できないようにするには、そのコンソールを実行しているコンピューターで、レジストリ キー **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** の値を **0**に設定します。  

    -   **操作 - リモートのキーボードとマウスのロック** – リモート キーボードとマウスをロックして、ユーザーがリモート コンピューターを操作するのを防ぎます。  

    -   **ヘルプ - リモート コントロールのバージョン情報** - ビューアーの現在のバージョンが表示されます。  

5.  リモート コンピューターのユーザーは、Windows 通知領域の Configuration Manager **[リモート コントロール]** アイコンまたはリモート コントロール セッション バーのアイコンをクリックすると、リモート コントロールのセッションについて、より多くの情報を得ることができます。  

### <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Windows のコマンド ラインから、リモート コントロール ビューアーを起動するには  

-   Windows のコマンド プロンプトで、「_<Configuration Manager インストール フォルダー>\>_**\AdminConsole\Bin\x64\CmRcViewer.exe**」と入力します。  

CmRcViewer.exe は次のコマンドライン オプションをサポートします。  

- *アドレス* - 接続先クライアント コンピューターの NetBIOS 名、完全修飾ドメイン名 (FQDN)、または IP アドレスを指定します。
- *サイト サーバー名* - リモート制御セッションに関連するステータス メッセージの送信先の System Center Configuration Manager サイト サーバーの名前を指定します。
- **/?** - リモート コントロール ビューアーのコマンド ライン オプションを表示します。  
     
**例: CmRcViewer.exe** *<アドレス\>* *<\\\サイト サーバー名>*  
