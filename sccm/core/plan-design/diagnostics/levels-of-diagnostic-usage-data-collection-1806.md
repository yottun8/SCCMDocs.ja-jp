---
title: 1806 での診断情報と使用状況データ
titleSuffix: Configuration Manager
description: バージョン 1806 で収集される診断情報と使用状況データのレベルについて説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a0287beb-70a9-4b57-a627-e7bfba27fd3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d964295134538cf281af214830a5bc416484be51
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893673"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1806"></a>バージョン 1806 での診断の使用状況データ収集のレベル

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager バージョン 1806 では、**基本**、**エンハンス**、**フル**の 3 つのレベルの診断結果と使用状況データが収集されます。 既定では、この機能は、エンハンス レベルに設定されます。 以降のセクションでは、各レベルで収集されるデータについて詳しく説明します。

以前のバージョンからの変更は、***[新規]***、***[更新]***、***[削除]***、または ***[移動]*** で示されます。


> [!IMPORTANT]
>  Configuration Manager は、基本レベルとエンハンス レベルでは、サイト コード、サイト名、IP アドレス、ユーザー名、コンピューター名、物理アドレス、電子メール アドレスを収集しません。 フル レベルで収集したこの情報に特別な目的はありません。 ログ ファイルやメモリ スナップショットなどの詳細な診断情報に含まれる可能性があります。 Microsoft が個人の特定、連絡、広告作成の目的でこの情報を使用することはありません。



##  <a name="bkmk_change"></a> レベルを変更する方法
 管理者に指定された役割に基づいた管理スコープに、**サイト** オブジェクト クラスにおける**変更**アクセス許可が含まれる場合、その管理者は、Configuration Manager コンソールの診断結果と使用状況データの設定で収集されるデータ レベルを変更できます。

データ収集レベルの変更は、コンソールで **[管理]** > **[概要]** > **[サイトの構成]** > **[サイト]** に移動して行います。 **[階層設定]** を開き、使用するデータのレベルを選択します。  



##  <a name="bkmk_level1"></a> レベル 1 - 基本
基本レベルには階層に関するデータが含まれています。これには、インストールまたはアップグレードのエクスペリエンスを向上させるために必要なデータや、階層に適用できる Configuration Manager 更新プログラムを判断するために役立つデータが含まれます。

Configuration Manager バージョン 1806 では、このレベルには次のデータが含まれます。

- Configuration Manager コンソール接続に関する統計情報: OS のバージョン、言語、SKU とアーキテクチャ、システム メモリ、論理プロセッサの数、接続サイト ID、インストールされた .NET のバージョン、コンソールの言語パック

- アプリケーションと展開の種類の数に関する基本情報: アプリの合計、複数の展開の種類を持つアプリの合計、依存関係を持つアプリの合計、置き換えられたアプリの合計、使用中の展開テクノロジの数

- Configuration Manager サイト階層の基本データ: サイトのリスト、種類、バージョン、状態、クライアントの数、タイム ゾーン

- ***[更新]*** 基本的なデータベース構成: プロセッサー、メモリ サイズ、メモリの設定、Configuration Manager データベースの構成、Configuration Manager データベースのサイズ、クラスターの構成、および分散ビューの構成

- 探索の基本的な統計: 探索数、最小/最大/平均のグループ サイズ、およびサイトが完全に Azure Active Directory サービスを使用して実行された時間

- マルウェア対策クライアントのバージョンに関するエンドポイント保護の基本情報

- イメージの基本的な OS 展開数

- サイト システム サーバーの基本情報: 使用されるサイト システムの役割、インターネットと SSL ステータス、OS、プロセッサ、物理または仮想マシン、高可用性のサイト サーバーの使用

- Configuration Manager データベース スキーマ (すべてのオブジェクト定義のハッシュ)

- 構成された診断結果と使用状況データのレベル、オンラインまたはオフライン モード、更新プログラムの高速構成

- クライアントの言語とロケールの数

- Configuration Manager クライアント バージョン、OS バージョン、Office バージョンの数

