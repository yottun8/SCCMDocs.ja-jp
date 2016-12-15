---
title: "iOS アプリケーションの作成 | Microsoft Docs"
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
ms.sourcegitcommit: e9e34359f4412ba07b9fb49f871a1eb2d36cecf8
ms.openlocfilehash: eb2d1245932d71bd10fd63d95a155eae7d128836


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>System Center Configuration Manager で iOS アプリケーションを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

iOS デバイス用アプリケーションを作成して展開するときに、以下の考慮事項について留意してください。  

## <a name="general-considerations"></a>一般的な考慮事項  
 Configuration Manager では、次のアプリの種類の展開がサポートされています。  

|デバイスの種類|サポートされているファイル|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> System Center Configuration Manager では、iOS アプリをインポートするときに、プロパティ一覧 (.plist) ファイルを指定する必要はありません。|  

 次の展開操作がサポートされています。  

|デバイスの種類|サポートされている操作|  
|-----------------|-----------------------|  
|iOS|**利用可能**、**必須**。 インストールとアンインストールの両方に、ユーザーが同意する必要があります。

> [!IMPORTANT]  
>  現在、エンド ユーザーは iOS 向け Microsoft Intune 会社ポータル アプリから会社のアプリをインストールできません。 これは、iOS App Store に公開されたアプリに設けられた制限によるものです (「App Store レビューに関するガイドライン」の第 2 節をご覧ください)。 ユーザーが会社アプリ (管理されている App Store アプリ、基幹業務アプリ パッケージなど) をインストールするには、自身のデバイスで Intune Web ポータルを参照する必要があります (portal.manage.microsoft.com)。 Intune ポータル サイト アプリで有効化されるモバイル管理機能について詳しくは、「[Microsoft Intune の登録済みデバイス管理機能](https://technet.microsoft.com/library/dn600287.aspx)」をご覧ください。  



<!--HONumber=Dec16_HO1-->


