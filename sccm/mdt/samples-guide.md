---
title: MDT サンプル
titleSuffix: Microsoft Deployment Toolkit
description: 'Microsoft Deployment Toolkit サンプル。 '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 2ff0100c-b7ef-4e09-8c96-fc1898390b6d
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 6b36da9f98749858829ab591571496532b26f290
ms.sourcegitcommit: 7198ec49d9ce68c6d55bfb9e2d537b5442a132cb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2018
ms.locfileid: "33915974"
---
# <a name="microsoft-deployment-toolkit-samples-guide"></a>Microsoft Deployment Toolkit サンプル ガイド  
 このガイドは Microsoft® Deployment Toolkit (MDT) 2013 に付属し、Windows オペレーティング システムと Microsoft Office の展開に関するガイダンスを専門家チーム向けに提供します。 具体的には、このガイドは特定の展開シナリオに適したサンプル構成設定を示すことを目的としています。  

> [!NOTE]
>  このドキュメントでは、特に指定がない限り、*Windows* という表記は、Windows 8.1、Windows 8、Windows 7、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 の各オペレーティング システムを示します。 MDT では、ARM プロセッサ ベースのバージョンの Windows はサポートされていません。 同様に、特に指定がない限り、*MDT* は MDT 2013 を示します。  

 **このガイドを使用する前に**  

 目次にあるシナリオ トピックの一覧を確認してください。  

1.  組織の展開の目標に最も近いシナリオを選択します。  

2.  選択したシナリオのサンプル構成設定を確認します。  

3.  サンプル構成設定を実際の環境での構成設定の基盤として使用します。  

4.  サンプル構成設定を実際の環境に合わせてカスタマイズします。  

 多くの場合、環境の構成設定を完了するために複数のシナリオが必要になる可能性があります。  

 このガイドに含まれているのはサンプル構成設定のみであるため、環境の構成設定をカスタマイズするとき、詳細については次の表に示すガイドを参考にしてください。  

 |ガイド|ガイドの内容|  
 |-|-|  
 |*クイック スタート ガイド - Microsoft System Center 2012 R2 Configuration Manager* |新しいコンピューターへの展開シナリオにおいて、System Center 2012 R2 Configuration Manager を使用して Windows 8.1 オペレーティング システムをインストールします。|  
 |*クイック スタート ガイド - ライト タッチ インストール* |新しいコンピューターへの展開シナリオにおいて、起動可能なメディアを使用したライト タッチ インストール (LTI) を行うことによって、Windows 8.1 オペレーティング システムをインストールします。|  
 |*クイック スタート ガイド - ユーザー駆動型インストール* |新しいコンピューターへの展開シナリオにおいて、ユーザー駆動型インストールの手法と System Center 2012 R2 Configuration Manager を使用して Windows 8.1 オペレーティング システムをインストールします。|  
 |*Microsoft Deployment Toolkit の使用* |ゼロ タッチ インストール (ZTI) および LTI による展開に使用する構成ファイルをさらにカスタマイズします。 このガイドには、構成全般についてのガイダンスと、構成設定に関するテクニカル リファレンスも収録されています。|


