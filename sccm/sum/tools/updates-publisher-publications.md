---
title: パブリケーションを管理する
titleSuffix: Configuration Manager
description: System Center Updates Publisher を使用して、ソフトウェア更新プログラムのグループをパブリケーションとして管理します
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: f0ec652a9fb7d4ef6bef881bfc96f1be2b4e297a
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424342"
---
# <a name="manage-publications-in-updates-publisher"></a>Updates Publisher でパブリケーションを管理する

*適用対象:System Center Updates Publisher*

パブリケーションを使用することで、更新プログラムとバンドルのグループを単一オブジェクトとして管理できます。 これには、管理サーバーに更新プログラムを公開して、Updates Publisher の他のインストールと共に使用するグループとしてパブリケーションをエクスポートすることも含まれます。

## <a name="create-publications"></a>パブリケーションを作成する
次の 2 つの方法でパブリケーションを作成します。

-   **[更新プログラム] ワークスペース**で更新プログラムとバンドルを管理するときに、その時点で作成される新しいパブリケーションにそれらを[割り当てる](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication)ことができます。

-   **[パブリケーション] ワークスペース**で、リボンの **[パブリケーション]** タブにある **[作成]** ボタンを使用できます。 このメソッドでは、将来使用するパブリケーションを作成できます。 その後、更新プログラムを割り当てるときに、このパブリケーションを使用できます。

## <a name="rename-a-publication"></a>パブリケーションの名前を変更する
パブリケーションの名前を変更するには、**[パブリケーション] ワークスペース**からパブリケーションを選択し、リボンの **[パブリケーション]** タブで **[編集]** を選択します。

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>パブリケーションの更新プログラムでパブリケーションの種類を変更する
**[パブリケーション] ワークスペース**から、パブリケーションに割り当てられている更新プログラムとバンドルの**パブリケーションの種類**を変更できます。

1. 変更する更新プログラムを含むパブリケーションを選択し、1 つまたは複数の更新プログラムかバンドルを **[All &lt;publication name> member updates]\(すべての <パブリケーション名> メンバー更新プログラム)** の一覧から選択します。

2. 次に、**[ホーム]** タブで以下のオプションのいずれかを選択します。 使用できるオプションは、選択した更新プログラムのパブリケーションの種類によって異なります。

   -   **自動**
   -   **コンテンツ全体**
   -   **メタデータのみ**

変更後は、新しい値を確認するためにパブリケーションの表示を更新する必要がある場合があります。

別のパブリケーションの種類については、「[Assign updates and bundles to a publication (パブリケーションに更新プログラムとバンドルを割り当てる)](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication)」をご覧ください。

> [!TIP]    
> バンドルのパブリケーションの種類を設定すると、バンドル内のすべてのソフトウェア更新プログラムは、バンドルのパブリケーションの種類と共に公開されます。

## <a name="remove-updates-from-a-publication"></a>パブリケーションから更新プログラムを削除する
パブリケーションから更新プログラムまたはバンドルを削除するには、**[パブリケーション] ワークスペース**で変更するパブリケーションを選択し、次に削除する更新プログラムまたはバンドルを選択します。 次に、リボンの **[ホーム]** タブで **[削除]** を選択します。

パブリケーションから更新プログラムを削除した後、これらのプログラムは Updates Publisher のリポジトリで引き続き使用できます。

## <a name="publish-publications"></a>パブリケーションを管理する
更新プログラムとバンドルを公開するとき、これらの更新プログラムとバンドルに関する情報 (メタデータ) と、場合によっては更新プログラムのバイナリ (コンテンツ全体) が、デバイスへの展開のために Updates Publisher によって更新サーバーに追加されます。

