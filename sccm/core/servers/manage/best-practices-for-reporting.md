---
title: "レポートのベスト プラクティス"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager のレポート機能の使用に関する役立つヒントをいくつか示します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: b66e4417658e8a5f25056ed37b5367d57ff72781
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2017
---
# <a name="best-practices-for-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager のレポートのベスト プラクティス

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のレポートに関する以下のベスト プラクティスを使用してください。  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>パフォーマンスを最大化するためにレポート サービス ポイントをリモート サイト システム サーバーにインストールする  
 レポート サービス ポイントはサイト サーバーかリモート サイト システムにインストールできますが、リモート サイト システム サーバーにインストールすることでパフォーマンスが向上します。  

## <a name="optimize-sql-server-reporting-services-queries"></a>SQL Server Reporting Services のクエリを最適化する  
 通常、レポートの遅延はクエリの実行と結果の取得にかかる時間に起因します。 Microsoft SQL Server を使用している場合は、クエリ アナライザーやプロファイラーなどのツールをクエリの最適化に役立てることができます。  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>レポートのサブスクリプションの処理を標準業務時間外に実行するようにスケジュールする  
 可能な場合は、レポートのサブスクリプション処理を通常の業務時間外に実行するようにスケジュールを設定し、Configuration Manager サイト データベース サーバーの CPU の処理負荷を最小化します。 これにより、予定外のレポート要求に対する可用性も向上されます。  

## <a name="next-steps"></a>次のステップ
[レポートの構成](configuring-reporting.md)
