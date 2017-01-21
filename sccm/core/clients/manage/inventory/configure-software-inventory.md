---
title: "ソフトウェア インベントリの構成 | Microsoft Docs"
description: "System Center Configuration Manager のソフトウェア インベントリとインベントリ除外フォルダーを設定します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: cc226259-0e28-410a-94d3-223bdc948818
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 7ba943bee7faf417099cde0388649e4907525738


---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager でソフトウェア インベントリを構成する方法

*適用対象: System Center Configuration Manager (Current Branch)*

**Skpswi.dat** という名前の非表示ファイルを作成し、そのファイルをクライアントのハード ドライブのルートに配置することで、そのハード ドライブを System Center Configuration Manager ソフトウェア インベントリから除外できます。 このファイルは、ソフトウェア インベントリから除外するフォルダー構造のルートに配置することもできます。 この手順は、単一のワークステーションまたはサーバー クライアント (たとえば、大規模なファイル サーバー) 上でソフトウェア インベントリを無効にするときに使用できます。  

> [!NOTE]  
>  このファイルがクライアント コンピューターのドライブから削除されない限り、ソフトウェア インベントリによってクライアントのドライブが以後インベントリされることはありません。  

### <a name="to-exclude-folders-from-software-inventory"></a>ソフトウェア インベントリからフォルダーを除外するには  

1.  Notepad.exe を使用して、 **Skpswi.dat**という名前の空のファイルを作成します。  

2.  **Skpswi.dat** ファイルを右クリックして、 **[プロパティ]**をクリックします。 SkpSwi.dat ファイルのプロパティで、[非表示] 属性を選択します。 ****  

3.  ソフトウェア インベントリから除外する各クライアントのハード ドライブまたはフォルダーのルートに Skpswi.dat ファイルを配置します。 ****  



<!--HONumber=Dec16_HO3-->


