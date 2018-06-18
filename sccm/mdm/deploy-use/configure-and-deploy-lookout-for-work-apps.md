---
title: Lookout for Work アプリを展開する
titleSuffix: Configuration Manager
description: Lookout for Work アプリを構成し、展開します。
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87ad7a768128cb11a1fc361c90a6eccac454a28c
ms.sourcegitcommit: 9cff0702c2cc0f214173b47ec241f7e5a40f84e6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34752592"
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Lookout for Work アプリを構成し、展開する

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、Android デバイス用と iOS デバイス用の Lookout for Work アプリを構成し、展開する方法について説明します。



## <a name="android-google-play-store-app"></a>Android (Google Play ストア アプリ)
1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]** > **[アプリケーション管理]** > **[アプリケーション]** の順にクリックします。  

2.  ソフトウェアの展開ウィザードの **[全般]** ページで、次の情報を指定します。  
    - 種類: **[Android アプリケーション パッケージ (Google Play 内)]** を選択します。
    - 場所: Google Play ストアから Lookout for Work アプリ リンクをコピーし、ここに貼り付けます。
    - 発行元: Lookout Mobile Security
    - 名前: Lookout for Work
    - 説明: Lookout は、モバイルの脅威に対し最高レベルの保護性能があり、デバイスを安全に保ちます。 Lookout アプリがインストールされている場合は、このアプリによって、脅威からデバイスが保護されます。 脅威が検出された場合、ユーザーと IT 管理者に対してアラートが表示されます。
    - 管理カテゴリ: コンピューター管理  

    正常に完了すると、アプリケーションの一覧に Lookout for Work アプリが表示されます。  

3.  **[ホーム]** タブの **[展開]** グループで、**[展開]** を選択し、Lookout for Work アプリをユーザーに展開します。   
    >[!IMPORTANT]  
    >Lookout MTP コンソールで登録管理オプションに追加した同じユーザーを選択する必要があります。  

    **[必須のインストール]** オプションを選択します。 このオプションを選択した場合は、ユーザーのデバイスに Lookout アプリをインストールする必要があります。  



## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (Lookout アプリの Enterprise 署名版)

1. お使いのデバイスで iOS 管理がセットアップされていることを確認します。 デバイスの iOS 管理のセットアップ方法については、[iOS および Mac のデバイス管理のセットアップ](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)に関するページを参照してください。  

2. Lookout for Work iOS アプリに再署名します。 Lookout により、その Lookout for Work iOS アプリが the iOS App Store の外部で配布されます。 アプリの配布の前に、iOS Enterprise Developer Certificate でアプリに再署名する必要があります。 Lookout for Work iOS アプリの再署名に関する詳細については、Lookout サイトの「[Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/articles/114094038714)」 (Lookout for Work iOS アプリの再署名プロセス) を参照してください。  

3. iOS ユーザーの Azure Active Directory (Azure AD) 認証を有効にします。
   1.  [Azure Portal の [Azure AD] ブレード](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)にサインインし、アプリの登録ページに移動します。  
   2.  [名前] に **[Lookout for Work iOS アプリ]** を指定し、[アプリケーションの種類] として **[ネイティブ]** を選択します。  
  ![アプリの追加ダイアログのスクリーンショット。ネイティブ クライアント アプリ オプションが表示されています。](media/aad-add-app-reg.png)

   3.  このリダイレクト URI には、形式 `lookoutwork://com.lookout.enterprise.<yourcompanyname>` を使用します。`<yourcompanyname>` は会社の名前に変更してください。 例: `lookoutwork://com.lookout.enterprise.contoso`
   4. **[作成]** をクリックし、アプリを作成します。 
   5.  新しいアプリを開き、**[設定]** をクリックし、リダイレクト URI を追加します。 形式 `companyportal://code/<originalURI>` を使用します。`<originalURI>` は、元のリダイレクト URI を URL でエンコードしたバージョンになります。 たとえば、`companyportal://code/lookoutwork%3A%2F%2Fcom.lookout.enterprise.contoso` などです。
   6.  アプリ設定で、**[必要なアクセス許可]** に移動し、**[追加]** をクリックします。 次の委任されたアクセス許可を選択します。  

       | API  | アクセス許可  |
       |---------|---------|
       | Lookout MTP     | Lookout MTP にアクセスする         |
       | Microsoft Graph     | サインインし、ユーザー プロファイルを読む        |  

   詳細については、「[ネイティブ クライアント アプリケーションの構成](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application)」を参照してください。  


4. Configuration Manager で、再署名した .ipa ファイルをアップロードします。 最小 OS バージョンを iOS 8.0 以降に設定します。 詳細については、[iOS アプリケーションの作成](/sccm/apps/get-started/creating-ios-applications)に関するページを参照してください。   


5. 管理対象アプリ構成ポリシーを作成します。 詳細については、[モバイル アプリ構成ポリシーを使用して iOS アプリを構成する](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies)方法に関するページを参照してください。  


6. Lookout for Work アプリをユーザーに展開します。 詳細については、「[アプリケーションの展開](/sccm/apps/deploy-use/deploy-applications)」をご覧ください。  

  Lookout コンソールで登録管理オプションに追加した同じユーザーを選択します。 **[必須のインストール]** オプションを選択します。 このオプションを選択した場合は、ユーザーのデバイスに Lookout アプリをインストールする必要があります。



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>展開したアプリをデバイスで開いたときの動作

ユーザーがデバイスで Lookout for Work を開くと、アプリをアクティブにするよう求められます。 Azure AD オプションを使用してサインインすることを選択する必要があります。 以下の記事に、エンドユーザー フローの詳細なチュートリアルがあります。

- [Android デバイスで Lookout for Work のインストールを求められる](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [Lookout for Work が Android デバイスで検出した脅威を解決する必要がある](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>次のステップ
- [コンプライアンス ポリシーのデバイス脅威保護の規則を有効にする](enable-device-threat-protection-rule-compliance-policy.md)
