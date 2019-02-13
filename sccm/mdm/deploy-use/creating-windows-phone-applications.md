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
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24ce7609a2e3e3ec9cfd9363ebd58cba3ec4dadd
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120667"
---
# <a name="create-windows-phone-applications-in-configuration-manager"></a>Configuration Manager で Windows Phone アプリケーションを作成する

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

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
