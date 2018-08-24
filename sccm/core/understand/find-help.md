---
title: ヘルプの検索
titleSuffix: Configuration Manager
description: Configuration Manager の詳細情報に関するリソースを見つけます。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e6be541a1b26961684f0577f2540132b81f50b7a
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385475"
---
# <a name="find-help-for-using-configuration-manager"></a>Configuration Manager の使用に関するヘルプの検索

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、Configuration Manager の使用に関するヘルプを検索するための複数のリソースで以下のセクションを提供します。  

- [製品ドキュメント](#bkmk_Info)  

- [製品に関するフィードバックの共有](#product-feedback)  

- [Configuration Manager チームのブログをフォローする](#BKMK_ProductGroupBlog)  

- [サポート オプションとコミュニティ リソース](#BKMK_SupportOptions)  

製品のユーザー補助機能のヘルプについては、[ユーザー補助機能](/sccm/core/understand/accessibility-features)に関するページをご覧ください。  



##  <a name="bkmk_Info"></a> 製品ドキュメント  

最新の製品ドキュメントにアクセスするには、[ライブラリのインデックス](https://docs.microsoft.com/sccm/)から開始します。  

<a name="BKMK_SearchTips"></a>  

検索、フィードバックの提供、および製品ドキュメントの使用の詳細に関するヒントについては、「[ドキュメントの使用方法](/sccm/core/understand/use-docs)」をご覧ください。  



<a name="product-feedback"></a>  

## <a name="BKMK_1806Feedback"></a> バージョン 1806 以降の製品に関するフィードバック

Configuration Manager バージョン 1806 以降では、コンソールから直接、製品に関するフィードバックを送信できます。 ログを添付する必要がある場合は、[フィードバック ハブ](#BKMK_FeedbackHub)を使用します。 次の操作を行うことができます。<!--1357542-->

  - **気に入った機能の報告**: 気に入ったもののフィードバックを送信します。
  - **問題点、改善点の報告**: 気に入らなかったもののフィードバックを送信します。
  - **提案の送信**: アイデアを共有するために [UserVoice の Web サイト](https://configurationmanager.uservoice.com/)に移動します。

![Configuration Manager 1806 でフィードバックを送信する](media/1806-send-a-smile.png)


### <a name="send-a-smile"></a>気に入った機能の報告

気に入ったもののフィードバックを送信するには、次の手順に従います。 
1. コンソールの右上隅で、スマイル マークをクリックします。 
2. ドロップダウン メニューで、**[気に入った機能の報告]** を選択します。
3. テキスト ボックスを使用して、気に入った点を説明します。 
4. 自分の電子メール アドレスとスクリーンショットを共有するかどうかを選択します。 
5. **[フィードバックの送信]** をクリックします。
     - インターネット接続がない場合は、下部にある **[保存]** ボタンをクリックします。 「[後で送信するために保存したフィードバックを送信する](#BKMK_NoInternet)」セクションに記載されている手順に従って、マイクロソフトにフィードバックを送信します。 

![Configuration Manager 1806 でフィードバック フォームを送信する](media/1806-feedback-form.png)


### <a name="send-a-frown"></a>問題点、改善点の報告

気に入らなかったもののフィードバックを送信するには、次の手順に従います。

1. コンソールの右上隅で、スマイル マークをクリックします。 
2. ドロップダウン メニューで、**[問題点、改善点の報告]** を選択します。
3. テキスト ボックスを使用して、気に入らなかった点を説明します。 
4. 自分の電子メール アドレスとスクリーンショットを共有するかどうかを選択します。 
5. **[フィードバックの送信]** をクリックします。
     - インターネット接続がない場合は、下部にある **[保存]** ボタンをクリックします。 「[後で送信するために保存したフィードバックを送信する](#BKMK_NoInternet)」セクションに記載されている手順に従って、マイクロソフトにフィードバックを送信します。  


### <a name="information-sent-with-feedback"></a>フィードバックで送信される情報
 
   - OS ビルド情報
   - Configuration Manager 階層 ID
   - 製品のビルド情報
   - 言語情報
   - デバイスの識別子 
       - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId


### <a name="BKMK_NoInternet"></a> 後で送信するために保存したフィードバックを送信する

1. **[フィードバックの提供]** ウィンドウの下部で **[保存]** をクリックします。 
2. .zip ファイルを保存します。 ローカル コンピューターにインターネット アクセスがない場合は、インターネットに接続されているコンピューターにファイルをコピーします。 
3. 必要に応じて、`cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe` にある UploadOfflineFeedback.exe をコピーします。
    - cd.latest フォルダーの詳細については、[CD.Latest フォルダー](../servers/manage/the-cd.latest-folder.md)に関するページを参照してください。

4. インターネット接続されているコンピューターで、コマンド プロンプトを開きます。 
5. 
          `UploadOfflineFeedback.exe -f c:\folder\location_of.zip` コマンドを実行します。
    
    - 任意で、次を指定できます。
        -  `-t, --timeout` データ送信のタイムアウト (秒)。 0 は制限なしです。 既定値は 30 です。
        - `-s --silent` コンソールにログを記録しない (--verbose との組み合わせは不可)
        - `-v, --verbose` 詳細なログをコンソールに出力する (--silent との組み合わせは不可)
        - `--help` ヘルプ画面の表示



##  <a name="BKMK_FeedbackHub"></a> バージョン 1802 以前の製品に関するフィードバック

製品の潜在的な欠陥は、Windows 10 に組み込まれている[フィードバック ハブ アプリ](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)を通じて報告してください。 **新しいフィードバックを追加する**場合は、必ず、**[エンタープライズ管理]** カテゴリを選択してから、以下のサブカテゴリのいずれかを選択してださい。
 - Configuration Manager クライアント
 - Configuration Manager コンソール
 - Configuration Manager OS の展開
 - Configuration Manager サーバー

Configuration Manager の新しい機能のアイデアについて投票する場合は、引き続き [UserVoice ページ](https://configurationmanager.uservoice.com/)をご利用ください。


##  <a name="BKMK_ProductGroupBlog"></a> Configuration Manager チームのブログ  

Configuration Manager のエンジニアリング チームとパートナー チームは、[Enterprise Mobility + Security ブログ](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager)を使用して、Configuration Manager と関連技術に関する技術情報やその他のニュースを提供しています。 ブログの記事は、製品ドキュメントとサポート情報を補足するものです。  


##  <a name="BKMK_SupportOptions"></a> サポート オプションとコミュニティ リソース  

次のリンクは、サポート オプションとコミュニティ リソースに関する情報を提供します。  

-   [Microsoft サポート](https://aka.ms/cmcbsupport)  

-   [Configuration Manager コミュニティ: System Center Configuration Manager (Current Branch) サバイバル ガイド](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Configuration Manager フォーラム ページ](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->