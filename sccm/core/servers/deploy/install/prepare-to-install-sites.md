---
title: "サイトのインストールの準備 | Microsoft Docs"
description: "複数のサイトのインストール中に時間を節約し、エラーを回避するために、これらの詳細を確認してください。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 0534d1eb587cb01f35d811d72ddfe6ceb07e5b7c

---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>System Center Configuration Manager サイトのインストールを準備する

*適用対象: System Center Configuration Manager (Current Branch)*

1 つ以上の System Center Configuration Manager サイトの適切な展開を準備するには、この記事の詳細を理解してください。 次の手順で、複数のサイトのインストールの時間を節約し、1 つ以上のサイトの再インストールが必要になるような失敗を防ぎます。
 > [!TIP]
 >  次のシナリオは、次と同様が、System Center Configuration Manager の現在ブランチ サイトのインストールと似ていますが、異なります。
 > -  **アップグレード**: System Center Configuration Manager をインストールして System Center 2012 Configuration Manager から**アップグレード**します。「[Upgrade to System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)」(System Center Configuration Manager へのアップグレード) を参照してください。
 > -  **更新**: コンソールで更新プログラムを使用して、新しい**更新プログラムのバージョン** を既存の System Center Configuration Manager サイトにインストールします。「[Updates for System Center Configuration Manager](../../../../core/servers/manage/updates.md)」 (System Center Configuration Manager の更新) を参照してください。
 > -  **移行**: 別の Configuration Manager 階層から現在の System Center Configuration Manager 階層に**データを移行**するには、「[Planning for migration to System Center Configuration Manager](../../../../core/migration/planning-for-migration.md)」(System Center Configuration Manager への移行の計画) を参照してください。



## <a name="a-namebkmkoptionsa-options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a> 異なる種類のサイトをインストールするためのオプション
新しい Configuration Manager をインストールする場合は、使用可能なソース ファイルのバージョンは、既に階層内にあるサイトのバージョン (存在する場合) に依存し、使用可能なインストール方法はインストールするサイトの種類に依存します。  

サイトをインストールする前に、階層を計画したことを確認し、インストールするサイトの種類を理解してください。 詳細については、「[Design a hierarchy of sites](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)」(サイトの階層の設計) を参照してください。


### <a name="first-site"></a>最初のサイト
階層にインストールするこの最初のサイトは、中央管理サイトまたはスタンドアロンのプライマリ サイトのいずれかです。

