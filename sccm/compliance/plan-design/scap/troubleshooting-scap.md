---
title: SCAP のトラブルシューティング
titleSuffix: Configuration Manager
description: Configuration Manager の SCAP 拡張機能をトラブルシューティングする方法を説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bb3bcd0e7301ff2ef7baeff29de038cbd8476525
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383281"
---
# <a name="troubleshoot-the-scap-extensions-for-configuration-manager"></a>Configuration Manager の SCAP 拡張機能をトラブルシューティングする

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager の SCAP 拡張機能は、SCAP データ ストリームと連携し、ACS 機能を持つ SCAP 検証ツールが USGCB をサポートするように設計されています。 通常、NIST の Web サイトからダウンロードする USGCB SCAP データ ストリームで問題は発生しません。

以下の方法を使って問題の診断とトラブルシューティングを行います。  

- SCAP 拡張機能クライアント (scmdcm.msi) のコンポーネントがすべてのターゲット コンピューターにインストールされていることを確認します。  

- Microsoft.Sces.ScapToDcm.exe ツールのログ ファイル出力を確認します。  

- SCAP 拡張機能を使用する場合の一般的な問題と解決策を確認します。  

- SCAP 拡張機能に関する質問またはフィードバックを Microsoft に問い合わせます。



## <a name="review-microsoftscesscaptodcmexe-log"></a>Microsoft.Sces.ScapToDcm.exe のログを確認する

`–log` パラメーターを指定すると、Microsoft.Sces.ScapToDcm.exe ツールはカスタマイズされた名前付きログ ファイルを作成します。 ログ ファイルには、Microsoft.Sces.ScapToDcm.exe ツールの実行結果に関する情報が含まれています。 たとえば、ログ ファイルには、Microsoft.Sces.ScapToDcm.exe ツールの実行中に破棄またはスキップされた XCCDF/DataStream 入力ファイル内の項目の数が含まれています。

次の表に、ログ ファイルに表示される情報の一部と、情報の種類ごとの説明を示します。

### <a name="information-found-in-the-microsoftscesscaptodcmexe-log-file"></a>Microsoft.Sces.ScapToDcm.exe ログ ファイルで見つかる情報

| 情報 | 説明 |
| --- | --- |
| **破棄** | テストの種類がサポートされているテストの種類ではないために、項目は破棄される場合があります。 |
| **スキップ** | OVAL 定義 ID は無効なプラットフォーム用です。 </br> </br> OVAL 定義 ID は XCCDF/DataStream 入力ファイルで参照されません。</br> </br> OVAL テスト ID は XCCDF/DataStream 入力ファイルで参照されません。 </br> </br> XCCDF プロファイル ID は 1 に等しいどんな `@select` ステートメントも含みません。 </br> </br> XCCDF プロファイル ID は true である抽象属性を含みます。 </br> </br> XCCDF プロファイル ID は限定規則を含みません。|



## <a name="common-problems-and-solutions"></a>一般的な問題と解決策

トラブルシューティングの参考になるように、一般的な問題と解決策をいくつか示します。

- ベースラインに対して**エラー**または**不明**状態が表示され、Internet Explorer がレポートを正常に表示できません。 ブラウザー エラー は "レポートが空または無効です" です。  

     - ベースラインを再度実行します。 ベースラインを選択し、**[評価]** をクリックします。 そして **[Compliant State]\(準拠状態\)**/**[Last Evaluation update]\(評価の最終更新\)** が監視されるのを待ちます。 最終評価日が現在の日付/時刻に更新された後 (評価が完了したことを意味します)、基準を選択して、レポートを再び表示します。  

     - Internet Explorer が引き続きレポートを表示できない場合、基準が大きすぎる可能性があります。 より小さな子の基準を作成するより小さなバッチ サイズを使用して、内容を再生成します。  

     - この問題が親の基準で発生する場合は、代わりに子の基準を展開します。  

- 指定された USGCB 設定を含むグループ ポリシー オブジェクト (GPO) を作成しました。 それらを、Windows 7 を実行しているコンピューターを含む組織単位 (OU) にリンクしました。 コンプライアンス レポートで、一部の設定が正しく構成されていないことが示されます。  

     - グループ ポリシーのアクセス許可が正しくないか、正しい OU にリンクされていない可能性があります。  

     - より可能性が高いのは、新しい設定がまだ有効になっていないことです。 既定では、Active Directory クライアントは 90 分ごとにグループ ポリシーの更新を確認します。 このサイクルが、ポリシーを正しく構成したにもかかわらず、設定が適用されていないように見える理由の 1 つである場合があります。  

     - 多くのコンピューターの設定は、有効にするために再起動が必要です。 たとえば、**[システム暗号化: 暗号化、ハッシュ、署名のための FIPS 準拠アルゴリズムを使う]** の設定では、指定した暗号化アルゴリズムを Windows に使用させるためにはコンピューターを再起動する必要があります。 グループ ポリシーの更新間隔をバイパスするには、管理者特権のコマンド プロンプトで次のコマンドを入力します。`gpupdate /force` グループ ポリシーの更新が完了したら、コンピューターを再起動してすべての設定を有効にします。 詳しくは、「[グループ ポリシー更新ユーティリティの説明](https://support.microsoft.com/help/298444)」をご覧ください。

- 自分の組織の情報を使用して、データベース接続を提供する場合に問題が発生します。  

     - データベース接続情報を構成する方法について詳しくは、[SCAP のインストールと構成](/sccm/compliance/plan-design/scap/install-configure-scap)に関する記事をご覧ください。  
