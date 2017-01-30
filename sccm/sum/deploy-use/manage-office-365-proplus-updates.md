---
title: "Office 365 ProPlus 更新プログラムの管理 | Microsoft Docs"
description: "Configuration Manager が WSUS カタログからサイト サーバーに Office 365 のクライアント更新プログラムを同期したら、その更新プログラムをクライアントに展開できるようになります。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/04/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 46c8004afee4b18d5c7a2fcc5dac0f7d0d1f823c
ms.openlocfilehash: fb2fc409c2f734816e4f3bf93d61a748d957ebf0

---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>Configuration Manager での Office 365 ProPlus の更新プログラムの管理

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager バージョン 1602 以降では、ソフトウェア更新管理のワークフローを使用して、Office 365 クライアントの更新プログラムを管理できます。 マイクロソフトが Office コンテンツ配信ネットワーク (CDN) に対する新しい Office 365 のクライアント更新プログラムを公開するときには、Windows Server Update Services (WSUS) に対する更新パッケージも公開します。 Configuration Manager が WSUS カタログからサイト サーバーに Office 365 クライアント更新プログラムを同期したら、その更新プログラムをクライアントに展開できるようになります。

## <a name="office-365-client-management-dashboard"></a>Office 365 クライアント管理ダッシュボード  
Configuration Manager バージョン 1610 より、Office 365 クライアント管理ダッシュボードを Configuration Manager コンソールで利用できます。 このダッシュボードを表示するには、**[ソフトウェア ライブラリ]** > **[概要]** > **[Office 365 クライアント管理]** に移動します。

<!--- >[!NOTE]
>In the **What's New** workspace in the Configuration Manager console, the new dashboard is incorrectly named **Office 365 Servicing dashboard**. --->

ダッシュボードには、次のチャートが表示されます。

- Office 365 クライアントの数
- Office 365 クライアントのバージョン
- Office 365 クライアントのバージョン
- Office 365 クライアントのチャネル     
詳細については、「[Office 365 ProPlus 更新プログラム チャネルの概要](https://technet.microsoft.com/library/mt455210.aspx)」をご覧ください。
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

ダッシュボードの上部にある [**コレクション**] ドロップダウン設定を使用して、特定のコレクションのメンバーでダッシュボードのデータをフィルター処理します。

<!---
 On the upper-right side of the dashboard, click **Office 365 Installer** to start the Office 365 Client Installation Wizard to deploy Office 365 apps to clients. For details, see [Deploy Office 365 apps to clients](#deploy-office-365-apps-to-clients).
- On the middle-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new automatic deployment rule (ADR). To create an ADR for Office 365 apps, select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- On the lower-right side of the dashboard, click **Create Client Agent Settings** to open Client Agent settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings).
--->

## <a name="deploy-office-365-updates-with-configuration-manager"></a>Configuration Manager で Office 365 の更新プログラムを展開する
Configuration Manager で Office 365 の更新プログラムを展開するには、次の手順を使用します。

1.  Configuration Manager を使用して Office 365 クライアントの更新プログラムを管理するための[要件を確認します](https://technet.microsoft.com/library/mt628083.aspx) (このトピックの「**構成マネージャーを使用して Office 365 クライアントの更新を管理するための要件**」セクションを参照してください)。  

2.  Office 365 のクライアント更新プログラムを同期するための[ソフトウェア更新ポイントを構成します](../get-started/configure-classifications-and-products.md)。 分類の**更新プログラム**を設定して、製品の **Office 365 クライアント**を選択します。 Office 365 クライアント製品を選択できるようになるには、ソフトウェア更新プログラムを少なくとも 1 回同期しておく必要があります。 分類の**更新プログラム**を使用するには、ソフトウェア更新ポイントの構成後にソフトウェア更新プログラムを同期する必要があります。  

3.  Office 365 クライアントが Configuration Manager から更新プログラムを受信できるようにします。 そのためには、Configuration Manager クライアント設定またはグループ ポリシーを使用します。 次のいずれかの方法を使用してクライアントを有効にします。  
    - 方法 1: Configuration Manager バージョン 1606 以降では、Configuration Manager クライアント設定を使用して Office 365 のクライアント エージェントを管理できます。 この設定を構成し、Office 365 の更新プログラムを展開すると、Configuration Manager クライアント エージェントは、Office 365 のクライアント エージェントと通信して、配布ポイントから Office 365 の更新プログラムをダウンロードしてインストールします。 Configuration Manager は、Office 365 ProPlus クライアント エージェント設定のインベントリを取得します。
      1.  Configuration Manager コンソールで、**[管理]** > **[概要]** > **[クライアント設定]** の順にクリックします。  

      2.  クライアント エージェントを有効にする適切なデバイスの設定を開きます。 既定およびカスタムのクライアント設定の詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)」を参照してください。  

      3.  **[ソフトウェアの更新]** を選択し、**[Office 365 クライアント エージェントの管理を有効にする]** の設定に **[はい]** を設定します。  

    - 方法 2: Office 展開ツールまたはグループ ポリシーを使用して、Configuration Manager から [Office 365 クライアントが更新プログラムを受信できるようにします](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient)。  

4. [Office 365 の更新プログラムをクライアントに展開します](deploy-software-updates.md)。  

<!--  ## Add other languages for Office 365 update downloads
Beginning in Configuration Manager version 1610, you can add support for Configuration Manager to download updates for any languages supported by Office 365 regardless of whether they are supported in Configuration Manager.

### To add support to download updates for additional languages
Use the following procedure on the central administration site, or stand-alone primary site, where the software update point site system role is installed.
1. From a command prompt, type *wbemtest* as an administrative user to open the Windows Management Instrumentation Tester.
2. Click **Connect**, and then type *root\sms\site_<siteCode>*.
3. Click **Query**, and then run the following query:
   *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*
4. Double-click the object with the site code for the central administration site or stand-alone primary site.

5. Browse the properties for View Embedded.
3). Find the SMS_EmbeddedProperty instance with the PropertyName of "AdditionalUpdateLanguagesForO365"
4). Set Value2 to be additional languages, e.g.:  pt-pt,af-za,nn-no, and save
5). Right click to download an O365 update, choose languages from UI
6). Verify that the language packs got downloaded including the UI specified ones plus the SDK specified ones. Admin can check the content package share specified to verify this.
-->

<!-- ## Change the update channel after you enable Office 365 clients to receive updates from Configuration Manager
To change the update channel after you enable Office 365 clients to receive updates from Configuration Manager, you must distribute a registry key value change to Office 365 clients using group policy. Change the **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** registry key to use one of the following values:

- Current Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Deferred Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- First Release for Current Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- First Release for Deferred Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf
-->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->



<!--HONumber=Jan17_HO1-->


