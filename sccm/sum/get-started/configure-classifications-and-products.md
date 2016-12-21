---

title: "同期させる分類と製品を構成する | System Center Configuration Manager"
description: "Configuration Manager コンソールで次の手順を利用し、同期させる分類と製品を構成します。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 46cf461c92348e1a90533518355f2b5982ae5770



---
#  <a name="configure-classifications-and-products-to-synchronize"></a>同期する分類と製品の構成  

*適用対象: System Center Configuration Manager (Current Branch)*


> [!NOTE]  
>  このセクションの手順は、最上位サイトの場合のみ従ってください。  

 ソフトウェアの更新ポイント コンポーネントのプロパティで指定した設定に基づき、Configuration Manager で、同期プロセス中にソフトウェア更新メタデータが取得されます。 ソフトウェア更新を初めて同期した後、あるいは新しい製品や分類がリリースされるとき、プロパティに進み、新しい項目を選択する必要があります。 次の手順を使用し、同期させる分類と製品を構成します。  

#### <a name="to-configure-classifications-and-products-to-synchronize"></a>同期させる分類と製品を構成する方法  

1.  **Configuration Manager** コンソールで、**[管理]**、**[サイトの構成]**、**[サイト]** に移動します。

2. 中央管理サイトまたはスタンドアロン プライマリ サイトを選択します。  

3.  [ホーム **** ] タブの [設定 **** ] グループで [サイト コンポーネントの構成 ****] をクリックし、[ソフトウェアの更新ポイント ****] を選択します。

4.  [分類] タブで、ソフトウェア更新プログラムを同期させるソフトウェア更新プログラムの分類を指定します。 ****  

    > [!NOTE]  
    >  すべてのソフトウェア更新プログラムは、各種の更新プログラムを整理するための更新プログラムの分類により定義されます。 同期プロセス中に、指定した分類のソフトウェアの更新プログラムのメタデータが同期されます。 Configuration Manager には次の更新プログラムの分類でソフトウェアの更新を同期する機能が用意されています。  
    >   
    > - **重要な更新**: セキュリティに関連しない重要な不具合に対処する、特定の問題を解決するために広範にリリースされる更新プログラムを示します。  
    > - **定義ファイルの更新**: ウイルスまたはその他の定義ファイルの更新を示します。  
    > - **機能パック**: 製品リリースに先立って配布され、通常は次回の製品版リリースに含まれる、製品の新機能を示します。  
    > - **セキュリティ更新プログラム**: 製品固有でセキュリティに関係する問題に対して、広範にリリースされた更新を示します。  
    > - **Service Pack**: アプリケーションに適用される修正プログラムを累積したセットを示します。 これらの修正プログラムには、セキュリティ更新プログラム、重要な更新プログラム、ソフトウェア更新プログラムなどが含まれています。  
    > - **ツール**: 1 つまたは複数のタスクを完了するためのユーティリティまたは機能を示します。  
    > - **更新プログラムのロールアップ**: 容易に展開できるようにパッケージにまとめられた修正プログラムを累積したセットを示します。 これらの修正プログラムには、セキュリティの更新プログラム、重要な更新プログラム、更新プログラムなどが含まれています。 更新プログラムのロールアップは、通常セキュリティまたは製品コンポーネントなど特定の領域に対応します。  
    > - **更新プログラム**: 現在インストールされているアプリケーションまたはファイルの更新プログラムを示します。  
    > - **アップグレード**: Windows 10 の機能のアップグレードを指定します。  
    >   
    >      ソフトウェアの更新ポイントとサイトは最低限 WSUS 4.0 と [修正プログラム 3095113](https://support.microsoft.com/kb/3095113) を実行して、**アップグレード**の分類を取得する必要があります。  

5.  [製品 **** ] タブで、ソフトウェア更新プログラムを同期させる製品の更新の分類を指定し、[閉じる ****] をクリックします。  

    > [!NOTE]  
    >  各ソフトウェア更新プログラムのメタデータは、更新プログラムが適用される製品を定義します。 製品とは、オペレーティング システムまたはアプリケーションの特定エディションのことです (Windows Server 2012 など)。 製品ファミリは、個々の製品が派生する基礎となるオペレーティング システムまたはアプリケーションです。 製品ファミリの例として Windows があり、Windows Server 2012 はそのメンバーです。 製品ファミリまたは製品ファミリ内の個別製品を指定できます。 選択する製品が多くなるほど、ソフトウェア更新プログラムを同期させるのに必要な時間が長くなります。  
    >   
    >  ソフトウェア更新プログラムが複数の製品に適用可能な状態で、少なくとも 1 つの製品の同期を選択している場合、選択されていない製品も含めてすべての製品が Configuration Manager コンソールに表示されます。 たとえば、選択しているオペレーティング システムが Windows Server 2012 のみで、ソフトウェア更新プログラムが Windows 8 と Windows Server 2012 に適用される場合、Configuration Manager コンソールには両方の製品が表示されます。  

    > [!IMPORTANT]  
    >  Configuration Manager は、ソフトウェアの更新ポイントを初めてインストールするときに選択できる製品と製品ファミリのリストを保存します。 Configuration Manager のリリース後にリリースされる製品と製品ファミリは、選択できる使用可能な製品と製品ファミリのリストを更新する、ソフトウェア更新プログラムの同期を完了するまでは選択できない可能性があります。  


## <a name="next-steps"></a>次のステップ
ソフトウェア更新プログラムの同期を開始し、新しい基準でソフトウェア更新プログラムを取得します。 詳細については、「[ソフトウェア更新プログラムの同期](synchronize-software-updates.md)」を参照してください。



<!--HONumber=Nov16_HO1-->