発行に関するオプションを設定する前に、Updates Publisher の [[更新サーバー]](/sccm/sum/tools/updates-publisher-options#update-server) オプションを構成する必要があります。 この構成オプションを開くには、**[更新プログラム] ワークスペース** &gt; **[概要]** に移動し、**[Configure WSUS and Signing Certificate]\(WSUS と署名証明書の構成)** を選択します。 また、Updates Publisher オプションの更新サーバー ページに移動できます。

> [!NOTE]   
> Updates Publisher では、375 メガバイト (MB) 以下のサイズの更新プログラムのみを公開できます。

### <a name="to-publish-a-publication"></a>パプリケーションを公開するには

1. **[パブリケーション] ワークスペース**に移動し、公開またはエクスポートする更新プログラムとバンドルのグループを含むパブリケーションを選択します。 次に、リボンの **[ホーム]** タブから **[公開]** を選択します。

2. **[公開]** ウィザードの **[選択]** ページで、新しく証明書を発行してすべての更新プログラムを署名することを選択できますが、パブリケーションの種類は変更できません。

3. ウィザードを完了します。

   公開に失敗した場合は UpdatesPublisher.log ファイルへのリンクが表示され、詳しい情報を確認できます。

## <a name="export-a-publication"></a>パブリケーションをエクスポートする
Updates Publisher のリポジトリからパブリケーションをエクスポートできます。 これにより、そのパブリケーションに割り当てられている更新プログラムとバンドルがエクスポートされ、更新プログラム カタログが作成されます。 作成後、このカタログを Updates Publisher の別のインスタンスに[追加](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs)および[インポート](/sccm/sum/tools/updates-publisher-catalogs#mport-updates)できます。 また、パブリケーションの一部ではない[更新プログラムのエクスポート](/sccm/sum/tools/manage-updates-with-updates-publisher#export-updates)もできます。

パブリケーションをエクスポートするには、**[パブリケーション] ワークスペース**に移動し、エクスポートする更新プログラムを含むパブリケーションを選択します。 一度に 1 つのパブリケーションを選択できます。

パブリケーションを選択したら、リボンの **[ホーム]** タブから **[エクスポート]** を選択し、次にカタログのエクスポートのパスとファイル名を入力します。

エクスポートの一部として依存するソフトウェア更新プログラムをエクスポート (インクルード) するオプションもあります。

## <a name="rename-a-publication"></a>パブリケーションの名前を変更する
パブリケーションの名前を変更するには、**[パブリケーション] ワークスペース**からパブリケーションを選択し、リボンの **[パブリケーション]** タブから **[編集]** を選択します。

## <a name="delete-a-publication"></a>パブリケーションを削除する
パブリケーションを削除するには、**[パブリケーション] ワークスペース**からパブリケーションを選択し、リボンの **[パブリケーション]** タブから **[削除]** を選択します。

Updates Publisher からパブリケーションを削除した後、そのパブリケーションに含まれていた更新プログラムは Updates Publisher のリポジトリで引き続き使用できます。

## <a name="expire-or-reactivate-updates-and-bundles"></a>更新プログラムとバンドルの期限切れ設定または再アクティブ化
**[更新プログラム] ワークスペース**を使用して更新プログラムとバンドルを選択し、期限切れにするか再アクティブ化することができます。 更新プログラムとバンドルを必要に応じて選択し、期限切れにするか再アクティブ化することができます。

-   **更新プログラムまたはバンドルを期限切れにするには**、[更新プログラム] ワークスペースで 1 つまたは複数の更新プログラムかバンドルを選択し、次に **[ホーム]** タブから **[期限切れ]** を選択します。更新プログラムまたはバンドルを Configuration Manager に期限切れとして公開するまでは、再アクティブ化できます。

    Configuration Manager からカスタム更新プログラムまたはバンドルを取り除く (削除する) 前に期限切れの設定を行い、次に Configuration Manager に対してこの期限切れの状態を公開する必要があります。 Configuration Manager の更新プログラムやバンドルが期限切れになった後は、更新プログラムやバンドルを展開または再アクティブ化することはできません。

-   **更新プログラムまたはバンドルを再アクティブ化するには**、[更新プログラム] ワークスペースで期限切れにする更新プログラムを 1 つまたは複数選択し、次にリボンの **[ホーム]** タブから **[再アクティブ化]** を選択します。 期限切れの更新プログラムが Configuration Manager に期限切れとしてすでに公開済みの場合は、再アクティブ化できません。
