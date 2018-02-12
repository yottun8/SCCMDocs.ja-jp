---
title: "Configuration Manager の非推奨になった機能"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager でサポートされなくなった機能について説明します。"
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: d49e0f839106af652f7b49227b6c4f8c957347d9
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2018
---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>System Center Configuration Manager から削除された機能と非推奨の機能

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、System Center Configuration Manager のサポート対象から削除されたか、今後の更新で削除される予定 (非推奨) の機能について説明します。 この記事は、Configuration Manager の使用に影響する可能性のある将来の変更について早期に注意するものです。  

この情報は、今後のリリースで変更される可能性があります。また、Configuration Manager の非推奨の機能をすべて記載しているわけではありません。

## <a name="deprecated-features"></a>非推奨の機能  

|**機能**|**最初に非推奨と発表**|**サポートの削除**|  
|-|-|-|  
|バージョン 1511 では新しいソフトウェア センターのエクスペリエンスが提供され、これまでアプリケーション カタログにしか表示されなかったアプリ (ユーザーが利用できるアプリ) がソフトウェア センターに表示されるようになりました。 </br></br>アプリケーション カタログの主な機能がソフトウェア センターに含まれるようになったため、Web ベースのアプリケーション カタログのエクスペリエンスは、今後数か月の間に使用できなくなります。|2017 年 8 月 11 日| アプリケーション カタログの Web サイトでのユーザー エクスペリエンスは、2018 年 6 月 1 日以降にリリースされる最初の更新プログラムでサポートが終了します。|
|ソフトウェア センターは新しい現代的な外観へと一新されます。 以前のバージョンのソフトウェア センターは、今後数か月の間に使用できなくなります。<br><br>新しいソフトウェア センターを使用するようにクライアントをセットアップするには、クライアント設定 **[コンピューター エージェント]** > **[新しいソフトウェア センターの使用]** を有効化します。<br><br>ソフトウェア センターの詳細については、「[System Center Configuration Manager のアプリケーション管理の計画と構成](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management)」を参照してください。|2016 年 12 月 13 日|ソフトウェア センターの以前のバージョンは、2018 年 1 月 1 日以降にリリースされる最初の更新プログラムによってサポートが終了します。|
|Configuration Manager によるバーチャル ハード ディスク (VHD) の管理。 </br></br>これには、新しい VHD の作成オプション、またはタスク シーケンスを使用した VHD の管理オプションの削除と、Configuration Manager コンソールからのバーチャル ハード ディスクのノードの削除が含まれます。 </br></br>このサポートが削除されると、既存の VHD は削除されませんが、Configuration Manager コンソール内からアクセスできなくなります。  |2017 年 1 月 6 日 |バージョン 1710|
|タスク シーケンス: <br /> - ディスクをダイナミックに変換 <br /> - 展開ツールのインストール |2016 年 11 月 18 日|バージョン 1710|
|System Center Configuration Manager Upgrade Assessment Tool。 </br></br>Upgrade Assessment Tool は、System Center Configuration Manager と Application Compatibility Toolkit (ACT) 6.x の両方に依存します。 ACT の最終バージョンは、Windows 10 v1511 ADK に同梱されていました。 今後、ACT が更新されることはないため、Upgrade Assessment Tool のサポートは廃止されます。 </br></br>Upgrade Assessment Tool は、[アップグレードの準備](/sccm/core/clients/manage/upgrade/upgrade-analytics)機能に置き換えられます。 非推奨に関する注記は、2016 年 9 月 12 日に [UAT のダウンロード ページ](https://www.microsoft.com/download/details.aspx?id=37145)に追加されました。 | 2016 年 9 月 12 日  | 2017 年 7 月 11 日 |
|タスク シーケンス: <br /> - OSDPreserveDriveLetter  <br /><br /> 既定で、オペレーティング システムの展開中に、Windows セットアップが使用する最適なドライブ文字を決定するようになりました (通常は C:)。 別のドライブを使用するように指定する場合は、オペレーティング システムの適用タスク シーケンスのステップで場所を変更できます。 **[このオペレーティング システムの適用先を選択してください。]** の設定に進みます。 **[特定の論理ドライブ文字]** を選び、使うドライブを選びます。 |2016 年 6 月 20 日 |バージョン 1606 |
|ネットワーク アクセス保護 (NAP) - System Center 2012 Configuration Manager の機能|2015 年 7 月 10 日|バージョン 1511|  
|帯域外管理 - System Center 2012 Configuration Manager の機能|2015 年 10 月 16 日|バージョン 1511|



<br></br>
バージョン 1511 の System Center Configuration Manager リリースで削除された機能の詳細を次に示します。

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
 - [Microsoft サポート ライフサイクル](https://support.microsoft.com/lifecycle) Web サイト
 - [Configuration Manager の Current Branch バージョンのサポート](/sccm/core/servers/manage/current-branch-versions-supported)
