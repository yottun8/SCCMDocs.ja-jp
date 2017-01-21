---
title: "クライアントの管理 | Microsoft Docs"
description: "System Center Configuration Manager でクライアントを管理する方法について説明します。"
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
caps.latest.revision: 17
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 238ef5814c0c1b832c28d63c9f3879e21a6c439b
ms.openlocfilehash: dfdb5a95b672d3858d094750625cb5f6ef50700d


---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>System Center Configuration Manager でクライアントを管理する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager クライアントがインストールされ、Configuration Manager サイトに正しく割り当てられると、**[デバイス]** ノードの **[資産とコンプライアンス]** ワークスペースと、**[デバイス コレクション]** ノードの 1 つまたは複数のコレクションにデバイスが表示されます。 デバイスまたはデバイスが含まれたコレクションを選択するときに、さまざまな管理操作を選択できます。 ただし、コンソールの他のワークスペースを使用するか、Configuration Manager コンソールを使用しないタスクを実行して、別の方法でクライアントを管理することもできます。  

 **[資産とコンプライアンス]** ワークスペースから Configuration Manager クライアントを管理するタスクの概要、および Configuration Manager クライアントの管理に役立つその他のタスクの詳細については、このトピックを参照してください。 クライアントの構成方法については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../core/clients/deploy/configure-client-settings.md)」を参照してください。  

> [!NOTE]  
>  Configuration Manager クライアントがインストールされていても、Configuration Manager コンソールに表示されない場合があります。 このシナリオは、クライアントがサイトに正常に割り当てられていない場合や、コンソールの更新やコレクション メンバーシップの更新が必要な場合に生じる可能性があります。  
>   
>  また、Configuration Manager クライアントがインストールされていないのに、デバイスがコンソールに表示されることもあります。 このシナリオは、デバイスが検出されているが、Configuration Manager クライアントのインストールと割り当てが行われていない場合に生じる可能性があります。 Exchange Server コネクタを使用する管理されるモバイル デバイスでは、Configuration Manager クライアントはインストールされません。 さらに、Microsoft Intune に登録されているデバイスには、Configuration Manager クライアントはインストールされません。  
>   
>  Configuration Manager コンソールで **[クライアント]** 列を使用して、Configuration Manager クライアントがインストールされていて Configuration Manager コンソールから管理できるかどうかを判断できます。  

##  <a name="a-namebkmkmanagingclientsdevicesnodea-manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a> [デバイス] ノードを使用してクライアントを管理する  
 [ **資産とコンプライアンス** ] ワークスペースの [ **デバイス** ] ノードから 1 つまたは複数のデバイスを管理するには、次の手順と表に従います。  

> [!IMPORTANT]  
>  デバイスの種類によっては、一部のオプションを使用できません。  

#### <a name="to-manage-clients-from-the-devices-node"></a>[デバイス] ノードを使用してクライアントを管理するには  

1.  Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。  

2.  [ **資産とコンプライアンス** ] ワークスペースで [ **デバイス**] をクリックします。  

