---
title: 診断および使用状況データに関するよくあるご質問
titleSuffix: Configuration Manager
description: System Center Configuration Manager の診断および使用状況データに関してよく寄せられる質問を説明します。
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38b59e520baf9fddb09f71f459de409f38adad2b
ms.sourcegitcommit: 32a257fafbb29aece8b4f435dd5614fcef305328
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2019
ms.locfileid: "54005451"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>System Center Configuration Manager の診断および使用状況データに関してよく寄せられる質問

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、Configuration Manager の診断および使用状況データに関してよく寄せられる質問の回答を示します。

## <a name="faqs"></a>よく寄せられる質問

###  <a name="bkmk_off"></a> テレメトリを無効にするには、どうすればよいですか。  
テレメトリは無効にできません。 ただし、収集されるテレメトリ データのレベルを選択することはできます。 テレメトリ データが送信されるタイミングを管理するには、サービス接続ポイントをオフライン モードで使用します。

Configuration Manager の現在のブランチは、Windows 10 と Microsoft Intune の新しいバージョンをサポートするために、定期的に更新する必要があります。 Microsoft では、少なくとも基本レベルの診断および使用状況データを必要としています。 このデータは、製品を最新の状態に保ち、更新プログラムのエクスペリエンスおよび製品の品質とセキュリティを向上させるために使用されます。

###  <a name="bkmk_retention"></a> データの保存期間を教えてください。  
 診断と使用状況データは 1 年間は保存されます。  

###  <a name="bkmk_update"></a> 製品をインストールまたは更新するときに、診断と使用状況のデータは送信されますか。  
 いいえ。 診断および使用状況データは、サイトがインストールされて使用できる状態になったら送信されます。  

###  <a name="bkmk_frequency"></a> データはどのくらいの頻度で送信されますか。  
 SQL ストアド プロシージャは (サイトがインストールされた日) から 7 日おきに実行されます。 オンライン モードでは、サービス接続ポイントはクエリの実行後にデータをアップロードするように構成されています。 オフライン モードでは、管理者はサービス接続ツールを使用してデータをアップロードします。 (サイトがインストールされてから 7 日間経過すると、初めてデータをオフラインで使用できるようにはなります。)  

###  <a name="bkmk_network"></a> データを使用してネットワーク マップを作成できますか。  
 診断と使用状況データのレベルの説明のとおり、サイトの詳細には各サイトからのタイム ゾーン情報が含まれます。 この情報により、階層の複数のサイトの広範な位置情報とグローバル分散を理解できます。 このデータには、IP アドレスや詳細な地理情報など、ネットワークの詳細情報は含まれません。 詳細については、[診断結果と使用状況データの記事](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data#articles)一覧を参照し、使用しているバージョンの診断結果と使用状況データの収集レベルを検索します。


###  <a name="bkmk_tables"></a> カスタム テーブルのデータを確認できますか。  
 いいえ。 Configuration Manager では、SQL ストアド プロシージャを使用して、診断と使用状況データを収集します。 このストアド プロシージャは、データベースの既定の製品テーブルに対して実行されます。 これらすべての SQL テーブルには、**TEL_** の接頭語が付きます。 SQL スキーマ検出クエリの一部として、すべてのテーブル名は既知の既定値と比較するためにハッシュされます。 この動作により、データベースにカスタム テーブルが存在することが決定されます。 カスタム テーブルが存在するということは、データベース スキーマが既定から拡張されていることを知らせます。 それには、それらのテーブルに格納されるデータは含まれていません。  

###  <a name="bkmk_databases"></a> 他のデータベースの名前や、他のデータベース内のデータを確認できますか。 
 いいえ。 データを収集するストアド プロシージャは、サイト データベースに限定されます。  

### <a name="bkmk_gdpr"></a> Configuration Manager は、一般データ保護規則 (GDPR) の対象ですか?
 いいえ。 Configuration Manager は、GDPR の監視対象ではありません。 ユーザーが直接展開、管理、操作する、オンプレミスの製品です。 Microsoft が収集する診断結果と使用状況データにより、今後のリリースのインストールのエクスペリエンス、品質、セキュリティが向上します。 この診断と使用状況データは、GDPR の監視対象です。 ただし、エンド ユーザー識別情報 (EUII) やエンドユーザー疑似識別子 (EUPI) が収集されたり、Microsoft に送信されたりすることはありません。 GDPR の詳細については、[Microsoft の GDPR セキュリティ センター](https://microsoft.com/gdpr)を参照してください。 Configuration Manager のデータの詳細については、「[診断結果と使用状況データ](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)」を参照してください。


## <a name="see-also"></a>関連項目  
 [診断結果と使用状況データ](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)
