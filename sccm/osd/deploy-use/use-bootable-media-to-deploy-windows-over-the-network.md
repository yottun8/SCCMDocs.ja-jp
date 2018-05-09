---
title: 起動可能なメディアを使用したネットワーク経由での Windows の展開
titleSuffix: Configuration Manager
description: System Center Configuration Manager での起動可能なメディアによる展開を使用して、セットアップ先のコンピューターの起動と同時にオペレーティング システムを展開できます。
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4f7ec06d5bd5f23ac2b8afa2a288dfb8c971f950
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>System Center Configuration Manager で起動可能なメディアを使用してネットワーク経由で Windows を展開する

*適用対象: System Center Configuration Manager (Current Branch)*

起動可能なメディアによる展開を使用してセットアップ先のコンピューターを起動するときにオペレーティング システムを展開できます。 メディアには、タスク シーケンス、オペレーティング システム イメージ、およびその他のネットワーク上の必要なコンテンツへのポインターが含まれています。 セットアップ先コンピューターは、起動するときに、ポインターで参照されている項目を取得します。 コンテンツのない起動可能なメディアを使用すると、メディア上で交換しなくてもセットアップ先コンピューターを更新できます。

次に挙げるオペレーティング システムの展開シナリオでは、マルチキャストを使用してネットワーク経由でオペレーティング システムを展開できます。

-   [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)  

-   [既存のコンピューターの置き換えと設定の転送](replace-an-existing-computer-and-transfer-settings.md)  

いずれかのオペレーティング システムの展開シナリオの手順を完了してから、次のセクションを使用して、起動可能なメディアでオペレーティング システムを展開します。  

## <a name="configure-deployment-settings"></a>展開の設定の構成  
起動可能なメディアを使用してオペレーティング システムの展開プロセスを開始する場合、オペレーティング システムをメディアから使用できるように展開を構成します。 このオプションはソフトウェアの展開ウィザードの **[展開の設定]** ページか展開のプロパティの **[配置の設定]** タブで設定することができます。 **[利用できるようにする項目]** の設定では、次のいずれかを設定します。

-   Configuration Manager クライアント、メディア、PXE

-   メディアと PXE のみ

-   メディアと PXE のみ (非表示)

## <a name="create-the-bootable-media"></a>起動可能なメディアを作成する
起動可能なメディアとして USB フラッシュ ドライブと CD/DVD セットのどちらかを指定できます。 起動可能なドライブに選ぶオプションは、メディアを起動するコンピューターがサポートするものでなければなりません。 詳細については、「[起動可能なメディアの作成](create-bootable-media.md)」を参照してください。  

##  <a name="BKMK_Deploy"></a> 起動可能なメディアからオペレーティング システムをインストールする  
コンピューターの起動可能なドライブに起動可能なメディアを挿入し、電源を入れてオペレーティング システムをインストールします。