3.  1 つまたは複数のデバイスを選んだ後、リボンから (またはデバイスを右クリックして) 次のいずれかのクライアント管理タスクを選びます。  

    -   **ユーザー デバイスのアフィニティ情報を管理する**  

         ソフトウェアをユーザーに効率的に展開するのに役立つ、ユーザーとデバイスの関連付けを構成できます。  

         「[System Center Configuration Manager でのユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)」を参照してください  

    -   **新規または既存のコレクションにデバイスを追加する**  

         これらのコレクション関連の操作を使用すると、ダイレクト規則を使用して、選択したデバイスをコレクションに迅速に追加できます。  

         [System Center Configuration Manager でのコレクションの操作とメンテナンス](../../../core/clients/manage/collections/operations-and-maintenance-for-collections.md)  

    -   **クライアント プッシュ ウィザードを使用してクライアントのインストールと再インストールを実行する**  

         クライアント プッシュ ウィザードを使用すると、Configuration Manager クライアントのインストールと再インストールを効率的に実行し、サイト構成オプションおよびクライアント プッシュ インストール用に指定した追加の client.msi プロパティを使用して、Windows を実行するコンピューターでクライアントを修復したり再構成したりできます。  

        > [!TIP]  
        >  Configuration Manager クライアントのインストール (および再インストール) を実行するには、さまざまな方法があります。 クライアント プッシュ ウィザードはコンソールから実行できるため、クライアントのインストールには便利な方法ですが、このクライアント インストール方法には数多くの依存関係があり、すべての環境に適しているわけではありません。 クライアント プッシュを使用してクライアントを正常にインストールできない場合は、他の多くのクライアント インストール方法を使用できます。 依存関係の詳細については、「[System Center Configuration Manager で Windows コンピューターにクライアントを展開するための前提条件](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)」を参照してください。 他のクライアント インストール方法の詳細については、「[System Center Configuration Manager でのクライアントのインストール方法](../../../core/clients/deploy/plan/client-installation-methods.md)」を参照してください。  

         「 [クライアント プッシュを使用した Configuration Manager クライアントのインストール方法](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)」を参照してください。  

    -   **サイトの再割り当て**  

         1 つまたは複数のクライアント (管理しているモバイル デバイスを含む) を、階層内の別のプライマリ サイトに再割り当てします。 新しいサイトへのクライアントの再割り当ては、個別に行うことも、複数のクライアントを選択して一括で行うこともできます。  

    -   **クライアントをリモート管理する**  

         リソース エクスプローラーを実行して、ハードウェアとソフトウェアのインベントリ情報を Windows クライアントから確認したり、リモート コントロール、リモート アシスタンス、またはリモート デスクトップを使用してこれらの情報をリモートで管理できます。  

         「[System Center Configuration Manager でリソース エクスプローラーを使用してハードウェア インベントリを表示する方法](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)」および「[System Center Configuration Manager でリソース エクスプローラーを使用してソフトウェア インベントリを表示する方法](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)」を参照してください。  

         「[System Center Configuration Manager を使用して Windows クライアント コンピューターをリモート管理する方法](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)」を参照してください。  

    -   **クライアントを承認する**  

         クライアントが HTTP および自己署名証明書を使用してサイト システムと通信する場合、信頼されるコンピューターとして識別されるように、これらのクライアントを承認する必要があります。 既定では、各クライアントを手動で承認せずに済むように、サイト構成により、同じ Active Directory フォレストおよび信頼されるフォレストのクライアントは自動的に承認されます。 ただし、信頼できるワークグループ コンピューター、および信頼できるが承認されていないその他のコンピューターは手動で承認する必要があります。  

        > [!WARNING]  
        >  一部の管理機能は承認されていないクライアントでも動作する可能性がありますが、このシナリオは Configuration Manager ではサポートされていません。  

         HTTP ではなく常に HTTPS を使用してサイト システムと通信するクライアントや、HTTP を使用してサイト システムと通信する際に PKI 証明書を使用するクライアントは、承認する必要はありません。 これらのクライアントは、PKI 証明書を使用して Configuration Manager との信頼を確立します。  

    -   **クライアントをブロックまたはブロック解除する**  

         信頼できなくなったクライアントをブロックして、このクライアントがクライアント ポリシーを受け取るのを防いだり、Configuration Manager サイト システムがこのクライアントと通信するのを防ぎます。  

        > [!WARNING]  
        >  クライアントをブロックすると、クライアントから Configuration Manager サイト システムへの通信のみ防ぐことができます。クライアントから他のデバイスへの通信を防ぐことはできません。 また、HTTPS の代わりに HTTP を使用してクライアントがサイト システムに通信する場合、セキュリティ上の制限がいくつか生じます。  

         後で変更が必要になった場合、ブロックしていたクライアントのブロックを解除できます。 ただし、ブロックしたときに AMT 用にプロビジョニングされていた Inel AMT 搭載コンピューターのブロックを解除する場合、そのコンピューターを再度、帯域外管理するためには、追加の手順を実行する必要があります。  

         「[System Center Configuration Manager でクライアントをブロックするかどうかの判断](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md)」を参照してください。  

    -   **必要な PXE 展開をクリアする**  

         このオプションを使用して、選択したコンピューターに必要な PXE 展開を再展開します。  

         「[System Center Configuration Manager で PXE を使用してネットワーク経由で Windows を展開する](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)」を参照してください。  

    -   **クライアントのプロパティを管理する**  

         クライアントを対象とした探索データと展開を表示できます。 また、オペレーティング システムをデバイスに展開するためにタスク シーケンスで使用される変数を構成することもできます。  

    -   **クライアントを削除する**  

        > [!WARNING]  
        >  Configuration Manager クライアントをアンインストールする場合やコレクションから削除する際、クライアントを削除しないでください。  

         **[削除]** 操作を実行して、Configuration Manager データベースからクライアント レコードを手動で削除します。通常、この操作は、トラブルシューティング以外では使用しないでください。 クライアント レコードを削除しても、Configuration Manager クライアントが引き続きインストールされており、Configuration Manager と通信している場合は、クライアント履歴と以前の関連付けは失われますが、定期探索によってクライアント レコードが再作成されて Configuration Manager コンソールに表示されます。  

        > [!NOTE]  
        >  Configuration Manager によって登録されているモバイル デバイス クライアントを削除すると、この操作により、モバイル デバイス クライアントに発行された PKI 証明書が失効し、IIS によって CRL がチェックされない場合でも、この証明書が管理ポイントで拒否されるようになります。 モバイル デバイス レガシ クライアントを削除しても、これらのクライアントの証明書は失効しません。  

         クライアントをアンインストールするには、「 [Configuration Manager クライアントのアンインストール](#BKMK_UninstalClient)」を参照してください。  

         クライアントを新しいプライマリ サイトに割り当てるには、「[System Center Configuration Manager でクライアントをサイトに割り当てる方法](../../../core/clients/deploy/assign-clients-to-a-site.md)」を参照してください。  

         クライアントをコレクションから削除するには、コレクションのプロパティを再構成します。 「[System Center Configuration Manager でコレクションを管理する方法](../../../core/clients/manage/collections/manage-collections.md)」を参照してください。  

    -   **モバイル デバイスをワイプする**  

         ワイプ コマンドをサポートするモバイル デバイスをワイプできます。  

         この操作により、個人設定や個人データを含め、モバイル デバイスのすべてのデータが削除されます。 通常、この操作で、モバイル デバイスが工場出荷時の設定にリセットされます。 モバイル デバイスは、紛失や盗難にあうなど、信頼できなくなった場合にワイプします。  

        > [!TIP]  
        >  モバイル デバイスでリモート ワイプ コマンドがどのように処理されるかについては、製造元のドキュメントを参照してください。  

         ワイプ要求を送信すると、モバイル デバイスがワイプ コマンドを受信するまで、通常、待ち時間が発生します。  

        -   モバイル デバイスが Configuration Manager または Microsoft Intune によって登録されている場合、クライアントは、クライアント ポリシーの次回ダウンロード時にワイプ コマンドを受信します。  

        -   モバイル デバイスが Exchange Server コネクタによって管理されている場合、モバイル デバイスは、Exchange との次回同期時にワイプ コマンドを受信します。  

         [ **ワイプのステータス** ] 列を使用して、モバイル デバイスがワイプ コマンドをいつ受信するのかを監視できます。 モバイル デバイスが Configuration Manager にワイプ確認を送信するまで、ワイプ コマンドをキャンセルできます。  

    -   **モバイル デバイスをインベントリから削除する**  

         **[インベントリから削除]** オプションをサポートしているのは、Intune に登録されたか、\-オンプレミス モバイル デバイス管理で登録されたモバイル デバイスのみです。  

         詳細については、「 [System Center Configuration Manager によるリモート ワイプ、リモート ロック、パスコードのリセットを使用したデータの保護](../../../mdm/deploy-use/wipe-lock-reset-devices.md)」をご覧ください。  

    -   **デバイスの所有権を変更する**  

         デバイスがドメインに参加しておらず、Configuration Manager クライアントがインストールされていない場合は、デバイスの所有権を **[会社]** または **[個人]** に変更できます。  

         アプリケーションの要件にこの値を使用して、展開を制御できます。また、この構成を使用して、ユーザー デバイスから収集するインベントリの量を制御できます。  

        デバイス リストで所有権値を表示するには、ビューに列を追加する必要が生じることがあります。そうするには、任意の列見出しを右クリックして **[デバイスの所有者]**を選びます。

         詳細については、「[System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM)](../../../mdm/understand/hybrid-mobile-device-management.md)」を参照してください。  

