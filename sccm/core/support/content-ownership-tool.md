---
title: Content Ownership Tool
titleSuffix: Configuration Manager
description: Content Ownership Tool を使用して、Configuration Manager 内の孤立したパッケージの所有権を変更します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 962b19f1849628776eb1b9059089f7ce8e6df3ee
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385983"
---
# <a name="content-ownership-tool"></a>Content Ownership Tool

*適用対象: System Center Configuration Manager (Current Branch)*

Content Ownership Tool は、[Configuration Manager のツール](/sccm/core/support/tools)の 1 つです。 これにより、Configuration Manager 内の孤立したパッケージの所有権が変更されます。 孤立したパッケージには、所有しているサイト サーバーがありません。 パッケージはこのサイト サーバーによって所有され続けている場合、サイト サーバーを削除することによって孤立させることができます。

Configuration Manager 階層内の任意のサイト サーバー上で Content Ownership Tool を実行します。 十分なパッケージのアクセス許可を持つ管理ユーザーとしてサインインします。  

> [!Tip]  
> `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` で **ContentLibraryCleanup.exe** を使用して、配布ポイントから孤立したコンテンツを*削除*します。 詳細については、「[コンテンツ ライブラリのクリーンアップ ツール](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool)」を参照してください。  



## <a name="features"></a>機能

- 孤立したパッケージをすべて表示する  

- 孤立していない場合でも、すべてのパッケージを表示する  

- サイトへの接続の状態を表示する  

- 名前、サイト コード、またはパッケージの種類によってパッケージをフィルター処理する  

- 任意の表示列で並べ替える  

- 1 つのアクションを使って 1 つまたは複数のパッケージの割り当てを変更する  

- 所有権の転送アクティビティの進行状況を表示する  



## <a name="usage"></a>使用方法

**ContentOwnershipTool.exe** を実行してツールを開始します。 コンピューター上のローカル管理者のアクセス許可は、ツールを実行するためには必要ありません。

コマンドライン パラメーターはありません。

> [!Important]   
> このツールによって、孤立したパッケージの所有権が変更されます。 パッケージ自体が、保存されている配布ポイントから移動されることはありません。 この所有権の変更によって、パッケージが配布ポイントで更新されることはありません。 また、これにより、クライアントがパッケージの展開用のポリシーを再評価することもありません。 所有権が変更された後に、新しいサイト サーバーがソース ファイルにアクセスできることを確認します。 各パッケージのソース ファイルに対する**読み取り**アクセス許可がある必要があります。 



## <a name="see-also"></a>関連項目

- [コンテンツ管理の基本的な概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [コンテンツ ライブラリ](/sccm/core/plan-design/hierarchy/the-content-library)
