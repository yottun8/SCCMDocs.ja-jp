---
title: Configuration Manager のワークロードを Intune に切り替える
titleSuffix: Configuration Manager
description: Configuration Manager で現在管理されているワークロードを Microsoft Intune に切り替える方法について説明します。
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 739773e83213033103b414cc9bb79f7abccb230c
ms.sourcegitcommit: 2cc635835709fb8d86cdb63ea34233b36c94d4d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2018
ms.locfileid: "52258946"
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Configuration Manager のワークロードを Intune に切り替える
「[Prepare Windows 10 devices for co-management](co-management-prepare.md)」(共同管理用に Windows 10 デバイスを準備する) では、共同管理用に Windows 10 デバイスを準備しました。 これらのデバイスは AD、Azure AD に参加し、Intune に登録され、Configuration Manager クライアントがインストールされています。 Windows 10 デバイスが AD に参加し、Configuration Manager クライアントがインストールされていても、まだ Azure AD に参加していないか、Intune に登録されていない場合があります。 次の手順では、共同管理を有効にし、残りの Windows 10 デバイス (Intune に登録されていない Configuration Manager クライアント) を共同管理用に準備して、特定の Configuration Manager ワークロードの Intune への切り替えを開始できるようにします。


## <a name="switch-configuration-manager-workloads-to-intune"></a>Configuration Manager のワークロードを Intune に切り替える

