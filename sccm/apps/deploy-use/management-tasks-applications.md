---
title: "System Center Configuration Manager アプリケーションの管理タスク | System Center Configuration Manager"
description: "System Center Configuration Manager アプリケーションおよび展開の種類を管理します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b8ecf5334304f0aaae62b3fa5d6f84da84d97799


---
# <a name="management-tasks-for-system-center-configuration-manager-applications"></a>System Center Configuration Manager アプリケーションの管理タスク

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、System Center Configuration Manager アプリケーションと展開の種類を管理する方法を説明します。  
  
アプリケーションと展開の種類の作成については、「[Create applications with System Center Configuration Manager](../../apps/deploy-use/create-applications.md)」 (System Center Configuration Manager でアプリケーションを作成する) を参照してください。  
  
> [!IMPORTANT]  
>  アプリケーションの種類または展開の種類によっては、使用できない管理オプションがあります。  

##  <a name="manage-applications"></a>アプリケーションを管理する  
 **[ソフトウェア ライブラリ]** ワークスペースで、**[アプリケーション管理]** > **[アプリケーション]** の順に展開し、管理するパッケージを選んで、管理タスクを選びます。  
  
|タスク|説明|  
|----------|-------------|  
|**アクセス アカウントの管理**|[アクセス アカウントの管理 **** ] ダイアログ ボックスを開くと、選択したアプリケーションに関連付けられたコンテンツへのアクセス許可のレベルを指定できます。|  
|**事前設定コンテンツ ファイルの作成**|事前設定コンテンツ ファイルの作成ウィザードを開始します。このウィザードは、コンテンツのリモート配布ポイントへの配布を管理するのに役立ちます。 **** スケジュールおよび調整によってリモート配布ポイントの問題が有効に解決できない場合は、配布ポイントにコンテンツを事前設定することができます。<br /><br /> 「[コンテンツとコンテンツ インフラストラクチャの管理](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。|  
|**リビジョン履歴**|[アプリケーションのリビジョン履歴 **** ] ダイアログ ボックスが開きます。このダイアログ ボックスでは、このアプリケーションに加えられたリビジョンのプロパティを確認したり、古いアプリケーション リビジョンを削除したり、このアプリケーションの旧バージョンを復元したりすることができます。<br /><br /> 「[アプリケーションを修正して置き換える方法](../../apps/deploy-use/revise-and-supersede-applications.md)」を参照してください。|  
|**展開の種類の作成**|選択されたアプリケーションに新しい展開の種類を追加できるようにするには、 **展開の種類の作成ウィザード** を開きます。<br /><br /> 「[Create applications with System Center Configuration Manager](../../apps/deploy-use/create-applications.md)」 (System Center Configuration Manager でアプリケーションを作成する) を参照してください。|  
|**統計情報の更新**|[監視 **** ] ワークスペースの、[展開 **** ] ノードに表示されるこのアプリケーションの展開に関する情報を更新します。<br /><br /> 「[System Center Configuration Manager コンソールからのアプリケーションの監視](../../apps/deploy-use/monitor-applications-from-the-console.md)」を参照してください。|  
|**復帰**|このオプションは [インベントリから削除する **** ] 管理タスクを使ってインベントリから削除されたアプリケーションを復帰させるのに使用します。|  
|****|アプリケーションをインベントリから削除すると、展開に使用することはできなくなりますが、このアプリケーション自体やその展開は削除されません。 クライアント コンピューターにインストールされたアプリケーションの既存のコピーが削除されることはありません。 アプリケーションのすべてのリビジョンは 60 日後に Configuration Manager から削除されます。 ただし、インストール済みのアプリケーションのコピーは削除されません。<br /><br /> アプリケーションを削除するには、まずインベントリから削除し、次にその展開を削除し、さらにその他の展開による参照を削除してから、すべてのリビジョンを削除します。<br /><br /> 「[アプリケーションを修正して置き換える方法](../../apps/deploy-use/revise-and-supersede-applications.md)」を参照してください。|  
|**エクスポート**|アプリケーションのエクスポート ウィザード **** が開きます。このウィザードは選択したアプリケーションを .zip ファイルにエクスポートするので、これをアーカイブしたり、別のサイトにインストールできます。 アプリケーションのコンテンツをエクスポートする場合は、そのコンテンツを含むフォルダーが作成されます。<br /><br /> さらに、アプリケーションの依存関係や、置き換え関係、そのアプリケーションと依存関係の条件やコンテンツもエクスポートできます。<br /><br /> Windows PowerShell コマンドレットの **Export-CMApplication**は、同じ機能を実行します。 詳しくは、Microsoft System Center 2012 Configuration Manager SP1 コマンドレット リファレンス ドキュメントの [ http://go.microsoft.com/fwlink/p/?LinkID=258880](http://go.microsoft.com/fwlink/p/?LinkID=258880) を参照してください。|  
|**削除**|現在選択しているアプリケーションを削除します。<br /><br /> ほかのアプリケーションが依存している場合、アクティブな展開がある場合、または依存タスク シーケンスがある場合は、そのアプリケーションを削除できません。|  
|**展開のシミュレート**|アプリケーション展開のシミュレーション ウィザードを開きます。このウィザードを使うと、アプリケーションをインストールしたり、アンインストールせずに、コンピューターへのアプリケーションの展開結果をテストできます。 ****<br /><br /> 「[Simulate application deployments with System Center Configuration Manager](../../apps/deploy-use/simulate-application-deployments.md)」 (System Center Configuration Manager でアプリケーションの展開をシミュレーションする) を参照してください。|  
|**デプロイ**|ソフトウェアの展開ウィザードを開きます。このウィザードを使うと、階層内のコンピューターのグループに対して選択したアプリケーションを展開できます。 ****<br /><br /> 「[Deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md)」 (System Center Configuration Manager でアプリケーションを展開する) を参照してください。|  
|**コンテンツの配布**|コンテンツの配布ウィザードを開きます。このウィザードを使うと、階層内の配布ポイントに選択したアプリケーションのコンテンツをコピーできます。 ****<br /><br /> 「[コンテンツとコンテンツ インフラストラクチャの管理](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。|  
|**関係の表示**|選択したアプリケーションと他のアプリケーションとの関係が図示されます。 次のいずれかを選択します。<br><br> - **依存関係** – 選択したアプリケーションが依存しているアプリケーションや、そのアプリケーションに依存しているアプリケーションを表示します。<br>-                    **置き換え** – 置き換えられるアプリケーションや、選択したアイテムを置き換えるアプリケーションを表示します。<br>- **グローバル条件** – このアプリケーションが参照するグローバル条件を表示します。<br /><br /> 「[How to revise and supersede applications in System Center Configuration Manager](../../apps/deploy-use/revise-and-supersede-applications.md)」 (System Center Configuration Manager でアプリケーションを修正して置き換える方法) および「[How to create global conditions in System Center Configuration Manager](../../apps/deploy-use/create-global-conditions.md)」 (System Center Configuration Manager でグローバル条件を作成する方法) を参照してください。|  
  
##  <a name="manage-deployment-types"></a>展開の種類を管理する  
 [ソフトウェア ライブラリ **** ] ワークスペースで、[アプリケーションの管理 ****] を展開し、[アプリケーション ****] を選択して、管理したい展開の種類を含むアプリケーションを選びます。詳細ウィンドウで [展開の種類 **** ] タブをクリックし、管理する展開の種類を選択してから、管理タスクを選択します。  
  
|タスク|説明|  
|----------|-------------|  
|**優先順位を上げる**|選択した展開の種類の優先順位を上げます。 展開の種類は順番に評価されます。 展開の種類が特定の要件を満たしている場合はそれが実行され、優先順位一覧に表示されたほかの展開の種類は評価されません。|  
|**優先順位を下げる**|選択した展開の種類の優先順位を下げます。|  
|**削除**|選択した展開の種類を削除します。<br><br>別のアプリケーションの展開の種類によって参照されている展開の種類は、削除できません。<br>展開の種類を削除するには、まずほかの展開の種類に含まれる展開の種類の依存関係を削除する必要があります。<br>さらに、削除する展開の種類を参照する展開の種類を含むアプリケーションの、以前のリビジョンも削除する必要があります。|  
|**コンテンツの更新**|選択した展開の種類のコンテンツを更新します。<br /><br /> 仮想アプリケーションを含む展開の種類に対してウィザードを使用する場合、コンテンツの更新ウィザード **** が開始されます。 このウィザードを使うと、選択した仮想アプリケーションの公開オプションと要件の規則を変更できます。 詳細については、「[Create applications](../../apps/deploy-use/create-applications.md)」 (アプリケーションを作成する) を参照してください。<br /><br /> 展開の種類のコンテンツを更新すると、アプリケーションの新しいリビジョンが作成されます。 これにより、新しいアプリケーションと共にクライアント デバイスが更新される場合があります。|  
  




<!--HONumber=Nov16_HO1-->


