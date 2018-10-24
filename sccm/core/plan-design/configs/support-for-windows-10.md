---
title: Windows 10 のサポート
titleSuffix: Configuration Manager
description: System Center Configuration Manager でクライアントとして、または OSD 用にサポートされている Windows 10 のバージョンについて説明します
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 67a25cc788c417409306e506de97cb0fdf1cf2e8
ms.sourcegitcommit: 265d38d55ca0db043e3a7131a56f123e1d98aa5b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2018
ms.locfileid: "48236142"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Configuration Manager での Windows 10 のサポート  

*適用対象: System Center Configuration Manager (Current Branch)*


次のような、Configuration Manager でサポートされる Windows 10 のバージョンについて説明します
 -  [Configuration Manager クライアントとしての Windows 10](#windows-10-as-a-client)
 -  [Windows 10 用のアセスメント & デプロイメント キット (ADK)](#windows-10-adk)

> [!Tip]
> クライアントとしての Windows Server のビルドは、関連する Windows 10 バージョンと同じものがサポートされています。 たとえば、Windows Server 2016 は Windows 10 LTSB 2016 と同じビルド バージョンで、Windows Server バージョン 1803 は Windows 10 バージョン 1803 と同じビルド バージョンです。
> 
> サイト システムとしての Windows Server の詳細については、「[Configuration Manager サイト システム サーバーでサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#the-server-core-installation-of-windows-server-version-1803)」を参照してください。



## <a name="windows-10-as-a-client"></a>クライアントとしての Windows 10

Configuration Manager は、Windows 10 の新しいバージョンが利用可能になると、できるだけ早くそのバージョンに対してクライアントとしてのサポートを提供しようとします。 製品には個別の開発およびリリースのスケジュールがあるため、Configuration Manager で提供するサポートは、各製品のリリース時期によって異なります。

Configuration Manager バージョンは、[そのバージョンのサポート](/sccm/core/servers/manage/current-branch-versions-supported)の終了後に、マトリックスから除外されます。 同様に、Enterprise 2015 LTSB または 1511 などの Windows 10 バージョンのサポートは、サポートから削除されると、マトリックスから除外されます。

-   Configuration Manager の現在のブランチの最新バージョンでは、セキュリティ更新プログラムと重要な更新プログラムの両方が受信されます。これらには、Windows 10 のバージョンに関する問題の修正プログラムが含まれる場合があります。 Microsoft で Configuration Manager の現在のブランチの新しいバージョンがリリースされた際、以前のバージョンでは、セキュリティ更新プログラムのみが受信されます。 詳細については、[Configuration Manager の Current Branch バージョンのサポート](/sccm/core/servers/manage/current-branch-versions-supported)に関するページをご覧ください。  

    > [!Note]  
    > Windows 10 を最新状態に保つ最良の方法は、Configuration Manager を最新状態に保つことです。 詳細については、「[Configuration Manager とサービスとしての Windows](/sccm/core/understand/configuration-manager-and-windows-as-service)」を参照してください。  

-   この情報は、「[クライアントとデバイスのサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)」の補足です。  

-   Configuration Manager の Long-Term Servicing Branch を使用する場合は、「[Long-Term Servicing Branch でサポートされている構成](/sccm/core/understand/supported-configurations-for-ltsb)」を参照してください。  

<br/>
次の表は、さまざまなバージョンの Configuration Manager でクライアントとして使用できる Windows 10 のバージョン一覧です。

| Windows 10 バージョン | Configuration Manager 1710 | Configuration Manager 1802 | Configuration Manager 1806 |
|---------------------|-----|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |
| Enterprise 2016 LTSB            <!--10/13/2026-->   | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |
| 1607   <!--04/09/2019-->   | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |
| 1703   <!--10/08/2019-->   | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |
| 1709   <!--04/14/2020-->   | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |
| 1803   <!--11/10/2020-->   | ![サポートされていません](media/Red_X.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |
| 1809   <!--04/12/2021?-->   | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされています](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

> [!Note]  
> 半期チャネル バージョンの Windows 10 のサポートには、エディション: Enterprise、Pro、Education、および Pro Education が含まれます。   

| キー |
|--|
| ![サポートされています](media/green_check.png) = **サポートされています**  |
| ![サポートされていません](media/Red_X.png) = **サポートされていません** |

 > [!NOTE]  
 > バージョン 1802 以降の Configuration Manager は、Windows 10 ARM64 デバイス上のクライアントをサポートします。 既存のクライアント管理機能は、これらの新しいデバイスで動作します。 たとえば、ハードウェアとソフトウェアのインベントリ、ソフトウェア更新プログラム、アプリケーション管理などです。 OS の展開は現在はサポートされていません。 <!-- 1353704 --> 

Windows ライフサイクルの詳細については、「[Windows ライフサイクルのファクト シート](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)」を参照してください。



## <a name="windows-10-adk"></a>Windows 10 ADK

Configuration Manager を使用してオペレーティング システムを展開する場合、Windows ADK は必須の外部依存コンポーネントです。 詳細については、[OS 展開のインフラストラクチャ要件](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk-for-windows-10)に関するページを参照してください。

次の表は、さまざまなバージョンの Configuration Manager で使用できる Windows 10 ADK のバージョン一覧です。

| Windows 10 ADK バージョン  | Configuration Manager 1710 | Configuration Manager 1802 | Configuration Manager 1806 |
|--------------------|-----|-----|-----|-----|
| 1703  | ![下位互換性あり](media/blue_compat.png) | ![下位互換性あり](media/blue_compat.png) | ![サポートされていません](media/Red_X.png)   |
| 1709  | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | ![下位互換性あり](media/blue_compat.png) |
| 1803  | ![サポートされていません](media/Red_X.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |
| 1809  | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされています](media/green_check.png) |

|キー|
|--|
| ![サポートされています](media/green_check.png) = **サポートされています** <br/> Microsoft では、展開している Windows のバージョンに合う Windows ADK を使用することをお勧めします。 たとえば、Windows 10 バージョン 1703 を展開している場合は、Windows 10 バージョン 1703 用 Windows ADK を使用します。 Windows ADK コンポーネントのサポートについては、「[DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)」(DISM でサポートされているプラットフォーム) および「[USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1)」(USMT の要件) を参照してください。 |
| ![下位互換性あり](media/blue_compat.png)  = **下位互換性あり** <br/> この組み合わせはテストされていませんが、動作するはずです。 既知の問題や注意事項が記述されます。 |
| ![サポートされていません](media/Red_X.png) = **サポートされていません** |

 > [!Note]  
 > Configuration Manager は、Windows 10 ADK の x86 および amd64 コンポーネントのみをサポートします。 ARM または ARM64 コンポーネントは現在はサポートされていません。 

> [!Tip]
> Windows Server のビルドには、関連付けられている Windows 10 バージョンと同じ Windows ADK が必要です。 たとえば、Windows Server 2016 は Windows 10 LTSB 2016 と同じビルド バージョンです。
