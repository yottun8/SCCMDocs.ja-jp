---
title: "ビジネス向け Windows ストアからのアプリの管理 | Microsoft Docs"
description: "System Center Configuration Manager を使用してビジネス向け Windows ストアからアプリを管理および展開します。"
ms.custom: na
ms.date: 3/29/2017
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
ms.sourcegitcommit: 6accec2d356861b273b25ba2b6338d9684a46ff6
ms.openlocfilehash: f2d9da1c584f78e27e84b7f55e7ffe4dd052a27c
ms.lasthandoff: 03/29/2017

---

# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>System Center Configuration Manager によるビジネス向け Windows ストアからのアプリの管理
[ビジネス向け Windows ストア](https://www.microsoft.com/business-store)は、組織向けの Windows アプリを検索して、個別に、または一括で購入できる場所です。 Configuration Manager にストアを接続することで、購入したアプリのリストを Configuration Manager と同期し、それらを Configuration Manager コンソールで表示し、他のアプリと同様に展開できます。


## <a name="online-and-offline-apps"></a>オンライン アプリとオフライン アプリ

ビジネス向け Windows ストアは、次の 2 種類のアプリをサポートしています。

- **オンライン** - この種類のライセンスでは、ユーザーとデバイスはストアに接続してアプリとそのライセンスを取得する必要があります。 Windows 10 デバイスは、Azure Active Directory ドメインに参加している必要があります。
- **オフライン** - ストアに接続したり、インターネットに接続したりせずに、組織はアプリとラインセンスをキャッシュして、そのオンプレミス ネットワークに展開できます。

ビジネス向け Windows ストアの詳細については、[こちら](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview?f=255&MSPPError=-2147217396)を参照してください。

Configuration Manager では、Configuration Manager クライアントを実行している Windows 10 デバイスと、Microsoft Intune に登録されている Windows 10 デバイスの両方でビジネス向け Windows ストアのアプリを管理できます (ハイブリッド構成と呼ばれます)。 Configuration Manager は、オンラインおよびオフライン アプリ向けに次の機能を提供します。

> [!IMPORTANT]
> この機能を使用するには、Windows 10 デバイスで 2015 年 11 月 (1511) リリース以降が実行されている必要があります。


|機能|オフライン アプリ|オンライン アプリ|
|------------|------------|------------|
|アプリ データと Configuration Manager の同期<br>(同期は 24 時間ごとに発生)|○|○|
|ストア アプリからの Configuration Manager アプリケーションの作成|○|○|
|ストアからの無料アプリのサポート|○|○|
|ストアからの有料アプリのサポート|×|○|
|ユーザーまたはデバイス コレクションへの必要な展開のサポート|○|○|
|ユーザーまたはデバイス コレクションへの利用可能な展開のサポート|○|○|
|ストアからの基幹業務アプリのサポート|○|○|

Configuration Manager クライアントを含む Windows 10 PC にオンライン ライセンス アプリを展開するには、Windows 10 Creators Update 以降を実行する必要があります。

## <a name="deploying-online-apps-using-the-windows-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Configuration Manager クライアントを実行している PC でのビジネス向け Windows ストアを使用したオンライン アプリの展開
完全な Configuration Manager クライアントを実行している PC にビジネス向け Windows ストア アプリを展開する前に、次のことを考慮してください。

- すべての機能を利用するには、PC で Windows 10 Creators Update 以降を実行する必要があります。
- PC は Azure Active Directory に社内参加済みで、管理ツールとしてビジネス向け Windows ストアを登録したのと同じ AAD テナントにある必要があります。
- PC は、組み込み管理者アカウントでログインしているときに、ビジネス向け Windows ストア アプリにアクセスできません。
- PC にはビジネス向け Windows ストアへのライブ インターネット接続が必要です。

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>以前のバージョンの Windows 10 を実行している PC に関する注記
(Configuration Manager クライアントを含む) Creators Update より前のバージョンの Windows 10 を実行している PC では、次の機能が適用されます。


- アプリケーションをインストールするユーザー、インストール期限に達するアプリケーションまたは必須の展開のインストール後の再評価により、インストールが実行された場合:
    - アプリケーションはビジネス向け Windows ストア アプリを起動することで "実行" されます。 
    - したがって、実際にインストールされる前に、エンド ユーザーはストアからインストールを完了する必要があります。
    - Configuration Manager コンソールではアプリケーション ステータスは失敗と報告され、"Windows Store アプリをクライアント PC で開いています。ユーザーがインストールを完了するのを待機しています" というエラーが表示されます。
- 次のアプリケーションの評価サイクル時:
    - アプリケーションがストアからエンド ユーザーによってインストールされた場合、そのアプリケーションで報告されるステータスは **[成功]** となります。 
    - エンド ユーザーがストアからのアプリのインストールを試行しなかった場合:
        - 必須の展開でストアの起動が試行され、アプリケーションのインストールが再度実行されます。
        - 利用可能な展開は再実行されません。

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>以前のバージョンの Windows 10 を実行している PC についてのその他の注記:

- ビジネス向け Windows ストアから基幹業務アプリを展開することはできません。
- ストアから有料アプリを展開する場合、エンド ユーザーはストアにログインし、アプリ自体を購入するよう求められます。
- コンシューマー バージョンの Windows Store へのアクセスを無効にしてグループ ポリシーを展開した場合、ビジネス向け Windows ストアが有効な場合でも、ビジネス向け Windows ストアから展開することはできません。


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

1. ビジネス向け Windows ストアから少なくとも 1 つのアプリを購入したことを確認します。 Configuration Manager コンソールの**管理**ワークスペースで、[**Cloud Services**] を展開して、[**ビジネス向け Windows ストア**] をクリックします。
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

