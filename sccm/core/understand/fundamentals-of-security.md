---
title: "セキュリティの基礎 | Microsoft Docs"
description: "System Center Configuration Manager のセキュリティ層について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: b4d12eaadaf0324515f6ae595a737f576bd5076c


---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>System Center Configuration Manager のセキュリティの基礎

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のセキュリティは、複数の階層で構成されています。 オペレーティング システムとネットワークの両方に、Windows セキュリティ機能によって最初の層が提供されます。この層には、次が含まれます。  

-   Configuration Manager コンポーネント間でファイルを転送するためのファイル共有  

-   ファイルとレジストリ キーを保護するためのアクセス制御リスト (ACL)  

-   通信を保護するための IPsec  

-   セキュリティ ポリシーを設定するためのグループ ポリシー  

-   Configuration Manager コンソールなどの配布されたアプリケーションの DCOM アクセス許可  

-   セキュリティ プリンシパルを保存するための Active Directory ドメイン サービス  

-   Configuration Manager セットアップ中に作成された一部のグループを含む、Windows アカウント セキュリティ  

さらにファイアウォールや侵入検知などのセキュリティ コンポーネントを使用することで、環境全体を徹底的に防御することができます。 業界標準の PKI 実装によって発行される証明書により、認証、署名および暗号化が提供されます。  

Windows Server とネットワーク インフラストラクチャによって提供されるセキュリティだけでなく、いくつかの方法で、Configuration Manager によって Configuration Manager コンソールとそのリソースへのアクセスが制御されます。 既定では、Configuration Manager コンソールがインストールされているコンピューター上でコンソールを実行するために必要なファイルおよびレジストリ キーへのアクセス権は、ローカル管理者のみにあります。  

次のセキュリティ階層は、Windows Management Instrumentation (WMI) によるアクセスに基づいています。これは **SMS プロバイダー**に特有のものです。 SMS プロバイダーは、サイト データベースの情報を照会するためのユーザー アクセスを付与する Configuration Manager コンポーネントです。 既定では、SMS プロバイダーへのアクセスは、ローカルの **SMS 管理** グループのメンバーに限定されています。 このグループには最初のうち、Configuration Manager をインストールしたユーザーのみが含まれています。 他のアカウントに Common Information Model (CIM) リポジトリおよび SMS プロバイダーへのアクセス許可を与えるには、SMS 管理グループに他のアカウントを追加します。  

最後のセキュリティ階層は、サイト データベース内のオブジェクトに対するアクセス許可に基づいています。 既定では、Configuration Manager をインストールする際に使用したローカル システム アカウントおよびユーザー アカウントは、サイト データベース内のすべてのオブジェクトを管理できます。 Configuration Manager コンソールで、**ロール ベース管理**を使用すると、追加の管理ユーザーに対してアクセス許可を付与したり、制限したりすることができます。  

このトピックの残りの部分では、Configuration Manager に関連するセキュリティの側面を説明します。  

## <a name="role-based-administration"></a>役割に基づいた管理  
 Configuration Manager は、ロール ベース管理を使用して、オブジェクト (コレクション、展開、サイトなど) を保護できます。 この管理モデルは、階層内のすべてのサイトのセキュリティのアクセス権の設定およびサイトの設定を一元的に定義および管理します。 セキュリティ ロールによって、管理ユーザーおよびグループに、各種の Configuration Manager オブジェクトへのアクセス許可 (クライアント設定を作成または変更するためのアクセス許可など) が割り当てられます。 セキュリティ スコープは、管理ユーザーが管理を担当する特定のオブジェクトのインスタンス (Microsoft Office をインストールするアプリケーションなど) をグループ化します。 セキュリティ ロール、セキュリティ スコープ、およびコレクションの組み合わせによって、管理ユーザーが表示および管理できるオブジェクトが定義されます。 Configuration Manager は、一般的な管理タスクのためにいくつかの既定のセキュリティ ロールをインストールします。 ただし、独自のセキュリティ ロールを作成して、特定のビジネスの要件をサポートすることができます。  

 詳細については、「[System Center Configuration Manager のロール ベース管理の構成](../../core/servers/deploy/configure/configure-role-based-administration.md)」をご覧ください。  

## <a name="securing-client-endpoints"></a>クライアント エンドポイントの保護  
 サイト システムの役割へのクライアント通信は、自己署名入り証明書または公開キー基盤 (PKI) 証明書を使用して保護されます。 Configuration Manager がインターネットで検出したコンピューター クライアントと、モバイル デバイス クライアントは、HTTPS を使用してクライアント エンドポイントを保護できるように、PKI 証明書を使用する必要があります。 クライアントが接続するサイト システムの役割は、HTTPS または HTTP を使用してクライアント通信を行うように構成できます。 クライアント コンピューターは、利用可能な最も安全な方法を常に使用して通信し、HTTP 通信を許可するサイト システムの役割がある場合にのみ、安全性が劣るイントラネットでの HTTP による通信方法を代替で使用します。  

 詳細については、「[System Center Configuration Manager の暗号化コントロールのテクニカル リファレンス](../../protect/deploy-use/cryptographic-controls-technical-reference.md)」を参照してください。  

## <a name="configuration-manager-accounts-and-groups"></a>Configuration Manager のアカウントとグループ  
 Configuration Manager では、ほとんどのサイト操作に**ローカル システム** アカウントを使用します。 ただし、いくつかの管理タスクでは、追加のアカウントを作成して管理する必要がある場合があります。 いくつかの既定のグループと SQL Server の役割がセットアップ時に作成されます。 必要に応じて、これらの既定のグループと役割にコンピューターまたはユーザー アカウントを手動で追加することもできます。  

 詳細については、「[System Center Configuration Manager で使用されるアカウント](../../core/plan-design/hierarchy/accounts.md)」を参照してください。  

## <a name="privacy"></a>プライバシー  
 多くのクライアントを効果的に管理できるため、エンタープライズ管理製品には多くの利点がありますが、このソフトウェアが組織のユーザーのプライバシーに影響を与える可能性について注意する必要があります。 System Center Configuration Manager にはデータを収集してデバイスを監視するための多くのツールが備わっています。これらのいくつかではプライバシーの問題が生じる可能性があります。  

 たとえば、構成マネージャー クライアントをインストールすると、既定で多数の管理設定が有効になります。 その結果、クライアント ソフトウェアから情報が Configuration Manager サイトに送信されます。 クライアント情報は Configuration Manager データベースに格納されます。Microsoft に送信されることはありません。 System Center Configuration Manager を実装する前に、プライバシー要件について検討してください。  



<!--HONumber=Dec16_HO3-->