##  <a name="a-namebkmkmanagingclientsdevicecollectionsnodea-manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> [デバイス コレクション] ノードを使用してクライアントを管理する  
 [ **資産とコンプライアンス** ] ワークスペースの [ **デバイス コレクション** ] ノードからコレクション内のデバイスを管理するには、次の手順と表に従います。  

 [ **デバイス** ] ノードから単一のデバイスまたは複数のデバイスを選択する場合に実行できるクライアント管理タスクの多くは、コレクション レベルでも実行できます。 そのため、管理タスクをコレクション内の適合するすべてのデバイスに自動的に適用できるというメリットがあります。 この方法は、複数のクライアントを同時に管理するのに便利ですが、大量のネットワーク パケットが生成されてサイト サーバーの CPU 使用率が高くなる可能性があります。  

 次の表に示すように、コレクション レベルでのみ実行できるクライアント管理タスクもあります。  

 コレクション レベルのクライアント管理タスクを実行する前に、コレクションにどの程度の数のデバイスが含まれているのか、それらのデバイスが低帯域幅のネットワーク接続で接続されていないかどうか、およびすべてのデバイスでタスクを完了するのにどの程度の時間がかかるのかを検討します。 クライアント管理タスクを実行する際、タスクをコンソールから停止することはできません。  

