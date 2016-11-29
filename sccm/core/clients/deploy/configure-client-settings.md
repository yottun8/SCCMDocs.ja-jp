---
title: "クライアント設定の構成 | System Center Configuration Manager"
description: "System Center Configuration Manager でクライアント設定を選択します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9e3162e04da90748379145e37f6b378badab97d3

---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager でクライアント設定を構成する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のすべてのクライアント設定は、Configuration Manager コンソールの **[管理]** ワークスペースの **[クライアント設定]** ノードから管理できます。 カスタム設定が適用されていない、階層内のすべてのユーザーおよびデバイスの設定を構成する場合は、既定の設定を変更します。 別の設定を一部のユーザーまたはデバイスのみに適用する場合は、カスタム設定を作成して、それらをコレクションに展開します。  

> [!NOTE]  
>  クライアントを管理する構成項目を使用して、デバイスの構成対応の評価、追跡、および修復を行うことができます。 詳細については、「[System Center Configuration Manager でのデバイス コンプライアンスの確認](../../../compliance/understand/ensure-device-compliance.md)」を参照してください。  

##  <a name="a-namebkmkdefaultclientsettingsa-how-to-configure-the-default-client-settings"></a><a name="BKMK_DefaultClientSettings"></a> 既定のクライアント設定の構成方法  

 階層内のすべてのクライアントの既定のクライアント設定を構成するには、次の手順に従います。  

#### <a name="to-configure-the-default-client-settings"></a>既定のクライアント設定を構成するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [ **管理** ] ワークスペースで、[ **クライアント設定**] をクリックしてから、[ **既定のクライアント設定**] を選択します。  

3.  [ **ホーム** ] タブで [ **プロパティ**] をクリックします。  

4.  ナビゲーション ウィンドウで、各設定のグループのクライアント設定を表示および構成します。 クライアント設定の詳細については、「[System Center Configuration Manager のクライアント設定について](../../../core/clients/deploy/about-client-settings.md)」を参照してください。  

5.  [ **OK** ] をクリックして [ **既定のクライアント設定** ] ダイアログ ボックスを閉じます。  

 クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 単一クライアントのポリシーの取得を開始するには、「[System Center Configuration Manager でクライアントを管理する方法](../../../core/clients/manage/manage-clients.md)」の「[Configuration Manager クライアントのポリシーの取得開始](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)」セクションを参照してください。  

##  <a name="a-namebkmkcustomclientsettingsa-how-to-create-and-deploy-custom-client-settings"></a><a name="BKMK_CustomClientSettings"></a> カスタム クライアント設定を作成および展開する方法  
 選択したユーザーまたはデバイスのコレクションにカスタム設定を構成して展開するには、次の手順に従います。 これらのカスタム設定を展開すると、既定のクライアント設定が上書きされます。  

> [!NOTE]  
>  この手順を始める前に、これらのカスタム クライアント設定を必要とするユーザーまたはデバイスを含むコレクションがあることを確認します。  

#### <a name="to-configure-and-deploy-custom-client-settings"></a>カスタム クライアント設定を構成および展開するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [ **管理** ] ワークスペースで [ **クライアント設定**] をクリックします。  

3.  [ **ホーム** ] タブの [ **作成** ] グループで、[ **カスタム クライアント設定の作成**] をクリックして、デバイスまたはユーザーのどちらのカスタム クライアント設定を作成するかに応じて、次のいずれかのオプションをクリックします。  

    -   **カスタム クライアント デバイス設定の作成**  

    -   **カスタム クライアント ユーザー設定の作成**  

4.  [ **カスタム クライアント デバイス設定の作成** ] または [ **カスタム クライアント ユーザー設定の作成** ] ダイアログ ボックスで、カスタム設定の一意の名前および説明 (省略可能) を指定します。  

5.  グループの設定が表示されている利用可能なチェック ボックスを 1 つまたは複数オンにします。  

6.  ナビゲーション ウィンドウの最初のグループ設定をクリックし、利用可能なカスタム設定を表示および構成します。 残りのグループ設定ごとにこのプロセスを繰り返します。 各クライアント設定の詳細については、「[System Center Configuration Manager のクライアント設定について](../../../core/clients/deploy/about-client-settings.md)」を参照してください。  

7.  [ **OK** ] をクリックして、[ **カスタム クライアント デバイス設定の作成** ] または [ **カスタム クライアント ユーザー設定の作成** ] ダイアログ ボックスを閉じます。  

8.  作成したカスタム クライアント設定を選択します。 [ **ホーム** ] タブの [ **クライアント設定** ] グループで、[ **展開**] をクリックします。  

9. [ **コレクションの選択** ] ダイアログ ボックスで、カスタム設定を使用して構成するデバイスまたはユーザーが含まれるコレクションを選択し、[ **OK**] をクリックします。 選択したコレクションを確認するには、詳細ウィンドウで [ **展開** ] タブをクリックします。  

10. 作成したカスタム クライアント設定の順序を表示します。 複数のカスタム クライアント設定がある場合は、順序番号に従って適用されます。 競合がある場合は、順序番号が一番小さい設定によってその他の設定が上書きされます。 順序番号を変更するには、[ **ホーム** ] タブの [ **クライアント設定** ] グループで、[ **項目を上に移動** ] または [ **項目を下に移動**] をクリックします。  

 クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 単一クライアントのポリシーの取得を開始するには、「[System Center Configuration Manager でクライアントを管理する方法](../../../core/clients/manage/manage-clients.md)」の「[Configuration Manager クライアントのポリシーの取得開始](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)」セクションを参照してください。  

##  <a name="a-namebkmkresultantclientsettingsa-how-to-view-resultant-client-settings"></a><a name="BKMK_ResultantClientSettings"></a> クライアント設定の結果を表示する方法  
 同じデバイス、ユーザー、または、ユーザー グループに複数のクライアント設定が展開されている場合、優先順位と設定が複雑になることがあります。 計算されたクライアントの設定の結果を表示するには、次の手順に従います。  

#### <a name="to-view-the-resultant-client-settings"></a>クライアントの設定の結果を表示するには  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]**をクリックします。  

2.  [ **資産とコンプライアンス** ] ワークスペースで [ **デバイス**]、[ **ユーザー**] または [ **ユーザー コレクション**] をクリックします。  

3.  [ **クライアント設定** ] グループで、デバイス、ユーザー、または、ユーザー グループを選択して、[ **クライアントの設定の結果**] を選択します。  または、デバイス、ユーザー、または、ユーザー グループを右クリックして、[ **クライアント設定**] を選択し、[ **クライアントの設定の結果**] をクリックします。  

4.  左ウィンドウからクライアント設定を選択すると、設定の結果が表示されます。  

    > [!NOTE]  
    >  クライアント設定の結果を表示するには、ログオンしたユーザーがクライアント設定に対する読み取りアクセス権を持っている必要があります。  

    > [!NOTE]  
    >  表示される設定の結果は、読み取り専用です。 設定を変更するには、上記の手順を使用します。  



<!--HONumber=Nov16_HO1-->


