---
title: "System Center Configuration Manager クライアントが実行されていないデバイスのコンプライアンスを管理するための一般的なタスク | System Center Configuration Manager"
description: "いくつかの一般的なシナリオを使用して、System Center Configuration Manager のコンプライアンス設定について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 116cca2a-0a98-43fd-ac9e-e3daeddefce3
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f69250fbe51ea8902a0446a613d66be390ea7434


---
# <a name="common-tasks-for-managing-compliance-on-devices-not-running-the-system-center-configuration-manager-client"></a>System Center Configuration Manager クライアントが実行されていないデバイスのコンプライアンスを管理するための一般的なタスク

*適用対象: System Center Configuration Manager (Current Branch)*

以下のシナリオでは、一般的なシナリオに従って作業することで、System Center Configuration Manager コンプライアンス設定を使用する方法の概要を説明します。  

 「[System Center Configuration Manager クライアントを使用せずに管理されているデバイスの構成項目](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)」には、コンプライアンス設定に関する知識を既にお持ちの方を対象とした、使用するすべての機能に関する詳細なドキュメントが記載されています。  

 作業を開始する前に、「[コンプライアンス設定を使ってみる](../../compliance/get-started/get-started-with-compliance-settings.md)」をお読みになり、いくつかの基本的なコンプライアンス設定を確認してください。また、[コンプライアンス設定の計画と構成](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)に関するページをお読みになり、必要な前提条件の実装方法をご確認してください。  

## <a name="general-information-for-each-scenario"></a>各シナリオ共通の情報  
 各シナリオでは、特定のタスクを実行する構成項目を作成します。 構成項目の作成ウィザードを開き、次の手順に従います。  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[構成項目]** の順にクリックします。  

3.  [ホーム **** ] タブの [作成 **** ] グループで、[構成項目の作成 ****] をクリックします。  

