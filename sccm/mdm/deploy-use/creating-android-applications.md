---
title: Android アプリケーションを作成する
titleSuffix: Configuration Manager
description: Configuration Manager で Android デバイス用アプリケーションを作成して展開する方法。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a95a7735cc7f7afb6a16b030de6925926335e403
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385220"
---
# <a name="create-android-applications-in-configuration-manager"></a>Configuration Manager で Android アプリケーションを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager アプリケーションには、1 つ以上の展開の種類があります。 展開の種類は、インストール ファイルとデバイスにソフトウェアを展開するために必要な情報で構成されています。 また、展開の種類には、ソフトウェアを展開するタイミングと方法を指定する規則があります。  

Configuration Manager アプリケーションと展開の種類を作成する手順については、[アプリケーションの作成](/sccm/apps/deploy-use/create-applications#bkmk_create)に関するページを参照してください。 

Android デバイス用アプリケーションを作成して展開するときに、以下の考慮事項について留意してください。  



## <a name="general-considerations-for-android-apps"></a>Android アプリに関する一般的な考慮事項

Configuration Manager では、Android の .apk パッケージの展開がサポートされています。 

次の展開操作がサポートされています。

|デバイスの種類|サポートされている操作|
|-|-|
|Android|**利用可能**、**必須**: インストールとアンインストールの両方に、ユーザーが同意する必要があります。|
|Android for Work |**利用可能**、**必須** |



## <a name="approve-and-deploy-android-for-work-apps"></a>Android for Work アプリの承認と展開

Configuration Manager の管理者として、[Play for Work Web サイト](https://play.google.com/work) でアプリを承認することもできます。 その後、管理対象の Android for Work デバイスにそれらのアプリを展開します。

Play for Work ストアのアプリを承認し、Configuration Manager コンソールと同期し、管理対象の Android for Work デバイスに展開するには、次の手順を実行します。 アプリをユーザーの仕事用プロファイルに展開するには、Play for Work でアプリを承認する必要があります。 その後、アプリを Configuration Manager コンソールと同期します。

1. ブラウザーを開き、 https://play.google.com/work に移動します。  

2. Microsoft Intune テナントにバインドした Google 管理者アカウントを使用してサインインします。  

3. ご利用の環境に展開するアプリを参照します。 各アプリについて **[承認]** を選択し、Android for Work でアプリを使用できるようにします。  

4. Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[Cloud Services]** を展開して **[Android for Work]** ノードを選択します。  

5. リボンの **[同期]** をクリックします。  

6. アプリが同期するまで、最大 10 分待機します。次に、**[ソフトウェア ライブラリ]** ワークスペースに移動し、**[アプリケーション管理]** を展開して **[ストア アプリのライセンス情報]** ノードを選択します。  

7. Play for Work から同期したアプリを選択し、**[アプリケーションの作成]** をクリックします。  

8. ウィザードを完了します。  

9. **[ソフトウェア ライブラリ]** ワークスペースに移動し、**[アプリケーション管理]** を展開して **[アプリケーション]** ノードを選択します。 Android for Work アプリを選択して、通常どおりに展開します。  

Play for Work アプリを Configuration Manager と同期するには、最初に Play for Work Web サイトで少なくとも 1 つのアプリを承認します。

**利用可能**として展開されたアプリは、ポータル サイトではなく、仕事用バッジの付いた Google Play アプリに表示されます。 これにより、信頼できるソースからアプリを展開できます。 作業用バッジの付いた Google Play アプリは信頼できるソースです。 信頼できないソースからのアプリを許可する必要はありません。
