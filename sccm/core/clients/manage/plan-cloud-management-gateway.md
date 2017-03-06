---
title: "クラウド管理ゲートウェイの計画 | Microsoft Docs"
description: 
ms.date: 12/19/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1df2d8bcd73633ac1d37cc3ef31343be9c5bc95d
ms.openlocfilehash: 6e2895565e868eb80a8f4f4b46b8a28eb4961e28
ms.lasthandoff: 12/19/2016

---

# <a name="plan-for-cloud-management-gateway-in-configuration-manager"></a>Configuration Manager でクラウド管理ゲートウェイを計画する

*適用対象: System Center Configuration Manager (Current Branch)*

バージョン 1610 より、クラウド管理ゲートウェイは、インターネット上で Configuration Manager クライアントを管理する簡単な方法を提供します。 クラウド管理ゲートウェイ サービスは、Microsoft Azure に展開され、Azure サブスクリプションを必要とします。 このサービスは、クラウド管理ゲートウェイ コネクタ ポイントと呼ばれる新しいロールを使って、オンプレミスの Configuration Manager インフラストラクチャに接続します。 デプロイされて構成されると、クライアントは、内部のプライベート ネットワーク上にいるかどうか、またはインターネット上にあるかどうかに関係なく、オンプレミスの Configuration Manager サイト システムの役割にアクセスできるようになります。

Configuration Manager コンソールを使って、Azure にサービスを展開し、クラウド管理ゲートウェイ コネクタ ポイントの役割を追加して、クラウド管理ゲートウェイ トラフィックを許可するサイト システムの役割を構成します。 クラウド管理ゲートウェイは現在、管理ポイントとソフトウェアの更新ポイントの役割のみをサポートしています。

コンピューターを認証し、異なる層のサービス間の通信を暗号化するには、クライアント証明書および Secure Socket Layer (SSL) 証明書が必要です。 クライアント コンピューターは通常、グループ ポリシーの適用を介してクライアント証明書を受け取ります。 クライアントと役割をホストしているサイト システム サーバー間のトラフィックを暗号化するには、CA からカスタム SSL 証明書を作成する必要があります。 クラウド管理ゲートウェイ サービスの展開を Configuration Manager に許可する管理証明書を Azure で設定する必要もあります。

## <a name="requirements-for-cloud-management-gateway"></a>クラウド管理ゲートウェイの要件

-   クライアント コンピューターとクラウド管理ゲートウェイ コネクタ ポイントを実行するサイト システム サーバー

-   クライアント コンピューターからの通信を暗号化し、クラウド管理ゲートウェイ サービスの ID を認証するために使用される内部 CA からのカスタムの SSL 証明書

-   クラウド サービスの Azure サブスクリプション

-   Azure での Configuration Manager の認証に使用される Azure 管理証明書

## <a name="specifications-for-cloud-management-gateway"></a>クラウド管理ゲートウェイの仕様

- クラウド管理ゲートウェイの各インスタンスは、4,000 クライアントをサポートします。
- 可用性を高めるため、クラウド管理ゲートウェイのインスタンスを少なくとも&2; つ作成することをお勧めします。
- クラウド管理ゲートウェイは、管理ポイントとソフトウェアの更新ポイントの役割のみをサポートしています。
-   クラウド管理ゲートウェイに関しては、Configuration Manager の次の機能が現在のところサポートされていません。

    -   クライアント プッシュによるクライアントの展開とアップグレード
    -   サイトの自動割り当て
    -   ユーザー ポリシー
    -   アプリケーション カタログ (ソフトウェア承認要求を含む)
    -   完全なオペレーティング システム展開 (OSD)
    -   Configuration Manager コンソール
    -   ［リモート ツール］
    -   Web サイトのレポート
    -   Wake On LAN
    -   Mac、Linux、UNIX クライアント
    -   Azure Resource Manager
    -   ピア キャッシュ
    -   オンプレミス モバイル デバイス管理

## <a name="cost-of-cloud-management-gateway"></a>クラウド管理ゲートウェイのコスト

>[!IMPORTANT]
>以下のコスト情報は、見積もり目的のみで提供されます。 ご利用の環境によっては、変動要素が他にも存在し、それがクラウド管理ゲートウェイの総コストに影響を与えることがあります。

クラウド管理ゲートウェイでは、次の Microsoft Azure の機能が使用され、その料金が Azure サブスクリプション アカウントに請求されます。

-   バーチャル マシン

    -   現在のところ、クラウド管理ゲートウェイには Standard\_A2 バーチャル マシンが必要になります。 サービスを作成するとき、サービスをサポートする VM の数を選択できます (既定は&1; です)。

    -   1 台の Azure Standard\_A2 バーチャル マシンでインターネット ベースのクライアントを約 2,000 台同時にサポートできると予想されます (この数値は見積もり目的でのみ提供されます)。

    -   予想されるコストについては、「[Azure の料金計算ツール](https://azure.microsoft.com/en-us/pricing/calculator/)」を参照してください。

      >[!NOTE]
      >バーチャル マシンのコストは地域によって異なります。

-   送信データの転送

    -   サービスから送信されるデータに対して料金が発生します。 予想されるコストについては、「[Azure 帯域幅の料金詳細](https://azure.microsoft.com/en-us/pricing/details/bandwidth/)」を参照してください。

    -   インターネット ベースのクライアントが 1 時間ごとにポリシーを更新する場合、クライアントあたり毎月約 100 MB が予想されます (この数値は見積もり目的でのみ提供されます)。

    >[!NOTE]
    > クラウド管理ゲートウェイでサポートされている他のアクションを実行すると (ソフトウェアの更新プログラムやアプリケーションの展開など)、Azure から送信されるデータが増えます。

-   コンテンツ ストレージ

    -   クラウド管理ゲートウェイで管理されるインターネット ベースのクライアントは、Windows Update から無料でソフトウェア更新プログラム コンテンツを受信します。

    -   その他の必要なコンテンツ (アプリケーションなど) は、クラウド ベースの配布ポイントに配布する必要があります。 現在のところ、クラウド管理ゲートウェイでは、コンテンツをクライアントに送信するときにのみ、クラウド配布ポイントがサポートされます。

    - 詳細については、「[クラウドベースの配布にかかるコスト](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution)」を参照してください。

## <a name="next-steps"></a>次のステップ

[Set up cloud management gateway](setup-cloud-management-gateway.md) (クラウド管理ゲートウェイの設定)

