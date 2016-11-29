---
title: "Active Directory Domain Services のクライアント インストール プロパティ |System Center Configuration Manager"
description: "System Center Configuration Manager で Active Directory Domain Services に発行されたクライアント インストール プロパティを使用します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
caps.latest.revision: 6
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d5cdaa80abca6d003d3e07c2068c12de64ccab67

---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services-in-system-center-configuration-manager"></a>System Center Configuration Manager で Active Directory Domain Services に発行されたクライアント インストールのプロパティについて

*適用対象: System Center Configuration Manager (Current Branch)*

Active Directory スキーマを System Center Configuration Manager 用に拡張して、サイトが Active Directory Domain Services に公開されるとき、多くのクライアント インストール プロパティが Active Directory Domain Services に公開されます。 コンピューターでこれらのクライアント インストール プロパティを見つけることができる場合は、Configuration Manager クライアントの展開時にそれらを使用できます。  

 クライアント インストール プロパティの発行に Active Directory ドメイン サービスを使用すると、次の利点があります。  

-   ソフトウェアの更新ポイント ベースのクライアント インストールとグループ ポリシーのクライアント インストールで、セットアップ パラメーターを各コンピューターで提供する必要がありません。  

-   この情報は自動的に生成されるため、インストール プロパティを手動で入力するために発生する人的ミスのリスクが排除されます。  

> [!NOTE]  
>  Configuration Manager 用に Active Directory スキーマを拡張する方法、およびサイトの公開方法の詳細については、「[System Center Configuration Manager のスキーマ拡張](../../plan-design/network/schema-extensions.md)」を参照してください。  

 クライアント インストール (CCMSetup) は、次の方法のいずれかを使用して指定されたプロパティが他にない場合にのみ、Active Directory ドメイン サービスに発行されたクライアント インストールプロパティを使用します。  

-   手動インストール  

-   グループ ポリシーを使用したクライアント インストール プロパティの準備  

> [!NOTE]  
>  クライアント インストール プロパティは、クライアントがインストールされ、Configuration Manager サイトに割り当てられると、クライアントのインストールに使用され、割り当てられたサイトの新しい設定で上書きする場合があります。  

 どの Configuration Manager クライアント インストール方法で Active Directory Domain Services を使用してクライアント インストール プロパティを取得するかを判断するには、以下のセクションの詳細を使用します。  

## <a name="client-push-installation"></a>クライアント プッシュ インストール  
 クライアント プッシュ インストールでは、インストール　プロパティの取得に Active Directory ドメイン サービスは使用されません。  

 その代わりに、[クライアント プッシュ インストール のプロパティ] **** ダイアログ ボックスの [クライアント] **** タブで client.msi インストール プロパティを指定することができます。 これらのオプションとクライアント関連のサイト設定は、クライアントがクライアント インストールの際に読み込むファイルに保存されています。  

> [!NOTE]  
>  クライアント プッシュ インストール、フォールバック ステータス ポイント、または信頼されたルート キーでは、[クライアント] **** タブで CCMSetup プロパティを設定する必要はありません。 これらの設定はクライアント プッシュ インストールを使用してインストールをしたときに、自動で行われます。  

 [クライアント] **** タブで指定する client.msi プロパティは、サイトが Active Directory ドメイン サービスに公開されると、Active Directory ドメイン サービスに発行されます。 これらの設定は CCMSetup がインストール プロパティなしで実行されるクライアント インストールで読み込まれます。  

## <a name="software-update-point-based-installation"></a>ソフトウェアの更新ポイント経由のインストール  
 ソフトウェアの更新ポイント ベースのインストール方法では、CCMSetup コマンド ラインへのインストール プロパティの追加はサポートされていません。  

 グループ ポリシーを使用してクライアント コンピューターでコマンド ライン プロパティが提供されなかった場合は、CCMSetup は Active Directory ドメイン サービス でインストール プロパティを検索します。  

## <a name="group-policy-installation"></a>グループ ポリシーによるインストール  
 グループ ポリシーのインストール方法では、CCMSetup コマンド ラインへのインストール プロパティの追加はサポートされていません。  

 クライアント コンピューターでコマンド ライン プロパティが提供されなかった場合は、CCMSetup は Active Directory ドメイン サービス でインストール プロパティを検索します。  

## <a name="manual-installation"></a>手動インストール  
 CCMSetup は、次の状況で Active Directory ドメイン サービスのインストール プロパティを検索します。  

-   CCMSetup.exe コマンドの後にコマンド ライン プロパティが指定されていない。  

-   コンピューターにグループ ポリシーを使用してインストール プロパティが提供されていない。  

## <a name="logon-script-installation"></a>ログオン スクリプトによるインストール  
 CCMSetup は、次の状況で Active Directory ドメイン サービスのインストール プロパティを検索します。  

-   CCMSetup.exe コマンドの後にコマンド ライン プロパティが指定されていない。  

-   コンピューターにグループ ポリシーを使用してインストール プロパティが提供されていない。  

## <a name="software-distribution-installation"></a>ソフトウェアの配布によるインストール  
 CCMSetup は、次の状況で Active Directory ドメイン サービスのインストール プロパティを検索します。  

-   CCMSetup.exe コマンドの後にコマンド ライン プロパティが指定されていない。  

-   コンピューターにグループ ポリシーを使用してインストール プロパティが提供されていない。  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services-for-published-information"></a>発行されている情報を取得するために Active Directory Domain Services にアクセスできないクライアントのインストール  
 これらのクライアントには次のものがあります。  

-   ワークグループ コンピューター  

-   Active Directory Domain Services に公開されていない Configuration Manager サイトに割り当てられたクライアント  

-   インターネットにあるときにインストールされたクライアント  

 これらのクライアント コンピューターは、Active Directory ドメイン サービスからインストール プロパティを読み込むことができないため、発行されたインストール プロパティにアクセスすることができません。  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Active Directory Domain Services に発行されたクライアント インストール プロパティ  
 次に一覧表示する各項目の詳細については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」を参照してください。  

-   Configuration Manager サイト コード。  

-   サイト サーバー署名証明書。  

-   信頼されたルート キー。  

-   HTTP おようび HTTPS 用のクライアント通信ポート。  

-   フォールバック ステータス ポイント。 サイトに複数のフォールバック ステータス ポイントがある場合は、最初にインストールしたフォールバック ステータス ポイントのみが Active Directory ドメイン サービスに発行されます。  

-   クライアントが HTTPS のみを使用して通信する必要があることを示す設定。  

-   PKI 証明書に関する設定:  

    -   クライアントの PKI 証明書を使用するかどうか。  

    -   証明書の選択条件 (Configuration Manager に使用できる有効な PKI 証明書がクライアントに複数あるために必要な場合)。  

    -   どの証明書を使用するかを判断する設定（証明書選択プロセスの後に有効な証明書がクライアントに複数ある場合）。  

    -   信頼されたルート（CA）証明書の一覧を含む証明書発行者の一覧  

-   ｃlient.msi インストール プロパティは、[クライアント プッシュ インストールのプロパティ] **** ダイアログ ボックスの [クライアント] **** タブで指定します。



<!--HONumber=Nov16_HO1-->


