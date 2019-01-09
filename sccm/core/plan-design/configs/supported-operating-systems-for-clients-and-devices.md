---
title: サポートされるクライアントとデバイス
titleSuffix: Configuration Manager
description: Configuration Manager がクライアントとデバイスをサポートする OS のバージョンについて説明します。
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6f60d7f3a8c3bd81f4de38b2ce4080f54756de14
ms.sourcegitcommit: c60e057075a83f07d1ca2577c3de1c7d7c8e9cec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2018
ms.locfileid: "53626465"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Configuration Manager でクライアントとデバイスに対してサポートされる OS のバージョン

*適用対象:System Center Configuration Manager (Current Branch)*

 Configuration Manager は、Windows、Mac、Linux、および UNIX コンピューター上のクライアント ソフトウェアのインストールをサポートします。  

#### <a name="requirements-and-limitations-for-all-clients"></a>すべてのクライアントの要件と制限事項  

-   Configuration Manager サービスについては、スタートアップの種類や**ログオン方法**の設定の変更はサポートされていません。 変更すると、主要なサービスが正しく実行できなくなる可能性があります。    

-   root 以外のアカウント下のコンピューターでは、Linux または UNIX の Configuration Manager クライアントや Mac 用クライアントをインストールすることも実行することもサポートされません。 そのようにすると、主要なサービスが正しく実行できなくなる可能性があります。  



##  <a name="windows-computers"></a>Windows コンピューター  

 次のバージョンの Windows OS を管理するには、Configuration Manager に含まれているクライアントを使用します。 詳しくは、「[Windows コンピューターにクライアントを展開する方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)」をご覧ください。  


### <a name="supported-client-os-versions"></a>サポートされているクライアントの OS のバージョン

-   **Windows 10**  

    詳細については、[Windows 10 のサポート](/sccm/core/plan-design/configs/support-for-windows-10)に関するページをご覧ください。  

-   **Windows 8.1** (x86、x64):Professional、Enterprise    

-   **Windows 7 SP1** (x86、x64):Professional、Enterprise、および Ultimate    


### <a name="supported-server-os-versions"></a>サポートされているサーバーの OS のバージョン

