---
title: "CD.Latest フォルダー | Microsoft Docs"
description: "Configuration Manager コンソール内から製品の更新を提供する新しい更新プロセスについて説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: dcf56f6b82f89e81d636ea920f36133e245cbb1e


---
# <a name="the-cdlatest-folder-for-system-center-configuration-manager"></a>System Center Configuration Manager の CD.Latest フォルダー

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager は、Configuration Manager コンソール内から製品の更新を提供する新しい更新プロセスを導入します。 Configuration Manager を更新するこの新しいメソッドをサポートするために、サイトの更新されたバージョン用の Configuration Manager インストール ファイルのコピーを含む、**CD.Latest** という名前の新しいフォルダーが作成されます。  

1606 以降の更新プログラムでは、CD.Latest フォルダーに **Redist** というフォルダーが含まれます。セットアップ時にダウンロードして使用される再頒布可能ファイルがここに入ります。 これらのファイルは、その CD.Latest フォルダーにある Configuration Manager ファイルのバージョンに一致します。 CD.Latest フォルダーからセットアップを実行する場合、そのセットアップのバージョンに一致するファイルを使用する必要があります。 そのためには、新しい現行のファイルを Microsoft からダウンロードするようにセットアップに指示するか、CD.Latest フォルダーに含まれている Redist フォルダーのファイルを使用するようにセットアップに指示できます。

ただし、2016 年 10 月にリリースされた構成基準バージョン 1606 のような構成基準メディアには、Redist フォルダーは含まれません。 コンソール内の更新プログラムをインストールするまで、Redist フォルダーは作成されません。 それまでは、構成基準メディアからサイトをインストールするときに使った Redist フォルダーを使ってください。  

> [!TIP]
> バージョン 1606 をまだインストールしていない場合、使用する再頒布可能ファイルが現行のものであることを確認する必要があります。 再頒布可能ファイルを最近ダウンロードしていない場合は、Microsoft からダウンロードするようセットアップを計画します。   

 次は、中央管理サイトまたはプライマリ サイト サーバー上の CD.Latest フォルダーを作成または更新するシナリオです。  

-   Configuration Manager コンソール内から、更新プログラムまたは修正プログラムをインストールします。Configuration Manager インストール フォルダーでフォルダーが作成または更新されます。  

-   組み込み Configuration Manager バックアップ タスクを実行します。指定されたバックアップ フォルダーの場所でフォルダーが作成または更新されます。  

CD.Latest フォルダーからのソース ファイルは、次に対してサポートされています。  

1.  **バックアップと回復:** CD.Latest フォルダーには、サイトの回復の一部として、サイトの再インストールに使用するソース ファイルが含まれています。 Configuration Manager サイトを回復するには、サイト バックアップに CD.Latest フォルダーを含める必要があります (組み込みのサイトのバックアップ タスクには、サイトのバックアップの一部として自動的にこのフォルダーが含まれます)。  

    -   **サイト回復の一部としてサイトを再インストールする場合は** 、バックアップに含まれている CD.Latest フォルダーからサイトをインストールします。 これにより、サイトのバックアップおよびサイト データベースに一致するファイルのバージョンを使用してサイトがインストールされます。  

        > [!IMPORTANT]  
        >  適切な CD.Latest フォルダーとそこから取得できる内容がない場合は、サイトを回復できず、再インストールが必要になります。  

    -   CD.Latest フォルダーがないが、稼働中の子プライマリ サイトまたは中央管理サイトがある場合は、そのサイトを参照サイトとして使用してサイトを回復できます。  

2.  **子プライマリ サイトをインストールするには:** 1 つまたは複数のコンソール内の更新プログラムがインストールされている中央管理サイトの下に新しい子プライマリ サイトをインストールするときに、中央管理サイトの CD.Latest フォルダーからセットアップとソース ファイルを使用する必要があります。 セットアップが中央管理サイトの CD.Latest フォルダーのコピーから実行される場合、中央管理サイトのバージョンに対応するインストール ソース ファイルが使用されます。 詳細については、「[セットアップ ウィザードを使用してサイトをインストールする](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)」を参照してください。  

3.  **スタンドアロン プライマリ サイトを展開するには:** 新しい中央管理サイトをインストールしてスタンドアロン プライマリ サイトを拡張するときには、プライマリ サイトの CD.Latest フォルダーからセットアップとソース ファイルを使用して、新しい中央管理サイトをインストールする必要があります。 CD.Latest フォルダーのコピーから実行される場合、プライマリ サイトのバージョンに対応するインストール ソース ファイルが使用されます。 詳細については、「[セットアップ ウィザードを使用してサイトをインストールする](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)」の「[スタンドアロン プライマリ サイトを拡張する](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)」を参照してください

> [!IMPORTANT]  
>  更新された CD.Latest のソース ファイルは、次に対してサポートされていません。  
>   
>  -   新しい階層の新しいサイトのインストール  
>  -   Upgrading a Microsoft System Center 2012 Configuration Manager サイトから System Center Configuration Manager へのアップグレード



<!--HONumber=Dec16_HO3-->


