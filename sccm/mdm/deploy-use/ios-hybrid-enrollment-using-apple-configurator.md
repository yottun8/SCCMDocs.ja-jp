---
title: 'Apple Configurator を使用した iOS デバイスの登録 '
titleSuffix: Configuration Manager
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.date: 08/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de83706e92150a654967ec5cf38c5b18508d4e2b
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416913"
---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>Apple Configurator と Configuration Manager を使用した iOS ハイブリッド登録

*適用対象します。System Center Configuration Manager (Current Branch)*

企業で、従業員が使用する iOS デバイスを購入した場合、Microsoft Intune を使用してそのデバイスを管理できます。 企業所有の iOS デバイスの登録を準備するには、Configuration Manager コンソールで登録プロファイルを構成し、Apple Configurator で使用できるようにプロファイルの URL をエクスポートします。 登録のための iOS デバイスの準備として、USB ケーブルで Mac コンピューターにデバイスを接続し、Apple Configurator を使ってデバイスをセットアップします。 Apple Configurator はデバイスを出荷時の設定に戻して登録プロファイルを追加し、ユーザーが最初に電源をオンにしてセットアップ アシスタントのプロセスを実行したときに、デバイスを登録できるようにします。

そのデバイスを使用して企業の電子メールと企業のリソース (アプリやデータなど) にアクセスするユーザーが 1 人だけという専用 iOS デバイスの場合、次の手順が推奨されます。  

## <a name="prerequisites"></a>[前提条件]  

-   iOS デバイスへの物理的なアクセス  

