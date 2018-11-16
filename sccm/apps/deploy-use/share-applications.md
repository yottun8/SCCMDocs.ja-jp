---
title: ソフトウェア センターのアプリケーションを共有する
titleSuffix: Configuration Manager
description: System Center Configuration Manager でソフトウェア センターのアプリケーションのリンクを共有します。
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 309a369358789e1948ab7b17ddb0e3619ae1b129
ms.sourcegitcommit: 2504617dc4db90e205327d06cab32f050e88dbf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2018
ms.locfileid: "51505161"
---
# <a name="share-an-application-from-software-center"></a>ソフトウェア センターからのアプリケーションの共有

*適用対象: System Center Configuration Manager (Current Branch)* <!-- 1706 -->

アプリケーションの詳細ビューで、![[共有]](media/share15.png) **[共有]** ボタンを使用して、ソフトウェア センターのアプリケーションのハイパーリンクをコピーすることができます。 共有できるのはアプリケーションのハイパーリンクのみです。 アプリケーションが使用できなくなった場合は、ハイパーリンクによって、アプリケーションの利用不可メッセージを含むウィンドウが開きます。

1. **[アプリケーション]** を選択し、アプリケーションを選択します。
2. ![[共有]](media/share15.png) **[共有]** ボタンをクリックします。
3. ウィンドウ内の **[コピー]** をクリックします。
4. メールに URL を貼り付けて、アプリケーションを共有します。  

> [!TIP]  
>  Outlook 電子メールでリンクを作成するには、**Ctrl** + **K** キーを押して、URL を貼り付けます。  
>  
> 既定では、受信者がリンクをクリックすると、ソフトウェア センターのプロトコルに関するセキュリティ アラートが Outlook に表示されます。 お使いの環境でこれを防ぐには、信頼されているプロトコル キーをレジストリに追加します。 たとえば、`HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:` などです。  
