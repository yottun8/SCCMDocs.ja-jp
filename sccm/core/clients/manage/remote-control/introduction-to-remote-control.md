---
title: リモート コントロール
titleSuffix: Configuration Manager
description: System Center Configuration Manager のリモート コントロールの概要
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 29350919-6a25-446b-a0da-05e8914fbb26
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a6f6ea0d68a8ba8d2db20bd8a77d5e480314150
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32331966"
---
# <a name="introduction-to-remote-control-in-system-center-configuration-manager"></a>System Center Configuration Manager のリモート コントロールの概要

*適用対象: System Center Configuration Manager (Current Branch)*

リモート コントロールを使用して、リモートでの管理、支援の提供、階層内の任意のコンピューターの表示ができます。 リモート コントロールを使用することで、クライアント コンピューターのハードウェアやソフトウェアの構成に関する問題のトラブルシューティングを行ったり、サポートを提供したりできます。 Configuration Manager では、Configuration Manager クライアントでサポートされるオペレーティング システムを実行する、すべてのワークグループ コンピューターとドメインに参加しているコンピューターのリモート コントロールをサポートします。 詳細については、「[System Center Configuration Manager のクライアントとデバイスのサポートされるオペレーティング システム](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)」をご覧ください。

また、Configuration Manager によって、Configuration Manager コンソールから Windows リモート デスクトップとリモート アシスタンスを実行して、クライアント設定を構成することができます。  

> [!NOTE]  
>  Configuration Manager コンソールからワークグループに属するクライアント コンピューターにリモート アシスタンス セッションを確立することはできません。 

 Configuration Manager コンソールでのリモート コントロール セッションは、**[資産とコンプライアンス]** > **[デバイス]**、任意のデバイス コレクション、Windows コマンド プロンプト ウィンドウ、または Windows の **[スタート]** メニューから開始できます。  
