---
title: "アプリケーションを修正して置き換える方法 | Microsoft Docs"
description: "System Center Configuration Manager アプリケーションのバージョンを操作し、置き換える方法を学習します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a04ac74df97741f49d7aae7b599bb60d5725a592
ms.openlocfilehash: 28bea9210c9c58dabbb00a995e78cfedd1738291


---
# <a name="revise-and-supersede-applications-in-system-center-configuration-manager"></a>System Center Configuration Manager でアプリケーションを修正して置き換える

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、System Center Configuration Manager アプリケーションのバージョンを操作する方法と、アプリケーションを新しいバージョンで置き換える方法について説明します。  

##  <a name="application-revisions"></a>アプリケーションのリビジョン  
 アプリケーションまたはアプリケーションに含まれる展開の種類を修正すると、Configuration Manager はそのアプリケーションの新しいリビジョンを作成します。 各アプリケーションのリビジョン履歴を表示できます。 プロパティの表示、旧リビジョンのアプリケーションの復元、または旧リビジョンの削除を行うこともできます。  

### <a name="to-display-an-application-revision-history"></a>アプリケーションのリビジョン履歴を表示するには  

1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]** > **[アプリケーション管理]** > **[アプリケーション]** の順に選択し、必要なアプリケーションを選択します。  

3.  **[ホーム]** タブの **[アプリケーション]** グループで **[リビジョン履歴]** を選択して **[アプリケーションのリビジョン履歴]** ダイアログ ボックスを開きます。  

### <a name="to-view-an-application-revision"></a>アプリケーションのリビジョンを表示するには  

1.  **[アプリケーションのリビジョン履歴]** ダイアログ ボックスで、アプリケーションのリビジョンを選択し、**[表示]** を選択します。  

2.  [プロパティ **** ] ダイアログ ボックスで、選択したアプリケーションのプロパティを確認します。  

    > [!NOTE]  
    >  表示されるアプリケーションのプロパティは、読み取り専用です。  

3.  [プロパティ] **** ダイアログ ボックスを閉じます。  

### <a name="to-restore-an-application-revision"></a>アプリケーションのリビジョンを復元するには  

1.  **[アプリケーションのリビジョン履歴]** ダイアログ ボックスで、アプリケーションのリビジョンを選択し、**[復元] **を選択します。  

2.  **[リビジョン復元の確認]** ダイアログ ボックスで **[はい]** を選択すると、選択したアプリケーションのリビジョンが復元されます。  

### <a name="to-delete-an-application-revision"></a>アプリケーションのリビジョンを削除するには  

1.  **[アプリケーションのリビジョン履歴]** ダイアログ ボックスで、アプリケーションのリビジョンを選択し、**[削除]** を選択します。  

2.  **[アプリケーションのリビジョンの削除]** ダイアログ ボックスで、**[はい]** を選択します。  

> [!IMPORTANT]  
>  現在のアプリケーションが既にインベントリから削除され、参照が含まれない場合にのみ、そのアプリケーション リビジョンを削除できます。  

##  <a name="application-supersedence"></a>アプリケーションの置き換え  
 Configuration Manager のアプリケーション管理では、置き換えの関係を使用して、既存のアプリケーションをアップグレードまたは置き換えできます。 アプリケーションを置き換える際、新しい展開の種類を指定して置換対象のアプリケーションの展開の種類を置き換えたり、置き換わるアプリケーションをインストールしたりする前に、置換対象のアプリケーションをアップグレードするのか置換対象のアプリケーションをアンインストールするのか決定することもできます。  

> [!IMPORTANT]  
>  置き換え対象の展開の種類をアンインストールするオプションを選択すると、別のコレクションの種類に展開された展開の種類で展開の種類を置き換えることはできません。  たとえば、置換対象の展開の種類をアンインストールするオプションが選択されている場合、デバイス コレクションに展開されている展開の種類を、ユーザー コレクションに展開されている展開の種類で置き換えることはできません。  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>アプリケーションをアップグレードするか、置き換えるかを決定します。  
 アプリケーションを置き換えるか、アップグレードするかどうかは、アプリケーション プロパティ ダイアログ ボックスの [ **置き換えの関係の指定** ] ダイアログ ボックスで指定します。 このダイアログ ボックスで [ **アンインストール** ] オプションを有効にするかどうかによって、置き換えの種類が決まります。  

-   (同じアプリケーション ID のまま) 同じアプリケーションの新しいバージョンに更新する必要がある場合は、**[アンインストール]** を有効に**しない**でください。  

