---
title: "CNG 証明書の概要"
titleSuffix: Configuration Manager
description: "Configuration Manager の CNG 証明書の概要"
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 
author: vhorne
ms.author: victorh
manager: angrobe
ms.openlocfilehash: f5f5138270d4f14b76b2c41e41ec034a0c12a932
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="cng-certificates-overview"></a>CNG 証明書の概要
<!-- 1356191 --> 

Configuration Manager の Cryptography: Next Generation (CNG) 証明書のサポートは制限されています。 Configuration Manager クライアントは、PKI クライアント認証証明書と CNG キー格納プロバイダー (KSP) の秘密キーを使用できます。 Configuration Manager クライアントは KSP をサポートしているので、PKI クライアント認証証明書用の TPM KSP など、ハードウェアベースの秘密キーをサポートしています。

## <a name="supported-scenarios"></a>サポートされるシナリオ
次のシナリオに [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) 証明書テンプレートを使用できます。

- HTTPS 管理ポイントを使用したクライアントの登録と通信。   
- HTTPS 配布ポイントを使用したソフトウェアの配布とアプリケーションの展開。   
- オペレーティング システムの展開。  
- クライアント メッセージ SDK (最新の更新プログラム) と ISV プロキシ。   
- クラウド管理ゲートウェイの構成。  

> [!NOTE]
> CNG は Crypto API (CAPI) と下位互換性があります。 クライアントで CNG のサポートが有効な場合でも、CAPI 証明書は引き続きサポートされます。

## <a name="unsupported-scenarios"></a>サポートされていないシナリオ

次のシナリオは、現在サポートされていません。

- アプリケーション カタログ Web サービス、アプリケーション カタログ Web サイト、登録ポイント、および登録プロキシ ポイント ロールは、インターネット インフォメーション サービス (IIS) の Web サイトに CNG 証明書がバインドされた HTTPS モードでインストールされている場合に機能しません。 ユーザーまたはユーザー グループ コレクションに展開されているアプリケーションやパッケージでも、ソフトウェア センターに使用可能と表示されません。

- 状態移行ポイントは、IIS の Web サイトに CNG 証明書がバインドされた HTTPS モードでインストールされている場合に機能しません。

- CNG 証明書を使用したクラウド配布ポイントの作成。

- NDES ポリシー モジュールがクライアント認証証明書に CNG 証明書を使用している場合、NDES ポリシー モジュールから証明書登録ポイント (CRP) への通信は失敗します。

- CNG 証明書が指定されている場合、タスク シーケンス メディアの作成で起動可能なメディアを作成できません。

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