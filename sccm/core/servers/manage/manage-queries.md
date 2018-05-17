---
title: クエリを管理する
titleSuffix: Configuration Manager
description: クエリを管理する方法について説明します。 詳しい参照情報を記載した表が含まれています。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9d538106f2cc30a9eca5be51c4174af531bbbda9
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>System Center Configuration Manager でクエリを管理する方法

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、System Center Configuration Manager でクエリを管理する方法について説明します。  

 クエリの作成方法については、「[System Center Configuration Manager でクエリを管理する方法](../../../core/servers/manage/create-queries.md)」を参照してください。  

## <a name="how-to-manage-queries"></a>クエリを管理する方法  
 **[監視]** ワークスペースで **[クエリ]** を選択し、管理するクエリと管理タスクを選択します。  

 次の表で、管理タスクに関する詳細と、各タスクを選択する前に必要となる追加情報について説明します。  

|管理タスク|詳細|説明|  
|---------------------|-------------|----------------------|  
|**実行**|Configuration Manager コンソールで選択されたクエリを実行し、結果を表示します。|詳細情報はありません。|  
|**クライアントのインストール**|**クライアントのインストール ウィザード** を開くと、クエリによって戻されたコンピューターに Configuration Manager クライアントをインストールできます。<br /><br /> このオプションは、モバイル デバイスやユーザー、またはユーザー グループを返すクエリでは使用できません。|クライアント プッシュで Configuration Manager をインストールする方法の詳細については、「[How to deploy clients to Windows computers](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)」 (Windows コンピューターにクライアントを展開する方法) を参照してください。|  
|**エクスポート**|別のサイトへインポートができる Managed Object Format (MOF) と呼ばれる形式のファイルにクエリをエクスポートする**オブジェクトのエクスポート ウィザード** を開きます。|詳細情報はありません。|  
|**移動**|選択したクエリを **[クエリ]** ノードの下に作成されたフォルダーに移動する **[選択した項目の移動]** ダイアログ ボックスを開きます。|詳細情報はありません。|  

## <a name="see-also"></a>関連項目  
 [System Center Configuration Manager でのクエリの操作とメンテナンス](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
