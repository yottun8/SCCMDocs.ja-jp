---
title: "実稼働前コレクションのクライアント アップグレードをテストする | System Center Configuration Manager"
description: "System Center Configuration Manager で実稼働前コレクションのクライアント アップグレードをテストします。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
caps.latest.revision: 10
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e648b94a475bda2b35d69ff0a8863d2e0d248fb


---
# <a name="how-to-test-client-upgrades-in-a-preproduction-collection-in-system-center-configuration-manager"></a>System Center Configuration Manager で実稼働前コレクションのクライアント アップグレードをテストする方法

*適用対象: System Center Configuration Manager (Current Branch)*

Windows PC やデバイスで Configuration Manager クライアントをアップグレードするために、サイトの他の部分をアップグレードする前に、実稼働前コレクションで新しいクライアント バージョンをテストできます。  これを行うと、実稼働前コレクションに含まれるデバイスのみが新しいクライアントにアップグレードされます。 この実稼働前コレクションでクライアントをテストし終えた後で、そのクライアントを昇格できます。これにより、サイトの他の部分で新しいバージョンのクライアント ソフトウェアを使用できるようになります。  

 実稼働前環境でのクライアントのテストは、3 つの基本的な手順に従って実行します。  

1.  「[自動クライアント アップグレードを構成して実稼働前コレクションを使用するには](#BKMK_config) 」の手順を実行して、実稼働前コレクションを使用する。  

2.  「[新しいバージョンのクライアントを含む Configuration Manager の更新プログラムをインストールするには](#BKMK_install) 」の手順を実行して、新しいバージョンのクライアントを含む更新プログラムをインストールする。 インストール中、新しいクライアント ソフトウェアの実稼働前コレクションを使用するように指定します。  

3.  実稼働前環境で十分にテストした後、「[新しいクライアントを実稼働環境に昇格するには](#BKMK_promote) 」の手順に従って新しいクライアントを昇格する。  

> [!TIP]  
>  Configuration Manager の以前のバージョン \(Configuration Manager 2007 または System Center 2012 Configuration Manager など\) から、サーバー インフラストラクチャをアップグレードする場合は、Configuration Manager クライアントをアップグレードする前に、現在のすべてのブランチの更新プログラムのインストールを含む、サーバーのアップグレードを完了することをお勧めします。   現在のブランチの最新の更新プログラムには、クライアントの最新バージョンが含まれているため、使用するすべての Configuration Manager 更新プログラムをインストールした後に、クライアントのアップグレードを実行することをお勧めします。  

##  <a name="a-namebkmkconfiga-to-configure-automatic-client-upgrades-to-use-a-preproduction-collection"></a><a name="BKMK_config"></a> 自動クライアント アップグレードを構成して実稼働前コレクションを使用するには  

1. 実稼働前クライアントを展開するコンピューターを含むコレクションを設定します。 この手順の詳細については、「[How to create collections](..\collections\create-collections.md)」 (コレクションを作成する方法) を参照してください。

> [!NOTE]
> 実稼働前コレクションには、ワークグループ コンピューターを含めないでください。 ワークグループ コンピューターは、配布ポイントに必要な認証を使用して、実稼働前クライアント パッケージにアクセスできません。   

1.  Configuration Manager コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** の順に選択し、**[階層設定]** をクリックします。  

     **[階層設定のプロパティ]** の **[クライアント アップグレード]**タブで次の操作を実行します。  

    -    **[実稼働前クライアントを使用して実稼働前コレクション内のすべてのクライアントを自動的にアップグレードする]**を選びます。  

    -   実稼働前コレクションとして使用するコレクションの名前を入力します。  

2.  **[OK]** をクリックして、クライアント アップグレード設定を保存します。  

##  <a name="a-namebkmkinstalla-to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a><a name="BKMK_install"></a> 新しいバージョンのクライアントを含む Configuration Manager の更新プログラムをインストールするには  

1.  Configuration Manager コンソールで、**[管理]** > **[Cloud Services]** > **[更新プログラムとサービス]** の順に開き、**利用可能な**更新プログラムを選択して、**[更新パックのインストール]** をクリックします。  

     更新プログラムのインストールの詳細については、「[System Center Configuration Manager の更新プログラム](../../../../core/servers/manage/updates.md)」を参照してください  

2.  更新プログラムのインストール中に、ウィザードの **[クライアント オプション]** ページで **[実稼働前コレクションでのテスト]**を選び、 **[次へ]**をクリックします。  

3.  ウィザードの残りの手順を完了し、更新パックをインストールします。  

     ウィザードを完了すると、実稼働前コレクション内のクライアントが、更新されたクライアントの展開を開始します。 **[監視]** > **[クライアント ステータス]** > **[実稼働前クライアント展開]**と移動して、アップグレード済みのクライアントの展開を監視できます。 詳細については、「[System Center Configuration Manager でクライアントの展開ステータスを監視する方法](../../../../core/clients/deploy/monitor-client-deployment-status.md)」を参照してください。

    > [!NOTE]
    > 実稼働前コレクションでサイト システムの役割をホストしているコンピューターの展開ステータスは、クライアントが正常に展開された場合でも、 **未開始** として報告されることがあります。 クライアントを実稼働環境に昇格すると、展開のステータスが正しく報告されます。

##  <a name="a-namebkmkpromotea-to-promote-the-new-client-to-production"></a><a name="BKMK_promote"></a> 新しいクライアントを実稼働環境に昇格するには  

1.  Configuration Manager コンソールで、**[管理]** > **[Cloud Services]** > **[更新プログラムとサービス]** の順に開き、**[実稼働前クライアントの昇格]** をクリックします。

    > [!TIP]
    > **[実稼働前クライアントの昇格]** ボタンは、コンソールの **[監視]** > **[クライアント ステータス]** > **[実稼働前クライアント展開]**で、クライアント展開を監視中である場合も使用することができます。

2.  ダイアログ ボックスで、実稼働および実稼働前のクライアント バージョンを確認し、正しい実稼働前コレクションが指定されていることを確認して、 **[昇格]**をクリックします。 確認ボックスで **[はい]**をクリックします。  

3.  ダイアログ ボックスが閉じた後、階層で使われている現在のクライアントのバージョンが、更新されたクライアントのバージョンに置き換えられます。 その後、サイト全体のクライアントをアップグレードできます。 詳細については、「[System Center Configuration Manager で Windows コンピューター用クライアントをアップグレードする方法](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)」を参照してください。  



<!--HONumber=Nov16_HO1-->


