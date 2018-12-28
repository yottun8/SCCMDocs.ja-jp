---
title: Intune サブスクリプションの構成
titleSuffix: Configuration Manager
description: System Center Configuration Manager を使用して Intune サブスクリプションを構成します。
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 99de8fe7-560e-401a-8ab2-6d87d091be17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a009159a4bd0588f80f140f588b17911101cc72c
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418562"
---
# <a name="configure-your-intune-subscription-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用した Intune サブスクリプションの構成

*適用対象します。System Center Configuration Manager (Current Branch)*

Intune サブスクリプションを使用すると、インターネット上でデバイスを管理できます。 たとえば、デバイスを登録できるユーザー コレクションを指定したり、ユーザーに表示される情報を定義したりすることができます。 Intune サブスクリプションを作成するときに、Intune の会社のポータルに会社のロゴや独自のカラー スキームを含めて、会社のブランドを追加できます。

Intune サブスクリプションは、次のことを実行します。

-   Intune サービスに接続するためにサービス接続ポイントによって必要とされる証明書を取得します
-   ユーザーがモバイル デバイスを登録できるようにするユーザー コレクションを定義します
-   サポートするモバイル プラットフォームを定義して構成します

> [!IMPORTANT]
>  Configuration Manager で Microsoft Intune のサブスクリプションを作成すると、サイトのサービス接続ポイントが「オンライン モード」になります。 「[System Center Configuration Manager のサービス接続ポイントについて](../../core/servers/deploy/configure/about-the-service-connection-point.md)」を参照してください。

## <a name="to-create-the-microsoft-intune-subscription"></a>Microsoft Intune サブスクリプションを作成するには

1.  まだであれば、[Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216) で Microsoft Intune アカウントにサインアップします。  Intune アカウントを作成した後は、ユーザーを Intune アカウントに追加したり、追加の設定を構成したりする必要はありません。

2.  Configuration Manager コンソールで、**[管理]** をクリックします。

3.  **[管理]** ワークスペースで、 **[クラウド サービス]** を展開して **[Microsoft Intune サブスクリプション]** をクリックします。 **[ホーム]** タブで、 **[Microsoft Intune サブスクリプションの追加]** をクリックします。

![Intune サブスクリプションを作成する](../media/mdm-set-intune.png)

4. [Microsoft Intune サブスクリプションの作成] ウィザードの **[概要]** ページで、内容を確認して、**[次へ]** をクリックします。

5. **[サブスクリプション]** ページで、**[サインイン]** をクリックし、職場または学校のアカウントを使用してサインインします。 **[モバイル デバイス管理機関の設定]** ダイアログで、チェック ボックスをオンにして、Configuration Manager コンソールから Configuration Manager を使用してのみモバイル デバイスを管理するようにします。 サブスクリプションを続行するには、このオプションを選択する必要があります。

   > [!IMPORTANT]
   >  管理機関として Configuration Manager を選択すると、Configuration Manager バージョン 1610 以降の Microsoft Intune および Microsoft Intune バージョン 1705 でのみ、Microsoft サポートに問い合わせることや、既存のマネージド デバイスの登録解除と再登録を行うことなく、管理機関を変更できます。 詳細については、「[Change your MDM authority](/sccm/mdm/deploy-use/change-mdm-authority)」(MDM 機関を変更する) を参照してください。

6. プライバシー リンクを確認するには、リンクをクリックして、**[次へ]** をクリックします。

7. **[全般]** ページで、以下のオプションを指定して **[次へ]** をクリックします。

   - **コレクション**:自分のモバイル デバイスを登録するユーザーを含むユーザー コレクションを指定します。

     > [!NOTE]
     >  コレクションからユーザーを削除すると、そのユーザーのデバイスは、ユーザー レコードがユーザー データベースから削除されるまで最長 24 時間管理されます。

   - **会社名**:会社名を指定します。

   - **会社のプライバシー ドキュメントの URL**:会社のプライバシー情報をインターネットからアクセス可能なリンクを発行する場合は、たとえばユーザーが会社のポータルからアクセスできるリンクを提供 http://www.contoso.com/CP_privacy.htmlします。 プライバシー情報を使用すると、ユーザーが企業と共有する情報を明確にすることができます。

   - **会社のポータルの配色**:必要に応じて、会社ポータルの青の既定の色を変更します。

   - **Configuration Manager サイト コード**:モバイル デバイスを管理するプライマリ サイトのサイト コードを指定します。

   > [!NOTE]
   >  サイト コードの変更は、新しいデバイスの登録だけに影響します。既に登録済みのデバイスのサイト コードは変わりません。

8. **[会社の連絡先情報]** ページで、ポータル サイト アプリの **[IT に連絡]** でユーザーに表示する会社の連絡先情報を指定します。 会社の連絡先情報を指定し、**[次へ]** をクリックします。

9. **[会社のロゴ]** ページでは、ポータル サイトにロゴを表示するかどうかを選択し、**[次へ]** をクリックします。

10. ウィザードを完了します。

> [!div class="button"]
> [< 前のステップ](confirm-dns.md)  [次のステップ >](terms-and-conditions.md)