-   デバイスのシリアル番号 - [iOS シリアル番号を取得する方法](https://support.apple.com/en-us/HT204308)  

-   [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017) がインストールされている Mac コンピューター  

-   Mac コンピューターにデバイスを接続するための USB ケーブル  

## <a name="add-a-corporate-owned-device-enrollment-profile"></a>企業所有デバイスの登録プロファイルを追加する

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[概要]** > **[会社が所有しているすべてのデバイス]** > **[iOS]** > **[登録プロファイル]** の順に移動します。 **[プロファイルの作成]** をクリックして、プロファイルの作成ウィザードを開きます。 次の各ページで、設定を構成します。  

2.  **[全般]** ページで、以下の情報を指定します。  

    -   **[名前]** (ユーザーには表示されません)  

    -   **[説明]** (ユーザーには表示されません)  

    -   **[ユーザー アフィニティ]** – デバイスの登録方法を指定します。 ほとんどのセットアップ アシスタント シナリオに **[ユーザー アフィニティを要求する]** を使用します。  

        -   **ユーザー アフィニティのプロンプト**:デバイスは、初期セットアップ時にユーザーに関連付ける必要があり、会社のデータとそのユーザーとしての電子メールにアクセスが許可されますできます。  

        -   **ユーザー アフィニティなし**:デバイスは、ユーザーと関連付けられません。 このデバイス関連付け情報を使用すると、ローカルのユーザー データにアクセスしなくてもタスクを実行できます。 ユーザーへの関連付けが必要なアプリが動作しません。

    **[次へ]** をクリックして、続行します。  

3.  **[Device Enrollment Program]** ページで **[このプロファイルの Device Enrollment Program の設定を構成する]** チェック ボックスをオフのままにして、**[次へ]** をクリックします。  

4.  概要を確認し、**[次へ]** をクリックして登録プロファイルを作成します。 **[閉じる]** をクリックして、ウィザードを終了します。 登録するデバイスの IMEI 番号またはシリアル番号を追加する準備ができました。  

## <a name="predeclare-devices-to-enroll-with-setup-assistant"></a>セットアップ アシスタントで登録するデバイスを事前宣言する

このステップでは、ハードウェア ID (IMEI またはシリアル番号) のリストを提供することにより、企業所有としてデバイスを事前宣言します。

詳しくは、「[IMEI または iOS シリアル番号を持つデバイスの事前宣言](predeclare-devices-with-hardware-id.md)」をご覧ください。 事前宣言が済んだ後、このページに戻って次のステップに進みます。

## <a name="export-the-profile-to-deploy-to-ios-devices"></a>iOS デバイスに展開するプロファイルをエクスポートする

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[概要]** > **[会社が所有しているすべてのデバイス]** > **[iOS]** > **[登録プロファイル]** の順に移動します。

2.  モバイル デバイスに展開する登録プロファイルを選び、**[エクスポート...]** をクリックします。

3.  **[プロファイルの URL]** をコピーし、編集できるファイルに保存します。   

4.  Apple Configurator 2 をサポートするには、2.0 プロファイルの URL を編集する必要があります。 URL の次の部分を置き換えます。  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     を  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  編集したプロファイルの URL を保存します。 [次のセクション](#step-4-prepare-the-device-with-apple-configurator)では、このファイルを使って登録プロファイルの URL を Apple Configurator に追加します。  

> [!NOTE]
> 登録プロファイルの URL はエクスポートされてから 2 週間有効です。 2 週間が経過したら、iOS デバイスを登録するために新しい URL をエクスポートする必要があります。

## <a name="prepare-the-device-with-apple-configurator"></a>Apple Configurator を使用してデバイスを準備する

登録できるように iOS デバイスを準備するには、Mac コンピューターに各デバイスを接続し、登録プロファイルをデバイスにアップロードします。  

> [!WARNING]  
>  Apple Configurator は、デバイスをワイプし、出荷時の構成にリセットします。  

1. Mac コンピューターで **Apple Configurator 2** を開きます。  

2. メニュー バーの **[Apple Configurator 2]** > **[Preferences]** \(設定) をクリックします。  

3. [Preferences]\(設定) ウィンドウで **[Servers]** (サーバー) を選択します。左側のウィンドウの下に表示されている "+" 記号をクリックすると、MDM サーバー ウィザードが起動します。 **[次へ]** をクリックします。  

4. [前のステップ](#step-3-export-the-profile-to-deploy-to-ios-devices)で保存した**名前**と**登録 URL** を入力します。 **[次へ]** をクリックします。  

   > [!NOTE]
   > Apple TV の信頼プロファイルの要件について警告が表示された場合は、灰色の [X] をクリックすることで **[Trust Profile]** (信頼プロファイル) オプションを安全に無効にすることができます。 アンカー証明書の警告も安全に無視できます。

   続行するには、ウィザードが完了するまで **[Next]** (次へ) をクリックします。  

5. **[Servers]** (サーバー) ウィンドウで、新しいサーバーのプロファイルの隣にある 「Edit」 (編集) をクリックします。 先に入力した URL と登録 URL が完全に一致することを確認します。 異なる場合は再度 URL を入力し、**[Save]** (保存) をクリックします。  

6. USB ケーブルで iOS デバイスを Mac コンピューターに接続します。  

   > [!WARNING]  
   >  このプロセスでは、デバイスを出荷時の構成にリセットします。 デバイスを接続する前に、デバイスをリセットし、電源をオンにします。 ベスト プラクティスとして、デバイスが Hello 画面になってから続行する必要があります。  

7. **[Prepare]** (準備) をクリックします。 **[Prepare iOS Device]** (iOS デバイスの準備) ウィンドウの **[Manual]** (手動) を選択して、**[Next]** (次へ) をクリックします。  

8. **[Enroll in MDM Server]** (MDM サーバーへの登録) ウィンドウで、作成したサーバー名を選択して、**[Next]** (次へ) をクリックします。  

9. **[Create an Organization]** (組織の作成) ウィンドウで、**組織**を選択するか、または新しい組織を作成して、**[Next]** (次へ) をクリックします。  

10. **[Configure iOS Setup Assistant]** (iOS セットアップ アシスタントの構成) ウィンドウで、ユーザーに表示される手順を選択して、**[Prepare]** (準備) をクリックします。 要求されたら、信頼設定の更新を確認します。  

11. 完了したら、USB ケーブルを外してかまいません。  

登録を準備するすべてのデバイスについて、この手順を繰り返します。

## <a name="distribute-devices"></a>デバイスを配布する

これで、デバイスを企業登録できるようになりました。 デバイスの電源を切り、ユーザーにデバイスを配布します。 デバイスの電源をオンにすると、セットアップ アシスタントが起動して、登録を開始する会社や学校のアカウントをユーザーに確認するプロンプトが表示されます。
