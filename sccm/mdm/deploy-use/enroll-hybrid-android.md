---
title: Microsoft Intune を使用して Android ハイブリッド デバイスの管理をセットアップする
titleSuffix: Configuration Manager
description: Configuration Manager と Intune を使用して Android モバイル デバイスを管理できるように準備します。
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fb488ccfc186fcc56ea91c30b6c0319aead5208e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416981"
---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使ったハイブリッド Android モバイル デバイスのセットアップ

*適用対象します。System Center Configuration Manager (Current Branch)*

この記事では、Android デバイスと Android for Work デバイスのハイブリッド登録を有効にする方法について説明します。 Configuration Manger を使用し、構成された Microsoft Intune サブスクリプションからデバイスを管理できるようになります。 ユーザーは、Google Play から Android 用の会社のポータル アプリをダウンロードすることで、Android (Samsung KNOX Standard を含む) および Android for Work デバイスを登録することができます。

Configuration Manager を利用することで、コンプライアンス設定の管理、Android デバイスのワイプまたは削除、アプリの展開、ソフトウェアとハードウェアのインベントリの収集を実行できます。 Android 用の会社のポータル アプリを Android デバイスにインストールしなければ、インベントリとコンプライアンス設定などの管理機能を利用できませんが、Android デバイスにアプリを展開することはできます。  



## <a name="enable-android-enrollment"></a>Android の登録を有効にする  
次の手順で、Configuration Manager が仕事用プロファイルを使用せずに Android デバイスを管理できるようになります (つまり "従来の Android" の登録)。

1. 任意のプラットフォームの登録をセットアップする前に、「[ハイブリッド MDM をセットアップする](setup-hybrid-mdm.md)」に記載されている前提条件と手順を完了しておきます。  
2. Configuration Manager コンソールの **[管理]** ワークスペースで、**[概要]** > **[クラウド サービス]** > **[Microsoft Intune サブスクリプション]** に移動し、Intune サブスクリプションを選択します。  
3. **[ホーム]** タブの **[サブスクリプション]** グループで、**[プラットフォームの構成]**  >  **[Android]** の順に選択します。  
4. **[Microsoft Intune サブスクリプションのプロパティ]** ダイアログ ボックスで、**[Android]** タブを選択し、**[Android の登録を有効にする]** ボックスをクリックします。 **[個人所有のデバイスをブロックする]** を選択して、登録を[事前に宣言されたデバイス](predeclare-devices-with-hardware-id.md)に制限できます。

   セットアップが完了したら、デバイスを登録する方法をユーザーに知らせる必要があります。 「[デバイスの登録についてユーザーに通知する事柄](/intune/end-user-educate)」に関する記事をご覧ください。 この情報は、Microsoft Intune と Configuration Manager の両方によって管理されるモバイル デバイスに適用されます。



## <a name="enable-android-for-work-enrollment"></a>Android for Work の登録を有効にする
次の手順で、Configuration Manager が仕事用プロファイルを使って、Android デバイスを管理できるようになります。

