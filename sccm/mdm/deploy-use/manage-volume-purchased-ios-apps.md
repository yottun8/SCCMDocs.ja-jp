---
title: "ボリューム購入 iOS アプリの管理 | Microsoft Docs"
description: "iOS アプリ ストアから購入したアプリを展開および管理し、そのライセンスを追跡します。"
ms.custom: na
ms.date: 05/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: c6a6137fa978e1ea28aefea2aea4e29ba661efd6
ms.openlocfilehash: 55f1204b088a7b636a90561f20aa41c7de72bc05
ms.contentlocale: ja-jp
ms.lasthandoff: 05/04/2017

---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Manage volume-purchased iOS apps with System Center Configuration Manager

*適用対象: System Center Configuration Manager (Current Branch)*



 iOS アプリ ストアでは、社内で実行するアプリの複数ライセンスを購入できます。 これは、購入したアプリの複数コピーを追跡する管理費を削減するのに役立ちます。  

 System Center Configuration Manager は、このプログラムを通じて購入した iOS アプリを、App Store からライセンス情報をインポートし、使用されているライセンスの数を追跡して展開および管理するのに役立ちます。  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>iOS デバイス用のボリューム購入アプリの管理  
 Apple ボリューム購入プログラム (VPP) で iOS アプリ用の複数ライセンスを購入します。 このためには、Apple Web サイトから Apple VPP アカウントをセットアップし、以下の機能を備えた Configuration Manager に Apple VPP トークンをアップロードします。  

-   ボリューム購入情報を Configuration Manager と同期します。 
 
- ビジネス向け Apple Volume Purchase Program と教育向け Apple Volume Purchase Program の両方のアプリを同期します。

- Configuration Manager を使用して、複数の Apple Volume Purchase Program トークンを関連付けます。

-   購入したアプリが Configuration Manager コンソールに表示されます。  

-   アプリを展開し、監視し、使用されているライセンスの数をアプリごとに追跡できます。  

-   Configuration Manager では、展開されている Volume Purchase Program をアンインストールすることによって、必要な場合にライセンスを再利用できます。  

## <a name="before-you-start"></a>アップグレードを開始する前に  
 開始する前に、Apple から VPP トークンを取得し、これを Configuration Manager にアップロードする必要があります。  

-   既存の Apple VPP アカウントの VPP トークンを異なる MDM 製品で使用していた場合、Configuration Manager で使用するための新しい VPP トークンを生成する必要があります。  
-   各トークンは、1 年間有効です。  
-   既定では、Configuration Manager は Apple VPP サービスと 1 日に 2 回同期します。これにより、ライセンスが Configuration Manager と同期されるようになります。  
      同期されるのはライセンスの変更のみです。 ただし、1 週間に 1 回、完全同期が実行されます。  
      **[同期]** を選択して手動で同期するときは、常に完全同期が実行されます。  
-   Configuration Manager データベースを回復または復元する必要がある場合は、同期されるライセンスのデータを最新のものにするために、後から手動同期を実行することをお勧めします。  
-   また、iOS デバイスを管理 (アプリの展開を含む) できるようにするには、Apple から有効な Apple Push Notification サービス (APN) 証明書をインポートしておく必要があります。 詳細については、「[Set up iOS hybrid device management](enroll-hybrid-ios-mac.md)」 (iOS ハイブリッド デバイス管理のセットアップ) を参照してください。  

System Center Configuration Manager 1702 以降では、デバイスとユーザーにライセンスされたアプリを展開できるようになりました。 デバイス ライセンスをサポートするアプリ機能に応じて、次のように、展開時に適切なライセンスが要求されます。

|||||
|-|-|-|-|
|Configuration Manager バージョン|アプリでのデバイス ライセンスのサポート|展開コレクションの種類|要求されるライセンス|
|1702 より前|○|ユーザー|ユーザー ライセンス|
|1702 より前|×|ユーザー|ユーザー ライセンス|
|1702 より前|○|デバイス|ユーザー ライセンス|
|1702 より前|×|デバイス|ユーザー ライセンス|
|1702 以降|○|ユーザー|ユーザー ライセンス|
|1702 以降|×|ユーザー|ユーザー ライセンス|
|1702 以降|○|デバイス|デバイス ライセンス|
|1702 以降|×|デバイス|ユーザー ライセンス|

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>手順 1 - Apple VPP トークンを取得およびアップロードするには  

1.  Configuration Manager コンソールで、**[管理]**、**[クラウド サービス]**、**[Apple Volume Purchase Program のトークン]** の順に選択します。   

