---
title: "クライアント設定を構成する"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager でクライアント設定を選択します。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: "5"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 20a8f91d10d98542f08e440bcfbc1a6f98a51932
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager でクライアント設定を構成する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のすべてのクライアント設定は、**[管理]** > **[クライアント設定]** から管理できます。 カスタム設定が適用されていない、階層内のすべてのユーザーおよびデバイスの設定を構成する場合は、既定の設定を変更します。 別の設定を一部のユーザーまたはデバイスのみに適用する場合は、カスタム設定を作成して、それらをコレクションに展開します。  

各クライアント設定の詳細については、「[System Center Configuration Manager のクライアント設定について](../../../core/clients/deploy/about-client-settings.md)」を参照してください。

> [!NOTE]  
>  クライアントを管理する構成項目を使用して、デバイスの構成対応の評価、追跡、および修復を行うことができます。 詳細については、「[System Center Configuration Manager でのデバイス コンプライアンスの確認](../../../compliance/understand/ensure-device-compliance.md)」を参照してください。  

##  <a name="configure-the-default-client-settings"></a>既定のクライアント設定を構成する    

1.  Configuration Manager コンソールで、**[管理]** > **[クライアント設定]** > **[既定のクライアント設定]** の順に選択します。  

3.  **[ホーム]** タブで **[プロパティ]** を選択します。  

4.  ナビゲーション ウィンドウで、各設定のグループのクライアント設定を表示および構成します。  

 クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 単一クライアントのポリシーの取得を開始するには、「[System Center Configuration Manager でクライアントを管理する方法](../../../core/clients/manage/manage-clients.md)」の「[Configuration Manager クライアントのポリシーの取得開始](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)」セクションを参照してください。  

##  <a name="create-and-deploy-custom-client-settings"></a>カスタム クライアント設定を作成および展開する  
これらのカスタム設定を展開すると、既定のクライアント設定が上書きされます。 この手順を始める前に、これらのカスタム クライアント設定を必要とするユーザーまたはデバイスを含むコレクションがあることを確認します。  

1.  Configuration Manager コンソールで、**[管理]** > **[クライアント設定]** の順に選択します。  

3.  **[ホーム]** タブの **[作成]** グループで、**[カスタム クライアント設定の作成]** を選択してから、次のいずれかを選択します。  

    -   **カスタム クライアント デバイス設定の作成**  

    -   **カスタム クライアント ユーザー設定の作成**  

4.  一意の名前と、必要に応じて説明を指定します。  

5.  設定のグループが表示されているチェック ボックスのうち 1 つまたは複数をオンにします。  

6.  ナビゲーション ウィンドウの各設定のグループを選択し、利用可能な設定を構成して **[OK]** をクリックします。   

8.  作成したカスタム クライアント設定を選択します。 **[ホーム]** タブの **[クライアント設定]** グループで、**[展開]** を選択します。  

9. **[コレクションの選択]** ダイアログ ボックスで適切なコレクションを選択し、**[OK]** を選択します。 選択したコレクションを確認するには、詳細ウィンドウで **[展開]** タブをクリックします。  

10. 作成したカスタム クライアント設定の順序を表示します。 複数のカスタム クライアント設定がある場合は、順序番号に従って適用されます。 競合がある場合は、順序番号が一番小さい設定によってその他の設定が上書きされます。 順序番号を変更するには、**[ホーム]** タブの **[クライアント設定]** グループで、**「Move Item Up」 (項目を上に移動)** または **「Move Item Down」 (項目を下に移動)** を選択します。  

 クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 単一クライアントのポリシーの取得を開始するには、「[System Center Configuration Manager でクライアントを管理する方法](../../../core/clients/manage/manage-clients.md)」の「[Configuration Manager クライアントのポリシーの取得開始](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)」セクションを参照してください。  

## <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Windows 10 拡張テレメトリを制限し、Windows Analytics デバイスの正常性に関連したデータのみを送信するようにする
<!-- 1356148 -->

1710 更新プログラムでは、Windows 10 テレメトリ データ コレクション レベルを **[拡張 (制限あり)]** に設定できます。 この設定を行うと、デバイスから **[拡張]** テレメトリ レベルのデータのすべてを報告されなくても、Windows 10 バージョン 1709 以降で、ご利用の環境のデバイスに関する、アクションにつながる有用な情報を得ることができます。

[拡張 (制限あり)] テレメトリ レベルには、基本レベルから収集されたメトリックとともに、Windows Analytics に関連する **[拡張]** レベルから収集されたデータのサブセットも含まれます。 テレメトリ レベルの詳細については、[テレメトリ レベル](https://docs.microsoft.com/windows/configuration/configure-windows-telemetry-in-your-organization#telemetry-levels)に関する記事をご覧ください。

1.  Configuration Manager コンソールで、**[管理]** > **[クライアント設定]** > **[既定のクライアント設定]** の順に選択します。  

2.  **[ホーム]** タブで **[プロパティ]** を選択します。  

3.  **[クラウド サービス]** を開き、Windows 10 テレメトリを **[拡張]** に設定します。

##  <a name="view-client-settings"></a>クライアント設定を表示する  
 同じデバイス、ユーザー、または、ユーザー グループに複数のクライアント設定が展開されている場合、優先順位と設定が複雑になることがあります。 クライアント設定を表示するには  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[デバイス]** > **[ユーザー]** または **[ユーザー コレクション]** の順に選択します。  

3.  **[クライアント設定]** グループで、デバイス、ユーザー、または、ユーザー グループを選択して、**[クライアントの設定の結果]** を選択します。  

4.  左ウィンドウからクライアント設定を選択すると、設定が表示されます。 この表示では、設定は読み取り専用です。 

    > [!NOTE]  
    >  クライアント設定を表示するには、クライアント設定に対する読み取りアクセス権を持っている必要があります。  

    