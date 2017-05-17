---
title: "Windows Device Guard の管理方法 | Microsoft Docs"
description: "System Center Configuration Manager を使用して Windows Device Guard を管理する方法について説明します。"
ms.custom: na
ms.date: 04/14/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 49599f529bb409f40caf9057989762e759f1c0ac
ms.openlocfilehash: 113dddb2939fedf24e8d489ff4443bd5e3e72c65
ms.contentlocale: ja-jp
ms.lasthandoff: 05/17/2017


---


# <a name="device-guard-management-with-configuration-manager"></a>Configuration Manager を使用した Device Guard 管理

*適用対象: System Center Configuration Manager (Current Branch)*

## <a name="introduction"></a>概要
Windows Device Guard は、マルウェアやその他の信頼されていないソフトウェアから PC を守るために設計された Windows 10 機能を集めたものです。 承認されているコードのみを実行することで、悪意のあるコードの実行を防ぎます。

Device Guard は、セキュリティ機能に基づき、ソフトウェアとハードウェアの両方を守ります。 CCI (構成可能なコードの整合性) はソフトウェア ベースのセキュリティ層です。この層で、PC 上での実行を許可するソフトウェアの明示的一覧を強制します。 CCI 自体には、ハードウェアの前提条件もファームウェアの前提条件もありません。 Device Guard ポリシーを Configuration Manager で展開すると、以下で説明する Windows バージョンと SKU の最小要件を満たす対象コレクションの PC で CCI ポリシーが有効になります。 任意で、Configuration Manager で展開したコードの整合性ポリシーのハイパーバイザー ベースの保護を対応ハードウェア上でグループ ポリシーにより有効にできます。

Device Guard の詳細については、「[Device Guard 展開ガイド](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)」を参照してください。

Configuration Manager を使用すれば、コレクションの PC で Device Guard を実行するモードを構成できる Device Guard ポリシーを展開できます。 

次のモードのいずれかを構成できます。

1.    **強制の有効化** - 信頼されている実行可能ファイルのみを実行できます。
2.    **監査のみ** - すべての実行可能ファイルの実行を許可しますが、信頼されていない実行可能ファイルが実行された場合、ローカル クライアント イベント ログに記録します。

>[!TIP]
>このバージョンの Configuration Manager では、Device Guard はプレリリース機能です。 有効にする方法については、「[System Center Configuration Manager のプレリリース機能](/sccm/core/servers/manage/pre-release-features)」をご覧ください。

### <a name="what-can-run-when-you-deploy-a-device-guard-policy"></a>Device Guard ポリシーの展開時に実行できるもの

Windows Device Guard では、管理する PC 上で実行できるものを強力に制御できます。 これは、高いセキュリティが導入され、不要なソフトウェアの実行が許可されない部署の PC で特に役立ちます。

ポリシーを実行するときは、一般的に、次の実行可能ファイルの実行が許可されます。

- Windows オペレーティング システムのコンポーネント
- ハードウェア デベロッパー センターのドライバー (Windows Hardware Quality Labs の署名あり)
- Windows ストア アプリ
- Configuration Manager クライアント 
- Device Guard ポリシーの処理後に PC がインストールした Configuration Manager で展開されたすべてのソフトウェアが処理されます。 
- Windows コンポーネントの更新元:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager

>[!IMPORTANT]
>上述のいずれかの更新メカニズムまたはインターネットからインストールされるかどうかに関係なく、インターネットやサードパーティのソフトウェア更新から自動的に更新する Windows に**組み込まれていない**ソフトウェアは上記に含まれていません。 Configuration Manager クライアントで展開されるソフトウェア変更のみが実行を許可されます。

## <a name="before-you-start"></a>アップグレードを開始する前に

Device Guard ポリシーを構成または展開する前に、次の情報をお読みください。

- Device Guard 管理は Configuration Manager のプレリリース機能であり、変更される場合があります。
- Device Guard を使用するには、管理する PC で Windows 10 Enterprise Creators Update 以降を実行する必要があります。
- ポリシーがクライアント PC で処理されると、Configuration Manager はそのクライアントで管理インストーラーとして構成されます。ポリシーの処理後に SCCM で展開されたソフトウェアは自動的に信頼されます。 Device Guard ポリシーの処理前に Configuration Manager によりインストールされたソフトウェアが自動的に信頼されることはありません。
- このプレリリース版では、クライアント PC は Device Guard ポリシーの展開を受け入れると、2 時間という期間でこのポリシーの処理時間をランダム化します。 
- Device Guard ポリシーを正常に処理するには、クライアント PC をドメイン コントローラーに接続する必要があります。
- 展開中に構成可能な、Device Guard ポリシーの既定のコンプライアンスの評価スケジュールは 1 日ごとです。 ポリシー処理で問題が発生した場合、コンプライアンスの評価スケジュールを短く設定すると解消される可能性があります。たとえば、1 時間ごとに設定します。 このスケジュールは、エラーが発生したとき、クライアントが Device Guard ポリシーの処理を再試行する頻度を示します。
- 選択した強制モードに関係なく、Device Guard ポリシーを展開すると、クライアント PC は拡張子が .hta の HTML アプリケーションを実行できなくなります。

