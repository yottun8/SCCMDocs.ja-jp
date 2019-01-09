---
title: Technical Preview 1611 の機能
titleSuffix: Configuration Manager
description: System Center Configuration Manager の Technical Preview バージョン 1611 で使用できる機能について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 71ad5ae8ff823d03951d5f9ae1a13e8051cba23e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416573"
---
# <a name="capabilities-in-technical-preview-1611-for-system-center-configuration-manager"></a>System Center Configuration Manager の Technical Preview 1611 の機能

「オブジェクトの*適用対象: System Center Configuration Manager (Technical Preview)*



この記事では、System Center Configuration Manager の Technical Preview バージョン 1611 で使用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、説明のトピック「[System Center Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、および Technical Preview の機能に関するフィードバックを提供する方法について理解してください。    

**この Technical Preview の既知の問題:**   
- ***前提条件の状態***: バージョン 1611 をインストールする場合、前提条件の全体的な状態は、警告付きで合格として表示されます。ただし、警告の原因となった前提条は一覧表示されません。 この状況は、次の 2 つの前提条件によって発生することがあります。
  - SQL インデックス作成メモリのオプション
  - SQL Server のバージョンがサポートされているかどうかの確認  

  これらは警告にすぎないので、無視することができます。

- ***PowerShell***:Configuration Manager コンソールから Windows PowerShell に接続するとき、次のエラーが表示される可能性があります: **Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml がデジタル署名されていない**。  

   この問題は、特定のファイルをバージョン 1610 の署名付きバージョンのファイルに置き換えることで解決できます。 バージョン 1610 のインストールの **&lt;install directory>\AdminConsole\bin\\** フォルダーから拡張子 **.psd1**、**.ps1xml**、**.psm1** を持つすべてのファイルをコピーします。 これらのファイルを、ご利用の Technical Preview 1611 がインストールされている **&lt;install directory>\AdminConsole\bin\\** フォルダーに貼り付けて、1611 バージョンのファイルを上書きします。


**このバージョンでお試しいただける新機能を次に示します。**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>利用可能な展開とタスク シーケンスのコンテンツを事前キャッシュする
このテクニカル プレビューでは、利用可能な展開とタスク シーケンスについて、事前キャッシュ機能を使用するように設定できます。これにより、ユーザーがコンテンツをインストールする前に、関連するコンテンツのみをクライアントにダウンロードさせることができます。

たとえば、Windows 10 のインプレース アップグレード タスク シーケンスを展開する場合で、すべてのユーザーに対して必要なタスク シーケンスは 1 つのみで、複数のアーキテクチャおよび/または言語に対応する必要があるとします。 Current Branch では、利用可能な展開を作成した場合、その後ユーザーがソフトウェア センターで **[インストール]** をクリックすると、その時点でコンテンツがダウンロードされます。 この場合は、インストールできる状態になるまで、さらに時間がかかります。 あるいは、Current Branch では、利用可能なタスク シーケンスの展開を作成した場合、タスク シーケンスで参照されるすべてのコンテンツがダウンロードされます。 これには、すべての言語およびアーキテクチャ用のオペレーティング システム アップグレード パッケージが含まれます。 各パッケージのサイズが約 3 GB だとすると、ダウンロード パッケージは非常に大きくなものとなります。

コンテンツの事前キャッシュ機能には、クライアントが展開を受信してすぐに適用可能なコンテンツのみをダウンロードできるようにするオプションが用意されています。 したがって、ユーザーがソフトウェア センターで **[インストール]** をクリックすると、コンテンツはローカルのハード ドライブ上にあるため、コンテンツは準備完了の状態にあり、インストールが迅速に開始されます。

### <a name="to-configure-the-pre-cache-feature"></a>事前キャッシュ機能を構成するには

1. 特定のアーキテクチャおよび言語に対応したオペレーティング システム アップグレード パッケージを作成します。 パッケージの **[データ ソース]** タブでアーキテクチャと言語を指定します。 言語については、10 進数変換を使用します (たとえば、1033 は英語を表す 10 進数です。これを 16 進数で表すと 0x0409 となります)。 詳細については、「[オペレーティング システムをアップグレードするタスク シーケンスの作成](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)」を参照してください。

    アーキテクチャと言語の値は、次の手順で作成するタスク シーケンス ステップの条件と照合してオペレーティング システム アップグレード パッケージの事前キャッシュが必要かどうかを判断するために使用されます。
2. さまざまな言語およびアーキテクチャに対して条件付きステップを適用するタスク シーケンスを作成します。 たとえば、英語バージョンの場合は、次のようなステップを作成することが可能です。

    ![事前キャッシュのプロパティ](media/precacheproperties2.png)

    ![事前キャッシュのオプション](media/precacheoptions2.png)  

3. タスク シーケンスを展開します。 事前キャッシュの機能については、次のように構成します。
    - **[全般]** タブで、**[このタスク シーケンス用のコンテンツを事前にダウンロードする]** を選択します。
    - **[展開設定]** タブで、**[目的]** を **[利用可能]** にしてタスク シーケンスを構成します。 **必須**の展開を作成する場合、事前キャッシュ機能は動作しません。
    - **[スケジュール]** タブの **[この展開が使用可能になる日時を指定する]** 設定では、将来の適切な時刻を選択します。これにより、展開をユーザーが利用できるようにする前に、コンテンツを事前キャッシュするのに十分な時間をクライアントに与えます。 たとえば、利用可能時間を 3 時間先に設定することで、コンテンツを事前キャッシュするのに十分な時間を確保することができます。  
    - **[配布ポイント]** タブで、**[展開オプション]** 設定を構成します。 ユーザーがインストールを開始する前にコンテンツを事前キャッシュしない場合は、これらの設定を使用します。


### <a name="user-experience"></a>ユーザー側の表示と操作
- クライアントは、展開ポリシーを受け取ると、コンテンツの事前キャッシュを開始します。 これには、参照されるすべてのコンテンツ (他のパッケージの種類) と、オペレーティング システム アップグレード パッケージのうち、タスク シーケンスで設定した条件に基づいてクライアントと一致したものが含まれます。
- ユーザーが展開を利用可能になると (展開の **[スケジュール]** タブの設定)、新しい展開に関する情報をユーザーに提供する通知が表示され、展開がソフトウェア センターで確認可能な状態になります。 ユーザーはソフトウェア センターに移動し、**[インストール]** をクリックしてインストールを開始します。
- コンテンツが完全に事前キャッシュされていない場合は、展開の **[展開オプション]** タブで指定した設定が使用されます。 展開を作成した時間と、展開をクライアントが利用できるようにする時間との間隔を適切な長さに設定して、コンテンツを事前キャッシュするのに十分な時間をクライアントに与えることをお勧めします。


## <a name="see-also"></a>関連項目
[System Center Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)
