---
title: サポート センターのクイックスタート
titleSuffix: Configuration Manager
description: トラブルシューティングのために、Configuration Manager クライアントの状態を迅速にキャプチャします。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5a9865a591f6947447ebb088b5e5e25db1e9fa54
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52458118"
---
# <a name="support-center-quickstart-guide"></a>サポート センターのクイックスタート ガイド

*適用対象: System Center Configuration Manager (Current Branch)*

サポート センターには、トラブルシューティングやリアルタイムのログ表示などの強力な機能が用意されています。 サポート センターを使用すると、Configuration Manager クライアント コンピューターの状態をわずか数分でキャプチャすることもできます。 この機能には、リモート クライアントへのアクセスが含まれます。

クライアントの状態をキャプチャする、完全な*トラブルシューティング バンドル* ファイル (.zip) を作成します。 バンドルに含めることができるのは、ログ ファイルだけではありません。 レジストリ設定やクライアント構成など、他の種類のデータを含めることができます。 サポート センター ビューアーを使用するサポート技術者にそのバンドルを渡します。



## <a name="prerequisites"></a>[前提条件]

- Configuration Manager クライアントに対するローカル管理者権限。  

- サポート センター インストーラー。 このファイルは `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` のサイト サーバー上にあります。 詳細については、[サポート センターの「インストール」](/sccm/core/support/support-center#install)を参照してください。  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>手順 1: ローカル クライアントで、データ バンドルを作成する

1.  Configuration Manager クライアントにサポート センターをインストールします。  

2.  **[スタート]** メニューに移動し、**[Microsoft System Center]** グループで **[サポート センター]** を選択します。  

3.  リボンの [ホーム] タブで、**[選択したデータを収集]** を選択します。 既定では、サポート センターは最小限のデータ セット (ログ ファイル、クライアント構成、およびオペレーティング システム) のみを収集します。  

4.  コンピューターのフォルダーにトラブルシューティング バンドル ファイル (.zip) を保存します。 既定では、ファイル名は次の例に似ています: `Support_c885cdfed3c7482bba4f9e662978ec07.zip`。  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>手順 2:サポート センター ビューアーを使用して、データ バンドルを確認する

1.  **サポート センター ビューアー**を起動します。 このアクションは、サポート センターをインストールしている任意のコンピューターで実行できます。  

2.  **[Open bundle]/(バンドルを開く/)** を選択し、バンドル ファイルを参照して、**[開く]** を選択します。  

3.  サポート センター ビューアーでファイルが処理されたら、利用可能な各タブに切り替えます。サポート センターが既定で収集するデータの種類を確認します。  

    - **構成**  

        - Configuration Manager クライアント構成  

        - オペレーティング システム  

        - コンピューター  

        - サービス  

        - ネットワーク アダプター  

    - **ログ**: リストで 1 つまたは複数のエントリを選択し、**[開く]** を選択します。 このアクションは、選択したログ ファイルをログ ビューアーで開きます。 この機能を使用して、エラー コードを検索します。高度なフィルターを使用すると、ログ ファイルをすばやく分析できます。  



## <a name="collect-more-data"></a>さらに多くのデータを収集する

サポート センターでは、これらの基本機能に加えその他のクライアントの状態を広範に収集できます。 **[サポート センター]** を開き、**[Collect All Data]/(すべてのデータを収集/)** を選択します。 このプロセスは、通常、最新のコンピューター上でも数分間かかります。 サポート センターは、次の追加のデータを収集します。

  - **ポリシー**: 要求されたポリシー構成および実際のポリシー構成の両方を含む、Configuration Manager のポリシー設定を収集します。  

  - **[Certificates]\(証明書\)**: クライアント証明書の公開キー情報。 サポート センターでは、証明書の秘密キーは収集されません。  

  - **[Client registry]\(クライアント レジストリ\)**: レジストリからクライアント構成情報を収集します。 サポート センターでは、Configuration Manager のレジストリ情報だけが収集されます。  

  - **[Client WMI]\(クライアント WMI\)**: WMI からのクライアント構成情報。 サポート センターでは、クライアント ポリシーは収集されません。  

  - **[トラブルシューティング]**: Active Directory、管理ポイント、ネットワーク、ポリシー割り当て、および登録に関する一般的なクライアントの問題の診断に役立つリアルタイムのトラブルシューティング データ。  

  - **[Debug dumps]\(デバッグ ダンプ\)**: クライアントおよび関連プロセスのデバッグ ダンプを実行します。 デバッグ ダンプは大きくなる可能性があります。 このオプションは、クライアントのパフォーマンスに関する問題をトラブルシューティングするときにのみ、有効にしてください。  