#### <a name="to-manage-clients-from-the-device-collections-node"></a>[デバイス コレクション] ノードを使用してクライアントを管理するには  

1.  Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。  

2.  [ **資産とコンプライアンス** ] ワークスペースで [ **デバイス コレクション**] をクリックします。  

3.  コレクションを選んだ後、リボンから (またはコレクションを右クリックして) 次のいずれかのクライアント管理タスクを選びます。  

    -   **マルウェアがないかどうかコンピューターをスキャンし、マルウェア対策の定義ファイルをダウンロードする**  

         「[System Center Configuration Manager での Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)」を参照してください。  

    -   **ソフトウェア、構成基準、タスク シーケンスを展開する**  

         ソフトウェアと構成基準の展開の詳細については、以下を参照してください。  

        -   [System Center Configuration Manager でのソフトウェア更新プログラムの展開](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [System Center Configuration Manager におけるコンプライアンス設定の計画と構成](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **電源管理設定を構成する**  

         「[System Center Configuration Manager で電源プランを作成して適用する方法](../../../core/clients/manage/power/create-and-apply-power-plans.md)」を参照してください。 電源プランは Windows を実行するコンピューターにのみ使用できます。  

    -   **直ちにポリシーをダウンロードするようにコンピューターに通知する**  

         クライアント通知を使用して、構成したクライアント ポリシーのポーリング間隔に関係なく、直ちにコンピューター ポリシーをダウンロードするように、選択した Windows クライアントに通知します。  

         クライアント通知タスクは、[ **監視** ] ワークスペースの [ **クライアントの操作** ] ノードに表示されます。  

##  <a name="a-namebkmkclientcachea-configure-the-client-cache-for-configuration-manager-clients"></a><a name="BKMK_ClientCache"></a> Configuration Manager クライアントにクライアントキャッシュを構成する  
 Windows Configuration Manager クライアントがアプリケーションとプログラムをインストールする際に備えて一時ファイルを格納するために使用する、場所とディスク容量を構成できます。 ソフトウェアの更新ではクライアント キャッシュも使用されますが、ソフトウェアの更新は構成されているキャッシュ サイズには制限されず、常にキャッシュへのダウンロードが試みられます。 Configuration Manager クライアントを手動でインストールする際、クライアント プッシュ インストールを使用する際、またはクライアントのインストール後に、クライアント キャッシュ設定を構成できます。

Configuration Manager バージョン 1606 では、Configuration Manager コンソールでクライアント設定を使用してキャッシュ フォルダー サイズを指定できます。   

 Configuration Manager クライアント キャッシュの既定の場所は %*windir*%\ccmcache で、既定のディスク容量は 5120 MB です。  

> [!IMPORTANT]  
>  クライアント キャッシュに使用するフォルダーは暗号化しないでください。 Configuration Manager は暗号化されたフォルダーにコンテンツをダウンロードすることはできません。  

### <a name="about-client-cache"></a>クライアント キャッシュについて  

Configuration Manager クライアントは、展開を受けた後まもなく要求されたソフトウェアのコンテンツをダウンロードしますが、スケジュールされた展開時刻まで、それを実行しません。 スケジュールされた時刻になると、Configuration Manager クライアントはコンテンツがキャッシュで利用可能かどうかを確認します。 キャッシュにコンテンツがあり、それが正しいバージョンの場合は、クライアントは必ずこのキャッシュされたコンテンツを使用します。 しかし、要求されたコンテンツのバージョンが変更されたり、別のパッケージを入れるためにコンテンツが削除された場合は、コンテンツはキャッシュに再びダウンロードされます。  

クライアントがキャッシュのサイズより大きいプログラム コンテンツまたはアプリケーション コンテンツをダウンロードしようとすると、Configuration Manager はステータス メッセージ ID 10050 を生成します。 キャッシュ サイズが後で拡大された場合、要求されるプログラムとアプリケーションでダウンロード再試行動作が変わります。  

-   要求されるプログラムの場合:クライアントは、コンテンツのダウンロードを自動的に再試行しません。 パッケージとプログラムを再度展開する必要があります。  
-   要求されるアプリケーションの場合:アプリケーションの展開は状態ベースで行われるので、クライアントは、クライアント ポリシーを次にダウンロードするときに、自動的にコンテンツのダウンロードを再試行します。  

クライアントがダウンロードしようとするパッケージのサイズがキャッシュ サイズより小さくても、現在キャッシュに空きがない場合、キャッシュ領域が利用可能になるまで、またはダウンロードがタイムアウトするまで、あるいはキャッシュ領域による失敗の再試行回数の上限まで、要求された展開は再試行を繰り返します。 キャッシュ サイズが後で拡大されると、Configuration Manager クライアントは、次回の再試行時に再びパッケージのダウンロードを試みます。 クライアントは 4 時間ごとに 18 回になるまでコンテンツのダウンロードを試みます。  

キャッシュされたコンテンツは自動的には削除されず、クライアントがコンテンツを使用した後、少なくとも 1 日の間キャッシュに保持されます。 パッケージのプロパティを、クライアント キャッシュの内容を保持するオプションで構成すると、クライアントはキャッシュからコンテンツを自動的に削除しません。 クライアント キャッシュ領域が、24 時間以内にダウンロードされたパッケージによって使用されているときに、新しいパッケージをダウンロードする必要がある場合は、キャッシュ サイズを拡張するか、削除オプションを使って、保持しているキャッシュ コンテンツを削除できます。  

 手動によるクライアントのインストール中またはクライアントのインストール後に、クライアント キャッシュを構成するには、次の手順を使用します。  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>手動によってクライアントをインストールするときにクライアント キャッシュを構成するには  

必要に応じて次のプロパティを指定して、インストール ソースの場所から CCMSetup.exe コマンドを実行します。プロパティはスペースで区切ります。  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > バージョン 1606 では、SMSCACHESIZE ではなく Configuration Manager コンソールの **[クライアント設定]** で使用可能なキャッシュ サイズ設定を使用します。 詳細については、「[クライアントのキャッシュ設定](../../../core/clients/deploy/about-client-settings.md#client-cache-settings)」を参照してください。

CCMSetup.exe 用のこれらのコマンド ライン プロパティを使用する方法の詳細については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」を参照してください。  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>クライアント プッシュ インストールによってクライアントをインストールするときにクライアント キャッシュを構成するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [ **管理** ] ワークスペースで [ **サイトの構成**] を展開して、[ **サイト**] をクリックします。  

3.  [ **サイト** ] 一覧で、サイト全体の自動クライアント プッシュ インストールを構成するサイトを選択します。  

4.  [ **ホーム** ] タブの [ **設定** ] グループで、[ **クライアント インストール設定**] をクリックし、[ **インストールのプロパティ**] タブを選択します。  

5.  [ **インストールのプロパティ** ] タブで、必要に応じて次のプロパティを指定します。プロパティはスペースで区切ります。  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > バージョン 1606 では、SMSCACHESIZE ではなく Configuration Manager コンソールの **[クライアント設定]** で使用可能なキャッシュ サイズ設定を使用します。 詳細については、「[クライアントのキャッシュ設定](../../../core/clients/deploy/about-client-settings.md#client-cache-settings)」を参照してください。

       CCMSetup.exe 用のこれらのコマンド ライン プロパティを使用する方法の詳細については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」を参照してください。  

6.  [ **OK** ] をクリックして、指定したプロパティを保存します。  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>クライアント コンピューターでクライアント キャッシュ フォルダーを構成するには  

1.  クライアント コンピューターで、コントロール パネルの [ **Configuration Manager** ] に移動し、ダブルクリックしてプロパティを開きます。  

2.  [ **キャッシュ** ] タブをクリックします。  

3.  クライアント キャッシュにあてるディスク領域を指定します。  

4.  クライアント キャッシュ フォルダーの場所を変更するには、[ **場所の変更**] をクリックして、新しい場所を指定します。 既定の場所は *%windir%*\ccmcache です。  

5.  クライアント キャッシュ フォルダーに現在格納されているファイルを削除するには、[ **ファイルの削除**] をクリックします。  

6.  [ **OK** ] をクリックして [ **Configuration Manager のプロパティ**] を閉じます。  

### <a name="to-configure-client-cache-size-in-client-settings"></a>[クライアント設定] でクライアント キャッシュ サイズを構成するには

バージョン 1606 以降、クライアントを再インストールしなくても、クライアント キャッシュ フォルダーのサイズを調整できるようになりました。 これを行うには、Configuration Manager コンソールで [クライアント設定] を使用してクライアント キャッシュ サイズを構成します。  

1. Configuration Manager コンソールで、 **[管理]** > **[クライアント設定]**に移動します。

2. **[既定のクライアント設定]**をダブルクリックします。
  また、キャッシュ サイズをより選択的に適用するためにカスタム クライアント設定を作成することもできます。 既定およびカスタムのクライアント設定の詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../core/clients/deploy/configure-client-settings.md)」を参照してください。

 3. **[クライアントのキャッシュ設定]** をクリックして、 **[クライアント キャッシュ サイズを構成する]** に **[はい]**を選びます。

 4. **[MB]** または **[ディスクの割合を設定]**を使用して、最大キャッシュ サイズを調整します。 いずれか小さい方のサイズにキャッシュが調整されます。

 5. **[OK]**をクリックします。

    Configuration Manager クライアントは、次のクライアント ポリシーがダウンロードされるときにこれらの設定値を使ってキャッシュ サイズを構成します。

##  <a name="a-namebkmkuninstalclienta-uninstall-the-configuration-manager-client"></a><a name="BKMK_UninstalClient"></a> Configuration Manager クライアントをアンインストールする  
 **/Uninstall** プロパティを付けて **CCMSetup.exe** を使用すると、Windows Configuration Manager クライアント ソフトウェアをコンピューターからアンインストールできます。 個々のコンピューター上でコマンド プロンプトから CCMSetup.exe を実行するか、パッケージとプログラムを展開して、コンピューターのコレクションからクライアントをアンインストールします。  

> [!WARNING]  
>  Configuration Manager クライアントをモバイル デバイスからアンインストールすることはできません。 Configuration Manager クライアントをモバイル デバイスから除去する必要がある場合は、デバイスをワイプする必要があります。ワイプはモバイル デバイス上のすべてのデータを削除します。  

 次の手順に従って、Configuration Manager クライアントをコンピューターからアンインストールします。  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>コマンド プロンプトから Configuration Manager クライアントをアンインストールするには  

1.  Windows コマンド プロンプトを開き、CCMSetup.exe のある場所へフォルダーを移動します。  

2.  「 **Ccmsetup.exe /uninstall**」と入力し、 **Enter**キーを押します。  

> [!NOTE]  
>  アンインストール処理はサイレントで実行され、画面に結果は表示されません。 クライアントのアンインストールが成功したことを確認するには、クライアント コンピューター上の **%windir%\ ccmsetup** フォルダー内にあるログ ファイル *CCMSetup.log* を確認します。  

##  <a name="a-namebkmkconflictingrecordsa-manage-conflicting-records-for-configuration-manager-clients"></a><a name="BKMK_ConflictingRecords"></a> Configuration Manager クライアントの競合しているレコードを管理する  
 Configuration Manager は、ハードウェア ID を使用して重複している可能性のあるクライアントを特定し、競合するレコードについて警告を発します。 たとえば、コンピューターを再インストールする場合、ハードウェア ID が同じであっても Configuration Manager の使用する GUID が異なる可能性があります。  

 コンピューター アカウントの Windows 認証または信頼されたソースからの PKI 証明書を使用して Configuration Manager が競合を解決できる場合、競合は自動的に解決されます。 ただし、Configuration Manager が競合を解決できない場合は階層設定が使用され、重複するハードウェア ID を検出したときにレコードを自動的にマージするか (既定の設定)、新しいクライアント レコードをマージ、ブロック、または作成するタイミングを管理者が決定できます。 重複レコードを手動で管理すると決定した場合、Configuration Manager コンソールを使用して競合するレコードを手動で解決する必要があります。  


#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>競合しているレコードの管理に関する階層の設定を変更するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [ **管理** ] ワークスペースで [ **サイトの構成**] を展開して、[ **サイト**] をクリックします。  

3.  [ **サイト** ] グループで、[ **階層設定**] をクリックして、[ **クライアントの承認と競合レコードの処理** ] タブをクリックします。  

4.  競合しているレコードを自動的に結合する場合は [ **競合しているレコードを自動的に解決する** ] をクリックし、さもなければ [ **競合しているレコードを手動で解決する**] をクリックしてから、[ **OK**] をクリックします。  

    > [!NOTE]  
    >  Configuration Manager がコンピューター アカウントまたは PKI 証明書を使って競合が解決できるときは、この設定は無視され、競合は自動的に解決されます。  

#### <a name="to-manually-resolve-conflicting-records"></a>競合しているレコードを手動で解決するには  

1.  Configuration Manager コンソールで、**[監視]** をクリックします。  

2.  [ **監視** ] ワークスペースで、[ **システムのステータス**] を展開してから、[ **競合しているレコード**] をクリックします。  

3.  結果ウィンドウで 1 つまたは複数の競合しているレコードを選択し、[ **競合しているレコード**] をクリックします。  

4.  [ **競合しているレコード** ] ダイアログ ボックスで、次のうちの 1 つを選択し、[ **OK**] をクリックします。  

    -   [**結合** ]: 新しく検出されたレコードを既存のクライアント レコードと結合して、1 つの統合されたレコードを作成します。  

    -   [**新規** ]: 競合しているクライアント レコードに対して新しいレコードを作成します。  

    -   [**ブロック** ]: 競合しているクライアント レコードに対して新しいレコードを作成しますが、ブロックに設定します。  

## <a name="manage-duplicate-hardware-identifiers"></a>重複するハードウェア識別子を管理する
Configuration Manager バージョン 1610 より、PXE ブートとクライアント登録で Configuration Manager が無視するハードウェア ID の一覧を指定できます。 それにより 2 つの一般的な問題に対処できます。

1. Surface Pro 3 など、新しいデバイスの多くにオンボード イーサネット ポートが含まれません。 オペレーティング システムの展開で有線接続を確立するとき、一般的に USB/イーサネット アダプターが使用されます。 しかしながら、コストや汎用性に起因し、多くの場合、共有アダプターになります。 そのアダプターの MAC アドレスを利用してデバイスを識別するため、展開ごとに管理者による追加措置がないと、アダプターの再利用が問題になります。 Configuration Manager の現行の Branch Version 1610 では、このアダプターの MAC アドレスを除外できます。そのため、このシナリオで簡単に再利用できます。
2. SMBIOS ID は一意のハードウェア識別子ですが、専門的なハードウェア デバイスには ID が重複するものもあります。 上記の USB/イーサネット アダプターのシナリオほど一般的ではありませんが、ハードウェア ID の一覧を利用してこの問題に対処することもできます。

#### <a name="to-add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Configuration Manager で無視するハードウェア識別子を追加するには  
1. Configuration Manager コンソールで、[**管理**] > [**概要**] > [**サイトの構成**] > [**サイト**] の順に移動します。
2. **[ホーム]** タブの **[サイト]** グループで、 **[階層設定]**をクリックします。
3. [**クライアントの承認と競合レコードの処理**] タブに移動します。
4. [**重複するハードウェア ID**] セクションで [**追加**] をクリックして 新しいハードウェア識別子を追加します。

##  <a name="a-namebkmkpolicyretrievala-initiate-policy-retrieval-for-a-configuration-manager-client"></a><a name="BKMK_PolicyRetrieval"></a> Configuration Manager クライアントのポリシーの取得開始  
 Windows Configuration Manager クライアントは、クライアント設定として構成されているスケジュールに従ってクライアント ポリシーをダウンロードします。 ただし、トラブルシューティングのシナリオやテストなどで、クライアントからアドホックなポリシー取得を開始するケースもあり得ます。  

 次の手順に従って、Configuration Manager クライアントの  [ **操作** ] タブを使用するか、コンピューターでスクリプトを実行することにより、クライアントから特別なポリシー取得をスケジュールされたポーリング間隔以外で開始します。 この手順を実行するには、ローカル管理者権限でクライアント コンピューターにログオンしている必要があります。  

> [!NOTE]  
>  クライアント通知を使用して、スケジュールしたクライアント ポリシーのポーリング間隔に関係なく、クライアント ポリシーの取得を開始することができます。  
>   
>  Linux および UNIX を実行しているクライアントを管理できます。 Linux および UNIX を実行するクライアントのポリシー取得については、「 [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU)」をご覧ください。  

#### <a name="to-initiate-client-policy-retrieval-by-using-client-notification"></a>クライアント通知を使用してクライアント ポリシーの取得を開始するには  

1.  Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。  

2.  [ **資産とコンプライアンス** ] ワークスペースで [ **デバイス コレクション**] をクリックします。  

3.  ポーリングをダウンロードするコンピューターを含むデバイス コレクションを選択します。次に、[ **ホーム** ] タブの [ **コレクション** ] グループで、[ **クライアント通知** ] をクリックし、[ **コンピューター ポリシーのダウンロード**] をクリックします。  

    > [!NOTE]  
    >  また、[ **デバイス** ] ノードの一時コレクション ノードに表示されるデバイスから 1 つまたは複数のデバイスを選択して、クライアント通知を使用してポリシーの取得を開始することもできます。  

#### <a name="to-manually-initiate-client-policy-retrieval-by-using-the-actions-tab-on-the-configuration-manager-client"></a>Configuration Manager クライアントの [操作] タブを使用してクライアント ポリシーの取得を手動で開始するには  

1.  コンピューターのコントロール パネルで、[ **Configuration Manager** ] を選択します。  

2.  [ **操作** ] タブをクリックします。  

3.  **[コンピューター ポリシーの取得および評価サイクル]** をクリックしてコンピューター ポリシーを開始し、**[直ちに実行]** をクリックします。  

4.  **[OK]** をクリックしてプロンプトを確定します。  

5.  ユーザー クライアント設定で必要な他の操作 (**[ユーザー ポリシーの取得および評価サイクル]** など) に関して、手順 3 と 4 を繰り返します。  

6.  [ **OK** ] をクリックして [ **Configuration Manager のプロパティ**] を閉じます。  

#### <a name="to-manually-initiate-client-policy-retrieval-by-using-a-script"></a>スクリプトを使用してクライアント ポリシーの取得を手動で開始するには  

1.  メモ帳などのテキスト エディターを開きます。  

2.  次をコピーし、ファイルに挿入します。  

    ```  
    on error resume next  

    dim oCPAppletMgr 'Control Applet manager object.  
    dim oClientAction 'Individual client action.  
    dim oClientActions 'A collection of client actions.  

    'Get the Control Panel manager object.  
    set  oCPAppletMgr=CreateObject("CPApplet.CPAppletMgr")  
    if err.number <> 0 then  
        Wscript.echo "Couldn't create control panel application manager"  
        WScript.Quit  
    end if  

    'Get a collection of actions.  
    set oClientActions=oCPAppletMgr.GetClientActions  
    if err.number<>0 then  
        wscript.echo "Couldn't get the client actions"  
        set oCPAppletMgr=nothing  
        WScript.Quit  
    end if  

    'Display each client action name and perform it.  
    For Each oClientAction In oClientActions  

        if oClientAction.Name = "Request & Evaluate Machine Policy" then  
            wscript.echo "Performing action " + oClientAction.Name   
            oClientAction.PerformAction  
        end if  
    next  

    set oClientActions=nothing  
    set oCPAppletMgr=nothing  
    ```  

3.  ファイルを .vbs 拡張子で保存します。  

4.  クライアント コンピューターにおいて、次のいずれかの方法でこのファイルを実行します。  

    -   エクスプローラーを使用してファイルに移動し、スクリプト ファイルをダブルクリックします。  

    -   コマンド プロンプトを開き、「**cscript &lt;パス\ファイル名.vbs>**」と入力します。  

5.  [ **Windows スクリプト ホスト** ] ダイアログ ボックスで、[ **OK** ] をクリックします。  



<!--HONumber=Dec16_HO3-->


