---
title: クラウド管理ゲートウェイを監視する
titleSuffix: Configuration Manager
description: クラウド管理ゲートウェイ (CMG) 経由でクライアントおよびネットワーク トラフィックを監視します。
ms.date: 09/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ef27c67b9b17f41fbe71d57fdea9552b7dff9f7
ms.sourcegitcommit: 2badee2b63ae63687795250e298f463474063100
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2018
ms.locfileid: "45601043"
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Configuration Manager でクラウド管理ゲートウェイを監視する

*適用対象: System Center Configuration Manager (Current Branch)*

クラウド管理ゲートウェイ (CMG) を実行中で、そのゲートウェイ経由でクライアントが接続されている場合、クライアントおよびネットワーク トラフィックを監視して、サービスのパフォーマンスを把握することができます。



## <a name="monitor-clients"></a>クライアントの監視

CMG 経由で接続されているクライアントは、オンプレミス クライアントと同様に、Configuration Manager コンソールに表示されます。 詳細については、「[System Center Configuration Manager でクライアントを監視する方法](/sccm/core/clients/manage/monitor-clients)」を参照してください。



## <a name="monitor-traffic-in-the-console"></a>コンソールでトラフィックを監視する

Configuration Manager コンソールを使用して、CMG のトラフィックを監視する場合は、次の操作を行います。

1. **[管理]** ワークスペースに移動し、**[Cloud Services]** を展開して **[クラウド管理ゲートウェイ]** ノードを選択します。  

2. リスト ウィンドウで CMG を選択します。  

3. 詳細ウィンドウで、CMG 接続ポイントと接続しているサイト システムの役割のトラフィック情報を確認します。  



## <a name="set-up-outbound-traffic-alerts"></a>送信トラフィック アラートの設定

送信トラフィック アラートを使用すると、ネットワーク トラフィックが 14 日のしきい値レベルに達したときに知ることができます。 CMG を作成するときに、トラフィック アラートを設定できます。 この部分をスキップして、サービスの実行後にアラートを設定することもできます。 アラート設定はいつでも調整できます。

1. **[管理]** ワークスペースに移動し、**[Cloud Services]** を展開して **[クラウド管理ゲートウェイ]** ノードを選択します。  

2. リスト ウィンドウで CMG を選択してから、リボンで **[プロパティ]** を選択します。  

3. **[アラート]** タブに移動して、しきい値とアラートを有効にします。 14 日のデータしきい値をギガバイト (GB) 単位で指定します。 また、別のアラート レベルを上げるためにしきい値の割合を指定します。  

4. 完了したら、**[OK]** を選択します。  



## <a name="monitor-logs"></a>監視ログ

CMG によって、多くのログ ファイルにエントリが生成されます。 詳細については、「[System Center Configuration Manager のログ ファイル](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)」を参照してください。



## <a name="cloud-management-dashboard"></a>クラウド管理ダッシュボード
<!--1358461--> バージョン 1806 以降では、クラウド管理ダッシュボードでは、CMG の使用量を一元化したビューが提供されます。 クラウド管理のためにサイトが [Azure サービス](/sccm/core/servers/deploy/configure/azure-services-wizard)にオンボードされている場合、クラウド ユーザーおよびデバイスに関するデータも表示されます。  

次のスクリーンショットは、利用可能な 2 つのタイルを表示したクラウド管理ダッシュ ボードの一部です。  
![クラウド管理ダッシュボード タイルの CMG トラフィックと現在のオンライン クライアント](media/1358461-cmg-dashboard.png)

Configuration Manager コンソールで、**[監視]** ワークスペースに移動します。 **[クラウド管理]** ノードを選択して、ダッシュボード タイルを表示します。  



## <a name="connection-analyzer"></a>接続アナライザー

バージョン 1806 以降では、トラブルシューティングを支援するリアルタイム検証のために CMG 接続アナライザーを使用します。 コンソール内ユーティリティは、サービスの状態と、CMG 接続ポイント経由で CMG トラフィックを許可する任意の管理ポイントへの通信チャネルをチェックします。

1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動します。 **[クラウド サービス]** を展開し、**[クラウド管理ゲートウェイ]** ノードを選択します。  

2. 対象となる CMG インスタンスを選択して、リボンにある **[接続アナライザー]** を選択します。  

3. [CMG connection analyzer]\(CMG 接続アナライザー\) ウィンドウで、サービスを認証するための次のいずれかのオプションを選択します。  

     1. **Azure AD のユーザー**: このオプションを使用して、Azure AD に参加している Windows 10 デバイスにサインイン済みのクラウド ベースのユーザー ID と同じ通信をシミュレートします。 **[サインイン]** をクリックして、この Azure AD ユーザー アカウントのための資格情報を安全に入力します。  

     2. **クライアント証明書**: このオプションを使用して、[クライアント認証証明書](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate)を使用した Configuration Manager クライアントと同じ通信をシミュレートします。  

4. **[開始]** を選択して、分析を開始します。 アナライザー ウィンドウに結果が表示されます。 エントリを選択すると、[説明] フィールドにさらに詳しい詳細が表示されます。  

