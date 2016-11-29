---
title: "PFX 証明書プロファイルを作成する | System Center Configuration Manager"
description: "System Center Configuration Manager で PFX ファイルを使用して暗号化されたデータ交換をサポートするユーザーに固有の証明書を生成する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0185ab18-663d-468a-ba54-4f3f232fd4d2
caps.latest.revision: 5
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4a4025325e635061cb99caed9cdb07390e90ea90


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager で PFX 証明書プロファイルを作成する方法

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager では、ユーザーのデバイスに Personal Information Exchange (.pfx) ファイルをプロビジョニングできます。 PFX ファイルを使用してユーザー固有の証明書を生成すると、データ交換の暗号化に対応できます。 PFX 証明書は、Configuration Manager 内で作成するか、またはインポートすることもできます。 System Center Configuration Manager では、インポートしたか、新しく作成した PFX 証明書を iOS、Android、および Windows 10 のデバイスに配置できます。 これらのファイルを複数のデバイスに配置すると、ユーザー ベースの PKI 通信をサポートできます。  

> [!TIP]  
>  このプロセスの手順について説明したチュートリアルは、「 [Configuration Manager で PFX 証明書プロファイルを作成および展開する方法](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)」に記載されています。  

## <a name="create-and-deploy-personal-information-exchange-pfx-certificate-profiles"></a>Personal Information Exchange (PFX) 証明書プロファイルを作成、配置する  

#### <a name="how-to-create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Personal Information Exchange (PFX) 証明書プロファイルの作成と配置方法  

1.  System Center Configuration Manager コンソールで、[**資産とコンプライアンス**] をクリックします。  

2.  [ **資産とコンプライアンス** ] ワークスペースで、[ **コンプライアンス設定**]、[ **会社のリソースへのアクセス**] の順に展開してから、[ **証明書プロファイル**] をクリックします。  

3.  [ **ホーム** ] タブの [ **作成** ] グループで、[ **証明書プロファイルの作成**] をクリックします。 **[証明書プロファイルの作成]** ウィザードを開きます。  

4.  **[証明書プロファイルの作成]** ウィザードの **[全般]** ページで、次の情報を指定します。  

    -   **名前**: 証明書プロファイルの固有な名前を入力します。 最大 256 文字を使用できます。  

    -   **説明**: System Center Configuration Manager コンソールで証明書プロファイルを区別しやすくなるように、簡単な説明と他の関連情報を入力します。 最大 256 文字を使用できます。  

    -   **作成する証明書プロファイルの種類を指定します**: 次の証明書プロファイルの種類のいずれかを選択します。  

        -   **信頼された証明機関証明書**: ユーザーまたはデバイスが他のデバイスを認証する必要があり、信頼されたルート証明機関 (CA) 証明書または中間 CA 証明書を展開して証明書チェーンを形成したい場合に、この種類を選択します。 たとえば、リモート認証ダイヤルイン ユーザー サービス (RADIUS) サーバーや仮想プライベート ネットワーク (VPN) サーバーなどのデバイスで認証する場合が当てはまります。 また、SCEP 証明書プロファイルを作成する前に、信頼された証明機関証明書を構成する必要があります。 この場合は、信頼された CA 証明書は、ユーザーまたはデバイスに証明書を発行する証明機関の信頼されたルート証明書でなければなりません。  

        -   **SCEP (Simple Certificate Enrollment Protocol) 設定**: Simple Certificate Enrollment Protocol とネットワーク デバイス登録サービスの役割を使用して、デバイスまたはユーザーの証明書を要求する場合は、この証明書プロファイルの種類を選択します。  

        -   **Personal Information Exchange – PKCS #12 (PFX) 設定のインポート**: PFX 証明書をインポートする場合に、これを選択します。  

5.  **[証明書プロファイルの作成]** ウィザードの **[証明書のプロパティ]** ウィンドウで、対象デバイス上の PFX 証明書の格納場所を指定します。  

    -   **トラステッド プラットフォーム モジュール (TPM) にインストールする (存在する場合)**  

    -   **トラステッド プラットフォーム モジュール (TPM) にインストールする (それ以外は失敗)**  

    -   **ソフトウェア キー記憶域プロバイダーにインストールする**  

     **[次へ]**をクリックします。  

6.  **[証明書プロファイルの作成]** ウィザードの **[サポート対象のプラットフォーム]** ウィンドウで、インポートされた PFX ファイルを受け取ることができるオペレーティング システムまたはプラットフォームを指定します。  

    -   **Windows 10**  

    -   **iPhone**  

    -   **iPad**  

    -   **Android**  

7.  **[次へ]**をクリックし、 **[概要]** ページを確認してウィザードを終了します。  

8.  現在、PFX ファイルを含む証明書プロファイルは **[証明書プロファイル]** ワークスペースから取得できます。  **資産とコンプライアンス** ワークスペースで、 **コンプライアンス設定** > **会社のリソースへのアクセス** > **証明書プロファイル** の順に進み、右クリックして [ユーザー コレクション] に新しい証明書を配置します。  

9. ダウンロード センターから入手できる Windows 8.1 用 SDK を使用して ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525))、PFX 作成スクリプトを配置します。 Configuration Manager 2012 SP2 に追加された PFX 作成スクリプトは、SDK に SMS_ClientPfxCertificate クラスを追加します。 このクラスには、次のメソッドが含まれています。  

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

    -   <blob\> = The PFX base64-encrypted blob  

    -   $Password = PFX ファイルのパスワード  

    -   $ProfileName = PFX プロファイル名  

    -   ComputerName = ホスト コンピューター名  



<!--HONumber=Nov16_HO1-->


