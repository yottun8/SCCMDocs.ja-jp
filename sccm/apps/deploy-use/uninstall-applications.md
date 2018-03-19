---
title: "アプリケーションのアンインストール"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager を使用したアプリケーションのアンインストール"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
caps.latest.revision: 
caps.handback.revision: 
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 11b6f7ad65296131622b707fcb68d77183e3a288
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2017
---
# <a name="uninstall-applications-with-system-center-configuration-manager"></a>System Center Configuration Manager でのアプリケーションのアンインストール

*適用対象: System Center Configuration Manager (Current Branch)*


以前に展開したアプリケーションをアンインストールするには、次の操作を実行します。

-   展開の種類の作成ウィザードの **[コンテンツ]** ページで、展開の種類のコンテンツをアンインストールするコマンド ラインを指定します。  

-   **[アンインストール]** の展開操作を使用するアプリケーションを展開します。  

> [!IMPORTANT]  
> アプリケーションの種類によっては、アンインストールをサポートしていません。  

 次のリストに、アプリケーションのアンインストール動作についての詳細を示します。  

-   System Center Configuration Manager (Configuration Manager) アプリケーションをアンインストールしても、依存アプリケーションは自動的にアンインストールされません。  

-   ユーザーが **[アンインストール]** 操作を使用するアプリケーションを展開する際に、そのアプリケーションがコンピューターのすべてのユーザーにインストールされている場合、ユーザーのアカウントにアプリケーションをアンインストールする許可がないとアンインストールが失敗する可能性があります。  

-   アプリケーションがユーザーまたはデバイスに展開されているコレクションからユーザーまたはデバイスを削除しても、アプリケーションはデバイスからは自動的に削除されません。  

-   展開の目的が **[アンインストール]** である展開は、要件の規則を確認しません。 その展開が実行されているコンピューターにアプリケーションがインストールされると、そのアプリケーションはアンインストールされます。  

> [!IMPORTANT]  
> **[アンインストール]** の展開操作を使用してアプリケーションを展開する前に、コレクションに対するアプリケーションの既存の展開またはシミュレート済みの展開を削除する必要があります。  

 展開の種類を作成する方法の詳細については、「[アプリケーションの作成](../../apps/deploy-use/create-applications.md)」を参照してください。  

 アプリケーションの展開方法の詳細については、「[アプリケーションの展開](../../apps/deploy-use/deploy-applications.md)」を参照してください。  

## <a name="uninstall-an-application"></a>アプリケーションをアンインストールする  

1.  次のいずれかの方法を使用して、uninstall コマンド ラインでアプリケーションの展開の種類を構成します。  

    -   展開の作成ウィザードの **[全般]** ページで、**[この展開の種類の情報をインストール ファイルから自動的に特定する]** オプションを選択します。 情報がインストール ファイルで使用できる場合は、uninstall コマンド ラインが展開の種類のプロパティに自動的に追加されます。  

    -   展開の種類の作成ウィザードの **[コンテンツ]** ページにある **[プログラムのアンインストール]** フィールドで、コマンド ラインを指定してアプリケーションをアンインストールします。  

        > [!NOTE]  
        >  展開の種類の作成ウィザードの **[全般]** ページで **[展開の種類の情報を手動で指定する]** オプションを選択した場合にのみ、**[コンテンツ]** ページが表示されます。  

    -   *[*<*展開の種類名*> プロパティ**] **ダイアログ ボックスの **[プログラム]** タブで、コマンド ラインを指定して** [プログラムをアンインストールする] フィールドのアプリケーションをアンインストールします。  

2.  アプリケーションを展開し、ソフトウェアの展開ウィザードの **[展開設定]** ページで展開の操作の **[アンインストール]** を選択します。  

    > [!NOTE]  
    >  **[アンインストール]**の展開の操作を選択した場合には、展開の目的は自動的に **[必須]**に構成されます。  
