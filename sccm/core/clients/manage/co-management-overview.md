---
title: Windows 10 デバイスの共同管理
titleSuffix: Configuration Manager
description: Configuration Manager と Microsoft Intune の両方を使用して Windows 10 デバイスを同時に管理する方法について説明します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 1791217e22e2bcc6d5fd2603abee3aaced816afe
ms.sourcegitcommit: 1f8731ed8f0308cb2cb576722adb0821a366e9ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2018
ms.locfileid: "51223740"
---
# <a name="co-management-for-windows-10-devices"></a>Windows 10 デバイスの共同管理    

以前の Windows 10 の更新プログラムで、Windows 10 デバイスをオンプレミスの Active Directory (AD) とクラウドベースの Azure AD に同時に結合できるようになっています (ハイブリッド Azure AD)。 Configuration Manager バージョン 1710 以降の共同管理では、この機能強化が利用されています。 共同管理により、Configuration Manager と Intune の両方を使用して Windows 10 バージョン 1709 のデバイスを同時に管理することができます。 <!-- 1350871 -->


## <a name="why-co-management"></a>共同管理の理由

多くのユーザーは、モバイル デバイスを管理する場合と同じ低コストで簡単なクラウド ベースのソリューションを使って、Windows 10 デバイスを管理することを望んでいます。 ただし、従来の管理から最新の管理への移行は困難な場合があります。  


## <a name="what-is-co-management"></a>共同管理とは

共同管理により、Configuration Manager と Intune の両方を使用して Windows 10 デバイスを同時に管理することができます。 これは、従来の管理から最新の管理への橋渡しとなるソリューションであり、段階的なアプローチを使って移行する方向を提示します。


## <a name="benefits"></a>メリット 