4.  次のように構成項目の作成ウィザードの **[全般]** タブで、構成項目の名前と説明を指定し、このトピックの各シナリオに適した構成項目の種類を選択します。  

     ![構成項目の作成ウィザードの全般ページが表示されます。](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-81-and-windows-10-devices-managed-without-the-configuration-manager-client"></a>Configuration Manager クライアントを使用せずに管理されている Windows 8.1 および Windows 10 デバイスのシナリオ  

### <a name="scenario-restrict-access-to-the-app-store-on-all-windows-pcs"></a>シナリオ: すべての Windows PC でアプリ ストアへのアクセスを制限する  
 このシナリオでは、あなたは機密性の高い情報を処理する会社の IT 管理者です。 このため、ユーザーがインストールできるアプリを制限します。 Windows 10 PC のすべてのユーザーについて、Windows ストアからのアプリのダウンロードを禁止するために、次の操作を実行します。  

#### <a name="steps"></a>手順  

1.  構成項目の作成ウィザードの **[全般]** ページで、構成項目の種類として **[Windows 8.1 および Windows 10]** を選択し、 **[次へ]**をクリックします。  

2.  **[サポートされているプラットフォーム]** ページで、すべての Windows 10 プラットフォームを選択します。  

3.  **[デバイス設定]** ページで、 **[ストア]**を選択し、 **[次へ]**をクリックします。  

4.  **[ストア]** ページで、 **[アプリケーション ストア]** の値として **[禁止]**を選択します。  

5.  **[対応していない設定を修復する]** を選択して、変更がすべての PC に確実に適用されるようにします。  

6.  ウィザードを完了して構成項目を作成します。  

 これで、「[構成基準の作成と展開に関する一般的なタスク](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)」トピックの情報を使用して、作成した構成をデバイスに簡単に展開できるようになります。  

## <a name="scenarios-for-windows-phone-devices-managed-without-the-configuration-manager-client"></a>Configuration Manager クライアントを使用せずに管理されている Windows Phone デバイスのシナリオ  

### <a name="scenario-disable-the-use-of-screen-capture-on-a-windows-phone"></a>シナリオ: Windows Phone で画面のキャプチャの使用を無効にする  
 このシナリオでは、会社で Windows Phone 8.1 デバイスを使用します。 これらのデバイスでは、機密情報を含む販売アプリを実行します。 会社を保護するため、会社の外部への機密情報の送信に使用される可能性がある、デバイスの画面のキャプチャを使用できないようにします。  

1.  構成項目の作成ウィザードの **[全般]** ページで、構成項目の種類として **[Windows Phone]** を選択し、 **[次へ]**をクリックします。  

2.  **[サポートされているプラットフォーム]** ページで、**[すべての Windows Phone 8.1]** プラットフォームを選択します。  

3.  **[デバイス設定]** ページで、 **[デバイス]**を選択し、 **[次へ]**をクリックします。  

4.  **[デバイス]** ページで、 **[画面の取り込み]** の値として **[無効]**を選択します。  

5.  **[対応していない設定を修復する]** を選択して、変更がすべての Windows Phone 8.1 デバイスに確実に適用されるようにします。  

6.  ウィザードを完了して構成項目を作成します。  

 これで、「[System Center Configuration Manager での構成基準の作成と展開に関する一般的なタスク](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)」トピックの情報を使用して、作成した構成をデバイスに簡単に展開できるようになります。  

## <a name="scenarios-for-ios-and-mac-os-x-devices-managed-without-the-configuration-manager-client"></a>Configuration Manager クライアントを使用せずに管理されている iOS および Mac OS X デバイスのシナリオ  

### <a name="scenario-disable-the-camera-on-ios-devices"></a>シナリオ: iOS デバイスでカメラを無効にする  
 このシナリオでは、会社は、新しい製品デザインのための設計図を作成しています。 ここには、漏えいしてはならない機密情報が含まれています。 会社ではすべての従業員に iPhone または iPad を支給しているため、設計図の撮影に使用されないように、これらのデバイスのカメラを使用できないようにします。  

1.  構成項目の作成ウィザードの **[全般]** ページで、構成項目の種類として **[iOS および Mac OS X]** を選択し、 **[次へ]**をクリックします。  

2.  **[サポートされているプラットフォーム]** ページで、すべての iPhone および iPad デバイスのプラットフォームを選択します。  

3.  **[デバイス設定]** ページで、 **[セキュリティ]**を選択し、 **[次へ]**をクリックします。  

4.  **[セキュリティ]** ページで、 **[カメラ]** の値として **[禁止]**を選択します。  

5.  **[対応していない設定を修復する]** を選択して、変更がすべての iOS デバイスに確実に適用されるようにします。  

6.  ウィザードを完了して構成項目を作成します。  

 これで、「[System Center Configuration Manager での構成基準の作成と展開に関する一般的なタスク](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)」トピックの情報を使用して、作成した構成をデバイスに簡単に展開できるようになります。  

## <a name="scenarios-for-android-and-samsung-knox-devices-managed-without-the-configuration-manager-client"></a>Configuration Manager クライアントを使用せずに管理されている Android デバイスと Samsung KNOX デバイスのシナリオ  

### <a name="scenario-require-a-password-on-all-android-5-devices"></a>シナリオ: すべての Android 5 デバイスでパスワードを要求する  
 このシナリオでは、Android 5 デバイスに対してのみ、デバイスで 6 文字以上のパスワードを構成するようにユーザーに要求する構成アイテムを作成します。 さらに、ユーザーが 5 回正しくないパスワードを入力すると、デバイスがワイプされます。  

1.  構成項目の作成ウィザードの **[全般]** ページで、構成項目の種類として **[Android および Samsung KNOX]** を選択し、 **[次へ]**をクリックします。  

2.  **[サポートされているプラットフォーム]** ページで、**[Android 5]** のみを選択します (設定がこのプラットフォームにのみ適用されるようにするため)。  

3.  **[デバイス設定]** ページで、 **[パスワード]**を選択し、 **[次へ]**をクリックします。  

4.  **[パスワード]** ページで、次の設定を構成します。  

    -   **[デバイスのパスワードの設定が必要]** > **[必須]**  

    -   **[パスワードの最小文字数]** > **6**  

    -   **[デバイスをワイプするまでのログオン失敗回数]** > **5**  

5.  ウィザードを完了して構成項目を作成します。  

 これで、「[構成基準の作成と展開に関する一般的なタスク](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)」トピックの情報を使用して、作成した構成をデバイスに簡単に展開できるようになります。  




<!--HONumber=Nov16_HO1-->


