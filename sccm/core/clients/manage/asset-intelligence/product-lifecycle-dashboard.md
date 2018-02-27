---
title: "製品ライフサイクル ダッシュボード"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager の製品ライフサイクル ダッシュボードについて説明します。"
ms.custom: na
ms.date: 02/13/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: cfc54c1beb92d0102897f77ce3c287cc0ef9e0f4
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2018
---
# <a name="use-the-product-lifecycle-dashboard-to-manage-microsoft-lifecycle-policy-in-system-center-configuration-manager"></a>System Center Configuration Manager の製品ライフサイクル ダッシュボードを使用して Microsoft のライフサイクル ポリシーを管理する

*適用対象: System Center Configuration Manager (Technical Preview)*

[Technical Preview バージョン 1802](/sccm/core/get-started/capabilities-in-technical-preview-1802) 以降では、Configuration Manager の製品ライフサイクル ダッシュボードを使うことができます。 このダッシュボードには、Configuration Manager で管理されているデバイスにインストールされている Microsoft 製品の Microsoft 製品ライフサイクル ポリシーの状態が表示されます。 このダッシュボードでは、環境内にある Microsoft 製品についての情報、サポート可能性の状態、およびサポート終了日が提供されます。 このダッシュボードを使って、各製品のサポートを利用できるかどうかを理解することができます。 お使いの Microsoft 製品の現在のサポート期限になる前に更新を計画するのに役立ちます。  

Microsoft の製品ライフサイクル ポリシーについては、「[Microsoft ライフサイクル ポリシー](https://support.microsoft.com/en-us/lifecycle)」を参照してください。

## <a name="prerequisites"></a>[前提条件] 

 製品ライフサイクル ダッシュボードでデータを見るには、次のものが必要です。 
- Configuration Manager コンソールを実行するコンピューター上に、Internet Explorer 9 以降をインストールする必要があります。 
- ダッシュボードのハイパーリンク機能は SQL Server Reporting Services (SSRS) レポートにリンクするため、レポート サービス ポイントが必要です。 詳細については、「[System Center Configuration Manager のレポート](/sccm/core/servers/manage/reporting)」を参照してください。 
- 資産インテリジェンス同期ポイントを構成して同期する必要があります。 詳細については、「[System Center Configuration Manager で資産インテリジェンスを構成する](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence)」を参照してください。

ダッシュボード内のデータは、資産インテリジェンス同期ポイントがインストールされていることに依存します。 ダッシュボードは、製品タイトルのメタデータとして、資産インテリジェンス カタログを使います。 メタデータは、階層内のインベントリ データと比較されます。 

>[!NOTE]
>資産インテリジェンス サービス ポイントを初めて構成する場合は、忘れずに[資産インテリジェンス ハードウェア インベントリ クラスを有効](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence)にしてください。 ライフサイクル ダッシュボードは資産インテリジェンス ハードウェア インベントリ クラスに依存しており、クライアントがハードウェア インベントリをスキャンして返すまで、データは表示されません。  

## <a name="use-the-microsoft-product-lifecycle-dashboard"></a>Microsoft 製品ライフサイクル ダッシュボードを使用する

管理対象デバイスから収集されたインベントリ データを基にして、ダッシュボードは現在のすべての製品についての情報を表示します。 ただし、オペレーティング システムと SQL Server に関して表示される情報は、次のバージョンに制限されます。

- Windows Server 2008 以降
- Windows XP 以降
- SQL Server 2008 以降

Configuration Manager コンソールのライフサイクル ダッシュボードにアクセスするには、**[資産とコンプライアンス]**  >  **[資産インテリジェンス]**  >  **[製品のライフサイクル]** の順に移動します。

>[!NOTE]
>ダッシュボードのデータは、Configuration Manager コンソールの接続先のサイトに基づきます。 コンソールが最上位層サイトに接続している場合は、階層全体のデータが表示されます。 子プライマリ サイトに接続しているときは、そのサイトのデータだけが表示されます。

### <a name="product-lifecycle-dashboard"></a>製品ライフサイクル ダッシュボード

![製品ライフサイクル ダッシュボード](/sccm/core/clients/manage/asset-intelligence/media/product-lifecycle-dashboard.png)

ダッシュボードには、次のタイルがあります。 
- **[Top five products past end-of-life]\(ライフサイクルが終了した上位 5 製品\):** このタイルは、環境内で見つかったライフサイクルが終了した製品の統合データ ビューです。 グラフには、インストールされているソフトウェアのうち、オペレーティング システムおよび SQL サーバー製品のサポート ライフサイクルと比較して有効期限が切れているものが示されます。  
- **[Top five products nearing end-of-life]\(ライフサイクル終了が近づいている上位 5 製品\):** このタイルは、環境内で見つかったライフサイクル終了が 6 か月以内に近づいている製品の統合データ ビューです。 グラフには、インストールされているソフトウェアのうち、オペレーティング システムおよび SQL サーバー製品のサポート ライフサイクルと比較して有効期限が 6 か月以内のものが示されます。
- **[Lifecycle data for installed products]\(インストールされている製品のライフサイクル データ\):** このタイルには、製品がサポート対象から期限切れ状態に移行する時期の概要が示されます。 グラフには、製品がインストールされているクライアントの数の内訳、サポート可用性の状態、および次に行う手順の詳細へのリンクが表示されます。 このグラフには次の情報が含まれています。     
    - 残りサポート時間
    - 環境内での数 
    - メインストリーム サポート終了日
    - 延長サポート終了日
    - 次のステップ 

>[!IMPORTANT]
>このダッシュボードに表示される情報は、お客様の利便性のため、お客様の社内においてのみ使うことを想定して提供されています。 コンプライアンス対応を確認する場合、この情報のみに依存しないでください。 https://support.microsoft.com/en-us/lifecycle にアクセスして、表示された情報の正しさと、サポート情報を利用できるかどうかを確認してください。

## <a name="reporting"></a>レポート
**[製品のライフサイクル]** カテゴリに次の新しいレポートが追加されます。
- **[製品のライフサイクルの概要]:** 製品ライフサイクルの一覧が表示されます。 ユーザーが定義できる製品名と有効期限までの日数でフィルター処理できます。 
- **[特定のソフトウェア製品を搭載したコンピューター]:** 指定した製品が検出されたコンピューターの一覧が表示されます。
- **[組織内の期限切れの製品一覧]:** 環境内にあるライフサイクルの有効期限が切れた製品の詳細が表示されます。 
- **[組織内で有効切れの製品を使用しているマシンの一覧]:** 有効期限が切れた製品が存在するコンピューターが表示されます。 このレポートは、製品名でフィルター処理できます。

## <a name="next-steps"></a>次のステップ
Technical Preview ブランチのインストールまたは更新については、「[System Center Configuration Manager の Technical Preview](/sccm/core/get-started/technical-preview)」をご覧ください。  

