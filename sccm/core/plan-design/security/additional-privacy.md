---
title: "System Center Configuration Manager のプライバシーに関する声明 - Configuration Manager Cmdlet Library"
description: "System Center Configuration Manager 展開からデータを Microsoft が収集して使用する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- en-gb
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bcac4e2b6f8377a27417cb2519814ad9e74ee542

---
# <a name="additional-information-about-privacy-for-system-center-configuration-manager"></a>System Center Configuration Manager のプライバシーに関する詳細

*適用対象: System Center Configuration Manager (Current Branch)*


## <a name="updates-and-servicing"></a>更新プログラムとサービス
System Center Configuration Manager には、最新の更新プログラムと機能を適用して、Configuration Manager の展開を最新の状態に保つのに役立つ新しい更新モデルが導入されています。 この機能がインストールされると、監理者が選択するサイト サーバーに新しいサイト システムの役割が追加されます。この役割は、サービス接続ポイントと呼ばれています。 収集される情報とその用途の詳細については、本書の「使用状況データ」セクションを参照してください。


## <a name="usage-data"></a>使用状況データ
System Center Configuration Manager では、自身の診断および使用状況データが収集されます。このデータは、今後のリリースでインストールのエクスペリエンス、品質、セキュリティを向上させるために Microsoft によって使用されます。
診断および使用状況データは、それぞれの System Center Configuration Manager 階層で有効になります。 これは、各プライマリ サイトと中央管理サイトで毎週実行される SQL Server クエリで構成されます。 階層が中央管理サイトを使用している場合、プライマリ サイトからのデータはそのサイトに複製されます。 階層の最上位のサイトでは、サービス接続ポイントが、更新プログラムをチェックするときに、この情報を送信します。 サービス接続ポイントがオフライン モードの場合、情報は、サービス接続ツールを使用して転送されます。

Configuration Manager は、サイトの SQL Server データベースからのみデータを収集します。クライアントやサイト サーバーから直接データを収集することはありません。

管理者は、Configuration Manager コンソールの "利用状況データ" セクションで、収集されるデータのレベルを変更できます。

