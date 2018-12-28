---
title: ハイブリッド MDM の新機能のアーカイブ
titleSuffix: Configuration Manager
description: System Center Configuration Manager と Intune のハイブリッド展開で使用できる過去のモバイル デバイス管理機能のアーカイブです。
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 172ca284a5a030682e01d9be63031180d7175421
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423203"
---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune での過去のハイブリッド機能

*適用対象します。System Center Configuration Manager (Current Branch)*

この記事では、System Center Configuration Manager と Intune のハイブリッド展開で使用できる過去のモバイル デバイス管理 (MDM) 機能の詳細について説明します。  

##  <a name="compatibility-with-configuration-manager-versions"></a>Configuration Manager のバージョンとの互換性  

 この記事の各セクションでは、3 つの異なるカテゴリにあるハイブリッド機能を一覧表示します。 次のガイダンスを使用すると、各カテゴリの機能とさまざまなバージョンの Configuration Manager との互換性を判断できます。  

|機能のカテゴリ|
|-|  
|**Microsoft Intune の新機能** - 通常、このカテゴリに一覧表示されたすべての機能は、System Center 2012 R2 Configuration Manager リリースを含むすべての Configuration Manager のリリースで動作します。これらの機能は Intune サービスのみを必要とし、Configuration Manager の追加機能は必要ないためです。<br /><br /> **Configuration Manager Technical Preview の新機能** - このカテゴリに一覧表示されたすべての機能は、指定されたバージョンの Technical Preview リリースでのみ動作します。 これらの機能を試すには、機能の説明で指定されたバージョンの Technical Preview をインストールする必要があります。 詳細については、「[System Center Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を参照してください。<br /><br /> **Configuration Manager (現在のブランチ) の新機能** - このカテゴリに一覧表示されたすべての機能は、バージョン 1511 や 1602 など、指定されたバージョンの Configuration Manager (現在のブランチ) でのみ動作します。 ハイブリッド展開に旧バージョンの Configuration Manager を使用している場合は、機能の説明で指定されたバージョンの Configuration Manager (現在の分岐) にアップグレードする必要があります。 詳細については、「[System Center Configuration Manager へのアップグレード](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)」を参照してください。|  



## <a name="april-2017"></a>2017 年 4 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **管理対象ブラウザーで利用できる MyApps**  
  Microsoft MyApps では、管理対象ブラウザー内のサポートが改善されました。 管理対象ではない管理対象ブラウザーのユーザーは MyApps サービスに直接移動します。そこで管理者によってプロビジョニングされた自分の SaaS アプリにアクセスできます。 Intune 管理の対象になっているユーザーは、組み込まれている管理対象ブラウザーのブックマークから MyApps に引き続きアクセスできます。

- **管理対象ブラウザーとポータル サイトの新しいアイコン**  
  管理対象ブラウザーは、Android 版アプリと iOS 版アプリの両方で更新されたアイコンを受け取ります。 新しいアイコンには更新された Intune バッジが含まれ、Enterprise Mobility + Security (EM+S) の他のアプリとの一貫性が向上します。 管理対象ブラウザーの新しいアイコンは、[Intune アプリ UI の新機能に関するページ](https://docs.microsoft.com/intune/whats-new-app-ui)で確認できます。

  ポータル サイトは、Android 版アプリ、iOS 版アプリ、Windows 版アプリの更新されたアイコンを受け取り、EM+S の他のアプリとの一貫性を向上させます。 アイコンは 4 月から 5 月後半にかけてすべてのプラットフォームに徐々に提供されます。

- **Android ポータル サイトのサインイン進捗状況インジケーター**  
  Android ポータル サイト アプリの更新プログラムには、ユーザーがアプリを起動または再開したとき、サインイン進捗状況インジケーターが表示されます。 このインジケーターには新しい状態が次々と表示されます。"接続しています..." から始まり、"サインインしています..." に進み、さらに "セキュリティ要件を確認しています..." に進み、その後、ユーザーはアプリにアクセスできます。 Android のポータル サイト アプリの新しい画面は [Intune アプリ UI の新機能に関するページ](https://docs.microsoft.com/intune/whats-new-app-ui)で確認できます。

- **アプリが SharePoint Online にアクセスすることを禁止する**  
  アプリ基準の条件付きアクセス ポリシーを作成し、アプリ保護ポリシーが適用されていないアプリが [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online) にアクセスすることを禁止できるようになりました。 アプリ基準の条件付きアクセス シナリオでは、Azure ポータルを利用して SharePoint Online へのアクセスを与えるアプリを指定できます。

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Configuration Manager Technical Preview 1704 の新機能

- **アプリ構成ポリシーを使用した Android アプリの構成**  
  Android for Work デバイスでアプリを実行するとき、ユーザーは Configuration Manager のアプリ構成ポリシーを使って、事前に構成された設定を配布します。 Android アプリ構成ポリシーは、Android for Work を実行しているデバイス上でのみ使用できます。 これらのポリシーは、Play for Work ストアから承認されたアプリに適用されます。 詳しくは、「[アプリ構成ポリシーを使用した Android アプリの構成](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies)」をご覧ください。



## <a name="march-2017"></a>2017 年 3 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **Android 用ポータル サイト アプリに関する新しいユーザー エクスペリエンス**  
  Android のポータル サイト アプリのユーザー インターフェイスが変わり、より現代的な外観になりました。 注目の新機能:

  - 色:会社ポータルのタブ ヘッダーの色が IT によるブランド化します。
  - アプリ:**アプリ** タブで、**おすすめアプリ**と**すべてのアプリ**ボタンが更新されました。
  - 検索:**アプリ** タブで、**検索**ボタンは浮動アクション ボタン。
  - アプリを移動するには。**すべてのアプリ**のタブ付きビューを表示します。**おすすめ**、**すべて**、および**カテゴリ**簡単に移動します。
  - サポート:**デバイス**と**IT に連絡**タブは、読みやすさを向上させるために更新されます。

  以上の変更に関する詳細については、「[Intune とエンド ユーザー アプリの UI の更新](https://docs.microsoft.com/intune/whats-new-app-ui)」を参照してください。

- **Windows 10 ポータル サイトの署名スクリプト**  
  Windows 10 ポータル サイト アプリをダウンロードし、サイドロードする必要がある場合に、スクリプトを利用し、組織のアプリ署名プロセスを簡素化および合理化できるようになりました。 スクリプトとその使用方法に関する手順をダウンロードする方法については、TechNet ギャラリーの「[Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript)」 (Windows 10 ポータル サイトの Microsoft Intune の署名スクリプト) を参照してください。 この告知の詳細については、Intune サポート チーム ブログの「[Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/)」 (Windows 10 ポータル サイト アプリを更新する) を参照してください。

- **中国の Android ユーザー向けサポートを強化**  
  中国には Google Play ストアがないため、Android デバイスでは中国のマーケットプレースからアプリを入手する必要があります。 ポータル サイトはこのワークフローをサポートします。 中国の Android ユーザーをリダイレクトし、現地のアプリ ストアからポータル サイト アプリや Outlook アプリをダウンロードできるようにします。 これにより、モバイル デバイス管理とモバイル アプリケーション管理の両方で、条件付きアクセス ポリシーを有効にしたときのユーザー エクスペリエンスが向上します。 Android 向けのポータル サイト アプリまたは Outlook アプリは中国の次のアプリ ストアで入手できます。

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **ポータル サイト アプリを最新の状態に維持**  
  2016 年 12 月に公開した更新プログラムでは、iOS、Android、Windows 8.1 以降、Windows Phone 8.1 以降のデバイスを登録するときに、ユーザーのグループに対する多要素認証 (MFA) の強制を有効にできるようになりました。 この機能は、Android (v5.0.3419.0 以降) 向けまたは iOS (v2.1.17 以降) 向けのポータル サイト アプリの特定のベースライン バージョンがないと動作しません。

  Intune の管理機能は継続的に改善されています。 その多くが、サポートされているすべてのプラットフォームのポータル サイト アプリに合わせて、更新プログラムが調整されています。 デバイスにインストールされているポータル サイト アプリを常に最新バージョンにしておくことをお勧めします。 そうすることで、機能強化された Intune を活用し、最高のユーザー エクスペリエンスを得られます。

  >[!Tip]
  > アプリ ストアからアプリを自動的に更新するようにデバイスを設定するよう、ユーザーに連絡してください。 Android 向けポータル サイト アプリをネットワーク共有で利用できるようにしている場合、[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=49140)から最新版をダウンロードできます。

- **iOS および Android の MAM での Microsoft Teams の有効化**  
  iOS と Android 向けの Microsoft Teams アプリが、Intune モバイル アプリ管理 (MAM) 機能で有効になりました。 会話や会社のデータは常に保護された状態で、デバイスを問わず、自由に働く能力をチームに与えることができるようになりました。 詳しくは、Enterprise Mobility and Security ブログの「[Microsoft Teams announcement](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/)」(Microsoft Teams からの告知) をご覧ください。

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Configuration Manager Technical Preview 1703 の新機能

- **Apple Volume Purchase Program シナリオのサポートの追加**  
   テクニカル プレビュー 1703 以降、次のボリューム購入プログラム (VPP) シナリオがサポートされています。

   - デバイスのライセンス - デバイスのライセンスをサポートし、デバイス コレクションに展開されるアプリで必要なライセンスは、デバイスごとに 1 つのみになりました。 以前は、デバイスのユーザーごとにライセンスを使用する必要がありました。 詳細については、「[ボリューム購入した iOS アプリをデバイス コレクションに展開する](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections)」を参照してください。
   - 1 つのハイブリッド テナントに対する複数の VPP トークンの使用。両方のトークンは VPP アプリを管理するために使用されます。
   - VPP 教育用トークンの使用。ビジネス用トークンと教育用トークンを区別できます。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能

以下の機能は以前、Configuration Manager Technical Preview リリースで利用できました。 現在は、Intune と Configuration Manager (Current Branch) バージョン 1702 のハイブリッド展開で使用できます。

- [Android for Work のサポート](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [非準拠アプリのコンプライアンス設定](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [PFX 証明書の作成と配布および S/MIME のサポート](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [ハイブリッド MDM の作成ウィザードで Android と iOS のバージョン指定が不要に](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

次の追加のハイブリッド機能も、Configuration Manager (Current Branch) のバージョン 1702 に含まれます。

- **Apple Volume Purchase Program (VPP) のサポートの向上**  
  - ライセンスされたアプリをユーザーだけでなくデバイスにも展開できるようになりました。 デバイス ライセンスをサポートするアプリ機能に応じて、次のように、展開時に適切なライセンスが要求されます。

    | Configuration Manager バージョン | アプリでのデバイス ライセンスのサポート | 展開コレクションの種類 | 要求されるライセンス |
    |-|-|-|-|
    |1702 より前|はい|ユーザー|ユーザー ライセンス|
    |1702 より前|いいえ|ユーザー|ユーザー ライセンス|
    |1702 より前|はい|デバイス|ユーザー ライセンス|
    |1702 より前|いいえ|デバイス|ユーザー ライセンス|
    |1702 以降|はい|ユーザー|ユーザー ライセンス|
    |1702 以降|いいえ|ユーザー|ユーザー ライセンス|
    |1702 以降|はい|デバイス|デバイス ライセンス|
    |1702 以降|いいえ|デバイス|ユーザー ライセンス|

  - iOS Volume Purchase Program for Education から購入したアプリを展開し追跡できるようになりました。

  - 複数の Apple Volume Purchase Program トークンを Configuration Manager に関連付けることができるようになりました。

  ボリューム購入した iOS アプリの詳細については、[「ボリューム購入 iOS アプリの管理」](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps) を参照してください。

- **ビジネス向け Microsoft Store での基幹業務アプリのサポート**  
  ビジネス向け Microsoft Store から、カスタマイズされた基幹業務アプリを同期できるようになりました。

- **新しい Mobile Threat Defense 監視ツール**  
    Mobile Threat Defense サービス プロバイダーでコンプライアンス状態を監視する新しい方法を利用できるようになりました。

    詳細については、[「Mobile Threat Defense コンプライアンスの監視」](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance) を参照してください。





## <a name="february-2017"></a>2017 年 2 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **ポータル Web サイトのモダナイズ**

  ポータル Web サイトでは、マネージド デバイスを持っていないユーザーを対象とするアプリがサポートされます。 Web サイトは、新しい濃い色の配色、動的な図、ヘルプデスクの連絡先詳細や既存のマネージド デバイスに関する情報を含む "ハンバーガー メニュー" を使用して、他の Microsoft 製品やサービスに合わせられます。 ランディング ページは、おすすめアプリや最近更新されたアプリのカルーセルを使用して、ユーザーが利用できるアプリを強調するために再配置されます。 [[UI の更新]](https://docs.microsoft.com/intune/whats-new-app-ui) ページでは、更新前と後のイメージを利用できます。

- **Windows デバイス用の新しい MDM サーバー アドレス**

  Windows および Windows Phone デバイスを登録するための MDM サーバー アドレスは、manage.microsoft.com から enrollment.manage.microsoft.com に変更されました。 Windows または Windows Phone デバイスを登録するときに求められた場合は、MDM サーバー アドレスとして enrollment.manage.microsoft.com を使用するようユーザーに通知してください。 この更新では、EnterpriseEnrollment.contoso.com を manage.microsoft.com にリダイレクトする DNS 内の CNAME を、EnterpriseEnrollment.contoso.com to EnterpriseEnrollment-s.manage.microsoft.com にリダイレクトする DNS 内の CNAME に置き換える必要もあります。 この変更の詳細については、 http://aka.ms/intuneenrollsvrchange を参照してください。

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Configuration Manager Technical Preview 1702 の新機能

- **Android for Work のサポート**

  Configuration Manager Technical Preview 1702 を使用するハイブリッド MDM 環境で、Android for Work を使用して Android デバイスを管理できるようになりました。 サポートされている Android デバイスを、Android for Work デバイスとして登録できます。これによりデバイス上に作業プロファイルが作成され、Play for Work で承認されたアプリをそこに展開できます。 これらのデバイスの構成項目、コンプライアンス ポリシー、およびリソース アクセス プロファイルを展開することもできます。 詳細については、[「Android for Work のサポート」](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support) を参照してください。

- **非準拠アプリのコンプライアンス設定**

  コンプライアンス ポリシーで、Android および iOS のアプリの非準拠アプリの規則を作成できるようになりました。 指定されたアプリケーションがデバイスにインストールされている場合、そのアプリケーションは "非準拠" としてマークされ、適用される条件付きアクセス ポリシーに従い、会社のリソースにアクセスできなくなります。 詳細については、「[条件付きアクセス デバイス コンプライアンス ポリシーの改善](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements)」をご覧ください。

- **PFX 証明書の作成と配布および S/MIME のサポート**

  PFX 証明書を作成してハイブリッド環境のユーザーに展開できるようになりました。 これらの証明書は、ユーザーが登録したデバイスで S/MIME メールの暗号化と復号化に使用できます。 詳細については、[「S/MIME サポートを含む PFX 証明書を作成する」](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support) を参照してください。

- **追加の iOS 構成設定のサポート**
   
    構成項目の一部として、構成できる 42 個の iOS 設定が追加されました。 これらの設定の大部分 (35 個) は、監視対象の iOS デバイスに対して追加されました。 詳細については、[「iOS デバイスの新しいコンプライアンス設定」](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices) を参照してください。



## <a name="january-2017"></a>2017 年 1 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **Android 7.1.1 のサポート**

  Intune では、Android 7.1.1 を完全にサポートし管理できるようになりました。

- **iOS デバイスがアクティブでないか、管理コンソールと通信できない問題を解決する**

  ユーザーのデバイスと Intune との接続が切れた場合、会社のリソースへ再度アクセスできるように、新しいトラブルシューティングの手順を指定できます。 「[Devices are inactive, or the admin console cannot communicate with them](https://docs.microsoft.com/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them)」 (デバイスがアクティブでないか、管理コンソールと通信できない) を参照してください。

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Configuration Manager Technical Preview 1701 の新機能

- **ハイブリッド MDM の作成ウィザードで Android と iOS のバージョン指定が不要に**

  ハイブリッド モバイル デバイス管理 (MDM) の Technical Preview 1701 から、Intune で管理されるデバイスの新しいポリシーとプロファイルを作成する場合に Android および iOS の特定のバージョンを指定する必要がなくなりました。 この変更により、新しい Configuration Manager のリリースまたは拡張機能を必要とせずに、ハイブリッド展開で新しい Android および iOS のバージョンによりすばやくサポートを提供できます。 詳細については、「[作成ウィザードで Android と iOS のバージョン指定が不要に](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)」を参照してください。



## <a name="december-2016"></a>2016 年 12 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **登録での Multi-Factor Authentication (MFA) が Azure Portal に移動する**

  これまで、Intune の登録に MFA を設定するには、Intune コンソールまたは構成マネージャー コンソールを使用していました。 この更新された機能、今すぐにログインしている、 [Microsoft Azure ポータル](https://manage.windowsazure.com)Intune の資格情報を使用して、Azure AD MFA の設定を構成します。 詳細については、[Microsoft Intune への多要素認証](https://aka.ms/mfa_ad)に関する記事を参照してください。

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


## <a name="november-2016"></a>2016 年 11 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **新しい Microsoft Intune ポータル サイトが Windows 10 デバイスで利用可能になる**

  Microsoft は、新しい [Windows 10 デバイス用のポータル サイト アプリ](https://www.microsoft.com/store/apps/9wzdncrfj3pz)をリリースしました。 このアプリでは新しい Windows 10 ユニバーサル形式を利用し、PC やモバイルなどすべての Windows 10 デバイスで同じ更新されたユーザー エクスペリエンスが提供されますが、以前のポータル サイトアプリで提供されている同じ機能はすべて引き続き利用できます。

  この新しいアプリでは、Windows 10 デバイスでのシングル サインオン (SSO) や証明書ベースの認証など、プラットフォーム機能も利用します。 アプリは、既存の Windows 8.1 ポータル サイトおよび Windows Phone 8.1 ポータル サイトのインストールのアップグレードとして Windows ストアから入手できるようになります。 詳細については、[Intune サポート チームのブログ](http://aka.ms/intunecp_universalapp)を参照してください。

  新しいポータル サイト アプリでは、Configuration Manager コンソールで**使用可能**とマークされたビジネス アプリケーションの Windows ストアも表示されます。


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能

Configuration Manager Technical Preview リリースで以前に提供されていた次の機能は、Intune と Configuration Manager (Current Branch) バージョン 1610 のハイブリッド展開で使用できるようになりました。

* [構成項目の追加設定とエクスペリエンス向上](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [DEP プロファイルの追加設定](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [ビジネス向け Windows ストアの有料アプリ](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Windows 10 VPN プロファイルのネイティブ接続の種類](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
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

## <a name="october-2016"></a>2016 年 10 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

2016 年 10 月に導入された次の Intune 機能は、ハイブリッド展開で動作します。

- **モバイル アプリケーション管理の条件付きアクセス**

  Outlook など、Intune モバイル アプリケーション管理ポリシーをサポートするアプリからのアクセスのみを許可するように、Exchange Online へのアクセスを制限することができます。 [この新機能](/intune/deploy-use/allow-policy-managed-apps-access-to-o365)は、組み込みのメール クライアントや Intune MAM ポリシーが構成されていない他のアプリへのアクセスをブロックできるため、Intune のモバイル アプリ管理 (MAM) ポリシーと組み合わせると効果的です。 これにより、ユーザーが組織のデータにアクセスする際に、Intune MAM を使用して保護できるアプリを使用するようになります。 Intune モバイル アプリ管理は、Azure Portal から使用することができます。 [設定] ブレードの新しい [条件付きアクセス] セクションを探してください。

- **Android 用 Intune アプリ ラッピング ツール**

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

## <a name="september-2016"></a>2016 年 9 月

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

## <a name="august-2016"></a>2016 年 8 月

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

## <a name="july-2016"></a>2016 年 7 月

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

* Configuration Manager コンソールから Windows 10 デバイスに対してビジネス向け Windows ストアのアプリを検索、管理、配布する ([1604](#new-in-1604-technical-preview))
*   Android デバイス用の SmartLock 設定 ([1604](#new-in-1604-technical-preview))
*   Windows 10 デバイス用のアプリトリガー VPN ([1605](#new-in-1605-technical-preview))
*   リモート デバイスの操作の新しいエクスペリエンス ([1605](#new-in-1605-technical-preview))
*   ビジネス向け Windows ストアのアプリ ([1605](#new-in-1605-technical-preview))
*   ボリューム購入アプリの全般的な向上 ([1605](#new-in-1605-technical-preview))
*   Windows 情報保護 (WIP) ([1605](#new-in-1605-technical-preview))
*   IMEI または iOS シリアル番号を持つ会社所有のデバイスの事前宣言 ([1605](#new-in-1605-technical-preview))
*   デバイスを自動的にコレクションごとに分類 ([1606](#new-in-1606-technical-preview))

新機能については、特定の Technical Preview リリースに関するドキュメントを参照してください。

## <a name="june-2016"></a>2016 年 6 月

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

  Intune と Configuration Manager を使用している場合に、デバイス コレクションにデバイスを自動的に配置するために使用できる、デバイス カテゴリを作成することができます。 ユーザーは Intune にデバイスを登録するときに、デバイス カテゴリの選択を求められます。 Configuration Manager コンソールから、デバイスのカテゴリをさらに変更できます。 詳細については、「[Capabilities in Technical Preview 1606 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606)」 (System Center Configuration Manager の Technical Preview 1606 の機能) の「[Automatically categorize devices into collections](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category)」 (デバイスを自動的にコレクションごとに分類) を参照してください。

  > [!IMPORTANT]
  > この機能は、Microsoft Intune の 2016 年 6 月のリリースで動作します。 これらの手順を実行する前に、今回のリリースに更新していることを確認してください。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能
2016 年 6 月の Configuration Manager (現在のブランチ) では、ハイブリッド新機能は導入されていません。

##  <a name="may-2016"></a>2016 年 5 月  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能  
 2016 年 5 月に導入された次の Intune 機能は、ハイブリッド展開で動作します。

- **MAM SDK:PIN の長さの構成をサポート**

  デバイス PIN のように MAM アプリに対して PIN の長さを指定できるようになりました。 その際には、設定した新しい制限にエンドユーザーが準拠する必要があります。 より長いアカウントの入力に対応するために、PIN 画面が若干変更されています。 詳細については、「[MAM policy settings for Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings)」 (Android 用の MAM ポリシー設定) および 「[MAM policy settings for iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings)」 (iOS 用の MAM ポリシー設定) を参照してください。  

- **Android および iOS 用の Skype for Business**

  [登録ポリシーのない MAM](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune) で Skype for Business を対象にできるようになりました。 ユーザーがログインすると、MAM ポリシーが適用されます。  

- **MAM ポリシーによる管理に使用できる新しいアプリ**

  Intune に登録されていないデバイスで、Android 用の Microsoft Word、Excel、および PowerPoint の各アプリを MAM ポリシーに関連付けできるようになりました。 サポートされているすべてのアプリの一覧については、[Microsoft Intune アプリケーション パートナー](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx) ページの Microsoft Intune モバイル アプリケーション ギャラリーを参照してください。  

- **Android ポータル サイト アプリ:エンドユーザー トースト通知**

  エンドユーザーがポータル サイトで自分のデバイスを登録または削除すると、Android ポータル サイト アプリからトースト通知が表示されます。  

- **会社のポータル web サイト:デバイス id バナーはエンドユーザーに詳細を提供します。**

  エンドユーザーは、ポータル Web サイトを使用しているときに、選択したデバイスをより簡単に識別できるようになりました。 不正なデバイスが選択されている場合は、ホーム ページ バナーの **[Tap here]** (ここをタップ) リンクをタップして、適切なデバイスを選択できます。  


### <a name="new-in-1605-technical-preview"></a>1605 Technical Preview の新機能  
 2016 年 5 月に導入された次の新機能は、Intune と Configuration Manager Technical Preview 1605 のハイブリッド展開で使用できます。 これらの機能は、Configuration Manager コンソールを使用して構成および管理する必要があります。  

- **Windows 10 デバイス用のアプリトリガー VPN**

  Configuration Manager と Intune を使用して管理されている Windows 10 デバイスの場合、Configuration Manager 管理コンソールで構成した VPN 接続を自動的に開くアプリの一覧を追加できます。 詳細については、「[Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)」 (System Center Configuration Manager の Technical Preview 1605 の機能) の「[App-triggered VPN for Windows 10 devices](/sccm/core/get-started/capabilities-in-technical-preview-1605)」 (Windows 10 デバイス用のアプリトリガー VPN) を参照してください。  

- **リモート デバイスの操作の新しいエクスペリエンス**

  Configuration Manager コンソールからリモート デバイスの操作を実行するため、エクスペリエンスが改善されました。

  **[削除/ワイプ]**、**[パスコードのリセット]**、**[リモート ロック]**、および **[アクティブ化ロックのバイパス]** などの一般的な操作は、**[資産とコンプライアンス]** ワークスペースからアクセスする **[リモート デバイスの操作]** メニューに移動しました。

  詳細については、「[Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)」 (System Center Configuration Manager の Technical Preview 1605 の機能) の「[New experience for remote device actions](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions)」 (リモート デバイスの操作の新しいエクスペリエンス) を参照してください。  

- **ビジネス向け Windows ストアのアプリ**

  [ビジネス向け Windows ストア](https://www.microsoft.com/en-us/business-store)は、組織向けのアプリを検索して、個別に、または一括で購入できる場所です。 ストアを Configuration Manager に接続すると、一括購入したアプリを Configuration Manager コンソールから管理できます。 詳細については、「[Capabilities in Technical Preview 1605 for System Center Configuration Manage](/sccm/core/get-started/capabilities-in-technical-preview-1605)」 (System Center Configuration Manager の Technical Preview 1605 の機能) の「[Windows Store for Business apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps)」 (ビジネス向け Windows ストアのアプリ) を参照してください。  

- **ボリューム購入アプリの全般的な向上**

  ビジネス向け Windows ストアおよび iOS App Store のボリューム購入アプリが同じビューの **[ストア アプリのライセンス情報]** に統合されています。 また、iOS 用ボリューム購入アプリを作成する方法が向上しています。 詳細については、「[Capabilities in Technical Preview 1605 for System Center Configuration Manage](/sccm/core/get-started/capabilities-in-technical-preview-1605)」 (System Center Configuration Manager の Technical Preview 1605 の機能) の「[General improvements for volume-purchased apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps)」 (ボリューム購入アプリの全般的な向上) を参照してください。  

- **IMEI または iOS シリアル番号を持つ会社所有のデバイスの事前宣言**

  会社が所有するデバイスの International station Mobile Equipment Identity (IMEI) 番号をインポートすることでデバイスを識別できるようになりました。 デバイスの IMEI 番号を含むコンマ区切り値 (.csv) ファイルをアップロードするか、デバイス情報を手動で入力することができます。  iOS デバイスのシリアル番号をインポートすることもできます。  詳細については、「[Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)」 (System Center Configuration Manager の Technical Preview 1605 の機能) の「[Pre-declare corporate-owned devices with IMEI or iOS serial number](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI)」 (IMEI または iOS シリアル番号を持つ会社所有のデバイスの事前宣言) を参照してください。  

- **Windows 情報保護 (WIP)**

  Windows 情報保護 (WIP) ポリシー (保護されているアプリ、WIP 保護レベル、およびネットワーク上の企業データを検索する方法を選択できるようにするなど) を展開するのに便利な構成項目を作成することができます。 WIP の詳細については、次のトピックを参照してください。  

  -   [Windows 情報保護 (WIP) を使用したエンタープライズ データの保護](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [System Center Configuration Manager を使用した Windows 情報保護 (WIP) ポリシーの作成と展開](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能  
 2016 年 5 月の Configuration Manager (現在のブランチ) では、ハイブリッド新機能は導入されていません。  

##  <a name="april-2016"></a>2016 年 4 月  

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

  Intune にデバイスを登録していないユーザーと、適切な証明書がインストールされていないユーザーは、Android ポータル サイト アプリにサインインできず、メッセージ「必要な証明書がデバイスに見つからないため、サインインできません」が表示されます。 このメッセージには 「How to resolve this」 (この解決方法) リンクが含まれており、ユーザーがタップすると、証明書のインストール手順を確認できます。 エンドユーザーが問題を解決するために従う手順を確認するには、Intune ライブラリの「[デバイスに必要な証明書がない](/intune/enduser/using-your-android-device-with-intune)」を参照してください。  

- **iOS ポータル サイト アプリの機能強化**

  ホーム画面上のコンテンツを更新するための pull-to-refresh 操作のサポートが追加されました。これには、一覧表示されたアプリ、一覧表示されたデバイス、および IT 連絡先情報が含まれます。 pull-to-refresh 操作は、コンプライアンスまたはポリシー情報をチェックしません。このチェックを行うには、現在のデバイスのタイルを選択し、**[同期]** ボタンをタップします。  

- **Windows 10 Mobile および Windows Phone 8.1 ポータル サイト アプリの機能強化**

  エンドユーザーが基幹業務アプリをインストールする際に、強化されたアプリ インストール エクスペリエンスが得られるようになりました。 アプリのインストールに長い時間がかかる場合、そのデバイスを手動で同期して、同期プロセスを強制的に再開できます。 エンドユーザーの手順を確認するには、Intune ライブラリの「[Sync your device manually to speed up app installations](/intune/enduser/using-your-windows-device-with-intune)」 (アプリ インストールを高速化するための手動でのデバイスの同期) を参照してください。  

###  <a name="new-in-1604-technical-preview"></a>1604 Technical Preview の新機能
 2016 年 4 月に導入された次の新機能は、Intune と Configuration Manager Technical Preview 1604 のハイブリッド展開で使用できます。 これらの機能は、Configuration Manager コンソールを使用して構成および管理する必要があります。  

- **Configuration Manager コンソールから Windows 10 デバイスに対してビジネス向け Windows ストアのアプリを検索、管理、配布する**


  Configuration Manager Technical Preview 1604 では、管理している Windows 10 デバイスに対してアプリを検索、管理、配布できるように、ビジネス向け Windows ストアがサポートされています。 詳細については、「[Capabilities in Technical Preview 1604 for System Center Configuration Manage](/sccm/core/get-started/capabilities-in-technical-preview-1604)」 (System Center Configuration Manager の Technical Preview 1604 の機能) の「[Manage volume-purchased apps from the Windows Store for Business](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business)」 (ビジネス向け Windows ストアからのボリューム購入アプリの管理) を参照してください。  

- **Android デバイスの SmartLock 設定**

  新しい設定が Android および Samsung KNOX Standard 構成項目に追加され、互換性のある Android デバイスで SmartLock 機能を制御することができます。  この設定を使用して、エンドユーザーが SmartLock を構成することを禁止できます。 詳細については、「[Capabilities in Technical Preview 1604 for System Center Configuration Manage](/sccm/core/get-started/capabilities-in-technical-preview-1604.md)」 (System Center Configuration Manager の Technical Preview 1604 の機能) の「[SmartLock setting for Android devices](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices)」 (Android デバイスの SmartLock 設定) を参照してください。  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能  
 2016 年 4 月の Configuration Manager (現在のブランチ) では、ハイブリッド新機能は導入されませんでした。  

##  <a name="march-2016"></a>2016 年 3 月  

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

  サードパーティのモバイル デバイス管理 (MDM) ベンダーを使用して、iOS の "オープンイン" 管理を利用できます。 構成プロファイル設定で制限を設定し、MDM ソフトウェアを使用してアプリを展開できます。 ユーザーが管理対象アプリをインストールすると、制限が適用されます。 詳細情報を確認します。[Microsoft Intune モバイル アプリ管理ポリシーと iOS の Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) Intune ライブラリ。  

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

  これらのアプリは Configuration Manager コンソールの [アプリケーション] ノードに表示されます。 アプリケーションの展開の詳細については、「[System Center Configuration Manager でアプリケーションを展開する方法](../../apps/deploy-use/deploy-applications.md)」をご覧ください。  

- **Android Samsung KNOX Standard デバイスのキオスク モードの設定**

  キオスク モードでは、特定の機能のみ実行できるようにデバイスをロックできます。  Configuration Manager (現在のブランチ) バージョン 1602 以降では、Samsung KNOX Standard デバイスのキオスク モードの設定を指定できるようになりました。 詳細については、「[System Center Configuration Manager クライアントを使用せずに管理されている Android デバイスと Samsung KNOX Standard デバイスの構成項目を作成する](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)」を参照してください。  

- **iOS のアクティベーション ロック**

  Configuration Manager (現在のブランチ) バージョン 1602 以降では、iOS 7.1 以降用の「iPhone を探す」アプリの機能である、iOS のアクティベーション ロックを管理できます。 iPhone を探すアプリをデバイスで使用すると、アクティブ化ロックが自動的に有効になります。  詳細については、「[Manage iOS Activation Lock bypass for System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock)」 (System Center Configuration Manager での iOS のアクティベーション ロック バイパスの管理) を参照してください。  



## <a name="notices"></a>通知

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 および System Center 2012 R2 Configuration Manager (RTM):2017 年 4 月 10 日に終了するハイブリッド モバイル デバイス管理のサポート
*2017 年 1 月 11 日*

System Center 2012 Configuration Manager SP1 と System Center 2012 R2 Configuration Manager RTM のサポートは 2016 年 7 月 12 日に終了しました。 これに続き、2017 年 4 月 10 日にハイブリッド MDM の Microsoft Intune サービスに接続するこれらのリリースのサポートが終了します。 この日付以降、ハイブリッド MDM はこれらのリリースをもって機能を停止します。 Intune コネクタが Intune サービスに接続できなくなるため、マネージド デバイスは実質的にアンマネージドとなります。 アップグレードが実施されるまで、Configuration Manager のデータ (ポリシーとアプリケーションなど) は Intune にフローアップせず、マネージド デバイスのデータは Configuration Manager にフローダウンしません。

Configuration Manager 2012 SP1 または R2 RTM でハイブリッド展開を実行している場合は、2017 年 4 月 10 日より前に、Configuration Manager (Current Branch) または Configuration Manager 2012 (R2 SP1 または SP2) の最新のサポートされているサービス パックにアップグレードしてサービスの中断を回避することをお勧めします。

その他のリソース:
-   [System Center Configuration Manager (Current Branch) へのアップグレード](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [System Center 2012 R2 Configuration Manager SP1 へのアップグレードの計画](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [System Center 2012 Configuration Manager SP2 へのアップグレードの計画](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Windows Phone 8 ポータル サイトのアップロードは非推奨とされます
*2016 年 10 月 25 日*

11 月に Windows 8、Windows Phone 8、および Windows RT に対する Intune サポートが非推奨とされ、Windows Phone 8 ポータル サイトのサポートが終了するので、Configuration Manager コンソールでは、署名済みのポータル サイト アプリをアップロードする機能が廃止されました。  既に登録されている Windows 8、Windows Phone 8、および Windows RT デバイスは引き続きサポートされますが、これらのプラットフォームへの追加デバイスの登録はサポートされていません。
