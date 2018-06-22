---
title: ソフトウェア更新プログラムの前提条件
titleSuffix: Configuration Manager
description: System Center Configuration Manager でのソフトウェア更新プログラムの前提条件について説明します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: 1c5377096ef67057f3f38bb71fb611b7993ecb6b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353108"
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>System Center Configuration Manager でのソフトウェア更新プログラムの前提条件

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、System Center Configuration Manager でのソフトウェア更新プログラムの前提条件の一覧を示します。 前提条件ごとに、外部の依存関係と内部の依存関係を別の表にまとめています。  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Configuration Manager 外部のソフトウェア更新プログラムの依存関係  
 次のセクションに、ソフトウェア更新の外部の依存関係の一覧を示します。  

### <a name="internet-information-services"></a>インターネット インフォメーション サービス  
 ソフトウェアの更新ポイント、管理ポイント、および配布ポイントを実行するには、サイト システム サーバーにインターネット インフォメーション サービス (IIS) がインストールされている必要があります。 詳細については、「[サイト システムの役割の前提条件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)」を参照してください。  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 ソフトウェア更新プログラムの同期と、クライアントでのソフトウェア更新プログラムの適用性スキャンを行うには、Windows Server Update Services (WSUS) が必要です。 WSUS サーバーは、ソフトウェア更新ポイントの役割を作成する前にインストールする必要があります。 ソフトウェアの更新ポイントでは、次のバージョンの WSUS がサポートされています。  

-   WSUS 10.0 (Windows Server 2016 における役割)
-   WSUS 6.2 および 6.3 (Windows Server 2012 および Windows Server 2012 R2 における役割)  
-   WSUS 3.2 (Windows Server 2008 R2 における役割)  

1 つのサイトにソフトウェアの更新ポイントが複数ある場合、すべてのポイントが同じバージョンの WSUS を実行するようにします。  