## <a name="deploying-windows-8-applications-using-mdt"></a>MDT を使用した Windows 8 アプリケーションの展開  
 MDT を使用して、.appx というファイル拡張子を持つ Windows 8 アプリケーション パッケージを展開できます。 この形式は、Windows 8 の新しいアプリケーション パッケージです。 この形式のアプリケーションの詳細については、[Microsoft Store アプリの開発](http://msdn.microsoft.com/windows/apps)に関するページをご覧ください。  

 MDT を使用して Windows 8 アプリケーションを展開するには、次の手順を実行します。  

-   「[LTI を使用した Windows 8 アプリケーションの展開](#DeployWin8LTI)」の説明に従って、LTI を使用して Windows 8 アプリケーションを展開します。  

-   「[UDI を使用した Windows 8 アプリケーションの展開](#DeployWin8UDI)」の説明に従って、ユーザー駆動型インストール (UDI) を使用して Windows 8 アプリケーションを展開します。  

###  <a name="DeployWin8LTI"></a> LTI を使用した Windows 8 アプリケーションの展開  
 コマンド ラインからインストール プロセスを開始する他のアプリケーションと同様に、LTI を使用して Windows 8 アプリケーションを展開することができます。 Deployment Workbench の [Applications]\(アプリケーション\) ノードで LTI 展開に Windows 8 アプリケーションを追加できます。  

 **LTI を使用して Windows 8 アプリケーションを展開するには**  

1.  アプリケーションを格納するためのネットワーク共有フォルダーを作成します。  

2.  前の手順で作成したネットワーク共有フォルダーに Windows 8 アプリケーションをコピーします。  

     Windows 8 アプリケーションの .appx ファイルとその他の必要なファイル (アプリケーションの証明書が入っている .cer ファイルなど) をすべてコピーします。  

3.  新しいアプリケーション ウィザードを使用して、Deployment Workbench の [Applications]\(アプリケーション\) ノード上に Windows 8 アプリケーションの LTI アプリケーション項目を作成します。  

     新しいアプリケーション ウィザードへの入力中、ウィザードの **[Command Details]** \(コマンドの詳細\) ページで、**[Command line]** \(コマンド ライン\) に「**app_file_name**」と入力します (*app_file_name* は Windows 8 アプリケーションの名前)。  

     Deployment Workbench で New Application Wizard での設定を完了する方法の詳細については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の次のセクションを参照してください。  

    -   「Create a New Application That Is Deployed from the Deployment Share」 (展開共有から展開される新しいアプリケーションの作成)  

    -   「Create a New Application That Is Deployed from Another Network Shared Folder」 (別のネットワーク共有フォルダーから展開される新しいアプリケーションの作成)  

4.  LTI タスク シーケンスの前の手順で作成した LTI アプリケーション項目を選択します。  

###  <a name="DeployWin8UDI"></a> UDI を使用した Windows 8 アプリケーションの展開  
 コマンド ラインからインストール プロセスを開始する他のアプリケーションと同様に、UDI を使用して Windows 8 アプリケーションを展開することができます。 UDI Wizard Designer の **[ApplicationPage]** ウィザード ページで UDI 展開に Windows 8 アプリケーションを追加できます。  

> [!NOTE]
>  UDI を使用して Windows 8 および Windows 8 アプリケーションを展開するには、System Center 2012 R2 Configuration Manager が必要です。  

 **UDI を使用して Windows 8 アプリケーションを展開するには**  

1.  アプリケーションを格納するためのネットワーク共有フォルダーを作成します。  

     このフォルダーは、以降の手順で作成する Configuration Manager アプリケーション用のソース フォルダーになります。  

2.  前の手順で作成したネットワーク共有フォルダーに Windows 8 アプリケーションをコピーします。  

     Windows 8 アプリケーションの .appx ファイルとその他の必要なファイル (アプリケーションの証明書が入っている .cer ファイルなど) をすべてコピーします。  

3.  Windows 8 アプリケーションを Configuration Manager アプリケーションとして追加します。  

4.  Configuration Manager コンソール上のアプリケーションの作成ウィザードを使用して、Windows 8 アプリケーションの Configuration Manager アプリケーション項目を作成します。  

     アプリケーションの作成ウィザードへの入力中、展開の種類の作成ウィザードを使用して、Windows 8 アプリケーションを展開するための展開の種類を作成します。 展開の種類の作成ウィザードの **[コンテンツ]** ページで、**[インストール プログラム]** に「**app_file_name**」と入力します (*app_file_name* は Windows 8 アプリケーションの名前)。  

     Configuration Manager コンソール上のアプリケーションの作成ウィザードの設定を完了する方法の詳細については、Configuration Manager に付属している System Center 2012 Configuration Manager のドキュメント ライブラリにある次のセクションを参照してください。  

    -   [Configuration Manager でのアプリケーションの作成方法](http://technet.microsoft.com/library/gg682159.aspx)  

    -   [Configuration Manager で展開の種類を作成する方法](http://technet.microsoft.com/library/gg682174.aspx#BKMK_Step3)  

    -   [Configuration Manager でアプリケーションおよび展開の種類を管理する方法](http://technet.microsoft.com/library/gg682031)  

5.  Configuration Manager アプリケーションの展開に必要なユーザーとデバイスのアフィニティをサポートするために、Configuration Manager のユーザーとデバイスのアフィニティ (UDA) 機能が正しく構成されていることを確認します。  

     Configuration Manager アプリケーションの展開をサポートするために UDA を構成する方法の詳細については、「[Configuration Manager でのユーザーとデバイスのアフィニティの管理方法](http://technet.microsoft.com/library/gg699365)」を参照してください。  

6.  手順 4 で作成したアプリケーションを対象ユーザーに展開します。  

     アプリケーションの展開方法の詳細については、「[Configuration Manager でのアプリケーションの展開方法](http://technet.microsoft.com/library/gg682082)」を参照してください。  

7.  UDI Wizard Designer を使用して、手順 4 で作成した Configuration Manager アプリケーションを含むように **[ApplicationPage]** ウィザード ページを構成します。  

     UDI Wizard Designer を使用して **[ApplicationPage]** ウィザード ページを構成する方法の詳細については、MDT ドキュメント「*Quick start Guide for User-Driven Installation*」(クイック スタート ガイド - ユーザー駆動型インストール) の「Step 5-11: Customize the UDI Wizard Configuration File for the Target Computer」(手順 5-11: UDI Wizard の構成ファイルをターゲット コンピューター用にカスタマイズする) セクションを参照してください。  

8.  LTI タスク シーケンスの前の手順で作成した UDI アプリケーション項目を選択します。  

    > [!NOTE]
    >  Windows 8 アプリケーションは、タスク シーケンスではインストールされず、ユーザーによる対象のコンピューターへの初回ログオン時に (手順 5 で構成した UDA 設定での定義に従って)、UDI のユーザー中心のアプリ インストーラー機能 (AppInstall.exe) を使用してインストールされます。  

     UDI で使用するユーザー中心のアプリ インストーラー機能の詳細については、MDT ドキュメントの*ツールキットのリファレンス*に関するページの「User-Centric App Installer Reference」 (ユーザー中心のアプリ インストーラーのリファレンス) セクションを参照してください。  

## <a name="managing-mdt-using-windows-powershell"></a>Windows PowerShell を使用した MDT の管理  
 Deployment Workbench と Windows PowerShell を使用して、MDT 展開共有を管理することができます。 MDT には、Microsoft.BDD.SnapIn という Windows PowerShell™ スナップインが含まれています。Windows PowerShell で MDT 固有の機能を使用する前に、このスナップインを読み込む必要があります。 MDT Windows PowerShell スナップインを構成する要素は次のとおりです。  

-   展開共有のコンテンツへのアクセスを提供する Windows PowerShell プロバイダー (MDTProvider)  

-   MDT 展開共有を管理する機能を提供するコマンドレット  

 Windows PowerShell を使用して MDT 展開共有を管理するには、次の手順を実行します。  

-   「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

-   「[Windows PowerShell を使用した展開共有の作成](#CreateDeployShare)」の説明に従って、Windows PowerShell を使用して展開共有を作成します。  

-   「[Windows PowerShell を使用した展開共有の表示](#ViewDeployShareProp)」の説明に従って、Windows PowerShell を使用して展開共有のプロパティを表示します。  

-   「[Windows PowerShell を使用した展開共有の一覧の表示](#ViewListDeployShare)」の説明に従って、Windows PowerShell を使用して展開共有の一覧を表示します。  

-   「[Windows PowerShell を使用した展開共有の更新](#UpdateDeployShare)」の説明に従って、展開共有を更新します。これにより、新しい Windows Preinstallation Environment (Windows PE) ブート イメージが生成されます。  

-   「[Windows PowerShell を使用した、リンクされた展開共有の更新](#UpdateLinkedDeployShare)」の説明に従って、リンクされた展開共有を更新します。これにより、展開共有からリンクされた展開共有にコンテンツがレプリケートされます。  

-   「[Windows PowerShell を使用した展開メディアの更新](#UpdateDeployMedia)」の説明に従って、展開メディアを更新します。これにより、展開共有から展開メディアにコンテンツがレプリケートされます。  

-   「[Windows PowerShell を使用した展開共有項目の管理](#ManageItemDeployShare)」の説明に従って、展開共有に格納した項目 (オペレーティング システム、オペレーティング システム パッケージ、アプリケーション、デバイス ドライバーなど) を管理します。  

-   「[展開共有の事前設定の自動化](#AutomatePopulateDeployShare)」の説明に従って、展開共有に格納する項目 (オペレーティング システム、オペレーティング システム パッケージ、アプリケーション、デバイス ドライバーなど) の事前設定を自動化します。  

-   「[Windows PowerShell を使用した展開共有フォルダーの管理](#ManageDeployShareFolder)」の説明に従い、Windows PowerShell を使用して、展開共有内のフォルダーを管理します。  

###  <a name="LoadMDTSnapIn"></a> MDT Windows PowerShell スナップインの読み込み  
 MDT コマンドレットは、Windows PowerShell の **Microsoft.BDD.SnapIn** スナップインで提供されます。MDT コマンドレットを使用する前に、このスナップインを読み込む必要があります。 MDT Windows PowerShell スナップインは、次のいずれかの方法を使用して読み込むことができます。  

-   「[システム モジュール インポート タスクを使用した MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapInImport)」の説明に従って、Windows PowerShell モジュール コンソールを使用して MDT Windows PowerShell スナップインを読み込みます。  

-   「[Add-PSSnapIn コマンドレットを使用した MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapInCmdlet)」の説明に従って、**Add-PSSnapIn** コマンドレットを使用して MDT Windows PowerShell スナップインを読み込みます。  

####  <a name="LoadMDTSnapInImport"></a> システム モジュール インポート タスクを使用した MDT Windows PowerShell スナップインの読み込み  
 システム モジュール インポート タスクを実行すると、すべての Windows PowerShell モジュールと各モジュールに含まれるスナップインが、%Windir%\System32\WindowsPowerShell\1.0\Modules ディレクトリに自動的に格納されます。 MDT のインストール プロセス中に、MDT Windows PowerShell の **Microsoft.BDD.SnapIn** スナップインが、そのフォルダーに自動的にインストールされます。  

> [!NOTE]
>  Windows PowerShell 3.0 がコンピューターにインストールされていない場合、システム モジュール インポート タスクは Windows 7 と Windows Server 2008 R2 のみで使用できます。 Windows PowerShell 3.0 以降では、モジュールに含まれているコマンドレットを初めて使用するときにモジュールが自動的にインポートされます。  

 次のいずれかの操作を実行することによって、システム モジュール インポート タスクと同時に Windows PowerShell コンソールを開始できます。  

-   タスク バーで **[Windows PowerShell]** アイコンを右クリックし、**[システム モジュールをインポートする]** をクリックします。  

-   **[スタート]** をクリックし、**[管理ツール]** をポイントして、**[Windows PowerShell Modules]** をクリックします。  

 Windows PowerShell コンソールの開始と同時にシステム モジュールをインポートする方法の詳細については、「[Starting Windows PowerShell with Import System Modules](http://msdn.microsoft.com/library/windows/desktop/hh847866.aspx)」 (システム モジュールのインポートと同時に Windows PowerShell を開始する) を参照してください。  

####  <a name="LoadMDTSnapInCmdlet"></a> Add-PSSnapIn コマンドレットを使用した MDT Windows PowerShell スナップインの読み込み  
 Windows PowerShell 環境から [Add-PSSnapIn](http://technet.microsoft.com/library/hh849705.aspx) コマンドレットを使用して MDT Windows PowerShell の **Microsoft.BDD.PSSnapIn** スナップインを読み込むことができます。次の例を参照してください。  

```  
Add-PSSnapin -Name Microsoft.BDD.PSSnapIn  
```  

###  <a name="CreateDeployShare"></a> Windows PowerShell を使用した展開共有の作成  
 MDT Windows PowerShell コマンドレットを使用して展開共有を作成することができます。 標準の Windows PowerShell コマンドレットと Windows Management Instrumentation (WMI) クラス コマンドの呼び出しを使用して展開共有のルート フォルダーを作成し、共有します。 MDTProvider という Windows PowerShell プロバイダーと、[NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) コマンドレットを使用して、展開共有を事前設定します。 **Add-MDTPersistentDrive** コマンドレットを使用して MDTProvider 用の Windows PowerShell ドライブを永続化します。  

 **MDT Windows PowerShell コマンドレットを使用して展開共有を準備するには**  

1.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

2.  新しい展開共有のルートとなるフォルダーを作成します。これには、次の例に示すように **New-Item** コマンドレットを使用します。「[New-Item コマンドレットの使用](http://technet.microsoft.com/library/ee176914.aspx)」の説明を参照してください。  

    ```  
    New-Item "C:\MDTDeploymentShare$" -Type directory  
    ```  

     コマンドレットによりフォルダーが正常に作成されたことが表示されます。  

3.  前の手順で作成したフォルダーを共有します。これには、次の例に示すように **WMI win32_share** クラスを使用します。  

    ```  
    ([wmiclass]"win32_share").Create("C:\MDTDeploymentShare$", "MDTDeploymentShare$",0)  
    ```  

     **win32_share** クラスを呼び出すと、呼び出しの結果が返されます。 **ReturnValue** の値がゼロ (0) の場合、呼び出しは正常に完了しています。  

4.  新しい共有フォルダーを展開共有として指定します。これには、次の例に示すように [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) コマンドレットを使用します。  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose  
    ```  

     このコマンドレットを使用すると、展開共有の作成と、その新しい展開共有へのテンプレート情報のコピーが自動的に開始されます。 コピー プロセスが完了すると、コマンドレットの表示に、新しい展開共有の情報が示されます。  

    > [!NOTE]
    >  *Name* パラメーターに指定した値 (DS002) は一意である必要があり、既存の展開共有の Windows PowerShell ドライブと同じにすることはできません。  

5.  適切な展開共有フォルダーが作成されたことを確認します。これには、次の例に示すように **dir** コマンドを使用します。  

    ```  
    dir ds002:  
    ```  

     展開共有のルートにある既定のフォルダーの一覧が表示されます。  

6.  永続化された MDT 展開共有の一覧に新しい展開共有を追加します。これには、次の例に示すように **Add-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    $NewDS=Get-PSDrive "DS002"  
    Add-MDTPersistentDrive  -Name "DS002" -InputObject $NewDS Verbose  
    ```  

     この例では、*$NewDS* 変数を使用して新しい展開共有の Windows PowerShell ドライブ オブジェクトをコマンドレットに渡しています。  

     別の方法として、次の例に示すように、[NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) と **Add-MDTPersistentDrive** コマンドレットを結合することもできます。  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose | Add-MDTPersistentDrive -Verbose  
    ```  

     この例では、Windows PowerShell のパイプラインを使って *Name* パラメーターと *InputObject* パラメーターの両方を指定しています。  

###  <a name="ViewDeployShareProp"></a> Windows PowerShell を使用した展開共有プロパティの表示  
 [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) コマンドレットと MDTProvider Windows PowerShell プロバイダーを使用して、MDT 用の展開共有のプロパティを表示することができます。 同じプロパティを Deployment Workbench でも表示できます。  

 **MDT Windows PowerShell コマンドレットを使用して展開共有のプロパティを表示するには**  

1.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

2.  MDT 展開共有用の Windows PowerShell ドライブが復元されていることを確認します。これには、次の例に示すように **Restore-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Windows PowerShell ドライブを共有している MDT 展開が既に復元されている場合は、コマンドレットによるドライブの復元ができないことを示す警告メッセージが表示されます。  

3.  Windows PowerShell ドライブを共有している MDT 展開が正しく復元されていることを確認します。これには、次のように [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットを使用します。  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     MDTProvider を使用して提供されている Windows PowerShell ドライブの一覧が表示されます。  

4.  展開共有のプロパティを表示します。これには、次の例に示すように [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) コマンドレットを使用します。  

    ```  
    Get-ItemProperty "DS002:"  
    ```  

     この例では、*DS002:* が、手順 3 で返された Windows PowerShell ドライブの名前です。 このコマンドレットを実行すると、展開共有のプロパティが返されます。  

###  <a name="ViewListDeployShare"></a> Windows PowerShell を使用した展開共有の一覧の表示  
 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットと MDTProvider Windows PowerShell プロバイダーを使用して、MDT 用の展開共有の一覧を表示することができます。 Deployment Workbench 上でも同じ展開共有の一覧を表示できます。  

 **MDT Windows PowerShell コマンドレットを使用して展開共有の一覧を表示するには**  

1.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

2.  MDT 展開共有用の Windows PowerShell ドライブが復元されていることを確認します。これには、次の例に示すように **Restore-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Windows PowerShell ドライブを共有している MDT 展開が既に復元されている場合は、コマンドレットによるドライブの復元ができないことを示す警告メッセージが表示されます。  

3.  Windows PowerShell ドライブを共有している MDT 展開の一覧を展開共有ごとに表示します。これには、次のように [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットを使用します。  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     MDTProvider を使用して提供されている Windows PowerShell ドライブ (各展開共有に 1 つずつ) の一覧が表示されます。  

###  <a name="UpdateDeployShare"></a> Windows PowerShell を使用した展開共有の更新  
 **Update-MDTDeploymentShare** コマンドレットと MDTProvider Windows PowerShell プロバイダーを使用して、展開共有を更新することができます。 展開共有を更新すると、LTI 展開を開始するために必要な Windows PE ブート イメージ (WIM ファイルおよび ISO (国際標準化機構) ファイル) が作成されます。 「Update a Deployment Share in the Deployment Workbench」 (Deployment Workbench での展開共有の更新) の説明に従って、Deployment Workbench を使用して同じ処理を実行することもできます。  

 **Windows PowerShell を使用して展開共有を更新するには**  

1.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

2.  Windows PowerShell ドライブを共有している MDT 展開が復元されていることを確認します。これには、次の例に示すように **Restore-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Windows PowerShell ドライブを共有している MDT 展開が既に復元されている場合は、コマンドレットによるドライブの復元ができないことを示す警告メッセージが表示されます。  

3.  Windows PowerShell ドライブを共有している MDT 展開が正しく復元されていることを確認します。これには、次のように [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットを使用します。  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     MDTProvider を使用して提供されている Windows PowerShell ドライブの一覧が表示されます。  

4.  次の例に示すように、**Update-MDTDeploymentShare** コマンドレットを使用して展開共有を更新します。  

    ```  
    Update-MDTDeploymentShare -Path "DS002:" -Force  
    ```  

     この例では、*DS002:* が、手順 3 で返された Windows PowerShell ドライブの名前です。  

    > [!NOTE]
    >  展開共有の更新は長時間かかることがあります。 コマンドレットの進行状況は、Windows PowerShell コンソールの上部に表示されます。  

     更新が正常に終了した場合、コマンドレットからの出力は返されません。  

###  <a name="UpdateLinkedDeployShare"></a> Windows PowerShell を使用した、リンクされた展開共有の更新  
 **Update-MDTLinkedDS** コマンドレットと MDTProvider Windows PowerShell プロバイダーを使用して、リンクされた展開共有を更新 (レプリケート) することができます。 リンクされた展開共有を更新すると、元の展開共有からリンクされた展開共有にコンテンツがレプリケートされます。 「Replicate Linked Deployment Shares in the Deployment Workbench」 (Deployment Workbench でのリンクされた展開共有のレプリケート) の説明に従って、Deployment Workbench を使用して同じ処理を実行することもできます。  

 **Windows PowerShell を使用してリンクされた展開共有を更新するには**  

1.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

2.  Windows PowerShell ドライブを共有している MDT 展開が復元されていることを確認します。これには、次の例に示すように **Restore-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Windows PowerShell ドライブを共有している MDT 展開が既に復元されている場合は、コマンドレットによるドライブの復元ができないことを示す警告メッセージが表示されます。  

3.  Windows PowerShell ドライブを共有している MDT 展開が正しく復元されていることを確認します。これには、次のように [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットを使用します。  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     MDTProvider を使用して提供されている Windows PowerShell ドライブの一覧が表示されます。  

4.  次の例に示すように、**Update-MDTDeploymentShare** コマンドレットを使用して展開共有を更新します。  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     この例では、*DS002:* が、手順 3 で返された Windows PowerShell ドライブの名前です。  

    > [!NOTE]
    >  リンクされた展開共有の更新は長時間かかることがあります。 コマンドレットの進行状況は、Windows PowerShell コンソールの上部に表示されます。  

     更新が正常に終了した場合、コマンドレットからの出力は返されません。  

###  <a name="UpdateDeployMedia"></a> Windows PowerShell を使用した展開メディアの更新  
 **Update-MDTMedia** コマンドレットと MDTProvider Windows PowerShell プロバイダーを使用して、展開メディアを更新 (生成) することができます。 展開メディアを更新すると、元の展開共有からリンクされた展開共有にコンテンツがレプリケートされた後、.iso ファイルと .wim ファイルが生成されます。 「Generate Media Images in the Deployment Workbench」 (Deployment Workbench でのメディア イメージの生成) の説明に従って、Deployment Workbench を使用して同じ処理を実行することもできます。  

 **Update-MDTMedia** コマンドレットが完了すると、次のファイルが作成されています。  

-   *media_folder* フォルダー内の .iso ファイル (*media_folder* はメディア用に指定したフォルダーの名前)  

     .iso ファイルの生成はオプションであり、次の方法によって構成します。  

    -   **[media Properties]** \(メディアのプロパティ\) ダイアログ ボックスの **[General]** \(全般\) タブで、**[Generate a Lite Touch bootable ISO image]** \(ライト タッチの起動可能な ISO イメージを生成する\) チェック ボックスをオンにする (メディア生成にかかる時間を短縮するために、起動可能な DVD を作成する場合または .iso ファイルから仮想マシン (VM) を起動する場合を除いて、このチェック ボックスはオフにしてください。)  

    -   [Set-ItemProperty](http://technet.microsoft.com/library/hh849844) コマンドレットを使用して同じプロパティを設定する  

-   *media_folder*\Content\Deploy\Boot フォルダー内の WIM ファイル (*media_folder* は、メディア用に指定したフォルダーの名前)  

 **Windows PowerShell を使用してリンクされた展開共有を更新するには**  

1.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

2.  MDT 展開共有用の Windows PowerShell ドライブが復元されていることを確認します。これには、次の例に示すように **Restore-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Windows PowerShell ドライブを共有している MDT 展開が既に復元されている場合は、コマンドレットによるドライブの復元ができないことを示す警告メッセージが表示されます。  

3.  Windows PowerShell ドライブを共有している MDT 展開が正しく復元されていることを確認します。これには、次のように [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットを使用します。  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     MDTProvider を使用して提供されている Windows PowerShell ドライブの一覧が表示されます。  

4.  次の例に示すように、**Update-MDTDeploymentShare** コマンドレットを使用して展開共有を更新します。  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     この例では、*DS002:* が、手順 3 で返された Windows PowerShell ドライブの名前です。  

    > [!NOTE]
    >  リンクされた展開共有の更新は長時間かかることがあります。 コマンドレットの進行状況は、Windows PowerShell コンソールの上部に表示されます。  

     更新が正常に終了した場合、コマンドレットからの出力は返されません。  

###  <a name="ManageItemDeployShare"></a> Windows PowerShell を使用した展開共有内の項目の管理  
 展開共有には、オペレーティング システム、アプリケーション、デバイス ドライバー、オペレーティング システム パッケージ、タスク シーケンスなどの展開の実行に使用する項目が格納されます。 これらの項目は、Windows PowerShell のコマンドレットと MDT によって提供されるコマンドレットを使用して管理できます。  

 Windows PowerShell コマンドレットを使用して項目を直接操作する方法の詳細については、「[項目を直接操作する](http://technet.microsoft.com/library/dd315266.aspx)」を参照してください。 Windows PowerShell を使用して、展開共有のフォルダー構造を管理することもできます。 詳細については、「[Windows PowerShell を使用した展開共有フォルダーの管理](#ManageDeployShareFolder)」を参照してください。  

####  <a name="ImportItemDeployShare"></a> 展開共有への項目のインポート  
 MDT コマンドレットを使用して、オペレーティング システム、アプリケーション、デバイス ドライバーなどの各種類の項目をインポートできます。 項目の種類ごとに特定の MDT コマンドレットがあります。 Windows PowerShell を使用して展開共有に複数の項目をインポートする場合は、「[展開共有の事前設定の自動化](#AutomatePopulateDeployShare)」を参照してください。  

 展開共有に項目をインポートするために使用する MDT Windows PowerShell コマンドレットの一覧と、各コマンドレットの簡単な説明を次の表に示します。 各コマンドレットに対応するセクションに、各コマンドレットの使用方法を示す例があります。  

 |**コマンドレット** | **説明** |  
 |-|-|  
 |**Import-MDTApplication** |展開共有にアプリケーションをインポートします。|  
 |**Import-MDTDriver** |展開共有に 1 つまたは複数のデバイス ドライバーをインポートします。|  
 |**Import-MDTOperatingSystem** |展開共有に 1 つまたは複数のオペレーティング システムをインポートします。|  
 |**Import-MDTPackage** |展開共有に 1 つまたは複数のオペレーティング システム パッケージをインポートします。|  
 |**Import-MDTTaskSequence** |展開共有にタスク シーケンスをインポートします。|  

####  <a name="ViewPropertyDeployShare"></a> 展開共有内の項目のプロパティを表示  
 展開共有内の項目には、それぞれ異なる一連のプロパティがあります。 [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) コマンドレットを使用して、展開共有内の項目のプロパティを表示できます。 [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) コマンドレットでは、MDTProvider を使用して特定の 1 つの項目のプロパティを表示することができます (Deployment Workbench 上にプロパティを表示できるのと同じです)。  

 Windows PowerShell を使用して展開共有内の複数の項目のプロパティを表示する場合は、「[展開共有の事前設定の自動化](#AutomatePopulateDeployShare)」を参照してください。  

 **Windows PowerShell を使用して展開共有内の 1 つの項目のプロパティを表示するには**  

1.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

2.  Windows PowerShell ドライブを共有している MDT 展開が復元されていることを確認します。これには、次の例に示すように **Restore-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Windows PowerShell ドライブを共有している MDT 展開が既に復元されている場合は、コマンドレットによるドライブの復元ができないことを示す警告メッセージが表示されます。  

3.  Windows PowerShell ドライブを共有している MDT 展開が正しく復元されていることを確認します。これには、次の例に示すように [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットを使用します。  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     MDTProvider を使用して提供されている Windows PowerShell ドライブの一覧が表示されます。  

4.  プロパティを表示する対象である項目の種類に該当する項目の一覧を取得します。これには、次の例に示すように [Get-Item](http://technet.microsoft.com/library/hh849788) コマンドレットを使用します。  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     この例では、展開共有内のすべてのオペレーティング システムの一覧が表示されます。 出力は、パイプを使用して **Format-List** コマンドレットに渡され、オペレーティング システムの長い名前を表示できるように処理されます。 **Format-List** コマンドレットの使用方法の詳細については、「[Format-List コマンドレットの使用](http://technet.microsoft.com/library/ee176830.aspx)」を参照してください。 同じプロセスを使用して (デバイス ドライバーやアプリケーションなどの) その他の種類の項目の一覧を取得できます。  

    > [!TIP]
    >  また、[Get-Item](http://technet.microsoft.com/library/hh849788) コマンドレットを使用するのではなく、**dir** コマンドを使用してオペレーティング システムの一覧を表示することもできます。  

5.  前の手順で表示した項目のうち、いずれか 1 つの項目のプロパティを表示します。これには、次の例に示すように [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) コマンドレットを使用します。  

    ```  
    Get-ItemProperty -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     この例では、*Path* パラメーターの値は、前の手順で返されたファイル名を含む完全修飾パスとして指定した、項目の Windows PowerShell パスです。 同じプロセスを使用して (デバイス ドライバーやアプリケーションなどの) その他の種類の項目のプロパティを表示できます。  

####  <a name="RemoveItemDeployShare"></a> 展開共有からの項目の削除  
 [Remove-Item](http://technet.microsoft.com/library/hh849765) コマンドレットを使用して、展開共有から項目を削除することができます。 [Remove-Item](http://technet.microsoft.com/library/hh849765) コマンドレットでは、MDTProvider を使用して特定の項目を削除することができます (Deployment Workbench 上の項目を削除できるのと同じです)。 Windows PowerShell を使用して展開共有内の複数の項目を削除する場合は、「[展開共有の事前設定の自動化](#AutomatePopulateDeployShare)」を参照してください。  

> [!NOTE]
>  タスク シーケンスで使用されている項目を削除すると、タスク シーケンスにエラーが発生します。 項目を削除する前に、その項目が展開共有内の他の項目によって参照されていないことを確認してください。 項目を削除すると復元することはできません。  

 **Windows PowerShell を使用して展開共有から項目を削除するには**  

1.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

2.  Windows PowerShell ドライブを共有している MDT 展開が復元されていることを確認します。これには、次の例に示すように **Restore-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Windows PowerShell ドライブを共有している MDT 展開が既に復元されている場合は、コマンドレットによるドライブの復元ができないことを示す警告メッセージが表示されます。  

3.  Windows PowerShell ドライブを共有している MDT 展開が正しく復元されていることを確認します。これには、次の例に示すように [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットを使用します。  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     MDTProvider を使用して提供されている Windows PowerShell ドライブの一覧が表示されます。  

4.  プロパティを表示する対象である項目の種類に該当する項目の一覧を取得します。これには、次の例に示すように [Get-Item](http://technet.microsoft.com/library/hh849788) コマンドレットを使用します。  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     この例では、展開共有内のすべてのオペレーティング システムの一覧が表示されます。 出力は、パイプを使用して **Format-List** コマンドレットに渡され、オペレーティング システムの長い名前を表示できるように処理されます。 **Format-List** コマンドレットの使用方法の詳細については、「[Format-List コマンドレットの使用](http://technet.microsoft.com/library/ee176830.aspx)」を参照してください。 同じプロセスを使用して (デバイス ドライバーやアプリケーションなどの) その他の種類の項目の一覧を取得できます。  

    > [!TIP]
    >  また、[Get-Item](http://technet.microsoft.com/library/hh849788) コマンドレットを使用するのではなく、**dir** コマンドを使用してオペレーティング システムの一覧を表示することもできます。  

5.  前の手順で表示した項目のうち、いずれか 1 つの項目を削除します。これには、次の例に示すように [Remove-Item](http://technet.microsoft.com/library/hh849765) コマンドレットを使用します。  

    ```  
    Remove-Item -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     この例では、*Path* パラメーターの値は、前の手順で返されたファイル名を含む完全修飾パスとして指定した、項目の Windows PowerShell パスです。  

     同じプロセスを使用して (デバイス ドライバーやアプリケーションなどの) その他の種類の項目を削除できます。  

    > [!NOTE]
    >  タスク シーケンスで使用されている項目を削除すると、タスク シーケンスにエラーが発生します。 項目を削除する前に、その項目が展開共有内の他の項目によって参照されていないことを確認してください。  

###  <a name="AutomatePopulateDeployShare"></a> 展開共有の事前設定の自動化  
 MDT Windows PowerShell コマンドレットでは、個々の項目を管理できます。 一方、Windows PowerShell のスクリプト機能を使用すると、コマンドレットを用いて展開共有の事前設定を自動化できます。  

 たとえば、さまざまな部署向けに複数の展開共有を展開する必要がある組織や、他の組織向けにオペレーティング システム展開サービスを提供する組織があるとします。 どちらの例でも、組織には、一貫性のある構成がなされた展開共有を作成して事前設定する機能が必要です。  

 複数の項目を管理するための 1 つの方法は、展開共有内の、管理する対象であるすべての項目の一覧を含むコンマ区切り値 (CSV) ファイルを使用することです。そのために、[Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) コマンドレットを使用します。  

 次に示す Windows PowerShell スクリプトの抜粋では、.csv ファイル内の情報に基づいてアプリケーションの一覧をインポートするために、[Import-CSV](http://technet.microsoft.com/library/dd347665.aspx)、[ForEach-Object](http://technet.microsoft.com/library/hh849731)、および **Import-MDTApplication** コマンドレットを使用しています。  

```  
$List=Import-CSV "C:\MDT\Import-MDT-Apps.csv"  
ForEach-Object ($App in $List) {  
Import-MDTApplication –path $App.ApplicationFolder -enable "True" –Name $App.DescriptiveName –ShortName $App.Shortname –Version $App.Version –Publisher $App.Publisher –Language $App.Language –CommandLine $App.CommandLine –WorkingDirectory $App.WorkingDirectory –ApplicationSourcePath $App.SourceFolder –DestinationFolder $App.DestinationFolder –Verbose  
}  
```  

 この例では、C:\MDT\Import-MDT-Apps.csv ファイルに、アプリケーションをインポートするために必要な各変数のフィールドが含まれています。 [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) コマンドレットで使用する .csv ファイルを作成する方法の詳細については、「[Import-Csv コマンドレットの使用](http://technet.microsoft.com/library/ee176874.aspx)」を参照してください。  

 この同じ方法を使用して、オペレーティング システム、デバイス ドライバー、およびその他の項目を展開共有にインポートすることができます。そのためには次の手順を実行します。  

1.  事前設定する展開共有項目の種類ごとに、.csv ファイルを作成します。  

2.  [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) コマンドレットで使用する .csv ファイルを作成する方法の詳細については、「[Import-Csv コマンドレットの使用](http://technet.microsoft.com/library/ee176874.aspx)」を参照してください。  

3.  展開共有の事前設定を自動化するために使用する Windows PowerShell スクリプト ファイルを作成します。  

     Windows PowerShell スクリプトを作成する方法の詳細については、「[Windows PowerShell でのスクリプティング](http://technet.microsoft.com/scriptcenter/powershell.aspx)」を参照してください。  

4.  展開共有項目をインポートする前に、前提条件となる必要なすべてのフォルダー構造を展開共有内に作成します。  

     詳細については、「[Windows PowerShell を使用した展開共有フォルダーの管理](#ManageDeployShareFolder)」を参照してください。  

5.  手順 1 で作成した .csv ファイルのいずれかに [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) コマンドレット行を追加します。  

     [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) コマンドレットの詳細については、「[Import-Csv コマンドレットの使用](http://technet.microsoft.com/library/ee176874.aspx)」を参照してください。  

6.  前の手順の [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) コマンドレットに指定した .csv ファイルにある各項目を処理する [ForEach-Object](http://technet.microsoft.com/library/hh849731) コマンドレットのループを作成します。  

     [ForEach-Object](http://technet.microsoft.com/library/hh849731) コマンドレットの詳細については、「[ForEach-Object コマンドレットの使用](http://technet.microsoft.com/library/ee176828)」を参照してください。  

7.  前の手順で作成した [ForEach-Object](http://technet.microsoft.com/library/hh849731) コマンドレットのループ内に、展開共有項目をインポートする目的に合った MDT コマンドレットを追加します。  

     展開共有に項目をインポートするために使用する MDT コマンドレットの詳細については、「[展開共有への項目のインポート](#ImportItemDeployShare)」を参照してください。  

###  <a name="ManageDeployShareFolder"></a> Windows PowerShell を使用した展開共有フォルダーの管理  
 **mkdir** コマンドなどのコマンド ライン ツールを使用するか、[New-Item](http://technet.microsoft.com/library/hh849795) コマンドレットなどの Windows PowerShell コマンドレットと MDTProvider Windows PowerShell プロバイダーを使用して、展開共有内のフォルダーを管理することができます。 展開共有と同じフォルダー構造を Deployment Workbench 上で表示し、管理することもできます。 Windows PowerShell コマンドレットを使用して項目を直接操作する方法の詳細については、「[項目を直接操作する](http://technet.microsoft.com/library/dd315266.aspx)」を参照してください。  

#### <a name="create-a-folder-in-a-deployment-share-using-windows-powershell"></a>Windows PowerShell を使用した展開共有内のフォルダーの作成  
 **Windows PowerShell を使用して展開共有内にフォルダーを作成するには**  

1.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

2.  Windows PowerShell ドライブを共有している MDT 展開が復元されていることを確認します。これには、次の例に示すように **Restore-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Windows PowerShell ドライブを共有している MDT 展開が既に復元されている場合は、コマンドレットによるドライブの復元ができないことを示す警告メッセージが表示されます。  

3.  Windows PowerShell ドライブを共有している MDT 展開の一覧 (各展開共有に 1 ドライブ) を表示します。これには、次のように [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットを使用します。  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     MDTProvider を使用して提供されている Windows PowerShell ドライブ (各展開共有に 1 つずつ) の一覧が表示されます。  

4.  展開共有内の Operating Systems フォルダーに *Windows_8* というフォルダーを作成します。これには、次の例に示すように **mkdir** コマンドを使用します。  

    ```  
    mkdir "DS002:\Operating Systems\Windows_8"  
    ```  

     この例では、*DS002:* が、手順 3 で返された Windows PowerShell ドライブの名前です。  

5.  次のコマンドを入力して、フォルダーが正常に作成されたことを確認します。  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Windows_8 フォルダーと、Operating Systems フォルダー内の他の既存フォルダー (もしあれば) が表示されます。  

6.  展開共有内の Operating Systems フォルダーに *Windows_7* というフォルダーを作成します。これには、次の例に示すように [New-Item](http://technet.microsoft.com/library/hh849795) コマンドレットを使用します。「[New-Item コマンドレットの使用](http://technet.microsoft.com/library/ee176914.aspx)」の説明を参照してください。  

    ```  
    New-Item "DS002:\Operating Systems\Windows_7" -Type directory  
    ```  

     コマンドレットによりフォルダーが正常に作成されたことが表示されます。  

7.  次のコマンドを入力して、フォルダーが正常に作成されたことを確認します。  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Windows_7 フォルダーと、Operating Systems フォルダー内の他の既存フォルダー (もしあれば) が表示されます。  

#### <a name="delete-a-folder-in-a-deployment-share-using-windows-powershell"></a>Windows PowerShell を使用した展開共有内のフォルダーの削除  
 **Windows PowerShell を使用して展開共有内のフォルダーを削除するには**  

1.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

2.  Windows PowerShell ドライブを共有している MDT 展開が復元されていることを確認します。これには、次の例に示すように **Restore-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Windows PowerShell ドライブを共有している MDT 展開が既に復元されている場合は、コマンドレットによるドライブの復元ができないことを示す警告メッセージが表示されます。  

3.  Windows PowerShell ドライブを共有している MDT 展開の一覧 (各展開共有に 1 ドライブ) を表示します。これには、次のように [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットを使用します。  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     MDTProvider を使用して提供されている Windows PowerShell ドライブ (各展開共有に 1 つずつ) の一覧が表示されます。  

4.  展開共有内の Operating Systems フォルダーにある *Windows_8* というフォルダーを削除します。これには、次の例に示すように **rmdir** コマンドを使用します。  

    ```  
    rmdir "DS002:\Operating Systems\Windows_8"  
    ```  

     この例では、*DS002:* が、手順 3 で返された Windows PowerShell ドライブの名前です。  

5.  次のコマンドを入力して、フォルダーが正常に削除されたことを確認します。  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Operating Systems フォルダー内のフォルダーの一覧に Windows_8 フォルダーはもう表示されません。  

6.  展開共有内の Operating Systems フォルダーにある *Windows_7* というフォルダーを削除します。これには、次の例に示すように [Remove-Item](http://technet.microsoft.com/library/hh849765) コマンドレットを使用します。  

    ```  
    Remove-Item "DS002:\Operating Systems\Windows_7"  
    ```  

     コマンドレットによりフォルダーが正常に削除されたことが表示されます。  

7.  次のコマンドを入力して、フォルダーが正常に作成されたことを確認します。  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Operating Systems フォルダー内のフォルダーの一覧に Windows_7 フォルダーはもう表示されません。  

#### <a name="rename-a-folder-in-a-deployment-share-using-windows-powershell"></a>Windows PowerShell を使用した展開共有内のフォルダーの名前変更  
 **Windows PowerShell を使用して展開共有内のフォルダーの名前を変更するには**  

1.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

2.  MDT 展開共有用の Windows PowerShell ドライブが復元されていることを確認します。これには、次の例に示すように **Restore-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Windows PowerShell ドライブを共有している MDT 展開が既に復元されている場合は、コマンドレットによるドライブの復元ができないことを示す警告メッセージが表示されます。  

3.  MDT 展開共有用の Windows PowerShell ドライブ (各展開共有に 1 つずつ) の一覧を表示します。これには、次のように [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットを使用します。  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     MDTProvider を使用して提供されている Windows PowerShell ドライブ (各展開共有に 1 つずつ) の一覧が表示されます。  

4.  展開共有内の Operating Systems フォルダーにある *Windows_8* というフォルダーの名前を *Win_8* に変更します。これには、次の例に示すように **ren** コマンドを使用します。  

    ```  
    ren "DS002:\Operating Systems\Windows_8" "Win_8"  
    ```  

     この例では、*DS002:* が、手順 3 で返された Windows PowerShell ドライブの名前です。  

5.  次のコマンドを入力して、フォルダーが正常に削除されたことを確認します。  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Windows_8 フォルダーの名前が *Win_8* に変更されました。  

6.  展開共有内の Operating Systems フォルダーにある *Windows_7* というフォルダーの名前を *Win_7* に変更します。これには、次の例に示すように [Rename-Item](http://technet.microsoft.com/library/hh849763) コマンドレットを使用します。  

    ```  
    Rename-Item "DS002:\Operating Systems\Windows_7" "Win_7"  
    ```  

     コマンドレットによりフォルダー名が正常に変更されたことが表示されます。  

7.  次のコマンドを入力して、フォルダーが正常に作成されたことを確認します。  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Windows_7 フォルダーの名前が *Win_7* に変更されました。  

## <a name="automating-the-application-of-operating-system-service-packs-in-deployment-shares"></a>展開共有内のオペレーティング システム サービス パック適用の自動化  
 オペレーティング システム サービス パックは、ソフトウェアのライフ サイクルに標準的に組み込まれています。 展開共有に格納された既存のオペレーティング システムは、新しく展開されたコンピューターや更新されたコンピューター上で最新の推奨セキュリティ機能と構成設定を確実に使用するために、サービス パックを適用して更新する必要があります。  

 ある組織が多数の展開共有を使用していて、各展開共有に複数のオペレーティング システムが格納されているとします。このような場合、サービス パックを適用することによって各展開共有内のオペレーティング システムを手動で更新する処理は、時間がかかる作業です。 展開共有内のオペレーティング システム サービス パック適用を自動化するには、次のような方法があります。  

-   サービス パックが既に含まれている更新されたソースのコンテンツ (Windows 7 SP1 メディアなど) を、既存のオペレーティング システムが格納されている展開共有内のフォルダーにコピーします。「[更新されたソース メディアからのオペレーティング システム サービス パック適用の自動化](#AutomateAppFromUSM)」の説明を参照してください。  

-   参照コンピューターにサービス パックを適用したうえで、更新されたイメージを参照コンピューターからキャプチャします。「[参照コンピューターと Windows PowerShell を使用したオペレーティング システム サービス パック適用の自動化](#AutomateAppUsingRef)」の説明を参照してください。  

###  <a name="AutomateAppFromUSM"></a> 更新されたソース メディアからのオペレーティング システム サービス パック適用の自動化  
 サービス パックが含まれたソース メディア (たとえば、SP1 が既に含まれている Windows 7 の DVD) がある場合は、Windows PowerShell を使用してオペレーティング システム サービス パックの更新プロセスを自動化できます。  

 この方法を使用すると、サービス パックを含むオペレーティング システムのソース メディアが、Windows PowerShell を用いて、展開共有にあるサービス パックを含まない既存のオペレーティング システム ファイルに上書きコピーされます。  

 **Windows PowerShell を使用して、更新されたソース メディアからのオペレーティング システム サービス パックの適用を自動化するには**  

1.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

2.  Windows PowerShell ドライブを共有している MDT 展開が復元されていることを確認します。これには、次の例に示すように **Restore-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Windows PowerShell ドライブを共有している MDT 展開が既に復元されている場合は、コマンドレットによるドライブの復元ができないことを示す警告メッセージが表示されます。  

3.  MDT 展開共有用の Windows PowerShell ドライブ (各展開共有に 1 つずつ) の一覧を表示します。これには、次の例に示すように [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットを使用します。  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     MDTProvider を使用して提供されている Windows PowerShell ドライブ (各展開共有に 1 つずつ) の一覧が表示されます。  

4.  展開共有から既存のオペレーティング システムのフォルダーを削除します。これには、次の例に示すように [Get-ChildItem](http://technet.microsoft.com/library/hh849800) コマンドレットと [Remove-Item](http://technet.microsoft.com/library/hh849765) コマンドレットを使用します。  

    ```  
    Get-ChildItem “DS002:\Operating Systems\Windows 7” –recurse | Remove-Item –recurse –force  
    ```  

     この例では、*DS002:* が、手順 3 で返された Windows PowerShell ドライブの名前です。  

5.  サービス パックを含むオペレーティング システム ソース ファイルのコンテンツをコピーします。これには、次の例に示すように [Copy-Item](http://technet.microsoft.com/library/hh849793) コマンドレットを使用します。  

    ```  
    Copy-Item "E:\*" -Destination "DS002:\Operating Systems\Windows 7"-Recurse -Force  
    ```  

     この例では、オペレーティング システム ソース ファイルはドライブ E 上にあり、*DS002:* が、手順 3 で返された Windows PowerShell ドライブの名前です。  

6.  **Update-MDTMedia** コマンドレットを使用し、展開共有に基づいて MDT 展開メディアを更新します。  

 **Update-MDTMedia** コマンドレットを使用し、展開共有に基づいて MDT 展開メディアを更新する方法の詳細については、「[Windows PowerShell を使用した展開メディアの更新](#UpdateDeployMedia)」を参照してください。  

###  <a name="AutomateAppUsingRef"></a> 参照コンピューターと Windows PowerShell を使用したオペレーティング システム サービス パック適用の自動化  
 オペレーティング システムにまだ適用されていないサービス パック単体の場合 (たとえば Windows 7 のイメージにまだ組み込まれていない Windows 7 用の SP1 など)、Windows PowerShell を使用して、オペレーティング システム サービス パックの更新プロセスを自動化することができます。  

 この方法を使用する場合は、サービス パックを含まないオペレーティング システムを参照コンピューターに展開します。 その後、参照コンピューターにサービス パックを適用します。 次に、参照コンピューターのオペレーティング システム イメージをキャプチャします。 最後に Windows PowerShell を使用して、キャプチャした .wim ファイルを展開共有にあるオペレーティング システムの Install.wim ファイルに上書きコピーします。  

 **Windows PowerShell を使用して、更新されたソース メディアからのオペレーティング システム サービス パックの適用を自動化するには**  

1.  対象のオペレーティング システムを参照コンピューターに展開します。  

     参照コンピューターを展開する方法の詳細については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) にある次のリソースを参照してください。  

    -   「Preparing for LTI Deployment to the Reference Computer」 (参照コンピューターへの LTI 展開の準備)  

    -   「Deploying To and Capturing an Image of the Reference Computer in LTI」 (LTI での参照コンピューターへの展開とイメージのキャプチャ)  

2.  必要なサービス パックを参照コンピューターにインストールします。  

     サービス パックをインストールする方法の詳細については、サービス パックに付属のドキュメントを参照してください。  

3.  参照コンピューターのイメージをキャプチャします。そのためには、**Sysprep and Capture** (システム準備とキャプチャ) のタスク シーケンス テンプレートを基にしたタスク シーケンスを作成して展開します。  

     **Sysprep and Capture** タスク シーケンス テンプレートを基にしたタスク シーケンスの作成の詳細については、「Create a New Task Sequence in the Deployment Workbench」 (Deployment Workbench での新しいタスク シーケンスの作成) を参照してください。  

4.  「[MDT Windows PowerShell スナップインの読み込み](#LoadMDTSnapIn)」の説明に従って、MDT Windows PowerShell スナップインを読み込みます。  

5.  Windows PowerShell ドライブを共有している MDT 展開が復元されていることを確認します。これには、次の例に示すように **Restore-MDTPersistentDrive** コマンドレットを使用します。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Windows PowerShell ドライブを共有している MDT 展開が既に復元されている場合は、コマンドレットによるドライブの復元ができないことを示す警告メッセージが表示されます。  

6.  MDT 展開共有用の Windows PowerShell ドライブ (各展開共有に 1 つずつ) の一覧を表示します。これには、次の例に示すように [Get-PSDrive](http://technet.microsoft.com/library/hh849796) コマンドレットを使用します。  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     MDTProvider を使用して提供されている Windows PowerShell ドライブ (各展開共有に 1 つずつ) の一覧が表示されます。  

7.  手順 3 でキャプチャした .wim ファイルを展開共有にあるオペレーティング システムの Install.wim ファイルに上書きコピーします。これには、次の例に示すように [Copy-Item](http://technet.microsoft.com/library/hh849793) コマンドレットを使用します。  

    ```  
    Copy-Item "DS002:\Captures\Win7SP1.wim" -Destination "DS002:\Operating Systems\Windows 7\sources\Install.wim" Force  
    ```  

     この例では、手順 6 で返された Windows PowerShell ドライブの名前である共有 DS002: の Capture フォルダーにキャプチャされたオペレーティング システム イメージ ファイル (Win7SP1.wim) があり、既存の Windows 7 オペレーティング システムは *Windows 7*という名前のフォルダーに格納されています。  

8.  **Update-MDTMedia** コマンドレットを使用し、展開共有に基づいて MDT 展開メディアを更新します。  

     **Update-MDTMedia** コマンドレットを使用し、展開共有に基づいて MDT 展開メディアを更新する方法の詳細については、「[Windows PowerShell を使用した展開メディアの更新](#UpdateDeployMedia)」を参照してください。  

## <a name="customizing-deployment-based-on-chassis-type"></a>シャーシの種類に基づいた展開のカスタマイズ  
 コンピューターのシャーシの種類に基づいて、展開をカスタマイズすることができます。 スクリプトにより、CustomSettings.ini ファイル内に処理可能なローカル変数が作成されます。 ローカル変数 `IsLaptop`、`IsDesktop`、`IsServer` は、それぞれコンピューターがポータブル コンピューター、デスクトップ コンピューター、サーバーであることを示します。  

> [!NOTE]
>  以前のバージョンの Deployment Workbench では、`IsServer` フラグは、既存のオペレーティング システムがサーバー オペレーティング システム (Windows Server 2003 Enterprise Edition など) であることを示していました。 このフラグは名前が `IsServerOS` に変更されました。  

 **CustomSettings.ini ファイルにローカル変数を実装するには**  

1.  `[Settings]` セクションにある `Priority` の行に、シャーシの種類に基づいて展開をカスタマイズするためのカスタム セクションを追加します (次の例では `ByChassisType` を追加しています。*Chassis* はコンピューターの種類を表します)。  

2.  手順 1 で定義したカスタム セクションに対応するカスタム セクションを作成します (次の例では `ByChassisType` を作成しています。*Chassis* はコンピューターの種類を表します)。  

3.  検出するシャーシの種類ごとにサブセクションを定義します (次の例では `Subsection=Laptop-%IsLaptop%, Subsection=Desktop-%IsDesktop%, Subsection=Server-%IsServer%` を定義しています)。  

4.  手順 3 で定義した各サブセクションに、`True` と `False` それぞれの状態を表すサブセクションを作成します (次の例では `[Laptop-True], [Laptop-False], [Desktop-True], [Desktop-False]` のように作成しています)。  

5.  `True` と `False` の各サブセクションの下に、シャーシの種類に基づいた適切な設定を追加します。  

 **リスト 1.CustomSettings.ini ファイル内のシャーシの種類に基づいて展開をカスタマイズする例**  

```  
[Settings]  

Priority=...,ByLaptopType,ByDesktopType,ByServerType  

[ByLaptopType]  
Subsection=Laptop-%IsLaptop%  

[ByDesktopType]  
Subsection=Desktop-%IsDesktop%  

[ByServerType]  
Subsection=Server-%IsServer%  
.  
.  
.  

[Laptop-True]  
.  
.  
.  

[Laptop-False]  
.  
.  
.  

[Desktop-True]  
.  
.  
.  

[Desktop-False]  
.  
.  
.  

[Server-True]  
.  
.  
.  

[Server-False]  
.  
.  
.  
```  

## <a name="deploying-applications-based-on-earlier-application-versions"></a>アプリケーションの以前のバージョンに基づいたアプリケーションの展開  
 通常、既存のコンピューターにオペレーティング システムをインストールするときは、既にコンピューターにインストールされている同じアプリケーションをインストールします。 これを行うには、MDT スクリプト (特に ZTIGather.wsf) を使用して次の 2 つの独立した情報ソースへのクエリを実行します。  

-   **Configuration Manager ソフトウェア インベントリ機能。** Configuration Manager による前回のコンピューター インベントリ作成時点でインストールされていたアプリケーション パッケージごとに、1 つのレコードが含まれています。この例では、アプリケーション パッケージは、Windows 8.1、Windows 8、Windows 7、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2 の [プログラムと機能] に表示されるものです。  

-   **マッピング テーブル。** レコードごとにどのパッケージとプログラムをインストールする必要があるかを定義します ([プログラムと機能] または [プログラムの追加と削除] では、厳密にどのパッケージによってアプリケーションがインストールされたかは明示されず、インベントリのみに基づいて自動的にパッケージを選択することは不可能であるため)。  

 **コンピューターに固有の動的なアプリケーションのインストールを実行するには**  

1.  MDT DB のテーブルを使用して、対象のオペレーティング システムに登録されているアプリケーションに特定のパッケージを関連付けます。  

2.  [プログラムと機能] または [プログラムの追加と削除] に表示されるアプリケーションに適切なパッケージを関連付けるデータをテーブルに事前設定します。

     **テーブルを事前設定する SQL クエリ**  

    ```  
    use [MDTDB]  
    go  
    INSERT INTO [PackageMapping] (ARPName, Packages) VALUES('Office12.0', 'XXX0000F:Install Office 2010 Professional Plus')  
    go  
    ```  

     挿入した行により、`Office12.0` のエントリを持つすべてのコンピューターが、Microsoft Office 2010 Professional Plus パッケージに関連付けられます。  

     これは、2007 Microsoft Office system (Office 12.0) を現在実行しているすべてのコンピューターに Microsoft Office 2010 Professional Plus がインストールされることを意味します。 その他のパッケージがあれば、同様のエントリを追加します。 エントリがない項目は無視されます (パッケージはインストールされません)。  

3.  新しいテーブル内の情報とインベントリ データを簡単に結合できるようにするため、ストアド プロシージャを作成します。  

    ```  
    use [MDTDB]  
    go  

    if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[RetrievePackages]') and OBJECTPROPERTY(id, N'IsProcedure') = 1)  
    drop procedure [dbo].[RetrievePackages]  
    go  

    CREATE PROCEDURE [dbo].[RetrievePackages]  
    @MacAddress CHAR(17)  
    AS  

    SET NOCOUNT ON  

    /* Select and return all the appropriate records based on current inventory */  
    SELECT * FROM PackageMapping  
    WHERE ARPName IN  
    (  
      SELECT ProdID0 FROM CM_DB.dbo.v_GS_ADD_REMOVE_PROGRAMS a, CM_DB.dbo.v_GS_NETWORK_ADAPTER n  
      WHERE a.ResourceID = n.ResourceID AND  
      MACAddress0 = @MacAddress  
    )  
    go  
    ```  

     上記の例に示したストアド プロシージャでは、SQL Server が MDT DB として実行されているコンピューターに、Configuration Manager の中央プライマリ サイト データベースが格納されていると想定しています。 中央プライマリ サイトのデータベースが別のコンピューター上に配置されている場合は、適切な変更をストアド プロシージャに加える必要があります。 さらに、データベースの名前 (`CM_DB`) を更新する必要があります。 また、Configuration Manager データベースの **v_GS_ADD_REMOVE_PROGRAMS** ビューに対する読み取りアクセス権を追加のアカウントに付与することも検討してください。  

4.  このデータベース テーブルへのクエリを実行するように CustomSettings.ini ファイルを構成します。具体的には、データベースの情報を参照するセクションの名前 (**Priority** リストの `[DynamicPackages]`) を指定します。  

    ```  
    [Settings]  
    …  
    Priority=MacAddress, DefaultGateway, DynamicPackages, Default  
    …  
    ```  

5.  `[DynamicPackages]` セクションを作成し、データベース セクションの名前を指定します。  

    ```  
    [DynamicPackages]  
    SQLDefault=DB_DynamicPackages  
    ```  

6.  データベース セクションを作成し、データベースの情報とクエリの詳細を指定します。  

    ```  
    [DB_DynamicPackages]  
    SQLServer=SERVER1  
    Database=MDTDB  
    StoredProcedure=RetrievePackages  
    Parameters=MacAddress  
    SQLShare=Logs  
    Instance=SQLEnterprise2005  
    Port=1433  
    Netlib=DBNMPNTW  
    ```  

     上記の例では、*SERVER1* という名前の SQL Server インスタンスを実行しているコンピューター上の、*MDTDB* という名前の MDT DB へのクエリが実行されます。 データベースには、`RetrievePackages` という名前のストアド プロシージャが保存されています (手順 3 で作成したもの)。  

 ZTIGather.wsf を実行すると、構造化照会言語 (SQL) の `SELECT` ステートメントが自動的に生成され、**MakeModelQuery** というカスタム キーの値が、クエリにパラメーターとして渡されます。  

 ```  
 EXECUTE RetrievePackages ?  
 ```  

 カスタム キー **MACAddress** の実際の値が、対応する "?" に置き換わります。  このクエリから、手順 2 で入力した行を含むレコード セットが返されます。  

 個数が可変の引数は、ストアド プロシージャに渡すことができません。 そのため、コンピューターに複数の MAC アドレスがある場合、すべての MAC アドレスをストアド プロシージャに渡すことができるとは限りません。 別の方法として、ストアド プロシージャをビューに置き換え、`IN` 句を指定した `SELECT` ステートメントを使用してビューにクエリを実行し、すべての MAC アドレス値を渡します。  

 ここに示したシナリオに基づいて、現在のコンピューターに対して `Office12.0` の値がテーブルに挿入されている場合 (手順 2)、1 つの行 (`XXX0000F:Install Office 2010 Professional Plus`) が返されます。 これは、XXX0000F:Install Office 2001 Professional Plus というパッケージが、状態復元フェーズ中に ZTI プロセスによってインストールされることを示します。  

## <a name="fully-automated-lti-deployment-scenario"></a>完全に自動化された LTI 展開シナリオ  
 LTI の主な目的は、展開プロセスをできるだけ自動化することです。 ZTI は MDT スクリプトと Windows 展開サービスを使用して展開を完全に自動化しますが、LTI は、より少ないインフラストラクチャ要件で実行できるように設計されています。  

 LTI 展開プロセスで使用する Windows Deployment Wizard を自動化し、表示されるウィザードのページを減らす (またはまったく表示させない) ことができます。 CustomSettings.ini に **SkipWizard** プロパティを指定すると、Windows Deployment Wizard 全体をスキップすることができます。 ウィザードの個々のページをスキップするには、次のプロパティを使用します。  

-   **SkipAdminPassword**  

-   **SkipApplications**  

-   **SkipBDDWelcome**  

-   **SkipBitLocker**  

-   **SkipBitLockerDetails**  

-   **SkipTaskSequence**  

-   **SkipCapture**  

-   **SkipComputerBackup**  

-   **SkipComputerName**  

-   **SkipDomainMembership**  

-   **SkipFinalSummary**  

-   **SkipLocaleSelection**  

-   **SkipPackageDisplay**  

-   **SkipProductKey**  

-   **SkipSummary**  

-   **SkipTimeZone**  

-   **SkipUserData**  

これらの各プロパティの詳細については、MDT ドキュメントの*ツールキットのリファレンス*に関するページに記載されているそれぞれのプロパティを参照してください。  

スキップするウィザードのページごとに、対応するプロパティの値を指定します。通常、ウィザードのページから CustomSettings.ini および BootStrap.ini ファイル内に値を収集します。 これらのファイルに構成する必要があるプロパティの詳細については、MDT ドキュメントの*ツールキットのリファレンス*に関するページにある「Providing Properties for Skipped Deployment Wizard Pages」 (スキップした展開ウィザードのページに必要なプロパティの指定) のセクションを参照してください。  

## <a name="fully-automated-lti-deployment-for-a-refresh-computer-scenario"></a>コンピューターの更新シナリオを完全に自動化した LTI 展開  
 次の例は、コンピューターの更新シナリオにおいて、Windows Deployment Wizard のすべてのページをスキップするために使用する CustomSettings.ini ファイルを示しています。 このサンプルでは、ウィザードのページをスキップする場合に使用するプロパティが、ウィザードのページをスキップするプロパティのすぐ下に示されています。  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  
SkipCapture=YES  
SkipAdminPassword=YES  
SkipProductKey=YES  

DeploymentType=REFRESH  

SkipDomainMembership=YES  
JoinDomain=DomainName  
DomainAdmin=Administrator  
DomainAdminDomain=DomainName  
DomainAdminPassword=a_secure_password  

SkipUserData=yes  
UserDataLocation=AUTO  
UDShare=\\Servername\Sharename\Directory  
UDDir=%ComputerName%  

SkipComputerBackup=YES  
ComputerBackuplocation=AUTO  
BackupShare=\\Servername\Backupsharename  
BackupDir=%ComputerName%  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%ComputerName%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  
UserID=Administrator  
UserDomain=DomainName  
UserPassword=P@ssw0rd  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=DomainName\Username  
```  

## <a name="fully-automated-lti-deployment-for-a-new-computer-scenario"></a>新しいコンピューターのシナリオを完全に自動化した LTI 展開  
 次の例は、新しいコンピューターのシナリオにおいて、Windows Deployment Wizard のすべてのページをスキップするために使用する CustomSettings.ini ファイルを示しています。 このサンプルでは、ウィザードのページをスキップする場合に使用するプロパティが、ウィザードのページをスキップするプロパティのすぐ下に示されています。  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  

SkipCapture=YES  
ComputerBackupLocation=\\WDG-MDT-01\Backup$\  
BackupFile=MyCustomImage.wim  

SkipAdminPassword=YES  
SkipProductKey=YES  

SkipDomainMembership=YES  
JoinDomain=WOODGROVEBANK  
DomainAdmin=Administrator  
DomainAdminDomain=WOODGROVEBANK  
DomainAdminPassword=P@ssw0rd  

SkipUserData=Yes  
UserDataLocation=\\WDG-MDT-01\UserData$\Directory\usmtdata  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%SerialNumber%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=WOODGROVEBANK\PilarA  
CaptureGroups=YES  
SLShare=\\WDG-MDT-01\UserData$\Logs  
Home_page=http://www.microsoft.com/NewComputer  
```  

## <a name="calling-web-services-in-mdt"></a>MDT での Web サービスの呼び出し  
 以前のバージョンの MDT では、規則の処理は CustomSettings.ini とデータベースによってサポートされており、このファイルとデータベースから、ローカル コンピューターから収集した値を (通常は WMI を使って) 取得し、展開時に各コンピューターに対して必要な処理を決定することができました。 さらに、SQL クエリやストアド プロシージャ呼び出しを実行して外部データベースから追加情報を取得することもできました。 ただし、その方法には問題があり、特に、安全な SQL 接続を行うことが課題でした。  

 この問題への対応策として、MDT には、CustomSettings.ini に定義した簡単な規則に基づいて Web サービス呼び出しを行う機能が用意されています。 それらの Web サービス要求に特別なセキュリティ上のコンテキストは不要であり、また、必要な任意の TCP/IP ポートを使用できるため、ファイアウォールの構成を簡素化できます。  

 特定の Web サービスを呼び出す CustomSettings.ini の構成方法を次に示します。 このシナリオでは、Web サービスはインターネット検索からランダムに選択されます。 郵便番号が Web サービスに入力として渡され、指定の郵便番号に対応する市区町村、都道府県、市外局番、タイム ゾーン (文字) が返されます。  

```  
[Settings]  
Priority=Default, USZipService  
Properties=USZip, City, State, Zip, Area_Code, Time_Zones   
[Default]  
USZip=98052   
[USZipService]  
WebService=http://www.webservicex.net/uszip.asmx/GetInfoByZIP  
Parameters=USZip  
```  

 このコードを実行すると、次のような出力が生成されます。
```  
Added new custom property USZIP  
Added new custom property CITY  
Added new custom property STATE  
Added new custom property ZIP  
Added new custom property AREA_CODE  
Added new custom property TIME_ZONES  
Using from [Settings]: Rule Priority = DEFAULT, USZIPSERVICE  
------ Processing the [DEFAULT] section ------  
Property USZIP is now = 98052  
Using from [DEFAULT]: USZIP = 98052  
------ Processing the [USZIPSERVICE] section ------  
Using COMMAND LINE ARG: Ini file = CustomSettings.ini  
CHECKING the [USZIPSERVICE] section  
About to execute web service call to http://www.webservicex.net/uszip.asmx/GetInfoByZIP: USZip=98052  
Response from web service: 200 OK  
Successfully executed the web service.  
Property CITY is now = Redmond  
Obtained CITY value from web service:  CITY = Redmond  
Property STATE is now = WA  
Obtained STATE value from web service:  STATE = WA  
Property ZIP is now = 98052  
Obtained ZIP value from web service:  ZIP = 98052  
Property AREA_CODE is now = 425  
Obtained AREA_CODE value from web service:  AREA_CODE = 425  
------ Done processing CustomSettings.ini ------  
```  

 Web サービスを実行するとき、注意する必要があることが何点かあります。  

-   プロキシ サーバーを使って特別な処理を行わないでください。 匿名のプロキシが存在する場合は、それを使用してかまいませんが、プロキシを認証すると問題が発生する可能性があります。 ほとんどの場合、Web サービスは呼び出されません。  

-   CustomSettings.ini または ZTIGather.xml を使用すると、XML マークアップに定義された、Web サービス呼び出しの結果として返されるプロパティが検索されます (データベース クエリやその他の規則を使用する場合と同様)。 ただし、XML 検索では大文字と小文字が区別されます。 さいわい、ここで説明している Web サービスからは、ZTIGather.xml が必要とするすべて大文字のプロパティ名が返されます。 対応策として、小文字の、または大文字と小文字が混在したエントリをマッピングし直すことができます。  

-   Web サービスへの `POST` 要求をお勧めします。Web サービス呼び出しが `POST` をサポートできるようにするためです。  

## <a name="connecting-to-network-resources"></a>ネットワーク リソースへの接続  
 LTI および ZTI の展開処理中に、展開共有をホストしているサーバーとは異なるサーバー上のネットワーク リソースにアクセスすることが必要な場合があります。 他のサーバー上の共有フォルダーまたはサービスにアクセスするためには、そのサーバー上で認証されている必要があります。 たとえば、MDT スクリプト用の展開共有をホストしているサーバーとは異なるサーバー上の共有フォルダーにアプリケーションをインストールすることができます。  

> [!NOTE]
>  展開共有をホストしているサーバー以外のサーバー上でホストされている SQL Server データベースにクエリを実行するには、MDT ドキュメントの*ツールキットのリファレンス*に関するページで **Database**、**DBID**、**DBPwd**、**Instance**、**NetLib**、**Order**、**Parameters**、**ParameterCondition**、**SQLServer**、**SQLShare**、**Table** の各プロパティを参照してください。  

 ZTIConnect.wsf スクリプトを使用して他のサーバーに接続し、そのサーバー上のリソースにアクセスすることができます。 ZTIConnect.wsf スクリプトの構文は次のとおりです (*unc_path* は、サーバー接続用の UNC (汎用名前付け規則) パス)。  

```  
Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:unc_path  
```  

 ほとんどの場合は、タスク シーケンサーのタスクとして ZTIConnect.wsf スクリプトを実行します。 展開共有をホストしているサーバー以外のサーバーへのアクセスが必要なタスクの前に、ZTIConnect.wsf スクリプトを実行します。  

 **ビルドのタスク シーケンスに 1 つのタスクとして ZTIConnect.wsf スクリプトを追加するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Task Sequences に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  詳細ウィンドウ上の ***task_sequence*** をクリックします (*task_sequence* は、変更するタスク シーケンス)。  

4.  操作ウィンドウで **[プロパティ]** をクリックします。  

5.  [Task Sequence]\(タスク シーケンス\) タブをクリックし、**group** (*group* は、ZTIConnec.wsf スクリプトを実行するグループ) に移動して、**[Add]** \(追加\) をクリックします。 **[General]** \(全般\) をクリックし、次に **[Run Command Line]** \(コマンド ラインの実行\) をクリックします。  

    > [!NOTE]
    >  このタスクは、ターゲット サーバー上のリソースへのアクセスを必要とするタスクを追加する前に、追加してください。  

6.  次の情報を使用して新しいタスクの **[Properties]** \(プロパティ\) タブの設定を完了します。

    |**ボックス** |**操作** |  
    |-|-|  
    |**名前** |「**Connect to server**」と入力します (server は、接続先サーバーの名前)。|  
    |**説明** |接続を行う必要がある理由を説明するテキストを入力します。|  
    |**コマンド** |「**Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:unc_path**」と入力します (*unc_path* は、サーバー上の共有フォルダーへの UNC パス)。|  

7.  次の情報を使用して新しいタスクの **[Options]** \(オプション\) タブの設定を完了します。 指定がない限り、既定値をそのまま使用し、**[OK]** をクリックします。  

    |**ボックス** |**操作** |  
    |-|-|  
    |**成功コード** |「**0 3010**」と入力します。 (ZTIConnect.wsf スクリプトが正常に完了したときに返されるコード)|  
    |**条件のリスト ボックス** |必要な条件があれば追加します。 (ほとんどの場合、このタスクに条件は不要です。)|  

 ZTIConnect.wsf スクリプトを実行するタスクを追加した後に、後続のタスクにより、ZTIConnect.wsf スクリプトの **/uncpath** オプションで指定したサーバー上のネットワーク リソースにアクセスできます。  

## <a name="deploying-the-correct-device-drivers-to-computers-with-the-same-hardware-devices-but-different-make-and-model"></a>ハードウェア デバイスが同じで製造元とモデルが異なるコンピューターへの正しいデバイス ドライバーの展開  
 ドライバー セットに実質的な違いはないにもかかわらず、モデル番号と名前が異なる場合があります。 モデル番号と名前にこのような差異があると、特定の 1 つのモデルに対して複数のデータベース エントリを作成するために費やされる時間が不必要に増える可能性があります。 次の手順では、モデル番号を表す部分文字列を返すユーザー出口関数呼び出しを使用して、新しいプロパティを定義する方法を示します。  

 **モデルの別名を作成するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share* に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[プロパティ]** をクリックします。  

4.  **プロパティ**のダイアログ ボックスで、**[Rules]** \(規則\) タブをクリックします。  

5.  MDT DB の [Make and Model]\(製造元とモデル\) のセクションに、ハードウェアの種類を示す別名を作成します。 モデルの型をモデル名の左かっこ "(" の位置で切り捨てます。 たとえば、*HP DL360 (G112)* は、*HP DL360* になります。  

6.  **ModelAlias** というカスタム変数を各セクションに追加します。  

7.  新しい `[SetModel]` セクションを作成します。  

8.  `[Settings]` セクションの **[Priority]** \(優先度\) セクションに `[SetModel]` セクションを追加します。  

9. `ModelAlias` セクションに、モデル名を "(" で切り捨てるユーザー出口スクリプトを参照する行を追加します。  

10. **MMApplications** データベース検索を作成します (**ModelAlias** は **Model** に等しい)。  

11. モデルの名前を切り捨てるユーザー出口スクリプトを作成し、CustomSettings.ini ファイルと同じディレクトリに配置します。  

    次に CustomSettings.ini とユーザー出口スクリプトをそれぞれ示します。  

     **CustomSettings.ini**:  

    ```  
    [Settings]   
    Priority=SetModel, MMApplications, Default   
    Properties= ModelAlias   
    [SetModel]   
    ModelAlias=#SetModelAlias()#   
    Userexit=Userexit.vbs   
    [MMApplications]   
    SQLServer=Server1  
    Database=MDTDB   
    Netlib=DBNMPNTW   
    SQLShare=logs   
    Table= MakeModelSettings    
    Parameters=Make, ModelAlias   
    ModelAlias=Model   
    Order=Sequence  
    ```  

     **ユーザー出口スクリプト**:  

    ```  
    Function UserExit(sType, sWhen, sDetail, bSkip)   
      UserExit = Success   
    End Function   

    Function SetModelAlias()   
      If Instr(oEnvironment.Item("Model"), "(") <> 0 Then   
        SetModelAlias = Left(oEnvironment.Item("Model"), _  
                          Instr(oEnvironment.Item("Model"), _  
                            "(") - 1)   
        oLogging.CreateEntry "USEREXIT – " & _  
          "ModelAlias has been set to " & SetModelAlias, _  
          LogTypeInfo  
      Else   
        SetModelAlias = oEnvironment.Item("Model")   
        oLogging.CreateEntry " USEREXIT - " & _  
          "ModelAlias has not been changed.", LogTypeInfo   
      End if   
    End Function  
    ```  

## <a name="configuring-conditional-task-sequence-steps"></a>条件付きタスク シーケンス ステップの構成  
 シナリオによっては、定義済みの条件に基づく条件付きタスク シーケンス ステップを実行することが適しています。 タスク シーケンス ステップを実行するかどうかを決定するために、条件を組み合わせて追加できます。 たとえば、タスク シーケンス変数の値と、レジストリ設定の値を使用して、タスク シーケンス ステップを実行するかどうかを決定します。  

 MDT を使用して、以下に基づく条件付きタスク シーケンスを実行します。  

-   1 つ以上の **IF** ステートメント  

-   タスク シーケンス変数  

-   対象のオペレーティング システムのバージョン  

-   WMI クエリのブール型の結果  

-   レジストリ設定  

-   ターゲット コンピューターにインストールされているソフトウェア  

-   フォルダーのプロパティ  

-   ファイルのプロパティ  

### <a name="configuring-a-conditional-task-sequence-step"></a>条件付きタスク シーケンス ステップの構成  
 条件付きタスク シーケンス ステップは、Deployment Workbench でタスク シーケンス ステップの **[Options]** \(オプション\) タブに構成します。 タスク シーケンス ステップに 1 つ以上の条件を追加して、ステップを実行する場合または実行しない場合の適切な条件を作成できます。  

> [!NOTE]
>  あらゆる条件付きタスク シーケンス ステップに、少なくとも 1 つの **IF** ステートメントが必要です。  

 **タスク シーケンス ステップの [Options]\(オプション\) タブを表示するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Task Sequences に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  詳細ウィンドウ上の **task_sequence** をクリックします (*task_sequence* は、構成するタスク シーケンスの名前)。  

4.  操作ウィンドウで **[プロパティ]** をクリックします。  

5.  [***task_sequence*** **Properties**]\(task_sequence のプロパティ\) ダイアログ ボックスの **[Task Sequence]** \(タスク シーケンス\) タブで、***step*** をクリックします (*step* は、構成するタスク シーケンス ステップの名前)。次に、**[Options]** \(オプション\) タブをクリックします。  

 タスク シーケンス ステップの **[Options]** \(オプション\) タブで、次の操作を行います。  

-   **[Add]** \(追加\)。 タスク シーケンス ステップに条件を追加するには、このボタンをクリックします。  

-   **[Remove]** \(削除\)。 タスク シーケンス ステップの既存の条件を削除するには、このボタンをクリックします。  

-   **[Edit]** \(編集\)。 タスク シーケンス ステップの既存の条件を編集するには、このボタンをクリックします。  

### <a name="if-statements-in-conditions"></a>条件としての IF ステートメント  
 タスク シーケンスのすべての条件には、1 つ以上の **IF** ステートメントが含まれます。 **IF** ステートメントは、条件付きタスク シーケンス ステップを作成するための基本です。 タスク シーケンス ステップの条件に含めることができる **IF** ステートメントは 1 つだけですが、複数の **IF** ステートメントを最上位レベルの **IF** ステートメントの下に入れ子にすることで、より複雑な条件を作成することができます。  

 **IF** ステートメントは、次の表に示す条件に基づいて、**[IF Statement Properties]** \(IF ステートメントのプロパティ\) ダイアログ ボックスで構成できます。  

 |**条件** |**このオプションを選択した場合のタスク シーケンス実行条件** |  
 |-|-|  
 |**[All conditions]** \(すべての条件\) |この **IF** ステートメントの下にあるすべての条件が、true である必要があります。|  
 |**[Any conditions]** \(いずれかの条件\) |この **IF** ステートメントの下にあるいずれかの条件が、true である場合。|  
 |**なし** |この **IF** ステートメントの下にあるどの条件も、true でない場合。|  

 条件にその他の基準 (たとえば、タスク シーケンス変数やレジストリ設定の値) を追加して、タスク シーケンス ステップを実行するための条件の指定を完了します。  

 **タスク シーケンス ステップに IF ステートメントの条件を追加するには**  

1.  [***step*** **Option**]\(step のオプション\) タブ (*step* は、構成するタスク シーケンス ステップの名前) で、**[Add]** \(追加\) をクリックし、次に **[If statement]** \(IF ステートメント\) をクリックします。  

2.  **[If Statement Properties]** \(IF ステートメントのプロパティ\) ダイアログ ボックスで、**condition** をクリックし (*condition* は、前述の表に示した条件のどれか)、次に **[OK]** をクリックします。  

### <a name="task-sequence-variables-in-conditions"></a>条件としてのタスク シーケンス変数  
 **Task Sequence Variable** (タスク シーケンス変数) 条件を使用して、**Set Task Sequence Variable** (タスク シーケンス変数の設定) タスクによって作成された、またはタスク シーケンス内の任意のタスクによって作成されたタスク シーケンス変数を評価します。 たとえば、Windows XP クライアント コンピューターのネットワークがあり、その中に、ドメインに属するコンピューターと、ワークグループに属するコンピューターがあるとします。 最新のドメイン ポリシーにより、すべてのユーザー設定をネットワーク上に保存することが必要になったため、ドメインに属していないコンピューター、つまり、ワークグループに属するコンピューターについてのみ、ユーザー設定を保存する必要があります。 このような場合、**Capture User Files and Settings** (ユーザー ファイルと設定のキャプチャ) タスクに、ワークグループに属するコンピューターをターゲットにする条件を追加します。  

 **タスク シーケンス変数に基づく条件を追加するには**  

1.  [***step*** **Option**]\(step のオプション\) タブ (*step* は、構成するタスク シーケンス ステップの名前) で、**[Add Condition]** \(条件の追加\) をクリックし、次に **[Task Sequence Variable]** \(タスク シーケンス変数\) をクリックします。  

2.  **[Task Sequence Variable]** \(タスク シーケンス変数\) の条件のダイアログ ボックスで、**[Variable]** \(変数\) ボックスに「**OSDJoinType**」と入力します。  

    > [!NOTE]
    >  この変数は、ドメインに参加しているコンピューターの場合は **0** に設定され、ワークグループに属するコンピューターの場合は **1** に設定されます。  

3.  **[Condition]** \(条件\) ボックスで、**[equal]** \(等しい\) をクリックします。  

4.  **[Value]** \(値\) ボックスに「**1**」を入力し、**[OK]** をクリックします。  

### <a name="operating-system-version-in-conditions"></a>条件としてのオペレーティング システムのバージョン  
 **Operating System Version** (オペレーティング システムのバージョン) 条件を使用して、対象のコンピューターの、または既存のクライアント (イメージをキャプチャする場合) の既存オペレーティング システムのバージョンを確認できます。 たとえば、Windows Server 2003 から Windows Server 2008 にアップグレードする複数のサーバーを含むネットワークがあるとします。 ネットワーク設定をコピーし、Windows Server 2003 を実行しているサーバーのみに適用する必要があります。 その他すべてのサーバーは、Windows Server 2008 の既定のネットワーク設定になります。  

 **オペレーティング システムのバージョンに基づく条件を追加するには**  

1.  Task Sequence Editor で、**[Capture Network Settings]** \(ネットワーク設定のキャプチャ\) タスクをクリックします。  

2.  **[Add Condition]** \(条件の追加\) をクリックし、次に **[Operating System Version]** \(オペレーティング システムのバージョン\) をクリックします。  

3.  **[Architecture]** \(アーキテクチャ\) ボックスで、該当するサーバーをクリックします。 この例では、**[x86]** をクリックします。  

4.  **[Operating system]** \(オペレーティング システム\) ボックスで、条件を設定する対象のオペレーティング システムとバージョンをクリックします。 この例では、**[x86 Windows 2003]** をクリックします。  

5.  **[Condition]** \(条件\) ボックスで関連する条件をクリックし、**[OK]** をクリックします。  

### <a name="file-properties-in-conditions"></a>条件としてのファイルのプロパティ  
 **File Properties** (ファイルのプロパティ) 条件を使用して特定のファイルのバージョンやタイムスタンプを確認し、タスクまたはタスク グループを実行するかどうかを決定できます。 この例の運用環境には、継続的に更新され、ネットワークに追加したすべての新しいサーバーに使用される Windows Server 2003 のイメージが含まれています。 環境内のすべてのサーバー コンピューターでは、デジタル アクセス オブジェクト (DAO) アプリケーション プログラミング インターフェイス (API) バージョン 3.60.6815 を必要とするカスタム アプリケーションを実行します。  

 既存のすべてのサーバーが正常に動作しています。 ただし、イメージを使用してネットワークに追加された新しい各サーバーはアプリケーションを実行できません。 イメージの管理と更新は別のグループが担当しているため、イメージを使用して展開された DAO の既存バージョンが正しくない場合は、DAO の適切なバージョンをインストールするように展開タスク シーケンスを変更することにします。  

 **Configuration Manager 2007 R3 でタスク シーケンス ステップにファイルのプロパティの条件を追加するには**  

1.  DAO 3.60.6815 をインストールするパッケージを Configuration Manager 2007 R3 で作成します。 この *DAO* というパッケージを、*InstallDAO* というプログラムを使用して呼び出します。 パッケージの作成の詳細については、「[パッケージの作成方法](http://technet.microsoft.com/library/bb693627.aspx)」を参照してください。  

2.  DAO パッケージを展開するための **Install Software** (ソフトウェアのインストール) ステップを作成します。  

3.  手順 2 で作成した **[Install Software]** \(ソフトウェアのインストール\) というタスク シーケンス ステップをクリックし、次に **[Options]** \(オプション\) タブをクリックします。  

4.  **[Add Condition]** \(条件の追加\) をクリックし、次に **[File Properties]** \(ファイルのプロパティ\) をクリックします。  

5.  **[Path]** \(パス\) ボックスに「**C:\Program Files\Microsoft Shared\DAO\dao360.dll**」と入力します。  

6.  **[Check the version]** \(バージョンを確認する\) チェック ボックスをオンにし、条件として **[not equals]** \(等しくない\) をクリックします。  

7.  **[Version]** \(バージョン\) ボックスに「**3.60.6815**」を入力します。  

8.  この例では、**[Check the timestamp]** \(タイムスタンプを確認する\) チェック ボックスをオフにして **[OK]** をクリックします。  

### <a name="folder-properties-in-conditions"></a>条件としてのフォルダーのプロパティ  
 **Folder Properties** (フォルダーのプロパティ) 条件を使用して特定のフォルダーのタイムスタンプを確認し、タスクまたはタスク グループを実行するかどうかを決定できます。 たとえば、考えられる状況として、社内で開発したアプリケーションを Windows 8 で使用できるように更新したとします。 しかし、ネットワーク上のすべてのコンピューターにアプリケーションの最新バージョンがインストールされているとは限らないため、アプリケーションをアップグレードする前に、データ変換処理を行う必要があります。  

 アプリケーションがインストールされているフォルダーのタイムスタンプが 2007/12/31 またはそれより前である場合、ターゲット コンピューター上で実行されているアプリケーションは互換性のないバージョンであり、ターゲット コンピューター上でデータ変換処理を実行する必要があります。 アプリケーションの以前のバージョンがインストールされているコンピューター上でデータ変換処理を行うタスク シーケンス ステップを条件付きで実行します。  

 **フォルダーのプロパティの条件をタスク シーケンス ステップに追加するには**  

1.  Configuration Manager コンソールまたは Deployment Workbench のタスク シーケンス エディターで、***task_sequence*** を編集します (*task_sequence* は、編集するタスク シーケンス)。  

2.  データ変換処理を実行するための **Command Line** (コマンド ライン) タスクを作成します。  

3.  手順 1 で作成したタスクをクリックします。  

4.  **[Add Condition]** \(条件の追加\) をクリックし、次に **[Folder Properties]** \(フォルダーのプロパティ\) をクリックします。  

5.  **[Path]** \(パス\) ボックスに、アプリケーションがインストールされているフォルダーのパスを入力します。  

6.  **[Check the timestamp]** \(タイムスタンプを確認する\) チェック ボックスをオンにします。  

7.  条件として **[Less than or equals]** \(指定の値以下\) をクリックします。  

8.  **[Date]** \(日付\) ボックスで **[12/31/2007]** をクリックします。  

9. **[Time]** \(時刻\) ボックスで **[12:00:00 AM]** をクリックし、次に **[OK]** をクリックします。  

### <a name="registry-settings-in-conditions"></a>条件としてのレジストリ設定  
 **Registry Setting** (レジストリ設定) 条件を使用して、レジストリ内のキーと値の有無およびレジストリ値に格納されている対応するデータを確認することができます。 たとえば、少数のコンピューター上で現在使用しているアプリケーションが Windows 8 で実行できず、現在 Windows XP を実行しているコンピューターをアップグレードするための Windows 8 展開を準備したとします。 タスク シーケンスの最初のタスクに条件を作成し、レジストリ内に互換性のないアプリケーションのエントリがあるかどうかを確認して、該当するエントリが見つかった場合には、そのコンピューターの展開プロセスを中断するようにします。  

 **レジストリ設定の条件をタスク シーケンス ステップに追加するには**  

1.  Configuration Manager コンソールまたは Deployment Workbench のタスク シーケンス エディターで、***task_sequence*** を編集します (*task sequence* は、Windows 8 を展開するタスク シーケンス)。  

2.  タスク シーケンスの最初のタスクをクリックし、**[Options]** \(オプション\) タブをクリックします。  

3.  **[Add Condition]** \(条件の追加\) をクリックし、次に **[Registry Setting]** \(レジストリ設定\) をクリックします。  

4.  **[Root key]** \(ルート キー\) の一覧で、**[HKEY_LOCAL_MACHINE]** をクリックします。  

5.  **[Key]** \(キー\) ボックスに「**SOFTWARE\WOODGROVE**」と入力します。  

6.  条件として **[not exists]** \(存在しない\) をクリックします。 この例では、タスクが実行されて、キーが存在しない場合にのみシーケンスが続行します。  

7.  または、**[Value name]** \(値の名前\) ボックスに値の名前を入力した場合は、条件によって値が存在しないことを確認することもできます。  

8.  **exists/not exists** (存在する/存在しない) 以外の条件を使用した場合は、値と値の型を指定します。  

9. **[OK]** をクリックします。  

### <a name="wmi-queries-in-conditions"></a>条件としての WMI クエリ  
 **WMI Query** (WMI クエリ) 条件を使用すると、WMI クエリを実行できます。 このクエリで少なくとも 1 つのレコードが返された場合、この条件は True と評価されます。 たとえば、展開チームが特定のモデル (Dell 1950 など) のすべてのサーバーのオペレーティング システムをアップグレードする必要があるとします。 WMI クエリを使用して各コンピューターのモデルを確認し、適切なモデルが見つかった場合にのみ、展開を続行することができます。  

 **タスク シーケンス ステップに WMI クエリの条件を追加するには**  

1.  Configuration Manager コンソールまたは Deployment Workbench のタスク シーケンス エディターで、***task_sequence*** を編集します (*task sequence* は、サーバーをアップグレードするタスク シーケンス)。  

2.  タスク シーケンスの最初のタスクをクリックし、**[Options]** \(オプション\) タブをクリックします。  

3.  **[Add Condition]** \(条件の追加\) をクリックし、次に **[Query WMI]** \(WMI のクエリ\) をクリックします。  

4.  **[WMI Namespace]** \(WMI 名前空間\) ボックスに「**root\cimv2**」と入力します。  

5.  **[WQL Query]** \(WQL クエリ\) ボックスに「**Select \* From Win32_ComputerSystem WHERE Model LIKE "%Dell%%1950%"**」と入力します。 **[OK]** をクリックします。  

### <a name="installed-software-in-conditions"></a>条件としてのインストール済みソフトウェア  
 **Installed Software** (インストール済みソフトウェア) 条件を使用して、対象のコンピューターに特定のソフトウェアが現在インストール済みであるかどうかを確認できます。 この条件を使用して評価できるのは、Microsoft インストーラー (MSI) ファイルを使用してインストールされたソフトウェアのみです。 たとえば、Microsoft SQL Server 2012 を実行しているサーバーを除くすべてのサーバーのオペレーティング システムをアップグレードするとします。  

 **タスク シーケンス ステップにインストール済みソフトウェアの条件を追加するには**  

1.  Configuration Manager コンソールまたは Deployment Workbench のタスク シーケンス エディターで、***task_sequence*** を編集します (*task sequence* は、サーバーをアップグレードするタスク シーケンス)。  

2.  タスク シーケンスの最初のタスクをクリックし、**[Options]** \(オプション\) タブをクリックします。  

3.  **[Add Condition]** \(条件の追加\) をクリックし、次に **[Installed Software]** \(インストール済みソフトウェア\) をクリックします。  

4.  **[Browse]** \(参照\) をクリックし、SQL Server 2012 の MSI ファイルをクリックします。  

5.  **[Match this specific product]** \(この特定の製品に一致する\) チェック ボックスをオンにすることで、SQL Server 2012 がインストールされているコンピューターのみをこのクエリで検出する対象のコンピューターにする (その他のバージョンはすべて除外する) ことを指定します。  

6.  **[OK]** をクリックします。  

### <a name="complex-conditions"></a>複雑な条件  
 **IF** ステートメントを使用して複数の条件をグループ化し、複雑な条件を作成することができます。 たとえば、特定のステップを、Windows Server 2003 または Windows Server 2008 を実行している Contoso 1950 コンピューターに対してのみ実行する必要があるとします。 プログラムの **IF** ステートメントとして記述した場合は、次のようになります。  

```  
IF ((Computer Model IS “Contoso 1950”) AND (operating system=2003 OR operating system=2008))  
```  

 **複雑な条件を追加するには**  

1.  Configuration Manager コンソールまたは Deployment Workbench のタスク シーケンス エディターで、***task_sequence*** を編集します (*task sequence* は、サーバーをアップグレードするタスク シーケンス)。  

2.  条件を追加するタスク シーケンス ステップをクリックし、**[Options]** \(オプション\) タブをクリックします。  

3.  **[Add condition]** \(条件の追加\) をクリックし、**[If Statement]** \(IF ステートメント\)、**[All conditions]** \(すべての条件\) の順にクリックします。 **[OK]** をクリックします。  

4.  条件ステートメントをクリックし、**[Add condition]** \(条件の追加\)、**[WMI Query]** \(WMI クエリ\) をクリックします。  

5.  WMI 名前空間として **root\cimv2** が指定されていることを確認し、**[WQL Query]** \(WQL クエリ\) ボックスに「**SELECT \* FROM Win32_ComputerSystem WHERE ComputerModel LIKE “%Contoso%1950%”**」と入力します。 **[OK]** をクリックします。  

6.  **IF** ステートメントをクリックし、**[Add condition]** \(条件の追加\) をクリックします。 **[If stamement]** \(IF ステートメント\) をクリックし、次に **[Any condition]** \(任意の条件\) をクリックします。 **[OK]** をクリックします。  

7.  2 番目の **IF** ステートメントをクリックします。 **[Add Condition]** \(条件の追加\) をクリックし、次に **[Operating System Version]** \(オペレーティング システムのバージョン\) をクリックします。  

8.  **[Architecture]** \(アーキテクチャ\) ボックスで、サーバーのアーキテクチャをクリックします。 この例では、**[x86]** をクリックします。  

9. **[Operating system]** \(オペレーティング システム\) ボックスで、オペレーティング システムとバージョンをクリックします。 この例では、**[x86 Windows 2003 original release]** をクリックします。 **[OK]** をクリックします。  

10. 2 番目の **IF** ステートメントをクリックします。 **[Add Condition]** \(条件の追加\) をクリックし、次に **[Operating System Version]** \(オペレーティング システムのバージョン\) をクリックします。  

11. **[Architecture]** \(アーキテクチャ\) ボックスで、サーバーのアーキテクチャをクリックします。 この例では、**[x86]** をクリックします。  

12. **[Operating system]** \(オペレーティング システム\) ボックスで、オペレーティング システムとバージョンをクリックします。 この例では、**[x86 Windows 2008 original release]** をクリックします。 **[OK]** をクリックします。  

## <a name="creating-a-highly-scalable-lti-deployment-infrastructure"></a>高度にスケーラブルな LTI 展開インフラストラクチャの作成  
 このシナリオでは、展開インフラストラクチャとして電子的なソフトウェア配布を利用することができないため、MDT を使用して完全に自動化された LTI 展開インフラストラクチャを構築します。 このスケーラブルな LTI インフラストラクチャでは、SQL Server、Windows 展開サービス、Windows Server 2003 分散ファイル システム レプリケーション (DFS-R) 技術を使用します。  

 スケーラブルな LTI インフラストラクチャを構築する方法は次のとおりです。  

-   適切なインフラストラクチャが存在することを確認します。「[適切なインフラストラクチャが存在することの確認](#EnsureInfrastructure)」の説明を参照してください。  

-   MDT にコンテンツを追加します。「[MDT へのコンテンツの追加](#AddContent)」の説明を参照してください。  

-   Windows 展開サービスを準備します。「[Windows 展開サービスの準備](#PrepareDeployment)」の説明を参照してください。  

-   DFS-R を構成します。「[分散ファイル システム レプリケーションの構成](#ConfigureFileReplication)」の説明を参照してください。  

-   SQL Server レプリケーションに必要な準備をします。「[SQL Server レプリケーションのための準備](#PrepareSQLReplication)」の説明を参照してください。  

-   SQL Server レプリケーションを構成します。「[SQL Server レプリケーションの構成](#ConfigureSQLReplication)」の説明を参照してください。  

 このシナリオは、MDT がマスター展開サーバー上に構成されていて、このドキュメントの冒頭で説明したように MDT DB の構成が既に完了していることを前提にしています。  

###  <a name="EnsureInfrastructure"></a> 適切なインフラストラクチャが存在することの確認  
 高度にスケーラブルな LTI 展開インフラストラクチャでは、コンテンツのレプリケーションにハブとスポークのトポロジを使用します。そのため、運用環境においてマスター展開サーバーの役割を実行する展開サーバーを最初に指定します。  マスター展開サーバーに必要なコンポーネントを次に示します。  

 |**必要なコンポーネント** |**目的やコメント** |  
 |-|-|  
 |Windows Server 2003 R2|DFS-R をサポートするために必要|  
 |MDT |展開共有のマスター コピーを含む|  
 |SQL Server 2005|MDT DB のレプリケーションを可能にするには、完全バージョンであることが必要|  
 |DFS-R |展開共有のレプリケーションに必要|  
 |Windows 展開サービス |ネットワーク PXE ベースのインストールの展開を開始できるようにするために必要|  

 マスター展開サーバーを選択したら、LTI 展開をサポートする追加のサーバーを各サイト上にプロビジョニングします。  子展開サーバーに必要なコンポーネントを次に示します。  

 |**必要なコンポーネント** |**目的やコメント** |  
 |-|-|  
 |Windows Server 2003 R2|DFS-R をサポートするために必要|  
 |Microsoft SQL Server 2005 Express Edition |MDT DB のレプリケートされたコピーを受信|  
 |DFS-R |展開共有のレプリケーションに必要|  
 |Windows 展開サービス |ネットワーク PXE ベースのインストールの展開を開始できるようにするために必要|  

> [!NOTE]
>  それぞれの子サーバー上に Windows 展開サービスをセットアップし、構成する必要がありますが、ブート イメージまたはインストール イメージを追加する必要はありません。  

###  <a name="AddContent"></a> MDT へのコンテンツの追加  
 Deployment Workbench を使用してマスター展開サーバーにコンテンツを事前設定します。また、次の各セクションで説明されている手順に従って、MDT DB を作成して事前設定します。 データベースを事前設定する方法については、以下を参照してください。  

-   アプリケーションの構成については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Configuring Applications in the Deployment Workbench」 (Deployment Workbench でのアプリケーションの構成) のセクションを参照  

-   オペレーティング システムの構成については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Configuring Operating Systems in the Deployment Workbench」 (Deployment Workbench でのオペレーティング システムの構成) のセクションを参照  

-   オペレーティング システム パッケージの構成については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Configuring Packages in the Deployment Workbench」 (Deployment Workbench でのパッケージの構成) のセクションを参照  

-   デバイス ドライバーの構成については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Configuring Device Drivers in the Deployment Workbench」 (Deployment Workbench でのデバイス ドライバーの構成) のセクションを参照  

-   タスク シーケンスの構成については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」の「Configuring Task Sequences in the Deployment Workbench」 (Deployment Workbench でのタスク シーケンスの構成) のセクションを参照  

> [!NOTE]
>  展開共有の更新時に作成した LiteTouchPE_x86.wim ファイルが Windows 展開サービスに追加されていることを確認します。  

###  <a name="PrepareDeployment"></a> Windows 展開サービスの準備  
 LiteTouchPE_x86.wim ファイルは、DFS-R レプリケーション グループによって定期的にレプリケートされるため、新しくレプリケートされた Windows PE 環境を反映するようにブート構成データ ストアを定期的に更新する必要があります。 展開サーバーごとに、次の手順を実行します。  

 **Windows 展開サービスを準備するには**  

1.  コマンド プロンプト ウィンドウを開きます。  

2.  「**WDSUtil/set-server/BCDRefreshPolicy/Enabled:yes/RefreshPeriod:60**」と入力し、Enter キーを押します。  

> [!NOTE]
>  ここに示す例では更新間隔を 60 分に設定していますが、この値は、DFS R の更新間隔と同じ間隔でレプリケートするように構成することもできます。  

###  <a name="ConfigureFileReplication"></a> 分散ファイル システム レプリケーションの構成  
 LTI 展開アーキテクチャをスケーリングするとき、MDT 展開共有と Windows PE ライト タッチ ブート環境およびマスター展開サーバーの両方から子展開サーバーにコンテンツをレプリケートするための基礎として DFS-R を使用します。  

> [!NOTE]
>  以下の手順を実行する前に、DFS-R がインストールされていることを確認します。  

 **展開コンテンツをレプリケートするように DFS-R を構成するには**  

1.  DFS 管理コンソールを開きます。  

2.  DFS 管理コンソール上の DFS 管理を展開します。  

3.  **[レプリケーション]** を右クリックし、**[新しいレプリケーション グループ]** をクリックします。  

4.  新しいレプリケーション グループ ウィザードの **[レプリケーション グループの種類]** ページで、**[新しい汎用レプリケーション グループ]** をクリックします。  

5.  **[次へ]** をクリックします。  

6.  **[名前およびドメイン]** ページに次の情報を入力します。  

    -   **[レプリケーション グループの名前]** ボックスにレプリケーション グループの名前、たとえば、「**MDT 2010 Replication Group**」を入力します。  

    -   **[レプリケーション グループのオプションの説明]** ボックスに、たとえば「**Group for replication of MDT 2010 data**」と入力します。  

    -   **[ドメイン]** ボックスに正しいドメイン名が表示されていることを確認します。  

7.  **[次へ]** をクリックします。  

8.  **[レプリケーション グループのメンバー]** ページで次の手順を実行します。  

    1.  **[追加]** をクリックします。  

    2.  このレプリケーション グループのメンバーになるすべてのサーバー、たとえば、すべての子展開サーバーとマスター展開サーバーの名前を入力します。  

    3.  **[OK]** をクリックします。  

9. **[次へ]** をクリックします。  

10. **[トポロジの選択]** ページで、**[ハブおよびスポーク]** をクリックし、**[次へ]** をクリックします。  

11. **[ハブ メンバー]** ページでマスター展開サーバーをクリックし、**[追加]** をクリックします。  

12. **[次へ]** をクリックします。  

13. **[ハブとスポークの接続]** ページで、子展開サーバーそれぞれについて、表示されているマスター展開サーバーが **[ハブ メンバー (必須)]** であることを確認します。  

14. **[次へ]** をクリックします。  

15. **[レプリケーション グループのスケジュールおよび帯域幅]** ページにサーバー間でコンテンツをレプリケートするためのスケジュールを指定します。  

16. **[次へ]** をクリックします。  

17. **[プライマリ メンバー]** ページの **[プライマリ メンバー]** ボックスで、マスター展開サーバーをクリックします。  

18. **[次へ]** をクリックします。  

19. **[レプリケートするフォルダー]** ページで **[追加]** をクリックし、次の手順を実行します。  

    1.  **[レプリケートするフォルダーのローカル パス]** ボックスの **[参照]** をクリックし、*X:\\* 展開フォルダーに移動します (*X* は、展開サーバー上のドライブ文字)。  

    2.  **[パスに応じた名前を使用]** をクリックします。  

    3.  **[OK]** をクリックします。  

    4.  **[追加]** をクリックします。  

    5.  **[レプリケートするフォルダーの追加]** ダイアログ ボックスの **[参照]** をクリックし、*X:* \RemoteInstall\Boot フォルダーに移動します。  

    6.  **[パスに応じた名前を使用]** をクリックします。  

20. **[次へ]** をクリックします。  

21. **[Local Path of Distribution on Other Members]** \(他のメンバーにおける配布のローカル パス\) ページで、次の手順を実行します。  

    1.  配布グループ内のすべてのメンバーを選択し、**[編集]** をクリックします。  

    2.  **[ローカル パスの編集]** ダイアログ ボックスの **[有効]** をクリックします。  

    3.  子展開サーバーで展開共有フォルダーを格納するパスを、たとえば、「***X:\Deployment***」と入力します (*X* は展開サーバー上のドライブ文字)。  

    4.  **[OK]** をクリックします。  

22. **[次へ]** をクリックします。  

23. **[Local Path of Boot on Other Members]** \(他のメンバーにおける起動のローカル パス\) ページで、次の手順を実行します。  

    1.  配布グループ内のすべてのメンバーを選択し、**[編集]** をクリックします。  

    2.  **[ローカル パスの編集]** ダイアログ ボックスの **[有効]** をクリックします。  

    3.  子展開サーバー上に展開共有フォルダーを格納するパスを、たとえば「***X:\RemoteInstall\Boot***」と入力します (*X* は展開サーバー上のドライブ文字)。  

    4.  **[OK]** をクリックします。  

24. **[次へ]** をクリックします。  

25. **[Remote Settings and Create Replication Group]** \(リモート設定およびレプリケーション グループの作成\) ページで **[作成]** をクリックし、新しいレプリケーション グループの作成ウィザードを完了します。  

26. **[確認]** ページの **[閉じる]** をクリックしてウィザードを終了します。  

> [!NOTE]
>  新しいレプリケーション グループがレプリケーション ノードの下に現在表示されていることを確認します。  

###  <a name="PrepareSQLReplication"></a> SQL Server レプリケーションのための準備  
 SQL Server レプリケーションを構成する前に、いくつかの事前構成手順を実行して、展開サーバーが正しく構成されていることを確認します。  

 **マスター展開サーバー上の SQL Server レプリケーション用に準備するには**  

1.  データベース スナップショットを格納するフォルダーを作成し、そのフォルダーを共有として構成します。  

    > [!NOTE]
    >  スナップショット フォルダーのセキュリティ保護に関する詳細については、「[スナップショット フォルダーのセキュリティ保護](http://msdn2.microsoft.com/library/ms151151.aspx)」を参照してください。  

2.  SQL Server Browser サービスが有効になっていて、[自動] に設定されていることを確認します。  

3.  **[SQL Server Surface Area Configuration]** ボックスの **[ローカル接続およびリモート接続]** をクリックします。  

 **子展開サーバー上の SQL Server レプリケーション用に準備するには**  

1.  **[SQL Server Surface Area Configuration]** ボックスの **[ローカル接続およびリモート接続]** をクリックします。  

2.  必要に応じて、レプリケートされた MDT DB をホストする空のデータベースを作成します。  

> [!NOTE]
>  このデータベースは、マスター展開サーバー上の MDT DB と同じ名前にする必要があります。 たとえば、マスター展開サーバー上の MDT DB が *MDTDB* という名前の場合は、子展開サーバー上に *MDTDB* という名前の空のデータベースを作成します。  

###  <a name="ConfigureSQLReplication"></a> SQL Server レプリケーションの構成  
 展開インフラストラクチャを構築するために必要なファイルとフォルダーのレプリケーションを構成した後は、MDT DB をレプリケートする SQL Server を構成します。  

> [!NOTE]
>  中央に 1 つの MDT DB のみを管理することも可能ですが、MDT DB のレプリケートされたバージョンを維持すると、ワイド エリア ネットワーク (WAN) 全体のデータ転送をより細かく制御できます。  

 SQL Server 2005 では、雑誌配布モデルに似たレプリケーション モデルが採用されています。  

1.  *雑誌*が*発行元*から入手可能になります (発売されます)。  

2.  *ディストリビューター*を使用してパブリケーションが配布されます。  

3.  *リーダー*がパブリケーションにサブスクライブすることで、定期的にそのパブリケーションがサブスクライバーに配布されます (*プッシュ サブスクリプション*)。  

 ここに示した用語が、SQL Server レプリケーションのセットアップと構成ウィザードの全体で使用されます。  

#### <a name="configure-a-sql-server-publisher"></a>SQL Server パブリッシャーの構成  
 マスター展開サーバーを SQL Server パブリッシャーとして構成するには、次の手順を実行します。  

1.  SQL Server Management Studio を開きます。  

2.  **[レプリケーション]** ノードを右クリックし、**[ディストリビューションの構成]** をクリックします。  

3.  ディストリビューションの構成ウィザードで、**[次へ]** をクリックします。  

4.  **[ディストリビューター]** ページで、**['ServerName' を独自のディストリビューターとする (SQL Server はディストリビューション データベースとログを作成します)]** をクリックし、**[次へ]** をクリックします。  

5.  **[スナップショット フォルダー]** ページの **[Preparing for SQL Server Replication]** \(SQL Server レプリケーション用の準備\) セクションで、作成したスナップショット フォルダーへの UNC パスを入力します。  

6.  **[ディストリビューション データベース]** ページで、**[次へ]** をクリックします。  

7.  **[パブリッシャー]** ページで、マスター展開サーバーをクリックすることでディストリビューターとして設定し、**[次へ]** をクリックします。  

8.  **[ウィザードのアクション]** ページで、**[ディストリビューションを構成する]** をクリックし、**[次へ]** をクリックします。  

9. **[完了]** をクリックし、ウィザードが完了したら、**[閉じる]** をクリックします。  

#### <a name="enable-the-mdt-db-for-replication"></a>MDT DB のレプリケーションの有効化  
 マスター展開サーバー上の MDT DB をレプリケーション対象として有効にするには、次の手順を実行します。  

1.  SQL Server Management Studio で、**[レプリケーション]** ノードを右クリックし、**[パブリッシャーのプロパティ]** をクリックします。  

2.  **[パブリッシャーのプロパティ]** ページで、次の手順を実行します。  

    1.  **[パブリッシャー データベース]** をクリックします。  

    2.  MDT DB をクリックし、**[トランザクション]** をクリックします。  

    3.  **[OK]** をクリックします。  

 これで MDT DB がトランザクションとスナップショット レプリケーション用に構成されました。  

#### <a name="create-a-publication-of-the-mdt-db"></a>MDT DB のパブリケーションの作成  
 子展開サーバーがサブスクライブできる MDT DB のパブリケーションを作成するには、次の手順を実行します。  

1.  SQL Server Management Studio で レプリケーション] を展開し、**[ローカル パブリケーション]** を右クリックして **[新しいパブリケーション]** をクリックします。  

2.  パブリケーションの新規作成ウィザードで、**[次へ]** をクリックします。  

3.  **[パブリケーション データベース]** ページで、MDT DB をクリックし、**[次へ]** をクリックします。  

4.  **[パブリケーションの種類]** ページで、**[スナップショット パブリケーション]** をクリックし、**[次へ]** をクリックします。  

5.  **[アーティクル]** ページで、すべての**テーブル、ストアド プロシージャ**、および**ビュー**を選択し、**[次へ]** をクリックします。  

6.  **[アーティクルの問題点]** ページで、**[次へ]** をクリックします。  

7.  **[テーブル行のフィルター選択]** ページで、**[次へ]** をクリックします。  

8.  **[スナップショット エージェント]** ページで、次の手順を実行します。  

    1.  **[スナップショットをすぐに作成し、サブスクリプションを初期化できるようにそのスナップショットを保持する]** を選択します。  

    2.  **[以下のスケジュールでスナップショット エージェントを実行する]** をクリックします。  

    3.  **[変更]** をクリックします。  

    > [!NOTE]
    >  データベースのレプリケートの 1 時間前に実行されるスケジュールを指定します。  

9. **[次へ]** をクリックします。  

10. **[エージェント セキュリティ]** ページで、スナップショット エージェントが実行されるアカウントをクリックし、**[次へ]** をクリックします。  

11. **[ウィザードのアクション]** ページで、**[パブリケーションを作成する]** をクリックし、**[次へ]** をクリックします。  

12. **[ウィザードの完了]** ページの **[パブリケーション名]** ボックスに、わかりやすいパブリケーション名を入力します。  

13. **[完了]** をクリックしてウィザードを完了し、ウィザードによるパブリケーションの作成が終了したら、**[閉じる]** をクリックします。  

    > [!NOTE]
    >  パブリケーションはすぐに SQL Server Management Studio の [ローカル パブリケーション] ノードの下に表示されます。  

#### <a name="subscribe-child-deployment-servers-to-the-published-mdt-db"></a>展開済み MDT DB への子展開サーバーのサブスクライブ  
 MDT DB がパブリッシュされたので、子展開サーバーをサブスクライバーとしてこのパブリケーションに追加できます。パブリケーションに追加した子展開サーバーは一定のスケジュールに従ってデータベースのコピーを受け取り、展開時にクライアント コンピューターから、WAN を経由せずネットワークのローカル データベースにクエリを実行できるようになります。  

 **展開済み MDT DB パブリケーションに子展開サーバーをサブスクライブするには**  

1.  SQL Server Management Studio で、[レプリケーション] の [ローカル パブリケーション] に移動します。  

2.  前のセクションで作成したパブリケーションを右クリックし、**[新しいサブスクリプション]** をクリックします。  

3.  サブスクリプションの新規作成ウィザードで、**[次へ]** をクリックします。  

4.  **[パブリケーション]** ページで、前のセクションで作成したパブリケーションをクリックします。  

5.  **[ディストリビューション エージェントの場所]** ページで、**[ディストリビューター SERVERNAME ですべてのエージェントを実行する (プッシュ サブスクリプション)]** をクリックし、**[次へ]** をクリックします。  

6.  **[サブスクライバー]** ページで、次の手順を実行して個々の子展開サーバーを追加します。  

    1.  **[サブスクライバーの追加]** をクリックし、次に **[SQL Server サブスクライバーの追加]** をクリックします。  

    2.  個々の子展開サーバーを追加します。  

    3.  子展開サーバーを追加するたびに、**[サブスクリプション データベース]** ボックスで、その子展開サーバー上の空の MDT DB をクリックします。  

    > [!NOTE]
    >  空の MDT DB がまだ作成されていない場合は、**[サブスクリプション データベース]** ボックスで、新しいデータベースを作成するオプションを選択します。  

    > [!NOTE]
    >  このデータベースは、マスター展開サーバー上の MDT DB と同じ名前にする必要があります。 たとえば、マスター展開サーバー上の MDT DB が *MDTDB* という名前の場合は、子展開サーバー上に *MDTDB* という名前の空のデータベースを作成します。  

7.  **[次へ]** をクリックします。  

8.  **[ディストリビューション エージェントのセキュリティ]** ページで、**[…]** をクリックして、 **[ディストリビューション エージェントのセキュリティ]** ダイアログ ボックスを開きます。  

9. ディストリビューション エージェントに使用するアカウントの詳細情報を入力し、**[次へ]** をクリックします。  

10. **[同期スケジュール]** ページで、次の手順を実行します。  

    1.  **[エージェント スケジュール]** ボックスで、[**<スケジュールの定義\>**] をクリックします。  

    2.  マスター展開サーバーと子展開サーバー間でデータベースをレプリケートするために使用するスケジュールを指定し、**[次へ]** をクリックします。  

11. **[サブスクリプションの初期化]** ページで **[次へ]** をクリックします。  

12. **[ウィザードのアクション]** ページで、**[サブスクリプションを作成する]** をクリックし、**[次へ]** をクリックします。  

13. **[完了]** をクリックし、ウィザードの処理が正常に完了したら、**[閉じる]** をクリックします。  

 以上で SQL Server のレプリケーションの構成が完了しました。マスター展開サーバーから、そのマスターにサブスクライブしているすべての子展開サーバーに、MDT DB が定期的にレプリケートされます。  

#### <a name="configure-customsettingsini"></a>CustomSettings.ini の構成  
 LTI 展開インフラストラクチャが正常に作成されました。各場所に、LTI 展開サーバーと、次の項目のレプリケートされたコピーが格納されます。  

-   展開共有  

-   MDT DB  

-   Windows 展開サービスに追加した LiteTouchPE_x86 Windows PE 環境  

 次に、展開共有でローカル展開サーバーの展開コンテンツ (展開共有とデータベース) を使用できるように CustomSettings.ini ファイルを構成します。そのサーバーから Windows 展開サービスによって LiteTouchPE_x86.wim 環境が配布されます。  

 LiteTouchPE_x86.wim ファイルが Windows 展開サービスから配布されると、使用する Windows 展開サービス サーバーの名前が付いたレジストリ キーが構成されます。 このサーバー名は、MDT によって変数 (%WDSServer%) にキャプチャされます。その変数を使用して CustomSettings.ini を構成できます。  

 **常にローカルの LTI 展開サーバーを使用するには**  

> [!NOTE]
>  次の手順は、展開共有が作成され、Deployment$ 共有として設定されていることを前提とします。  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share* に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[プロパティ]** をクリックします。  

4.  **[Rules]** \(規則\) タブをクリックし、CustomSettings.ini ファイルを変更して次のプロパティを構成します。  

    -   追加する各 SQL Server セクションに、サーバー名 **%WDSServer%** を使用するように **SQLServer** を構成します (例: **SQLServer=%WDSServer%**)。  

    -   **DeployRoot** を構成する場合は、**DeployRoot** を、**%WDSServer%** 変数を使用するように構成します (例: **DeployRoot=\\\\%WDSServer%\Deployment$**)。  

5.  **[Edit Bootstrap.ini]** \(Bootstrap.ini の編集\) をクリックします。  

6.  **%WDSServer%** プロパティを使用するように BootStrap.ini を構成します。そのためには、**DeployRoot** 値を **DeployRoot=\\\\%WDSServer%\Deployment$** に追加するか、値を変更します。  

7.  **[ファイル]** をクリックし、次に **[保存]** をクリックして BootStrap.ini ファイルに変更を保存します。  

8.  **[OK]** をクリックします。  

     展開共有と LiteTouchPE_x86.wim Windows PE 環境を更新する必要があります。  

9. 操作ウィンドウで **[Update Deployment Share]** \(展開共有の更新\) をクリックします。  

     展開共有の更新ウィザードが開始されます。  

10. **[Options]** \(オプション\) ページで、展開共有を更新する目的のオプションを選択し、**[Next]** \(次へ\) をクリックします。  

11. **[Summary]** \(概要\) ページで詳細情報が正しいことを確認し、**[Next]** \(次へ\) をクリックします。  

12. **[Confirmation]** \(確認\) ページで **[Finish]** \(完了\) をクリックします。  

 次の例は、このセクションで説明する手順を実行後の CustomSettings.ini を示しています。  

 **スケーラブルな LTI 展開インフラストラクチャ用に構成したサンプルの CustomSettings.ini**  

```  
[Settings]  
Priority=CSettings,CPackages, CApps, CAdmins, CRoles, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac  

[CSettings]  
SQLServer=%WDSServer%  
Instance=  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerSettings  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CPackages]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerPackages  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CApps]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerApplications  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CAdmins]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerAdministrators  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CRoles]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerRoles  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
```  

## <a name="selecting-a-local-mdt-server-when-multiple-servers-exist"></a>複数のサーバーが存在する場合のローカル MDT サーバーの選択  
 このシナリオでは、複数の MDT サーバーを使用して、複数のサイトへの大量の同時展開をサポートします。 LTI 展開が初期化された時点の既定の動作では、MDT サーバーへのパスを要求して接続し、展開プロセスを開始するために必要なファイルにアクセスします。  

 Windows Deployment Wizard では、LocalServer.xml ファイルを使用して、場所ごとに既知の展開サーバーの選択肢を提示できます。  

 LocationServer.xml ファイルの使用方法は次のとおりです。  

-   LocationServer.xml の目的と用途を理解します。「[LocationServer.xml について](#UnderstandingLocationServer)」を参照してください。  

-   LocationServer.xml ファイルを作成します。「[LocationServer.xml ファイルの作成](#CreateLocationServer)」を参照してください。  

-   Extra Files ディレクトリに LocationServer.xml ファイルを追加します。「Extra Files ディレクトリへの LocationServer.xml ファイルの追加」を参照してください。  

-   BootStrap.ini ファイルを更新します。「[BootStrap.ini ファイルの更新](#UpdateBootstrap)」を参照してください。  

-   展開共有を更新します。「[展開共有の更新](#UpdateDeploymentShare)」を参照してください。  

 このシナリオは、MDT が展開サーバー上に構成されていることを前提としています。  

###  <a name="UnderstandingLocationServer"></a> LocationServer.xml について  
 最初に、LocationServer.xml が MDT でどのように使用されるかを理解する必要があります。 LTI の実行時、MDT スクリプトによって BootStrap.ini ファイルが読み取られて処理され、展開に関する初期情報が収集されます。 その後、展開サーバーへの接続が確立されます。 したがって、通常は **DeployRoot** プロパティを使用して、接続する必要がある接続先サーバーを BootStrap.ini ファイル内に指定します。  

 BootStrap.ini ファイル内に **DeployRoot** プロパティが含まれていない場合は、MDT スクリプトによって、展開サーバーへのパスをユーザーに確認するウィザード ページが読み込まれます。 **HTML Application (HTA)** ウィザード ページの初期化中、MDT スクリプトによって、LocationServer.xml ファイルの有無が確認されます。このファイルが存在する場合は、利用可能な展開サーバーが LocationServer.xml を使って表示されます。  

#### <a name="understand-when-to-use-locationserverxml"></a>どのような場合に LocationServer.xml を使用するかについての理解  
 MDT には、LTI 展開時に接続先サーバーを決定する複数の方法が用意されています。 さまざまなシナリオに応じて、それぞれに適した展開サーバー検索方法が存在します。そのため、LocationServer.xml はどのような場合に適しているかを理解することが重要です。  

 MDT には、最も適切な展開サーバーを自動的に検出して使用する複数の方法があります。 それらの方法を次の表に示します。

 |**方法** |**詳細** |  
 |-|-|  
 |**%WDSServer%** |この方法は、MDT サーバーが Windows 展開サービス サーバーと同じサーバーでホストされているときに使用します。<br /><br /> LTI 展開を Windows 展開サービスから開始すると、環境変数 %WDSServer% が作成され、Windows 展開サービス サーバーの名前が事前設定されます。<br /><br /> **DeployRoot** 変数でこの変数を使用して、Windows 展開サービス サーバー上の展開共有に自動的に接続できます。次に例を示します。<br /><br /> **DeployRoot=\\\\%WDSServer%\Deployment$** |  
 |**場所ベースの自動化** |MDT では、BootStrap.ini ファイル内で場所ベースの自動化のしくみを使用して、展開先となるサーバーを決定できます。<br /><br /> **Default Gateway** プロパティを使用してさまざまな場所を区別します。各 **Default Gateway** に異なる MDT サーバーを指定します。<br /><br /> 場所ベースの自動化の詳細については、「Selecting the Methods for Applying Configuration Settings」 (構成設定を適用する方法の選択) を参照してください。|  

 上記の表に示したそれぞれの方法は、特定のシナリオ向けに指定の場所にある展開サーバーの選択を自動化する 1 つの方法を提供します。 これらの方法は、特定のシナリオを対象にしています。たとえば、MDT サーバーが Windows 展開サービスと同じホストに共存している場合などです。  

 これらの方法が適さない他のシナリオもあります。たとえば、特定の場所に複数の展開サーバーがある場合や、自動化のロジックが使用できない場合です (たとえば、ネットワークが十分にセグメント化されていないため場所を特定できない、MDT サーバーが Windows 展開サービスから切り離されているなど)。  

 このようなシナリオにおいて、展開時にこの情報を提供する柔軟な方法が LocationServer.xml ファイルであり、サーバー名や展開共有名に関する情報を必要としません。  

###  <a name="CreateLocationServer"></a> LocationServer.xml ファイルの作成  
 LTI 展開時に利用可能な展開サーバーの一覧を表示するには、各サーバーに関する詳細情報を含む LocationServer.xml ファイルを作成します。 MDT に既定の LocationServer.xml ファイルはありません。次のガイダンスに従って作成してください。  

#### <a name="create-a-locationserverxml-file-to-support-multiple-locations"></a>複数の場所をサポートする LocationServer.xml ファイルの作成  
 LocationServer.xml を作成して使用する最も簡単な方法として、LocationServer.xml ファイルを作成したら、展開に含まれる各展開サーバー (同じ場所にある、または異なる複数の場所にある) のエントリを追加します。  

 サーバーごとに新しいセクションを作成して LocationServer.xml ファイルを作り、次の情報を追加します。  

-   一意識別子  

-   場所の名前 (その場所のわかりやすい名前を表すために使用します)  

-   その場所の、MDT サーバーへの UNC パス  

 複数の場所用に構成されたサンプルの LocationServer.xml ファイルを使用し、これらの各プロパティを指定して LocationServer.xml ファイルを作成する方法を以下に示します。  

 **複数の場所をサポートするサンプルの LocationServer.xml ファイル**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 この形式を使用して、場所ごとに異なるサーバー エントリを指定するか、1 つの場所に複数のサーバーが存在する場合は、その場所にあるサーバーごとに異なるサーバー エントリを指定します。次の例を参照してください。   

 **複数の場所にある複数のサーバーをサポートするサンプルの LocationServer.xml ファイル**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ DS1, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso HQ DS2, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS02\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

#### <a name="create-a-locationserverxml-file-to-load-balance-multiple-servers-at-different-locations"></a>異なる場所にある複数のサーバーの負荷を分散する LocationServer.xml ファイルの作成  
 LocationServer.xml を使用して場所エントリごとに複数のサーバーを指定し、基本的な負荷分散を実行することで、1 つの場所が選択されたとき、MDT によって、利用可能なサーバーの一覧から展開サーバーが自動的に選択されます。 この機能を提供するために、LocationServer.xml ファイルでは重み付けメトリックの指定がサポートされています。  

 次の例は、異なる場所にある複数のサーバー用に構成されたサンプルの LocationServer.xml ファイルを示しています。  

 **異なる複数の場所向けのサンプルの LocationServer.xml ファイル**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <Server1>\\STLDS01\Deployment$</Server1>  
        <Server2>\\STLDS02\Deployment$</Server2>  
        <Server3>\\STLDS03\Deployment$</Server3>  
        <Server weight=”1”>\\STLDS01\Deployment$</Server>  
        <Server weight=”2”>\\STLDS02\Deployment$</Server>  
        <Server weight=”4”>\\STLDS03\Deployment$</Server>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 重み付けメトリックを指定するには、<server weight\> タグを使用します。このタグが MDT によるサーバーの選択プロセスで使用されます。 サーバーが選択される確率は、次のように計算されます。  

 **すべてのサーバーの重みの合計に対する、そのサーバーの重みの割合**  

 前の例では、Contoso 本社にある 3 台のサーバーは、重みが 1、2、4 と表示されています。 重み 2 のサーバーが選択される確率は、7 分の 2 になります。 そのため、重み付けシステムを使用するには、各場所で使用できるサーバーの容量を決定し、各サーバーを他の各サーバーに対して相対的なサーバー容量によって重み付けします。  

### <a name="adding-the-locationserverxml-file-to-the-extra-files-directory"></a>Extra Files ディレクトリへの LocationServer.xml ファイルの追加  
 LocationServer.xml ファイルを作成した後、***X:\\Deploy\Control フォルダー***の LiteTouch_x86 および LiteTouch_x64 Windows PE ブート イメージに追加します。 Deployment Workbench を使用して他のファイルやフォルダーをこれらの Windows PE イメージに追加します。そのために、展開共有プロパティに追加のディレクトリを指定します。  

 **LocationServer.xml を展開共有に追加するには**  

1.  ルート展開共有フォルダー内に *Extra Files* というフォルダーを作成します (例: D:\Production Deployment Share\Extra Files)。  

2.  追加ファイルが存在する Windows PE の場所を反映したフォルダー構造を Extra Files フォルダー内に作成します。  

     たとえば、LocationServer.xml ファイルは Windows PE の \Deploy\Control フォルダーに存在している必要があります。そのため、同じフォルダー構造を Extra Files の下に作成します (例: D:\Production Deployment Share\Extra Files\Deploy\Control)。  

3.  LocationServer.xml を *deployment_share*\Extra Files\Deploy\Control フォルダーにコピーします (*deployment_share* は、展開共有のルート フォルダーへの完全修飾パス)。  

4.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

5.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share* に移動します (*deployment_share* は、構成する展開共有の名前)。  

6.  操作ウィンドウで **[プロパティ]** をクリックします。  

7.  [***deployment_shareProperties***]\(deployment_share のプロパティ\) ダイアログ ボックス (deployment_share は展開共有の名前) で、次の手順を実行します。  

    1.  **[Windows PE platform Settings]** \(Windows PE platform の設定\) タブをクリックします (*platform* は、構成する Windows PE イメージのアーキテクチャ)。  

    2.  **[Windows PE Customizations]** \(Windows PE のカスタマイズ\) セクションの **[Extra directory to add]** \(追加するディレクトリ\) ボックスに「***path***」 (*path* は、Extra Files フォルダーへの完全修飾パス。例: D:\Production Deployment Share\Extra Files) を入力し、**[OK]** をクリックします。  

###  <a name="UpdateBootstrap"></a> BootStrap.ini ファイルの更新  
 Deployment Workbench を使用して展開共有を作成すると、**DeployRoot** プロパティが自動的に作成され、BootStrap.ini ファイル内に事前設定されます。 **DeployRoot** プロパティの事前設定には LocationServer.xml ファイルを使用するため、BootStrap.ini ファイルからはこの値を削除する必要があります。  

 **BootStrap.ini から DeployRoot プロパティを削除するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share* に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[プロパティ]** をクリックします。  

4.  ***[deployment_shareProperties]*** \(deployment_share のプロパティ\) ダイアログ ボックス (*deployment_share* は展開共有の名前) で、**[Rules]** \(規則\) タブをクリックし、次に **[Edit BootStrap.ini]** \(BootStrap.ini の編集\) をクリックします。  

5.  **DeployRoot** の値 (例: **DeployRoot=\\\Server\Deployment$**) を削除します。  

6.  **[ファイル]** をクリックし、次に **[保存]** をクリックして BootStrap.ini ファイルに変更を保存します。  

7.  **[OK]** をクリックして変更を送信します。  

###  <a name="UpdateDeploymentShare"></a> 展開共有の更新  
 次に、LocationServer.xml ファイルと更新された BootStrap.ini ファイルを含む新しい LiteTouch_x86 および LiteTouch_x64 ブート環境を生成するように展開共有を更新する必要があります。  

 **展開共有を更新するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share* に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[Update Deployment Share]** \(展開共有の更新\) をクリックします。  

     展開共有の更新ウィザードが開始されます。  

4.  **[Options]** \(オプション\) ページで、展開共有を更新する目的のオプションを選択し、**[Next]** \(次へ\) をクリックします。  

5.  **[Summary]** \(概要\) ページで詳細情報が正しいことを確認し、**[Next]** \(次へ\) をクリックします。  

6.  **[Confirmation]** \(確認\) ページで **[Finish]** \(完了\) をクリックします。  

> [!NOTE]
>  更新プロセスが完了したら、新しい LiteTouch_x86 および LiteTouch_x64 Windows PE 環境を Windows 展開サービスに再度追加するか、展開時に使用するブート メディアに書き込みます。  

## <a name="replacing-an-existing-computer-with-a-new-computer-using-lite-touch-installation"></a>ライト タッチ インストールを使用した、新しいコンピューターと既存のコンピューターの置き換え  
 MDT を使用して、エンタープライズ アーキテクチャ内の既存コンピューターを置き換える新しいコンピューターにイメージを展開できます。 このような状況が発生する例として、あるオペレーティング システムから別のオペレーティング システムにアップグレードする場合や (新しいオペレーティング システムには新しいハードウェアが必要な場合もあります)、組織が既存のアプリケーション用に、より新しく高速なコンピューターの使用を望んでいる場合があります。  

 既存のコンピューターを新しいコンピューターで置き換える場合は、ユーザー アカウントやユーザー状態データなど、1 つのコンピューターから別のコンピューターに移行されるすべての設定を考慮に入れることをお勧めします。 さらに、移行が失敗した場合に備えて回復策を作成することが重要です。  

 このサンプルの展開では、CORP ドメイン内の既存コンピューター WDG-EXIST-01 を新しいコンピューター (WDG-NEW-02) で置き換えます。そのために WDG-EXIST-01 からユーザー状態データをキャプチャし、ネットワーク共有に保存します。 WDG-NEW-02 に既存のイメージを展開し、最終的に、キャプチャしたユーザー状態データを WDG-NEW-02 に復元します。 展開は、展開サーバー (WDG-MDT-01) から実行されます。  

 MDT で Standard Client Replace タスク シーケンス テンプレートを使用して、必要なすべての展開タスクを実行するタスク シーケンスを作成します。  

 このデモの前提事項は次のとおりです。  

-   展開サーバー (WDG MDT 01) 上に MDT がインストールされている  

-   展開共有が既に作成され、事前設定されている (オペレーティング システム イメージ、アプリケーション、デバイス ドライバーを格納済み)  

-   参照コンピューターのイメージが既にキャプチャされ、新しいコンピューター (WDG NEW 02) に展開される  

-   展開サーバー (WDG MDT 01) 上にネットワーク共有フォルダー (UserStateCapture$) を作成し、適切な共有アクセス許可を指定して共有済み  

 このサンプルを開始する前に、展開共有が存在している必要があります。 展開共有の作成の詳細については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Managing Deployment Shares in the Deployment Workbench」 (Deployment Workbench での展開共有の管理) を参照してください。  

### <a name="step-1-create-a-task-sequence-to-capture-the-user-state"></a>手順 1: ユーザー状態をキャプチャするタスク シーケンスの作成  
 Deployment Workbench で New Task Sequence Wizard を使用して [Task Sequences]\(タスク シーケンス\) ノード上に MDT タスク シーケンスを作成します。 コンピューター置換の展開シナリオの最初の部分 (既存コンピューター上でのユーザー状態のキャプチャ) を実行するには、New Task Sequence Wizard で Standard Client Replace タスク シーケンス テンプレートを選択します。  

 **コンピューター置換の展開シナリオでユーザー状態をキャプチャするタスク シーケンスを作成するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Task Sequences に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[New Task Sequence]** \(新しいタスク シーケンス\) をクリックします。  

     New Task Sequence Wizard が開始されます。  

4.  次の情報を使用して New Task Sequence Wizard の設定を完了します。 特に明記しない限り、既定値を使用します。  

    |**ウィザードのページ** |**操作** |  
    |-|-|  
    |**General Settings** (全般設定) |1.**[Task sequence ID]** \(タスク シーケンス ID\) に「**VISTA_EXIST**」と入力します。<br />2.**[Task sequence name]** \(タスク シーケンス名\) に「**Perform Replace Computer Scenario on Existing Computer**」と入力します。<br />3.**[次へ]** をクリックします。|  
    |**Select Template** (テンプレートの選択) |**The following task sequence templates are available**. **[Select the one you would like to use as a starting point]** \(以下のタスク シーケンス テンプレートが利用可能です。土台として使用するテンプレートを選択してください\) で、**[Standard Client Replace Task Sequence]** \(標準クライアント置換タスク シーケンス\) を選択し、**[Next]** \(次へ\) をクリックします。|  
    |**概要** |構成の詳細が正しいことを確認し、**[Next]** \(次へ\) をクリックします。|  
    |**Confirmation** (確認) |**[完了]** をクリックします。|  

 New Task Sequence Wizard が完了し、**VISTA_EXIST** タスク シーケンスがタスク シーケンスの一覧に追加されます。  

### <a name="step-2-create-a-task-sequence-to-deploy-operating-system-and-restore-the-user-state"></a>手順 2: オペレーティング システムを展開してユーザー状態を復元するタスク シーケンスの作成  
 Deployment Workbench で New Task Sequence Wizard を使用して [Task Sequences]\(タスク シーケンス\) ノード上に MDT タスク シーケンスを作成します。 コンピューター置換の展開シナリオの 2 番目の部分 (既存コンピューターでのオペレーティング システムの展開とユーザー状態の復元) を実行するには、New Task Sequence Wizard で Standard Client Replace タスク シーケンス テンプレートを選択します。  

 **コンピューター置換の展開シナリオでユーザー状態を展開するタスク シーケンスを作成するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Task Sequences に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[New Task Sequence]** \(新しいタスク シーケンス\) をクリックします。  

     New Task Sequence Wizard が開始されます。  

4.  次の情報を使用して New Task Sequence Wizard の設定を完了します。 特に明記しない限り、既定値を使用します。  

    |**ウィザードのページ**|**操作**|  
    |-|-|  
    |**General Settings** (全般設定)|1.**[Task sequence ID]** \(タスク シーケンス ID\) に「**VISTA_NEW**」と入力します。<br />2.**[Task sequence name]** \(タスク シーケンス名\) に「**Perform Replace Computer Scenario on New Computer**」と入力します。<br />3.**[次へ]** をクリックします。|  
    |**Select Template** (テンプレートの選択)|**The following task sequence templates are available**. **Select the one you would like to use as a starting point**\(以下のタスク シーケンス テンプレートが利用可能です。土台として使用するテンプレートを選択してください\) で、**Standard Client Task Sequence**\(標準クライアント タスク シーケンス\) を選択し、**Next**\(次へ\) をクリックします。|  
    |**Select OS** (OS の選択)|**The following operating system images are available to be deployed with this task sequence**. Select one to use\(このタスク シーケンスでは以下のオペレーティング システム イメージを展開できます。使用するイメージを選択してください\) で、***captured_vista_image*** (*captured_vista_image* は、参照コンピューターから Deployment Workbench の Operating Systems\(オペレーティング システム\) ノードに追加された、キャプチャされたイメージ) を選択し、*Next*\(次へ\) をクリックします。|  
    |**Specify Product Key** (プロダクト キーの指定)|**[Do not specify a product key at this time]** \(今回はプロダクト キーを指定しない\) を選択し、**[Next]** \(次へ\) をクリックします。|  
    |OS Settings (OS 設定)|1.**[Full Name]** \(フル ネーム\) に「**Woodgrove Employee**」と入力します。<br />2.**[Organization]** \(組織\) に「**Woodgrove Bank**」と入力します。<br />3.**[Internet Explorer Home Page]** \(Internet Explorer ホーム ページ\) に「**http://www.woodgrovebank.com**」と入力します。<br />4.**[次へ]** をクリックします。|  
    |**Admin Password** (管理者パスワード)|**[Administrator Password]** \(管理者パスワード\) と **[Please confirm Administrator Password]** \(管理者パスワードの確認\) に「**P@ssw0rd**」と入力し、**[Finish]** \(完了\) をクリックします。|  
    |**Confirmation** (確認)|**[完了]** をクリックします。|  

 New Task Sequence Wizard が完了し、**VISTA_NEW** タスク シーケンスがタスク シーケンスの一覧に追加されます。  

### <a name="step-3-customize-the-mdt-configuration-files"></a>手順 3: MDT 構成ファイルのカスタマイズ  
 MDT のタスク シーケンスが作成されたら、ユーザー状態情報をキャプチャするための構成設定を指定する MDT 構成ファイルをカスタマイズします。 具体的には、展開プロセスの最初の方で作成した展開共有のプロパティでファイルを変更して CustomSettings.ini ファイルをカスタマイズします。 展開共有内の構成ファイルを確実に更新するために、後の手順で展開共有を更新します。  

 **ユーザー状態情報をキャプチャするための MDT 構成ファイルをカスタマイズするには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share* に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[プロパティ]** をクリックします。  

     **プロパティ**のダイアログ ボックスが表示されます。  

4.  **プロパティ**のダイアログ ボックスで、**[Rules]** \(規則\) タブをクリックします。  

5.  **[Rules]** \(規則\) タブで、次の例に示すように、必要な変更を反映するように CustomSettings.ini ファイルを編集します。 環境に必要な追加の変更があれば行います。  

     **カスタマイズした CustomSettings.ini ファイル**  

    ```  
    [Settings]  
    Priority=Default  
    Properties=MyCustomProperty  

    [Default]  
    OSInstall=Y  

    UDShare=\\WDG-MDT-01\UserStateCapture$  
    UDDir=%OSDCOMPUTERNAME%  
    UserDataLocation=NETWORK  
    SkipCapture=NO  
    SkipAdminPassword=YES  
    SkipProductKey=YES  

    ```  

6.  **プロパティ**のダイアログ ボックスで **[OK]** をクリックします。  

7.  開いているすべてのウィンドウとダイアログ ボックスを閉じます。  

### <a name="step-4-configure-the-windows-pe-options-for-the-deployment-share"></a>手順 4: 展開共有の Windows PE オプションの構成  
 Deployment Workbench の [Deployment Shares]\(展開共有\) ノード上に展開共有の Windows PE オプションを構成します。  

> [!NOTE]
>  既存のコンピューター (WDG-EXIST-01) と新しいコンピューター (WDG-NEW-01) のデバイス ドライバーが Windows Vista に含まれている場合は、この手順をスキップし、次の手順に進みます。  

 **展開共有の Windows PE オプションを構成するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share* に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[プロパティ]** をクリックします。  

     **プロパティ**のダイアログ ボックスが表示されます。  

4.  **プロパティ**のダイアログ ボックスの [**Windows PE *platform* Components**]\(Windows PE platform のコンポーネント\) タブ (*platform* は、構成する Windows PE イメージのアーキテクチャ) で、**[Selection profile]** \(選択プロファイル\) の ***device_drivers*** (*device_drivers* は、デバイス ドライバー選択プロファイルの名前) を選択し、**[OK]** をクリックします。  

### <a name="step-5-update-the-deployment-share"></a>手順 5: 展開共有の更新  
 展開共有の Windows PE オプションを構成した後、展開共有を更新します。 展開共有を更新すると、すべての MDT 構成ファイルが更新され、カスタマイズしたバージョンの Windows PE が生成されます。 カスタマイズしたバージョンの Windows PE を使用して参照コンピューターを起動し、LTI 展開プロセスを開始します。  

 **Deployment Workbench で展開共有を更新するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share* に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作] ウィンドウで **[Update Deployment Share]** \(展開共有の更新\) をクリックします。  

     展開共有の更新ウィザードが開始されます。  

4.  **[Options]** \(オプション\) ページで、展開共有を更新する目的のオプションを選択し、**[Next]** \(次へ\) をクリックします。  

5.  **[Summary]** \(概要\) ページで詳細情報が正しいことを確認し、**[Next]** \(次へ\) をクリックします。  

6.  **[Confirmation]** \(確認\) ページで **[Finish]** \(完了\) をクリックします。  

 Deployment Workbench による展開共有の更新が開始されます。 Deployment Workbench により、LiteTouchPE_x86.iso と LiteTouchPE_x86.wim ファイル (32 ビットの対象のコンピューター用) または LiteTouchPE_x64.iso と LiteTouchPE_x64.wim ファイル (64 ビットの対象のコンピューター用) が *deployment_share*\Boot フォルダーに作成されます (*deployment_share* は、展開共有として使用される共有フォルダー)。  

### <a name="step-6-create-the-lti-bootable-media"></a>手順 6: LTI の起動可能なメディアの作成  
 展開共有を更新したときに作成された、カスタマイズしたバージョンの Windows PE を使用してコンピューターを起動するための方法です。 Deployment Workbench により、LiteTouchPE_x86.iso と LiteTouchPE_x86.wim ファイル (32 ビットの対象のコンピューター用) または LiteTouchPE_x64.iso と LiteTouchPE_x64.wim ファイル (64 ビットの対象のコンピューター用) が *deployment_share*\Boot フォルダーに作成されます (*deployment_share* は、展開共有として使用される共有フォルダー)。 これらのいずれかのイメージから、適切な LTI の起動可能なメディアを作成します。  

 **LTI の起動可能なメディアを作成するには**  

1.  エクスプローラーで *deployment_share*\Boot フォルダーに移動します (*deployment_share* は、展開共有として使用される共有フォルダー)。  

2.  既存のコンピューター (WDG-EXIST-01) および新しいコンピューター (WDG-NEW-02) として使用するコンピューターの種類に基づいて、次のタスクのいずれかを実行します。  

    -   参照コンピューターが物理コンピューターの場合は、ISO ファイルの CD または DVD を作成します。  

    -   参照コンピューターが VM の場合は、ISO ファイルから直接 VM を起動するか、ISO ファイルの CD または DVD から VM を起動します。  

### <a name="step-7-start-the-existing-computer-with-the-lti-bootable-media"></a>手順 7: LTI の起動可能なメディアを使用した既存コンピューターの起動  
 プロセスの最初の方で作成した LTI の起動可能なメディアを使用して既存のコンピューター (WDG-EXIST-01) を起動します。 この CD では、既存のコンピューター上に Windows PE を起動し、MDT 展開プロセスを開始します。 MDT の展開プロセスの終わりに、ユーザー状態移行情報が、UserStateCapture$ 共有フォルダーに格納されます。  

> [!NOTE]
>  Windows 展開サービスからターゲット コンピューターを起動して、MDT プロセスを開始することもできます。 詳細については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Preparing Windows Deployment Services」 (Windows 展開サービスの準備) を参照してください。  

 **LTI の起動可能なメディアを使用して既存のコンピューターを起動するには**  

1.  プロセスの最初の方で作成した LTI の起動可能なメディアを使用して WDG-EXIST-01 を起動します。  

     Windows PE が起動し、Windows Deployment Wizard が開始されます。  

2.  次の情報を使用して、Windows Deployment Wizard の設定を完了します。 特に明記しない限り、既定値を使用します。  

    |**ウィザードのページ**|**操作**|  
    |-|-|  
    |**Welcome to Deployment** (ようこそ)|**[Run the Deployment Wizard]** \(展開ウィザードの実行\) をクリックして新しいオペレーティング システムをインストールし、**[Next]** \(次へ\) をクリックします。|  
    |**Specify Credentials for connecting to network shares.** (ネットワーク共有パスへの接続に必要な資格情報を指定します。)|1.**[User Name]** \(ユーザー名\) に「**Administrator**」と入力します。<br />2.**[Password]** \(パスワード\) に「**P@ssw0rd**」と入力します。<br />3.**[Domain]** \(ドメイン\) に「**CORP**」と入力します。<br />4.**[OK]** をクリックします。|  
    |**Select a task sequence to execute on this computer.** (このコンピューター上で実行するタスク シーケンスを選択します。)|[*Perform Replace Computer Scenario on Existing Computer*]\(既存コンピューター上でコンピューター置換シナリオを実行する\) をクリックし、**[Next]** \(次へ\) をクリックします。|  
    |**Specify where to save your data and settings** (データと設定を保存する場所を指定します。)|**[次へ]** をクリックします。|  
    |**Specify where to save a complete computer backup** (コンピューターの完全バックアップを保存する場所を指定します。)|**[Do not back up the existing computer]** \(既存のコンピューターをバックアップしない\) をクリックし、**[Next]** \(次へ\) をクリックします。|  
    |**Ready to begin** (開始する準備ができました)|**[Begin]** \(開始\) をクリックします。|  

     エラーまたは警告が発生した場合は、MDT ドキュメント「*トラブルシューティングのリファレンス*」を参照してください。  

3.  **[Deployment Summary]** \(展開の概要\) ダイアログ ボックスで、**[Details]** \(詳細\) をクリックします。  

     エラーまたは警告が発生した場合は、エラーまたは警告を確認し、診断情報を記録します。  

4.  **[Deployment Summary]** \(展開の概要\) ダイアログ ボックスで、**[Finish]** \(完了\) をクリックします。  

 ユーザー状態移行情報がキャプチャされ、プロセスの最初の方で作成したネットワーク共有フォルダー (UserStateCapture$) に格納されます。  

### <a name="step-8-start-the-new-computer-with-the-lti-bootable-media"></a>手順 8: LTI の起動可能なメディアを使用した新しいコンピューターの起動  
 プロセスの最初の方で作成した LTI の起動可能なメディアを使用して新しいコンピューター (WDG-NEW-02) を起動します。 この CD では、参照コンピューター上に Windows PE を起動し、MDT 展開プロセスを開始します。 MDT の展開プロセスの最後に、Windows Vista が新しいコンピューター上に展開され、キャプチャされたユーザー状態移行情報が新しいコンピューター上に復元されます。  

> [!NOTE]
>  Windows 展開サービスからターゲット コンピューターを起動して、MDT プロセスを開始することもできます。 詳細については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Preparing Windows Deployment Services」 (Windows 展開サービスの準備) を参照してください。  

 **LTI の起動可能なメディアを使用して新しいコンピューターを起動するには**  

1.  プロセスの最初の方で作成した LTI の起動可能なメディアを使用して WDG-NEW-02 を起動します。  

     Windows PE が起動し、Windows Deployment Wizard が開始されます。  

2.  次の情報を使用して、Windows Deployment Wizard の設定を完了します。 特に明記しない限り、既定値を使用します。  

    |**ウィザードのページ**|**操作**|  
    |--|--|
    |**Welcome to Deployment** (ようこそ)|**[Run the Deployment Wizard]** \(展開ウィザードの実行\) をクリックして新しいオペレーティング システムをインストールし、**[Next]** \(次へ\) をクリックします。|  
    |**Specify Credentials for connecting to network shares.** (ネットワーク共有パスへの接続に必要な資格情報を指定します。)|1.**[User Name]** \(ユーザー名\) に「**Administrator**」と入力します。<br />2.**[Password]** \(パスワード\) に「**P@ssw0rd**」と入力します。<br />3.**[Domain]** \(ドメイン\) に「**CORP**」と入力します。<br />4.**[OK]** をクリックします。|  
    |**Select a task sequence to execute on this computer.** (このコンピューター上で実行するタスク シーケンスを選択します。)|**[Perform Replace Computer Scenario on New Computer]** \(新しいコンピューター上でコンピューター置換シナリオを実行する\) をクリックし、**[Next]** \(次へ\) をクリックします。|  
    |**Configure the computer name** (コンピューター名の構成)|**[Computer name]** \(コンピューター名\) に「**WDG-NEW-02**」と入力し、**[Next]** \(次へ\) をクリックします。|  
    |**Join the computer to a domain or workgroup** (コンピューターをドメインまたはワークグループに参加させる)|**[次へ]** をクリックします。|  
    |**Specify whether to restore user data** (ユーザー データを復元するかどうかの指定)|1.**[Specify a location]** \(場所の指定\) をクリックします。<br />2.**[Location]** \(場所\) に「**\\\WDG-MDT-01\UserStateCapture$\WDG-EXIST-01**」と入力します。<br />3.**[次へ]** をクリックします。|  
    |**Locale Selection** (ロケール選択)|**[次へ]** をクリックします。|  
    |**Set the Time Zone** (タイム ゾーンの設定)|**[次へ]** をクリックします。|  
    |**Specify whether to capture an image** (イメージをキャプチャするかどうかの指定)|**[Do not capture an image of this computer]** \(このコンピューターのイメージをキャプチャしない\) をクリックし、**[Next]** \(次へ\) をクリックします。|  
    |**Specify the BitLocker configuration** (BitLocker 構成の指定)|**[Do not enable BitLocker for this computer]** \(このコンピューターの BitLocker を有効にしない\) をクリックし、**[Next]** \(次へ\) をクリックします。|  
    |**Ready to begin** (開始する準備ができました)|**[Begin]** \(開始\) をクリックします。|  

     エラーまたは警告が発生した場合は、MDT ドキュメント「*トラブルシューティングのリファレンス*」を参照してください。  

3.  **[Deployment Summary]** \(展開の概要\) ダイアログ ボックスで、**[Details]** \(詳細\) をクリックします。  

     エラーまたは警告が発生した場合は、エラーまたは警告を確認し、診断情報を記録します。  

4.  **[Deployment Summary]** \(展開の概要\) ダイアログ ボックスで、**[Finish]** \(完了\) をクリックします。  

 これで Windows Vista が新しいコンピューターにインストールされ、キャプチャされたユーザー状態移行情報も復元されます。  

## <a name="integrating-custom-deployment-code-into-mdt"></a>MDT へのカスタム展開コードの統合  
 展開チームにとって、Deployment Workbench 上の定義済みタスク シーケンス操作や既定の MDT 構成ファイルでは満たすことができない、固有の複雑な要件がターゲット環境に存在することがよくあります。 このような状況では、要件に合わせてカスタム コードを実装します。  

 MDT にカスタム展開コードを統合する方法は次のとおりです。  

-   「[適切なスクリプト言語の選択](#ChooseAppropLanguage)」の説明に従って、スクリプト言語を選択します。  

-   「[ZTIUtility の活用方法の理解](#UnderstandLeverageZTI)」の説明に従って、ZTIUtility.vbs を活用します。  

-   「[カスタム展開コードの統合](#IntegrateCustomDeploy)」の説明に従って、カスタム展開コードを統合します。  

 以降のセクションでは、MDT が展開サーバー上に構成されていることを前提としています。  

###  <a name="ChooseAppropLanguage"></a> 適切なスクリプト言語の選択  
 アプリケーションのインストールまたは MDT タスク シーケンス ステップでは、Windows または Windows PE で実行できるすべてのコードを呼び出すことができますが、.vbs または .wsf ファイル形式のスクリプトの使用をお勧めします。  

 .wsf ファイルを使用する利点として、組み込みのログ機能や、ZTI および LTI プロセスで既に使用されている事前定義されたその他の関数があります。 それらの関数は、MDT に付属している ZTIUtility スクリプトで使用できます。  

 カスタム スクリプトから参照された場合、ZTIUtility スクリプトは MDT 環境とセットアップ クラスを初期化します。 次のクラスを使用できます。  

-   **Logging**。 このクラスは、すべての MDT スクリプトで使用するログ機能を提供します。 展開時のスクリプト実行ごとに 1 つのログ ファイルを作成し、すべてのスクリプトの統合されたログ ファイルも作成します。 これらのログ ファイルは、TRACE32 による読み取り用の形式で作成されます。このツールは、[System Center Configuration Manager 2007 Toolkit V2](https://www.microsoft.com/download/en/details.aspx?id=9257) で使用できます。  

-   **Environment**。 このクラスは、WMI および MDT による規則の処理を通して収集される環境変数を構成して、スクリプトから直接参照できるようにします。 これにより、展開プロパティの読み取りが可能になり、ZTI および LTI プロセスによって使用されるすべての構成情報にアクセスできるようになります。  

-   **Utility**。 このクラスは、ZTI および LTI スクリプトで使用される一般的なユーティリティを提供します。 カスタム コードを開発する場合は常に、再利用できるコードがあるかどうかをこのクラスで調べて確認することをお勧めします。 このセクションでは、このクラスが提供する機能の一部に関する追加情報を後で示します。  

-   **Database**。 このクラスは、データベースに接続してデータベースから情報を読み取るなどの機能を実行します。 一般に、データベース クラスに直接アクセスすることはお勧めしません。代わりに、データベース検索を実行する方法として規則の処理を使用してください。  

-   **Strings**。 このクラスは、一般的な文字列処理ルーチンを実行します。たとえば、区切られた項目のリスト、16 進数値の表示、文字列からの空白の除去、文字列の右揃え、文字列の左揃え、値を強制的に文字列形式にする、値を強制的に配列形式にする、ランダムなグローバル一意識別子 (GUID) の生成、Base64 変換などを行います。  

-   **FileHandling**。 このクラスは、パスの正規化、ファイルとフォルダーのコピー、移動、削除などの機能を実行します。  

-   **clsRegEx**。 このクラスは、正規表現の機能を実行します。  

 MDT には、クライアントの Microsoft Visual Basic® Scripting Edition (VBScript) をさらに堅牢で信頼性の高いものにするために、いくつかの変更が実装されています。 次のような変更です。  

-   新しい API やエラー処理を含む ZTIUtility.vbs (メイン スクリプト ライブラリ) への大幅な変更  

-   ZTI_*xxx*.wsf スクリプトの全体的な構造の新しい外観  

 MDT スクリプトの全体的な構造も変更されました。 MDT スクリプトの多くは VBScript **クラス** オブジェクト内にカプセル化されました。 クラスは **RunNewInstance** 関数によって初期化され、呼び出されます。  

> [!NOTE]
>  既存の MDT 2008 Update 1 スクリプトの多くは、ZTIUtility.vbs に大幅な変更を加えていても、そのまま MDT で使用できます (ほとんどの MDT スクリプトに ZTIUtility.vbs が含まれているため)。  

###  <a name="UnderstandLeverageZTI"></a> ZTIUtility の活用方法の理解  
 ZTIUtility.vbs ファイルには、カスタム コードで利用できるオブジェクト クラスが含まれています。 MDT とカスタム コードを統合に使用できる方法は次のとおりです。  

-   ZTIUtility.vbs に定義された Logging クラス (「[ZTIUtility Logging クラスの使用](#UseZTILogging)」を参照)  

-   ZTIUtility.vbs に定義された Environment クラス (「[ZTIUtility Environment クラスの使用](#UseZTIEnvironment)」を参照)  

-   ZTIUtility.vbs に定義された Utility クラス (「[ZTIUtility Utility クラスの使用](#UseZTIUtility)」を参照)  

####  <a name="UseZTILogging"></a> ZTIUtility Logging クラスの使用  
 ZTIUtiliy.vbs の Logging クラスは、ZTI または LTI 展開中に、他のスクリプトと同じ方法でカスタム コードを使用して状態情報、警告、エラーのログを記録する簡単なメカニズムを提供します。 また、この標準化によって、**[LTI Deployment Summary]** \(LTI 展開の概要\) ダイアログ ボックスにカスタム コードの状態が正しく報告されます。  

 次に示すカスタム コード スクリプトの例では、**oLogging.CreateEntry** と **TestAndFail** 関数を使用して、さまざまなスクリプト操作の結果に応じて、さまざまな種類のメッセージのログを記録しています。  

 **ZTIUtility Logging を使用したスクリプトの例: ZTI_Example.wsf**  

```  
<job id="ZTI_Example">  
<script language="VBScript" src="ZTIUtility.vbs"/>  
<script language="VBScript">  

' //*******************************************************  
' //  
' // Copyright (c) Microsoft Corporation.  All rights reserved  
' // Microsoft Deployment Toolkit Solution Accelerator  
' // File: ZTI_Example.wsf  
' //  
' // Purpose: Example of scripting with the  
' //          Microsoft Deployment Toolkit.  
' //  
' // Usage: cscript ZTI_Example.wsf [/debug:true]  
' //  
' //*******************************************************  

Option Explicit  
RunNewInstance  

'//--------------------------------------------------------  
'// Main Class  
'//--------------------------------------------------------  
Class ZTI_Example  

'//--------------------------------------------------------  
'// Main routine  
'//--------------------------------------------------------  

Function Main()  

  Dim iRetVal  
  Dim sScriptPath  

  iRetVal = SUCCESS  

  oLogging.CreateEntry "Begin example script…", _  
    LogTypeInfo  

  ' %ServerA% is a generic variable available within  
  ' every CustomSettings.ini file.  

  sScriptPath = "\\" & oEnvironment.Item("ServerA") & _  
    "\public\products\Applications\User\Technet\USEnglish"  

  ' Validate a connection to server, net connect with  
  ' credentials if necessary.  
  iRetVal = oUtility.ValidateConnection( sScriptPath )  
  TestAndFail iRetVal, 9991, "Validate Connection to [" & _  
    sScriptPath & "]"  

  'Run Setup Program  

  iRetVal = oUtility.RunWithHeartbeat( """" & _  
    sScriptPath & "\setup.exe"" /?" )  
  TestAndFail iRetVal, 9991, "RunWithHeartbeat [" & _  
    sScriptPath & "]"  

  'Perform any cleanup from installation process  

  oShell.RegWrite "HKLM\Software\Microsoft\SomeValue", _  
    "Done with Execution of XXX.", "REG_SZ"  

  Main = iRetVal  

End Function  

End Class  

</script>  
</job>  
```  

> [!NOTE]
>  **ZTIProcess()** を **ProcessResults()** と共に呼び出すスクリプトの継続的な使用を希望する場合は、引き続き使用できます。 ただし、特定の拡張エラー処理機能は有効になりません。  

####  <a name="UseZTIEnvironment"></a> ZTIUtility Environment クラスの使用  
 ZTIUtiliy.vbs の environment クラスでは、MDT プロパティにアクセスし、MDT プロパティを更新できます。 上記の例では、**oEnvironment.Item("Memory")** を使って、使用可能な RAM の量を取得しています。また、MDT ドキュメントの*ツールキットのリファレンス*に関するページで説明されているように、プロパティの値を取得するためにも使用できます。  

####  <a name="UseZTIUtility"></a> ZTIUtility Utility クラスの使用  
 ZTIUtility.vbs スクリプトには、よく使われるさまざまなユーティリティが含まれていて、カスタム展開スクリプトで使用できます。 それらのユーティリティは、**oLogging** および **oEnvironment** クラスを使用するのと同じ方法で使用できます。  

次の表では、使用可能ないくつかの便利な関数とその出力について説明します。 使用可能なすべての関数の一覧については、ZTIUtility.vbs ファイルを参照してください。  

|**関数**|**出力**|  
|-|-|
|**oUtility.LocalRootPath**|ターゲット コンピューター上の展開プロセスによって使用されるルート フォルダーのパスを返します。例: C:\MININT|  
|**oUtility.BootDevice**|システムのブート デバイスを返します。例: MULTI(0)DISK(0)RDISK(0)PARTITION(1)|  
|**oUtility.LogPath**|展開時に使用されるログ フォルダーのパスを返します。例: C:\MININT\SMSOSD\OSDLOGS|  
|**oUtility.StatePath**|現在構成されている状態ストアのパスを返します。例: C:\MININT\StateStore|  
|**oUtility.ScriptName**|関数を呼び出すスクリプトの名前を返します。例: Z-RAMTest|  
|**oUtility.ScriptDir**|関数を呼び出すスクリプトのパスを返します。例: \\\server_name\Deployment$\Scripts|  
|**oUtility.ComputerName**|ビルド プロセス中に使用されるコンピューター名を決定します。例: computer_name|  
|**oUtility.ReadIni(file, section, item)**|指定した項目を .ini ファイルから読み取ることができるようにします。|  
|**oUtility.WriteIni(file, section, item, value)**|指定した項目を .ini ファイルに書き込むことができるようにします。|  
|**oUtility.Sections(file)**|.ini ファイルのセクションを読み取り、参照用のオブジェクトに格納します。|  
|**oUtility.SectionContents(file, section)**|指定した .ini ファイルの内容を読み取り、オブジェクトに格納します。|  
|**oUtility.RunWithHeartbeat(sCmd)**|コマンドの実行時にハートビート情報を 0.5 秒おきにログに書き込みます。|  
|**oUtility.FindFile**<br /><br /> **(sFilename,sFoundPath)**|DeployRoot フォルダーと標準のサブフォルダー内で指定されたファイルを検索します (サービス、ツール、USMT、テンプレート、スクリプト、コントロールなど)。|  
|**oUtility.findMappedDrive(sServerUNC)**|ドライブが指定した UNC パスにマップされているかどうかを確認し、ドライブ文字を返します。|  
|**oUtility.ValidateConnection(sServerUNC)**|指定されたサーバーに既存の接続があるかどうかを確認し、ない場合は作成を試みます。|  
|**MapNetworkDrive**<br /><br /> **(sShare, SDomID, sDomPwd)**|共有として指定された UNC パスにドライブ文字をマップし、使用されているドライブ文字を返します。失敗した場合はエラーを返します。|  
|**VerifyPathExists(strPath)**|指定されたパスが存在することを確認します。|  
|**oEnvironment.Substitute(sVal)**|文字列が指定された場合、その文字列内の変数または関数を展開します。|  
|**oEnvironment.Item**<br /><br /> **(sName)**|永続的なストアに対して変数の読み取りまたは書き込みを行います。|  
|**oEnvironment.Exists**<br /><br /> **(sName)**|変数が存在するかどうかを確認するためのテストを実行します。|  
|**oEnvironment.ListItem**<br /><br /> **(sName)**|永続的なストアに対して、**array** 型の変数の読み取りまたは書き込みを行います。|  
|**oLogging.ReportFailure**<br /><br /> **(sMessage, iError)**|回復不能なエラーが検出された場合に構造化された終了を実行するために使用します。|  
|**oLogging.CreateEvent**<br /><br /> **(iEventID, iType, sMessage, arrParms)**|ログ ファイルにメッセージを書き込み、定義されているサーバーにイベントを送信します。|  
|**oLogging.CreateEntry**<br /><br /> **(sLogMsg, iType)**|ログ ファイルにメッセージを書き込みます。|  
|**TestAndFail(iRc, iError, sMessage)**|**iRc** が false の場合または失敗した場合に、**iError** を使用してスクリプトを終了します。|  
|**TestAndLog(iRc , sMessage)**|**iRc** が false の場合または失敗した場合にのみ、警告をログに書き込みます。|  

###  <a name="IntegrateCustomDeploy"></a> カスタム展開コードの統合  
 カスタム展開コードは複数の方法で MDT プロセスに統合することができますが、使用する方法に関係なく、次の 2 つの規則に従う必要があります。  

-   カスタム展開コードのスクリプト名は、必ず文字 Z で始まる必要があります。  

-   カスタム展開コードは、展開共有の Scripts フォルダーに配置する必要があります。例: D:\Production Deployment Share\Scripts  

 カスタム コードを統合するためによく使われる方法は次のとおりです。これらの方法を使用すると一貫したログ記録を取得することもできます。  

-   コードを MDT アプリケーションとして展開する  

-   コードを MDT タスク シーケンス コマンドとして起動する  

-   コードをユーザー出口スクリプトとして起動する  

#### <a name="deploy-custom-code-as-an-mdt-application"></a>カスタム コードを MDT アプリケーションとして展開  
 カスタム展開コードを Deployment Workbench にインポートし、他のアプリケーションと同じ方法で管理できます。  

 **カスタム展開コードを実行する新しいアプリケーションを作成するには**  

1.  カスタム展開コードを *deployment_share*\Scripts フォルダー (*deployment_share* は、展開共有への完全修飾パス) にコピーします。  

2.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

3.  Deployment Workbench コンソール ツリー上の Deployment Shares/*deployment_share*/Applications に移動します (*deployment_share* は、構成する展開共有の名前)。  

4.  操作] ウィンドウで **[New Application]** \(新しいアプリケーション\) をクリックします。  

     New Application Wizard が開始されます。  

5.  次の情報を使用して、New Application Wizard の設定を完了します。 特に明記しない限り、既定値を使用します。  

    |**ウィザードのページ**|**操作**|  
    |-|-|  
    |**Application Type** (アプリケーションの種類)|**[Application without source files or elsewhere on the network]** \(ソース ファイルがないかネットワークの別の場所にあるアプリケーション\) をクリックし、**[Next]** \(次へ\) をクリックします。|  
    |**詳細**|アプリケーションの情報に基づいてこのページの設定を完了し、**[Next]** \(次へ\) をクリックします。|  
    |**Command Details** (コマンドの詳細)|1.**[Command line]** \(コマンド ライン\) ボックスに「**cscript.exe %SCRIPTROOT%\custom_code**」と入力します (*custom_code* は、開発したカスタム コードの名前)。<br />2.**[Working directory]** \(作業ディレクトリ\) ボックスに「***working_directory***」と入力します (working_directory は、カスタム コードの作業ディレクトリの名前。通常は、**[Command line]** \(コマンド ライン\) ボックスに指定したのと同じフォルダー)。<br />3.**[次へ]** をクリックします。|  
    |**概要**|構成設定が正しいことを確認し、**[Next]** \(次へ\) をクリックします。|  
    |**Confirmation** (確認)|**[完了]** をクリックします。|  

 Deployment Workbench の [Applications]\(アプリケーション\) ノードにアプリケーションが表示されます。  

#### <a name="add-the-custom-code-as-a-task-sequence-step"></a>タスク シーケンスのステップとしてカスタム コードを追加  
 カスタム展開コードは、タスク シーケンス内の任意のポイントから直接呼び出すことができます。これにより、標準のタスク シーケンスの規則とオプションにアクセスできます。  

 **既存のタスク シーケンスにカスタム展開コードを追加するには**  

1.  カスタム展開コードを *deployment_share*\Scripts フォルダー (*deployment_share* は、展開共有への完全修飾パス) にコピーします。  

2.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

3.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share/Task Sequences* に移動します (*deployment_share* は、構成する展開共有の名前)。  

4.  詳細ウィンドウ上の ***task_sequence*** をクリックします (*task_sequence* は、カスタム コードを実行するタスク シーケンスの名前)。  

5.  操作ウィンドウで **[プロパティ]** をクリックします。  

6.  ***[task_sequenceProperties]*** \(task_sequence のプロパティ\) ダイアログ ボックスで、**[Task Sequence]** \(タスク シーケンス\) タブをクリックします。  

7.  コンソール ツリー上の *group* に移動します (*group* は、タスク スケジュール ステップを追加するグループ)。  

8.  **[Add]** \(追加\) をクリックし、**[General]** \(全般\)、**[Run Command Line]** \(コマンド ラインの実行\) をクリックします。  

9. コンソール ツリー上で **[Run Command Line]** \(コマンド ラインの実行\) をクリックし、**[Properties]** \(プロパティ\) タブをクリックします。  

10. **[Name]** \(名前\) ボックスに「***name***」を入力します (*name* は、カスタム コードのわかりやすい名前)。  

11. **[Properties]** \(プロパティ\) タブの **[Command line]** \(コマンド ライン\) ボックスに「***command_line***」と入力します (*command_line* は、カスタム コードを実行するコマンド。例:**cscript.exe %SCRIPTROOT%\CustomCode.vbs**)。  

12. **[Start in]** \(開始する場所\) ボックスに「***path***」を入力します (*path* は、カスタム コードの作業フォルダーへの完全修飾パス。通常は、**[Command line]** \(コマンド ライン\) に指定したのと同じパス)。次に、**[OK]** をクリックします。  

 新しく作成したタスク シーケンス ステップが、タスク シーケンス ステップの一覧に表示されます。  

#### <a name="run-custom-code-as-a-user-exit-script"></a>カスタム コードをユーザー出口スクリプトとして実行  
 CustomSettings.ini から **UserExit** ディレクティブを使用して、カスタム コードをユーザー出口スクリプトとして実行することもできます。 この方法では、CustomSettings.ini の規則検証プロセスに情報を渡すメカニズムが提供され、MDT のプロパティが動的に更新されます。  

 ユーザー出口スクリプトと **UserExit** ディレクティブの詳細については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「User Exit Scripts in the CustomSettings.ini File」 (CustomSettings.ini ファイル内のユーザー出口スクリプト) のセクションを参照してください。  

## <a name="installing-device-drivers-using-various-installation-methods"></a>さまざまなインストール方法を使用したデバイス ドライバーのインストール  
 このシナリオでは、MDT を使用して、さまざまな種類のハードウェアにオペレーティング システムを展開します。 展開プロセスの一部として、それぞれの種類のハードウェアが正しく動作するように、デバイス ドライバーを識別してインストールします。 主なデバイス ドライバーの種類は 2 種類です。展開プロセスにおいて、それぞれを異なる方法で処理する必要があります。  

-   .inf ファイルを含むデバイス ドライバー (このファイルを使用してデバイス ドライバーを Deployment Workbench にインポートできます)  

-   アプリケーションとしてパッケージ化されたデバイス ドライバー (アプリケーションとしてインストールする必要があります)  

 MDT を使用すると、オペレーティング システム展開の一部として両方の種類のドライバーを処理できます。  

 デバイス ドライバーをインストールするには、次の方法があります。  

-   各デバイス ドライバーのインストール方法を決定します。「[デバイス ドライバーのインストールに使用する方法の決定](#WhichMethodtoInstallDriver)」を参照してください。  

-   既定のドライバーの方法を使用します。「[既定のドライバーの方法を使用したデバイス ドライバーのインストール](#InstallOutofBoxDrivers)」を参照してください。  

-   アプリケーションとしてインストールします。「[アプリケーションとしてのデバイス ドライバーのインストール](#InstallDriversasApplications)」を参照してください。  

 このシナリオは、MDT が展開サーバー上で実行されていることを前提としています。  

###  <a name="WhichMethodtoInstallDriver"></a> デバイス ドライバーのインストールに使用する方法の決定  
 デバイス ドライバーは、ハードウェアの製造元から次の 2 つの形式のいずれかでリリースされます。  

-   パッケージとして。抽出可能であり、ドライバーを Deployment Workbench にインポートするために使用する .inf ファイルが含まれています。  

-   アプリケーションとして。従来のアプリケーション インストール プロセスを使用してインストールする必要があります。  

 抽出して .inf ファイルにアクセスできるデバイス ドライバー パッケージの場合は、最初に Deployment Workbench 上の [Out-of-Box Drivers]\(既定のドライバー\) ノードにドライバーをインポートすることで、MDT のドライバー検出とインストールの自動プロセスを利用できます。  

 抽出して .inf ファイルを分離することができないデバイス ドライバー パッケージ、または MSI や Setup.exe ファイルなどのアプリケーション インストーラーを使用して最初にインストールしないと正しく動作しないデバイス ドライバー パッケージの場合は、MDT Install Application 機能を使用して、展開プロセス中に通常のアプリケーションと同じようにデバイス ドライバーをインストールできます。  

###  <a name="InstallOutofBoxDrivers"></a> 既定のドライバーの方法を使用したデバイス ドライバーのインストール  
 .inf ファイルを含むデバイス ドライバー パッケージを Deployment Workbench にインポートし、展開プロセスの一部として自動的にインストールできます。 この種類のデバイス ドライバー展開を実装するには、最初にデバイス ドライバーを Deployment Workbench に追加します。  

 **デバイス ドライバーを Deployment Workbench に追加するには**  

1.  ハードウェアの種類を展開するために必要なデバイス ドライバーをダウンロードし、一時的な場所にデバイス ドライバー パッケージを抽出します。  

2.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

3.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Out-of-Box Drivers に移動します (*deployment_share* は、構成する展開共有の名前)。  

4.  操作] ウィンドウで、**[Import Drivers]** \(ドライバーのインポート\) をクリックします。  

     Import Device Driver Wizard が開始されます。  

5.  **[Specify Directory]** \(ディレクトリの指定\) ページの **[Driver source directory]** \(ドライブ ソース ディレクトリ\) セクションで **[Browse]** \(参照\) をクリックし、新しいデバイス ドライバーが格納されているフォルダーに移動し、**[Next]** \(次へ\) をクリックします。  

    > [!NOTE]
    >  New Device Driver Wizard により、ドライバー ソース ディレクトリのすべてのサブディレクトリが検索されます。そのため、インストールするドライバーが複数ある場合は、それらのドライバーを同じルート ディレクトリ内の別々のフォルダーに抽出し、ドライバー ソース ディレクトリを、すべてのドライバー ソース フォルダーを含むルート ディレクトリとして設定します。  

6.  **[Summary]** \(概要\) ページで、設定が正しいことを確認します。**[Next]** \(次へ\) をクリックすると、ドライバーが Deployment Workbench にインポートされます。  

7.  **[Confirmation]** \(確認\) ページで **[Finish]** \(完了\) をクリックします。  

 デバイス ドライバーの中に、起動に必要なドライバー (大容量記憶装置ドライバーやネットワーク クラス ドライバーなど) が含まれている場合は、次に展開共有を更新して、新しいドライバーを含む新しい LiteTouch_x86 および LiteTouch_x64 のブート環境を生成する必要があります。  

 **ライト タッチ Windows PE イメージにデバイス ドライバーを追加するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share* に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[Update Deployment Share]** \(展開共有の更新\) をクリックします。  

     展開共有の更新ウィザードが開始されます。  

4.  **[Options]** \(オプション\) ページで、展開共有を更新する目的のオプションを選択し、**[Next]** \(次へ\) をクリックします。  

5.  **[Summary]** \(概要\) ページで詳細情報が正しいこと確認し、**[Next]** \(次へ\) をクリックします。  

6.  **[Confirmation]** \(確認\) ページで **[Finish]** \(完了\) をクリックします。  

###  <a name="InstallDriversasApplications"></a> アプリケーションとしてのデバイス ドライバーのインストール  
 デバイス ドライバーがアプリケーションとしてパッケージ化されていて、.inf ファイルが入っているフォルダーをドライバー ファイルとは別に抽出できない場合は、デバイス ドライバーを Deployment Workbench にアプリケーションとして追加すると、展開プロセス中にインストールされます。  

 アプリケーションはタスク シーケンス ステップとして指定するか、CustomSettings.ini 内に指定できます。ただし、デバイス ドライバー アプリケーションは、デバイスが接続されたコンピューター上でタスク シーケンスが実行される場合にのみ、インストールしてください。 これを確実に行うには、適切なデバイス ドライバー アプリケーションを展開するタスク シーケンス ステップを、条件付きタスク シーケンス ステップとして実行します。 ターゲット コンピューター上のデバイスに関する WMI クエリを使用して、タスク シーケンス ステップを実行するための条件付き基準を指定できます。  

#### <a name="add-the-device-driver-application-to-the-deployment-workbench"></a>デバイス ドライバー アプリケーションを Deployment Workbench に追加  
 各デバイス ドライバー アプリケーションは、最初に Deployment Workbench にインポートする必要があります。  

> [!NOTE]
>  展開時にアプリケーションを表示するかどうかを、アプリケーションの**プロパティ**のダイアログ ボックスで **[Hide this application in the Deployment Wizard]** \(Deployment Wizard にこのアプリケーションを表示しない\) チェック ボックスをオンまたはオフにして構成します。 展開時に使用する各デバイス ドライバー アプリケーションについて、このプロセスを繰り返します。  

 **デバイス ドライバー アプリケーションを Deployment Workbench に追加するには**  

1.  デバイス ドライバー アプリケーションをダウンロードし、一時的な場所に保存します。  

2.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

3.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Applications に移動します (*deployment_share* は、構成する展開共有の名前)。  

4.  操作] ウィンドウで **[New Application]** \(新しいアプリケーション\) をクリックします。  

     New Application Wizard が開始されます。  

5.  **[Application Type]** \(アプリケーションの種類\) ページで、**[Application with source files]** \(ソース ファイルありのアプリケーション\) をクリックし、**[Next]** \(次へ\) をクリックします。  

6.  **[Details]** \(詳細\) ページで、アプリケーションに関する適切な詳細情報を入力し、**[Next]** \(次へ\) をクリックします。  

7.  **[Source]** \(ソース\) ページの **[Source directory]** \(ソース ディレクトリ\) セクションで **[Browse]** \(参照\) をクリックし、デバイス ドライバー アプリケーションのソース ファイルを含むディレクトリに移動し、そのディレクトリをクリックします。 **[OK]** をクリックします。  

8.  **[次へ]** をクリックします。  

9. **[Destination]** \(宛先\) ページで宛先ディレクトリの名前を入力し、**[Next]** \(次へ\) をクリックします。  

10. **[Command Details]** \(コマンドの詳細\) ページの **[Command line]** \(コマンド ライン\) セクションに、デバイス ドライバー アプリケーションのサイレント インストールを実行するためのコマンドを入力します。  

11. **[Summary]** \(概要\) ページで、設定が正しいことを確認します。**[Next]** \(次へ\) をクリックすると、デバイス ドライバー アプリケーションが Deployment Workbench にインポートされます。  

12. **[Confirmation]** \(確認\) ページで **[Finish]** \(完了\) をクリックします。  

 アプリケーションが Deployment Workbench にインポートされたら、正しいハードウェア上で実行される場合に限ってアプリケーションがインストールされるように、適切なロジックを使用してアプリケーションを展開プロセスに追加します。 これを行うには、次のようなさまざまな方法があります。  

-   展開タスク シーケンスの一部としてデバイス ドライバー アプリケーションを指定します。  

-   CustomSettings.ini 内にデバイス ドライバー アプリケーションを指定します。  

-   MDT DB 内にデバイス ドライバー アプリケーションを指定します。  

 それぞれの方法について、以下のセクションで詳しく説明します。  

####  <a name="SpecifyDeviceAppTask"></a> タスク シーケンスの一部としてデバイス ドライバー アプリケーションを指定  
 デバイス ドライバー アプリケーションを展開プロセスに追加する最初の方法は、タスク シーケンスを使用して各デバイス ドライバー アプリケーションのステップを追加する方法です。  

 タスク シーケンス内のデバイス ドライバー アプリケーションを管理するには、2 つの主な方法があります。  

-   ハードウェア モデルごとに新しいタスク シーケンス グループを作成し、コンピューターが特定のハードウェアの種類に一致した場合にそのグループの操作を実行するクエリを追加します。  

-   ハードウェア固有のアプリケーション用のタスク シーケンス グループを作成し、各タスク シーケンス アクションにクエリを追加します。各タスク シーケンス ステップは、ハードウェアの種類と一致するかどうかを評価され、一致が見つかった場合にのみ実行されます。  

 **ハードウェアの種類ごとに新しいタスク シーケンス グループを作成するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Task Sequences に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  詳細ウィンドウで、***task_sequence*** をクリックします (*task_sequence* は、デバイス ドライバー アプリケーションのインストールが必要な展開タスク シーケンス)。  

4.  操作ウィンドウで **[プロパティ]** をクリックします。  

5.  ***[task_sequenceProperties]*** \(task_sequence のプロパティ\) ダイアログ ボックスの **[Task Sequence]** \(タスク シーケンス\) タブで、詳細ウィンドウの State Restore/Windows Update (Pre-Application Installation) に移動します。  

6.  **[Task Sequence]** \(タスク シーケンス\) タブで **[Add]** \(追加\) をクリックし、**[New Group]** \(新しいグループ\) をクリックします。  

     これにより、タスク シーケンス内に新しいタスク シーケンス グループが作成されます。 この新しいタスク シーケンス グループを使用して、ハードウェア固有のデバイス ドライバー アプリケーションをインストールするステップを作成します。  

7.  詳細ウィンドウで、**[New Group]** \(新しいグループ\) をクリックします。  

8.  **[Properties]** \(プロパティ\) タブの **[Name]** \(名前\) ボックスに「***group_name***」と入力します (*group_name* は、グループの名前。例: *Hardware Specific Applications – Dell Computer Corporation*)。  

9. **[Options]** \(オプション\) タブで **[Add]** \(追加\) をクリックし、**[Query WMI]** \(WMI のクエリ\) をクリックします。  

10. **[Task Sequence WMI Condition]** \(タスク シーケンスの WMI 条件\) ダイアログ ボックスに次の詳細情報を入力します。  

    -   **[WMI namespace]** \(WMI 名前空間\) ボックスに「**root\cimv2**」と入力します。  

    -   **[WQL query]** \(WQL クエリ\) ボックスに WMI クエリ言語 (WQL) のクエリを入力します。このクエリでは、**Win32_ComputerSystem** クラスを使用して、アプリケーションが特定のアプリケーションの種類の対象にのみインストールされるようにします。次の例を参照してください。  

         **Select \* FROM Win32_ComputerSystem WHERE Model LIKE *%hardware_model%* AND Manufacturer LIKE *%hardware_manufacturer%***  

         この例で、*hardware_model* はコンピューター モデルの名前 (例: Latitude D620) であり、*hardware_manufacturer* はコンピューター製造元の名前です (例: Dell Corporation)。  

         **%** 記号はワイルドカード文字です。これを名前に含めることで、管理者は、***hardware_model*** または ***hardware_manufacturer***に指定した値を含むコンピューター モデルや製造元を取得できます。  

     WMI および WQL クエリの詳細については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Add WMI Queries to Task Sequence Step Conditions」 (タスク シーケンス ステップの条件への WMI クエリの追加) のセクションを参照してください。また、「[Querying with WQL](http://msdn.microsoft.com/library/aa392902.aspx)」 (WQL を使ったクエリ) もご覧ください。  

11. **[OK]** をクリックしてクエリを送信し、次に **[OK]** をクリックしてタスク シーケンスに対する変更を送信します。  

> [!NOTE]
>  各デバイス ドライバー アプリケーションをインストールする対象となるハードウェアの種類ごとに、このプロセスを繰り返す必要があります。  

 ハードウェア固有のタスク シーケンス グループの作成後、デバイス ドライバー アプリケーションを各グループに追加することができます。  

 **ハードウェア固有のタスク シーケンス グループにデバイス ドライバー アプリケーションを追加するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Task Sequences に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  詳細ウィンドウで、***task_sequence*** をクリックします (*task_sequence* は、デバイス ドライバー アプリケーションのインストールが必要な展開タスク シーケンス)。  

4.  操作ウィンドウで **[プロパティ]** をクリックします。  

5.  ***[task_sequenceProperties]*** \(task_sequence のプロパティ\) ダイアログ ボックスで、**[Task Sequence]** \(タスク シーケンス\) タブをクリックします。  

6.  詳細ウィンドウ上の State Restore/*hardware_specific_group* に移動します (*hardware_specific_group* は、デバイス ドライバー アプリケーションをインストールするタスク シーケンス ステップの追加先となる、ハードウェア固有のグループの名前)。  

7.  **[Task Sequence]** \(タスク シーケンス\) タブで **[Add]** \(追加\) をクリックし、**[General]** \(全般\)、**[Install Application]** \(アプリケーションのインストール\) の順にクリックします。  

     **[Install Application]** \(アプリケーションのインストール\) タスク シーケンス ステップが詳細ウィンドウに表示されます。  

8.  詳細ウィンドウで **[Install Application]** \(アプリケーションのインストール\) をクリックします。  

9. **[Properties]** \(プロパティ\) タブで **[Install a single application]** \(アプリケーションを 1 つだけインストールする\) をクリックし、**[Application to install]** \(インストールするアプリケーション\) の一覧で ***hardware_application*** を選択します (*hardware_application* は、ハードウェア固有のアプリケーションをインストールするためのアプリケーション)。  

> [!NOTE]
>  展開時に使用する必要があるデバイス ドライバー アプリケーションごとに、このプロセスを繰り返す必要があります。  

#### <a name="specify-the-device-driver-application-in-customsettingsini"></a>CustomSettings.ini 内にデバイス ドライバー アプリケーションを指定  
 LTI または ZTI の展開が始まったとき、最初に完了する必要がある操作の 1 つは、BootStrap.ini と CustomSettings.ini コントロール ファイルの処理です。 これらのファイルの両方に、展開を動的にカスタマイズするために使用できる規則が含まれています。  

 MDT での CustomSettings.ini ファイルの処理方法により、このファイルは、特定の条件に基づいてアプリケーションを追加するために使用できます。 このロジックは、特定のハードウェアの種類に基づいて展開時にデバイス ドライバー固有のアプリケーションを追加するときに使用します。 アプリケーションは CustomSettings.ini 内でアプリケーションの GUID によって参照されます。GUID は、展開共有の Applications.xml ファイル内にあります。  

 **インポートしたアプリケーションの GUID を検索するには**  

1.  展開サーバーの展開共有にある Control フォルダーを開きます。例: D:\Production Deployment Share\Control  

2.  Applications.xml ファイルを見つけて開きます。  

3.  必要なアプリケーションを検索します。  

4.  アプリケーションの `<guid>` タグで囲まれた行を探してアプリケーションの GUID を確認します。例: `<application guid={c303fa6e-3a4d-425e-8102-77db9310e4d0}>`  

 初期化プロセスの一部として、LTI と ZTI の両方のプロセスで、プロセスを実行しているコンピューターに関する情報が収集されます。 このプロセスの一部として WMI クエリが実行され、**Win32_ComputerSystem** クラスから取得した製造元と型番を表す値が、変数 **%Make%** と **%Model%** にそれぞれ事前設定されます。  

 CustomSettings.ini ファイルの処理時に、これらの値を使用して、検出された製造元とモデルに応じてファイルのセクションを動的に読み取ることができます。  次に示すサンプルは、CustomSettings.ini ファイルの例です。  

 **ハードウェア固有のアプリケーションのインストール用に構成されたサンプルの CustomSettings.ini**  

```  
[Settings]  
Priority=Make, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  

[Dell Computer Corporation]  
Subsection=Dell-%Model%  

[Dell-Latitude D620]  
MandatoryApplications001={1D7DF331-47B7-472C-87B3-442597EC2F7D}  

[Dell-Latitude D610]  
MandatoryApplications001={c303fa6e-3a4d-425e-8102-77db9310e4d0}  
```  

 次のプロパティを使用して、CustomSettings.ini にアプリケーションを指定します。  

-   **Applications**。 展開管理者が展開プロセスの一部としてアプリケーション ウィザードを表示することを希望しない場合、このプロパティを使用して、CustomSettings.ini に **SkipApplications=YES** と指定できます。  

-   **MandatoryApplications**. このプロパティは、展開管理者が展開時にアプリケーション ウィザードを表示することを希望する場合に使用できます。それにより、インストールする追加のアプリケーションを展開時に展開エンジニアが選択できるようになります。  

     アプリケーション ウィザードを使用し、**MandatoryApplications** プロパティを使用していない場合 (たとえば、**SkipApplications=NO**)、**Applications** プロパティで指定したアプリケーションは上書きされます。  

     前述のサンプルは、**%Make%** および **%Model%** 変数の値を使用して、アプリケーション一覧がどのように作成されるかを動的に操作する方法を示しています。 次のいずれかの方法を使用して、各種類のハードウェアの製造元とモデルを表す値を検索できます。  

-   **システム情報ツール**。 このツールの [システムの概要] ノードを使用して、**システム製造元** (製造元) と**システム モデル** (モデル) を確認します。  

-   **Windows PowerShell**。 **Get-WMIObject –class Win32_ComputerSystem** コマンドレットを使用して、コンピューターの製造元とモデルを確認します。  

-   **Windows Management Instrumentation コマンド ライン**。 **CSProduct Get Name, Vendor** を使用して、コンピューターの名前 (モデル) とベンダー (製造元) を取得します。  

 **ハードウェア固有のロジックを追加するために CustomSettings.ini を変更するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share* に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[プロパティ]** をクリックします。  

4.  **[Rules]** \(規則\) タブをクリックします。  

5.  このタブで入力した情報は、CustomSettings.ini ファイルに格納されます。 CustomSettings.ini ファイルのエントリを変更し、デバイス ドライバー固有のアプリケーションを指定した各ハードウェア モデル用のロジックを追加します。「[タスク シーケンスの一部としてデバイス ドライバー アプリケーションを指定](#SpecifyDeviceAppTask)」を参照してください。  

6.  **[OK]** をクリックして変更を送信します。  

7.  詳細ウィンドウで *deployment_share* をクリックします (*deployment_share* は、構成する展開共有の名前)。  

8.  操作ウィンドウで **[Update Deployment Share]** \(展開共有の更新\) をクリックします。  

     展開共有の更新ウィザードが開始されます。  

9. **[Options]** \(オプション\) ページで、展開共有を更新する目的のオプションを選択し、**[Next]** \(次へ\) をクリックします。  

10. **[Summary]** \(概要\) ページで詳細情報が正しいことを確認し、**[Next]** \(次へ\) をクリックします。  

11. **[Confirmation]** \(確認\) ページで **[Finish]** \(完了\) をクリックします。  

 LTI 展開の既定では、すべての利用可能なアプリケーションが Windows Deployment Wizard に表示されます。 デバイス ドライバー固有のアプリケーションは特定のハードウェアの種類にのみ適用されるため、常に表示することが望ましいとは限りません。 デバイス ドライバー固有のアプリケーション パッケージを CustomSettings.ini 内に指定すると、アプリケーション構成の **[Hide the application in the Deployment Wizard]** \(Deployment Wizard にこのアプリケーションを表示しない\) オプションを使用して、アプリケーションが表示されないようにすることができます。  

 **Deployment Wizard にアプリケーションを表示しないようにするには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Applications に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  詳細ウィンドウで ***device_driver_application*** をクリックします (*device_driver_application* は、Deployment Wizard に表示しないアプリケーション)。  

4.  操作ウィンドウで **[プロパティ]** をクリックします。  

5.  **[General]** \(全般\) タブで、**[Hide the application in the Deployment Wizard]** \(Deployment Wizard にこのアプリケーションを表示しない\) チェック ボックスをオンにします。  

6.  **[Apply]** \(適用\) をクリックし、**プロパティ**のダイアログ ボックスを閉じます。  

#### <a name="specify-the-device-driver-application-in-the-mdt-db"></a>MDT DB 内にデバイス ドライバー アプリケーションを指定  
 MDT DB は、CustomSettings.ini ファイルのデータベース バージョンであり、展開時にクエリを実行して、展開中に使用する情報を取得できます。 MDT DB の使用の詳細については、「Selecting the Methods for Applying Configuration Settings」 (構成設定を適用する方法の選択) を参照してください。  

 展開時に MDT DB へのクエリを実行する場合、ターゲット コンピューターを特定する 3 つの方法があります。  

-   個々のコンピューターを (MAC アドレスや資産タグなどを使用して) 検索します。  

-   コンピューターの場所を (既定のゲートウェイを使用して) 検索します。  

-   コンピューターの製造元とモデルを (WMI の製造元またはモデルのクエリを使用して) を検索します。  

 作成する各データベース エントリについて、展開プロパティ、アプリケーション、Configuration Manager パッケージを使用するかどうか、管理者を指定できます。 製造元とモデルのエントリをデータベース内に作成すると、必要なハードウェア固有のデバイス ドライバー アプリケーションを追加できます。  

 **デバイス ドライバー アプリケーションのインストールを可能にするエントリを MDT DB に作成するには**  

> [!NOTE]
>  デバイス ドライバー アプリケーションを必要とするハードウェアの製造元とモデルごとに、このプロセスを繰り返します。  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/**deployment_share**/Advanced Configuration/Database/Make and Model に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[New]** \(新規\) をクリックします。  

4.  **[プロパティ]** ダイアログ ボックスの **[ID]** タブで、**[製造元]** ボックスに「***make_name***」を入力します (*make_name* は、ターゲット コンピューターの製造元を連想できるわかりやすい名前)。  

5.  **モデル**ボックスに、入力***model_name*** (ここで*model_name*に対象のコンピューターのモデルと関連付けるには簡単に関連したわかりやすい名前)。  

6.  **[Applications]** \(アプリケーション\) タブで、そのモデルのハードウェアに必要な各デバイス ドライバー アプリケーションを追加します。  

## <a name="initiating-mdt-using-windows-deployment-services"></a>Windows 展開サービスを使用した MDT の開始  
 Windows Server 2008 では、更新され、再設計されたバージョンのリモート インストール サービス (Windows Server 2003 SP2 での既定の展開ツール) として Windows 展開サービスを使用します。 Windows 展開サービスを使用して Windows オペレーティング システムを展開することができます。特に、Windows 7、Windows Server 2008 またはそれ以降のオペレーティング システムを、コンピューターの PXE 対応ネットワーク アダプターまたはブート メディアを使用してネットワーク経由で展開できます。  

 Windows 展開サービスを展開する前に、お使いの環境に次のどの統合オプションが最適かを確認してください。  

-   オプション 1. コンピューターを PXE で起動して LTI プロセスを開始します。  

-   オプション 2. Windows 展開サービスのイメージ ストアからオペレーティング システム イメージを展開します。  

-   オプション 3. MDT でのマルチキャストと、Windows Server 2008 の Windows 展開サービス サーバーの役割を使用します。  

### <a name="option-1-boot-computers-in-pxe-to-initiate-the-lti-process"></a>オプション 1: コンピューターを PXE で起動して LTI プロセスを開始する  
 Windows 展開サービスを動的ホスト構成プロトコルと共に使用して MDT の展開プロセスを開始することで、オペレーティング システムの展開を管理するためのコストを最小限に抑えます。 これにより、起動可能なメディアを作成して各ターゲット コンピューターに配布する必要がなくなります。  

#### <a name="create-and-import-the-deployment-workbench-windows-pe-image-into-windows-deployment-services"></a>Deployment Workbench の Windows PE イメージを作成して Windows 展開サービスにインポートする  
 新しい MDT の展開共有を作成する場合、または既存の MDT 展開共有を変更する場合は、カスタマイズした Windows PE ブート イメージを作成できます。 展開共有が更新されると、Windows PE ブート イメージが自動的に生成され、展開共有に関する情報によって更新されます。その後、展開共有の構成時に指定された追加のドライバーまたはコンポーネントがあれば、それらが挿入されます。  

 Windows PE ブート イメージは、CD または DVD に書き込み可能な ISO イメージ ファイルと、起動可能な WIM ファイルの両方として生成されます。 Windows 展開サービスに WIM ファイルをインポートすると、PXE で起動可能なコンピューターに、インストールの初期化に使われる LTI Windows PE ブート イメージをダウンロードしてネットワーク全体で実行できます。  

 **起動可能な Windows PE イメージを Deployment Workbench で作成するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share* に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[プロパティ]** をクリックします。  

     ***[deployment_shareProperties]*** \(deployment_share のプロパティ\) ダイアログ ボックスで [**Windows PE *platform* Settings**]\(Windows PE platform の設定\) タブをクリックします (platform は、構成する Windows PE イメージのアーキテクチャ)。  

4.  **[Lite Touch Boot Image Settings]** \(ライト タッチ ブート イメージの設定\) 領域で、**[Generate a Lite Touch bootable RAM disk ISO image]** \(ライト タッチの起動可能な RAM ディスク ISO イメージを生成する\) チェック ボックスをオンにします。  

5.  [**Windows PE *platform* Components**]\(Windows PE platform のコンポーネント\) タブをクリックします (*platform* は、構成する Windows PE イメージのアーキテクチャ)。  

6.  **[Driver Injection]** \(ドライバー挿入\) セクションで、組み込む適切なドライバーの種類をクリックします。  

    > [!NOTE]
    >  この手順は、Windows PE に必要なデバイス ドライバーが既に含まれている場合は、必要ありません。  

7.  **[Driver Injection]** \(ドライバー挿入\) セクションの **[Selection profile]** \(選択プロファイル\) の一覧で、適切なドライバー選択プロファイルを選びます。  

8.  **プロパティ**のダイアログ ボックスで **[OK]** をクリックします。  

    > [!NOTE]
    >  この手順は、Windows PE に必要なデバイス ドライバーが既に含まれている場合は、必要ありません。  

9. 詳細ウィンドウで ***deployment_share*** をクリックします (*deployment_share* は、構成する展開共有の名前)。  

10. 操作ウィンドウで **[Update Deployment Share]** \(展開共有の更新\) をクリックします。  

     展開共有の更新ウィザードが開始されます。  

11. **[Options]** \(オプション\) ページで、展開共有を更新する目的のオプションを選択し、**[Next]** \(次へ\) をクリックします。  

12. **[Summary]** \(概要\) ページで詳細情報が正しいことを確認し、**[Next]** \(次へ\) をクリックします。  

13. **[Confirmation]** \(確認\) ページで **[Finish]** \(完了\) をクリックします。  

     このプロセスが完了すると、展開共有の Boot フォルダーに複数のブート イメージが含まれています。たとえば次のようになります。  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.wim  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim  

 CD または DVD に直接書き込まれた ISO ファイルを作成できます。または、新しいハードウェア上で LTI プロセスを初期化するために ISO ファイルを使用できます。 同様に、ブート WIM ファイルを Windows 展開サービスにインポートし、物理的なメディアを必要とせずに、新しいコンピューター上の LTI 展開プロセスを初期化できるようにすることができます。  

 **Windows 展開サービスに Windows PE イメージをインポートするには**  

1.  Windows 展開サービス コンソールを起動し、Windows 展開サービスに接続します。  

2.  コンソール ツリー上の **[Boot Images]** \(ブート イメージ\) を右クリックし、**[Add Boot Image]** \(ブート イメージの追加\) をクリックします。  

3.  インポートする WIM イメージを参照して選択します。例: D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim  

4.  インポート プロセスによってブート イメージからメタデータが自動的に読み取られますが、**[Image Name]** \(イメージ名\) と **[Image Description]** \(イメージの説明\) の値は編集できます。**[Image Name]** \(イメージ名\) は、クライアントが PXE で起動するときに Windows ブート マネージャーによって表示されるブート オプション情報に反映されます。  

5.  ブート イメージがインポートされると、PXE で起動して Windows 展開サービスから応答を受信したすべてのコンピューターに、LTI ブート イメージをダウンロードし、LTI インストールを開始できます。  

 Windows 展開サービスのインストールと構成については、このガイドでは説明しません。 Windows 展開サービスの詳細については、[Windows 展開サービスのガイド](http://technet.microsoft.com/library/cc265612.aspx)に関するページをご覧ください。  

#### <a name="use-windows-deployment-services-to-automatically-detect-the-deployment-server"></a>Windows 展開サービスを使用した展開サーバーの自動検出  
 Windows 展開サービスを使用して MDT ブート イメージをホストする場合、MDT 展開共有が Windows 展開サービスと同じサーバー上でホストされていれば、追加のオプションを使用できます。  

 PXE クライアントに MDT ブート イメージが読み込まれると、ブート イメージをホストしている Windows 展開サービス サーバーの名前がキャプチャされ、MDTProperty **WDSServer** に格納されます。 以降は、ブート イメージの BootStrap.ini ファイル内および展開共有の CustomSettings.ini ファイル内の **DeployRoot** プロパティで、このプロパティを参照できます。 それにより、Windows 展開サービスから起動するクライアントは自動的に、Windows 展開サービス サーバー上でホストされている展開共有を使用して起動します。 そのため、構成ファイル内にサーバー名を指定する必要がなくなります。  

 **ローカルの Windows 展開サービス サーバーを展開サーバーとして設定するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Advanced Configuration/Database に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[プロパティ]** をクリックします。  

4.  **[Rules]** \(規則\) タブをクリックします。  

     このタブで入力した情報は、CustomSettings.ini ファイルに格納されます。  

5.  **DeployRoot** プロパティを、**%WDSServer%** 変数を使用するように構成します。例: **DeployRoot=\\\\%WDSServer%\Deployment$**  

6.  **[Edit Bootstrap.ini]** \(Bootstrap.ini の編集\) をクリックします。  

7.  **%WDSServer%** プロパティを使用するように BootStrap.ini を構成します。そのためには、**DeployRoot** 値を **DeployRoot=\\\\%WDSServer%\Deployment$** に追加するか、値を変更します。  

8.  **[ファイル]** メニューの **[保存]** をクリックして BootStrap.ini ファイルに変更を保存します。  

9. **[OK]** をクリックします。  

     展開共有を更新する必要があります。  

10. 詳細ウィンドウで **deployment_share** をクリックします (*deployment_share* は、構成する展開共有の名前)。  

11. 操作ウィンドウで **[Update Deployment Share]** \(展開共有の更新\) をクリックします。  

     展開共有の更新ウィザードが開始されます。  

12. **[Options]** \(オプション\) ページで、展開共有を更新する目的のオプションを選択し、**[Next]** \(次へ\) をクリックします。  

13. **[Summary]** \(概要\) ページで詳細情報が正しいことを確認し、**[Next]** \(次へ\) をクリックします。  

14. **[Confirmation]** \(確認\) ページで **[Finish]** \(完了\) をクリックします。  

15. 更新されたブート WIM を Windows 展開サービスにインポートします。  

### <a name="option-2-deploy-an-operating-system-image-from-the-windows-deployment-services-store"></a>オプション 2: Windows 展開サービスのストアからオペレーティング システム イメージを展開する  
 オペレーティング システムの展開用に Windows 展開サービスを既に使用している場合は、MDT の機能を拡張するために、MDT を次のように構成します。まず、MDT のストアを使用するのではなく、既に使用されている Windows 展開サービスのオペレーティング システム イメージを参照するようにします。また、Windows 展開サービスによる展開を、ドライバー管理、アプリケーション展開、更新プログラムのインストール、規則の処理、およびその他の MDT 機能によって補完するようにします。 MDT が Windows 展開サービスのオペレーティング システム イメージを参照するようになった後は、そのイメージを MDT の展開共有にステージングされたオペレーティング システムと同様に扱うことができます。  

 **Windows 展開サービスのオペレーティング システム イメージを参照するには**  

> [!NOTE]
>  次の手順では、少なくとも 1 つのオペレーティング システム イメージをあらかじめ Windows 展開サービス サーバーにインポートしておく必要があります。  

1.  Windows 展開サービスのイメージにアクセスできるように MDT を更新します。そのためには、Windows メディアの Sources フォルダーから Windows 展開サービス サーバー上の C:\Program Files\Microsoft Deployment Toolkit\bin フォルダーに、次のファイルをコピーします。  

    -   Wdsclientapi.dll  

    -   Wdscsl.dll  

    -   Wdsimage.dll  

    -   Wdstptc.dll (Windows Server 2008 のソース ディレクトリからコピーする場合のみ)  

    > [!NOTE]
    >  使用されている Windows ソース ディレクトリは、MDT がインストールされているコンピューター上で実行されているオペレーティング システムのプラットフォームと一致する必要があります。  

2.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

3.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Operating Systems に移動します (*deployment_share* は、構成する展開共有の名前)。  

4.  操作ウィンドウで **[Import Operating System]** \(オペレーティング システムのインポート\) をクリックします。  

     New OS Wizard が開始されます。  

5.  **[OS Type]** \(OS の種類\) ページで **[Windows Deployment Services images]** \(Windows 展開サービスのイメージ\) をクリックし、**[Next]** \(次へ\) をクリックします。  

6.  **[WDS Server]** \(WDS サーバー\) ページで、参照される Windows 展開サービス サーバーの名前 (例: **WDSSvr001**) を入力し、**[Next]** \(次へ\) をクリックします。  

7.  **[Summary]** \(概要\) ページで設定が正しいことを確認し、**[Next]** \(次へ\) をクリックします。  

8.  **[Confirmation]** \(確認\) ページで **[Finish]** \(完了\) をクリックします。  

     これで、Windows 展開サービス サーバー上の利用可能なイメージすべてを MDT タスク シーケンスで使用できるようになります。  

> [!NOTE]
>  Windows 展開サービスからイメージをインポートしても、Windows 展開サービス サーバーから展開共有にソース ファイルはコピーされません。 MDT は、元の場所にあるソース ファイルを引き続き使用します。  

### <a name="option-3-use-multicasting-with-mdt-and-the-windows-server-2008-windows-deployment-services-role"></a>オプション 3: MDT でのマルチキャストと Windows Server 2008 の Windows 展開サービス サーバーの役割を使用する  
 Windows 展開サービスは Windows Server 2008 のリリースに伴って拡張され、マルチキャスト転送を使用したイメージの展開をサポートしています。 MDT には、MDT と Windows 展開サービスのマルチキャストを統合する更新も含まれています。  

 さらに、更新された Windows 自動インストール キット (Windows AIK) バージョン 1.1 には、Wdsmcast.exe が含まれています。 これにより、マルチキャスト セッションを手動で参加させることができます。また、アクティブなマルチキャスト セッションから、Wdsmcast.exe を起動するクライアントにファイルをコピーできます。  

 LTIApply.wsf スクリプトから展開共有のオペレーティング システム ソース ファイルにアクセスするときは、Wdsmcast.exe が使用されます。 LTIApply.wsf は、実行している Windows PE のバージョンに応じて、展開共有の *deployment_share*\Tools\x86 または *deployment_share*\Tools\x64 フォルダー内で Wdsmcast.exe を検索します (*deployment_share* は、展開共有を含むファイル システム フォルダーの名前)。  

 LTIApply.wsf を実行すると常に、既存のマルチキャスト ストリームから WIM イメージへのアクセスと WIM イメージのダウンロードが試みられます。ただし、マルチキャスト ストリームが存在しない場合は、標準ファイル コピーが使用されます。  

> [!NOTE]
>  このプロセスは、WIM イメージ ファイルのみに適用されます。  

 MDT マルチキャスト用に準備する場合の展開サーバーの前提条件は次のとおりです。  

-   展開サーバーでは、Windows Server 2008 以降が実行されている必要があります。  

-   サーバーの管理コンソールから Windows 展開サービスの役割がインストールされている必要があります。  

-   Windows Server 2008 用 Windows AIK 1.1 がインストールされている必要があります。  

-   MDT がインストールされている必要があります。  

-   MDT を使用したあらゆる展開と同様に、少なくとも 1 つのオペレーティング システム WIM イメージが、ソース ファイルのフルセットとして、またはカスタム イメージとセットアップ ファイルとしてインポートされている必要があります。  

> [!NOTE]
>  マルチキャストには最新バージョンの Windows AIK を使用することが重要です。初期のバージョンの Windows AIK (たとえば Windows AIK 1.0) に含まれる Windows PE は、マルチキャスト サーバーからのダウンロードをサポートしていません。  

 **既存の展開共有からのマルチキャスト用に MDT を構成するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share* に移動します (*deployment_share* は、構成する展開共有の名前)。  

3.  操作ウィンドウで **[プロパティ]** をクリックします。  

4.  **[General]** \(全般\) タブで、**[Enable multicast for this deployment share (requires Windows Server 2008 Windows Deployment Services)]** \(この展開共有のマルチキャストを有効にする \(Windows Server 2008 Windows 展開サービスが必要\)\) チェック ボックスをオンにします。  

5.  **[OK]** をクリックします。  

6.  操作ウィンドウで **[Update Deployment Share]** \(展開共有の更新\) をクリックします。  

     展開共有の更新ウィザードが開始されます。  

7.  **[Options]** \(オプション\) ページで、展開共有を更新する目的のオプションを選択し、**[Next]** \(次へ\) をクリックします。  

8.  **[Summary]** \(概要\) ページで詳細情報が正しいことを確認し、**[Next]** \(次へ\) をクリックします。  

9. **[Confirmation]** \(確認\) ページで **[Finish]** \(完了\) をクリックします。  

 これで、Windows 展開サービスのマルチキャスト転送用に展開共有が構成されました。  

 このプロセスにより、既存の MDT の展開共有を直接使用する Windows 展開サービスの自動キャスト マルチキャスト転送が作成されます。 MDT はスケジュールされたキャスト転送を作成しません。 また、Windows 展開サービスに追加のイメージはインポートされないこと、ブート イメージに対するマルチキャストは使用できないことに注意してください。Windows PE が実行開始された後でないと、マルチキャスト クライアントの読み込みができないためです。  

 **Windows 展開サービスでマルチキャスト転送が生成されていることを確認するには**  

1.  **[スタート]** をクリックし、**[管理ツール]** をポイントして、**[Windows 展開サービス]** をクリックします。  

2.  Windows 展開サービス コンソール ツリー上の **[サーバー]** を右クリックし、**[サーバーの追加]** をクリックします。  

3.  **[サーバーの追加]** ダイアログ ボックスで **[ローカル コンピューター]** をクリックし、**[OK]** をクリックします。  

4.  Windows 展開サービス コンソール ツリー上の **[サーバー]** をクリックし、***server_name*** をクリックします (*server_name* は、Windows 展開サービスを実行しているコンピューターの名前)。 **[マルチキャスト転送]** をクリックします。  

5.  詳細ウィンドウに、展開共有の新しい自動キャスト転送が表示されます。例: **BDD Share Deployment$**  

6.  **BDD Share Deployment$** という自動キャスト転送の状態が **[アクティブ]** に設定されていることを確認します。  

 コンピューターが展開された後、オペレーティング システムがマルチキャスト転送からダウンロードされたことを確認します。そのためには、\Windows\Temp\DeploymentLogs フォルダー内の BDD.log ファイルを調べます。  

 logs フォルダーには 2 つのエントリがあります。両方とも "**マルチキャスト転送**" で始まります。これらのエントリをチェックし、転送が成功したことを確認します。 MDT と Windows 展開サービスを使用したマルチキャスト転送の詳細については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Enable Windows Deployment Services Multicast Deployment for LTI Deployments」 (Windows 展開サービスのマルチキャスト展開を LTI 展開用に有効にする) のセクションを参照してください。  

## <a name="performing-staged-deployments-using-mdt-oem-preload"></a>MDT を使用したステージングされた展開の実行 (OEM プリロード)  
 多くの組織では、コンピューターを実稼働ネットワークに展開する前に、コンピューターにオペレーティング システム イメージを読み込みます。 場合によっては、組織内でステージング環境でのコンピューターの構築を担当するチームが、オペレーティング システム イメージの読み込みを実行します。 また、オペレーティング システム イメージの読み込みが、コンピューターのハードウェア ベンダーによって実行される場合もあります。これは*相手先ブランド供給* (OEM) とも呼ばれます。  

> [!NOTE]
>  OEM のプリロード プロセスは、展開が LTI を使用して実行される場合にのみ、MDT でサポートされています。 Configuration Manager では、事前設定されたメディア機能を使用します。  

### <a name="overview-of-the-oem-preload-process-in-mdt"></a>MDT での OEM プリロード プロセスの概要  
 OEM プリロード プロセスは、3 つのフェーズに分かれています。  

-   **フェーズ 1**:  ステージング環境に適用される、参照コンピューターのメディア ベースのイメージを作成します。  

-   **フェーズ 2**:  ステージング環境でターゲット コンピューターに、参照コンピューター イメージを適用します。  

-   **フェーズ 3**:  運用環境でターゲット コンピューターの展開を完了します。  

 フェーズ 1 とフェーズ 3 は、通常、展開組織によって実行されます。 組織が OEM プリロード プロセスを使用するかどうかによって、フェーズ 2 は、組織が実行する場合と、コンピューターを供給するコンピューター ハードウェア ベンダーが実行する場合があります。 組織がフェーズ 2 を実行する場合は、ステージング環境は組織内になります。 OEM がフェーズ 2 を実行する場合は、OEM の環境がステージング環境になります。  

#### <a name="overview-of-mdt-configuration-files-in-the-oem-preload-process"></a>OEM プリロード プロセスでの MDT 構成ファイルの概要  
 個別の MDT 構成ファイル (CustomSettings.ini と Bootstrap.ini) が、OEM プリロード プロセスのフェーズ 1 とフェーズ 3 で実行されるタスク シーケンスに使用されます。 ただし、両方の構成ファイルは、別のフォルダー構造で同時に存在します。  

 最初のフェーズでは、構成ファイルは、参照コンピューターの作成時に使用され、そのフェーズで使用されるタスク シーケンスに固有のフォルダーに格納されます。 OEM プリロード プロセスの 3 番目および最後のフェーズで使用する構成ファイルは、そのフェーズで使用されるタスク シーケンスに固有のフォルダーに格納されます。  

 構成ファイルに対する変更を行うときは、構成ファイルへの変更が、各 OEM プリロード プロセスのフェーズの適切なタスク シーケンスに対応することを確認してください。  

#### <a name="overview-of-mdt-log-files-in-the-oem-preload-process"></a>OEM プリロード プロセスでの MDT ログ ファイルの概要  
 OEM プリロード プロセスのフェーズ 1 およびフェーズ 3 で、MDT の個別のログ ファイルが生成されます。  

-   フェーズ 1 の MDT ログ ファイルは、C:\MININT および C:\SMSTSLog フォルダーに格納されます。  

-   フェーズ 3 の MDT ログ ファイルは、x86 ベースの展開では %WINDIR%\System32\CCM\Logs フォルダー、x64 ベースの展開では %WINDIR%\SysWow64\CCM\Logs フォルダーに格納されます。  

 MDT に関連する展開の問題の診断またはトラブルシューティング時に、適切なフォルダーを使用します。  

### <a name="staged-deployments-using-lti"></a>LTI を使用した段階的展開  
 LTI 展開では、*リムーバブル メディア (メディア)* という展開共有の種類を使用して OEM プリロード プロセスを実行します。 OEM プリロード プロセスでは、その他の展開共有の種類はサポートされていません。  

 OEM プリロード プロセスを実行するには、対象のオペレーティング システムの展開に使用されるタスク シーケンスに加え、ライトタッチ OEM タスク シーケンスというタスク シーケンス テンプレートに基づいてタスク シーケンスを作成します。 次に、*リムーバブル メディア (メディア)* という展開共有を作成します。最終的には展開共有の内容の ISO ファイルが作成されます。具体的には、LiteTouchPE_x86.iso ファイルまたは LiteTouchPE_x64.iso ファイルです (ターゲット コンピューターのプロセッサ プラットフォームに基づく)。 展開共有の更新プロセスでも、ユニバーサル ディスク フォーマットのメディアを作成するために使用できるフォルダー構造が作成されます。  

#### <a name="lti-oem-preload-processphase-1-create-a-media-based-image"></a>LTI OEM プリロード プロセス—フェーズ 1: メディア ベースのイメージを作成する  
 展開組織は、OEM プリロード プロセスの最初のフェーズを実行します。 このフェーズの最終的な成果物は、OEM または展開組織内のステージング環境に送られる、起動可能なイメージ (ISO ファイルなど) またはメディア (DVD など) です。 この手順の大部分は、Deployment Workbench で実行します。  

 **OEM または展開組織内のステージング環境に提供されるメディア ベースのイメージを作成するには**  

1.  Deployment Workbench で、次のノードを展開共有として事前設定します。  

    -   オペレーティング システム  

    -   アプリケーション  

    -   パッケージ  

    -   Out-of-Box Drivers (既定のドライバー)  

     この手順の実行について詳しくは、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」の「Managing Deployment Shares in the Deployment Workbench」 (Deployment Workbench での展開共有の管理) を参照してください。  

2.  Deployment Workbench で Litetouch OEM タスク シーケンスというタスク シーケンス テンプレートを基にして新しいタスク シーケンスを作成します。  

     この手順の実行について詳しくは、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Configuring Task Sequences in the Deployment Workbench」 (Deployment Workbench でのタスク シーケンスの構成) を参照してください。  

3.  運用環境への展開後、ターゲット コンピューター上に対象のオペレーティング システムを展開するために使用する 1 つまたは複数のタスク シーケンスを作成します。  

     この手順の実行について詳しくは、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Configuring Task Sequences in the Deployment Workbench」 (Deployment Workbench でのタスク シーケンスの構成) を参照してください。  

4.  OEM 展開に必要なアプリケーション、オペレーティング システム、ドライバー、パッケージ、およびタスク シーケンスを含む選択プロファイルを作成します。  

     この手順の実行について詳しくは、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Manage Selection Profiles」 (選択プロファイルの管理) を参照してください。  

5.  展開メディアを作成します。  

     この手順の実行について詳しくは、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Manage LTI Deployment Media」 (LTI 展開メディアの管理) を参照してください。  

6.  前の手順において Deployment Workbench で作成した展開メディアを更新します。  

     展開メディアを更新すると、Deployment Workbench で LiteTouchMedia.iso ファイルが作成されます。 この手順の実行について詳しくは、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」の「Manage LTI Deployment Media」 (LTI 展開メディアの管理) を参照してください。  

7.  前の手順で作成した LiteTouchMedia.iso ファイルを DVD に書き込みます。  

    > [!NOTE]
    >  ISO ファイルを OEM または組織のステージング環境に配布する場合、この手順は必要ありません。  

8.  ISO ファイルまたは DVD を、OEM または組織のステージング環境に配布します。  

#### <a name="lti-oem-preload-processphase-2-apply-the-image-to-the-target-computer"></a>LTI OEM プリロード プロセス—フェーズ 2: ターゲット コンピューターにイメージを適用する  
 OEM プリロード プロセスの 2 番目のフェーズは、OEM によって、または展開組織の展開チームによってステージング環境で実行されます。 プロセスのこのフェーズ中に、フェーズ 1 で作成した .iso ファイルまたは DVD が対象のコンピューターに適用されます。 このフェーズの成果物は、運用環境への展開準備が完了した、対象のコンピューターに展開されたイメージです。  

 **対象のコンピューターにイメージを適用するには**  

1.  フェーズ 1 で作成したメディアを使用してターゲット コンピューターを起動します。  

     Windows PE が起動し、Windows Deployment Wizard が開始されます。  

2.  Windows Deployment Wizard で、**[OEM Preinstallation Task Sequence for Staging Environment]** \(ステージング環境用の OEM プレインストール タスク シーケンス\) というタスク シーケンスをクリックします。  

     そのタスク シーケンスが開始され、起動可能なメディアの内容が、ターゲット コンピューターのローカル ハード ディスクにコピーされます。  

3.  Windows Deployment Wizard の **OEM Preinstallation Task Sequence for Staging Environment** タスク シーケンスが完了すると、ハード ディスクは残りの展開プロセスを開始できる状態になり、Windows Deployment Wizard を実行して、オペレーティング システムを展開するために使用されるその他のタスク シーケンスを処理します。  

     **OEM Preinstallation Task Sequence for Staging Environment** タスク シーケンスは、対象のコンピューターにイメージを展開し、LTI プロセスを開始します。 Windows Deployment Wizard が再び開始され、ターゲット コンピューターにオペレーティング システムを展開するために使用されるタスク シーケンスを実行します。  

4.  ステージング環境内の必要な数だけの対象のコンピューターに最初のハード ディスクの内容を複製します。  

5.  対象のコンピューターが、展開される運用環境に配布されます。  

#### <a name="lti-oem-preload-processphase-3-complete-target-computer-deployment"></a>LTI OEM プラロード プロセス—フェーズ 3: ターゲット コンピューターの展開を完了する  
 OEM プリロード プロセスの 3 番目および最後のフェーズは、展開組織の運用環境で実行されます。 プロセスのこのフェーズでは、ターゲット コンピューターが起動され、前のフェーズでステージング環境内のハード ディスクに配置した起動可能なメディア イメージが起動します。  

 **運用環境で対象のコンピューターの展開を完了するには**  

1.  ターゲット コンピューターを起動します。  

     Windows PE が起動し、Windows Deployment Wizard が開始されます。  

2.  ターゲット コンピューターごとに特定の構成情報を使用して Windows Deployment Wizard を実行します。  

     この手順の実行について詳しくは、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の「Running the Deployment Wizard」 (Deployment Wizard の実行) を参照してください。  

 このフェーズが完了すると、ターゲット コンピューターは運用環境で使用できる状態になります。  

## <a name="using-windows-powershell-to-perform-common-tasks"></a>Windows PowerShell を使用した一般的なタスクの実行  
 Deployment Workbench 上での MDT 管理タスクは、基礎になる Windows PowerShell コマンドレットによって実行します。コマンドレットを使用して、次のセクションに示すような管理タスクを自動化できます。  

 MDT の管理を自動化する手順は次のとおりです。  

-   新しい展開共有を作成します。「[新しい展開共有の作成](#CreateNewDeployShare)」を参照してください。  

-   展開共有内にフォルダーを作成します。「[フォルダーの作成](#CreateFolder)」を参照してください。  

-   展開共有からフォルダーを削除します。「[フォルダーの削除](#DeleteFolder)」を参照してください。  

-   デバイス ドライバーを展開共有にインポートします。「[デバイス ドライバーのインポート](#ImportDeviceDriver)」を参照してください。  

-   展開共有からデバイス ドライバーを削除します。「[デバイス ドライバーの削除](#DeleteDeviceDriver)」を参照してください。  

-   オペレーティング システム パッケージを展開共有にインポートします。「[オペレーティング システム パッケージのインポート](#ImportOpSysPackage)」を参照してください。  

-   展開共有からオペレーティング システム パッケージを削除します。「[オペレーティング システム パッケージの削除](#DeleteOpSysPackage)」を参照してください。  

-   オペレーティング システムを展開共有にインポートします。「[オペレーティング システムのインポート](#ImportOpSys)」を参照してください。  

-   展開共有からオペレーティング システムを削除します。「[オペレーティング システムの削除](#DeleteOpSys)」を参照してください。  

-   展開共有内にアプリケーションを作成します。「[アプリケーションの作成](#CreateApplication)」を参照してください。  

-   展開共有からアプリケーションを削除します。「[アプリケーションの削除](#DeleteApplication)」を参照してください。  

-   展開共有内にタスク シーケンスを作成します。「[タスク シーケンスの作成](#CreateTaskSequence)」を参照してください。  

-   展開共有からタスク シーケンスを削除します。「[タスク シーケンスの削除](#DeleteTaskSequence)」を参照してください。  

-   MDT DB を作成します。「[MDT DB の作成](#CreateMDTDB)」を参照してください。  

-   選択プロファイルを作成します。「[選択プロファイルの作成](#CreateSelectProfile)」を参照してください。  

-   展開共有を更新します。「[展開共有の更新](#UpdatingDeployShare)」を参照してください。  

-   リンクされた展開共有を作成します。「[リンクされた展開共有の作成](#CreateLinkedDeployShare)」を参照してください。  

-   リンクされた展開共有を更新します。「[リンクされた展開共有の更新](#UpdatingLinkedDeployShare)」を参照してください。  

-   リンクされた展開共有を削除します。「[リンクされた展開共有の削除](#DeleteLinkedDeployShare)」を参照してください。  

-   展開メディアを作成します。「[メディアの作成](#CreateMedia)」を参照してください。  

-   展開メディアを生成します。「[メディアの生成](#GenerateMedia)」を参照してください。  

-   展開メディアを削除します。「[メディアの削除](#DeleteMedia)」を参照してください。  

###  <a name="CreateNewDeployShare"></a> 新しい展開共有の作成  
 次の Windows PowerShell コマンドにより、D:\Production Deployment Share に *Production$* という新しい展開共有が作成されます。 新しい展開共有が Deployment Workbench に Production として表示されます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "D:\Production Deployment Share" -Description "Production" -NetworkPath "\\Deployment_Server\Production$" -Verbose | add-MDTPersistentDrive -Verbose  
    ```  

###  <a name="CreateFolder"></a> フォルダーの作成  
 次の Windows PowerShell コマンドにより、Deployment Workbench コンソール ツリー上の Deployment Workbench\/Deployment Shares\/Production\/Applications に Adobe フォルダーが作成されます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Applications" -enable "True" -Name "Adobe" -Comments "This folder contains Adobe software" -ItemType "folder" -Verbose remove-psdrive DS001 -Verbose  
    ```  

    > [!NOTE]
    >  スクリプトに "`remove-psdrive`" を追加すると、続行する前にバックグラウンド プロセスを終了します。  

###  <a name="DeleteFolder"></a> フォルダーの削除  
 次の Windows PowerShell コマンドにより、Deployment Workbench\/Deployment Shares\/Production\/Applications\/Adobe フォルダーが削除されます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Remove-item -path "DS002:\Applications\Adobe" -Verbose  
    ```  

> [!NOTE]
>  フォルダーが空でない場合、スクリプトは失敗します。  

###  <a name="ImportDeviceDriver"></a> デバイス ドライバーのインポート  
 次の Windows PowerShell コマンドにより、Dell 2407 WFP モニターのデバイス ドライバーが運用展開共有にインポートされます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtdriver -path "DS002:\Out-of-Box Drivers\Monitor" -SourcePath "D:\Drivers\Dell\2407 WFP" -Verbose  
    ```  

###  <a name="DeleteDeviceDriver"></a> デバイス ドライバーの削除  
 次の Windows PowerShell コマンドにより、Dell 2407 WFP モニターのデバイス ドライバーが運用展開共有から削除されます。  

```  
Remove-item -path "DS002:\Out-of-Box Drivers\Dell Inc. Monitor 2407WFP.INF 1.0" -Verbose  
```  

###  <a name="ImportOpSysPackage"></a> オペレーティング システム パッケージのインポート  
 次の Windows PowerShell コマンドは、D:\\Updates\\Microsoft\\Vista の下にあるすべてのオペレーティング システム パッケージをインポートします。 これらのオペレーティング システム パッケージは、運用展開共有 (D:\\Production Deployment Share) に格納されます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtpackage -path "DS002:\Packages" -SourcePath "D:\Updates\Microsoft\Vista" -Verbose  
    ```  

###  <a name="DeleteOpSysPackage"></a> オペレーティング システム パッケージの削除  
 次の Windows PowerShell コマンドにより、指定したオペレーティング システム パッケージが運用展開共有から削除されます。  

```  
Remove-item -path "DS002:\Packages\Package_1_for_KB940105 neutral x86 6.0.1.0 KB940105" -Verbose  
```  

###  <a name="ImportOpSys"></a> オペレーティング システムのインポート  
 次の Windows PowerShell コマンドにより、D:\\Operating Systems\\Windows Vista x86 にある Windows Vista オペレーティング システムがインポートされます。 オペレーティング システムは、運用展開共有 (D:\\Production Deployment Share) に格納されます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtoperatingsystem -path "DS002:\Operating Systems" -SourcePath "D:\Operating Systems\Windows Vista x86" -DestinationFolder "Windows Vista x86" -Verbose  
    ```  

###  <a name="DeleteOpSys"></a> オペレーティング システムの削除  
 次の Windows PowerShell コマンドにより、Windows Vista HOMEBASIC オペレーティング システムが運用展開共有から削除されます。  

```  
Remove-item -path "DS002:\Operating Systems\Windows Vista HOMEBASIC in Windows Vista x86 install.wim" -Verbose  
```  

###  <a name="CreateApplication"></a> アプリケーションの作成  
 次の Windows PowerShell コマンドにより、D:\\Software\\Adobe\\Reader 9 にあるソース ファイルを使用して、Adobe Reader 9 アプリケーションが作成されます。 アプリケーションは、運用展開共有 (D:\\Production Deployment Share) に格納されます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-MDTApplication -path "DS002:\Applications" -enable "True" -Name "Adobe Reader 9" -ShortName "Reader" -Version "9" -Publisher "Adobe" -Language "" -CommandLine "setup.exe" -WorkingDirectory ".\Applications\Adobe Reader 9" -ApplicationSourcePath "D:\Software\Adobe\Reader 9" -DestinationFolder "Adobe Reader 9" -Source ".\Applications\Adobe Reader 9" -Verbose  
    ```  

###  <a name="DeleteApplication"></a> アプリケーションの削除  
 次の Windows PowerShell コマンドにより、運用展開共有から Adobe Reader 9 アプリケーションが削除されます。  

```  
Remove-item -path "DS002:\Applications\Adobe Reader 9" -Verbose  
```  

###  <a name="CreateTaskSequence"></a> タスク シーケンスの作成  
 次の Windows PowerShell コマンドにより、**Windows Vista Production Build** (Windows Vista 運用ビルド) タスク シーケンスが運用展開共有 (D:\\Production Deployment Share) に作成されます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdttasksequence -path "DS002:\Task Sequences" -Name "Windows Vista Business Production Build" -Template "Client.xml" -Comments "Approved for use in the production environment.  This task sequence uses the Standard Client task sequence template" -ID "Vista_Ref" -Version "1.0" -OperatingSystemPath "DS002:\Operating Systems\Windows Vista BUSINESS in Windows Vista x86 install.wim" -FullName "Fabrikam User" -OrgName "Fabrikam" -HomePage "http://www.Fabrikam.com" -AdminPassword "secure_password" -Verbose  
    ```  

###  <a name="DeleteTaskSequence"></a> タスク シーケンスの削除  
 次の Windows PowerShell コマンドにより、**Windows Vista Production Build** (Windows Vista 運用ビルド) タスク シーケンスが運用展開共有から削除されます。  

```  
Remove-item -path "DS002:\Task Sequences\Windows Vista Business Production Build" -force -Verbose  
```  

###  <a name="CreateMDTDB"></a> MDT DB の作成  
 次の Windows PowerShell コマンドにより、運用展開共有のための新しい MDT DB が *deployment\_server* サーバー上に作成されます。 データベース接続は TCP\/IP を経由します。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-MDTDatabase -path "DS002:" -SQLServer "DeploymentServer" -Netlib "DBMSSOCN" -Database "MDT2010" -SQLShare "DB_Connect" -Force -Verbose  
    ```  

###  <a name="CreateSelectProfile"></a> 選択プロファイルの作成  
 次の Windows PowerShell コマンドにより、新しいアプリケーション選択プロファイルが作成されます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Selection Profiles" -enable "True" -Name "Applications" -Comments "" -Definition "<SelectionProfile><Include path="Applications" /></SelectionProfile>" -ReadOnly "False" -Verbose  
    ```  

###  <a name="UpdatingDeployShare"></a> 展開共有の更新  
 次の Windows PowerShell コマンドにより、運用展開共有 (D:\\Production Deployment Share) が更新されます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  
    
-   ```
    Update\-MDTDeploymentShare \-path "DS002:" \-Verbose  
    ```
    
###  <a name="CreateLinkedDeployShare"></a> リンクされた展開共有の作成  
 次の Windows PowerShell コマンドにより、運用展開共有にリンクされた展開共有が作成され、\\\\*remote\_server\_name*\\Deployment$ 共有に格納されます。 Everything (すべて) という選択プロファイルは、リンクされた展開共有にレプリケートされる内容を決定するために使われます。 運用展開共有の内容が、\\\\*remote\_server\_name*\\Deployment$ 共有に既に存在する内容とマージされます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Linked Deployment Shares" -enable "True" -Name "LINKED001" -Comments "" -Root "\\RemoteServerName\Deployment$" -SelectionProfile "Everything" -Replace "False" -Verbose  
    ```  

###  <a name="UpdatingLinkedDeployShare"></a> リンクされた展開共有の更新  
 次の Windows PowerShell コマンドにより、LINKED001 展開共有が更新されます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Replicate-MDTContent -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="DeleteLinkedDeployShare"></a> リンクされた展開共有の削除  
 次の Windows PowerShell コマンドにより、LINKED001 展開共有が削除されます。  

-   Add\-PSSnapIn Microsoft.BDD.PSSnapIn  

-   ```  
    Remove-item -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="CreateMedia"></a> メディアの作成  
 次の Windows PowerShell コマンドにより、起動可能なメディアを作成するために使われる内容を含むソース フォルダーが作成されます。 運用展開共有がソースとして使用されます。 Everything 選択プロファイルにより、メディア コンテンツ フォルダーに格納される内容が決定します。 メディアが生成されるときに LiteTouchMedia.iso ファイルが作成されます。 メディアは、x86 と x64 の両方のプラットフォームをサポートします。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Media" -enable "True" -Name "MEDIA001" -Comments "some comment here" -Root "D:\Media" -SelectionProfile "Everything" -SupportX86 "True" -SupportX64 "True" -GenerateISO "True" -ISOName "LiteTouchMedia.iso" -Verbose  
    ```  

-   ```  
    New-PSDrive -Name "MEDIA001" -PSProvider "MDTProvider" -Root "D:\Media\Content" -Description "Embedded media deployment share" -Force -Verbose  
    ```  

###  <a name="GenerateMedia"></a> メディアの生成  
 次の Windows PowerShell コマンドにより、D:\\Media に LiteTouchMedia.iso ファイルが作成されます。このファイルには MEDIA001 メディア ソース フォルダーの内容が使用されます。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Generate-MDTMedia -path "DS002:\Media\MEDIA001" -Verbose  
    ```  

###  <a name="DeleteMedia"></a> メディアの削除  
 次の Windows PowerShell コマンドにより、MEDIA001 メディアが運用展開共有から削除されます。  

```  
Remove-item -path "DS002:\Media\MEDIA001" -Verbos  
```  

## <a name="delaying-domain-join-to-avoid-application-of-group-policy-objects"></a>グループ ポリシー オブジェクトの適用を避けるためのドメイン参加遅延  
 グループ ポリシーは、一元的な一対多のモデルを使用して多数の Active Directory Domain Services (AD DS) コンピューターとユーザー オブジェクトを効率的に管理する機能を提供する、充実した柔軟なテクノロジです。 グループ ポリシー設定は、グループ ポリシー オブジェクト (GPO) に格納され、1 つ以上の AD DS サービス コンテナー (サイト、ドメイン、組織単位 (OU)) にリンクされます。  

 組織によっては、グループ ポリシー設定による制限が存在し、オペレーティング システム展開中に問題が発生することがあります。 たとえば、次のグループ ポリシー設定は、自動ログオン プロセスを中断できます。  

-   自動ログオンの制限  

-   管理者アカウントの名前変更  

-   法的バナーとキャプション  

-   制限の厳しいセキュリティ ポリシー (たとえば、セキュリティ特化 – 機能制限 [SSLF] ポリシー)  

 展開中に GPO が原因と考えられる問題が発生しないようにするための 1 つのオプションとして、展開プロセスにおいてできる限り遅い時点で、コンピューターをドメインに参加します。 このような参加を行うには、ZTIDomainJoin.wsf スクリプトを実行するカスタム タスク シーケンス ステップを使用します。  

 ターゲット コンピューターをドメインに参加させるには、ZTIDomainJoin.wsf スクリプトで **DomainAdmin**、**DomainAdminDomain**、**DomainAdminPassword**、**JoinDomain**、**MachineObjectOU** の各プロパティを使用します。 これらのプロパティは、Windows Deployment Wizard、展開共有規則、MDT DB、Configuration Manager のコンピューターと収集に関する規則を使用して宣言できます。 使用するアカウントに、ドメイン内のコンピューター オブジェクトの作成および削除に必要な権限が必要です。  

 通常、ZTIConfigure.wsf スクリプトでは、これらのプロパティに指定した値を使用して Unattend.xml または Unattend.txt ファイルを更新します。 これらの設定はその後、Windows セットアップ プログラムによって解析され、システムは、展開プロセスの早い段階でドメインに参加しようとします。 それによりターゲット コンピューターにドメインの GPO に指定された設定が適用され、展開プロセスが失敗する可能性があります。  

 展開プロセス中にターゲット コンピューターのドメイン参加を意図的に遅らせるために、Unattend.xml ファイルから特定の要素を削除できます。 関連付けられたプロパティ要素がファイルにない場合、ZTIConfigure.wsf スクリプトは Unattend.xml ファイルへのプロパティ書き込みをスキップします。  

> [!NOTE]
>  このサンプルでの回避策は、Windows 7、Windows Server 2008、または Windows Server 2008 R2 オペレーティング システムを展開する場合にのみ有効です。  

 **対象のコンピューターが Windows セットアップ中にドメイン参加を試みないように unattend.xml ファイルを準備する**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Task Sequences/*task_sequence* に移動します (*deployment_share* は展開共有の名前。*task_sequence* は、構成するタスク シーケンスの名前)。  

3.  操作ウィンドウで **[プロパティ]** をクリックします。  

4.  **[OS Info]** \(OS 情報\) タブで **[Edit Unattend.xml]** \(Unattend.xml の編集\) をクリックします。  

     Windows システム イメージ マネージャー (Windows SIM) が開始されます。  

5.  **応答ファイル** ウィンドウ上の **4 specialize/Identification/Credentials**に移動します。 **[Credentials]** \(資格情報\) を右クリックし、**[削除]** をクリックします。  

6.  **[はい]** をクリックします。  

7.  応答ファイルを保存し、Windows SIM を終了します。  

8.  タスク シーケンスの**プロパティ**のダイアログ ボックスで、**[OK]** をクリックします。  

 `Credentials` 要素が unattend.xml ファイル内にないため、ZTIConfigure.wsf スクリプトを使用してドメイン参加情報を Unattend.xml ファイル内に事前設定することができません。これにより、Windows セットアップによるドメイン参加の試みが行われないようにすることができます。  

 **対象のコンピューターをドメインに参加させるタスク シーケンス ステップを追加するには**  

1.  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントします。 **[Microsoft Deployment Toolkit]** をポイントし、**[Deployment Workbench]** をクリックします。  

2.  Deployment Workbench コンソール ツリー上の Deployment Workbench/Deployment Shares/*deployment_share*/Task Sequences/*task_sequence* に移動します (*deployment_share* は展開共有の名前。*task_sequence* は、構成するタスク シーケンスの名前)。  

3.  操作ウィンドウで **[プロパティ]** をクリックします。  

4.  **[Task Sequence]** \(タスク シーケンス\) タブ上の [State Restore\(状態復元\) ノードに移動します。  

5.  **Recover From Domain** (ドメインから復旧) タスク シーケンス ステップが存在することを確認します。 存在する場合は、手順 9. に進みます。  

6.  タスク シーケンスの**プロパティ**のダイアログ ボックスで、**[Add]** \(追加\) をクリックし、**[Settings]** \(設定\) に移動して **[Recover From Domain]** \(ドメインから復旧\) をクリックします。  

7.  **Recover From Domain** タスク シーケンス ステップをタスク シーケンス エディターに追加します。 ステップがタスク シーケンスの適切な位置にあることを確認します。  

8.  **Recover From Domain** タスク シーケンス ステップの設定が、目的どおりに構成されていることを確認します。  

9. タスク シーケンスの**プロパティ**のダイアログ ボックスで、**[OK]** をクリックしてタスク シーケンスを保存します。
