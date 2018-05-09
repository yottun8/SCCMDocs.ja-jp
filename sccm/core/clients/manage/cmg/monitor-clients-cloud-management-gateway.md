---
title: クラウド管理ゲートウェイを監視する
titleSuffix: Configuration Manager
description: クラウド管理ゲートウェイ (CMG) 経由でクライアントおよびネットワーク トラフィックを監視します。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a4ecbeb2484297160797b7b5632c86cee4ff1122
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Configuration Manager でクラウド管理ゲートウェイを監視する

*適用対象: System Center Configuration Manager (Current Branch)*

クラウド管理ゲートウェイを実行中で、そのゲートウェイ経由でクライアントが接続されている場合、クライアントおよびネットワーク トラフィックを監視して、サービスのパフォーマンスを把握することができます。



## <a name="monitor-clients"></a>クライアントの監視

クラウド管理ゲートウェイ経由で接続されているクライアントは、オンプレミス クライアントと同様に、Configuration Manager コンソールに表示されます。 詳細については、「[System Center Configuration Manager でクライアントを監視する方法](/sccm/core/clients/manage/monitor-clients)」を参照してください。



## <a name="monitor-traffic-in-the-console"></a>コンソールでトラフィックを監視する

Configuration Manager コンソールを使用して、クラウド管理ゲートウェイのトラフィックを監視する場合は、次の操作を行います。

1. **[管理] > [クラウド サービス] > [Cloud Management Gateway]** に移動します。

2. リスト ウィンドウでクラウド管理ゲートウェイを選択します。

3. 詳細ウィンドウで、クラウド管理ゲートウェイ接続ポイントと接続しているサイト システムの役割のトラフィック情報を確認します。



## <a name="set-up-outbound-traffic-alerts"></a>送信トラフィック アラートの設定

送信トラフィック アラートを使用すると、ネットワーク トラフィックが 14 日のしきい値レベルに達したときに知ることができます。 クラウド管理ゲートウェイを作成するときに、トラフィック アラートを設定できます。 この部分をスキップして、サービスの実行後にアラートを設定することもできます。 アラート設定はいつでも調整できます。

1. **[管理] > [クラウド サービス] > [Cloud Management Gateway]** に移動します。

2. リスト ウィンドウでクラウド管理ゲートウェイを右クリックし、**[プロパティ]** を選択します。

3. **[アラート]** タブをクリックします。しきい値とアラートを有効にします。 14 日のデータしきい値をギガバイト (GB) 単位で指定します。 また、別のアラート レベルを上げるためにしきい値の割合を指定します。

4. 完了したら、**[OK]** をクリックします。



## <a name="monitor-logs"></a>監視ログ

クラウド管理ゲートウェイは、複数のログ ファイルにエントリを生成します。 詳細については、「[System Center Configuration Manager のログ ファイル](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)」を参照してください。