-   (アプリケーション ID が異なる) 別のアプリケーションに変更する場合は、[ **アンインストール**] を有効にします。 置き換えられたアプリケーションのバージョンは、削除する必要があります。  

### <a name="supersede-dependent-applications"></a>依存アプリケーションの置き換え  
 この例の**マスター アプリケーション**とは、依存関係がある展開対象のアプリケーションを指します。  

 置き換えの関係を作成することによって、依存アプリケーションを新しいバージョンに更新できます。  

1.  新しい依存アプリケーションと元の依存アプリケーションの両方がマスターのアプリケーションの同じ依存関係グループに含まれていることを確認します。  

2.  元の依存アプリケーションを新しい依存アプリケーションに置き換える、置き換えの関係を作成します。  

 マスター アプリケーションの新規インストール中に、この新しい依存アプリケーションがインストールされます。 マスター アプリケーションの既存のインストールは、新しい依存アプリケーションで更新されます。  

 最終的に、マスター アプリケーションのすべての展開で、新しい依存アプリケーションが使用されることになります。  

### <a name="further-considerations"></a>その他の注意事項  

-   依存アプリケーションには、複数の置き換えの関係を指定できます。 置き換えチェーンの最上位にある依存アプリケーションがインストールされます。  

-   依存アプリケーションは、マスター アプリケーションがインストールされているデバイスに展開されている必要があります。そうでなければ、依存アプリケーションはインストールされません。  

-   マスター アプリケーションの新規インストールに複数の依存関係がある場合、依存関係の順番は、インストールされる依存アプリケーションのバージョンによって決まります。  

### <a name="to-specify-a-supersedence-relationship"></a>置き換えの関係を指定するには  

1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]** > **[アプリケーション管理]** > **[アプリケーション]** の順に選択し、別のアプリケーションを置き換えるアプリケーションを選択します。  

3.  **[ホーム]** タブの **[プロパティ]** グループで **[プロパティ]** を選択して、**[<アプリケーション名> プロパティ]** ダイアログ ボックスを開きます。  

4.  *[<アプリケーション名\>* **プロパティ]**ダイアログ ボックスの **[置き換え]** タブで、**[追加]** を選択します。  

5.  [置き換えの関係の指定 **** ] ダイアログ ボックスで、[参照 ****] をクリックします。  

6.  **[アプリケーションの選択]** ダイアログ ボックスで、置き換えるアプリケーションを選択して、**[OK]** を選択します。  

7.  **[置き換えの関係の指定]** ダイアログ ボックスで、置換対象のアプリケーションの展開の種類の代わりとなる置き換える展開の種類を選択します。  

    > [!NOTE]  
    >  既定では、新しい展開の種類によって置換対象のアプリケーションの展開の種類はアンインストールされません。 このシナリオは、既存のアプリケーションにアップグレードを展開する場合によく使用されます。 新しい展開の種類をインストールする前に既存の展開の種類を削除するには、[アンインストール **** ] を選択します。 アプリケーションをアップグレードする際、まず、ラボ環境でこれをテストしていることを確認します。  

8.  **[OK]** を選択して、**[置き換えの関係の指定]** ダイアログ ボックスを閉じます。  

9. **[OK]** を選択して、*[<アプリケーション名\>* **プロパティ]** ダイアログ ボックスを閉じます。  

### <a name="to-display-applications-that-supersede-the-current-application"></a>現在のアプリケーションを置き換えるアプリケーションを表示するには  

1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]** を選択します。  

2.  **[ソフトウェア ライブラリ]** ワークスペースで、**[アプリケーション管理]** を展開し、**[アプリケーション]** を選択してから、目的のアプリケーションを選択します。  

3.  **[ホーム]** タブの **[プロパティ]** グループで **[プロパティ]** を選択して、*[<アプリケーション名\>* **プロパティ]** ダイアログ ボックスを開きます。  

4.  *[<アプリケーション名\>* **プロパティ]** ダイアログ ボックスの **[参照]** タブで、**[リレーションシップの種類]** ドロップダウン リストから **[このアプリケーションを置き換えるアプリケーション]** を選択します。  

5.  選択したアプリケーションを置き換えるアプリケーションのリストを確認し、**[OK]** を選択して *[<アプリケーション名\>* **プロパティ]** ダイアログ ボックスを閉じます。  



<!--HONumber=Dec16_HO3-->

