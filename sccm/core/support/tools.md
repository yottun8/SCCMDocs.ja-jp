---
title: Configuration Manager ツール
titleSuffix: Configuration Manager
description: Configuration Manager インフラストラクチャの管理とトラブルシューティングに役立つツールについて説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd23bd523eb64f7d00f71c38c79a180c4e2e569a
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386543"
---
# <a name="configuration-manager-tools"></a>Configuration Manager ツール

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager ツールには、[クライアント ベースのツール](#client-tools)と[サーバー ベースのツール](#server-tools)があります。 これらのツールは、Configuration Manager インフラストラクチャのサポートとトラブルシューティングに役立ちます。 

Configuration Manager バージョン 1806 以降、これらのツールはサイト サーバーの `CD.Latest\SMSSETUP\Tools` フォルダーに含まれるようになりました。 追加でインストールする必要はなくなりました。<!--1357145--> これらのバージョンのツールは、Configuration Manager バージョン 1806 以降で使用してください。

[クライアントとデバイスでサポートされるオペレーティング システム](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)に関するページでサポート対象クライアントとして示されているすべての Windows オペレーティング システムは、これらのツールを使用できます。

> [!Note]  
> [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=50012) は、Microsoft ダウンロード センターから引き続き入手できます。 Configuration Manager バージョンが 1806 以降の場合は、サイト サーバーの CD.Latest フォルダーにあるツールのバージョンを使用してください。 一部のツールは以前はツールキットに含まれていましたが、バージョン 1806 には含まれていませんでした。 これらの以前のバージョンのツールはサポートされなくなりました。


## <a name="client-tools"></a>クライアント ツール

- [CMTrace](/sccm/core/support/cmtrace): Configuration Manager ログ ファイルの表示、監視、および分析を行います  

- [Client Spy](/sccm/core/support/clispy): ソフトウェアの配布、インベントリ、および測定に関する問題を解決します

- [Deployment Monitoring Tool](/sccm/core/support/deployment-monitoring-tool): アプリケーション、更新プログラム、およびベースラインの展開の問題を解決します  

- [Policy Spy](/sccm/core/support/policy-spy): ポリシーの割り当てを表示します  

- [Power Viewer Tool](/sccm/core/support/power-viewer-tool): 電源管理機能の状態を表示します  

- [Send Schedule Tool](/sccm/core/support/send-schedule-tool): 構成基準のスケジュールと評価をトリガーします  

> [!Note]  
> ClientTools フォルダーには、Microsoft.Diagnostics.Tracing.EventSource.dll ファイルも含まれています。 一部のクライアント ツールにはこのライブラリが必要です。 直接使用することはできません。  


## <a name="server-tools"></a>サーバー ツール

- [DP Job Queue Manager](/sccm/core/support/dp-job-manager): 配布ポイントに対するコンテンツ配布ジョブの問題を解決します  

- [Collection Evaluation Viewer](/sccm/core/support/ceviewer): コレクション評価の詳細を表示します  

- [Content Library Explorer](/sccm/core/support/content-library-explorer): コンテンツ ライブラリの単一インスタンス ストアのコンテンツを表示します  

- [Content Library Transfer](/sccm/core/support/content-library-transfer): ドライブ間でコンテンツ ライブラリを転送します  

- [Content Ownership Tool](/sccm/core/support/content-ownership-tool): 孤立したパッケージの所有権を変更します。 これらのパッケージは、所有するサイト サーバーがないサイトに存在します。  

- [Role-based Administration and Auditing Tool](/sccm/core/support/rbaviewer): 管理者の監査ロールの構成を支援します  

- [Run Meter Summarization Tool](/sccm/core/support/run-meter-summ): 使用状況測定の概要作成タスクを実行し、使用状況測定データを分析します

> [!Note]  
> ServerTools フォルダーには、以下のファイルも格納されています 
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll 
>
> 一部のサーバー ツールにはこれらのライブラリが必要です。 直接使用することはできません。  



## <a name="other-tools"></a>その他のツール

- [Content Library Cleanup Tool](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool): `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` で **ContentLibraryCleanup.exe** を使用して、配布ポイントから孤立したコンテンツを削除します。  

- [Hierarchy Maintenance Tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe): サイト サーバー上の `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` 共有フォルダーで **Preinst.exe** を使用して、階層マネージャー コンポーネントにコマンドを渡します。  

- [Update Reset Tool](/sccm/core/servers/manage/update-reset-tool): コンソール内の更新プログラムにダウンロードやレプリケートの問題がある場合に、`CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` で **CMUpdateReset.exe** を使用して問題を解決します。  

- [Service Connection Tool](/sccm/core/servers/manage/use-the-service-connection-tool): サービス接続ポイントがオフラインの場合に、`CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` で **ServiceConnectionTool.exe** を使用してサイトを最新の状態に保ちます。  