## <a name="how-to-create-a-device-guard-policy"></a>Device Guard ポリシーの作成方法
1.    Configuration Manager コンソールで、 **[資産とコンプライアンス]**をクリックします。
2.    **[資産とコンプライアンス]** ワークスペースで **[Endpoint Protection]** を展開してから、**[Device Guard ポリシー]** をクリックします。
3.    **[ホーム]** タブの **[作成]** グループで **[Device Guard ポリシーの作成]** をクリックします。
4.    **Device Guard ポリシーの作成ウィザード**の **[全般]**ページで、次を指定します。
    - **名前**: この Device Guard ポリシーの一意の名前を入力します。 
    - **[説明]** - 必要に応じて、Configuration Manager コンソールで識別に役立ちそうなポリシーの説明を入力します。
    - **強制モード** - クライアント PC の Device Guard に次の強制モードの 1 つを選択します。
        - **強制の有効化** - 信頼されている実行可能ファイルのみを実行できます。
        - **監査のみ** - すべての実行可能ファイルの実行を許可しますが、信頼されていない実行可能ファイルが実行された場合、ローカル クライアント イベント ログに記録します。
5.    **[次へ]** をクリックし、ウィザードを完了します。

## <a name="how-to-deploy-a-device-guard-policy"></a>Device Guard ポリシーの展開方法
1.    Configuration Manager コンソールで、 **[資産とコンプライアンス]**をクリックします。
2.    **[資産とコンプライアンス]** ワークスペースで **[Endpoint Protection]** を展開してから、**[Device Guard ポリシー]** をクリックします。
3.    ポリシーの一覧から展開するポリシーを選択し、**[ホーム]** タブの **[展開]** グループで **[展開]** をクリックします。
4.    **[Deploy Device Guard Policy (Device Guard ポリシーの展開)]** ダイアログ ボックスで、ポリシーを展開するコレクションを選択し、クライアントがポリシーを評価するスケジュールを構成し、最後に、構成されている保守管理期間外でクライアントがポリシーを評価できるか選択します。
5.    完了したら、**[OK]** をクリックしてポリシーを展開します。 

クライアント PC でポリシーが処理されたら、**[コンピューターの再起動]** の **[クライアント設定]** に基づき、そのクライアントで再起動がスケジュールされます。
**クライアント PC を再起動するまで、ポリシーは適用されません。**

## <a name="how-to-monitor-a-device-guard-policy"></a>Device Guard ポリシーの監視方法

展開されたポリシーを監視し、ポリシーがすべての PC に正しく適用されていることを確認するとき、「[Monitor compliance settings](/sccm/compliance/deploy-use/monitor-compliance-settings)」 (コンプライアンス設定を監視する) というトピックの情報が役立ちます。

クライアント PC の次のログ ファイルを使用し、Device Guard ポリシーの処理を監視します。

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

特定のソフトウェアのブロックや監査を検証するには、次のローカル クライアント イベント ログを確認します。 イベント ビューアーでは、関連ログは次のようになっています。

1.    実行可能ファイルをブロックまたは監査するには、**[アプリケーションとサービス ログ]**、**[Microsoft]**、**[Windows]**、**[Code Integrity]**、**[Operational]** の順に選択します。
2.    Windows インストーラーとスクリプト ファイルをブロックまたは監査するには、**[アプリケーションとサービス ログ]**、**[Microsoft]**、**[Windows]**、**[AppLocker]**、**[MSI and Script]** の順に選択します。

## <a name="security-and-privacy-information-for-device-guard"></a>Device Guard のセキュリティとプライバシーの情報

- このプレリリース版では、運用環境の場合、Device Guard ポリシーを **[監査のみ]** 強制モードで展開しないでください。 このモードは機能テストの対象をラボ設定のみとします。
- **[監査のみ]** モードでポリシーが展開されているデバイスや **[強制の有効化]** モードでポリシーを展開しているが、まだ再起動されておらず、ポリシーが適用されていないデバイスは無防備であり、信頼されていないソフトウェアがインストールされます。
そのような状況では、デバイスを再起動しても、**[強制の有効化]** モードでポリシーを受け入れても、ソフトウェアが引き続き実行される可能性があります。
- Device Guard ポリシーが適用されていることを確認するために、ラボ環境でデバイスを用意し、**[強制の有効化]** ポリシーを展開し、デバイスを再起動してからデバイスをエンド ユーザーに提供してください。
- **[強制の有効化]** でポリシーを展開し、その後、**[監査のみ]** で同じデバイスにポリシーを展開する行為はお止めください。 信頼されていないソフトウェアが実行される可能性があります。
- Configuration Manager を利用し、Device Guard ポリシーでクライアント PC の CCI を有効にするとき、ローカル管理者権限を持つユーザーが Device Guard ポリシーを回避したり、その他の方法で信頼されていないソフトウェアを実行したりすることをポリシーで**防げない**ことに注意してください。 
- ローカル管理者権限を持つユーザーが CCI を無効にすることを防ぐ唯一の方法は、署名付きのバイナリ ポリシーを展開することです。これはグループ ポリシーで可能ですが、現在のところ、Configuration Manager ではサポートされていません。
- クライアント PC に管理インストーラーとして Configuration Manager を設定するとき、AppLocker ポリシーが使用されます。 AppLocker は管理インストーラーの識別にのみ利用されます。すべての強制は CCI で行われます。 





