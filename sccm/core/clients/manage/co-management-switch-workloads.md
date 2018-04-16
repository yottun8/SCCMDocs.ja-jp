---
title: Configuration Manager のワークロードを Intune に切り替える
titleSuffix: System Center Configuration Manager
description: Configuration Manager で現在管理されているワークロードを Microsoft Intune に切り替える方法について説明します。
ms.prod: configuration-manager
ms.suite: na
ms.technology:
- configmgr-client
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.service: ''
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: cdfe52768499b929db473ac08d42207059965ffd
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2018
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Configuration Manager のワークロードを Intune に切り替える
「[Prepare Windows 10 devices for co-management](co-management-prepare.md)」(共同管理用に Windows 10 デバイスを準備する) では、共同管理用に Windows 10 デバイスを準備しました。 これらのデバイスは AD、Azure AD に参加し、Intune に登録され、Configuration Manager クライアントがインストールされています。 Windows 10 デバイスが AD に参加し、Configuration Manager クライアントがインストールされていても、まだ Azure AD に参加していないか、Intune に登録されていない場合があります。 次の手順では、共同管理を有効にし、残りの Windows 10 デバイス (Intune に登録されていない Configuration Manager クライアント) を共同管理用に準備して、特定の Configuration Manager ワークロードの Intune への切り替えを開始できるようにします。

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

## <a name="modify-your-co-management-settings"></a>共同管理設定の変更
ウィザードを使用して共同管理を有効にした後に、共同管理のプロパティの設定を変更できます。  
- Configuration Manager コンソールで、**[管理]** > **[概要]** > **[クラウド サービス]** > **[Co-management]\(共同管理\)** の順に移動します。  
共同管理オブジェクトを選択してから、[ホーム] タブで **[プロパティ]** をクリックします。 

## <a name="workloads-able-to-be-transitioned-to-intune"></a>Intune に切り替えられるワークロード
特定のワークロードについては Intune に切り替えることができます。 ワークロードが切り替えられるようになったことに伴い、次の一覧は更新されます。
1. デバイス コンプライアンス ポリシー
2. リソースのアクセス ポリシー
3. Windows Update のポリシー
4. エンドポイント保護 (Configuration Manager バージョン 1802 以降)
      - Windows Defender ウイルス対策
      - Windows Defender Application Guard
      - Windows Defender ファイアウォール
      - Windows Defender SmartScreen
      - Windows 暗号化
      - Windows Defender Exploit Guard
      - Windows Defender Application Control
      - Windows Defender セキュリティ センター
      - Windows Defender Advanced Threat Protection



## <a name="monitor-co-management"></a>共同管理の監視
共同管理を有効にした後に、次の方法を使用して共同管理デバイスを監視できます。
- **SQL ビューと WMI クラス**: Configuration Manager サイト データベースの **v&#95;ClientCoManagementState** SQL ビュー、または **SMS&#95;Client&#95;ComanagementState** WMI クラスに対するクエリを実行できます。 WMI クラスの情報を使用して、共同管理の展開状態を判断するカスタム コレクションを Configuration Manager に作成することができます。 詳細については、[コレクションの作成方法](/sccm/core/clients/manage/collections/create-collections)に関するページを参照してください。 SQL ビューと WMI クラスでは次のフィールドを使用できます。 
    - **MachineId**: Configuration Manager クライアントの一意のデバイス ID を指定します。
    - **MDMEnrolled**: デバイスが MDM に登録されているかどうかを指定します。 
    - **Authority**: デバイスが登録されている機関を指定します。
    - **ComgmtPolicyPresent**: Configuration Manager の共同管理ポリシーがクライアントに存在するかどうかを指定します。 **MDMEnrolled** 値が **0** の場合、クライアントに共同管理ポリシーが存在するかどうかにかかわらず、デバイスは共同管理されていません。

   > [!Note]    
   > **MDMEnrolled** フィールドと **ComgmtPolicyPresent** フィールドの両方の値が **1** の場合、デバイスは共同管理されています。

- **展開ポリシー**: **[監視]** > **[展開]** で作成されたポリシーが 2 つあります。1 つはパイロット グループのためのポリシー、もう 1 つは運用のためのポリシーです。 これらのポリシーは、Configuration Manager がポリシーを適用したデバイス数のみをレポートします。 Intune に登録されているデバイス数は、デバイスを共同管理するための前提要件ですが、考慮されていません。  

## <a name="check-compliance-for-co-managed-devices"></a>共同管理されるデバイスのコンプライアンスの確認
条件付きアクセスが Configuration Manager と Intune のどちらで管理されている場合でも、ユーザーはソフトウェア センターを使用して共同管理対象 Windows 10 デバイスのコンプライアンスを確認できます。 条件付きアクセスが Intune で管理されている場合は、ポータル サイト アプリを使用してコンプライアンスを確認することもできます。

## <a name="next-steps"></a>次のステップ
次のリソースを使用して、Intune に切り替えるワークロードを管理できます。
- [デバイス コンプライアンス ポリシー](https://docs.microsoft.com/intune/device-compliance-get-started)
- [リソースのアクセス ポリシー](https://docs.microsoft.com/intune/device-profiles)
- [Windows Update for Business ポリシー](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Microsoft Intune の Endpoint Protection](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
