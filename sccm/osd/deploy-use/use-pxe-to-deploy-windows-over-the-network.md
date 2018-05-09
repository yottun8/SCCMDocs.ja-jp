---
title: ネットワーク経由で OSD に PXE を使用する
titleSuffix: Configuration Manager
description: PXE による OS の展開を使用して、コンピューターのオペレーティング システムを更新するか、新しいコンピューターに新しいバージョンの Windows をインストールします。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: deb8321400eac4085cefca8686f2703cea5f659a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>System Center Configuration Manager で PXE を使用してネットワーク経由で Windows を展開する

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager での PXE (Preboot execution environment) によるオペレーティング システムの展開では、クライアント コンピューターはネットワーク経由でオペレーティング システムを要求し、展開することができます。 この展開シナリオでは、OS イメージとブート イメージを PXE 対応配布ポイントに送信します。

> [!NOTE]  
>  x64 BIOS コンピューターのみを対象とする OS の展開を作成する場合は、配布ポイントに x64 ブート イメージと x86 ブート イメージの両方を用意する必要があります。

PXE を使用した OS の展開は、次のシナリオで使用できます。

-   [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)  

いずれかの OS の展開シナリオのステップを完了させてから、この記事のセクションを参照して、PXE による展開を準備します。



##  <a name="BKMK_Configure"></a> PXE 要求を許可するために少なくとも 1 つの配布ポイントを構成する
PXE ブート要求を作成する Configuration Manager クライアントにオペレーティング システムを展開するには、PXE 要求を受け入れるように 1 つ以上の配布ポイントを構成する必要があります。 構成された配布ポイントは、PXE ブート要求に応答し、実行する適切な展開アクションを決定します。 詳細については、[配布ポイントのインストールと変更に関するトピック](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#pxe)を参照してください。  



## <a name="prepare-a-pxe-enabled-boot-image"></a>PXE 対応のブート イメージの作成
PXE を使用して OS を展開するには、1 つ以上の PXE 対応配布ポイントに配布される、x86 と x64 の両方の PXE 対応ブート イメージが必要です。 この情報を使用して、ブート イメージで PXE を有効にして、配布ポイントにブート イメージを配布します。

-   ブート イメージで PXE を有効にするには、**[データ ソース]** タブのブート イメージ プロパティで、**[このブート イメージを PXE 対応の配布ポイントから展開する]** を選択します。

-   ブート イメージのプロパティを変更する場合は、再配布ポイントにブート イメージを再配布します。 詳細については、「[コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)」をご覧ください。



##  <a name="BKMK_PXEExclusionList"></a> PXE 展開の除外リストの作成
PXE を使用してオペレーティング システムを展開する場合、配布ポイントで除外リストを作成できます。 除外リストには、配布ポイントが無視すべきコンピューターの MAC アドレスを追加します。 リストに追加されたコンピューターは、Configuration Manager が PXE 展開で使用する展開タスク シーケンスを受け取りません。

#### <a name="to-create-the-exclusion-list"></a>除外リストを作成するには

1.  PXE 対応の配布ポイントにテキスト ファイルを作成します。 例として、このテキスト ファイルを **pxeExceptions.txt**と名づけます。

2.  メモ帳などのプレーン テキスト エディターを使用して、PXE 対応配布ポイントが無視するべきコンピューターの MAC アドレスを追加します。 MAC アドレス値はコロンを使って区切り、各アドレスを別の行に入力します。 例: `01:23:45:67:89:ab`

3.  PXE 対応の配布ポイント サイト システム サーバーにテキスト ファイルを保存します。 テキスト ファイルはサーバーの任意の場所に保存できます。

4.  PXE 対応配布ポイントのレジストリを編集して、**MACIgnoreListFile** レジストリ キーを作成します。 PXE 対応の配布ポイント サイト システム サーバーでテキスト ファイルのフル パスの文字列値を追加します。 次のレジストリ パスを使用します。

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  レジストリ エディターの使用方法を誤ると、重大な問題が発生し、オペレーティング システムの再インストールが必要になることがあります。 レジストリ エディターの使用方法を誤った結果生じた問題については、解決できる保証はありません。 レジストリ エディターは、ご自身の責任において使用してください。

     このレジストリの変更を行った後、サーバーの再起動は必要ありません。



## <a name="manage-duplicate-hardware-identifiers"></a>重複するハードウェア識別子を管理する
複数のコンピューターが重複する SMBIOS 属性を持っている場合、または共有ネットワーク アダプターを使用している場合は、Configuration Manager で複数のコンピューターが同じデバイスとして認識される場合があります。 階層の設定で重複するハードウェア識別子を管理することにより、これらの問題を軽減できます。 詳細については、「[重複するハードウェア識別子を管理する](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers)」を参照してください。



##  <a name="BKMK_RamDiskTFTP"></a>RamDisk TFTP ブロック サイズとウィンドウ サイズ
PXE 対応配布ポイントの RamDisk TFTP ブロック サイズとウィンドウ サイズをカスタマイズできます。 ネットワークをカスタマイズしている場合、ブロックまたはウィンドウのサイズが大きいと、ブート イメージのダウンロードがタイムアウト エラーで失敗する可能性があります。 RamDisk TFTP ブロック サイズとウィンドウ サイズのカスタマイズにより、特定のネットワーク要件に対応する PXE を使用する場合に、TFTP トラフィックを最適化できます。 最も効率的な構成を判断するには、環境内でカスタマイズした設定をテストします。 詳細については、「[PXE 対応配布ポイント上の RamDisk TFTP ブロック サイズとウィンドウ サイズのカスタマイズ](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)」を参照してください。



## <a name="configure-deployment-settings"></a>展開の設定の構成
PXE による OS の展開を使用するには、OS を PXE ブート要求から使用できるように展開を構成します。 展開のプロパティの **[展開設定]** タブで、使用できるオペレーティング システムを構成します。 **[利用できるようにする項目]** の設定では、次のいずれかのオプションを選択します。

-   Configuration Manager クライアント、メディア、PXE

-   メディアと PXE のみ

-   メディアと PXE のみ (非表示)



##  <a name="BKMK_Deploy"></a> タスク シーケンスの展開
ターゲット コレクションに OS を展開します。 詳細については、「 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)」をご覧ください。 PXE を使用してオペレーティング システムを展開するとき、展開が必須か使用可能かを設定することができます。

