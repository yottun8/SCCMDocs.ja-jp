---
title: "リモート コントロールのセキュリティとプライバシー | System Center Configuration Manager"
description: "System Center Configuration Manager のリモート コントロールのセキュリティとプライバシーの情報を確認します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9b36c01e6ea3a5e63523b5e32b151c0b972f9877


---
# <a name="security-and-privacy-for-remote-control-in-system-center-configuration-manager"></a>System Center Configuration Manager のリモート コントロールのセキュリティとプライバシー

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックには、System Center 2012 Configuration Manager のリモート コントロールのセキュリティとプライバシーの情報が含まれています。  

##  <a name="a-namebkmksecurityhardwareinventorya-security-best-practices-for-remote-control"></a><a name="BKMK_Security_HardwareInventory"></a> リモート コントロールのセキュリティのベスト プラクティス  
 ここでは、リモート コントロールを使用してクライアント コンピューターを管理するときのセキュリティのベスト プラクティスについて説明します。  

|セキュリティのベスト プラクティス|説明|  
|----------------------------|----------------------|  
|Kerberos 認証ではなく NTLM 認証が使用されていたら、リモート コンピューターに接続しない。|Kerberos 認証ではなく NTLM 認証が使用されて、リモート コントロール セッションが認証されていることを Configuration Manager が検出すると、リモート コンピューターの ID が検証できないという警告が表示されます。 そのリモート コントロール セッションを続けないでください。 NTLM 認証は Kerberos よりも弱い認証プロトコルで、再生攻撃やなりすましに対して脆弱です。|  
|リモート コントロール ビューアーでは、クリップボードの共有を無効にしてください。|クリップボードが実行可能ファイルやテキストなどのオブジェクトをサポートすると、接続を開始するコンピューターでプログラムを実行するリモート コントロール セッション中に、ホスト コンピューターのユーザーに使用される可能性があります。|  
|コンピューターをリモートで管理する場合は、特権アカウントのパスワードを入力しない。|キーボード入力を監視するソフトウェアによって、パスワードが捕捉される可能性があります。 また、クライアント コンピューターで実行されているプログラムが、リモート コントロール ユーザーを想定したプログラムではない場合は、そのプログラムによってパスワードがキャプチャされている可能性があります。 アカウントおよびパスワードが必要な場合は、エンド ユーザーが入力するようにしてください。|  
|リモート コントロール セッション中は、キーボードとマウスをロックする。|Configuration Manager がリモート コントロール接続の終了を検出すると、Configuration Manager は自動的にキーボードとマウスをロックし、ユーザーがオープンなリモート コントロール セッションを制御できなくなります。 ただ、直ちに検出されないことがあり、リモート コントロール サービスが終了した場合は、検出されません。<br /><br /> 操作を選択する **リモートのキーボードとマウス** で、 **ConfigMgr リモート コントロール** ウィンドウです。|  
|ソフトウェア センターのリモート コントロール設定をユーザーに構成させない。|クライアント設定 [ユーザーはソフトウェア センターでポリシー設定または通知設定を変更できる] を無効にして、ユーザーが盗み見られないようにします。 ****<br /><br /> この設定はコンピューターに対するもので、ログオン ユーザーに対するものではありません。|  
|[ドメイン] Windows ファイアウォールのプロファイルを有効にします。 ****|クライアント設定を有効にする **クライアントのファイアウォール例外プロファイルでリモート制御を有効にする** クリックして、 **ドメイン** イントラネット コンピューター用に Windows ファイアウォールです。|  
|リモート コントロール セッション中にログオフし、別のユーザーとしてログオンする場合は、リモート コントロール セッションの接続を切断する前に、ログオフしていることを確認してください。|このシナリオでログオフしないと、セッションがオープンのまま残ります。|  
|ユーザーにローカルの管理者権限を与えない。|ユーザーにローカルの管理者権限を与えると、リモート コントロール セッションが乗っ取られたり、資格情報が侵害される可能性があります。|  
|グループ ポリシーまたは Configuration Manager のいずれかを使用してリモート アシスタンス設定を構成し、両方は使用しない。|Configuration Manager およびグループ ポリシーを使用して、リモート アシスタンス設定に対する変更を構成することができます。 クライアントでグループ ポリシーが更新されると、既定では、サーバーで変更されたポリシーのみが変更され、プロセスが最適化されます。 Configuration Manager によりローカル セキュリティ ポリシーの設定が変更されますが、これは、グループ ポリシーの更新が適用されない限り、上書きされない可能性があります。<br /><br /> 両方の場所でポリシーを設定すると、矛盾が生じる可能性があります。 リモート アシスタンス設定を構成するには、いずれかの方法を選択してください。|  
|クライアント設定 [リモート コントロールのアクセス許可をユーザーに要求する] を有効にする。 ****|リモート コントロール セッションの確認をユーザーに要求するこのクライアント設定を回避する方法はありますが、この設定を有効にすると、ユーザーが機密情報の作業中に盗み見られるリスクが低減されます。<br /><br /> また、リモート コントロール セッション中に表示されるアカウント名を確認し、アカウントが認証されない可能性があれば接続を切断するように、ユーザーを教育します。|  
|アクセス許可のあるユーザーの一覧を制限する。|ローカルの管理者権限は、リモート コントロールを使用できるユーザーには不要です。|  

### <a name="security-issues-for-remote-control"></a>リモート コントロールのセキュリティの問題  
 リモート コントロールを使用するクライアント コンピューターの管理では、次のセキュリティの問題があります。  

-   リモート コントロールの監査メッセージを信頼性があるものとは考えない。  

     リモート コントロール セッションを開始してから、代替資格情報を使用してログオンした場合、監査メッセージを送信するのは元のアカウントで、代替資格情報を使用するアカウントではありません。  

     Configuration Manager コンソールのインストールではなく、リモート コントロールのバイナリ ファイルをコピーしてから、コマンド プロンプトでリモート コントロールを実行すると、監査メッセージは送信されません。  

##  <a name="a-namebkmkprivacyhardwareinventorya-privacy-information-for-remote-control"></a><a name="BKMK_Privacy_HardwareInventory"></a> リモート コントロールのプライバシー情報  
 リモート コントロールを使用すると、Configuration Manager クライアント コンピューターでアクティブなセッションを表示することや、場合によってはそれらのコンピューターに保存されたあらゆる情報を表示することが可能です。 既定では、リモート コントロールは無効になっています。  

 リモート コントロールは、リモート コントロール セッションの開始前に明確に通知してユーザーの同意を得るように構成することができますが、ユーザーに許可を得たり気付かれたりすることなくユーザーを監視するように構成することもできます。 "表示のみ" アクセス レベルを構成して、リモート コントロールやフル コントロールでは何も変更できないようにすることができます。 リモート コントロール セッションで接続中の管理者のアカウントが表示されるので、コンピューターに接続しているユーザーを識別することができます。  

 既定では、Configuration Manager は、ローカルの Administrators グループにリモート コントロール権限を付与します。  

 リモート コントロールを構成する前に、プライバシー要件について検討してください。  



<!--HONumber=Nov16_HO1-->

