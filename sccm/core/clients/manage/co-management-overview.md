---
title: Windows 10 デバイスの共同管理
titleSuffix: Configuration Manager
description: Configuration Manager と Microsoft Intune の両方を使用して Windows 10 デバイスを同時に管理する方法について説明します。
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: e4b8bd58d30cd87ffc461289edbfc5da9a684cda
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2018
---
# <a name="co-management-for-windows-10-devices"></a>Windows 10 デバイスの共同管理    
<!-- 1350871 -->
多くのユーザーは、モバイル デバイスを管理する場合と同じ低コストで簡単なクラウド ベースのソリューションを使って、Windows 10 デバイスを管理することを望んでいます。 ただし、従来の管理から最新の管理への移行は困難な場合があります。 以前の Windows 10 の更新プログラムで、Windows 10 デバイスをオンプレミスの Active Directory (AD) とクラウドベースの Azure AD に同時に結合できるようになっています (ハイブリッド Azure AD)。 Configuration Manager バージョン 1710 以降、共同管理ではこの機能強化を活用し、Configuration Manager と Intune の両方を使用して複数の Windows 10 バージョン 1709 (Fall Creators Update とも呼ばれる) のデバイスを同時に管理できるようになりました。 これは、従来の管理から最新の管理への橋渡しとなるソリューションであり、段階的なアプローチを使って移行する方向を提示します。 

共同管理を達成するには、主に 2 つのパスがあります。  1 つは、Configuration Manager の管理対象でハイブリッド Azure AD 参加済みの Windows 10 デバイスを Intune に登録する、という Configuration Manager がプロビジョニングする共同管理です。 もう 1 つは、Intune に登録してから Configuration Manager クライアントでインストールする、という Intune がプロビジョニングするデバイスで、共同管理状態を達成する方法です。

## <a name="prerequisites"></a>[前提条件]
共同管理を有効にする前に、次の前提条件が満たされている必要があります。 一般的な前提条件のほか、Configuration Manager クライアントがインストールされているデバイスとインストールされていないデバイスとで異なる前提条件があります。

> [!IMPORTANT]
> Windows 10 Mobile デバイスでは共同管理はサポートされません。

### <a name="general-prerequisites"></a>一般的な前提条件
共同管理を有効にするための一般的な前提条件は次のとおりです。  

- Configuration Manager バージョン 1710 以降
- Azure AD
- すべてのユーザーの EMS または Intune のライセンス
- [Azure AD の自動登録](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)が有効
- Intune のサブスクリプション &#40;MDM 機関が **Intune** に設定されたもの&#41;


   > [!Note]  
   > ハイブリッド MDM 環境 (Intune と Configuration Manager が統合された環境) では、共同管理を有効にできません。 Intune スタンドアロンへの移行については、[ハイブリッド MDM から Intune スタンドアロンへの移行の開始](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)に関する記事をご覧ください。

### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Configuration Manager クライアントがインストールされているデバイスの追加の前提条件
- Windows 10、バージョン 1709 (Fall Creators Update とも呼ばれます) 以降
- [ハイブリッド Azure AD への参加](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (AD と Azure AD に参加)

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Configuration Manager クライアントがインストールされていないデバイスの追加の前提条件
- Windows 10、バージョン 1709 (Fall Creators Update とも呼ばれます) 以降
- Configuration Manager の[クラウド管理ゲートウェイ](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) (Intune を使用して Configuration Manager クライアントをインストールする場合)

## <a name="workloads-you-can-switch-to-intune"></a>Intune に切り替えることができるワークロード
共同管理を有効にした後も、Configuration Manager が引き続きすべてのワークロードを管理します。 準備ができたら、Intune で使用可能なワークロードの管理を始めることができます。 次のワークロードを Intune で管理できます。   

### <a name="compliance-policies"></a>コンプライアンス ポリシー
コンプライアンス ポリシーは、デバイスが条件付きアクセス ポリシーによって "準拠している" と見なされるために遵守する必要がある規則および設定を定義します。 コンプライアンス ポリシーを使用して、条件付きアクセスとは別に、デバイスのコンプライアンスに関する問題を監視および修復することもできます。 詳しくは、「[デバイス コンプライアンス ポリシー](/sccm/mdm/deploy-use/device-compliance-policies)」をご覧ください。  

### <a name="windows-update-for-business-policies"></a>Windows Update for Business ポリシー
Windows Update for Business ポリシーでは、Windows Update for Business によって直接管理されている Windows 10 デバイスの Windows 10 機能更新プログラムまたは品質更新プログラムに対し、遅延ポリシーを構成できます。 遅延については、「[Windows Update for Business 遅延ポリシーの構成](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)」をご覧ください。  

### <a name="resource-access-policies"></a>リソースのアクセス ポリシー
リソースのアクセス ポリシーで、デバイスに対する VPN、Wi-Fi、電子メール、および証明書の設定を構成します。 詳細については、[リソース アクセス プロファイルの展開](/sccm/protect/deploy-use/deploy-wifi-vpn-email-cert-profiles)に関するページを参照してください。

### <a name="endpoint-protection"></a>Endpoint Protection 
<!-- 1357365 -->
Configuration Manager 1802 以降では、Endpoint Protection のワークロードを Intune に移行することができます。 詳細については、[Intune に移行可能なワークロード](/sccm/core/clients/manage/co-management-switch-workloads.md#Workloads-able-to-be-transitioned-to-Intune)と[Configuration Manager の Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection) に関するページを参照してください。

## <a name="architectural-overview-for-co-management"></a>共同管理のアーキテクチャの概要
次の図では、共同管理のアーキテクチャの概要と、既存の構成および Intune インフラストラクチャに共同管理がどのように組み込まれるのかを示します。

![共同管理のアーキテクチャの図](./media/co-management-arch.svg)

## <a name="scenarios-to-enable-co-management"></a>共同管理を有効にするシナリオ  
Microsoft Intune に登録された Windows 10 デバイスと既存の Windows 10 Configuration Manager クライアントのどちらについても、共同管理を有効にすることができます。 どちらのシナリオでも、Windows 10 デバイスは Configuration Manager と Intune によって共同管理されるだけでなく、AD と Azure AD に参加します。  

### <a name="devices-enrolled-in-intune"></a>Intune に登録されたデバイス  
Windows 10 デバイスを Intune に登録したら、Configuration Manager クライアントを (特定のコマンドライン引数を使って) デバイスにインストールし、共同管理用にクライアントを準備できます。 その後、Configuration Manager コンソールから共同管理を有効にして、特定の Windows 10 デバイスの特定のワークロードを Intune に移動する作業を始めます。  

Windows 10 デバイスがまだ Intune に登録されていない場合は、Azure の自動登録を使って登録できます。 新しい Windows 10 デバイスの場合は、[Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) を使って、Intune にデバイスを登録する自動登録を含む Out of Box Experience (OOBE) を構成できます。  

### <a name="configuration-manager-clients"></a>Configuration Manager クライアント
Configuration Manager クライアントである Windows 10 デバイスの場合は、デバイスを登録して、Configuration Manager コンソールから共同管理を有効にできます。 Configuration Manager は、Azure AD テナントの情報に基づいて、Intune への自動登録をトリガーします。  


## <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>共同管理対象デバイスに対して Azure の Intune で利用できるリモート操作
Windows 10 デバイスの共同管理を有効にすると、Azure の Intune から次のリモート操作を実行できます。  
- [出荷時の設定に戻す](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [選択的ワイプ](https://docs.microsoft.com/intune/apps-selective-wipe)
- [デバイスの削除](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [デバイスの再起動](https://docs.microsoft.com/intune/device-restart)
- [新たに開始](https://docs.microsoft.com/intune/device-fresh-start)

## <a name="next-steps"></a>次のステップ
[共同管理用に Windows 10 デバイスを準備する](co-management-prepare.md)