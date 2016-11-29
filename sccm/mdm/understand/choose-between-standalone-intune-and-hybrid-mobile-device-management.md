---
title: "Intune スタンドアロンかハイブリッド MDM を選択する |System Center Configuration Manager"
description: "Intune と Configuration Manager を使用してハイブリッド モバイル デバイス管理を展開するか、Intune スタンドアロンを実行するかを選択します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2e6ec1b2b822298d4fa6a17e2d7439167b83080a

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Microsoft Intune スタンドアロンか System Center Configuration Manager を使用するハイブリッド モバイル デバイス管理を選択する

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Intune によるモバイル デバイス管理 (MDM) について最もよく寄せられる質問の 1 つは、"Intune と Configuration Manager を使用してハイブリッド MDM を展開すべきか、クラウドのみの構成で Intune スタンドアロンを実行すべきか" というものです。 これは重要な決断であり、実装した後は簡単に変更できません。  

 Intune スタンドアロン展開はオンプレミス インフラストラクチャを必要とせず、Web コンソールで管理されます。 迅速性があり軽量なため、クラウドファースト志向の組織に人気があります。  

 ハイブリッド MDM 展開は Intune と Configuration Manager が必要であり、経験豊富な Configuration Manager 管理者に馴染みのあるツールを使用して管理されます。 大規模な環境だけでなく、MDM や従来のクライアントの "単一画面" での管理を提供します。  

##  <a name="what-does-intune-standalone-mean"></a>Intune スタンドアロンとは  
 根本的には Intune はクラウド サービスです。 北米、ヨーロッパおよびアジアでホストされる Intune データセンターです。モバイル デバイスにセキュリティ ポリシー、電子メールと Wi-Fi プロファイル、アプリケーション、インベントリなどを提供します。  

 Intune スタンドアロン実装では、オンプレミス インフラストラクチャは必要ありません。 すべての構成、管理、展開およびレポートは、世界中のどこからでもアクセス可能な、Web ベース コンソールを介して行われます。  

 Microsoft Exchange やネットワーク デバイス登録サービス (NDES) などのオンプレミス アプリケーションで使用する場合、オンプレミス コネクタを介して Intune サービスに接続できます。  

 クラウド サービスである Intune は短期間でビルドおよび展開できます。  

##  <a name="what-does-hybrid-mdm-mean"></a>ハイブリッド MDM とは  
 Configuration Manager への投資を最大限に生かしたい組織、詳細な制御を必要とする顧客、Intune の規模の制限を超える顧客は、Intune を使用してモバイル デバイスを管理するハイブリッド実装を使用できます。  

 ハイブリッド展開には、Microsoft System Center 2012 Configuration Manager SP1 以降が必要です。  

 Intune サービスは、中央管理サイトまたは Configuration Manager 階層のプライマリ サイトにインストールされている、サービス接続ポイント サイト システムの役割 (公式には Microsoft Intune コネクタとして知られる) を使用して Configuration Manager に接続されます。 Intune テナントを接続できるのは 1 つの Configuration Manager 階層のみで、Configuration Manager 階層を接続できるのは 1 つの Intune テナントのみです。  

 ハイブリッド MDM 構成では、処理およびストレージ オーバーヘッドの一部が、オンプレミスの Configuration Manager インフラストラクチャで実行されます。 この効率向上により、ハイブリッド MDM では Intune スタンドアロンよりもさらに規模を大きくできます。  

 ハイブリッド展開では、Configuration Manager 管理者に馴染みのあるツールを使用できます。 ハイブリッド MDM が実装されている場合、モバイル デバイスでロールベースの管理制御 (RBAC)、SQL Server Reporting Services (SSRS)、およびコレクション メンバーシップ クエリを使用する複雑なデバイスとユーザーのグループ化などの高度な機能を使用できるようになります。  

