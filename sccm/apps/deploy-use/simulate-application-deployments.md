---
title: "アプリケーションの展開をシミュレートする | System Center Configuration Manager"
description: "アプリケーションをインストールすることなく、展開の種類に関する検出方法、要件、および依存関係を評価します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a7d9267d35b58fdc6a01b869eb739e9c721db4a4


---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>System Center Configuration Manager でアプリケーションの展開をシミュレートする

*適用対象: System Center Configuration Manager (Current Branch)*

アプリケーションをインストールしたり、アンインストールせずに、コンピューターへのアプリケーションの展開適用性をテストしたいときは、展開シミュレーションを使用します。 シミュレーションされた展開は、展開の種類について検出された方法、要件、依存関係を評価し、[監視 **** ] ワークスペースの [展開 **** ] ノードに結果を表示します。 System Center Configuration Manager でアプリケーションの展開をシミュレーションするときは、このトピックの手順を使用します。  

> [!NOTE]  
>  モバイル デバイスのコレクションには、展開シミュレーションを使用できません。  
>   
>  アプリケーションの展開シミュレーションがアクティブな場合は、展開目的が [アンインストール] のアプリケーション展開を行うことはできません。 ****  
  
シミュレートしたアプリケーションの展開を構成するには、次の手順を実行します。
  
1.  Configuration Manager コンソールで、次のいずれかを選択します。  

    -   ユーザーのコレクション  

    -   デバイスのコレクション  

    -   Configuration Manager アプリケーション  

2.  [ **ホーム** ] タブの [ **展開** ] グループで、[ **展開のシミュレート**] をクリックします。  

3.  アプリケーション展開のシミュレーション ウィザードで、次の情報を指定します。 ****  

    -   **アプリケーション** - **[参照]** をクリックし、シミュレーションされた展開を作成するアプリケーションを選択します。  

    -   **コレクション** - **[参照]** をクリックし、シミュレーションされた展開に使用するコレクションを選択します。  

    -   **アクション** - ドロップダウン リストから、選択したアプリケーションのインストールをシミュレーションするか、アンインストールをシミュレーションするかを選択します。  

    -   **ユーザーのログインに関係なく自動的に展開する** - このオプションをオンにすると、クライアントがログインしているかどうかにかかわらず、クライアントはシミュレーションされた展開を評価します。  

4.  [次へ ****] をクリックし、[概要 **** ] ページで情報を確認して、ウィザードを完了し、シミュレーションされたアプリケーション展開を作成します。  

5.  シミュレーションされるアプリケーションは、[ **監視** ] ワークスペースの [ **展開** ] ノードに、[ **シミュレート**] の目的で表示されます。 アプリケーション展開の監視方法の詳細については、「[Configuration Manager でのアプリケーションの監視方法](../../apps/deploy-use/monitor-applications-from-the-console.md)」を参照してください。  



<!--HONumber=Nov16_HO1-->


