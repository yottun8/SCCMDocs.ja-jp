---
title: 更新プログラムを管理する
titleSuffix: Configuration Manager
description: System Center Updates Publisher で展開し作成した更新プログラムを管理する
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4de365b7df3a18abdfc5a92e9516bad84818ac35
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896746"
---
# <a name="manage-software-updates-in-updates-publisher"></a>Updates Publisher のソフトウェア更新プログラムの管理

「オブジェクトの*適用対象: System Center Updates Publisher*     

System Center Updates Publisher で、リポジトリにインポートしたソフトウェア更新プログラムとバンドルを管理するため、**[更新プログラム] ワークスペース**を使用します。  

管理タスクには、更新プログラムとバンドルの複製、編集、期限切れまたは再アクティブ化、パブリケーションへの割り当てが含まれます。 その他の Updates Publisher のインストールで使用するカスタム カタログをエクスポートすることもできます。

管理できる更新プログラムを取得するには:
-  Updates Publisher のインストールに[更新プログラム カタログを追加](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs)します。
-  このカタログからリポジトリに更新プログラムを[インポート](/sccm/sum/tools/updates-publisher-catalogs#import-updates)します。

[独自の更新プログラムを作成する](/sccm/sum/tools/create-updates-with-updates-publisher)こともできます。



## <a name="create-a-duplicate-of-an-update"></a>更新プログラムの複製の作成
リポジトリにある更新プログラムの複製またはコピーを作成できます。 これにより、元の更新プログラムをする代わりにコピーを変更できます。 更新プログラムのバンドルのコピーは作成できません。

コピーを作成するには、**[更新プログラム] ワークスペース**で更新プログラムを選択し、**[複製]** を選択します。 更新プログラムのコピーは、更新プログラムの名前に *Copy of (～のコピー)* が追加されて、[更新プログラム] ワークスペース内の同じ場所に表示されます。

作成した新しいコピーは、**Unexpired (有効期限内)** の状態になっていますが、それ以外は元の設定を保持しています。

## <a name="edit-updates-and-bundles"></a>更新プログラムとバンドルの編集
リポジトリ内の更新プログラムとバンドルを選択し、変更できます。

**[更新プログラム] ワークスペース**で、更新プログラムまたはバンドルを選択し、**[ホーム]** タブの **[編集]** を選択して編集ウィザードを開きます。 更新プログラムのウィザードとバンドルのウィザードはそれぞれ独立していますが密接に関連しており、この 2 つのウィザードには、[[Create Update]\(更新プログラムの作成)](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard) ウィザードまたは [[バンドルの作成]](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-bundle-wizard) ウィザードに表示されるオプションと同じものが表示されます。

編集する際は、更新プログラムまたはバンドルについての詳細をお使いの環境で使用できるように変更できます。 たとえば、適用性や優先順位のルールの編集や、言語の変更ができます。 また、製品やベンダーを変更することで、更新プログラムやバンドルをカスタム フォルダーに移動させ、個人用に更新プログラムをグループ化することもできます。

## <a name="assign-updates-and-bundles-to-a-publication"></a>更新プログラムとバンドルをパブリケーションに割り当てる
**[更新プログラム] ワークスペース**で更新プログラムとバンドルを選択し、リボンの **[ホーム]** タブにある **[割り当て]** を選択してパブリケーションに追加します。 **[Assign Software Updates]\(ソフトウェア更新プログラムの割り当て)** ウィザードが開始します。
-  更新プログラムとバンドルを単一タスクとして選択して発行する方法については、「[Publish updates and bundles (更新プログラムとバンドルの発行)](#publish-updates-and-bundles-from-the-updates-workspace)」をご覧ください。
-  更新プログラムとバンドルのグループを単一オブジェクトとして管理する方法については、「[Manage publications (パブリケーションの管理)](/sccm/sum/tools/updates-publisher-publications)」をご覧ください。 更新プログラムをパブリケーションに割り当てると、そのパブリケーションとパブリケーションに割り当てられたすべての更新プログラムを管理できるようになります。

更新プログラムをパブリケーションに割り当てるとき:

-   期限切れまたは期限切れでない更新プログラムとバンドルをどちらも同じパブリケーションに含めることができます。

-   パブリケーションの種類を指定します。

    -   **[Full Content]\(すべてのコンテンツ)** – WSUS サーバーに更新プログラムのすべてのコンテンツを発行します。 これにはメタデータと更新プログラム バイナリも含まれます。

    -   **[Metadata only]\(メタデータのみ)** – メタデータのみを発行します。更新プログラム バイナリは発行されません。 コンプライアンス対応データを収集する場合に、このオプションが必要になる場合があります。

    -   **[自動]** – このモードは、Updates Publisher を Configuration Manager に接続した場合にのみ使用可能です (詳しくは、[ConfigMgr サーバー](/sccm/sum/tools/updates-publisher-options#configmgr-server) オプションに関する記事をご覧ください)。

    この種類を使用して、Updates Publisher は Configuration Manager に照会し、更新プログラムまたはバンドルのすべてのコンテンツを発行するか、メタデータのみを発行するかを判断します。 更新プログラムのすべてのコンテンツは、その更新プログラムが **[Requested client count threshold]\(要求したクライアント数のしきい値)** と **[Package source size threshold] \(パッケージ ソースのサイズのしきい値)** の条件を満たしているときにのみ発行されます (この 2 つのしきい値は、Updates Publisher オプションの **[ConfigMgr サーバー]** ページで指定します)。

-   パブリケーションを選択します。

    -   使用するパブリケーションを既に作成してある場合は、**[Assign software update to existing publications]\(ソフトウェア更新プログラムを既存のパブリケーションに割り当てる)** を使用します。 このオプションを使用するには、パブリケーションが少なくとも 1 つ存在する必要があります。

    -   適切なパブリケーションがない場合は、**[Assign software update to a new publication]\(ソフトウェア更新プログラムを新しいパブリケーションに割り当てる)** を使用します。 これにより、指定した名前で新しいパブリケーションが作成されます。

更新プログラムをパブリケーションに割り当てると、**[パブリケーション] ワークスペース**を使用して、パブリケーションをグループとして[発行](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations)または[エクスポート](/sccm/sum/tools/updates-publisher-publications#export-a-pubilcation)できます。

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>[更新プログラム] ワークスペースから更新プログラムとバンドルを発行する
更新プログラムとバンドルを発行するとき、これらの更新プログラムとバンドルに関する情報 (メタデータ) と、場合によっては更新プログラムのバイナリ (すべてのコンテンツ) が、デバイスへの展開のために Updates Publisher によって更新サーバーに追加されます。

発行に関するオプションを設定する前に、Updates Publisher の [[更新サーバー]](/sccm/sum/tools/updates-publisher-options#update-server) オプションを構成する必要があります。 この構成オプションを開くには、**[更新プログラム] ワークスペース** &gt; **[概要]** に移動し、**[Configure WSUS and Signing Certificate]\(WSUS と署名証明書の構成)** を選択します。 また、Updates Publisher オプションの [更新サーバー] ページに移動できます。

更新プログラムとバンドルを発行する方法は 2 つあります。
-   [更新プログラム] ワークスペースから直接 (*更新プログラムとバンドルを発行する*には、次の手順に従います)。
-   [パブリケーション] ワークスペースから [パブリケーション](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations)として。  

> [!NOTE]   
> Updates Publisher では、375 メガバイト (MB) 以下のサイズの更新プログラムのみを発行できます。

### <a name="to-publish-updates-and-bundles"></a>更新プログラムとバンドルを発行するには
1.  **[更新プログラム] ワークスペース**に移動し、発行する更新プログラムとバンドルを 1 つまたは複数選択します。 次に、リボンの **[ホーム]** タブで **[発行]** を選択します。

2.  **[発行]** ウィザードの **[選択]** ページで、更新プログラムの発行方法を選択します。 このオプションは、[更新プログラムの割り当て](#assign-updates-and-bundles-to-a-publication)に対するものと同じです (**すべてのコンテンツ**、**メタデータのみ**、または**自動**)。

    また、すべての更新プログラムを新しい発行元証明書で署名することも選択できます。

3.  ウィザードを完了します。

発行が失敗した場合は、多くの情報が得られる UpdatesPublisher.log ファイルへのリンクが表示されます。

## <a name="export-updates"></a>更新プログラムのエクスポート
更新プログラムとバンドルを Updates Publisher リポジトリからエクスポートして、カスタム更新カタログを作成できます。 次に、このカタログを Updates Publisher の別のインスタンスに[追加](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs)して[インポート](/sccm/sum/tools/updates-publisher-catalogs#mport-updates)できます。 ([更新プログラムをパブリケーションとしてエクスポート](/sccm/sum/tools/updates-publisher-publications##export-a-publication)することもできます)。

直接エクスポートするには、**[更新プログラム] ワークスペース** > **[すべてのソフトウェア更新プログラム]** に移動し、1 つまたは複数の更新プログラムとバンドルを選択します。 ベンダーや製品のフォルダーをエクスポートすることはできませんが、フォルダーを選択してからフォルダー内の更新プログラムをエクスポート用に選択できます。

1 つまたは複数の更新プログラムを選択したら、リボンの **[ホーム]** タブで **[エクスポート]** を選択し、次にカタログのエクスポート先のパスとファイル名を入力します。

依存するソフトウェア更新プログラムをエクスポート (インクルード) するオプションもあります。

## <a name="delete-updates-and-bundles"></a>更新プログラムとバンドルの削除
更新プログラムとバンドルを削除して、Updates Publisher リポジトリから取り除くことができます。

**[更新プログラム] ワークスペース** > **[すべてのソフトウェア更新プログラム]** に移動し、1 つまたは複数の個々の更新プログラムを選択します。 次に、リボンの **[ホーム]** タブで **[削除]** を選択します。

-   選択した更新プログラムの中に、未発行か期限切れの更新プログラムやバンドルしか含まれてない場合は、取り除く前に削除の確認を求められます。

-   選択した更新プログラムの中に、発行済みか有効期限内の更新プログラムやバンドルが含まれている場合は、警告が表示されます。 リポジトリから削除する前に、更新プログラムを[期限切れ](/sccm/sum/tools/updates-publisher-pubilcations#expire-or-reactivate-updates-and-bundles)の状態にしてからその変更を発行する必要があります。  

ベンダーから更新プログラムまたはバンドルを削除してからカタログをインポートした場合、その更新プログラムはリポジトリに格納されます。

## <a name="manage-vendor-and-product-folders"></a>ベンダーと製品のフォルダーの管理
更新プログラムのインポート先または作成先のベンダーと各ベンダーの製品の一覧を表示するには、**[更新プログラム] ワークスペース** > **[概要]** > **[すべてのソフトウェア更新プログラム]** に移動します。

ベンダーと製品のフォルダーは、ウィザードを使用してソフトウェア更新プログラムやバンドルのインポートまたは作成を行う際に、Updates Publisher によって自動で作成されます。 これらのフォルダーは手動でも作成できます。

-   ベンダーのフォルダーを作成するには、**[更新プログラム] ワークスペース** のナビゲーション ウィンドウで **[すべてのソフトウェア更新プログラム]** を右クリックし、**[Create Vendor]\(ベンダーの作成)** を選択します。

-   ベンダーのフォルダーの下に製品のフォルダーを作成するには、ベンダーのフォルダーを右クリックし、**[Create Product]\(製品の作成)** を選択します。

フォルダーを作成するだけでなく、リポジトリ内のベンダーまたは製品のフォルダー名を変更したり、フォルダーを削除したりできます。 変更、削除するには、フォルダーを右クリックして **[名前の変更]** または **[削除]** を選択します。 フォルダーを削除すると、そのフォルダ内のすべての更新プログラム、バンドル、製品のフォルダーが Updates Publisher リポジトリから削除されます。

ご自身で作成したフォルダーも含め、ベンダーと製品のフォルダー間で更新プログラムを移動できます。 更新プログラムまたはバンドルを新しいフォルダーに移動するには、更新プログラムまたはバンドルを選択してから **[編集]** する必要があります。 次に、[更新プログラムの編集] ウィザードの **[情報]** ページで、ベンダーと製品の再割り当てができます。 **[更新プログラムの編集]** ウィザードが完了したら、新しいフォルダーに変更を適用し、更新プログラムを移動させます。

## <a name="view-the-xml-of-an-update-or-bundle"></a>更新プログラムまたはバンドルの XML の表示
**[更新プログラム] ワークスペース** で更新プログラムまたはバンドルを 1 つ選択し、次に XML の **[表示]** を選択して更新プログラムの XML 構造を表示します。 XML 構造を直接編集するオプションはありません。
