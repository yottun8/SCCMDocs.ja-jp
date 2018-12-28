---
title: アプリ構成ポリシーを使用した Android for Work アプリの構成
titleSuffix: Configuration Manager
description: ユーザーがアプリを実行する前にアプリ構成ポリシーをユーザーに展開すると、Android for Work を実行しているデバイスの構成の問題を解消するのに役立ちます。
ms.date: 09/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9126d188-7780-45a4-b21d-7fcf4fad7da2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6f83f26f746c54e3d1defe31df47b3c7c8a7e117
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417950"
---
# <a name="apply-settings-to-android-for-work-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>System Center Configuration Manager でアプリ構成ポリシーを使用し、Android for Work アプリに設定を適用する

*適用対象します。System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のアプリ構成ポリシーを使用し、ユーザーがアプリを実行するときに必要となるような設定を配布できます。 たとえば、アプリで次のような詳細の指定がユーザーに要求されます。
- カスタム ポート番号
- 言語の設定
- セキュリティ設定
- 会社のロゴなど、ブランドの設定

ユーザーが設定を間違って入力すると、それを修正する負担がヘルプ デスクにかかり、アプリの展開が遅くなります。 そのような問題を回避するために、アプリ構成ポリシーを使用することで、ユーザーがアプリを実行する前に、必要な設定をユーザーに展開できます。 設定はユーザーに自動的に関連付けられています。 ユーザー側では、いかなる操作も必要ありません。
構成ポリシーをユーザーやデバイスに直接展開する代わりに、アプリを展開するときに、ポリシーを展開の種類に関連付けます。 アプリでポリシー設定が確認されるたびに (通常はアプリの初回実行時)、ポリシー設定が適用されます。

Android アプリ構成ポリシーは、Android for Work を実行しているデバイス上でのみ使用できます。 アプリ構成ポリシーは、Play for Work ストアから承認されたアプリに適用されます。 Android のボリューム購入アプリに関する詳細については、[アプリを Android for Work デバイスに展開する方法](https://docs.microsoft.com/intune/deploy-use/android-for-work-apps)に関するページをご覧ください。

アプリのインストールの種類については、「[アプリケーション管理の概要](/sccm/apps/understand/introduction-to-application-management)」を参照してください。

## <a name="create-an-app-configuration-policy"></a>アプリ構成ポリシーを作成する

1. Configuration Manager コンソールで、**[ソフトウェア ライブラリ]** > **[アプリケーション管理]** > **[アプリ構成ポリシー]** の順に選択します。
2. **[ホーム]** タブの **[アプリ構成ポリシー]** グループで、**[アプリケーション構成ポリシーを作成します]** を選択します。
3. アプリ構成ポリシーの作成ウィザードの **[全般]** ページで、ポリシーの次の情報を設定します。
   - **名前**。 ポリシーの一意の名前を入力します。
   - **説明**。 (オプション) ポリシーの識別を簡単にするために、説明を追加できます。
   -  **構成ポリシーの種類を選択します**。 アプリ構成ポリシーの対象とするプラットフォームを指定します。**Android for Work アプリ構成ポリシー**します。
   -  **検索とフィルター処理を向上させるために割り当てたカテゴリ**。 (オプション) カテゴリを作成し、ポリシーに割り当てるには、**[カテゴリ]** を選択します。 カテゴリを利用すると、Configuration Manager コンソールの項目を並べ替えたり、検索したりするときに便利です。
4. **[Android for Work ポリシー]** ページで、構成ポリシー情報の設定方法を選択します。
   - **名前と値のペアを指定します**。 入れ子を利用しないプロパティ リスト ファイルにこのオプションを利用できます。 名前と値のペアを指定するには
        1. 新しい JSON ペアを追加するには、**[新規作成]** を選択します。
        2. **[名前と値のペアの追加]** ダイアログ ボックスで、次のように詳細を指定します。
            - **種類**。 一覧から、指定する値の種類を選択します。
            - **名前**。 値を指定するプロパティ リスト キーの名前を入力します。
            - **値**。 入力したキーに適用する値を入力します。

   - **プロパティ リスト JSON ファイルを参照します**。 アプリ構成 JSON ファイルを既に用意している場合、あるいは入れ子を利用する、より複雑なファイルに対してはこのオプションを使用します。 **[アプリ構成ポリシー]** フィールドで、正しい JSON 形式でプロパティ リスト情報を入力します。
5. 先に作成した JSON ファイルをインポートするには、**[ファイルの選択]** を選択します。
6. **[次へ]** を選択します。 JSON コードにエラーがある場合、続行する前に修正します。
7. ウィザードの手順を完了します。

新しいアプリ構成ポリシーが **[ソフトウェア ライブラリ]** ワークスペースの **[アプリ構成ポリシー]** ノードに表示されます。

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>アプリ構成ポリシーを Configuration Manager アプリケーションに関連付ける

アプリ構成ポリシーと Android for Work アプリの展開を関連付けるには、「[アプリケーションの展開](/sccm/apps/deploy-use/deploy-applications)」トピックの手順に従い、通常どおりにアプリを展開します。

ソフトウェアの展開ウィザードの **[アプリ構成ポリシー]** ページで、**[新規]** を選択します。 **[アプリ構成ポリシーの選択]** ダイアログ ボックスで、アプリケーションの展開の種類とそれを関連付けるアプリ構成ポリシーを選択します。
展開の種類がインストールされると、アプリ構成ポリシー設定が自動的に適用されます。
