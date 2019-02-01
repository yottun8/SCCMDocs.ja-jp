---
title: Azure でのラボの作成
titleSuffix: Configuration Manager
description: Azure テンプレートを使用して、Configuration Manager Technical Preview ラボの作成を自動化する
ms.date: 01/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a6f087b6905d307c707b95e3926a01b0c482f857
ms.sourcegitcommit: b8167a60fd6f2d8387b2db723976c0e2c4198d33
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "54833025"
---
# <a name="create-a-configuration-manager-technical-preview-lab-in-azure"></a>Azure で Configuration Manager Technical Preview ラボを作成する

「オブジェクトの*適用対象: System Center Configuration Manager (Technical Preview)*

<!--3556017-->

このガイドでは、Microsoft Azure で Configuration Manager ラボ環境を構築する方法について説明します。 Azure テンプレートを使用して、Azure リソースを用いたラボの作成が簡略化および自動化されます。 このプロセスでは、最新バージョンの Configuration Manager Technical Preview Branch をインストールします。 

Configuration Manager Current Branch の詳細については、「[Azure での Configuration Manager](/sccm/core/understand/configuration-manager-on-azure)」を参照してください。



## <a name="prerequisites"></a>[前提条件]

このプロセスでは、次のオブジェクトを作成できる Azure サブスクリプションが必要です。 
- 4 つの Standard_D2s_v3 仮想マシン
- Standard_LRS ストレージ アカウント

> [!Tip]  
> 予想されるコストについては、「[Azure の料金計算ツール](https://azure.microsoft.com/pricing/calculator/)」を参照してください。  



## <a name="process"></a>プロセス

1. [Configuration Manager テンプレート](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/)に移動します。  

2. **[Deploy to Azure]\(Azure にデプロイ\)** を選択すると、Azure ポータルが開きます。  

3. 次の情報を使用して、Azure クイック スタート テンプレートを完了します。

    - 基本  

        - **サブスクリプション**:VM を作成するサブスクリプションの名前  

        - **リソース グループ**:これらの VM に使用するリソース グループを選択します  

        - **場所**: このラボ環境をホストする Azure データ センターを選択します  

    - 設定  

        - **プレフィックス**:マシンのプレフィックス名。 詳細については、「[Azure VM の情報](#azure-vm-info)」を参照してください。  

        - **管理者ユーザー名**:管理者権限を持つ、VM のユーザーの名前。 このユーザーを使用して、VM にサインインします。  

        - **管理者パスワード**:パスワードは、Azure の複雑さの要件を満たす必要があります。 詳細については、[adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile) に関するページを参照してください。  

    > [!Important]  
    > Azure では次の設定が必要です。 既定値を使用します。 これらの値は変更しないでください。  
    > 
    > - **[\_artifacts Location]\(_artifacts の場所\)**:このテンプレートのスクリプトの場所 <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **[\_artifacts Location Sas Token]\(_artifacts の場所の SAS トークン\)**:成果物の場所にアクセスするには、sasToken が必要です  
    > 
    > - **場所**: すべてのリソースの場所

4. 使用条件を読みます。 同意する場合は、**[上記の使用条件に同意する]** を選択します。 その後、**[購入]** を選択して続行します。 

Azure では設定を検証してから、デプロイを開始します。 Azure ポータルでデプロイの状態を確認します。 プロセスには、2 時間から 4 時間かかる場合があります。 Azure ポータルにデプロイが正常に行われたことが示されても、構成スクリプトは引き続き実行されます。 プロセス中に VM を再起動しないでください。

構成スクリプトの状態を確認するには、`<prefix>PS1` サーバーに接続し、`%windir%\TEMP\ProvisionScript\PS1.json` ファイルを表示します。 すべての手順が完了と示されたら、プロセスは完了です。

VM に接続するには、まず、Azure ポータルから各 VM のパブリック IP アドレスを取得します。 VM に接続する場合、ドメイン名は `contoso.com` となります。 デプロイ テンプレートで指定した資格情報を使用します。 詳細については、「[Windows が実行されている Azure 仮想マシンに接続してログオンする方法](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon)」を参照してください。



## <a name="azure-vm-info"></a>Azure VM の情報

4 つのすべての VM には、次の仕様があります。
- Standard_D2s_v3。2 つの CPU コアと 8 GB のメモリがあります  
- Windows Server 2016 Datacenter Edition
- 150 GB のディスク領域
- パブリックとプライベートの両方の IP アドレス。 パブリック IP は、TCP ポート 3389 でのリモート デスクトップ接続のみを許可するネットワーク セキュリティ グループにあります。 

デプロイ テンプレートで指定したプレフィックスは、VM 名のプレフィックスです。 たとえば、プレフィックスとして "contoso" を設定した場合、ドメイン コントローラーのコンピューター名は `contosoDC` となります。


### `<prefix>DC`

Active Directory ドメイン コントローラー

#### <a name="windows-features-and-roles"></a>Windows の機能と役割
- Active Directory Domain Services (ADDS)
- .NET
- Remote Differential Compression (RDC)


### `<prefix>PS1`

- SQL Server
- Windows 10 ADK (Windows PE を含む) 
- Configuration Manager プライマリ サイト

#### <a name="windows-features-and-roles"></a>Windows の機能と役割
- .NET
- Remote Differential Compression (RDC) 
- インターネット インフォメーション サービス (IIS)


### `<prefix>MPDP`

- 管理ポイント
- 配布ポイント

#### <a name="windows-features-and-roles"></a>Windows の機能と役割
- .NET
- Remote Differential Compression (RDC) 
- インターネット インフォメーション サービス (IIS)
- バックグラウンド インテリジェント転送サービス (BITS)


### `<prefix>Other`

この VM は、クライアントとして、またはその他のサイトの役割をホストするために使用できます。

#### <a name="windows-features-and-roles"></a>Windows の機能と役割
- .NET
- Remote Differential Compression (RDC) 


