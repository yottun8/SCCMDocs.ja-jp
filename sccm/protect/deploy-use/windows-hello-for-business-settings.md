---
title: "Windows Hello for Business の設定 | Microsoft Docs"
description: "System Center Configuration Manager に Windows Hello for Business を統合する方法について説明します。"
ms.custom: na
ms.date: 09/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: "17"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 43586e55f2c0c5cf117b94c61250f26ba4233f53
ms.sourcegitcommit: 4c3906cf9614420cb8527da9e48978eb0b8f0e7a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2017
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager における Windows Hello for Business の設定

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager を、Windows 10 デバイスの代替サインイン方法である Windows Hello for Business (旧称: Microsoft Passport for Windows) と統合することができます。 Hello for Business では、パスワード、スマート カード、または仮想スマート カードの代わりに Active Directory または Azure Active Directory アカウントを使用します。  

Hello for Business を使用すると、パスワードの代わりに **ユーザー ジェスチャ** を使用してログインできます。 ユーザー ジェスチャには、単純な暗証番号 (PIN)、生体認証、または指紋リーダーなどの外部のデバイスがあります。

[Windows Hello for Business の詳細](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)

 Configuration Manager と Windows Hello for Business を統合するには、次の 2 つの方法があります。  

-   Configuration Manager を使用して、ユーザーがサインインに使用できるジェスチャと使用できないジェスチャを制御できます。  

-   Windows Hello for Business のキー格納プロバイダー (KSP) に認証証明書を格納できます。 詳細については、「[Certificate profiles](introduction-to-certificate-profiles.md)」 (証明書プロファイル) をご覧ください。  

- ドメインに参加しており構成マネージャー クライアントを実行している Windows 10 デバイスに Windows Hello for Business ポリシーを展開できます。 この構成については、以下の「[ドメインに参加している Windows 10 デバイスで Windows Hello for Business を構成する](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices)」で説明されています。 Configuration Manager と Microsoft Intune を使用する (ハイブリッド) の場合は、Windows 10、および Windows 10 モバイル デバイスでこれらの設定を構成できます。 詳細については、[Windows Hello for Business 設定の構成 (ハイブリッド)](../../mdm/deploy-use/windows-hello-for-business-settings.md)に関する記事を参照してください。

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>ドメインに参加している Windows 10 デバイスで Windows Hello for Business を構成する
Windows Hello for Business プロファイルを作成して展開することで、ドメインに参加している Windows 10 デバイスで Windows Hello for Business の設定を制御できます。 これは、推奨される方法です。


証明書ベースの認証を使用している場合は、[証明書プロファイルの構成](#configure-a-certificate-profile)に関するセクションで説明されているように、証明書プロファイルも展開する必要があります。 キー ベースの認証を使用している場合は、証明書プロファイルを展開する必要はありません。

## <a name="configure-a-windows-hello-for-business-profile"></a>Windows Hello for Business プロファイルの構成  

Configuration Manager コンソールの **[会社のリソースへのアクセス]** で、**[Windows Hello for Business プロファイル]** を右クリックし、**[新規]** を選択してプロファイル ウィザードを開始します。 ウィザードによって要求された設定を指定し、最後のページで設定を確認して、**[閉じる]** をクリックします。 設定の例を次に示します。  

![Windows Hello for Business の設定](../media/Hello-for-Business-settings.png)

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configuration Manager で証明書プロファイルを構成して、Windows Hello for Business の登録証明書を登録する  
 Windows Hello for Business の証明書ベースのログオンを使用する場合は、次の構成を行います。  

-   Configuration Manager の証明書プロファイル。  

-   証明書プロファイルで、スマート カード ログオンの EKU を使用するテンプレートを選びます。  

-   ビジネス向け Windows Hello キー コンテナーに証明書プロファイルを保存する場合、証明書プロファイルで**スマート カード ログオン** EKU が使用されているときには、キー登録で証明書が正しく検証されるように次のアクセス許可を構成する必要があります。
最初に **Key Admins** グループを作成しておき、すべての Configuration Manager 管理ポイント コンピューターをこのグループに追加する必要があります。

一部の構成ではアクセス許可を構成する必要がなかったり、さらに構成が必要だったりする場合があります。 詳細については、次の表をご覧ください。

|||||
|-|-|-|-|
|Windows クライアント バージョン|Configuration Manager 1602 または 1606|Configuration Manager 1610|Configuration Manager 1702 以降|
|Windows 10 Anniversary Update|必要な修正プログラムはありません<br><br>必要なアクセス許可はありません<br><br>Windows スキーマの更新は必要ありません|必要な修正プログラムはありません (「**警告**」をご覧ください)<br><br>必要なアクセス許可はありません<br><br>Windows スキーマの更新は必要ありません|アクセス許可を構成します<br><br>Active Directory に Windows Server 2016 のスキーマを適用します|
|Windows 10 Creators Update 以降|サポートされていません|[この修正プログラム](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)をインストールします<br><br>アクセス許可を構成します<br><br>Active Directory に Windows Server 2016 のスキーマを適用します|アクセス許可を構成します<br><br>Active Directory に Windows Server 2016 のスキーマを適用します|

> [!WARNING]
> [修正プログラム](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)は Configuration Manager 1610 および Windows 10 Anniversary Update では不要ですが、インストールは可能です。  修正プログラムをインストールした場合は、アクセス許可を構成して Active Directory に Windows Server 2016 のスキーマを適用する必要があります。

## <a name="to-configure-permissions"></a>アクセス許可を構成するには

1.  ドメイン管理者または同等の資格情報でドメイン コントローラーまたは管理ワークステーションにログインします。
2.  **[Active Directory Users and Computers]** を開きます。
3.  ナビゲーション ウィンドウで、ドメイン名を右クリックし、**[プロパティ]** をクリックします。
4.  **[*<domain name>* のプロパティ]** ダイアログ ボックスの **[セキュリティ]** タブで、**[詳細設定]** をクリックします。 **[セキュリティ]** タブが表示されない場合、**[Active Directory Users and Computers]** の **[表示]** メニューの **[高度な機能]** をオンにします。
5.  [ **追加**] をクリックします。
6.  **[*<domain name>* のアクセス許可エントリ]** ダイアログ ボックスで **[プリンシパルの選択]** をクリックします。
7.  **[ユーザー、コンピューター、サービス アカウント、またはグループの選択]** ダイアログ ボックスの **[選択するオブジェクト名を入力します]** テキスト ボックスに「**Key Admins**」と入力します。  **[OK]**をクリックします。
8.  **[適用先]** リストから **[Descendant User objects (子孫ユーザー オブジェクト)]** を選択します。
9.  ページの一番下までスクロールし、**[すべてクリア]** をクリックします。
10. **[プロパティ]** セクションで **[Read msDS-KeyCredentialLink (msDS-KeyCredentialLink を読む)]** を選択します。
11. **[OK]** を 3 回クリックし、タスクを完了します。


## <a name="next-steps"></a>次のステップ

詳細については、「[Certificate profiles](introduction-to-certificate-profiles.md)」 (証明書プロファイル) をご覧ください。  




