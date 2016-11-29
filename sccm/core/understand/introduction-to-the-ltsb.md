---
title: "Long-Term Servicing Branch の概要 | System Center Configuration Manager"
description: "System Center Configuration Manager の Long-Term Servicing Branch について説明します。"
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2a45cfb3e00d8078fbf45bdc8a2668b7dd0a62c6
ms.openlocfilehash: 926d1b1299e7851bd1d9168237859c5cd7a65abe


---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>System Center Configuration Manager の Long-Term Servicing Branch の概要

*適用対象: System Center Configuration Manager (Long-Term Servicing Branch)*

このトピックでは、Configuration Manager の Long-Term Servicing Branch (LTSB) と、このブランチのドキュメントについて説明します。


LTSB は、Configuration Manager のブランチの 1 つであり、Current Branch のバージョン 1606 に基づいています。 Current Branch と比較すると、LTSB の[機能は制限されています](#features-that-are-not-available-in-the-ltsb-of-configuration-manager)。 LTSB は、[ソフトウェア アシュアランス (SA) または同等のサブスクリプション権限が期限切れになることを許可した](/sccm/core/understand/learn-more-editions#software-assurance-and-the-ltsb)お客様向けに設計されています。

**ライセンスの概要:**   
2016 年 10 月 1 日の時点で System Center Configuration Manager ライセンスに対してソフトウェア アシュアランス (SA) が有効になっているお客様または同等のサブスクリプション権限を持っているお客様には、2016 年 10 月リリースのバージョン 1606 の System Center Configuration Manager を使用する権限があります。 2016 年 10 月 1 日以降、System Center Configuration Manager に対する権限を持つお客様には、インストール時に Current Branch および Long-Term Servicing Branch (LTSB) の 2 つのライセンス オプションが表示されます。

**ライセンスの詳細:**  
[Microsoft ボリューム ライセンス プログラムを通して購入する製品の使用条件についてはこちらを参照してください](http://go.microsoft.com/fwlink/?LinkId=800052)。

System Center Configuration Manager に対して永続的な権利を持つお客様または、10 月 1 日の後に SA またはサブスクリプションが期限切れになったお客様は、該当する時点で最新のバージョンである System Center Configuration Manager LTSB をインストールできます。
- System Center Configuration Manager のソフトウェア アシュアランスとライセンスの要件については、「[System Center Configuration Manager licensing and branches](learn-more-editions.md)」 (System Center Configuration Manager のライセンスとブランチ) を参照してください。
-   さまざまなブランチの違いについては、「[Which branch of Configuration Manager should I use](which-branch-should-i-use.md)」(どのブランチの Configuration Manager を使用すればよいですか) を参照してください。

新しいサイトをインストールするか、サポートされる System Center 2012 Configuration Manager サイトから LTSB にアップグレードするには、バージョン 1606 の基準メディアを使用します。 この基準メディアは、Microsoft System Center 2016 に付属する DVD または System Center Configuration Manager (Current Branch および Long-Term Servicing Branch 1606) リリースから使用できます。 LTSB をインストールできる基準メディアは、Configuration Manager の Current Branch バージョン 1606 のインストールにも使用できます。 基準メディアの詳細については、「[Baseline and update versions](/sccm/core/servers/manage/updates#baseline-and-update-versions)」(基準バージョンと更新プログラムのバージョン) を参照してください。

LTSB サイトをインストールする方法については、「[Install and Upgrade for the Long-Term Servicing Branch](install-the-ltsb.md)」(Long-Term Servicing Branch のインストールとアップグレード) を参照してください。 System Center 2016 の入手方法については、「[System Center 2016 documentation](https:\technet.microsoft.com\system-center-docs\System-Center-2016)」(System Center 2016 のドキュメント) を参照してください。

> [!IMPORTANT]
> 階層内のすべてのサイトは同じブランチを実行する必要があります。 異なるサイトに LTSB と Current Branch が混在している階層の使用はサポートされません。
>
> 同様に、復元を使用する場合、サイトまたはサイト データベースを元のブランチに復元する必要があります。 Current Branch サイト データベースを LTSB インストールに復元することはできません。また、その逆も同様です。


## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Configuration Manager の LTSB で使用できない機能
Current Branch と比較すると、LTSB には次のサポートの制限があります。

- 新しい機能の更新プログラムを受信しません。
- Microsoft Intune サブスクリプションの追加はサポートされません。そのため、以下は使用できません。
  - ハイブリッド MDM 構成の Intune
  - オンプレミス MDM
-   Windows 10 サービス ダッシュボード、サービス プランの使用、Windows 10 の Current Branch (CB) および Current Branch for Business (CBB) はサポートされません
- Windows 10 LTSB および Windows Server の今後のリリースはサポートされません
-   資産インテリジェンスはサポートされません
-   クラウドベースの配布ポイントはサポートされません
-   Exchange Connector としての Exchange Online のサポートはサポートされません
-   プレリリース機能はサポートされません


これらの機能のサポートは LTSB に含まれていません。一部の機能は Configuration Manager コンソールに表示されますが、選択または使用することはできません。

また、Current Branch のサポート対象として新しいオペレーティング システムが追加されても、LTSB のサポート対象には追加されません。

## <a name="documentation-for-the-ltsb"></a>LTSB のドキュメント
LTSB はバージョン 1606 Current Branch に基づいているので、LTSB に使用するドキュメントは、[Current Branch に適用されるオンライン ドキュメント](https://docs.microsoft.com/sccm/)です。ただし、以下のトピックで説明するように、LTSB 固有の注意事項と制限事項があります。  

-   [Long-Term Servicing Branch の概要](introduction-to-the-ltsb.md) - (このトピック)

-   [Which branch of Configuration Manager should I use](which-branch-should-i-use.md) (どのブランチの Configuration Manager を使用すればよいですか) – ニーズに合わせて最適なブランチをインストールできるように、System Center Configuration Manager ブランチの違いについて説明しています。

-   [Install the  Long-Term Servicing Branch](install-the-ltsb.md) (Long-Term Servicing Branch のインストール) - 新しい LTSB サイトをインストールする方法、System Center 2012 Configuration Manager サイトを LTSB にアップグレードする方法について説明しています。

-   [Upgrade the  Long-Term Servicing Branch to the Current Branch](convert-to-current-branch.md) (Long-Term Servicing Branch を Current Branch にアップグレードする) – LTSB インストールを Current Branch インストールに変換する方法について説明しています。

-   [Licensing and branches for System Center Configuration Manager](learn-more-editions.md) (System Center Configuration Manager のライセンスとブランチ) – System Center Configuration Manager のソフトウェア アシュアランスと関連するライセンスの要件について説明しています。
-   [Supported Configurations for the Long-Term Servicing Branch](supported-configurations-for-ltsb.md) (Long-Term Servicing Branch のサポートされる構成) - LTSB で使用できるオペレーティング システムと依存する製品 (SQL Server など) のバージョンと要件について説明しています。


適用されるブランチ固有のドキュメントを区別するには、次のガイドを参照してください。  
-   「*適用先: Current Branch*」という見出しがあるトピックは、Current Branch と Long-Term Servicing Branch の両方に適用されます (ただし、トピックの一部は新しいバージョンの Current Branch にのみ適用される場合もあります)。

-   LTSB に適用されないトピックの部分を特定するには、"バージョン 1610 以降" などの言葉で Current Branch のバージョン 1606 の後に導入された機能と変更点を特定します。 バージョン 1610 以降の機能は、1606 バージョンの Current Branch の後に導入されているので、LTSB では使用できません。

### <a name="similarities-between-the-current-branch-and-the-ltsb"></a>Current Branch と LTSB の類似点
LTSB は Current Branch バージョン 1606 に基づいています (ただし、Intune の統合やクラウド関連の機能などの例外はあります)。そのため、2 つのブランチの展開計画、構成、管理に関するほとんどのタスクは同じです。

たとえば、LTSB は、Current Branch と同じ数のサイト、サイトの種類、クライアント、全般的なインフラストラクチャをサポートしています。 そのため、Current Branch のサイトおよび階層の計画、設計に関するトピックのガイドを参照できます。 同様に、両方のブランチでサポートされる機能 (ソフトウェア更新プログラム、オペレーティング システムの展開) の場合、Current Branch ドキュメントの該当するセクションを参照できます。ただし、Current Branch の 1606 バージョンの後に導入された変更にはアクセスできないという注意点があります。


## <a name="how-to-identify-your-branch-and-version"></a>ブランチとバージョンを特定する方法
Configuration Manager サイトのバージョン情報を表示すると、ブランチも確認できます。

お使いのサイトのバージョンを確認するには、コンソールの左上にある **[System Center Configuration Manager のバージョン情報]** を選択します。**[サイトのバージョン]** に "**5.0.8412.1000**" と表示されます。

サイトのブランチ (LTSB または Current Branch) を確認するには、コンソールで **[管理]** > **[サイトの構成]** > **[サイト]** を選択し、**[階層設定]** を開きます。  Current Branch に変換するオプションがあり、選択できる状態の場合、サイトは LTSB バージョンを実行しています。 サイトが Current Branch を実行している場合、このオプションは淡色表示されます。

さまざまなバージョンの Configuration Manager については、「[Updates for Configuration Manager](/sccm/core/servers/manage/updates)」(Configuration Manager の更新プログラム) トピックの「**Baseline and update versions**」(基準と更新プログラムのバージョン) を参照してください。

## <a name="exceptions-for-using-the-ltsb"></a>LTSB の使用に関する例外
### <a name="updates-and-servicing-of-the-ltsb"></a>LTSB の更新プログラムとサービス
LTSB のコンソール内更新プログラムでは、重要なセキュリティ更新プログラムのみを使用できます。

ただし、コンソールには、以降の Current Branch リリース用の通常の更新プログラムに関する情報が表示されます。 これらの更新プログラムは LTSB に使用できないので、ダウンロードされず、インストールすることもできません。

重要なセキュリティ修正プログラムについてコンソール内更新プログラムをサポートするには、LTSB で[サービス接続ポイント](/sccm/core/servers/deploy/configure/about-the-service-connection-point)を使用する必要があります。 Current Branch と同様に、このサイト システムの役割はオフライン モードまたはオンライン モードで構成できます。 LTSB は、Current Branch と同じテレメトリと使用状況データを収集および送信します。

LTSB は、Current Branch のドキュメントで説明されているように、Hotfix Installer and Update Registration ツールの使用をサポートしています。

更新プログラムとサービスの全般的な情報については、「 [Updates for Configuration Manager](/sccm/core/servers/manage/updates)」(Configuration Manager の更新プログラム) を参照してください。

### <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>サイトの拡張と CD.Latest フォルダーの変更
新しい中央管理サイトをインストールして LTSB を実行し、スタンドアロンのプライマリ サイトを実行する場合、1606 基準メディアのセットアップおよびソース ファイルを使用する必要があります  (Current Branch の場合、CD.Latest フォルダーのセットアップを実行し、ソース ファイルを使用します)。

サイトの拡張には CD.Latest フォルダーのセットアップを実行しませんが、サイトの回復には CD.Latest フォルダーを使用します。また、最初の LTSB サイトが中央管理サイトだったときに、新しい子プライマリ サイトをインストールする場合にも、CD.Latest フォルダーを使用します。

サイトの拡張の詳細については、「[Use the Setup Wizard to install sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)」(セットアップ ウィザードを使用してサイトをインストールする) の「[Expand a stand-alone primary site](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site)」(スタンドアロン プライマリ サイトを拡張する) を参照してください
CD.Latest フォルダーの詳細については、「[The CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder)」(CD.Latest フォルダー) を参照してください。



<!--HONumber=Nov16_HO1-->


