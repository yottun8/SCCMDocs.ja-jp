---
title: リスクに基づいてアクセスを制限する
titleSuffix: Configuration Manager
description: デバイス、ネットワーク、アプリケーションのリスクに基づいてアクセスを制限します。
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 62db216d2047ee0272c6b3fa226493b5e8af5f84
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128723"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>デバイス、ネットワーク、アプリケーションのリスクに基づき、会社のリソースへのアクセスを管理する

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

Lookout によって実施されたリスク評価に基づいて、モバイル デバイスから会社のリソースへのアクセスを制御します。 Lookout は、Microsoft Intune に統合されているデバイス脅威保護ソリューションです。 リスクは、Lookout サービスによって収集されたデータに基づきます。 Lookout は、OS の脆弱性、インストールされている悪意のあるアプリケーション、および悪意のあるネットワーク プロファイルについてのデータを、デバイスから収集します。 

Configuration Manager のコンプライアンス ポリシーによって有効にされた、Lookout がレポートするリスク評価に基づいて、条件付きアクセス ポリシーを構成します。 これらのポリシーは、デバイスを許可したり、デバイスで検出された脅威のために Configuration Manager が非準拠と決定したデバイスをブロックしたりします。

> [!Important]  
> 2018 年 8 月 14 日の時点では、ハイブリッド モバイル デバイス管理は[非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)です。 詳細については、[ハイブリッド MDM の概要](/sccm/mdm/understand/hybrid-mobile-device-management)に関するページを参照してください。<!--Intune feature 2683117-->  



## <a name="how-does-it-work"></a>機能

ハイブリッド MDM 展開と Lookout デバイス脅威防御で会社のリソースを守るしくみとはどのようなものですか。

Lookout のモバイル アプリ (Lookout for Work) は、モバイル デバイスで実行されます。 Lookout for Work は、ファイル システム、ネットワーク スタック、デバイスをキャプチャします。また、入手できる場合はアプリケーションの使用状況データもキャプチャします。 このアプリは、Lookout デバイス脅威保護クラウド サービスにこのデータを送信して、モバイルの脅威に関する集約デバイス リスクを計算します。 要件に合わせて脅威のリスク レベルの分類を変更するには、Lookout コンソールを使用します。  

Configuration Manager のコンプライアンス ポリシーには、Lookout のデバイス脅威リスク評価に基づく、Lookout モバイル脅威防御のための新しいルールが追加されています。 このルールを有効にすると、Configuration Manager でデバイスのコンプライアンスが評価されます。

デバイスがコンプライアンス ポリシーに準拠していない場合は、Exchange Online や SharePoint Online などのリソースへのアクセスを、条件付きアクセス ポリシーでブロックできます。 アクセスがブロックされると、エンド ユーザーは問題を解決して会社のリソースに再度アクセスするためのチュートリアルを受け取ります。 ユーザーは、Lookout for Work アプリ経由でこのチュートリアルを起動します。



## <a name="supported-platforms"></a>[サポートされているプラットフォーム]

- **Android 4.1 以降**、Microsoft Intune に登録済み。  

- **iOS 8 以降**、Microsoft Intune に登録済み。  


Lookout でサポートされているプラットフォームと言語の詳細については、この [Lookout のサポートに関する記事](https://personal.support.lookout.com/hc/articles/114094140253)をご覧ください。



## <a name="prerequisites"></a>[前提条件]

- [ハイブリッド MDM](/sccm/mdm/understand/hybrid-mobile-device-management)  

- Microsoft Intune のサブスクリプションと Azure Active Directory。  

- Lookout Mobile EndPoint Security のエンタープライズ サブスクリプション。 詳細については、「[Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)」を参照してください。  



## <a name="example-scenarios"></a>シナリオ例


### <a name="control-access-based-on-threat-from-malicious-apps"></a>悪意のあるアプリからの脅威に基づいてアクセスを制御する

マルウェアなど、悪意のあるアプリがデバイスで検出されると、そのデバイスで次の動作が禁止されます。

- 脅威を解決する前に企業の電子メールに接続すること  

- OneDrive for Work アプリを利用して企業のファイルを同期すること  

- ビジネス クリティカルなアプリケーションにアクセスすること  

#### <a name="access-blocked-when-malicious-apps-are-detected"></a>悪意のあるアプリが検出されるとブロックされるアクセス

![悪意のあるアプリが検出されるとアクセスをブロックする条件付きアクセス ポリシー](media/config-mgr-maliciousapps_blocked.png)

#### <a name="device-unblocked-and-is-able-to-access-company-resources-when-the-threat-is-remediated"></a>脅威が取り除かれるとブロックが解除されて会社のリソースにアクセスできるデバイス

![デバイスが準拠しているとアクセスを許可する条件付きアクセス ポリシー](media/config-mgr-maliciousapps-unblocked.png)


### <a name="control-access-based-on-threat-to-network"></a>ネットワークに対する脅威に基づいてアクセスを制御する

man-in-the-middle 攻撃のようなネットワークの脅威を検出し、デバイス リスクに基づき、WiFi ネットワークへのアクセスを制限します。

#### <a name="access-to-network-through-wifi-blocked"></a>ブロックされた WiFi 経由でのネットワークへのアクセス

![ネットワークの脅威に基づいて WiFi アクセスをブロックする条件付きアクセス](media/config-mgr-network-wifi-blocked.png)

#### <a name="access-granted-on-remediation"></a>修復後に許可されるアクセス

![脅威が取り除かれたらアクセスを許可する条件付きアクセス](media/config-mgr-network-wifi-unblocked.png)


### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>ネットワークへの脅威に基づいて SharePoint Online へのアクセスを制御する

man-in-the-middle 攻撃のようなネットワークの脅威を検出し、デバイス リスクに基づき、企業ファイルの同期を制限します。

#### <a name="access-blocked-sharepoint-online-based-on-network-threat-detected-on-the-device"></a>デバイスで検出されたネットワークの脅威に基づいてアクセスをブロックされた SharePoint Online

![SharePoint Online へのデバイスのアクセスをブロックする条件付きアクセス](media/config-mgr-network-spo-blocked.png)


#### <a name="access-granted-on-remediation"></a>修復後に許可されるアクセス

![脅威が取り除かれるとアクセスを許可する条件付きアクセス](media/config-mgr-network-spo-unblocked.png)



## <a name="next-steps"></a>次のステップ

このソリューションを実装するには、次の手順を使用します。  

1.  [Lookout モバイル脅威防御のサブスクリプションを設定する](set-up-your-subscription-with-lookout.md)
2.  [Intune で Lookout MTP の接続を有効にする](enable-lookout-connection-in-intune.md)
3.  [Lookout for work アプリケーションを構成し、展開する](configure-and-deploy-lookout-for-work-apps.md)
4.  [コンプライアンス ポリシーを構成する](enable-device-threat-protection-rule-compliance-policy.md)
5.  [Lookout の統合に関するトラブルシューティング](troubleshoot-lookout-integration.md)
