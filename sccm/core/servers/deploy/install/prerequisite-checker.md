---
title: 前提条件チェッカー
titleSuffix: Configuration Manager
description: 前提条件チェッカーを使用して、サイトやサイト システムの役割のインストールを妨げる可能性のある問題を特定し、修正する方法について説明します。
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c28152031a540ea3fd5f2ef7233c24fb86c8b7f7
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422030"
---
# <a name="prerequisite-checker-for-system-center-configuration-manager"></a>System Center Configuration Manager の前提条件チェッカー

*適用対象:System Center Configuration Manager (Current Branch)*

 System Center Configuration Manager サイトをインストールまたはアップグレードするためのセットアップを実行する前や、サイト システムの役割を新しいサーバーにインストールする前に、使用するバージョンの Configuration Manager からこのスタンドアロン アプリケーション (**Prereqchk.exe**) を実行して、サーバーの対応状況を確認することができます。 前提条件チェッカーを使用して、サイトやサイト システムの役割のインストールを妨げる問題を特定し、修正します。  

> [!NOTE]  
>  前提条件チェッカーは、セットアップの過程で必ず実行されます。  

既定で、前提条件チェッカーを実行した場合:  

-   チェッカーが実行されるサーバーが検証されます。  
-   既存のサイト サーバーがあるかどうか、ローカル コンピューターがスキャンされ、そのサイトに該当するチェックだけが実行されます。  
-   サイトが検出されなかった場合は、すべての前提条件の規則が実行されます。  
-   セットアップに必要なソフトウェアと設定がインストールされていることがルールに従って確認されます。 必須ソフトウェアがさらに別の構成やソフトウェア更新プログラムを必要とし、それらが前提条件チェッカーによって確認されない場合があります。  
-   チェック結果は、コンピューターのシステム ドライブ上の **ConfigMgrPrereq.log** ファイルに記録されます。 ログ ファイルには、アプリケーションのインターフェイスに表示されない追加情報が含まれることがあります。  

コマンド プロンプトから、特定のオプションを指定して前提条件チェッカーを実行した場合:  

-   前提条件チェッカーでは、コマンド ラインに指定したサイト サーバーまたはサイト システムに関連したチェックだけが実行されます。  
-   リモート コンピューターを確認するには、ユーザー アカウントに、そのリモート コンピューターに対する管理者権限が必要です。  

前提条件チェッカーが実行する確認の詳細については、「[System Center Configuration Manager の前提条件の確認の一覧](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md)」を参照してください。  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>前提条件チェッカー ファイルを別のコンピューターにコピーする  

1.  エクスプローラーで、次のいずれかの場所に移動します。  

    -   **&lt;*Configuration Manager インストール メディア*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager インストール パス*\>\BIN\X64**  

2.  次のファイルを別のコンピューターのフォルダーにコピーします。  

    -   Prereqchk.exe  
    -   Prereqcore.dll  
    -   Basesql.dll  
    -   Basesvr.dll  
    -   Baseutil.dll  

##  <a name="run-prerequisite-checker-with-default-checks"></a>前提条件チェッカーで既定のチェックを実行する  

1.  エクスプローラーで、次のいずれかの場所に移動します。  

    -   **&lt;*Configuration Manager インストール メディア*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager インストール パス*\>\BIN\X64**  

2.  **prereqchk.exe** を実行して前提条件チェッカーを起動します。   
    既存のサイトが検索され、見つかった場合は、アップグレードの準備ができているかどうかがチェックされます。 サイトが見つからなかった場合は、すべてのチェックが実行されます。 **[サイトの種類]** 列に、規則が関連付けられているサイト サーバーまたはサイト システムの情報が表示されます。  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>コマンド プロンプトから前提条件チェッカーを起動して既定のすべてのチェックを実行する  

1.  コマンド プロンプト ウィンドウを開いて、次のいずれかの場所に移動します。  

    -   **&lt;*Configuration Manager インストール メディア*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager インストール パス*\>\BIN\X64**  

2.  「  **prereqchk.exe /LOCAL** 」と入力して、前提条件チェッカーを起動し、サーバーに対してすべての前提条件チェックを実行します。  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>コマンド プロンプトからオプションを使用して前提条件チェッカーを実行する  

1. コマンド プロンプト ウィンドウを開いて、次のいずれかの場所に移動します。  

   -   **&lt;*Configuration Manager インストール メディア*\>\SMSSETUP\BIN\X64**  
   -   **&lt;*Configuration Manager インストール パス*\>\BIN\X64**  

