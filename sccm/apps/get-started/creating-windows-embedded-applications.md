---
title: "Windows Embedded アプリケーションの作成 |System Center Configuration Manager"
description: "Windows Embedded デバイス用アプリケーションを作成して展開するときに検討する必要がある考慮事項について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
caps.latest.revision: 7
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b329978126a205a1e790b58465f011c51d4fd171


---
# <a name="create-windows-embedded-applications-with-system-center-configuration-manager"></a>System Center Configuration Manager で Windows Embedded アプリケーションを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

アプリケーションを作成するための System Center Configuration Manager の他の要件と手順に加えて、Windows Embedded デバイス用アプリケーションを作成および展開するときには次の考慮事項について検討する必要があります。  

## <a name="general-considerations"></a>一般的な考慮事項  

-   書き込みフィルターが有効にされた Windows Embedded デバイスにアプリケーションを展開するときに、展開中にデバイスで書き込みフィルターを無効にし、展開後にデバイスを再起動するかどうかを指定できます。 書き込みフィルターを無効にしないと、ソフトウェアが一時オーバーレイに展開され、デバイスへの変更を永続的なものにする別の展開が行われない限り、デバイスの再起動時にソフトウェアがインストールされることはありません。  

-   アプリケーションを Windows Embedded デバイスに展開する場合、デバイスが、メンテナンス期間が構成されたコレクションのメンバーであることを確認します。 これにより、書き込みフィルターを無効または有効にするタイミングと、デバイスを再起動するタイミングを管理できます。  

-   書き込みフィルターの動作を制御するユーザー エクスペリエンス設定は、[ **メンテナンスの期限または期間中の変更を確定する (再起動が必要)**] という名前のチェック ボックスです。  

## <a name="tips-for-deploying-applications"></a>アプリケーションを展開するためのヒント  

### <a name="use-required-applications-rather-than-available-applications-for-windows-embedded-devices-that-have-write-filters-enabled"></a>書き込みフィルターを有効にした Windows Embedded デバイスで使用できるアプリケーションではなく、必須のアプリケーションを使用する  
 ユーザーは、書き込みフィルターを有効にした Windows Embedded デバイスのソフトウェア センターからはアプリケーションをインストールできないため、これらのデバイスで使用できるアプリケーションではなく、必須のアプリケーションの展開の目的で常にアプリケーションを展開します。 通常、これは問題になりません。Windows Embedded オペレーティング システムを実行するコンピューターは、複数のユーザーに対して、1 つのアプリケーションを同じ方法で実行する必要がある場合が多いためです。 そのため、このようなデバイスは IT 部門によって高度に管理され、ロックされています。 必須のアプリケーションは、次のシナリオに最適です。 ただし、書き込みフィルターを有効にするときに、ユーザーが組み込みデバイスで複数のアプリケーションを実行する場合、ユーザーには次の制限について説明してください。  

-   ユーザーは、ソフトウェア センターから必要なソフトウェアをインストールできない。  

-   ユーザーは、ソフトウェア センターの [オプション] タブで営業時間を変更できない。  

-   ユーザーは、必須のアプリケーションのインストールを延期できない。  

 さらに、Configuration Manager がソフトウェアのインストールおよび更新の変更内容をコミットしている場合、低い権限のユーザーはメンテナンス期間中にログオンできません。 この期間、サービスは稼働しているため、デバイスが使用できないことを示すメッセージがユーザーに表示されます。  

### <a name="do-not-deploy-applications-to-windows-embedded-devices-that-have-write-filters-enabled-if-the-applications-require-the-user-to-accept-the-license-terms"></a>アプリケーションのライセンス条項に同意することをユーザーに求める場合、書き込みフィルターを有効にした Windows Embedded デバイスにはアプリケーションを展開しない  
 Configuration Manager が組み込みデバイスにソフトウェアをインストールできるように書き込みフィルターを無効にすると、低い権限のユーザーはデバイスにログオンできなくなります。 インストールするにはユーザーがライセンス条項に同意する必要がある場合、この操作が不可能になり、インストールは失敗します。 インストールにユーザー操作が必要な場合は、Windows Embedded デバイスにソフトウェアを展開しないでください。 [適用可能なプラットフォーム] リストを使用すると、このようなオペレーティング システムを除外できます。  



<!--HONumber=Nov16_HO1-->


