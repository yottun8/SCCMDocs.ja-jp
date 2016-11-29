---
title: "アーカイブ | ハイブリッド MDM の新機能 |Microsoft Intune |System Center Configuration Manager"
description: "System Center Configuration Manager と Intune のハイブリッド展開で使用できる過去のモバイル デバイス管理機能のアーカイブです。"
ms.custom: na
ms.date: 10/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: Mtillman
ms.author: mtillman
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: bfc4baefbdddc5125c38272f2087d214151c91d5
ms.openlocfilehash: 4c0910ae365e1fda7b9747b79e13782a6056c0da

---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune での過去のハイブリッド機能

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、System Center Configuration Manager と Intune のハイブリッド展開で使用できる過去のモバイル デバイス管理 (MDM) 機能の詳細について説明します。  

##  <a name="compatibility-with-configuration-manager-versions"></a>Configuration Manager のバージョンとの互換性  

 この記事の各セクションでは、3 つの異なるカテゴリにあるハイブリッド機能を一覧表示します。 次のガイダンスを使用すると、各カテゴリの機能とさまざまなバージョンの Configuration Manager との互換性を判断できます。  

|機能のカテゴリ|
|-|  
|**Microsoft Intune の新機能** - 通常、このカテゴリに一覧表示されたすべての機能は、System Center 2012 R2 Configuration Manager リリースを含むすべての Configuration Manager のリリースで動作します。これらの機能は Intune サービスのみを必要とし、Configuration Manager の追加機能は必要ないためです。<br /><br /> **Configuration Manager Technical Preview の新機能** - このカテゴリに一覧表示されたすべての機能は、指定されたバージョンの Technical Preview リリースでのみ動作します。 これらの機能を試すには、機能の説明で指定されたバージョンの Technical Preview をインストールする必要があります。 詳細については、「[System Center Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を参照してください。<br /><br /> **Configuration Manager (現在のブランチ) の新機能** - このカテゴリに一覧表示されたすべての機能は、バージョン 1511 や 1602 など、指定されたバージョンの Configuration Manager (現在のブランチ) でのみ動作します。 ハイブリッド展開に旧バージョンの Configuration Manager を使用している場合は、機能の説明で指定されたバージョンの Configuration Manager (現在の分岐) にアップグレードする必要があります。 詳細については、「[System Center Configuration Manager へのアップグレード](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)」を参照してください。|  

## <a name="new-hybrid-features-in-june-2016"></a>2016 年 6 月のハイブリッド新機能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能
2016 年 6 月に導入された次の Intune 機能は、ハイブリッド展開で動作します。

- **Intune のサービス正常性** Intune のサービス正常性情報は、他の Microsoft サービスと共に中央の場所に移動されました。 この情報は、Office 365 管理ポータルの [サービス正常性] に表示されるようになりました。 詳細については、この[ブログ記事](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/)を参照してください。

- **強化された Windows 10 エンタープライズ データ ポリシーの構成エクスペリエンス**

  Intune では、Windows 10 情報保護ポリシーを構成するためのエクスペリエンスが強化されました。 この強化では、アプリの規則を作成したり、ネットワーク境界の定義やその他の Windows 情報の保護設定を指定したりする方法が向上しています。 詳細については、「[Microsoft Intune を使用して Windows 情報保護 (WIP) ポリシーを作成する](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune)」を参照してください。

- **Intune 用の Cisco ISE ネットワーク アクセス制御ポリシー**

  Cisco Identity Service Engine (ISE) 2.1 と Microsoft Intune の両方を使用するユーザーは、ISE でネットワーク アクセス制御ポリシーを設定できます。このポリシーを使用して、WiFi または VPN を使用してネットワークに接続する必要があるデバイスは、アクセス許可を受けるために次の条件を満たす必要があります。

  - Intune で管理する必要がある
  - 展開されているすべての Intune コンプライアンス ポリシーに準拠している必要がある

  非準拠デバイスのエンドユーザーは、登録を行うとともに、アクセス許可を受けるためにすべてのコンプライアンス問題を修正するよう求められます。

- **ブラウザーの条件付きアクセス**

  Exchange Online と SharePoint Online が、管理対象の準拠 iOS および Android デバイスでサポートされている Web ブラウザーからのみアクセスできるように、条件付きアクセス ポリシーを設定することができます。 iOS および Android デバイスで Outlook Web Access (OWA) および SharePoint サイトにサインインしようとするエンドユーザーは、Intune にデバイスを登録するとともに、サインインを完了するために非準拠に関するすべての問題を修正するよう求められます。 詳細については、次を参照してください:

  * [Intune で Exchange Online と新しい Exchange Online Dedicated への電子メール アクセスを制限する](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Microsoft Intune で SharePoint Online へのアクセスを制限する](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online による条件付きアクセスのサポート**

  Dynamics CRM Online が管理対象の準拠 iOS および Android デバイスからのみアクセスできるように、条件付きアクセス ポリシーを設定することができます。 iOS および Android で Dynamics CRM モバイル アプリにサインインしようとするエンドユーザーは、Intune に登録するとともに、サインインを完了するために非準拠に関するすべての問題を修正するよう求められます。 詳細については、「[Restrict access to Dynamics CRM Online with Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune)」 (Microsoft Intune での Dynamics CRM Online へのアクセスの制限) を参照してください。

- **Android ポータル サイト アプリの更新**

  Intune では、Android ポータル サイトのユーザーに影響を与える次の新しいポリシーが使用されるようになりました。   

  ポリシー  |ユーザーに対する影響  
  ---------|---------
  デバイスで、不明なソース (Android 4.0 以降) からのアプリのインストールを無効にする必要がある     |  Android 4.0 以降のデバイスのエンドユーザーに対して、「不明なソースからのインストールを無効にする必要があります」というメッセージが表示されます。 ユーザーはデバイスで **[設定]、[セキュリティ]** に移動し、**[不明なソース]** をオフにする必要があります。 ユーザーはコンプライアンス メッセージ内のリンクを使用すると、このメッセージについて、およびこの設定の無効化が求められる理由について、詳細情報を得ることができます。
  デバイスで、不明なソース (Android 4.0 以降) からのアプリのインストールを無効にする必要がある  |    Android 4.0 以降のデバイスのエンドユーザーに対して、「端末をスキャンしてセキュリティ上の脅威を確認」というメッセージが表示されます。 ユーザーはデバイスで **[設定]、[Google]、[セキュリティ]** に移動し、**[端末をスキャンしてセキュリティ上の脅威を確認]** をオンにする必要があります。 ユーザーはコンプライアンス メッセージ内のリンクを使用すると、このメッセージについて、およびこの設定の有効化が求められる理由について、詳細情報を得ることができます。     
  USB デバッグを無効にする必要がある (Android 4.2 以降)  | Android 4.2 以降のデバイスのエンドユーザーに対して、「USB デバッグを無効にする必要があります」というメッセージが表示されます。 ユーザーはデバイスで **[設定]、[開発者オプション]** に移動し、**[USB デバッグ]** をオフにする必要があります。 ユーザーはコンプライアンス メッセージ内のリンクを使用すると、このメッセージについて、およびこの設定の無効化が求められる理由について、詳細情報を得ることができます。
  Android のセキュリティ更新プログラムの最低限レベル (Android 6.0 以降)  | Android 6.0 以降のデバイスのエンドユーザーに対して、「このデバイスは Android の最小セキュリティ パッチ レベルを満たしていません」というメッセージが表示されます。 ユーザーは、必要なセキュリティ更新プログラムをインストールする必要があります。 コンプライアンス メッセージ内のリンクを使用すると、必要なセキュリティ更新プログラムをインストールする方法、および現在インストールされているセキュリティ更新プログラムを確認する方法について、情報を得ることができます。

- **iOS ポータル サイト アプリの更新**

  * エンドユーザーが基幹業務アプリをインストールする際に、強化されたアプリ インストール エクスペリエンスが得られるようになりました。 アプリのインストールに長い時間がかかる場合、そのデバイスを手動で同期して、同期プロセスを強制的に再開できます。 エンドユーザーの手順を確認するには、「Sync your iOS device manually」 (iOS デバイスの手動同期) を参照してください。
  * iOS 用 Microsoft Intune ポータル サイト アプリが更新され、iOS Version 8.0 以降をサポートするようになりました。 この更新は、デバイスで iOS Version 8.0 以降が実行されている場合にのみ、エンドユーザーがポータル サイト アプリをインストールし、Intune に新しいデバイスを登録できることを意味します。 サポートされていないバージョンの iOS が実行されているデバイスを登録済みの場合、ユーザーはそのデバイス上のポータル サイト アプリを引き続き使用できます。


### <a name="new-in-1606-technical-preview"></a>1606 Technical Preview の新機能
2016 年 6 月に導入された次の新機能は、Intune と Configuration Manager Technical Preview 1606 のハイブリッド展開で使用できます。

- **デバイスを自動的にコレクションごとに分類**

  Intune と Configuration Manager を使用している場合に、デバイス コレクションにデバイスを自動的に配置するために使用できる、デバイス カテゴリを作成することができます。 ユーザーは Intune にデバイスを登録するときに、デバイス カテゴリの選択を求められます。 Configuration Manager コンソールから、デバイスのカテゴリをさらに変更できます。 詳細については、「[Capabilities in Technical Preview 1606 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606.md)」 (System Center Configuration Manager の Technical Preview 1606 の機能) の「[Automatically categorize devices into collections](/sccm/core/get-started/capabilities-in-technical-preview-1606.md#dmp_category)」 (デバイスを自動的にコレクションごとに分類) を参照してください。

  > [!IMPORTANT]
  > この機能は、Microsoft Intune の 2016 年 6 月のリリースで動作します。 これらの手順を実行する前に、今回のリリースに更新していることを確認してください。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能
2016 年 6 月の Configuration Manager (現在のブランチ) では、ハイブリッド新機能は導入されていません。

##  <a name="new-hybrid-features-in-may-2016"></a>2016 年 5 月のハイブリッド新機能  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能  
 2016 年 5 月に導入された次の Intune 機能は、ハイブリッド展開で動作します。

- **MAM SDK: PIN の長さの構成のサポート**

  デバイス PIN のように MAM アプリに対して PIN の長さを指定できるようになりました。 その際には、設定した新しい制限にエンドユーザーが準拠する必要があります。 より長いアカウントの入力に対応するために、PIN 画面が若干変更されています。 詳細については、「[MAM policy settings for Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings)」 (Android 用の MAM ポリシー設定) および 「[MAM policy settings for iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings)」 (iOS 用の MAM ポリシー設定) を参照してください。  

- **Android および iOS 用の Skype for Business**

  [登録ポリシーのない MAM](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune) で Skype for Business を対象にできるようになりました。 ユーザーがログインすると、MAM ポリシーが適用されます。  

- **MAM ポリシーによる管理に使用できる新しいアプリ**

  Intune に登録されていないデバイスで、Android 用の Microsoft Word、Excel、および PowerPoint の各アプリを MAM ポリシーに関連付けできるようになりました。 サポートされているすべてのアプリの一覧については、[Microsoft Intune アプリケーション パートナー](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx) ページの Microsoft Intune モバイル アプリケーション ギャラリーを参照してください。  

- **Android ポータル サイト アプリ: エンドユーザー トースト通知**

  エンドユーザーがポータル サイトで自分のデバイスを登録または削除すると、Android ポータル サイト アプリからトースト通知が表示されます。  

- **ポータル Web サイト: デバイス識別バナーがエンドユーザーに詳細情報を提供**

  エンドユーザーは、ポータル Web サイトを使用しているときに、選択したデバイスをより簡単に識別できるようになりました。 不正なデバイスが選択されている場合は、ホーム ページ バナーの **[Tap here]** (ここをタップ) リンクをタップして、適切なデバイスを選択できます。  


### <a name="new-in-1605-technical-preview"></a>1605 Technical Preview の新機能  
 2016 年 5 月に導入された次の新機能は、Intune と Configuration Manager Technical Preview 1605 のハイブリッド展開で使用できます。 これらの機能は、Configuration Manager コンソールを使用して構成および管理する必要があります。  

- **Windows 10 デバイス用のアプリトリガー VPN**

  Configuration Manager と Intune を使用して管理されている Windows 10 デバイスの場合、Configuration Manager 管理コンソールで構成した VPN 接続を自動的に開くアプリの一覧を追加できます。 詳細については、「[Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)」 (System Center Configuration Manager の Technical Preview 1605 の機能) の「[App-triggered VPN for Windows 10 devices](/sccm/core/get-started/capabilities-in-technical-preview-1605)」 (Windows 10 デバイス用のアプリトリガー VPN) を参照してください。  

- **リモート デバイスの操作の新しいエクスペリエンス**

  Configuration Manager コンソールからリモート デバイスの操作を実行するため、エクスペリエンスが改善されました。

  [**削除/ワイプ**]、[**パスコードのリセット**]、[**リモート ロック**]、および [**アクティブ化ロックのバイパス**] などの一般的な操作は、[**資産とコンプライアンス**] ワークスペースからアクセスする [**リモート デバイスの操作**] メニューに移動しました。

  詳細については、「[Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)」 (System Center Configuration Manager の Technical Preview 1605 の機能) の「[New experience for remote device actions](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions)」 (リモート デバイスの操作の新しいエクスペリエンス) を参照してください。  

- **ビジネス向け Windows ストアのアプリ**

  [ビジネス向け Windows ストア](https://www.microsoft.com/en-us/business-store)は、組織向けのアプリを検索して、個別に、または一括で購入できる場所です。 ストアを Configuration Manager に接続すると、一括購入したアプリを Configuration Manager コンソールから管理できます。 詳細については、「[Capabilities in Technical Preview 1605 for System Center Configuration Manage](/sccm/core/get-started/capabilities-in-technical-preview-1605)」 (System Center Configuration Manager の Technical Preview 1605 の機能) の「[Windows Store for Business apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps)」 (ビジネス向け Windows ストアのアプリ) を参照してください。  

- **ボリューム購入アプリの全般的な向上**

  ビジネス向け Windows ストアおよび iOS App Store のボリューム購入アプリが同じビューの **[ストア アプリのライセンス情報]** に統合されています。 また、iOS 用ボリューム購入アプリを作成する方法が向上しています。 詳細については、「[Capabilities in Technical Preview 1605 for System Center Configuration Manage](/sccm/core/get-started/capabilities-in-technical-preview-1605)」 (System Center Configuration Manager の Technical Preview 1605 の機能) の「[General improvements for volume-purchased apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps)」 (ボリューム購入アプリの全般的な向上) を参照してください。  

- **IMEI または iOS シリアル番号を持つ会社所有のデバイスの事前宣言**

  会社が所有するデバイスの International station Mobile Equipment Identity (IMEI) 番号をインポートすることでデバイスを識別できるようになりました。 デバイスの IMEI 番号を含むコンマ区切り値 (.csv) ファイルをアップロードするか、デバイス情報を手動で入力することができます。  iOS デバイスのシリアル番号をインポートすることもできます。  詳細については、「[Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)」 (System Center Configuration Manager の Technical Preview 1605 の機能) の「[Pre-declare corporate-owned devices with IMEI or iOS serial number](../../core/get-started/capabilities-in-technical-preview-1605.md#pre-declare-corporate-owned-devices-with-with-imei-or-ios-serial-number)」 (IMEI または iOS シリアル番号を持つ会社所有のデバイスの事前宣言) を参照してください。  

- **Windows 情報保護 (WIP)**

  Windows 情報保護 (WIP) ポリシー (保護されているアプリ、WIP 保護レベル、およびネットワーク上の企業データを検索する方法を選択できるようにするなど) を展開するのに便利な構成項目を作成することができます。 WIP の詳細については、次のトピックを参照してください。  

  -   [Windows 情報保護 (WIP) を使用したエンタープライズ データの保護](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [System Center Configuration Manager を使用した Windows 情報保護 (WIP) ポリシーの作成と展開](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能  
 2016 年 5 月の Configuration Manager (現在のブランチ) では、ハイブリッド新機能は導入されていません。  

##  <a name="new-hybrid-features-in-april-2016"></a>2016 年 4 月のハイブリッド新機能  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能  
 2016 年 4 月に導入された次の Intune 機能は、ハイブリッド展開で動作します。  

- **MAM ユーザー コンプライアンス**

  Azure Active Directory (AAD) テナントのすべてのユーザーについて、アプリケーション管理ポリシーの状態を表示できるようになりました。  詳細については、Intune ライブラリの「[Microsoft Intune でのモバイル アプリ管理ポリシーの監視](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)」を参照してください。  

- **Outlook 連絡先の同期を防ぐための MAM コントロール (Android)**

  アプリケーションが Android デバイス上のネイティブのアドレス帳に連絡先を同期するのを防ぐための新しい設定を使用できます。 この新しい設定は、最初に Android デバイス上の Outlook アプリケーションでサポートされました。 詳細については、Intune ライブラリの「[Microsoft Intune でのモバイル アプリ管理ポリシーの作成および展開](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)」を参照してください。  

- **ポータル Web サイトの機能強化**

  Windows 10 Mobile および Windows Phone 8.1 のユーザーが基幹業務アプリをインストールする際に、次の新しい状態が表示されて、インストールの状態に関する詳細情報を確認できるようになりました。  

  -   **デバイスが同期するのを待っています**: ユーザーが [インストール] をタップし、デバイスが Intune インフラストラクチャと同期しようとしています。 インストールを完了するには、この同期が必要です。 「デバイスが同期するのを待っています」メッセージはリンクにもなっており、同期プロセスが時間がかかるか停止した場合にユーザーがタップすると、Intune でデバイスを手動で同期する手順を確認できます。  

  -   **ダウンロード中** – ユーザーのダウンロード要求が処理されており、デバイスがアプリをダウンロードおよびインストールしています。  

- **Android ポータル サイト アプリの機能強化**

  Intune にデバイスを登録していないユーザーと、適切な証明書がインストールされていないユーザーは、Android ポータル サイト アプリにサインインできず、メッセージ「必要な証明書がデバイスに見つからないため、サインインできません」が表示されます。 このメッセージには [How to resolve this] (この解決方法) リンクが含まれており、ユーザーがタップすると、証明書のインストール手順を確認できます。 エンドユーザーが問題を解決するために従う手順を確認するには、Intune ライブラリの「[デバイスに必要な証明書がない](/intune/enduser/using-your-android-device-with-intune)」を参照してください。  

- **iOS ポータル サイト アプリの機能強化**

  ホーム画面上のコンテンツを更新するための pull-to-refresh 操作のサポートが追加されました。これには、一覧表示されたアプリ、一覧表示されたデバイス、および IT 連絡先情報が含まれます。 pull-to-refresh 操作は、コンプライアンスまたはポリシー情報をチェックしません。このチェックを行うには、現在のデバイスのタイルを選択し、**[同期]** ボタンをタップします。  

- **Windows 10 Mobile および Windows Phone 8.1 ポータル サイト アプリの機能強化**

  エンドユーザーが基幹業務アプリをインストールする際に、強化されたアプリ インストール エクスペリエンスが得られるようになりました。 アプリのインストールに長い時間がかかる場合、そのデバイスを手動で同期して、同期プロセスを強制的に再開できます。 エンドユーザーの手順を確認するには、Intune ライブラリの「[Sync your device manually to speed up app installations](/intune/enduser/using-your-windows-device-with-intune)」 (アプリ インストールを高速化するための手動でのデバイスの同期) を参照してください。  

###  <a name="new-in-1604-technical-preview"></a>1604 Technical Preview の新機能
 2016 年 4 月に導入された次の新機能は、Intune と Configuration Manager Technical Preview 1604 のハイブリッド展開で使用できます。 これらの機能は、Configuration Manager コンソールを使用して構成および管理する必要があります。  

- **Configuration Manager コンソールから Windows 10 デバイスに対してビジネス向け Windows ストアのアプリを検索、管理、配布する**


  Configuration Manager Technical Preview 1604 では、管理している Windows 10 デバイスに対してアプリを検索、管理、配布できるように、ビジネス向け Windows ストアがサポートされています。 詳細については、「[Capabilities in Technical Preview 1604 for System Center Configuration Manage](/sccm/core/get-started/capabilities-in-technical-preview-1604)」 (System Center Configuration Manager の Technical Preview 1604 の機能) の「[Manage volume-purchased apps from the Windows Store for Business](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business)」 (ビジネス向け Windows ストアからのボリューム購入アプリの管理) を参照してください。  

- **Android デバイスの SmartLock 設定**

  新しい設定が Android および Samsung KNOX 構成項目に追加され、互換性のある Android デバイスで SmartLock 機能を制御することができます。  この設定を使用して、エンドユーザーが SmartLock を構成することを禁止できます。 詳細については、「[Capabilities in Technical Preview 1604 for System Center Configuration Manage](/sccm/core/get-started/capabilities-in-technical-preview-1604.md)」 (System Center Configuration Manager の Technical Preview 1604 の機能) の「[SmartLock setting for Android devices](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices)」 (Android デバイスの SmartLock 設定) を参照してください。  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能  
 2016 年 4 月の Configuration Manager (現在のブランチ) では、ハイブリッド新機能は導入されませんでした。  

##  <a name="new-hybrid-features-in-march-2016"></a>2016 年 3 月のハイブリッド新機能  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能  
 2016 年 3 月に導入された次の Intune 機能は、ハイブリッド展開で動作します。  

- **Outlook 連絡先の同期を防ぐための MAM コントロール (iOS)**

  アプリケーションが iOS デバイス上のネイティブのアドレス帳に連絡先を同期するのを防ぐための新しい設定を使用できます。 この新しい設定は、iOS デバイス上の Outlook アプリケーションでサポートされています。 この設定およびその他の設定の詳細については、Intune ライブラリの「[Create and deploy MAM policies](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)」 (MAM ポリシーの作成および展開) を参照してください。  

- **Skype for Business Online による条件付きアクセスのサポート**

  Skype for Business Online が管理対象の準拠 iOS および Android デバイスからのみアクセスできるように、条件付きアクセス ポリシーを設定することができます。  詳細については、Intune ライブラリの「[Skype for Business Online のアクセスの管理](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune)」を参照してください。  

- **iOS 9.3 サポート**

  3 月 21 日月曜日、Apple は iOS 9.3 が利用できるようになったことを発表しました。 iOS デバイスの管理に現在使用できるすべての既存の Intune 機能は、ユーザーがデバイスを iOS 9.3 にアップグレードしたときにシームレスに動作し続けます。  

- **ポータル Web サイトから直接使用可能な Windows アプリ パッケージ**

  Windows 8、Windows 8.1 および Windows RT PC のユーザーは、ポータル Web サイトから Windows アプリ パッケージ (.appx 拡張子) を直接インストールできるようになりました。 以前は、アプリをインストールするには、管理者が展開するか、またはユーザーがデバイスにポータル サイト アプリをインストールする必要がありました。  

- **ユーザーがポータル Web サイトからデバイスをリモートでロックできる**

  ポータル Web サイトに新しいリモート ロック オプションが追加されており、ユーザーはデバイスを紛失したり盗難にあったりした場合に、ポータルからデバイスをリモートでロックできます。  

- **サードパーティの MDM ソリューションに登録されているデバイスに対して iOS の "オープンイン" 管理を利用する**

  サードパーティのモバイル デバイス管理 (MDM) ベンダーを使用して、iOS の "オープンイン" 管理を利用できます。 構成プロファイル設定で制限を設定し、MDM ソフトウェアを使用してアプリを展開できます。 ユーザーが管理対象アプリをインストールすると、制限が適用されます。 Intune ライブラリの「[Microsoft Intune mobile app management policies and iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune)」 (Microsoft Intune モバイル アプリ管理ポリシーと iOS の Open In) を参照してください。  

- **MAM をサポートする Microsoft アプリ**

  Intune モバイル アプリケーション管理ポリシーで使用できる Microsoft アプリの一覧が、最新のアプリを含めるように更新されました (Intune に登録されているデバイスに対してのみ)。  

- **Microsoft Intune 用の Adobe Reader を社内の Intune 管理 iOS デバイスに展開する**

  Intune モバイル アプリケーション管理ポリシーを使用して、登録デバイスで iOS 用 Adobe Reader アプリを管理できるようになりました。  

- Android での Rights Management 共有アプリのサポート

  IT がデバイスの管理に Intune を使用するかどうかにかかわらず、IT 管理者は、エンドユーザーがイメージ、AV、および PDF ファイルをより安全に表示できるようにモバイル アプリケーション管理ポリシーを展開できます。  

- **Android および iOS のポータル サイト アプリの機能強化**

  -   モバイル アプリケーション管理 (MAM) によって管理されているアプリをユーザーが起動すると、アプリが会社によって管理されていることを通知するメッセージが表示されます。 ユーザーは [詳細情報] リンクをタップして、"管理対象アプリ" に関する詳細情報を確認できるようになりました。 また、[次回から表示しない] をタップすると、アプリの起動時にこのメッセージが表示されないようにできます。  

  -   ユーザーに登録プロセスを順に案内し、ユーザーが登録しなければならない理由の詳細、および IT 管理者が登録デバイスで確認できる内容と確認できない内容の詳細を示すために、新しい画面が追加されました。  

  -   登録エラー メッセージが、ポータル サイト アプリに表示されるようになりました。  

### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview の新機能  
 2016 年 3 月の Configuration Manager Technical Preview では、ハイブリッド新機能は導入されませんでした。  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能  
 2016 年 3 月に導入された次の新機能は、Intune と Configuration Manager (現在のブランチ) バージョン 1602 のハイブリッド展開で使用できます。 これらの機能は、Configuration Manager コンソールを使用して構成および管理する必要があります。  

- **iOS アプリ構成ポリシー**

  Configuration Manager (現在のブランチ) バージョン 1602 では、ユーザーが iOS アプリを実行するときに必要となる可能性がある設定をアプリ構成ポリシーで指定できます。 詳細については、「[Configure iOS apps with app configuration policies in System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies)」 (System Center Configuration Manager でのアプリ構成ポリシーを使用した iOS アプリの構成) を参照してください。  

- **ボリューム購入 iOS アプリの管理**

  Configuration Manager (現在のブランチ) バージョン 1602 では、Apple Volume-Purchase Program (VPP) からボリューム購入したアプリを展開して管理できます。そのために、アプリ ストアからライセンス情報をインポートして、使用したライセンスの数を追跡します。 詳細については、「[Manage volume-purchased iOS apps with System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps)」 (System Center Configuration Manager でのボリューム購入 iOS アプリの管理) を参照してください。  

- **Office モバイル アプリの自動作成**

  Configuration Manager (現在のブランチ) バージョン 1602 以降では、バージョン 1511 からアップグレードすると、Android および iOS 用の次の Microsoft Office モバイル アプリが作成されます。  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (iOS のみ)  
  -   Microsoft Outlook  

  これらのアプリは Configuration Manager コンソールの [アプリケーション] ノードに表示されます。 アプリケーションの展開の詳細については、「[System Center Configuration Manager でアプリケーションを展開する方法](../../apps/deploy-use/deploy-applications.md)」を参照してください。  

- **Android Samsung KNOX デバイスのキオスク モードの設定**

  キオスク モードでは、特定の機能のみ実行できるようにデバイスをロックできます。  Configuration Manager (現在のブランチ) バージョン 1602 以降では、Samsung KNOX デバイスのキオスク モードの設定を指定できるようになりました。 詳細については、「[System Center Configuration Manager クライアントを使用せずに管理されている Android デバイスと Samsung KNOX デバイスの構成項目を作成する方法](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)」を参照してください。  

- **iOS のアクティベーション ロック**

  Configuration Manager (現在のブランチ) バージョン 1602 以降では、iOS 7.1 以降用の「iPhone を探す」アプリの機能である、iOS のアクティベーション ロックを管理できます。 iPhone を探すアプリをデバイスで使用すると、アクティブ化ロックが自動的に有効になります。  詳細については、「[Manage iOS Activation Lock bypass for System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock)」 (System Center Configuration Manager での iOS のアクティベーション ロック バイパスの管理) を参照してください。  



<!--HONumber=Nov16_HO1-->