- マネージド デバイスのオペレーティング システムおよび Exchange Connector によって設定されたポリシーの数

- Windows 10 デバイスの数 (ブランチおよびビルド別)

- Windows Update for Business を使用している Windows 10 クライアントの数  

- データベースのパフォーマンス指標: レプリケーション処理情報、プロセッサおよびディスク使用率が上位の SQL Server ストアド プロシージャ

- 配布ポイントと管理ポイントの種類および構成の基本情報: 保護済み、事前設定済み、PXE、マルチキャスト、SSL の状態、プル/ピア配布ポイント、MDM 対応、SSL 対応

- 管理コンソールのプロパティ ページとウィザードへの拡張機能のハッシュされた一覧

- セットアップ情報:
     - ビルド、インストールの種類、言語パック、有効にされた機能   

     - リリース前の使用、セットアップ メディアの種類、ブランチの種類

     - ソフトウェア アシュアランスの有効期限      

     - 更新プログラム パックの展開の状態とエラー、ダウンロードの進行状況、前提条件エラー     

     - 更新プログラムの高速リングの使用

     - アップグレード後のスクリプトのバージョン

- SQL のバージョン、Service Pack レベル、エディション、照合順序 ID、文字セット     

- 診断結果と使用状況データの統計情報: 実行時、ランタイム、エラー

- ネットワーク探索が有効であるか、無効であるか

- Azure Active Directory に参加しているクライアントの数

- 種類別に作成された段階的展開の数

- 拡張相互運用性クライアントの数

- 255 文字より長いハードウェア インベントリ プロパティのハッシュされたリスト

- ***[移動]*** 共同管理登録方法別のクライアントの数  

- ***[移動]*** 共同管理の登録に関するエラーの統計情報  

- ***[新規]*** 最も近い 3 か月の間隔までの Windows OS の経過期間によるクライアントの数  

- ***[新規]*** クライアントで使用される上位 10 のプロセッサ名  

- ***[新規]*** 主な Configuration Manager オブジェクトの数と処理速度: 探索データ レコード (DDR)、状態メッセージ、ステータス メッセージ、ハードウェア インベントリ、ソフトウェア インベントリ、および受信トレイ内のファイルの総数  

- ***[新規]*** サイト サーバーのディスクとプロセッサのパフォーマンス情報  

- ***[新規]*** Configuration Manager サイト サーバーのプロセスのアップタイムとメモリ使用量の情報  

- ***[新規]*** Configuration Manager サイト サーバーのプロセスでのクラッシュの数、および可能な場合は Watson 署名 ID  



##  <a name="bkmk_level2"></a> レベル 2 - エンハンス
エンハンス レベルはセットアップ終了後の既定値です。 このレベルには、基本レベルで収集されたデータと機能固有のデータ (頻度と使用期間)、Configuration Manager クライアントの設定 (コンポーネント名、状態、ポーリング間隔などの特定の設定)、およびソフトウェアの更新に関する基本情報が含まれます。

これが推奨レベルです。このレベルでは、製品やサービスを今後適切に改善するために最小限必要なデータを Microsoft に提供します。 このレベルでは、オブジェクト名 (サイト、ユーザー、コンピューター、またはオブジェクト)、セキュリティ関連のオブジェクトの詳細、またはソフトウェア更新プログラムを必要とするシステムの数などの脆弱性は収集されません。

Configuration Manager バージョン 1806 では、このレベルには次のデータが含まれます。