-  **Windows Server 2019**:Standard、Datacenter <sup>[注 1](#bkmk_note1)</sup>  
    (Configuration Manager バージョン 1806 以降。)

-  **Windows Server 2016**:Standard、Datacenter <sup>[注 1](#bkmk_note1)</sup>  

-   **Windows Storage Server 2016**:Workgroup、Standard  

-   **Windows Server 2012 R2** (x64):Standard、Datacenter <sup>[注 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64):Standard、Datacenter <sup>[注 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 SP1** (x64):Standard、Enterprise、Datacenter <sup>[注 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2008 R2** (x86、x64):Workgroup、Standard、Enterprise    

-   **Windows Server 2008 SP2** (x86、x64):Standard、Enterprise、Datacenter <sup>[注 1](#bkmk_note1)</sup>    


#### <a name="server-core"></a>Server Core
次のバージョンでは具体的に OS の Server Core インストールが参照されます。 <sup>[注 3](#bkmk_note3)</sup>  

Windows Server の半期チャネル バージョンは Server Core インストールです (Windows Server バージョン 1809 など)。 Configuration Manager クライアントとして、これらは関連する Windows 10 の半期チャネル バージョンと同じようにサポートされています。 詳細については、[Windows 10 のサポート](/sccm/core/plan-design/configs/support-for-windows-10)に関するページをご覧ください。


-   **Windows Server 2019** (x64) <sup>[注 2](#bkmk_note2)</sup>  

-   **Windows Server 2016** (x64) <sup>[注 2](#bkmk_note2)</sup>   

-   **Windows Server 2012 R2** (x64) <sup>[注 2](#bkmk_note2)</sup>     

-   **Windows Server 2012** (x64) <sup>[注 2](#bkmk_note2)</sup>     

-   **Windows Server 2008 R2** サービス パックなし、または SP1 (x64)     

-   **Windows Server 2008 SP2** (x86、x64)   

#### <a name="bkmk_note1"></a> 注 1
 Configuration Manager では Windows Server Datacenter エディションがテストおよびサポートされていますが、Windows Server に対して公式に認定されていません。 Windows Server Datacenter エディションに固有の問題に対しては、Configuration Manager の修正プログラムのサポートは提供されません。 Windows Server の認定プログラムについて詳しくは、[Windows Server カタログ](https://www.windowsservercatalog.com/)をご覧ください。 

#### <a name="bkmk_note2"></a> 注 2
 [クライアント プッシュ インストール](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation)をサポートするには、[ファイルおよび記憶域サービス] サーバー ロールのファイル サーバー サービスを追加します。 Server Core への Windows 機能のインストールについて詳しくは、「[Install roles, role services, and features by using Windows PowerShell cmdlets](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installwps)」(Windows PowerShell コマンドレットを使用して役割、役割サービス、機能をインストールする) をご覧ください。  

#### <a name="bkmk_note3"></a> 注 3
 新しいソフトウェア センター アプリは、Windows Server Core のどのバージョンでもサポートされていません。<!--SCCMDocs issue 683-->



##  <a name="windows-embedded-computers"></a>Windows Embedded コンピューター  

 Windows Embedded デバイスを管理するには、デバイス上に Configuration Manager クライアントをインストールします。 詳細については、「[Windows Embedded デバイスへのクライアント展開の計画](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices)」を参照してください。  


### <a name="requirements-and-limitations"></a>要件と制限事項

-   すべてのクライアント機能は、書き込みフィルターが有効ではない Windows Embedded システムでサポートされます。  

-   次のいずれかを使用するクライアントは、電源管理以外のすべての機能がサポートされます。  

    -   Enhanced Write Filter (EWF)    

    -   RAM ファイル ベースの書き込みフィルター (FBWF)    

    -   Unified Write Filter (UWF)  

-   アプリケーション カタログは、どのような Windows Embedded デバイスについてもサポートされません。  


### <a name="supported-os-versions"></a>サポートされている OS のバージョン  

-   **Windows 10 Enterprise** (x86、x64)  

-   **Windows 10 IoT Enterprise** (x86、x64)  
    このバージョンには、長期的なサービス チャネル (LTSC) が含まれています。 詳しくは、「[Overview of Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise)」(Windows 10 IoT Enterprise の概要) をご覧ください。<!--SCCMDocs issue 560-->  

-   **Windows Embedded 8.1 Industry** (x86、x64)    

-   **Windows Embedded 8 Standard** (x86、x64)    

-   **Windows Thin PC** (x86、x64)    

-   **Windows Embedded POSReady 7** (x86、x64)    

-   **Windows Embedded Standard 7 SP1** (x86、x64)    



## <a name="windows-ce-computers"></a>Windows CE コンピューター

 Configuration Manager に含まれる Configuration Manager モバイル デバイス レガシ クライアントで Windows CE デバイスを管理します。  


### <a name="requirements-and-limitations"></a>要件と制限事項  

-   モバイル デバイス クライアントのインストールには、0.78 MB の記憶領域が必要です。 サインインするには、さらに最大で 256 KB の追加の記憶領域が必要な場合があります。    

-   これらのモバイル デバイスの機能は、プラットフォームとクライアントの種類によって異なります。 サポートされる管理機能の詳細については、「[デバイス管理ソリューションの選択](/sccm/core/plan-design/choose-a-device-management-solution)」を参照してください。  


### <a name="supported-os-versions"></a>サポートされている OS のバージョン  

-   Windows CE 7.0 (ARM および x86 プロセッサ)  

#### <a name="supported-languages-include"></a>次の言語がサポートされています

-   中国語 (簡体字、繁体字)    

-   英語 (米国)    

-   フランス語 (フランス)    

-   ドイツ語    

-   イタリア語    

-   日本語  

-   韓国語  

-   ポルトガル語 (ブラジル)  

-   ロシア語  

-   スペイン語 (スペイン)  



## <a name="mac-computers"></a>Mac コンピューター  

 Mac 向けの Configuration Manager クライアントで macOS コンピューターを管理します。  

 Configuration Manager メディアでは、Mac クライアント インストール パッケージは提供されません。 [Microsoft ダウンロード センター](http://go.microsoft.com/fwlink/?LinkID=525184)から、**追加のオペレーティング システム用のクライアント**をダウンロードします。  

 詳しくは、「[Mac にクライアントを展開する方法](/sccm/core/clients/deploy/deploy-clients-to-macs)」をご覧ください。  


### <a name="supported-versions"></a>サポートされるバージョン

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)

-   **Mac OS X 10.13** (macOS High Sierra)

- **macOS Mojave (10.14)** 


##  <a name="linux-and-unix-servers"></a>Linux および UNIX サーバー  

> [!Important]  
> 2018 年 3 月 22 日現在、Configuration Manager 向けの Linux および UNIX クライアントは非推奨になっています。 詳しくは、「[Linux と Unix のクライアント サポートの廃止告知](/sccm/core/plan-design/changes/whats-new-in-version-1802#deprecation-announcement-for-linux-and-unix-client-support)」をご覧ください。  

 Linux および UNIX 用の Configuration Manager クライアントで Linux および UNIX サーバーを管理します。  

 Configuration Manager メディアでは、Linux および UNIX クライアント インストール パッケージは提供されません。 [Microsoft ダウンロード センター](http://go.microsoft.com/fwlink/?LinkID=525184)から、**追加のオペレーティング システム用のクライアント**をダウンロードします。 クライアント インストール パッケージに加え、クライアント ダウンロードには、各コンピューター上でクライアントのインストールを管理するスクリプトも含まれています。  


### <a name="requirements-and-limitations"></a>要件と制限事項

-   Linux および UNIX 向けクライアントの OS ファイルの依存関係を確認するには、「[Linux および UNIX サーバーへのクライアントの展開の前提条件](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#BKMK_ClientDeployPrereqforLnU)」をご覧ください。  

-   Linux または UNIX を実行するコンピューターでサポートされている管理機能の概要については、「[UNIX および Linux サーバーにクライアントを展開する方法](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)」をご覧ください。  

-   Linux および UNIX のサポートされるバージョンの場合、一覧に示したバージョンには後続のマイナー バージョンがすべて含まれます。 たとえば、CentOS バージョン 6 には CentOS 6.3 が含まれています。 同様に、サービス パックを使用する OS (SUSE Linux Enterprise Server 11 SP1 など) がサポートされている場合は、その OS のバージョンの後続のサービス パックもサポートに含まれます。  

-   Linux と UNIX でクライアントをインストールする方法については、「[UNIX および Linux サーバーにクライアントを展開する方法](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)」をご覧ください。  


### <a name="supported-versions"></a>サポートされるバージョン

次のバージョンは、指定された .tar ファイルを使用してサポートされます。  

#### <a name="aix"></a>AIX  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 6.1 (Power)|ccm-Aix61ppc.&lt;ビルド\>.tar|  
|バージョン 7.1 (Power)|ccm-Aix71ppc.&lt;ビルド\>.tar|  

#### <a name="centos"></a>CentOS  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 5 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 5 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 6 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 6 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 7 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

#### <a name="debian"></a>Debian  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 5 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 5 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 6 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 6 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 7 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 7 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 8 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 8 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;ビルド\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 5 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 5 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 6 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 6 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 7 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 5 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 5 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 6 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 6 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 7 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

#### <a name="solaris"></a>Solaris  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 10 x86|ccm-Sol10x86.&lt;ビルド\>.tar|  
|バージョン 10 SPARC|ccm-Sol10sparc.&lt;ビルド\>.tar|  
|バージョン 11 x86|ccm-Sol11x86.&lt;ビルド\>.tar|  
|バージョン 11 SPARC|ccm-Sol11sparc.&lt;ビルド\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 10 SP1 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 10 SP1 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 11 SP1 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 11 SP1 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 12 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|バージョン|TAR ファイル|  
|-|-|  
|バージョン 10.04 LTS x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 10.04 LTS x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 12.04 LTS x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 12.04 LTS x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 14.04 LTS x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 14.04 LTS x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 16.04 LTS x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 16.04 LTS x64|ccm-Universalx64.&lt;ビルド\>.tar|  



##  <a name="bkmk_OnpremOS"></a> オンプレミス モバイル デバイス管理  

 Configuration Manager には、クライアント ソフトウェアをインストールすることがないオンプレミスであるデバイスを管理する組み込みの機能があります。 詳しくは、「[オンプレミス インフラストラクチャを使用したモバイル デバイスの管理](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure)」をご覧ください。  


### <a name="requirements-and-limitations"></a>要件と制限事項

-   階層の最上位層で、**サービス接続ポイント**を構成します。  


### <a name="supported-operating-systems"></a>サポートされるオペレーティング システム

- **Windows 10 Pro** (x86、x64)  

- **Windows 10 Pro Enterprise** (x86、x64)  

- **Windows 10 IoT Enterprise** (x86、x64)  
    このバージョンには、長期的なサービス チャネル (LTSC) が含まれています。 詳しくは、「[Overview of Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise)」(Windows 10 IoT Enterprise の概要) をご覧ください。<!--SCCMDocs issue 560-->  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

- **Windows 10 IoT Mobile Enterprise**  

- **Surface Hub の Windows 10 Team**  



##  <a name="bkmk_ExSrvConOS"></a> Exchange Server コネクタ  

Configuration Manager は、Configuration Manager クライアントをインストールすることがない、Exchange サーバーに接続するデバイスの限定された管理をサポートしています。 詳しくは、「[Configuration Manager と Exchange によるモバイル デバイスの管理](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)」をご覧ください。  


### <a name="supported-versions-of-exchange-server"></a>サポートされている Exchange Server のバージョン

- **Exchange Online (Office 365)**:このバージョンには、Business Productivity Online Standard Suite が含まれます  

- **Exchange Server 2016** (バージョン 1802 以降)  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** または **Exchange Server 2010 SP2** 
