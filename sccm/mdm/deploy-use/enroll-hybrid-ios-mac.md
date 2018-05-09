---
title: Microsoft Intune を使用した iOS および Mac ハイブリッド デバイス管理の設定
titleSuffix: Configuration Manager
description: System Center Configuration Manager と Microsoft Intune を使用して iOS デバイス管理を設定します。
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9407180df12902c17f4de8e52be13229ce35c60b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune で iOS ハイブリッド デバイス管理の設定します

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager と Intune を使用して、iOS および Mac OS デバイスの登録を有効にし、iPhone、iPad、Mac のユーザーが会社の電子メールとリソースにアクセスできるようにします。 ユーザーが Intune の会社のポータル アプリをインストールすると、そのデバイスをポリシーの対象にできます。 iOS および Mac デバイスを管理するには、Apple Push Notification サービス (APNs) 証明書を Apple からインポートする必要があります。 この証明書で、Intune が Apple のデバイス管理サービスと接続を確立して、iOS と Mac デバイスを管理できるようになります。  

 企業所有の iOS デバイスを登録することもできます。  「[Enroll company-owned devices](enroll-company-owned-devices.md)」 (会社所有のデバイスの登録) をご覧ください。  

**必要条件**<br>
任意のプラットフォームの登録をセットアップする前に、「[ハイブリッド MDM をセットアップする](setup-hybrid-mdm.md)」に記載されている前提条件と手順を完了しておきます。

iOS デバイス登録を準備するには、次の手順に従います。  

## <a name="download-a-certificate-signing-request"></a>証明書署名要求のダウンロード
Apple からの APNs 証明書を要求するには、証明書署名要求ファイルが必要です。  

1.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]** >  **[Microsoft Intune サブスクリプション]** に移動します。  

2.  **[ホーム]** タブで、 **[APNs 証明書要求の作成]** をクリックします。 **[Apple Push Notification サービス証明書署名要求の要求]** ダイアログ ボックスが開きます。  

3.  **[参照]** をクリックして、新しい証明書署名要求ファイルの保存先のパスを指定します。 証明書署名要求ファイルをローカルに保存します。  

4.  **[ダウンロード]** をクリックします。 新しい Microsoft Intune 証明書署名要求ファイルがダウンロードされ、Configuration Manager によって保存されます。 証明書署名要求ファイルは、Apple Push Certificates Portal からの信頼関係証明書を要求するために使用します。  

## <a name="request-an-mdm-push-certificate-from-apple"></a>Apple からの MDM プッシュ証明書の要求
MDM プッシュ証明書は、管理サービス、Intune、および登録済み iOS モバイル デバイスの間に信頼関係を確立するために使用されます。  

1.  ブラウザーで [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) に接続し、会社の Apple ID でサインインします。 この Apple ID は、将来 APNs 証明書を更新するときにも使用する必要があります。  

2.  証明書署名要求 (.csr) ファイルを使用してウィザードを完了します。 MDM プッシュ証明書をダウンロードして、pem ファイルをローカルに保存します。 この証明書 (.pem) ファイルは、Apple Push Notification サーバーと Intune のモバイル デバイス管理機関との間に信頼関係を確立するために使用されます。  

> [!NOTE]  
>  Configuration Manager コンソールで iOS の登録が有効になるまでは、Apple Push Notification Service (APNs) 証明書を Intune にアップロードしないでください。  

## <a name="enable-enrollment-and-upload-the-mdm-push-certificate"></a>登録を有効にして MDM プッシュ証明書をアップロードする
iOS の登録を有効にして APNs 証明書をアップロードします。  

1.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]**  >  **[Microsoft Intune サブスクリプション]** に移動します。  

2.  **[ホーム]** タブの **[サブスクリプション]** グループで、**[プラットフォームの構成]**  >  **[iOS]** の順にクリックします。  

3.  **[Microsoft Intune サブスクリプションのプロパティ]** ダイアログ ボックスで、 **[iOS]** タブを選択し、 **[iOS の登録を有効にする]** チェック ボックスをオンにします。  
4.  **[参照]** をクリックし、Apple からダウンロードした APNs 証明書 (.cer) ファイルに移動します。 Configuration Manager に APNs 証明書情報が表示されます。 **[OK]** をクリックして、APNs 証明書を Intune に保存します。  

セットアップが完了したら、デバイスを登録する方法をユーザーに知らせる必要があります。 「[デバイスの登録についてユーザーに通知する事柄](https://docs.microsoft.com/intune/end-user-educate)」に関する記事をご覧ください。 この情報は、Microsoft Intune と Configuration Manager の両方によって管理されるモバイル デバイスに適用されます。

## <a name="configure-enrollment-restrictions"></a>登録制限を構成する

個人所有のデバイスをブロックすることで、登録できるデバイスを制限できます。 これにより、ユーザーが会社のポータルを使用して、個人のデバイスを登録するのを防ぐことができます。 個人所有のデバイスをブロックすると、登録できるデバイスは次に示すものに限定されます。
- [事前に宣言されたデバイス](predeclare-devices-with-hardware-id.md)
- [Apple Configurator の管理対象デバイス](ios-hybrid-enrollment-using-apple-configurator.md)
- [Device Enrollment Program (DEP) の管理対象デバイス](ios-device-enrollment-program-for-hybrid.md)
- [デバイス登録マネージャー アカウント](enroll-devices-with-device-enrollment-manager.md)で登録されているデバイス

### <a name="to-enable-enrollment-restrictions"></a>登録制限を有効にするには
1.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]**  >  **[Microsoft Intune サブスクリプション]** に移動します。
2.  **[ホーム]** タブの **[サブスクリプション]** グループで、**[プラットフォームの構成]**  >  **[iOS]** の順にクリックします。
3.  **[個人所有のデバイスをブロックする]** を選択して、登録を会社所有のデバイスに制限します。

> [!div class="button"]
[< 前のステップ](create-service-connection-point.md)  [次のステップ >](set-up-additional-management.md)
