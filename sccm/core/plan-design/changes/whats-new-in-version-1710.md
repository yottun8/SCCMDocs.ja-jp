---
title: 新しいバージョン 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: System Center Configuration Manager のバージョン 1710 で導入された変更点および新機能について詳しく説明します。
ms.date: 1/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4dcf5ce0c31f72db1e6af3ac9e024c83afe92337
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250665"
---
# <a name="what39s-new-in-version-1710-of-system-center-configuration-manager"></a>System Center Configuration Manager のバージョン 1710 の新機能

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager Current Branch の更新プログラム 1710 は、バージョン 1610、1702、または 1706 を実行しているインストール済みのサイトで、コンソール内の更新プログラムとして利用可能です。

このリリースには、新機能に加え、バグ修正などの追加の変更も含まれています。 詳細については、「[Summary of changes in System Center Configuration Manager current branch, version 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran)」(System Center Configuration Manager Current Branch バージョン 1710 の変更点の概要) を参照してください。

このリリースでは、次の追加の更新プログラムも利用できるようになりました。
- [System Center Configuration Manager Current Branch バージョン 1710 の更新プログラムのロールアップ](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [System Center Configuration Manager Current Branch バージョン 1710 の更新プログラムのロールアップ 2](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> 新しいサイトをインストールするには、Configuration Manager の基準バージョンを使用する必要があります。  
>  詳細については、下記のリンクをクリックしてください。    
>   - [新しいサイトのインストール](/sccm/core/servers/deploy/install/installing-sites)  
>   - [サイトで更新プログラムをインストールする](/sccm/core/servers/manage/updates)  
>   - [基準バージョンと更新プログラムのバージョン](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

次の各セクションでは、Configuration Manager のバージョン 1710 で導入された変更点および新機能について詳しく説明します。  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>サイトのインフラストラクチャ

### <a name="updates-for-peer-cache-----sms500850---"></a>ピア キャッシュの更新プログラム  <!-- sms500850 -->
今回のリリース以降、ピア キャッシュはプレリリース機能ではなくなりました。  今回のリリースでは、ピア キャッシュのその他の変更は導入されませんでした。 詳細については、「[Configuration Manager クライアントのピア キャッシュ](/sccm/core/plan-design/hierarchy/client-peer-cache)」を参照してください。

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>クラウド配布ポイントの Azure Government クラウドのサポート   <!-- sms491428 -->
Azure Government クラウドで[クラウドベースの配布ポイント](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)を使用できるようになりました。   

### <a name="inventory-default-unit-revision----sms503697---"></a>インベントリの既定の単位のリビジョン <!-- sms503697 -->
デバイスにギガバイト (GB)、テラバイト (TB)、およびそれより大きいサイズのハード ドライブが含まれるようになったため、このリリースでは、多くのビューで使用される既定の単位 (SMS_Units) をメガバイト (MB) から GB に変更しています。 たとえば、v_gs_LogicalDisk.FreeSpace 値では GB 単位で報告されるようになりました。


<!-- ## Migration  -->


## <a name="client-management"></a>クライアント管理

### <a name="co-management-for-windows-10-devices"></a>Windows 10 デバイスの共同管理    
<!-- 1350871 -->以前の Windows 10 の更新プログラムで、Windows 10 デバイスをオンプレミスの Active Directory (AD) とクラウドベースの Azure AD に同時に結合できるようになっています (ハイブリッド Azure AD)。 Configuration Manager バージョン 1710 以降、共同管理ではこの機能強化を活用し、Configuration Manager と Intune の両方を使用して複数の Windows 10 バージョン 1709 (Fall Creators Update とも呼ばれる) のデバイスを同時に管理できるようになりました。 これは、従来の管理から最新の管理への橋渡しとなるソリューションであり、段階的なアプローチを使って移行する方向を提示します。 詳細については、「[Windows 10 デバイスの共同管理](/sccm/comanage/overview)」をご覧ください。

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Configuration Manager コンソールからコンピューターを再起動 <!-- 1356283 -->
これ以降のリリースでは、Configuration Manager コンソールを使用して再起動を必要とするクライアント デバイスを識別し、再起動するようにクライアント通知を行うアクションを使用できます。

「[System Center Configuration Manager でクライアントを管理する方法](/sccm/core/clients/manage/manage-clients#restart-clients)」を参照してください。


<!-- ## Compliance settings -->


## <a name="application-management"></a>アプリケーション管理
### <a name="improvements-for-run-scripts------1236459---"></a>スクリプトの実行の改善   <!-- 1236459 -->
今回のリリースでは、**スクリプトの実行**機能がいくつか改善され、マネージド デバイス上で実行する PowerShell スクリプトを展開できるようになりました。 この機能はバージョン 1706 で初めて導入されました。

次のような改善点があります。
- セキュリティ スコープを使用してスクリプトの実行を使用できるユーザーを制御する
- 実行するスクリプトのリアルタイム監視
- スクリプトのパラメーターはスクリプトの作成ウィザードに表示され、検証をサポートしています。また、必須または省略可能が指定されています。

スクリプトの実行の使用については、[スクリプトの作成と実行](../../../apps/deploy-use/create-deploy-scripts.md)に関するページを参照してください。

### <a name="new-mobile-application-management-policy-settings"></a>新しいモバイル アプリケーション管理ポリシーの設定
<!-- 1324760 -->次の設定がモバイル アプリケーション管理ポリシーの設定に追加されました。
- **連絡先の同期を無効にする**: アプリでデバイス上のネイティブ連絡先アプリにデータを保存できなくなります。
- **印刷を無効にする**: アプリで職場または学校のデータを印刷できなくなります。

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>ソフトウェア センターで 250x250 を超えるアイコンが変形しなくなります  
<!-- 1356194 -->

今回のリリース以降、ソフトウェア センターではアイコンのサイズが 250 x 250 を超えてもアイコンが変形しなくなります。 そのようなアイコンはソフトウェア センターではぼやけて表示されます。 最大 512x512 のピクセル寸法でアイコンを設定でき、変形することなく表示されます。

ソフトウェア センターでアプリのアイコンを追加するには、[アプリケーションの作成](/sccm/apps/deploy-use/create-applications)に関するページを参照してください。

## <a name="operating-system-deployment"></a>オペレーティング システムの展開
 > [!TIP]   
 > <!-- 1354281 -->Windows 10 バージョン 1709 (Fall Creators Update とも呼ばれます) リリース以降、Windows メディアには複数のエディションが含まれるようになりました。 オペレーティング システム アップグレード パッケージまたはオペレーティング システム イメージを使用するようにタスク シーケンスを構成する場合は、必ず [Configuration Manager による使用をサポートしているエディション](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client)を選択してください。

### <a name="add-child-task-sequences-to-a-task-sequence"></a>子タスク シーケンスをタスク シーケンスに追加する
<!-- 1261338 -->

別のタスク シーケンスを実行する新しいタスク シーケンスのステップを追加することができ、タスク シーケンス間に親子関係を作成できます。 これにより、再利用可能なモジュール型のタスク シーケンスをより多く作成できます。  

子タスク シーケンスの詳細については、[子タスク シーケンス](/sccm/osd/understand/task-sequence-steps#child-task-sequence)に関するセクションを参照してください。

## <a name="software-center-customization"></a>ソフトウェア センターのカスタマイズ
<!-- 1351224 -->エンタープライズ ブランド要素を追加して、ソフトウェア センターのタブの表示を指定できます。 ソフトウェア センターに特定の会社名を追加したり、ソフトウェア センターの構成の基調となる色を設定したり、会社のロゴを設定したり、またはクライアント デバイスに表示されるタブを設定したりできます。

詳細については、「[System Center Configuration Manager のアプリケーション管理の計画と構成](/sccm/apps/plan-design/plan-for-and-configure-application-management)」を参照してください。

## <a name="software-updates"></a>ソフトウェア更新プログラム

### <a name="surface-driver-updates-----1098490---"></a>Surface ドライバーの更新プログラム  <!-- 1098490 -->
今回のリリース以降、Surface ドライバーの更新プログラムの管理はプレリリース機能ではなくなりました。  


## <a name="reporting"></a>レポート

### <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Windows 10 拡張テレメトリを制限し、Windows Analytics デバイスの正常性に関連したデータのみを送信するようにする
<!-- 1356148 -->

Windows 10 テレメトリ データ コレクション レベルを **[拡張 (制限あり)]** に設定できます。 この設定を行うと、デバイスから **[拡張]** テレメトリ レベルのデータのすべてを報告されなくても、Windows 10 バージョン 1709 以降で、ご利用の環境のデバイスに関する、アクションにつながる有用な情報を得ることができます。

詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](/sccm/core/clients/deploy/configure-client-settings)」を参照してください。

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>モバイル デバイス管理

### <a name="actions-for-non-compliance"></a>コンプライアンス非対応に対するアクション 
<!--1321366 -->    
コンプライアンスに対応していないデバイスに適用される時間順のアクションを構成できるようになりました。 たとえば、コンプライアンスに対応していないデバイスをユーザーに電子メールで通知したり、そのようなデバイスにコンプライアンス非対応とマークしたりすることができます。 詳細については、「[コンプライアンス非対応に対するアクションの設定](/sccm/mdm/deploy-use/actions-for-noncompliance)」を参照してください。

### <a name="windows-10-arm64-device-support"></a>Windows 10 ARM64 デバイスのサポート
<!-- 1355000 -->

Windows 10 を実行する ARM64 デバイスを使用できるようになると、それらのデバイスでハイブリッド モバイル デバイス管理 (MDM) シナリオがサポートされます。

次のようなシナリオがサポートされます。

- [デバイスの登録](../../../mdm/deploy-use/enroll-hybrid-windows.md)
- [リモートの完全ワイプおよび選択的ワイプ アクションの実行](../../../mdm/deploy-use/wipe-lock-reset-devices.md)
- [構成項目とベースラインによる設定の管理](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [コンプライアンス ポリシー](../../../mdm/deploy-use/device-compliance-policies.md)と[条件付きアクセス](../../../protect/deploy-use/manage-access-to-services.md)の管理
- 以下による会社のリソースへのアクセス管理:
   - [証明書プロファイル](../../../mdm/deploy-use/create-pfx-certificate-profiles.md)
   - [VPN プロファイル](../../../mdm/deploy-use/create-vpn-profiles.md)
   - [Wi-Fi プロファイル](../../../mdm/deploy-use/create-wifi-profiles.md)
   - [電子メール プロファイル](../../../mdm/deploy-use/create-exchange-activesync-profiles.md)
- [Windows Hello for Business ポリシーの構成](../../../mdm/deploy-use/windows-hello-for-business-settings.md)
- [アプリケーションを管理する](../../../mdm/deploy-use/management-tasks-applications.md)

> [!NOTE]
> これらのデバイスで複数のアーキテクチャ用にビルドされた .appxbundle アプリケーションの配置は機能しない可能性があり、この時点でこのシナリオはサポートされていません。

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Configuration Manager コンソールの VPN プロファイル エクスペリエンスの向上 
<!-- 1318232 -->

このリリースでは、選択したプラットフォームに適した設定が表示されるように、VPN プロファイル ウィザードとプロパティ ページが更新されました。


- 各プラットフォームには独自のワークフローがあります。つまり、新しい VPN プロファイルには、プラットフォームによってサポートされる設定のみが含まれます。
- **[全般]** ページの後に、**[サポートされているプラットフォーム]** ページが表示されるようになりました。  プロパティの値を設定する前に、プラットフォームを選ぶことができます。
- プラットフォームが **[Android]**、**[Android for Work]**、または **[Windows Phone 8.1]** に設定されている場合は、**[サポートされているプラットフォーム]** ページは必要なく、表示されません。
- Configuration Manager のクライアント ベースのワークフローが、ハイブリッド モバイル デバイス (MDM) のクライアント ベースの Windows 10 ワークフローと統合されました。これらは同じ設定をサポートします。
- 各プラットフォームのワークフローには、そのワークフローに対して適切な設定のみが含まれます。  たとえば、Android のワークフローには Android に適した設定が含まれ、iOS または Windows 10 Mobile に適した設定は表示されなくなりました。
- [自動 VPN] ページは廃止され、削除されました。

これらの変更は、新しい VPN プロファイルに適用されます。  

互換性のリスクを最小限に抑えるため、既存の VPN プロファイルは変更されません。  既存のプロファイルを編集すると、プロファイル作成時のままの設定が表示されます。  

詳細については、「[System Center Configuration Manager のモバイル デバイスの VPN プロファイル](../../../mdm/deploy-use/create-vpn-profiles.md)」を参照してください。

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Cryptography: Next Generation (CNG) 証明書のサポートの制限<!-- 1356191 -->

Configuration Manager では、Cryptography: Next Generation (CNG) 証明書がサポートされます。 Configuration Manager クライアントは、PKI クライアント認証証明書と CNG キー格納プロバイダー (KSP) の秘密キーを使用できます。 Configuration Manager クライアントは KSP をサポートしているので、PKI クライアント認証証明書用の TPM KSP など、ハードウェアベースの秘密キーをサポートしています。

詳細については、「[CNG certificates overview](../network/cng-certificates-overview.md)」(CNG 証明書の概要) を参照してください。

## <a name="protect-devices"></a>デバイスを保護する

### <a name="create-and-deploy-exploit-guard-policies"></a>Exploit Guard ポリシーを作成し、展開する
<!-- 1355468 -->

攻撃の回避、フォルダー アクセスの制御、悪用に対する保護、およびネットワーク保護という、Windows Defender Exploit Guard の 4 つのコンポーネントすべてを管理する[ポリシーを作成し、展開する](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)ことができます。

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Windows Defender Application Guard ポリシーの作成と展開
<!-- 1351960 -->

Configuration Manager Endpoint Protection を使用して [Windows Defender Application Guard ポリシーを作成して展開](/sccm/protect/deploy-use/create-deploy-application-guard-policy)できます。

### <a name="device-guard-policy-changes"></a>Device Guard ポリシーの変更
<!-- 1355092 -->Device Guard ポリシーに関連する次の 3 つの変更が加えられました。

- Device Guard ポリシーは、Windows Defender Application Control ポリシーという名前に変更されました。 そのため、たとえば、**Device Guard ポリシーの作成ウィザード**は **Windows Defender Application Control ポリシーの作成ウィザード**になります。
- Windows バージョン 1709 の Fall Creators Update を使用するデバイスでは、Windows Defender Application Control ポリシーを適用するための再起動は必要なくなりました。 再起動は既定ですが、[再起動を無効にする](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)ことができます。
- インテリジェント セキュリティ グラフから信頼されている[ソフトウェアを自動実行するようにデバイスを設定する](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)ことができます。





## <a name="next-steps"></a>次のステップ
このバージョンをインストールする準備ができたら、[Configuration Manager の更新プログラム](/sccm/core/servers/manage/updates)に関するページを参照してください。
