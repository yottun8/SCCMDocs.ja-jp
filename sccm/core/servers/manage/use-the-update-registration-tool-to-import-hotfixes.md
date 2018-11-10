---
title: 更新登録ツール
titleSuffix: Configuration Manager
description: Configuration Manager コンソールに更新プログラムを手動でインポートするために、どのような場合に、どのような方法で更新登録ツールを使用するかについて説明します。
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 94f0da3fa9f4aa43ce4818b7b6edf752df53d66a
ms.sourcegitcommit: ee434c53b3695a039b56298082b6f61f1006d9dd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49943276"
---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-system-center-configuration-manager"></a>修正プログラムを System Center Configuration Manager にインポートするには、更新登録ツールを使用します。

*適用対象: System Center Configuration Manager (Current Branch)*

一部の Configuration Manager の更新プログラムは、Microsoft クラウド サービスからは使用できず、帯域外でのみ取得されます。 たとえば、特定の問題に対処する限定リリース修正プログラムです。   
帯域外のリリースをインストールする必要があり、更新プログラムまたは修正プログラムのファイル名の末尾に拡張子 **update.exe** が付いている場合、**更新登録ツール**を使用して手動で更新プログラムを Configuration Manager コンソールにインポートします。 このツールを使用すると、更新プログラム パッケージを抽出し、サイト サーバーに転送して、Configuration Manager コンソールに更新プログラムを登録できます。  

 修正プログラム ファイルのファイル拡張子が **.exe** である場合 (ただし、**update.exe** を除く)、「[修正プログラム インストーラーを使用して、System Center Configuration Manager の更新プログラムをインストールする](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)」を参照してください。  

> [!NOTE]  
>  このトピックでは、System Center Configuration Manager を更新する修正プログラムをインストールする方法に関する一般的なガイダンスを提供します。 特定の修正プログラムまたは更新プログラムに関する詳細については、Microsoft サポートで、対応するサポート技術情報 (KB) 記事を参照してください。  

 **更新登録ツールを使用するための前提条件:**  

-   末尾が **.update.exe** という拡張子の帯域外の更新プログラムのみを、このツールを使用してインストールすることができます。  

-   このツールは、Microsoft から直接取得した個々の更新プログラムに対して、自己完結します。  

-   このツールには、サービス接続ポイントのモードとの依存関係はありません。  

-   このツールは、サービス接続ポイントをホストするコンピューターで実行する必要があります。  

-   このツールが実行されるコンピューター (サービス接続ポイント コンピューター) には、.NET Framework 4.52 がインストールされている必要があります。  

-   ツールを実行するために使用するアカウントには、サービス接続ポイントをホストするコンピューター (ツールが実行される) の**ローカル管理者**のアクセス許可が必要です。  

-   ツールの実行に使用するアカウントには、サービス接続ポイントをホストするコンピューターの **&lt;ConfigMgr インストール ディレクトリ\>EasySetupPayload\offline** フォルダーへの**書き込み**アクセス許可が必要です。  

### <a name="to-use-the-update-registration-tool"></a>更新登録ツールを使用するには  

1.  サービス接続ポイントをホストするコンピューターで、以下を実行します。  

    -   管理者特権でコマンド プロンプトを開き、**&lt;製品\>-&lt;製品バージョン\>-&lt;サポート技術情報の記事 ID\>-ConfigMgr.Update.exe** を格納する場所にディレクトリを変更します。  

2.  更新登録ツールを起動するには、次のコマンドを実行します。  

    -   **&lt;製品\>-&lt;製品バージョン\>-&lt;サポート技術情報の記事 ID\>-ConfigMgr.Update.exe**  

    修正プログラムが登録されると、24 時間以内にコンソールに新しい更新プログラムとして表示されます。  次のようにして、プロセスを高速化できます。

    - Configuration Manager コンソールを開き、**[管理]** > **[更新とサービス]** の順に移動して、**[更新プログラムの確認]** をクリックします  (1702 より前のバージョンでは、[更新とサービス] は、**[管理]** > **[クラウド サービス]** にありました)。 

    更新登録ツールは、ローカル コンピューター上の .log ファイルにその操作を記録します。 ログ ファイルは、修正プログラムの .exe ファイルと同じ名前で、**%SystemRoot%Temp** フォルダーに保存されます。  

     更新プログラムが登録されると、更新登録ツールを閉じることができます。  

3.  Configuration Manager コンソールを開き、**[管理]** > **[更新とサービス]** の順に移動します。 インポートされた修正プログラムは、インストールできるようになりました  (1702 より前のバージョンでは、[更新とサービス] は、**[管理]** > **[クラウド サービス]** にありました)。

 更新プログラムのインストールの詳細については、「[Install in-console updates for System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)」(System Center Configuration Manager の更新プログラムのコンソール内インストール) を参照してください。  
