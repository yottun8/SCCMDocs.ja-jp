---
title: "ビジネス向け Windows ストアからのアプリの管理 | System Center Configuration Manager"
description: "System Center Configuration Manager を使用してビジネス向け Windows ストアからアプリを管理および展開します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: 11
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e293b2ec4debf7a8513f1e3544ac234616f04d7

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>System Center Configuration Manager によるビジネス向け Windows ストアからのアプリの管理

*適用対象: System Center Configuration Manager (Current Branch)*

[ビジネス向け Windows ストア](https://www.microsoft.com/business-store)は、組織向けのアプリを検索して、個別に、または一括で購入できる場所です。 Configuration Manager にストアを接続することで、購入したアプリのリストを Configuration Manager と同期し、それらを Configuration Manager コンソールで表示し、他のアプリと同様に展開できます。


## <a name="online-and-offline-apps"></a>オンライン アプリとオフライン アプリ

ビジネス向け Windows ストアは、次の 2 種類のアプリをサポートしています。

- **オンライン** - この種類のライセンスでは、ユーザーとデバイスはストアに接続してアプリとそのライセンスを取得する必要があります。 Windows 10 デバイスは、Azure Active Directory ドメインに参加している必要があります。
- **オフライン** - ストアに接続したり、インターネットに接続したりせずに、組織はアプリとラインセンスをキャッシュして、そのオンプレミス ネットワークに展開できます。

ビジネス向け Windows ストアの詳細については、[こちら](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview)を参照してください。

Configuration Manager では、Configuration Manager クライアントを実行している Windows 10 デバイスと、Microsoft Intune に登録されている Windows 10 デバイスの両方でビジネス向け Windows ストアのアプリを管理できます (ハイブリッド構成と呼ばれます)。 Configuration Manager は、オンラインおよびオフライン アプリ向けに次の機能を提供します。

> [!IMPORTANT]
> この機能を使用するには、Windows 10 デバイスで 2015 年 11 月 (1511) リリース以降が実行されている必要があります。

|機能|オフライン アプリ|オンライン アプリ|
|------------|------------|------------|
|アプリ データと Configuration Manager の同期<br>(同期は 24 時間ごとに発生)|○|○|
|ストア アプリからの Configuration Manager アプリケーションの作成|○|○|
|ストアからの無料アプリのサポート|○|○|
|ストアからの有料アプリのサポート|×|いいえ|
|ユーザーまたはデバイス コレクションへの必要な展開のサポート|○|○<sup>1</sup>|
|ユーザーまたはデバイス コレクションへの利用可能な展開のサポート|○<sup>3</sup>|×<sup>2</sup>|

<sup>1</sup> Intune で管理されているデバイスのみをサポートします。 Configuration Manager コンソールでオンライン アプリケーションを作成し、Configuration Manager クライアントが管理するデバイスに展開することは禁止されていませんが、これは正しく機能しません。 エンド ユーザーは、アプリ ストアの該当するページにリダイレクトされ、そこでアプリを手動でインストールする必要があります。

<sup>2</sup> オンライン アプリは、Configuration Manager クライアントで管理されているデバイスのユーザーまたはデバイス コレクションにのみ利用可能として展開できます。ただし、エンド ユーザーは、ソフトウェア センターでアプリを選択すると、ビジネス向け Windows ストアにリダイレクトされ、そこでアプリを手動でインストールする必要があります。 Microsoft Intune に登録されたデバイスへの利用可能な展開はサポートされていません。

<sup>3</sup> Intune で管理されているデバイスはサポートされていません。

> [!IMPORTANT]
> このリリースでは、中央管理サイトと少なくとも 1 つのプライマリ サイトを含む Configuration Manager 階層がある場合、ビジネス向け Windows ストアのオフライン アプリを Intune で管理されているデバイスに展開する操作は失敗します。


## <a name="activate-the-windows-store-for-business-capability"></a>ビジネス向け Windows ストアの機能のアクティブ化
これはプレリリース機能であるため、Configuration Manager をビジネス向け Windows ストアに接続する前に、以下の手順を実行する必要があります。

**プレリリース版の機能の使用に同意する**
1. Configuration Manager コンソールの **[管理]** ワークスペースで、**[サイトの構成]** > **[サイト]** の順にクリックします。
2. 階層内の最上位のサイトを選択し、**[階層設定]** を開きます。
3. **[階層プロパティの設定]** ダイアログ ボックスで、**[プレリリース機能を使用することに同意する]** チェック ボックスをオンにします。
4. **[OK]**をクリックします。

**ビジネス向け Windows ストア機能のアクティブ化**
1. Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]** > **[更新プログラムとサービス]** > **[機能]** の順にクリックします。
2. **[ビジネス向け Windows ストアの統合]** を選択し、**[ホーム]** タブの **[機能]** グループで、**[有効にする]** をクリックします。
3. Configuration Manager コンソールをいったん閉じてから再び開きます。
4. **[ビジネス向け Windows ストア]** が、**[管理]** ワークスペースの **[クラウド サービス]** の下に表示されます。

