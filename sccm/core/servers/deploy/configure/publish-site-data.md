---
title: "サイト データの発行 | Microsoft Docs"
description: "Configuration Manager サイトを Active Directory Domain Services に発行する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: eb44c1c8c908e9cac17dc6d3011a3111eeb949b1


---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>System Center Configuration Manager のサイト データの発行

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 用に Active Directory スキーマを拡張すると、Configuration Manager サイトを Active Directory Domain Services (AD DS) に発行できるため、Active Directory コンピューターが信頼済みソースから安全にサイト データを取得することが可能になります。 サイト情報の AD DS への発行は Configuration Manager の基本機能には必要ではありませんが、この構成により管理オーバーヘッドが低減されます。  

-   **AD DS に発行するようにサイトが構成されている場合は**、Active Directory にサイト データを発行することにより、Configuration Manager クライアントがグローバル カタログ サーバーへの LDAP クエリ実行して自動的に管理ポイントを検出できるようになります。  

-   **サイトを AD DS に発行しない場合**、クライアントには、その既定の管理ポイントを特定するための、それに代わるメカニズムが必要となります。  

クライアントでの管理ポイントの検出方法については、「[クライアントが System Center Configuration Manager のサイト リソースやサービスを検索する方法を理解する](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)」を参照してください。  

## <a name="configure-sites-to-publish-to-ad-ds"></a>AD DS に発行するためのサイトの構成  
 基本的な手順は次のとおりです。  

-   サイトデータを発行する各フォレスト内で[ System Center Configuration Manager の Active Directory スキーマを拡張し](../../../../core/plan-design/network/extend-the-active-directory-schema.md)、**System Management** コンテナーが存在していることを確認する必要があります。  

-   データを発行する各プライマリ サイトのコンピューター アカウントには、   **システム管理** コンテナーとそのすべての子オブジェクトに対する **フル コントロール** 権限を付与する必要があります。  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Configuration Manager サイトが Active Directory フォレストにサイト情報を発行できるようにするには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  **[管理]** ワークスペースで、 **[サイトの構成]** を展開して、 **[サイト]**をクリックします。 このサイトのデータを発行するように構成するサイトを選択し、 **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]**をクリックします。  

3.  サイト プロパティの [発行] タブで、このサイトのサイト データの発行先のフォレストを選択します。 ****  

4.  [OK] をクリックして構成を保存します。 ****  

 発行に使用する Active Directory フォレストを構成するには、次の手順に従います。  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Active Directory フォレストを発行用に構成するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [ **管理** ] ワークスペースで [ **Active Directory フォレスト**] をクリックします。 Active Directory フォレストの検索を前に実行している場合は、検出されたフォレストが結果ウィンドウに表示されます。 Active Directory フォレストの探索を実行すると、ローカル フォレストと信頼済みフォレストがすべて探索されます。 信頼されていないフォレストだけを手動で追加します。  

    -   以前に検出したフォレストを構成するには、結果ウィンドウでフォレストを選択し、[ **ホーム** ] タブの [ **プロパティ** ] グループで、[ **プロパティ** ] をクリックしてフォレストのプロパティを開きます。 手順 3 に進みます。  

    -   一覧表示されていない新しいフォレストを構成するには、 **[ホーム]** タブの **[作成]** グループで、 **[フォレストの追加]** をクリックして **[フォレストの追加]** ダイアログ ボックスを開きます。 手順 3 に進みます。  

3.  **[全般]** タブで、検出するフォレストの構成を完了し、 **[Active Directory フォレスト アカウント]**を指定します。  

    > [!NOTE]  
    >  Active Directory フォレストの探索で、信頼されていないフォレストを検出して、そのフォレストに発行するにはグローバル アカウントが必要です。 サイト サーバーのコンピューター アカウントを使用しない場合は、グローバル アカウントのみ選択できます。  

4.  サイト データをこのフォレストに発行できるようにする場合は、[発行] タブで、必要な構成を行います。 ****  

    > [!NOTE]  
    >  サイトでフォレストへの発行を有効にした場合は、Configuration Manager 用にフォレストの Active Directory スキーマを拡張する必要があり、Active Directory フォレスト アカウントにそのフォレスト内のシステム コンテナーのフル コントロール権限が付与されていなければなりません。  

5.  このフォレストを Active Directory フォレストの探索で使用するための構成が完了したら、[ **OK** ] をクリックして構成を保存します。  



<!--HONumber=Dec16_HO3-->


