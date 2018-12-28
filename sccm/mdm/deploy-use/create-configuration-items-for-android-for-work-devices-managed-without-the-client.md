---
title: Intune で管理されている Android for Work デバイスの構成項目を作成する方法
titleSuffix: Configuration Manager
ms.date: 2017-07-31
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ab6784fd-8c57-4be9-858f-50fe39f2ff5f
author: aczechowski
ms.author: aaroncz
ms.openlocfilehash: 0b2104b72a155f269beefc6f64c2615b62266b66
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415468"
---
# <a name="how-to-create-configuration-items-for-android-for-work-devices-managed-with-intune"></a>Intune で管理されている Android for Work デバイスの構成項目を作成する方法

 System Center Configuration Manager の **Android for Work** 構成項目を使って、Microsoft Intune に登録されているか、Configuration Manager によってオンプレミスで管理されている Android デバイスおよび Android for Work デバイスの設定を管理します。  

### <a name="to-create-an-android-for-work-configuration-item"></a>Android for Work の構成項目を作成するには  

1. Configuration Manager コンソールで、**[資産とコンプライアンス]** をクリックします。  

2. **[資産とコンプライアンス]** ワークスペースで **[コンプライアンス設定]** を展開して、**[構成項目]** をクリックします。  

3. **[ホーム]** タブの **[作成]** グループで、**[構成項目の作成]** をクリックします。  

4. **構成項目の作成ウィザード** の **[全般]** ページで、構成項目の名前と、必要に応じて説明を入力します。  

5. **[作成する構成項目の種類の指定]** で、**[Android for Work]** を選びます。  

6. Configuration Manager コンソールで構成項目を検索およびフィルター処理するのに役立つカテゴリを作成して割り当てる場合は、**[カテゴリ]** を選択します。  

   **[次へ]** をクリックします。

7. ウィザードの **[デバイスの設定]** ページで、構成する設定グループを選択します。 詳細については、「[Android for Work の構成項目設定のリファレンス](#android-for-work-configuration-item-settings-reference)」を参照してください。選択したら、**[次へ]** をクリックします。  

   > [!TIP]  
   >  必要な設定が一覧にない場合は、 **[既定の設定グループに含まれない追加の設定を構成する]** チェック ボックスをオンにします。  

8. 各設定ページで、必要な設定と、その設定がデバイスに対応していないときにその設定を修正するかどうかを構成します (これがサポートされている場合)。  

9. 設定グループごとに、構成項目が非対応であることが検出されたときに報告される重要度を構成することもできます。  

   -   **なし** - このコンプライアンス規則を満たしていないデバイスは、Configuration Manager レポート用に非対応重要度を何も報告しません。  

   -   **情報** - このコンプライアンス規則を満たしていないデバイスは、Configuration Manager レポート用に**情報**というレベルで非対応重要度を報告します。  

   -   **警告** - このコンプライアンス規則を満たしていないデバイスは、Configuration Manager レポート用に**警告**というレベルで非対応重要度を報告します。  

   -   **重大** - このコンプライアンス規則を満たしていないデバイスは、Configuration Manager レポート用に**重大**というレベルで非対応重要度を報告します。  

   -   **重大 (イベント)** - このコンプライアンス規則を満たしていないデバイスは、Configuration Manager レポート用に**重大**というレベルで非対応重要度を報告します。 重要度のレベルは、アプリケーションのイベント ログでも Windows のイベントとしてログが登録されます。  

10. ウィザードの **[プラットフォームの適用性]** ページで、前に選択したサポート対象プラットフォームと互換性がないすべての設定を確認します。 前に戻ってこれらの設定を削除するか、操作を続行できます。  

    > [!TIP]  
    >  サポートされていない設定のコンプライアンスは評価されません。  

11. ウィザードを完了します。  

    新しい構成項目は、 **[資産とコンプライアンス]** ワークスペースの **[構成項目]** ノードに表示されます。  

##  <a name="android-for-work-configuration-item-settings-reference"></a>Android for Work の構成項目設定のリファレンス  

### <a name="password"></a>パスワード  

|設定|詳細|  
|-------------|-------------|  
|**デバイスのパスワードの設定が必要**|サポート対象デバイスのパスワードが必要です。|  
|**パスワードの最小文字数**|パスワードの最小の長さ。|  
|**パスワードの有効期限 (日数)**|パスワードの変更が必要になるまでの日数。|  
|**記憶するパスワードの数**|最近使用したパスワードを再利用できないようにします。|  
|**デバイスをワイプするまでのログオン失敗回数**|ログインの試みがこの回数だけ失敗した場合は、デバイスがワイプされます。|  
|**デバイスをロックするまでのアイドル時間**|デバイスが使用されていない場合に、ロックされるまでの時間を選択します。|
|**パスワードの品質**|必要なレベルのパスワードの複雑さと、生体認証デバイスを使用できるかどうかを選択します。|  
|**Smart Lock と他の信頼のエージェントを許可する**|互換性のある Android デバイスで Smart Lock 機能が制御できるようになります。 信頼エージェントとも呼ばれるこの電話機能では、デバイスが特定の Bluetooth デバイスに接続したときや、NFC タグの近くにある場合など、信頼できる場所にある場合、デバイスのロック画面のパスワードを無効化またはバイパスすることができます。 この設定を使用して、エンド ユーザーが Smart Lock を構成することを禁止できます。|
|**ロック解除用の指紋**|&nbsp;|

###  <a name="work-profile"></a>仕事用プロファイル  
 これらの設定は、Samsung KNOX デバイスのみに適用されます。  

|設定の名前|詳細|  
|------------------|-------------|  
|**仕事用プロファイルと個人プロファイル間でのデータ共有を許可する**|次の中から選択します。<br>- **未構成**<br>- **既定の共有制限**<br>- **仕事用プロファイル内のアプリで、個人プロファイルからの共有要求の処理を許可する**<br>- **個人プロファイル内のアプリで、仕事用プロファイルからの共有要求の処理を許可する**<br><br>(カスタム URI を使用する「[コピーと貼り付け構成項目設定](#copy-paste-configuration-item-settings)」も参照してください)|  
|**デバイスがロックされているときに仕事用プロファイルの通知を表示しない (Android 6.0 以上)**||
|**アプリの既定のアクセス許可ポリシーを設定する (Android 6.0 以上)**|次の中から選択します。<br>- **未構成**<br>- **常に確認する**<br>- **自動許可**<br>- **自動拒否**|

### <a name="copy-paste-configuration-item-settings"></a>コピーと貼り付け構成項目設定
**[仕事用プロファイルと個人プロファイル間でのデータ共有を許可する]** オプションのいずれも、コピーと貼り付けの動作を禁止していません。 コピーと貼り付けを禁止するには、カスタム設定を使用して構成してください。 これはカスタム URI から設定できます。

- OMA-URI: ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- 値の種類:ブール型

DisallowCrossProfileCopyPaste を true に設定すると、Android for Work の個人プロファイルと仕事用プロファイル間でのコピー/貼り付け動作を防止します。

## <a name="see-also"></a>関連項目  
 [System Center Configuration Manager クライアントを使用せずに管理されているデバイスの構成項目](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