詳細については、[http://go.microsoft.com/fwlink/?LinkID=626566](http://go.microsoft.com/fwlink/?LinkID=626566) にある、使用状況データ レベルと設定に関する "詳細" 記事をご覧ください。


## <a name="customer-experience-improvement-program"></a>カスタマー エクスペリエンス向上プログラム
カスタマー エクスペリエンス向上プログラム ("CEIP") は、お使いのコンピューターのハードウェア構成とマイクロソフトのソフトウェアおよびサービスの使用方法について情報を Configuration Manager コンソールから収集し、傾向や使用パターンを分析するためのプログラムです。 また、CEIP は発生したエラーの種類と回数、ソフトウェアとハードウェアのパフォーマンス、およびサービスの速度の情報も収集します。  お客様の氏名、住所、またはその他の連絡先情報は収集しません。 お客様のコンピューターから CEIP データは収集されません。

収集した情報は、Microsoft 製品やサービスの品質、信頼性、およびパフォーマンスの向上のために役立たせていただきます。

CEIP によって収集、処理、または送信される情報については、CEIP のプライバシーに関する声明 ([http://go.microsoft.com/fwlink/?LinkID=525211](http://go.microsoft.com/fwlink/?LinkID=525211)) を参照してください。

## <a name="oms-connector"></a>OMS コネクタ
Microsoft Operations Management Suite Connector では、System Center Configuration Manager から Microsoft Operations Management Suite にコレクションなどのデータが同期されます。 Microsoft Azure サブスクリプション ID と秘密鍵は、管理者が機能を構成するときに Configuration Manager データベースに保管されます。 Azure Active Directory クライアント シークレットと Microsoft Operations Management Suite ワークスペース共有キーは、オンプレミス System Center Configuration Manager データベースに保存されます。 System Center Configuration Manager と Microsoft Operations Management Suite 間のすべての通信で HTTPS が使用されます。 無作為に選択された利用統計情報データを除き、コレクションに関する追加情報は Microsoft に提供されません。 Microsoft Operations Management Suite により収集される情報については、[http://go.microsoft.com/fwlink/?LinkId=823545](http://go.microsoft.com/fwlink/?LinkId=823545) にある、ログ分析データ セキュリティに関する詳細をご覧ください。

## <a name="asset-intelligence"></a>資産インテリジェンス
資産インテリジェンスによって、IT 管理者が構成標準への適合性を定義し、追跡して積極的に管理することができます。 物理アプリケーションおよび仮想アプリケーションの展開と使用に関するメータリング機能やレポート機能を使用して、組織は情報を十分に把握したうえでソフトウェア ライセンスに関する決定を下し、ライセンス上のコンプライアンス要件を遵守できます。 Configuration Manager クライアントから使用状況データを収集した後で、管理者は各種の機能を使用してコレクション、クエリ、レポートなどのデータを表示できます。

毎回の同期時に、既知のソフトウェアのカタログが Microsoft からダウンロードされます。 IT 管理者は、組織で検出され、調査してカタログに追加する予定の分類されていないソフトウェア タイトルに関する情報を Microsoft に送信することもできます。 この情報をアップロードする前に、アップロードされるデータの詳細な内容がダイアログ ボックスに表示されます。 アップロードされたデータを取り消すことはできません。 資産インテリジェンスからは、Microsoft にユーザーおよびコンピューターに関する情報やライセンスの使用状況は送信されません。

ソフトウェア タイトルがアップロードされると、Microsoft の調査担当者が特定および分類し、この機能を使用するすべてのお客様とカタログのその他のお客様がソフトウェアの情報を利用できるようにします。 アップロードされたすべてのソフトウェア タイトルは、そのアプリケーションの情報と分類がカタログに登録されるという点で公開という扱いになり、カタログのその他のお客様がダウンロードできるようになります。 資産インテリジェンス データの収集を構成し、Microsoft に送信する情報を決める前に、組織のプライバシーに関する要件を考慮してください。

Asset Intelligence は既定では、System Center Configuration Manager で有効になっていません。 分類されていないタイトルは自動的にアップロードされません。また、システムはこのタスクを自動化するように設計されていません。 各ソフトウェア タイトルのアップロードを手動で選択および承認する必要があります。

## <a name="endpoint-protection"></a>Endpoint Protection
Microsoft Cloud Protection Service (以前の Microsoft Active Protection Service/MAPS) 該当製品: System Center Endpoint Protection と System Center Configuration Manager の Endpoint Protection 機能 (System Center Endpoint Protection と Windows Defender for Windows 10 の管理用)。 System Center Endpoint Protection for Linux または System Center Endpoint Protection for Mac の場合、この機能は実装されていません。

Microsoft Cloud Protection Service のマルウェア対策コミュニティは、System Center Endpoint Protection のユーザーが世界各地から参加している自発的なオンライン コミュニティです。 Microsoft Cloud Protection Service に参加した場合は、System Center Endpoint Protection から情報が自動的にマイクロソフトに送信されます。マイクロソフトはこの情報を参考にして、脅威が潜んでいないかどうか調査するソフトウェアを特定し、System Center Endpoint Protection の機能強化を図ります。 このコミュニティは、悪意のある新しいソフトウェアへの大量感染の阻止に役立ちます。 Microsoft Cloud Protection Service のレポートに、Endpoint Protection クライアントが削除できる可能性があるマルウェアまたは望ましくない可能性があるソフトウェアの詳細が含まれている場合、Microsoft Cloud Protection Service がこれに対処するために最新の署名をダウンロードします。 また、Microsoft Cloud Protection Service が "誤検知" (最初はマルウェアと判断された対象がマルウェアではないと判明する場合) を検出して修正することもあります。

Microsoft Cloud Protection Service レポートには、ファイル名、暗号化ハッシュ、ベンダー、サイズ、日付スタンプなど、マルウェアの可能性があるファイルに関する情報が含まれています。 また、Microsoft Cloud Protection Service はファイルの出所を示す完全 URL を収集することがあります。 そのような URL には、検索用語やフォームに入力されたデータなど、個人情報が含まれることがあります。 望ましくないソフトウェアに関する通知が Endpoint Protection から届いたときに行った措置がレポートに含まれることもあります。 Microsoft Cloud Protection Service レポートに含まれるその情報は、マルウェアと望ましくない可能性があるソフトウェアがどの程度効率的に Endpoint Protection で検出され、駆除されるかを Microsoft が計測したり、新しいマルウェアを特定したりするときに役立ちます。

Microsoft Cloud Protection Service には、基本メンバーシップまたは上級メンバーシップのいずれかで参加できます。 基本メンバーのレポートには上記の情報が含まれています。 上級メンバーのレポートにはさらに、ソフトウェアの場所、ファイル名、ソフトウェアの動作、およびコンピューターに与える影響など、Endpoint Protection で検出されたソフトウェアに関する詳細情報が記載されます。 マイクロソフトの調査担当者は、これらのレポートを Microsoft Cloud Protection Service に参加する他の Endpoint Protection ユーザーからのレポートと併せて、新たな脅威を迅速に検知するために役立てています。 その後、分析条件を満たすプログラムについてマルウェア定義を作成し、更新した定義ファイルを Microsoft Update 経由ですべてのユーザーに提供します。

特定の種類のマルウェア感染を検知して修正するため、製品からお客様の PC のセキュリティ状態に関する情報が定期的に Microsoft Cloud Protection Service に送信されます。 この情報には、お客様の PC のセキュリティ設定や、PC の起動時に読み込まれるドライバーと他のソフトウェアを記録しているログ ファイルが含まれます。
PC を一意に識別する番号も送信されます。 また、Microsoft Cloud Protection Service が潜在的なマルウェア ファイルが接続する IP アドレスを収集することがあります。

Microsoft Cloud Protection Service レポートは、マイクロソフトのソフトウェアおよびサービスを向上させるために使用されます。 また、統計またはその他のテストや分析を行ったり、定義を生成するために使用される場合もあります。 レポートへのアクセスが与えられるのは、業務上その使用が不可欠な Microsoft の従業員、契約社員、パートナー、および製造元に限られています。

Microsoft Cloud Protection Service が意図的に個人情報を収集することはありません。 Microsoft Cloud Protection Service によって個人情報が収集された場合でも、Microsoft がその情報を使用してお客様の身元を特定したりお客様に連絡したりすることはありません。

収集されるデータに関する詳細は、[http://go.microsoft.com/fwlink/?LinkId=823547](http://go.microsoft.com/fwlink/?LinkId=823547) にある製品ドキュメントで確認できます。

## <a name="site-hierarchy-geographical-view-with-bing-maps"></a>サイト階層 – Bing Maps を使用した地図
サイト階層の地図機能では、Microsoft Bing Maps の提供する地図を使って Configuration Manager 物理サーバー トポロジを表示できます。 この機能を実現するために、お客様の入力した場所情報が、サーバーから Bing Maps の Web サービスに送信されます。

マイクロソフトではこの情報を、Microsoft Bing Maps およびその他の Microsoft のサイトとサービスを提供および向上するために役立てています。 詳細については、「Microsoft プライバシーに関する声明」(http://go.microsoft.com/fwlink/?LinkId=823548) を参照してください。
サイト階層で地図を使用しないように選択できます。 階層図では、Bing Maps サービスを使用せずに階層を表示することができます。

## <a name="microsoft-intune-subscription"></a>Microsoft Intune サブスクリプション
Microsoft Intune のサブスクリプションを購入したお客様は、Microsoft Intune を介して接続しているモバイル デバイスを Configuration Manager を使用して管理できます。 [Microsoft Online Services のプライバシーに関する声明](http://go.microsoft.com/fwlink/?LinkId=262214)は、Microsoft Intune など、Microsoft オンライン サービスに適用されます。 お客様が Microsoft Intune サブスクリプションもお持ちの場合、このプライバシーに関する声明と共に [Microsoft Online Services のプライバシーに関する声明](http://go.microsoft.com/fwlink/?LinkId=262214)もお読みください。

Microsoft Intune とのすべての通信で HTTPS が使用されます。 管理者が Microsoft Intune サブスクリプションを構成し、iOS サポートの構成に必要な Certificate Signing Request (CSR) をダウンロードするには、組織のアカウントとパスワードを使用して Microsoft Intune にサインインする必要があります。 これらの資格情報は Configuration Manager に保管されません。 Microsoft Intune とのその他の通信は、Microsoft Intune によって自動生成される PKI 証明書を使用して認証されます。

Microsoft Intune に接続されるデバイスを管理するために、一部の情報が Microsoft Intune との間で送受信されます。 この情報には、サービスに割り当てられているすべてのユーザーのユーザー プリンシパル名 (UPN) と、Microsoft Intune で管理されるデバイスのデバイス インベントリ情報が含まれます。 Manage.Microsoft.com 配布ポイントに割り当てられるコンテンツのアプリケーション名、発行元、バージョンなどのメタデータは、Microsoft Intune に送信されます。 Manage.Microsoft.com 配布ポイントに割り当てられる実際のバイナリ コンテンツは、暗号化されてから、Microsoft Intune にアップロードされます。

既定では、この機能は構成されていません。 管理者は、Manage.Microsoft.com 配布ポイントに転送される内容と、サービスに割り当てるユーザーを制御できます。 また、この機能はいつでも削除できます。



<!--HONumber=Nov16_HO1-->