### <a name="application-management"></a>アプリケーション管理  

   - アプリの要件: 展開テクノロジで参照される組み込み条件の数

   - アプリの置き換え、チェーンの最大深度

   - アプリケーション承認の統計情報と使用頻度

   - アプリケーションのコンテンツ サイズの統計情報

   - アプリケーションの展開情報: インストール/アンインストールの使用、承認が必要、ユーザーの介入が有効/無効、依存関係、置き換え、インストールの権限機能の使用回数  

   - アプリケーション ポリシーのサイズと複雑さの統計情報

   - 使用可能なアプリケーション要求の統計

   - パッケージとプログラムの基本的な構成情報: 展開オプションとプログラムのフラグ

   - 展開の種類の使用状況/ターゲットに関する基本情報: 対象となるユーザー/デバイス、必須/使用可能、ユニバーサル アプリ

   - App-V 環境と展開のプロパティの数

   - アプリケーションへの適用の数 (OS 別)  

   - タスク シーケンスによって参照されているアプリケーションの数

   - アプリケーション カタログの個別のブランドの数

   - ダッシュボードを使用して作成された Office 365 アプリケーションの数

   - パッケージの数 (種類別)  

   - パッケージ/プログラムの展開の数  

   - Windows 10 ライセンスが供与されたアプリケーションのライセンスの数  

   - Windows インストーラーの展開の種類の数 (アンインストール コンテンツの設定別)

   - ビジネス向け Microsoft ストア アプリの数と同期の統計情報: 集計されたアプリの種類、ライセンスされたアプリの状態、オンラインおよびオフラインのライセンスされたアプリ数  

   - メンテナンス期間の種類と期間  

   - 時間帯あたりのユーザーまたはデバイスあたりのアプリケーション展開数の最小/最大/平均値

   - 特に一般的なアプリケーション インストール エラー コード (展開テクノロジ別)

   - MSI 構成オプションとカウント

   - 必要なソフトウェア展開に関する通知に対するエンドユーザー操作の統計情報   

   - Universal Data Access の使用状況、作成方法

   - 集計されたユーザーとデバイスのアフィニティの統計情報 

   - デバイスごとのプライマリ ユーザーの最大および平均数  

   - ***[新規]*** 種類別のアプリケーションのグローバル条件の使用状況  

   - ***[新規]*** ソフトウェア センターのカスタマイズ構成  

   - ***[新規]*** パッケージ変換マネージャーの前提条件と数  

   - ***[新規]*** 種類別のアプリケーションの検出方法の数  

   - ***[新規]*** アプリケーションの実施エラーの数  

   - ***[新規]*** MSI インストーラーのプロパティ 

   - ***[新規]*** ユーザーのインストール要求の統計情報



### <a name="client"></a>クライアント  

   - Active Management Technology (AMT) クライアント バージョン

   - BIOS の動作時間 (年単位)

   - セキュア ブートが有効になっているデバイスの数

   - TPM の状態ごとのデバイスの数

   - クライアントの自動アップグレード: クライアントのパイロット運用、除外使用状況を含む展開の構成 (拡張相互運用性クライアント)

   - クライアントのキャッシュ サイズ構成

   - クライアント展開のダウンロード エラー

   - ***[更新]*** クライアントの正常性の統計情報とクライアントのバージョン別の主要な問題のまとめ

   - クライアント通知操作の動作状態: それぞれの実行回数、対象となるクライアントの最大数、平均の成功率

   - クライアント インストールの数 (ソースの場所の種類別)  

   - クライアント インストール エラーの数  

   - Hyper-V または Azure で仮想化されたデバイスの数  

   - ソフトウェア センターのアクションの数   

   - UEFI 対応デバイスの数

   - クライアントで使用される展開方法、展開方法ごとのクライアントの数

   - 有効なクライアント エージェントの一覧/数  

   - OS の動作時間 (月単位)

   - ハードウェア インベントリ クラス、ソフトウェア インベントリ ルール、およびファイル収集規則の数

   - デバイス正常性構成証明書の統計情報: 最も一般的なエラー コード、オンプレミス サーバーの数、さまざまな状態のデバイスの数

   - 既定のブラウザーごとのデバイスの数  

   - ***[新規]*** Configuration Manager で生成されたサーバー認証証明書の数  

   - ***[新規]*** モデル別の Microsoft Surface デバイスの数  


