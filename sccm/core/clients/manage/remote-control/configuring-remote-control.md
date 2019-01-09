---
title: リモート コントロールの構成
titleSuffix: Configuration Manager
description: System Center Configuration Manager でリモート コントロールをセットアップします。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fac81f08f4750ab6cc133ddc3a3bb9f73780fcd
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422540"
---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>System Center Configuration Manager でのリモート コントロールの構成

*適用対象:System Center Configuration Manager (Current Branch)*

 この手順では、リモート コントロールの既定のクライアント設定を構成する方法について説明します。 これらの設定は、階層内のすべてのコンピューターに適用されます。 これらの設定を一部のコンピューターのみに適用する必要がある場合は、カスタム クライアント デバイス設定を、これらのコンピューターを含むコレクションに割り当てます。 詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../../core/clients/deploy/configure-client-settings.md)」をご覧ください。 

リモート アシスタンスまたはリモート デスクトップを使用するには、Configuration Manager コンソールを実行するコンピューターでインストールして、構成する必要があります。 リモート アシスタンスまたはリモート デスクトップをインストールおよび構成する方法の詳細については、Windows のドキュメントを参照してください。  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>リモート コントロールを有効にしてクライアント設定を構成するには  

1. Configuration Manager コンソールで、**[管理]** > **[クライアント設定]** > **[既定のクライアント設定]** の順に選択します。  

2. **[ホーム]** タブの **[プロパティ]** グループで、**[プロパティ]** を選択します。  

3. **[既定]** ダイアログ ボックスで、**[リモート ツール]** を選択します。  

4. リモート コントロール、リモート アシスタンス、およびリモート デスクトップのクライアント設定を構成します。 構成できるリモート ツールのクライアント設定の一覧については、「[リモート ツール](../../../../core/clients/deploy/about-client-settings.md#remote-tools)」を参照してください。  

   表示される会社の名前を変更する、 **ConfigMgr リモート コントロール**  ダイアログ ボックスの値を構成する **ソフトウェア センターで表示される組織名** で、 **コンピューター エージェント** クライアント設定します。  

   クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始する場合は、「 [System Center Configuration Manager でクライアントを管理する方法](../../../../core/clients/manage/manage-clients.md)」を参照してください。  

#### <a name="enable-keyboard-translation"></a>キーボード変換を有効にする

既定では、Configuration Manager は、キーの位置をビューアーの場所から共有先の場所に転送します。 このため、ビューアーと共有先でキーボードの構成が異なる場合に問題が生じる可能性があります。 たとえば、英語キーボードを使用しているビューアーが「A」を入力しても、共有先のフランス語キーボードでは「Q」となってしまいます。 文字そのものがビューアーのキーボードから共有先に送信され、ビューアーが入力したものが共有先に届くようにリモート コントロールを構成するオプションが利用できるようになりました。

キーボード変換を有効にするには、**[Configuration Manager のリモート コントロール]** で **[アクション]** を選択し、**[キーボード変換を有効にする]** を選択してキーの位置を送信します。

> [!NOTE]
>
> ~!#@$% などの特殊なキーは、正しく変換されません。


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>リモート コントロール ビューアー用のキーボード ショートカット

|ショートカット キー|説明|  
|-----------------------|-----------------|  
|Alt + PageUp|実行しているプログラムの間を左から右へ切り替えます。|  
|Alt + PageDown|実行しているプログラムの間を右から左へ切り替えます。|  
|Alt + Insert|実行しているプログラムを開いた順に繰り返し表示します。|  
|Alt + Home|**[開始]** メニューを表示します。|  
|Ctrl + Alt + End|Windows セキュリティ ダイアログ ボックス (Ctrl+Alt+Del) を表示します。|  
|Alt + Delete キー|Windows メニューを表示します。|  
|Ctrl + Alt + (テンキーの) マイナス記号|ローカル コンピューターのアクティブ ウィンドウをリモート コンピューターのクリップボードにコピーします。|  
|Ctrl + Alt + (テンキーの) プラス記号|ローカル コンピューターのウィンドウ領域全体をリモート コンピューターのクリップボードにコピーします。|  
