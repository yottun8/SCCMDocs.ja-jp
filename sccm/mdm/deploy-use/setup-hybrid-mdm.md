---
title: "ハイブリッド MDM のセットアップ | Microsoft Docs"
description: "Configuration Manager と Intune を使用してハイブリッド デバイス登録をセットアップします。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0a6cb36aad455b38db628f26b97e1b4c00adc741
ms.openlocfilehash: 12ef5c1faf5fe5780ddb7c12cfe6d533e9785f6d

---

# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用してハイブリッド モバイル デバイス管理 (MDM) をセットアップする

*適用対象: System Center Configuration Manager (Current Branch)*


Configuration Manager で iOS デバイス、Windows デバイス、および Android デバイスを管理するには、まず Intune に登録する必要があります。 Intune を使用して Configuration Manager へのハイブリッド デバイス登録をセットアップするには、以下の手順を実行します。 以下の手順を完了すると、ユーザーが "Bring Your Own Device" (BYOD) 登録を利用できるようになります。 この手順は、[会社所有のデバイスを登録する](enroll-company-owned-devices.md)ための前提条件でもあります。

 |手順|説明|  
 |-----------|-------------|  
 |**手順 1:** [MDM コレクションを作成する](#step-1-create-an-mdm-collection)|デバイスの登録を許可するユーザーを使用して Configuration Manager ユーザー コレクションを作成します|  
 |**手順 2:** [ドメイン名の要件](#step-2-domain-name-requirements)|組織のドメイン ネーム サービス (DNS) と Active Directory ユーザー管理が MDM の要件を満たしていることを確認します|
 |**手順 3:** [Intune サブスクリプションを構成する](#step-3-configure-intune-subscription)|Intune サービスを使用すると、インターネット上でデバイスを管理できます。|  
 |**手順 4:** [使用条件を追加する](#step-4-add-terms-and-conditions)| 使用条件を作成します。ユーザーは、ポータル サイト アプリを使用する前にこの使用条件に同意する必要があります。|
 |**手順 5:** [サービス接続ポイントを作成する](#step-5-create-service-connection-point)|サービス接続ポイントは、設定とソフトウェアの展開情報を Configuration Manager に送信し、モバイル デバイスからステータス メッセージとインベントリ メッセージを取得します。 |  
 |**手順 6:** [プラットフォームの登録を有効にする](#step-6-enable-platform-enrollment)|[iOS](#ios-and-mac-enrollment-setup) デバイスと [Windows](#windows-enrollment-setup) デバイスの MDM 登録には、サービスとデバイス間の通信のために追加の手順が必要です。 Android の場合、追加の構成は必要ありません。|  
 |**手順 7:** [追加の管理をセットアップする](#step-7-set-up-additional-management)|(省略可能) 登録デバイスの構成アイテムと条件付きアクセスを設定します|
 |**手順 8:** [MDM の構成を確認する](#step-8-verify-mdm-configuration)|ログ ファイルを見て、サービス接続ポイントが正常に作成されたことと、ユーザー アカウントが同期していることを確認します。|
 |**手順 9:** [デバイスを登録する](#step-9-enroll-devices)|組織のニーズに合わせてデバイスを登録する方法をユーザーに伝えるか、会社所有のデバイスを登録し始めます|

Configuration Manager を使用せずに Intune を使用する場合
> [!div class="button"]
[Intune ドキュメントを見る >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)

## <a name="step-1-create-an-mdm-collection"></a>手順 1: MDM コレクションを作成する
デバイスを管理対象に登録できるユーザーを指定するには、Configuration Manager ユーザー コレクションが必要です。 Intune のライセンスはユーザーごとに割り当てられるため、使用できるのはユーザー コレクション (デバイス コレクションではなく) のみです。

> [!NOTE]
> Intune にデバイスを登録する場合、Office 365 ポータルまたは Azure Active Directory ポータルでユーザーにライセンスを割り当てる必要はありません。 Intune サブスクリプションに関連付けられたコレクションにユーザーを含める ([後の手順](#step-3-configure-intune-subscription)を参照) だけで済みます。

テスト目的で**ダイレクト規則**をセットアップし、デバイスを登録できる特定のユーザーを追加することができます。 Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[ユーザー コレクション]** を選択し、**[ホーム]** タブ > **[作成]** グループをクリックし、**[ユーザー コレクションの作成]** をクリックします。 配布を広範にするには、**クエリ規則**を使用してユーザーを定義するようにします。 コレクションの詳細については、「[System Center Configuration Manager でコレクションを作成する方法](https://technet.microsoft.com/library/mt629371.aspx)」を参照してください。

![MDM のユーザー コレクションを作成する](../media/mdm-create-user-collection.png)

## <a name="step-2-domain-name-requirements"></a>手順 2: ドメイン名の要件

必要に応じて、Configuration Manager 外部の依存関係を満たすため、次の手順を実行します。

1. デバイスを登録するには、各ユーザーに Intune ライセンスが割り当てられている必要があります。 Intune ライセンスをユーザーに割り当てるには、パブリックに解決できるユーザー プリンシパル名 (UPN) (たとえば、johndoe@contoso.com) または Azure Active Directory で構成された代替ログイン ID を各ユーザーが持っている必要があります。 代替ログイン ID を構成すると、たとえば UPN が NetBIOS 形式 (CONTOSO\johndoe など) の場合でも、ユーザーが電子メール アドレスでサインインできるようになります。

  - 会社がパブリックに解決できる UPN (つまり johndoe@contoso.com), を使用している場合、それ以上の構成は必要ありません。
  - 会社が解決できない UPN (つまり CONTOSO\johndoe) を使用している場合、[Azure Active Directory で代替 ID を構成する](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync)必要があります。

2.  Active Directory Federation Services (AD FS) を展開および構成する (オプション)

     シングル サインオンをセットアップすると、ユーザーは会社の資格情報を使用してサインインし、Intune のサービスにアクセスできます。

     詳細については、以下のトピックを参照してください。
    -   [シングル サインオンを準備する](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [チェックリスト: AD FS 2.0 を使用してシングル サインオンを実装および管理する](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  ディレクトリ同期の展開と構成

     ディレクトリ同期を使用すると、同期したユーザー アカウントで Intune を設定できます。 同期したユーザー アカウントとセキュリティ グループは、Intune に追加されます。 Configuration Manager MDM と Microsoft Intune をセットアップするときに、デバイスを登録できない一般的な原因は、ディレクトリ同期が有効になっていないことです。

     詳しくは、Active Directory ドキュメント ライブラリの「 [ディレクトリ統合](http://go.microsoft.com/fwlink/?LinkID=271120) 」をご覧ください。

4.  省略可能で推奨されない手順: Active Directory フェデレーション サービスを使用していない場合は、ユーザーの Microsoft Online パスワードをリセットします。

     AD FS を使用していない場合、各ユーザーの Microsoft Online パスワードを設定する必要があります。

## <a name="step-3-configure-intune-subscription"></a>手順 3: Intune サブスクリプションを構成する
 Intune サブスクリプションを使用すると、インターネット上でデバイスを管理できます。 たとえば、デバイスを登録できるユーザー コレクションを指定したり、ユーザーに表示される情報を定義したりすることができます。 Intune サブスクリプションは、次のことを実行します。

-   Intune サービスに接続するためにサービス接続ポイントによって必要とされる証明書を取得します
-   ユーザーがモバイル デバイスを登録できるようにするユーザー コレクションを定義します
-   サポートするモバイル プラットフォームを定義して構成します

> [!IMPORTANT]
>  Configuration Manager で Microsoft Intune のサブスクリプションを作成すると、サイトのサービス接続ポイントが「オンライン モード」になります。 「[System Center Configuration Manager のサービス接続ポイントについて](../../core/servers/deploy/configure/about-the-service-connection-point.md)」を参照してください。

### <a name="to-create-the-microsoft-intune-subscription"></a>Microsoft Intune サブスクリプションを作成するには

1.  まだであれば、[Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216) で Microsoft Intune アカウントにサインアップします。  Intune アカウントを作成した後は、ユーザーを Intune アカウントに追加したり、追加の設定を構成したりする必要はありません。

2.  Configuration Manager コンソールで、[ **管理**] をクリックします。

3.  **[管理]** ワークスペースで、 **[クラウド サービス]**を展開して **[Microsoft Intune サブスクリプション]**をクリックします。 **[ホーム]** タブで、 **[Microsoft Intune サブスクリプションの追加]**をクリックします。

![Intune サブスクリプションを作成する](../media/mdm-set-intune.png)

4.  [Microsoft Intune サブスクリプションの作成] ウィザードの [ **概要** ] ページで、内容を確認して、[ **次へ**] をクリックします。

5.  [ **サブスクリプション** ] ページで、[ **サインイン** ] をクリックし、職場または学校のアカウントを使用してサインインします。 **[モバイル デバイス管理機関の設定]** ダイアログで、チェック ボックスをオンにして、Configuration Manager コンソールから Configuration Manager を使用してのみモバイル デバイスを管理するようにします。 サブスクリプションを続行するには、このオプションを選択する必要があります。

    > [!IMPORTANT]
    >  管理機関として Configuration Manager を選んだら、後から管理機関を Microsoft Intune に変更することはできません。

6.  プライバシー リンクを確認するには、リンクをクリックして、[次へ ****] をクリックします。

7.  [ **全般** ] ページで、以下のオプションを指定して [ **次へ**] をクリックします。

  -   **コレクション**:モバイル デバイスを登録するユーザーが含まれるユーザー コレクションを指定します。

      > [!NOTE]
      >  コレクションからユーザーを削除すると、そのユーザーのデバイスは、ユーザー レコードがユーザー データベースから削除されるまで最長 24 時間管理されます。

  -   **会社名**: 会社の名前を指定します。

  -   **会社のプライバシー ドキュメントの URL**: 会社のプライバシー保護情報を、インターネットからアクセス可能な場所で公開する場合は、ユーザーが会社ポータルからアクセスできるように、そのリンクを指定します (たとえば http://www.contoso.com/CP_privacy.html)。 プライバシー情報を使用すると、ユーザーが企業と共有する情報を明確にすることができます。

  -   **会社ポータルの配色**:オプションで、既定の色 (青) を会社ポータル向けに変更できます。

  -   **Configuration Manager サイト コード**:モバイル デバイスを管理するための、プライマリ サイトのサイト コードを指定します。

    > [!NOTE]
    >  サイト コードの変更は、新しいデバイスの登録だけに影響します。既に登録済みのデバイスのサイト コードは変わりません。

8.  **[会社の連絡先情報]** ページで、ポータル サイト アプリの **[IT に連絡]** でユーザーに表示する会社の連絡先情報を指定します。 会社の連絡先情報を指定し、**[次へ]** をクリックします。

9. **[会社のロゴ]** ページでは、ポータル サイトにロゴを表示するかどうかを選択し、**[次へ]**をクリックします。

10. ウィザードを完了します。

## <a name="step-4-add-terms-and-conditions"></a>手順 4: 使用条件を追加する
 モバイル デバイス用に Intune 管理を構成したら、 **[使用条件]**を作成できます。 使用条件は、デバイスを登録するとどうなるかをユーザーに説明するために使用します。 ユーザーはデバイスを登録する前に、使用条件に同意する必要があります。 Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[概要]** > **[コンプライアンス設定]** > **[使用条件]** の順に移動して、**[使用条件の作成]** をクリックします。 「[System Center Configuration Manager での使用条件](terms-and-conditions.md)」を参照してください。

##  <a name="step-5-create-service-connection-point"></a>手順 5: サービス接続ポイントを作成する
サブスクリプションを作成したら、サービス接続ポイントのサイト システムの役割をインストールして、Intune サービスに接続できるようにします。 このサイト システムの役割は、設定とアプリケーションを Intune サービスにプッシュします。

 サービス接続ポイントは、設定とソフトウェアの展開情報を Configuration Manager に送信し、モバイル デバイスからステータス メッセージとインベントリ メッセージを取得します。 Configuration Manager サービスは、モバイル デバイスと通信し、設定を保存するゲートウェイとして機能します。

> [!NOTE]
>  サービス接続ポイントのサイト システムの役割は、中央管理サイトかスタンドアロン プライマリ サイトだけにインストールできます。 サービス接続ポイントにはインターネット アクセスが必要です。


### <a name="configure-the-service-connection-point-role"></a>サービス接続ポイントの役割を構成する

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。

2.  **[管理]** ワークスペースで **[サイト]** を展開して、**[サーバーとサイト システムの役割]** をクリックします。

3.  対応する手順を使用して、 **サービス接続ポイント** の役割を新規または既存のサイト システム サーバーに追加します。

    -   新しいサイト システム サーバー: **[ホーム]** タブの **[作成]** グループにある **[サイト システム サーバーの作成]** をクリックして、サイト システム サーバーの作成ウィザードを開始します。

    -   既存のサイト システム サーバー: サービス接続ポイントの役割をインストールするサーバーをクリックします。 [ホーム **** ] タブの [サーバー **** ] グループにある [サイト システムの役割の追加 **** ] をクリックして、サイト システムの役割の追加ウィザードを開始します。

4.  **[システムの役割の選択]** ページで、 **[サービス接続ポイント]**を選んで、 **[次へ]**をクリックします。

![サービス接続ポイントを作成する](../media/mdm-service-connection-point.png)

5.  ウィザードを完了します。

### <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>サービス接続ポイントが Microsoft Intune サービスで認証を行う方法
 サービス接続ポイントは、インターネット経由でモバイル デバイスを管理するクラウド ベースの Intune サービスへの接続を確立することによって、Configuration Manager を拡張します。 サービス接続ポイントは、次のように Intune サービスで認証を行います。

1.  Configuration Manager コンソールで Intune サブスクリプションを作成する場合、Configuration Manager 管理者は、Azure Active Directory に接続して認証されます。Azure Active Directory は、各 ADFS サーバーにリダイレクトして、ユーザーに対してユーザー名とパスワードの入力を求めるダイアログを表示します。 次に、Intune はテナントに証明書を発行します。

2.  手順 1 の証明書は、サービス接続ポイントのサイトの役割にインストールされ、Microsoft Intune サービスとのそれ以降のすべての通信を認証および承認するために使用されます。

## <a name="step-6-enable-platform-enrollment"></a>手順 6: プラットフォームの登録を有効にする
  デバイスの登録を有効にするには、デバイス プラットフォームごとに必要な追加の構成があります。
  - [iOS と Mac の登録セットアップ](#ios-and-mac-enrollment-setup): Apple MDM プッシュ証明書を取得します
  - [Windows の登録セットアップ](#windows-enrollment-setup): DNS を構成し、Windows PC、Windows 10 Mobile デバイス、Windows Phone デバイスのすべてで登録を有効にします
  - Android: Android デバイスの場合、登録を有効にするために必要な追加の手順はありません

MDM 管理を有効にした後は、各ユーザーが登録できるデバイスの数を指定できます (ユーザーごとに最大 15 デバイス)。

### <a name="ios-and-mac-enrollment-setup"></a>iOS と Mac の登録セットアップ
  以下の手順で、Apple MDM プッシュ証明書を Intune サービスにアップロードして Apple デバイスの管理を有効にします。

  1.  **証明書署名要求をダウンロード** - Apple からの APNs 証明書を要求するには、証明書署名要求ファイル (.csr) が必要です。  

      1.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]** >  **[Microsoft Intune サブスクリプション]** に移動します。  

      2.  **[ホーム]** タブで、 **[APNs 証明書要求の作成]**をクリックします。 **[Apple Push Notification サービス証明書署名要求の要求]** ダイアログ ボックスが開きます。  

      3.  **[参照]** をクリックして、新しい証明書署名要求 (.csr) ファイルの保存先のパスを指定します。 証明書署名要求 (.csr) ファイルをローカルに保存します。  

      4.  **[ダウンロード]**をクリックします。 新しい Microsoft Intune .csr ファイルがダウンロードされ、Configuration Manager によって保存されます。 .csr ファイルは、Apple Push Certificates Portal からの信頼関係証明書を要求するために使用します。  

  2.  **Apple からの APNs 証明書の要求** - Apple Push Notification サービス (APNs) 証明書は、管理サービス、Intune、および登録済み iOS モバイル デバイスの間に信頼関係を確立するために使用されます。  

      1.  ブラウザーで [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) に接続し、会社の Apple ID でサインインします。 この Apple ID は、将来 APNs 証明書を更新するときにも使用する必要があります。  

      2.  証明書署名要求 (.csr) ファイルを使用してウィザードを完了します。 APNs 証明書をダウンロードして、.pem ファイルをローカルに保存します。 この APNs 証明書 (.pem) ファイルは、Apple Push Notification サーバーと Intune のモバイル デバイス管理機関との間に信頼関係を確立するために使用されます。  

  3.  **登録を有効にし、APNs 証明書をアップロード** - iOS の登録を有効にするには、APNs 証明書をアップロードします。  

      1.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]**  >  **[Microsoft Intune サブスクリプション]** に移動します。  

      2.  **[ホーム]** タブの **[サブスクリプション]** グループで、**[プラットフォームの構成]**  >  **[iOS]** の順にクリックします。  

          > [!NOTE]  
          >  Configuration Manager コンソールで iOS の登録が有効になるまでは、Apple Push Notification サービス (APNs) 証明書をアップロードしないでください。  

      3.  **[Microsoft Intune サブスクリプションのプロパティ]** ダイアログ ボックスで、 **[iOS]** タブを選択し、 **[iOS の登録を有効にする]** チェック ボックスをオンにします。  

      4.  **[参照]**をクリックし、Apple からダウンロードした APNs 証明書 (.cer) ファイルに移動します。 Configuration Manager に APNs 証明書情報が表示されます。 **[OK]** をクリックして、APNs 証明書を Intune に保存します。    


[iOS と Mac の登録](enroll-hybrid-ios-mac.md)に関する追加情報を参照してください。

### <a name="windows-enrollment-setup"></a>Windows の登録セットアップ  
Configuration Manager を Intune と共に使用して、Windows を実行しているデスクトップやノート PC、その他のデバイスをモバイル デバイスとして管理することができます。 会社または学校のアカウントをデバイスに追加することで、[Azure Active Directory に参加するときに自動的に登録する](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/enroll-hybrid-windows#azure-active-directory-enrollment)ように Windows 10 デバイスを構成することもできます。

DNS エイリアス (CNAME レコード タイプ) を作成すると、デバイスの登録時にサーバー名が自動的に入力されるため、ユーザーがデバイスを簡単に登録できるようになります。 また、Windows PC とモバイル デバイスの登録を有効にすることができるようになります。  

1. Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]** > **[Microsoft Intune サブスクリプション]** に移動し、以下を実行します。  
  - **Windows PC:** **[ホーム]** タブで、**[プラットフォームの構成]**、**[Windows]** の順にクリックします。 **[全般]** タブで **[Windows の登録を有効にする]**を選択します。  
  - **Windows 10 Mobile と Windows Phone:** **[ホーム]** タブで、**[プラットフォームの構成]**、**[Windows Phone]** の順にクリックします。  **[全般]** タブで、  **[Windows Phone 8.1 と Windows 10 Mobile]**を選びます。

2.  また、ポータル サイト アプリを使用して登録を簡易化するように Configuration Manager を構成することもできます。
(省略可能) 会社の DNS レコードに DNS エイリアス (CNAME レコード タイプ) を作成し、会社のドメインの URL に送信された要求を Microsoft のクラウド サービス サーバーにリダイレクトするようにします。  たとえば、会社の Web サイトが contoso.com の場合、EnterpriseEnrollment.contoso.com を EnterpriseEnrollment-s.manage.microsoft.com にリダイレクトする CNAME を DNS に作成する必要があります。  

|型|ホスト名|指定先|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  

詳細については、[Windows の登録](enroll-hybrid-windows.md)に関するページを参照してください。

### <a name="android-enrollment-setup"></a>Android の登録セットアップ
Configuration Manager を Intune と共に使用して、Android を実行している電話とタブレットを管理できます。
1.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]**  >  **[Microsoft Intune サブスクリプション]** に移動します。  

2.  **[ホーム]** タブの **[サブスクリプション]** グループで、**[プラットフォームの構成]**  >  **[Android]** の順にクリックします。  

3.  **[Microsoft Intune サブスクリプションのプロパティ]** ダイアログ ボックスで、 **[Android]** タブを選択し、 **[Android の登録を有効にする]** チェック ボックスをオンにします。

詳細については、[Android](enroll-hybrid-android.md) に関するページを参照してください。

## <a name="step-7-set-up-additional-management"></a>手順 7: 追加の管理をセットアップする
(省略可能) デバイスを登録する前に、追加の管理をセットアップすることができます。 このような管理ソリューションは、デバイスの登録後に作成し、展開することができますが、多くの組織は、デバイスを管理対象にするときに展開することを好みます。

**構成アイテム**を使用すると、デバイスのプラットフォームに基づいて、登録されるデバイスで PIN を必須にする、暗号化を必須にするなどの設定を管理できます。
- [Windows 10 デバイスと Windows 8.1 デバイス](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)
- [Windows Phone デバイス](/sccm/compliance/deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client)
- [iOS デバイスと Mac デバイス](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)
- [Android デバイスと Samsung KNOX Standard デバイス](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)

管理対象デバイスには次の**アプリケーション**を展開できます。
- [iOS アプリケーション](/sccm/apps/get-started/creating-ios-applications)
- [Mac アプリケーション](/sccm/apps/get-started/creating-mac-computer-applications)
- [Windows PC アプリケーション](/sccm/apps/get-started/creating-windows-applications)
- [Windows Phone アプリケーション](/sccm/apps/get-started/creating-windows-phone-applications)
- [Android アプリケーション](/sccm/apps/get-started/creating-android-applications)

**条件付きアクセス**を使用すると、次のような会社のリソースへのアクセスを管理できます。  
- [電子メールへのアクセス](/sccm/protect/deploy-use/manage-email-access)
- [SharePoint へのアクセス](/sccm/protect/deploy-use/manage-sharepoint-online-access)
- [Skype for Business へのアクセス](/sccm/protect/deploy-use/manage-skype-for-business-online-access)
- [Dynamic CRM Online](/sccm/protect/deploy-use/manage-dynamics-crm-online-access)

## <a name="step-8-verify-mdm-configuration"></a>手順 8: MDM の構成を確認する

 次のログ ファイルをチェックして、特定のデバイス管理コンポーネントを確認できます。

-   Cloudusersync.log を参照して、ユーザー アカウントが正常に同期されていることを確認する。

-   Sitecomp.log で、サービス接続ポイントが正常に作成されたことを確認する。

## <a name="step-9-enroll-devices"></a>手順 9: デバイスを登録する
これでハイブリッド セットアップは完了です。 デバイスを Configuration Manager に登録するには、いくつかの方法があります。
- ユーザー所有 (BYOD) のデバイス: [デバイスの登録方法をユーザーに伝えます](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。登録に関するガイダンスは Intune 管理デバイスとハイブリッド管理デバイスで同じです。
- 会社所有 (COD) のデバイス: [会社所有のデバイスを登録します](enroll-company-owned-devices.md)。会社所有のデバイスの登録方法に関するガイダンスはプラットフォームごとに異なります。

## <a name="managing-intune-subscriptions-associated-with-configuration-manager"></a>Configuration Manager に関連付けられている Intune サブスクリプションの管理

Microsoft Intune (試用版サブスクリプションまたは有料サブスクリプション) を Configuration Manager に追加してから、別の Intune サブスクリプションに切り替える必要がある場合は、**Microsoft Intune サブスクリプション**と**サービス接続ポイント**の両方を Configuration Manager コンソールから削除する必要があります。これにより、新しいサブスクリプションを追加することができるようになります。

### <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Configuration Manager から Intune サブスクリプションを削除する方法

> [!IMPORTANT]
>  サブスクリプションを削除すると、Intune サブスクリプションによって管理されるデバイスに構成された、ユーザー登録、ポリシー、アプリの展開などのすべてのコンテンツが削除されます。

1.  Configuration Manager コンソールで、**[管理]** > **[概要]** > **[Cloud Services]** > **[Microsoft Intune サブスクリプション]** の順に移動します。

2.  表示された **[Microsoft Intune サブスクリプション]** を右クリックしてから、**[削除]** をクリックします。

3.   ウィザードで、**[Configuration Manager から Microsoft Intune サブスクリプションを削除]**、**[次へ]**、**[次へ]** の順にクリックして、サブスクリプションを削除します。


### <a name="how-to-remove-the-service-connection-point-role"></a>サービス接続ポイントの役割を削除する方法

1.  **[管理]** > **[概要]** > **[サイトの構成]** > **[サーバーとサイト システムの役割]** の順に移動します。

2.  **[サービス接続ポイント]** の役割をホストするサーバーを選びます。

3.  **[サイト システムの役割]** 一覧で、**[サービス接続ポイント]** を選んでから、リボンに表示されている **[役割の削除]** をクリックします。 ロールを削除することを確認します。 サービス接続ポイントが削除されます。

これで、新しいサービス接続ポイントを作成したり、Configuration Manager に新規 Intune サブスクリプションを追加したり、Configuration Manager を MDM 機関として設定したりできるようになります。

### <a name="how-to-change-mdm-authority-to-intune"></a>MDM 機関を Intune に変更する方法

バージョン 1610 以降では、MDM 機関を Configuration Manager から Intune に切り替えることができます。 この機能についての情報は間もなく公開されます。



<!--HONumber=Dec16_HO3-->


