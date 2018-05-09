---
title: SCAP のトラブルシューティング
titleSuffix: Configuraton Manager
description: 構成基準として SCAP コンプライアンス設定をインポートし、結果をエクスポートする
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 05010d73916ac4c012c157a470ed98dce47fc747
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="troubleshoot-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Microsoft System Center Configuration Manager の SCAP 拡張機能のトラブルシューティング

*適用対象: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> この機能は、Technical Preview バージョン 1803 で[プレリリース機能](/sccm/core/servers/manage/pre-release-features)として初めて導入されました。 プレリリース版の SCAP 拡張機能は、現在サポートされているバージョンの Configuration Manager Current Branch と LTSB 1606 にインストールできます。 1803 Technical Preview 以降のインストール ファイルは cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi にあります。 

Microsoft System Center Configuration Manager の SCAP 拡張機能は、SCAP データ ストリームと連携し、ACS 機能を持つ SCAP 検証ツールが USGCB をサポートするように設計されています。 通常、NIST の Web サイトからダウンロードする USGCB SCAP データ ストリームで問題は発生しません。

ただし、次の方法を使用して発生する可能性のある問題の診断とトラブルシューティングを行うことができます。

- SCAP 拡張機能クライアント (scmdcm.msi) のコンポーネントがすべてのターゲット コンピューターにインストールされていることを確認します。
- Microsoft.Sces.ScapToDcm.exe ツールのログ ファイル出力を確認します。
- SCAP 拡張機能を使用する場合の一般的な問題と解決策を確認します。
- SCAP 拡張機能に関する質問またはフィードバックを Microsoft に問い合わせます。



## <a name="review-microsoftscesscaptodcmexe-tool-log"></a>Microsoft.Sces.ScapToDcm.exe ツール ログのレビュー

Microsoft.Sces.ScapToDcm.exe ツールは、–log パラメーターが指定されると、カスタマイズされた名前付きログ ファイルを作成します。 ログ ファイルには、Microsoft.Sces.ScapToDcm.exe ツールの実行結果に関する情報が含まれています。 たとえば、ログ ファイルには、Microsoft.Sces.ScapToDcm.exe ツールの実行中に破棄またはスキップされた XCCDF/DataStream 入力ファイル内の項目の数が含まれています。

次の表に、ログ ファイルに表示される情報の一部と、情報の種類ごとの説明を示します。

### <a name="description-of-information-found-in-microsoftscesscaptodcmexe-log-files"></a>Microsoft.Sces.ScapToDcm.exe ログ ファイルで見つかった情報の説明

| 情報 | 説明 |
| --- | --- |
| 破棄 | テストの種類がサポートされているテストの種類ではないために、項目は破棄される場合があります。 |
| Skip |OVAL 定義 ID は無効なプラットフォーム用です。 </br> </br> OVAL 定義 ID は XCCDF/DataStream 入力ファイルで参照されません。</br> </br> OVAL テスト ID は XCCDF/DataStream 入力ファイルで参照されません。 </br> </br> XCCDF プロファイル ID は 1 に等しいどんな @select ステートメントも含みません。 </br> </br> XCCDF プロファイル ID は true である抽象属性を含みます。 </br> </br> XCCDF プロファイル ID は限定規則を含みません。|

## <a name="common-problems-and-solutions"></a>一般的な問題と解決策

次の表に、いくつかの一般的な問題とトラブルシューティングに役立つソリューションを示します。

表 1.6 一般的な問題と解決策

| 問題 | 解決方法 |
| --- | --- |
| 基準の何らかの**エラー**または**不明**状態があり、IE がレポートを正常に表示できない場合。 IE には「&quot;レポートは空であるか、無効です&quot;」と表示されます。 | 基準を選択し **[評価]** をクリックして基準を再実行して待機し、**準拠状態**/**最終評価の更新**を監視します。 最終評価日が現在の日付/時刻に更新された後 (評価が完了したことを意味します)、基準を選択して、レポートを再び表示します。 IE が引き続きレポートを表示できない場合、基準が大きすぎる可能性があります。 より小さな子の基準を作成するより小さなバッチ サイズを使用して、内容を再生成します。 この問題が親の基準で発生する場合は、代わりに子の基準を展開します。 |
| 所定の USGCB 設定を含むグループ ポリシー オブジェクト (GPO) を作成し、Windows 7 を実行しているコンピューターを含む組織単位 (OU) にリンクしましたが、コンプライアンス レポートには設定の一部が正しく構成されていないことが示されています。 | グループ ポリシーのアクセス許可が正しくないか、正しい OU にリンクされていない可能性があります。 ただし、より可能性が高いのは新しい設定がまだ有効になっていないことです。 既定では、Active Directory のドメインに属しているクライアント コンピューターのグループ ポリシーは、90 分おきにグループ ポリシーの更新をチェックします。 これは、ポリシーを正しく構成したにもかかわらず、設定が適用されていないように見える理由の 1 つである場合があります。 注意すべきもう 1 つの要因は、多くのコンピューターの設定を有効にするには、再起動が必要であることです。 たとえば、**システム暗号化: 暗号化、ハッシュ、署名のための FIPS 準拠アルゴリズムの使用という設定では、指定した暗号化アルゴリズムを Windows に使用させるためにはコンピューターを再起動する必要があります。 管理者特権で、コマンド プロンプトでコマンド gpupdate /force を入力することにより、グループ ポリシーの更新間隔をバイパスできます。グループ ポリシーの更新が完了したら、コンピューターを再起動してすべての設定を有効にします。 詳細については、サポート技術情報の記事 298444 の[グループ ポリシー更新ユーティリティの説明](http://support.microsoft.com/kb/298444)に関するページを参照してください。 |
| 自分の組織の情報を使用して、データベース接続を提供する場合に問題が発生します。 | データベース接続情報を構成する方法の手順については、[SCAP のインストールと構成](/sccm/compliance/plan-design/scap/install-configure-scap)に関する記事を参照してください。 

## <a name="next-step"></a>次のステップ
> [!div class="nextstepaction"]
> [SCAP 拡張機能のインストールと構成](/sccm/compliance/plan-design/scap/install-configure-scap)