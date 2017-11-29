---
title: "Windows Defender Application Guard ポリシーの作成と展開"
titleSuffix: Configuration Manager
description: "Windows Defender Application Guard ポリシーを作成して展開します。"
ms.custom: na
ms.date: 11/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 
caps.latest.revision: "5"
author: ErikjeMS
ms.author: erikje
manager: angrobe
ms.openlocfilehash: db2508e5bbd1435fce432b6ef98d7968e68ea5ab
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-deploy-windows-defender-application-guard-policy----1351960---"></a>Windows Defender Application Guard ポリシーの作成と展開 <!-- 1351960 -->

Configuration Manager Endpoint Protection を使用して [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) ポリシーを作成して展開できます。 これらのポリシーを使用すると、信頼できない Web サイトをオペレーティング システムの他の部分からはアクセスできない安全な分離コンテナーで開くことでユーザーを保護できます。

## <a name="prerequisites"></a>必要条件

Windows Defender Application Guard ポリシーを作成して展開するには、Windows 10 Fall Creator の更新プログラムを使用する必要があります。 また、ネットワーク分離ポリシーを使用して、ポリシーを展開する Windows 10 デバイスを構成する必要があります。 詳細については、「[Windows Defender Application Guard の概要](https://docs.microsoft.com/en-us/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview)」を参照してください。 この機能は、最新の Windows 10 Insider Build でのみ動作します。 これをテストするには、クライアントが最新の Windows 10 Insider Build で実行されている必要があります。


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>ポリシーを作成します。使用可能な設定を参照するには、次の手順を実行します。

1. Configuration Manager コンソールで、**[資産とコンプライアンス]** を選択します。
2. **[資産とコンプライアンス]** ワークスペースで、**[概要]** > **[Endpoint Protection]** > **[Windows Defender Application Guard]** の順に選択します。
3. **[ホーム]** タブの **[作成]** グループで、**[Windows Defender Application Guard ポリシーの作成]** をクリックします。
4. [ブログ記事](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)を参照として使用して、使用可能な設定を参照および構成することができます。
5. **[ネットワーク定義]** ページでは、企業の ID を指定し、企業ネットワークの境界を定義します。

    > [!NOTE]
    > Windows 10 PC の場合、クライアントでネットワーク分離リストが 1 つだけ保存されます。 2 種類のネットワーク分離リストを作成し、次のクライアントに展開することができます。
    >
    >  - Windows 情報保護から 1 つ
    >  - Windows Defender Application Guard から 1 つ
    >
    > 両方のポリシーを展開する場合、ネットワーク分離リストが一致している必要があります。 一致しないリストを同じクライアントに展開すると失敗します。 詳細については、[Windows 情報保護のドキュメント](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm)を参照してください。
    > 
    > 

6. 完了したら、ウィザードを終了し、1 つ以上の Windows 10 デバイスにポリシーを展開します。

## <a name="next-steps"></a>次のステップ
Windows Defender Application Guard の詳細については、[このブログ記事](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)を参照してください。 また、Windows Defender Application Guard のスタンドアロン モードの詳細については、[このブログ記事](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)を参照してください。
