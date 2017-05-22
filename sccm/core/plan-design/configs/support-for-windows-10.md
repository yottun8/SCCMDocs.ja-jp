---
title: "Windows 10 のサポート | Microsoft Docs"
description: "System Center Configuration Manager でクライアントとして、または OSD 用にサポートされている Windows 10 バージョンについて説明します。"
ms.custom: na
ms.date: 05/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 065b1fcb25d7c7845b6f26e757b36e7fb97ce013
ms.openlocfilehash: 2ec25e9b093d9451d8880ba36f4d022ec4bad001
ms.contentlocale: ja-jp
ms.lasthandoff: 05/10/2017

---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>System Center Configuration Manager の Windows 10 のサポート

*適用対象: System Center Configuration Manager (Current Branch)*


 このトピックでは、さまざまなバージョンの System Center Configuration Manager Current Branch で使用できる Windows 10 のバージョンについて説明します。 以下は、必要な操作の例です。
 -  Configuration Manager クライアントとしての Windows 10。
 -  Windows 10 Windows アセスメント & デプロイメント キット (ADK)。

## <a name="windows-10-as-a-client"></a>クライアントとしての Windows 10
Configuration Manager は、Windows 10 の新しいバージョンがリリースされると、できるだけ早く、そのバージョンに対してクライアントとしてのサポートを提供しようとします。 製品には個別の開発およびリリースのスケジュールがあるため、Configuration Manager で提供するサポートは、各製品のバージョンおよびブランチのリリース時期によって異なります。

たとえば、Configuration Manager バージョンは、[そのバージョンのサポート](/sccm/core/servers/manage/current-branch-versions-supported)の終了後に、マトリックスから除外されます。 同様に、Enterprise 2015 LTSB または 1607 (CBB) などの Windows 10 バージョンのサポートは、Configuration Manager でサポートされる構成リストから削除されると、マトリックスから除外されます。 詳細については、「[非推奨オペレーティング システム](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems)」を参照してください。

-   次の情報は、「[クライアントとデバイスのサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)」の補足です。
-   Configuration Manager の Long-Term Servicing Branch を使用する場合は、「[Long-Term Servicing Branch でサポートされている構成](/sccm/core/understand/supported-configurations-for-ltsb)」を参照してください。

|Windows 10 のバージョン                    |Configuration Manager 1606          |Configuration Manager 1610          |    Configuration Manager 1702 |
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB                   |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |
|1507 <br />(*エディションを参照*)            |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |
|1511 (CB)、(CBB)<br />(*エディションを参照*) |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |
|Enterprise 2016 LTSB                   |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |
|1607 (CB)    <br />Anniversary Update<br />(*エディションを参照*)      |![下位互換性あり](media/blue_compat.png) |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |
|1607 (CBB)    <br />Anniversary Update<br />(*エディションを参照*)      |![サポートされていません](media/Red_X.png)   |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |
|1703 (CB)    <br />Creators Update<br />(*エディションを参照*)      |![サポートされていません](media/Red_X.png)   |![サポートされていません](media/Red_X.png) |![下位互換性あり](media/blue_compat.png) |


**エディション:** Enterprise、Pro、Education、Pro Education   

|キー|
|--|
|![サポートされています](media/green_check.png) = **サポートされています**  |
|![サポートされていません](media/blue_compat.png)  = **下位互換性あり** - つまり、既存のクライアント管理機能 (ハードウェア インベントリ、ソフトウェア インベントリ、ソフトウェア更新プログラムなど) は、新しい Windows 10 Current Branch のビルドで動作する必要があります。 既知の問題や注意事項が記述されます。 <br><br>この方法では、新しい Configuration Manager 更新バージョンを必要とせずに、アプリケーションの互換性サポートが含まれる新しい Windows 10 CB ビルドを 1 日で展開して管理することができます。 |
|![サポートされています](media/Red_X.png) = **サポートされていません**|


## <a name="windows-10-adk"></a>Windows 10 ADK
Configuration Manager を使用してオペレーティング システムを展開する場合、[Windows ADK は必須の外部依存コンポーネント](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)です。

次の表は、さまざまなバージョンの Configuration Manager で使用できる Windows 10 ADK のバージョン一覧です。

|Windows 10 のバージョン |Configuration Manager 1606 |Configuration Manager 1610  |Configuration Manager 1702 |
|--------------------|-----|-----|-----|
|1507  |![サポートされていません](media/Red_X.png)         |![サポートされていません](media/Red_X.png)  |![サポートされていません](media/Red_X.png)|
|1511  |![下位互換性あり](media/blue_compat.png)|![サポートされていません](media/Red_X.png)  |![サポートされていません](media/Red_X.png)|
|1607  |![サポートされています](media/green_check.png)       |![サポートされています](media/green_check.png)|![下位互換性あり](media/blue_compat.png) |
|1703  |![サポートされていません](media/Red_X.png)         |![サポートされていません](media/Red_X.png)  |![サポートされています](media/green_check.png) |  

|キー|
|--|
|![サポートされています](media/green_check.png) = **サポートされています** - Windows では、展開している Windows のバージョンに合う Windows ADK を使用することをお勧めします。 たとえば、Windows 10 バージョン 1703 を展開している場合は、Windows 10 バージョン 1703 用 Windows ADK を使用します。  |
|![下位互換性あり](media/blue_compat.png)  = **下位互換性あり** - この組み合わせはテストされていませんが、おそらく動作します。 既知の問題や注意事項が記述されます。 |
|![サポートされています](media/Red_X.png) = **サポートされていません**|