-   **必要な展開**: 必要な展開では、ユーザーの介入なしに、PXE を使用します。 ユーザーは PXE ブートをバイパスできません。 ただし、ユーザーが配布ポイントが応答する前に PXE ブートをキャンセルすれば、OS は展開されません。

-   **利用可能な展開**: 利用可能な展開では、ユーザーがセットアップ先のコンピューターにいる必要があります。 ユーザーは、PXE ブート プロセスを続けるために F12 キーを押す必要があります。 F12 キーを押すユーザーがいない場合、コンピューターは現在の OS、または次に利用可能なブート デバイスから起動します。

Configuration Manager コレクションまたはコンピューターに割り当てられた最終の PXE 展開の状態をクリアすることにより、必要な PXE 展開を再展開することができます。 **必須の PXE 展開の消去**アクションの詳細については、[クライアントの管理](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode)または[コレクションの管理](/sccm/core/clients/manage/collections/manage-collections#how-to-manage-device-collections)に関するトピックを参照してください。 この操作でその展開の状態がリセットされ、最新の必要な展開が再インストールされます。

> [!IMPORTANT]
> PXE プロトコルはセキュリティ保護されていません。 PXE サーバーと PXE クライアントのどちらも、サイトへの不正なアクセスを防御するデータセンターといった物理的に安全なネットワークに置かれていることを確認します。



##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>PXE ブートのクライアントが使用するブート イメージの選択方法
クライアントが PXE で起動する場合、使用するブート イメージが Configuration Manager によってクライアントに提供されます。 Configuration Manager は、アーキテクチャが厳密に一致するブート イメージを使用します。 正確なアーキテクチャのブート イメージがない場合、Configuration Manager は、互換性のあるアーキテクチャを持つブート イメージを使用します。 次の一覧では、PXE ブートのクライアントが使用するブート イメージがどのように選択されるかについて説明します。
1. Configuration Manager は、ブートしようとしているクライアントの MAC アドレスまたは SMBIOS に一致するシステム レコードをサイト データベースで検索します。  

    > [!NOTE]
    > サイトに割り当てられているコンピューターを、別のサイトの PXE にブートした場合、そのコンピューターでポリシーを表示できません。 たとえば、クライアントが既にサイト A に割り当てられている場合、サイト B の管理ポイントと配布ポイントは、サイト A のポリシーにアクセスできず、クライアントは正常に PXE ブートしません。

2. Configuration Manager は、手順 1 で見つかったシステム レコードに展開されているタスク シーケンスを探します。

3. 手順 2 で見つかったタスク シーケンスの一覧で、Configuration Manager はブートしようとしているクライアントのアーキテクチャに一致するブート イメージを探します。 同じアーキテクチャのブート イメージが見つかった場合は、そのブート イメージを使用します。

4. 同じアーキテクチャのブート イメージが見つからなかった場合、Configuration Manager は、クライアントのアーキテクチャと互換性があるブート イメージを探します。 手順 2. で見つかったタスク シーケンスの一覧で探します。 たとえば、64 ビット クライアントは、32 ビットおよび 64 ビットのブート イメージと互換性があります。 32 ビット クライアントは、32 ビットのブート イメージのみと互換性があります。 UEFI クライアントは、64 ビットのブート イメージのみと互換性があります。
