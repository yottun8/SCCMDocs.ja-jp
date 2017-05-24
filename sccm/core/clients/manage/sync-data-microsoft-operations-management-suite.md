---
title: "データの同期 | Microsoft Docs | Microsoft Operations Management Suite "
description: "Microsoft Operations Management Suite に System Center Configuration Manager からのデータを同期します。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 3acfaa2cf8c64ece5cef65b80372067336d6a815
ms.contentlocale: ja-jp
ms.lasthandoff: 05/17/2017

---


# <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Microsoft Operations Management Suite に Configuration Manager からのデータを同期


*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Operations Management Suite (OMS) Connector を使用して、System Center Configuration Manager のコレクションなどのデータを Microsoft Azure の OMS Log Analytics に同期することができます。 これにより、Configuration Manager 展開のデータが OMS で表示できるようになります。
> [!TIP]
> OMS コネクタは、プレリリースの機能です。 詳細については、「[更新プログラムからのプレリリース機能の使用](/sccm/core/servers/manage/pre-release-features)」を参照してください。

バージョン 1702 以降では、OMS コネクタを使用して、Microsoft Azure Government Cloud にある OMS ワークスペースに接続することができます。 その場合、OMS コネクタをインストールする前に構成ファイルを変更する必要があります。 このトピックの「[Azure Government Cloud で OMS コネクタを使用する](#fairfaxconfig)」を参照してください。

## <a name="prerequisites"></a>必要条件
- Configuration Manager で OMS コネクタをインストールする前に、Configuration Manager に OMS へのアクセス許可を付与する必要があります。 具体的には、OMS Log Analytics ワークスペースを含む Azure *リソース グループ*への*共同作成者アクセス許可*を付与する必要があります。 この手順は Log Analytics コンテンツに記載されています。 OMS ドキュメントの「[Configuration Manager に OMS へのアクセス許可を付与する](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms)」を参照してください。

- OMS コネクタは、[オンライン モード](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation)の[サービス接続ポイント](/sccm/core/servers/deploy/configure/about-the-service-connection-point)をホストするコンピューターにインストールする必要があります。

  OMS をスタンドアロン プライマリ サイトに接続した状態で、使用環境に中央管理サイトを追加する予定の場合は、現在の接続を削除してから、新しい中央管理サイトで接続を再構成する必要があります。

- サービス接続ポイントには、OMS 用の Microsoft Monitoring Agent、および OMS コネクタをインストールする必要があります。  エージェントと OMS コネクタは、同じ **OMS ワークスペース**を使用するように構成する必要があります。 エージェントをインストールする場合は、OMS ドキュメントの「[エージェントのダウンロードとインストール](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent)」を参照してください。

- コネクタとエージェントをインストールしたら、Configuration Manager データを使用するように OMS を構成する必要があります。  そのためには、OMS ポータルで [Configuration Manager コレクションをインポート](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections)します。



## <a name="install-the-oms-connector"></a>OMS コネクタをインストールする  
1. Configuration Manager コンソールで、[プレリリース機能を使用するように階層](/sccm/core/servers/manage/pre-release-features)を構成してから、OMS コネクタの使用を有効にします。  

2. 次に、**[管理]** > **[クラウド サービス]** > **[OMS コネクタ]** の順に移動します。 リボンで、[Operations Management Suite への接続の作成] をクリックします。 これにより、**Operation Management Suite への接続ウィザード**が開きます。 **[次へ]** を選択します。  


3.    **[全般]** ページで、次の情報を設定していることを確認し、**[次へ]** を選択します。  
  - [Web アプリケーションや Web API] 管理ツールとして Configuration Manager を登録し、[この登録のクライアント ID](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications) を設定していること。  
  - Azure Active Directory で、登録済み管理ツールのクライアント キーを作成していること。  

  - 「[Configuration Manager に OMS へのアクセス許可を付与する](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms)」で説明するように、Azure の管理ポータルで、登録済みの Web アプリ、OMS にアクセスする権限を指定していること。  

4.    **[Azure Active Directory]** ページで、OMS に対して接続設定を構成します。その場合、**[テナント]**、**[クライアント ID]**、および **[クライアントの秘密鍵]** を指定してから、**[次へ]** を選択します。  

5.    **[OMS Connection Configuration]** (OMS 接続構成) ページで、接続設定を入力します。その場合、**[Azure サブスクリプション]**、**[Azure リソース グループ]**、および **[Operations Management Suite ワークスペース]** に入力します。  ワークスペースは、サービス接続ポイントにインストールされている Microsoft Management Agent に構成されているワークスペースと一致する必要があります。  

6.    **[概要]** ページで接続設定を確認してから、**[次へ]** を選択します。 **[進行状況]** ページに接続状態を表示し、**[完了]** をクリックします。

Configuration Manager を OMS にリンクした後は、コレクションを追加または削除したり、OMS 接続のプロパティを表示できます。

## <a name="verify-the-oms-connector-properties"></a>OMS コネクタのプロパティを確認する
1.    Configuration Manager コンソールで、**[管理]** > **[クラウド サービス]** の順に移動し、**[OMS コネクタ]** を選択して **[OMS 接続]** ページを開きます。
2.    このページには、2 つのタブがあります。
  - **Azure Active Directory:**   
    このタブには、**[テナント]**、**[クライアント ID]**、**[クライアントのシークレット キーの有効期限]** が表示され、クライアントのシークレット キーが期限切れになったことを確認できます。

  - **OMS 接続のプロパティ:**  
    このタブには、**[Azure サブスクリプション]**、**[Azure リソース グループ]**、**[Operations Management Suite ワークスペース]**、および **[Device collections that Operations Management Suite can get data for]** (Operations Management Suite がデータを取得するデバイス コレクション) のリストが表示されます。 **[追加]** と **[削除]** ボタンを使用して使用できるコレクションを変更します。

## <a name="fairfaxconfig"> </a> Azure Government Cloud で OMS コネクタを使用する


1.  Configuration Manager コンソールがインストールされている任意のコンピューターで、Government クラウドをポイントするように、***&lt;CM install path>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config*** 構成ファイルを編集します。

  **編集内容:**

    設定名 *FairFaxArmResourceID* の値が、"https://management.usgovcloudapi.net/" と同一になるように変更します。

   - **元の値:**
      &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **編集後の値:**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  設定名 *FairFaxAuthorityResource* の値が、"https://login.microsoftonline.com/" と同一になるように変更します。

  - **元の値:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **編集後の値:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.com/&lt;/value>

2.    2 つの変更を含むファイルを保存したら、同じコンピューター上で Configuration Manager コンソールを再起動し、そのコンソールを使用して OMS コネクタをインストールします。 コネクタをインストールするには、「[Microsoft Operations Management Suite に Configuration Manager からのデータを同期](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)」の情報を使用し、Microsoft Azure Government クラウド上にある **Operations Management Suite のワークスペース**を選択します。

3.    OMS コネクタをインストールしたら、サイトに接続されているコンソールを使用する際に Government クラウドへの接続を使用できます。

