---
title: "ビジネス向け Windows ストアからのアプリの管理 | Microsoft Docs"
description: "System Center Configuration Manager を使用してビジネス向け Windows ストアからアプリを管理および展開します。"
ms.custom: na
ms.date: 02/14/2017
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
ms.sourcegitcommit: f955b5aadfc617e08d5d933dee8e42de838f83c0
ms.openlocfilehash: bf2937f5ba86db19d9cb40e2c98cbb8ba365f7eb
ms.lasthandoff: 02/15/2017

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>System Center Configuration Manager によるビジネス向け Windows ストアからのアプリの管理

*適用対象: System Center Configuration Manager (Current Branch)*

[ビジネス向け Windows ストア](https://www.microsoft.com/business-store)は、組織向けの Windows アプリを検索して、個別に、または一括で購入できる場所です。 Configuration Manager にストアを接続することで、購入したアプリのリストを Configuration Manager と同期し、それらを Configuration Manager コンソールで表示して、他のアプリと同様に展開できます。


## <a name="online-and-offline-apps"></a>オンライン アプリとオフライン アプリ

ビジネス向け Windows ストアは、次の&2; 種類のアプリをサポートしています。

- **オンライン** - この種類のライセンスでは、ユーザーとデバイスはストアに接続してアプリとそのライセンスを取得する必要があります。 Windows 10 デバイスは、Azure Active Directory ドメインに参加している必要があります。
- **オフライン** - ストアに接続したり、インターネットに接続したりせずに、組織はアプリとラインセンスをキャッシュして、そのオンプレミス ネットワークに展開できます。

ビジネス向け Windows ストアの詳細については、[こちら](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview)を参照してください。

Configuration Manager では、Configuration Manager クライアントを実行している Windows 10 デバイスと、Microsoft Intune に登録されている Windows 10 デバイスでビジネス向け Windows ストアのアプリを管理できます (ハイブリッド構成)。 Configuration Manager は、オンラインおよびオフライン アプリ向けに次の機能を提供します。

> [!IMPORTANT]
> これらの機能を使用するには、Windows 10 デバイスで 2015 年 11 月 (1511) リリース以降が実行されている必要があります。

|機能|オフライン アプリ|オンライン アプリ|
|------------|------------|------------|
|アプリ データと Configuration Manager の同期<br>(同期は 24 時間ごとに行われます。即刻、同期を開始することもできます。)|○|○|
|ストア アプリからの Configuration Manager アプリケーションの作成|○|○|
|ストアからの無料アプリのサポート|○|○<sup>1</sup>|
|ストアからの有料アプリのサポート|いいえ|○<sup>1</sup>|
|ユーザーまたはデバイス コレクションへの必要な展開のサポート|○|○<sup>1</sup>|
|ユーザーまたはデバイス コレクションへの利用可能な展開のサポート|はい<sup>2</sup>|いいえ|

<sup>1</sup> Intune で管理されているデバイスのみサポートされます。 Configuration Manager コンソールでオンライン アプリケーションを作成し、Configuration Manager クライアントが管理するデバイスに展開することは禁止されていませんが、展開は正しく機能しません。 ユーザーはアプリ ストアの該当ページにリダイレクトされるので、そこでアプリを手動でインストールします。

<sup>2</sup>Configuration Manager クライアントで管理されるデバイスのみサポートされます。

<!--- ## Activate the Windows Store for Business capability
Because this is a pre-release feature, before you can connect Configuration Manager to the Windows Store for Business, you must take the following steps:

**Give your consent to use pre-release features**
1. In the **Administration** workspace of the Configuration Manager console, choose **Site Configuration** > **Sites**.
2. Select the top-level site in your hierarchy, then, open **Hierarchy Settings**.
3. In the **Hierarchy Settings Properties** dialog box, check the box, **Consent to use Pre-Release** features.
4. Choose **OK**.

**Activate the Windows Store for Business capability**
1. In the **Administration** workspace of the Configuration Manager console, choose **Cloud Services** > **Updates and Servicing** > **Features**.
2. Select **Windows Store for Business Integration**, and then in the **Home** tab, in the **Features** group, choose **Turn on**.
3. Close and re-open the Configuration Manager console.
4. You'll now see the node **Windows Store for Business** in the **Administration** workspace under **Cloud Services**. --->

## <a name="set-up-windows-store-for-business-synchronization"></a>ビジネス向け Windows ストアの同期の設定

> [!IMPORTANT]
> Configuration Manager とビジネス向け Windows ストアの間の接続を設定するとき、ストアから同期されたアプリ コンテンツが保存するフォルダーを指定する必要があります。
このフォルダーが安全であり、そのコンテンツをデバイスに展開できるようにするには、次のアクセス許可を配置します。
-    サービス接続ポイント サイト システム ロール (階層の最上位サイト) をインストールするコンピューターで、**Computer$** アカウントを利用して指定したフォルダーの読み書き権限を用意する必要があります。
-    アプリの作成者に、指定したフォルダーの読み取り権限を与える必要があります。
-    SMS プロバイダーのインスタンスをホストする各コンピューターの **Computer$** アカウントで、指定したフォルダーを使用できる必要があります。


Azure Active Directory で、Configuration Manager を Web アプリケーションまたは Web API 管理ツールとして登録します。 後で必要なクライアント ID が表示されます。
1. [https://manage.windowsazure.com](https://manage.windowsazure.com) の Active Directory ノードで、Azure Active Directory を選択し、**[アプリケーション]**、**[追加]** を選択します。
2.  **[組織で開発中のアプリケーションを追加]** を選択します。
3.  アプリケーションの名前を入力し、**[Web アプリケーション]** と **[Web API]** の一方または両方を選択し、**[次へ]** を選択します。
4.  **[サインオン URL]** と **[アプリケーション ID/URI]** の両方に同じ URL を入力します。 URL はあらゆるものを使用でき、実際のアドレスに解決する必要はありません。 たとえば、*https://yourdomain/sccm* を入力できます。
5.  ウィザードを終了します。

Azure Active Directory で、登録済み管理ツールのクライアント キーを作成します。
1.  作成したアプリケーションを強調表示し、**[構成]** を選択します。
2.  **[キー]** で、リストから期間を選択し、**[保存]** を選択します。 これにより、新しいクライアント キーが作成されます。 ビジネス向け Windows ストアを Configuration Manager に正常にオンボードするまで、このページから移動しないでください。

ビジネス向け Windows ストアで、ストア管理ツールとして Configuration Manager を設定します。
1.  [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) を開き、サインインを求められたらサインインします。
2.  要求された場合は、使用条件に同意します。
3.  **[管理ツール]** で、**[Add a management tool]** (管理ツールを追加) を選択します。
4.  **[Search for the tool by name]** (名前でツールを検索) で、先ほど Azure Active Directory で作成したアプリケーションの名前を入力して、**[追加]** を選択します。
5.  インポートしたアプリケーションの横にある **[アクティブ化]** を選択します。
6.  オフラインでライセンスされるアプリケーションを購入する場合、**[管理]、[アカウント情報]** ページで、**[オフラインでライセンスされたアプリの表示]** をクリックします。

> [!Note]
> ビジネス向け Windows ストアのアプリの展開に複数の管理ツールを使用している場合、以前はそれらのうちの&1; つのみをビジネス向け Windows ストアと関連付けることができました。 今では Intune や Configuration Manager など、複数の管理ツールをストアと関連付けることができます。

ストアのアカウントを Configuration Manager に追加します。

1. ビジネス向け Windows ストアから少なくとも&1; つのアプリを購入します。 Configuration Manager コンソールの**管理**ワークスペースで、**[クラウド サービス]** を展開して、**[ビジネス向け Windows ストア]** を選択します。
2.  **[ホーム]** タブの**[ビジネス向け Windows ストア]** グループで、**[ビジネス向け Windows ストア アカウントの追加]** を選択します。
3.  Azure Active Directory からテナント ID、クライアント ID、クライアントの秘密鍵を追加し、ウィザードを完了します。
4. 完了した時点で、Configuration Manager コンソールの **[ビジネス向け Windows ストア]** で設定されたアカウントが表示されます。

ユーザーがダウンロードできるアプリケーション カタログに表示されるアプリ言語を変更します。

1.    Configuration Manager コンソールの**管理**ワークスペースで、**[クラウド サービス]** > **[更新とサービス]** > **[ビジネス向け Windows ストア]** の順に選択します。
2.    ビジネス向け Windows ストアのアカウントを選択し、**[プロパティ]** を選択します。
3.    **[言語]** タブを選択します。
4.    アプリケーション カタログに表示される言語を追加または削除します。 ユーザーが利用できる既定のアプリケーション カタログ言語を選択します。

>[!IMPORTANT]
>今回のリリースでは、同期される言語を変更した場合、サイト サーバーで SMS Executive サービスを再起動する必要があります。再起動後、言語設定が有効になります。


Azure Active Directory からのクライアントの秘密鍵を変更します。

1.    Configuration Manager コンソールの**管理**ワークスペースで、**[クラウド サービス]** > **[更新とサービス]** > **[ビジネス向け Windows ストア]** の順に選択します。
2.    ビジネス向け Windows ストアのアカウントを選択し、**[プロパティ]** を選択します。
3.    **[ビジネス アカウントのプロパティ用の Windows ストア]** ダイアログ ボックスで、**[クライアントの秘密鍵]** フィールドに新しいキーを入力し、**[確認]** を選択します。 確認されたら、**[適用]** を選択してダイアログ ボックスを閉じます。

## <a name="sync-apps-from-the-store-with-configuration-manager"></a>Configuration Manager でストアからのアプリを同期する

同期は 24 時間ごとに行われます。次の手順で、同期を即刻開始することもできます。

1. Configuration Manager コンソールの**管理**ワークスペースで、**[クラウド サービス]** > **[更新とサービス]** > **[ビジネス向け Windows ストア]** の順に選択します。
3.    **[ホーム]** タブの **[同期]** グループで、**[今すぐ同期]** を選択します。
4.    購入したアプリが **[アプリケーション管理]** ワークスペースの **[ストア アプリのライセンス情報]** ノードに表示されます。


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>ビジネス向け Windows ストアのアプリから Configuration Manager アプリケーションを作成して展開する

この手順では、ビジネス向け Windows ストアのアプリから無料のアプリを&1; つ以上入手しているか、有料アプリを&1; つ以上購入しているものと想定しています。

1.  Configuration Manager コンソールの **[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** を展開し、**[ストア アプリのライセンス情報]** を選択します。
2.  展開するアプリを選択し、**[ホーム]** タブの **[作成]** グループで、**[アプリケーションの作成]** を選択します。
ビジネス向け Windows ストアのアプリを含む Configuration Manager アプリケーションが作成されます。 他の Configuration Manager のアプリケーションと同様に、このアプリケーションを展開して監視できます。

> [!IMPORTANT]
> Intune に登録されたデバイスの場合、展開されたアプリは当初デバイスを登録したユーザーのみが利用できます。 それ以外のユーザーはアプリを使用できません。

## <a name="monitor-windows-store-for-business-apps"></a>ビジネス向け Windows ストアのアプリの監視

**[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** を展開し、**[ストア アプリのライセンス情報]** を選択します。

管理するストア アプリごとに、アプリの情報を表示できます。これには、アプリの名前、プラットフォーム、所有しているアプリのライセンスの数、利用可能なライセンスの数が含まれます。

