---
title: "デバイスをコレクションに自動的に分類する | System Center Configuration Manager"
description: "System Center Configuration Manager でデバイスをコレクションに自動的に分類します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6e1e8c1da1209be03d4a1377dcc0c9ce9478a216

---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>System Center Configuration Manager でデバイスをコレクションに自動的に分類する

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Intune と Configuration Manager を使用している場合に、デバイス コレクションにデバイスを自動的に配置するために使用できるデバイス カテゴリを作成することができます。 ユーザーは Intune にデバイスを登録するときに、デバイス カテゴリの選択を求められます。 Configuration Manager コンソールから、デバイスのカテゴリをさらに変更できます。

> [!IMPORTANT]  
    >  この機能は、Microsoft Intune の **2016 年 6 月**のリリースで機能します。 これらの手順を実行する前に、今回のリリースに更新していることを確認してください。

## <a name="create-device-categories"></a>デバイス カテゴリを作成する

1.  Configuration Manager コンソールの [**資産とコンプライアンス**] ワークスペースで、[**概要**] を展開してから [**デバイス コレクション**] をクリックします。
2.  [**ホーム**] タブの [**デバイス コレクション**] グループで、[**デバイス カテゴリの管理**] をクリックします。
3.  [**デバイス カテゴリの管理**] ダイアログ ボックスでは、カテゴリの作成、編集、または削除ができます。

## <a name="associate-a-collection-with-a-device-category"></a>コレクションをデバイス カテゴリに関連付ける

コレクションをデバイス カテゴリと関連付けると、指定したカテゴリのすべてのデバイスがそのコレクションに追加されます。

> [!IMPORTANT]  
    >  [**すべてのシステム**] などの組み込みコレクションにデバイス カテゴリの規則を追加することはできません。

1.  デバイス コレクションの [**プロパティ**] ダイアログの [**メンバーシップの規則**] で、[**規則の追加**] > [**デバイス カテゴリの規則**] の順にクリックします。
2.  [**デバイス カテゴリの選択**] ダイアログ ボックスで、コレクション内のすべてのデバイスに適用される 1 つ以上のカテゴリを選択します。
3.  [**デバイス カテゴリの選択**] ダイアログ ボックスと [コレクションのプロパティ] ダイアログ ボックスを閉じます。


## <a name="change-the-category-of-a-device"></a>デバイスのカテゴリを変更する

1.  Configuration Manager コンソールの [**資産とコンプライアンス**] ワークスペースで、[**概要**] を展開してから [**デバイス**] をクリックします。
2.  [**デバイス**] の一覧からデバイスを選択して、[**ホーム**] タブの [**デバイス**] グループで [**カテゴリの変更**] をクリックします。
3.  [**デバイス カテゴリの編集**] ダイアログ ボックスで、このデバイスに適用するカテゴリを選択し、[**OK**] をクリックします。

## <a name="view-which-category-a-device-belongs-to"></a>デバイスが属するカテゴリを表示する

1.  Configuration Manager コンソールの [**資産とコンプライアンス**] ワークスペースで、[**概要**] を展開してから [**デバイス**] をクリックします。
2.  [**デバイス**] 一覧の [**デバイス カテゴリ**] 列にカテゴリが表示されます。
> [!TIP]  
    >  [**デバイス カテゴリ**] 列が表示されない場合、[**デバイス**] 一覧のいずれかの列の見出し ([**名前**] など) を右クリックし、[**デバイス カテゴリ**] を選択します。

デバイスをカテゴリに割り当て、その後、カテゴリを削除した場合、[**Microsoft Intune に各ユーザーが登録したデバイス一覧**] レポートには、[**デバイス カテゴリ**] 列にカテゴリ名ではなく GUID が表示されます。



<!--HONumber=Nov16_HO1-->


