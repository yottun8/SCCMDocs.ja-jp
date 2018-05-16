---
title: Windows 10 のサポート
titleSuffix: Configuration Manager
description: System Center Configuration Manager でクライアントとして、または OSD 用にサポートされている Windows 10 のバージョンについて説明します
ms.date: 04/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 947392d4c11b419e0e373fbe83db42522d3c5f25
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="support-for-windows-10-in-system-center-configuration-manager"></a>System Center Configuration Manager での Windows 10 のサポート  

*適用対象: System Center Configuration Manager (Current Branch)*


次のような、Configuration Manager でサポートされる Windows 10 のバージョンについて説明します
 -  [Configuration Manager クライアントとしての Windows 10](#windows-10-as-a-client)
 -  [Windows 10 用のアセスメント & デプロイメント キット (ADK)](#windows-10-adk)



## <a name="windows-10-as-a-client"></a>クライアントとしての Windows 10
Configuration Manager は、Windows 10 の新しいバージョンが利用可能になると、できるだけ早くそのバージョンに対してクライアントとしてのサポートを提供しようとします。 製品には個別の開発およびリリースのスケジュールがあるため、Configuration Manager で提供するサポートは、各製品のリリース時期によって異なります。

たとえば、Configuration Manager バージョンは、[そのバージョンのサポート](/sccm/core/servers/manage/current-branch-versions-supported)の終了後に、マトリックスから除外されます。 同様に、Enterprise 2015 LTSB または 1511 などの Windows 10 バージョンのサポートは、サポートから削除されると、マトリックスから除外されます。 詳細については、「[非推奨のオペレーティング システム](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems)」を参照してください。

-   この情報は、「[クライアントとデバイスのサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)」の補足です。  

-   Configuration Manager の Long-Term Servicing Branch を使用する場合は、「[Long-Term Servicing Branch でサポートされている構成](/sccm/core/understand/supported-configurations-for-ltsb)」を参照してください。  

<br/>
次の表は、さまざまなバージョンの Configuration Manager でクライアントとして使用できる Windows 10 のバージョン一覧です。

| Windows 10 バージョン | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802 |
|---------------------|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |
| Enterprise 2016 LTSB            <!--10/13/2026-->   | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |
| 1607   <br />(*エディションを参照*)   <!--04+6/10/2018-->   | ![サポートされています](media/green_check.png) <sup>1</sup> | ![サポートされています](media/green_check.png) <sup>1</sup> | ![サポートされています](media/green_check.png) <sup>1</sup> |
| 1703   <br />(*エディションを参照*)   <!--10+6/09/2018-->   | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |
| 1709   <br />(*エディションを参照*)   <!--04+6/09/2019-->   | ![下位互換性あり](media/blue_compat.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |
| 1803   <br />(*エディションを参照*)   <!--11/12/2019-->   | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされています](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

**エディション:** Enterprise、Pro、Education、Pro Education   

<sup>1</sup> 詳細については、[Windows ライフサイクルのファクト シート](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)とその "Enterprise および Education エディションのサービス提供延長" セクションを参照してください。

| キー |
|--|
| ![サポートされています](media/green_check.png) = **サポートされています**  |
| ![下位互換性あり](media/blue_compat.png)  = **下位互換性あり** <br/> 既存のクライアント管理機能は、これらの新しい Windows 10 バージョンで動作します。 たとえば、ハードウェア インベントリ、ソフトウェア インベントリ、ソフトウェア更新プログラムなどです。 既知の問題や注意事項が記述されます。 <br><br>この方法では、アプリケーションの互換性サポートが含まれる新しい Windows ビルドをすぐに展開して管理することができ、新しい Configuration Manager 更新バージョンを必要としません。 |
| ![サポートされていません](media/Red_X.png) = **サポートされていません** |

 > [!NOTE]  
 > バージョン 1802 以降の Configuration Manager は、Windows 10 ARM64 デバイス上のクライアントをサポートします。 既存のクライアント管理機能は、これらの新しいデバイスで動作します。 たとえば、ハードウェアとソフトウェアのインベントリ、ソフトウェア更新プログラム、アプリケーション管理などです。 OS の展開は現在はサポートされていません。 <!-- 1353704 --> 



## <a name="windows-10-adk"></a>Windows 10 ADK
Configuration Manager を使用してオペレーティング システムを展開する場合、[Windows ADK は必須の外部依存コンポーネント](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)です。

次の表は、さまざまなバージョンの Configuration Manager で使用できる Windows 10 ADK のバージョン一覧です。

| Windows 10 ADK バージョン  | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802   |
|--------------------|-----|-----|-----|
| 1703  | ![サポートされています](media/green_check.png) | ![下位互換性あり](media/blue_compat.png) | ![下位互換性あり](media/blue_compat.png) |
| 1709  | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |
| 1803  | ![サポートされていません](media/Red_X.png)   | ![サポートされていません](media/Red_X.png) | ![サポートされています](media/green_check.png) |

|キー|
|--|
| ![サポートされています](media/green_check.png) = **サポートされています** <br/> Windows では、展開している Windows のバージョンに合う Windows ADK を使用することをお勧めします。 たとえば、Windows 10 バージョン 1703 を展開している場合は、Windows 10 バージョン 1703 用 Windows ADK を使用します。 Windows ADK コンポーネントのサポートについては、「[DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)」(DISM でサポートされているプラットフォーム) および「[USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1)」(USMT の要件) を参照してください。 |
| ![下位互換性あり](media/blue_compat.png)  = **下位互換性あり** <br/> この組み合わせはテストされていませんが、動作するはずです。 既知の問題や注意事項が記述されます。 |
| ![サポートされていません](media/Red_X.png) = **サポートされていません** |

 > [!Note]  
 > Configuration Manager は、Windows 10 ADK の x86 および amd64 コンポーネントのみをサポートします。 ARM または ARM64 コンポーネントは現在はサポートされていません。 