> [!WARNING]  
>  **アップグレード**のソフトウェア更新プログラムの分類は、WSUS 4.0 以降のみでサポートされています。 この新しい分類を同期し、Windows 10 サービス プランで Windows 10 コンピューターを評価できるようにする前に、ソフトウェアの更新ポイントとサイト サーバーに WSUS の [修正プログラム 3095113](https://support.microsoft.com/kb/3095113) をインストールする必要があります。 この修正プログラムは、Windows 10 の機能アップグレードを同期および配布するために、Windows Server 2012 ベースのサーバーまたは Windows Server 2012 R2 ベースのサーバーで WSUS を有効にします。 詳細については、「[サービスとしての Windows の管理](../../osd/deploy-use/manage-windows-as-a-service.md)」を参照してください。  
>   
>  [修正プログラム 3095113](https://support.microsoft.com/kb/3095113) をインストールする前に**アップグレード**分類のソフトウェア更新プログラムを同期する場合は、「[KB 3095113 をインストールする前のアップグレード カテゴリの同期からの回復](#BKMK_RecoverUpgrades)」をご覧ください。  

### <a name="wsus-administration-console"></a>WSUS 管理コンソール  
 ソフトウェアの更新ポイントがリモート サイトのシステム サーバー上にあり、WSUS がそのサイト サーバーにインストールされていない場合、Configuration Manager サイト サーバーには WSUS 管理コンソールが必要です。  

> [!IMPORTANT]  
> サイト サーバーの WSUS バージョンは、ソフトウェアの更新ポイントで実行されている WSUS バージョンと同じにする必要があります。
>
> WSUS 管理コンソールを使って WSUS の設定を構成しないでください。 Configuration Manager はソフトウェアの更新ポイントで実行されている WSUS のインスタンスに接続し、適切な設定を構成します。  



### <a name="windows-update-agent"></a>Windows 更新エージェント  
 クライアントが WSUS サーバーに接続できるようにするには、Windows Update エージェント (WUA) クライアントが必要です。 WUA は、コンプライアンスのスキャンに必要なソフトウェア更新プログラムの一覧を取得します。  

 Configuration Manager をインストールすると、最新バージョンの WUA がダウンロードされます。 次に、Configuration Manager クライアントをインストールすると、必要に応じて WUA がアップグレードされます。 インストールに失敗した場合は、別の方法で WUA をアップグレードする必要があります。  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Configuration Manager 内部のソフトウェア更新プログラムの依存関係  
 次のセクションに、Configuration Manager のソフトウェア更新の内部の依存関係の一覧を示します。  

### <a name="management-points"></a>管理ポイント  
 管理ポイントは、クライアント コンピューターと Configuration Manager サイト間で情報を転送します。 管理ポイントは、ソフトウェア更新プログラムに必要です。  

### <a name="software-update-points"></a>ソフトウェアの更新ポイント  
 Configuration Manager でソフトウェア更新プログラムを展開できるようにするには、ソフトウェアの更新ポイントを WSUS サーバーにインストールする必要があります。 詳細については、「[ソフトウェアの更新ポイントのインストールと構成](../get-started/install-a-software-update-point.md)」を参照してください。

### <a name="distribution-points"></a>配布ポイント  
 ソフトウェア更新プログラムのコンテンツを保存できる配布ポイントが必要です。 配布ポイントをインストールして、コンテンツを管理する方法の詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

### <a name="client-settings-for-software-updates"></a>ソフトウェア更新プログラムのクライアントの設定  
 既定では、クライアントのソフトウェア更新プログラムは有効です。 ただし、クライアントがソフトウェア更新プログラムのコンプライアンスを評価する方法とタイミングを制御し、ソフトウェア更新プログラムのインストール方法を制御するために使用できるその他の設定があります。  

 詳細については、以下の記事を参照してください。  

-   [ソフトウェア更新プログラムのクライアントの設定](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

-   [ソフトウェア更新プログラムのクライアントの設定](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>レポート サービス ポイント  
 レポート サービス ポイントのサイト システムの役割は、ソフトウェア更新プログラムのレポートを表示できます。 この役割は任意ですが、使用することをお勧めします。 レポート サービス ポイントの作成方法の詳細については、[レポートの構成](../../core/servers/manage/configuring-reporting.md)に関するページを参照してください。  

##  <a name="BKMK_RecoverUpgrades"></a> KB 3095113 をインストールする前のアップグレード カテゴリの同期からの回復  
 **アップグレード**分類を同期する前に、ソフトウェアの更新ポイントとサイト サーバーに WSUS の[修正プログラム 3095113](https://support.microsoft.com/kb/3095113) をインストールする必要があります。 **アップグレード**分類が有効になっているときに修正プログラムがインストールされていない場合、WSUS は関連付けられているパッケージを適切にダウンロードして展開できない場合でも、Windows 10 ビルド 1511 の機能アップグレードを表示します。 
 
 [修正プログラム 3095113](https://support.microsoft.com/kb/3095113) を最初にインストールせずにアップグレードを同期する場合、WSUS データベース (SUSDB) に使用できないデータを読み込みます。 アップグレードを適切に展開するには、そのデータをクリアする必要があります。 この問題から回復するには、次の手順を実行します。  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>KB 3095113 をインストールする前に、アップグレード分類の同期から回復するには  

1.  **アップグレード**分類のソフトウェア更新プログラムを削除します。 次のサンプル スクリプトのような PowerShell スクリプトを使用することができます。  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  次の手順に進む前に、Configuration Manager 階層内のすべてのソフトウェアの更新ポイントでスクリプトを実行する必要があります。  

     **アップグレード**分類のソフトウェア更新プログラムを一括で削除するために、テキスト ファイルから複数の GUID を読み取るように PowerShell スクリプトを変更できます。  

2.  ソフトウェアの更新ポイント コンポーネントのプロパティで**アップグレード**分類をオフにします  (詳細については、「[同期する分類と製品の構成](../get-started/configure-classifications-and-products.md)」を参照してください)。ソフトウェア更新プログラムの同期を開始します  (詳細については、「[ソフトウェア更新プログラムの同期](../get-started/synchronize-software-updates.md)」を参照してください)。  

3.  ソフトウェアの更新ポイントとサイト サーバーに、WSUS の [修正プログラム 3095113](https://support.microsoft.com/kb/3095113) をインストールする必要があります。  

4.  ソフトウェアの更新ポイント コンポーネントのプロパティで**アップグレード**分類を選択します  (詳細については、「[同期する分類と製品の構成](../get-started/configure-classifications-and-products.md)」を参照してください)。ソフトウェア更新プログラムの同期を開始します  (詳細については、「[ソフトウェア更新プログラムの同期](../get-started/synchronize-software-updates.md)」を参照してください)。  

## <a name="next-steps"></a>次のステップ
[ソフトウェア更新管理の準備](../get-started/prepare-for-software-updates-management.md)