1. Configuration Manager コンソールで、**[管理]** > **[概要]** > **[クラウド サービス]** > **[Co-management]\(共同管理\)** の順に移動します。    
2. [ホーム] タブの [管理] グループで、 **[Configure co-management]\(共同管理の構成\)** を選択して Co-management Configuration Wizard \(共同管理の構成ウィザード\) を開きます。    
3. [サブスクリプション] ページで **[サインイン]** をクリックして Intune テナントにサインインし、**[次へ]** をクリックします。   
4. [Enablement]\(有効化\) ページで、**[パイロット]** または **[すべて]** を選択して Intune での自動登録を有効にし、**[次へ]** をクリックします。 **[パイロット]** を選ぶと、パイロット グループのメンバーである Configuration manager クライアントのみが Intune に自動的に登録されます。 このオプションにより、クライアントのサブセットで共同管理を有効にして初期テストを行ってから、段階的アプローチでロールアウトできます。 デバイス用の Intune のアプリが Intune に既に登録されている場合、Configuration Manager クライアントの展開にコマンド ラインを使用できます。 詳細については、「[Windows 10 devices enrolled in Intune](co-management-prepare.md#windows-10-devices-enrolled-in-intune)」(Intune に登録されている Windows 10 デバイス) を参照してください。
5. [Workloads]\(ワークロード\) ページで、Configuration Manager のワークロードを切り替える先として Pilot Intune または Intune による管理を選択し、**[次へ]** をクリックします。 **[Pilot Intune]\(Pilot Intune\)** 設定を選択すると、パイロット グループのデバイスの場合にのみ、関連するワークロードを切り替えます。 **[Intune]** 設定を選択すると、共同管理されているすべての Windows 10 デバイスについて関連するワークロードを切り替えます。 
        
   > [!Important]    
   > ワークロードを切り替える前に、Intune の対応するワークロードの構成と展開が適切に行われていることを確認します。 そうすることで、デバイス用の管理ツールのいずれかでワークロードが常に管理されていることを確認します。   
1. [ステージング] ページで、次の設定を構成した後、**[次へ]** をクリックします。
    - **パイロット**: パイロット グループには、選択した 1 つまたは複数のコレクションが含まれます。 共同管理の段階的なロールアウトの一部としてこのグループを使います。 小規模なテスト コレクションで開始し、共同管理をロールアウトするユーザーとデバイスを増やしながら、パイロット グループにコレクションを追加します。 パイロット グループのコレクションは共同管理のプロパティからいつでも変更できます。
    - **運用**: 1 つまたは複数のコレクションで **[Exclusion group]\(除外グループ\)** を構成します。 このグループのいずれかのコレクションのメンバーであるデバイスは、共同管理から除外されます。 
2. 共同管理を有効にするには、ウィザードを終了します。  

<!--1357377--> Configuration Manager バージョン 1806 以降では、共同管理ワークロードを切り替えるときに、共同管理されたデバイスで自動的に Microsoft Intune から MDM ポリシーが同期されます。 この同期は、Configuration Manager コンソールのクライアント通知から**コンピューター ポリシーのダウンロード**操作を開始するときにも行われます。 詳細については、「[クライアント通知を使用してクライアント ポリシーの取得を開始する](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification)」を参照してください。

## <a name="modify-your-co-management-settings"></a>共同管理設定の変更
ウィザードを使用して共同管理を有効にした後に、共同管理のプロパティの設定を変更できます。  
- Configuration Manager コンソールで、**[管理]** > **[概要]** > **[クラウド サービス]** > **[Co-management]\(共同管理\)** の順に移動します。  
共同管理オブジェクトを選択してから、[ホーム] タブで **[プロパティ]** をクリックします。 

## <a name="workloads-able-to-be-transitioned-to-intune"></a>Intune に切り替えられるワークロード
特定のワークロードについては Intune に切り替えることができます。 ワークロードが切り替えられるようになったことに伴い、次の一覧は更新されます。
1. デバイス コンプライアンス ポリシー
2. リソース アクセス ポリシー: リソースのアクセス ポリシーで、デバイスに対する VPN、Wi-Fi、電子メール、および証明書の設定を構成します。 詳細については、[リソース アクセス プロファイルの展開](https://docs.microsoft.com/intune/device-profiles)に関するページを参照してください。
      - 電子メールのプロファイル
      - Wi-Fi プロファイル
      - VPN プロファイル
      - 証明書プロファイル
3. Windows Update のポリシー
4. エンドポイント保護 (Configuration Manager バージョン 1802 以降)
      - Windows Defender Application Guard
      - Windows Defender ファイアウォール
      - Windows Defender SmartScreen
      - Windows 暗号化
      - Windows Defender Exploit Guard
      - Windows Defender Application Control
      - Windows Defender セキュリティ センター
      - Windows Defender Advanced Threat Protection
      - Windows Information Protection

5. デバイス構成 (Configuration Manager バージョン 1806 以降) <!--1357903-->
       - バージョン 1806 以降では、デバイス構成ワークロードを移動すると、**リソース アクセス** ワークロードと **Endpoint Protection** ワークロードも移動されます。
       - バージョン 1806 以降では、Intune がデバイス構成機関であっても、Configuration Manager から共同管理デバイスに引き続き設定を展開できます。 この例外は、組織で必要とされる設定を構成するために使用できるかもしれませんが、Intune ではまだ利用できません。 この例外は、[Configuration Manager の構成基準](/sccm/compliance/deploy-use/create-configuration-baselines.md)で指定します。 ベースラインを作成するとき、または既存のベースラインのプロパティの **[全般]** タブ上で、**[Always apply this baseline even for co-managed clients]\(共同管理クライアントにもこのベースラインを常に適用する\)** のオプションを有効にします。
6. Office 365 クイック実行 アプリ (Configuration Manager バージョン 1806 以降) <!--1357841-->
       - ワークロードを移動した後は、デバイスの **Intune ポータル サイト**にアプリが表示されます。
       - デバイスが再起動されない場合、Office 更新プログラムがクライアントに表示されるまでに約 24 時間かかる場合があります。 
       - **Office 365 アプリケーションがデバイス上の Intune で管理されているか**という新しいグローバル条件があります。 この条件は、新しい Office 365 アプリケーションの要件として既定で追加されます。 このワークロードを移行すると、共同管理されたクライアントでアプリケーションの要件が満たされなくなるため、Configuration Manager で展開される Office 365 がインストールされません。
7. モバイル アプリ ([プレリリース機能](/sccm/core/servers/manage/pre-release-features)として Configuration Manager バージョン 1806 以降) <!--1357892-->
      - このワークロードを移行すると、Intune から展開された使用可能なアプリが、すべてポータル サイトで使用可能になります。 
      -  Configuration Manager から展開するアプリは、ソフトウェア センターで使用できます。

## <a name="monitor-co-management"></a>共同管理の監視
共同管理を有効にした後に、次の方法を使用して共同管理デバイスを監視できます。

- [共同管理ダッシュボード](/sccm/core/clients/manage/co-management-dashboard)
- **SQL ビューと WMI クラス**: Configuration Manager サイト データベースの **v&#95;ClientCoManagementState** SQL ビュー、または **SMS&#95;Client&#95;ComanagementState** WMI クラスに対するクエリを実行できます。 WMI クラスの情報を使用して、共同管理の展開状態を判断するカスタム コレクションを Configuration Manager に作成することができます。 詳細については、[コレクションの作成方法](/sccm/core/clients/manage/collections/create-collections)に関するページを参照してください。 SQL ビューと WMI クラスでは次のフィールドを使用できます。 
    - **MachineId**: Configuration Manager クライアントの一意のデバイス ID を指定します。
    - **MDMEnrolled**: デバイスが MDM に登録されているかどうかを指定します。 
    - **Authority**: デバイスが登録されている機関を指定します。
    - **ComgmtPolicyPresent**: Configuration Manager の共同管理ポリシーがクライアントに存在するかどうかを指定します。 **MDMEnrolled** の値が **0** の場合、デバイスは クライアントに共同管理ポリシーが存在するかどうかにかかわらず共同管理されていません。

   > [!Note]    
   > **MDMEnrolled** フィールドと **ComgmtPolicyPresent** フィールドの両方の値が **1** の場合、デバイスは共同管理されています。

- **展開ポリシー**: **[監視]** > **[展開]** で 2 つのポリシーが作成されます。1 つはパイロット グループ用で、もう 1 つは運用のためのものです。 これらのポリシーは、Configuration Manager がポリシーを適用したデバイス数のみをレポートします。 Intune に登録されているデバイス数は、デバイスを共同管理するための前提要件ですが、考慮されていません。  

## <a name="check-compliance-for-co-managed-devices"></a>共同管理されるデバイスのコンプライアンスの確認
条件付きアクセスが Configuration Manager と Intune のどちらで管理されていても、ユーザーはソフトウェア センターを使用して、共同管理対象 Windows 10 デバイスのコンプライアンスを確認できます。 条件付きアクセスが Intune で管理されている場合は、ポータル サイト アプリを使用してコンプライアンスを確認することもできます。

## <a name="next-steps"></a>次のステップ
次のリソースを使用して、Intune に切り替えるワークロードを管理できます。
- [デバイス コンプライアンス ポリシー](https://docs.microsoft.com/intune/device-compliance-get-started)
- [リソースのアクセス ポリシー](https://docs.microsoft.com/intune/device-profiles)
- [Windows Update for Business ポリシー](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Microsoft Intune の Endpoint Protection](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
