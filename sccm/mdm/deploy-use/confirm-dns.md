---
title: ドメイン名の要件を確認する
titleSuffix: Configuration Manager
description: System Center Configuration Manager を使用してドメイン名の要件を確認します。
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e80a001153012763f56686df66ab7c6fcbf9b88
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127390"
---
# <a name="confirm-domain-name-requirements-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用したドメイン名の要件の確認

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

必要に応じて、Configuration Manager 外部の依存関係を満たすため、次の手順を実行します。

1. デバイスを登録するには、各ユーザーに Intune ライセンスが割り当てられている必要があります。 Intune ライセンスをユーザーに割り当てるには、パブリックに解決できるユーザー プリンシパル名 (UPN) (たとえば、johndoe@contoso.com) または Azure Active Directory で構成された代替ログイン ID を各ユーザーが持っている必要があります。 代替ログイン ID を構成すると、たとえば UPN が NetBIOS 形式 (CONTOSO\johndoe など) の場合でも、ユーザーが電子メール アドレスでサインインできるようになります。

   - 会社がパブリックに解決できる UPN (つまり johndoe@contoso.com) を使用している場合、それ以上の構成は必要ありません。
   - 会社が解決できない UPN (つまり CONTOSO\johndoe) を使用している場合、[Azure Active Directory で代替 ID を構成する](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync)必要があります。

2. Active Directory Federation Services (AD FS) を展開および構成する (オプション)

    シングル サインオンをセットアップすると、ユーザーは会社の資格情報を使用してサインインし、Intune のサービスにアクセスできます。

    詳細については、以下のトピックを参照してください。
   -   [シングル サインオンを準備する](http://go.microsoft.com/fwlink/?LinkID=271124)
   -   [チェックリスト: AD FS 2.0 を使用してシングル サインオンを実装および管理する](http://go.microsoft.com/fwlink/?LinkID=271125)

3. ディレクトリ同期の展開と構成

    ディレクトリ同期を使用すると、同期したユーザー アカウントで Intune を設定できます。 同期したユーザー アカウントとセキュリティ グループは、Intune に追加されます。 Configuration Manager MDM と Microsoft Intune をセットアップするときに、デバイスを登録できない一般的な原因は、ディレクトリ同期が有効になっていないことです。

    詳しくは、Active Directory ドキュメント ライブラリの「 [ディレクトリ統合](http://go.microsoft.com/fwlink/?LinkID=271120) 」をご覧ください。

4. このオプションでは、推奨されません。Active Directory フェデレーション サービスを使用していない場合は、ユーザーの Microsoft Online パスワードをリセットします。

    AD FS を使用していない場合、各ユーザーの Microsoft Online パスワードを設定する必要があります。

> [!div class="button"]
> [< 前のステップ](create-mdm-collection.md)  [次のステップ >](configure-intune-subscription.md)
