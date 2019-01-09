---
title: Windows をクライアント アップグレードから除外する
titleSuffix: Configuration Manager
description: Windows クライアントを System Center Configuration Manager のアップグレードから除外する方法について説明します。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b14ff463d6f39e74ad757d992fda1042f534a2cd
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414669"
---
# <a name="how-to-exclude-upgrading-clients-for-windows-computers-in-system-center-configuration-manager"></a>System Center Configuration Manager で Windows コンピューター用クライアントをアップグレードから除外する方法

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

バージョン 1610 より、クライアントのコレクションを更新されたクライアントのバージョンの自動インストールから除外できるようになりました。 これは、ソフトウェアの更新に基づいたアップグレード、ログオン スクリプト、およびグループ ポリシーなどのその他の方法とともに、自動アップグレードに適用されます。 これは、クライアントをアップグレードする際により注意が必要なコンピューターのコレクションに使用できます。 除外されるコレクション内にあるクライアントは、更新されたクライアント ソフトウェアのインストールの要求を無視します。

## <a name="configure-exclusion-for-automatic-upgrades"></a>自動アップグレードからの除外を構成する

1. Configuration Manager コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** の順に選択し、**[階層設定]** をクリックします。

2. **[クライアント アップグレード]** タブをクリックします。

3. **[指定したクライアントをアップグレードから除外する]** チェック ボックスをクリックして、[除外コレクション] で除外するコレクションを選択します。 除外するコレクションを 1 つだけ選択できます。

4.  **[OK]** をクリックしてコンソールを閉じ、構成を保存します。 クライアントがポリシーを更新すると、除外されるコレクション内のクライアントに、クライアント ソフトウェアの更新プログラムが自動的にインストールされなくなります。 詳細については、「[Windows コンピューター用クライアントをアップグレードする方法](upgrade-clients-for-windows-computers.md)」を参照してください。

![自動アップグレード除外の設定](media/automatic_upgrade_exclusion.png)



>[!NOTE]
>ユーザー インターフェイスにどの方法でもクライアントがアップグレードされないことが示されますが、これらの設定をオーバーライドするために使用できる 2 つの方法があります。 クライアント プッシュ インストールと手動クライアント インストールを使用すると、この設定をオーバーライドできます。 詳細については、次のセクションを参照してください。

## <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>除外されるコレクション内にあるクライアントをアップグレードする方法

コレクションが除外されるように設定されている限り、そのコレクションのメンバーは、除外をオーバーライドする 2 つの方法のいずれかでクライアント ソフトウェアを更新することしかできません。
- **クライアント プッシュ インストール**: クライアント プッシュ インストールを使用して、除外されるコレクション内にあるクライアントをアップグレードすることができます。 これは管理者の意図と見なされるために許可され、除外からコレクション全体を削除しなくてもクライアントをアップグレードすることができます。       

- **手動クライアント インストール**: ccmsetup で、コマンド ライン スイッチ ***/ignoreskipupgrade*** を使用すると、除外されるコレクション内のクライアントを手動でアップグレードすることができます。

  このスイッチを使用しないで除外されるコレクションのメンバーであるクライアントを手動でアップグレードしようとすると、クライアントに新しいクライアント ソフトウェアがインストールされません。 詳細については、「[Configuration Manager クライアントの手動インストール方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)」をご覧ください。

クライアント インストール方法の詳細については、「[System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)」をご覧ください。
