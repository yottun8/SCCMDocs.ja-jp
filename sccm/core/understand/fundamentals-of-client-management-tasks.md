---
title: "クライアント管理の基礎 | System Center Configuration Manager"
description: "System Center Configuration Manager クライアントを管理するために実行できるタスクについて説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b746c051eee42bcea5c01ced359f568c5aae5fd8


---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>System Center Configuration Manager のクライアント管理タスクの基礎

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager クライアントをインストールした後は、いくつかのタスクを実行して、クライアントを管理できます。  Configuration Manager コンソールから開始するタスクや、クライアントの Windows コントロール パネルでクライアントの Configuration Manager アプリから開始または表示できるタスクがあります。  

## <a name="the-console"></a>コンソール  
 Configuration Manager コンソール内から、次のタスクを含むさまざまなクライアント管理タスクを実行できます。  

-   アプリケーション、ソフトウェア更新プログラム、メンテナンス スクリプト、およびオペレーティング システムの展開。 指定した日付と時刻までにこれらをインストールするように構成したり、ユーザーが要求したときにインストールできるようにしたり、アプリケーションをアンインストールするように構成したりできます。  

-   マルウェアおよびセキュリティの脅威からコンピューターを保護し、問題が検出されたときに通知を出力する。  

-   コンプライアンスに準拠しているかどうかを監視して修復するためのクライアントの構成設定の定義。  

-   ハードウェアおよびソフトウェアのインベントリ情報の収集。これには、Microsoft のライセンス情報の監視および調整が含まれます。  

-   リモート コントロールを使用してコンピューターをトラブルシューティングします。  

-   コンピューターの電力消費を管理および監視するための電源管理設定の実装。  

これらの操作をほぼリアルタイムで監視するには、Configuration Manager コンソールを使用して、アラートおよびステータス情報を表示します。 データおよび過去の傾向を取得するには、SQL Reporting Services の統合レポート機能を使用できます。  クライアントは、クライアントのステータスとしての詳細をサイトに送信します。  クライアント ステータス情報では、クライアントとクライアント アクティビティの正常性に関するデータが提供されます。これらのデータはコンソールで、または Configuration Manager の組み込みレポートを使用して表示できます。 このデータを使用すると、応答していないコンピューターを識別できます。また、問題が自動的に修復されることもあります。  

 クライアントの管理タスクに関する詳細については、「[System Center Configuration Manager でクライアントを管理する方法](../../core/clients/manage/manage-clients.md)」および「[System Center Configuration Manager で Linux および UNIX サーバーのクライアントを管理する方法](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md)」を参照してください。 レポートの使用の詳細については、   
「            [System Center Configuration Manager のレポートの概要](../../core/servers/manage/introduction-to-reporting.md)」を参照してください。  

## <a name="the-windows-control-panel-app"></a>Windows コントロール パネル アプリケーション  
 構成マネージャー クライアント ソフトウェアをインストールすると、コントロール パネルに **Configuration Manager** クライアント アプリケーションがインストールされます。 ソフトウェア センターとは異なり、このアプリケーションはエンドユーザーではなく、ヘルプ デスクを対象として設計されています。 一部の構成オプションにはローカルの管理アクセス許可が必要であり、ほとんどのオプションには Configuration Manager の機能についての技術的な知識が必要です。 このアプリケーションを使用すると、クライアントで次のタスクを実行できます。  

-   クライアントに関するプロパティ (ビルド番号、割り当てられているサイト、接続する管理ポイント、PKI 証明書または自己署名入り証明書のいずれを使用するかなど) の表示。  

-   最初にインストールされた後に、クライアントがクライアント ポリシーを正常にダウンロードしたこと、および Configuration Manager コンソールで構成したクライアント設定に従って、クライアント設定が想定したとおりに有効または無効になっていることの確認。  

-   クライアントのアクション (Configuration Manager コンソールで最近構成の変更が行われ、次のスケジュール時間まで待機せずに、クライアント ポリシーをダウンロードする場合など) の開始。  

-   Configuration Manager サイトへのクライアントの手動での割り当て、またはサイトを見つけることができるように DNS に発行する管理ポイントの DNS サフィックスの指定。  

-   一時的にファイルを格納するクライアント キャッシュの構成、およびソフトウェアをインストールするためにディスク容量が必要な場合のキャッシュ内のファイルの削除。  

-   インターネット ベースのクライアント管理のための設定の構成  

-   クライアントに展開されている構成基準の表示、コンプライアンスの評価の開始、およびコンプライアンス レポートの表示。  



<!--HONumber=Nov16_HO1-->


