---
title: ハイブリッド MDM のリソースを Intune スタンドアロンに移行する
titleSuffix: Configuration Manager
description: ハイブリッド MDM のユーザーとデバイスを Azure 上の Intune に移行する方法を説明します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: 09ea3340d8474c69e6e346fc68120b8849159374
ms.sourcegitcommit: 316899b08f2ef372993909e08e069f7edfed1d33
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2018
ms.locfileid: "44111044"
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>ハイブリッド MDM のユーザーとデバイスを Intune スタンドアロンに移行する

*適用対象: System Center Configuration Manager (Current Branch)*    

この記事では、ハイブリッド MDM から Azure での Intune を使用するクラウドのみのエクスペリエンスに移行します。 

> [!Important]  
> 2018 年 8 月 14 日の時点では、ハイブリッド モバイル デバイス管理は[非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)です。 詳細については、[ハイブリッド MDM の概要](/sccm/mdm/understand/hybrid-mobile-device-management)に関するページを参照してください。<!--Intune feature 2683117-->  


段階的なアプローチを使用して、Intune スタンドアロンへの移行を開始します。 このアプローチでは、ほとんどのユーザーとデバイスはまだハイブリッド MDM で管理したまま、ユーザーとデバイスの小さなサブセットでテストします。 Intune の機能を検証した後、さらに多くのリソースの Intune への移行を開始します。    

詳細については、以下の記事を参照してください。    
  
1.  [Configuration Manager のデータの Microsoft Intune へのインポート](migrate-import-data.md)   

    Intune Data Importer ツール:  

    - Configuration Manager 階層から選択したオブジェクトに関するデータを収集します  

    - インポートの対象に選択できるオブジェクトについての詳細を提供します   

    - 一部のオブジェクトをインポートできない理由についての情報を提供します  

    - 選択したオブジェクトを Microsoft Intune テナントにインポートします  

    この手順は省略可能です。 Configuration Manager から Intune にオブジェクトを再作成するプロセスを自動化することによって、時間を節約できます。  

2.  [Intune でのユーザーの移行を準備する](migrate-prepare-intune.md)    

    - Configuration Manager からインポートされたオブジェクトを検証します  

    - 新しいオブジェクトを作成します  

    - Azure AD グループを作成し、これらのグループにオブジェクトを割り当てます  

    - NDES と Exchange コネクタをインストールします  

    手順を完了して、Intune スタンドアロンへの移行を開始するときに、ユーザーに対して透過的にする必要があります。   

3.  [特定のユーザー (混在 MDM 機関) のMDM 機関を変更する](migrate-mixed-authority.md)    

    同じテナントに混在 MDM 機関を構成します。 一部のユーザーを選択して Intune で管理し、他のすべてのデバイスは引き続きハイブリッド MDM で管理します。 他のユーザーの移行を始める前に、少数のユーザーのデバイス上で Intune の機能が動作していることをテストします。   

4.  [MDM 機関を Intune スタンドアロンに変更する](change-mdm-authority.md)     

    テナント レベルの MDM 機関を Configuration Manager から Intune に変更します。 残りのすべてのユーザーとデバイスは、Intune スタンドアロンに移行されます。 前の手順で Intune の機能を徹底的にテストし、ユーザーのほとんどまたはすべてを移行した後、テナント レベルの MDM 機関を変更します。



## <a name="request-assistance"></a>サポートを要求する
<!--Intune bug 2339232--> Microsoft FastTrack プログラムからのサポートを求めるには、[FastTrack for Microsoft 365](https://fasttrack.microsoft.com/microsoft365/capabilities?view=security) に移動して開始します。

1. [サインイン] をクリックして、組織の ID を入力します  

2. ダッシュボードに移動し、指示に従って **[Request for Assistance]\(サポートの要求\)** フォームに移動します。    

3. Microsoft は要求を確認し、特定のニーズや適格性に応じて適切なチームに渡します。  

このダッシュボードでは、Microsoft Cloud でのエクスペリエンスをすばらしいものにするのに役立つ FastTrack の専門家からのベスト プラクティス、ツール、リソースを見つけることもできます。

