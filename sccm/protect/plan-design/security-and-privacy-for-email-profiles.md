---
title: 電子メール プロファイルのセキュリティとプライバシー
titleSuffix: Configuration Manager
description: System Center Configuration Manager でデバイスの電子メール プロファイルを管理する場合のセキュリティのベスト プラクティスについて説明します。
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 601e3a8d-e9e7-456f-a844-f19c3dae12a9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: b0386f507ef131a38438fd0d76bfdc223a841245
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140764"
---
# <a name="security-and-privacy-for-email-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager の電子メール プロファイルのセキュリティとプライバシー

*適用対象: System Center Configuration Manager (Current Branch)*

## <a name="security-best-practices-for-email-profiles"></a>電子メール プロファイルのセキュリティ上のベスト プラクティス  
 デバイスの電子メール プロファイルを管理するときには、次のセキュリティのベスト プラクティスに従ってください。  

|セキュリティのベスト プラクティス|説明|  
|----------------------------|----------------------|  
|可能な限り、使用する電子メール インフラストラクチャとクライアント オペレーティング システムでサポートできる、最も安全なオプションを選択します。|電子メール プロファイルは、デバイスで既にサポートしている電子メール設定を中央から配付して管理するのに便利です。 Configuration Manager では、電子メール機能は追加されません。<br /><br /> 使用するデバイスと電子メール インフラストラクチャに推奨されているセキュリティ上のベスト プラクティスを特定および実装し、それに従います。|  

## <a name="privacy-information-for-email-profiles"></a>電子メール プロファイルのプライバシー情報  
 既定では、デバイスは電子メール プロファイルを評価しません。 また、電子メール プロファイルを構成してから、電子メール プロファイルをユーザーに展開する必要があります。  

 電子メール プロファイルを構成する前に、プライバシー要件について検討してください。  
