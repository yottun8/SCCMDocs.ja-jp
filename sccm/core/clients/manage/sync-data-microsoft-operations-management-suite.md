---
title: "データの同期 | Microsoft Operations Management Suite | System Center Configuration Manager"
description: "Microsoft Operations Management Suite に System Center Configuration Manager からのデータを同期します。"
ms.custom: na
ms.date: 10/13/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: 5786f0734ce186601f5173003b9b133ed6ae8b11

---
# <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Microsoft Operations Management Suite に Configuration Manager からのデータを同期

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Operations Management Suite (OMS) Connector を使用して、System Center Configuration Manager のコレクションなどのデータを OMS に同期できます。 これにより、Configuration Manager 展開のデータが OMS で表示できるようになります。

## <a name="add-an-oms-connection-to-configuration-manager"></a>OMS 接続を Configuration Manager に追加する

OMS 接続を追加するために、Configuration Manager 環境で最初に[サービス接続ポイント](../../../core/servers/deploy/configure/about-the-service-connection-point.md)を[オンライン モード](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/)で構成する必要があります。 OMS 接続を環境内に追加する場合、このサイト システムの役割を実行するマシンに Microsoft Monitoring Agent もインストールされます。
1.  **[管理]** ワークスペースで **[OMS コネクタ]** を選択します。 リボンで、[Operations Management Suite への接続の作成] をクリックします。 これにより、**Operation Management Suite への接続ウィザード**が開きます。 **[次へ]** を選択します。
2.  **[全般]** 画面で、次の情報を設定していることを確認し、**[次へ]** を選択します。

    * [Web アプリケーションや Web API] 管理ツールとして Configuration Manager を登録し、[この登録のクライアント ID](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/) を設定していること。
    * Azure Active Directory で、登録済み管理ツールのクライアント キーを作成していること。
    * 「[Configuration Manager に OMS へのアクセス許可を付与する](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms)」で説明するように、Azure の管理ポータルで、登録済みの Web アプリ、OMS にアクセスする権限を指定していること。

3.  [**Azure Active Directory**] 画面で、OMS に接続設定を入力します。そのためには、**[テナント]**、**[クライアント ID]**、および **[クライアントの秘密鍵]** を選択してから、**[次へ]** を選択します。
4.  **[OMS Connection Configuration]** (OMS 接続構成) 画面を入力して、接続設定を入力します。そのためには、**[Azure サブスクリプション]**、**[Azure リソース グループ]**、および **[Operations Management Suite ワークスペース]** に入力します。
5.  **[概要]** 画面で、**[次へ]** の接続設定を確認します。 **[進行状況]** 画面に接続状態を表示し、**[完了]** をクリックします。

> [!NOTE]
> OMS の階層の最上位サイトに接続する必要があります。 OMS をスタンドアロン プライマリ サイトに接続し、環境に中央管理サイトを追加する場合は、OMS 接続を削除し、新しい階層内に OMS 接続を再作成する必要があります。

Configuration Manager を OMS にリンクした後は、コレクションを追加または削除したり、OMS 接続のプロパティを表示できます。

## <a name="viewing-microsoft-operations-management-suite-connection-properties-in-configuration-manager"></a>Configuration Manager での Microsoft Operations Management Suite 接続のプロパティの表示

1.  **[クラウド サービス]** に移動し、**[OMS コネクタ]** を選択して **[OMS 接続のプロパティ]** ページを開きます。
2.  このページには、2 つのタブがあります。
  * **[Azure Active Directory]** タブには **[テナント]**、**[クライアント ID]**、**[Client secret key expiration]** (クライアント秘密鍵の期限切れ) が表示され、期限切れになった場合に、**[クライアント秘密鍵]** を **[確認]** できます。
  * **[OMS 接続のプロパティ]** タブには、**[Azure サブスクリプション]**、**[Azure リソース グループ]**、**[Operations Management Suite ワークスペース]**、および **[Device collections that Operations Management Suite can get data for]** (Operations Management Suite がデータを取得するデバイス コレクション) を表示されます。 **[追加]** と **[削除]** ボタンを使用して使用できるコレクションを変更します。



<!--HONumber=Nov16_HO1-->


