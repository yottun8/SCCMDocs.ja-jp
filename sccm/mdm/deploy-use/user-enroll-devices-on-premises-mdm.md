---
title: 'ユーザーがオンプレミス MDM にデバイスを登録する方法 '
titleSuffix: Configuration Manager
description: System Center Configuration Manager でのオンプレミス モバイル デバイス管理の対象となるデバイスをユーザーが登録する方法について説明します。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15774704665b2b52daf1061db221ab0eb158eceb
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347520"
---
# <a name="how-users-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>System Center Configuration Manager でのオンプレミス モバイル デバイス管理の対象となるデバイスをユーザーが登録する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager オンプレミス モバイル デバイス管理では、ユーザーがデバイスを登録できます。ただし、ユーザーに登録権限が付与され (そのためにはクライアント設定を更新します)、ユーザーのデバイスにルート証明書がインストールされ、それによりデバイスが必須のサイト システムの役割をホストしているサーバーと信頼できる通信を行えるようになっている必要があります。 登録をセットアップする方法の詳細については、「[System Center Configuration Manager でのオンプレミスのモバイル デバイス管理のデバイス登録の設定](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)」を参照してください。  

> [!NOTE]  
>  Configuration Manager の現在のブランチでは、次のオペレーティング システムを実行しているデバイスをオンプレミス モバイル デバイス管理で登録することができます。  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team\( Configuration Manager バージョン 1602 以降\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

次のタスクでは、オンプレミスのモバイル デバイス管理の対象となるコンピューターとデバイスを登録し、その登録を検証する方法について説明します。  

-   [Windows 10 コンピューターの登録](#bkmk_enrollDesk)  

-   [Windows 10 Mobile デバイスの登録](#bkmk_enrollMob)  

-   [デバイス登録の確認](#bkmk_verify)  

##  <a name="bkmk_enrollDesk"></a> Windows 10 コンピューターの登録  

1.  Windows 10 コンピューターで、 **[設定]** に移動します。  

2.  **[アカウント]** をクリックし、 **[職場のアクセス]** をクリックします。  

3.  [職場のアクセス] の **[職場または学校への接続]** で、 **[接続]** をクリックし、職場の電子メール アドレスを入力し、 **[続行]** をクリックします。  

4.  登録プロキシ ポイント サイト システムの役割をホストしているサーバーの FQDN を入力し、**[続行]** をクリックします。  

5.  [サービスに接続しています] で、職場の電子メールのパスワードを入力し、 **[サインイン]** をクリックします。  

6.  サインイン情報を記憶するために **[スキップ]** をクリックします。少し経つと、デバイスが接続されます。  

##  <a name="bkmk_enrollMob"></a> Windows 10 Mobile デバイスの登録  

1.  Windows 10 Mobile デバイスで、 **[設定]** に移動します。  

2.  **[アカウント]** をクリックし、 **[職場のアクセス]** をクリックします。  

3.  **[接続]** をクリックします。  

4.  職場の電子メール アドレスと、登録プロキシ ポイント サイト システムの役割をホストしているサーバーの FQDN を入力します。 **[接続]** をクリックします。  

5.  次の画面で、職場の電子メール アドレスとパスワードを入力し、 **[サインイン]** をクリックします。 少し経つと、デバイスが登録されます。 **[完了]** をクリックします。  

##  <a name="bkmk_verify"></a> デバイス登録の確認  
 Configuration Manager コンソールで、デバイスが正常に登録されていることを確認できます。  

1.  Configuration Manager コンソールを起動します。  

2.  [資産とコンプライアンス][概要][デバイス]が必要とするサイト システムの役割との間で信頼された通信を行うために必要です。 登録されているデバイスが一覧に表示されます。  
