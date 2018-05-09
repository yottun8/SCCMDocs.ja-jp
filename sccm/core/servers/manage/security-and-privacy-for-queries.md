---
title: クエリのセキュリティとプライバシー
titleSuffix: Configuration Manager
description: サイト データベースから情報のクエリを実行するときのセキュリティとプライバシーのベスト プラクティスを理解します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2d84385782df17d4019d6de65bcc7006aeab8b24
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>System Center Configuration Manager のクエリのセキュリティとプライバシー

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager でクエリを使用すると、指定した条件に基づいてサイト データベースの情報を取得できます。 Configuration Manager は、標準操作中にサイト データベース情報を収集します。 たとえば、探索またはインベントリで収集された情報を使用して、特定の条件に合うデバイスを識別するようにクエリを構成することができます。  

 クエリの詳細については、「[System Center Configuration Manager のクエリの概要](../../../core/servers/manage/introduction-to-queries.md)」を参照してください。 クエリを使用して取得できる情報を収集する Configuration Manager 操作に関するセキュリティのベスト プラクティスとプライバシー情報の詳細については、「[System Center Configuration Manager のセキュリティとプライバシー](../../../core/plan-design/security/security-and-privacy.md)」を参照してください。  

## <a name="security-best-practices-for-queries"></a>クエリについて推奨するセキュリティ運用方法  
 以下は、クエリについてのセキュリティのベスト プラクティスです。  

|セキュリティのベスト プラクティス|説明|  
|----------------------------|----------------------|  
|ネットワークの場所に保存されているクエリをエクスポートまたはインポートする場合は、場所とネットワーク チャネルをセキュリティで保護します。|ネットワーク フォルダーにアクセスできるユーザーを制限します。<br /><br /> ネットワークの場所とサイト サーバーの間で、サーバー メッセージ ブロック (SMB) 署名またはインターネット プロトコル セキュリティ (IPsec) を使用して、攻撃者によってインポートされる前のクエリ データが改ざんされるのを防止します。|  

## <a name="see-also"></a>関連項目  
 [System Center Configuration Manager のクエリのテクニカル リファレンス](../../../core/servers/manage/queries-technical-reference.md)