## <a name="set-up-windows-store-for-business-synchronization"></a>ビジネス向け Windows ストアの同期の設定

**Azure Active Directory で、"Web アプリケーションや Web API" 管理ツールとして Configuration Manager を登録します。後で必要なクライアント ID が表示されます。**
1. [https://manage.windowsazure.com](https://manage.windowsazure.com) の Active Directory ノードで、Azure Active Directory を選択し、**[アプリケーション]** > **[追加]** をクリックします。
2.  **[組織で開発中のアプリケーションを追加]** をクリックします。
3.  アプリケーションの名前を入力し、**[Web アプリケーション]** または **[Web API]**、あるいはその両方を選択し、**次へ進む**矢印をクリックします。
4.  **[サインオン URL]** と **[アプリケーション ID/URI]** の両方に同じ URL を入力します。 URL はあらゆるものを使用でき、実際のアドレスに解決する必要はありません。 たとえば、*https://yourdomain>/sccm* を入力できます。
5.  ウィザードを完了します。

**Azure Active Directory で、登録済み管理ツールのクライアント キーを作成します。**
1.  作成したアプリケーションを強調表示し、**[構成]** をクリックします。
2.  **[キー]** で、リストから期間を選択して、**[保存]** をクリックします。 これにより、新しいクライアント キーが作成されます。 ビジネス向け Windows ストアを Configuration Manager に正常にオンボードするまで、このページから移動しないでください。

**ビジネス向け Windows ストアで、ストア管理ツールとして Configuration Manager を構成します。**
1.  [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) を開き、サインインを求められたらサインインします。
2.  要求された場合は、使用条件に同意します。
3.  **[管理ツール]** で、**[Add a management tool]** (管理ツールを追加) をクリックします。
4.  **[Search for the tool by name]** (名前でツールを検索) で、先ほど AAD で作成したアプリケーションの名前を入力して、**[追加]** クリックします。
5.  インポートしたアプリケーションの横にある **[アクティブ化]** をクリックします。
6.  オフラインでライセンスされるアプリケーションを購入する場合、**[管理] > [アカウント情報]** ページで、**[オフラインでライセンスされたアプリの表示]** をクリックします。

**ストアのアカウントを Configuration Manager に追加します。**

1. ビジネス向け Windows ストアから少なくとも 1 つのアプリを購入したことを確認します。Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]** を展開し、**[ビジネス向け Windows ストア]** をクリックします。
2.  **[ホーム]** タブの**[ビジネス向け Windows ストア]** グループで、**[ビジネス向け Windows ストア アカウントの追加]** をクリックします。
3.  Azure Active Directory からテナント ID、クライアント ID、クライアント キーを追加し、ウィザードを完了します。
4. 完了した時点で、Configuration Manager コンソールの **[ビジネス向け Windows ストア]** で構成されたアカウントが表示されます。


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>ビジネス向け Windows ストアのアプリから Configuration Manager アプリケーションを作成して展開します。
1.  Configuration Manager コンソールの **[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** を展開し、**[ストア アプリのライセンス情報]** をクリックします。
2.  展開するアプリを選び、**[ホーム]** タブの **[作成]** グループで、**[アプリケーションの作成]** をクリックします。
ビジネス向け Windows ストアのアプリを含む Configuration Manager アプリケーションが作成されます。 他の Configuration Manager のアプリケーションと同様に、このアプリケーションを展開して監視できます。

> [!IMPORTANT]
> Intune に登録されたデバイスの場合、展開されたアプリは当初デバイスを登録したユーザーのみが利用できます。 それ以外のユーザーはアプリにアクセスできません。

## <a name="monitor-windows-store-for-business-apps"></a>ビジネス向け Windows ストアのアプリの監視

**[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** を展開し、**[ストア アプリのライセンス情報]** をクリックします。

管理するストア アプリごとに、アプリの情報を表示できます。これには、アプリの名前、プラットフォーム、所有しているアプリのライセンスの数、利用可能なライセンスの数が含まれます。



<!--HONumber=Nov16_HO1-->


