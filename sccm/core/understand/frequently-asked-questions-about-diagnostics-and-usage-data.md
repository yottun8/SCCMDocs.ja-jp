---
title: "診断データに関する FAQ | System Center Configuration Manager"
description: "System Center Configuration Manager の診断および使用状況データに関してよく寄せられる質問を説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f5d0bf6215e827b58dcbc4a64c509c2f07b44815


---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>System Center Configuration Manager の診断および使用状況データに関してよく寄せられる質問

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の診断および使用状況データに関してよく寄せられる質問は次のとおりです。  

###  <a name="a-namebkmkoffa-how-do-i-turn-off-telemetry"></a><a name="bkmk_off"></a> テレメトリを無効にするには、どうすればよいですか。  
 Configuration Manager の現在のブランチは、Windows 10 と Microsoft Intune の新しいバージョンをサポートするために、定期的に更新する必要があります。 製品を最新の状態に保ち、更新プログラムのエクスペリエンスおよび製品の品質とセキュリティを向上させるために、Microsoft は少なくとも基本レベルの診断および使用状況データを必要としています。  

###  <a name="a-namebkmkretentiona-what-is-the-data-retention-period"></a><a name="bkmk_retention"></a> データの保存期間を教えてください。  
 診断結果と使用状況データは 1 年間は保持されます。  

###  <a name="a-namebkmkupdatea-is-diagnostics-and-usage-data-sent-when-installing-or-updating-the-product"></a><a name="bkmk_update"></a> 製品をインストールまたは更新するときに、診断と使用状況のデータは送信されますか。  
 いいえ。 診断および使用状況データは、サイトがインストールされて使用できる状態になったら送信されます。  

###  <a name="a-namebkmkfrequencya-how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a> データはどのくらいの頻度で送信されますか。  
 SQL ストアド プロシージャは (サイトがインストールされた日) から 7 日おきに実行されます。 オンライン モードでは、サービス接続ポイントはクエリの実行後にデータをアップロードするように構成されています。 オフライン モードでは、管理者はサービス接続ツールを使用してデータをアップロードします。 (注: サイトがインストールされてから 7 日間経過すると、初めてデータをオフラインで使用できるようにはなります。)  

###  <a name="a-namebkmknetworka-can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a> データを使用してネットワーク マップを作成できますか。  
 System Center Configuration Manager での診断の使用状況データ収集レベルについての説明のとおり、サイトの詳細には各サイトからのタイムゾーン情報が含まれます。 これにより、階層の複数のサイトの広範な位置情報とグローバル分散を理解できます。 ただし、IP アドレスや詳細な地理情報など、ネットワークの詳細情報は収集されません。
 - [1511 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [1602 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [1606 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)


###  <a name="a-namebkmktablesa-can-you-see-data-in-custom-tables"></a><a name="bkmk_tables"></a> カスタム テーブルのデータを確認できますか。  
 いいえ。 データベース内の既定の製品テーブルに対する診断および使用状況データは、SQL ストアド プロシージャによって収集されます (これらのすべてには接頭辞 **TEL_** が付いています)。 SQL スキーマ検出クエリの一部として、すべてのテーブル名は既知の既定値と比較するためにハッシュされます。 これにより、カスタム テーブルがデータベースに存在する (つまり、データベース スキーマが既定値から拡張された) けれども、それらのテーブル内にはデータが含まれていないことが分かります。  

###  <a name="a-namebkmkdatabasesa-can-you-see-names-of-other-databases-or-data-in-other-databases"></a><a name="bkmk_databases"></a> 他のデータベースの名前、またはその他のデータベース内のデータを確認できますか。  
 いいえ。 データを収集するストアド プロシージャは、サイト データベースに限定されます。  

## <a name="see-also"></a>関連項目  
 [System Center Configuration Manager の診断結果と使用状況データ](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)



<!--HONumber=Nov16_HO1-->


