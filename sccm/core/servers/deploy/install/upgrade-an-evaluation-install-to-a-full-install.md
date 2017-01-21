---
title: "評価版のアップグレード | Microsoft Docs"
description: "評価版の System Center Configuration Manager を製品版にアップグレードする方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 66dc01b7d1eeed5ad8262c60164460b669301aaf

---
# <a name="upgrade-an-evaluation-install-of-system-center-configuration-manager-to-a-full-install"></a>System Center Configuration Manager の評価版から製品版へのアップグレード

*適用対象: System Center Configuration Manager (Current Branch)*



 System Center Configuration Manager を評価版としてインストールすると、180 日後に Configuration Manager コンソールが読み取り専用になります。ライセンス認証するには、セットアップの **[サイトのメンテナンス]** ページでプロダクト キーを入力する必要があります。 この 180 日の前または後のいつでも、評価版を製品版にアップグレードできます。  

> [!NOTE]  
>  Configuration Manager コンソールを Configuration Manager の評価版に接続すると、コンソールのタイトル バーに、評価版が期限切れになるまでの日数が表示されます。 ただし、この日数は自動的に更新されず、サイトに新しく接続した場合だけ更新されます。  

 **評価版インストールを実行している次のサイトをアップグレードできます。**  

-   中央管理サイト  

-   プライマリ サイト  

セカンダリ サイトは評価版としては処理されないため、親プライマリ サイトを製品版にアップグレードした後で、セカンダリ サイトを変更する必要はありません。  

**評価版を製品版にアップグレードするための前提条件:**  

-   アップグレード中に使用する正しい製品が必要です。  

-   アカウントには、サイトがインストールされているコンピューターの **管理者** の権限が必要です  

### <a name="to-upgrade-an-evaluation-edition-of-configuration-manager-to-a-licensed-edition"></a>Configuration Manager の評価版を製品版にアップグレードするには  

1.  サイト サーバーで、 インストール フォルダー (**%path%\BIN\X64**) から **SETUP.exe** (Configuration Manager のセットアップ) を探して実行します。  インストール メディアからセットアップを実行した場合はサイトのメンテナンス オプションを利用できないため、サイト サーバーの Configuration Manager フォルダーにある Setup のコピーを実行する必要があります。  

2.  [ **開始する前に** ] ページで [ **次へ**] をクリックします。  

3.  [ **はじめに** ] ページで [ **サイトのメンテナンスを実施するか、このサイトをリセットする**] を選択し、[ **次へ**] をクリックします。  

4.  **[サイトのメンテナンス]** ページで、 **[25 文字のプロダクト キーを入力して、評価版を製品版にアップグレードする]**を選び、正しいプロダクト キーを入力して、 **[次へ]**をクリックします。  

5.  [ **マイクロソフト ソフトウェア ライセンス条項** ] ページで、ライセンス条項を読んで同意し、[ **次へ**] をクリックします。  

6.  [ **構成** ] ページで [ **閉じる** ] をクリックして、ウィザードを閉じます。  

    > [!NOTE]  
    >  アップグレードしたサイトに Configuration Manager コンソールを接続したままの場合は、サイトに接続し直さないと、コンソールのタイトル バーに評価版と表示される可能性があります。  



<!--HONumber=Dec16_HO3-->


