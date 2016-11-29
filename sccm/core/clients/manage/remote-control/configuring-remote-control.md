---
title: "リモート コントロールの構成 | System Center Configuration Manager"
description: "System Center Configuration Manager でリモート コントロールをセットアップします。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: aea35afe970e20bc2b22f9ae3f413a3c735caae1


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>System Center Configuration Manager でのリモート コントロールの構成

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager でリモート コントロールを使用するには、次の構成手順を実行する必要があります。  

## <a name="how-to-enable-remote-control-and-configure-client-settings"></a>リモート コントロールを有効にして、クライアント設定を構成する方法  
 この手順に従って、リモート コントロールの既定のクライアント設定を構成し、階層内のすべてのコンピューターに適用します。 これらの設定を一部のコンピューターのみに適用する場合は、カスタム クライアント デバイス設定を作成して、リモート コントロール セッションを使用するコンピューターを含むコレクションに割り当てます。 カスタムのデバイス設定の作成方法の詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../../core/clients/deploy/configure-client-settings.md)」を参照してください。  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>リモート コントロールを有効にしてクライアント設定を構成するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [ **管理** ] ワークスペースで [ **クライアント設定**] をクリックします。  

3.  [既定のクライアント設定 ****] をクリックします。  

4.  **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]**をクリックします。  

5.  **既定**  ダイアログ ボックスで、をクリックして **リモート ツール**です。  

6.  必要なリモート コントロール、リモート アシスタンス、およびリモート デスクトップのクライアント設定の構成 構成できるリモート ツールのクライアント設定の一覧については、「[About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md#BKMK_RemoteToolsDeviceSettings)」 (System Center Configuration Manager でのクライアント設定について) トピックの「[Remote Tools](../../../../core/clients/deploy/about-client-settings.md)」 (リモート ツール) セクションを参照してください。  

    > [!NOTE]  
    >  表示される会社の名前を変更する、 **ConfigMgr リモート コントロール** ] ダイアログ ボックスの値を構成する **ソフトウェア センターで表示される組織名** で、 **コンピューター エージェント** クライアント設定します。  

    > [!IMPORTANT]  
    >  リモート アシスタンスまたはリモート デスクトップを使用するには、Configuration Manager コンソールを実行するコンピューターでインストールして、構成する必要があります。 リモート アシスタンスまたはリモート デスクトップをインストールおよび構成する方法の詳細については、Windows のドキュメントを参照してください。  

7.  [OK] **** をクリックして [既定の設定] **** ダイアログ ボックスを閉じます。  

 クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始する場合は、「 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)」を参照してください。  



<!--HONumber=Nov16_HO1-->


