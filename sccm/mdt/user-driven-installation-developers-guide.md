---
title: ユーザー駆動型インストール
titleSuffix: Microsoft Deployment Toolkit
description: 'Microsoft Deployment Toolkit 2013 のユーザー駆動型インストールの開発者ガイド。 '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: a2b3a3a0-7b81-4191-b1f9-c618e59347c3
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 434178f100c32a4188ecf5283066f9332035f761
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2018
---
# <a name="user-driven-installation---developers-guide"></a>ユーザー駆動型インストール - 開発者ガイド
ユーザー駆動型インストール (UDI) は、Microsoft® System Center 2012 R2 Configuration Manager でオペレーティング システムの展開 (OSD) 機能を使用して、Windows 8.1 などの Windows® クライアント オペレーティング システムのコンピューターへの展開を簡略化するのに役立ちます。 UDI は Microsoft Deployment Toolkit (MDT) の一部です。  

## <a name="introduction"></a>概要  
 通常、OSD 機能を使用してオペレーティング システムを展開する場合は、オペレーティング システムの展開に必要なすべての情報を提供する必要があります。 この情報は、構成ファイルまたはデータベース (CustomSettings.ini ファイルや MDT データベース [MDT DB] など) で構成されます。 展開を開始する前に、すべての構成設定を指定する必要があります。  

 UDI は、展開を実行する直前に、構成情報を提供できるウィザード ベースのインターフェイスを提供します。 この動作により、汎用の OSD タスク シーケンスを作成してから、展開時にコンピューターに固有の情報を提供することができ、展開プロセスの柔軟性が向上します。  

### <a name="target-audience"></a>対象読者  
 このガイドは、UDI ウィザードのカスタム ウィザード ページ、および UDI ウィザード デザイナーのカスタム ウィザード ページ エディターを作成する開発者向けに書かれています。 このガイドは、以下を使用した Windows アプリケーションの開発を十分に理解していることを前提としています。  

-   C++: カスタム ウィザード ページを作成するために使用  

-   Microsoft .NET Framework: カスタム ウィザード ページ エディターを作成するために使用  

-   Windows Presentation Foundation (WPF): カスタム ウィザード ページ エディターを作成するために使用  

