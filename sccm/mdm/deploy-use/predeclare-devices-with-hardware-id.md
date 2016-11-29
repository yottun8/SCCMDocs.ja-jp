---
title: "IMEI または iOS シリアル番号を持つデバイスの事前宣言"
description: "IMEI または iOS シリアル番号を持つ会社所有のデバイスの事前宣言"
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6cd640085e90b2945326e3fa942ae9bd7b8f7e24
ms.openlocfilehash: 2550fef062b5ef508e4c0492a5a9c63ffcb9084a

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>IMEI または iOS シリアル番号を持つデバイスの事前宣言

*適用対象: System Center Configuration Manager (Current Branch)*

会社が所有するデバイスの International station Mobile Equipment Identity (IMEI) 番号または iOS シリアル番号をインポートすることでデバイスを識別できるようになりました。 デバイスの IMEI 番号を含むコンマ区切り値 (.csv) ファイルをアップロードするか、デバイス情報を手動で入力することができます。  インポートされた情報によって登録するデバイスの**所有権**が、デバイスの一覧で "**企業**" として設定されます。 Intune ライセンスも、サービスにアクセスする各ユーザーに必要です。  

## <a name="predeclare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>IMEI または iOS シリアル番号を持つ会社所有のデバイスの事前宣言

1.  Configuration Manager コンソールで [資産とコンプライアンス]、[概要]、[会社が所有しているすべてのデバイス]、[事前に宣言されたデバイス] の順に移動し、[事前に宣言されたデバイスを追加します] をクリックします。 事前に宣言されたデバイス ウィザードが開きます。
2.  デバイス情報を追加する方法を指定します。
     -  IMEI 番号と詳細を含む .csv ファイルをアップロードします。
     -  IMEI 番号と詳細を手動で追加します。 情報を手動で入力するには、IMEI 番号または iOS シリアル番号とデバイスの詳細を入力します。

      アップロードされたファイルの場合、情報を含む .csv ファイルを参照し、会社所有のデバイスを事前に宣言します。 ファイルには、次の形式が必要です。ただし、一番上の行 (ガイダンスのためだけに提供) は除きます。 各行には、IMEI 番号または iOS シリアル番号を含める必要があります。 IOS デバイスのシリアル番号のみ事前に宣言できます。他のデバイス プラットフォームでは IMEI 番号を使用します。 この表には、サンプル データが含まれます。
      | IMEI #  | iOS シリアル #  | OS | 説明 |
      | :------------ |:---------------|:-----|:-----|
      | 123456789012345    |   | WINDOWS | 会社所有の Windows デバイス|
      |       | A1B2C3D4E5C6 |   iOS |  会社所有の iOS デバイス|
      | 223456789012345 | E6D5C4B3A210 |   iOS |    その他の iOS デバイス|
      | 323456789012345 |        |   iOS |  3 番目の iOS デバイス|
      | 123456789012346 |         |   Android |     会社所有の Android デバイス|

    .csv ファイルにヘッダー行を含めないでください。 上の例では、わかりやすくするためにのみヘッダーが含まれています。

    **列には、次の値をそのまま使用できます。**    
      - 列 1: スペースなしの IMEI 番号
      - 列 2: iOS シリアル番号
      - 列 3: デバイスのオペレーティング システム:
         - IOS: すべての iOS デバイス
         - WINDOWS: Windows Phone、Window 10 Mobile、および Windows PC など
         - ANDROID – すべての Android デバイス
      - 列 4: 詳細 (オプション): Configuration Manager コンソールに表示される追加のデバイス情報 1024 文字の制限。

    [次へ] をクリックします。 ****

3. ファイル インポートの結果を確認します。 デバイス番号が確実にインポートされている場合、Configuration Manager はそれらのデバイスと交換の**詳細**を表示します。 詳細を上書きするデバイスを選択します。 デバイスの詳細を変更するには、デバイスの ID またはシリアル番号を再インポートする必要があります。 [**次へ**] をクリックして続行するか、[**戻る**] をクリックして最新の詳細を保持して、ウィザードを完了します。

4. インポートに iOS シリアル番号が含まれている場合は、それらのデバイスを登録プロファイルに割り当てる必要があります。 使用可能なプロファイルの一覧から [**割り当てる登録プロファイル**] を選択し、[**次へ**] をクリックします。

5. [**次へ**] をクリックして、概要を表示し、ウィザードを完了します。



<!--HONumber=Nov16_HO1-->


