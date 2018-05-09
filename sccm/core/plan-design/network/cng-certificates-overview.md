---
title: CNG 証明書の概要
titleSuffix: Configuration Manager
description: 'Configuration Manager クライアントとサーバーの Cryptography: Next Generation (CNG) 証明書のサポートについて説明します。'
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4a4f37330f94111bcc41b81d9127039056f69e2b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="cng-certificates-overview"></a>CNG 証明書の概要
<!-- 1356191 --> 

Configuration Manager の Cryptography: Next Generation (CNG) 証明書のサポートは制限されています。 Configuration Manager クライアントは、PKI クライアント認証証明書と CNG キー格納プロバイダー (KSP) の秘密キーを使用できます。 Configuration Manager クライアントは KSP をサポートしているので、PKI クライアント認証証明書用の TPM KSP など、ハードウェアベースの秘密キーをサポートしています。

## <a name="supported-scenarios"></a>サポートされるシナリオ
次のシナリオに [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) 証明書テンプレートを使用できます。

- HTTPS 管理ポイントを使用したクライアントの登録と通信   
- HTTPS 配布ポイントを使用したソフトウェアの配布とアプリケーションの展開   
- オペレーティング システムの展開  
- クライアント メッセージ SDK (最新の更新プログラム) と ISV プロキシ   
- クラウド管理ゲートウェイの構成  

バージョン 1802 以降では、以下の HTTPS が有効なサーバーの役割には CNG 証明書を使ってください。<!-- 1357314 -->   
- 管理ポイント
- 配布ポイント
- ソフトウェアの更新ポイント
- 状態移行ポイント     

> [!NOTE]
> CNG は Crypto API (CAPI) と下位互換性があります。 クライアントで CNG のサポートが有効な場合でも、CAPI 証明書は引き続きサポートされます。

## <a name="unsupported-scenarios"></a>サポートされていないシナリオ

次のシナリオは、現在サポートされていません。

- 次のサーバーの役割は、インターネット インフォメーション サービス (IIS) の Web サイトに CNG 証明書がバインドされた HTTPS モードでインストールされている場合には機能しません。 
    - アプリケーション カタログ Web サービス
    - アプリケーション カタログ Web サイト
    - 登録ポイント  
    - 登録プロキシ ポイント  

- ユーザーまたはユーザー グループ コレクションに展開されているアプリケーションやパッケージでも、ソフトウェア センターに使用可能と表示されません。

- CNG 証明書を使用したクラウド配布ポイントの作成。

- NDES ポリシー モジュールがクライアント認証に CNG 証明書を使用している場合、証明書登録ポイントへの通信は失敗します。

- タスク シーケンス メディアの作成時に CNG 証明書を指定すると、起動可能なメディアを作成するウィザードが失敗します。

## <a name="to-use-cng-certificates"></a>CNG 証明書を使用するには

CNG 証明書を使用するには、証明機関 (CA) が対象コンピューターに CNG 証明書テンプレートを提供する必要があります。 テンプレートの詳細は、シナリオによって異なります。ただし、次のプロパティは必須です。

- **[互換性]** タブ

    - **[証明機関]** が Windows Server 2008 以降である必要があります。 (Windows Server 2012 推奨)

    - **[証明書の受信者]** が Windows Vista/Server 2008 以降である必要があります。 (Windows 8/Windows Server 2012 推奨)

- **[暗号化]** タブ

    - **[プロバイダーのカテゴリ]** が **[キー格納プロバイダー]** である必要があります。 (必須)

> [!NOTE]
> 環境または組織によって要件は異なる場合があります。 組織の PKI 専門家に相談してください。 CNG を利用するには、証明書テンプレートにキー格納プロバイダーを使用する必要がある、という点を考慮することが重要です。

最適な結果を得るには、Active Directory の情報から [サブジェクト名] を構築することをおすすめします。 **[サブジェクト名の形式]** の [DNS 名] を使用し、代替サブジェクト名にその DNS 名を含めます。 それ以外の場合は、デバイスを証明書プロファイルに登録するときに、この情報を提供する必要があります。