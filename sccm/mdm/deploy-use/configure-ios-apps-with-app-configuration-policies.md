---
title: Configure iOS apps with app configuration policies
titleSuffix: Configuration Manager
description: iOS 8 以降を実行しているデバイスの構成問題の解消に役立ちます。ユーザーがアプリを実行する前にアプリ構成ポリシーをユーザーに展開します。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: f0a78038-ea22-4826-9c07-1771b7dd2e8d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e5d00b1efd02d3b096a0b64033b450f0da949eeb
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32349461"
---
# <a name="apply-settings-to-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>System Center Configuration Manager でアプリ構成ポリシーを使用し、iOS アプリに設定を適用する

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager (Configuration Manager) のアプリ構成ポリシーを使用し、ユーザーがアプリを実行するときに必要となるような設定を配布できます。 たとえば、アプリで次のような詳細の指定がユーザーに要求されます。
- カスタム ポート番号
- 言語の設定
- セキュリティ設定
- 会社のロゴなど、ブランドの設定

ユーザーが設定を間違って入力すると、それを修正する負担がヘルプ デスクにかかり、アプリの展開が遅くなります。
そのような問題を回避するために、アプリ構成ポリシーを使用することで、ユーザーがアプリを実行する前に、必要な設定をユーザーに展開できます。 設定はユーザーに自動的に関連付けられています。 ユーザー側では、いかなる操作も必要ありません。
構成ポリシーをユーザーやデバイスに直接展開する代わりに、Configuration Manager でアプリ構成ポリシーを使用するには、アプリを展開するとき、ポリシーを展開の種類に関連付けます。 アプリでポリシー設定が確認されるとき (通常、アプリを初めて実行するとき)、ポリシー設定が適用されます。

現在のところ、アプリ構成ポリシーは、iOS 8 以降を実行しているデバイスのみで利用可能で、次のアプリケーションの種類をサポートします。

- **iOS 用アプリ パッケージ (*.ipa ファイル)**
- **iOS 用アプリ パッケージ (App ストア内)**

アプリのインストールの種類については、「[アプリケーション管理の概要](/sccm/apps/understand/introduction-to-application-management)」を参照してください。

## <a name="create-an-app-configuration-policy"></a>アプリ構成ポリシーを作成する

1. Configuration Manager コンソールで、**[ソフトウェア ライブラリ]**、**[アプリケーション管理]**、**[アプリ構成ポリシー]** の順に選択します。
2. **[ホーム]** タブの **[アプリ構成ポリシー]** グループで、**[新しいアプリケーション構成ポリシーを作成します]** を選択します。
3. アプリ構成ポリシーの作成ウィザードの **[全般]** ページで、ポリシーの次の情報を設定します。
  - **名前**。 ポリシーの一意の名前を入力します。
  - **説明**。 (オプション) ポリシーの識別を簡単にするために、説明を追加できます。
  - **検索とフィルター処理を向上させるために割り当てたカテゴリ**。 (オプション) カテゴリを作成し、ポリシーに割り当てるには、**[カテゴリ]** を選択します。 カテゴリを利用すると、Configuration Manager コンソールの項目を並べ替えたり、検索したりするときに便利です。
4. **[iOS ポリシー]** ページで、構成ポリシー情報の設定方法を選択します。
  - **名前と値のペアを指定します**。 入れ子を利用しないプロパティ リスト ファイルにこのオプションを利用できます。

      *名前と値のペアを指定するには*
        1. 新しいペアを追加するには、**[新規作成]** を選択します。
        2. **[名前と値のペアの追加]** ダイアログ ボックスで、次を指定します。
            - **種類**。 一覧から、指定する値の種類を選択します。
            - **名前**。 値を指定するプロパティ リスト キーの名前を入力します。
            - **値**。 入力したキーに適用する値を入力します。

  - **プロパティ リスト ファイルを参照する** アプリ構成 XML ファイルを既に用意している場合、あるいは入れ子を利用するより複雑なファイルに対してこのオプションを使用します。

    *プロパティ リスト ファイルを参照するには*

      1.  **[アプリ構成ポリシー]** フィールドで、正しい XML 形式でプロパティ リスト情報を入力します。

      XML プロパティ リストの詳細については、iOS 開発者ライブラリの [XML プロパティ リスト](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html)に関するページを参照してください。

XML プロパティ リストの形式は、構成するアプリによって異なります。 使う形式について詳しくは、アプリの供給元にお問い合わせください。
Intune は、プロパティ リストの次のデータ型をサポートしています。
            
            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
データ型の詳細については、iOS 開発者ライブラリの[プロパティ リスト](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html)に関するページを参照してください。
Intune では、プロパティ リストで次の種類のトークンもサポートします。
            
            ```
            {{userprincipalname}} - (Example: John@contoso.com)
            {{mail}} - (Example: John@contoso.com)
            {{partialupn}} - (Example: John)
            {{accountid}} - (Example: fc0dc142-71d8-4b12-bbea-bae2a8514c81)
            {{deviceid}} - (Example: b9841cd9-9843-405f-be28-b2265c59ef97)
            {{userid}} - (Example: 3ec2c00f-b125-4519-acf0-302ac3761822)
            {{username}} - (Example: John Doe)
            {{serialnumber}} - (Example: F4KN99ZUG5V2) for iOS devices
            {{serialnumberlast4digits}} - (Example: G5V2) for iOS devices
            ```

{{ 文字と }} 文字を使うことができるのはトークンの種類のみであり、他の目的には使わないでください。
            
5. 先に作成した XML ファイルをインポートするには、**[ファイルの選択]** を選択します。
6. **[次へ]** を選択します。 XML コードにエラーがある場合、続行する前に修正する必要があります。
7. ウィザードの手順を完了します。

新しいアプリ構成ポリシーが **[ソフトウェア ライブラリ]** ワークスペースの **[アプリ構成ポリシー]** ノードに表示されます。

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>アプリ構成ポリシーを Configuration Manager アプリケーションに関連付ける

アプリ構成ポリシーと iOS アプリの展開を関連付けるには、「[アプリケーションの展開](/sccm/apps/deploy-use/deploy-applications)」というトピックの手順を利用し、通常行うようにアプリを展開します。

ソフトウェアの展開ウィザードの **[アプリ構成ポリシー]** ページで、**[新規]** を選択します。 **[アプリ構成ポリシーの選択]** ダイアログ ボックスで、アプリケーションの展開の種類とそれを関連付けるアプリ構成ポリシーを選択します。
展開の種類がインストールされると、アプリ構成ポリシー設定が自動的に適用されます。

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>モバイル アプリ構成 XML ファイルの形式の例

モバイル アプリ構成ファイルを作成するとき、この形式を使用し、次の値の 1 つまたは複数指定できます。

```
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
</dict>
```
