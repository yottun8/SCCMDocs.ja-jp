---
title: "PFX 証明書プロファイルの作成 | Microsoft Docs"
description: "System Center Configuration Manager で PFX ファイルを使用して暗号化されたデータ交換をサポートするユーザーに固有の証明書を生成する方法について説明します。"
ms.custom: na
ms.date: 03/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3b1451edaed69a972551bd060293839aa11ec8b2
ms.openlocfilehash: 2495cef2442706b343bac6d510946c1226b64cfc
ms.lasthandoff: 03/28/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager で PFX 証明書プロファイルを作成する方法

*適用対象: System Center Configuration Manager (Current Branch)*

証明書プロファイルは、ユーザーが会社のリソースにシームレスにアクセスできるように、Active Directory 証明書サービスとネットワーク デバイス登録サービスの役割を使用して、管理対象のデバイスの認証証明書をプロビジョニングします。 たとえば、証明書プロファイルを作成し、展開して、ユーザーが VPN 接続およびワイヤレス接続を開始するために必要な証明書を提供することができます。

[証明書プロファイル](../../protect/deploy-use/introduction-to-certificate-profiles.md)に関する記事には、証明書プロファイルの作成と構成に関する一般的な情報が記載されています。 このトピックでは、PFX 証明書に関連した証明書プロファイルの具体的な情報をいくつか取り上げます。

-  Configuration Manager では、要件、デバイスの種類、オペレーティング システムにも応じて、異なる証明書ストアに証明書を展開することがサポートされています。 Intune に登録されている次のデバイスがサポートされます。

 -   iOS  

- その他の前提条件については、[証明書プロファイルの前提条件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)に関する記事を参照してください。

## <a name="pfx-certificate-profiles"></a>PFX 証明書プロファイル
System Center Configuration Manager では、ユーザーのデバイスに Personal Information Exchange (.pfx) ファイルをプロビジョニングできます。 PFX ファイルを使用してユーザー固有の証明書を生成すると、データ交換の暗号化に対応できます。 PFX 証明書は、Configuration Manager 内で作成するか、またはインポートすることもできます。

> [!TIP]  
>  このプロセスの手順について説明したチュートリアルは、「 [Configuration Manager で PFX 証明書プロファイルを作成および展開する方法](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)」に記載されています。  

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Personal Information Exchange (PFX) 証明書プロファイルの作成と配置  

### <a name="get-started"></a>作業開始

1.  System Center Configuration Manager コンソールで、[**資産とコンプライアンス**] をクリックします。  

2.  [ **資産とコンプライアンス** ] ワークスペースで、[ **コンプライアンス設定**]、[ **会社のリソースへのアクセス**] の順に展開してから、[ **証明書プロファイル**] をクリックします。  

3.  [ **ホーム** ] タブの [ **作成** ] グループで、[ **証明書プロファイルの作成**] をクリックします。

4.  **[証明書プロファイルの作成]** ウィザードの **[全般]** ページで、次の情報を指定します。  

    -   **名前**: 証明書プロファイルの固有な名前を入力します。 最大 256 文字を使用できます。  

    -   **説明**: System Center Configuration Manager コンソールで証明書プロファイルを区別しやすくなるように、簡単な説明と他の関連情報を入力します。 最大 256 文字を使用できます。  

    -   **[作成する証明書プロファイルの種類を指定します]**: PFX 証明書の場合、次のいずれかを選びます。  

        -   **Personal Information Exchange -- PKCS #12 (PFX) 設定 -- インポート**: PFX 証明書をインポートするには、これを選びます。  
        -   **[Personal Information Exchange -- PKCS #12 (PFX) 設定 -- 作成]**: 新しい PFX 証明書を作成するには、これを選びます。

### <a name="import-a-pfx-certificate"></a>PFX 証明書をインポートする

PFX 証明書をインポートするには、Configuration Manager SDK が必要です。 ユーザー用にインポートしたすべての証明書は、ユーザーが登録しているすべてのデバイスに展開されます。

1. **[証明書プロファイルの作成ウィザード]** の **[PFX 証明書]** ページで、証明書を保存する展開先デバイス上の場所を指定します。
    -     **トラステッド プラットフォーム モジュール (TPM) にインストールする (存在する場合)**  
    -   **トラステッド プラットフォーム モジュール (TPM) にインストールする (それ以外は失敗)** 
    -   **Windows Hello for Business にインストールする (それ以外は失敗)** 
    -   **ソフトウェア キー記憶域プロバイダーにインストールする** 
2. [次へ] をクリックします。 **** 
3. ウィザードの **[サポートされているプラットフォーム]** ページでこの証明書をインストールするデバイスのプラットフォームを選び、**[次へ]** をクリックします。
4. ダウンロード センターから入手できる Windows 8.1 用 SDK を使用して ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525))、PFX 作成スクリプトを配置します。 Configuration Manager 2012 SP2 に追加された PFX 作成スクリプトは、SDK に SMS_ClientPfxCertificate クラスを追加します。 このクラスには、次のメソッドが含まれています。  

    -   ImportForUser  

    -   DeleteForUser  

     サンプル スクリプト:  

