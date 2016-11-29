---
title: "アプリ構成ポリシーで iOS アプリを構成する | System Center Configuration Manager"
description: "iOS 8 以降を実行しているデバイスの構成問題の解消に役立ちます。ユーザーがアプリを実行する前にアプリ構成ポリシーをユーザーに展開します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-app
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74d5d776-e37d-45de-bdba-43541b03d12c
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9cbf28afbbe69f9a027ffad2a699b9d6b625e690


---
# <a name="configure-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Configure iOS apps with app configuration policies in System Center Configuration Manager

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager のアプリ構成ポリシーを使用して、ユーザーがアプリを実行するときに必要となるような設定を指定します。 たとえば、ユーザーはアプリに次の内容を指定することが必要になる場合があります。
- カスタム ポート番号
- 言語の設定
- セキュリティ設定
- 会社のロゴなどのブランドの設定

ユーザーがこれらの設定を誤って入力すると、ヘルプ デスクの負荷が増加し、新しいアプリの採用も遅くなる可能性があります。
アプリ構成ポリシーを使用すると、ユーザーがアプリを実行する前にこれらの設定をポリシー内のユーザーに展開できるため、上記の問題を排除するのに役立ちます。 設定が自動的に指定されるため、ユーザーの操作は不要です。
これらのポリシーをユーザーやデバイスに直接展開しないでください。 代わりに、アプリケーションを展開する際に、ポリシーを展開の種類に関連付けます。 ポリシー設定は、アプリがポリシーを確認する際に (通常は初めて実行したときに) 必ず使用されます。

アプリ構成ポリシーは、現在 iOS 8 以降を実行しているデバイスのみで利用可能で、次のアプリケーションの種類をサポートします。

- **iOS アプリ パッケージ (*.ipa ファイル)**
- **iOS 用アプリ パッケージ (App ストア内)**

アプリのインストールの種類については、「[アプリケーション管理の概要](/sccm/apps/understand/introduction-to-application-management)」を参照してください。

## <a name="create-an-app-configuration-policy"></a>アプリ構成ポリシーを作成する

1. Configuration Manager コンソールで、**[ソフトウェア ライブラリ]**、**[アプリケーション管理]**、**[アプリ構成ポリシー]** の順にクリックします。
3. **[ホーム]** タブの **[アプリ構成ポリシー]** グループで、**[新しいアプリケーション構成ポリシーを作成します]** をクリックします。
4. **アプリ構成ポリシーの作成ウィザード**の **[全般]** ページで、次の情報を指定します。
    - **名前**: ポリシー固有の名前を指定します。
    - **説明**: 必要に応じて、ポリシーの説明を入力します。ポリシーの識別に役立ちます。
    - **検索とフィルター処理を向上させるために割り当てたカテゴリ**: 必要に応じて、**[カテゴリ]** をクリックし、カテゴリを作成してポリシーに割り当てます。 Configuration Manager コンソールの項目を並べ替えたり、検索したりするときに便利です。
5. **[iOS ポリシー]** ページで、構成ポリシー情報の指定方法を選択します。
    - **名前と値のペアを指定する**: 入れ子を利用しないプロパティ リスト ファイルにこのオプションを利用できます。
    名前と値のペアを指定するには
        - 新しいペアを追加するには、**[新規作成]** をクリックします。
        - **[名前と値のペアの追加]** ダイアログ ボックスで、次を指定します。
            - **種類**: 一覧から、指定する値の種類を選択します。
            - **名前**: 値を指定するプロパティ リスト キーの名前を入力します。
            - **値**: 入力したキーに適用する値を入力します。
        - プロパティ リスト ファイルを参照する: アプリ構成 XML ファイルを既に用意している場合、あるいは入れ子を利用するより複雑なファイルに対してこのオプションを使用します。
        プロパティ リスト ファイルを参照するには
            - **[アプリ構成ポリシー]** フィールドで、正しい XML 形式でプロパティ リスト情報を入力します。
            XML プロパティ リストの詳細については、iOS 開発者ライブラリの [XML プロパティ リスト](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html)に関するページを参照してください。
            XML プロパティ リストの形式は、構成するアプリによって異なります。 使用する形式の詳細については、アプリの供給元にお問い合わせください。
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
            さらに、Intune では、プロパティ リストに次の種類のトークンを利用できます。
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

            The {{ and }} characters are used by token types only and must not be used for other purposes.
            ```
            **[ファイルの選択]** をクリックし、以前に作成した XML ファイルをインポートすることもできます。
6. [次へ] をクリックします。 **** XML コードにエラーがある場合、続行する前に修正する必要があります。
6. ウィザードを完了します。

新しいアプリ構成ポリシーが **[ソフトウェア ライブラリ]** ワークスペースの **[アプリ構成ポリシー]** ノードに表示されます。

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>アプリ構成ポリシーを Configuration Manager アプリケーションに関連付ける

アプリ構成ポリシーと iOS アプリの展開を関連付けるには、「[アプリケーションの展開](/sccm/apps/deploy-use/deploy-applications)」というトピックの手順を利用し、通常行うようにアプリを展開します。
**ソフトウェアの展開ウィザード**の **[アプリ構成ポリシー]** ページで、**[新規]** をクリックします。 次に、**[アプリ構成ポリシーの選択]** ダイアログ ボックスで、アプリケーションの展開の種類とそれを関連付けるアプリ構成ポリシーを選択します。
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



<!--HONumber=Nov16_HO1-->


