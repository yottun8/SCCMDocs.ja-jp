---
title: UUP プレビュー
titleSuffix: Configuration Manager
description: UUP 統合のプレビューについての説明
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 0b0da585-0096-410b-8035-6b7a312f37f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 27a960758d8d3939798ae270404d5dd1afbea62d
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2019
ms.locfileid: "55072987"
---
# <a name="uup-private-preview-instructions"></a>UUP プライベート プレビューの説明

> [!Note]  
> この情報は、製品版のリリース前に大幅に変更される可能性があるプレビュー機能に関連します。 Microsoft は、ここで提供される情報に関して、明示または黙示を問わず、いかなる保証も行いません。  

## <a name="benefits"></a>メリット

### <a name="feature-updates"></a>機能更新プログラム

Windows 10 の Unified Update Platform (UUP) の機能更新プログラムは、お客様が今日のサービスに関して抱えている複数の問題を軽減するように設計されています。 UUP 機能更新プログラムの次のような点をお試しください。

- 最新のセキュリティ コンプライアンス レベルへの直接アップグレード。準拠するようにアップグレードした直後にセキュリティ更新プログラムをインストールする必要はなくなります。 最新の累積的セキュリティ更新プログラムを収めるため、新しい機能更新プログラムが毎月公開されます。 毎月機能更新プログラムのコンテンツの大部分を再ダウンロードしたり配布したりする必要はありません。セキュリティ更新プログラム コンポーネントだけです。これは累積的更新プログラムとも共有されます。

- アップグレード プロセスの間に、すべての Features on Demand (FOD) と言語パックを保持して失われないようにする必要があります。

- UUP の機能更新プログラムでは高速インストール ファイルがサポートされ、各クライアントでダウンロードする必要があるコンテンツの量を削減できます。

UUP について詳しくは、Windows に関するブログの投稿「[An update on our Unified Update Platform (UUP) (Unified Update Platform (UUP) に関する更新)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/)」をご覧ください。


### <a name="cumulative-updates"></a>累積的更新プログラム

UUP の累積的更新プログラムでは、FOD と言語パックの内容をオフラインで配布できます。エンド ユーザーは必要に応じてそれらを取得でき、インターネットへのアクセスや、管理者による面倒なステージング作業は必要ありません。



## <a name="set-up-instructions"></a>セットアップ手順

### <a name="1-send-your-wsus-id-to-your-uup-preview-contact-at-microsoft"></a>1.自分の WSUS ID を Microsoft の UUP プレビュー連絡先に送信します

UUP のプライベート プレビューに参加するには、ユーザーの環境をプレビューのホワイトリストに登録できるように、ユーザーの WSUS ID を Microsoft と共有する必要があります。 この ID がないと、プレビューが公開されるまで、ユーザーは UUP の更新プログラムを見ることができません。

自分の WSUS ID を取得するには:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

**MUUrl** プロパティは `https://sws.update.microsoft.com` である必要があります。 これを変更する場合は、サポート記事の「[WSUS synchronization fails with SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception)」 (WSUS の同期が SoapException で失敗する) の解決方法を参照してください。


### <a name="2-update-configmgr"></a>2.ConfigMgr を更新します

環境内の高速インストール ファイルを同期している場合、運用環境では ConfigMgr 1810 の現在のブランチが、ラボ環境では 1812 のテクニカル プレビュー ブランチが必要です。

環境内の高速インストール ファイルを同期していない場合、運用環境ではさらに ConfigMgr 1810 の修正プログラム KB4482615 が、ラボ環境では 1812 のテクニカル プレビュー ブランチが必要です。


#### <a name="diagnostics-and-usage-data-level"></a>診断結果と使用状況データのレベル
このプレビュー期間中に、Configuration Manager の診断結果とデータの使用状況のレベルを上げることを検討します。 **フル**  レベルは、Microsoft でこの新機能に関する問題をより適切に分析し、トラブルシューティングするのに役立ちます。 詳細については、「[バージョン 1810 での診断の使用状況データ収集のレベル](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1810)」を参照してください。


#### <a name="update-rollup-for-configmgr-1810-4486457"></a>ConfigMgr 1810 の更新プログラムのロールアップ (4486457)

1. バージョン 1810 の更新プログラム ロールアップを使用して、サイトを更新します。 詳細については、[コンソール内の更新プログラムのインストール](/sccm/core/servers/manage/install-in-console-updates)に関するページを参照してください。  

2. クライアントを更新します。  

    - このプロセスを簡単にするには、自動クライアント アップグレードの使用を検討します。 詳細については、「[クライアントをアップグレードする](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade)」をご覧ください。  

    - 使用されていないコンテンツの**約 6 GB の不必要なダウンロード**をクライアントに対して行わなくてもよいように、UUP 更新プログラムの対象であるすべてのクライアントをアップグレードする必要があります。

