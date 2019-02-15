---
title: Windows Defender Application Guard ポリシーの作成と展開
titleSuffix: Configuration Manager
description: Windows Defender Application Guard ポリシーを作成して展開します。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6446fed2d48fc6428bdc3fbc7a24f728c206dc7
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132423"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Windows Defender Application Guard ポリシーの作成と展開 
*適用対象: System Center Configuration Manager (Current Branch)* 
 <!-- 1351960 -->作成して展開[Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) Configuration Manager のエンドポイントを使用してポリシー保護します。 これらのポリシーを使用すると、信頼できない Web サイトをオペレーティング システムの他の部分からはアクセスできない安全な分離コンテナーで開くことでユーザーを保護できます。

## <a name="prerequisites"></a>[前提条件]

Windows Defender Application Guard ポリシーを作成して展開するには、Windows 10 Fall Creator (1709) の更新プログラムを使用する必要があります。 また、ネットワーク分離ポリシーを使用して、ポリシーを展開する Windows 10 デバイスを構成する必要があります。 詳細については、「[Windows Defender Application Guard の概要](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview)」を参照してください。 


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>ポリシーを作成します。使用可能な設定を参照するには、次の手順を実行します。

1. Configuration Manager コンソールで、**[資産とコンプライアンス]** を選択します。
2. **[資産とコンプライアンス]** ワークスペースで、**[概要]** > **[Endpoint Protection]** > **[Windows Defender Application Guard]** の順に選択します。
3. **[ホーム]** タブの **[作成]** グループで、**[Windows Defender Application Guard ポリシーの作成]** をクリックします。
4. [記事](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard)を参照として使用して、使用可能な設定を参照および構成することができます。 Configuration Manager では、特定のポリシー設定を設定することができます。[ホスト対話の設定](#BKMK_HIS)と[アプリケーションの動作](#BKMK_AppB)を参照してください。
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

6. 完了したら、ウィザードを終了し、1 つ以上の Windows 10 1709 デバイスにポリシーを展開します。

### <a name="bkmk_HIS"></a> ホスト対話の設定
ホスト デバイスと Application Guard コンテナー間の対話を構成します。 Configuration Manager バージョン 1802 より前のバージョンでは、アプリケーションの動作とホスト対話はどちらも **[設定]** タブにあります。

- **クリップボード** - Configuration Manager 1802 より前のバージョンでは [設定] の下
    - 許可されているコンテンツの種類
        - テキスト
        - イメージ
- **印刷:**
    - XPS への印刷を有効にする
    - PDF への印刷を有効にする
    - ローカル プリンターへの印刷を有効にする
    - ネットワーク プリンターへの印刷を有効にする
- **グラフィックス:** (Configuration Manager バージョン 1802 以降)
    - 仮想グラフィックス プロセッサ アクセス
- **ファイル:** (Configuration Manager バージョン 1802 以降)
    - ダウンロードしたファイルをホストに保存する

### <a name="bkmk_ABS"></a> アプリケーションの動作の設定
Application Guard セッション内でアプリケーションの動作を構成します。 Configuration Manager バージョン 1802 より前のバージョンでは、アプリケーションの動作とホスト対話はどちらも **[設定]** タブにあります。

- **コンテンツ:**
   - エンタープライズ サイトはサード パーティ プラグインなどのエンタープライズ以外のコンテンツを読み込める
- **その他:**
    - ユーザーが生成したブラウザー データを保持する
    - 分離された Application Guard セッションでの監査セキュリティ イベント



## <a name="next-steps"></a>次のステップ
Windows Defender Application Guard の詳細を確認する: [Windows Defender Application Guard の概要](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview)。
[Windows Defender Application Guard の FAQ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard)。
