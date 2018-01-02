---
title: "ハイブリッド MDM のユーザーとデバイスを Intune スタンドアロンに移行する"
titleSuffix: Configuration Manager
description: "ハイブリッド MDM のユーザーとデバイスを Azure 上の Intune に移行する方法を説明します。"
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: 30474f6dd0216078ab1ac1f4bd9f5044f1b174f0
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2017
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>ハイブリッド MDM のユーザーとデバイスを Intune スタンドアロンに移行する

*適用対象: System Center Configuration Manager (Current Branch)*    

この記事は、Azure 上の Intune を使用してハイブリッド MDM (Intune と Configuration Manager の統合) からクラウドのみのエクスペリエンスに移行する準備ができたと判断した場合に役立ちます。 準備ができたか判断できない場合は、「[Microsoft Intune スタンドアロンか System Center Configuration Manager を使用するハイブリッド モバイル デバイス管理を選択する](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)」を参照してください。 

ほとんどのユーザーとデバイスをハイブリッド MDM. で管理しつつ、ごく一部のユーザーとデバイスをテストできるようにする段階的なアプローチを使用して、Intune スタンドアロンへの移行を開始できます。 そして Intune の機能の検証後、さらに多くのユーザーの Intune への移行を開始できます。    

次のトピックでは、段階的なアプローチを使用して Intune スタンドアロンにユーザーを移行する手順を説明します。    
  
1.  [Configuration Manager のデータの Microsoft Intune へのインポート](migrate-import-data.md)   
    Intune Data Importer ツールは、Configuration Manager 階層から選択したオブジェクトに関するデータを収集し、インポートのために選択できるオブジェクトに関する詳細と、一部のオブジェクトがインポートできない理由に関する情報を提供し、選択したオブジェクトを Microsoft Intune テナントにインポートできるようにします。 この手順は任意ですが、Configuration Manager から Intune にオブジェクトを再作成するプロセスを自動化することによって、多くの時間を節約できます。 
2.  [Intune でのユーザーの移行を準備する](migrate-prepare-intune.md)    
    Configuration Manager からインポートされたオブジェクトを検証する、新しいオブジェクトを作成する、AAD グループを作成する、これらのグループにオブジェクトを割り当てる、NDES と Exchange コネクタをインストールするなどを行います。手順を完了して、Intune スタンドアロンへの移行を開始するときに、ユーザーに対して透過的にする必要があります。  
3.  [特定のユーザー (混在 MDM 機関) の MDM 機関を変更する](migrate-mixed-authority.md)    
    一部のユーザーを Intune で管理し、他のすべてのデバイスを引き続きハイブリッド MDM (Intune と Configuration Manager の統合) で管理するように選択することで、同じテナントで混在 MDM 機関を構成します。 追加のユーザー移行を開始する前に、ごく一部のユーザーのデバイス上で Intune 機能が想定通りに機能していることをテストできます。 
4.  [MDM 機関を Intune スタンドアロンに変更する](change-mdm-authority.md)     
    テナント レベルの MDM 機関を Configuration Manager から Intune に変更します。 残りのすべてのユーザーとデバイスは、Intune スタンドアロンに移行されます。 前の手順で Intune の機能を徹底的にテストし、ユーザーのほとんどまたはすべてを既に移行した後に、テナント レベルの MDM 機関を変更します。