### <a name="cloud-services"></a>Cloud Services  

  - Azure Active Directory の検出に関する統計情報

  - クラウド管理ゲートウェイの構成と使用状況の統計情報: リージョンと環境の数、認証/承認の統計情報

  - Configuration Manager に接続されている Azure Active Directory アプリケーションとサービスの数

  - Azure Log Analytics に同期されているコレクションの数

  - Upgrade Analytics コネクタの数

  - Azure Log Analytics クラウド コネクタが有効になっているかどうか  

  - ***[新規]*** クラウド配布ポイントをソースの場所として使ったプル配布ポイントの数  


### <a name="co-management"></a>共同管理  
  - 共同管理の集計された使用状況の統計情報: 登録されているクライアントの数、ポリシーを受信するクライアント、ワークロードの状態、パイロット/除外のコレクション サイズ、登録エラー  

  - 登録スケジュールと履歴の統計情報  

  - 共同管理対象のクライアントの数  

  - 関連する Microsoft Intune テナント


### <a name="collections"></a>コレクション  

   - コレクション ID の使用状況 (ID が不足していない)

   - コレクションの評価統計情報: クエリ時間、割り当て数/未割り当て数、種類別の数、ID のロールオーバー、規則の使用状況

   - 展開なしのコレクション


### <a name="compliance-settings"></a>コンプライアンス設定  

  - 構成基準の基本情報: 数、展開数、参照数

  - コンプライアンス ポリシー エラーの統計情報

  - 構成アイテムの数 (種類別)  

  - 修復設定を含む、組み込み設定を参照する展開の数  

  - 修復設定を含む、カスタム設定に対して作成された規則および展開の数  

  - 展開された Simple Certificate Enrollment Protocol (SCEP)、VPN、Wi-Fi、証明書 (.pfx)、コンプライアンス ポリシー テンプレートの数

  - SCEP 証明書、VPN、Wi-Fi、証明書 (.pfx)、プラットフォーム別のコンプライアンス ポリシー展開の数

  - Windows Hello for Business ポリシー (作成済み、展開済み)  

  - ***[新規]*** 展開済みの Microsoft Edge ブラウザー ポリシーの数  


### <a name="content"></a>Content  

  - 境界グループの統計情報: 高速の数、低速の数、グループあたりの数、フォールバック リレーションシップ

  - 境界グループの情報: 各境界グループに割り当てられた境界とサイト システムの数  

  - 境界グループのリレーションシップとフォールバックの構成

  - クライアント コンテンツのダウンロードの統計

  - 境界の数 (種類別)  

  - ピア キャッシュ クライアントの数、使用状況の統計情報、および部分的なダウンロードの統計情報

  - 配布マネージャーの構成情報: スレッド、再試行の待ち時間、再試行回数、プル配布ポイントの設定  

  - 配布ポイントの構成情報: ブランチ キャッシュの使用、配布ポイントの監視

  - 配布ポイント グループの情報: 各配布ポイント グループに割り当てられたパッケージと配布ポイントの数  

  - ***[新規]*** コンテンツ ライブラリの種類、ローカルまたはリモートのいずれであるか  


### <a name="endpoint-protection"></a>Endpoint Protection  

   - Windows Advanced Threat Protection (ATP) ポリシー: ポリシーの数、ポリシーが展開されているかどうか

   - エンドポイント保護機能用に構成されたアラートの数  

   - エンドポイント保護ダッシュボードに表示するように選択されたコレクションの数  

   - Windows Defender Exploit Guard ポリシー、展開、および対象クライアントの数

   - エンドポイント保護の展開エラー、エンドポイント保護ポリシーの展開エラー コードの数  

   - Endpoint Protection のマルウェア対策および Windows ファイアウォール ポリシーの使用状況 (グループに割り当てられている固有のポリシーの数)<br /><br /> このデータには、ポリシーに含まれている設定に関する情報は含まれません。  


### <a name="migration"></a>移行  

  - 移行されたオブジェクト (移行ウィザードを使用) の数


### <a name="mobile-device-management-mdm"></a>モバイル デバイス管理 (MDM)  

   - 発行されたモバイル デバイス アクションの数: 各種コマンド (ロック、ピン留め、ワイプ、インベントリからの削除、今すぐ同期)

   - モバイル デバイス ポリシーの数  

   - Configuration Manager および Microsoft Intune によって管理されるモバイル デバイスの数と、そのデバイスの登録方法 (一括、ユーザー ベース)  

   - 複数の登録済みモバイル デバイスを持つユーザーの数  

   - モバイル デバイスのポーリング スケジュールと統計情報、モバイル デバイスのチェックイン期間  


