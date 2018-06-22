---
title: レポートのベスト プラクティス
titleSuffix: Configuration Manager
description: System Center Configuration Manager のレポート機能の使用に関する役立つヒントをいくつか示します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 87ed3a0591107695a1f418b38f2e3f5cb9168c63
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337593"
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
