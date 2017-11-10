---
title: "拡張相互運用性クライアントを Current Branch で使用する "
titleSuffix: Configuration Manager
description: "Configuration Manager サイトで、Configuration Manager の Long-Term Servicing Branch のクライアントを使用する方法について説明します。"
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: ba79f2b9cf0cdfc4525645a647dddb624a0a5e5b
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2017
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>将来のバージョンの Current Branch サイトとの拡張相互運用性のために構成マネージャー クライアント ソフトウェアを使用する

*適用対象: System Center Configuration Manager (Current Branch)、(Long-Term Servicing Branch)*  

場合によっては、会社のポリシーで、構成マネージャー クライアントを一部の PC で定期的に更新することが許可されていないことがあります。 たとえば、変更管理ポリシーに準拠する必要がある場合や、デバイスがミッション クリティカルな場合が挙げられます。

大半のクライアントについては、可能な場合、クライアントの自動更新を引き続き使用する必要がありますが、Configuration Manager の更新プログラム 1610 以降は、長期的な使用を目的とした新しいクライアントである拡張相互運用性クライアント (EIC) をインストールすることで、このようなニーズに対応できます。

EIC は、バージョン 1610 以降を実行する Configuration Manager サイトと互換性があります。 EIC は、キオスク デバイスや販売時点管理デバイスのように、頻繁に更新できない特定の PC にのみ使用します。 それ以外の PC にはすべて、最新の構成マネージャー クライアントを使用します。

## <a name="how-this-scenario-works"></a>このシナリオのしくみ

通常、Current Branch の新しいコンソール内更新プログラムをインストールすると、その新機能を使用できるように、クライアント ソフトウェアが自動的に更新されます。

このシナリオでは、Current Branch を使用し、新しい機能と更新プログラムを受信します。 ほとんどのクライアントは、Current Branch のクライアント ソフトウェアを実行しており、インストールする各バージョンの更新プログラムでそのクライアント ソフトウェアを更新できます。 ただし、クライアント ソフトウェアの更新プログラムを受信させたくない重要なシステムのサブセットには、拡張相互運用性クライアントをインストールします。 拡張相互運用性クライアントの場合、新しいバージョンのクライアント ソフトウェアを明示的に展開するまで、新しいクライアント ソフトウェアはインストールされません。

>[!IMPORTANT]
>Current Branch サイトはバージョン 1610 以降を実行する必要があります。

## <a name="how-to-use-the-eic"></a>EIC の使用方法

1. Configuration Manager の更新プログラム 1606 のインストール メディアに含まれる \SMSSETUP\Client フォルダーから、EIC (クライアント バージョン 5.00.8412) を取得します。 フォルダーの内容をすべてコピーするようにします。
2. デバイスに EIC を手動でインストールします。 [詳細については、クライアントを手動でインストールする方法に関するページをご覧ください](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)。
3. クライアントのアップグレードからこのコレクションを除外します。

>[!TIP]
>ボリューム ランセンス サービス センター (VLSC) で System Center Configuration Manager バージョン 1606 を見つけるには、[VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) の **[Downloads and Keys]\(ダウンロードとキー\)** タブに移動し、"system center config" を検索し、**[System Center Config Mgr (current branch and LTSB)]\(System Center Configuration Manager (現在のブランチと LTSB)\)** を選択します。

## <a name="the-extended-interoperability-client-software"></a>拡張相互運用性クライアント ソフトウェア

少なくとも 2018 年 11 月 18 日までは、Configuration Manager (Current Branch) の更新バージョンで現在の EIC が継続的にサポートされる予定です。 それ以降は、新しい EIC の詳細、または既存の EIC のサポート延長について、こちらのページをご確認ください。

>[!TIP]
>EIC は、リリース日から少なくとも 2 年間にわたりサポートされます (「[System Center Configuration Manager の Current Branch バージョンのサポート](/sccm/core/servers/manage/current-branch-versions-supported)」をご覧ください)。 たとえば現在の EIC は、1610 のリリースから 2 年間、つまり 2018 年 11 月 18 日までサポートされます。

クライアントのサポートが期限切れになる前に、Current Branch で管理するデバイスの拡張相互運用性クライアントを更新するように計画を立ててください。 更新するには、新しいバージョンのクライアントを Microsoft からダウンロードし、現在の拡張相互運用性クライアントを使用しているデバイスにその新しいクライアント ソフトウェアを展開します。

## <a name="limitations-of-the-extended-interoperability-client"></a>拡張相互運用性クライアントの制限

- 拡張相互運用性クライアント ソフトウェアの更新プログラムは、コンソール内更新プログラムを使用して入手できません。 新しいクライアント ソフトウェアを展開する方法の詳細については、新しいクライアントのリリース時に提供されます。
- EIC では、ソフトウェアの更新、インベントリ、およびパッケージとプログラムのみがサポートされます。

## <a name="next-steps"></a>次のステップ

[クライアントを監視する方法](/sccm/core/clients/manage/monitor-clients)に関するページの情報を使用して、クライアントがデバイスに適切にインストールされていることを確認します。