### <a name="microsoft-intune-troubleshooting"></a>Microsoft Intune のトラブルシューティング  

   - Microsoft Intune にレプリケートされたデバイス アクション (ワイプ、インベントリからの削除、ロック)、使用状況データ、およびデータ メッセージの数とサイズ

   - 状態、ステータス、インベントリ、RDR、DDR、UDX、テナントの状態、POL、LOG、証明書、CRP、再同期、CFD、RDO、BEX、ISM、および Microsoft Intune からダウンロードされたコンプライアンス メッセージの数とサイズ

   - Microsoft Intune のユーザー同期に関する完全な統計とデルタ統計


### <a name="on-premises-mobile-device-management-mdm"></a>オンプレミス モバイル デバイス管理 (MDM)  

   - Windows 10 一括登録パッケージおよびプロファイルの数  

   - オンプレミス MDM アプリケーション展開に関する展開成功/失敗の統計情報  


### <a name="os-deployment"></a>OS の展開  

   - ブート イメージ、ドライバー、ドライバー パッケージ、マルチキャスト対応の配布ポイント、PXE 対応の配布ポイント、およびタスク シーケンスの数  

   - Configuration Manager クライアント バージョン別のブート イメージの数

   - Windows PE バージョン別のブート イメージの数

   - エディション アップグレード ポリシーの数

   - PXE から除外されたハードウェア識別子の数

   - OS バージョン別の OS 展開の数

   - 時間経過による OS アップグレードの数

   - コンテンツを事前にダウンロードするオプションを使用したタスク シーケンスの展開の数

   - タスク シーケンス ステップの使用数

   - インストールされている Windows ADK のバージョン  

   - ***[新規]*** イメージのサービス タスクの数  


### <a name="site-updates"></a>サイトの更新プログラム  

   - インストールされた Configuration Manager 修正プログラムのバージョン


### <a name="software-updates"></a>ソフトウェア更新プログラム  

   - 自動展開規則で使用される使用可能なデルタと期限デルタ  

   - 更新プログラムあたりの割り当て数の平均/最大値  

   - クライアント更新の評価とスキャンのスケジュール  

   - ソフトウェアの更新ポイントで同期される分類

   - クラスターの修正プログラム適用の統計情報  

   - Windows 10 高速更新プログラムの構成

   - アクティブな Windows 10 サービス プランに使用される構成  

   - 展開された Office 365 更新プログラムの数  

   - 同期されている Microsoft Surface ドライバーの数

   - 更新プログラムのグループと割り当ての数  

   - 更新プログラム パッケージの数と、パッケージの対象配布ポイント数の最大/最小/平均値  

   - System Center Update Publisher で作成および展開された更新プログラムの数  

   - 作成および展開されている Windows Update for Business ポリシーの数

   - Windows Update for Business 構成の集計された統計

   - 同期に関連付けられた自動展開規則の数  

   - 新しく作成する、または更新プログラムを既存のグループに追加する自動展開規則の数  

   - 複数の展開を含む自動展開規則の数  

   - 更新プログラム グループの数と、グループあたりの更新プログラム数の最小/最大/平均値  

   - 更新プログラムの数と、展開済み、期限切れ、置き換え済み、ダウンロード済み、および EULA を含む更新プログラムの割合  

   - ソフトウェア更新ポイントの負荷分散の統計情報

   - ソフトウェアの更新ポイントの同期スケジュール  

   - ソフトウェア更新プログラムの展開が含まれるコレクション数の合計/平均値、および展開された更新プログラム数の最大/平均値  

   - 更新スキャン エラー コードとマシンの数  

   - Windows 10 ダッシュボードのコンテンツ バージョン  

   - ***[新規]*** サードパーティのソフトウェア更新プログラム カタログのサブスクリプションの数と使用状況  

   - ***[新規]*** コンテンツありの場合とコンテンツなしの場合で展開されたソフトウェア更新プログラムの数  


