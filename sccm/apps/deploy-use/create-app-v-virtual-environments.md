---
title: "App-V 仮想環境を作成する | System Center Configuration Manager"
description: "Microsoft Application Virtualization を使用して仮想環境を作成し、アプリが互いにデータを共有できるようにします。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 625ea93d855089f6dbbdcc8368032e61b8a1ba0b


---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>System Center Configuration Manager で App-V 仮想環境を作成する

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager で Microsoft Application Virtualization (App-V) 仮想環境を使用すると、展開した仮想アプリケーションで、クライアント Windows PC と同じファイル システムとレジストリを共有できます。 つまり、標準の仮想アプリケーションとは異なり、これらのアプリケーションは、相互にデータを共有できます。 アプリケーションがインストールされた場合、または、インストールされたアプリケーションをクライアントが次回評価するときに、クライアント PC に仮想環境が作成または変更されます。 複数のアプリケーションがファイル システムまたはレジストリ値を変更しようとしたときに、順序が先のアプリケーションが優先されるように、アプリケーションを並べることができます。  

> [!IMPORTANT]  
>  マルウェアなどに対するセキュリティ保護を実現するために、App-V 仮想環境には依存しないでください。  

 App-V 仮想環境を Configuration Manager に作成するには、次の手順を実行します。  

## <a name="create-an-app-v-virtual-environment"></a>App-V 仮想環境を作成する  

1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]** > **[アプリケーション管理]** > **[App-V 仮想環境]** の順にクリックします。  

3.  [ホーム **** ] タブの [作成 **** ] グループで、[仮想環境の作成 ****] をクリックします。  

4.  [仮想環境の作成 **** ] ダイアログ ボックスで、次の情報を指定します。  

    -   **名前** - 仮想環境の一意の名前を 128 文字以下で指定します。  

    -   **説明** - 必要に応じて、仮想環境の説明を指定します。  

5.  [追加 **** ] をクリックして、新しい展開の種類を仮想環境に追加します。 展開の種類を少なくとも 1 つ追加する必要があります。  

6.  [アプリケーションの追加 **** ] ダイアログ ボックスで、128 文字以下の [グループ名 **** ] を指定します。このグループは、仮想環境に追加するアプリケーションのグループを参照するときに使用します。  

7.  [追加 ****] をクリックし、グループに追加する App-V 5 アプリケーションと展開の種類を選択し、[OK ****] をクリックします。  

8.  [アプリケーションの追加 **** ] ダイアログ ボックスで、[順位を上げる **** ] または [順位を下げる **** ] をクリックして、同じ仮想環境内で複数のアプリケーションがファイル システムまたはレジストリ設定を変更しようとしたときに、優先するアプリケーションを指定します。  

9. [OK **** ] をクリックして [仮想環境の作成 **** ] ダイアログ ボックスに戻ります。  

10. グループの追加を完了したら、[OK **** ] をクリックして仮想環境を作成します。 新しい仮想環境が Configuration Manager コンソールの [**APP-V 仮想環境**] ノードに表示されます。 [App-V 仮想環境のステータス ****] レポートを使用して、仮想環境の状態を監視できます。  

    > [!NOTE]  
    >  アプリケーションがインストールされたとき、またはインストールされたアプリケーションをクライアントが次回評価するときに、クライアント PC に仮想環境が追加または変更されます。  



<!--HONumber=Nov16_HO1-->