##  <a name="planning-choices-and-intune-deployment-timelines"></a>計画に関する選択と Intune 展開のタイムライン  
 Intune の技術は急速に革新し、進化しています。月単位で更新され、新機能や拡張機能、拡大規模、Azure Portal の新しい管理コンソール操作、Azure Active Directory の動的グループなどが提供されます。 そのため、設計の決定の際には、製品の今後の方向性を考慮する必要があります。  

 ハイブリッド構成で現在提供されている固有の機能の多くは、サービスの短期、中期、長期の開発時に、Intune スタンドアロンで機能的にレプリケートされます。  

 スタンドアロンとハイブリッドのどちらかを選ぶ場合、展開のタイムラインを考慮する必要があります。 顧客は実稼働環境への展開準備が整うまで、設計、ビルド、ユーザー受け入れテスト、パイロット フェーズを含む複数の展開を繰り返し、多くの場合、完了するまで何か月もかかるのが普通です。 そのため、Intune 階層設計を選ぶ場合は、実際の展開の時期と、サービスの短期、中期、長期的な方向性を考慮してください。  

 進化し続ける Intune サービスに対応するために、簡単に構成を選択できるようにする必要があります。 これからは、顧客が従来のクライアントとモバイル デバイスの両方で単一の管理コンソールを必要とする場合にのみ、ハイブリッド MDM 環境を選ぶようにすべきです。  現在、スケーラビリティの向上に力を注いでいます。Azure Portal を通じたロールベース アクセスを追加し、Azure Active Directory の統合をさらに深化させ、動的グループを短中期的サービスの更新に合わせてすべて調整しています。  

 最終的には、現在の構成の選択に関係なく、スムーズにハイブリッド構成とスタンドアロン構成の選択を簡単に切り替えられるようにするためにも力を注いでいます。 現時点では、MDM 機関を切り替えるために、Microsoft サポートによる手動操作とテナントによるかなりの労力が必要になります。 これを簡単にするため、ハイブリッドと Intune スタンドアロンの共存を可能にすることを目標としています。これが実現すれば、ユーザーは 2 種類の管理間で切り替えられるため、どちらか一方を選ぶ必要がなくなります。  この変更により、サポートに問い合わせる必要があるといった今日の課題を解決でき、デバイスを登録解除して再登録する必要がなくなります。  

##  <a name="pros-and-cons-of-intune-standalone"></a>Intune スタンドアロンの長所と短所  

|長所|短所|  
|----------|----------|  
|迅速なビルドと展開<br /><br /> オンプレミス インフラストラクチャがない<br /><br /> より頻繁な更新と機能リリース<br /><br /> 習得が簡単<br /><br /> 外部で管理コンソールが使用可能|レポート機能の制限<br /><br /> セキュリティ ロールの制限<br /><br /> 外部ツール (PowerShell など) がない<br /><br /> アプリ インベントリの制限<br /><br /> 基本的なユーザーとデバイスのグループ化機能<br /><br /> Silverlight が必要|  

##  <a name="pros-and-cons-of-hybrid-mdm"></a>ハイブリッド MDM の長所と短所  

|長所|短所|  
|----------|----------|  
|拡張可能<br /><br /> 高度なツール (Configuration Manager コンソール、PowerShell、ログなど)<br /><br /> ロールベースのアクセス制御 (RBAC)<br /><br /> 詳細なレポート<br /><br /> MDM と従来のクライアントを "単一画面" で管理<br /><br /> アプリ インベントリの拡張<br /><br /> 高度なユーザーとデバイスのグループ化<br /><br /> 複数の Exchange On-premises および Exchange Online コネクタのサポート<br /><br /> 複数の NDES/CRP ロールのサポート<br /><br /> "会社所有" としてデバイスをマークできる<br /><br /> 優れたトラブルシューティング機能<br /><br /> サブスクリプションに含まれる Configuration Manager ユーザー CAL|オンプレミスの複雑さ (構成と管理)<br /><br /> 習得が難しい<br /><br /> 更新プログラムと機能リリースに必要なサービス提供<br /><br /> 追加のライセンス要件 (Windows、SQL Server など)|  

##  <a name="planning-decisions"></a>計画に関する決定事項  
 ![ハイブリッドに関する決定事項](../../mdm/understand/media/hybrid-decisions.png)  

