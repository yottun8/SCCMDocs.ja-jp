---
title: Windows 10 デバイスの共同管理
titleSuffix: Configuration Manager
description: Configuration Manager と Microsoft Intune の両方を使用して Windows 10 デバイスを同時に管理する方法について説明します。
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/28/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 3d7ca4bb72f6f3f76855faac125385374347ba55
ms.sourcegitcommit: d67c6246bb6027cd5501e772b0521f9272407c28
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2018
---
# <a name="co-management-for-windows-10-devices"></a>Windows 10 デバイスの共同管理    
 以前の Windows 10 の更新プログラムで、Windows 10 デバイスをオンプレミスの Active Directory (AD) とクラウドベースの Azure AD に同時に結合できるようになっています (ハイブリッド Azure AD)。 Configuration Manager バージョン 1710 以降、共同管理ではこの機能強化を活用し、Configuration Manager と Intune の両方を使用して複数の Windows 10 バージョン 1709 デバイスを同時に管理できるようになりました。 <!-- 1350871 -->
## <a name="why-co-management"></a>共同管理の理由
多くのユーザーは、モバイル デバイスを管理する場合と同じ低コストで簡単なクラウド ベースのソリューションを使って、Windows 10 デバイスを管理することを望んでいます。 ただし、従来の管理から最新の管理への移行は困難な場合があります。  
## <a name="what-is-co-management"></a>共同管理とは
共同管理により、Configuration Manager と Intune の両方を使用して Windows 10 デバイスを同時に管理することができます。 これは、従来の管理から最新の管理への橋渡しとなるソリューションであり、段階的なアプローチを使って移行する方向を提示します。

