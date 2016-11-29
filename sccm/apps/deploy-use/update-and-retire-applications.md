---
title: "アプリケーションの更新とインベントリからの削除 | System Center Configuration Manager"
description: "System Center Configuration Manager を使用して、展開済みのアプリケーションを、改訂、置き換え、またはアンインストールします。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
caps.latest.revision: 9
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5eafaca3317f22b0e0b434d9161785cc90c701b7


---
# <a name="update-and-retire-applications-with-system-center-configuration-manager"></a>System Center Configuration Manager でのアプリケーションの更新とインベントリからの削除

*適用対象: System Center Configuration Manager (Current Branch)*


いつかは、アプリケーションに変更を加えたり、アンインストールしたり、既に展開されているアプリケーションを新しいアプリケーションに置き換えたりすることが必要になる可能性があります。 System Center Configuration Manager には、それを実現するための次のような機能が含まれています。  
  
-   **アプリケーションの改訂** - アプリケーションや展開の種類を変更するときに、Configuration Manager はこれらの変更の履歴を保持します。 いつでも以前のリビジョンにアプリケーションを戻すことができます。 プロパティの表示、旧リビジョンのアプリケーションの復元、または旧リビジョンの削除を行うこともできます。  

     詳細については、「[アプリケーションのリビジョン](/sccm/apps/deploy-use/revise-and-supersede-applications#application-revisions)」を参照してください。  

-   **Supersede applications** - 置き換えの関係を使用して、既存のアプリケーションをアップグレードするか置き換えることができます。 アプリケーションを置き換える際、新しい展開の種類を指定して置換対象のアプリケーションの展開の種類を置き換えたり、置き換わるアプリケーションをインストールする前に、置換対象のアプリケーションをアップグレードするのか置換対象のアプリケーションをアンインストールするのか構成することもできます。  

     詳細については、「[アプリケーションの置き換え](/sccm/apps/deploy-use/revise-and-supersede-applications#application-supersedence)」を参照してください。  

-   **アプリケーションのアンインストール** - Configuration Manager では簡単にアプリケーションをアンインストールできます。 これは、エンドユーザーが操作を一切行うことなく、自動実行できます。  
  
詳細については、「[アプリケーションのアンインストール](../../apps/deploy-use/uninstall-applications.md)」を参照してください。  
   



<!--HONumber=Nov16_HO1-->


