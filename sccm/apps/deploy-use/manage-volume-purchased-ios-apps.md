---
title: "ボリューム購入 iOS アプリの管理 | Microsoft Docs"
description: "iOS アプリ ストアから購入したアプリを展開および管理し、そのライセンスを追跡します。"
ms.custom: na
ms.date: 02/08/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5e7cead-e257-405b-a2aa-b0130e48dc40
caps.latest.revision: 23
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 191e01f6b8a1ef2b9e193abd62d7981e6c977c1d
ms.openlocfilehash: fb771bc94f49f25cfe01ff67c88572c8f2b18909


---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Manage volume-purchased iOS apps with System Center Configuration Manager

*適用対象: System Center Configuration Manager (Current Branch)*



 iOS アプリ ストアでは、社内で実行するアプリの複数ライセンスを購入できます。 これは、購入したアプリの複数コピーを追跡する管理費を削減するのに役立ちます。  

 System Center Configuration Manager では、このプログラムを通じて購入したアプリを、アプリ ストアからライセンス情報をインポートし、使用したライセンスの数を追跡することにより、展開および管理できます。  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>iOS デバイス用のボリューム購入アプリの管理  
 Apple ボリューム購入プログラム (VPP) で iOS アプリ用の複数ライセンスを購入します。 このためには、Apple Web サイトから Apple VPP アカウントをセットアップし、以下の機能を備えた Configuration Manager に Apple VPP トークンをアップロードします。  

-   ボリューム購入情報を Configuration Manager と同期します。  

-   購入したアプリが Configuration Manager コンソールに表示されます。  

-   アプリを展開し、監視し、使用されているライセンスの数をアプリごとに追跡できます。  

-   Configuration Manager では、ユーザーに展開されているボリューム購入アプリケーションをアンインストールすることによって、必要な場合にライセンスを再利用できます。  

## <a name="before-you-start"></a>アップグレードを開始する前に  
 開始する前に、Apple から VPP トークンを取得し、これを Configuration Manager にアップロードする必要があります。  

> [!IMPORTANT]  
>  -   現時点では、各組織が取得できる VPP アカウントとトークンは&1; つだけです。  
> -   サポートされているのは、ビジネス向けの Apple Volume Purchase Program のみです。  
> -   いったん Apple VPP アカウントを Intune に関連付けると、その後、異なるアカウントに関連付けることができなくなります。 そのため、使用するアカウントの詳細を複数のユーザーに与えておきます。  
> -   既存の Apple VPP アカウントの VPP トークンを異なる MDM 製品で使用していた場合、Configuration Manager で使用するための新しい VPP トークンを生成する必要があります。  
> -   各トークンは、1 年間有効です。  
> -   既定では、Configuration Manager は Apple VPP サービスと&1; 日に&2; 回同期します。これにより、ライセンスが Configuration Manager と同期されるようになります。  
>   
>      同期されるのはライセンスの変更のみです。 ただし、1 週間に&1; 回、完全同期が実行されます。  
>   
>      **[同期]** を選択して手動で同期するときは、常に完全同期が実行されます。  
> -   Configuration Manager データベースを回復または復元する必要がある場合は、同期されるライセンスのデータを最新のものにするために、後から手動同期を実行することをお勧めします。  
> -   iOS ボリューム購入アプリケーションはユーザーまたはデバイス コレクションに展開できますが、ユーザーが存在しないデバイス (たとえば、Device Enrollment Program (DEP) または Apple Configurator を使用してユーザー アフィニティなしで登録したデバイスなど) に展開した VPP アプリはインストールされません。  

 また、iOS デバイスを管理 (アプリの展開を含む) できるようにするには、Apple から有効な Apple Push Notification サービス (APN) 証明書をインポートしておく必要があります。 詳細については、「[Set up iOS hybrid device management](../../mdm/deploy-use/enroll-hybrid-ios-mac.md)」 (iOS ハイブリッド デバイス管理のセットアップ) を参照してください。  

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>手順 1 - Apple VPP トークンを取得およびアップロードするには  

1.  Configuration Manager コンソールで、**[管理]**、**[クラウド サービス]**、**[Apple Volume Purchase Program のトークン]** の順に選択します。   

3.  **[ホーム]** タブの **[Apple Volume Purchase Program のトークン]** グループで、**[Apple Volume Purchase Program トークンを追加する]** を選択します。  

4.  **[Apple Volume Purchase Program トークンを追加する]** ウィザードの **[全般]** ページで、次を構成します。   

    -   **[名前]** -Configuration Manager コンソールに表示されるこのトークンの名前を入力します。  

    -   **[トークン]** - **[参照]** を選択し、Apple の Web サイトからダウンロードした VPP トークンを選択します。  

         **[See Apple VPP account]** (Apple VPP アカウントを確認する) リンクを選択し、まだサインアップしていない場合は、ビジネスまたは教育向け Volume Purchase Program にサインアップします。 サインアップして、アカウントの Apple VPP トークンをダウンロードします。  

    -   **[説明]** - 必要に応じて、Configuration Manager コンソールでこの VPP トークンを識別するための説明を入力します。  

    -   **[カテゴリの割り当て (検索とフィルター処理が向上します)]** - 必要に応じて、Configuration Manager コンソールで検索しやすくするために VPP トークンにカテゴリを割り当てることができます。  

5.  **[次へ]** を選択し、ウィザードを完了します。  

**[Apple Volume Purchase Program のトークン]** ノードで、Apple VPP トークンに関する情報 (最終更新時刻、有効期限、最終同期時刻など) を表示できるようになります。

**[ホーム]** タブの **[同期]** グループにある **[同期]** を選択することで、Apple で保持されているデータをいつでも Configuration Manager と完全同期できます。  

## <a name="step-2---deploy-a-volume-purchased-app"></a>手順 2 - ボリューム購入アプリのデプロイ  

1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]**、**[アプリケーション管理]**、**[ストア アプリのライセンス情報]** の順に選択します。  

3.  展開するアプリを選択し、**[ホーム]** タブの **[作成]** グループで、**[アプリケーションの作成]** を選択します。
作成した Configuration Manager アプリケーションには、購入した iOS アプリが含まれています。 他の Configuration Manager のアプリケーションと同様に、このアプリケーションを展開して監視できます。

    > [!IMPORTANT]  
    > 展開の目的として **[必須]** を選択する必要があります。 [利用可能] のインストールは現在サポートされていません。

 アプリをデプロイするとき、アプリをインストールする各ユーザーによってライセンスが使用されます。  

 ライセンスを再利用するには、展開アクションを **アンインストール**に変更する必要があります。 アプリがアンインストールされた後、ライセンスが再利用されます。  

## <a name="step-3---monitor-ios-vpp-apps"></a>手順 3 - iOS VPP アプリの監視  
 **ソフトウェア ライブラリ** ワークスペースの**ストア アプリのライセンス情報**ノードに、ボリューム購入した iOS アプリに関する情報が表示されます。 この情報には、アプリごとに所有しているライセンスの合計数と展開されている数が含まれます。

 また、**iOS 向け Apple Volume Purchase Program アプリとライセンス数**レポートを使用して、購入したすべての VPP アプリのライセンスの使用状況を監視することもできます。  

 このレポートには、各アプリケーションの名前と購入したライセンスの総数、使用可能なライセンスの数などが表示されます。  

 Configuration Manager でのレポートの実行については、「[System Center Configuration Manager のレポート](../../core/servers/manage/reporting.md)」を参照してください。  



<!--HONumber=Feb17_HO2-->


