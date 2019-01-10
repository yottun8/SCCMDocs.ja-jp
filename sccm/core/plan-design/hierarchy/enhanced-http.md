---
title: 拡張 HTTP
titleSuffix: Configuration Manager
description: 先進認証を使用して、PKI サーバー認証証明書を必要とせずにクライアント通信をセキュリティ保護します。
ms.date: 10/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f2fab639082e6871e5df8dcebe0d1b3a440624c
ms.sourcegitcommit: 1bf26b83fa7da637d299a21e1d3bc61f2d7d8c10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2019
ms.locfileid: "54060367"
---
# <a name="enhanced-http"></a>拡張 HTTP

*適用対象: System Center Configuration Manager (Current Branch)*

<!--1356889,1358460-->

> [!Tip]  
> この機能はバージョン 1806 で[プレリリース機能](/sccm/core/servers/manage/pre-release-features)として初めて導入されました。 バージョン 1810 からは、この機能はプレリリース機能ではなくなりました。  


すべての Configuration Manager 通信パスで HTTPS 通信を使用することが推奨されていますが、PKI 証明書の管理のオーバーヘッドが原因で、一部の顧客にとっては、この使用が困難な課題になります。 Azure Active Directory (Azure AD) の統合を導入することで、一部は軽減されますが、証明書要件のすべてには対応できません。 

Configuration Manager バージョン 1806 では、クライアントがシステム クライアントと通信する方法を強化しました。 これらの強化の主な目的は、以下の 2 つです。  

- PKI サーバー認証証明書を必要とせずに機密性のクライアント通信を保護できる。  

- クライアントは、ネットワーク アクセス アカウント、クライアント PKI 証明書、Windows 認証を必要とせずに、配布ポイントからコンテンツに安全にアクセスできる。  

> [!Note]  
> PKI 証明書は、以下の要件がある顧客にとっては引き続き有効なオプションです。   
> - すべてのクライアント通信が HTTPS 経由で行われる  
> - 署名インフラストラクチャの高度な制御  


## <a name="bkmk_scenario"></a> シナリオ

これらの強化によって、次のシナリオでの動作が向上しました。  


### <a name="bkmk_scenario1"></a> シナリオ 1:管理ポイントに対するクライアント
<!--1356889-->

[Azure AD 参加済みデバイス](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices)は、HTTP 用に構成された管理ポイントと通信できます。 サイト サーバーは、管理ポイントに対する証明書を生成して、安全なチャネル経由での通信を可能にします。   

> [!Note]  
> この動作は、クラウド管理ゲートウェイ経由で通信する Azure AD 参加済みクライアント用に HTTPS が有効な管理ポイントを必要とする Configuration Manager Current Branch バージョン 1802 から変更されました。 詳細については、「[HTTPS 用の管理ポイントを有効にする](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps)」を参照してください。  


### <a name="bkmk_scenario2"></a> シナリオ 2:配布ポイントに対するクライアント
<!--1358228-->

ワークグループまたは Azure AD 参加済みクライアントは、HTTP 用に構成されている配布ポイントから安全なチャネル経由で、認証やコンテンツのダウンロードを行うことができます。 これらの種類のデバイスは、クライアント上の PKI 証明書を必要とせずに、HTTPS 用に構成された配布ポイントを使用して、認証やコンテンツのダウンロードを行うこともできます。 ワークグループまたは Azure AD 参加済みクライアントにクライアント認証証明書を追加するのは簡単ではありません。

この動作には、タスク シーケンスがブート メディア、PXE、またはソフトウェア センターから実行されている OS 展開シナリオが含まれます。 詳細については、「[ネットワーク アクセス アカウント](/sccm/core/plan-design/hierarchy/accounts#network-access-account)」を参照してください。<!--1358278-->


### <a name="bkmk_scenario3"></a> シナリオ 3:Azure AD デバイス ID 
<!--1358460-->

Azure AD 参加済みデバイスまたは[ハイブリッド Azure AD デバイス](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices)は、サインインしている Azure AD ユーザーがいない場合、割り当てられているサイトと安全に通信できます。 現在は、デバイス中心のシナリオで CMG および管理ポイントを使用して認証を行うには、クラウドベースのデバイス ID で十分になりました。 (ユーザー中心のシナリオでは、ユーザー トークンがまだ必要です。)  


## <a name="prerequisites"></a>[前提条件]  

- HTTP クライアント接続用に構成された管理ポイント。 サイトのシステム ロール プロパティの **[全般]** タブで、このオプションを設定します。  

- HTTP クライアント接続用に構成された配布ポイント。 サイトのシステム ロール プロパティの **[全般]** タブで、このオプションを設定します。 **[クライアントに匿名接続を許可する]** オプションを有効にしないでください。  

- クラウド管理のために、サイトを Azure AD にオンボードします。  

    - 既にサイトでこの前提条件を満たしている場合は、Azure AD アプリケーションを更新する必要があります。 Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[クラウド サービス]** を展開して **[Azure Active Directory テナント]** を選択します。 Azure AD テナントを選択し、**[アプリケーション]** ウィンドウで Web アプリケーションを選択して、リボンにある **[アプリケーション設定の更新]** を選択します。  

- "*[シナリオ 3](#bkmk_scenario3) のみ*":Windows 10 バージョン 1803 以降を実行していて、Azure AD に参加しているクライアント。 



## <a name="configure-the-site"></a>サイトを構成する

1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[サイトの構成]** を展開して **[サイト]** ノードを選択します。 サイトを選択して、リボンの **[プロパティ]** を選択します。  

2. **[クライアント コンピューターの通信方法]** タブに切り替えます。**[HTTPS または HTTP]** オプションを選択してから、**[HTTP サイト システムには Configuration Manager によって生成された証明書を使用する]** オプションを有効にします。  

> [!Tip]
> 管理ポイントがサイトから新しい証明書を受信して構成するまで、最大 30 分待機します。

Configuration Manager コンソールでこれらの証明書を確認できます。 **[管理]** ワークスペースに移動して、**[セキュリティ]** を展開し、**[証明書]** ノードを選択します。 SMS 発行ルートによって発行されたサイト サーバー ロール証明書と共に、**SMS 発行**ルート証明書を検索します。

この構成でクライアントが管理ポイントおよび配布ポイントと通信する方法の詳細については、「[クライアントからサイト システムとサービスへの通信](/sccm/core/plan-design/hierarchy/communications-between-endpoints#Planning_Client_to_Site_System)」をご覧ください。



## <a name="see-also"></a>関連項目
- [セキュリティの計画](/sccm/core/plan-design/security/plan-for-security)  

- [構成マネージャー クライアントのセキュリティとプライバシー](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [セキュリティの構成](/sccm/core/plan-design/security/configure-security)  

- [エンドポイント間の通信](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