### <a name="sqlperformance-data"></a>SQL/パフォーマンス データ  

   - サイトの概要の構成および期間

   - 最大データベース テーブルの数  

   - 探索の運用統計 (見つかったオブジェクトの数)

   - 探索の種類、有効化、スケジュール (完全、増分)

   - SQL AlwaysOn レプリカ情報、使用状況、正常性の状態

   - SQL 変更の追跡のパフォーマンスの問題、保有期間、自動クリーンアップの状態

   - SQL の変更の追跡の保有期間

   - 特に一般的な、および特に費用の高いメッセージの種類を含む、状態およびステータス メッセージのパフォーマンス統計情報


### <a name="miscellaneous"></a>その他  

   - 同期スケジュールと平均時間を含む、データ ウェアハウス サービス ポイントの構成

   - スクリプトと実行の統計情報の数

   - Wake On LAN (WOL) サイトの数

   - 使用状況とパフォーマンスの統計情報のレポート
  
   - 段階的展開の使用状況の統計  

   - ***[新規]*** CMPivot の使用状況の統計  

   - ***[新規]*** 管理分析情報の項目数と進行状況  

   - ***[新規]*** サイト サーバー上の非 Configuration Manager の固有のプロセスでのクラッシュの数、および可能な場合は Watson 署名 ID



##  <a name="bkmk_level3"></a> レベル 3 - フル
フル レベルには、基本レベルとエンハンス レベルのすべてのデータが含まれます。 また、Endpoint Protection の詳細情報、更新プログラムの対応率、およびソフトウェア更新プログラム情報も含まれています。 このレベルには、キャプチャ時にメモリやログ ファイルに存在していた、個人情報が含まれる可能性があるシステム ファイルやメモリ スナップショットなどの詳細な診断情報を含めることもできます。

Configuration Manager バージョン 1806 では、このレベルには次のデータが含まれます。

- 自動展開規則の評価スケジュールの情報

- ATP の正常性の概要

- コレクションの評価および更新の統計情報

- コンプライアンスとエラーでのコンプライアンス ポリシーの統計情報

- コンプライアンス設定: SCEP、VPN、Wi-Fi、コンプライアンス ポリシー テンプレートの構成の詳細

- System Center Configuration Manager の DCM 構成パックの使用状況

- クライアント展開のインストール エラーの詳細

- Endpoint Protection の正常性の概要: 保護済み、危険、不明、未サポート クライアントの数を含む

- Endpoint Protection ポリシーの構成

- アプリケーションのインストール権限を使用して構成されたプロセスの一覧

- 最後のソフトウェア更新プログラムのスキャンが実行されてからの経過時間の最小/最大/平均値

- ソフトウェア更新プログラムの展開コレクションの非アクティブなクライアント数の最小/最大/平均値

- パッケージあたりのソフトウェア更新プログラム数の最小/最大/平均値

- MSI 製品コードの展開の統計情報 

- ソフトウェア更新プログラムの展開の全体的なコンプライアンス対応状況

- 期限切れのソフトウェア更新プログラムが含まれるグループの数

- ソフトウェア更新プログラムの展開のエラー コードと数

- ソフトウェア更新プログラムの展開情報: クライアントと UTC 時刻の対象となっている展開の割合、必須/オプション/サイレント、再起動抑制

- ソフトウェアの更新ポイントで同期されるソフトウェア更新プログラムの製品

- ソフトウェア更新プログラムのスキャン成功の割合

- 環境内の上位 50 の CPU

- Microsoft Intune で管理されるデバイス向けの Exchange Active Sync (EAS) 条件付きアクセス ポリシーの種類 (ブロックまたは検疫)

- ビジネス向け Microsoft ストア アプリケーションの詳細: AppID、オンライン状態またはオフライン状態、合計購入ライセンス数を含む、同期したアプリケーションの非集計リスト
