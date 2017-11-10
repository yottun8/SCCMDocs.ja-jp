---
title: "ハイブリッド展開用にユーザー所有のデバイスを登録する"
titleSuffix: Configuration Manager
description: "Configuration Manager を使用してハイブリッド展開用にユーザー所有のデバイスを登録するさまざまな方法について説明します。"
ms.custom: na
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
caps.latest.revision: "13"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 9bc0e23680ff2c7a5099938e546e50e03f998f5e
ms.sourcegitcommit: 1132886e07d0c0a87dcc7eeef4577dd8d8840023
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/01/2017
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Configuration Manager を使用してハイブリッド展開用にユーザー所有のデバイスを登録する

*適用対象: System Center Configuration Manager (Current Branch)*

ユーザー所有のデバイスは、"bring your own devices"、略して "BYOD" と呼ばれるプロセスで登録を行うことで管理対象にすることができます。 これを行うには、ユーザーがポータル サイト アプリをインストールしてデバイス (iOS、macOS、Android) にサインインするか、職場または学校アカウントをデバイスに追加してドメイン (Windows) に参加します。 このプロセスによりデバイスが Intune に登録され、ユーザーが Intune で管理されるリソースにアクセスできるようになり、Intune が PIN の要求などの特定のデバイス設定を管理できるようになります。

デバイスを管理対象にするには、管理者として最初に[モバイル デバイス管理を設定](setup-hybrid-mdm.md)し、[登録を有効にします](enable-platform-enrollment.md)。 登録を有効にすると、ユーザーは自分のデバイスを登録できます。 ユーザーと共有する考慮事項と手順については、「[Microsoft Intune に関してエンド ユーザーを教育する方法](https://docs.microsoft.com/intune/end-user-educate)」を参照してください。

デバイスを購入する会社または学校は、[会社所有のデバイスの管理](enroll-company-owned-devices.md)を可能にするプログラムを利用できます。