この更新プログラムの詳細については、「[Update rollup for System Center Configuration Manager current branch, version 1810](https://support.microsoft.com/help/4486457)」 (System Center Configuration Manager Current Branch バージョン 1810 の更新プログラムのロールアップ) を参照してください。


<!-- 
#### 1812 Technical Preview
The 1812 Technical Preview is equivalent in supported UUP scenarios to the ConfigMgr 1810 UUP Hotfix (KB4482615).

The only note is that client upgrade of 1812 Technical Preview is broken from 1810.1 TP or 1811 TP. To work around this issue, you'll need to uninstall 1810.1 TP and 1811 TP clients, then install the 1812 TP client cleanly. All clients you target UUP updates to must be on 1812 Technical Preview (or later) to prevent **unnecessarily downloading around 6 GB** of unused content to the client.
 -->


### <a name="3-update-windows-clients-to-supported-versions"></a>3.サポートされているバージョンに Windows クライアントを更新します

#### <a name="for-express-installation-file-sync"></a>高速インストール ファイル同期の場合
高速コンテンツの場合、次の Windows バージョンがサポートされています。

- **Windows 10 バージョン 1809** とセキュリティ以外の累積的更新プログラム [KB4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976) (1 月 22 日リリース) 以降。 この更新プログラムはカタログでのみ使用でき、WSUS には直接同期されません。 展開のために環境内に更新プログラムをインポートするには、「[Microsoft Update カタログから更新プログラムをインポートする](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)」をご覧ください。

- **Windows 10 バージョン 1803** と [KB4284835](https://support.microsoft.com/help/4284835) (2017 年 6 月の累積的セキュリティ更新プログラム) 以降  

- **Windows 10 バージョン 1709** と [KB4338825](https://support.microsoft.com/help/4338825) (2017 年 7 月の累積的セキュリティ更新プログラム) 以降  


#### <a name="for-non-express-installation-file-sync"></a>非高速インストール ファイル同期の場合
非高速コンテンツの場合は、追加のパッチを適用する必要があります。 約 6 GB の使用されていないコンテンツの不必要なダウンロードがクライアントに対して行われないようにするには、この更新プログラムが不可欠です。 サポートされている Windows バージョンには、次のビルドが含まれます。

- **Windows 10 バージョン 1809** とセキュリティ以外の累積的更新プログラム [KB4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976) (1 月 22 日リリース) 以降。 この更新プログラムはカタログでのみ使用でき、WSUS には直接同期されません。 展開のために環境内に更新プログラムをインポートするには、「[Microsoft Update カタログから更新プログラムをインポートする](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)」をご覧ください。


- **Windows 10 バージョン 1803** と **Windows 10 バージョン 1709** のクライアントには、ベースの累積的更新プログラム レベルに加えて、非累積的更新プログラムが必要です。
    - 累積的更新プログラム
        - 1803:[KB4284835](https://support.microsoft.com/help/4284835) (2017 年 6 月の累積的セキュリティ更新プログラム) から 2019 年 1 月の累積的セキュリティ更新プログラムまで (両端を含む)
        - 1709:[KB4338825](https://support.microsoft.com/help/4338825) (2017 年 7 月の累積的セキュリティ更新プログラム) から 2019 年 1 月の累積的セキュリティ更新プログラムまで (両端を含む)
    - 非累積的更新プログラム:この更新プログラムはカタログでのみ使用でき、WSUS には直接同期されません。 展開のために環境内に更新プログラムをインポートするには、「[Microsoft Update カタログから更新プログラムをインポートする](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)」をご覧ください。
        - 1803:[KB4483541](https://support.microsoft.com/help/4483541)
        - 1709:[KB4483530](https://support.microsoft.com/help/4483530)


### <a name="4-enable-express-installation-on-clients-in-client-settings"></a>4.クライアント設定でクライアントの高速インストールを有効にします

高速コンテンツが同期されるかどうかに関係なく、高速インストールを有効にするクライアントの設定を、UUP 更新プログラムに対して設定する必要があります。 この設定により、UUP 更新プログラムに関連するすべてのコンテンツを ConfigMgr でダウンロードするのではなく、ConfigMgr で Windows 更新エージェント (WUA) にクライアントにダウンロードする必要のあるコンテンツを決定させることができます。 オプションの FOD と言語パックのコンテンツがあり、更新プログラムに関連付けられているすべてのクライアントで必要ではない少量の余分なデータが発生するため、この設定は高速以外のシナリオに対しても必要です。

この設定を有効にしても、サーバーのコンテンツのダウンロードには影響せず、クライアントのダウンロード動作だけです。 上記の ConfigMgr と Windows クライアントのバージョンをまだ有効にしていない場合は、この設定を有効にする前に、有効にすることが重要です。これらのバージョンでは、WSUS での更新プログラムの直接承認に関する互換性の問題が修正され、高速コンテンツが同期されない場合でも、UUP 更新プログラムに対するこのチャネルを ConfigMgr で使用できるようになります。

クライアントで高速インストールを有効にするには:

1. Configuration Manager コンソールで、**[管理]** \ **[クライアント設定]** に移動します  

2. 使用するクライアント設定のプロパティを開くか、または適切に展開するために新しく作成します。  

3. **[ソフトウェア更新プログラム]** グループで、**[クライアントでの高速インストール ファイルのインストールを有効にする]** を **[はい]** に設定します

![[ソフトウェア更新プログラム] グループで強調表示されているクライアント設定](../media/uup-preview-client-settings.png)


### <a name="5-make-sure-your-adrs-are-set-as-desired"></a>5.ADR が適切に設定されていることを確認します 

UUP 更新プログラムの同期を有効にする前に、自動展開規則 (ADR) および導入されている他の更新インフラストラクチャについて検討します。 既存の ADR およびサービス プランの一部としてこれらの更新プログラムを自動的に展開したくない場合は、フィルターで除外するように ADR を更新します。「[同期されている UUP を検索する方法](#how-to-find-synced-uup-updates)」をご覧ください。 既存のサービス プランでは、非 UUP のみが既定で展開されますが、サービス プランを更新してこの動作を変更することができます。

また、これらの更新プログラムを同期することだけでコンプライアンス レポートや他のインフラストラクチャが影響を受けるかどうかを検討し、事前に必要な変更を行います。 たとえば、すべての製品でコンプライアンスを測定する場合、UUP と非 UUP 両方の累積的 Windows 10 更新プログラムが非準拠または準拠として表示されるので、値が非対称になります。



## <a name="enable-uup-and-start-testing"></a>UUP を有効にしてテストを開始する

### <a name="select-products-and-classifications-to-sync"></a>同期する製品と分類を選択する

UUP 更新プログラムの同期と試用を始める準備ができて、パイロットが表示されるように WSUS が有効にされたことを Microsoft から通知されたら、新製品を有効にします。

1. [ソフトウェア更新プログラムを同期](/sccm/sum/get-started/synchronize-software-updates)して、新しい製品が設定されるようにします  

2. Configuration Manager コンソールで、**[管理]** \ **[サイトの構成]** \ **[サイト]** の順に移動します  

3. 最上位サイト (中央管理サイト (CAS)、スタンドアロンのプライマリのどちらか) を選択します  

4. **[サイト コンポーネントの構成]** \ **[ソフトウェアの更新ポイント]** を開きます  

5. **[製品]** タブでは、WSUS サーバーがプレビューに追加されると、2 つの新しい製品が表示されます。 これらの製品には、プレビュー UUP コンテンツが含まれます。  

    - **Windows 10 UUP プレビュー**  
    - **Windows Server UUP プレビュー**  

6. **[分類]** タブで、以下を選択します。  

    - **[セキュリティ更新プログラム]**:UUP の累積的更新プログラムを表示する場合  
    - **[アップグレード]**:UUP の機能更新プログラムを表示する場合  

7. ソフトウェア更新プログラムを同期して、新しい UUP 更新プログラムを表示します


### <a name="how-to-find-synced-uup-updates"></a>同期されている UUP を検索する方法

UUP 更新プログラムを環境に同期した後は、テストのためにそれらを検索する必要があります。 Configuration Manager コンソール内でプレビュー更新プログラムを検索するには、2 つの簡単な方法があります。

- これらのプレビュー更新プログラムは別の製品なので、常に製品を使用してこれらの更新プログラムをフィルター処理または検索できます。 UUP または非 UUP の機能更新プログラムを展開するかどうかを選択できるように、製品フィルターがサービス プランに追加されています。  

- ソフトウェア ライブラリの **[すべてのソフトウェア更新プログラム]** ノードと **[すべての Windows 10 更新プログラム]** ノードおよび ADR のフィルターに、新しいオプションの列 **[タグ]** があります。 このフィールドは、UUP 更新プログラムの場合は **[UUP]** に設定され、UUP 以外の更新プログラムの場合は空白に設定されます。  


### <a name="updates-available-during-preview"></a>プレビュー期間中に使用可能な更新プログラム

- Windows 10 1809 累積的更新プログラム
    - 2 月のセキュリティ更新プログラム (2/12)  

- Windows 10 1803 累積的更新プログラム
    - 12 月のセキュリティ更新プログラム (12/11)
    - 1 月のセキュリティ更新プログラム (1/8)
    - 1 月の非セキュリティ更新プログラム (1/15)
    - 2 月のセキュリティ更新プログラム (2/12)  

- Windows 10 1709 累積的更新プログラム
    - 12 月のセキュリティ更新プログラム (12/11)
    - 1 月のセキュリティ更新プログラム (1/8)
    - 1 月の非セキュリティ更新プログラム (1/15)
    - 2 月のセキュリティ更新プログラム (2/12)  

- Windows 10 1809 機能更新プログラム (1709 または 1803 から)
    - 12 月 (12/11) のセキュリティ更新プログラムのコンプライアンス
    - 1 月 (1/8) のセキュリティ更新プログラムのコンプライアンス
    - 2 月のセキュリティ更新プログラムのコンプライアンス (2/12)  

- Windows 10 1803 機能更新プログラム (1709 または 1803 から)   
    - 12 月のセキュリティ更新プログラムのコンプライアンス (12/11)
    - 1 月のセキュリティ更新プログラムのコンプライアンス (1/8)
    - 2 月のセキュリティ更新プログラムのコンプライアンス (2/12)  

UUP がまだプレビュー段階 (プライベートまたはパブリック) の場合、必要に応じて、3 月およびそれ以降のセキュリティ更新プログラムも、引き続きこれらすべての領域で公開されます。 プレビューが完了した後は、Windows 10 バージョン 1809 累積的更新プログラムおよび機能更新プログラム (Windows 10 バージョン 1803 から) のみが、運用環境でサポートされます。


### <a name="scenarios-to-try"></a>試すシナリオ

#### <a name="feature-updates"></a>機能更新プログラム
- 選択したセキュリティ コンプライアンス レベルへの直接アップグレード  

- アップグレードの前に FOD と言語パックがインストールされているアップグレード (これらはアップグレードの過程で保持されます)  

- オプションとして、機能更新プログラムの高速インストール ファイルの同期を有効にし、各クライアントでダウンロードする必要があるコンテンツの量を減らします。  

    > [!Note]  
    > このクライアントのベネフィットと引き換えに、累積的更新プログラムの高速インストール ファイルの場合など、サーバーのダウンロードと配布は大きくなります。  

#### <a name="cumulative-updates"></a>累積的更新プログラム
プレビュー期間中は、複数の連続する更新プログラムに対して UUP 型の更新プログラムを使用してクライアントの準拠を維持し、継続的に予測が行われているような感覚にします。

#### <a name="content"></a>Content
各メジャー バージョン (1809、1803、1709)、アーキテクチャ、および言語の組み合わせに対する最初の更新プログラムは、ファイルの数とディスク容量の両方の点で、以前の非 UUP 更新プログラムと比較して、大きく見えるはずです。 この余分なコンテンツは、主に累積的更新プログラムに対するすべての FOD と言語パックによるものです。 機能更新プログラムの場合 (特に高速が有効になっている場合)、その最初の更新プログラムには大きい追加コンテンツがあります。 

ただし、以降の更新プログラムでは (累積的更新プログラムと、高コンプライアンス レベルでの月単位の機能更新プログラムの両方)、すべての FOD と言語パックのコンテンツは更新プログラム間でインテリジェントに共有されて、再ダウンロードまたは再配布の必要がないため、ダウンロードして配布する必要がある新しいコンテンツの量ははるかに少なくなります。 プレビュー期間中の 1709 と 1803 では、この月単位のダウンロードのサイズは、非 UUP のシナリオでの累積的更新プログラムのサイズとほぼ同じになります。 ただし、1809 では、累積的更新プログラムの増分ダウンロードが月ごとにどんどん小さくなるため、状況ははるかによくなります。 

非高速で非 UUP の 1803 に関して 12 か月間にダウンロードおよび配布されたコンテンツの総量を見ると、UUP の 1809 とほぼ同等ですが、その転換点を過ぎると、リリースの有効期間全体でダウンロードおよび配布されたコンテンツの総量は UUP の 1809 の方が少なくなります。 高速の場合、転換点は 1809 より早く、高速は機能更新プログラムだけで累積的更新プログラムはないので、高速での大規模なサーバー コンテンツのコストは毎月ではなくリリースごと 1 回だけです。

#### <a name="supported-content-channels"></a>サポートされているコンテンツ チャネル
プレビューでは、現実のエンタープライズ環境で使用しているものでテストします。 UUP では、以下のすべてのコンテンツ チャネルがサポートされます。
- Windows 配信の最適化
- Configuration Manager のピア キャッシュ
- Windows BranchCache
- サーバーにダウンロードしないで (展開パッケージなし) Microsoft Update から直接ダウンロードする展開 (これを使用する場合は、配信の最適化の併用を推奨)
- サード パーティの代替コンテンツ プロバイダー

詳しくは、「[Windows 10 更新プログラムの配信の最適化](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)」をご覧ください。
