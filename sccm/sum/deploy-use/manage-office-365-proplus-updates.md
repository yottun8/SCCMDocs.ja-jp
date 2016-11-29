---

title: "Office 365 ProPlus の更新プログラムの管理 | Configuration Manager"
description: "Configuration Manager が WSUS カタログからサイト サーバーに Office 365 のクライアント更新プログラムを同期したら、その更新プログラムをクライアントに展開できるようになります。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 58a551425591332264592713fa3cc4e04d9939aa


---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>Configuration Manager での Office 365 ProPlus の更新プログラムの管理

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager バージョン 1602 以降では、ソフトウェア更新管理のワークフローを使用して、Office 365 クライアントの更新プログラムを管理できます。 マイクロソフトが Office コンテンツ配信ネットワーク (CDN) に対する新しい Office 365 のクライアント更新プログラムを公開するときには、Windows Server Update Services (WSUS) に対する更新パッケージも公開します。 Configuration Manager が WSUS カタログからサイト サーバーに Office 365 クライアント更新プログラムを同期したら、その更新プログラムをクライアントに展開できるようになります。

#### <a name="to-deploy-office-365-updates-with-configuration-manager"></a>Configuration Manager で Office 365 の更新プログラムを展開するには
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



<!--HONumber=Nov16_HO1-->


