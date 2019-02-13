---
title: アプリケーションを管理する
titleSuffix: Configuration Manager
description: System Center Configuration Manager でアプリケーションを管理します。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4ff166d93812b07c37c31228ca395f0cfcf94de6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156959"
---
# <a name="manage-applications-in-system-center-configuration-manager"></a>System Center Configuration Manager でのアプリケーションの管理

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Intune または Configuration Manager のオンプレミス デバイス管理でデバイスを管理すると、さらに次のアプリケーションの種類も管理できます。
- Windows Phone アプリケーション パッケージ (*.xap ファイル)
- iOS アプリ パッケージ (*.ipa ファイル)
- Android アプリ パッケージ (*.apk ファイル)
- Android 用アプリ パッケージ (Google Play 内)
- Windows Phone アプリケーション パッケージ (Windows Phone ストア内)
- MDM を介した Windows インストーラー
- Web アプリケーション

このセクションでは、ハイブリッド MDM またはオンプレミス MDM を使用したアプリケーションの作成と管理について詳しく説明します。

「[System Center Configuration Manager アプリケーションの管理タスク](../../apps/deploy-use/management-tasks-applications.md)」では、System Center Configuration Manager のアプリケーションと展開の種類の管理に関するより一般情報を提供しています。

## <a name="deploying-and-monitoring-apps"></a>アプリの展開と監視

System Center Configuration Manager でアプリケーションを展開し監視するモバイル デバイスのプロセスは、ラップトップやデスクトップ コンピューターなどのオンサイト デバイスのプロセスと同じです。 アプリケーションの展開と監視に関する一般情報は、次のトピックを参照してください。

- [System Center Configuration Manager でアプリケーションを展開する](../../apps/deploy-use/deploy-applications.md)
- [System Center Configuration Manager でアプリケーションを監視する](../../apps/deploy-use/monitor-applications-from-the-console.md)

アプリケーションの展開と監視において留意すべき、モバイル デバイスの管理に固有の考慮事項は次のとおりです。

- MDM 登録デバイスは、シミュレートされた展開、ユーザー エクスペリエンス、またはスケジュール設定をサポートしていません。

- 既に構成している場合は、iOS アプリの構成ポリシーを使用して展開を関連付けることができます。 [アプリ構成ポリシーを使用した iOS アプリの構成](configure-ios-apps-with-app-configuration-policies.md)に関する記事を参照してください。

### <a name="next-steps"></a>次のステップ

いずれはアプリケーションに変更を加えたり、アンインストールしたり、既に展開されているアプリケーションを新しいアプリケーションに置き換えたりすることが必要になる可能性があります。 「[System Center Configuration Manager でのアプリケーションの更新とインベントリからの削除](../../apps/deploy-use/update-and-retire-applications.md)」を参照して、これらの機能を理解してください。