**インストール メディア**: 中央管理サイトまたはスタンドアロンのプライマリ サイトを新しい階層で最初のサイトとしてインストールするには、Configuration Manager の[基準バージョンを使用する](../../../../core/servers/manage/updates.md#bkmk_Baselines)必要があります。 サイトの [CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) フォルダーから更新されたソース ファイルを使用して、新しい階層の最初のサイトをインストールしないでください。

**インストール方法**: [Configuration Manager のセットアップ ウィザード](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)を使用していずれかの種類のサイトをインストールするか、[スクリプトを使用してコマンドラインからインストール](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)するために使用するスクリプトを構成することができます。


### <a name="additional-sites"></a>追加のサイト
最初のサイトをインストールした後、いつでもサイトを追加することができます。 サイトを追加するには次のオプションがあります ([サポートされている制限](../../../../core/plan-design/configs/size-and-scale-numbers.md)以内)。

既存のサイト          |インストール可能な追加サイト  
---------                   |---------
中央管理サイト |   子プライマリ サイトをインストールする            
子プライマリ サイト          |   セカンダリ サイトをインストールする        
スタンドアロン プライマリ サイト    |   セカンダリ サイトをインストールする<br />プライマリ サイト拡張する。スタンドアロン プライマリ サイトを子プライマリ サイトに変換します。

**インストール メディア**: 中央管理サイトをスタンドアロン プライマリ サイトにインストールして拡張する場合、または新しい子プライマリ サイトを既存の階層にインストールする場合は、既存のサイトのバージョンに対応するインストール メディア (ソース ファイル) を使用する必要があります。
> [!IMPORTANT]
> コンソール内の更新プログラムをインストールした結果、以前にインストールしたサイトのバージョンが変更された場合は、更新したサイトの元のインストール メディアを使用するのではなく、[CD.Latest フォルダー](../../../../core/servers/manage/the-cd.latest-folder.md)にあるソース ファイルを使用してください。  Configuration Manager では、新しいサイトが接続する既存のサイトのバージョンに対応したソース ファイルを使用する必要があります。


セカンダリ サイトは、Configuration Manager コンソール内からインストールする必要があるので、常に親プライマリ サイトからソース ファイルを使用してインストールします。

**インストール方法**: 追加のサイトのインストールに使用する方法は、インストールするサイトの種類によって異なります。
-   **中央管理サイトを追加する**  
Configuration Manager のセットアップ ウィザードまたはスクリプト化されたコマンド ラインを使用すると、既存のスタンドアロン プライマリ サイトに親サイトとして新しい中央管理サイトをインストールすることができます。  詳細については、「[スタンドアロン プライマリ サイトを拡張する](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)」を参照してください。
-   **子プライマリ サイトを追加する**  
Configuration Manager のセットアップ ウィザードまたはコマンド ライン インストールを使用すると、中央管理サイトの下に子プライマリ サイトを追加することができます。
-   **セカンダリ サイトを追加する**   
Configuration Manager コンソールを使用して、プライマリ サイトの下に子サイトとしてセカンダリ サイトをインストールします。 セカンダリ サイトでは、その他の方法はサポートされていません。



## <a name="a-namebkmktasksa--common-tasks-to-complete-before-starting-an-install"></a><a name="bkmk_tasks"></a>  インストールを開始する前に完了する一般的なタスク
-   展開に使用する階層トポロジを把握します     
     (「[System Center Configuration Manager のサイト階層の設計](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)」を参照してください)。  

-   Configuration Manager で使用するための前提条件とサポートされる構成を満たす個別のサーバーを準備および構成します (「[サイトとサイト システムの前提条件](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md)」を参照してください)。  

-   サイト データベースをホストするように SQL Server をインストールして構成します (    
    「[System Center Configuration Manager の SQL Server バージョンのサポート](../../../../core/plan-design/configs/support-for-sql-server-versions.md)」を参照してください)。  

-   Configuration Manager をサポートするためにネットワーク環境を準備します (「[Configure firewalls, ports, and domains to prepare for Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains)」(Configuration Manager を準備するためにファイアウォール、ポート、およびドメインを構成する) を参照してください)。  

-   PKI を使用する場合は、インフラストラクチャと証明書を準備すします (「[Configuration Manager での PKI 証明書の要件](../../../../core/plan-design/network/pki-certificate-requirements.md)」を参照してください)。

-   サイト サーバーまたはサイト システム サーバーとして使用するコンピューターに最新のセキュリティ更新プログラムをインストールし、必要な場合はそれらを再起動します。



## <a name="a-namebkmksitecodesa--about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a>  サイト名とサイト コードについて
サイト コードとサイト名は、Configuration Manager 階層内でサイトを識別および管理するために使用します。 Configuration Manager コンソールには、サイト コードとサイト名が、&lt;サイト コード\> - &lt;サイト名\> の形式で表示されます。 階層にあるサイトごとに固有なサイト コードが付いている必要があります。 Active Directory スキーマが Configuration Manager 用に拡張されており、サイトがデータを発行する場合は、Active Directory フォレスト内で使用するサイト コードは、必ず固有でなければなりません。サイトが Configuration Manager の別の階層や以前の Configuration Manager のインストールで使用されていても、同じサイト コードを付けることはできません。 階層を展開する前に、どのようなサイト コードとサイト名を使用するかを、十分検討してください。

### <a name="specify-a-site-code-and-site-name"></a>サイト コードとサイト名の指定
Configuration Manager のセットアップ時に、インストールする中央管理サイト、プライマリ サイト、セカンダリ サイトのサイト コードとサイト名を指定する必要があります。 サイト コードは、階層にある各サイトを識別できる固有なコードでなければなりません。 サイト コードはフォルダー名の一部になるので、次の名前 ( Configuration Manager や Microsoft Windows で予約されている名前など) をサイト コードに使用しないでください。
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> Configuration Manager のセットアップでは、指定したサイト コードが既に使用されていないかどうかは検証されません。



Configuration Manager のセットアップ中にサイト コードを指定するときは、必ず 3 文字の英数字を入力してください。 A ～ Z の文字、0 ～ 9 の数字、またはこれらの組み合わせだけを使用できます。 文字や数字の順序は、サイト間の通信には影響しません。 たとえば、プライマリ サイトに ABC、セカンダリ サイトに DEF という名前を付ける必要はありません。

サイト名とは、サイトを識別するわかりやすい名前のことです。 A ～ Z、a ～ z、0 ～ 9、およびハイフン (-) だけを使ってください。
> [!IMPORTANT]
> サイトをインストールした後で、サイト コードやサイト名を変更することはできません。

### <a name="reuse-a-site-code"></a>サイト コードの再利用
Configuration Manager 階層内で中央管理サイトまたはプライマリ サイトにサイト コードを複数回使用することはできません。元のサイトとサイト コードがアンインストールされた場合でも同じです。 サイト コードを再利用すると、オブジェクト ID が階層で競合する可能性があります。 セカンダリ サイトやサイト コードを Configuration Manager の階層や Active Directory フォレストで使用しなくなった場合は、そのセカンダリ サイトのサイト コードを再利用することができます。


## <a name="limits-and-restrictions-for-installed-sites"></a>インストール後のサイトの制限と制約
サイトをインストールする前に、サイトと階層に適用される次の制限事項を理解します。
-   セットアップの完了後は、サイトをアンインストールしてから新しい値で再インストールしない限り、次のサイトのプロパティを変更することはできません。  
    -   プログラム ファイルのインストール ディレクトリ  
    -   サイト コード  
    -   サイトの説明  
-   階層に中央管理サイトが含まれている場合:  
    -   Configuration Manager では、階層から子プライマリ サイトを移動して、スタンドアロン プライマリ サイトを作成したり異なる階層に接続したりすることはできません。 代わりに、子プライマリ サイトをアンインストールし、新しいスタンドアロンのプライマリ サイトまたは別の階層の中央管理サイトの子サイトとして再インストールします。  


## <a name="a-namebkmkoptionalstepsa--optional-steps-to-run-before-starting-setup"></a><a name="bkmk_optionalsteps"></a>  セットアップを開始する前に実行するオプションの手順
**[セットアップ ダウンローダー](../../../../core/servers/deploy/install/setup-downloader.md)**を手動で実行し、Configuration Manager の更新されたセットアップ ファイルをダウンロードすることができます。

セットアップを実行するコンピューターがインターネットに接続されていない場合、または複数のサイト サーバーをインストールする場合は、セットアップ ダウンローダーを使用して、セットアップ ファイルの必要な更新プログラムをダウンロードすることをご検討ください。

-  既定では、セットアップはインターネットに接続して、更新されたセットアップ ファイルをダウンロードします
-  既定では、Redist という名前のフォルダーにファイルが格納されます
-  以前にこれらのファイルのコピーを格納したネットワーク上の場所を指定できます


**セットアップを実行する前に [Prerequisite Checker](../../../../core/servers/deploy/install/prerequisite-checker.md)** を手動で実行して、問題を特定して修正できます。 セットアップを開始してサイトをインストールする前、およびサーバーにサイト システムの役割をインストールする前に、前提条件チェッカーを実行して、コンピューターがサイトまたはサイト システムの役割をホストするための要件を満たしていることを確認できます。
 -  既定では、セットアップは前提条件チェッカーを実行します。
 -  エラーが発生した場合は、問題が解決するまでセットアップは停止します。


サイト システムとクライアントに使用する**オプションのポートを特定** します。
 -  既定では、サイト システムとクライアントは通信に定義済みのポートを使用します。
 -  セットアップ時に、代替ポートを構成することができます。
 -  詳細については、「[System Center Configuration Manager で使用されるポート](../../../../core/plan-design/hierarchy/ports.md)」を参照してください。



<!--HONumber=Dec16_HO3-->


