---
title: 非推奨の機能
titleSuffix: Configuration Manager
description: System Center Configuration Manager でサポートされなくなった機能について説明します。
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 967c0ff71af5b3586568bf3f5d2fee7ed5b8bb06
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337736"
---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>System Center Configuration Manager から削除された機能と非推奨の機能

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、Configuration Manager のサポートから非推奨になった、または削除された機能を示します。 非推奨の機能は、今後の更新で削除されます。 これらの将来的な変更は、Configuration Manager の使用に影響する可能性があります。  

この情報は今後のリリースで変更されます。 Configuration Manager の非推奨の機能は個別に含まれないことがあります。



## <a name="deprecated-features"></a>非推奨の機能  

|機能|最初に非推奨と発表|削除されたサポート&nbsp;|  
|-----------|---|--------------|  
|これまではアプリケーション カタログにしか表示されなかったユーザーが利用できるアプリが、新しいソフトウェア センターでは表示されるようになりました。 </br></br>そのため、Web ベースのアプリケーション カタログのエクスペリエンスは、今後数か月で使用できなくなります。|2017 年 8 月 11 日| アプリケーション カタログの Web サイトでのユーザー エクスペリエンスは、2018 年 6 月 1 日以降にリリースされる最初の更新プログラムでサポートが終了します。|
|以前のバージョンのソフトウェア センター。<br><br>ソフトウェア センターの詳細については、「[アプリケーション管理の計画と構成](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only)」をご覧ください。|2016 年 12 月 13 日|バージョン 1802|
|Configuration Manager によるバーチャル ハード ディスク (VHD) の管理。 </br></br>この非推奨機能には、新しい VHD の作成オプション、またはタスク シーケンスを使用した VHD の管理オプションの削除と、Configuration Manager コンソールからのバーチャル ハード ディスクのノードの削除が含まれます。 </br></br>既存の VHD は削除されませんが、Configuration Manager コンソール内からはアクセスできなくなります。  |2017 年 1 月 6 日 |バージョン 1710|
|タスク シーケンス: <br /> - ディスクをダイナミックに変換 <br /> - 展開ツールのインストール |2016 年 11 月 18 日|バージョン 1710|
|System Center Configuration Manager Upgrade Assessment Tool。 </br></br>Upgrade Assessment Tool は、System Center Configuration Manager と Application Compatibility Toolkit (ACT) 6.x の両方に依存します。 ACT の最終バージョンは、Windows 10 v1511 ADK に同梱されていました。 今後、ACT が更新されることはないため、Upgrade Assessment Tool のサポートは廃止されます。 </br></br>Upgrade Assessment Tool は、[アップグレードの準備](/sccm/core/clients/manage/upgrade/upgrade-analytics)機能に置き換えられます。 非推奨に関する注記は、2016 年 9 月 12 日に [UAT のダウンロード ページ](https://www.microsoft.com/download/details.aspx?id=37145)に追加されました。 | 2016 年 9 月 12 日  | 2017 年 7 月 11 日 |
|タスク シーケンス: <br /> - OSDPreserveDriveLetter  <br /><br /> 既定で、オペレーティング システムの展開中に、Windows セットアップが使用する最適なドライブ文字を決定するようになりました (通常は C:)。 別のドライブを使用するように指定する場合は、オペレーティング システムの適用タスク シーケンスのステップで場所を変更できます。 **[このオペレーティング システムの適用先を選択してください。]** の設定に進みます。 **[特定の論理ドライブ文字]** を選び、使うドライブを選びます。 |2016 年 6 月 20 日 |バージョン 1606 |
|ネットワーク アクセス保護 (NAP) - System Center 2012 Configuration Manager の機能|2015 年 7 月 10 日|バージョン 1511|  
|帯域外管理 - System Center 2012 Configuration Manager の機能|2015 年 10 月 16 日|バージョン 1511|



## <a name="features-removed-in-version-1511"></a>バージョン 1511 で削除された機能
次のセクションでは、バージョン 1511 で削除された機能の詳細を示します。

###  <a name="bkmk_amt"></a> 帯域外管理  
 Configuration Manager では、Configuration Manager コンソール内からの AMT ベースのコンピューターに対するネイティブ サポートは削除されました。  

-   [Microsoft System Center Configuration Manager 用 Intel SCS アドオン](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)を使用すれば、AMT ベースのコンピューターは引き続き完全に管理されます。 アドオンを使用することで、最新の機能にアクセスして AMT を管理できます。Configuration Manager にこれらの変更が組み込まれるまでに適用されていた制限は解除されます。  

-   System Center 2012 Configuration Manager での帯域外管理は、この変更の影響を受けません。  

###  <a name="bkmk_nap"></a> ネットワーク アクセス保護  
 System Center Configuration Manager では、ネットワーク アクセス保護のサポートが削除されました。 この機能は Windows Server 2012 R2 で非推奨となり、Windows 10 からは削除されています。  

 ネットワーク アクセス保護の代替方法については、「 *ネットワーク ポリシーとアクセス サービスの概要* 」で [非推奨の機能](https://technet.microsoft.com/library/hh831683.aspx)に関する説明を参照してください。



## <a name="more-information"></a>説明
詳細については、次をご覧ください。
 - [削除と非推奨](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - [マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)
 - [Configuration Manager の Current Branch バージョンのサポート](/sccm/core/servers/manage/current-branch-versions-supported)
