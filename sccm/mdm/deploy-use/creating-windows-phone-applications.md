---
title: Windows Phone アプリケーションを作成する
titleSuffix: Configuration Manager
description: Configuration Manager で Windows Phone デバイス用アプリケーションを作成して展開する方法。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 77eb0b750934641ceb66b2c8aa611544c654f54f
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385441"
---
# <a name="create-windows-phone-applications-in-configuration-manager"></a>Configuration Manager で Windows Phone アプリケーションを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager アプリケーションには、1 つ以上の展開の種類があります。 展開の種類には、インストール ファイルとデバイスにソフトウェアを展開するために必要な情報が含まれています。 また、展開の種類には、ソフトウェアを展開するタイミングと方法を指定する規則があります。  

Configuration Manager アプリケーションと展開の種類を作成する手順については、[アプリケーションの作成](/sccm/apps/deploy-use/create-applications#bkmk_create)に関するページを参照してください。 

Windows Phone デバイス用アプリケーションを作成して展開するときは、以下の考慮事項について留意してください。  


Configuration Manager では、次のアプリ ファイルの種類の展開がサポートされています。  

|デバイスの種類|サポートされているファイルの種類|  
|-----------------|---------------------|  
|Windows Phone 8|xap|  
|Windows Phone 8.1|xap、appx、appxbundle|
|Windows 10 Mobile|xap、appx、appxbundle|

Windows Phone アプリを**利用可能**または**必須**として展開します。 アプリのアンインストールにも展開を使用します。  
