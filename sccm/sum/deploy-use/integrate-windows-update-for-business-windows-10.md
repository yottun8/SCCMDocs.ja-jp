---

title: "Windows 10 における Windows Update for Business との統合 | Configuration Manager"
description: "Windows Update サービスに接続しているデバイスに関して、Windows Update for Business を利用し、組織の Windows 10 デバイスを最新の状態に維持します。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c4c6e50d0e1a34653226369cffdc0bde905398fc


---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Windows 10 における Windows Update for Business との統合

*適用対象: System Center Configuration Manager (Current Branch)*

Windows Update for Business (WUfB) を使用すると、組織内の Windows 10 ベースのデバイスが Windows Update (WU) サービスに直接接続しているときに、最新のセキュリティ防御と Windows の機能によってこれらのデバイスが常に最新に保たれるようにすることができます。 Configuration Manager には、WUfB を使用してソフトウェア更新プログラムを取得する Windows 10 コンピューターと、WSUS を使用して取得する Windows 10 コンピューターを区別する機能があります。  

 WUfB または Windows Insider などの WU から更新プログラムを受信するように Configuration Manager クライアントが設定されている場合に、以下に示す Configuration Manager の一部の機能が使用できなくなりました。  

-   Windows Update の適用状況レポート:  

    -   Configuration Manager では WU に発行された更新プログラムは認識されません。 WU から更新プログラムを受信するように構成された Configuration Manager クライアントでは、これらの更新プログラムは Configuration Manager コンソールで **[不明]** と表示されます。  

    -   全体的な適用ステータスのトラブルシューティングが困難になっています。これは、以前は **[不明]** ステータスが WSUS からのスキャン状態を報告していないクライアントに対してのみ使用されていたためです。  今後はこれに、WU から更新プログラムを受信する Configuration Manager クライアントも含まれることになります。  

    -   更新プログラムの適用ステータスに基づいた (会社のリソースに対する) 条件付きアクセスは、WU から更新プログラムを受信するクライアントに対して適切に機能しません。これは、これらのクライアントが Configuration Manager からの適用状況要件を満たすことがないためです。  

    -   定義の更新の適用状況は全体的な更新プログラムの適用状況レポートの一部であるため、これも期待される役目を果たしません。  定義の更新の適用状況は条件付きアクセス評価の一部でもあります。  

-   更新プログラムの適応ステータスに基づく Defender の全体的な Endpoint Protection のレポートでは、スキャン データの不足により正確な結果が返されません。  

-   Configuration Manager は、Office、IE、および Visual Studio などの Microsoft の更新プログラムを、WUfB に接続して更新プログラムを受信するクライアントに展開できません。  

-   Configuration Manager は、WSUS に発行され、かつ Configuration Manager を介して管理されるサード パーティの更新プログラムを、WUfB に接続して更新プログラムを受信するクライアントに展開できません。  

-   ソフトウェア更新プログラムのインフラストラクチャを使用する Configuration Manager の完全なクライアント展開は、WUfB に接続して更新プログラムを受信するクライアントに対しては機能しません。  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>WUfB を使用して Windows 10 の更新プログラムを取得するクライアントを識別する  
 次の手順を使用して、Windows 10 の更新プログラムとアップグレードの取得に WUfB を使用するクライアントを識別し、WSUS を使用して更新プログラムを取得することをやめるようそれらのクライアントを構成して、これらのクライアントのソフトウェア更新ワークフローを無効にするためのクライアント エージェント設定を展開します。  

 **必要条件**  

-   Windows 10 Desktop Pro または Windows 10 Enterprise Edition バージョン 1511 以降を実行するクライアント  

-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) が展開され、クライアントが WUfB を使用して Windows 10 の更新プログラムとアップグレードを取得している。  

#### <a name="to-identify-clients-that-use-wufb"></a>WUfB を使用するクライアントを識別するには  

1.  Windows Update エージェントが以前有効になっていた場合は、WSUS がスキャンされないように、無効にします。   
    レジストリ キー **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer** を設定し、コンピューターによって WSUS または Windows Update がスキャンされるかどうかを指定できます。  この値が 2 の場合、WSUS についてはスキャンされません。  

2.  Configuration Manager リソース エクスプローラーで、**Windows Update** ノードの下に新しい属性 **UseWUServer** を確認できます。  

3.  更新プログラムとアップグレードのために WUfB を介して接続されているすべてのコンピューターを対象とした **UseWUServer** 属性に基づいて、コレクションを作成します。  

4.  ソフトウェア更新プログラム ワークフローを無効にするクライアント エージェント設定を作成し、WUfB に直接接続されているコンピューターのコレクションに、この設定を展開します。  

5.  WUfB を介して管理されているコンピューターの対応ステータスには **[不明]** と表示され、全体のコンプライアンス対応率をカウントする際に、これらのコンピューターは除外されます。  



<!--HONumber=Nov16_HO1-->


