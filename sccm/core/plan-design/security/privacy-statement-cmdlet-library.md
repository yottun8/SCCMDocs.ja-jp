---
title: "System Center Configuration Manager のプライバシーに関する声明 - Configuration Manager Cmdlet Library | Microsoft Docs"
description: "System Center Configuration Manager コマンドレット ライブラリに関連するデータを Microsoft が収集して使用する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 767d0594eb871462df038997ea3b7e29615e05f7
ms.openlocfilehash: 10d8e8948d66a6b9b74e16a02cfbfc4ced66596c


---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>System Center Configuration Manager のプライバシーに関する声明 - Configuration Manager Cmdlet Library

*適用対象: System Center Configuration Manager (Current Branch)*

このプライバシーに関する声明は、System Center Configuration Manager Cmdlet Library の機能に適用されます。  

## <a name="usage-data"></a>使用状況データ  
 **この機能のデータ:**   
System Center Configuration Manager Cmdlet Library を利用すると、Windows PowerShell のコマンドレットおよびスクリプトを使用して Configuration Manager 階層を管理できます。 Cmdlet Library は、傾向および使用パターンを識別することを目的に、ライブラリに含まれるコマンドレットのお客様による使用方法に関する情報を収集します。  また、Cmdlet Library は、コマンドレットの使用時に発生したエラーの種類と数も収集します。  

 **収集、処理、または送信される情報:**   
収集される使用状況データには、コマンドレットの開始、停止、および終了、非推奨のコマンドレットの実行、コマンドレットに関する SMS プロバイダーの操作のアクティビティ  メトリックスが含まれます。 この情報は、個人を特定するものではありません。  収集されるエラー情報には、コマンドレットから返されるエラーのほか、例外エラーの詳細が含まれます。 エラーの詳細レポートには、お客様のコンピューターに接続されているデバイスのシリアル番号など、個人を特定できる情報が意図せず含まれる場合があります。 Cmdlet Library は、エラー レポートに含まれる情報のフィルター処理および匿名化を行い個人を特定できる情報を削除してから、当該レポートをマイクロソフトに送信します。  

 **情報の使用:**   
マイクロソフトは、これらの情報をマイクロソフトが提供する製品およびサービスの品質、セキュリティ、および整合性の改善のために使用します。  

 **選択または制御:**   
この使用状況データ機能は既定で有効になっています。 System Center Configuration Manager Cmdlet Library には、この機能を制御する 2 つのレジストリ キーが含まれます。  

 この機能を完全に停止するには、Windows イベント トレーシング (ETW) プロバイダーごとに 1 つずつある、次の 2 つのレジストリ キーの値を設定する必要があります。  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (ドライブ プロバイダーの使用状況データの停止)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (コマンドレットの使用状況データの停止)  

 使用状況データ設定を変更する際は、コンピューターに応じて固有の変更を行います。  

 使用状況データ (収集) の構成方法の詳細については、 [System Center Configuration Manager Cmdlet Library のドキュメント](https://technet.microsoft.com/en-us/library/dn958404.aspx)を参照してください。   



<!--HONumber=Dec16_HO3-->


