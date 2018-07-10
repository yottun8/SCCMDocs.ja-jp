---
title: Configuration Manager とサービスとしての Windows
titleSuffix: Configuration Manager
description: サービスとしての Windows をサポートするために Configuration Manager の Current Branch を導入する場合の基本情報について説明します。
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e2fb6b022526ce4bae1de21012ac996dbcea35cf
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2018
ms.locfileid: "36260909"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager とサービスとしての Windows

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager では、Windows 10 の機能更新プログラムを包括的に制御できます。 サービス モデルとして Windows を完全に導入するには、Configuration Manager の Current Branch モデルを導入する必要もあります。 Windows 10 を最新の状態に保つには、最適なエクスペリエンスを実現するために Configuration Manager を最新の状態に保つ必要があります。 Windows 10 の魅力的な新しい企業の機能を最大限に活用するには、新しいバージョンの Configuration Manager が必要です。 この記事は、Configuration Manager の Current Branch を導入するために必要な主な記事のランディング ページとして提供されています。 Configuration Manager の Current Branch を準備してからサービスとしての Windows に進みます。

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Configuration Manager の Current Branch の導入に関する主な記事

| アーティクル        | 説明          | 
| ------------- |-------------|
|[Configuration Manager Current Branch の概要](/sccm/core/plan-design/changes/whats-new-incremental-versions)|Configuration Manager (Current Branch) の新しいサービス モデルの要点を簡単に説明します。|
|[サポート ライフサイクル](/sccm/core/servers/manage/current-branch-versions-supported)|新しいサポートおよびサービス モデルについて説明します。|
|[削除された項目と非推奨の項目](/sccm//core/plan-design/changes/deprecated/removed-and-deprecated)|Configuration Manager の使用に影響する可能性のある将来の変更について早期に注意するものです。|
|[Configuration Manager Current Branch の更新](/sccm/core/servers/manage/updates)|Configuration Manager に機能更新プログラムを適用するための簡単なコンソール内の方式について説明します。|
|[利用可能な更新プログラムの取得](/sccm/core/servers/manage/install-in-console-updates#get-available-updates)|新しい Configuration Manager の機能更新プログラムを取得するために利用できる 2 つのモードについて説明します。|
|[更新プログラムのチェックリスト](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)|更新プログラムのバージョン固有のチェックリスト (適用可能な場合) を提供します。| 
|[新しい Configuration Manager の機能更新プログラムのインストール](/sccm/core/servers/manage/install-in-console-updates#bkmk_install)|機能更新プログラムの簡単なインストール手順について説明します。|
|[Windows 10 のサポート](/sccm/core/plan-design/configs/support-for-windows-10)|Windows 10 (および ADK) バージョンのサポート マトリックスを提供します。|
|[Configuration Manager の Technical Preview](/sccm/core/get-started/technical-preview)|ConfigMgr テクニカル プレビュー プログラムに関する情報を提供します。|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>サービスとしての Windows の導入に関する主な記事
| アーティクル        | 説明          | 
| ------------- |-------------|
|[サービスとしての Windows の管理](/sccm/osd/deploy-use/manage-windows-as-a-service)|サービス プランを使用して Windows 10 の機能更新プログラムを展開する方法について説明します。|
|[タスク シーケンスによる Windows 10 のアップグレード](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)|追加の推奨事項で Windows 10 をアップグレードするためのタスク シーケンスの作成に関する詳細。|
|[段階的展開](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|段階的展開は、複数のコレクションでのタスク シーケンスの調整および順序付けされたロールアウトを自動化します。|  
|[Windows 10 更新プログラムの配信の最適化](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)|Configuration Manager を使用して、Windows 10 を最新の状態に保つための更新プログラムのコンテンツを管理します。|
|[Upgrade Readiness との統合](/sccm/core/clients/manage/upgrade/upgrade-analytics)|Upgrade Readiness を使用すると、Windows 10 にアップグレードするため、環境内のデバイスの対応性を評価および分析することができます。| 
|[Windows Update for Business 統合 (オプション)](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|Configuration Manager を使用して、Windows Update for Business (WUfB) ポリシーを定義して展開する方法について説明します。|
|[Microsoft Intune と Windows Update for Business での共同管理の使用 (オプション)](/sccm/core/clients/manage/co-management-overview)|共同管理の概要を示します。| 


## <a name="related-articles"></a>関連記事

- [ConfigMgr 2012 から System Center Configuration Manager (Current Branch) へのインプレース アップグレード](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [ConfigMgr 2007 から System Center Configuration Manager (Current Branch) への移行の計画](/sccm/core/migration/planning-for-migration)