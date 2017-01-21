---
title: "System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM) | Microsoft Docs"
description: "System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM) について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 238ef5814c0c1b832c28d63c9f3879e21a6c439b
ms.openlocfilehash: caedfa2f89daf9ebad72602161dd618f0d18b4ab

---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune

*適用対象: System Center Configuration Manager (Current Branch)*


Configuration Manager と Microsoft Intune を使用して iOS、Windows、Android デバイスを管理できます。 すべての管理タスクは Configuration Manager コンソールから処理されます。このコンソールでは、インターネット経由で Microsoft Intune のオンライン サービスとシームレスに統合された残りの管理タスクを実行します。  Configuration Manager を利用し、ユーザーが自分のデバイスで安全かつ管理された方法で会社のリソースにアクセスできるように設定できます。 つまり、会社のデータを守ると共に、ユーザー個人のデバイスや会社支給のデバイスから会社のデータにアクセスできるようにします。 デバイスの管理機能:

-   デバイスの削除とワイプ
-   パスワード、セキュリティ、ローミング、暗号化、ワイヤレス通信などのコンプライアンス設定の構成
-   デバイスへの基幹業務 (LOB) アプリの展開
-   Windows ストア、Windows Phone ストア、App Store、または Google Play に接続するデバイスへのアプリの展開
-   ハードウェア インベントリの収集
-   組み込みレポートを使用したソフトウェア インベントリの収集