```  
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  

```  

次のスクリプト変数はスクリプトに合わせて変更する必要があります。  

   -   blob\ = PFX の base64 で暗号化された blob  
   -   $Password = PFX ファイルのパスワード  
   -   $ProfileName = PFX プロファイル名  
   -   ComputerName = ホスト コンピューター名   

### <a name="create-a-new-pfx-certificate"></a>新しい PFX 証明書を作成する

PFX 証明書を作成して展開すると、ユーザーが登録しているすべてのデバイスに同じ証明書がインストールされます。

1. ウィザードの **[サポートされているプラットフォーム]** ページでこの証明書をインストールするデバイスのプラットフォームを選び、**[次へ]** をクリックします。
2. ウィザードの **[証明機関]** ページで、次のように構成します。
    - **[プライマリ サイト]** - 証明機関を選ぶ Configuration Manager のプライマリ サイトを選びます。
    - **[証明機関]** - プライマリ サイトを選んだ後、一覧から証明機関を選び、**[次へ]** をクリックします。
3. ウィザードの **[PFX 証明書]** ページで、次の値を構成します。
    - **[更新しきい値 (%)]** - 証明書の有効期間の残りがどの程度 (%) になったら、デバイスが更新を要求するかを指定します。
    - **[証明書テンプレート名]** - **[参照]** をクリックして、発行元 CA に追加されている証明書テンプレートの名前を選びます。 証明書テンプレートを参照するには、Configuration Manager コンソールを実行するために使うユーザー アカウントが、証明書テンプレートに対する**読み取り**アクセス許可を持っている必要があります。 または、証明書テンプレートの名前を入力します。 
    - **[サブジェクト名の形式]** - 一覧から、Configuration Manager が証明書要求のサブジェクト名を自動生成する方法を選びます。 証明書がユーザー用の場合、サブジェクト名にユーザーのメール アドレスを追加することもできます。 **[共通名]** または **[完全な識別名]** を選びます。
    - **[サブジェクトの別名]** - Configuration Manager が証明書要求のサブジェクトの別名 (SAN) を自動生成する方法を指定します。 たとえば、ユーザー証明書の種類を選択した場合は、サブジェクトの別名にユーザー プリンシパル名 (UPN) を含めることができます。 次の中から選択します。
        - **電子メール アドレス** 
        - **ユーザー プリンシパル名 (UPN)** 
    - **証明書の有効期間** - 
    - **[Windows キー記憶域プロバイダー]** (サポートされているプラットフォームとして Windows を選んだ場合にのみ表示されます) - 
        -     **トラステッド プラットフォーム モジュール (TPM) にインストールする (存在する場合)**  
        -   **トラステッド プラットフォーム モジュール (TPM) にインストールする (それ以外は失敗)** 
        -   **Windows Hello for Business にインストールする (それ以外は失敗)** 
        -   **ソフトウェア キー記憶域プロバイダーにインストールする** 
4. [次へ] をクリックします。 ****

### <a name="finish-up"></a>完了

1.  **[次へ]**をクリックし、 **[概要]** ページを確認してウィザードを終了します。  
2.  現在、PFX ファイルを含む証明書プロファイルは **[証明書プロファイル]** ワークスペースから取得できます。 
3.  プロファイルを展開するには、**[資産とコンプライアンス]** ワークスペースで、**[コンプライアンス設定]** > **[会社のリソースへのアクセス]** > **[証明書プロファイル]** の順に開き、証明書を右クリックして、**[展開]** をクリックします。 



## <a name="see-also"></a>関連項目
「[新しい証明書プロファイルを作成する](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile)」では、証明書プロファイルの作成ウィザードについて説明します。

[Wi-Fi、VPN、電子メール、および証明書プロファイルの展開](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)に関する記事では、証明書プロファイルの展開について説明します。
