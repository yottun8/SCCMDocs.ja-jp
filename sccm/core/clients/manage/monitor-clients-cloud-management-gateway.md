---
title: "クライアントを監視する | クラウド監視ゲートウェイ | Microsoft Docs"
description: 
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 2753efaca58447417cf0671645e737d052f0849b

---

# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Configuration Manager でクラウド管理ゲートウェイを監視する

*適用対象: System Center Configuration Manager (Current Branch)*

バージョン 1610 以降、クラウド管理ゲートウェイ サービスを実行中で、そのサービス経由でクライアントが接続していると、クライアントとネットワーク トラフィックを監視し、サービスのパフォーマンスを把握できるようになりました。

## <a name="monitor-clients"></a>クライアントの監視

クラウド管理ゲートウェイ サービス経由で接続されているクライアントは、オンプレミス クライアントと同様に、Configuration Manager コンソールに表示されます。 詳細については、「[System Center Configuration Manager でクライアントを監視する方法](monitor-clients.md)」を参照してください。

## <a name="monitor-traffic-in-the-console"></a>コンソールでトラフィックを監視する

Configuration Manager コンソールを使用して、クラウド管理ゲートウェイのトラフィックを監視できます。

1. **[管理] > [クラウド サービス] > [Cloud Management Gateway]** に移動します。

2. 一覧ウィンドウにあるクラウド管理ゲートウェイ サービスを選択します。

3. 詳細ウィンドウで、接続しているクラウド管理ゲートウェイ接続の役割とサイト システムの役割のトラフィック情報を確認します。

## <a name="set-up-outbound-traffic-alerts"></a>送信トラフィック アラートの設定

送信トラフィック アラートを使用すると、トラフィックが 14 日 (2 週間) のしきい値レベルに達したときに知ることができます。 クラウド管理ゲートウェイ サービスを作成するときに、トラフィック アラートを設定するオプションが表示されます。 この部分をスキップして、サービスの実行後にアラートを設定することもできます。 また、いつでもアラート設定を調整できます。

1. **[管理] > [クラウド サービス] > [Cloud Management Gateway]** に移動します。

2. 一覧ウィンドウのクラウド管理ゲートウェイ サービスを右クリックし、**[プロパティ]** を選択します。

3. [アラート] タブをクリックし、しきい値とアラートを有効 (または無効) にすることができます。 次に 14 日のしきい値 (GB 単位) と、異なるアラート レベルを上げるためのしきい値の割合を指定します。

4. 完了したら、**[OK]** をクリックします。

## <a name="monitor-logs"></a>監視ログ

クラウド管理ゲートウェイ サービスは、次のログ ファイルにエントリを生成します。

-   **Cloudmgr.log** – クラウド管理ゲートウェイ サービスの展開、進行中のサービスの状態、およびサービスに関連する使用状況データについてのエントリが含まれます。

-   **SMS\_Cloud\_ProxyConnector.log** – クラウド管理ゲートウェイ サービスとクラウド管理ゲートウェイ接続ポイントの間の接続の設定に関する詳細が含まれます。

詳細については、「[System Center Configuration Manager のログ ファイル](/sccm/core/plan-design/hierarchy/log-files)」を参照してください。



<!--HONumber=Dec16_HO3-->

