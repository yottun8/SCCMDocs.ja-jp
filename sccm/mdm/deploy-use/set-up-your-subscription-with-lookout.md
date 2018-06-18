---
title: Lookout サブスクリプションを設定する
titleSuffix: Configuration Manager
description: Lookout Mobile Threat Defense を構成する方法を説明します。
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 85c2ae1039058f39bd96c7d0752f798504b0dd4d
ms.sourcegitcommit: 9cff0702c2cc0f214173b47ec241f7e5a40f84e6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34746112"
---
# <a name="set-up-your-subscription-for-lookout-mobile-threat-defense"></a>Lookout Mobile Threat Defense のサブスクリプションを設定する

*適用対象: System Center Configuration Manager (Current Branch)*

Lookout Mobile Threat Defense のサブスクリプションを設定するには、次の手順が必要です。

| #        |手順  |
| ------------- |-------------|
| 1 | [Azure AD の情報を収集する](#collect-azure-ad-information) |
| 2 | [サブスクリプションを構成する](#configure-your-subscription) |
| 3 | [登録グループを構成する](#configure-enrollment-groups) |
| 4 | [状態の同期を構成する](#configure-state-sync) |
| 5 | [エラー レポートの電子メール受信者情報を構成する](#configure-error-report-email-recipient-information) |
| 6 | [登録設定を構成する](#configure-enrollment-settings) |
| 7 | [電子メールの通知を構成する](#configure-email-notifications) |
| 8 | [脅威の分類を構成する](#configure-threat-classification) |
| 9 | [登録の監視](#watching-enrollment) |


> [!IMPORTANT]  
> Azure AD テナントとまだ関連付けられていない既存の Lookout Mobile Endpoint Security テナントは、Azure AD および Intune との統合に使用できません。 新しい Lookout Mobile Endpoint Security テナントの作成については、Lookout のサポートに問い合わせてください。 新しいテナントを使って Azure AD ユーザーをオンボーディングします。




## <a name="collect-azure-ad-information"></a>Azure AD の情報を収集する
Lookout Mobility Endpoint Security テナントは、Lookout と Intune を統合するために Azure AD サブスクリプションに関連付けられます。 Lookout Mobile Threat Defense サービスのサブスクリプションを有効にするには、Lookout のサポート (enterprisesupport@lookout.com) に次の情報を伝えてください。

- **Azure AD テナント ID**
- Lookout コンソールへの*フル* アクセス用の **Azure AD グループ オブジェクト ID**
- Lookout コンソールへの*制限付き*アクセス用の **Azure AD グループ オブジェクト ID** (省略可能)

次の手順に従って、Lookout サポート チームに提供する必要のある情報を収集してください。

1. [Azure Portal](https://portal.azure.com) にサインインして、サブスクリプションを選択します。 

2. サブスクリプションの名前を選択すると、表示される URL にサブスクリプション ID が含まれています。 サブスクリプション ID の検索に問題がある場合は、[Microsoft サポート記事](https://support.office.com/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b)でサブスクリプション ID の検索に関するヒントを参照してください。

3. Azure AD のグループ ID を確認します。  
     > [!NOTE]   
     > **グループ オブジェクト ID** は、Azure Portal の [Azure AD] ブレードのグループの **[プロパティ]** ページにあります。  

   Lookout コンソールは 2 つのレベルのアクセスをサポートします。  

   - **フル アクセス:** Azure AD の管理者は、フル アクセス権を持つユーザーのグループを作成できるだけでなく、必要に応じて制限付きアクセス権を持つユーザーのグループも作成できます。 これらのグループのユーザーだけが、**Lookout コンソール**にサインインできます。
   - **制限付きアクセス:** このグループのユーザーは、Lookout コンソールの構成と登録に関連する複数のモジュールにアクセスできず、Lookout コンソールの**セキュリティ ポリシー** モジュールには読み取りアクセス権だけがあります。  

     > [!TIP]  
     > アクセス許可の詳細については、[Lookout サポートに関するこの記事](https://personal.support.lookout.com/hc/articles/114094105653)をご覧ください。


4. この情報を収集した後で、Lookout のサポート (メール: enterprisesupport@lookout.com) にお問い合わせください。 Lookout サポートは、主要連絡先を使用してサブスクリプションをオンボーディングし、収集された情報を使用して Lookout Enterprise アカウントを作成します。



## <a name="configure-your-subscription"></a>サブスクリプションを構成する

1. Lookout のサポート担当者が Lookout Enterprise アカウントを作成すると、[ログイン URL](https://aad.lookout.com/les?action=consent) へのリンクを含む Lookout からの電子メールが、会社の主要な連絡先に送られます。

2. Lookout コンソールに初めてログインする場合、グローバル管理者の Azure AD ロールを持つユーザー アカウントを使用し、Azure AD テナントを登録する必要があります。 以降のサインインにこのレベルの Azure AD 特権は必要ありません。 同意ページが表示されます。 **[同意する]** を選んで登録を完了します。 受け入れて同意すると、Lookout コンソールにリダイレクトされます。

   ![Lookout コンソールの初回ログイン ページのスクリーンショット](media/lookout-initial-login.png)

3. [Lookout コンソール](https://aad.lookout.com)で **[System]\(システム\)** モジュールから **[Connectors]\(コネクタ\)** タブを選択し、**[Intune]** を選択します。

   ![[Connectors] (コネクタ) タブが開き [Intune] オプションが強調表示されている Lookout コンソールのスクリーンショット](media/lookout-setup-intune-connector.png)

4. **[Connectors]\(コネクタ)** > **[Connection Settings]\(接続設定)** を選択し、**[Heartbeat Frequency]\(ハートビート頻度)** を分単位で指定します。

   ![ハートビートの頻度が構成された接続設定タブのスクリーンショット](media/lookout-connection-settings.png)



## <a name="configure-enrollment-groups"></a>登録グループを構成する
1. ベスト プラクティスとして、Lookout の統合をテストする少数のユーザーを含む Azure AD セキュリティ グループを [Azure Portal](https://portal.azure.com) に作成することをお勧めします。

    > [!NOTE]  
    > Azure AD の登録グループに属するユーザーが有する、Lookout のサポートを受け Intune に登録されているデバイスのうち、識別されてサポートされているものはすべて、Lookout MTD コンソールでのアクティブ化の対象になります。

2. [Lookout コンソール](https://aad.lookout.com)の **[System]\(システム\)** モジュールで、**[Connectors]\(コネクタ)** タブを選択し、**[Enrollment Management]\(登録管理\)** を選択し、Lookout に登録するデバイスのユーザー セットを定義します。 Azure AD セキュリティ グループの登録の **[表示名]** を追加します。

    ![Intune コネクタ登録ページのスクリーンショット](media/lookout-enrollment.png)

    >[!IMPORTANT]  
    > Azure Portal のセキュリティ グループの **[プロパティ]** に表示される **[表示名]** は大文字と小文字が区別されます。 次の画像のように、セキュリティ グループの **[Display Name]\(表示名\)** は大文字と小文字が混在していますが、タイトルはすべて小文字です。 Lookout コンソールでは、セキュリティ グループの **[Display Name]\(表示名\)** の大文字/小文字と一致させます。
    >![Azure Portal での Azure Active Directory サービスの [プロパティ] ページのスクリーンショット](media/aad-group-display-name.png)

    >[!NOTE]  
    >新しいデバイスをチェックする時間の増分には既定値 (5 分) を使うのがベスト プラクティスです。 現時点での制限事項、**Lookout はグループの表示名を検証できません:** Azure Portal の **[表示名]** フィールドが Azure AD セキュリティ グループと厳密に一致していることを確認してください。 **入れ子のグループを作成することはできません:** Lookout で使用する Azure AD セキュリティ グループには、ユーザーのみを含める必要があります。 他のグループを含めることはできません。

3.  グループを追加して、次にサポートされるデバイスでユーザーが Lookout for Work アプリを開いたときに、そのデバイスが Lookout でアクティブ化されます。

4.  結果に問題がなければ、他のユーザー グループまで登録を広げます。



## <a name="configure-state-sync"></a>状態の同期を構成する
**[State Sync]** (状態同期) オプションで、Intune に送信するデータの種類を指定します。 Lookout と Intune の統合が正常に動作するには、デバイスの状態と脅威の状態の両方が必要です。 これらの設定は既定では有効になっています。



## <a name="configure-error-report-email-recipient-information"></a>エラー レポートの電子メール受信者情報を構成する
**[Error Management]** (エラー管理) オプションで、エラー レポートを受け取る必要のあるメール アドレスを入力します。

![Intune コネクタ エラー管理ページのスクリーンショット](media/lookout-connector-error-notifications.png)



## <a name="configure-enrollment-settings"></a>登録の設定を構成する
**[System]** (システム) モジュールの **[Connectors]** (コネクタ) ページで、デバイスが切断と判断されるようになるまでの日数を指定します。 切断されたデバイスは非準拠と見なされ、SCCM 条件付きアクセス ポリシーに基づいて、社内アプリケーションへのアクセスをブロックされます。 1 ～ 90 日の範囲の値を指定できます。

![Lookout 登録設定](media/lookout-console-enrollment-settings.png)



## <a name="configure-email-notifications"></a>電子メールの通知を構成する
脅威のメール通知を受け取る場合は、通知を受け取るユーザー アカウントで [Lookout コンソール](https://aad.lookout.com)にサインインします。 **[System]\(システム\)** モジュールの **[Preferences]\(基本設定\)** タブで、通知が必要な脅威レベルを選択して、**[ON]\(オン\)** に設定します。 変更内容を保存します。

![ユーザー アカウントが表示された設定ページのスクリーンショット](media/lookout-email-notifications.png) メール通知を受け取る必要がなくなったら、通知を [オフ] に設定して変更を保存します。



## <a name="configure-threat-classification"></a>脅威の分類を構成する
Lookout Mobile Threat Defense によって、さまざまな種類のモバイルの脅威が分類されます。 [Lookout の脅威分類](http://personal.support.lookout.com/hc/articles/114094130693)には、既定のリスク レベルが関連付けられています。 これらの設定は会社の要件に合わせていつでも変更できます。

![脅威と分類を示すポリシー ページのスクリーンショット](media/lookout-threat-classification.png)

>[!IMPORTANT]  
> リスク レベルは、モバイルでの脅威に対する防御の重要な側面です。 Intune 統合では、実行時、これらのリスク レベルに基づいてデバイスのコンプライアンスが判断されます。 Intune 管理者は、デバイスにアクティブな脅威がある場合にデバイスを非準拠として特定するルールをポリシーに設定します。脅威には、**高**、**中**、**低**の最小レベルがあります。 Mobile Threat Defense での脅威分類ポリシーは、Intune でのデバイスのコンプライアンス判断に直接影響を与えます。



## <a name="watching-enrollment"></a>登録の監視
セットアップが完了すると、Mobile Threat Defense は Azure AD のポーリングを開始し、指定された登録グループに対応するデバイスを探します。 デバイス モジュールで登録されたデバイスに関する情報を検索できます。 デバイスの初期状態は保留中と表示されます。 デバイスで Lookout for Work アプリがインストールされ、開かれ、アクティブ化されると、デバイスの状態が変化します。 Lookout for Work アプリをデバイスにプッシュする方法の詳細については、「[Lookout for Work アプリを構成し、展開する](configure-and-deploy-lookout-for-work-apps.md)」を参照してください。


## <a name="next-steps"></a>次のステップ
[Intune 管理コンソールで Lookout MTP の接続を有効にする](enable-lookout-connection-in-intune.md)
