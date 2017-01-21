---
title: "証明書プロファイルを監視する | Microsoft Docs"
description: "System Center Configuration Manager 証明書プロファイルのコンプライアンス状態を監視する方法を説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
caps.latest.revision: 7
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 34e1f57798a9745303dd6d03a8b4362c01c5efbb


---
# <a name="how-to-monitor-certificate-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager で証明書プロファイルを監視する方法

*適用対象: System Center Configuration Manager (Current Branch)*


階層内のユーザーに System Center Configuration Manager 証明書プロファイルを展開した後は、以下の手順に従って、証明書プロファイルのコンプライアンス対応状態を監視できます。  

-   [Configuration Manager コンソールでコンプライアンス評価結果を表示する方法](#BKMK_console)  

-   [レポートを使用してコンプライアンス評価結果を表示する方法](#BKMK_Reports)  

##  <a name="a-namebkmkconsolea-how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a> Configuration Manager コンソールでコンプライアンス評価結果を表示する方法  
 System Center Configuration Manager コンソールで、展開した証明書プロファイルのコンプライアンスの詳細を表示するには、この手順に従います。  

> [!NOTE]  
>  SCEP 証明書のコンプライアンスを監視するには、Configuration Manager コンソールを使用するのではなく、 [How to View Compliance Results by Using Reports](#BKMK_Reports)の説明に従ってレポートを使用してください。 具体的には、レポート ノード **[会社のリソースへのアクセス]**の下にあるこれらの証明書のレポートを使用します。  
>   
>  -   証明書の発行履歴  
> -   証明書の有効期限が近づいている資産の一覧  
> -   証明書の発行ステータス別資産の一覧  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Configuration Manager コンソールでコンプライアンス結果を表示するには  

1.  System Center Configuration Manager コンソールで、**[監視]** をクリックします。  

2.  [監視] **** ワークスペースで、[展開] ****をクリックします。  

3.  [展開 **** ] 一覧で、コンプライアンス情報を確認する証明書プロファイルの展開を選択します。  

4.  メイン ページで、証明書プロファイルの展開のコンプライアンスの概要を確認できます。 詳しい情報を表示するには、証明書プロファイルの展開を選択してから、[ホーム **** ] タブの [展開 **** ] グループで [ステータスの表示 **** ] をクリックして、[展開ステータス **** ] ページを開きます。  

     [展開のステータス] **** ページには次のタブがあります。  

    -   **対応**: 証明書プロファイルに対応している資産とその数を示します。 規則をダブルクリックすると、 **[資産とコンプライアンス]** ワークスペースの **[ユーザー]** ノードに一時ノードを作成できます。 このノードには、証明書プロファイルに対応しているすべてのユーザーが含まれます。 このプロファイルに対応しているユーザーは、[資産の詳細 **** ] ウィンドウにも表示されます。 詳細情報を表示するには、一覧内のユーザーをダブルクリックします。  

        > [!IMPORTANT]  
        >  証明書プロファイルをクライアント デバイスに適用できない場合は評価されませんが、 対応しているという結果が返されます。  

    -   **エラー**: 選択した証明書プロファイルの展開で発生したエラーとその影響を受けた資産の数の一覧を示します。 規則をダブルクリックすると、 **[資産とコンプライアンス]** ワークスペースの **[ユーザー]** ノードに一時ノードを作成できます。 このノードには、このプロファイルでエラーが発生したすべてのユーザーが含まれます。 ユーザーを選択すると、[資産の詳細 **** ] ウィンドウに、選択した問題に影響を受けているユーザーが表示されます。 問題の詳細情報を表示するには、一覧内のユーザーをダブルクリックします。  

    -   **非対応**: 証明書プロファイルにある非対応の規則とその影響を受けた資産の数の一覧を示します。 規則をダブルクリックすると、 **[資産とコンプライアンス]** ワークスペースの **[ユーザー]** ノードに一時ノードを作成できます。 このノードには、このプロファイルに対応していないすべてのユーザーが含まれます。 ユーザーを選択すると、[資産の詳細 **** ] ウィンドウに、選択した問題に影響を受けているユーザーが表示されます。 問題の詳細情報を表示するには、一覧内のユーザーをダブルクリックします。  

    -   **不明**: 選択した証明書プロファイルに対応しているかどうかを報告しなかった全ユーザーと、デバイスにあるクライアントの現在の状態を一覧表示します。  

5.  [展開ステータス **** ] ページで、展開した証明書プロファイルのコンプライアンスの詳細情報を確認できます。 [展開] **** ノードの下に一時ノードが作成されるため、後から再度この情報をすばやく確認できます。  

     証明書の登録ステータスは、数値で表示されます。 次の表に、その数値の意味を示します。  

    |登録ステータス|説明|  
    |-----------------------|-----------------|  
    |0x00000001|登録が正常に完了し、証明書が発行されました。|  
    |0x00000002|要求が送信され登録を待っているか、要求が帯域外で送信されました。|  
    |0x00000004|登録を延期する必要があります。|  
    |0x00000010|エラーが発生しました。|  
    |0x00000020|登録ステータスが不明です。|  
    |0x00000040|ステータス情報がスキップされました。 これは、ハイパーリンク "http://msdn.microsoft.com/ja-jp/windows/ms721572"\l"_security_certification_authority_gly"の証明機関が無効であるか監視対象に選択されていない場合に発生することがあります。|  
    |0x00000100|登録が拒否されました。|  

##  <a name="a-namebkmkreportsa-how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a> レポートを使用してコンプライアンス評価結果を表示する方法

 System Center Configuration Manager のコンプライアンスの設定には、証明書プロファイルの対応状態を監視するための組み込みレポートが含まれています。 これらのレポートには、[コンプライアンスおよび設定管理] ****のカテゴリがあります。  

> [!IMPORTANT]  
>  コンプライアンス設定でレポートの [デバイス フィルター **** ] と [ユーザー フィルター **** ] パラメーターを指定するときは、必ず、ワイルドカード (%) 文字を使ってください。  

 System Center Configuration Manager でのレポートの構成方法に関して詳しくは、「[System Center Configuration Manager のレポート](../../core/servers/manage/reporting.md)」を参照してください。  



<!--HONumber=Dec16_HO3-->