3.  **[ホーム]** タブの **[Apple Volume Purchase Program のトークン]** グループで、**[Apple Volume Purchase Program トークンを追加する]** を選択します。  

4.  **[Apple Volume Purchase Program トークンを追加する]** ウィザードの **[全般]** ページで、次を構成します。   

    -   **[名前]** -Configuration Manager コンソールに表示されるこのトークンの名前を入力します。  

    -   **[トークン]** - **[参照]** を選択し、Apple の Web サイトからダウンロードした VPP トークンを選択します。  

         **[See Apple VPP account]** (Apple VPP アカウントを確認する) リンクを選択し、まだサインアップしていない場合は、ビジネスまたは教育向け Volume Purchase Program にサインアップします。 サインアップして、アカウントの Apple VPP トークンをダウンロードします。  

    -   **[説明]** - 必要に応じて、Configuration Manager コンソールでこの VPP トークンを識別するための説明を入力します。  

    -   **[カテゴリの割り当て (検索とフィルター処理が向上します)]** - 必要に応じて、Configuration Manager コンソールで検索しやすくするために VPP トークンにカテゴリを割り当てることができます。  
    -   **Apple ID** - VPP トークンに関連付けられている Apple の電子メール ID を入力します。
    -   **トークンの種類** - 使用する VPP トークンの種類を選択します。 トークンの種類は **[ビジネス]** と **[EDU]** から選択できます。

5.  **[次へ]** を選択し、ウィザードを完了します。  

**[Apple Volume Purchase Program のトークン]** ノードで、Apple VPP トークンに関する情報 (最終更新時刻、有効期限、最終同期時刻など) を表示できるようになります。

**[ホーム]** タブの **[同期]** グループにある **[同期]** を選択することで、Apple で保持されているデータをいつでも Configuration Manager と完全同期できます。  

## <a name="step-2---deploy-a-volume-purchased-app"></a>手順 2 - ボリューム購入アプリのデプロイ  

1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]**、**[アプリケーション管理]**、**[ストア アプリのライセンス情報]** の順に選択します。  

3.  展開するアプリを選択し、**[ホーム]** タブの **[作成]** グループで、**[アプリケーションの作成]** を選択します。
作成された Configuration Manager アプリケーションには、ビジネス向け Windows ストアのアプリが含まれます。 他の Configuration Manager のアプリケーションと同様に、このアプリケーションを展開して監視できます。

    > [!IMPORTANT]  
    > 展開の目的として **[必須]** を選択する必要があります。 [利用可能] のインストールは現在サポートされていません。

 アプリを展開するときに、各ユーザーによって、またはデバイスのインストールの場合はアプリをインストールする各デバイスによって、ライセンスが使用されます。  デバイス ライセンスをサポートするアプリを含むデバイス コレクションを対象にすると、デバイス ライセンスが要求されます。  デバイス ライセンスをサポートしないアプリを含むデバイス コレクションを対象にすると、ユーザー ライセンスが要求されます。 

 **[ストア アプリのライセンス情報]** ノードからアプリを作成すると、選択したアプリのトークンのライセンスにアプリが関連付けられます。  たとえば、ノードに同じアプリの 2 つのバージョンが表示される場合があります。 これは、アプリの各バージョンが異なる Apple VPP トークンに関連付けられているためです。  したがって、各トークンからアプリを作成し、それらを個別に展開することができます。

 ライセンスを再利用するには、**[アンインストール]** の展開アクションを使用してアプリの新しい展開を作成する必要があります。 元の展開では展開アクションを変更できません。 アプリがアンインストールされた後、ライセンスが再利用されます。  

## <a name="step-3---monitor-ios-vpp-apps"></a>手順 3 - iOS VPP アプリの監視  
 **ソフトウェア ライブラリ** ワークスペースの**ストア アプリのライセンス情報**ノードに、ボリューム購入した iOS アプリに関する情報が表示されます。 この情報には、アプリごとに所有しているライセンスの合計数と展開されている数が含まれます。 さらに、ビューには、アプリが関連付けられている VPP トークンと、そのトークンの種類が表示されます。

 また、**iOS 向け Apple Volume Purchase Program アプリとライセンス数**レポートを使用して、購入したすべての VPP アプリのライセンスの使用状況を監視することもできます。  

 このレポートには、各アプリケーションの名前と購入したライセンスの総数、使用可能なライセンスの数などが表示されます。  

 Configuration Manager でのレポートの実行については、「[System Center Configuration Manager のレポート](../../core/servers/manage/reporting.md)」を参照してください。  

