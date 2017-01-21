---
title: "Endpoint Protection の構成 | Microsoft Docs"
description: "System Center Configuration Manager でクライアント コンピューターのセキュリティとマルウェアを管理する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 3678fd1e2ba70ad1cc03a3e0ca294901fae96255


---
# <a name="configuring-endpoint-protection-in-system-center-configuration-manager"></a>System Center Configuration Manager での Endpoint Protection の構成

*適用対象: System Center Configuration Manager (Current Branch)*

Endpoint Protection を利用し、Configuration Manager クライアント コンピューターのセキュリティとマルウェアを管理する前に、このトピックを利用して設定します。  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Configuration Manager の Endpoint Protection の構成方法  
 Configuration Manager の Endpoint Protection には、この製品の内外で依存関係があります。  

### <a name="configure-endpoint-protection-in-configuration-manager"></a>Configuration Manager の Endpoint Protection の構成  
Endpoint Protection は 5 つの手順で構成します。

|手順|説明|
|---|----|
|手順 1|[Endpoint Protection ポイント サイト システムの役割](endpoint-protection-site-role.md) - Endpoint Protection ポイント サイト システムの役割をインストールする |
|手順 2|[Endpoint Protection のアラートの構成](endpoint-configure-alerts.md) - 階層で特定のセキュリティ イベントが発生したときに監理者に通知するように Endpoint Protection アラートを構成します。|
|手順 3 | [Endpoint Protection クライアントの定義ファイルの更新ソースを構成する](endpoint-definition-updates.md) - クライアント コンピューターでマルウェア対策定義を最新の状態に維持するために利用できる方法から選択します。|
|手順 4|[既定のマルウェア対策ポリシーを構成し、カスタムのマルウェア対策ポリシーを作成する](endpoint-antimalware-policies.md) - Endpoint Protection クライアントがインストールされると、既定のマルウェア対策ポリシーが適用されます。カスタム ポリシーはクライアントの展開から 60 分以内に適用されます。|
|手順 5|[Endpoint Protection のカスタム クライアント設定を構成する](endpoint-protection-configure-client.md) - Endpoint Protection のカスタム クライアント設定を構成し、コンピューターの集合に展開します。|

> [!IMPORTANT]  
>  Windows 10 コンピューターの Endpoint Protection を管理する場合、Windows Defender のマルウェア定義ファイルを更新し、配布するように Configuration Manager を構成する必要があります。 Windows Defender は Windows 10 に含まれていますが、SCEPInstall をインストールする必要があります。また、Endpoint Protection のカスタム クライアント設定が必要です (手順 5)。  



<!--HONumber=Dec16_HO3-->


