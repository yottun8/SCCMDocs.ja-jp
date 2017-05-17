---
title: "拡張相互運用性クライアントを Current Branch で使用する | Microsoft Docs"
description: "Configuration Manager サイトで、Configuration Manager の Long-Term Servicing Branch のクライアントを使用する方法について説明します。"
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: 0
author: robstackmsft
ms.author: robstack
Robots: NOINDEX,NOFOLLOW
ms.translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 30d0177dc7fcc7f39d00c48067130d587435bf2d
ms.contentlocale: ja-jp
ms.lasthandoff: 12/16/2016

---
# <a name="use-the-client-software-from-the-version-1606-baseline-media-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>将来的なバージョンの Current Branch サイトとの拡張相互運用性のためにバージョン 1606 基準メディアのクライアント ソフトウェアを使用する

*適用対象: System Center Configuration Manager (Current Branch)、(Long-Term Servicing Branch)*  

System Center 2016 に付属するバージョン 1606 基準メディアの DVD、または System Center Configuration Manager (Current Branch および Long-Term Servicing Branch 1606) に含まれる Windows コンピューター用 Configuration Manager クライアント ソフトウェア (client.msi) を使用して、Current Branch サイトに属するデバイスを管理できます。 このクライアントは、拡張相互運用性クライアントと呼ばれます。

## <a name="how-this-scenario-works"></a>このシナリオのしくみは次のとおりです。
通常、Current Branch の新しいコンソール内更新プログラムをインストールすると、その新機能を使用できるように、クライアント ソフトウェアが自動的に更新されます。

このシナリオでは、Current Branch を使用し、新しい機能と更新プログラムを受信します。 ほとんどのクライアントは、Current Branch のクライアント ソフトウェアを実行しており、インストールする各バージョンの更新プログラムでそのクライアント ソフトウェアを更新できます。 ただし、クライアント ソフトウェアの更新プログラムを受信させたくない重要なシステムのサブセットには、拡張相互運用性クライアントをインストールします。 拡張相互運用性クライアントの場合、新しいバージョンのクライアント ソフトウェアを明示的に展開するまで、新しいクライアント ソフトウェアはインストールされません。

新しいバージョンの Configuration Manager をインストールするときに Current Branch クライアントが自動的に更新されないようにする方法の詳細については、Current Branch 1610 で利用できるようになる予定です。

Current Branch サイトはバージョン 1606 以降を実行する必要があります。

## <a name="the-extended-interoperability-client-software"></a>拡張相互運用性クライアント ソフトウェア
Current Branch サイトで System Center 2016 または System Center Configuration Manager (Current Branch および Long-Term Servicing Branch 1606) リリースの拡張相互運用性クライアントを使用する場合、2016 年 10 月 12 日リリースの一般公開から 2 年間サポートされます。

クライアントのサポートが期限切れになる前に、Current Branch で管理するデバイスの拡張相互運用性クライアントを更新するように計画を立ててください。 更新するには、新しいバージョンのクライアントを Microsoft からダウンロードし、現在の拡張相互運用性クライアントを使用しているデバイスにその新しいクライアント ソフトウェアを展開します。

**拡張相互運用性クライアントの制限:**
-     拡張相互運用性クライアント ソフトウェアの更新プログラムは、コンソール内更新プログラムを使用して入手できません。 新しいクライアント ソフトウェアを展開する方法の詳細については、新しいクライアントのリリース時に提供される予定です。

## <a name="identify-the-client-version-you-use"></a>使用しているクライアント バージョンを確認する
Current Branch と LTSB の両方のクライアントについて、メジャー バージョンを次に示します。

|クライアント バージョン|Branch およびバージョン |  
|----------------|---------------------|
|5.00.8325.xxxx |    - Current Branch 1511|
|5.00.8355.xxxx    |- Current Branch 1602|
|5.00.8412.1307    |- Current Branch 1606 </br> - 1606 修正プログラム ロールアップ (KB3186654) が適用された Current Branch 1606</br>- バージョン 1606 基準メディアの拡張相互運用性クライアント|  

クライアントのバージョンは、Configuration Manager コントロール パネル アプレットの **[全般]** タブで確認できます。

アプレットの **[コンポーネント]** タブで、一部のコンポーネントには異なる値が表示されます。 たとえば、クライアント バージョン 8412.1307 の場合、一部のコンポーネントは 5.00.8412.**1000** または 5.00.8412.**1006** のように表示されることがあります。  一部のコンポーネントに見られる末尾 4 桁の違いは正常であり、コンポーネントが最新のクライアント バージョンに更新できないエラーを示すものではありません。

