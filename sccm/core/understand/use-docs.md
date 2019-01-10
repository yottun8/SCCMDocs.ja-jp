---
title: ドキュメントの使用方法
titleSuffix: Configuration Manager
description: Configuration Manager テクニカル ドキュメント ライブラリの使用に関するヒントについて説明します。
ms.date: 09/07/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 27eea5c93ec66207e48390e3c7a0352a3a255ceb
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424739"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>Configuration Manager ドキュメントの使用方法

*適用対象:System Center Configuration Manager (Current Branch)*

この記事の各セクションでは、Configuration Manager ドキュメント ライブラリの使用に関する複数のリソースとヒントを紹介しています。  

- [検索方法](#bkmk_searchtips)  

- [ドキュメント バグ、改善、質問、新しいアイデアを送信する](#bkmk_docfeedback)  

- [変更通知を取得する方法](#bkmk_notifications)  

- [ドキュメントに寄稿する方法](#bkmk_contribute)  


製品の全般的なヘルプについては、「[ヘルプの検索](/sccm/core/understand/find-help)」を参照してください。


##  <a name="bkmk_searchtips"></a> 検索   
 必要な情報を検索するときに、以下の検索のヒントをご覧ください。  

-   任意の検索エンジンで Configuration Manager のコンテンツを見つけるとき、検索キーワードと共に `SCCM` を含めます。  

    - docs.microsoft.com からの結果で Configuration Manager Current Branch を探します。 technet.microsoft.com または msdn.microsoft.com からの結果は、以前の製品バージョンが対象になります。  

    - さらに検索結果を現在のコンテンツ ライブラリに絞るには、`site:docs.microsoft.com` を含め、検索エンジンの範囲を指定します。  

-   ユーザー インターフェイスとオンライン ドキュメントの用語と一致する検索用語を使用します。 コミュニティ コンテンツで見られる非公式な用語や略語は使用しないでください。 たとえば、「MP」ではなく「管理ポイント」、「DT」ではなく「展開の種類」、「SUM」ではなく「ソフトウェア更新プログラム」のように検索します。  

-   現在表示されている記事の中で検索するには、ブラウザーの**検索**機能を使用します。 ほとんどの最新 Web ブラウザーで、**Ctrl**+**F** キーを押し、検索語句を入力します。  

-   docs.microsoft.com の各記事には、コンテンツの検索を支援するため、次のフィールドが含まれています。  

    - **[検索]**: 右上隅にあります。 すべての記事を検索するには、このフィールドに語句を入力します。 Configuration Manager ライブラリ内の記事には、"ConfigMgr" スコープが自動的に含まれます。  

    - 左側の目次の上で**タイトル別にフィルター処理**します。 現在の目次を検索するには、このフィールドに語句を入力します。 このフィールドは、現在のノードに関してのみ、記事のタイトルに表示される語句と一致します。 たとえば、コア インフラストラクチャやアプリケーション管理が検索されます。  

- 見つけられない項目がありますか。 [フィードバックを送信してください。](#bkmk_docfeedback) 問題を投稿される場合、お使いの検索エンジン、お試しになったキーワード、検索対象の記事をお伝えください。 このフィードバックは、Microsoft がコンテンツを最適化し、より良い検索を実現するために役立ちます。  



## <a name="bkmk_docfeedback"></a> フィードバック

記事の右上にある **[フィードバック]** リンクをクリックし、一番下の [フィードバック] セクションに進みます。 このセクションは GitHub Issues と統合されています。 GitHub Issues との統合の詳細については、[ドキュメント プラットフォームのブログの投稿](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs)に関するページを参照してください。

Configuration Manager 製品自体のフィードバックを投稿するには、**[製品のフィードバック]** をクリックしてください。 詳細については、「[製品に関するフィードバック](/sccm/core/understand/find-help#product-feedback)」を参照してください。 

ドキュメントに関するフィードバックを送信するには、[GitHub アカウント](https://github.com/join)が必要です。 サインイン後、MicrosoftDocs の 1 回限りの承認を受けます。 次に **[コンテンツに関するフィードバック]** をクリックし、タイトルとコメントを入力し、**[フィードバックの送信]** をクリックします。 このアクションによって、[SCCMdocs リポジトリ](https://github.com/MicrosoftDocs/SCCMdocs/issues)に対象記事の新しい問題が提出されます。

この統合によって、対象記事に未処理または終了済みの問題があればそれも表示されます。 表示された場合、確認してから新しい問題を送信してください。 関連する問題が見つかった場合、顔アイコンをクリックして意見を追加します。あるいは、問題を展開してコメントを追加できます。 

#### <a name="types-of-feedback"></a>フィードバックの種類
GitHub Issues を使用し、次の種類のフィードバックを送信します。
- ドキュメント バグ:内容が古い、はっきりしない、紛らわしい、あるいは不完全です。
- ドキュメント改善:記事を良くするための提案。
- ドキュメント質問:既存のドキュメントが見つからず、困っています。
- ドキュメント アイデア:新しい記事の提案。 ドキュメントに関するフィードバックとして、UserVoice の代わりにこの方法を使用します。
- 称賛:情報が役立った記事に関する好意的なフィードバック。
- ローカリゼーション:コンテンツの翻訳に関するフィードバック。
- 検索エンジン最適化 (SEO):コンテンツを検索できない問題に関するフィードバック。 コメントには、検索エンジン、キーワード、対象記事を含めます。

[製品フィードバック](/sccm/core/understand/find-help#product-feedback)、[製品質問](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)、[サポート依頼](https://aka.ms/cmcbsupport)など、ドキュメント以外のトピックで問題が投稿された場合、その問題は完了とされ、ユーザーはその問題の本来のフィードバック チャンネルにリダイレクトされます。

docs.microsoft.com プラットフォームに関するフィードバックを投稿するには、[ドキュメント フィードバック](https://aka.ms/sitefeedback)に関するページをご覧ください。 このプラットフォームには、見出し、目次、右側のメニューなど、すべてのラッパー コンポーネントが含まれています。 また、フォント、アラート ボックス、ページ アンカーなど、ブラウザーで記事をレンダリングする方法も含まれています。



## <a name="bkmk_notifications"></a> 記事

ドキュメント ライブラリの内容が変わったときに通知を受け取るには、次の手順を使用します。

1. [ドキュメント検索](https://docs.microsoft.com/search/index?scope=ConfigMgr)を使用し、1 件または一連の記事を見つけます。 次に例を示します。
    - タイトルが["Log files for troubleshooting - Configuration Manager"](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr) という 1 件の記事を検索します
    - [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr) に関するあらゆる記事を検索します
2. 右上隅にある **RSS** リンクをクリックします。 
3. あらゆる RSS アプリケーションでこのフィードを利用し、検索結果に変更があったときに通知を受け取ることができます。


> [!Tip]  
> GitHub で [SCCMdocs リポジトリ](https://github.com/MicrosoftDocs/SCCMdocs)の**推移を観察する**こともできます。 この方法ではたくさんの通知が生成されます。 また、Microsoft で使用されるプライベート リポジトリからの変更は含まれません。  



## <a name="bkmk_contribute"></a> 投稿

Configuration Manager ドキュメント ライブラリは、docs.microsoft.com のほとんどのコンテンツと同様に、GitHub ではオープンソースになっています。 このライブラリは、コミュニティの寄稿を受け入れ、奨励しています。 概要については、[投稿に関するガイド](https://docs.microsoft.com/contribute) ページをご覧ください。 [GitHub アカウント](https://github.com/join)の作成が唯一の前提条件です。

#### <a name="basic-steps-to-contribute-to-sccmdocs"></a>SCCMdocs に寄稿するための基本手順
1. 対象記事で **[編集]** をクリックします。 GitHub でソース ファイルが開きます。  

2. ソース ファイルを編集するには、鉛筆アイコンをクリックします。  

3. マークダウン ソースで変更を加えます。 詳細については、「[How to use Markdown for writing Docs](https://docs.microsoft.com/contribute/how-to-write-use-markdown)」 (ドキュメントの記述にマークダウンを使用する方法) を参照してください。  

4. ファイル変更の提案セクションで、公開コミット コメントを入力し、自分が "変更した内容" を説明します。 **[Propose file change]\(ファイル変更の提案\)** をクリックします。  

5. 下にスクロールし、行った変更を確認します。 **[pull request の作成]** をクリックし、フォームを開きます。 この変更を行った "理由" を説明します。 記事の作成者のタグを付け、確認を求めます。 **[pull request の作成]** をクリックします。  


### <a name="what-to-contribute"></a>貢献できること

投稿に関心があるがどこから始めればよいかわからない場合は、以下の提案をご覧ください。  

- 問題の一覧を見て、コミュニティ宛てのラベルを探します。  
  - [good-first-issue](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)   
  - [help-wanted](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    このようなラベルは、コミュニティの貢献が求められる問題に対して Microsoft の作成者が割り当てるものです。  

- 記事の正しさを確認します。 `mm/dd/yyyy` 形式で **ms.date** メタデータを更新します。 このような貢献によって、コンテンツが新しい状態で維持されます。  

- 自分の経験に基づき、説明、例、手本を追加します。 このような貢献によって、コミュニティの力が利用され、知識が共有されます。   

- 英語以外の言語の翻訳を訂正します。 このような貢献によって、ローカライズされたコンテンツの有用性が上がります。  

> [!Note]  
> Microsoft の従業員でない場合、規模の大きい投稿を行うには貢献者使用許諾契約書 (CLA) に署名する必要があります。 GitHub では、投稿がしきい値に達すると自動的にこの契約への署名が求められます。  


### <a name="tips"></a>ヒント

Configuration Manager のドキュメントに投稿する場合、次の一般的なガイドラインに従ってください。

- いきなり大規模な pull requests を行わないでください。 そうではなく、[問題を報告](https://docs.microsoft.com/sccm/core/understand/use-docs#bkmk_docfeedback)してディスカッションを開始してください。 これで、大量の時間を費やす前にその方向性が正しいかどうか確認できます。  

- [Microsoft スタイル ガイド](https://aka.ms/MicrosoftStyle)をご覧ください。 [Microsoft のスタイルとボイスに関する 10 のヒント](https://docs.microsoft.com/style-guide/top-10-tips-style-voice)を把握してください。  

- 作業の出発点として[pull request のテンプレート](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md)を使用してください。  

- [GitHub Flow ワークフロー](https://guides.github.com/introduction/flow/)に従ってください。  

- ご自身の投稿について、ブログやツイート (その他何でも) を使ってたくさん報告しましょう。  

(この一覧は、[.NET の投稿に関するガイド](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts)から借用されたものです。)
