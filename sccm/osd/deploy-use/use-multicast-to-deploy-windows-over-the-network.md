---
title: "マルチキャストを使用してネットワーク経由で Windows を展開する | Configuration Manager"
description: "System Center Configuration Manager 環境内でマルチキャストを使用すると、複数のコンピューターがオペレーティング システム イメージを同時にダウンロードできるようになります。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
caps.latest.revision: 13
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: da83037a28194e3bae1e6afe4d4bca1ce43f2bf6


---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>System Center Configuration Manager でマルチキャストを使用してネットワーク経由で Windows を展開する

*適用対象: System Center Configuration Manager (Current Branch)*

マルチキャストは、複数のクライアントが同じオペレーティング システム イメージをダウンロードすることが多い System Center Configuration Manage 環境で使用できるネットワーク最適化の方法です。 マルチキャストを使用すると、配布ポイントがデータのコピーを各々のクライアントに別々の接続で送信する代わりに、マルチキャストしますので、複数のコンピューターが同時にオペレーティング システム イメージをダウンロードすることになります。  

 次に挙げるオペレーティング システムの展開シナリオでは、マルチキャストを使用してネットワーク経由でオペレーティング システムを展開できます。  

-   [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)  

 いずれかのオペレーティング システムの展開シナリオのステップを完了させてから、次のセクションを参照して、マルチキャストをサポートします。  

##  <a name="a-namebkmkconfigurea-configure-a-distribution-point-to-support-multicast"></a><a name="BKMK_Configure"></a> マルチキャストをサポートする配布ポイントの構成  
 オペレーティング システムを展開するときにマルチキャストを使用するには、マルチキャストをサポートするように配布ポイントを構成する必要があります。 詳細については、「[マルチキャストをサポートする配布ポイントの構成](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)」を参照してください。  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>マルチキャスト展開用のオペレーティング システム イメージの準備  
 マルチキャストをサポートするようにオペレーティング システム イメージ パッケージを構成するには、「[マルチキャスト展開用のオペレーティング システム イメージを準備する](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast)」を参照してください。  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> タスク シーケンスの展開  
 オペレーティング システムをターゲット コレクションに展開します。 詳細については、「 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)」をご覧ください。  



<!--HONumber=Nov16_HO1-->


