---
title: "Windows Phone アプリケーションの作成 | Microsoft Docs"
description: "Windows Phone デバイス用アプリケーションを作成して展開するときに検討する必要がある考慮事項について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 866113ff-efd0-40d2-ac3a-2edd49732a24
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 557888d1f1f899e3198c430bbe5ccdd44178f824
ms.openlocfilehash: 5cd1ba42afd13e98565d24d1ec8a3ee209e8532c


---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>System Center Configuration Manager で Windows Phone アプリケーションを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

アプリケーションを作成するための System Center Configuration Manager の他の要件と手順に加えて、Windows Phone デバイス用アプリケーションを作成および展開するときには次の考慮事項について検討する必要があります。  

## <a name="general-considerations"></a>一般的な考慮事項  
 Configuration Manager では、次のアプリ ファイルの種類の展開がサポートされています。  

|デバイスの種類|サポートされているファイルの種類|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap、.appx、.appxbundle|  

 次の展開操作がサポートされています。  

|デバイスの種類|サポートされている操作|  
|-----------------|-----------------------|  
|Windows Phone 8 および Windows Phone 8.1|利用可能、必須、アンインストール|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>最新の Windows Phone 会社ポータル アプリケーションに置き換え関係を展開する手順  
 次の表に、Windows Phone 8 用の最新の会社ポータル アプリケーションを作成する手順とその簡単な説明、および関連情報のある場所へのリンクをまとめます。  

|手順|説明|  
|----------|----------------------|  
|**ステップ 1:** 最新の会社ポータル アプリケーションを取得する。|[Windows Phone 8 ポータル サイト アプリ](http://go.microsoft.com/fwlink/?LinkId=268440)をダウンロードします。|  
|**ステップ 2:** 会社ポータル アプリケーションに、Symantec 証明書を使って署名する。|ポータル サイト アプリに署名する方法については、「[System Center Configuration Manager と Microsoft Intune による Windows Phone および Windows 10 Mobile のハイブリッドのデバイス管理のセットアップ](../../mdm/deploy-use/enroll-hybrid-windows.md)」を参照してください。|  
|**ステップ 3:** 最新バージョンの会社ポータルアプリケーションを含む新しいアプリケーションを作成して置き換え関係を指定する。|詳細については、「[アプリケーションの作成](../../apps/deploy-use/create-applications.md)」と「[アプリケーションを修正して置き換える方法](../../apps/deploy-use/revise-and-supersede-applications.md)」を参照してください。|  
|**ステップ 4:** Microsoft Intune サブスクリプションの作成ウィザードでアプリケーションを追加する。|詳細については、「[System Center Configuration Manager と Microsoft Intune による Windows Phone および Windows 10 Mobile のハイブリッドのデバイス管理のセットアップ](../../mdm/deploy-use/enroll-hybrid-windows.md)」を参照してください。|  
|**ステップ 5:** Microsoft Intune サブスクリプションの作成ウィザードで会社ポータル アプリケーションを追加したときに自動的に作成された展開を削除する。|Microsoft Intune のサブスクリプションによって、このアプリケーションの展開が自動的に作成されますが、この展開には置き換えを設定できないので削除します。|  
|**手順 6:**アプリケーションの新しい展開を作成する。 **ソフトウェアの展開ウィザード**の [**展開設定**] ページで [**このアプリケーションの置き換えられるバージョンを自動的にアップグレードする**] チェック ボックスをオンにします。|置き換え関係を設定して作成したアプリケーションの新しい展開を作成します。|  
|**ステップ 7 (オプション):** 既定では、置き換えるアプリケーションがデバイスに 7 日後にインストールされる。 登録済みデバイスに、これより早く会社ポータル アプリケーションを展開したい場合は、[**展開の再評価スケジュールを指定する**] を小さな値に設定します。<br /><br /> この値を既定値より小さくすると、ネットワークとクライアント コンピューターのパフォーマンスが低下する可能性があります。|詳細情報はありません。|  



<!--HONumber=Dec16_HO3-->