|手順|決定事項|
|-|-|  
|<img src="media/hybrid-1.png" style="min-width:32px">|**管理予定のデバイスの数**<br /><br /> Intune スタンドアロンでは最大 50,000 台のデバイスがサポートされます。 ハイブリッド MDM では最大 300,000 台のデバイスがサポートされます。<br /><br /> 非常に大きなサイズの展開では、スタンドアロンとハイブリッド MDM のいずれの場合も、Microsoft アカウント チームに問い合わせることをお勧めします。 Microsoft アカウント チームが、規模と制限事項について詳しく説明できる Intune の専門家と連絡できるようにします。|  
|![ハイブリッド&#45;2](../../mdm/understand/media/hybrid-2.png)|**詳細なアクセス制御が必要かどうか (RBAC)**<br /><br /> ロールベースのアクセス制御 (RBAC) は、System Center 2012 Configuration Manager に追加されたものです。 RBAC では、Configuration Manager 管理者は複雑なアクセス許可セットを設計および展開し、Configuration Manager のオブジェクトと機能への管理者アクセスを制限できます。<br /><br /> Intune スタンドアロンでは、フル アクセスと読み取り専用アクセスの 2 つの管理者ロールのみが提供されます。<br /><br /> 組織で特定の管理者の適用範囲を特定のユーザー、デバイス、機能、またはオブジェクトにする必要がある場合、Configuration Manager で RBAC を使用する必要があります。<br /><br /> 組織に小規模の管理チームがあり、複雑な詳細アクセス制御を必要としない場合、セキュリティ ロールが組み込まれている Intune が最適です。|  
|![ハイブリッド&#45;3](../../mdm/understand/media/hybrid-3.png)|**詳細なレポート機能が必要かどうか**<br /><br /> Configuration Manager を使用するハイブリッド MDM には、SQL Server Reporting Services (SSRS) を使用する詳細なレポート機能が含まれます。 Configuration Manager には、34 個の組み込み MDM レポートと、400 個を超える標準的な Configuration Manager レポートが付属します。 SSRS では、管理者とビジネス アナリストは独自のカスタム レポートを作成することもできます。 さらに、Configuration Manager データベースを、オーケストレーション ツールなどの外部ツールで照会し、カスタム通知などの特定の機能を提供することができます。 Configuration Manager で実行されるすべてのレポートには、従来の PC インベントリとモバイル デバイス インベントリが共存する、非 MDM データも含まれます。<br /><br /> Intune スタンドアロンでは 9 個のレポートが提供されます。 これらのレポートはカスタマイズできません。また、入力変数も限られています。 レポートの印刷や、CSV または HTML へのエクスポートは可能です。<br /><br /> 組織が詳細なレポート機能を必要とし、SSRS を管理するための帯域幅と知識がある場合は、ハイブリッド MDM が最適です。<br /><br /> 組織で単にレポート エンジンと定義済みレポートを使用するだけの場合は、Intune スタンドアロンのレポート機能で十分です。|  
|![ハイブリッド&#45;4](../../mdm/understand/media/hybrid-4.png)|**インターネットにアクセスせずに Windows 10 デバイスを管理するかどうか**<br /><br /> Configuration Manager (現在のブランチ) では、オンプレミス インフラストラクチャのみを使用し、MDM チャネルを介して Windows 10 デバイスを管理することができます。<br /><br /> オンプレミス モバイル デバイス管理機能は、インターネットにアクセスできないクライアントを MDM で管理できるように設計されており、単一使用デバイス (キオスク デバイスなど) や IoT デバイスが主な対象です。<br /><br /> Intune スタンドアロンではクラウドのみのアプローチが使用されるため、管理対象デバイスはすべてインターネットへのアクセスが必要になります。 組織がオンプレミス モバイル デバイス管理で Windows 10 デバイスを管理する場合、ハイブリッド MDM 構成が必要です。 オンプレミス モバイル デバイス管理では、インターネットとイントラネット モバイル デバイスの両方を同時に管理できないことに注意してください。|  
|![ハイブリッド&#45;5](../../mdm/understand/media/hybrid-5.png)|**完全なアプリケーション インベントリが必要かどうか**<br /><br /> 既定では、Intune スタンドアロンで収集されるのは、Intune が管理して展開するアプリ用のアプリケーション インベントリのみです。 つまり、インベントリ レポートには、Intune ポータル サイト外のユーザーがインストールしたサイドロードされたアプリに関する情報は含まれません。<br /><br /> Configuration Manager を使用するハイブリッド MDM では、管理者は特定のデバイスを "会社所有" として指定することができます。 デバイスが会社所有デバイスとして設定されている場合、拡張アプリ インベントリが収集され、デバイスの完全なアプリ リストにアクセスできます。<br /><br /> 組織で管理対象デバイスから個人的にインストールされたアプリに関する情報が必要な場合は、ハイブリッド MDM が必要です。 この選択に基づいて決定する前に、自分自身とエンドユーザーのプライバシーへの影響を考慮してください。|  
|![ハイブリッド&#45;6](../../mdm/understand/media/hybrid-6.png)|**従来のファット クライアントのように PC を管理するかどうか**<br /><br /> スタンドアロン構成と比較した場合のハイブリッド MDM の利点の 1 つは、"単一画面" での管理です。 これは、組織が、1 つの管理ツール (つまり、Configuration Manager コンソール) からデスクトップ コンピューター、サーバー、モバイル デバイスのフリート全体を管理できることを意味します。 Configuration Manager クライアントでも、ハードウェアとソフトウェアのインベントリ、ソフトウェアの更新管理、ソフトウェアの展開、オペレーティング システムの展開などの高度な管理機能を非モバイル デバイスで使用できます。<br /><br /> 組織が従来の Windows、Linux/UNIX、および Mac クライアントの管理を望む場合、Configuration Manager は管理プラットフォームとして最適です。<br /><br /> Intune スタンドアロンでも、Intune PC 管理クライアントを使用して従来の PC 管理 (Windows 7、8.1、および 10) が提供されます。 ハードウェア インベントリ、Windows 更新、エンドポイント保護、単純なソフトウェア展開などの、基本的な PC 管理が提供されます。 クライアントは Configuration Manager を使用しないため、Intune スタンドアロンとハイブリッド MDM の両方の展開で使用できます。|  
|![ハイブリッド&#45;7](../../mdm/understand/media/hybrid-7.png)|**オンプレミス インフラストラクチャを管理するかどうか**<br /><br /> オンプレミス インフラストラクチャには、ある程度の管理オーバーヘッドと複雑さが伴います。 Configuration Manager は、インフラストラクチャを管理し、維持するためにかなりの知識、経験、投資が必要な製品です。<br /><br /> 少なくとも、ハイブリッド MDM では、データベース ロール、レポート サービス ロール、サービス接続ポイント ロールを持つ、単一の Configuration Manager プライマリ サイトが必要です。 従来の PC 管理が必要な場合、管理ポイント、配布ポイント、ソフトウェアの更新ポイント、およびアプリケーション カタログのロールも必要になる場合があります。 証明書の展開、Mac 管理、エンドポイント保護などの高度な機能にはさらに多くのロールが必要になり、より複雑になります。<br /><br /> Configuration Manager 階層には、必要に応じて、正常で機能していることを確認するために重点的な管理とメンテナンスが必要になります。<br /><br /> Configuration Manager 階層のオーバーヘッドが必要でない場合は、Intune スタンドアロン展開が最適です。|  
|![ハイブリッド&#45;8](../../mdm/understand/media/hybrid-8.png)|**外部ツールが必要かどうか**<br /><br /> Configuration Manager はエンタープライズ レベルの成熟製品であり、コンソールを使用せずにさまざまな方法でサービスと対話できます。 ハイブリッド MDM 展開では、管理者は Configuration Manager SDK または PowerShell を使用して、モバイル デバイスをプログラムで管理できます。 また、管理者は、System Center Orchestrator、PowerBI、サードパーティ製の各種アドインなどのツールを利用することもできます。<br /><br /> Intune スタンドアロン展開では、Silverlight コンソールを使用してすべての管理タスクを実行する必要があり、外部ツールは使用できません。|  
|![ハイブリッド&#45;9](../../mdm/understand/media/hybrid-9.png)|**MDM 機能の高速更新が必要かどうか**<br /><br /> Configuration Manager (現在のブランチ) で更新プログラムと機能は迅速に提供されますが、Intune などのクラウド サービスを展開すれば、運用環境の展開がさらに迅速になります。<br /><br /> Intune スタンドアロンでは、ハイブリッド MDM 展開より前に新機能が提供される場合があります。<br /><br /> 組織が最先端であるために、Intune スタンドアロンでは、適時、最新の MDM 機能を提供します。|



<!--HONumber=Nov16_HO1-->


