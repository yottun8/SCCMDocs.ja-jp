---
title: "ハイブリッド MDM の新機能 |Microsoft ドキュメント"
description: "System Center Configuration Manager と Intune のハイブリッド展開で使用できるモバイル デバイス管理の新機能について説明します。"
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 9f3088e90c3259adc3c3b9c6873978d1db4dd1d8
ms.openlocfilehash: 05e4a9687d29c5377303afd8b08352a6a77fa58e

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用したハイブリッド モバイル デバイス管理の新機能

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、System Center Configuration Manager と Intune のハイブリッド展開で使用できるモバイル デバイス管理 (MDM) の新機能の詳細について説明します。  

##  <a name="compatibility-with-configuration-manager-versions"></a>Configuration Manager のバージョンとの互換性  

 この記事の各セクションでは、3 つの異なるカテゴリにあるハイブリッド機能を一覧表示します。 次のガイダンスを使用すると、各カテゴリの機能とさまざまなバージョンの Configuration Manager との互換性を判断できます。  

|機能のカテゴリ|説明|
|-|-|
|**Microsoft Intune の新機能** | 通常、このカテゴリに一覧表示されたすべての機能は、System Center 2012 R2 Configuration Manager リリースを含むすべての Configuration Manager のリリースで動作します。これらの機能は Intune サービスのみを必要とし、Configuration Manager の追加機能は必要ないためです。|
|**Configuration Manager Technical Preview の新機能**| このカテゴリに一覧表示されたすべての機能は、指定されたバージョンの Technical Preview リリースでのみ動作します。 これらの機能を試すには、機能の説明で指定されたバージョンの Technical Preview をインストールする必要があります。 詳細については、「[System Center Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」をご覧ください。|
|**Configuration Manager (現在のブランチ) の新機能**| このカテゴリに一覧表示されたすべての機能は、バージョン 1511 や 1602 など、指定されたバージョンの Configuration Manager (現在のブランチ) でのみ動作します。 ハイブリッド展開に旧バージョンの Configuration Manager を使用している場合は、機能の説明で指定されたバージョンの Configuration Manager (現在の分岐) にアップグレードする必要があります。 詳細については、「[System Center Configuration Manager へのアップグレード](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)」を参照してください。|

## <a name="new-hybrid-features-in-december-2016"></a>2016 年 12 月のハイブリッド新機能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

2016 年 12 月に導入された次の Intune 機能は、ハイブリッド展開で動作します。

- **登録での Multi-Factor Authentication (MFA) が Azure Portal に移動する**

  これまで、Intune の登録に MFA を設定するには、Intune コンソールまたは構成マネージャー コンソールを使用していました。 この機能更新により、Intune の資格情報で Microsoft Azure Portal (https://manage.windowsazure.com) にログインし、Azure AD を使用して MFA の設定を構成するようになりました。 詳細については、「Microsoft Intune のMulti-Factor Authentication」 (https://aka.ms/mfa_ad) を参照してください。

- **Android 用ポータル サイト アプリが中国で利用可能になる**

  Android 用ポータル サイト アプリが中国で利用できるようになりました。 中国には Google Play ストアがないため、Android デバイスでは中国のアプリ マーケットプレースからアプリを入手する必要があります。 Android 用ポータル サイト アプリは、次のストアからダウンロードできます。

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  Android 用ポータル サイト アプリは、Google Play サービスを使って Microsoft Intune サービスと通信します。 中国では Google Play サービスをまだ利用できないので、次のタスクが完了するまで最大 8 時間かかることがあります。

  | Configuration Manager 管理コンソール | Android 用 Intune ポータル サイト アプリ | Intune ポータル サイト Web サイト |
  |----|----|----|      
  | 削除/ワイプ (すべてのデータの削除)   | リモート デバイスの削除 | デバイスの削除 (ローカルおよびリモート) |
  | 削除/ワイプ (会社データの削除)   | デバイスのリセット | デバイスのリセット|
  | 新規アプリまたは更新アプリの展開 | 使用可能な基幹業務アプリのインストール | デバイスのパスコードのリセット|
  | リモート ロック | | |
  | パスコードのリセット | | |        


## <a name="new-hybrid-features-in-november-2016"></a>2016 年 11 月のハイブリッド新機能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

2016 年 11 月に導入された次の Intune 機能は、ハイブリッド展開で動作します。

- **新しい Microsoft Intune ポータル サイトが Windows 10 デバイスで利用可能になる**

  Microsoft は、新しい [Windows 10 デバイス用のポータル サイト アプリ](https://www.microsoft.com/store/apps/9wzdncrfj3pz)をリリースしました。 このアプリでは新しい Windows 10 ユニバーサル形式を利用し、PC やモバイルなどすべての Windows 10 デバイスで同じ更新されたユーザー エクスペリエンスが提供されますが、以前のポータル サイトアプリで提供されている同じ機能はすべて引き続き利用できます。

  この新しいアプリでは、Windows 10 デバイスでのシングル サインオン (SSO) や証明書ベースの認証など、プラットフォーム機能も利用します。 アプリは、既存の Windows 8.1 ポータル サイトおよび Windows Phone 8.1 ポータル サイトのインストールのアップグレードとして Windows ストアから入手できるようになります。 詳細については、[Intune サポート チームのブログ](http://aka.ms/intunecp_universalapp)を参照してください。

  新しいポータル サイト アプリでは、Configuration Manager コンソールで**使用可能**とマークされたビジネス アプリケーションの Windows ストアも表示されます。


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能

Configuration Manager Technical Preview リリースで以前に提供されていた次の機能は、Intune と Configuration Manager (Current Branch) バージョン 1610 のハイブリッド展開で使用できるようになりました。

* [構成項目の追加設定とエクスペリエンス向上](/sccm/core/plan-design/changes/whats-new-in-version-1610?branch=sccm-1610-release#new-compliance-settings-for-configuration-items)
* [DEP プロファイルの追加設定](#new-in-configuration-manager-technical-preview-1609)
* [ビジネス向け Windows ストアの有料アプリ](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Windows 10 VPN プロファイルのネイティブ接続の種類](#new-in-configuration-manager-technical-preview-1609)
* [Intune コンプライアンス チャート](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [コンソールからのポリシー同期の要求](/sccm/mdm/deploy-use/sync-intune-device)
* [Windows Defender の構成設定](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

次の追加のハイブリッド機能も、 Configuration Manager (Current Branch) のバージョン 1610 に含まれます。

- **登録されるデバイス数の増加**

  ユーザーが最大 15 台のデバイスを登録できるようになりました。 以前の制限はユーザーあたり 5 台のデバイスでした。


- **追加のセキュリティのサポート**

  完全な権限を持つ管理者に加えて、次の組み込みのセキュリティ ロールが、事前に宣言されたデバイス、iOS 登録プロファイル、および Windows 登録プロファイルを含むすべての企業所有のデバイス ノードの項目にフル アクセスできるようになりました。

    - 資産マネージャー
    - 会社リソース アクセス マネージャー

  Configuration Manager コンソールのこれらの領域への読み取り専用アクセスは、引き続き読み取り専用アナリスト ロールに与えられます。

- **Windows 情報保護アプリからの VPN アクセスの自動トリガー**

  Windows 10 VPN プロファイルに Windows 情報保護プライマリ ドメインを追加して、関連付けられたすべてのアプリがデバイスで実行されるときに、それらに VPN 接続を自動的にトリガーさせることができます。 このオプションは、ネイティブ接続の種類を選択した場合のみ使用できます。

- **Windows 10 VPN プロファイルの条件付きアクセス**

    Configuration Manager コンソールで作成した Windows 10 VPN プロファイル経由で VPN アクセスできるようにするためには、Azure Active Directory に登録された Windows 10 デバイスを対応させる必要があります。 これは、VPN プロファイル ウィザードの [認証方法] ページの新しい **[この VPN 接続の条件付きアクセスを有効にする]** チェックボックスおよび Windows 10 VPN プロファイルの VPN プロファイルのプロパティによって可能です。 このオプションは、ネイティブ接続の種類を選択した場合のみ使用できます。

    プロファイルの条件付きアクセスを有効にした場合、シングル サインオン認証用の別の証明書を指定することもできます。

## <a name="new-hybrid-features-in-october-2016"></a>2016 年 10 月のハイブリッド新機能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

2016 年 10 月に導入された次の Intune 機能は、ハイブリッド展開で動作します。

- **モバイル アプリケーション管理の条件付きアクセス**

  Outlook など、Intune モバイル アプリケーション管理ポリシーをサポートするアプリからのアクセスのみを許可するように、Exchange Online へのアクセスを制限することができます。 [この新機能](/intune/deploy-use/allow-policy-managed-apps-access-to-o365)は、組み込みのメール クライアントや Intune MAM ポリシーが構成されていない他のアプリへのアクセスをブロックできるため、Intune のモバイル アプリ管理 (MAM) ポリシーと組み合わせると効果的です。 これにより、ユーザーが組織のデータにアクセスする際に、Intune MAM を使用して保護できるアプリを使用するようになります。 Intune モバイル アプリ管理は、Azure Portal から使用することができます。 [設定] ブレードの新しい [条件付きアクセス] セクションを探してください。

-   **Android 用 Intune アプリ ラッピング ツール**

  アプリで Intune モバイル アプリケーション管理 (MAM) ポリシーを使用できるようにするには、Intune アプリ ラッピング ツールを使用します。

- **Android Samsung KNOX Standard と Intune との互換性**

  Samsung Galaxy Ace 電話の特定のモデルは、Samsung KNOX Standard デバイスとして Intune で管理できません。 これらのデバイスを Intune に登録すると、標準の Android デバイスとして管理されます。

  この影響を受けるモデル番号は次のとおりです。

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  管理者とエンドユーザーは、これ以上操作を行う必要はありません。 詳細については、Samsung KNOX の Web サイトを参照してください。

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Configuration Manager Technical Preview 1610 の新機能

2016 年 10 月の Configuration Manager Technical Preview 1610 では、次のハイブリッド新機能が導入されました。

- **管理コンソールからのポリシー同期の要求**

  Configuration Manager コンソールから、登録モバイル デバイスでのポリシー同期を要求できます。デバイス自体でポータル サイト アプリでの同期を要求する必要はありません。 これは、[リモート デバイスの操作] メニューにある **[Send Sync Request]** (同期要求の送信) と呼ばれる新しい操作であり、[デバイス] ノードでモバイル デバイスを選択するとリボンに表示されます。

- **Windows Defender の構成設定**

  Configuration Manager コンソールの構成項目を使用して、Intune に登録されている Windows 10 コンピューターで Windows Defender クライアント設定を構成できるようになりました。 構成項目ウィザードには、**Windows Defender** と呼ばれる新しい設定グループがあります。 この機能は、Windows 10 バージョン 1511 以降でのみサポートされています。


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能

2016 年 8 月の Configuration Manager (現在のブランチ) では、ハイブリッド新機能は導入されていません。

## <a name="new-hybrid-features-in-september-2016"></a>2016 年 9 月のハイブリッド新機能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

2016 年 9 月に導入された次の Intune 機能は、ハイブリッド展開で動作します。

- **Android 用ポータル サイトへの "通知" の追加**

  Android 用ポータル サイトのホームページに新しい通知アイコンが追加されました。 このアイコンをタップすると [通知] ページが開き、ポータル サイト アプリの中でエンドユーザーが注目する必要のある項目がすべて表示されます。たとえば、デバイスのコンプライアンス非対応、登録の更新、登録のアクティブ化です。 iOS 版のポータル サイト アプリには既に、この通知機能が追加されています。 この新しい [通知] ページの導入に伴い、[会社アクセスのセットアップ] ページがポータル サイトの起動または再開のたびに表示されることはなくなりました (ただし、デバイスが登録済みである場合)。 管理者が独自にエンドユーザー向けガイドを作成している場合は、必要に応じてこの変更をドキュメントに反映してください。 更新後のスクリーン ショットは[こちら](https://aka.ms/androidcpupdate)にあります。

- **iOS ポータル サイト アプリのサポートの変更**

  iOS 用 Microsoft Intune ポータル サイト アプリのすべてのユーザーが、アプリの最新バージョンを使用するように要求されます。 新しいユーザーは最新バージョンのみをダウンロードでき、現在のユーザーは最新バージョンへの更新を求められます。 最新バージョンを使用するには iOS 8.0 以降が必要であり、デバイスで以前の iOS バージョンを実行している場合は、デバイスを iOS 8.0 以降に更新したうえでポータル サイト アプリを最新バージョンに更新するまで、ポータル サイトを使用できず、登録することもできません。 iOS 8.0 以前のバージョンを実行している登録済みのデバイスは、引き続き管理対象であり、Intune 管理コンソールに表示されます。

- **フィードバック ボタンを Windows Phone 8.1 ポータル サイト アプリに追加**

  Windows Phone 8.1 ポータル サイト アプリでは、エンドユーザーが新しい [フィードバックの送信] ボタンを使用してアプリに関するフィードバックを送ることができます。 フィードバックを送信するには、ポータル サイト アプリの画面の右下にある "..." メニューをタップし、**[フィードバックの送信]** をタップします。 フィードバックは匿名化して収集され、ポータル サイト アプリのユーザー エクスペリエンス向上に役立てられます。

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Configuration Manager Technical Preview 1609 の新機能

2016 年 9 月の Configuration Manager Technical Preview 1609 では、次のハイブリッド新機能が導入されました。

- **構成項目設定の追加設定とエクスペリエンス向上**

  Android、iOS、および Windows 用に新しい設定が追加されており、[サポートされているプラットフォーム] ページで選択したプラットフォームに適用される設定のみがウィザードに表示されます。 詳細については、「[New compliance settings for configuration items in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items)」 (TP 1609 の構成項目の新しいコンプライアンス設定) を参照してください。

- **DEP プロファイルの追加設定**

  iOS デバイスの DEP プロファイルに、構成可能な設定として TouchID、ApplePay、および Zoom が追加されました。

- **ビジネス向け Windows ストアのアプリの有料アプリ**

  ビジネス向け Windows ストアに有料と無料の両方のアプリケーションを追加し、組織内のユーザーに展開できるようになりました。 詳細については、「[Enhancements to Windows Store for Business in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager)」 (TP 1609 のビジネス向け Windows ストアの機能強化) を参照してください。

- **Windows 10 VPN プロファイルのネイティブ接続の種類**

  OMA-URI を使用しなくても、Configuration Manager コンソールで Microsoft 自動、IKEv2、および PPTP 接続の種類を使用して、MDM 用の Windows 10 VPN プロファイルを作成できるようになりました。

- **Intune コンプライアンス チャート**

  [監視] ワークスペースの新しいチャートを使用して、全体的なデバイス コンプライアンスの簡易ビュー、および非準拠の主な理由を取得できます。 詳細については、「[Intune compliance charts in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts)」 (TP 1609 の Intune コンプライアンス チャート) を参照してください。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能

2016 年 9 月に導入された次の新機能は、Microsoft Intune と Configuration Manager パージョン 1606 (現在のブランチ) のハイブリッド展開で使用できます。

- **iOS 10 のサポート**

  すべての iOS プラットフォームを対象にしたプロファイルまたは構成項目がある場合は、これらも iOS 10 にプッシュできます。 iOS 10 を含む個々 の iOS プラットフォームをプロファイルおよび構成項目の対象にできるように、Configuration Manager バージョン 1606 への更新プログラムもリリースしました。 更新プログラムをインストールするには、Configuration Manager 管理者コンソールで **[管理] > [概要] > [Cloud Services] > [更新とサービス]** を選択します。 更新プログラムの詳細については、[http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616) を参照してください。

## <a name="new-hybrid-features-in-august-2016"></a>2016 年 8 月のハイブリッド新機能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

2016 年 8 月に導入された次の Intune 機能は、ハイブリッド展開で動作します。

- **ポータル サイト アプリでの Android 7 サポート**

  Android 用 Intune ポータル サイト アプリは、近日公開予定のモバイル デバイス用の Android 7.0 オペレーティング システムに対して "Day 0" サポートを提供します。

- **Google による Android 7.0 デバイスでのリモート パスコード リセット機能の削除**

  Google は、IT 管理者およびエンドユーザーが Android 7.0 デバイスのパスコードをリモートでリセットする機能を削除しています。 以前、IT 管理者はユーザーのパスコードをリモートでリセットでき、エンドユーザーはポータル Web サイトから自分のパスコードをリセットできました。

- **Samsung KNOX Standard デバイス用のアプリの許可およびブロック ポリシー**

  Samsung KNOX Standard デバイスに対してカスタム ポリシーを構成できるようになりました。これにより、次のいずれかを作成できます。

  - デバイスで実行できないようブロックされているアプリの一覧。 ブロックされているアプリの一覧で定義されているアプリは、インストールされていても、デバイスでアクティブにできません。
  - デバイスのユーザーが Google Play ストアからインストールできるアプリの一覧。 それ以外のアプリをストアからインストールすることはできません。

  これらの設定は、Samsung KNOX Standard を実行するデバイスでのみ使用できます。 詳細については、「[カスタム ポリシーを使用して、Samsung KNOX Standard デバイス用のアプリを許可またはブロックする](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps)」を参照してください。

- **ポータル サイトから Microsoft への [フィードバック] リンク**

   ポータル Web サイトでは、エンドユーザーが、ページの下部にある新しい [フィードバック] リンクをタップして、サイトの使用経験に関するフィードバックを Microsoft に送信できます。 フィードバックは匿名化して収集され、ポータル Web サイトのユーザー エクスペリエンス向上に役立てられます。

- **iOS Managed Browser の最小バージョンの 8.0 への更新**

  iOS 用 Microsoft Intune Managed Browser アプリが、iOS 8.0 以降を実行しているデバイスをサポートするように更新されました。 iOS 7.1 デバイスは既存の Managed Browser アプリをまだ使用できますが、Managed Browser の新機能にアクセスして最大限に活用するために、iOS 8.0 以降に更新することをユーザーにお勧めしてください。

### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview の新機能

2016 年 8 月の Configuration Manager Technical Preview では、ハイブリッド新機能は導入されていません。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能

2016 年 8 月の Configuration Manager (現在のブランチ) では、ハイブリッド新機能は導入されていません。

## <a name="new-hybrid-features-in-july-2016"></a>2016 年 7 月のハイブリッド新機能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

2016 年 7 月に導入された次の Intune 機能は、ハイブリッド展開で動作します。

- **Intune アプリ用の Xamarin SDK を使用可能**

  Intune アプリ SDK Xamarin コンポーネントを使用すると、Xamarin でビルドされたモバイル iOS および Android アプリで Intune モバイル アプリ管理機能を有効化できます。 このコンポーネントは、[Xamarin ストア](https://components.xamarin.com/view/Microsoft.Intune.MAM)または [Microsoft Intune Github ページ](https://github.com/msintuneappsdk)で入手できます。

- **Windows デバイス登録時のエンドユーザー エクスペリエンスの向上**

  条件付きアクセスを使用している場合は、ポータル Web サイトに Windows 8.1、Windows 10 デスクトップ、および Windows 10 Mobile の登録の手順が明記されています。 ユーザーに対して**デバイスの登録**手順と**社内参加**手順が切り離されて表示され、容易にデバイスの状態を確認したり、社内参加 (WPJ) エラーが発生した場合にプロセスを完了したりできます。 また、手順を切り離すことで、IT 管理者のトラブルシューティング プロセスが簡素化されることも考えられます。 以前は、エンドユーザーが登録を試みて、WPJ を除くすべての登録手順が正常に実行された場合、登録デバイスがデバイスの一覧に表示されずにユーザーが識別できなかったので、混乱を招いていました。

 - **Windows 10 デバイスでフル ワイプが使用可能に**

    モバイル デバイスとして登録されている Windows 10 PC およびラップトップをワイプして、デバイスを出荷時の設定にリセットできます。 詳細については、「[How to protect your devices with remote wipe](/sccm/mdm/deploy-use/wipe-lock-reset)」 (リモート ワイプを使用して Windows デバイスを保護する方法) を参照してください。

- **iOS ポータル サイト アプリのデバイス登録マネージャー アカウントの変更**

  Intune では、パフォーマンスと拡張性を向上させるために、iOS ポータル サイト アプリの [デバイス] ウィンドウにデバイス登録マネージャー (DEM) の一部のデバイスが表示されなくなりました。 表示されるのは、ポータル サイト アプリを使用して登録されている、アプリを実行中のローカル デバイスに限られます。

  DEM ユーザーはローカル デバイスで操作を実行できますが、その他の登録デバイスのリモート管理は Intune 管理コンソールからのみ実行できます。 また、Intune は Apple Device Enrollment Program または Apple Configurator ツールでの DEM アカウントの使用を廃止しようとしています。 これらの両方の登録方法では、ユーザーを介さない共有 iOS デバイスの登録が既にサポートされています。

  DEM アカウントは、ユーザーを介さない共有デバイスの登録が使用できない場合にのみ使用してください。 詳細については、「[Microsoft Intune のデバイス登録マネージャーを使用した企業所有のデバイスの登録](../deploy-use/enroll-devices-with-device-enrollment-manager.md)」を参照してください。

- **Android ポータル サイト アプリの変更**

  Android エンドユーザーに対して、デバイスに必要な証明書がないことを示すエラー メッセージが表示される場合は、[この問題を解決する方法] ボタンをタップして、不足している証明書をインストールする手順を確認できます。 ユーザーが手順を完了しても、"証明書がない" ことを示すエラー メッセージがさらに表示される場合は、IT 管理者に連絡してこのリンクを提示するよう求められます。このリンクには、証明書の問題を解決するために IT 管理者が使用できる手順が含まれています。

- **登録 Android デバイスへのサイドロード アプリのインストールの制限**

  Android 用 Intune ポータル サイト アプリを使用して Intune にデバイスを登録している場合を除き、Android デバイスは、ポータル Web サイトを介してアプリケーションをインストールできなくなりました。


### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview の新機能

2016 年 7 月の Configuration Manager Technical Preview では、ハイブリッド新機能は導入されていません。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能

Configuration Manager Technical Preview リリースで以前提供されていた次の機能は、Intune と Configuration Manager (現在のブランチ) バージョン 1606 のハイブリッド展開で使用できるようになりました。

* Configuration Manager コンソールから Windows 10 デバイスに対してビジネス向け Windows ストアのアプリを検索、管理、配布する ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   Android デバイス用の SmartLock 設定 ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   Windows 10 デバイス用のアプリトリガー VPN ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   リモート デバイスの操作の新しいエクスペリエンス ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   ビジネス向け Windows ストアのアプリ ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   ボリューム購入アプリの全般的な向上 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Windows 情報保護 (WIP) ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   IMEI または iOS シリアル番号を持つ会社所有のデバイスの事前宣言 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   デバイスを自動的にコレクションごとに分類 ([1606](whats-new-hybrid-archive.md#new-in-1606-technical-preview))

新機能については、特定の Technical Preview リリースに関するドキュメントを参照してください。

## <a name="notices"></a>通知

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 および System Center 2012 R2 Configuration Manager (RTM): 2017 年 4 月 10 日に終了するハイブリッド モバイル デバイス管理のサポート

*2017 年 1 月 11 日*

System Center 2012 Configuration Manager SP1 と System Center 2012 R2 Configuration Manager RTM のサポートは 2016 年 7 月 12 日に終了しました。 これに続き、2017 年 4 月 10 日にハイブリッド MDM の Microsoft Intune サービスに接続するこれらのリリースのサポートが終了します。 この日付以降、ハイブリッド MDM はこれらのリリースをもって機能を停止します。 Intune コネクタが Intune サービスに接続できなくなるため、管理対象のデバイスは実質的に非管理対象となります。 アップグレードが実施されるまで、Configuration Manager のデータ (ポリシーとアプリケーションなど) は Intune にフローアップせず、管理対象のデバイスのデータは Configuration Manager にフローダウンしません。

Configuration Manager 2012 SP1 または R2 RTM でハイブリッド展開を実行している場合は、2017 年 4 月 10 日より前に、Configuration Manager (Current Branch) または Configuration Manager 2012 (R2 SP1 または SP2) の最新のサポートされているサービス パックにアップグレードしてサービスの中断を回避することをお勧めします。

その他のリソース:
-   [System Center Configuration Manager (Current Branch) へのアップグレード](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [System Center 2012 R2 Configuration Manager SP1 へのアップグレードの計画](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [System Center 2012 Configuration Manager SP2 へのアップグレードの計画](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Windows Phone 8 ポータル サイトのアップロードの廃止
*2016 年 10 月 25 日*

11 月に Windows 8、Windows Phone 8、および Windows RT に対する Intune サポートが廃止され、Windows Phone 8 ポータル サイトのサポートが終了するので、Configuration Manager コンソールでは、署名済みのポータル サイト アプリをアップロードする機能が廃止されました。  既に登録されている Windows 8、Windows Phone 8、および Windows RT デバイスは引き続きサポートされますが、これらのプラットフォームへの追加デバイスの登録はサポートされていません。


## <a name="see-also"></a>関連項目

- [過去のハイブリッド MDM 機能](whats-new-hybrid-archive.md)
- [System Center 2012 Configuration Manager の MDM 向け新機能](https://technet.microsoft.com/library/mt445560.aspx)



<!--HONumber=Jan17_HO2-->


