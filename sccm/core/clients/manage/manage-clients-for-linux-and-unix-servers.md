---
title: "Linux および UNIX クライアントを管理する | Microsoft Docs"
description: "System Center Configuration Manager で Linux および UNIX サーバーのクライアントを管理します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: d3a44d516bb1e2766a7a10b62d52405eecef31fc


---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>System Center Configuration Manager で Linux および UNIX サーバーのクライアントを管理する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager で Linux および UNIX サーバーを管理する場合、サーバーを管理しやすいように、コレクション、メンテナンス期間、およびクライアント設定を構成できます。 また、Linux および UNIX 用の Configuration Manager クライアントにはユーザー インターフェイスがありませんが、クライアントにクライアント ポリシーの手動ポーリングを強制することもできます。

##  <a name="a-namebkmkcollectionsforlnua-collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 コレクションを使用して Linux および UNIX サーバーのグループを管理する方法は、コレクションで他のクライアントの種類を管理する方法と同じです。 コレクションとして使用できるのは、ダイレクト メンバーシップのコレクションまたはクエリ ベースのコレクションで、これにより、クライアント オペレーティング システム、ハードウェア構成、またはサイト データベースに格納されているクライアントに関するその他の詳細情報が特定されます。 たとえば、Linux および UNIX サーバーを含むコレクションを使用すると、次を管理できます。  

-   クライアント設定  

-   ソフトウェアの展開  

-   メンテナンス期間の適用  

 Linux または UNIX クライアントをそのオペレーティング システムまたはディストリビューションによって特定するには、そのクライアントからハードウェア インベントリを適切に収集しておく必要があります。 カスタム ハードウェア インベントリを収集する方法については、「[Hardware inventory for Linux and UNIX in System Center Configuration Manager](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)」 (System Center Configuration Manager でのハードウェア インベントリ) を参照してください。  

 ハードウェア インベントリの既定のクライアント設定には、クライアント コンピューターのオペレーティング システムに関する情報が含まれます。 **オペレーティング システム** クラスの **キャプション** プロパティを使用すると、Linux または UNIX サーバーのオペレーティング システムを特定できます。  

 Linux および UNIX 用の Configuration Manager クライアントを実行しているコンピューターに関する詳細は、 Configuration Manager コンソールの [資産とコンプライアンス] ワークスペースの [デバイス] ノードで確認できます。 Configuration Manager コンソールの [資産とコンプライアンス] ワークスペースでは、**[オペレーティング システム]** 列に、各コンピューターのオペレーティング システムの名前が表示されます。  

 既定では、Linux および UNIX サーバーは、 **[すべてのシステム]** コレクションのメンバーです。 Linux および UNIX サーバーのみが含まれるカスタム コレクション、またはそのコレクションのサブセットを作成することをお勧めします。 これにより、ソフトウェアを展開する、適用可能なコンピューター グループにクライアント設定を割り当てる、などの操作を管理できます。 たとえば、RHEL6 x64 コンピューターのソフトウェアを、Windows と Linux の両方のコンピューターを含むコレクションに展開すると、展開のステータスは一部成功として表示されます。 ソフトウェアを、RHEL6 x64 コンピューターのみを含むコレクションに展開すると、ステータス メッセージとレポートを使用して、展開が成功したことを正確に特定できます。  

 Linux および UNIX サーバーのカスタム コレクションを作成する場合は、オペレーティング システム属性のキャプション属性が含まれるメンバーシップの規則クエリを追加します。 コレクションを作成する方法については、「[System Center Configuration Manager でコレクションを作成する方法](../../../core/clients/manage/collections/create-collections.md)」を参照してください。  

##  <a name="a-namebkmkmaintenancewindowsforlnua-maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 Linux および UNIX サーバー用の Configuration Manager クライアントでは、メンテナンス期間を使用できます。 これは、Windows ベースのクライアントから変更されていません。  

 メンテナンス期間の詳細については、「[System Center Configuration Manager でメンテナンス期間を使用する方法](../../../core/clients/manage/collections/use-maintenance-windows.md)」を参照してください。  