ハイブリッド MDM で使用できる新機能については、「[What's new in hybrid mobile device management](../understand/whats-new-in-hybrid-mobile-device-management.md)」 (ハイブリッド モバイル デバイス管理の新機能) を参照してください。

このドキュメントでは、Configuration Manager を使ってコンピューターを管理しており、モバイル デバイスも管理するために Intune を使って Configuration Manager コンソールを拡張する場合を考えます。 Intune とハイブリッド モバイル デバイス管理の違いを理解するには、「[Microsoft Intune スタンドアロンか System Center Configuration Manager を使用するハイブリッド モバイル デバイス管理を選択する](choose-between-standalone-intune-and-hybrid-mobile-device-management.md)」を参照してください。

Configuration Manager を Intune を利用して拡張すると、会社所有のデバイスを登録して管理したり、ユーザーに個人デバイスの登録許可を与えたりできます。 Intune を使用する会社所有のデバイスを、Configuration Manager を使用して管理することもできます。

## <a name="hybrid-mdm-enrollment"></a>ハイブリッド MDM の登録
デバイスをハイブリッド管理するには、サービスに登録する必要があります。 デバイスの登録方法は、デバイスの種類、所有権、必要な管理のレベルによって異なります。 "Bring your own device" (BYOD) 登録の場合、ユーザーは個人のスマートフォン、タブレット、PC を登録できます。 企業所有デバイス (COD) 登録の場合、リモート ワイプ、共有デバイス、デバイスのユーザー アフィニティなどの管理シナリオを有効にできます。

 オンプレミスの、あるいはクラウドでホストされている [Exchange ActiveSync](#mobile-device-management-with-exchange-activesync-and-configuration-manager) を使用する場合、登録なしの簡単な Intune 管理を有効にできます。 Windows PC は [Intune クライアント ソフトウェア](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune)でも管理できます。

## <a name="overview-of-device-enrollment-methods"></a>デバイス登録方法の概要

 次の表は、登録方法とサポートされている機能をまとめたものです。 含まれる機能:
 - **ワイプ** - デバイスを出荷時の設定に戻します。すべてのデータが削除されます。 [デバイスをインベントリから削除する](../deploy-use/wipe-lock-reset-devices.md)
 - **アフィニティ** - ユーザーとデバイスを関連付けます。 モバイル アプリケーション管理 (MAM) と会社データへの制限付きアクセスのために必要です。 [ユーザー アフィニティ](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
 - **ロック** ユーザーが管理からデバイスを削除できないようにします。 iOS デバイスの場合、ロックには監視モードが必要になります。 [リモート ロック](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

 **iOS 登録方法**

| **方法** |  **ワイプ** |  **アフィニティ**    |   **ロック** | **詳細** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | いいえ|    [はい] |   × | [詳細](../deploy-use/setup-hybrid-mdm.md#step-6-enable-platform-enrollment)|
|**[DEM](#dem)**|   いいえ |いいえ |×  | [詳細](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   ○ |   オプション |  オプション|[詳細](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| ○ |   オプション |  いいえ| [詳細](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Windows と Android の登録方法**

| **方法** |  **ワイプ** |  **アフィニティ**    |   **ロック** | **詳細**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | いいえ|    [はい] |   × | [詳細](../deploy-use/setup-hybrid-mdm.md#windows-enrollment-setup)|
|**[DEM](#dem)**|   いいえ |いいえ |×  |[詳細](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

適切な方法を見つけるのに役立つ質問集が「[Choose how to enroll devices](/intune/get-started/choose-how-to-enroll-devices1)」 (デバイスの登録方法を選択する) にあります。

## <a name="byod"></a>BYOD
"Bring your own device" ユーザーは会社ポータル アプリをインストールし、自分のデバイスを登録します。 ドメインまたは Azure Active Directory に参加し、会社のネットワークに接続できます。 BYOD 登録を有効にすることは、ほとんどのプラットフォームで、さまざまな COD シナリオの前提条件になります。 「[Setup hybrid MDM](../deploy-use/setup-hybrid-mdm.md)」 (ハイブリッド MDM のセットアップ) を参照してください。 ([テーブルに戻る](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>企業所有のデバイス
企業所有のデバイス (COD) は、Configuration Manager コンソールで管理できます。 iOS デバイスは、Apple から提供されるツールを使用して直接登録できます。 デバイス登録マネージャーを利用することで、監理者とマネージャーはあらゆる種類のデバイスを登録できます。 IMEI 番号の付いたデバイスも識別し、会社所有のタグを付け、COD シナリオを実行できます。

[企業所有のデバイスの登録](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>DEM
デバイス登録マネージャーは、複数の会社所有デバイスの登録と管理に使用される特別なユーザー アカウントです。 マネージャーは会社ポータルをインストールし、さまざまユーザーなしデバイスを登録できます。 [DEM の詳細はこちらをご覧ください](../deploy-use/enroll-devices-with-device-enrollment-manager.md)。 ([テーブルに戻る](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP
Apple デバイス登録プログラム (DEP) 管理では、ポリシーを作成したら、DEP で購入し、管理する iOS デバイスに “無線で” 展開できます。 ユーザーがデバイスを初めてオンにし、iOS セットアップ アシスタントを実行すると、デバイスが登録されます。 この方法では **iOS 監視**モードがサポートされていますが、このモードでは次の操作が可能です。
   -    ロック登録
   -    条件付きアクセス
   -    脱獄検出
   -    モバイル アプリケーション管理

[DEP の詳細はこちらをご覧ください](../deploy-use/ios-device-enrollment-program-for-hybrid.md)。 ([テーブルに戻る](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB-SA
USB 接続、セットアップ アシスタント登録。 管理者はポリシーを作成し、それを Apple Configurator にエクスポートします。 ポリシーにより USB 接続の会社所有デバイスが準備されます。 管理者は、手動で各デバイスを登録する必要があります。 ユーザーはデバイスを受け取り、セットアップ アシスタントを実行し、デバイスを登録します。 この方法では **iOS 監視**モードがサポートされていますが、このモードでは次の操作が可能です。
   -    条件付きアクセス
   -    脱獄検出
   -    モバイル アプリケーション管理

詳細は、「[Setup Assistant enrollment with Apple Configurator](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)」 (Apple Configurator によるセットアップ アシスタント登録) にあります。 ([テーブルに戻る](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Exchange ActiveSync と Configuration Manager を使用したモバイル デバイス管理
登録されていないが、Exchange ActiveSync (EAS) に接続するモバイル デバイスは EAS MDM ポリシーを利用することで Intune で管理できます。 Intune は Exchange Connector を利用し、オンプレミスまたはクラウド ホストの EAS と通信します。

[Exchange ActiveSync および Intune を使用したモバイル デバイス管理](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)


##  <a name="supported-device-platforms"></a>サポートされているデバイス プラットフォーム

Configuration Manager ハイブリッド MDM で管理できるデバイス プラットフォーム:

[!INCLUDE[../includes/mdm-supported-devices](../includes/mdm-supported-devices.md)]

## <a name="next-steps"></a>次のステップ
 - [デバイス登録の前提条件](../deploy-use/setup-hybrid-mdm.md)
 - [企業所有のデバイスの管理](../deploy-use/enroll-company-owned-devices.md)



<!--HONumber=Dec16_HO3-->


