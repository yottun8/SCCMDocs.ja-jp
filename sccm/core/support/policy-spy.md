---
title: Policy Spy
titleSuffix: Configuration Manager
description: Policy Spy を使用して、Configuration Manager クライアント上のポリシー システムを表示およびトラブルシューティングします。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 66a9949723e6555ddb72ebfdb845a523fb29bfe5
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385993"
---
# <a name="policy-spy"></a>Policy Spy

*適用対象: System Center Configuration Manager (Current Branch)*

Policy Spy は、[Configuration Manager ツール](/sccm/core/support/tools)の 1 つです。 これは、Configuration Manager クライアント上のポリシー システムを表示およびトラブルシューティングするためのツールです。 **PolicySpy.exe** を実行して、ユーザー インターフェイスを開きます。 コマンドラインの使用の詳細については、「[Command-line syntax](#bkmk_policyspy-syntax)」(コマンドラインの構文) を参照してください。

> [!Important]  
> Policy Spy を管理者として実行します。 **管理者として実行**していない場合は、[Client Info]\(クライアント情報\) に次のエラーが表示されます。  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="bkmk_policyspy-syntax"></a> コマンドラインの構文

Policy Spy は、主にそのユーザー インターフェイスを介して使用することを想定しています。 Policy Spy では、自動化とバッチ処理をサポートするための制限付きのコマンドライン オプションが提供されます。

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>オプション: `/export`
このオプションでは、通知せずにローカルまたはリモート コンピューターのポリシーをエクスポートします。 `<ExportFilename>` は、XML でエクスポートしたポリシーを保存するファイル名です。 `<computername>` オプションを指定した場合、Policy Spy ではローカル コンピューターの代わりに、そのコンピューターのポリシーをエクスポートします。

> [!Note]  
> このコマンドライン オプションでは、ユーザーの資格情報を指定するための方法は提供されません。 別の資格情報を使用してリモート コンピューターにアクセスするには、**runas** コマンドを使用し、必要なセキュリティの資格情報で新しいコマンド プロンプトを開きます。  


## <a name="usage"></a>使用方法

### <a name="tools-menu"></a>[ツール] メニュー

**[ツール]** メニューでは、次のアクションを利用できます。  

- **Open Remote (リモートで開く)**: リモート コンピューター上の Configuration Manager クライアント ポリシーに接続します。 [接続] ダイアログ ボックスを使用して、リモート コンピューターの名前と省略可能なユーザーの資格情報を受信します。 接続に失敗した場合、[Client Info]\(クライアント情報\) ウィンドウにエラー情報が表示されます。 再度、接続に失敗した場合は、**[編集]** メニューで **[最新の情報に更新]** を選択するか、F5 キーを押すことで接続を試みます。  

- **ファイルを開く**: **[ポリシーのエクスポート]** オプションによって作成されたポリシー エクスポート ファイル (XML) を開きます。 このツールでは、ライブ ポリシーとまったく同じエクスポートされたポリシーが表示されます。 これにより、実際のクライアントに接続するときにのみ適用される一部の機能が無効にされます。  

- **マシンの割り当ての要求**: 対象のコンピューター上のコンピューター ポリシーの割り当てに対する要求をトリガーします。 エクスポートされたポリシーを表示すると、この機能は無効になります。  

- **コンピューター ポリシーの評価**: 対象のコンピューター上のコンピューター ポリシーの評価をトリガーします。 エクスポートされたポリシーを表示すると、この機能は無効になります。  

- **ユーザー割り当ての要求**: 現在、サインインしているユーザーに対するユーザー ポリシーの割り当ての要求をトリガーします。 ローカル コンピューターでポリシーを表示しているときにのみ、この機能を利用できます。  

- **ユーザー ポリシーの評価**: 現在、サインインしているユーザーに対するユーザー ポリシーの評価をトリガーします。 ローカル コンピューターでポリシーを表示しているときにのみ、この機能を利用できます。  

- **ポリシーのリセット**: 既定以外のポリシーをすべて削除して、サイト向けのポリシーの Cookie をリセットします。 コンピューター ポリシーの割り当てに対する要求をトリガーします。 エクスポートされたポリシーを表示すると、この機能は無効になります。  

- **ポリシーのエクスポート**: 対象のコンピューターのポリシーを XML ファイルにエクスポートします。 Policy Spy を使って任意のコンピューター上でこのファイルを表示します。 エクスポート ファイルを開くには、**[ツール]** メニューで **[ファイルを開く]** を選択します。 エクスポートされたポリシーを表示すると、この機能は無効になります。  


### <a name="edit-menu"></a>[編集] メニュー

**[編集]** メニューでは、次のアクションを利用できます。  

- **削除**: 結果ウィンドウで選択されているインスタンスを削除します。 このアクションは、ポリシー インスタンスでのみサポートされます。 ポリシー インスタンス以外のものを削除しようとすると、ツールによってエラー メッセージが表示されます。 エクスポートされたポリシーを表示すると、この機能は無効になります。  

- **最新の情報に更新**: 結果をすべて更新して、最新情報を表示します。 更新する前に展開されたツリー ノードはすべて、後で自動的に展開されます。 Policy Spy がターゲット コンピューターのポリシーに正常に接続されている場合、もう一度接続しようとします。 エクスポートされたポリシーを表示すると、この機能は無効になります。  

- **イベントのクリア**: [イベント] タブからすべての項目をクリアします。  



## <a name="results-pane"></a>結果ウィンドウ

結果ウィンドウでは、ターゲット コンピューター上のポリシー システムの異なるビューが表示されます。 次の 4 つのタブをクリックすることで、これらのビューにアクセスします。 
- [実際](#bkmk_policyspy-actual)
- [要求済み](#bkmk_policyspy-requested)
- [既定](#bkmk_policyspy-default)
- [イベント](#bkmk_policyspy-events)


### <a name="bkmk_policyspy-actual"></a> 実際

このタブには、クライアントの現在のポリシーが表示されます。 現在のポリシーでは、ソフトウェアの配布やインベントリなど、クライアントの動作とそのクライアント エージェントの動作を決定します。 タブには、コンピューターの名前空間と各ユーザー固有の名前空間のルート ノードを含む結果がツリー形式で表示されます。 名前空間ノードを展開して、クラスの一覧を表示します。 クラスを展開して、そのインスタンスの一覧を表示します。 クラスの一覧には、インスタンスがあるクラスのみが含まれます。


### <a name="bkmk_policyspy-requested"></a> 要求済み

このタブには、クライアントがその割り当てられたサイトから受信したポリシーの割り当てが表示されます。 タブには、コンピューターの名前空間と各ユーザー固有の名前空間のルート ノードを含む結果がツリー形式で表示されます。 名前空間ノードを展開すると、次のノードが表示されます。  

- **構成**: ポリシー オブジェクト、割り当てなどを含む、CCM_Policy_Config から派生した構成クラスの一覧を表示します。  

- **設定**: ポリシーによって生成されたアクティブな設定がすべて表示されます。 [設定] は、[構成] ノードの下に表示されます。 

> [!Note]   
> クライアントでこれらの設定が最終結果セットにマージされるため、複数のインスタンスが同じ名前で存在できます。 Policy Spy では、true のポリシー キーの代わりに、RealKey プロパティを使用することで、このノードの下にインスタンスが表示されます。 [実際] タブ上に表示される結果セットにこれらのインスタンスを関連付けます。  


### <a name="bkmk_policyspy-default"></a> 既定

このタブには、**[要求済み]** タブと同じ情報が表示されます。また、DefaultMachine と DefaultUser の名前空間のコンテンツも含まれます。


### <a name="bkmk_policyspy-events"></a> イベント

このタブには、発生したときにポリシー エージェント イベントが表示されます。 このビューでは、CCM_PolicyAgent_Event から派生したすべてのイベントに対して WMI イベント サブスクリプションが作成されます。 ビューには最大 200 件のイベントが表示されます。 必要に応じて、一覧の上部から最も古いイベントが削除されます。 一覧の最後の項目を選択した場合、新しいイベントを追加すると、一覧で自動的に下へスクロールされます。 それ以外の場合は、ビューではその現在の位置が保持され、下へスクロールするか、End キーを押して新しいイベントを表示する必要があります。 エクスポートされたポリシーを表示する場合、このビューは常に空になります。



## <a name="client-info-pane"></a>[Client Info]\(クライアント情報\) ウィンドウ
[クライアント情報] ウィンドウには、ターゲット コンピューターに対するプロパティの一覧が表示されます。 利用できる場合は、次のプロパティが表示されます。  
- 名前
- ID
- バージョン
- サイト
- 割り当てられている MP
- 常駐 MP
- プロキシ MP
- プロキシの状態



## <a name="details-pane"></a>詳細ウィンドウ
詳細ウィンドウには、現在の選択に関する詳細情報が表示されます。 アクティブな選択がない場合、バージョンなどの Policy Spy 自体に関する情報が表示されます。 それ以外の場合は、選択した項目の管理オブジェクト フォーマット (MOF) の表現が表示されます。

Policy Spy では、独自の MOF の生成ルーチンを使用して、WMI によって生成されるプレーン テキストの MOF ではなく、よりわかりやすい HTML 表示が作成されます。 この動作によって、Policy Spy が MOF を読みやすくするために、次の機能を追加できるようになります。  

- 構文の強調表示  

- インデントが設定されたオブジェクトと配列  

- プロパティがシステム、継承、およびローカル グループに配置されます。 既定では、システムと継承されたグループは折りたたまれます。 インスタンスが実際に使用するプロパティをすぐに表示できます。  

- MOF をコピーするか、プレーンテキストの MOF をクリップボードにコピーします。 この機能は、MofComp ツールを直接呼び出して、MOF をその他のアプリケーションに貼り付けるのに便利です。  

CCM_Policy_Policy から派生したポリシー オブジェクトのインスタンスの場合、詳細ウィンドウでは、表示する MOF の下にポリシーの本文が表示されます。 クライアントでポリシーの本文をダウンロードしていない場合、Policy Spy にはハイパーリンクが表示されます。 リンクをクリックして、クライアントの管理ポイントから直接ポリシーの本文をダウンロードします。 ツールでポリシーの本文を正常にダウンロードできた場合、ハイパーリンクが返信のコンテンツに置き換えられます。 それ以外の場合は、Policy Spy によって要求に失敗したことを示す表示に更新されます。

