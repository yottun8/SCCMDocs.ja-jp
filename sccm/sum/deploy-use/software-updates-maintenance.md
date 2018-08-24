---
title: ソフトウェア更新プログラムのメンテナンス
titleSuffix: Configuration Manager
description: Configuration Manager の更新プログラムをメンテナンスするには、WSUS クリーンアップ タスクをスケジュールするか、手動で実行します。
author: aczechowski
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3a44643870234a08169db1d55cc834e4ca5fcbb5
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385492"
---
# <a name="software-updates-maintenance"></a>ソフトウェア更新プログラムのメンテナンス

*適用対象: System Center Configuration Manager (Current Branch)*

WSUS クリーンアップ タスクは、Configuration Manager コンソールから、またはソフトウェアの更新ポイント コンポーネントのプロパティから、スケジュールして実行することができます。 最初に WSUS クリーンアップ タスクを実行することを選ぶと、次回から、ソフトウェア更新プログラムを最新に保つときにこのタスクが実行されます。  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>WSUS クリーンアップ ジョブをスケジュールし、実行するには 
次の手順を行い、WSUS クリーンアップ ジョブをスケジュールします。   

1.  Configuration Manager コンソールで、**[管理]** > **[概要]** > **[サイト構成]** > **[サイト]** の順に移動します。 
2. Configuration Manager 階層の最上位サイトを選択します。 

3.  **[設定]** グループで **[サイト コンポーネントの構成]** をクリックし、 **[ソフトウェアの更新ポイント]** をクリックして、ソフトウェアの更新ポイント コンポーネントのプロパティを開きます。  

4. **更新プログラムが置き換えられる場合の処理**を確認します。 必要に応じて処理を変更します。 
![更新プログラムが置き換えられる場合の処理のスクリーンショット](media/sccm-supersedence-behavior.PNG)

5.  **[置き換えの規則]** タブをクリックし、**[WSUS クリーンアップ ウィザードの実行]** を選びます。 バージョン 1806 では、オプションの名前が **[Run WSUS cleanup after synchronization]\(同期後に WSUS クリーンアップを実行する\)** に変更されています。 
 
6. **[OK]** (バージョン 1806 を実行している場合は、**[閉じる]**) をクリックします。

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>バージョン 1802 以前の WSUS クリーンアップの動作
Configuration Manager バージョン 1806 より前のバージョンでは、WSUS クリーンアップ オプションで次の項目が実行されます。 
- WSUS クリーンアップ ウィザードの **[期限切れの更新プログラム]** オプションは、最上位サイトの WSUS サーバーでのみ実行されます。 
![WSUS 期限切れの更新プログラムのクリーンアップのスクリーンショット](media/wsus-cleanup-expired.PNG)

-  Configuration Manager データベースでのソフトウェアの更新プログラムの構成アイテムのクリーンアップは、7 日ごとに実行され、コンソールから不要な更新プログラムが削除されます。 
   - このクリーンアップでは、期限切れの更新プログラムが現在展開されている場合には、その更新プログラムは Configuration Manager コンソールから削除されません。 

最上位の WSUS データベースと環境内の他のすべての WSUS データベースには、追加のメンテナンスが引き続き必要です。 詳細と手順については、ブログ記事「[The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://blogs.technet.microsoft.com/configurationmgr/2016/01/26/the-complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maintenance/)」 (Microsoft WSUS と Configuration Manager SUP のメンテナンスの完全ガイド) を参照してください。 


## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>バージョン 1806 以降の WSUS クリーンアップ動作
バージョン 1806 以降では、WSUS クリーンアップのオプションは同期の後に毎回実行され、次のクリーンアップ項目を実行します。<!--1357898 -->
- CAS およびプライマリ サイトでの WSUS サーバーの **[期限切れの更新プログラム]** オプション。
    - セカンダリ サイトの WSUS サーバー。期限切れの更新プログラムに対して WSUS のクリーンアップを実行しないでください。 
- Configuration Manager により、そのデータベースから置き換えられる更新プログラムのリストがビルドされます。 このリストは、ソフトウェアの更新ポイント コンポーネントのプロパティの置き換え動作に基づきます。 
    - 置き換えの動作条件を満たす更新プログラムの構成項目は、Configuration Manager コンソールでは期限切れです。
    - 更新プログラムは、CAS とプライマリ サイトの WSUS では拒否されますが、セカンダリ サイトの WSUS では拒否されません。
- Configuration Manager データベースでのソフトウェアの更新プログラムの構成アイテムのクリーンアップは、7 日ごとに実行され、コンソールから不要な更新プログラムが削除されます。 
    - このクリーンアップでは、期限切れの更新プログラムが現在展開されている場合には、その更新プログラムは Configuration Manager コンソールから削除されません。 

> [!NOTE]
> "置き換えられる更新プログラムが期限切れになるまで待機する月数"は、置き換える更新プログラムの作成日に基づきます。 たとえば、この設定を 2 か月にすると、置き換える更新プログラムが 2 か月経過した時に、置き換えられた更新プログラムは WSUS で拒否され、Configuration Manager で期限切れになります。 

すべての WSUS メンテナンスは、セカンダリ サイトの WSUS データベース上で手動で実行する必要があります。 次の **WSUS サーバー クリーンアップ ウィザード**のオプションは、CAS とプライマリ サイトでは実行されません。

- 使用されていない更新プログラムと更新プログラムのリビジョン
- サーバーに接続しないコンピューター
- 不要な更新ファイル

 詳細と手順については、ブログ記事「[The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://blogs.technet.microsoft.com/configurationmgr/2016/01/26/the-complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maintenance/)」 (Microsoft WSUS と Configuration Manager SUP のメンテナンスの完全ガイド) を参照してください。 

## <a name="updates-cleanup-log-entries"></a>更新プログラムのログ エントリのクリーンアップ
 
このクリーンアップは、次のエントリの wsyncmgr.log で確認することができます。 
  - このログ エントリが表示されたら、WSUS での置き換えられる更新プログラムの拒否は完了です。`Cleanup processed <number> total updates and declined <number>`
  - このエントリが表示されたら、WSUS クリーンアップは開始しています。`Calling WSUS Cleanup.`
  - このエントリが表示されたら、期限切れの更新プログラムの WSUS のクリーンアップは完了です。`Successfully completed WSUS Cleanup.`
  - このエントリが表示されたら、Configuration Manager の期限切れの更新プログラムの構成アイテムのクリーンアップが開始しています。`Deleting old expired updates...`
  - このエントリが表示されたら、Configuration Manager の期限切れの更新プログラムの構成アイテムのクリーンアップは完了です。`Deleted <number> expired updates total`