##  <a name="a-namebkmkclientsettingsforlnua-client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 Linux および UNIX サーバーに適用されるクライアント設定は、他のクライアントの設定と同じ方法で構成できます。  

 既定では、 **[既定のクライアント エージェント設定]** が Linux および UNIX サーバーに適用されます。 カスタム クライアント設定を作成し、特定のクライアント オペレーティング システムが含まれるコレクション、または複数のクライアント オペレーティング システムが混在するコレクションに展開することもできます。  

 Linux および UNIX クライアントにのみ適用される追加のクライアント設定はありません。 ただし、Linux および UNIX クライアントに適用されない既定のクライアント設定は存在します。 Linux および UNIX 用のクライアントには、そのクライアントがサポートする機能の設定のみが適用され、サポートされない機能の構成はすべて無視されます。  

 たとえば、ハードウェア インベントリのスケジュールを指定するカスタム クライアント デバイスの設定を作成し、Linux コンピューターを含むコレクションに割り当てると、 そのハードウェア インベントリのスケジュールは、Linux および UNIX サーバーに適用されます。 次に、リモート コントロールの設定を有効にして構成するカスタム クライアント デバイス設定を作成し、同じコレクションに割り当てます。 この場合、Linux および UNIX サーバーではリモート コントロールの設定が無視されます。 これは、Linux および UNIX 用のクライアントが、Configuration Manager でのリモート コントロールをサポートしていないためです。  

 クライアント設定の構成方法については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../core/clients/deploy/configure-client-settings.md)」を参照してください。  

##  <a name="a-namebkmkpolicyforlnua-computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a> Computer policy for Linux and UNIX servers  
 Linux および UNIX サーバーの Configuration Manager クライアントは、そのサイトを定期的にポーリングしてコンピューター ポリシーを確認し、要求された構成に関する詳細情報を取得して、展開をチェックします。  

 Linux または UNIX サーバーのクライアントにコンピューター ポリシーのポーリングを直ちに実行するように強制することもできます。 ポーリングを直ちに実行するには、サーバーで **ルート** 資格情報を使用して、 **/opt/microsoft/configmgr/bin/ccmexec -rs policy**コマンドを実行します。  

 コンピューター ポリシーのポーリングの詳細が、共有クライアントのログ ファイル **scxcm.log**に入力されます。  

> [!NOTE]  
>  Linux および UNIX 用の Configuration Manager クライアントによって、ユーザー ポリシーの要求や処理が実行されることはありません。  

##  <a name="a-namebkmkmanagelinuxcertsa-how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a> How to manage certificates on the client for Linux and UNIX  
 Linux および UNIX 用のクライアントをインストールした後、 **certutil** ツールを使用して、新しい PKI 証明書でクライアントを更新し、新しい証明書失効リスト (CRL) をインポートできます。 Linux および UNIX 用のクライアントをインストールするとき、このツールは次の場所に配置されます: **/opt/microsoft/configmgr/bin/certutil**  

 証明書を管理するには、各クライアントで、次のいずれかのオプションを指定して certutil を実行します。  

|オプション|説明|  
|------------|----------------------|  
|importPFX|このオプションを使用すると、証明書を指定して、クライアントが現在使用している証明書と置き換えることができます。<br /><br /> **-importPFX** を使用する場合は、**-password** コマンド ライン パラメーターを使って、PKCS#12 ファイルに関連付けられているパスワードを指定する必要もあります。<br /><br /> 追加のルート証明書の要件を指定するには、 **-rootcerts** を使用します。<br /><br /> 例: **certutil -importPFX &lt;Path to the PKCS#12 certificate> -password &lt;Certificate password\> [-rootcerts &lt;証明書のコンマ区切りの一覧>]**|  
|-importsitecert|このオプションを使用すると、管理サーバー上にあるサイト サーバー署名証明書を更新できます。<br /><br /> 例: **certutil -importsitecert &lt;DER 証明書のパス\>**|  
|-importcrl|このオプションを使用すると、1 つ以上の CRL ファイル パスを指定してクライアント上の CRL を更新できます。<br /><br /> 例: **certutil -importcrl &lt;CRL ファイル パスのコンマ区切りの一覧\>**|  



<!--HONumber=Dec16_HO3-->