## <a name="benefits"></a>メリット 
- Intune 機能をすぐに使用できる 
    - リモート操作
        - [出荷時の設定に戻す](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
        - [選択的ワイプ](https://docs.microsoft.com/intune/apps-selective-wipe)
        - [デバイスの削除](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
        - [デバイスの再起動](https://docs.microsoft.com/intune/device-restart)
        - [新たに開始](https://docs.microsoft.com/intune/device-fresh-start)
    - 次のワークロードでの Intune とのオーケストレーション:
        - [コンプライアンス ポリシー](https://docs.microsoft.com/intune/device-compliance-get-started)
        - [リソースのアクセス ポリシー](https://docs.microsoft.com/intune/device-profiles)
        - [Windows Update のポリシー](https://docs.microsoft.com/intune/windows-update-for-business-configure)
        - [エンドポイント保護](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10) (Configuration Manager 1802 以降) <!-- 1357365 -->
    
## <a name="how-to-configure-co-management"></a>共同管理の構成方法
共同管理を達成するには、主に 2 つのパスがあります。 1 つは、Configuration Manager の管理対象でハイブリッド Azure AD 参加済みの Windows 10 デバイスを Intune に登録する、という Configuration Manager がプロビジョニングする共同管理です。 もう 1 つは、Intune に登録してから Configuration Manager クライアントでインストールする、という Intune がプロビジョニングするデバイスで、共同管理状態を達成する方法です。

### <a name="configuration-manager"></a>**Configuration Manager**
 -  Configuration Manager バージョン 1710 以降へのアップグレード。


### <a name="azure-active-directory"></a>**Azure Active Directory**
  - [ハイブリッド Azure AD への参加](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (AD と Azure AD に参加)。
  - [Windows 10 の自動登録の有効化。](https://docs.microsoft.com/intune/windows-enroll)


### <a name="intune"></a>**Intune**
 - [Intune サブスクリプションのセットアップ方法。](/sccm/mdm/deploy-use/configure-intune-subscription) すなわち、https://docs.microsoft.com/en-us/intune/setup-steps
 - [ハイブリッド MDM から Intune スタンドアロンへの移行を開始。](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)


### <a name="enable-co-management"></a>共同管理を有効にする 
 Configuration Manager コンソールで、**[管理]** > **[概要]** > **[クラウド サービス]** > **[Co-management]\(共同管理\)** の順に移動します。 リボンから  **[Configure co-management]\(共同管理の構成\)** を選んで、**共同管理オンボード ウィザード**を開きます。 
   
1. **[サブスクリプション]** ページで **[サインイン]** をクリックして Intune テナントにサインインし、**[次へ]** をクリックします。    
2. **[Enablement]\(有効化\)** ページで **[Automatic enrollment into Intune]\(Intune への自動登録\)** 設定を選択します。 必要な場合には、Intune に既に登録されているデバイスのコマンド ラインをコピーします。 
3. **[ワークロード]** ページで、各ワークロードについて、Intune による管理のために移動するデバイス グループを選択します。
4. **[ステージング]** ページで、**[パイロット コレクション]** にするデバイス コレクションを選択します。 **[概要]** を確認して、ウィザードを完了します。 

### <a name="upgrade-windows-10-client"></a>Windows 10 クライアントをアップグレードする
- [Windows 10 バージョン 1709 (Fall Creators Update とも呼ばれる) 以降](/sccm/osd/deploy-use/manage-windows-as-a-service)にアップグレードします。

### <a name="configure-workloads-to-switch-to-intune"></a>ワークロードの Intune への切り替えを構成する 
[ワークロードの Intune への移行](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)に関する記事では、特定の Configuration Manager ワークロードを Intune に切り替える方法を説明しています。 この記事では、移行されるワークロードのデバイス グループの変更についても説明しています。

- **コンプライアンス ポリシー:** コンプライアンス ポリシーは、デバイスが条件付きアクセス ポリシーによって "準拠している" と見なされるために遵守する必要がある規則および設定を定義します。 コンプライアンス ポリシーを使用して、条件付きアクセスとは別に、デバイスのコンプライアンスに関する問題を監視および修復することもできます。 詳しくは、「[デバイス コンプライアンス ポリシー](https://docs.microsoft.com/intune/device-compliance-get-started)」をご覧ください。  

- **Windows Update ポリシー:** Windows Update for Business ポリシーでは、Windows Update for Business によって直接管理されている Windows 10 デバイスの Windows 10 機能更新プログラムまたは品質更新プログラムに対し、遅延ポリシーを構成できます。 遅延については、「[Windows Update for Business 遅延ポリシーの構成](https://docs.microsoft.com/intune/windows-update-for-business-configure)」をご覧ください。  

- **リソース アクセス ポリシー:** リソースのアクセス ポリシーで、デバイスに対する VPN、Wi-Fi、電子メール、および証明書の設定を構成します。 詳細については、[リソース アクセス プロファイルの展開](https://docs.microsoft.com/intune/device-profiles)に関するページを参照してください。

- **Endpoint Protection:** Configuration Manager 1802 以降では、Endpoint Protection のワークロードを Intune に移行することができます。 詳細については、[Microsoft Intune での Endpoint Protection](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10)<!-- 1357365 --> に関する記事と [ワークロードの Intune への移行](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)に関する記事をご覧ください。


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Intune に登録されたデバイスに Configuration Manager クライアントをインストールする
Windows 10 デバイスを Intune に登録したら、Configuration Manager クライアントを ([特定のコマンドライン引数を使って](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)) デバイスにインストールし、共同管理用にクライアントを準備できます。 その後、Configuration Manager コンソールから共同管理を有効にして、特定の Windows 10 デバイスの特定のワークロードを Intune に移動する作業を始めます。
Windows 10 デバイスがまだ Intune に登録されていない場合は、Azure の自動登録を使って登録できます。 新しい Windows 10 デバイスの場合は、[Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) を使って、Intune にデバイスを登録する自動登録を含む Out of Box Experience (OOBE) を構成できます。
 - Configuration Manager の[クラウド管理ゲートウェイ](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) を有効にします (Intune を使用して Configuration Manager クライアントをインストールする場合のみ)。

## <a name="monitor-co-management"></a>共同管理の監視
[共同管理ダッシュボード](/sccm/core/clients/manage/co-management-dashboard)を利用すれば、お使いの環境で共同管理しているコンピューターを確認できます。 各種グラフを見ることで、対処が必要なデバイスを特定できます。


## <a name="next-steps"></a>次のステップ
[共同管理用に Windows 10 デバイスを準備する](co-management-prepare.md)
