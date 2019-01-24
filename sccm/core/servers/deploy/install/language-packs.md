---
title: 言語パック
titleSuffix: Configuration Manager
description: Configuration Manager で使用できる言語サポートについて説明します。
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f6b10706638a476242051757145f725b262a7fc
ms.sourcegitcommit: 2687489aa409a050dcacd67f17b3dad3ab7f1804
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2019
ms.locfileid: "54316441"
---
# <a name="language-packs-in-configuration-manager"></a>Configuration Manager の言語パック

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、Configuration Manager の言語サポートに関する技術的な詳細情報について説明します。 Configuration Manager のサイト サーバーとクライアントは、言語に依存しないと見なされます。 中央管理サイトおよびプライマリ サイトに **サーバー言語パック** または **クライアント言語パック** をインストールすることで、表示言語のサポートを追加できます。 サイトのインストール中、そのサイトでサポートするサーバーとクライアントの言語を利用可能な言語パック ファイルから選びます。
 
各サイトに複数の言語をインストールします。 使用する言語のみをインストールする必要があります。  

- 各サイトで、Configuration Manager コンソール用に複数の言語がサポートされます。  

- 各サイトで個々のクライアント言語パックをインストールすることで、サポートが必要なクライアント言語のサポートのみを追加します。  

次のコンポーネントに一致する言語のサポートをインストールする場合について:  

- コンピューターの表示言語:Configuration Manager コンソールおよびそのコンピューターで実行されるクライアント ユーザー インターフェイスの両方において、その言語で情報が表示されます。  

- コンピューターの Web ブラウザーで使用している言語設定:アプリケーション カタログや SQL Server Reporting Services などの Web ベースの情報への接続時に、その言語で情報が表示されます。  


Configuration Manager のセットアップを実行すると、前提条件および再配布可能なファイルの一部として、言語パック ファイルがダウンロードされます。 [セットアップ ダウンローダー](setup-downloader.md)を使用して、セットアップを実行する前にこれらのファイルをダウンロードすることもできます。   



## <a name="server-languages"></a>サーバーの言語  

次の表を使用して、サーバーでサポートする言語にロケール ID をマッピングしてください。 ロケール ID の詳細については、「[Locale IDs Assigned by Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609)」 (Microsoft による割り当て済みロケール ID) を参照してください。  

|サーバーの言語|ロケール ID (LCID)|3 文字コード|  
|---------------------|------------------------|-----------------------|  
|英語 (既定)|0409|ENU|  
|中国語 (簡体字)|0804|CHS|  
|中国語 (繁体字、台湾)|0404|CHT|  
|チェコ語|0405|CSY|  
|オランダ語 - オランダ|0413|NLD|  
|フランス語|040c|FRA|  
|ドイツ語|0407|DEU|  
|ハンガリー語|040e|HUN|  
|イタリア語 - イタリア|0410|ITA|  
|日本語|0411|JPN|  
|韓国語|0412|KOR|  
|ポーランド語|0415|PLK|  
|ポルトガル語 - ブラジル|0416|PTB|  
|ポルトガル語 - ポルトガル|0816|PTG|  
|ロシア語|0419|RUS|  
|スペイン語 - スペイン|0c0a|ESN|  
|スウェーデン語|041d|SVE|  
|トルコ語|041f|TRK|  



## <a name="client-languages"></a>クライアントの言語  

次の表を使用して、クライアント コンピューターでサポートする言語にロケール ID をマッピングしてください。 ロケール ID の詳細については、「[Locale IDs Assigned by Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609)」 (Microsoft による割り当て済みロケール ID) を参照してください。  

|クライアントの言語|ロケール ID (LCID)|3 文字コード|  
|---------------------|------------------------|-----------------------|  
|英語 (既定)|0409|ENG|  
|中国語 - 簡体字|0804|CHS|  
|中国語 (繁体字、台湾)|0404|CHT|  
|チェコ語|0405|CSY|  
|デンマーク語|0406|DAN|  
|オランダ語 - オランダ|0413|NLD|  
|フィンランド語|040b|FIN|  
|フランス語|040c|FRA|  
|ドイツ語|0407|DEU|  
|ギリシャ語|0408|ELL|  
|ハンガリー語|040e|HUN|  
|イタリア語 - イタリア|0410|ITA|  
|日本語|0411|JPN|  
|韓国語|0412|KOR|  
|ノルウェー語|0414|NOR|  
|ポーランド語|0415|PLK|  
|ポルトガル語 (ブラジル)|0416|PTB|  
|ポルトガル語 (ポルトガル)|0816|PTG|  
|ロシア語|0419|RUS|  
|スペイン語 - スペイン|0c0a|ESN|  
|スウェーデン語|041d|SVE|  
|トルコ語|041f|TRK|  


### <a name="mobile-device-client-languages"></a>モバイル デバイス クライアントの言語  
モバイル デバイスの言語のサポートを追加する場合、サポートされるすべてのモバイル デバイス クライアントの言語が含まれます。 モバイル デバイスをサポートするために個々の言語パックを選択することはできません。  



## <a name="identify-installed-language-packs"></a>インストール済みの言語パックを特定する  
Configuration Manager クライアントを実行するコンピューターにインストールされている言語パックを特定するには、コンピューターのレジストリで、インストール済み言語パックのロケール ID (LCID) を確認します。 この情報は、次のレジストリ パスで確認できます。  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

ハードウェア インベントリをカスタマイズして、この情報を収集します。 次に、カスタム レポートを構築して言語の詳細を表示します。 カスタム ハードウェア インベントリの収集について詳しくは、「[ハードウェア インベントリを構成する方法](/sccm/core/clients/manage/inventory/configure-hardware-inventory)」をご覧ください。 レポートの作成について詳しくは、「[Configuration Manager レポートの管理](/sccm/core/servers/manage/operations-and-maintenance-for-reporting#BKMK_ManageReports)」をご覧ください。  
