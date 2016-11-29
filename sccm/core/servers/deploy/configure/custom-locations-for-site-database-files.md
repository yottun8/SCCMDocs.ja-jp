---
title: "カスタム データベース ファイルの場所 | System Center Configuration Manager"
description: "SQL Server データベース ファイルのカスタムの場所を指定する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e8625d753fd2832009c9a3dc0b12b9a44f93c091

---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>System Center Configuration Manager のサイト データベース ファイルのカスタムの場所

*適用対象: System Center Configuration Manager (Current Branch)*

 System Center Configuration Manager は、SQL Server データベース ファイルのカスタムの場所をサポートしています。  

> [!NOTE]  
>  既定以外のファイルの場所を指定するオプションは、SQL Server クラスターを使用する場合は使用できません。  

 新しいプライマリ サイトまたは中央管理サイトの**セットアップ中** に、次のことができます。  

-   サイト データベースの既定以外のファイルの場所の指定: Configuration Manager のセットアップによって、これらの場所を使用してサイト データベースが作成されます。  

-   カスタムのファイルの場所を使用する、事前に作成した SQL Server データベースの使用の指定: Configuration Manager のセットアップでは、事前に作成したデータベースとその構成済みのファイルの場所を使用します。  

**セットアップ後に** 、サイト データベース ファイルの場所を変更できます。 これには、次のようにサイトを停止して、SQL Server でファイルの場所を編集する必要があります。  

-   Configuration Manager サイト サーバーで、**SMS_Executive** サービスを停止します。  

-   使用する SQL Server のバージョンのドキュメントを参照して、ユーザー データベースの移動方法に関する説明に従います。 たとえば、SQL Server 2014 を使用する場合は、TechNet の「 [ユーザー データベースの移動](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) 」をご覧ください。  

-   データベース ファイルの移動が完了したら、Configuration Manager サイト サーバーで SMS_Executive サービスを再起動します。  



<!--HONumber=Nov16_HO1-->


