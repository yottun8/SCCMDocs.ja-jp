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
ms.openlocfilehash: a6e430248fdeedd310087c9a32c6d69ca1864a09
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2017
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>ハイブリッド MDM のユーザーとデバイスを Intune スタンドアロンに移行する

*適用対象: System Center Configuration Manager (Current Branch)*    

この記事は、Azure 上の Intune を使用してハイブリッド MDM (Intune と Configuration Manager の統合) からクラウドのみのエクスペリエンスに移行する準備ができたと判断した場合に役立ちます。 準備ができたか判断できない場合は、「[Microsoft Intune スタンドアロンか System Center Configuration Manager を使用するハイブリッド モバイル デバイス管理を選択する](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)」を参照してください。 

ほとんどのユーザーとデバイスをハイブリッド MDM. で管理しつつ、ごく一部のユーザーとデバイスをテストできるようにする段階的なアプローチを使用して、Intune スタンドアロンへの移行を開始できます。 そして Intune の機能の検証後、さらに多くのユーザーの Intune への移行を開始できます。    

次のトピックでは、段階的なアプローチを使用して Intune スタンドアロンにユーザーを移行する手順を説明します。    
  
1.  [Configuration Manager のデータの Microsoft Intune へのインポート](migrate-import-data.md)   
    Intune Data Importer ツールは、Configuration Manager 階層から選択したオブジェクトに関するデータを収集し、インポートのために選択できるオブジェクトに関する詳細と、一部のオブジェクトがインポートできない理由に関する情報を提供し、選択したオブジェクトを Microsoft Intune テナントにインポートできるようにします。 この手順は省略可能ですが、Configuration Manager から Intune にオブジェクトを再作成するプロセスを自動化することで、多くの時間を節約することができます。 
2.  [Intune でのユーザーの移行を準備する](migrate-prepare-intune.md)    
    Configuration Manager からインポートされたオブジェクトを検証する、新しいオブジェクトを作成する、AAD グループを作成する、これらのグループにオブジェクトを割り当てる、NDES と Exchange コネクタをインストールするなどを行います。手順を完了して、Intune スタンドアロンへの移行を開始するときに、ユーザーに対して透過的にする必要があります。  
3.  [特定のユーザー (混在 MDM 機関) の MDM 機関を変更する](migrate-mixed-authority.md)    
    一部のユーザーを Intune で管理し、他のすべてのデバイスを引き続きハイブリッド MDM (Intune と Configuration Manager の統合) で管理するように選択することで、同じテナントで混在 MDM 機関を構成します。 追加のユーザー移行を開始する前に、ごく一部のユーザーのデバイス上で Intune 機能が想定通りに機能していることをテストできます。 
4.  [MDM 機関を Intune スタンドアロンに変更する](change-mdm-authority.md)     
    テナント レベルの MDM 機関を Configuration Manager から Intune に変更します。 残りのすべてのユーザーとデバイスは、Intune スタンドアロンに移行されます。 前の手順で Intune の機能を徹底的にテストし、ユーザーのほとんどまたはすべてを既に移行した後に、テナント レベルの MDM 機関を変更します。

<!--
The following provides a typical workflow for migrating users from hybrid MDM to Intune standalone:
1.  Admin runs the Microsoft Intune Data Importer Tool, selecting which objects and assignments to import. Selected objects are imported into Intune standalone.
    1. Some objects cannot be imported because they contain settings the tool does not understand or setting that are not available in Intune standalone.
    2. Assignments are migrated. However, only if the collection an object was targeted to is based on a single Active Directory (AD) security group and the same group exists in Azure Active Directory (AAD).
    > [!Note]    
    > If you want, you can skip this step and create the objects that you want directly in Intune in the Azure portal without running the Intune Data Importer Tool. 
2.  Admin logs into the Intune on Azure portal
    1. Creates any additional objects required for their organization that were not imported by the Microsoft Intune Data Importer tool.
    2. Creates any required AAD groups and makes any additional assignments for each object to AAD groups.
    3. Installs the NDES connector on an on-premises server if using SCEP or PFX certificate deployment.
    4. Installs the Exchange connector on an on-premises server if using conditional access. 
3.  Admin ensures that all existing Intune users in their organization have an Intune license assigned to them using AAD or the Office administrator portal.
4.  Admin selects some test users to migrate to Intune standalone and removes them from the collection associated with the Intune subscription in Configuration Manager.
5.  Once removed from the collection, the user and all devices are managed by Intune in the Azure portal. Remaining users and devices continue to be managed by hybrid mobile device management in Configuration Manager. 
6.  Admin validates that things are working as expected on the device and moves more users to Intune standalone by removing them from the collection associated with the Intune subscription in Configuration Manager.
7.  Once the admin is comfortable with the functionality in Intune standalone, they can move the rest of their users and devices by switching their MDM authority to Intune standalone. This can be done by removing the Intune subscription from SCCM and choosing to change the MDM authority. Tenant level policies will be automatically migrated to Intune standalone, all objects and assignments in Intune standalone will remain, and devices will not be required to re-enroll.
-->