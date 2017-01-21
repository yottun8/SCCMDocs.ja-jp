---
title: "クライアントのアップグレード | Microsoft Docs"
description: "System Center Configuration Manager でクライアントをアップグレードする方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
caps.latest.revision: 8
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: c9794b9770e6fa5665af547d6b36559f85ade691


---
# <a name="upgrade-clients-in-system-center-configuration-manager"></a>System Center Configuration Manager でのクライアントのアップグレード

*適用対象: System Center Configuration Manager (Current Branch)*

社内の Windows コンピューター、UNIX/Linux サーバー、および Mac コンピューターで System Center Configuration Manager クライアント ソフトウェアをアップグレードするには、さまざまな方法があります。 次のセクションは、クライアントのアップグレード方法ごとの長所と短所を示したもので、どの方法が組織に適しているかを判断するのに役立ちます。  

> [!TIP]  
>  Configuration Manager の以前のバージョン \(Configuration Manager 2007 または System Center 2012 Configuration Manager など\) から、サーバー インフラストラクチャをアップグレードする場合は、Configuration Manager クライアントをアップグレードする前に、現在のすべてのブランチの更新プログラムのインストールを含む、サーバーのアップグレードを完了することをお勧めします。   現在のブランチの最新の更新プログラムには、クライアントの最新バージョンが含まれているため、使用するすべての Configuration Manager 更新プログラムをインストールした後に、クライアントのアップグレードを実行することをお勧めします。  

## <a name="group-policy-installation"></a>グループ ポリシーによるインストール  
 **サポートされるクライアント プラットフォーム:** Windows  

 **長所**  

-   クライアントをアップグレードする前に、コンピューターが検出されている必要はありません。  

-   新しいクライアントのインストールまたは更新で使用できます。  

-   コンピューターは、Active Directory ドメイン サービスに公表されたクライアント インストール プロパティを読み取ることができます。  

-   目的のクライアント コンピューターのインストール アカウントを構成してメンテナンスを行う必要はありません。  

 **短所**  

-   多数のクライアントをアップグレードした場合、ネットワーク トラフィックが増加する可能性があります。  

-   Active Directory スキーマが Configuration Manager 向けに拡張されていない場合、グループ ポリシー設定を使用してサイト内のコンピューターにクライアント インストール プロパティを追加する必要があります。  

 詳細については、「[グループ ポリシーを使用した Configuration Manager クライアントのインストール方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP)」を参照してください。  

## <a name="logon-script-installation"></a>ログオン スクリプトによるインストール  
 **サポートされるクライアント プラットフォーム:** Windows  

 **長所**  

-   クライアントをインストールする前に、コンピューターが検出されている必要はありません。  

-   新しいクライアントのインストールまたは更新で使用できます。  

-   CCMSetup のコマンド ライン プロパティを使用してサポートします。  

 **短所**  

-   多数のクライアントを短時間にアップグレードした場合、ネットワーク トラフィックが増加する可能性があります。  

-   ユーザーがネットワークに頻繁にログオンしない場合は、すべてのクライアント コンピューターでアップグレードするのに長時間かかる場合があります。  

 詳細については、「[ログオン スクリプトを使用した Configuration Manager クライアントのインストール方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript)」を参照してください。  

## <a name="manual-installation"></a>手動インストール  
 **サポートされるクライアント プラットフォーム:** Windows、UNIX/Linux、Mac OS X  

 **長所**  

-   クライアントをアップグレードする前に、コンピューターが検出されている必要はありません。  

-   テストの目的で役立ちます。  

-   CCMSetup のコマンド ライン プロパティを使用してサポートします。  

 **短所**  

-   自動化されていないため、時間を削減できます。  

 詳細については、以下のトピックを参照してください。  

-   [Configuration Manager クライアントの手動インストール方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [System Center Configuration Manager で Linux および UNIX サーバーのクライアントをアップグレードする方法](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

-   [System Center Configuration Manager で Mac コンピューター上のクライアントをアップグレードする方法](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>アップグレード インストール (アプリケーション管理)  
 **サポートされるクライアント プラットフォーム:** Windows  

> [!NOTE]  
>  この方法では、Configuration Manager 2007 クライアントをアップグレードすることはできません。 このシナリオでは、Configuration Manager 2007 サイトからのパッケージとして Configuration Manager クライアントを展開したり、自動クライアント アップグレードを使用して、最新バージョンのクライアントを含むパッケージを自動的に作成して展開したりできます。  

 **長所**  

-   CCMSetup のコマンド ライン プロパティを使用してサポートします。  

 **短所**  

-   大規模なコレクションに対してクライアントを配布する場合、ネットワーク トラフィックの量が増大する可能性があります。  

-   サイトで探索または割り当てられたコンピューター上のクライアント ソフトウェアをアップグレードするときのみ使用できます。  

 詳細については、「[パッケージとプログラムを使用した Configuration Manager クライアントのインストール方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp)」を参照してください。  

## <a name="automatic-client-upgrade"></a>自動クライアント アップグレード  

> [!NOTE]  
>  Configuration Manager 2007 クライアントを System Center Configuration Manager クライアントにアップグレードするために使用できます。 Configuration Manager 2007 クライアントは Configuration Manager サイトに割り当てることができますが、自動クライアント アップグレード以外の操作は実行できません。  

 **サポートされるクライアント プラットフォーム:** Windows  

 **長所**  

-   サイト内のクライアントを自動的に最新バージョンに保つのに使用できます。  

-   管理者による管理の手間はごくわずかしか必要ありません。  

 **短所**  

-   クライアント ソフトウェアのアップグレードにのみ使用できます。新しいクライアントのインストールには使用できません。  

-   同時に多くのクライアントをアップグレードするには適していません。  

-   サイトに関連付けられた階層内のすべてのクライアントに対して適用します。 コレクションでスコープを設定することはできません。  

-   スケジュール オプションは限定されています。  

 詳細については、「[System Center Configuration Manager で Windows コンピューター用クライアントをアップグレードする方法](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)」を参照してください。  

## <a name="client-testing"></a>クライアントのテスト  
 **サポートされるクライアント プラットフォーム:** Windows  

 **長所**  

-   小規模な実稼働前環境コレクションで新しいクライアント バージョンをテストするために使用できます。  

-   テストが完了すると、実稼働前環境のクライアントは実稼働環境に昇格され、Configuration Manager サイト全体で自動的にアップグレードされます。  

 **短所**  

-   クライアント ソフトウェアのアップグレードにのみ使用できます。新しいクライアントのインストールには使用できません。  

 [System Center Configuration Manager で実稼働前コレクションのクライアント アップグレードをテストする方法](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  



<!--HONumber=Dec16_HO3-->