-   WPF でサポートする言語 (C#、C++、または Microsoft Visual Basic® .NET など): カスタム ウィザード ページ エディターを作成するために使用  

### <a name="about-this-guide"></a>このガイドの内容  
 このガイドでは、組織の UTI をカスタマイズするために必要な参照情報を提供します。 このガイドでは、MDT のインストール (UDI を含む)、オペレーティング システムとアプリケーションを展開する UDI の構成、または UDI ウィザードを使用した展開の実行など、管理または操作のトピックについては説明しません。 これらのトピックの詳細については、MDT に含まれている「*Using the Microsoft Deployment Toolkit*」(Microsoft Deployment Toolkit の使用) の UDI に関するトピックを参照してください。  

## <a name="udi-development-overview"></a>UDI 開発の概要  
 UDI 開発では、UDI が提供する機能を拡張できます。 通常、UDI 開発は、UDI 展開プロセスで使用する追加の情報を収集する場合に必要になります。 この追加情報は、通常、Configuration Manager で UDI タスク シーケンス内のタスク シーケンス ステップが読み取るタスク シーケンス変数として保存されます。  

### <a name="udi-architecture"></a>UDI アーキテクチャ  
 UDI 開発の高度な目標は、UDI ウィザードに表示できるカスタム ウィザード ページを作成することです。 カスタム ウィザード ページを作成することで、UDI の既存の機能を拡張して、組織のビジネスと技術的な要件を満たすことができます。 カスタム ウィザード ページでは、UDI が提供するウィザード ページの追加情報、または代わりとなる情報が収集されます。  

 図 1 は、UDI ウィザード デザイナーと UDI ウィザード間のリレーションシップを示しています。  

 ![UDIDevelopersGuide1](media/UDIDevelopersGuide1.jpg "UDIDevelopersGuide1")  
図 1 UDI ウィザードと UDI ウィザード デザイナー間のリレーションシップ  

 **図 1UDI ウィザードと UDI ウィザード デザイナー間のリレーションシップ**  

 概念レベルでは、UDI 開発には次の作成が含まれます。  

-   **カスタム ウィザード ページ**。 ウィザード ページは、UDI ウィザードに表示され、展開プロセスを完了するために必要な情報を収集します。 ウィザード ページは、Microsoft Visual Studio® で C++ を使用して作成します。 カスタム ウィザード ページは、UDI ウィザードが読み取る DLL として実装されます。 UDI ソフトウェア開発キット (SDK) には、カスタム ウィザード ページの作成方法の例が含まれています。  

-   **カスタム ウィザード ページ エディター**。 カスタム ウィザード ページの動作を構成するには、ウィザード ページ エディターを使用します。 カスタム ウィザード ページ エディターは、UDI ウィザード デザイナーが読み取る DLL として実装されます。 ウィザード ページ エディターは、次を使用して作成します。  

    -   [WPF](http://msdn.microsoft.com/library/ms754130.aspx) バージョン 4.0  

    -   [Microsoft Prism](http://compositewpf.codeplex.com/) バージョン 4.0  

    -   [Microsoft Unity Application Block](http://unity.codeplex.com/) (Unity) バージョン 2.1  

     MDT には、UDI ウィザード デザイナーで使用するためのカスタム ウィザード ページ エディターを作成するために必要なすべてのアセンブリが含まれています。 UDI SDK には、カスタム ウィザード ページ エディターの作成方法の例が含まれています。  

 さらに、UDI ウィザード デザイナーは、サポートするウィザード ページ エディターの構成ファイルを使用します。 カスタム ウィザード ページおよびカスタム ウィザード ページ エディターを作成するプロセスの一環として、ウィザード ページ エディターの構成ファイルを作成します。 UDI ウィザード デザイナーは、UDI ウィザードの構成ファイルと対応する .app ファイルに必要な XML 情報を作成します。  

### <a name="preparing-the-udi-development-environment"></a>UDI 開発環境の準備  
 独自のカスタム ウィザード ページおよびウィザード ページ エディターの作成を開始する前に、次の手順を実行して UDI 開発環境を準備します。  

1.  「[UDI 開発環境の前提条件を準備する](#PrepareUDIDevelopmentEnvironmentPrerequisites)」の説明に従って、UDI 開発環境の前提条件を準備します。  

2.  「[UDI 開発環境を構成する](#ConfigureUDIDevelopmentEnvironment)」の説明に従って、UDI 開発環境を構成します。  

3.  「[UDI 開発環境を検証する](#VerifyUDIDeploymentEnvironment)」の説明に従って、UDI 開発環境が正しく構成されていることを確認します。  

####  <a name="PrepareUDIDevelopmentEnvironmentPrerequisites"></a> UDI 開発環境の前提条件を準備する  
 UDI 開発環境の前提条件を準備するには、次の手順を実行します。  

1.  「[UDI 開発環境の必須ハードウェアを準備する](#PrepareUDIDevelopmentEnvironmentHardwarePrerequisites)」の説明に従って、UDI 開発環境の必須ハードウェアを準備します。  

2.  「[UDI 開発環境の必須ソフトウェアを準備する](#PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites)」の説明に従って、UDI 開発環境の必須ソフトウェアを準備します。  

#####  <a name="PrepareUDIDevelopmentEnvironmentHardwarePrerequisites"></a> UDI 開発環境の必須ハードウェアを準備する  
 UDI 開発環境の必須ハードウェアは、ご利用になっている Microsoft Visual Studio 2010 のエディションのハードウェア要件と同じです。 これらの要件の詳細については、[Visual Studio 2010 製品](http://www.microsoft.com/visualstudio/products/2010-editions)で各エディションのシステム要件を参照してください。  

#####  <a name="PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites"></a> UDI 開発環境の必須ソフトウェアを準備する  
 UDI 開発環境には、次のソフトウェアの前提条件があります。  

-   Visual Studio 2010 でサポートされる任意の Windows オペレーティング システム (Windows 7 または Windows Server® 2008 R2 を推奨)。  

     開発するプロセッサ アーキテクチャをサポートする Windows オペレーティング システムが必要です。 64 ビット オペレーティング システムを使用して 32 ビットおよび 64 ビットの UDI 開発を行うことができます。 32 ビット オペレーティング システムでは、32 ビットの UDI 開発しかできません。 このため、64 ビット オペレーティング システムを使用する必要があります。  

    > [!NOTE]
    >  UDI 開発環境では、Intel Itanium バージョン (IA-64) の Windows オペレーティング システムはサポートされていません。  

     Visual Studio 2010 でサポートされるオペレーティング システムの詳細については、[Visual Studio 2010 製品](http://www.microsoft.com/visualstudio/products/2010-editions)で各エディションのシステム要件を参照してください。  

-   Microsoft .NET Framework バージョン 4.0 (Visual Studio 2010 で必要)  

-   C++ 言語 (UDI ウィザード ページの拡張で使用される言語)  

-   WPF でサポートしているその他の言語 (C#、Visual Basic .NET、または C++/CLI など)。UDI ウィザード デザイナーのウィザード ページ エディターを拡張するために使用されます。  

    > [!NOTE]
    >  UDI ウィザード デザイナーのウィザード ページ エディターのサンプル ソース コードは、C# で記述されています。 このサンプル ソース コードを使用する場合は、C# 言語をインストールします。  

####  <a name="ConfigureUDIDevelopmentEnvironment"></a> UDI 開発環境を構成する  
 開発環境の前提条件を満たしたら、次の手順を実行して、UDI 開発環境を構成します。  

1.  Visual Studio 2010 をインストールします。  

     C++ 言語および WPF でサポートされているその他の言語がインストールされていることを確認します。  

    > [!NOTE]
    >  UDI ウィザード デザイナー エディター ページのサンプル ソース コードは、C# で記述されています。 このサンプル ソース コードを使用する場合は、C# 言語をインストールします。  

     Visual Studio 2010 のインストールに関する詳細については、「[Visual Studio のインストール](http://msdn.microsoft.com/library/e2h7fzkw.aspx)」を参照してください。  

2.  MDT をインストールします。  

     MDT のインストール方法の詳細については、MDT ドキュメント「*Using the Microsoft Deployment Toolkit*」 (Microsoft Deployment Toolkit の使用) の「Installing or Upgrading to MDT」 (MDT のインストールまたはアップグレード) セクションを参照してください。  

3.  エクスプローラーで、*local_folder* を作成します (ここで *local_folder* は、開発用コンピューター上のローカル ドライブ上に作成される任意のフォルダーです)。  

4.  *installation_folder*\SDK フォルダーを *local_folder* にコピーします (ここで *installation_folder* は MDT をインストールしたフォルダーで、*local_folder* は開発用コンピューター上のローカル ドライブ上にある任意のフォルダーです)。  

     SDK フォルダーを別の場所にコピーするのは、管理者特権のアクセス許可がないと書き込めない Program Files フォルダーに MDT がインストールされているからです。 SDK フォルダーを別の場所にコピーすることで、管理者特権のアクセス許可がなくても SDK フォルダー内のファイルを変更することができます。  

5.  *installation_folder*\Templates\Distribution\Tools フォルダーを *local_folder* にコピーします (ここで *installation_folder* は MDT をインストールしたフォルダーで、*local_folder* はプロセスで以前に作成したフォルダーです)。  

6.  *local_folder*\Tools フォルダーの名前を *local_folder*\OSDSetupWizard に変更します (ここで *local_folder* はプロセスで以前に作成したフォルダーです)。  

     完了すると、*local_folder* 下のフォルダー構造は、図 2 のようになるはずです (ここで *local_folder* はプロセスで以前に作成したフォルダーで、図では *UDIDevelopment* として表示されています)。  

     ![UDIDevelopersGuide2](media/UDIDevelopersGuide2.jpg "UDIDevelopersGuide2")  
図 2 UDI 開発のフォルダー構造  

     **図 2UDI 開発のフォルダー構造**  

####  <a name="VerifyUDIDeploymentEnvironment"></a> UDI 開発環境を検証する  
 UDI 開発環境を構成したら、Visual Studio 2010 でサンプル プロジェクトが正しくビルドできることを確認することで、その UDI 開発環境が正しく構成されていることを検証します。  

 以下を判断することで、UDI 開発環境が正しく構成されていることを検証します。  

-   「[SamplePage プロジェクトが正しくビルドされることを検証する](#VerifySamplePageProjectBuildsCorrectly)」に記載されているように、SamplePage プロジェクトが正しくビルドされるかどうか  

-   「[SampleEditor プロジェクトが正しくビルドされることを検証する](#VerifySampleEditorProjectBuildsCorrectly)」に記載されているように、SampleEditor プロジェクトが正しくビルドされるかどうか  

#####  <a name="VerifySamplePageProjectBuildsCorrectly"></a> SamplePage プロジェクトが正しくビルドされることを検証する  
 SamplePage プロジェクトでは、UDI ウィザードのカスタム ウィザード ページの作成方法の例が提供されています。 SamplePage プロジェクトに関する詳細は、「[SamplePage Visual Studio ソリューションを確認する](#ReviewSamplePageVisualStudioSolution)」を参照してください。  

 **SamplePage プロジェクトが正しくビルドされることを検証するには**  

1.  Visual Studio 2010 を起動します。  

2.  SamplePage プロジェクトを開きます。  

     SamplePage プロジェクトは、*local_folder*\SDK\UDI\SamplePage フォルダーにあります (ここで *local_folder* はプロセスで以前に作成したフォルダーです)。  

3.  Visual Studio 2010 のソリューション エクスプローラーで、SamplePage プロジェクトを右クリックして、**[プロパティ]** をクリックします。  

     **[SamplePage プロパティ ページ]** ダイアログ ボックスが表示されます。  

4.  **[SamplePage プロパティ ページ]** ダイアログ ボックスで、[構成プロパティ]、[デバッグ] の順に移動します。  

5.  [デバッグ] プロパティの **[構成]** の下で **[すべての構成]** を選択します。  

6.  [デバッグ] プロパティの **[コマンド]** の下に「**$(TargetDir)\OSDSetupWizard.exe**」と入力します。  

7.  [デバッグ] プロパティの **[作業ディレクトリ]** の下に「**$ (targetdir)**」と入力します。  

8.  **[SamplePage プロパティ ページ]** ダイアログ ボックスで、[構成プロパティ]、[ビルド イベント]、[ビルド後のイベント] の順に移動します。  

9. [ビルド後のイベント] プロパティの **[コマンド ライン]** の下に以下を入力します。  

    ```  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\*.*" "$(TargetDir)"  
    xcopy /y /i "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\en-us" "$(TargetDir)en-us"  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\OSDResults\Images\UDI_Wizard_Banner.bmp" "$(ProjectDir)header.bmp"  
    copy /y "$(ProjectDir)Config.xml" "$(TargetDir)”  
    copy /y "$(ProjectDir)header.bmp" "$(TargetDir)header.bmp"  
    ```  

10. **[SamplePage プロパティ ページ]** ダイアログ ボックスで、**[OK]** をクリックします。  

11. プロジェクトを保存します。  

12. **[デバッグ]** メニューで **[デバッグの開始]** をクリックします。  

     ソースが最新ではないことを示す **[Microsoft Visual Studio]** ダイアログ ボックスが表示され、プロジェクトをビルドするかどうかの確認が求められます。  

13. **[Microsoft Visual Studio]** ダイアログ ボックスで、**[はい]** をクリックします。  

     OSDSetupWizard.exe に利用可能なデバッグ情報がないことを通知する **[No Debugging Information]\(デバッグ情報なし\)** ダイアログ ボックスが表示されます。  

14. **[No Debugging Information]\(デバッグ情報なし\)** ダイアログ ボックスで、**[はい]** をクリックします。  

     UDI ウィザードが開き、カスタム ウィザード ページが表示されます。  

15. **[Choose your location]\(場所を選択\)** で値が選択できることを確認します。  

16. **[Wizard with sample page]\(サンプル ページを使用したウィザード\)** フォームで、**[キャンセル]** をクリックします。  

     **[ウィザードの取り消し]** ダイアログ ボックスが表示されます。  

17. **[ウィザードの取り消し]** ダイアログ ボックスで、**[はい]** をクリックします。  

18. Visual Studio 2010 を閉じます。  

#####  <a name="VerifySampleEditorProjectBuildsCorrectly"></a> SampleEditor プロジェクトが正しくビルドされることを検証する  
 SampleEditor プロジェクトでは、UDI ウィザード デザイナーのカスタム ウィザード ページ エディターの作成方法の例が提供されています。 SampleEditor プロジェクトに関する詳細は、「[SamplePage Visual Studio ソリューションを確認する](#ReviewSamplePageVisualStudioSolution)」を参照してください。  

 **SampleEditor プロジェクトが正しくビルドされることを検証するには**  

1.  Visual Studio 2010 を起動します。  

2.  SampleEditor プロジェクトを開きます。  

     SampleEditor プロジェクトは、*local_folder*\SDK\UDI\SampleEditor フォルダーにあります (ここで *local_folder* はプロセスで以前に作成したフォルダーです)。  

3.  Visual Studio 2010 のソリューション エクスプローラーで、SampleEditor プロジェクトを選択します。  

4.  **[プロジェクト]** メニューから **[参照の追加]** をクリックします。  

     **[参照の追加]** ダイアログ ボックスが表示されます。  

5.  **[参照の追加]** ダイアログ ボックスで、**[参照]** タブをクリックします。  

6.  **[参照]** タブで、*installation_folder*\Bin に移動します (ここで *installation_folder* は MDT をインストールしたフォルダーです)。 次のファイルを選択し、**[OK]** をクリックします。  

    -   Microsoft.Enterprise.UDIDesigner.Common.dll  

    -   Microsoft.Enterprise.UDIDesigner.DataService.dll  

    -   Microsoft.Enterprise.UDIDesigner.Infrastructure.dll  

    -   Microsoft.Practices.Prism.dll  

    -   Microsoft.Practices.ServiceLocation.dll  

    -   Microsoft.Practices.Unity.dll  

    -   RibbonControlsLibrary.dll  

    > [!NOTE]
    >  **[参照]** タブで Ctrl キーを押しながらファイルをクリックすることで、複数のファイルを選択することができます。  

7.  ソリューション エクスプローラーで、[SampleEditor]、[参照] の順に移動します。  

8.  参照に警告やエラーがないことを確認します。  

9. ソリューション エクスプローラーで、SampleEditor プロジェクトを右クリックして、**[プロパティ]** をクリックします。  

     **[SampleEditor プロパティ ページ]** ダイアログ ボックスが表示されます。  

10. **[SampleEditor プロパティ ページ]** ダイアログ ボックスで、**[デバッグ]** タブをクリックします。  

11. **[デバッグ]** タブで、**[外部プログラムの開始]** をクリックします。  

12. **[外部プログラムの開始]** で、***installation_folder\Bin\UDIDesigner.exe*** (ここで *installation_folder* は MDT をインストールしたフォルダー) を入力し、**[OK]** をクリックします。  

    > [!TIP]
    >  省略記号 (...) ボタンをクリックしてフォルダーを参照し、UDIDesigner.exe を選択することもできます。  

13. **[ファイル]** メニューから **[すべて保存]** をクリックします。  

14. *local_folder*\SDK\SamplePage\SamplePage.dll.config ファイルを *installation_folder*\Bin\Config フォルダーにコピーします (ここで *local_folder* は構成プロセスで以前に開発用コンピューター上に作成したフォルダーで、*installation_folder* は MDT をインストールしたフォルダーです)。  

15. Visual Studio 2010 で **[デバッグ]** メニューから **[デバッグの開始]** をクリックします。  

     UDI ウィザード デザイナーが起動します。  

16. UDI ウィザード デザイナーのリボンで、**[開く]** をクリックします。  

     **[開く]** ダイアログ ボックスが表示されます。  

17. **[開く]** ダイアログ ボックスで、*local_folder*\SDK\SamplePage\SamplePage\Config.xml ファイルを開きます (ここで *local_folder* は構成プロセスで以前に開発用コンピューター上に作成したフォルダーです)。  

     Config.xml ファイルが開き、詳細ウィンドウにカスタム [StageGroup](#StageGroup) が表示されます。  

18. 詳細ウィンドウで、**[構成]** タブをクリックします。  

19. **[場所]** ボックスの構成情報で以下を確認します。  

    -   **[ロック解除]** ボタン: **[場所]** ボックスを有効または無効にするのに使用します  

    -   **[既定値]** ボックス: **[場所]** ボックスに表示される既定値を入力します  

    -   **[Friendly display name visible in summary page]\([概要] ページに表示する表示名\)**: **[概要]** ページに表示される情報のキャプションを入力します  

    -   **[場所]** リスト ボックス: 可能な場所の一覧が含まれます  

20. UDI ウィザード デザイナーを閉じます。  

21. Visual Studio 2010 を閉じます。  

## <a name="reviewing-the-udi-sdk-examples"></a>UDI SDK の例を確認する  
 開発を開始する前に、UDI SDK で提供されている例を確認します。 独自の UDI カスタム ウィザード ページとウィザード ページ エディターを作成するために、このガイドの情報と例のソース コードを使用します。  

 以下を確認することで、UDI SDK の例を検討します。  

-   「[SDK のフォルダーの内容を確認する](#ReviewContentsofSDKFolder)」に記載されている、インストール プロセスで以前にコピーした SDK のフォルダーの内容  

-   「[SamplePage Visual Studio ソリューションを確認する](#ReviewSamplePageVisualStudioSolution)」に記載されている、カスタム UDI ウィザード ページの例  

-   「[SampleEditor Visual Studio ソリューションを確認する](#ReviewSampleEditorVisualStudioSolution)」に記載されている、カスタム UDI ウィザード ページ エディターの例  

###  <a name="ReviewContentsofSDKFolder"></a> SDK のフォルダーの内容を確認する  
 UDI 開発環境の構成時に、MDT をインストールしたフォルダーから作成した別のフォルダーに SDK フォルダーをコピーしました。 表 1 に、SDK フォルダー直下のフォルダーとそれぞれの簡単な説明を一覧表示しています。  

### <a name="table-1-folders-in-the-udi-sdk"></a>表 1 UDI SDK 内のフォルダー  

|**フォルダー**|**フォルダーの内容**|  
|-|-|  
|Includes|UDI ウィザードのカスタム ウィザード ページの作成に必要な C++ ヘッダー ファイル|  
|Libs|カスタム ページにリンクされる C++ ライブラリ ファイル。32 ビットと 64 ビット バージョンのスタティック リンク ライブラリがあります。 **注:** Itanium バージョンのライブラリ (IA-64) は使用できません。|  
|SampleEditor|UDI ウィザード デザイナーで、C# で記述されている SamplePage ページを編集するために使用されるカスタム エディターをビルドするための Visual Studio プロジェクト|  
|SamplePage|Visual C++ で記述されているカスタム UDI ウィザード ページをビルドするための Visual Studio プロジェクト|  

###  <a name="ReviewSamplePageVisualStudioSolution"></a> SamplePage Visual Studio ソリューションを確認する  
 独自のカスタム ウィザード ページおよびウィザード ページ エディターの作成を開始する前に、次のタスクを実行して UDI 開発環境を準備します。  

-   「[ウィザード ページのライフ サイクルを確認する](#ReviewWizardPageLifeCycle)」の説明に従って、UDI ウィザード ページのライフ サイクルのステージを確認します。  

-   「[SamplePage の例を確認する](#ReviewSamplePageExample)」の説明に従って、UDI SDK 内の SamplePage の例に対する Visual Studio ソリューションを確認します。  

####  <a name="ReviewWizardPageLifeCycle"></a> ウィザード ページのライフ サイクルを確認する  
 UDI ウィザード ページには、ページのライフ サイクルの各ステージ (フェーズ) に対応するメソッドがあります。 独自のカスタム ウィザード ページ作成の一環として、コードでこれらのメソッドをオーバーライドする必要があります。 表 2 に、オーバーライドする必要があるメソッドと、ウィザード ページのライフ サイクルでメソッドを使用するタイミングなど、各メソッドの簡単な説明を一覧表示します。  

### <a name="table-2-methods-in-a-wizard-page-life-cycle"></a>表 2 ウィザード ページのライフ サイクルのメソッド  

|**方法**|**説明**|  
|-|-|  
|**OnWindowCreated**|このメソッドは、ページのウィンドウが作成された後に 1 回呼び出されます。<br /><br /> このメソッドには、最初にページを初期化し、1 回だけ実行される必要があるコードを記述します。 たとえば、このメソッドを使用して、フィールドを初期化したり、UDI ウィザードの構成ファイル内の **Setter** 要素から構成情報を読み取ります。|  
|**OnWindowShown**|このメソッドは、UDI ウィザードでページが表示されるたびに呼び出されます。 初めてページが表示されるときと、ウィザードで **[次へ]** または **[戻る]** をクリックしてページを移動するたびに呼び出されます。<br /><br /> このメソッドには、表示するページを準備するコードを記述します。たとえば、メモリ変数、タスク シーケンス変数、または環境変数を読み取り、それらの変数への変更に基づいてページを更新します。|  
|**OnCommonControlEvent**|このメソッドは、ウィザード ページが表示され、子 (通常は共通コントロール) から WM_NOTIFY メッセージを受信するたびに呼び出すことができます。<br /><br /> このメソッドには、通知メッセージに基づいて WM_NOTIFY を処理するコードを記述します。 たとえば、**TreeView** コントロールのクリック イベントまたはダブルクリック イベントへの応答など、共通コントロールからのイベントに応答することができます。|  
|**OnUnhandledEvent**|このメソッドは、ウィザード ページに未処理のウィンドウ メッセージが発生するたびに呼び出されます。 このメソッドは、これらの未処理のウィンドウ メッセージをインターセプトして処理する機会を提供します。<br /><br /> このメソッドには、ウィザード ページに関連するウィンドウ メッセージを処理するコードを記述します。 通常、このメソッドはオーバーライドする必要はありません。|  
|**OnNextClicked**|このメソッドは、ウィザードで **[次へ]** をクリックすると呼び出されます。<br /><br /> このメソッドには、次のウィザード ページに移動する前に必要なアクション (時間がかかる検証の実行など) を実行するコードを記述します。 検証に失敗した場合、**Next** 要求を取り消して、メッセージを表示することができます。|  
|**OnWindowHidden**|このメソッドは、前または次のウィザード ページが表示され、ページが非表示になるたびに呼び出されます。<br /><br /> このメソッドには、別のページが表示される前に、ページが非表示になる前のすべてのアクションを実行するコードを記述します。 通常、このメソッドはオーバーライドする必要はありません。|  

####  <a name="ReviewSamplePageExample"></a> SamplePage の例を確認する  
 SamplePage の例のウィザード ページのライフ サイクル中の一連のイベントを表す次のリストを使用して、SamplePage の例を確認します。  

1.  「[手順 1: UDI ウィザード (OSDSetupWizard.exe) で Config.xml ファイルを読み取る](#UDIWizardReadstheConfigFile)」で説明されているように、UDI ウィザード (OSDSetupWizard.exe) は、例の UDI ウィザードの構成ファイル (Config.xml ファイル) から構成情報を読み取ります。  

2.  「[手順 2: UDI ウィザードでカスタム ウィザード ページの DLL を読み込む](#UDIWizardLoadstheDLLforCustomWizardPage)」で説明されているように、UDI ウィザードは、UDI ウィザードの構成ファイルに一覧表示されている各ウィザード ページに必要な DLL を読み込みます。  

3.  「[手順 3: UDI ウィザードでカスタム ウィザード ページを表示する](#UDIWizardDisplaysCustomWizardPage)」で説明されているように、UDI ウィザードはカスタム ウィザード ページを表示し、目的のコントロールの対話を許可します。  

4.  「[手順 4: カスタム ウィザード ページで [次へ] ボタンがクリックされる](#TheNextButtonisClickedinCustomWizardPage)」で説明されているように、カスタム ウィザード ページが情報を収集するときに、**[次へ]** をクリックして次のウィザードを続行する前に必要なタスクを実行します。  

#####  <a name="UDIWizardReadstheConfigFile"></a> 手順 1: UDI ウィザード (OSDSetupWizard.exe) で Config.xml ファイルを読み取る  
 UDI ウィザード (OSDSetupWizard.exe) は起動するときに、既定で UDI ウィザードの構成ファイルを読み取ります。これは UDI ウィザードのプライマリ構成ファイル UDIWizard_Config.xml ファイルです。  

> [!NOTE]
>  この例では、構成ファイルとして Config.xml ファイルを使用しています。 MDT では、既定の構成ファイルは UDIWizard_Config.xml ファイルです。このファイルは、構成の MDT ファイル パッケージ内の Scripts フォルダー内にあります。  

 UDI ウィザードのタスク シーケンス ステップを **/definition** パラメーターを使用するように変更することで、UDI ウィザードが使用する既定の構成ファイルを上書きできます。 UDI ウィザードが使用する既定の構成ファイルを上書きする方法の詳細については、「Override the Configuration File That the UDI Wizard Uses」(UDI ウィザードが使用する構成ファイルを上書きする) を参照してください。  

 Config.xml ファイル内の最上位要素は次のとおりです。  

-   [DLLs](#DLLs) 要素  

-   [Style](#Style) 要素  

-   [Pages](#Pages) 要素  

-   [StageGroups](#StageGroups) 要素  

 UDI ウィザードの構成ファイルのスキーマとこれらの各要素の詳細については、「[UDI ウィザードの構成ファイル スキーマ リファレンス](#UDIWizardConfigurationFileSchemaReference)」を参照してください。  

 UDI ウィザードは **DLL** 要素をスキャンして読み込む .dll ファイルを検索します。 この例では、SamplePage.dll と SharedPages.dll の 2 つの .dll ファイルが一覧表示されます。 これらの .dll ファイルは、OSDSetupWizard.exe と同じ Tools\\*platform* フォルダー内にある必要があります (ここで *platform* は 32 ビット バージョンの場合は x86 または 64 ビット バージョンの場合は x64 です)。  

 UDI ウィザードをスキャンして、**Pages** 要素が定義されているページを検索します。 例では、**Custom** と **SummaryPage** の 2 つのページが定義されています。 **Page** 要素の **Type** 属性は、PageClassIDs.h ファイルで定義され、カスタム ページの型を一意に定義します。  

 例では、定義済みの型は **Microsoft.SamplePage.LocationPage** です。 カスタム ページには、今後作成する可能性がある他のページとの潜在的な競合を回避するため、以下を置き換えます。  

-   **Microsoft** を自分の組織名に置き換える。  

-   **SamplePage** を自分のプロジェクト名に置き換える。  

-   **LocationPage** を自分のカスタム ウィザード ページ名に置き換える。  

#####  <a name="UDIWizardLoadstheDLLforCustomWizardPage"></a> 手順 2: UDI ウィザードでカスタム ウィザード ページの DLL を読み込む  
 UDI ウィザードは DLL を読み込むときに、.dll ファイルに実装する必要がある **RegisterFactories** 関数を呼び出します。 例では、この関数は dllmain.ccp ファイルに実装されます。 作成するウィザードの各ページで、**RegisterFactories** 関数を実装する必要があります。  

 **RegisterFactories** 関数は、ウィザード ページのファクトリ クラスを UDI ウィザードのクラス ファクトリ レジストリに登録するために使用されます。 *クラス ファクトリ*は、別のクラスのインスタンスを作成できるクラスです。 **RegisterFactories** 関数は、ファクトリ クラスの新しいインスタンスを作成し、そのクラスを UDI ウィザードのクラス ファクトリ レジストリに渡すことで、ウィザードでそのファクトリ クラスを使用できるようにします。 UDI ウィザードは、カスタム ウィザード ページの **Page** 要素の **Type** 属性と一致する ID で登録されているファクトリ クラスを探します。  

 例では、ID は、**Microsoft.SamplePage.LocationPage** として PageClassIds.h ファイル内の **ID_Location** として定義されています。これは、Config.xml ファイル内の **Page** 要素の **Type** 属性と一致します。 **ID_Location** は dllmain.ccp ファイルに実装されている **RegisterFactories** 関数内のパラメーターとして渡されます。  

 Register_*name* 関数テンプレートを使用して関数を作成することで、新しいファクトリ インスタンスの作成と、新しく作成されたインスタンスの登録を簡素化することができます。 登録関数テンプレートを使用して指定された **name** 値には、**iClassFactory** インターフェイスを実装する必要があります。 [ClassFactoryImpl クラス](#ClassFactoryImplClass)は、クラス ファクトリの実装の詳細のほとんどを処理します。  

 **RegisterFactories** 関数を使用して、タスクの型と検証コントロールの型を登録することもできます。 詳細については、次をご覧ください。  

-   [カスタム UDI タスクの作成](#CreatingCustomUDITasks)  

-   [カスタム UDI 検証コントロールの作成](#CreatingCustomUDIValidators)  

> [!NOTE]
>  例には、1 つのカスタム ウィザードのページのみが含まれており、これを登録します。 例には、カスタム タスクまたは検証コントロールは含まれていないため、どのカスタム タスクまたは検証コントロールも登録されません。  

#####  <a name="UDIWizardDisplaysCustomWizardPage"></a> 手順 3: UDI ウィザードでカスタム ウィザード ページを表示する  
 例のカスタム ウィザード ページは、LocationPage.cpp ファイルで定義されます。 ウィザード ページは、ページが持つ機能のほとんどを提供するテンプレート クラスから派生されます。 すべてのウィザード ページは、[IWizardPage インターフェイス](#IWizardPageInterface) を実装する [WizardPageImpl Template クラス](#WizardPageImplTemplateClass)から派生する必要があります。 ウィザードの各ページには、ページのニーズに基づいて、他の省略可能なテンプレート クラスと対応するインターフェイスを実装できます。  

 [WizardPageImpl テンプレート クラス](#WizardPageImplTemplateClass)には、カスタム ウィザード ページを記述するのに役立ついくつかの便利なインターフェイスがあります。 [WizardPageImpl テンプレート クラス](#WizardPageImplTemplateClass)をカスタム ウィザード ページの基底クラスとして実装します。  

 使用可能なリスト:  

-   ウィザード ページのテンプレート クラス (「[ウィザード ページ ヘルパー クラス](#WizardPageHelperClasses)」を参照)  

-   ウィザード ページ テンプレート クラスのインターフェイス (「[ウィザード ページ インターフェイス](#WizardPageInterfaces)」を参照)  

 例のカスタム ウィザード ページは、[WizardPageImpl テンプレート クラス](#WizardPageImplTemplateClass)から派生され、[IWizardPage インターフェイス](#IWizardPageInterface)を実装します。 さらに、カスタム ウィザード ページは **IFieldCallback** インターフェイスを実装します。 これらはどちらも LocationPage.cpp ファイルに実装されます。  

 例のカスタム ウィザード ページは、次のメソッドをオーバーライドします。  

-   **OnWindowCreated**。 例のウィザード ページの **OnWindowCreated** メソッドは、次のメソッドを呼び出します。  

    -   [AddField](#AddField)。 このメソッドは、**IDD_LOCATION_PAGE** リソース内の **IDC_COMBO_LOCATION** ボックス コントロールと、Config.xml ファイル内の **Location** という名前の [Data](#Data) 要素を関連付けます。  

         **AddField** メソッドに加え、[AddRadioGroup](#AddRadioGroup) メソッドと [AddToGroup](#AddToGroup) メソッドを使用して、他のコントロールや動作をサポートすることもできます。  

        > [!NOTE]
        >  [InitFields](#InitFields) メソッドを呼び出す前に、必ず [AddField](#AddField)、[AddRadioGroup](#AddRadioGroup)、または [AddToGroup](#AddToGroup) のいずれかのメソッドを呼び出します。  

    -   [InitFields](#InitFields)。 フォームに追加したフィールド (コントロール) を初期化するには、このメソッドを使用します。 ページのポインターはパラメーターです。 例では、現在のページを参照する **this** ポインターが渡されています。  

        > [!NOTE]
        >  **this** ポインターの使用をサポートするには、[WizardPageImpl テンプレート クラス](#WizardPageImplTemplateClass)がサポートしているインターフェイスに加え、**IFieldCallback** インターフェイスを実装する必要があります。  

         **IFieldCallback** インターフェイスは、**SetFieldDefault** メソッドを呼び出します。このメソッドは、テキスト ボックスとチェック ボックスのコントロール以外のコントロールの既定値を設定するために使用されます。 例では、**SetFieldDefault** メソッドが、Config.xml ファイル内の [Field](#Field) 要素の **Default** 要素で指定された既定値に基づいて、コンボ ボックス コントロールの初期インデックスを設定します。  

     **OnWindowCreated** メソッドは、[IFormController インターフェイス](#IFormController-Interface)を使用してフォーム コントローラーを設定します。 フォーム コントローラーの設定に関する詳細については、「[フォームの設定](#SettingUptheForm)」を参照してください。  

-   **InitLocations**。 このメソッドは、Config.xml ファイル内の場所のリストからコンボ ボックスを設定します。 Confg.xml ファイル内の [Data](#Data) 要素と子 [DataItem](#DataItem) 要素により使用可能な値のリストが提供されます。  

-   **OnNextClicked**。 このメソッドは、次のタスクを実行します。  

    -   **SaveFields** メソッドを使用して、コンボ ボックスで選択した値で **TSLocation** タスク シーケンス変数を更新する  

    -   **SaveFields** メソッドを使用して、**[概要]** ページに表示される情報を追加する  

#####  <a name="TheNextButtonisClickedinCustomWizardPage"></a> 手順 4: カスタム ウィザード ページで [次へ] ボタンがクリックされる  
 ユーザーがカスタム ウィザード ページのフィールドへの入力を完了し、**[次へ]** をクリックしたときに、**OnNextClicked** メソッドが呼び出されます。 **OnNextClicked** メソッドは、次のウィザード ページに進む前に、カスタム ウィザード ページで行った構成の変更の記録など、必要なすべてのタスクを実行します。  

 例のカスタム ウィザード ページでは、**OnNextClicked** メソッドのオーバーライドが LocationPage.ccp ファイルに実装されます。 例のカスタム ウィザード ページの **OnNextClicked** メソッドでは、次のメソッドが呼び出されます。  

1.  [InitSection](#InitSection)。 このメソッドは、**[概要]** ページに表示される概要データのヘッダー (ラベル キャプション) を初期化します。 通常、この値は **DisplayName()** 関数を使用して設定できます。 このキャプションに関連付けられているデータは、[SaveFields](#SaveFields) メソッドを使用して保存されます。  

2.  [SaveFields](#SaveFields)。 このメソッドは、フィールド値をタスク シーケンス変数と **[概要]** ページに表示されるデータに保存します。  

###  <a name="ReviewSampleEditorVisualStudioSolution"></a> SampleEditor Visual Studio ソリューションを確認する  
 独自のカスタム ウィザード ページおよびウィザード ページ エディターの作成を開始する前に、次の手順を実行して UDI 開発環境を準備します。  

-   「[UDI ウィザード デザイナー アーキテクチャを確認する](#ReviewUDIWizardDesignerArchitecture)」の説明に従って、UDI ウィザード デザイナーのアーキテクチャを確認します。  

-   「[UDI ウィザード ページの構成可能なコンポーネントを確認する](#ReviewConfigurableComponentsofUDIWizardPage)」の説明に従って、UDI ウィザードの構成ファイルを使用してカスタマイズできる UDI ウィザード ページのコンポーネントを確認します。  

-   「[EditorPage の例を確認する](#ReviewEditorPageExample)」の説明に従って、UDI SDK で提供される EditorPage の例を確認します。  

####  <a name="ReviewUDIWizardDesignerArchitecture"></a> UDI ウィザード デザイナー アーキテクチャを確認する  
 UDI ウィザード デザイナーは、WPF、Prism、Unity を使用して開発されました。 UDI デザイナーは、UDI ウィザード (OSDSetupWizard.exe) が実行時に読み取る UDI ウィザードの構成ファイル (UDIWizard_Config.xml) を編集するために使用されます。 UDI ウィザードの構成ファイル内の [Pages](#Pages) 要素には、ウィザード ページごとに個別の [Page](#Page) 要素を持つページのリストが含まれています。  

 ウィザード ページの構成設定を編集するときに、UDI ウィザード デザイナーは、ウィザード ページの型に対応するカスタム ページ エディターを読み込みます。 カスタム ウィザード ページ エディターは、WPF ユーザー コントロールとして開発されています。 カスタム ウィザード ページ エディター ページでは、WPF の [Model–View–ViewModel](http://msdn.microsoft.com/magazine/dd419663.aspx) (MVVM) デザイン パターンが使用されます。  

 MVVM デザイン パターンは、提示されたデータからユーザー インターフェイス (UI、プレゼンテーション) を分離するのに役立ちます。 データは、UDI ウィザードの構成ファイル (例では Config.xml ファイル) 内の [Page](#Page) 要素の上のファサードです。これには、[IDataService](#IDataService) インターフェイスの [CurrentPage](#CurrentPage) プロパティを使用してアクセスします。  

 UDI ウィザード デザイナーでは、**DependencyAttribute** を使用して、Unity での依存関係挿入フレームワークに基づいて **DataService** クラスへのアクセスを取得します。 Unity での依存関係挿入フレームワークの詳細については、「[Inject Some Life into Your Applications—Getting to Know the Unity Application Block](http://msdn.microsoft.com/library/ff650806.aspx)」 (アプリケーションに活気を与える—Unity Application Block を理解する) を参照してください。  

####  <a name="ReviewConfigurableComponentsofUDIWizardPage"></a> UDI ウィザード ページの構成可能なコンポーネントを確認する  
 カスタム ウィザード ページを作成するときに、構成設定の一部をコードで設定して、ページをコンパイルした後に変更できないようにします。 ただし、その他の構成設定については、UDI ウィザード デザイナーを使用してこれらの構成設定の変更を許可する必要があります。  

 通常、UDI ウィザード デザイナーを使用して構成する構成設定は、UDI ウィザードの構成ファイル (例では Config.xml ファイル) に保存されます。 ただし、必要に応じて、独自の構成ファイルを別に作成することができます。 別の構成ファイルを使用する 1 つの例は、**アプリケーションの検出**タスクおよび **ApplicationPage** ウィザード ページの型が使用する UDIWizard_Config.xml.app ファイルです。  

 UDI ウィザード デザイナーを使用して管理できる一般的な構成設定のリストを以下に示します。  

-   **Field**にする必要があります。 フィールドを使用して、ユーザーが入力できるようにします。 フィールドは、各フィールドの構成設定が含まれている UDI ウィザードの構成ファイル (UDIWizard_Config.xml) 内の [Field](#Field) 要素として表示されます。 対応するウィザード ページ エディターは、[FieldElementControl](#FieldElementControl) を使用して、フィールドのフィールド構成設定を編集するためのメソッドを提供する必要があります。  

-   **プロパティ**。 セッターは、[Page](#Page) 要素のページ、[Field](#Field) 要素のフィールド、[Data](#Data) 要素または [DataItem](#DataItem) 要素のデータなど、ページ上のエンティティのプロパティの作成に役立ちます。 プロパティは [Setter]() 要素で構成します。 定義するプロパティごとに個別の [Setter]() 要素を追加します。 [SetterControl](#SetterControl) を使用してプロパティを編集し、他のコントロールを使用して [Setter]() 要素を構成します。  

-   **データ**。 データは、ウィザード ページおよびその他のコンポーネントで使用するための情報を格納するために使用されます。 [Data](#Data) 要素または [DataItem](#DataItem) 要素を使用して、ページまたはフィールドのデータを定義できます。 [Data](#Data) 要素または [DataItem](#DataItem) 要素を適切に使用することで、データはフラットでも階層構造でも定義することができます。 SDK の例の Config.xml では、フラットなデータ構造の構築方法が示されています。  

 作成するカスタム ウィザード ページ エディターで、これらの構成設定を管理できる必要があります。  

####  <a name="ReviewEditorPageExample"></a> EditorPage の例を確認する  
 EditorPage の例は、UDI ウィザードの構成ファイル内の **SamplePage** ウィザード ページの構成設定を構成するために使用されます。 EditorPage の例には、次の主要なコンポーネントがあります。  

-   **[場所]** コンボ ボックスの設定を構成するための UI  

-   **[場所]** コンボ ボックスに表示される、使用可能な場所のリストで場所を追加または編集するための UI  

-   UDI ウィザードの構成ファイルから読み込まれ、UDI ウィザードの構成ファイルに保存される構成設定  

-   その他のコンポーネントのサポート コード  

 次の手順を実行して、Visual Studio で EditorPage の例を確認します。  

1.  「[ウィザード ページ エディターの読み込みと初期化を確認する](#ReviewWizardPageEditorLoadingInitialization)」の説明に従って、**SampleEditor** ウィザード ページ エディターが UDI ウィザード デザイナーにどのように読み込まれ、初期化されるかを確認します。  

2.  「[[場所] コンボ ボックスを構成するために使用するユーザー インターフェイスを確認する](#ReviewUserInterfaceUsedtoConfigureLocationComboBox)」の説明に従って、LocationPageEditor.xaml ファイルと LocationPageEditor.xaml.cs ファイル内の **[場所]** コンボ ボックスを編集するために使用する UI を確認します。  

3.  「[使用可能な場所のリストを変更するために使用するユーザー インターフェイスを確認する](#ReviewUserInterfaceUsedtoModifyListofPossibleLocations)」の説明に従って、AddEditLocationView.xaml ファイルと AddEditLocationView.xaml.cs ファイル内のリストに場所を追加または編集するために使用する UI を確認します。  

4.  「[構成情報の管理に使用するコードを確認する](#ReviewCodeUsedtoManageConfigurationInformation)」の説明に従って、UDI ウィザードの構成ファイルに保存された構成情報を管理するために使用するコードを確認します。  

#####  <a name="ReviewWizardPageEditorLoadingInitialization"></a> ウィザード ページ エディターの読み込みと初期化を確認する  
 カスタム ウィザード ページ エディターは、必要に応じて、UDI ウィザード デザイナーによって読み込まれます。 UDI ウィザード デザイナーの構成ファイルは、UDI ウィザード デザイナーの起動時に読み込まれます。 UDI ウィザード デザイナーは、*install_folder*\Bin\Config フォルダー (ここで *install_folder* は MDT のインストール フォルダーの名前) をスキャンして、.config ファイル拡張子を持つファイルを検索します。  

 UDI 開発環境の構成時に、SamplePage.dll.confg ファイルを *install_folder*\Bin\Config フォルダーにコピーしました。 UDI ウィザード デザイナーを起動すると、SamplePage.dll.confg ファイルが検出され、読み込まれます。  

 UDI ウィザード デザイナーでは、SamplePage.dll.confg ファイル内の [Page](#Page) 要素の次の属性を使用して、EditorPage の例を読み込んで初期化します。  

-   **DesignerAssembly**。 この属性は、読み込む DLL の名前を決定します。 この DLL は、UDIDesigner.exe ファイルと同じフォルダー、つまり *install_folder*\Bin フォルダー (ここで *install_folder* は MDT がインストールされているフォルダーの名前) に配置されている必要があります。  

-   **DesignerType**。 この属性は、WPF ユーザー コントロールを含むクラスの Microsoft .NET 型名です。  

-   **種類**。 UDI ウィザードで読み込むカスタム ウィザード ページの型を構成するには、この属性を使用します。 UDI ウィザード デザイナーは、この属性を使用して、UDI ウィザードの構成ファイル内で適切な [Page](#Page) 要素を見つけます。  

-   **Dll**。 UDI ウィザード デザイナーによって作成される UDI ウィザードの構成ファイル内で [DLL](#DLL) 要素を構成するには、この属性の構成を使用します。  

-   **説明**。 ウィザード ページ エディターに関する情報を提供するには、この属性を使用します。 この属性の値は、UDI ウィザード デザイナーの **[新しいページの追加]** ダイアログ ボックスに表示されます。このダイアログ ボックスは、"ページ ライブラリ" にウィザード ページを追加するために使用されます。  

-   **DisplayName**。 UDI ウィザード デザイナーに表示されるカスタム ウィザード ページの名前を指定するには、この属性を使用します。 この属性の値は、UDI ウィザード デザイナーの **[新しいページの追加]** ダイアログ ボックスに表示されます。このダイアログ ボックスは、"ページ ライブラリ" にウィザード ページを追加するために使用されます。  

     例では、**SamplePage** カスタム ウィザード ページの型は、**Microsoft.SamplePage.LocationPage** で、Config.xml ファイルに保存されています。 Config.xml ファイルは、*local_folder*\SDK\SamplePage\SamplePage フォルダーにあります (ここで *local_folder* は構成プロセスで以前に開発用コンピューター上に作成したフォルダーです)。  

#####  <a name="ReviewUserInterfaceUsedtoConfigureLocationComboBox"></a> [場所] コンボ ボックスを構成するために使用するユーザー インターフェイスを確認する  
 ウィザード ページ エディターが読み込まれ初期化されると、**Microsoft.SamplePage.LocationPage** 型のページが編集されるときに、SampleEditor ウィザード ページ エディターが読み込まれます。 ページ エディターの UI は、LocationPageEditor.xaml ファイルに格納されます。  

 **[デザイン]** タブで UI を確認し、**[XAML]** タブでコードを確認する場合、グラフィカルな UI と、Extensible Application Markup Language (XAML) の要素と属性の間のリレーションシップを確認できます。  

 たとえば、XAML で **Controls:FieldElementControl** 要素を確認すると、それが対応する UI のレイアウトにどのように関連付けられるかを確認できます。 [FieldElementControl](#FieldElementControl) コントロールを定義するには、**Controls:FieldElementControl** 要素を使用します。  

 XAML ファイル内の **Binding** パラメーターは、サンプル ページ エディターのフィールドを UDI ウィザードの構成ファイル内の情報にバインドします。 たとえば、次のコードは、**[既定値]** テキスト ボックスを UDI ウィザードの構成ファイル (例では Config.xml) 内の [Default](#Default) 要素に結び付けます。  

```  
<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
```  

 詳細については、「[How to: Make Data Available for Binding in XAML](http://msdn.microsoft.com/library/ms748857.aspx)」 (方法: XAML でデータをバインディングに使用できるようにする) を参照してください。  

 グリッド ビューで使用できる場所のリストを編集するには、XAML で **Views:CollectionTControl.ColumnCollectionView** 要素を使用します。 [CollectionTControl](#CollectionTControl) を使用して、グリッド ビューを表示し、グリッド ビューを UDI 構成ファイル内の **Location** という名前を持つ [Data](#Data) 要素にバインドします。  

#####  <a name="ReviewUserInterfaceUsedtoModifyListofPossibleLocations"></a> 使用可能な場所のリストを変更するために使用するユーザー インターフェイスを確認する  
 使用可能な場所のリストを変更するための UI は、以下で構成されています。  

-   「[場所のリストを変更するためのコンテキスト依存のメニューとリボン ボタンを確認する](#ReviewContextSensitiveMenuandRibbonButtons)」で説明されている、場所のリスト内の項目を追加、削除、または順番を変更することができるコンテキスト依存のメニューとリボン ボタン  

-   「[場所を追加または変更するためのダイアログ ボックスを確認する](#ReviewDialogBoxforAddingEditingLocations)」で説明されている、場所のリスト内の項目を追加または編集するために選択したときに起動されるダイアログ ボックス  

######  <a name="ReviewContextSensitiveMenuandRibbonButtons"></a> 場所のリストを変更するためのコンテキスト依存のメニューとリボン ボタンを確認する  
 場所のリストを含むリスト ボックス内を右クリックすると、コンテキスト メニューが表示されます。 リボンには、同じタスクを実行できる対応するボタンがあります。 LocationPageEditor.xaml ファイル内の **Views:CollectionsTControl** コントロール要素は、実行されるアクションに基づいて呼び出すメソッドと、次のように設定したプロパティを定義します。  

-   **SelectedItem**。 このデータ バインド プロパティは、ユーザーがリストからの項目を選択したときにアクティブ化されます。 このプロパティは、ビュー モデル内の **CurrentLocation** プロパティに関連付けられます。このビュー モデルは LocationPageEditorViewModel.cs ファイル内にあり、既存項目を編集または削除する際に選択した項目を渡すために、[CollectionTControl](#CollectionTControl) コントロールによって使用されます。  

-   **AddItemAction**。 このアクションは、ユーザーがコンテキスト メニューから **[項目の追加]** オプションまたはリボンの対応するボタンをクリックしたときに実行されます。 **AddLocationAction** オブジェクトを返すビュー モデル内のプロパティへのデータ バインディングがあります。 このオブジェクトは **AddLocationCallback** メソッドで、LocationPageEditorViewModel.cs ファイル内に配置され、AddEditLocationView.xaml ファイル内のダイアログ ボックスを表示します。  

-   **EditItemAction**。 このアクションは、ユーザーがコンテキスト メニューから **[項目の編集]** オプションをクリックしたときに実行されます。 **EditLocationAction** オブジェクトを返すビュー モデル内のプロパティへのデータ バインディングがあります。 このオブジェクトは **EditLocationCallback** メソッドで、LocationPageEditorViewModel.cs ファイル内に配置され、AddEditLocationView.xaml ファイル内のダイアログ ボックスを表示します。  

-   **RemoveAction**。 このアクションは、ユーザーがコンテキスト メニューから **[項目の削除]** オプションをクリックしたときに実行されます。 **RemoveAction** オブジェクトを返すビュー モデル内のプロパティへのデータ バインディングがあります。 このオブジェクトは **EditLocationCallback** メソッドで、LocationPageEditorViewModel.cs ファイル内に配置され、場所の削除を確認するメッセージを表示します。  

######  <a name="ReviewDialogBoxforAddingEditingLocations"></a> 場所を追加または変更するためのダイアログ ボックスを確認する  
 場所のリストに新しい場所を追加または既存の場所を編集すると、AddEditLocationView.xaml ファイル内のメッセージが表示されます。 メッセージは、LocationPageEditorViewModel.cs ファイル内の [ShowDialogWindow](#ShowDialogWindow) ウィンドウ メソッドを使用して表示されます。  

 AddEditLocationView.xaml ファイルの UI は以下で構成されます。  

-   **DialogFrame** という名前のダイアログ枠には、次の要素が含まれます。  

    -   タイトル: ダイアログ枠の **DialogTitle** 属性を使用して構成します  

    -   **[OK]** ボタン: **Approved** プロパティのリターン状態を **True** に設定します (ユーザーが **[OK]** をクリックしたかどうかを判断するため、LocationPageEditorViewModel.cs ファイル内の **AddLocationCallback** メソッドでリターン状態がチェックされます)  

    -   **[キャンセル]** ボタン: **Approved** プロパティのリターン状態を **False** に設定します (ユーザーが **[キャンセル]** をクリックしたかどうかを判断するため、LocationPageEditorViewModel.cs ファイル内の **AddLocationCallback** メソッドでリターン状態がチェックされます)  

-   以下を含む WPF 要素:  

    -   ラベル: **Content** 属性を使用して構成します  

    -   テキスト ボックス: UDI 構成ファイル (例では Config.xml ファイル) 内の **Location** という名前の [Data](#Data) 要素にバインドされます  

######  <a name="ReviewCodeUsedtoManageConfigurationInformation"></a> 構成情報の管理に使用するコードを確認する  
 カスタム ウィザード ページの構成情報は、次の UDI ウィザードの構成ファイル内に格納されます。  

-   UDI SDK で提供される例の Config.xml ファイル (このファイルには、例の構成設定のみが含まれています)  

-   MDT で提供される UDIWizard_Config.xml ファイル。このファイルは、*installation_folder*\Templates\Distribution\Scripts folder フォルダー (ここで *installation_folder* は、MDT をインストールしたフォルダー) に格納され、すべての組み込みウィザードのページとステージの構成設定が含まれています  

 SampleEditor の例では、構成情報の管理に役立つ **Locations** ルーチンが LocationPageEditorViewModel.cs ファイルに配置されています。 **Locations** ルーチンは、UDI ウィザードの構成ファイルから場所のリストを返します。 具体的には、返されるリストには、UDI ウィザードの構成ファイル内の [DataItem](#DataItem) 要素ごとに 1 つの項目が含まれます。  

## <a name="creating-custom-udi-wizard-pages"></a>カスタム UDI ウィザード ページの作成  
 カスタム UDI ウィザード ページを作成するための高度なプロセスは次のとおりです。  

1.  開始点として、SamplePage ソリューションのコピーを作成します。  

2.  フォーム上に目的のコントロール (フィールド) を配置します。  

3.  ウィザード ページを読み込む (**OnWindowCreated** メソッドをオーバーライドする) ときに、適切なタスクを実行するためのコードを記述します。これには次の手順が含まれます。  

    1.  フォームを初期化します。  

    2.  メモリ変数、タスク シーケンス変数、環境変数、または XML ファイル情報 (**Setter** プロパティなど) を読み取ります。  

4.  ページを表示する (**OnWindowShown** メソッドをオーバーライドする) ときに、適切なタスクを実行するための任意のコードを記述します。これには次の手順が含まれます。  

    1.  手順 3 で、ページを読み込むときに読み取られた情報に基づいて、コントロールを有効または無効にします。  

    2.  読み取られた情報に基づいたコントロールの設定など、手順 3 でページを読み込むときに読み取られた情報に基づいて、コントロールを更新します。  

5.  ユーザーがウィザード ページと対話するときに、適切なタスクを実行するためのコードを記述します。  

6.  ユーザーが UDI ウィザードで **[次へ]** をクリックする (**OnNextClicked** メソッドをオーバーライドする) ときに、適切なタスクを実行するための任意のコードを記述します。これには次の手順が含まれます。  

    1.  任意のメモリ変数、タスク シーケンス変数、環境変数、または XML ファイル情報を更新します。  

    2.  概要ページの情報を更新します (ページのフィールドによって実行されない場合)。  

7.  ソリューションをビルドします。  

     作成する DLL のバージョンが、MDT のインストールと同じプロセッサ プラットフォーム (具体的には、Windows プレインストール環境 (Windows PE) のプロセッサ プラットフォーム) であることを確認します。 UDI ウィザードは、以下で実行できます。  

    -   **ターゲット コンピューター上の既存のオペレーティング システム**。 32 ビット バージョンのウィザード ページは、32 ビットまたは 64 ビットの Windows オペレーティング システムで実行できます。 ただし、64 ビット バージョンのウィザード ページは、64 ビットの Windows オペレーティング システムでのみ実行できます。  

    -   **ターゲット コンピューター上の Windows PE**。 Windows PE は、64 ビット バージョンの Windows PE で 32 ビット アプリケーションの実行をサポートしていません。 そのため、使用する予定の Windows PE の各プロセッサ アーキテクチャ用にウィザード ページのバージョンをビルドしている必要があります。  

8.  カスタム ウィザード ページの DLL を *installation_folder*\Templates\Distribution\Tools\ プラットフォーム フォルダーにコピーします (ここで *installation_folder* は MDT をインストールしたフォルダーで、*プラットフォーム*は 32 ビット バージョンの場合は **x86** または 64 ビット バージョンの場合は **x64** です)。  

9. カスタム ページ エディターを作成するための手順を完了します。  

## <a name="creating-custom-wizard-page-editors"></a>カスタム ウィザード ページ エディターの作成  
 カスタム UDI ウィザード ページ エディターを作成するための高度なプロセスは次のとおりです。  

1.  開始点として、SampleEditor ソリューションのコピーを作成します。  

2.  .xaml ファイルにプライマリ ページ エディター UI を作成します。  

3.  構成するウィザード ページで必要な [FieldElementControl](#FieldElementControl) コントロールのインスタンスを追加します (必要な場合)。  

4.  構成するウィザード ページで必要な [SetterControl](#SetterControl) コントロールのインスタンスを追加します (必要な場合)。  

5.  構成するウィザード ページで必要な [CollectionTControl](#CollectionTControl) コントロールのインスタンスを追加します (必要な場合)。  

6.  [IDataService](#IDataService) インターフェイスを追加します。  

7.  カスタム ウィザード ページ エディターを使用して、構成する構成設定に基づいて UDI ウィザードの構成ファイルを更新するための適切なコードを記述します。  

8.  .xaml ファイル内に子ダイアログ ボックスを作成し、構成するウィザード ページで必要な [IMessageBoxService](#IMessageBoxService) インターフェイスを使用して、それらをプライマリ ページ エディターから呼び出します。  

9. 構成するウィザード ページの要件に基づいて、UDI ウィザード デザイナーのリボンに適切なインターフェイスを追加します。  

10. ソリューションをビルドします。  

    > [!NOTE]
    >  作成する DLL のバージョンが MDT のインストールと同じプロセッサ プラットフォームであることを確認します。 たとえば、MDT の 64 ビット バージョンをインストールする場合は、カスタム ページ エディターの 64 ビット バージョンをビルドします。  

11. 必要な DLL を読み込む UDI ウィザード デザイナーの構成ファイルを作成し、ウィザード ページ エディターを対応するウィザード ページ (例では SamplePage.dll.config ファイル) にマップします。  

     ウィザード ページとウィザード ページ エディター間のマッピングを実行するために必要な要素の詳細については、[DesignerMappings](#DesignerMappings) 要素、子要素、および対応する属性を参照してください。  

12. 前の手順で作成した UDI ウィザード デザイナーの構成ファイルを、*installation_folder*\Bin\Config フォルダー (ここで *installation_folder* は、MDT のバージョンをインストールしたフォルダー) にコピーします。  

13. カスタム ウィザード ページ エディター用の DLL を *installation_folder*\Bin フォルダー (ここで *installation_folder* は、MDT をインストールしたフォルダー) にコピーします。  

##  <a name="CreatingCustomUDITasks"></a> カスタム UDI タスクの作成  
 *UDI タスク*は、[ITask インターフェイス](#ITaskinterface)を実装する C++ で記述された DLL です。 UDI ウィザード デザイナーの構成ファイル (.config ファイル) を作成し、それを *installation_folder*\Bin\Config フォルダー (ここで *installation_folder* は MDT をインストールしたフォルダー) に配置することで、DLL を UDI ウィザード デザイナーのタスク ライブラリに登録します。  

> [!NOTE]
>  同じ .dll ファイル内にウィザード ページ、タスク、および検証コントロールを含む DLL を作成することができます。 DLL 内のウィザード ページ、タスク、検証コントロールの構成設定を含む単一の UDI ウィザード デザイナーの構成ファイル (.config) を作成することもできます。  

 **カスタム UDI タスクを作成するには**  

1.  [ITask インターフェイス](#ITaskinterface)と次のメソッドを実装するコードを記述します。  

    -   [Init](#Init)。 このメソッドは、タスクを初期化するために呼び出されます。  

    -   [Execute](#Execute)。 このメソッドは、タスクを実行するために呼び出されます。  

2.  カスタム タスク クラス ファクトリをファクトリのレジストリに登録するコードを記述します。  

3.  カスタム タスクのソリューションをビルドします。  

    > [!NOTE]
    >  作成する DLL のバージョンが MDT のインストールと同じプロセッサ プラットフォームであることを確認します。 たとえば、MDT の 64 ビット バージョンをインストールする場合は、カスタム UDI タスクの 64 ビット バージョンをビルドします。  

4.  次の抜粋と同じように、UDI ウィザード デザイナーの構成ファイル内で [TaskLibrary](#TaskLibrary) 要素の下に [Task](#Task) 要素を作成します。  

    ```  
    <Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
       <TaskItem Type="Setter" Name="Status Bitmap">  
          <Param Name="BitmapFilename"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Log File">  
          <Param Name="log"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Write Configuration File">  
          <Param Name="writecfg"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Read Configuration File">  
          <Param Name="readcfg"/>  
       </TaskItem>  
    </Task>  
    ```  

    > [!NOTE]
    >  すべての [Task](#Task) 要素に **BitmapFilename** パラメーターを含める必要があります。 タスクに必要なその他のすべてのパラメーターを指定します。 たとえば、前述の抜粋では、ログ ファイルの場所のパラメーターを指定するために **log** パラメーターが使用されています。  

5.  前の手順で作成した UDI ウィザード デザイナーの構成ファイルを、*installation_folder*\Bin\Config フォルダー (ここで *installation_folder* は MDT をインストールしたフォルダー) にコピーします。  

6.  カスタム タスクの DLL を *installation_folder*\Templates\Distribution\Tools\ プラットフォーム フォルダーにコピーします (ここで *installation_folder* は MDT をインストールしたフォルダーで、*プラットフォーム*は 32 ビット バージョンの場合は **x86** または 64 ビット バージョンの場合は **x64** です)。  

##  <a name="CreatingCustomUDIValidators"></a> カスタム UDI 検証コントロールの作成  
 *UDI 検証コントロール*は、**IValidator** インターフェイスを実装する C++ で記述された DLL です。 UDI ウィザード デザイナーの構成ファイル (.config ファイル) を作成し、それを *installation_folder*\Bin\Config フォルダー (ここで *installation_folder* は MDT をインストールしたフォルダー) に配置することで、DLL を UDI ウィザード デザイナーの検証コントロール ライブラリに登録します。  

 **カスタム UDI 検証コントロールを作成するには**  

1.  **BaseValidator** クラスのサブクラスを作成し、次のメソッドを実装するコードを記述します。  

    -   **Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)**。 フォーム コントローラーは、検証コントロールを初期化するために **Init** メンバーを呼び出します。 このメソッドでは、**BaseValidator** クラスの **Init** メソッドを呼び出す必要があります。 通常、UDI ウィザードの構成ファイルから検証コントロール用に設定されたすべてのプロパティを読み取ります。 たとえば、**InvalidCharactersValidator** 検証コントロールはこのメソッドを使用して、**InvalidChars** プロパティの値を取得します。  

    -   **IsValid**。 フォーム コントローラーは、コントロールに有効なテキストが含まれているかどうかを表示するためにこのメソッドを呼び出します。 フィールドが空でないことを検証する検証コントロールの **IsValid** メソッドの例を次に示します。  

        ```  
        BOOL IsValid(LPBSTR pMessage)  
        {  
            __super::IsValid(pMessage);  

            _bstr_t text;  
            m_pText->GetText(text.GetAddress());  
            return (text.length() > 0);  
        }  
        ```  

    -   **Init(IControl \*pControl, LPCTSTR message)**。 フォーム コントローラーは、キーストロークごとおよびその他のイベントにこのメンバーを呼び出し、検証コントロールが、コントロールのコンテンツを検証し、ウィザード ページの下部でメッセージが更新 (またはクリア) されていることを検証できるようにします。  

     通常、メソッドをオーバーライドする必要があるのは、これらのメソッドだけです。 ただし、検証コントロールによっては、作成する **BaseValidator** クラスのサブクラス内の他のメソッドをオーバーライドする必要があります。 これらの他のメソッドの詳細については、**BaseValidator** クラスを参照してください。  

2.  カスタム タスク クラスをレジストリ ファクトリに登録するコードを記述します。  

3.  カスタム タスクのソリューションをビルドします。  

    > [!NOTE]
    >  作成する DLL のバージョンが MDT のインストールと同じプロセッサ プラットフォームであることを確認します。 たとえば、MDT の 64 ビット バージョンをインストールする場合は、カスタム UDI タスクの 64 ビット バージョンをビルドします。  

4.  次の抜粋と同じように、UDI ウィザード デザイナーの構成ファイル内で **ValidatorLibrary** 要素の下に [Validator](#Validator) 要素を作成します。  

    ```  
    <Validator   
    <Validator DLL="" Description="Must follow a pre-defined pattern" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern">  
       <Param Description="Enter the message you want displayed when the text in this field doesn't match the pattern:" Name="Message" DisplayName="Message"/>  
       <Param Description="The name of a pre-defined regular expression pattern. Must be Username, ComputerName, or Workgroup" Name="NamedPattern" DisplayName="Named Pattern"/>  
    </Validator>  
    ```  

    > [!WARNING]
    >  すべての [Validator](#Validator) 要素には、**Message** パラメーターを含める必要があります。 検証コントロールで必要なその他のすべてのパラメーターを指定します。 たとえば、前述の抜粋では、定義済みの正規表現パターンの名前にパラメーターを指定するために、**NamedPattern** パラメーターが使用されています。  

5.  前の手順で作成した UDI ウィザード デザイナーの構成ファイルを、*installation_folder*\Bin\Config フォルダー (ここで *installation_folder* は MDT をインストールしたフォルダー) にコピーします。  

6.  カスタム タスクの DLL を *installation_folder*\Templates\Distribution\Tools\ プラットフォーム フォルダーにコピーします (ここで *installation_folder* は MDT をインストールしたフォルダーで、*プラットフォーム*は 32 ビット バージョンの場合は **x86** または 64 ビット バージョンの場合は **x64** です)。  

## <a name="udi-wizard-reference"></a>UDI ウィザードのリファレンス  

### <a name="wizard-page-components"></a>ウィザード ページのコンポーネント  
 カスタム ページをビルドするには、あらかじめ作成されている複数のコンポーネントのいずれかを使用できます。  

#### <a name="creating-component-instances"></a>コンポーネントのインスタンスを作成する  
 UDI ウィザードは、クラス ファクトリを使用してオブジェクトの新しいインスタンスを作成します。 これらのファクトリは、文字列をファクトリへのキーとして使用して、ファクトリ レジストリに登録されます。 たとえば、**WmiRepository** コンポーネントは、文字列 "Microsoft.Wizard.WmiRepository" で識別され、IWmiRepository ヘッダー ファイルでは **ID_WmiRepository** として使用できます。  

 ページを **WizardPageImpl** のサブクラスとして記述しているとすると、次のような **WmiRepoistory** の新しいインスタンスを作成できます。  

```  
PWmiRepository pWmi;  
CreateInstance(Container(), ID_WmiRepository, &pWmi);  
```  

 **CreateInstance** 関数は、コンポーネントの新しいインスタンスを作成するためのタイプ セーフ テンプレート関数です。 **PWmiRepository** はスマート ポインターなので、参照カウントが処理されます。  

#### <a name="creatable-components"></a>作成可能なコンポーネント  
 レジストリに登録することができるコンポーネントのセットがあります。 最初のコンポーネントのセットは、メイン UDI ウィザードの実行可能ファイルで提供されているため、常に登録されます。 その他の 2 つのコンポーネントのセットは、"オプション" の DLLs で提供されます。 これらのコンポーネントを使用可能にするには、DLL が .config XML ファイルの **DLLs** セクションに一覧表示される必要があります。 コードで、どの実行可能ファイルに特定のコンポーネントが含まれているかを認識する必要はありません。  

 (OSDSetupWizard で定義された) ファクトリ レジストリに登録されたコンポーネントのコンポーネント ID のリスト (コンポーネント名は ID と同じですが、先頭に *ID_* が付きません) を表 3 に示します。  

### <a name="table-3-component-ids"></a>表 3 コンポーネント ID  

|**ID**|**説明**|  
|-|-|  
|ID_ACPowerTask|(ITask、IWizardComponent) ご利用のコンピューターがバッテリのみで実行されていないことを確認するプレフライト タスク|  
|ID_AppDiscoveryTask|(ITask、IWizardComponent) ご利用のコンピューターにインストールされているソフトウェア アイテムを検出するための特殊なタスク|  
|**ID_BackgroundTask**|(**IBackgroundTask**、**IWizardComponent**) 別のスレッドでタスクを実行するために使用できます|  
|**ID_CopyFilesTask**|(**ITask**、**IWizardComponent**) 1 つ以上のファイルをコピーするタスク|  
|**ID_FormController**|(**IFormController**) ページが独自のインスタンスを受け取るため、自分でインスタンスを作成する必要はほとんどありません|  
|**ID_InvalidCharactersValidator**|(**IValidator**) 検証コントロールに提供されるリストからの文字がテキスト フィールドに含まれないようにします|  
|**ID_Logger**|(**ILogger**) ページが共有インスタンスへのポインターを受け取るため、自分でインスタンスを作成する必要はほとんどありません|  
|**ID_NonEmptyValidator**|(**IValidator**) 空のフィールドがないことを確認する検証コントロール|  
|**ID_PasswordValidator**|(**IValidator**) 同じコンテンツを持つ 2 つのテキスト フィールドがないことを確認する検証コントロール|  
|**ID_Regex**|(**IRegEx**) 一致を検索する正規表現を評価します|  
|**ID_RegExValidator**|(**IValidator**) 正規表現または既知のパターンに対して検証する検証コントロール|  
|**ID_SimpleStringProperties**|(**IStringProperties**、**ISimpleStringProperties**) XML を使用せずに、タスクにプロパティを送信する簡単な方法を提供します|  
|**ID_ShellExecuteTask**|(**ITask**、**IWizardComponent**) 外部プログラムを実行します|  
|**ID_SummaryBag**|(**ISummaryBag**) Form メソッドを使用して、ページから間接的に利用できます|  
|**ID_TaskManager**|(**ITaskManager**、**IBackgroundCallback**、**IWizardComponent**) 一連のタスクと UI の実行を管理します|  
|**ID_WmiRepository**|(**IWmiRepository**、**IWizardComponent**) Windows Management Instrumentation (WMI) クエリを実行できます|  
|**ID_IXmlDocument**|(**IXmlDocument**) XML ドキュメントの読み取りと書き込みのためのファサードを提供します|  

 表 4 と表 5 に、定義済みの OSDRefreshWizard.dll、共有ページ、およびその他のコントロール コンポーネントを示します。  

### <a name="table-4-directory-controls"></a>表 4 ディレクトリ制御  

|**ID**|**説明**|  
|-|-|  
|**ID_Directory**|(**IDirectory**) ファイル システムからディレクトリ情報を取得するためのファサード|  

### <a name="table-5-defined-sharedpagesdll"></a>表 5 定義済み SharedPages.dll  

|**ID**|**説明**|  
|-|-|  
|**ID_ADHelper**|(**IADHelper**) Active Directory® ドメイン サービス (AD DS) で限定的な機能セットのファサードを提供します|  
|**ID_CpuInfo**|(**ICpuInfo**) CPU が 32 ビットまたは 64 ビットかどうかを判断します|  
|**ID_DomainJoinValidator**|(**IDomainJoinValidator**) 資格情報のセットがドメインに参加することが許可されているかどうかをチェックするためのいくつかのメソッドがあります|  
|**ID_DriveList**|(**IDriveList**、**IBindableList**、**IWizardComponent**) WMI を使用して、コンピューター上のドライブのリストを取得します|  
|**ID_WiredNetworkTask**|(**ITask**) (ワイヤレスではなく) 有線ネットワーク アダプターを使用してネットワークに接続しているかどうかをチェックするタスク|  

#### <a name="control-components"></a>コントロール コンポーネント  
 **GetControlWrapper** テンプレート関数を介して、ページ上のコントロールとやり取りします。この関数は、表 6 に一覧表示されているいずれかのコンポーネントの型へのアクセスを提供します。  

### <a name="table-6-components"></a>表 6 コンポーネント  

|**ダイアログ コントロール型**|**説明**|  
|-|-|  
|**CONTROL_CHECK_BOX**|(**ICheckBox**) チェック ボックス コントロールを操作するためのファサード|  
|**CONTROL_COMBO_BOX**|(**IComboBox**) コンボ ボックス コントロールのファサード|  
|**CONTROL_GENERIC**|(**IControl**) 有効化と表示状態をコントロールするため、ほとんどのコントロールの型を使用できるようにする|  
|**CONTROL_LIST_VIEW**|(**IListView**) リスト ビュー コントロールの機能へのアクセスを提供するファサード|  
|**CONTROL_PROGRESS_BAR**|(**IProgressBar**) 進行状況バー コントロールの位置を操作するためのファサード|  
|**CONTROL_RADIO_BUTTON**|(**IRadioButton**) ラジオ ボタン コントロールを操作するためのファサード|  
|**CONTROL_STATIC_TEXT**|(**IStaticText**) ラベルやテキスト ボックスなどのコントロールのテキストに読み取り/書き込みアクセス許可を提供するファサード|  
|**CONTROL_TREE_VIEW**|(**ItreeView**) ツリー ビュー コントロールを操作するためのファサード|  

#### <a name="image-list-component"></a>イメージ リスト コンポーネント  
 このコンポーネントは、ページ上の **ImageList** コントロールのファサードです。 イメージ リストは、**IListView** または **ITreeView** インターフェイスを使用して作成します。  

#### <a name="formcontroller-component"></a>FormController コンポーネント  
 このコンポーネントはウィザードによって作成され、ページに渡されます。 このコンポーネントには、**WizardPageImpl** 基底クラスが実装する **Form** メソッドを使用して、ページからアクセスします。  

#### <a name="invalidcharactervalidator-component"></a>InvalidCharacterValidator コンポーネント  
 これはページに含めることができる検証コントロールの型です。 この ID は、"Microsoft.Wizard.Validation.InvalidChars" のテキスト値を持つ **ID_InvalidCharactersValidator** (IValidator.h で定義済み) です。  

 この検証コントロールは、許可されていない文字のリストである **InvalidChars** と呼ばれる 1 つのプロパティ (.config ファイル内の **Setter** 要素) を検索します。 これはテキスト ボックス内の文字をチェックします。テキストにこのリストからの文字が含まれていると、コンポーネントはエラーを報告します。  

#### <a name="nonemptyvalidator-component"></a>NonEmptyValidator コンポーネント  
 これはページに含めることができる検証コントロールの型です。 この ID は、"Microsoft.Wizard.Validation.NonEmpty" のテキスト値を持つ **ID_NonEmptyValidator** (IValidator.h で定義済み) です。  

 テキスト ボックス (または **IStaticText** をサポートするその他のコントロール) に空の文字列値があると、この検証コントロールはエラーを報告します。  

#### <a name="passwordvalidator-component"></a>PasswordValidator コンポーネント  
 これはページに含めることができる検証コントロールの型です。 この ID は、"Microsoft.Wizard.Validation.Password" のテキスト値を持つ **ID_PasswordValidator** (IValidator.h で定義済み) です。  

 この検証コントロールは、2 つの異なるテキスト コントロール (**IStaticText** をサポートするコントロール) を使用して、これらに同じ値が含まれていない場合に、エラーを報告します。 つまり、**[パスワード]** と **[パスワードの確認]** のテキスト ボックスが一致しない場合には失敗します。  

 この検証コントロールでは、2 つのコントロールを必要とするため、他の検証コントロールよりも多くの設定が必要です。 設定は、次のようになります。  

```  
Form()->AddToGroup(IDC_EDIT_PASSWORD, IDC_EDIT_PASSWORD2);  
PValidator pValidator;  
Form()->AddValidator(IDC_EDIT_PASSWORD, ID_PasswordValidator, pMessage, &pValidator);  
PStaticText pPassword2;  
GetControlWrapper(View(), IDC_EDIT_PASSWORD2, CONTROL_STATIC_TEXT, &pPassword2);  
pValidator->SetProperty(0, pPassword2);  
```  

 最初に、**Confirm Password** コントロールを **Password** コントロールの "子" として定義します。 つまり、フォーム コントローラーで **Password** コントロールが無効にされた場合は、**Confirm Password** コントロールも無効にされます。 次に、パスワードの検証コントロールをフォームに追加します。 最後に、パスワード検証コントロールに **Confirm Password** コントロールへのインターフェイスを提供します。  

 2 つのコントロールの要件のため、この検証コントロールの設定には、.config XML ファイルではなく、コードを使用する必要があります。  

#### <a name="regexvalidator-component"></a>RegExValidator コンポーネント  
 これはページに含めることができる検証コントロールの型です。 この ID は、"Microsoft.Wizard.Validation.RegEx" のテキスト値を持つ **ID_RegExValidator** (IValidator.h で定義済み) です。  

 この検証コントロールは、(**IStaticText** をサポートしている) テキスト コントロールのコンテンツを正規表現と比較し、テキストが正規表現と一致しない場合は失敗します。  

 または、定義済みの名前付きパターンでこの検証コントロールを使用することができます。 正規表現を使用するには、XML に **Pattern** と呼ばれるセッター プロパティが含まれている必要があります。 代わりに名前付きのパターンを使用する場合は、表 7 の値のいずれかに設定された **NamedPattern** と呼ばれるセッターを使用します。  

### <a name="table-7-named-pattern-setters"></a>表 7 名前付きパターン セッター  

|**Pattern**|**説明**|  
|-|-|  
|ユーザー名|テキストがフォーム ドメイン\ユーザーまたは user@domain のいずれかであるかを確認します|  
|ComputerName|名前は 1 から 15 文字の長さである必要があり、(: や ? などの) 文字セットを含めることはできません|  
|ワークグループ|名前は 1 から 15 文字の長さである必要があり、文字セット (=、+、? など) を含めることはできません|  

#### <a name="factoryregistry-component"></a>FactoryRegistry コンポーネント  
 このコンポーネントは、すべてのクラス ファクトリとサービスを記録します。 **IFactoryRegistry** インターフェイスを実装し、ページの **Container** メソッドを通じて間接的に使用できます。 さらに、レジストリは拡張 DLL を読み込みます。 DLL を読み込むと、レジストリは **RegisterFactories** と呼ばれるエクスポートされた関数を探します。 この関数を実装し、その中でページ、タスク、および検証ツールのクラス ファクトリ (および登録するその他のクラス ファクトリ) を登録する必要があります。 サンプル プロジェクトからの例を次に示します。  

```  
extern "C" __declspec(dllexport) void RegisterFactories(IFactoryRegistry *factories)  
{  
Register<LocationPageFactory>(ID_LocationPage, factories);  
}  
```  

#### <a name="logger-component"></a>Logger コンポーネント  
 このコンポーネントは、(**WizardPageImpl** で実装される) **Logger** メソッドを使用してページで使用することができます。 ログ ファイルにエントリを書き込むには、このメソッドを使用します。 ログ ファイルのコンテンツは、UDI ウィザードの実行で発生する可能性がある問題の診断に役立ちます。  

#### <a name="propertybag-component"></a>PropertyBag コンポーネント  
 *property bag* は、メモリ変数のコンテナーです。 **Container()->Properties()** を使用して、自分のページから使用できます。 メモリ変数は、異なるページ間で一時データを渡すのに役立ちます。  

#### <a name="tsvariablebag-and-tsrepository-components"></a>TSVariableBag コンポーネントと TSRepository コンポーネント  
 **TSVariableBag** コンポーネントを使用すると、タスク シーケンス変数を読み書きすることができます。 これはユーザーが **[完了]** をクリック (既定) するまで、メモリに値を保持します。 **TSVariable** バッグには、ページの **TSVariables** メソッド (**WizardPageImpl** 基底クラスで実装される) を介してアクセスできます。 これらのコンポーネントは、すべての読み取りと書き込みのタスク シーケンス変数をログに記録します。  

#### <a name="wmirepository-component"></a>WmiRepository コンポーネント  
 このコンポーネントは、WMI クエリを操作するためのファサードを提供します。 **ID_WmiRepository** を使用して、**CreateInstance** ヘルパー関数を呼び出して、**IWmiRepository** インターフェイスをサポートするこのコンポーネントのインスタンスを取得できます。 このコンポーネントは、**IWmiIterator** インターフェイスを介して結果のレコードを返します。  

###  <a name="WizardPageHelperClasses"></a> ウィザード ページ ヘルパー クラス  
 UDI SDK で提供されている組み込みのヘルパー クラスを使用して、カスタム UDI ウィザード ページを作成することができます。 表 8 に、カスタム ウィザード ページの作成に使用できるヘルパー クラスを示します。  

### <a name="table-8-helper-classes"></a>表 8 ヘルパー クラス  

|**ヘルパー クラス**|**説明**|  
|-|-|  
|[ClassFactoryImpl クラス](#ClassFactoryImplClass)|これは、作成後にファクトリ レジストリに登録できるクラス ファクトリを作成するのに役立つ基底クラスです。|  
|[インターフェイス テンプレート クラス](#InterfaceTemplateClass)|複数のインターフェイスを実装するコンポーネントをビルドする場合に、このテンプレート クラスを使用します。|  
|[パス ヘルパー クラス](#PathHelperClass)|このクラスは、一般的なファイル操作またはディレクトリ操作を提供します。|  
|[Pointer テンプレート クラス](#PointerTemplateClass)|このクラスは、COM コンポーネントでの有効期間の管理に対して参照カウントを提供します。 インターフェイスでの操作が終わったら、インターフェイスを解放することが重要です。 このテンプレート クラスは、有効期間を自動的に処理します。|  
|[PUnknown クラス](#PUnkownClass)|このクラスは、IUnknown インターフェイス専用のスマート ポインターです。 その他のインターフェイスにはすべて、Pointer テンプレート クラスを使用します。|  
|[StringUtil ヘルパー クラス](#StringUtilHelperClass)|このクラスは、文字列の操作をより簡単にするヘルパー メソッドを提供します。|  
|[SubInterface テンプレート クラス](#SubInterfaceTemplateClass)|この基底クラスは、別のインターフェイスから自身を継承するインターフェイスをサポートするコンポーネントの実装を容易にします。|  
|[UnknownImpl テンプレート クラス](#UnknownImplTemplateClass)|このクラスは、COM コンポーネントの作成の詳細のほとんどを処理します。|  
|[WizardComponent テンプレート クラス](#WizardComponentTemplateClass)|この基底クラスは、コンポーネントの作成やログ記録などのウィザード サービスへのアクセスが必要なコンポーネントの作成に使用されます。|  
|[WizardPageImpl テンプレート クラス](#WizardPageImplTemplateClass)|この基底クラスは、すべてのカスタム ウィザード ページの基底クラスとして使用する必要があります|  

####  <a name="ClassFactoryImplClass"></a> ClassFactoryImpl クラス  
 これは、作成後にファクトリ レジストリに登録できるクラス ファクトリを作成するのに役立つ基底クラスです。  

 以下は、**ClassFactoryImpl** クラスを定義する、サンプル プロジェクトの LocationPage.h ファイルからの抜粋です。  

```  
#pragma once  

#include "ClassFactoryImpl.h"  

class LocationPageFactory :public ClassFactoryImpl  
{  
protected:  
    IUnknown *CreateNewInstance();  
};  
```  

 以下は、サンプル ウィザード ページでページのクラス ファクトリを定義するために使用された、LocationPage.cpp ファイルからの抜粋です。  

```  
IUnknown *LocationPageFactory::CreateNewInstance()  
{  
    return static_cast<IWizardPage *>(new LocationPage);  
}  
```  

####  <a name="InterfaceTemplateClass"></a> インターフェイス テンプレート クラス  
 複数のインターフェイスを実装するコンポーネントをビルドするときに、このテンプレート クラスを使用します。次に例を示します。  

```  
classLocationPage :public Interface<IFieldCallback, WizardPageImpl<IDD_LOCATION_PAGE>>  
```  

 このコードは、**IFieldCalback** と、**WizardPageImpl** がサポートするインターフェイス (**IWizardPage** になったのは偶然です) の両方をサポートする基底クラス チェーンを作成します。  

####  <a name="PathHelperClass"></a> パス ヘルパー クラス  
 このクラスは、一般的なファイル操作またはディレクトリ操作を提供します。  

```  
static inline std::wstring GetModulePath(HINSTANCE hModule)  
```  

 また、このメソッドに提供するインスタンス ハンドルを使用して、.exe または .dll ファイルへの完全なパスを返します。  

```  
static inline std::wstring GetModuleFilename(HINSTANCE hModule)  
```  

 クラスは、このメソッドに提供するインスタンス ハンドルを使用して、.exe または .dll ファイルの完全なパスとファイル名を返します。  

```  
static inline std::wstring GetDirecotryName(LPCWSTR fullName)  
```  

 。 。 。 または、ファイル名を削除してパスだけを返します。  

```  
static inline std::wstring GetFileName(LPCWSTR fullName)  
```  

 パスにファイル名がある場合、パス ヘルパー クラスはファイル名のみを返します。  

```  
static inline std::wstring Combine(LPCWSTR path, LPCWSTR name)  
```  

 最後に、クラスは、パスとファイル名 (または別のパス) を組み合わせた新しい文字列を返します。  

####  <a name="PointerTemplateClass"></a> ポインター テンプレート クラス  
 このクラスは、Pointer.h で定義されます。 COM コンポーネントは、有効期間の管理に参照カウントを使用するため、インターフェイスでの操作が終わったら、常にインターフェイスを解放することが重要です。 Microsoft では、有効期間を自動的に処理するテンプレート クラスを提供しています。 たとえば、XML インターフェイスのスマート ポインターが必要な場合は、次のようなコードを記述することができます。  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 1 行目で、スマート ポインターを定義します。 2 行目には、別の呼び出しを通じてスマート ポインターを取得することが示されています。 **&** 演算子は、既存のインターフェイスが含まれている場合には常にそれを解放し、内部ポインターのアドレスを返します。 このようなポインターを取得すると、変数がスコープ外になったときに、**Release** が **Pointer** インスタンスによって呼び出されます。 **AddRef** と **Release** を手動で呼び出す代わりに、スマート ポインターを使用することをお勧めします。  

 さらに、**Pointer** スマート ポインター クラスは、他のインターフェイスを取得するために **QueryInterface** を呼び出します。 たとえば、ファクトリ レジストリでコンポーネントの新しいインスタンスを作成するときのコードは、次のようになります。  

```  
PWizardComponent pComp = pUnknown;  
if (pComp != nullptr)  
    pComp->SetContainer(m_pContainer);  
```  

 1 行目で **IWizardComponent** インターフェイスを要求する **QueryInterface** をバックグラウンドで呼び出します。 コンポーネントがそのインターフェイスをサポートしていない場合、結果のスマート ポインターは **nullptr** と等しくなります。  

####  <a name="PUnkownClass"></a> PUnknown クラス  
 このクラスは、**IUnknown** インターフェイス専用のスマート ポインターです。 その他のインターフェイスにはすべて、**Pointer** テンプレート クラスを使用します。  

####  <a name="StringUtilHelperClass"></a> StringUtil ヘルパー クラス  
 このクラスは、Utilities.h で定義され、文字列の操作をより簡単にするヘルパー メソッドを提供します。  

```  
static inline int CompareIgnore(LPCWSTR first, LPCWSTR second)  
```  

 このメソッドは、2 つの文字列を大文字と小文字を区別せずに比較します (表 9 を参照)。  

### <a name="table-9-stringutil-helper-class"></a>表 9 StringUtil ヘルパー クラス  

|**戻り値**|**説明**|  
|-|-|  
|**0**|文字列が一致、大文字と小文字を区別しない|  
|**<0**|1 番目 < 2 番目|  
|**>0**|1 番目 > 2 番目|  

 次に例を示します。  

```  
static inline std::wstring Format(LPCWSTR input, int index, LPCWSTR value)  
static inline std::wstring Format(LPCWSTR input, int index, DWORD value)  
```  

 これらのメソッドは、パラメーターが **{0}** の形式であるという点で、Microsoft .NET の **Format** メソッドに少し似ています。 ただし、これらのメソッドは置換するだけで、入力の書式設定は実行しません。  

```  
static inline std::wstring Printf(std::wstring format, I val)  
static inline std::wstring Printf(std::wstring format, I val1, J val2)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3, L val4)  
```  

 これらは、**wstring** を返す **StringCchPrintf** のラッパーなので、自分で文字列やバッファーにメモリを割り当てる必要はありません。  

####  <a name="SubInterfaceTemplateClass"></a> SubInterface テンプレート クラス  
 この基底クラスは、別のインターフェイスから自身を継承するインターフェイスをサポートするコンポーネントの実装を容易にします。 たとえば、 **ICheckBox** インターフェイスは **IControl** から継承します。 このクラスを使用して **CheckBoxWrapper** を定義する方法を次に示します。  

```  
classCheckBoxWrapper :public SubInterface<IControl, UnknownImpl<ICheckBox> >  
```  

 基底インターフェイスは最初のパラメーターですが、派生インターフェイスは 2 番目のパラメーターです。  

####  <a name="UnknownImplTemplateClass"></a> UnknownImpl テンプレート クラス  
 このクラスは、UnknownImpl.h で定義され、COM コンポーネントの作成の詳細のほとんどを処理します。 この基底クラスの使用例を次に示します。  

```  
classDirectory :public UnknownImpl<IDirectory>  
```  

 このコードは、**IDirectory** インターフェイスをサポートするクラスを定義します。  

####  <a name="WizardComponentTemplateClass"></a> WizardComponent テンプレート クラス  
 このクラスは、IWizardComponent.h で定義され、コンポーネントの作成やログ記録などのウィザード サービスへのアクセスが必要なコンポーネントの作成に便利な基底クラスです。  

 例として、**CopyFilesTask** コンポーネントを定義する方法を以下に示します。  

```  
classCopyFilesTask :public WizardComponent<ITask>  
{  
    ...  
```  

 タスクが **ITask** の場合に、このテンプレート クラスのパラメーターがコンポーネントに使用する "メイン" インターフェイスです。 **WizardComponent** を使用することは、提供するインターフェイス (この例では **ITask**) と **IWizardComponent** の両方をコンポーネントがサポートすることを意味します。  

 クラス ファクトリ レジストリを使用して新しいコンポーネントを作成する場合は常に、レジストリによってコンポーネントの **IWizardComponent->SetContainer** が呼び出され、ウィザード サービスへのアクセスがコンポーネントに提供されます。  

####  <a name="WizardPageImplTemplateClass"></a> WizardPageImpl テンプレート クラス  
 このクラスをカスタム ページの基底クラスとして使用します。次に例を示します。  

```  
class LocationPage :public WizardPageImpl<IDD_LOCATION_PAGE>  
```  

 パラメーターは、ダイアログ ボックス テンプレートのリソース ID です。  

###  <a name="WizardPageInterfaces"></a> ウィザード ページのインターフェイス  
 UDI ウィザードでは、インターフェイスを使用して、ページ上のさまざまなコントロールにアクセスします。 ページ内で、**GetControlWrapper** 関数を使用して、コントロール ラッパーを取得します。 次に例を示します。  

```  
PStaticText pFormat;  
GetControlWrapper(View(), IDC_CHECK_PARTITION, CONTROL_STATIC_TEXT, &pFormat);  
```  

 ここでは、**PStaticText** は **IStaticText** インターフェイスへのスマート ポインターです。 スマート ポインターがスコープ外になるか、変数のアドレス (**&pFormat** など) をメソッドに渡すと、スマート ポインターによって COM **Release()** メソッドが自動的に呼び出されます。  

#### <a name="iadhelper-interface"></a>IADHelper インターフェイス  

```  
__interfaceIADHelper : IUnknown  
{  
    HRESULT Init(ILogger *pLogger);  
    HRESULT ValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain);  
    HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain);  
};  

```  

##### <a name="hresult-initilogger-plogger"></a>HRESULT Init(ILogger \*pLogger)  
 このコンポーネントを初期化し、それをロガーに渡して情報をログに記録できるようにします。  

##### <a name="hresultvalidlogonlpctstr-username-lpctstr-password-lpctstr-domain"></a>HRESULTValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain)  
 表 10 に示すように、このメソッドは、一連の資格情報が有効であるかどうかを検証します。  

### <a name="table-10-hresultvalidlogon"></a>表 10 HResultValidLogon  

|**HResult**|**説明**|  
|-|-|  
|S_OK|資格情報は有効です|  
|S_FALSE|資格情報は有効ではありません|  
|E_FAIL|ドメイン コントローラーが見つかりませんでした。詳細についてはログを確認してください|  

##### <a name="hresult-hasaccesslpctstr-username-lpctstr-password-lpctstr-domain-lpctstr-computername-lpctstr-accountdomain"></a>HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain)  
 このメソッドは、一連の資格情報に、AD DS 内のコンピューター オブジェクトに対する、表 11 に示すような読み取り/書き込みアクセス権があるかどうかを検証します。  

### <a name="table-11-hresult-hasaccess"></a>表 11 HResult HasAccess  

|**HRESULT**|**説明**|  
|-|-|  
|S_OK|ユーザーにはアクセス権があります|  
|E_FAIL|ユーザーにはアクセス権はありません。 詳細については、ログ ファイルを確認してください。|  

#### <a name="ibackgroundtask-interface"></a>IBackgroundTask インターフェイス  

```  
__interface IBackgroundTask : IUnknown  
{  
    HRESULT Init(ITask *pTask, int id, IBackgroundCallback *pCallback);  
    void Start(void);  
    BOOL Running(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    HRESULT Terminate(DWORD exitCode);  
    HRESULT GetExitCode(LPDWORD pCode, HRESULT *pHresult);  
    HRESULT Close(void);  
};  
```  

##### <a name="overview"></a>概要  
 **Progress** ページは、このクラスを使用して別のスレッドでタスクを実行します。 別のスレッドで操作を実行する場合も、常にこのクラスを使用できます。 *Tasks* は、**ITask** インターフェイスをサポートする任意のクラスです。  

 このインターフェイスは、IBackgroundTask.h インターフェイスで定義されている **ID_BackgroundTask** ("Microsoft.Wizard.BackgroundTask") コンポーネントによって実装されます。  

##### <a name="hresult-inititask-ptask-int-id-ibackgroundcallback-pcallback"></a>HRESULT Init(ITask \*pTask, int id, IBackgroundCallback \*pCallback)  
 表 12 に示されているように、このインターフェイスはコンポーネントを初期化します。  

### <a name="table-12-hresult-init"></a>表 12 HRESULT Init  

|**パラメーター**|**説明**|  
|-|-|  
|**pTask**|別のスレッドで実行するコードを含むクラスへのポインター|  
|**Id**|どのタスクの実行が完了したかを通知するため、コールバックの **Finished** メソッドで使用できる数。同じコールバック メソッドを使用して複数のタスクを開始する場合に役立ちます|  
|**pCallback**|タスクの実行が完了するたびに呼び出される、**Finished** メソッドを実装するクラス。**Finished** メソッドへの呼び出しは、UI スレッドではなく、バックグラウンド スレッドで行われます|  

##### <a name="void-startvoid"></a>void Start(void)  
 このメソッドはバックグラウンド スレッドでタスクを開始し、表 13 に示す要素を返します。  

### <a name="table-13-return-background-thread"></a>表 13 バックグラウンド スレッドの戻り値  

|**戻り値**|**説明**|  
|-|-|  
|**E_INVALIDARG**|タスクは既に実行されているため、今すぐ開始することはできません。|  
|**E_FAIL**|スレッドの開始に問題が発生しました。|  
|**S_OK**|スレッドが開始されました。|  

##### <a name="bool-running"></a>BOOL Running()  
 このメソッドは、バックグラウンド タスクが現在実行されている場合は TRUE を返し、実行されていない場合は FALSE を返します。  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 このメソッドは、スレッドの実行が停止するか、ミリ秒数が経過するまで待機します。  

##### <a name="hresult-terminatedword-exitcode"></a>HRESULT Terminate(DWORD exitCode)  
 このメソッドは、実行中のスレッドを中止します (表 14 と表 15 を参照)。 このメソッドが戻ってからこのプロセスが完了するまでに少し時間がかかる場合があります。  

### <a name="table-14-hresult-terminate-exit-code"></a>表 14 HRESULT Terminate 終了コード  

|**パラメーター**|**説明**|  
|-|-|  
|**exitCode**|Finished コールバック メソッドに送信される終了コード。**GetExitCode** メソッドからも使用できます。|  

### <a name="table-15-termination-codes"></a>表 15 終了コード  

|**戻り値**|**説明**|  
|-|-|  
|**E_FAIL**|終了の呼び出しが失敗しました。|  
|**S_OK**|スレッドを終了する要求が成功しました。|  

##### <a name="hresult-getexitcodelpdword-pcode-hresult-phresult"></a>HRESULT GetExitCode(LPDWORD pCode, HRESULT \*pHresult)  
 このメソッドを使用して、バックグラウンド スレッドで実行中のタスクの結果を取得します (表 16 を参照)。  

### <a name="table-16-result-codes"></a>表 16 結果コード  

|**パラメーター**|**説明**|  
|-|-|  
|**pCode**|戻り時に設定される **DWORD** へのポインター、または戻り値が必要ない場合は **nullptr**。 終了時に、スレッドが実行中の場合、タスクの **Execute** メソッドによってコードが返された場合、または **Terminate** メソッドを呼び出した場合にそのメソッドに値が渡された場合は、このパラメーターは **STILL_ACTIVE** に設定されます。|  
|**pHresult**|戻り時に設定される **HRESULT** へのポインター、または **HRESULT** 値が必要ない場合は **nullptr**。|  

##### <a name="hresult-closevoid"></a>HRESULT Close(void)  
 このメソッドは、バックグラウンド スレッドを解放します。 スレッドが現在実行されている場合は **E_INVALIDARG** を返し、それ以外の場合は **S_OK** を返します。  

#### <a name="icheckbox-interface"></a>ICheckBox インターフェイス  

```  
__interface ICheckBox : IControl  
{  
    void Check(BOOL check);  
    BOOL IsButtonChecked();  
};  
```  

##### <a name="void-checkbool-check"></a>void Check(BOOL check)  
 チェック ボックスのチェック状態を設定します。 メソッドが TRUE の場合はチェック ボックスがオンになり、メソッドが FALSE の場合は、チェック ボックスがオフになります。  

##### <a name="bool-isbuttonchecked"></a>BOOL IsButtonChecked()  
 このメソッドは、チェック ボックスの現在のチェック状態を報告します。  

#### <a name="icombobox-interface"></a>IComboBox インターフェイス  

```  
__interface IComboBox : IControl  
{  
    HRESULT Bind([in] IBindableList *pList);  
    HRESULT Select(int index);  
    int Selected(void);  
    void Add([in] LPCTSTR caption);  
    HRESULT GetText([out, retval] LPBSTR pText);  
    void Clear();  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、**CheckBoxWrapper** コンポーネントによって実装されます。 **GetControlWrapper** ヘルパー関数と **CONTROL_COMBO_BOX** 型を使用して、このコンポーネントのインスタンスを取得します。  

##### <a name="hresult-bindin-ibindablelist-plist"></a>HRESULT Bind([in] IBindableList \*pList)  
 **IBindableList** インターフェイスを実装するデータ ソースがある場合は、このメソッドを使用します。 リスト ボックスは、このリストからのキャプションを使用してコンテンツを初期化します。  

##### <a name="hresult-selectint-index"></a>HRESULT Select(int index)  
 インデックスでコンボ ボックス内の項目を選択します。  

##### <a name="int-selectedvoid"></a>int Selected(void)  
 このメソッドは、選択した項目のインデックスを返すか、何も選択されていない場合は **-1** を返します。  

##### <a name="void-addin-lpctstr-caption"></a>void Add([in] LPCTSTR caption)  
 コンボ ボックスに項目を手動で追加します。  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 コンボ ボックスで現在選択されている項目の文字列を取得します。  

##### <a name="void-clear"></a>void Clear()  
 コンボ ボックスからすべての項目を削除します。  

#### <a name="icontrol-interface"></a>IControl インターフェイス  

```  
__interface IControl : IUnknown  
{  
    HRESULT SetEnable(BOOL enable);  
    BOOL IsEnabled(void);  
    HRESULT SetVisible(BOOL visible);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、**ControlWrapper** コンポーネントによって実装されます。 **GetControlWrapper** ヘルパー関数と **CONTROL_GENERIC** 型を使用して、このコンポーネントのインスタンスを取得します。  

##### <a name="hresult-setenablebool-enable"></a>HRESULT SetEnable(BOOL enable)  
 コントロールを有効または無効にします。  

##### <a name="bool-isenabledvoid"></a>BOOL IsEnabled(void)  
 コントロールが有効になっている場合は TRUE、なっていない場合は FALSE を返します。  

##### <a name="hresult-setvisiblebool-visible"></a>HRESULT SetVisible(BOOL visible)  
 コントロールを表示または非表示にします。  

#### <a name="icpuinfo-interface"></a>ICpuInfo インターフェイス  

```  
__interface ICpuInfo : IUnknown  
{  
    BOOL Is64Bit(void);  
};  
```  

##### <a name="overview"></a>概要  
 新しい **ID_CpuInfo** コンポーネントを作成することで、このインターフェイスを取得します。 1 つのメソッドが、CPU が 32 ビットまたは 64 ビットかどうかを報告します。 このメソッドは CPU (オペレーティング システムではなく) の幅のみを報告するため、64 ビット コンピューターで 32 ビット オペレーティング システムを実行している場合は、TRUE が返されます。  

##### <a name="idirectory-interface"></a>IDirectory インターフェイス  

```  
__interface IDirectory : IUnknown  
{  
    BOOL FileExists(LPCWSTR name);  
    BOOL FindFirst([in] LPCWSTR name);  
    HRESULT FoundName([out, retval] LPBSTR name);  
    DWORD FoundAttributes(void);  
    BOOL FindNext(void);  
    void FinishFind(void);  
};  
```  

###### <a name="overview"></a>概要  
 **ID_Directory** を使用して作成する **Directory** コンポーネントは、ファイル システム内のディレクトリを操作するためのファサードを提供します。  

###### <a name="bool-fileexistslpcwstr-name"></a>BOOL FileExists(LPCWSTR name)  
 このメソッドは、指定した名前を持つファイルが存在する場合に TRUE を返します。  

###### <a name="bool-findfirstin-lpcwstr-name"></a>BOOL FindFirst([in] LPCWSTR name)  
 このメソッドは、指定した名前の最初の一致を検索します。 これはワイルドカード文字をサポートし、ファイル名とディレクトリ名の両方を返します。 このメソッドは、一致が見つかった場合は TRUE を返し、見つからなかった場合は FALSE を返します。  

###### <a name="hresult-foundnameout-retval-lpbstr-name"></a>HRESULT FoundName([out, retval] LPBSTR name)  
 このメソッドは、**FindFirst** または **FindNext** の呼び出しで見つかったファイルの名前を取得します。  

###### <a name="dword-foundattributesvoid"></a>DWORD FoundAttributes(void)  
 このメソッドは、見つかった最新のファイルまたはディレクトリの属性を返します。 次のようにコードを使用してディレクトリかどうかをテストできます。  

```  
pDirectory->FoundAttributes() & FILE_ATTRIBUTE_DIRECTORY  
```  

###### <a name="bool-findnextvoid"></a>BOOL FindNext(void)  
 次を検索します。 このメソッドは、別の一致が見つかった場合は TRUE を返し、見つからなかった場合は FALSE を返します。  

###### <a name="void-finishfindvoid"></a>void FinishFind(void)  
 このメソッドは、検索操作に使用されるリソースを解放します。  

#### <a name="idomainjoinvalidator-interface"></a>IDomainJoinValidator インターフェイス  

```  
__interface IDomainJoinValidator : IUnknown  
{  
    HRESULT Init(ILogger *pLogger, IWizardPageContainer *pContainer, IStaticText *pUsername, IStaticText *pPassword, IStaticText *pComputerName);  
    HRESULT IsUsernameValid(LPCWSTR domainName);  
    BOOL CanModifyComputerAdEntry(LPCWSTR domainName);  
};  
```  

##### <a name="overview"></a>概要  
 **CreateInstance** テンプレート関数に **ID_DomainJoinValidator** 値を使用して、このインターフェイスのインスタンスを取得します。  

##### <a name="hresult-initilogger-plogger-iwizardpagecontainer-pcontainer-istatictext-pusername-istatictext-ppassword-istatictext-pcomputername"></a>HRESULT Init(ILogger \*pLogger, IWizardPageContainer \*pContainer, IStaticText \*pUsername, IStaticText \*pPassword, IStaticText \*pComputerName)  
 表 17 に示すように、インスタンスを初期化します。  

### <a name="table-17-hresult-init---instance-initialization"></a>表 17 HRESULT Init - インスタンスの初期化  

|**パラメーター**|**説明**|  
|-|-|  
|**pLogger**|ページの **Logger** メソッドを介してページで使用できるロガー インスタンス|  
|**pContainer**|ページの **Container** から結果を渡します|  
|**pUsername**|検証するユーザー名を含むテキスト ボックス|  
|**pPassword**|検証するパスワードを含むテキスト ボックス|  
|**PComputerName**|最終的にドメインに参加するコンピューターの名前を含むテキスト ボックス|  

##### <a name="hresult-isusernamevalidlpcwstr-domainname"></a>HRESULT IsUsernameValid(LPCWSTR domainName)  
 このメソッドは、**IADHelper->ValidLogon** メソッドを使用して作業を実行します。 詳細については、そのメソッドを参照してください。  

##### <a name="bool-canmodifycomputeradentrylpcwstr-domainname"></a>BOOL CanModifyComputerAdEntry(LPCWSTR domainName)  
 ユーザーがコンピューターのエントリを変更する権限を持っているかどうかを検証します。 作業の大部分は **IADHelper->HasAccess** で実行されます。 このメソッドで FALSE が返される場合は、ログ ファイルで詳細を確認します。  

#### <a name="idrivelist-interface"></a>IDriveList インターフェイス  

```  
__interface IDriveList : IUnknown  
{  
    HRESULT Init(IWmiRepository *pWmi);  
    HRESULT SetWhereClause(LPCTSTR whereClause);  
    HRESULT SetMinimumDriveSize(__int64 size);  
    HRESULT Update(void);  
    HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned);  

    size_t Count(void);  
    HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value);  
    HRESULT GetCaption(size_t index,  LPBSTR pCaption);  
}  
```  

##### <a name="hresult-initiwmirepository-pwmi"></a>HRESULT Init(IWmiRepository \*pWmi)  
 他のコンポーネントを呼び出す前に、このメソッドを呼び出します。 このメソッドを呼び出す前に、新しい **WmiRepository** を作成する必要があります。  

##### <a name="hresult-setwhereclauselpctstr-whereclause"></a>HRESULT SetWhereClause(LPCTSTR whereClause)  
 このメソッドを使用すると、クエリで "where" 句として表示されるテキストを追加することができます。 たとえば、次の行では USB ドライブのみが返されます。  

```  
pDrives->SetWhereClause(L"WHERE InterfaceType='USB'");  
```  

##### <a name="hresult-setminimumdrivesizeint64-size"></a>HRESULT SetMinimumDriveSize(\__int64 size)  
 クエリから返されるドライブの最小ドライブ サイズをバイト単位で設定します。  

##### <a name="hresult-updatevoid"></a>HRESULT Update(void)  
 クエリを実行します。 このメソッドの呼び出し後に利用可能なドライブのリストは、ドライブ文字で並べ替えられます。  

##### <a name="hresult-addpropertyenumdiskquerysection-section-lpctstr-propname-lpctstr-propnamereturned"></a>HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned)  
 このメソッドは、クエリの結果に使用できるようにする追加のプロパティの名前を追加します。 このメソッドを呼び出してから、**Update** を呼び出します。 表 18 に、便利なプロパティのうちの 3 つを示します。  

### <a name="table-18-hresult-addproperty-useful-properties"></a>表 18 HRESULT AddProperty: 便利なプロパティ  

|**セクション**|**プロパティ**|**説明**|  
|-|-|-|  
|**DISKQUERY_LOGICALDISK**|**Size**|文字列として表されるサイズ (バイト単位)|  
|**DISKQUERY_DISKPARTITION**|**DiskIndex**|ディスク番号、0 から始まる整数値|  
|**DISKQUERY_LOGICALDISK**|**VolumeName**|ボリューム ラベル|  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 クエリが返すレコードの数。 **Update** を呼び出してから、このメソッドを呼び出します。  

##### <a name="hresult-getpropertysizet-index-lpctstr-propname--lpvariant-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value)  
 このメソッドは、表 19 に示すように、クエリの結果からプロパティの値を取得します。  

### <a name="table-19-hresult-getproperty"></a>表 19 HRESULT GetProperty  

|**パラメーター**|**説明**|  
|-|-|  
|**Index**|結果のレコードへの 0 から始まるインデックス|  
|**propName**|プロパティの名前 (“Size” など)|  
|**値**|戻り時に、このパラメーターにはプロパティのバリアント値が含まれます|  

##### <a name="hresult-getcaptionsizet-index--lpbstr-pcaption"></a>HRESULT GetCaption(size_t index, LPBSTR pCaption)  
 このメソッドは、**Caption** プロパティと同じレコードのキャプションを取得します。  

#### <a name="iimagelist-interface"></a>IImageList インターフェイス  

```  
__interface IImageList  
{  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    HImageList GetImageList(void);  
    int AddImage(HInstance hInstance, int resourceId);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、**ImageList** コンポーネントによって実装されます。 このコンポーネントのインスタンスは、**IListView** インターフェイスから取得します。  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 このコンポーネントで管理する新しいイメージ リストを作成します。 このメソッドを 1 回だけ呼び出します。  

##### <a name="himagelist-getimagelistvoid"></a>HImageList GetImageList(void)  
 このメソッドは、イメージ リストで別の操作を実行する必要がある場合に、イメージ リストのハンドルを返します。  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage (HInstance hInstance、int resourceId)  
 表 20 に示すように、新しいイメージをリソースからイメージ リストに追加します。  

### <a name="table-20-hresult-iimagelist-interface"></a>表 20 HRESULT IImageList インターフェイス  

|**パラメーター**|**説明**|  
|-|-|  
|**hInstance**|ビットマップのリソースを含むモジュールのインスタンス ハンドル|  
|**resourceId**|イメージ リストに読み込むリソースの ID|  

#### <a name="ilistview-interface"></a>IListView インターフェイス  

```  
__interface IListView : IControl  
{  
    int AddItem([in] LPCTSTR text);  
    int AddColumn(int width, [in] LPCTSTR text);  
    HRESULT SetSubItem(int index, int column, [in] LPCTSTR text);  
    int GetWidth(void);  
    void SetExtendedStyle(DWORD style);  
    int GetSelectedItem(void);  
    HRESULT SelectItem(int index);  
    BOOL IsItemChecked(int index);  
    int GetItemCount(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  
    HRESULT SetImage(int index, int imageIndex);  
    HRESULT Clear(void);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、**ControlWrapper** コンポーネントによって実装されます。 **GetControlWrapper** ヘルパー関数と **CONTROL_LIST_VIEW** 型を使用して、このコンポーネントのインスタンスを取得します。  

##### <a name="int-additemin-lpctstr-text"></a>int AddItem([in] LPCTSTR text)  
 リスト ボックスに新しい行を追加します。 このメソッドは追加した項目のインデックスを返します。  

##### <a name="int-addcolumnint-width-in-lpctstr-text"></a>int AddColumn(int width, [in] LPCTSTR text)  
 リスト ビューに新しい列を追加します。  

##### <a name="hresult-setsubitemint-index-int-column-in-lpctstr-text"></a>HRESULT SetSubItem(int index, int column, [in] LPCTSTR text)  
 表 21 に示すように、リスト ボックスの最初の列以外の列にあるテキストを設定します。  

### <a name="table-21-hresult-setsubitem"></a>表 21 HRESULT SetSubItem  

|**パラメーター**|**説明**|  
|-|-|  
|**index**|変更するリスト アイテムのインデックス|  
|**column**|更新する列のインデックス。最初の列は **AddItem** で設定され、2 列目以降はこのメソッドで設定されます|  
|**text**|列に表示する文字列|  

##### <a name="int-getwidthvoid"></a>int GetWidth(void)  
 このメソッドは、テキスト ボックス全体の幅を返します。  

##### <a name="void-setextendedstyledword-style"></a>void SetExtendedStyle(DWORD style)  
 このメソッドを使用すると、リスト ボックスに拡張スタイルを設定することができます。次に例を示します。  

```  
m_pList->SetExtendedStyle(LVS_EX_FULLROWSELECT);  
```  

##### <a name="int-getselecteditemvoid"></a>int GetSelectedItem(void)  
 このメソッドは、現在選択されているリスト ビュー項目のインデックスを返します。  

##### <a name="hresult-selectitemint-index"></a>HRESULT SelectItem(int index)  
 リスト内の選択した項目をこのインデックスに設定します。  

##### <a name="bool-isitemcheckedint-index"></a>BOOL IsItemChecked(int index)  
 このメソッドは、リスト内の項目が選択されている場合に TRUE を返します。 このメソッドは、**SetExtendedStyle** を呼び出して、チェック ボックスのスタイルを設定することを要求します。  

##### <a name="int-getitemcountvoid"></a>int GetItemCount(void)  
 このメソッドは、リスト ビュー内の項目の数を返します。  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 新しいイメージ リストを作成し、リスト ビューにアタッチします。  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 リスト ビューのイメージ リストにイメージを追加します。 最初に **CreateImageList** を呼び出す必要があります。  

##### <a name="hresult-setimageint-index-int-imageindex"></a>HRESULT SetImage(int index, int imageIndex)  
 特定のリスト ビュー項目の左側に表示されるイメージを設定します。  

##### <a name="hresult-clearvoid"></a>HRESULT Clear(void)  
 リスト ビューからすべての項目を削除します。  

#### <a name="iprogressbar-interface"></a>IProgressBar インターフェイス  

```  
__interface IProgressBar : IControl  
{  
    HRESULT SetPercentage(int position);  
    int GetPercentage(void);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、**ProgressBarWrapper** コンポーネントによって実装されます。 **GetControlWrapper** ヘルパー関数と **CONTROL_PROGRESS_BAR** 型を使用して、このコンポーネントのインスタンスを取得します。  

##### <a name="hresult-setpercentageint-position"></a>HRESULT SetPercentage(int position)  
 0 から 100 までの数を使用して進行状況バーの位置を設定します。 既定では、新しい Win32® 進行状況バーの最大範囲は 100 です。  

##### <a name="int-getpercentagevoid"></a>int GetPercentage(void)  
 このメソッドは、進行状況バーの現在の位置を返します。  

#### <a name="iradiobutton-interface"></a>IRadioButton インターフェイス  

```  
__interface IRadioButton : IControl  
{  
public:  
    void SetGroup(int firstId, int lastId);  
    void CheckRadio(int id);  
    BOOL IsButtonChecked(int id);  
    void EnableRadio(int id, BOOL enable);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、**RadioButtonWrapper** コンポーネントによって実装されます。 **GetControlWrapper** ヘルパー関数と **CONTROL_RADIO_BUTTON** 型を使用して、このコンポーネントのインスタンスを取得します。  

##### <a name="void-setgroupint-firstid-int-lastid"></a>void SetGroup(int firstId, int lastId)  
 ラッパーにグループとして扱う必要があるラジオ ボタンの範囲を提供します。 **CheckRadio** を呼び出す前に、このメソッドを呼び出します。  

##### <a name="void-checkradioint-id"></a>void CheckRadio(int id)  
 特定のラジオ ボタンを、選択したラジオ ボタンのグループ内の 1 つのボタンに設定します。 **SetGroup** を呼び出してから、このメソッドを呼び出します。  

##### <a name="bool-isbuttoncheckedint-id"></a>BOOL IsButtonChecked(int id)  
 このメソッドは、ラジオ ボタンが現在選択されている場合には TRUE を返し、それ以外の場合には FALSE を返します。  

##### <a name="void-enableradioint-id-bool-enable"></a>void EnableRadio(int id, BOOL enable)  
 このメソッドは、ラジオ ボタンを有効または無効にします。  

#### <a name="istatictext-interface"></a>IStaticText インターフェイス  

```  
__interface IStaticText : IControl  
{  
    HRESULT SetText([in] LPCTSTR pText);  
    HRESULT GetText([out, retval] LPBSTR pText);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、**StaticTextWrapper** コンポーネントによって実装されます。 **GetControlWrapper** ヘルパー関数と **CONTROL_STATIC_TEXT** 型を使用して、このコンポーネントのインスタンスを取得します。  

##### <a name="hresult-settextin-lpctstr-ptext"></a>HRESULT SetText([in] LPCTSTR pText)  
 コントロールのテキストを設定します。  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 このメソッドは、コントロールのテキストの現在の値を返します。  

####  <a name="ITaskinterface"></a> ITask インターフェイス  

```  
__interface IControl : IUnknown  
{  
    HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings);  
    HRESULT Execute(LPDWORD pReturnCode);  
};  
```  

 コンポーネントをプレフライト ページでタスクとして使用できるようにする場合、または **BackgroundTask** コンポーネントを使用してバックグラウンド スレッドで作業を実行する場合は、このインターフェイスを実装します。  

 **ITask** インターフェイスを実装するコンポーネントは次のとおりです。  

-   ID_ShellExecuteTask、L"Microsoft.Wizard.ShellExecuteTask"  

-   ID_CopyFilesTask、L"Microsoft.Wizard.CopyFilesTask"  

-   ID_ACPowerTask、L"Microsoft.OSDRefresh.ACPowerTask"  

-   ID_WiredNetworkTask、L"Microsoft.SharedPages.WiredNetworkTask"  

##### <a name="init"></a>初期状態  

```  
HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings)  
```  

 プレフライト ページのタスクを記述している場合は、このメソッドを呼び出してそのタスクを初期化します。 .config ファイルには、次のような XML が含まれます。  

```  
<Task DisplayName="Check Windows Scripting Host" Type="Microsoft.Wizard.ShellExecuteTask">  
  <Setter Property="filename">%windir%\system32\cscript.exe</Setter>  
  <Setter Property="parameters">Preflight\OSDCheckWSH.vbs</Setter>  
  <Setter Property="BitmapFilename">images\WinScriptHost.bmp</Setter>  
  <ExitCodes>  
    <ExitCode State="Success" Type="0" Value="0" Text="" />  
    <ExitCode State="Error" Type="-1" Value="*" Text="Windows Scripting Host not installed." />  
  </ExitCodes>  
</Task>  
```  

 **pProperties** パラメーターが 3 つのセッター値へのアクセスを提供するのに対し、**pTaskSettings** パラメーターは **Task** 要素と子へのアクセスを提供します。 ほとんどのタスクは、**pProperties** パラメーターからデータを読み取るだけで十分です。  

#####  <a name="Execute"></a> Execute  

```  
HRESULT Execute(LPDWORD pReturnCode)  
```  

 ここで、タスクを実行するコードを記述します。 このメソッドは、エラーがない場合には **S_OK** を返し、タスクの実行中にエラーが発生した場合は、別の **HRESULT** を返すことができます。 プレフライト ページを使用している場合は、このメソッドが返す **S_OK** 以外の値は、<ExitCodes\> セクションの <Error\> 要素と一致します。  

 **pReturnCode** パラメーターは、タスクの状態を報告する数値で更新する必要があります。 これらの値は、プレフライト ページによって <ExitCode\> 要素と整合されます。  

#### <a name="itreeview-interface"></a>ITreeView インターフェイス  

```  
__interface ITreeView : IControl  
{  
    void EnableCheckboxes(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  

    HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL);  
    void SetImage(HTREEITEM item, int image, int expandImage);  

    void Clear(void);  
    BOOL SetFirstVisible(HTREEITEM item);  
    BOOL SelectItem(HTREEITEM item);  
    void CheckItem(HTREEITEM item, UINT checkState);  
    HTREEITEM SelectedItem(void);  
    int SetItemHeight(SHORT height);  
    HRESULT EnableItem(HTREEITEM item, BOOL enable);  
    void Expand(HTREEITEM hItem, BOOL expand);  

    HTREEITEM GetChild(HTREEITEM hParent);  
    HTREEITEM GetParent(HTREEITEM hNode);  
    HTREEITEM GetNextItem(HTREEITEM hPrevious);  

    UINT IsChecked(HTREEITEM item);  
    BOOL IsEnabled(HTREEITEM item);  

    INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL *pCancel);  
    HRESULT SetEventHandler(ITreeViewEvent *pEventHandler);  

    void SetSelectedBackColor(COLORREF color);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、**TreeViewWrapper** コンポーネントによって実装されます。 **GetControlWrapper** ヘルパー関数と **CONTROL_TREE_VIEW** 型を使用して、このコンポーネントのインスタンスを取得します。  

##### <a name="void-enablecheckboxesvoid"></a>void EnableCheckboxes(void)  
 このメソッドは、**TVS_CHECKBOXES** スタイルを設定することで、ツリー ビュー コントロール内のチェック ボックスをオンにします。  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 ツリー ビュー コントロールに新しいイメージ リストを追加します。 **ImageList_Create** Win32 関数への呼び出し時に、**flags** パラメーターが渡されます。  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 インスタンス ハンドル **hInstance** を使用して、モジュール内のリソース (**resourceId**) からイメージをイメージ リストに追加します。  

##### <a name="htreeitem-additemlpctstr-text-htreeitem-hparent--null"></a>HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL)  
 ノードをツリー ビューに追加します。 **hParent** が NULL の場合、新しいノードは最上位レベルに追加されます。 それ以外の場合は、新しい項目を追加する親項目にハンドルが提供されます。 このメソッドは、新しい項目へのハンドルを返します。  

##### <a name="void-setimagehtreeitem-item-int-image-int-expandimage"></a>void SetImage(HTREEITEM item, int image, int expandImage)  
 ツリー ビュー項目に使用するイメージを設定します。 通常のイメージと展開されたイメージの両方を設定することができます。  

##### <a name="void-clearvoid"></a>void Clear(void)  
 ツリー ビューからすべての項目を削除します。  

##### <a name="bool-setfirstvisiblehtreeitem-item"></a>BOOL SetFirstVisible(HTREEITEM item)  
 ツリー ビュー項目が確実に表示されるようにします。 ツリー ビューは、この項目を表示するために必要に応じてスクロールされます。  

##### <a name="bool-selectitemhtreeitem-item"></a>BOOL SelectItem(HTREEITEM item)  
 現在選択されている項目を、提供する項目に設定します。 この後に **SetFirstVisible** を呼び出して、新しく選択した項目が確実に表示されるようにします。  

##### <a name="void-checkitemhtreeitem-item-uint-checkstate"></a>void CheckItem(HTREEITEM item, UINT checkState)  
 このメソッドは基本的に、ツリー ビュー内のチェック ボックスに表示されるイメージを設定します。 これらのイメージは、ツリー ビューが管理する別の **ImageList** コントロールにあります。 既定では、このイメージ リストには表 22 に示されている 3 つのイメージがあります。  

### <a name="table-22void-checkitem-image-list-default"></a>表 22 void CheckItem イメージ リストの既定値  

|**checkState**|**説明**|  
|-|-|  
|**0**|[新規]|  
|**1**|クリア|  
|**2**|オン|  

##### <a name="htreeitem-selecteditemvoid"></a>HTREEITEM SelectedItem(void)  
 このメソッドは、現在選択されているツリー ビュー項目のハンドルを返します。  

##### <a name="int-setitemheightshort-height"></a>int SetItemHeight(SHORT height)  
 このメソッドは、ツリー ビュー コントロール内のすべての項目の高さをピクセル単位で設定します。 以前の高さをピクセル単位で返します。  

##### <a name="hresult-enableitemhtreeitem-item-bool-enable"></a>HRESULT EnableItem(HTREEITEM item, BOOL enable)  
 このメソッドは、ツリー内の 1 つの項目を有効または無効にします。 子を持つ項目を無効にしても、その子は無効になりません。  

##### <a name="void-expandhtreeitem-hitem-bool-expand"></a>void Expand(HTREEITEM hItem, BOOL expand)  
 このメソッドは、ツリー内のノードを展開または折りたたみます。  

##### <a name="htreeitem-getchildhtreeitem-hparent"></a>HTREEITEM GetChild(HTREEITEM hParent)  
 このメソッドは、ツリー ビュー項目の最初の子を返し、子がない場合は NULL を返します。  

##### <a name="htreeitem-getparenthtreeitem-hnode"></a>HTREEITEM GetParent(HTREEITEM hNode)  
 このメソッドは、ツリー ビュー内のノードの親のハンドルを返し、ノードが最上位レベルにある場合は NULL を返します。  

##### <a name="htreeitem-getnextitemhtreeitem-hprevious"></a>HTREEITEM GetNextItem(HTREEITEM hPrevious)  
 **GetChild** によって返されるハンドルを使用してこのメソッドを呼び出して、ノードのすべての子を反復処理することができます。 このメソッドは、同じ親を共有するツリー内の次の兄弟を返します。  

##### <a name="uint-ischeckedhtreeitem-item"></a>UINT IsChecked(HTREEITEM item)  
 このメソッドは、ツリー ビュー ノードが選択されていない場合は **0** を返し、選択されている場合は **1** を返します。  

##### <a name="bool-isenabledhtreeitem-item"></a>BOOL IsEnabled(HTREEITEM item)  
 このメソッドは、ツリー ビュー ノードが有効になっている場合は TRUE を返し、それ以外の場合は FALSE を返します。  

##### <a name="intptr-commoncontroleventword-controlid-void-pinfo-bool-pcancel"></a>INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL \*pCancel)  
 このメソッドは内部でのみ使用されます。  

##### <a name="hresult-seteventhandleritreeviewevent-peventhandler"></a>HRESULT SetEventHandler(ITreeViewEvent \*pEventHandler)  
 選択した項目が変更されたとき、またはユーザーがツリー ビュー項目のチェックの状態を変更したときに通知を受信する場合は、このメソッドを呼び出します。 これらのコールバックを受信するには、**ITreeViewEvent** をコンポーネントに実装する必要があります。  

##### <a name="void-setselectedbackcolorcolorref-color"></a>void SetSelectedBackColor(COLORREF color)  
 選択した項目に使用する背景色を設定します。  

#### <a name="iwmiiteration-interface"></a>IWmiIteration インターフェイス  

```  
__interface IWmiIterator : IUnknown  
{  
    HRESULT Next(void);  
    HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは通常、WMI 呼び出しを使用する場合に、**IWmiRepository** とともに使用します。 **IWmiIteration** インターフェイスを使用すると、クエリで返される値を反復処理することができます。  

##### <a name="hresult-nextvoid"></a>HRESULT Next(void)  
 表 23 に示すように、クエリ結果内の次の項目に移動します。  

### <a name="table-23-hresult-nextvoid-query-returns"></a>表 23 HRESULT Next(void) クエリ結果  

|**HRRESULT**|**説明**|  
|-|-|  
|**S_OK**|次の結果に移動します。**GetProperty** を使用して、その結果のプロパティを取得できます。|  
|**S_FALSE**|リスト内にこれ以上項目がありません。|  
|**E_NOT_SET**|クエリ結果がありません。|  

##### <a name="hresult-getpropertylpctstr-propertyname-out-lpvariant-pvalue"></a>HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue)  
 このメソッドは、表 24 と表 25 に示すように、現在の結果レコードからプロパティの値を取得します。  

### <a name="table-24-hresult-getproperty"></a>表 24 HRESULT GetProperty  

|**パラメーター**|**説明**|  
|-|-|  
|**propertyName**|取得するプロパティの名前|  
|**pValue**|戻り時にプロパティ値を含む VARIANT 構造をポイントします|  

### <a name="table-25-hresult-getproperty-result"></a>表 25 HRESULT GetProperty 結果  

|**HRESULT**|**説明**|  
|-|-|  
|**S_OK**|プロパティ値が取得されました。|  
|**WBEM_E_NOT_FOUND**|その名前を持つプロパティはありません。|  
|**E_NOT_VALID_STATE**|現在のレコードが存在しません。|  

> [!NOTE]
>  **GetProperty** メソッドは、表 25 に一覧表示されている以外の WMI エラー コードを返すことができます。 一覧表示されている値は、返される一般的な結果です。  

#### <a name="iwmirepository-interface"></a>IWmiRepository インターフェイス  

```  
__interface IWmiRepository : IUnknown  
{  
    HRESULT SetNamespace(LPCWSTR namespaceName);  
    HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、**WmiRepository** コンポーネント (**ID_WmiRepository**) によって実装されます。  

##### <a name="hresult-setnamespacelpcwstr-namespacename"></a>HRESULT SetNamespace(LPCWSTR namespaceName)  
 このメソッドは、クエリに使用される WMI 名前空間を設定します。 **ExecQuery** を呼び出す前に、このメソッドを呼び出します。 このメソッドを呼び出さない場合、名前空間は root\cimv2 になります。 このメソッドは常に **S_OK** を返します。  

##### <a name="hresult-execquerylpcwstr-query-out-iwmiiterator-ppiterator"></a>HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator)  
 表 26 および表 27 で示されているように、**SetNamespace** への呼び出しで設定された WMI 名前空間に対してクエリを実行します。  

### <a name="table-26-hresult-execquery"></a>表 26 HRESULT ExecQuery  

|**パラメーター**|**説明**|  
|-|-|  
|**Query**|実行する WMI クエリの文字列|  
|**ppIterator**|戻り時にインターフェイスで入力されるインターフェイス ポインターにポインターを渡して、クエリの結果へのアクセスを提供します|  

### <a name="table-27-hresult-query-result"></a>表 27 HRESULT クエリ結果  

|**HRESULT**|**説明**|  
|-|-|  
|**S_OK**|クエリが成功しました|  
|**その他**|クエリが成功しなかった場合、WMI **HRESULT** を返します|  

#### <a name="iformcontroller-interface"></a>IFormController インターフェイス  

```  
__interface IFormController : IUnknown  
{  
    Init(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    SetPageInfo(ISettingsProperties *pPageInfo);  

    Validate(void);  

    AddToGroup(int groupControlId, int controlId);  
    UpdateCheckGroup(int groupControlId);  
    AddValidator(int controlId, IValidator *pValidator, IControl *pCOntrol = 0);  

    AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr);  
    DisableValidation(int controlId, BOOL disable);  

    AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type);  
    AddRadioGroup(LPCWSTR groupName, int radioControlId);  
    EnableRadioGroup(LPCWSTR groupName, BOOL enable);  
    InitFields(IFieldCallback *pFieldCallback = nullptr);  
    SaveFields(IFieldCallback *pFieldCallback = nullptr);  
    BOOL IsFieldDisabled(int controlId);  

    InitSection(LPCWSTR key, LPCWSTR sectionCaption);  
    AddSummaryItem(LPCWSTR first, LPCWSTR second);  
    SuppressLogValue(LPCWSTR tsVariableName);  
    SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption);  
    LoadText(int controlId, LPCWSTR tsVariableName);  

    void ControlEvent(WORD eventId, WORD controlId);  
    BOOL IsValid(void);  
 };  
```  

##### <a name="overview"></a>概要  
 UDI ウィザードの各ページには、このインターフェイスを実装する独自のフォーム コントローラーがあります。 このコントローラーを使用して、.config XML ファイル内のフィールド データをページ上のコントロールに接続します。 こうすると、詳細の多くがフォーム コントローラーによって処理されるようになります。  

#####  <a name="SettingUptheForm"></a> フォームの設定  
 通常、フォーム コントローラーは、ページの **OnWindowCreated** メソッドで設定します。 通常、これを行うには、表 28 に示されているメソッドの呼び出しが関与します。  

### <a name="table-28-onwindowcreated-method"></a>表 28 OnWindowCreated メソッド  

|**方法**|**説明**|  
|-|-|  
|**Init**|フォーム コントローラーを初期化します|  
|**AddField**|文字列名である .config XML ファイル内のフィールドと、ID であるページのダイアログ ボックス内のコントロール間の接続を提供します|  
|**AddRadioGroup**|ラジオ ボタンをダイアログ ボックス内のグループとコントロールの両方に接続するために使用されます|  
|**AddToGroup**|"子" コントロールを、その親とともに、または選択されているラジオ ボタンに基づいて有効または無効にすることができます|  
|**InitFields**|すべての **Add** メソッドを呼び出した後に呼び出して、フォームを設定します|  
|**Validate**|最初の検証を実行します|  

##### <a name="processing-form-events"></a>フォーム イベントの処理  
 次の呼び出しを **OnControlEvent** メソッドに追加します。  

```  
Form()->ControlEvent(eventId, controlId);  
```  

 この呼び出しは、フォーム コントローラーがフォームに関連するイベントを処理できるように、イベントを渡します。  

##### <a name="save-form-data"></a>フォーム データを保存する  
 **OnNextClicked** メソッドで、表 29 に示されているフォーム メソッドを呼び出します。  

### <a name="table-29-onnextclicked-method"></a>表 29 OnNextClicked メソッド  

|**方法**|**説明**|  
|-|-|  
|**InitSection**|このページの **[概要]** ページに表示されるセクションの名前を提供します|  
|**SaveFields**|フィールドの値をタスク シーケンス変数と **[概要]** ページに保存します|  

#####  <a name="Init"></a> Init  

```  
HRESULT Init(IWizardPageView *pView, IWizardPageContainer *pContainer)  
```  

 通常、このメソッドは、ページの **OnWindowCreated** メソッドの開始付近で呼び出します。 コマンドは、次のようになります。  

```  
Form()->Init(View(), Container());  
```  

##### <a name="setpageinfo"></a>SetPageInfo  

```  
HRESULT SetPageInfo(ISettingsProperties *pPageInfo)  
```  

 このメソッドは内部的に呼び出されるため、自分で呼び出す必要はありません。 このメソッドはページの XML をフォーム コントローラーに提供します。  

##### <a name="validate"></a>Validate  

```  
HRESULT Validate(void)  
```  

 このメソッドは、コントロールにアタッチされているすべての検証コントロールを実行します。 検証コントロールが失敗する場合、フォーム コントローラーによって警告メッセージが表示され、**[次へ]** ボタンが無効になり、検証コントロールの処理が停止されます。 通常、このメソッドは、**OnWindowCreated** メソッドの終了時に呼び出すだけで十分です。このメソッドは常に **S_OK** を返します。  

##### <a name="addtogroup"></a>AddToGroup  

```  
AddToGroup(int groupControlId, int controlId)  
```  

 このメソッドは、表 30 に示されているように、チェック ボックスまたはラジオ ボタンの "子" としてコントロールを追加します。 このような子コントロールはすべて、親コントロールが選択されていない場合は無効になります。 このメソッドは常に **S_OK** を返します。  

### <a name="table-30-addtogroup"></a>表 30 AddToGroup  

|**パラメーター**|**説明**|  
|-|-|  
|**groupControlId**|子コントロールの有効化状態を制御するチェック ボックスまたはラジオ ボタンの ID|  
|**Controlld**|子として追加するコントロールの ID|  

##### <a name="updatecheckgroup"></a>UpdateCheckGroup  

```  
HRESULT UpdateCheckGroup(int groupControlId)  
```  

 このメソッドは、親コントロールの状態に基づいて、グループの子コントロールの有効化状態または無効化状態を更新します。 通常、このメソッドはフォーム コントローラーによって呼び出されるため、自分で呼び出す必要はありません。  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, IValidator *pValidator, IControl *pControl = 0)  
```  

 このメソッドは、XML ではなく、コードで作成する検証コントロールがある場合にのみ呼び出します。 このメソッドは常に **S_OK** を返します。  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr)  
```  

 このメソッドは、XML ではなく、コードで作成する検証コントロールがある場合にのみ呼び出します。  

##### <a name="disablevalidation"></a>DisableValidation  

```  
HRESULT DisableValidation(int controlId, BOOL disable)  
```  

 表 31 に示されているように、このメソッドを呼び出してコントロールの検証コントロールを明示的に無効化するか、通常の検証を復元します。 このメソッドは、たとえば、フォーム検証でカバーされていないコントロールのルールを有効または無効にする場合や、コントロールの検証を無効にする必要がある場合に役立ちます。 つまり、通常はこのメソッドを呼び出すことはありません。 このメソッドは常に **S_OK** を返します。  

### <a name="table-31-hresult-disablevalidation"></a>表 31 HRESULT DisableValidation  

|**パラメーター**|**説明**|  
|-|-|  
|**controlId**|検証を有効または無効にするコントロール|  
|**無効化**|検証を無効にするには TRUE、通常の検証を復元するには FALSE に設定します。|  

#####  <a name="AddField"></a> AddField  

```  
HRESULT AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type)  
```  

 表 32 に示されているように、.config XML ファイルの **Field** 要素内の名前と、ページのダイアログ ボックス内のコントロール ID 間のコントロール マッピングを追加します。 **InitFields** はこの情報を使用するため、**InitFields** を呼び出してからこのメソッドを呼び出す必要があります。 このメソッドは常に **S_OK** を返します。  

### <a name="table-32-hresult-addfield"></a>表 32 HRESULT AddField  

|**パラメーター**|**説明**|  
|-|-|  
|**Fieldname**|ページの XML に表示されるフィールドの名前|  
|**controlId**|ページのダイアログ ボックス テンプレート内のコントロールの ID|  
|**suppressLog**|このフィールドからの値をログ ファイルに書き込まない場合は TRUE に設定します。パスワードまたは PIN フィールドに対してはこのパラメーターを常に TRUE に設定します。|  
|**種類**|コントロールの型。次のいずれかになります。<br /><br /> -   **CONTROL_STATIC_TEXT**<br />-   **CONTROL_COMBO_BOX**<br />-   **CONTROL_LIST_VIEW**<br />-   **CONTROL_PROGRESS_BAR**<br />-   **CONTROL_GENERIC**<br />-   **CONTROL_RADIO_BUTTON**<br />-   **CONTROL_CHECK_BOX**<br />-   **CONTROL_TREE_VIEW**|  

#####  <a name="AddRadioGroup"></a> AddRadioGroup  

```  
HRESULT AddRadioGroup(LPCWSTR groupName, int radioControlId)  
```  

 このメソッドは、表 33 に示されているように、名前付きのラジオ ボタン グループにコントロールを追加します。 これは **InitFields** メソッドの前に呼び出す必要があります。その理由は、そのメソッドが **RadioGroup** 要素で属性を使用してグループ内のすべてのラジオ ボタン コントロールの設定を制御するからです。 ラジオ グループをロックして、たとえば、すべてのオプション ボタンを無効化するが、子コントロールは選択されているラジオ ボタンにのみ基づいて有効化または無効化されるようにすることができます。 このメソッドは常に **S_OK** を返します。  

### <a name="table-33-hresult-addradiogroup"></a>表 33 HRESULT AddRadioGroup  

|**パラメーター**|**説明**|  
|-|-|  
|**groupName**|このページでラジオ ボタンのグループを定義する文字列|  
|**radioControlId**|このグループに追加する単一のラジオ ボタンの ID|  

##### <a name="enableradiogroup"></a>EnableRadioGroup  

```  
HRESULT EnableRadioGroup(LPCWSTR groupName, BOOL enable)  
```  

 このメソッドを使用すると、ラジオ ボタン グループ全体を有効または無効にすることができます。 ラジオ グループを無効すると、グループ内のすべてのラジオ ボタン コントロールと、**AddToGroup** を使って追加されたこれらのラジオ ボタンのすべての子が無効になります。 表 34 と表 35 を参照してください。  

### <a name="table-34-enableradiogroup"></a>表 34 EnableRadioGroup  

|**パラメーター**|**説明**|  
|-|-|  
|**groupName**|**AddRadioGroup** の呼び出しで既に定義したラジオ ボタン グループの名前|  
|**有効化**|ラジオ ボタン グループを有効にするには TRUE に設定し、グループを無効にするには FALSE を設定します|  

### <a name="table-35-hresult-enableradiogroup"></a>表 35 HRESULT EnableRadioGroup  

|**HRESULT**|**説明**|  
|-|-|  
|**S_OK**|グループは有効または無効になっています|  
|**E_INVALIDARG**|指定した名前を持つラジオ ボタン グループはありません|  

#####  <a name="InitFields"></a> InitFields  

```  
HRESULT InitFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 このメソッドを呼び出す前に、XML が制御できる各フィールドに対して **AddField** を呼び出します。 このメソッドは常に **S_OK** を返します。  

 **pFieldCallback** パラメーターは省略可能です。 指定すると、フォーム コントローラーは、**CONTROL_STATIC_TEXT** または **CONTROL_CHECK_BOX** のどちらでもないコントロールに対して **SetFieldDefault** を呼び出します。 この動作により、XML から既定値を取得して、それをコントロールで自分で設定することができます。  

#####  <a name="SaveFields"></a> SaveFields  

```  
HRESULT SaveFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 このメソッドは、フィールド値をタスク シーケンス変数と **[概要]** ページに表示される概要データに保存します。 **pFieldCallback** でポインターを提供することで、**CONTROL_STATIC_TEXT** をサポートしていないコントロールの値を保存することができますです。  

##### <a name="isfielddisabled"></a>IsFieldDisabled  

```  
BOOL IsFieldDisabled(int controlId)  
```  

 このメソッドを使用すると、フィールドが XML で無効になっているかどうかを判断することができます。  

#####  <a name="InitSection"></a> InitSection  

```  
HRESULT InitSection(LPCWSTR key, LPCWSTR sectionCaption)  
```  

 このメソッドは、表 36 に示されているように、 **[概要]** ページに表示される概要データを初期化します。 **SaveFields** を呼び出す前に、**OnNextClicked** メソッドでこのメソッドを呼び出します。 このメソッドは常に **S_OK** を返します。  

### <a name="table-36-hresult-initsection"></a>表 36 HRESULT InitSection  

|**パラメーター**|**説明**|  
|-|-|  
|**Key**|このパラメーターは、ページに一意である必要があります。 これは、各ページに独自の概要情報を持たせるために使用されます。|  
|**sectionCaption**|このページの概要情報の **[概要]** ページに表示されるヘッダー。 通常、このパラメーターの値として **DisplayName()** を使用します。|  

##### <a name="addsummaryitem"></a>AddSummaryItem  

```  
HRESULT AddSummaryItem(LPCWSTR first, LPCWSTR second)  
```  

 このメソッドを使用すると、XML で設定されたこれらの項目の他に、**[概要]** ページに概要項目を追加することができます。 表 37 を参照してください。  

### <a name="table-37-hresult-addsummaryitem"></a>表 37 HRESULT AddSummaryItem  

|**パラメーター**|**説明**|  
|-|-|  
|**First**|左側に表示される概要項目のキャプション|  
|**Second**|右側に表示される値|  

##### <a name="suppresslogvalue"></a>SuppressLogValue  

```  
HRESULT SuppressLogValue(LPCWSTR tsVariableName)  
```  

 値をログ ファイルに書き込まないタスク シーケンス変数に対してこのメソッドを呼び出します。 パスワード、PIN、またはユーザーが入力するその他の機密性の高い値を格納するタスク シーケンス変数に対してこのメソッドを呼び出します。  

##### <a name="savetext"></a>SaveText  

```  
HRESULT SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption)  
```  

 このメソッドは、テキスト コントロールの値をタスク シーケンス変数と概要セクションの両方に保存します。 通常、このメソッドは、フォーム コントローラーによってすべてのフィールドに対して呼び出されるため、自分で呼び出す必要はありません。 表 38 を参照してください。  

### <a name="table-38-hresult-savetext"></a>表 38 HRESULT SaveText  

|**パラメーター**|**説明**|  
|-|-|  
|**controlId**|保存する値 (またはテキストを返すことができるその他のコントロール) を含むテキスト ボックスの ID|  
|**tsVariableName**|変更するタスク シーケンス変数の名前|  
|**summaryCaption**|この値の **[概要]** ページのキャプション|  

##### <a name="loadtext"></a>LoadText  

```  
HRESULT LoadText(int controlId, LPCWSTR tsVariableName)  
```  

 このメソッドは、タスク シーケンス変数の値を読み取り、テキスト ボックスをこの値に設定します。  

##### <a name="controlevent"></a>ControlEvent  

```  
void ControlEvent(WORD eventId, WORD controlId)  
```  

 フォーム コントローラーが正常に機能するために実行する必要があるコントロール イベントを処理できるように、**OnControlEvent** メソッドでこのメソッドを呼び出します。 このメソッドに渡す値は、**OnControlEvent** メソッドに渡される値と同じです。  

##### <a name="isvalid"></a>IsValid  

```  
BOOL IsValid(void)  
```  

 このメソッドは、フォームの最新の検証の状態を返します。 検証コントロールのいずれかでエラーが報告された場合、このメソッドは FALSE を返します。 つまり、ページ上のすべてのコントロールが有効な場合にのみ TRUE を返します。  

#### <a name="ivalidator-interface"></a>IValidator インターフェイス  

```  
__interface IValidator : IUnknown  
{  
    HRESULT Init(IControl *pControl, LPCTSTR message);  
    HRESULT Init(IControl *pControl, IWizardPageContainer *pContainer, IStringProperties *pProperties);  
    BOOL, IsValid(LPBSTR pMessage);  
    HRESULT SetProperty(int propertyId, LPVARIANT pValue);  
    HRESULT SetProperty(int propertyId, IUnknown *pUnknown);  
    HRESULT SetProperty)(int propertyId, LPCTSTR pValue);  
};  
```  

##### <a name="overview"></a>概要  
 *検証コントロール*は、ページ上の 1 つのコントロールを検証できるコンポーネントです。 検証コントロールを実装する最も簡単な方法は、検証コントロールを BaseValidator.h ヘッダー ファイルで定義されている **BaseValidator** クラスのサブクラスにすることです。  

##### <a name="hresult-initicontrol-pcontrol-lpctstr-message"></a>HRESULT Init(IControl \*pControl, LPCTSTR message)  
 コードで検証コントロールを作成する場合は、このメソッドを呼び出して検証コントロールを初期化することができます。 表 39 を参照してください。  

### <a name="table-39-hresult-init"></a>表 39 HRESULT Init  

|**パラメーター**|**説明**|  
|-|-|  
|**pControl**|検証コントロールが検証する必要があるコントロール|  
|**Message**|コントロールが有効でない場合にページに表示するメッセージ|  

##### <a name="hresult-initicontrol-pcontrol-iwizardpagecontainer-pcontainer-istringproperties-pproperties"></a>HRESULT Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)  
 フォーム コントローラーは、このメソッドを呼び出して、ページの XML を基に作成する検証コントロールを初期化します。 表 40 を参照してください。  

### <a name="table-40-hresult-init-method"></a>表 40 HRESULT Init メソッド  

|**パラメーター**|**説明**|  
|-|-|  
|**pControl**|検証コントロールが検証する必要があるコントロール|  
|**pContainer**|検証コントロールでロガーへのアクセスが必要な場合、または他のコンポーネントを作成する必要がある場合|  
|**pProperties**|検証コントロールのプロパティ (セッター要素) へのアクセスを提供します|  

##### <a name="bool-isvalidlpbstr-pmessage"></a>BOOL, IsValid(LPBSTR pMessage)  
 このメソッドは、コントロールが有効な場合には TRUE を返し、無効な場合には FALSE を返します。 戻り時に、**pMessage** は、コントロールが無効なときに表示するメッセージを含む新しい **BSTR** で入力される必要があります。  

##### <a name="hresult-setpropertyint-propertyid-lpvariant-pvalue"></a>HRESULT SetProperty(int propertyId, LPVARIANT pValue)  
 XML で提供されていない追加の値が必要な場合に、このメソッドを実装できます。  

##### <a name="hresult-setpropertyint-propertyid-iunknown-punknown"></a>HRESULT SetProperty(int propertyId, IUnknown \*pUnknown)  
 XML で提供されていない追加の値が必要な場合に、このメソッドを実装できます。  

##### <a name="hresult-setpropertyint-propertyid-lpctstr-pvalue"></a>HRESULT SetProperty)(int propertyId, LPCTSTR pValue)  
 XML で提供されていない追加の値が必要な場合に、このメソッドを実装できます。  

#### <a name="iregex-interface"></a>IRegEx インターフェイス  

```  
__interface IRegEx : IUnknown  
{  
    BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex);  
    HRESULT GetMatch(size_t index, LPBSTR pValue);  
};  
```  

 このメソッドは、**ID_Regex** コンポーネント (IRegex.h) で実装され、正規表現処理のサポートを提供します。  

##### <a name="bool-matchesregexlpctstr-input-lpctstr-regex"></a>BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex)  
 このメソッドは、入力テキストに対して正規表現を実行します。 C++ 標準ライブラリの **regex_match** 関数を使用して実際の作業を実行します。 このメソッドは、一致が見つかった場合は TRUE を返し、それ以外の場合は FALSE を返します。  

##### <a name="hresult-getmatchsizet-index-lpbstr-pvalue"></a>HRESULT GetMatch(size_t index, LPBSTR pValue)  
 このメソッドを使用すると、最新の **MatchesRegex** の呼び出しから一致を取得できます。 このメソッドにはエラー処理がなく、**S_OK** を返すか、例外をスローすることに注意してください。  

#### <a name="isummaryinfo-interface"></a>ISummaryInfo インターフェイス  

```  
__interface ISummaryInfo : IUnknown  
{  
    size_t Count(void);  
    HRESULT Clear(void);  
    HRESULT AddInfo(LPCTSTR pFirst, LPCTSTR pSecond);  
    HRESULT GetInfo(size_t index, LPBSTR pFirst, LPBSTR pSecond);  
    HRESULT GetCaption(LPBSTR pCaption);  
    HRESULT SetCaption(LPCTSTR caption);  
};  
```  

 このインターフェイスを直接使用する必要はありません。 代わりに、**IFormController** を使用します。  

#### <a name="isummarybag"></a>ISummaryBag  

```  
__interface ISummaryBag : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetInfoByIndex(size_t index, [out] ISummaryInfo **ppSummary);  
    HRESULT GetInfoByKey(LPCTSTR key, [out] ISummaryInfo **ppSummary);  
};  
```  

 このインターフェイスを直接使用する必要はありません。 代わりに、**IFormController** を使用します。  

#### <a name="itsvariablebag-interface"></a>ITSVariableBag インターフェイス  

```  
__interface ITSVariableBag : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue);  
    void Clear(void);  
    HRESULT Remove([in] LPCTSTR variableName);  
    HRESULT SuppressLogValue([in] LPCTSTR variableName);  
    void Save(void);  
};  
```  

 このインターフェイスは、タスク シーケンス変数へのアクセスを提供します。 ページの **TSVariables()** メソッドを使用して、このインターフェイスにアクセスできます。  

##### <a name="void-getvaluein-lpctstr-variablename-out-lpbstr-pvalue"></a>void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue)  
 このメソッドは、タスク シーケンス変数の値を読み取ります。  

> [!NOTE]
>  値は、最初に読み取られてからキャッシュされます。  

##### <a name="void-setvaluein-lpctstr-variablename-in-lpctstr-pvalue"></a>void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue)  
 このメソッドは、タスク シーケンス変数の値を設定します。 この値は、メモリに保存されます。 タスク シーケンス値は、UDI ウィザードで **[完了]** をクリックすると書き込まれます。  

##### <a name="void-clearvoid"></a>void Clear(void)  
 このメソッドは、メモリに保存されているすべてのタスク シーケンス値を削除します。  

##### <a name="hresult-removein-lpctstr-variablename"></a>HRESULT Remove([in] LPCTSTR variableName)  
 このメソッドは、特定のタスク シーケンス値をメモリから削除します。 同じタスク シーケンス名を使用して次に **GetValue** を呼び出したときに、メソッドはタスク シーケンスから値を取得します。  

##### <a name="hresult-suppresslogvaluein-lpctstr-variablename"></a>HRESULT SuppressLogValue([in] LPCTSTR variableName)  
 UDI ウィザードで **[完了]** をクリックしたときなど、タスク シーケンス変数が書き込まれるときは常に、名前と値がログ ファイルに書き込まれます。 特定のタスク シーケンス変数の機密性の高い値 (パスワードや PIN など) のログへの記録を抑制するには、このメソッドを呼び出します。  

##### <a name="void-savevoid"></a>void Save(void)  
 このメソッドは、**SetValue** への呼び出しで設定されているすべてのタスク シーケンス値を保存します。  

#### <a name="itsvariablerepository-interface"></a>ITSVariableRepository インターフェイス  

```  
__interface ITSVariableRepository : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, BOOL logValue, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, BOOL logValue, [in] LPCTSTR value);  
};  
```  

 このインターフェイスは、タスク シーケンス変数の読み書きのため、**TSVariableBag** によって内部的に使用されます。  

#### <a name="iwizardfinish-interface"></a>IWizardFinish インターフェイス  

```  
__interface IWizardFinish : IUnknown  
{  
    HRESULT Canceled(void);  
    HRESULT Finished(void);  
};  
```  

 このインターフェイスは、UDI ウィザードで **[完了]** または **[キャンセル]** をクリックしたときに追加の処理を実行する高度なシナリオで役立ちます。 UDI ウィザードには、**[完了]** をクリックしたときにタスク シーケンス変数を保存する**完了**タスクが含まれています。 ウィザードをキャンセルすると、このタスクは **OSDSetupWizCancelled** タスク シーケンス変数を TRUE に設定するだけで、他のタスク シーケンス変数への変更は保存しません。  

 独自の完了コンポーネントを作成する場合は、次のようなコードを使用して登録する必要があります。  

```  
Register<MyFinishTaskFactory>(ID_MyFinishTask, pRegistry);  

PWizardFinish pFinish;  
CreateInstance(pRegistry, ID_MyFinishTask, &pFinish);  

PWizardFinishService pService;  
GetService<IWizardFinishService>(pRegistry, &pService);  

pService->Register(pFinish);  
```  

#### <a name="ibindablelist-interface"></a>IBindableList インターフェイス  

```  
__interface IBindableList : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetCaption(size_t index, LPBSTR pCaption);  
};  
```  

 コンボ ボックスにバインドするデータ ソース コンポーネントがある場合は、その **Bind** メソッドを呼び出すことでこのインターフェイスを実装します。  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 このメソッドは、リスト内の項目の数を返します。  

##### <a name="hresult-getcaptionsizet-index-lpbstr-pcaption"></a>HRESULT GetCaption(size_t index, LPBSTR pCaption)  
 このメソッドは、特定のインデックス位置にある項目のキャプションを返します。  

#### <a name="idatanodes-interface"></a>IDataNodes インターフェイス  

```  
__interface IDataNodes : IUnknown  
{  
    size_t Count();  
    HRESULT SetCaptionProperty(LPCTSTR captionProperty);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue);  
    HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode);  
};  
```  

 このインターフェイスは、ページに保存できる階層データへのアクセスを提供します。 このインターフェイスは、**Settings** メソッドを使用してページで使用できる **ISettingsProperties** インターフェイス上でメソッドを使用して取得します。  

 ページの XML 内のデータは次のようになります。  

```  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  
```  

 **Settings()->GetDataNode(L"Network", &pData)** を呼び出すことで、2 つのデータ項目を持つ (それぞれが 2 つのプロパティを持つ) **IDataNodes** インスタンスが提供されます。  

##### <a name="sizet-count"></a>size_t Count()  
 このメソッドは、**DataItem** 要素の数を返します。  

##### <a name="hresult-setcaptionpropertylpctstr-captionproperty"></a>HRESULT SetCaptionProperty(LPCTSTR captionProperty)  
 このインターフェイスをサポートするコンポーネントは、**IBindableList** もサポートします。これは、ページの XML のデータを使用してコンボ ボックスへの入力を容易にします。 このメソッドは、各 **DataItem** 要素内のどのプロパティ (セッター) をこのバインドに使用するかを制御します。 たとえば、**DisplayName** を使用してこのメソッドを呼び出し、メソッドはそのセッター プロパティをデータ バインディングに使用することができます。 その後、コンボ ボックスに **Public** と **Dev Team** が項目として含まれるようになります。  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-out-lpbstr-propertyvalue"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue)  
 このメソッドは、**DataItem** 要素のいずれかからプロパティを取得します。 表 41 と表 42 を参照してください。  

### <a name="table-41-dataitem-getproperty"></a>表 41 DataItem GetProperty  

|**パラメーター**|**説明**|  
|-|-|  
|**Index**|プロパティ値を取得する **DataItem** の (0 から始まる) インデックス値|  
|**propertyName**|値を取得するセッター プロパティの名前|  
|**propertyValue**|戻り時に、プロパティの文字列値が含まれます|  

### <a name="table-42-hresult-getproperty"></a>表 42 HRESULT GetProperty  

|||  
|-|-|  
|**HRESULT**|**説明**|  
|**S_OK**|プロパティが取得されました。|  
|**E_INVALIDARG**|インデックスが配列の末尾を超えました。|  

##### <a name="hresult-getnodesizet-index-out-isettingsproperties-ppnode"></a>HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode)  
 このメソッドは、**GetProperty** と似ていますが、**DataItem** から 1 つの値を返す代わりに、**ISettingsProperties** インターフェイスでラップされた **DataItem** 全体を返します。 表 43 と表 44 を参照してください。  

### <a name="table-43-hresult-getnode"></a>表 43 HRESULT GetNode  

|**パラメーター**|**説明**|  
|-|-|  
|インデックス|プロパティ値を取得する **DataItem** の (0 から始まる) インデックス値|  
|**ppNode**|終了時に、**DataItem** ノードをラップする **ISettingsProperties** インターフェイス|  

### <a name="table-44-hresult-getnode-results"></a>表 44 HRESULT GetNode Results  

|**HRESULT**|**説明**|  
|-|-|  
|**S_OK**|ノードが取得されました。|  
|**E_INVALIDARG**|インデックスが配列の末尾を超えました。|  

#### <a name="ifactoryregistry-interface"></a>IFactoryRegistry インターフェイス  

```  
__interface IFactoryRegistry : IUnknown  
{  
    void Register(LPCTSTR type,  IClassFactory *pFactory);  
    HRESULT LoadAndRegister(LPCTSTR dllName, ILogger *pLogger);  
    BOOL Contains(LPCTSTR type);  
    HRESULT GetFactory(LPCTSTR type,  IClassFactory **ppFactory);  
    HRESULT CreateInstance(LPCTSTR type,  IUnknown **ppInstance);  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
    HRESULT RegisterService(REFGUID iid, IUnknown *pService);  
    HRESULT GetService(REFGUID iid,  IUnknown **ppService);  
};  
```  

##### <a name="overview"></a>概要  
 新しいカスタム ページを作成するときに、少なくとも*ページ ファクトリ* (**IClassFactory** を実装するクラス) を作成する必要があります  (**ClassFactoryImpl** を自分のファクトリの基底クラスとして使用することができます)。  

##### <a name="void-registerlpctstr-type--iclassfactory-pfactory"></a>void Register(LPCTSTR type,  IClassFactory \*pFactory)  
 このメソッドは、クラス ファクトリをレジストリに登録します。 表 45 を参照してください。  

### <a name="table-45-iclassfactory-void-register"></a>表 45 IClassFactory void Register  

|**パラメーター**|**説明**|  
|-|-|  
|**種類**|登録するファクトリを識別する文字列。一般的に、一意にするために、このパラメーターに自分の会社名を文字列に含める必要があります。|  
|**pFactory**|クラス ファクトリ インスタンスへのポインター|  

##### <a name="hresult-loadandregisterlpctstr-dllname-ilogger-plogger"></a>HRESULT LoadAndRegister(LPCTSTR dllName, ILogger \*pLogger)  
 このメソッドは内部でのみ使用されます。  

##### <a name="bool-containslpctstr-type"></a>BOOL Contains(LPCTSTR type)  
 このメソッドは通常、内部で使用されます。 クラス ファクトリが型に登録されているかどうかを確認します。  

##### <a name="hresult-getfactorylpctstr-type--iclassfactory-ppfactory"></a>HRESULT GetFactory(LPCTSTR type,  IClassFactory **ppFactory)  
 このメソッドを使用すると、クラス ファクトリを取得することができます。 通常、**CreateInstance** を呼び出します。 ただし、同じコンポーネントを大量に作成する場合は、ファクトリを取得してから、インスタンスを作成するように指示する方がより効率的です。  

##### <a name="hresult-createinstancelpctstr-type--iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type,  IUnknown **ppInstance)  
 このメソッドは、その型を考慮して、コンポーネントの新しいインスタンスを作成します。 代わりに、タイプ セーフ オブジェクトを作成できる **CreateInstance** テンプレート メソッドを使用します。  

##### <a name="hresult-setcontaineriwizardpagecontainer-pcontainer"></a>HRESULT SetContainer(IWizardPageContainer \*pContainer)  
 このメソッドは内部でのみ使用されます。  

##### <a name="hresult-registerservicerefguid-iid-iunknown-pservice"></a>HRESULT RegisterService(REFGUID iid, IUnknown \*pService)  
 *サービス*は、複数の場所で使用できるコンポーネントの 1 つのインスタンスです。 このメソッドを使用して 1 つのページでサービスを登録してから、別のページからその同じインスタンスを取得できます。  

##### <a name="hresult-getservicerefguid-iid--iunknown-ppservice"></a>HRESULT GetService(REFGUID iid,  IUnknown **ppService)  
 このメソッドは、以前に RegisterService への呼び出しに登録されたサービスを取得します。  

##### <a name="hresult-setlanguagelangid-languageid"></a>HRESULT SetLanguage(LANGID languageId)  
 このメソッドは、UDI ウィザードの言語を **languageId** パラメーターで指定した言語識別子に設定します。  

##### <a name="langid-getlanguage"></a>LANGID GetLanguage()  
 このメソッドは、UDI ウィザードの **/locale** コマンド ライン パラメーターで指定された言語識別子の値を返します。 このメソッドは、次のいずれかの値を返します。  

-   **/locale** コマンド ライン パラメーターで指定された言語識別子の値  

-   **/locale** コマンド ライン パラメーターを指定しなかった場合は 0  

#### <a name="ilogger-interface"></a>ILogger インターフェイス  

```  
__interface ILogger : IUnknown  
{  
    HRESULT Init(LPCWSTR logFilename);  
    HRESULT MoveLog(LPCWSTR logFilename);  
    HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message);  
    HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message);  
    HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message);  
    HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Normal(LPCTSTR component, LPCTSTR message);      
    HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Verbose(LPCTSTR component, LPCTSTR message);  
    HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Debug(LPCWSTR component, LPCWSTR message);  
    HRESULT EnableDebug(BOOL debug);  
    HRESULT Close(void);  
    HRESULT GetLogFilename(LPBSTR pFilename);  
};  
```  

##### <a name="overview"></a>概要  
 UDI ウィザードは、情報をログ ファイルに記録します。これはフィールドで検出された問題のトラブルシューティングに役立ちます。 ページで情報をログに記録することをお勧めします。 このインターフェイスへのポインターは、ページ内からページの **Logger()** メソッドを使用して取得できます。 ログ ファイル内の行には、エラー、通常、詳細、またはデバッグ メッセージを表す "レベル" 番号が含まれます。  

> [!NOTE]
>  デバッグ サポートをオンにしない限り、デバッグ メッセージはログ ファイルに保存されません。 デバッグ サポートをオンにするには、次の行を .config ファイル内の **Style** 要素に追加します。  

```  
<Setter Property="debug">true</Setter>  
```  

##### <a name="init"></a>初期状態  

```  
HRESULT Init(LPCWSTR logFilename)  
```  

 このメソッドは内部でのみ使用されます。  

##### <a name="movelog"></a>MoveLog  

```  
HRESULT MoveLog(LPCWSTR logFilename)  
```  

 このメソッドは内部でのみ使用されます。  

##### <a name="logbase"></a>LogBase  

```  
HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message)  
```  

 このメソッドは内部でのみ使用されます。  

##### <a name="log"></a>ログ  

```  
HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message)  
```  

 このメソッドは内部でのみ使用されます。  

##### <a name="error"></a>エラー  

```  
HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message)  
```  

 エラーに関する情報を記録するには、このメソッドを呼び出します。 表 46 を参照してください。  

### <a name="table-46-hresult-error"></a>表 46 HRESULT Error  

|**パラメーター**|**説明**|  
|-|-|  
|**エラー**|呼び出しで返されたエラー コード (このコードは数値としてログ エントリに表示されます)。|  
|**コンポーネント**|エラーの原因を特定する文字列。通常は、記述したページまたはコンポーネントです。|  
|**Message**|エラーの原因を説明するメッセージ|  

#####  <a name="Error2"></a> Error2  

```  
HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 このメソッドは **Error** メソッドに似ていますが、2 つの部分から成るメッセージを提供できます。 最後のメッセージの出力ファイルには、"message" と “message2” が含まれます。 これは、とても便利なメソッドです。  

##### <a name="normal"></a>標準  

```  
HRESULT Normal(LPCTSTR component, LPCTSTR message)  
```  

 このメソッドは、通常のメッセージを記録します。 パラメーターの [Error](#Error) メソッドの説明を参照してください。  

##### <a name="normal2"></a>Normal2  

```  
HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 このメソッドは、通常のメッセージを記録します。 パラメーターの [Error2](#Error2) メソッドの説明を参照してください。  

##### <a name="verbose"></a>詳細  

```  
HRESULT Verbose(LPCTSTR component, LPCTSTR message)  
```  

 このメソッドは、詳細メッセージを記録します。 パラメーターの [Error](#Error) メソッドの説明を参照してください。  

##### <a name="verbose2"></a>Verbose2  

```  
HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 このメソッドは、詳細メッセージを記録します。 パラメーターの [Error2](#Error2) メソッドの説明を参照してください。  

##### <a name="debug"></a>デバッグ  

```  
HRESULT Debug(LPCWSTR component, LPCWSTR message)  
```  

 このメソッドは、デバッグ メッセージを記録します。 パラメーターの [Error](#Error) メソッドの説明を参照してください。 デバッグ メッセージは、有効にしないとファイルに保存されません。 詳細については「概要」セクションを参照してください。  

##### <a name="enabledebug"></a>EnableDebug  

```  
HRESULT EnableDebug(BOOL debug)  
```  

 このメソッドは内部でのみ使用されます。  

##### <a name="close"></a>閉じる  

```  
HRESULT Close(void)  
```  

 このメソッドは内部でのみ使用されます。  

##### <a name="getlogfilename"></a>GetLogFilename  

```  
HRESULT GetLogFilename(LPBSTR pFilename)  
```  

 このメソッドは、ログ ファイルの名前を取得します。  

#### <a name="iorientation-interface"></a>IOrientation インターフェイス  

```  
__interface IOrientation : IUnknown  
{  
    void SetController(IWizardDialogController *pController);  
    int AddPage(LPCTSTR name);  
    void SelectPage(int index);  
};  
```  

 このインターフェイスは内部でのみ使用されます。  

#### <a name="isettings-interface"></a>ISettings インターフェイス  

```  
__interface ISettings : IUnknown  
{  
    int NumDlls();  
    int NumPages();  

    HRESULT SetStage(LPCWSTR stageName);  
    HRESULT GetDllName(long index, __out LPBSTR pDllName);  
    HRESULT GetPageInfo(long index, __out ISettingsProperties **ppPageInfo);  
    HRESULT GetStyle(__out ISettingsProperties **ppStyleInfo);  
};  
```  

 このインターフェイスは内部でのみ使用されます。  

#### <a name="isettingsproperties-interface"></a>ISettingsProperties インターフェイス  

```  
__interface ISettingsProperties : IUnknown  
{  
    HRESULT GetAttribute(LPCTSTR attributeName, __out LPBSTR attributeValue);  
    IStringProperties * Properties();  
   RESULT SelectNodes(LPCTSTR xPath, __out IXMLDOMNodeList **ppList);  
    HRESULT SelectSingleNode(LPCTSTR xPath, __out IXMLDOMNode **ppNode);  
    HRESULT GetDataNode(LPCTSTR name, __out ISettingsProperties **ppNode);  
    HRESULT GetDataNodes(__out IDataNodes **ppNodes);  
    HRESULT GetChildDataNodes(LPCTSTR childeName, __out IDataNodes **ppNodes);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、ページ データへのアクセスを提供します。 ページ データの最上位レベルに到達するには、ページの **Settings()** メソッドを使用します。  

##### <a name="hresult-getattributelpctstr-attributename--lpbstr-attributevalue"></a>HRESULT GetAttribute(LPCTSTR attributeName,  LPBSTR attributeValue)  
 このメソッドを使用すると、メイン ノードにある属性の値を取得することができます。メイン ノードは、ページの **Settings()** メソッドを使用している場合の **Page** ノードです。  

##### <a name="istringproperties--properties"></a>IStringProperties * Properties()  
 このメソッドは、メイン ノードの下のセッター プロパティ値へのアクセスを提供します。 ページの場合、これらは最上位プロパティです。  

##### <a name="hresult-selectnodeslpctstr-xpath--ixmldomnodelist-pplist"></a>HRESULT SelectNodes(LPCTSTR xPath,  IXMLDOMNodeList **ppList)  
 XPath 式を使用して XML ノードのリストを直接取得する場合は、このメソッドを呼び出します。 可能な場合は、他のメソッドのいずれかを使用することをお勧めします。 このメソッドは、他の方法でノードにアクセスできない場合にのみ使用します。  

##### <a name="hresult-selectsinglenodelpctstr-xpath--ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xPath,  IXMLDOMNode **ppNode)  
 XPath 式を使用して 1 つの XML ノードを直接取得する場合は、このメソッドを呼び出します。 可能な場合は、他のメソッドのいずれかを使用することをお勧めします。 このメソッドは、他の方法でノードにアクセスできない場合にのみ使用します。  

##### <a name="hresult-getdatanodelpctstr-name--isettingsproperties-ppnode"></a>HRESULT GetDataNode(LPCTSTR name,  ISettingsProperties **ppNode)  
 **Data** 要素をその要素の **Name** 属性に基づいて取得します。  

##### <a name="hresult-getdatanodesidatanodes-ppnodes"></a>HRESULT GetDataNodes(IDataNodes **ppNodes)  
 このメソッドは、現在のノードの下の **DataItem** 要素のリストを取得します。 ページ レベルから **GetDataNode** を呼び出して、データの **ISettingsProperty** インターフェイスを取得します。 次に、そのインスタンスで、**GetDataNodes** を呼び出してレコードのリストを取得します。 この XML を前提とした例を示します。  

```  
    <Page …>  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  

PSettingsProperties pData;  
Settings()->GetDataNode(L"Network", &pData);  
PDataNodes pNodes;  
pData->GetDataNodes(&pNodes);  
```  

##### <a name="hresult-getchilddatanodeslpctstr-childename--idatanodes-ppnodes"></a>HRESULT GetChildDataNodes(LPCTSTR childeName,  IDataNodes **ppNodes)  
 このメソッドは、特定の **Data** ノード下の **DataItem** ノードのセットに到達するための簡単な方法を提供します。 **GetDataNodes** の例から XML を使用すると、次のコードは、**GetDataNodes** の下の例の 4 行のコードとまったく同じことを行いますが、エラーをチェックします。  

```  
ISimpleStringProperties Interface  
```  

#### <a name="isimplestringproperties-interface"></a>ISimpleStringProperties インターフェイス  

```  
__interface ISimpleStringProperties : IStringProperties  
{  
void Add(LPCTSTR propertyName, LPCTSTR value);  
};  
```  

 このインターフェイスは、それ自体では役に立ちません。 しかし、**ID_SimpleStringProperties** コンポーネントによって実装されます。このコンポーネントは、**IStringProperties** インターフェイスも実装します。 プロパティのセットをタスクなどの別のコンポーネントに渡す必要があるが、XML からの値を使用せずにプログラムで値を追加する場合は、このコンポーネントを使用できます。 このインターフェイスの使用例を次に示します。  

```  
PSimpleStringProperties *pProperties;  
CreateInstance(Container(), ID_SimpleStringProperties, &pProperties);  
pProperties->Add(L"filename", L"%windir%\\system32\\cscript.exe");  
pTask->Init(pProperties, nullptr);  
IStringProperties  
__interface IStringProperties : IUnknown  
{  
    HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue);  
};  
```  

 このインターフェイスは、XML に由来する一連のセッター要素への単純なアクセスを提供します。 このインターフェイスは、**Settings()->Properties()** を使用してページのプロパティに使用できます。  

##### <a name="hresult-getlpctstr-propertyname-out-lpbstr-ppropvalue"></a>HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue)  
 このメソッドは、1 つのプロパティ値を取得します。 表 47 と表 48 を参照してください。  

### <a name="table-47-ihresult-get-property-value"></a>表 47 IHRESULT Get プロパティ値  

|**パラメーター**|**説明**|  
|-|-|  
|**propertyName**|読み取るプロパティの名前|  
|**pPropValue**|終了時に、文字列としてプロパティ値が含まれます (このようなプロパティが存在しない場合は、この値は **nullptr** になります)。|  

### <a name="table-48-ihresult-get-property-value-results"></a>表 48 IHRESULT Get プロパティ値の結果  

|||  
|-|-|  
|**HRESULT**|**説明**|  
|**S_OK**|プロパティ値が取得されました。|  
|**E_INVALIDARG**|指定した名前を持つプロパティはありません。|  

#### <a name="itaskmanager-interface"></a>ITaskManager インターフェイス  

```  
__interface ITaskManager : IUnknown  
{  
    HRESULT Init(IWizardPageView *pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties *pPageInfo, ITaskManagerCallback *pCallback);  
    HRESULT SetFailMessage(LPCWSTR message);  

    HRESULT Start(void);  

    HRESULT GetTaskMessage(size_t index, LPBSTR message);  
    HRESULT GetResultType)(size_t index, LPBSTR type);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value);  
    int GetSelectedIndex(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    size_t FailedCount(void);  
    size_t WarningCount(void);  
    size_t SucceedCount(void);  
    size_t RunningCount(void);  

    void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo);  
    void OnControlEvent(WORD eventId, WORD controlId);  
    void EnableButtons(BOOL enable);  
}  
```  

 このインターフェイスは、プレフライト ページでタスクを実行する、**TaskManager** コンポーネント (ITaskManager.h 内の **ID_TaskManager**) によって実装されます。 プレフライト ページを直接使用する (ほとんどの場合はこの方法を使用します) か、独自のページをビルドして、このコンポーネントにほとんどの作業を実行させることができます。  

##### <a name="hresult-initiwizardpageview-ppageview-int-idlistview-int-idmessage-int-idretrybutton-isettingsproperties-ppageinfo-itaskmanagercallback-pcallback"></a>HRESULT Init(IWizardPageView \*pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties \*pPageInfo, ITaskManagerCallback \*pCallback)  
 他のメソッドを呼び出す前に、このメソッドを呼び出す必要があります。 これは **TaskManager** コンポーネントを初期化します。 表 49 を参照してください。  

### <a name="table-49-hresult-init"></a>表 49 HRESULT Init  

|**パラメーター**|**説明**|  
|-|-|  
|**pPageView**|タスクを実行するページへのアクセスを提供します (このページには、次のいくつかのパラメーターで参照されるコントロールの特定のセットが必要です)。|  
|**idListView**|タスクと、それらのタスクの状態のリストを表示する **ListView** コントロールのコントロール ID|  
|**idMessage**|選択したタスクのメッセージを表示するために使用されるテキスト ボックスのコントロール ID|  
|**idRetryButton**|クリックするとタスクを再実行できるボタンのコントロール ID|  
|**pPageInfo**|ページの XML のラッパー (**TaskManager** はこの XML から実行する一連のタスクを読み込みます)。|  
|**pCallback**|null にすることができます (このパラメーターが null ではない場合、**TaskManager** はタスクを開始するときに **Started** メソッドを呼び出し、実行が完了した各タスクに対して **Finished** メソッドを呼び出します)。|  

##### <a name="hresult-setfailmessagelpcwstr-message"></a>HRESULT SetFailMessage(LPCWSTR message)  
 このメソッドは、1 つ以上のタスクが失敗した場合に表示されるメッセージを設定します。  

##### <a name="hresult-startvoid"></a>HRESULT Start(void)  
 このメソッドは、すべてのタスクを開始します。 タスクはそれぞれ別のスレッドで開始されます。  

##### <a name="hresult-gettaskmessagesizet-index-lpbstr-message"></a>HRESULT GetTaskMessage(size_t index, LPBSTR message)  
 このメソッドは内部でのみ使用されます。 タスク リスト内のタスクのインデックスに基づいて、タスクの現在のメッセージを取得します。  

##### <a name="hresult-getresulttypesizet-index-lpbstr-type"></a>HRESULT GetResultType)(size_t index, LPBSTR type)  
 このメソッドは、現在のタスクの "型" を取得します。 使用可能な型を表 50 に示します。  

### <a name="table-50-hresult-getresulttype"></a>表 50 HRESULT GetResultType  

|**種類**|**説明**|  
|-|-|  
|**0**|成功したタスクを表します|  
|**1**|警告が返されたタスクを表します|  
|**-1**|失敗したタスクを表します|  

 型は、タスクの終了コードまたはエラー コードを見て、タスクの <ExitCodes\> XML 要素内の一致を検索することで取得されます。  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-lpbstr-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value)  
 このメソッドは、強調表示するタスクのメッセージの横にイメージを表示できるように、**BitmapFilename** セッター プロパティを取得するために進行状況ページとプレフライト ページで使用されます。 つまり、カスタム セッターをタスクの XML に追加した後に、このメソッドを使用してそれを取得できます。  

##### <a name="int-getselectedindexvoid"></a>int GetSelectedIndex(void)  
 このメソッドは、現在選択されているタスクのインデックスを取得します。これは、タスクに関する追加情報を取得して (**GetProperty** メソッドを参照)、選択したタスクに表示する場合に便利です。 進行状況ページとプレフライト ページでは、このメソッドを使用して選択したタスクのイメージを表示します。  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 このメソッドは、単体テストが終了する前にタスクが完了することを保証できるため、主に単体テストで役立ちます。 通常はこのメソッドを呼び出すことはありません。 すべてのタスクの実行が完了するか、待機時間が経過すると制御が戻ります。  

##### <a name="sizet-failedcountvoid"></a>size_t FailedCount(void)  
 このメソッドは、現在失敗としてマークされているタスクの数を返します。  

##### <a name="sizet-warningcountvoid"></a>size_t WarningCount(void)  
 このメソッドは、現在警告としてマークされているタスクの数を返します。  

##### <a name="sizet-succeedcountvoid"></a>size_t SucceedCount(void)  
 このメソッドは、現在成功としてマークされているタスクの数を返します。  

##### <a name="sizet-runningcountvoid"></a>size_t RunningCount(void)  
 このメソッドは、現在実行中のタスクの数を返します。  

##### <a name="void-oncommoncontroleventword-controlid-lpnmhdr-pinfo"></a>void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo)  
 **TaskManager** が必要なイベントを処理できるように、ページの **OnCommonControlEvent** からこのメソッドを呼び出します。  

##### <a name="void-oncontroleventword-eventid-word-controlid"></a>void OnControlEvent(WORD eventId, WORD controlId)  
 **TaskManager** が必要なイベントを処理できるように、ページの **OnControlEvent** からこのメソッドを呼び出します。  

##### <a name="void-enablebuttonsbool-enable"></a>void EnableButtons(BOOL enable)  
 このメソッドは内部でのみ使用されます。  

#### <a name="iwizardcomponent-interface"></a>IWizardComponent インターフェイス  

```  
__interface IWizardComponent : IUnknown  
{  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
};  
```  

##### <a name="overview"></a>概要  
 通常、このインターフェイスは直接実装せずに、代わりに **WizardComponent** テンプレート クラスを通じて実装します。 コンポーネントが、このインターフェイスを実装し、クラス ファクトリをレジストリに登録している場合は、コンポーネントは作成されるときに **IWizardPageContainer** インスタンスへのポインターを受け取ります。 これは、たとえば、コンポーネントで必要となる他のコンポーネントを作成するためにロガーまたはレジストリにアクセスするのに役立ちます。  

#### <a name="iwizarddialogcontroller-interface"></a>IWizardDialogController インターフェイス  

```  
__interface IWizardDialogController : IUnknown  
{  
    void Initialize(ISettings *pSettings);  
    void InitPages(void);  
    void Start();  
    void Next();  
    void Finish();  
    void Previous();  
    int NumPages();  
    void Cancel();  

    HRESULT Focus(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage();  

    void ChangePage(size_t newIndex);  
    IUnknown *CurrentPage(void);  
    HRESULT GetCurrentTitle([out, retval] LPBSTR pDisplayName);  
};  
```  

 このインターフェイスは内部でのみ使用されます。  

#### <a name="iwizarddialogview-interface"></a>IWizardDialogView インターフェイス  

```  
__interface IWizardDialogView : IUnknown  
{  
    HRESULT LoadBannerImage(LPCTSTR bannerFilename);  
    HRESULT LoadPage(LPCTSTR pageType, ISettingsProperties *pPageSettings, IWizardPageView **view);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    HRESULT Focus(WizardButtons button);  
    void EnableFinish(BOOL isFinish);  
    void Exit(int exitCode);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
    void SetTitle(LPCTSTR title);  
    void SetPageTitle(LPCTSTR title);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    HWND GetHwnd(void);  
    void UpdateFocus(void);  
};  
```  

 このインターフェイスは内部でのみ使用されます。  

####  <a name="IWizardPageInterface"></a> IWizardPage インターフェイス  

```  
__interface IWizardPage : IUnknown  
{  
    HRESULT SetPageSettings(ISettingsProperties *pPageSettings);  
    HINSTANCE GetInstanceHandle(void);  
    int GetDialogResourceId(void);  
    void WindowCreated(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    void WindowShown(void);  
    void WindowHidden(void);  

    HRESULT NextClicked(void);  
    void ControlEvent(WORD eventId, WORD controlId);  
    void CommonControlEvent(WORD controlId, LPNMHDR pInfo, LPBOOL pCancel);  
    void UnhandledEvent(HWND hwnd, UINT message, WPARAM wParam, LPARAM lParam);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、**WizardPageImpl** によって実装されるため、通常はこのインターフェイスを自分で実装する必要はありません。 ウィザードは、カスタム ページとやり取りするときにこれらのメソッドをすべて呼び出します。  

#### <a name="iwizardpagecontainer-interface"></a>IWizardPageContainer インターフェイス  

```  
__interface IWizardPageContainer : IUnknown  
{  
    ILogger * Logger(void);  
    IPropertyBag * Properties(void);  
    HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance);  
    HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance);  
    HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest);  
    HRESULT GotoPage(LPCTSTR pageName);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    BOOL InPreview(void);  
    HWND GetHwnd(void);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、(**WizardPageImpl** により実装される) **Container** メソッドを使用してページで使用でき、ウィザードのさまざまなサービスへのアクセスを提供します。  

##### <a name="ilogger--loggervoid"></a>ILogger * Logger(void)  
 ログ ファイルにメッセージを書き込むには、このメソッドを使用します。次に例を示します。  

```  
Logger()->Verbose(s_component, L"Message for log file");  
```  

##### <a name="ipropertybag--propertiesvoid"></a>IPropertyBag * Properties(void)  
 このメソッドは、"メモリ" 変数へのアクセスを提供します。この変数は、UDI ウィザードの実行中にのみメモリ内にあるプロパティです。 これらのプロパティは、**$memoryVarName$** 構文を使用して、コードまたは XML で他のページで使用できます。  

##### <a name="hresult-createinstancelpctstr-type-out-iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance)  
 このメソッドを使用すると、登録されている任意のコンポーネントの新しいインスタンスを作成することができます。 ただし、テンプレート関数 **CreateInstance** は厳密に型指定されているため、こちらの方を使用することをお勧めします。  

##### <a name="hresult-getservicerefiid-iid-out-iunknown-ppinstance"></a>HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance)  
 このメソッドを使用すると、登録されているサービスを取得することができます。 ただし、(**IUnknown** を使用せずに) 厳密に型指定されている **GetService** テンプレート関数を使用することをお勧めします。  

##### <a name="hresult-replacevariableslpctstr-source-out-lpbstr-pdest"></a>HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest)  
 このメソッドは、文字列値の内部で変数の操作を処理します。 表 51 と表 52 に示されている形式がサポートされます。  

### <a name="table-51-hresult-replacevariables"></a>表 51 HRESULT ReplaceVariables  

|**形式**|**説明**|  
|-|-|  
|**$Name$**|メモリ変数の値をこの名前で置き換えます (その名前を持つメモリ変数がない場合、“トークン” は削除されます)。|  
|**%Name%**|タスク シーケンス変数または環境変数のいずれか。 順序は次のとおりです。<br /><br /> 1.タスク シーケンス変数の値を使用します (存在する場合)。<br />2.環境変数の値を使用します (存在する場合)。<br />3.それ以外の場合は、文字列からこのテキストを削除します。|  

### <a name="table-52-hresult-parameter"></a>表 52 HRESULT パラメーター  

|**パラメーター**|**説明**|  
|-|-|  
|**移行元**|入力文字列。**$** 変数と **%** 変数の任意の組み合わせを含めるか、まったく含めないこともできます。|  
|**pDest**|戻り時に、表 51 に従って置換されたすべてのトークンが入った新しい文字列が含まれます。|  

##### <a name="hresult-gotopagelpctstr-pagename"></a>HRESULT GotoPage(LPCTSTR pageName)  
 このメソッドは完全にはテストされていません。 つまり、.config XML ファイルで定義されているページの名前に基づいて、特定のページに直接切り替えることができます。 このメソッドを呼び出すと、ページ上の **OnNextClicked** がバイパスされます。 さらに、このメソッドの動作は変更される可能性があるため、自己責任で使用してください。  

##### <a name="int-showmessageboxlpctstr-message-lpctstr-lpcaption-uint-utype"></a>int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType)  
 このメソッドは、指定したテキストとキャプションを使用してメッセージ ボックスを表示します。 **uType** パラメーターは、**MessageBox** Win32 関数に指定できる任意の値です。  

##### <a name="bool-inpreviewvoid"></a>BOOL InPreview(void)  
 このメソッドは、**/preview** スイッチを指定して "プレビュー" モードでウィザードを起動した場合には TRUE を返します。 プレビュー モードでは、**[次へ]** ボタンは無効になりません。 このメソッドを使用すると、たとえば、ページに有効なデータがないと問題が発生する可能性があるコードを、プレビュー モードでバイパスすることができます。  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 このメソッドは、メイン ダイアログ ボックスに **HWND** を返します。 このメソッドは注意して使用してください。 通常、UDI ウィザード アプリケーション プログラミング インターフェイスは、ウィンドウ ハンドルを直接操作することがないように設計されています。  

#### <a name="iwizardpageview-interface"></a>IWizardPageView インターフェイス  

```  
__interface IWizardPageView : IUnknown  
{  
    HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown **ppControl);  
    HWND GetHwnd(void);  
    HWND GetControl(int itemId);  
    HRESULT Show (void);  
    HRESULT Hide(void);  
    HRESULT Focus(int itemId);  
    IWizardPage * Page(void);  
    IFormController * Form(void);  

    HRESULT FocusWizardButton(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
};  
```  

 このインターフェイスは、(**WizardPageImpl** で実装される) **View** メソッドを使用して、ページ内のコードで使用できます。  

##### <a name="hresult-getcontrolwrapperint-itemid-dialogcontroltypes-controltype-iunknown-ppcontrol"></a>HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown \*ppControl)  
 UDI ウィザードは、ページ上のコントロールとやり取りするため、実際のファサードである*ラッパー*を使用します。 実際のコントロールではなく、これらのファサードを使用すると、テストからモック ファサードを提供できるため、ページのテストを記述するのがずっと簡単になります。  

 このメソッドを直接使用する代わりに、厳密に型指定された **GetControlWrapper** テンプレート メソッドを使用することをお勧めします。次に例を示します。  

```  
PComboBox m_pLanguagePackCombo;  
GetControlWrapper(View(), IDC_MY_COMBO, CONTROL_COMBO_BOX, &m_pCombo);  
```  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 このメソッドは、ページのウィンドウ ハンドルを返します。 通常、このウィンドウ ハンドルにアクセスする必要はありません。  

##### <a name="hwnd-getcontrolint-itemid"></a>HWND GetControl(int itemId)  
 必要な場合は、このメソッドを呼び出してページ上でコントロールのウィンドウ ハンドルを取得することができます  (**GetControlWrapper** テンプレート関数を呼び出すことをお勧めします)。  

##### <a name="hresult-show-void"></a>HRESULT Show (void)  
 このメソッドは内部でのみ使用されます。  

##### <a name="hresult-hidevoid"></a>HRESULT Hide(void)  
 このメソッドは内部でのみ使用されます。  

##### <a name="hresult-focusint-itemid"></a>HRESULT Focus(int itemId)  
 入力フォーカスを特定のコントロールに設定します。  

##### <a name="iwizardpage--pagevoid"></a>IWizardPage * Page(void)  
 このメソッドは内部でのみ使用されます。  

##### <a name="iformcontroller--formvoid"></a>IFormController * Form(void)  
 このメソッドは内部でのみ使用されます。  

##### <a name="hresult-focuswizardbuttonwizardbuttons-button"></a>HRESULT FocusWizardButton(WizardButtons button)  
 フォーカスをウィザードのいずれかのボタンに設定します。**WizardButtons** には **BackButton** と **NextButton** の 2 つの値があります。  

##### <a name="hresult-setenablewizardbuttons-button-bool-enable"></a>HRESULT SetEnable(WizardButtons button, BOOL enable)  
 いずれかのウィザード ボタンを有効または無効にすることを要求します。 ボタンが要求する状態と一致しない場合があります。 たとえば、**/preview** スイッチを使用して UDI ウィザードを実行する場合、ボタンは常に有効になります。 **WizardButtons** には **BackButton** と **NextButton** の 2 つの値があります。  

##### <a name="void-showwarningmessagelpctstr-message"></a>void ShowWarningMessage(LPCTSTR message)  
 このメソッドは、ページのコンテンツ領域の下部に警告メッセージを表示します。 このメッセージは、任意のテキストにすることができます。  

##### <a name="void-hidewarningmessagevoid"></a>void HideWarningMessage(void)  
 **ShowWarningMessage** への呼び出しで表示した警告メッセージを非表示にします。  

#### <a name="ixmldocument-interface"></a>IXmlDocument インターフェイス  

```  
__interface IXmlDocument : IUnknown  
    HRESULT Load(LPCTSTR filename);  
    HRESULT LoadXml(LPCTSTR xml);  
    HRESULT Save(LPCWSTR filename);  
    HRESULT GetParseErrorMessage(LPBSTR pMessage);  
    HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList **ppNodes);  
    HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode **ppNode);  
    HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns);  
    HRESULT AddAttribute(IXMLDOMNode *pNode, LPCWSTR name, LPCWSTR value);  
    HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode **ppNode);  
};  
```  

##### <a name="overview"></a>概要  
 このインターフェイスは、**ID_IXmlDocument** コンポーネントによって実装されます。これは、C++ で XML ドキュメントを操作しやすくように設計されたファサードです。  

##### <a name="hresult-loadlpctstr-filename"></a>HRESULT Load(LPCTSTR filename)  
 このメソッドは、外部ファイルから XML ドキュメントを読み込みます。 エラーなくファイルが読み込まれた場合は **S_OK** を返し、エラーが発生した場合は **S_FALSE** を返します。 エラーがある場合は、**GetParseErrorMessage** を呼び出すことでエラー メッセージを取得できます。  

##### <a name="hresult-loadxmllpctstr-xml"></a>HRESULT LoadXml(LPCTSTR xml)  
 このメソッドは、外部ファイルではなく、文字列から XML ドキュメントを読み込みます。 XML の読み取り先のソース以外は、動作は **Load** メソッドと同じです。  

##### <a name="hresult-savelpcwstr-filename"></a>HRESULT Save(LPCWSTR filename)  
 このメソッドは、メモリ内にある XML ドキュメントを外部ファイルに保存します。  

##### <a name="hresult-getparseerrormessagelpbstr-pmessage"></a>HRESULT GetParseErrorMessage(LPBSTR pMessage)  
 このメソッドは、読み込んでいる XML ドキュメントからのエラー メッセージ (ある場合) が含まれた新しい文字列を返します。 これは常に **S_OK** を返します。  

##### <a name="hresult-selectnodeslpctstr-xpath-ixmldomnodelist-ppnodes"></a>HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList \**ppNodes)  
 このメソッドを使用すると、XPath 式を使用して、ドキュメントからノードのコレクションを取得することができます。 これは常に **S_OK** を返します。  

##### <a name="hresult-selectsinglenodelpctstr-xpath-ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode \**ppNode)  
 このメソッドを使用すると、XPath 式を使用して、ドキュメントから 1 つのノードを取得することができます。 これは常に **S_OK** を返します。  

##### <a name="hresult-addschemalpctstr-filename-lpctstr-ns"></a>HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns)  
 このメソッドは、XML ドキュメントが読み込まれるときに、そのスキーマの検証に使用される外部スキーマ ファイルの名前を追加します。 指定する名前空間は、XPath クエリで使用できる文字列ですが、これはテストされていません。  

##### <a name="hresult-addattributeixmldomnode-pnode-lpcwstr-name-lpcwstr-value"></a>HRESULT AddAttribute(IXMLDOMNode \*pNode, LPCWSTR name, LPCWSTR value)  
 このメソッドは、XML ドキュメント内の既存のノードに新しい属性を追加します。 表 53 を参照してください。  

### <a name="table-53-hresult-addattribute"></a>表 53 HRESULT AddAttribute  

|**パラメーター**|**説明**|  
|-|-|  
|**pNode**|属性を追加するノード|  
|**名前**|新しい属性の名前|  
|**値**|新しい属性の値|  

##### <a name="hresult-createnodedomnodetype-type-lpcwstr-name-lpcwstr-ns-ixmldomnode-ppnode"></a>HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode \**ppNode)  
 新しいノードを作成するには、このメソッドを呼び出します。  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 新しいノードを作成すると、そのノードを子として別のノードに追加できます。これには、親の **appendChild** メソッドを呼び出します。  

### <a name="helper-functions"></a>ヘルパー関数  

#### <a name="createinstance-template-function"></a>CreateInstance テンプレート関数  

```  
HRESULT CreateInstance(IWizardPageContainer *pContainer, LPCTSTR type, I **ppObject)  
```  

 この関数は IWizardPageContainer.h で定義され、**IWizardPageContainer->CreateInstance** メソッドでタイプ セーフ ラッパーを提供します。次に例を示します。  

```  
CreateInstance<IDirectory>(Container(), ID_Directory, &pDirectory);  
```  

 このコードは、新しい **ID_Directory** を作成して、そのコンポーネントの **IDirectory** インターフェイスを取得します。  

#### <a name="getservice-template-function"></a>GetService テンプレート関数  

```  
void GetService(IWizardPageContainer *pContainer, I **ppService)  
```  

 この関数は IWizardPageContainer.h で定義され、**IWizardPageContainer->GetService** メソッドでタイプ セーフ ラッパーを提供します。次に例を示します。  

```  
GetService<ITSVariableBag>(Container(), &pTsBag);  
```  

 この関数は、**ITSVariableBag** インターフェイスをサポートするタスク シーケンス コンポーネントを取得します  (**ITSVariableBag** の場合、代わりに **WizardPageImpl** クラスの TSVariables メソッドを使用できます)。  

### <a name="udi-wizard-designer-configuration-file-schema-reference"></a>UDI ウィザード デザイナーの構成ファイル スキーマ リファレンス  
 このファイルは、UDI ウィザード デザイナーによって使用されます。 カスタム .dll ファイルごとに個別のファイルが作成されます。これには、カスタム ウィザード ページ エディター、カスタム タスク、またはカスタム検証コントロールを含めることができます。 ファイルは末尾を *.config* にして、*installation_folder*\Bin\Config フォルダー (ここで *installation_folder* は MDT をインストールしたフォルダー) 内にある必要があります。  

  UDI ウィザード デザイナーの構成ファイル内の要素とその説明を表 54 に示します。 **DesignerConfig** 要素は、このリファレンスのルート ノードです。  

### <a name="table-54-elements-in-the-udi-wizard-designer-configuration-file-and-their-descriptions"></a>表 54 UDI ウィザード デザイナーの構成ファイル内の要素とその説明  

|**要素名**|**説明**|  
|-|-|  
|[DesignerConfig](#DesignerConfig)|その他のすべての要素のルートを指定します|  
|[DesignerMappings](#DesignerMappings)|一連の [Page](#Page) 要素をグループ化します|  
|[Page](#Page)|UDI ウィザード デザイナーに読み込まれるウィザード ページ エディターを指定します。これはウィザード ページの構成設定を編集するために使用されます。|  
|[Param](#Param)|親 [Task](#Task) 要素または [Validator](#Validator) 要素に渡され、UDI ウィザードの構成ファイル内の [Setter]() 要素に対応するパラメーターを指定します。**注:** この要素の属性は、親が [Task](#Task) 要素または [Validator](#Validator) 要素の場合は異なります。|  
|[Task](#Task)|タスク ライブラリ内のタスクを指定します|  
|[TaskItem](#TaskItem)|タスクに渡されるパラメーターのグループを指定します|  
|[TaskLibrary](#TaskLibrary)|一連の [Task](#Task) 要素をグループ化します|  
|[Validator](#Validator)|検証コントロール ライブラリ内の検証コントロールを指定します|  
|[ValidatorLibrary](#ValidatorLibrary)|一連の [Validator](#Validator) 要素をグループ化します|  

####  <a name="DesignerConfig"></a> DesignerConfig  
 この要素は、その他のすべての要素のルートを指定します。  

##### <a name="element-information"></a>要素情報  
  表 55 では、[DesignerConfig](#DesignerConfig) 要素に関する情報を提供します。  

### <a name="table-55-designerconfig-element-information"></a>表 55 DesignerConfig 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|1: この要素が必要です。|  
|親要素|なし|  
|コンテンツ|**DesignerMappings**、**TaskLibrary**、**ValidatorLibrary**|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="DesignerMappings"></a> DesignerMappings  
 この要素は一連の [Page](#Page) 要素をグループ化します。  

##### <a name="element-information"></a>要素情報  
  表 56 では、[DesignerMappings](#DesignerMappings) 要素に関する情報を提供します。  

### <a name="table-56-designermappings-element-information"></a>表 56 DesignerMappings 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[DesignerConfig](#DesignerConfig) 要素内では 0 または 1 (この UDI ウィザード デザイナーの構成ファイルに対応する DLL にカスタム ウィザード ページが存在しない場合、この要素は省略可能です)。|  
|親要素|**DesignerConfig**|  
|コンテンツ|**Page**|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   - <DesignerMappings>  
        <Page DLL="SharedPages.dll"  
           Description="Used to display text that describes the current stagegroup"  
           Type="Microsoft.SharedPages.WelcomePage"  
           DisplayName="Welcome"   
           Image="Welcome_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.WelcomePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Captures or restores user state data"  
           Type="Microsoft.OSDRefresh.UserStatePage"  
           DisplayName="User Data"  
           Image="UserState_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.UserStatePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Allows selecting the image to install, target drive, and whether to format"  
           Type="Microsoft.OSDRefresh.VolumePage"  
           DisplayName="Volume"  
           Image="Volume_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.VolumePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
     </DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Page"></a> Page  
 この要素は、UDI ウィザード デザイナーに読み込まれるウィザード ページ エディターを指定します。これはウィザード ページの構成設定を編集するために使用されます。  

##### <a name="element-information"></a>要素情報  
表 57 では、[Page](#Page) 要素に関する情報を提供します。  

### <a name="table-57-page-element-information"></a>表 57 Page 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[DesignerMappings](#DesignerMappings) 要素で定義されているウィザード ページごとに 1 以上|  
|親要素|**DesignerMappings**|  
|コンテンツ|任意の整形式の XML コンテンツ|  

##### <a name="element-attributes"></a>要素の属性  
表 58 に [Page](#Page) 要素の属性とそれぞれの説明を示します。  

### <a name="table-58-attributes-and-corresponding-values-for-the-page-element"></a>表 58 Page 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**説明**|UDI ウィザード デザイナーに表示されるパラメーターに関する情報を提供するテキストを指定します|  
|**DesignerAssembly**|ウィザード ページ エディターに関連付けられている .dll ファイルの名前を指定します (.dll ファイルは *installation_folder*\Bin フォルダー (ここで *installation_folder* は MDT をインストールしたフォルダー) に存在している必要があります)。|  
|**DesignerType**|**DesignerAssembly** 属性で指定された .dll ファイル内でウィザード ページ エディターの名前を指定します (これは完全修飾の Microsoft .NET 名前空間を持つ、ウィザード ページ エディター用の Microsoft .NET 型です)。|  
|**DisplayName**|UDI ウィザード デザイナーに表示される、ページ エディターのわかりやすい名前を指定します|  
|**DLL**|ウィザード ページに関連付けられた .dll ファイルの名前を指定します (.dll ファイルは *installation_folder*\Templates\Distribution\Tools\\*platform* フォルダー (ここで *installation_folder* は MDT をインストールしたフォルダーで、*platform* は 32 ビット バージョンの場合は **x86** または 64 ビット バージョンの場合は **x64**) に存在している必要があります)**注:** DLL のプロセッサ アーキテクチャがインストールされている MDT プロセッサ アーキテクチャと一致していることを確認します。 たとえば、MDT の 32 ビット バージョンをインストールした場合は、必ず 32 ビットの DLL をウィザード ページに使用します。|  
|**Image**|ポータブル ネットワーク グラフィックス (PNG) 形式のページのイメージの名前を指定します (.png ファイルは *installation_folder*\Bin\Images フォルダー (ここで *installation_folder* は MDT をインストールしたフォルダー) に存在している必要があります)。|  
|**種類**|ウィザード ページ エディターを指定し、カスタム ページを登録したときに使用した名前と一致させる必要があります。|  

##### <a name="remarks"></a>備考  
 UDI ウィザード デザイナーは、テンプレートのように [Page](#Page) 要素を使用して新しいウィザード用に最初の XML を作成します。 UDI ウィザード デザイナーは、スキーマ検証を実行して、[Page](#Page) 要素と子要素が有効な形式になっていることを保証します。 この要素は、UDI ウィザード ページの型と、UDI ウィザード デザイナーがカスタム エディターを使用してこの型のページを編集および作成するために必要な情報とのマッピングを提供します。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="Param"></a> Param  
 この要素は、親 [Task](#Task) 要素または [Validator](#Validator) 要素に渡され、UDI ウィザードの構成ファイル内の [Setter]() 要素に対応するパラメーターを指定します。  

> [!NOTE]
>  この要素の属性は、親が [Task](#Task) 要素または [Validator](#Validator) 要素の場合は異なります。  

##### <a name="element-information"></a>要素情報  
 表 59 では、[Param](#Param) 要素に関する情報を提供します。  

### <a name="table-59-param-element-information"></a>表 59 Param 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[TaskItem](#TaskItem) または [Validator](#Validator) の親要素ごとに 1 以上|  
|親要素|**TaskItem**、**Validator**|  
|コンテンツ|任意の整形式の XML コンテンツ|  

##### <a name="element-attributes"></a>要素の属性  
  表 60 に [Param](#Param) 要素の属性とそれぞれの説明を示します。  

### <a name="table-60-attributes-and-corresponding-values-for-the-param-element"></a>表 60 Param 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**説明**|UDI ウィザード デザイナーに表示されるパラメーターに関する情報を提供するテキストを指定します。**注:** この属性は [Validator](#Validator) 要素に対してのみ有効です。|  
|**DisplayName**|UDI ウィザード デザイナーで、該当する UDI ウィザード ページに表示される検証コントロール パラメーターのわかりやすい名前を指定します (通常、この名前は **Name** 属性よりもわかりやすい名前にします)。**注:** この属性は [Validator](#Validator) 要素に対してのみ有効です。|  
|**名前**|親要素に応じて、タスクまたは検証コントロールに渡されるパラメーターの名前を指定します (この属性は、UDI ウィザードの構成ファイル内では、[Setter]() 要素の **Property** 属性になります)。**注:** このパラメーターは、[TaskItem](#TaskItem) と [Validator](#Validator) の両方の親要素で使用されます。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="Task"></a> Task  
 この要素は、タスク ライブラリ内のタスクを指定します。  

##### <a name="element-information"></a>要素情報  
 表 61 では、[Task](#Task) 要素に関する情報を提供します。  

### <a name="table-61-task-element-information"></a>表 61 Task 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[TaskLibrary](#TaskLibrary) 要素内で 1 以上 (**TaskLibrary** 要素が指定されている場合、この要素は省略できません)。|  
|親要素|**TaskLibrary**|  
|コンテンツ|**TaskItem**|  

##### <a name="element-attributes"></a>要素の属性  
  表 62 に [Task](#Task) 要素の属性とそれぞれの説明を示します。  

### <a name="table-62-attributes-and-corresponding-values-for-the-task-element"></a>表 62 Task 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**説明**|UDI ウィザード デザイナーに表示されるタスクに関する情報を提供するテキストを指定します|  
|**DLL**|タスクに関連付けられた .dll ファイルの名前を指定します (.dll ファイルは *installation_folder*\Templates\Distribution\Tools\\*platform* フォルダー (ここで *installation_folder* は MDT をインストールしたフォルダーで、*platform* は 32 ビット バージョンの場合は **x86** または 64 ビット バージョンの場合は **x64**) に存在している必要があります)|  
|**名前**|該当する UDI ウィザード ページおよび UDI ウィザード デザイナーで表示されるタスクの名前を指定します|  
|**種類**|ファクトリ レジストリに登録され、.dll ファイル内で特定のタスクを呼び出すために使用されるタスクの型を指定します|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="TaskItem"></a> TaskItem  
 この要素は、タスクに渡されるパラメーターのグループを指定します。  

##### <a name="element-information"></a>要素情報  
  表 63 では、[TaskItem](#TaskItem) 要素に関する情報を提供します。  

### <a name="table-63-taskitem-element-information"></a>表 63 TaskItem 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|**Task** 要素ごとに 1 回以上|  
|親要素|**Task**|  
|コンテンツ|**Param**|  

##### <a name="element-attributes"></a>要素の属性  
 表 64 に [TaskItem](#TaskItem) 要素の属性とそれぞれの説明を示します。  

### <a name="table-64-attribute-and-corresponding-values-for-the-taskitem-element"></a>表 64 TaskItem 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**種類**|UDI ウィザードの構成ファイル内に作成される要素の型を指定します。 この属性の値に対応する XML 要素が作成されます。 たとえば、この属性の値が [File](#File) の場合、**File** 要素が UDI ウィザードの構成ファイル内に作成されます。<br /><br /> 現時点では、次の値のみがサポートされています。<br /><br /> -   **File**: 2 つの [Param](#Param) 子要素が必要です (1 つは、**Name** 属性が **Source** に設定された **Param** 子要素で、もう 1 つは、**Name** 属性が **Dest** に設定された **Param** 子要素です)<br />-   [Setter](): 1 つの **Param** 子要素が必要です|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="TaskLibrary"></a> TaskLibrary  
 この要素は一連の [Task](#Task) 要素をグループ化します。  

##### <a name="element-information"></a>要素情報  
 表 65 では、[TaskLibrary](#TaskLibrary) 要素に関する情報を提供します。  

### <a name="table-65-tasklibrary-element-information"></a>表 65 TaskLibrary 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[DesignerConfig](#DesignerConfig) 要素内では 0 または 1 (この UDI ウィザード デザイナーの構成ファイルに対応する DLL にカスタム タスクが存在しない場合、この要素は省略可能です)。|  
|親要素|**DesignerConfig**|  
|コンテンツ|**Task**|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  

```  
<DesignerConfig>  
   - <TaskLibrary>  
        +<Task DLL="" Description="Executes a process with the given command line." Type="Microsoft.Wizard.ShellExecuteTask" Name="Shell Execute Task">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
        +<Task DLL="SharedPages.dll" Description="Check to ensure a wired network connection is available." Type="Microsoft.SharedPages.WiredNetworkTask" Name="Wired Network Check">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.OSDRefresh.ACPowerTask" Name="AC Power Check">  
        +<Task DLL="" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.Wizard.CopyFilesTask" Name="Copy Files Task">  
     </TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Validator"></a> Validator  
 この要素は、検証コントロール ライブラリ内の検証コントロールを指定します。  

##### <a name="element-information"></a>要素情報  
 表 66 では、[Validator](#Validator) 要素に関する情報を提供します。  

### <a name="table-66-validator-element-information"></a>表 66 Validator 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[ValidatorLibrary](#ValidatorLibrary) 要素内で 0 以上 (この要素は省略可能です)|  
|親要素|**ValidatorLibrary**|  
|コンテンツ|**Param**|  

##### <a name="element-attributes"></a>要素の属性  
表 67 に [Validator](#Validator) 要素の属性とそれぞれの説明を示します。  

### <a name="table-67-attributes-and-corresponding-values-for-the-validator-element"></a>表 67 Validator 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**説明**|UDI ウィザード デザイナーに表示される検証コントロールに関する情報を提供するテキストを指定します|  
|**DisplayName**|UDI ウィザード デザイナーに表示される検証コントロールのわかりやすい名前を指定します (通常、この名前は **Name** 属性よりもわかりやすい名前にします)。|  
|**DLL**|検証コントロールに関連付けられた .dll ファイルの名前を指定します (.dll ファイルは *installation_folder*\Templates\Distribution\Tools\\*platform* フォルダー (*installation_folder* は MDT をインストールしたフォルダーで、*platform* は 32 ビット バージョンの場合は **x86** または 64 ビット バージョンの場合は **x64**) に存在している必要があります)|  
|**名前**|該当する UDI ウィザード ページおよび UDI ウィザード デザイナーで表示される検証コントロールの名前を指定します|  
|**種類**|レジストリ ファクトリに登録され、.dll ファイル内で特定の検証コントロールを呼び出すために使用される検証コントロールの型を指定します|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="ValidatorLibrary"></a> ValidatorLibrary  
 この要素は、一連の [Validator](#Validator) 要素をグループ化します。  

##### <a name="element-information"></a>要素情報  
 表 68 では、[ValidatorLibrary](#ValidatorLibrary) 要素に関する情報を提供します。  

### <a name="table-68-validatorlibrary-element-information"></a>表 68 ValidatorLibrary 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[DesignerConfig](#DesignerConfig) 要素内では 0 または 1 (この UDI ウィザード デザイナーの構成ファイルに対応する DLL にカスタム検証コントロールが存在しない場合、この要素は省略可能です)|  
|親要素|**DesignerConfig**|  
|コンテンツ|**Validator**|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 <DesignerConfig\>   + <TaskLibrary\>   - <ValidatorLibrary\>        +<Validator DLL="" Description="Requires text in a field" Type="Microsoft.Wizard.Validation.NonEmpty" Name="NonEmpty"\>        +<Validator DLL="" Description="Doesn't allow certain characters to be in a field" Type="Microsoft.Wizard.Validation.InvalidChars" Name="InvalidChars"\>        +<Validator DLL="" Description="Must follow a pre-defined pattern" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern"\>        +<Validator DLL="" Description="Require the contents match a regular expression" Type="Microsoft.Wizard.Validation.RegEx" Name="RegEx"\>     </ValidatorLibrary\>   + <DesignerMappings\></DesignerConfig\>  

## <a name="udi-wizard-designer-reference"></a>UDI ウィザード デザイナーのリファレンス  

### <a name="controls"></a>コントロール  
 UDI ウィザード デザイナーで使用するためのカスタム ウィザード ページ エディターを作成するために使用されるコントロールは、WPF **UserControl** インスタンスです。 表 69 に、カスタム ウィザード ページ エディターの作成に使用できるコントロールを示します。  

### <a name="table-69-controls-that-can-be-used-to-create-custom-wizard-page-editors"></a>表 69 カスタム ウィザード ページ エディターの作成に使用できるコントロール  

|コントロール|説明|  
|-|-|  
|[CollectionTControl](#CollectionTControl)|このコントロールは、[Page](#Page) 要素内の [Data](#Data) 要素に格納されたデータを編集するために使用されます。|  
|[FieldElementControl](#FieldElementControl)|このコントロールは、.xaml ページ上の TextBox コントロールに通常はリンクされるフィールドを編集するために使用されます。|  
|[SetterControl](#SetterControl)|このコントロールは、UDI ウィザードの構成ファイル内の [setter]() 要素の値を変更するために使用されます。|  

####  <a name="CollectionTControl"></a> CollectionTControl  
 このコントロールは、データを編集するための多くの機能を提供します。 このコントロールの使用方法を学習する最善の方法は、サンプルを見ることです。このサンプルは、ページの **Data** 要素の下でデータを編集する方法を示します。 具体的には、このコントロール内の項目を追加、削除、および編集する方法を示します。  

####  <a name="FieldElementControl"></a> FieldElementControl  
 通常は.xaml ページ上の **TextBox** コントロールにリンクされるフィールドを編集するには、このコントロールを使用します。  

##### <a name="example"></a>例  
 次の .xaml ファイルからの抜粋は、子 **TextBox** コントロールを使用して、ウィザード ページ上のフィールドの既定値を構成するために **FieldElementControl** の使用法を示しています。  

```  
<Controls:FieldElementControl  
Width="450"  
Margin="0,5"  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
HeaderText="Location Combo Box"  
InstructionText="Here you can configure the behavior of the location combo box."  
HideValidationTab="True">  

<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
</Controls:FieldElementControl>  
```  

##### <a name="properties"></a>プロパティ  

###### <a name="fielddata"></a>FieldData  
 この文字列プロパティには、**FieldElementControl** をフィールドの基になる XML に接続するための情報が含まれています。 ページ エディター インターフェイスのプロパティに接続されます。 次の .xaml ファイルからの抜粋は、**FieldData** プロパティの使用方法を示しています。  

```  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
```  

 この抜粋では、ページ エディター インターフェイスは **ControlRoot** と呼ばれ、**ElementName** パラメーターで指定されます。 **ControlRoot** ページ エディター インターフェイスの **DataContext.Location** プロパティに対してバインドが実行されます。 **DataContext** は、UDI ウィザードの構成ファイル内の [Page](#Page) 要素をポイントするビュー モデルです。 **Location** は、可能な場所のリストを返すビューのプロパティで、UDI ウィザードの構成ファイル内の [Data](#Data) 要素によって定義されます。 それぞれの場所は UDI ウィザードの構成ファイル内の [DataItem](#DataItem) 要素によって定義されます。  

###### <a name="headertext"></a>HeaderText  
 この文字列プロパティを使用すると、[FieldElementControl](#FieldElementControl) コントロールのヘッダーを指定することができます。 ヘッダーは、コントロールのタイトルとして機能し、コントロールのすぐ上に表示される、太字のオレンジ色のテキストとして書式設定されます。  

###### <a name="instructiontext"></a>InstructionText  
 この文字列プロパティを使用すると、[FieldElementControl](#FieldElementControl) コントロールの情報テキストを指定することができます。 通常、このテキストは、フィールドの簡単な説明を提供し、フィールドの構成が対応するウィザード ページにどのように影響するかを説明するために使用されます。  

###### <a name="hideenablebutton"></a>HideEnableButton  
 このブール型プロパティを使用すると、状態を **Unlocked** と **Locked** (有効または無効) に切り替えるボタンの表示を制御できます。 次に設定した場合:  

-   **True**: ボタンは表示されません  

-   **False**: ボタンが表示されます (これが既定値です)  

###### <a name="hidedefaulttab"></a>HideDefaultTab  
 このブール型プロパティを使用すると、既定値の設定に使用されるコントロールを格納するセクションの表示を制御することができます。 このプロパティはタブを参照しますが、[FieldElementControl](#FieldElementControl) にはタブがなく、非表示にできるセクションがあります。 次に設定した場合:  

-   **True**: セクションは表示されません  

-   **False**: セクションが表示されます (これが既定値です)  

###### <a name="hideborder"></a>HideBorder  
 このブール型プロパティを使用すると、フィールド コントロールの周囲の枠線の表示を制御することができます。 次に設定した場合:  

-   **True**: 枠線は表示されません  

-   **False**: 枠線が表示されます (これが既定値です)  

###### <a name="hideimage"></a>HideImage  
 このブール型プロパティを使用すると、**FieldImageSource** プロパティで構成するイメージの表示を制御できます。 次に設定した場合:  

-   **True**: イメージは表示されません  

-   **False**: イメージが表示されます (これが既定値です)  

###### <a name="hidevalidationtab"></a>HideValidationTab  
 このブール型プロパティでは、検証コントロールのリストが管理されているセクションの表示を制御することができます。 このプロパティはタブを参照しますが、[FieldElementControl](#FieldElementControl) にはタブがなく、非表示にできるセクションがあります。 次に設定した場合:  

-   **True**: セクションは表示されません  

-   **False**: セクションが表示されます (これが既定値です)  

###### <a name="hidesummarytab"></a>HideSummaryTab  
 このブール型プロパティを使用すると、フィールドの概要キャプションを構成するセクションの表示を制御することができます。 フィールドからのキャプションと対応する値は、ステージ フロー内の **SummaryPage** ウィザード ページの型に表示されます。 このプロパティはタブを参照しますが、[FieldElementControl](#FieldElementControl) にはタブがなく、非表示にできるセクションがあります。 次に設定した場合:  

-   **True**: セクションは表示されません  

-   **False**: セクションが表示されます (これが既定値です)  

###### <a name="hidetasksequencetab"></a>HideTaskSequenceTab  
 このブール型プロパティを使用すると、フィールドに対応するタスク シーケンス変数を構成するセクションの表示を制御することができます。 このプロパティはタブを参照しますが、[FieldElementControl](#FieldElementControl) にはタブがなく、非表示にできるセクションがあります。 次に設定した場合:  

-   **True**: セクションは表示されません  

-   **False**: セクションが表示されます (これが既定値です)  


####  <a name="SetterControl"></a> SetterControl  
 UDI ウィザードの構成ファイル内の [Setter]() 要素の値を変更するには、このコントロールを使用します。 このコントロールには、**setter** 要素の値を変更するために使用される子コントロールが含まれます。  

##### <a name="example"></a>例  
 次の .xaml ファイルからの抜粋は、子 **TextBox** コントロールを使用して、**KeyLocationSetter** という名前の [Setter]() 要素を変更するための **SetterControl** の使用法を示しています。  

```  
<Controls:SetterControl Margin="5"  
        Width="450"  
        HeaderText="Title text"  
        SetterData="{Binding KeyLocationSetter}"   
        InstructionText="What this means…"  
        HorizontalAlignment="Left">  

    <TextBox  
                   Margin="0,3"  
                   Text="{Binding SetterData.SetterValue, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"  
    />  

</Controls:SetterControl>  
```  

##### <a name="properties"></a>プロパティ  

###### <a name="setterdata"></a>SetterData  
 これをセッターに接続するビューやビュー モデルのプロパティにバインドする必要があります。 これを行う方法は、**FieldElementControl** の説明にあるように、フィールドにバインドする方法と同様です。  

###### <a name="headertext"></a>HeaderText  
 このプロパティを使用すると、コントロールのヘッダーに表示されるテキストを設定することができます。 このプロパティをコントロールのタイトルと考えます。タイトルは既定では、太字のオレンジのテキストで表示されます。  

###### <a name="instructiontext"></a>InstructionText  
 このプロパティを、ヘッダーの下に表示するテキストに設定します。通常、このテキストは、フィールドの動作を変更するタイミングと理由をカスタム エディターのユーザーに知らせる指示テキストです。  

### <a name="interfaces"></a>インターフェイス  
表 70 に、カスタム ウィザード ページ エディターの作成に使用できるインターフェイスを示します。  

### <a name="table-70-interfaces-that-can-be-used-to-create-custom-wizard-page-editors"></a>表 70 カスタム ウィザード ページ エディターの作成に使用できるインターフェイス  

|**インターフェイス**|**説明**|  
|-|-|  
|[IDataService](#IDataService)|フィールドを UDI ウィザードの構成ファイル内の **Data** 要素に接続するには、このインターフェイスを使用します。|  
|[IMessageBoxService](#IMessageBoxService)|このインターフェイスは、メッセージ ボックスの表示に使用できるメソッドへのアクセスを提供します。|  

####  <a name="IDataService"></a> IDataService  
 このインターフェイスには、複数のプロパティとメソッドが含まれていますが、必要になる可能性があるプロパティは 1 つしかありません。 ここに記載されているのが、その唯一のプロパティです。  

 次のようなコードをクラス内で使用して、このインターフェイスへのポインターを取得するには、依存関係の挿入を使用できます。  

```  
[Dependency]  
public IDataService DataService { get; set; }  
```  

##### <a name="properties"></a>プロパティ  
 表 71 に、**IDataService** インターフェイスのプロパティを一覧表示します。  

### <a name="table-71-properties-for-the-idataservice-interface"></a>表 71 IDataService インターフェイスのプロパティ  

|**インターフェイス**|**説明**|  
|-|-|  
|[CurrentPage](#CurrentPage)|このプロパティは、UDI ウィザードの構成ファイルで編集されている現在のページのコンテキストの下にある XML 要素、属性、および値へのアクセスを提供します。|  

######  <a name="CurrentPage"></a> CurrentPage  

```  
XElement CurrentPage { get; set; }  
```  

 このプロパティは、現在のページの XML へのアクセスを提供します。 このプロパティを設定する必要はありませんが、ページの XML は自由に変更できます。 サンプル ページ エディターに、XML を変更する例を示します。 このプロパティは、主にカスタム データがある場合に使用します。 フィールドおよびプロパティ (セッター) の場合は、すべての詳細を処理するあらかじめビルドされているコントロールを使用できます。  

####  <a name="IMessageBoxService"></a> IMessageBoxService  
 このインターフェイスは、メッセージ ボックスの表示に使用できるメソッドへのアクセスを提供します。 メッセージ ボックスを表示するためになぜインターフェイスが必要なのか疑問に思うかもしれません。 実際には必要ありません。このインターフェイスは、デザイナーのページの自動テストの作成を支援するため、Microsoft ではこのインターフェイスをコードで使用しています。  

 ただし、これらのメソッドを使用することで、1 つの有益な利点がもたらされます。ダイアログ ボックスには UDI ウィザードに設定された "所有者" を常に持ち、これにより、ダイアログ ボックスがメイン ウィンドウで正常にグループ化されていることを保証します。  

 次のようなコードをクラス内で使用して、このインターフェイスへのポインターを取得するには、依存関係の挿入を使用できます。  

```  
[Dependency]  
public IMessageBoxService MessageBoxes { get; set; }  
```  

##### <a name="methods"></a>メソッド  
 表 72 に、**IMessageBoxService** インターフェイスのメソッドを一覧表示します。  

### <a name="table-72-methods-for-the-imessageboxservice-interface"></a>表 72 IMessageBoxService インターフェイスのメソッド  

|**方法**|**説明**|  
|-|-|  
|[ShowMessageBox](#ShowMessageBox)|このオーバーロードされたメソッドは、次のメンバーを使用してメッセージ ボックスを表示するのに使用されます。<br /><br /> -   [ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)<br />-   [ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)<br />-   [ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|  
|[ShowDialogWindow](#ShowDialogWindow)|新しいダイアログ ボックスを作成するには、このメソッドを呼び出します。|  
|[ShowWizardWindow](#ShowWizardWindow)|**[次へ]** と **[戻る]** ナビゲーション ボタンを含むダイアログ ボックス内にカスタム エディターを表示するには、このメソッドを使用します。|  

######  <a name="ShowMessageBox"></a> ShowMessageBox  
 このメソッドは、カスタム ウィザード ページ エディターの子であるメッセージ ボックスを表示します。 このメンバーはオーバー ロードされます。表 73 には、メンバーとそれぞれの簡単な説明のリストが含まれています。 各メンバーの完全な情報 (構文、使用状況、および使用例を含む) については、各メンバーに対応するセクションを参照してください。  

### <a name="table-73-overloaded-members-for-the-showmessagbox-method"></a>表 73 ShowMessagBox メソッドのオーバーロードされたメンバー  

|メンバー|説明|  
|-|-|  
|[ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)|アイコンと **[OK]** ボタンを含むメッセージ ボックスを表示します|  
|[ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)|アイコンおよびボタンのさまざまな組み合わせを含むメッセージ ボックスを表示します|  
|[ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|例外に関する情報を提供し、**[OK]** ボタンを含むメッセージ ボックスを表示します|  

######  <a name="ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon"></a> ShowMessageBox(String message, String caption, MessageBoxImage icon)  

```  
void ShowMessageBox(String message, String caption, MessageBoxImage icon);  
```  

 このメソッドは、**[OK]** ボタンを含むメッセージ ボックスを表示します。 表 74 を参照してください。  

### <a name="table-74-parameters-for-the-showmessageboxstring-message-string-caption-messageboximage-icon-method"></a>表 74 ShowMessageBox(String message, String caption, MessageBoxImage icon) メソッドのパラメーター  

|**パラメーター**|**説明**|  
|-|-|  
|**message**|メッセージ ボックスのコンテンツ領域に表示するメッセージ|  
|**caption**|ダイアログ ボックスのタイトル バーに表示するテキスト|  
|**icon**|メッセージ ボックスに表示するアイコンの型|  

######  <a name="ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon"></a> ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)  

```  
MessageBoxResult ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon);  
```  

 このメソッドは、表示するボタンのセットを含むメッセージ ボックスを表示し、どのボタンがクリックされたかを報告します。 表 75 を参照してください。  

### <a name="table-75-parameters-for-the-showmessageboxstring-message-string-caption-messageboxbutton-button-messageboximage-icon-method"></a>表 75 ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon) メソッドのパラメーター  

|**パラメーター**|**説明**|  
|-|-|  
|**message**|メッセージ ボックスのコンテンツ領域に表示するメッセージ|  
|**caption**|ダイアログ ボックスのタイトル バーに表示するテキスト|  
|**button**|表示するボタン|  
|**icon**|メッセージ ボックスに表示するアイコンの型|  

######  <a name="ShowMessageBox_Exception_exception"></a> ShowMessageBox(Exception exception)  

```  
void ShowMessageBox(Exception exception);  
```  

 このメソッドは、例外に関する情報を報告するメッセージ ボックスを表示します。 このメッセージ ボックスには、**[OK]** ボタンが 1 つ含まれます。 表 76 を参照してください。  

### <a name="table-76-parameters-for-the-showmessageboxexception-exception-method"></a>表 76 ShowMessageBox(Exception exception) メソッドのパラメーター  

|**パラメーター**|**説明**|  
|-|-|  
|**exception**|報告する例外 (ダイアログ ボックスは **exception.Message** をコンテンツとして使用します)。|  

######  <a name="ShowDialogWindow"></a> ShowDialogWindow  

```  
void ShowDialogWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 このメソッドは、**viewType** パラメーターで指定したテキストをコンテンツとして持つ新しいダイアログ ボックスを作成します。 UDI デザイナーは、この型の新しいインスタンスを作成し、それを **[OK]** ボタンと **[キャンセル]** ボタンを持つダイアログ ボックスでラップします。  

 dialogPayload パラメーターを使用して、コントロールにデータを渡します。 SDK ディレクトリ内の **SampleEditor** ソリューションには、この機能の使用方法の例が用意されています。  

######  <a name="ShowWizardWindow"></a> ShowWizardWindow  

```  
void ShowWizardWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 このメソッドを使用すると、**[次へ]** と **[戻る]** ナビゲーション ボタンを含むダイアログ ボックス内にカスタム エディターを表示することができます。 Microsoft では、このメソッドの使用方法のサンプルは提供していません。  

###  <a name="UDIWizardConfigurationFileSchemaReference"></a> UDI ウィザードの構成ファイル スキーマ リファレンス  
 このファイルは、UDI ウィザードで使用され、UDI ウィザード デザイナーによって構成されます。 このファイルは次を構成するために使用されます。  

-   UDI ウィザードに表示されるウィザード ページ  

-   UDI ウィザードのウィザード ページの順序  

-   ウィザードの各ページのフィールドの設定  

-   UDI ウィザード デザイナーで使用可能な StageGroups  

-   UDI ウィザード デザイナーの各配置ウィザードで使用可能なステージ  

  表 77 に、UDI ウィザードの構成ファイル内の要素とその説明を一覧表示します。 **Wizard** 要素は、このリファレンスのルート ノードです。  

### <a name="table-77-elements-in-the-udi-wizard-configuration-file-and-their-descriptions"></a>表 77 UDI ウィザードの構成ファイル内の要素とその説明  

|**要素名**|**説明**|  
|-|-|  
|[Data](#Data)|[Page](#Page) 要素内の個々の [DataItem](#DataItem) 要素をグループ化し、**Name** 属性で名前を付けます。|  
|[DataItem](#DataItem)|[Page](#Page) 要素内の個々の[Setter]() 要素をグループ化します。 [DataItem](#DataItem) 要素内に 1 つ以上の [Data](#Data) 要素を含めることで、階層データを作成できます。 各 **DataItem** 要素は、個々の項目を表します。 たとえば、利用可能なドライブのリストには、表示名の **DataItem** と、対応するドライブ文字の別の **DataItem** が含まれている場合があります。|  
|[既定](#Default)|[Field](#Field) または [RadioGroup](#RadioGroup) の親要素で指定されたフィールドの既定値を指定します。 既定値は、この要素のかっこで囲まれた値に設定されます。|  
|[DLL](#DLL)|UDI ウィザードおよび UDI ウィザード デザイナーによって読み込まれ、参照される DLL を指定します。|  
|[DLLs](#DLLs)|個々の [DLL](#DLL) 要素をグループ化します。|  
|[エラー](#Error)|タスクが返す可能性のあるエラー コードを指定します。 エラー コードの値は、タスクの **HRESULT** によって返され、この要素によってトラップされて、より具体的なエラー情報を提供します。|  
|[ExitCode](#ExitCode)|タスクの可能な終了コードを指定します。 終了コードは、タスクが想定する戻り値のコードです。 可能な終了コードの **ExitCode** 要素を作成します。 それ以外の場合は、**Value** 属性でアスタリスク (\*) を指定して、他の **ExitCode** 要素に一覧表示されないリターン コードを処理することができます。|  
|[ExitCodes](#ExitCodes)|[Task](#Task) 要素または **Error** 要素のために [ExitCode](#ExitCode) 要素と [Error](#Error) 要素のセットをグループ化します。|  
|[Field](#Field)|XML を使用したカスタマイズを提供するために使用される [Page](#Page) 要素内のコントロールのインスタンスを指定します。 すべてのコントロールで XML を使用したカスタマイズができるわけではありません。[Field](#Field) 要素を使用するコントロールだけです。|  
|[Fields](#Fields)|[Page](#Page) 要素内の個々の[Field](#Field) 要素をグループ化します。|  
|[File](#File)|**Microsoft.Wizard.CopyFilesTask** タスクの型を使用して、ファイルのコピー操作のソースとコピー先を指定します。 1 つのタスクで複数のファイルをコピーするために、個別の **File** 要素を含めることができます。|  
|[Page](#Page)|ページのインスタンスを指定し、ページのすべての構成設定を含めます。|  
|[PageRef](#PageRef)|[StageGroup](#StageGroup) 内の [Stage](#Stage) 内のページのインスタンスへの参照を指定します。|  
|[Pages](#Pages)|個々の [Page](#Page) 要素をグループ化します。|  
|[RadioGroup](#RadioGroup)|[Field](#Field) 要素内のラジオ ボタンのグループを指定します。|  
|[StageGroup](#StageGroup)|1 つ以上のステージのグループを指定します。|  
|[StageGroups](#StageGroups)|UDI ウィザードの構成ファイル内のステージ グループのセットをグループ化します。|  
|[Setter]()|**Property** プロパティで指定されているプロパティの値のプロパティ設定を指定します。|  
|[Stage](#Stage)|[StageGroup](#StageGroup) 内のステージを指定し、1 つ以上の [PageRef](#PageRef) 要素を含めます。|  
|[Style](#Style)|UDI ウィザードのルック アンド フィールを構成する個々の [setter]() 要素をグループ化します。これには、ウィザードの上部に表示されるタイトルと、UDI ウィザードに表示されるバナー イメージが含まれます。|  
|[Task](#Task)|親 [Page](#Page) 要素で指定されたページで実行されるタスクを指定します。|  
|[タスク](#Tasks)|[Page](#Page) 要素のタスクのセットをグループ化します。|  
|[Validator](#Validator)|親 [Field](#Field) 要素で指定されているフィールド コントロールの検証コントロールを指定します。|  
|[Wizard](#Wizard)|その他のすべての要素のルートを指定します。|  

####  <a name="Data"></a> Data  
 この要素は、[Page](#Page) 要素内の個々の [DataItem](#DataItem) 要素をグループ化し、**Name** 属性で名前を付けます。  

##### <a name="element-information"></a>要素情報  
表 78 では、[Data](#Data) 要素に関する情報を提供します。  

### <a name="table-78-data-element-information"></a>表 78 Data 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|各 [Page](#Page) 要素内で 0 以上 (この要素は省略可能です)|  
|親要素|**Page**、**DataItem**|  
|コンテンツ|**DataItem**、**Setter**|  

##### <a name="element-attributes"></a>要素の属性  
 表 79 に [Data](#Data) 要素の属性とそれぞれの説明を示します。  

### <a name="table-79-attributes-and-corresponding-values-for-the-data-element"></a>表 79 Data 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**名前**|[Data](#Data) 要素の名前を指定します。|  

##### <a name="remarks"></a>備考  
 **Name** 属性を使用すると、コードで特定のデータ セットを取得できます。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="DataItem"></a> DataItem  
 この要素は、[Page](#Page) 要素内の個々の [Setter]() 要素をグループ化します。 [DataItem](#DataItem) 要素内に 1 つ以上の [Data](#Data) 要素を含めることで、階層データを作成できます。 各 **DataItem** 要素は、個々の項目を表します。 たとえば、利用可能なドライブのリストには、表示名の **DataItem** と、対応するドライブ文字の別の **DataItem** が含まれている場合があります。  

##### <a name="element-information"></a>要素情報  
 表 80 では、[DataItem](#DataItem) 要素に関する情報を提供します。  

### <a name="table-80-dataitem-element-information"></a>表 80 DataItem 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|各 [Data](#Data) 要素内で 0 以上 (この要素は省略可能です)|  
|親要素|**Data**|  
|コンテンツ|**Data**、**Setter**|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

#### <a name="default"></a>Default  
 この要素は、[Field](#Field) または [RadioGroup](#RadioGroup) の親要素で指定されたフィールドの既定値を指定します。 既定値は、この要素のかっこで囲まれた値に設定されます。  

##### <a name="element-information"></a>要素情報  
表 81 では、[Default](#Default) 要素に関する情報を提供します。  

### <a name="table-81-default-element-information"></a>表 81 Default 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数 |[Field](#Field) 要素または [RadioGroup](#RadioGroup) 要素内で 0 以上 (この要素は省略可能です)|  
|親要素|**Field**、**RadioGroup**|  
|コンテンツ|任意の整形式の XML コンテンツが可能ですが、通常は標準テキストです|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 次の例では、**TimeZone** フィールドの既定値を "Pacific Standard Time" (太平洋標準時) に設定します。  

```  
<Field Name="TimeZone" Enabled="true" VarName="OSDTimeZone" Summary="Time Zone:">  
  <Default>Pacific Standard Time</Default>  
```  

####  <a name="DLL"></a> DLL  
 この要素は、読み込む UDI ウィザードと UDI ウィザード デザイナーの DLL と参照を指定します。  

##### <a name="element-information"></a>要素情報  
表 82 では、[DLL](#DLL) 要素に関する情報を提供します。  

### <a name="table-82-dll-element-information"></a>表 82 DLL 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[DLLs](#DLLs) 要素内で 1 回以上|  
|親要素|**DLLs**|  
|コンテンツ|この要素に許可されているコンテンツはありません|  

##### <a name="element-attributes"></a>要素の属性  
 表 83 に [DLL](#DLL) 要素の属性とそれぞれの説明を示します。  

### <a name="table-83-attributes-and-corresponding-values-for-the-dll-element"></a>表 83 DLL 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|名前|参照する UDI ウィザードと UDI ウィザード デザイナーの DLL の名前を指定します|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  

```  
<DLLs>  
  <DLL Name="OSDRefreshWizard.dll" />   
  <DLL Name="SharedPages.dll" />  
</DLLs>  
```  

####  <a name="DLLs"></a> DLLs  
 この要素は、個々の [DLL](#DLL) 要素をグループ化します。  

##### <a name="element-information"></a>要素情報  
表 84 では、[DLLs](#DLLs) 要素に関する情報を提供します。  

### <a name="table-84-dlls-element-information"></a>表 84 DLLs 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|1 台|  
|親要素|**Wizard**|  
|コンテンツ|**DLL**|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  

```  
<DLLs>  
   <DLL Name="OSDRefreshWizard.dll" />  
   <DLL Name="SharedPages.dll" />   
</DLLs>  
```  

####  <a name="Error"></a> Error  
 この要素は、タスクが返す可能性のあるエラー コードを指定します。 エラー コードの値は、タスクの **HRESULT** によって返されてトラップされ、より具体的なエラー情報を提供します。  

##### <a name="element-information"></a>要素情報  
 表 85 では、[Error](#Error) 要素に関する情報を提供します。  

### <a name="table-85-error-element-information"></a>表 85 Error 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|各 [ExitCode](#ExitCode) 要素内で 0 以上 (この要素は省略可能です)|  
|親要素|**ExitCodes**|  
|コンテンツ|任意の整形式の XML コンテンツ|  

##### <a name="element-attributes"></a>要素の属性  
 表 86 に、[Error](#Error) 要素の属性とそれぞれの説明を一覧表示します。  

###  

|**属性**|**説明**|  
|-|-|  
|**状態**|エラーが発生したタスクの戻り値の状態を指定します。 通常、この属性の値は Error に設定されます。 この値は、UDI ウィザードのウィザード ページの **[状態]** 列に表示されます。|  
|**Text**|タスクで発生したエラーの状態に関する説明テキストを指定します。|  
|**種類**|この要素が、エラー、警告、または成功を表すかどうかを指定します。 **Type** で指定された値は、[ExitCodes](#ExitCodes) 要素内で一意である必要があります。 この要素の有効な値を次に示します。<br /><br /> -   **0:** 要素は成功を表しています。<br />-   **1:**  要素は警告を表しています。<br />-   **-1:**  要素はエラーを表しています。|  
|**値**|タスクで数値として返されるコードの値を指定します。 アスタリスク (*) の値を指定すると、他の [Error](#Error) 要素に一覧表示されていないリターン コードの既定の要素を示します。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="ExitCode"></a> ExitCode  
 この要素は、タスクの可能な終了コードを指定します。 終了コードは、タスクが想定する戻り値のコードです。 可能な終了コードの **ExitCode** 要素を作成します。 それ以外の場合は、**Value** 属性でアスタリスク (\*) を指定して、他の **ExitCode** 要素に一覧表示されないリターン コードを処理することができます。  

##### <a name="element-information"></a>要素情報  
表 87 では、[ExitCode](#ExitCode) 要素に関する情報を提供します。  

### <a name="table-87-exitcode-element-information"></a>表 87 ExitCode 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|各 [ExitCodes](#ExitCodes) 要素内で 0 以上 (この要素は省略可能です)|  
|親要素|**ExitCodes**|  
|コンテンツ|少なくとも 1 つの [ExitCode](#ExitCode) 要素と 0 個以上の [Error](#Error) 要素|  

##### <a name="element-attributes"></a>要素の属性  
表 88 に [ExitCode](#ExitCode) 要素の属性とそれぞれの説明を示します。  

### <a name="table-88-attributes-and-corresponding-values-for-the-exitcode-element"></a>表 88 ExitCode 要素の属性と対応する値  

|**属性**|説明|  
|-|-|  
|**状態**|タスクの戻り値の状態を指定します。 この属性の値は、UDI ウィザードで対応するウィザード ページの **[状態]** 列に表示されます。 この属性には、タスクにとって意味のある任意の値を使用できます。 この属性に使用される一般的な値を次に示します。<br /><br /> -   Success<br />-   Warning<br />-   Error|  
|**Text**|タスクの終了コードに関する説明テキストを指定します。|  
|**種類**|この要素が、エラー、警告、または成功を表すかどうかを指定します。 Type で指定された値は、[ExitCodes](#ExitCodes) 要素内で一意である必要があります。 この要素の有効な値を次に示します。<br /><br /> -   **0:**  要素は成功を表しています。<br />-   **1:**  要素は警告を表しています。<br />-   **-1:**  要素はエラーを表しています。|  
|**値**|タスクで数値として返されるコードの値を指定します。 アスタリスク (*) の値を指定すると、他の [ExitCode](#ExitCode) 要素に一覧表示されていないリターン コードの既定の要素を示します。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="ExitCodes"></a> ExitCodes  
 この要素は、[Task](#Task) 要素または **Error** 要素のために [ExitCode](#ExitCode) 要素と [Error](#Error) 要素のセットをグループ化します。  

##### <a name="element-information"></a>要素情報  
表 89 では、[ExitCodes](#ExitCodes) 要素に関する情報を提供します。  

### <a name="table-89-exitcodes-element-information"></a>表 89 ExitCodes 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|各 [Task](#Task) 要素内で 1 回|  
|親要素|**Task**|  
|コンテンツ|**Error**、**ExitCode**|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="Field"></a> Field  
 この要素は、XML でのカスタマイズを提供するために使用される [Page](#Page) 要素内のコントロールのインスタンスを指定します。 すべてのコントロールで XML を使用したカスタマイズができるわけではありません。[Field](#Field) 要素を使用するコントロールだけです。  

##### <a name="element-information"></a>要素情報  
 表 90 では、[Field](#Field) 要素に関する情報を提供します。  

### <a name="table-90-field-element-information"></a>表 90 Field 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|各 [Field](#Field) 要素内で 0 以上 (この要素は省略可能です)|  
|親要素|**Fields**|  
|コンテンツ|**Default**、**Validator**|  

##### <a name="element-attributes"></a>要素の属性  
表 91 に、[Field](#Field) 要素の属性とそれぞれの説明を一覧表示します。  

### <a name="table-91-attributes-and-corresponding-values-for-the-field-element"></a>表 91 Field 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**Enabled**|ユーザー入力に対してフィールドを有効にするかどうかを指定します (属性は True または False に設定できます)|  
|**名前**|フィールドの名前を指定します|  
|**概要**|このフィールドが設定する値の **[概要]** ウィザード ページに表示される説明テキストを指定します|  
|**VarName**|親 [Field](#Field) 要素内のフィールドを使用して、読み取られる、または構成されるタスク シーケンス変数名を指定します|  

##### <a name="remarks"></a>備考  
 この要素には、0 個以上の [Default](#Default) 要素と 0 個以上の [Validator](#Validator) 要素を含めることができます。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="Fields"></a> Fields  
 この要素は、[Page](#Page) 要素内の個々の [Field](#Field) 要素をグループ化します。  

##### <a name="element-information"></a>要素情報  
表 92 では、[Fields](#Fields) 要素に関する情報を提供します。  

### <a name="table-92-fields-element-information"></a>表 92 Fields 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|各 [Page](#Page) 要素内で 0 以上 (この要素は省略可能です)|  
|親要素|**Page**|  
|コンテンツ|**Field**、**RadioGroup**|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="File"></a> File  
 この要素は、**Microsoft.Wizard.CopyFilesTask** タスクの型を使用して、ファイルのコピー操作のソースとコピー先を指定します。 1 つのタスクで複数のファイルをコピーするために、個別の [File](#File) 要素を含めることができます。  

##### <a name="element-information"></a>要素情報  
 表 93 では、[File](#File) 要素に関する情報を提供します。  

### <a name="table-93-file-element-information"></a>表 93 File 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|**Microsoft.Wizard.CopyFilesTask** のタスクの型を持つタスクごとに 1 以上|  
|親要素|**Task**|  
|コンテンツ|なし|  

##### <a name="element-attributes"></a>要素の属性  
 表 94 に、[File](#File) 要素の属性とそれぞれの説明を一覧表示します。  

### <a name="table-94-attributes-and-corresponding-values-for-the-file-element"></a>表 94 File 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**Dest**|**Source** 属性で指定されたファイルのコピー先のフォルダーへの完全修飾パスまたは相対パスを指定します。 環境変数は、パスの一部として許可されます。|  
|**移行元**|**Microsoft.Wizard.CopyFilesTask** タスクの型がコピーするソース ファイルへの完全修飾パスまたは相対パスを指定します。 この属性は、1 つの [File](#File) 要素を使用して複数のファイルをコピーできるように、ワイルドカード文字をサポートしています。 環境変数は、パスの一部として許可されます。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="PageElement"></a> Page  
 この要素は、ページのインスタンスを指定し、ページのすべての構成設定を含めます。  

##### <a name="element-information"></a>要素情報  
表 95 では、[Page](#Page) 要素に関する情報を提供します。  

### <a name="table-95-page-element-information"></a>表 95 Page 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[Pages](#Pages) 要素ごとに 1 以上|  
|親要素|**Pages**|  
|コンテンツ|**Data**、**Fields**、**Setter**、**Tasks**|  

##### <a name="element-attributes"></a>要素の属性  
表 96 に、[Page](#Page) 要素の属性とそれぞれの説明を一覧表示します。  

### <a name="table-96-attributes-and-corresponding-values-for-the-page-element"></a>表 96 Page 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**DisplayName**|UDI ウィザード デザイナーに表示されるウィザード ページのわかりやすい名前を指定します。 この名前は通常、**Name** 属性よりもわかりやすい名前です。|  
|**名前**|UDI ウィザード デザイナーに表示されるウィザード ページのわかりやすい名前を指定します。|  
|**種類**|DLL 内の特定のウィザード ページに直接関連するウィザード ページの型を指定します。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="PageRef"></a> PageRef  
 この要素は、[StageGroup](#StageGroup) 内の [Stage](#Stage) 内のページのインスタンスへの参照を指定します。  

##### <a name="element-information"></a>要素情報  
表 97 では、[PageRef](#PageRef) 要素に関する情報を提供します。  

### <a name="table-97-pageref-element-information"></a>表 97 PageRef 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[Stage](#Stage) 要素内で 1 以上|  
|親要素|**Stage**|  
|コンテンツ|なし|  

##### <a name="element-attributes"></a>要素の属性  
表 98 に、[PageRef](#PageRef) 要素の属性とその説明を一覧表示します。  

### <a name="table-98-attributes-and-corresponding-values-for-the-pageref-element"></a>表 98 PageRef 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**Page**|[StageGroup](#StageGroup) 内の [Stage](#Stage) 内のページのインスタンスを指定します。 この値を [Page](#Page) 要素の Name 属性に設定します。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="Pages"></a> Pages  
 この要素は、個々の [Page](#Page) 要素をグループ化します。  

##### <a name="element-information"></a>要素情報  
表 99 では、[Pages](#Pages) 要素に関する情報を提供します。  

### <a name="table-99-pages-element-information"></a>表 99 Pages 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|1 台|  
|親要素|**Wizard**|  
|コンテンツ|**Page**|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  

```  
<Pages>  
   + <Page Name="WelcomePage" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="ConfigScanPage" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="ConfigScanBareMetal" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="RebootPage" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
   + <Page Name="WelcomePageReplace" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="VolumePage" DisplayName="Volume" Type="Microsoft.OSDRefresh.VolumePage">  
   + <Page Name="UserRestorePage" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ComputerPage" DisplayName="New Computer Details" Type="Microsoft.OSDRefresh.ComputerPage">  
   + <Page Name="AdminAccounts" DisplayName="Administrator Password" Type="Microsoft.SharedPages.AdminAccountsPage">  
   + <Page Name="UDAPage" DisplayName="User Device Affinity" Type="Microsoft.OSDRefresh.UDAPage">  
   + <Page Name="LanguagePage" DisplayName="Language" Type="Microsoft.OSDRefresh.LanguagePage">  
   + <Page Name="ApplicationPage" DisplayName="Install Programs" Type="Microsoft.OSDRefresh.ApplicationPage">  
     <Page Name="SummaryPage" DisplayName="Summary" Type="Microsoft.Shared.SummaryPage" />   
   + <Page Name="UserCapturePageOldPC" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ProgressPage" DisplayName="Capture Data" Type="Microsoft.OSDRefresh.ProgressPage">  
   + <Page Name="RebootAfterCapture" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
</Pages>  
```  

####  <a name="RadioGroup"></a> RadioGroup  
 この要素は、[Field](#Field) 要素内のラジオ ボタンのグループを指定します。  

##### <a name="element-information"></a>要素情報  
表 100 では、[RadioGroup](#RadioGroup) 要素に関する情報を提供します。  

### <a name="table-100-radiogroup-element-information"></a>表 100 RadioGroup 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[Fields](#Fields) 要素内で 0 以上 (この要素は省略可能です)|  
|親要素|**Fields**|  
|コンテンツ|**既定**|  

##### <a name="element-attributes"></a>要素の属性  
 表 101 に、[RadioGroup](#RadioGroup) 要素の属性とそれぞれの説明を一覧表示します。  

### <a name="table-101-attributes-and-corresponding-values-for-the-radiogroup-element"></a>表 101 RadioGroup 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**Locked**|ラジオ ボタンのグループをユーザー入力に対して有効にするかどうかを指定します。 この属性には以下の設定ができます。<br /><br /> -   **True**:  ユーザーがグループ内のラジオ ボタンを選択できないように、ラジオ ボタンを無効にすることを指定します。<br />-   **False**:  ユーザーがグループ内のラジオ ボタンを選択できるように、ラジオ ボタンを有効にすることを指定します。|  
|**名前**|ラジオ ボタン グループの名前を指定します。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="StageGroup"></a> StageGroup  
 この要素は、展開ステージ グループを指定します。  

##### <a name="element-information"></a>要素情報  
表 102 では、[StageGroup](#StageGroup) 要素に関する情報を提供します。  

### <a name="table-102-stagegroup-element-information"></a>表 102 StageGroup 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[StageGroups](#StageGroups) 要素内で 1 以上|  
|親要素|**StageGroups**|  
|コンテンツ|**Stage**|  

##### <a name="element-attributes"></a>要素の属性  
 表 103 に、[StageGroup](#StageGroup) 要素の属性とその属性の説明を一覧表示します。  

### <a name="table-103-attributes-and-corresponding-values-for-the-stagegroup-element"></a>表 103 StageGroup 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**DisplayName**|UDI ウィザード デザイナーに表示されるステージ グループのわかりやすい名前を指定します。 この名前は通常、**Name** 属性よりもわかりやすい名前です。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="StageGroups"></a> StageGroups  
 この要素は、UDI ウィザードの構成ファイル内のステージ グループのセットをグループ化します。  

##### <a name="element-information"></a>要素情報  
表 104 では、[StageGroups](#StageGroups) 要素に関する情報を提供します。  

### <a name="table-104-stagegroups-element-information"></a>表 104 StageGroups 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[Wizard](#Wizard) 要素内で 0 以上|  
|親要素|**Wizard**|  
|コンテンツ|**StageGroup**|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="Setter"></a> Setter  
 この要素は、**Property** プロパティで指定されているプロパティの値のプロパティ設定を指定します。  

##### <a name="element-information"></a>要素情報  
 表 105 では、[Setter]() 要素に関する情報を提供します。  

### <a name="table-105-setter-element-information"></a>表 105 Setter 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|各親要素内で 0 以上 (この要素は省略可能です)|  
|親要素|**Data**、**DataItem**、**Page**、**Style**、**Task**、**Validator**|  
|コンテンツ|**Property** 属性に文字列値を含めます|  

##### <a name="element-attributes"></a>要素の属性  
表 106 に、[Setter]() 要素の属性とその説明を一覧表示します。  

### <a name="table-106-attributes-and-corresponding-values-for-the-setter-element"></a>表 106 Setter 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**プロパティ**|設定されるプロパティ名を指定します。 プロパティの名前は、この属性のかっこ内の値に設定されます。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

#### <a name="stage"></a>段階  
 この要素は、[StageGroup](#StageGroup) 内の [Stage](#Stage) を指定し、1 つ以上の [PageRef](#PageRef) 要素を含めます。  

##### <a name="element-information"></a>要素情報  
表 107 では、[Stage](#Stage) 要素に関する情報を提供します。  

### <a name="table-107-stage-element-information"></a>表 107 Stage 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[StageGroup](#StageGroup) 要素内で 1 回以上|  
|親要素|**StageGroup**|  
|コンテンツ|**PageRef**|  

##### <a name="element-attributes"></a>要素の属性  
表 108 に、[Stage](#Stage) 要素の属性とそれぞれの説明を一覧表示します。  

### <a name="table-108-attributes-and-corresponding-values-for-the-stage-element"></a>表 108 Stage 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**DisplayName**|UDI ウィザード デザイナーに表示されるウィザード ページのわかりやすい名前を指定します。 この名前は通常、**Name** 属性よりもわかりやすい名前です。|  
|**名前**|ステージの名前を指定します。 この要素の値は、**/stage: name** コマンド ライン パラメーターを使用して、UDI ウィザードを開始するときに使用されます。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="Style"></a> Style  
 この要素は、UDI ウィザードのルック アンド フィールを構成する個々の [Setter]() 要素をグループ化します。これには、ウィザードの上部に表示されるタイトルと、UDI ウィザードに表示されるバナー イメージが含まれます。  

##### <a name="element-information"></a>要素情報  
表 109 では、Style 要素に関する情報を提供します。  

### <a name="table-109-style-element-information"></a>表 109 Style 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|1 台|  
|親要素|**Wizard**|  
|コンテンツ|**Setter**|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  

```  
<Style>  
  <Setter Property="bannerFilename">UDI_Wizard_Banner.bmp</Setter>   
  <Setter Property="title">Operating System Deployment (OSD) Refresh Wizard</Setter>   
</Style>  
```  

####  <a name="TaskElement"></a> Task  
 この要素は、親 [Page](#Page) 要素で指定されたページで実行されるタスクを指定します。  

##### <a name="element-information"></a>要素情報  
表 110 では、[Task](#Task) 要素に関する情報を提供します。  

### <a name="table-110-task-element-information"></a>表 110 Task 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[Tasks](#Tasks) 要素内で 1 回以上|  
|親要素|**タスク**|  
|コンテンツ|**ExitCodes**、**File**、**Setter**|  

##### <a name="element-attributes"></a>要素の属性  
表 111 に [Task](#Task) 要素の属性とそれぞれの説明を示します。  

### <a name="table-111-attributes-and-corresponding-values-for-the-task-element"></a>表 111 Task 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**DependsOn**|タスクが別のタスクに依存するかどうかを指定します。 この属性の値は、別の [Task](#Task) 要素の **Name** 属性に設定されます。 **注:** この属性は、UDI ウィザード デザイナーを使用して構成することはできません。 ただし、.xml ファイルを直接変更することで、この属性を手動で [Task](#Task) 要素に追加することができます。|  
|**DisplayName**|UDI ウィザード デザイナーに表示されるタスクのわかりやすい名前を指定します。 この名前は通常、**Name** 属性よりもわかりやすい名前です。|  
|**名前**|タスクの名前を指定します。 この名前は一意にする必要があります。|  
|「|実行するタスクのタスク型を指定します。これはそのタスクを含む DLL で定義されます。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="Tasks"></a> Tasks  
 この要素は、[Page](#Page) 要素のタスクのセットをグループ化します。  

##### <a name="element-information"></a>要素情報  
表 112 では、[Tasks](#Tasks) 要素に関する情報を提供します。  

### <a name="table-112-tasks-element-information"></a>表 112 Tasks 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|各 [Page](#Page) 要素内で 0 または 1 (この要素は省略可能です)|  
|親要素|**Page**|  
|コンテンツ|**Task**|  

##### <a name="element-attributes"></a>要素の属性  
表 113 に [Tasks](#Tasks) 要素の属性とそれぞれの説明を示します。  

### <a name="table-113-attributes-and-corresponding-values-for-the-tasks-element"></a>表 113 Tasks 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|**NameTitle**|該当するウィザード ページでタスクの名前を含む列の上部に表示されるキャプションを指定します。|  
|**StatusTitle**|該当するウィザード ページでタスクの状態を含む列の上部に表示されるキャプションを指定します。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="ValidatorElement"></a> Validator  
 この要素は、親 [Field](#Field) 要素で指定されているフィールド コントロールの検証コントロールを指定します。  

##### <a name="element-information"></a>要素情報  
表 114 では、[Validator](#Validator) 要素に関する情報を提供します。  

### <a name="table-114-validator-element-information"></a>表 114 Validator 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|[Field](#Field) 要素内で 0 以上|  
|親要素|**Field**|  
|コンテンツ|**Setter**|  

##### <a name="element-attributes"></a>要素の属性  
表 115 に [Validator](#Validator) 要素の属性とその説明を示します。  

### <a name="table-115-attributes-and-corresponding-values-for-the-validator-element"></a>表 115 Validator 要素の属性と対応する値  

|**属性**|**説明**|  
|-|-|  
|「|検証コントロールの型を指定します。これはその検証コントロールを含む DLL で定義されます。|  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  
 ありません。  

####  <a name="Wizard"></a> Wizard  
 この要素は、その他のすべての要素のルートを指定します。  

##### <a name="element-information"></a>要素情報  
表 116 では、[Wizard](#Wizard) 要素に関する情報を提供します。  

### <a name="table-116-wizard-element-information"></a>表 116 Wizard 要素情報  

|**属性**|**値**|  
|-|-|  
|発生回数|1 台|  
|親要素|なし|  
|コンテンツ|**DLLs**、**Pages**、**StageGroups**、**Style**|  

##### <a name="element-attributes"></a>要素の属性  
 この要素には属性はありません。  

##### <a name="remarks"></a>備考  
 ありません。  

##### <a name="example"></a>例  

```  
<Wizard>  
   + <DLLs>  
   + <Style>  
   + <Pages>  
   + <StageGroups>  
</Wizard>  
```