以下の Intune 機能をすぐに使用できます。  
 
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
    - [エンドポイント保護](https://docs.microsoft.com/intune/endpoint-protection-windows-10) (Configuration Manager 1802 以降) <!-- 1357365 -->
    - [デバイス構成](https://docs.microsoft.com/intune/device-profile-create) (Configuration Manager 1806 以降) <!-- 1357903 -->
    - [Office クイック実行アプリ](https://docs.microsoft.com/intune/apps-add-office365) (Configuration Manager 1806 以降)<!--1357841-->
    - [モバイル アプリ](https://docs.microsoft.com/intune/app-management) (プレリリース機能として Configuration Manager 1806 以降) <!--1357892-->



## <a name="how-to-configure-co-management"></a>共同管理の構成方法

 共同管理を達成するには、主に 2 つのパスがあります。  

   - Configuration Manager が共同管理をプロビジョニングする: 構成マネージャー クライアントを既にインストールしてある Azure AD 参加済み Windows 10 デバイスを Intune に登録します。  

   - Intune でプロビジョニングする: Intune に既に登録されているデバイスの場合、構成マネージャー クライアントをインストールして共同管理状態にします。 


### <a name="configuration-manager"></a>Configuration Manager

 -  Configuration Manager バージョン 1710 以降へのアップグレード。


### <a name="azure-active-directory"></a>Azure Active Directory

 - Windows 10 デバイスは、Azure AD に参加している必要があります。 次のいずれかの種類です。  

     - [Hybrid Azure AD 参加済み](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup): デバイスがオンプレミスの Active Directory に参加し、Azure Active Directory に登録されている場合。

     - Azure AD のみに参加。 (このタイプは "クラウド ドメイン参加済み" とも呼ばれます)<!--SCCMDocs issue 605-->

 - [Windows 10 の自動登録の有効化](https://docs.microsoft.com/intune/windows-enroll)。  


### <a name="intune"></a>Intune

 - [Intune サブスクリプションのセットアップ方法](/sccm/mdm/deploy-use/configure-intune-subscription)または [Intune のセットアップ](/intune/setup-steps)  

 - [ハイブリッド MDM から Intune スタンドアロンへの移行を開始する](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  

 > [!Note]  
 > ハイブリッド MDM 環境 (Intune と Configuration Manager が統合された環境) では、共同管理を有効にできません。 ただし、Intune スタンドアロンへのユーザー移行を開始し、関連 Windows 10 デバイスの共同管理を有効にできます。 Intune スタンドアロンへの移行については、[ハイブリッド MDM から Intune スタンドアロンへの移行の開始](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)に関する記事をご覧ください。  


### <a name="enable-co-management"></a>共同管理を有効にする 

 > [!Important]  
 > バージョン 1802 以降で共同管理を有効にするには、Configuration Manager での管理ユーザー アカウントが、**すべて**のセキュリティ スコープの**完全な権限を持つ管理者**である必要があります。 詳細については、「[ロール ベース管理の基礎](/sccm/core/understand/fundamentals-of-role-based-administration)」を参照してください。<!--SCCMDoc issue 626-->  

 Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[Cloud Services]** を展開して **[共同管理]** を選択します。 リボンの **[共同管理の構成]** をクリックし、**共同管理オンボード ウィザード**を開きます。 
   
1. **[サブスクリプション]** ページで **[サインイン]** をクリックします。 Intune テナントにサインインし、**[次へ]** をクリックします。  

    > [!Tip]   
    > テナントへのサインインに使用されたアカウントに Intune ライセンスが割り当てられていることを確認してください。割り当てられていない場合は失敗し、"User not recognized" (ユーザーが認識されません) というエラー メッセージが表示されます。  

2. **[有効化]** ページで **[Automatic enrollment into Intune]\(Intune への自動登録\)** 設定を選択します。 必要な場合には、Intune に既に登録されているデバイスのコマンド ラインをコピーします。  

    > [!Note]  
    > バージョン 1806 以降では、すべてのクライアントの自動登録がすぐに行われるのではありません。 この動作は、大規模な環境に対する登録のスケーリング向上に役立ちます。 Configuration Manager は、クライアントの数に基づいて登録をランダム化します。 たとえば、環境に 100,000 のクライアントがある場合、この設定を有効にすると、登録は数日間にわたって行われます。<!--1358003-->  

3. **[ワークロード]** ページで、各ワークロードについて、Intune による管理のために移動するデバイス グループを選択します。  

4. **[ステージング]** ページで、**[パイロット コレクション]** にするデバイス コレクションを選択します。 **[概要]** を確認して、ウィザードを完了します。  


### <a name="upgrade-windows-10-client"></a>Windows 10 クライアントをアップグレードする

- [Windows 10 バージョン 1709 (Fall Creators Update とも呼ばれる) 以降](/sccm/osd/deploy-use/manage-windows-as-a-service)にアップグレードします。


### <a name="configure-workloads-to-switch-to-intune"></a>ワークロードの Intune への切り替えを構成する 

[ワークロードの Intune への移行](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)に関する記事では、特定の Configuration Manager ワークロードを Intune に切り替える方法を説明しています。 この記事では、移行されるワークロードのデバイス グループの変更についても説明しています。

#### <a name="compliance-policies"></a>コンプライアンス ポリシー 
コンプライアンス ポリシーは、デバイスが条件付きアクセス ポリシーによって "準拠している" と見なされるために遵守する必要がある規則および設定を定義します。 また、コンプライアンス ポリシーを使用して、条件付きアクセスとは別に、デバイスのコンプライアンスに関する問題を監視および修復します。 詳しくは、「[デバイス コンプライアンス ポリシー](https://docs.microsoft.com/intune/device-compliance-get-started)」をご覧ください。  

#### <a name="windows-update-policies"></a>Windows Update のポリシー
Windows Update for Business ポリシーでは、Windows Update for Business によって直接管理されている Windows 10 デバイスの Windows 10 機能更新プログラムまたは品質更新プログラムに対し、遅延ポリシーを構成できます。 遅延については、「[Windows Update for Business 遅延ポリシーの構成](https://docs.microsoft.com/intune/windows-update-for-business-configure)」をご覧ください。  

#### <a name="resource-access-policies"></a>リソースのアクセス ポリシー
リソースのアクセス ポリシーで、デバイスに対する VPN、Wi-Fi、電子メール、および証明書の設定を構成します。 詳細については、[リソース アクセス プロファイルの展開](https://docs.microsoft.com/intune/device-profiles)に関するページを参照してください。

#### <a name="endpoint-protection"></a>Endpoint Protection
Configuration Manager 1802 以降では、Endpoint Protection のワークロードを Intune に移行することができます。 詳細については、[Microsoft Intune での Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10)<!-- 1357365 --> に関する記事と[ワークロードの Intune への移行](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)に関する記事をご覧ください。

#### <a name="device-configuration"></a>デバイスの構成
Configuration Manager 1806 以降では、デバイスの構成ワークロードを Intune に移行することができます。 詳しくは、「[Microsoft Intune でのデバイス プロファイルの作成](https://docs.microsoft.com/intune/device-profile-create)」および「[Intune に切り替えられるワークロード](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)」をご覧ください。  <!--1357903-->

#### <a name="office-click-to-run-apps"></a>Office クイック実行アプリ
Configuration Manager 1806 以降では、Office 365 のワークロードを Intune に移行することができます。 詳細については、「[Intune に切り替えられるワークロード](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)」を参照してください。 <!--1357841-->

#### <a name="mobile-apps"></a>モバイル アプリ
Configuration Manager バージョン 1806 以降では、モバイル アプリのワークロードを Intune に移行することができます。 この機能はプレリリース版の機能です。 これを有効にする場合は、「[プレリリース機能](/sccm/core/servers/manage/pre-release-features)」を参照してください。 このワークロードを移行すると、Intune から展開された使用可能なアプリが、すべてポータル サイトで使用可能になります。 Configuration Manager から展開するアプリは、ソフトウェア センターで使用できます。<!--1357892-->


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Intune に登録されたデバイスに Configuration Manager クライアントをインストールする

Windows 10 デバイスを Intune に登録したら、構成マネージャー クライアントを[特定のコマンドラインを使って](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)デバイスにインストールし、共同管理用にクライアントを準備します。 その後、Configuration Manager コンソールから共同管理を有効にして、特定の Windows 10 デバイスの特定のワークロードを Intune に移動する作業を始めます。
Windows 10 デバイスがまだ Intune に登録されていない場合は、Azure の自動登録を使って登録します。 新しい Windows 10 デバイスの場合は、[Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) を使って、Intune にデバイスを登録する自動登録を含む Out of Box Experience (OOBE) を構成します。

Intune を使って構成マネージャー クライアントをインストールするときは、Configuration Manager で[クラウド管理ゲートウェイ](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway)を有効にします。



## <a name="monitor-co-management"></a>共同管理の監視

[共同管理ダッシュボード](/sccm/core/clients/manage/co-management-dashboard)を利用すれば、お使いの環境で共同管理しているコンピューターを確認できます。 各種グラフを見ることで、対処が必要なデバイスを特定できます。



## <a name="next-steps"></a>次のステップ

[共同管理用に Windows 10 デバイスを準備する](co-management-prepare.md)