1. Android for Work の管理者アカウントとして使用する [Google アカウントをで作成](https://accounts.google.com/SignUp)します。 または、この Intune テナントのすべての Android for Work 管理タスクに関連付けられているアカウントでサインインします。 このアカウントは、Android デバイスを管理する管理者間で共有する Google アカウントにすることができます。 このアカウントは、組織が Play for Work コンソールでアプリを管理し、発行するときに使用する Google アカウントです。 このアカウントを使用して、Play for Work ストアのアプリを承認し、アカウント名とパスワードを追跡します。
2. Android の登録を有効にするには、Google アカウントを Configuration Manager で管理される Intune テナントにバインドします。
   1. Configuration Manager コンソールの **[管理]** ワークスペースで、**[概要]** > **[クラウド サービス]** > **[Microsoft Intune サブスクリプション]** に移動し、Intune サブスクリプションを選択します。
   2. **[ホーム]** タブの **[サブスクリプション]** グループで、**[プラットフォームの構成]**  >  **[Android for Work]** の順に選択します。
   3. ダイアログ ボックスの **[Intune コンソールで Android for Work を構成する]** を選択します。 Web ブラウザーで Intune コンソールが開きます。
   4. Intune 管理者の資格情報を使用し、Azure Portal で Intune にサインインします。
   5. **[managed Google Play]** をクリックします。 
       1. **[同意する]** を選択し、[ユーザー情報とデバイス情報を Google に送信する](/intune/data-intune-sends-to-google)ためのアクセス許可を Microsoft に付与します。
       2. **[Launch Google to connect now]\(Google を起動して今すぐ接続します\)** を選択し、Google Play の Android for Work Web サイトを開きます。 お使いのブラウザーで、Web サイトが新しいタブで開きます。
       3. Google のサインイン ページで、手順 1 の Google アカウントを入力します。
       4. **[組織名]** には会社の名前を入力します。 **[エンタープライズ モビリティ管理 (EMM) プロバイダー]** には、"Microsoft Intune" が表示されるはずです。 
       5. Android for Work の規約に同意し、**[確認]** を選択します。 要求が処理されます。

   6. Google のサインイン コンポーネントで、手順 1 の Google アカウントの資格情報を入力し、会社情報を入力します。
3. Azure Portal で Intune に戻り、**[Android for Work]** 登録ブレードに移動し、**[仕事用プロファイル]** をクリックします。 これで Android for Work が有効になりました。 Android for Work デバイスには 2 つの登録オプションがあります。
   - **すべてのデバイスを Android として管理する** (無効)。 Android for Work をサポートするデバイスを含め、すべての Android デバイスが従来の Android デバイスとして登録されます。
   - **サポートされているデバイスを Android for Work として管理する** (有効)。 Android for Work をサポートするすべてのデバイスが Android for Work デバイスとして登録されます。 Android for Work をサポートしない Android デバイスは、従来の Android デバイスとして登録されます。

> [!NOTE]
> ある既知の問題では、**[これらのグループに所属するユーザーのサポートされているデバイスのみを Android for Work として管理する]** オプションが期待どおり動作しません。 指定の Azure AD グループにあるユーザーのデバイスが、Android for Work ではなく Android として登録されます。 Android for Work を有効にするには、**[サポートされているデバイスを Android for Work として管理する]** オプションを利用する必要があります。


セットアップが完了したら、デバイスを登録する方法をユーザーに知らせます。 「[デバイスの登録についてユーザーに通知する事柄](/intune/end-user-educate)」に関する記事をご覧ください。 この情報は、Microsoft Intune と Configuration Manager の両方によって管理されるモバイル デバイスに適用されます。

バインドが完了すると、アカウント名と組織名が Azure Portal の Intune に表示されます。 その時点で、両方のブラウザーを閉じることができます。

### <a name="enroll-an-android-for-work-device"></a>Android for Work デバイスを登録する
ユーザーが Android for Work デバイスを登録する方法は、Android の登録方法と似ています。 ユーザーはモバイル デバイスで Android 用の会社のポータル アプリをダウンロードしてインストールできます。 アプリでは登録プロセスの一環で仕事用プロファイルを作成するように求められます。 仕事用プロファイルを作成したら、管理対象バージョンのポータル サイトに切り替える必要があります。 管理対象のポータル サイトには、右下に小さなオレンジ色のブリーフケースのタグが付いています。

### <a name="manage-android-for-work-devices"></a>Android for Work デバイスを登録する
Android for Work の登録を有効にすると、Android for Work デバイスの次の管理タスクを実行できるようになります。
- [アプリの承認](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [構成アイテムの作成](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [コンプライアンス設定を管理する](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [電子メール プロファイルの管理](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [仕事用プロファイルの選択的ワイプ](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
> [< 前のステップ](create-service-connection-point.md)  [次のステップ >](set-up-additional-management.md)
