---
title: "iOS アプリケーションの作成 |System Center Configuration Manager"
description: "iOS デバイス用アプリケーションを作成して展開するときに検討する必要がある考慮事項について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5420109-6538-4430-9ca6-db352ee84c2e
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4c3845635846cae183e81d0ddb9c8222dabd8929


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>System Center Configuration Manager で iOS アプリケーションを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

アプリケーションを作成するための System Center Configuration Manager の他の要件と手順に加えて、iOS デバイス用アプリケーションを作成および展開するときには次の考慮事項について検討する必要があります。  

## <a name="general-considerations"></a>一般的な考慮事項  
 Configuration Manager では、次のアプリの種類の展開がサポートされています。  

|デバイスの種類|サポートされているファイル|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> System Center Configuration Manager では、iOS アプリをインポートするときに、プロパティ一覧 (.plist) ファイルを指定する必要はありません。|  

 次の展開操作がサポートされています。  

|デバイスの種類|サポートされている操作|  
|-----------------|-----------------------|  
|iOS|利用可能、必須 (ただし、ユーザーはインストールに同意する必要があります)、アンインストール|  

> [!IMPORTANT]  
>  現在、エンド ユーザーは iOS 向け Microsoft Intune 会社ポータル アプリから会社のアプリをインストールできません。 これは、iOS App Store に公開されたアプリに設けられた制限によるものです (「App Store レビューに関するガイドライン」の第 2 節をご覧ください)。 ユーザーが会社アプリ (管理されている App Store アプリ、基幹業務アプリ パッケージなど) をインストールするには、自身のデバイスで Intune Web ポータルを参照する必要があります (portal.manage.microsoft.com)。 Intune ポータル サイト アプリで有効化されるモバイル管理機能について詳しくは、「[Microsoft Intune の登録済みデバイス管理機能](https://technet.microsoft.com/library/dn600287.aspx)」をご覧ください。  



<!--HONumber=Nov16_HO1-->


