---
title: "SQL Server クラスター | Microsoft Docs"
description: "SQL Server クラスターを使用して System Center Configuration Manager サイト データベースをホストします。 サポートされているオプションに関する情報が含まれます。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e5a001ee018e240396498d134c5e75e325eae275


---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>SQL Server クラスターを使用した System Center Configuration Manager サイト データベースのホスト

*適用対象: System Center Configuration Manager (Current Branch)*


 SQL Server クラスターを使用して System Center Configuration Manager サイト データベースをホストします。 サイト データベースは、サーバー クラスターでサポートされているサイト システムの役割として唯一のものです。  

> [!NOTE]  
>  正常に構成して SQL Server クラスターを使用するには、SQL Server クラスターの構成が容易にこなせることが必要であり、SQL Server ドキュメント ライブラリで提供されているドキュメントと手順に従って作業します。  

 クラスターを使用すると、フェールオーバーをサポートできるため、サイト データベースの信頼性を高めることができます。 ただし、クラスター化されたサイト データベースを使用しても、処理や負荷分散に関するメリットが増えることはありません。 さらに、サイト サーバーが、サイト データベースに接続する前に SQL Server クラスターのアクティブ ノードを検索する必要があるため、パフォーマンスの低下が発生する可能性があります。  

 Configuration Manager をインストールする前に、Configuration Manager をサポートするために SQL Server クラスターを準備する必要があります。 (このセクションで後ほど説明する前提条件をご覧ください)。  

 Configuration Manager のセットアップ中に、[**サイト サーバーのバックアップ**] メンテナンス タスクをサポートするために、Microsoft Windows Server クラスターの各物理コンピューター ノードにボリューム シャドウ コピー サービス (VSS) ライターがインストールされます。  

 サイトのインストール後に Configuration Manager は、1 時間ごとにクラスター ノードが変更されたかどうかを確認し、Configuration Manager コンポーネントのインストールに影響する、検出したすべての変更 (ノードのフェールオーバーや SQL Server クラスターへの新しいノードの追加など) を自動的に管理します。  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>SQL Server フェールオーバー クラスターの使用でサポートされるオプション

-   単一インスタンス クラスター  

-   複数インスタンス構成  

-   複数のアクティブ ノード  

-   名前付きインスタンスと既定のインスタンスの両方がサポートされます。  

**必要条件:**  

-   サイト データベースは、サイト サーバーからリモートである必要があります (クラスターは、サイト システム サーバーを含めることはできません)。  

-   サイト サーバーのコンピューター アカウントを、クラスター内の各サーバーのローカルの Administrators グループに追加しなければなりません。  

-   Kerberos 認証をサポートするには、 **TCP/IP** ネットワーク通信プロトコルを各 SQL Server クラスター ノードのネットワーク接続に対して有効にする必要があります。 **名前付きパイプ** は不要ですが、Kerberos 認証に問題が発生したときのトラブルシューティングに使用できます。 ネットワーク プロトコルの設定は、 **[SQL Server ネットワークの構成]** にある **[SQL Server 構成マネージャー]**で構成します。  

-   PKI を使用する場合は、「&lt;Configuration Manager での PKI 証明書の要件>」を参照し、サイト データベースに SQL Server クラスターを使用する場合に必要となる特定の証明書の要件を確認します。  

**考慮する制限事項:**  

-   **インストールおよび構成:**  

    -   セカンダリ サイトには、SQL Server クラスターを使用できません。  

    -   サイト データベースに対して既定以外のファイルの場所を指定するオプションは、SQL Server クラスターを指定する場合は使用できません。  

-   **SMS プロバイダー:**  

    -   SQL Server クラスター、またはクラスター化された SQL Server ノードとして実行されるコンピューターに SMS プロバイダーのインスタンスをインストールすることはサポートされていません。  

-   **データ レプリケーションのオプション:**  

    -   **分散ビュー**を使用する場合は、サイト データベースをホストするために SQL Server クラスターを使用することはできません。  

-   **バックアップと回復:**  

    -   Configuration Manager では、名前付きインスタンスを使用する SQL Server クラスターの DPM バックアップはサポートしていませんが、SQL Server の既定インスタンスを使用する SQL Server クラスターの DPM バックアップはサポートしています。  

## <a name="to-prepare-a-clustered-sql-server-instance-for-the-site-database"></a>サイト データベースに対してクラスター化された SQL Server インスタンスを準備するには  

-   サイト データベースをホストする仮想 SQL Server クラスターを既存の Windows Server クラスター環境で作成します。 SQL Server クラスターをインストールおよび構成するための特定の手順については、使用している SQL Server のバージョンのドキュメントをご覧ください。 たとえば、SQL Server 2008 R2 を使用している場合は、  [SQL Server 2008 R2 フェールオーバー クラスターのインストール](http://go.microsoft.com/fwlink/p/?LinkId=240231)に関するページをご覧ください。 SQL Server 2014 を使用している場合は、「 [SQL Server フェールオーバー クラスターのインストール](https://technet.microsoft.com/library/hh231721\(v=sql.120\).aspx)」をご覧ください。  

-   SQL Server クラスター内の各コンピューターで、ドライブのルート フォルダーに **NO_SMS_ON_DRIVE.SMS** という名前のファイルを配置すると、Configuration Manager はサイト コンポーネントをそのドライブにインストールしません。 既定では、Configuration Manager は各物理ノードにいくつかのコンポーネントをインストールして、バックアップなどの操作をサポートします。  

-   サイト サーバーのコンピューター アカウントを、各 Windows Server クラスター ノード コンピューターのローカルの [Administrators] グループに追加します。 ****  

-   仮想 SQL Server インスタンスで、Configuration Manager セットアップを実行するユーザー アカウントに、**sysadmin** という SQL Server の役割を割り当てます。  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>クラスター化された SQL Server を使用して新しいサイトをインストールするには  
 クラスター化されたサイト データベースを使用するサイトをインストールするには、次の部分を変更したうえで通常のサイトのインストール プロセスに従って、Configuration Manager のセットアップを実行します。  

-   **[データベース情報]** ページで、サイト データベースをホストする仮想 SQL Server クラスター インスタンスの名前を指定します。  仮想インスタンスは、SQL Server を実行するコンピューターの名前を置き換えます。  

    > [!IMPORTANT]  
    >  仮想 SQL Server クラスター インスタンスの名前を入力するとき、Windows Server クラスターによって作成される仮想 Windows Server 名を入力しないでください。 仮想 Windows Server 名を使用すると、サイト データベースが、アクティブな Windows Server クラスター ノードのローカル ハード ディスクにインストールされます。 これにより、そのノードに障害が発生しても、正常にフェールオーバーできません。  



<!--HONumber=Dec16_HO3-->