2. 「**prereqchk.exe**」と入力し、次のコマンドライン オプションを指定します。  

   たとえば、プライマリ サイトをチェックするには、次の構文を使用します。  

      **prereqchk.exe [/NOUI] /PRI /SQL &lt;SQL Server の FQDN\> /SDK &lt;SMS プロバイダーの FQDN\> [/JOIN &lt;中央管理サイトの FQDN\>] [/MP &lt;管理ポイントの FQDN\>] [/DP &lt;配布ポイントの FQDN\>]**  

   **中央管理サイト サーバー**  

   -   **/NOUI**  

        必要なし。 ユーザー インターフェイスを表示せずに前提条件チェッカーを起動します。 このオプションは、他のどのオプションよりも先に入力する必要があります。  

   -   **/CAS**  

        必須。 ローカル コンピューターが、中央管理サイトの要件を満たしているかどうかを確認します。  

   -   **/SQL &lt;*SQL Server の FQDN*>**  

        必須。 完全修飾ドメイン名 (FQDN) を使用して、指定されたコンピューターが、Configuration Manager サイト データベースをホストする SQL Server の要件を満たしているかどうかを確認します。  

   -   **/SDK &lt;*SMS プロバイダーの FQDN*>**  

        必須。 指定されたコンピューターが、SMS プロバイダーの要件を満たしているかどうかを確認します。  

   -   **/Ssbport**  

        必要なし。 ファイアウォールの例外で SQL Server Service Broker (SSB) ポートの通信を許可するように設定されているかどうかを確認します。 既定の SSB ポートは 4022 です。  

   -   **InstallDir &lt;*Configuration Manager インストール パス*>**  

        必要なし。 サイトのインストールに最低限必要な空きディスク領域を確認します。  

   **プライマリ サイト サーバー:**  

   -   **/NOUI**  

       必要なし。 ユーザー インターフェイスを表示せずに前提条件チェッカーを起動します。 このオプションは、他のどのオプションよりも先に入力する必要があります。  

   -   **/PRI**  

        必須。 ローカル コンピューターがプライマリ サイトの要件を満たしているかどうかを確認します。  

   -   **/SQL &lt;*SQL Server の FQDN*>**  

        必須。 指定されたコンピューターが、Configuration Manager サイト データベースをホストする SQL Server の要件を満たしているかどうかを確認します。  

   -   **/SDK &lt;*SMS プロバイダーの FQDN*>**  

        必須。 指定されたコンピューターが、SMS プロバイダーの要件を満たしているかどうかを確認します。  

   -   **/JOIN &lt;*中央管理サイトの FQDN*>**  

        必要なし。 ローカル コンピューターが、中央管理サイト サーバーに接続する要件を満たしているかどうかを確認します。  

   -   **/MP &lt;*管理ポイントの FQDN*>**  

        必要なし。 指定されたコンピューターが、管理ポイントのサイト システムの役割の要件を満たしているかどうかを確認します。 このオプションは、 **/PRI** オプションを使用する場合のみ指定できます。  

   -   **/DP &lt;*配布ポイントの FQDN*>**  

        必要なし。 指定されたコンピューターが、配布ポイントのサイト システムの役割の要件を満たしているかどうかを確認します。 このオプションは、 **/PRI** オプションを使用する場合のみ指定できます。  

   -   **/Ssbport**  

        必要なし。 ファイアウォールの例外で SSB ポートの通信を許可するように設定されているかどうかを確認します。 既定の SSB ポートは 4022 です。  

   -   **InstallDir &lt;*Configuration Manager インストール パス*>**  

        必要なし。 サイトのインストールに最低限必要な空きディスク領域を確認します。  

   **セカンダリ サイト サーバー:**  

   -   **/NOUI**  

        必要なし。 ユーザー インターフェイスを表示せずに前提条件チェッカーを起動します。 このオプションは、他のどのオプションよりも先に入力する必要があります。  

   -   **/SEC &lt;*セカンダリ サイト サーバーの FQDN*>**  

        必須。 指定されたコンピューターがセカンダリ サイトの要件を満たしているかどうかを確認します。  

   -   **/INSTALLSQLEXPRESS**  

        必要なし。 指定されたコンピューターに SQL Server Express をインストールできるかどうかを確認します。  

   -   **/Ssbport**  

        必要なし。 ファイアウォールの例外で SSB ポートの通信を許可するように設定されているかどうかを確認します。 既定の SSB ポートは 4022 です。  

   -   **/Sqlport**  

        必要なし。 ファイアウォールの例外で SQL Server サービス ポートの通信を許可するように設定されており、そのポートが別の SQL Server の名前付きインスタンスで使用されていないことを確認します。 既定のポート番号は 1433 です。  

   -   **InstallDir &lt;*Configuration Manager インストール パス*>**  

        必要なし。 サイトのインストールに最低限必要な空きディスク領域を確認します。  

   -   **/SourceDir**  

        必要なし。 セカンダリ サイトのコンピューター アカウントが、セットアップのソース ファイルをホストするフォルダーにアクセスできるかどうかを確認します。  

   **Configuration Manager コンソール:**  

   -   **/Adminui**  

        必須。 Configuration Manager をインストールするための要件をローカル コンピューターが満たしているかどうかを確認します。  

3. 前提条件チェッカーのユーザー インターフェイスの **[前提条件の確認結果]** セクションに、検出された問題が一覧表示されます。  

   -   一覧にある問題をクリックすると、その解決方法が表示されます。  
   -   サイト サーバー、サイト システム、または Configuration Manager コンソールをインストールする前に、ステータスが **[エラー]** になっている問題をすべて解決する必要があります。  
   -   システム ドライブのルートにある **ConfigMgrPrereq.log** ファイルを開いて、前提条件チェッカーの結果を確認することもできます。 ログ ファイルには、前提条件チェッカーのユーザー インターフェイスに表示されていない情報が含まれていることがあります。  
