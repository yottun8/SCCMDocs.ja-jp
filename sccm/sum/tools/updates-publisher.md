---
title: Updates Publisher
titleSuffix: Configuration Manager
description: System Center Updates Publisher を使用して、カスタム更新プログラムを管理する
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2047874bb44c89e510abd52a387277e749cf65db
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896449"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

「オブジェクトの*適用対象: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) は、独立系ソフトウェア ベンダーまたは基幹業務アプリケーション開発者によるカスタム更新プログラムの管理を可能にするスタンドアロン ツールです。 これには、ドライバーと更新プログラムのバンドルなどの依存関係のある更新プログラムが含まれています。

Updates Publisher を使用すると、次の操作が行えます。

-   外部カタログからの更新プログラムのインポート (Microsoft 以外の更新カタログ)。
-   適用性や展開メタデータなどの更新定義の変更。
-   外部カタログへの更新プログラムのエクスポート。
-   更新サーバーへの更新プログラムの公開。

更新サーバーに更新プログラムを公開した後に System Center Configuration Manager を使用することで、マネージド デバイスに対してこれらの更新プログラムを検出および展開できます。

> [!TIP]  
> 前のバージョンの [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111) は引き続きサポートされます。 今回の更新バージョンには機能に関する変更はありませんが、サポートされるオペレーティング システムの追加、タスクを簡略化するための新機能、更新されたユーザーインターフェースなどが含まれています。

## <a name="workspaces"></a>ワークスペース
Updates Publisher を開くと、*[更新プログラム] ワークスペース*の概要ノードが既定として設定されています。

![Updates Publisher コンソール](media/console1.png)   


Updates Publisher には、整理に役立つ 4 つのワークスペースがあります。


**[更新プログラム] ワークスペース:** このワークスペースは、ソフトウェア更新プログラムの[作成](/sccm/sum/tools/create-updates-with-updates-publisher)と[管理](/sccm/sum/tools/manage-updates-with-updates-publisher)、バンドルの更新などに使用します。 これには、パブリケーションへの更新プログラムとバンドルの割り当て、公開、別の Updates Publisher のリポジトリへのエクスポートなどが含まれています。

**[パブリケーション] ワークスペース:** ここでは、[パブリケーションを管理](/sccm/sum/tools/updates-publisher-publications)します。 パブリケーションは作成した更新プログラムのグループで、更新プログラムのエクスポートと公開を簡略化します。

パブリケーションの管理には、更新プログラムをサーバに公開してクライアントが更新プログラムを見つけてインストールできること、他の Updates Publisher によるインストール用途のために更新プログラムとバンドルをエクスポートすること、またはパブリケーションのコンテンツや詳細を変更することなどが含まれています。



**[動作規則] ワークスペース:** ここでは、[適用規則を管理](/sccm/sum/tools/updates-publisher-applicability-rules)します。この規則は保存でき、展開した更新プログラムと共に使用できます。 規則には以下の 2 種類があります。

-   インストール可能な規則 – この規則は、クライアントによる更新プログラムのインストールの判断に役立ちます。
-   インストール済みの規則 – この規則は、更新プログラムが既にインストールされていることを確認します。

**[カタログ] ワークスペース:** このワークスペースは、[ソフトウェアの更新カタログの管理](/sccm/sum/tools/updates-publisher-catalogs)と追加に使用します。 これには、カタログから Updates Publisher のリポジトリへのソフトウェアの更新プログラムのインポートが含まれます。
## <a name="first-steps"></a>最初のステップ
作業を始めるには、まず Updates Publisher の[インストール](/sccm/sum/tools/install-updates-publisher)とオプションの[構成](/sccm/sum/tools/updates-publisher-options)を行います。
