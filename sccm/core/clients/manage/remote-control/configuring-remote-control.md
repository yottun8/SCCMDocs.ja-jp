---
title: "リモート コントロールの構成 |Microsoft Docs"
description: "System Center Configuration Manager でリモート コントロールをセットアップします。"
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: dudeso
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
ms.sourcegitcommit: 88828e68bc4aff216e83807ea8288c7d42c60cbd
ms.openlocfilehash: cbfa9dc6cb37518c0a561700272cc882b0041350


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>System Center Configuration Manager でのリモート コントロールの構成

*適用対象: System Center Configuration Manager (Current Branch)*

 この手順に従って、リモート コントロールの既定のクライアント設定を構成し、階層内のすべてのコンピューターに適用します。 これらの設定を一部のコンピューターのみに適用する場合は、カスタム クライアント デバイス設定を作成して、リモート コントロール セッションを使用するコンピューターを含むコレクションに割り当てます。 詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../../core/clients/deploy/configure-client-settings.md)」をご覧ください。 

リモート アシスタンスまたはリモート デスクトップを使用するには、Configuration Manager コンソールを実行するコンピューターでインストールして、構成する必要があります。 リモート アシスタンスまたはリモート デスクトップをインストールおよび構成する方法の詳細については、Windows のドキュメントを参照してください。  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>リモート コントロールを有効にしてクライアント設定を構成するには  

1.  Configuration Manager コンソールで、**[管理]** > **[クライアント設定]** > **[既定のクライアント設定]** の順に選択します。  

4.  **[ホーム]** タブの **[プロパティ]** グループで、**[プロパティ]** を選択します。  

5.  **[既定]** ダイアログ ボックスで、**[リモート ツール]** を選択します。  

6.  リモート コントロール、リモート アシスタンス、およびリモート デスクトップのクライアント設定を構成します。 構成できるリモート ツールのクライアント設定の一覧については、「[リモート ツール](../../../../core/clients/deploy/about-client-settings.md#remote-tools)」を参照してください。  

    表示される会社の名前を変更する、 **ConfigMgr リモート コントロール** ] ダイアログ ボックスの値を構成する **ソフトウェア センターで表示される組織名** で、 **コンピューター エージェント** クライアント設定します。  

 クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始する場合は、「 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)」を参照してください。  



<!--HONumber=Dec16_HO1-->


