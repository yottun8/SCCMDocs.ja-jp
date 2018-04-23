---
title: ハイブリッド MDM の新機能
titleSuffix: Configuration Manager
description: Configuration Manager と Intune のハイブリッド展開で使用できるモバイル デバイス管理の新機能について説明します。
ms.custom: na
ms.date: 04/02/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c6918983bca3e598fd99a8f7670ada3f7e43cfa6
ms.sourcegitcommit: d8a4a53630351b3d677bbdc5d203e7d330472cba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2018
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Configuration Manager と Microsoft Intune を使用したハイブリッド モバイル デバイス管理の新機能

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、System Center Configuration Manager と Intune のハイブリッド展開で使用できるモバイル デバイス管理 (MDM) の新機能の詳細について説明します。     

> [!Note]    
> Azure 上の Intune は、Microsoft が推奨する MDM ソリューションです。     
> - Intune スタンドアロンの新機能と更新内容の詳細については、「[Microsoft Intune の新機能](https://docs.microsoft.com/intune/whats-new)」を参照してください。    
> - Intune スタンドアロンに移行する詳細な方法については、「[Migrate hybrid MDM users and devices to Intune standalone](https://docs.microsoft.com/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)」(ハイブリッド MDM ユーザーとデバイスを Intune スタンドアロンに移行する) を参照してください。
> - Intune とハイブリッド MDM の UI の更新の詳細については、「[Intune とエンド ユーザー アプリの UI の更新](https://docs.microsoft.com/intune/whats-new-app-ui)」を参照してください。 

##  <a name="compatibility-with-configuration-manager-versions"></a>Configuration Manager のバージョンとの互換性  
この記事の各セクションでは、3 つの異なるカテゴリにあるハイブリッド機能を一覧表示します。 次のガイダンスを使用すると、各カテゴリの機能とさまざまなバージョンの Configuration Manager との互換性を判断できます。  

|機能のカテゴリ|説明|
|-|-|
|**Microsoft Intune の新機能** | 通常、このカテゴリに一覧表示されたすべての機能は、Configuration Manager のすべてのリリースで動作します。 これには System Center 2012 R2 Configuration Manager リリースが含まれています。これらの機能では Intune サービスのみが必要であり、Configuration Manager の追加機能は不要なためです。|
|**Configuration Manager Technical Preview の新機能**| このカテゴリに一覧表示されたすべての機能は、指定されたバージョンの Technical Preview リリースでのみ動作します。 これらの機能を試すには、機能の説明で指定されたバージョンの Technical Preview をインストールする必要があります。 詳細については、「[System Center Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を参照してください。|
|**Configuration Manager (現在のブランチ) の新機能**| このカテゴリに一覧表示されたすべての機能は、バージョン 1511 や 1602 など、指定されたバージョンの Configuration Manager (現在のブランチ) でのみ動作します。 ハイブリッド展開に旧バージョンの Configuration Manager を使用している場合は、機能の説明で指定されたバージョンの Configuration Manager (現在の分岐) にアップグレードする必要があります。 詳細については、「[System Center Configuration Manager へのアップグレード](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)」を参照してください。|



## <a name="april-2018"></a>2018 年 4 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>iOS 用ポータル サイト アプリに関するユーザー エクスペリエンスの更新プログラム 
<!--1412866-->
iOS 用のポータル サイト アプリに対して、主要なユーザー エクスペリエンスの更新プログラムをリリースしました。 この更新プログラムでは、ビジュアル面の完全な再設計により、最新の外観に一新されています。 アプリの機能が更新されていますが、その使いやすさとアクセシビリティも向上しています。  

次の点も改善されています。
- iPhone X のサポート。
- アプリの起動時間と応答の読み込み時間の短縮。
- 最新の状態情報をユーザーに提供する追加の進行状況バー。
- 物事が正しく進まなかった場合、それを報告しやすくするためのログのアップロード方法の向上。  

新しい外観を確認するには、[アプリの UI の新機能](/intune/whats-new-app-ui)に関するページを参照してください。



## <a name="march-2018"></a>2018 年 3 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

#### <a name="azure-active-directory-web-sites-can-require-the-intune-managed-browser-app-and-support-single-sign-on-for-the-managed-browser-public-preview"></a>Azure Active Directory の Web サイトでは、Intune Managed Browser アプリを要求し、Managed Browser (パブリック プレビュー) に対するシングル サインオンをサポートすることができる
<!-- 710595 --> 
Azure Active Directory (Azure AD) を使用している場合、モバイル デバイスでの Web サイトへのアクセスを Intune Managed Browser アプリに制限できるようになりました。 Managed Browser では、Web サイトのデータは安全性を維持され、エンド ユーザーの個人データと分離されます。 さらに、Managed Browser は、Azure AD によって保護されているサイトに対するシングル サインオン機能をサポートします。 Managed Browser にサインインすると、または Intune によって管理されている別のアプリでデバイスの Managed Browser を使うと、ユーザーが資格情報を入力しなくても、Managed Browser は Azure AD によって保護されている会社サイトにアクセスできます。 この機能は、Outlook Web Access (OWA) や SharePoint Online などのサイトだけでなく、Azure App プロキシ経由でアクセスされるイントラネット リソースのような他の企業サイトにも適用されます。



## <a name="february-2018"></a>2018 年 2 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **デバイス登録マネージャーを使う登録の macOS ポータル サイトによるサポート**  
    ユーザーは、macOS ポータル サイトで登録するときに、デバイス登録マネージャーを使うことができるようになりました。
    <!-- 1352411 -->


## <a name="january-2018"></a>2018 年 1 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **Android for Work のポータル サイト アプリの承認**  
  Android for Work を使用している組織は、Android 用のポータル サイト アプリを手動で承認します。 その後、管理された Google Play ストアから引き続き自動更新を受信します。
  <!--1797090 -->  

- **Intune の条件付きアクセス ポリシーは、Azure Portal からのみ利用できる**   
  このリリース以降は、**[Azure Active Directory]** > **[条件付きアクセス]** から [Azure Portal](https://portal.azure.com) の条件付きアクセス ポリシーを構成して管理する必要があります。 便宜上、**[Intune]** > **[条件付きアクセス]** の、Azure Portal 内にある Intune からこのブレードにアクセスすることもできます。
  <!-- 1737088 1634311 --> 

- **コンプライアンス メールの更新**    
  コンプライアンス違反のデバイスを報告するメールが送信される際に、そのコンプライアンス違反のデバイスの詳細が含まれます。 
  <!--1637547 -->

- **Android デバイスの "解決" アクションの新しい機能**    
  Android 用ポータル サイト アプリは、[デバイス暗号化の問題](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android)を解決するために、**[デバイス設定の更新]** の "解決" アクションを拡張しています。
  <!--1583480-->

- **Windows 10 向けポータル サイト アプリで利用できるリモート ロック**    
  エンドユーザーは、Windows 10 向けポータル サイト アプリから自分のデバイスをリモートでロックできるようになりました。 このアクションはエンド ユーザーがアクティブに使用しているローカル デバイスには表示されません。
  <!--676506-->

- **Windows 10 向けポータル サイト アプリの準拠に関する問題を容易に解決できる**   
  Windows デバイスを使用するエンド ユーザーは、ポータル サイト アプリ内で非準拠の理由をタップできます。 可能な場合には、問題を解決するために設定アプリの適切な場所に直接移動します。
  <!--676546-->    



## <a name="december-2017"></a>2017 年 12 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **利用可能なアプリケーションの展開で Android Enterprise がサポートされるようになりました**    
  Android Enterprise (旧称 Android for Work) アプリを、**必須**に加えて、**利用可能**として展開できるようになりました。 詳細については、「[System Center Configuration Manager で Android アプリケーションを作成する](/sccm/mdm/deploy-use/creating-android-applications)」を参照してください。



## <a name="november-2017"></a>2017 年 11 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **管理対象アプリから許可されているテキスト プロトコル**  
  Intune App SDK によって管理されているアプリは、SMS メッセージを送信できます。
  <!-- 1414050  -->   

- **macOS 用ポータル サイト アプリ提供開始**   
  macOS での Intune ポータル サイトのエクスペリエンスが更新されました。 ユーザーが登録済みのすべてのデバイスで必要となるすべての情報とコンプライアンス通知が明確に表示されるように最適化されています。 Intune ポータル サイトがデバイスに展開されると、macOS 用の Microsoft AutoUpdate によって更新プログラムが提供されます。 macOS デバイスから Intune ポータル サイトにログインすることで、新しい macOS 用 Intune ポータル サイトをダウンロードします。
  <!--1541700-->   

- **Microsoft Planner が承認済みアプリのモバイル アプリ管理 (MAM) リストの一部に**    
  iOS および Android 用の Microsoft Planner アプリが、モバイル アプリ管理 (MAM) に対する承認済みアプリの一部となりました。 Azure Portal の Intune App Protection ブレードからすべてのテナントに対してアプリを構成します。 詳細については、[承認済みアプリの MAM リスト](https://www.microsoft.com/cloud-platform/microsoft-intune-apps)に関するページをご覧ください。
  <!-- 1248473 -->    

- **iOS の管理対象アプリ ログにアクセス**    
  Managed Browser をインストールしているエンド ユーザーは、Microsoft が公開したすべてのアプリの管理状態を表示し、管理対象 iOS アプリの問題を解消するためにログを送信できるようになりました。
  <!-- 1469920 -->    

  iOS デバイスの Managed Browser でトラブルシューティング モードを有効にする方法については、「[iOS で Managed Browser を使用し、管理対象アプリ ログにアクセスする方法](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios)」を参照してください。

- **iOS 用ポータル サイト バージョン 2.9.0 でのデバイスのセットアップ ワークフローの機能強化**    
  iOS 用ポータル サイト アプリでのデバイス セットアップ ワークフローを改善しました。 言葉がよりわかりやすくなり、可能な範囲で画面をまとめました。 また、セットアップのテキスト全体でお客様の会社名を使用することで、表現がより会社に合ったものになっています。 この更新されたワークフローについては、「[アプリの UI の新機能](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017)」ページで確認できます。

- **Android 用ポータル サイト アプリに関するフィードバック プロンプト**    
  Android 用ポータル サイト アプリからエンド ユーザー フィードバックを要求されるようになりました。 このフィードバックは Microsoft に直接送信され、エンドユーザーは一般の Google Play ストアでアプリをレビューできます。 フィードバックは必須ではなく、ユーザーは簡単にこれを拒否して、アプリの使用を続行できます。 
  <!--1165249-->    

- **Windows 10 デバイスで確認できるデバイス情報のエンドユーザーへの通知**    
  Windows 10 用ポータル サイト アプリの [デバイスの詳細] 画面に **[所有権の種類]** が追加されました。 この情報により、ユーザーは Intune のエンド ユーザー ドキュメントから直接プライバシーの詳細を参照できます。この情報は、**[バージョン情報]** 画面でも確認できます。
  <!--1337920-->    

- **Android デバイスで利用できる新しい '解決' アクション**    
  Android のポータル サイト アプリの _[デバイス設定の更新]_ ページに '解決' アクションが導入されます。 このオプションを選択すると、デバイスの非準拠の原因になっている設定に、エンド ユーザーが直接誘導されます。 Android 向けのポータル サイト アプリでは現在のところ、[デバイス パスコード](https://docs.microsoft.com/intune-user-help/set-your-pin-or-password-android)、[デバイスの暗号化](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android)、[USB デバッグ](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-usb-debugging-android)、[不明なソース](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-unknown-sources-android)設定に対してこのアクションがサポートされています。 
  <!--1583480-->    


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能

- **コンプライアンス非対応に対するアクション**    
  コンプライアンスに対応していないデバイスに適用される時間順のアクションを構成できるようになりました。 たとえば、コンプライアンスに対応していないデバイスをユーザーに電子メールで通知したり、そのようなデバイスにコンプライアンス非対応とマークしたりすることができます。 詳細については、「[コンプライアンス非対応に対するアクションの設定](/sccm/mdm/deploy-use/actions-for-noncompliance)」を参照してください。
  <!--1321366 -->

- **新しいモバイル アプリケーション管理ポリシーの設定**     
  次の設定がモバイル アプリケーション管理ポリシーの設定に追加されました。
  - **連絡先の同期を無効にする:** アプリでデバイス上のネイティブ連絡先アプリにデータを保存できなくなります。
  - **印刷を無効にする:** アプリで職場または学校のデータを印刷できなくなります。
  <!-- 1324760 -->    

  「[Configuration Manager のモバイル アプリケーション管理ポリシーを使ったアプリの保護](/sccm/mdm/deploy-use/protect-apps-using-mam-policies)」を参照し、新しいアプリの保護のポリシー設定を試してください。

- **Windows 10 ARM64 デバイスのサポート**     
  Windows 10 を実行する ARM64 デバイスを使用できるようになると、それらのデバイスでハイブリッド モバイル デバイス管理 (MDM) シナリオがサポートされます。 詳細については、「[Windows 10 ARM64 デバイスのサポート](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support)」をご覧ください。
  <!-- 1355000 -->    

- **Configuration Manager コンソールの VPN プロファイル エクスペリエンスの向上**     
  このリリースでは、選択したプラットフォームに適した設定が表示されるように、VPN プロファイル ウィザードとプロパティ ページが更新されました。 この機能は、以前は Configuration Manager Technical Preview 1709 で使用できました。 現在は、Intune と Configuration Manager (Current Branch) バージョン 1710 のハイブリッド展開で使用できます。 詳しくは、「[Configuration Manager コンソールの VPN プロファイル エクスペリエンスの向上](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console)」をご覧ください。
  <!-- 1318232 -->


### <a name="new-in-configuration-manger-technical-preview-1711"></a>Configuration Manager Technical Preview 1711 の新機能

- **Windows 10 用の新しいコンプライアンス ポリシー オプション**   
  Windows 10 デバイスのコンプライアンス ポリシーに新しいオプションを構成できるようになりました。 新しい設定には、ファイアウォール、ユーザー アカウント制御、Windows Defender Anitivirus、OS ビルド バージョン管理に関するポリシーがあります。 詳細については、「[Windows 10 用の新しいコンプライアンス ポリシー オプション](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10)」をご覧ください。



## <a name="october-2017"></a>2017 年 10 月

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Configuration Manager Technical Preview 1709 の新機能

- **Configuration Manager コンソールの向上した VPN プロファイル エクスペリエンス**      
  VPN プロファイルの設定は、プラットフォームに従ってフィルター処理されるようになりました。 新しい VPN プロファイルを作成するとき、サポートされているプラットフォームのそれぞれに適した設定のみが選択されます。 既存の VPN プロファイルには影響しません。 この変更の詳細については、[こちら](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console)をご覧ください。
  <!-- 1313282 -->


### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能  

- **Android 向けポータル サイト アプリに関してユーザーの自己解決をサポートする**     
  Android 向けポータル サイト アプリでは、エンド ユーザーへの指示が追加されています。それは新しいユース ケースの理解や、可能な場合にはその自己解決にも役立ちます。
    - エンド ユーザーは、追加が許されているデバイスの最大数に達した場合、デバイスを削除するように [Azure Active Directory ポータル](https://account.activedirectory.windowsazure.com/r/#/profile)に誘導されます。
    - [Samsung Knox デバイスのアクティベーション エラーを解消する](https://go.microsoft.com/fwlink/?linkid=859718)か、[節電モードをオフにする](https://docs.microsoft.com/intune-user-help/power-saving-mode-android)ための手順がエンド ユーザーに表示されます。 いずれの解決策でも問題が解消されない場合、[Microsoft にログを送信する](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android)方法を説明します。
  <!-- 1573324, 1573150, 1558616, 1564878 -->      

- **Android 用ポータル サイトのデバイスのセットアップ進行状況インジケーター**    
  Android 用ポータル サイト アプリでは、ユーザーがデバイスを登録しているときに、デバイスのセットアップ進行状況インジケーターが示されます。 このインジケーターで新しいステータスが表示されます。初めに表示されるものから挙げると、[デバイスをセットアップしています...]、[デバイスを登録しています]、[デバイスの登録を終了しています]、[デバイスのセットアップを終了しています] です。  
  <!--1565657-->    

- **iOS 用ポータル サイトでの証明書ベースの認証のサポート**    
  iOS 用ポータル サイト アプリでの証明書ベースの認証 (CBA) のサポートが追加されました。 CBA を使用するユーザーは、ユーザー名を入力してから [Sign in with a certificate]\(証明書でサインイン\) リンクをタップします。 Android および Windows 用ポータル サイト アプリでは、既に CBA がサポートされています。 詳細については、[ポータル サイト アプリにサインインする](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal)方法に関するページをご覧ください。
  <!--1029830-->   

- **ポータル サイトのデバイスのセットアップ ワークフローを改善**     
  Android 用ポータル サイト アプリにおけるデバイスのセットアップ ワークフローを改善しました。 言語がよりわかりやすく、会社固有のものとなり、可能な範囲で画面をまとめるようにしました。 これらの機能強化は、[アプリ UI の新機能](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017)に関するページで確認できます。
  <!--1490692-->     

- **Android デバイスの連絡先情報へのアクセスを要求するガイダンスを改善**     
  Android 用ポータル サイト アプリでは、エンド ユーザーに対して連絡先情報へのアクセス許可を求めることがあります。 エンド ユーザーがこのアクセスを拒否した場合に、条件付きアクセスを許可するよう求めるアプリ内通知が表示されます。 
  <!--1484985-->     

- **Android 用に安全なスタートアップ修復**     
  Android デバイスを使用するエンド ユーザーは、ポータル サイト アプリ内で非準拠の理由をタップできます。 可能な場合には、問題を解決するために設定アプリの適切な場所に直接移動します。 
  <!--1490712-->    

- **Android Oreo 用ポータル サイト アプリでのエンド ユーザー向けの追加のプッシュ通知**    
  Android Oreo 用のポータル サイト アプリがバック グラウンド タスク (Intune サービスからポリシーを取得するなど) を実行しているときに、エンド ユーザーに知らせる追加の通知が表示されます。 この通知により、ポータル サイトがデバイス上でいつ管理タスクを実行しているかが、エンド ユーザーにとってより分かりやすくなります。 この機能強化は、Android Oreo 用のポータル サイト アプリの[ポータル サイト UI の全体的な最適化](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune)の一部です。 
  <!--1475932 -->     

- **仕事用プロファイルを使用した場合の Android 用ポータル サイト アプリの新しい動作**     
  仕事用プロファイルを使用して Android for Work デバイスを登録した場合は、仕事用プロファイルのポータル サイト アプリでデバイスの管理タスクが実行されます。 

  個人用プロファイルの MAM が有効なアプリを使用している場合を除いては、Android 用ポータル サイト アプリを使用することはなくなります。 仕事用プロファイルが正常に登録されると、仕事用プロファイル エクスペリエンスを向上させるために Intune が自動で個人用ポータル サイト アプリを非表示にします。

  Android 用ポータル サイト アプリは、ブラウザーで [Play ストアのポータル サイト](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)を表示して **[有効]** をタップすれば、いつでも個人用プロファイル内で有効化できます。
  <!--1485783-->    

- **維持モードに移行中の Windows 8.1 および Windows Phone 8.1 用ポータル サイト**    
  Windows 8.1 および Windows Phone 8.1 用ポータル サイト アプリが維持モードに移行中であることを知らせる通知が追加されました。 詳細については、「[通知](#notices)」をご覧ください。  
  <!--1428681-->    

- **サポートされていない Samsung Knox デバイスの登録をブロック**   
  ポータル サイト アプリは、サポートされている Samsung Knox デバイスのみを登録しようとします。 MDM 登録を妨げる KNOX のアクティベーション エラーを回避するため、デバイス登録はそのデバイスが [Samsung が公開しているデバイス一覧](https://www.samsungknox.com/knox-supported-devices/knox-workspace)にある場合のみ実行されます。 KNOX をサポートしている Samsung デバイスにはモデル番号がありますが、サポートしていないデバイスにはありません。 使用するデバイスが Knox に対応しているかどうかを、デバイスを購入したり展開したりする前に販売店に確認してください。 対応しているデバイスの一覧は、[Android および Samsung KNOX Standard ポリシー設定](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices)に関するページで確認できます。
  <!-- 1490695 -->     

- **Android 4.3 以前のサポートを終了**     
  Android 4.3 以前のサポートが終了したことを知らせる通知が追加されました。 詳細については、「[通知](#notices)」をご覧ください。
  <!--1171126, 1326920 -->     

- **登録済みデバイスでどのようなデバイス情報を表示できるかをエンド ユーザーに通知**     
  すべてのポータル サイト アプリの [デバイスの詳細] 画面に、**[所有権の種類]** が追加されます。 この情報により、[会社が確認できる情報](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune)に関するページから直接、プライバシーの詳細を確認できるようになります。 この機能強化は、近日中にすべてのポータル サイト アプリに展開される予定です。 iOS 用のこの機能については [9 月](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017)にお知らせしました。 
  <!--1165314-->     



## <a name="september-2017"></a>2017 年 9 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能     

- **Windows 10 のポータル サイト アプリに更新アクションが追加されました**    
    Windows 10 向けの会社ポータル アプリでは、ユーザーがプルして更新するか、デスクトップで F5 キーを押して、アプリのデータを更新できます。
    <!-- 1132468 -->     

- **iOS でどのようなデバイス情報を表示できるかをエンド ユーザーに通知**   
    iOS 用のポータル サイト アプリの [デバイスの詳細] 画面に **[所有権の種類]** が追加されました。 この情報により、ユーザーは Intune のエンド ユーザー ドキュメントから直接プライバシーの詳細を参照できます。この情報は、[バージョン情報] 画面でも確認できます。 
    <!--739894-->    

- **Android 用ポータル サイト アプリの文言の分かりやすさの向上**   
    Android 用ポータル サイト アプリの登録プロセスが簡略化されました。テキストが新しくなり、エンド ユーザーがより簡単に登録できるようになりました。 カスタム登録ドキュメントをお持ちの場合は、ドキュメントを更新して新しい画面を反映してください。 「[Intune とエンド ユーザー アプリの UI の更新](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017)」のページにサンプル画像があります。
    <!---1396349-->    

- **Windows Information Protection 許可ポリシーに Windows 10 のポータル サイト アプリを追加**    
    Windows 情報保護 (WIP) をサポートするために、Windows 10 のポータル サイト アプリが更新されました。 WIP 許可ポリシーにアプリを追加できます。 この変更により、アプリを **[適用除外]** 一覧に追加する必要がなくなります。 

    1 つの WIP 構成アイテムのみをデバイスに配信できます。 2 つの WIP 構成アイテムの対象が同じデバイスになっている場合、いずれの WIP ポリシーも適用されません。
    <!-- 677129 -->    

- **iOS 8.0 のサポート終了の通知を追加**    
    iOS 8.0 のサポート終了の通知が追加されました。 詳細については、「[通知](#notices)」をご覧ください。



## <a name="august-2017"></a>2017 年 8 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能     

- **Android ポータル サイト ユーザーおよびアプリ保護ポリシー ユーザーの新しいサインイン エクスペリエンス**    
  エンドユーザーは、Android デバイスを登録しなくても、Android ポータル サイト アプリを使用して、今すぐにアプリを閲覧したり、デバイスを管理したり、IT 連絡先情報を確認したりできます。 さらに、エンド ユーザーが既に Intune App Protection ポリシーによって保護されているアプリを使用し、Android ポータル サイトを起動している場合、エンド ユーザーがデバイスの登録を要求されることはありません。
  <!-- 621669 -->



## <a name="july-2017"></a>2017 年 7 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **Android および Windows Phone のサポート終了に関する通知の追加**    
    Android と Windows Phone のバージョンのサポート終了に関する通知が新たに追加されました。 詳細については、「[通知](#notices)」をご覧ください。


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能

以下の機能は以前、Configuration Manager Technical Preview リリースで利用できました。 現在は、Intune と Configuration Manager (Current Branch) バージョン 1706 のハイブリッド展開で使用できます。

- [Entrust 証明機関の Entrust のサポート](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [新しいモバイル アプリケーション管理ポリシーの設定](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Android for Work の共有構成の更新](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [新しいデバイス コンプライアンス ポリシー ルール](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Configuration Manager クライアントを使用して管理されていない Windows 10 デバイスの新しい構成設定](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [macOS VPN プロファイルの Cisco (IPsec) のサポート](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Android および iOS の登録制限](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 



## <a name="june-2017"></a>2017 年 6 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **MDM 機関を変更する**    
  Configuration Manager バージョン 1610 以降では、Microsoft サポートに連絡しなくても、MDM 機関を変更できます。 また、既存の管理対象デバイスの登録を解除してから再登録する必要もありません。 詳細については、「[Change your MDM authority](/sccm/mdm/deploy-use/change-mdm-authority)」(MDM 機関を変更する) を参照してください。

- **管理対象ブラウザーとアプリケーション プロキシの統合**    
  Intune Managed Browser は、ユーザーがリモートで作業している場合でも内部の Web サイトにアクセスできるように、Azure AD アプリケーション プロキシ サービスに統合できるようになりました。 ブラウザーのユーザーが、通常通りにサイトの URL を入力すると、Managed Browser がアプリケーション プロキシの Web ゲートウェイを介して要求をルーティングします。 詳細については、「[Managed Browser ポリシーを使用したインターネット アクセスの管理](https://docs.microsoft.com/intune/app-configuration-managed-browser)」を参照してください。

- **Android 用ポータル サイト アプリのアプリの保護ポリシーのエンド ユーザー エクスペリエンスが新しくなりました**  
  お客様のフィードバックに基づいて、Android 用ポータル サイト アプリを変更し、**[会社のコンテンツにアクセスする]** ボタンを表示しました。 目的は、エンド ユーザーがアプリの保護ポリシーをサポートするアプリ、Intune モバイル アプリケーション管理の機能にのみアクセスする必要があるときに、不要な登録プロセスを経由せずに済むようにすることです。 これらの変更は、[アプリ UI の新機能](https://docs.microsoft.com/intune/whats-new-app-ui)ページで確認できます。

- **ポータル サイトを簡単に削除するための新しいメニュー操作**  
  ユーザーからのフィードバックに基づき、Android 用ポータル サイト アプリで、デバイスからのポータル サイトの削除を開始する新しいメニュー操作を追加しました。 この操作は、ユーザーがデバイスからアプリを削除できるように、Intune の管理からデバイスを削除します。 これらの変更は、[アプリ UI の新機能](https://docs.microsoft.com/intune/whats-new-app-ui)ページおよび [Android エンドユーザー文書](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android)で確認できます。

- **アプリを Windows 10 Creators Update と同期するための機能強化**  
  Windows 10 用のポータル サイト アプリが、Windows 10 Creators Update (バージョン 1703) が搭載されたデバイスのアプリ インストール要求の同期を自動的に開始するようになりました。 この動作により、"同期保留中" 状態のときにアプリのインストールが停止する問題が減少します。 また、ユーザーは、アプリ内からの同期を手動で開始することができます。 これらの変更は、[アプリ UI の新機能](https://docs.microsoft.com/intune/whats-new-app-ui)ページで確認できます。

- **Windows 10 ポータル サイトの新しいガイド機能**   
  Windows 10 用のポータル サイト アプリでは、特定されていないデバイスや登録されていないデバイス向けのガイド付き Intune チュートリアルを利用できます。 新しい機能では、Azure Active Directory の登録 (条件付きアクセス機能に必要) と MDM の登録 (デバイス管理機能に必要) をユーザーに紹介する手順を表示します。 このガイド付きの機能は、ポータル サイトのホーム ページからアクセス可能になります。 ユーザーは、これらの登録を完了していない場合でも、引き続きアプリを使用できますが、機能が制限されます。

  この更新プログラムは、Windows 10 Anniversary Update (ビルド 1607) 以上を実行しているデバイスに表示されます。 これらの変更は、[アプリ UI の新機能](https://docs.microsoft.com/intune/whats-new-app-ui)ページで確認できます。

- **IOS 用ポータル サイト アプリでアプリのタイルの機能強化**  
  ポータル サイトで設定したブランドの色を反映するように、ホームページ上のアプリのタイルのデザインを更新しました。 詳細については、[アプリ UI の新機能](https://docs.microsoft.com/intune/whats-new-app-ui)を参照してください。

- **IOS 用ポータル サイト アプリでアカウントの選択機能を使用できるようになりました**  
  iOS デバイスのユーザーは、職場または学校アカウントを使って他の Microsoft アプリにサインインしている場合、ポータル サイトにサインインするときに、新しいアカウント選択機能が表示されることがあります。 詳細については、[アプリ UI の新機能](https://docs.microsoft.com/intune/whats-new-app-ui)を参照してください。

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Configuration Manager Technical Preview 1706 の新機能

- **新しい Windows 構成アイテムの設定**      
  新しい Windows 構成アイテムは、パスワード、デバイス、ストア、および Microsoft Edge の設定のカテゴリで使用できます。 詳細については、「[New Windows configuration item settings](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings)」(新しい Windows 構成アイテム) を参照してください。
  <!-- 1354715 -->

- **新しいデバイス コンプライアンス ポリシー ルール**   
  以前は Intune スタンドアロンにのみ使用可能だったコンプライアンス ポリシー用の新しいオプションを構成できるようになりました。 詳細については、「[デバイス コンプライアンス ポリシーの改善](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules)」を参照してください。

- **Android および iOS の登録制限**       
  管理者は、ユーザーが、ハイブリッド環境で個人の Android または iOS デバイスを登録できないことを指定できるようになりました。 このアクションにより、宣言済みのデバイス、会社が所有しているデバイス、またはデバイス登録プログラムで登録されている iOS デバイスに登録されるデバイスを制限することができます。 詳細については、「[Android および iOS の登録制限](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions)」を参照してください。
  <!-- 1290826 -->

- **Entrust 証明機関のサポート**      
  Configuration Manager は Entrust 証明機関をサポートするようになりました。 このサポートにより、Microsoft Intune に登録されたデバイスに PFX 証明書を発行できます。    
  <!-- 1350740 -->

  Configuration Manager で証明書登録ポイントの役割を追加するときに、証明機関として Entrust を構成できます。 PFX 証明書を発行する新しい証明書プロファイルを追加する場合は、Microsoft または Entrust のいずれかの証明機関を選択できます。

  **既知の問題**: 1706 Technical Preview では、PFX 証明書は、Microsoft 証明機関用に発行されません。 この問題は、インポートされた PFX 証明書または SCEP プロファイルには影響ありません。

- **macOS VPN プロファイルの Cisco (IPsec) のサポート**      
  接続タイプとして Cisco (IPsec) を指定して macOS VPN プロファイルを作成できます。 詳細については、「[VPN プロファイルの作成](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles)」を参照してください。
  <!-- 1321367 -->


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

  - 色: ポータル サイトのタブ ヘッダーに IT が設定したブランディングの色が付きます。
  - アプリ: **[アプリ]** タブの **[おすすめアプリ]** ボタンと **[すべてのアプリ]** ボタンが更新されました。
  - 検索: **[アプリ]** タブの **[検索]** ボタンはフローティング アクション ボタンです。
  - アプリ ナビゲーション: **[すべてのアプリ]** ビューで **[おすすめ]**、**[すべて]**、**[カテゴリ]** のタブ付きビューが表示され、移動がより簡単になりました。
  - サポート: **[マイ デバイス]** タブと **[IT に連絡]** タブが更新され、読みやすくなりました。

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



## <a name="notices"></a>通知

### <a name="windows-company-portal-send-feedback-option-may-no-longer-work"></a>Windows ポータル サイトの [フィードバックの送信] オプションは今後機能しない場合がある

Windows ポータル サイト アプリには、アプリに関するフィードバックを Microsoft に送信できるように 'フィードバックの送信' オプションがあります。 2018 年 4 月 30 日から、Windows 10 バージョン 1607 以降を実行している Windows 10 ポータル サイト アプリでのみ、このオプションが引き続きサポートされます。   

#### <a name="how-does-this-affect-me"></a>ユーザーへの影響

エンド ユーザーに Windows ポータル サイト アプリをインストールしていない場合、このメッセージは無視してください。

エンド ユーザーの中にポータル サイト アプリをインストールしている人がいる場合、次のシナリオにおいて、4 月 30 日から 'フィードバックの送信' ボタンが機能しなくなることに注意してください。  

 - Windows 10 バージョン 1507 とバージョン 1511 の Windows 10 ポータル サイト アプリ  

 - Windows Phone Windows 8.1 ポータル サイト アプリ  

影響を受けるデバイスの場合、'フィードバックの送信' オプションは機能せず、再試行でも動作しません。 影響を受けるデバイスで発生した現象について Microsoft にフィードバックを送信するには、下に記す代替フィードバック チャネルをご利用ください。

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>この変更に対して必要な準備

エンド ユーザーにこの変更を通知し、必要に応じてユーザー ガイダンスを更新してください。 

Windows Phone 8.1、Windows 10 バージョン 1507、Windows 10 バージョン 1511 でポータル サイトを利用しているエンド ユーザーに 2 つの代替フィードバック チャネルを利用できることをお知らせください。 代替フィードバック方法:  

- Windows 10 でフィードバック ハブ アプリを使用する  
- WinCPfeedback@microsoft.com に電子メールを送信する  

Windows 10 バージョン 1607 以降を利用しているエンド ユーザーに Microsoft Store で入手できる Windows ポータル サイトの最新版に更新するように要請します。



### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>維持モードに移行中の Windows 8.1 および Windows Phone 8.1 用ポータル サイト 
<!--1428681-->
*2017 年 10 月 6 日*   
 
2017 年 10 月以降、Windows 8.1 および Windows Phone 8.1 用ポータル サイト アプリは維持モードに移行されます。 このモードは、アプリや既存のシナリオ (登録やコンプライアンスなど) で、引き続きこれらのプラットフォームがサポートされることを意味します。 これらのアプリは引き続き、Microsoft Store などの既存のリリース チャネルからダウンロードできます。 

維持モードに移行すると、これらのアプリには重要なセキュリティ更新プログラムのみが適用されるようになります。 追加の更新プログラムや追加機能はリリースされなくなります。 新機能が必要な場合は、デバイスを Windows 10 または Windows 10 Mobile に更新することをおすすめします。 

### <a name="end-of-support-for-ios-80"></a>iOS 8.0 のサポートの終了 
<!---1164477--->
iOS の管理対象アプリとポータル サイト アプリから会社のリソースにアクセスするには、iOS 9.0 以降が必要になりました。 9 月以前に更新されていないデバイスは、ポータル サイトまたはそのアプリにアクセスできなくなります。 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>プラットフォーム サポートのお知らせ: Windows Phone 8.1 のメインストリーム サポートが 2017 年 7 月 11 日に終了
<!-- 1327781 -->
*2017 年 7 月 11 日*

Windows Phone 8.1 プラットフォームのメインストリーム サポートは終了しました。 Windows 8.1 PC のサポートに影響はありません。

Intune サービスによって管理されている Windows Phone 8.1 デバイス (ハイブリッド MDM に登録されているデバイスも含む) への直接的な影響はありません。 登録されたデバイスは引き続き動作します。 すべてのポリシー、構成、アプリが、期待どおりに動作し続けます。 Intune サービス内の Windows Phone 8.1 プラットフォーム、および Windows Phone 8.1 ポータル サイト アプリを対象とした機能強化はないことに注意してください。

できるだけ早い段階で、対象の Windows Phone 8.1 デバイスを Windows 10 Mobile にアップグレードすることをお勧めします。  

### <a name="end-of-support-for-android-43-and-lower"></a>Android 4.3 以前のサポートの終了
<!---1171127--->
*2017 年 7 月 6 日*

Android の管理対象アプリとポータル サイト アプリから会社のリソースにアクセスするには、Android 4.4 以降が必要になりました。 10 月 1 日以前に更新されていないデバイスは、ポータル サイトまたはそのアプリにアクセスできなくなります。 登録されたすべてのデバイスが 12 月までにインベントリから強制的に削除されるため、結果的に会社のリソースにアクセスできなくなります。 MDM なしのアプリ保護ポリシーを使用している場合、アプリは更新プログラムを受信せず、時間の経過と共にアプリのエクスペリエンスの質が低下します。



## <a name="see-also"></a>関連項目

- [過去のハイブリッド MDM 機能と通知](whats-new-hybrid-archive.md)
- [System Center 2012 Configuration Manager の MDM 向け新機能](https://technet.microsoft.com/library/mt445560.aspx)
