---
title: "起動可能なメディアを使用したネットワーク経由での Windows の展開 | Microsoft Docs"
description: "System Center Configuration Manager での起動可能なメディアによる展開を使用して、セットアップ先のコンピューターの起動と同時にオペレーティング システムを展開できます。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: beb730efbe4d9bae7c4c97f4e587c8919bd79049


---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>System Center Configuration Manager で起動可能なメディアを使用してネットワーク経由で Windows を展開する

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager での起動可能なメディアによる展開では、セットアップ先のコンピューターの起動と同時にオペレーティング システムを展開できます。 対象となるコンピューターが立ち上がると、タスク シーケンス、オペレーティング システム イメージ、およびその他の要求されたコンテンツをネットワークから取得します。 そのコンテンツはメディアには含まれていないため、メディアを再作成せずにコンテンツを更新することができます。  

 次に挙げるオペレーティング システムの展開シナリオでは、マルチキャストを使用してネットワーク経由でオペレーティング システムを展開できます。  

-   [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)  

-   [既存のコンピューターの置き換えと設定の転送](replace-an-existing-computer-and-transfer-settings.md)  

 いずれかのオペレーティング システムの展開シナリオの手順を完了してから、次のセクションを使用して、起動可能なメディアでオペレーティング システムを展開します。  

## <a name="configure-deployment-settings"></a>展開の設定の構成  
 起動可能なメディアを使用してオペレーティング システムの展開プロセスを開始する場合、オペレーティング システムをメディアから使用できるように展開を構成する必要があります。 これはソフトウェアの展開ウィザードの **[展開の設定]** ページか展開のプロパティの **[配置の設定]** タブで構成することができます。  **[利用できるようにする項目]** の設定では、次のいずれかを設定します。  

-   **Configuration Manager クライアント、メディア、PXE**  

-   **メディアと PXE のみ**  

-   **メディアと PXE のみ (非表示)**  

## <a name="create-the-bootable-media"></a>起動可能なメディアを作成する  
 起動可能なメディアとして USB フラッシュ ドライブと CD/DVD セットのどちらかを指定できます。 起動可能なドライブに選ぶオプションは、メディアを起動するコンピューターがサポートするものでなければなりません。 詳細については、「[起動可能なメディアの作成](create-bootable-media.md)」を参照してください。  

##  <a name="a-namebkmkdeploya-install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> 起動可能なメディアからオペレーティング システムをインストールする  
 コンピューターの起動可能なドライブに起動可能なメディアを挿入し、電源を入れてオペレーティング システムをインストールします。  



<!--HONumber=Dec16_HO3-->


