---
title: Windows アプリケーションを作成する
titleSuffix: Configuration Manager
description: Configuration Manager での Windows アプリケーションの作成と展開について詳しく説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 38732081ce27fde764f7d47a565ce1211cef1f54
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383561"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Configuration Manager で Windows アプリケーションを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

[アプリケーションを作成する](/sccm/apps/deploy-use/create-applications)ための Configuration Manager の他の要件と手順に加えて、Windows デバイス用アプリケーションを作成および展開するときには次の考慮事項について検討します。  



## <a name="bkmk_general"></a> 一般的な考慮事項  

Configuration Manager では、Windows 8.1 および Windows 10 デバイスの Windows アプリ パッケージ (.appx) 形式とアプリバンドル (.appxbundle) 形式の展開がサポートされています。

バージョン 1806 以降の Configuration Manager では、Windows 10 の新しいアプリ パッケージ (.msix) 形式とアプリ バンドル (.msixbundle) 形式もサポートされるようになりました。 現在、最新の [Windows Insider Preview](https://insider.windows.com/) ビルドでは、これらの新しい形式がサポートされています。<!--1357427-->  

- MSIX の概要については、「[A closer look at MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/)」(MSIX を詳しく調べる) をご覧ください。  

- 新しい MSIX アプリを作成する方法については、「[MSIX support introduced in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376)」(Insider ビルド 17682 で導入された MSIX のサポート) をご覧ください。  

Configuration Manager コンソールでアプリケーションを作成するときは、アプリケーション インストール ファイルの **[種類]** として **[Windows アプリケーション パッケージ (\*.appx、\*.appxbundle、\* msix、\*.msixbundle)]** を選択します。 詳細については、「[Create applications](/sccm/apps/deploy-use/create-applications)」 (アプリケーションを作成する) を参照してください。 

> [!Note]  
> Configuration Manager の新機能を利用するには、最初にクライアントを最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。<!--SCCMDocs issue 646-->  



## <a name="bkmk_provision"></a> デバイス上のすべてのユーザーに対して Windows アプリ パッケージをプロビジョニングする
<!--1358310--> バージョン 1806 以降では、デバイス上のすべてのユーザーに対して、Windows アプリ パッケージを含むアプリケーションをプロビジョニングします。 このシナリオの 1 つの一般的な例では、ある学校の生徒が使用するすべてのデバイスに、Minecraft: Education Edition などの、ビジネス向け Microsoft Store および教育機関向け Microsoft Store からアプリをプロビジョニングします。 これまでは、Configuration Manager では、これらのアプリケーションのユーザーごとのインストールのみがサポートされていました。 新しいデバイスにサインインした後、学生はアプリにアクセスするまで待機する必要があります。 これからは、すべてのユーザー用のデバイスにアプリがプロビジョニングされている場合、より迅速に生産性を高めることができます。

> [!Important]  
> 予期しない結果になる場合があるため、1 つのデバイス上で同じ Windows アプリ パッケージの異なるバージョンのインストール、プロビジョニング、および更新を行う際には注意してください。 この動作は、Configuration Manager を使用してアプリをプロビジョニングするが、ユーザーに Microsoft Store からのアプリの更新を許可する場合に発生する可能性があります。 詳細については、[ビジネス向け Microsoft Store からアプリを管理する](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps)場合の「次のステップ」のガイダンスを参照してください。  

オフライン ライセンス付きアプリをプロビジョニングする場合、Configuration Manager では、Windows での Microsoft Store からの自動更新は許可されません。  

Configuration Manager では、Windows の次のバージョンでアプリのプロビジョニングがサポートされています。<!--SCCMDocs-pr issue 2762-->
- インストール アクション: Windows 10 バージョン 1607 以降
- アンインストール アクション: Windows 10 バージョン 1703 以降

この機能に対して Windows アプリ展開の種類を構成するには、オプション **[このアプリケーションをデバイス上のすべてのユーザーにプロビジョニングする]** を有効にします。 詳細については、「[Create applications](/sccm/apps/deploy-use/create-applications)」 (アプリケーションを作成する) を参照してください。


> [!Note]  
> ユーザーが既にサインオンしているデバイスからプロビジョニングされたアプリケーションをアンインストールする必要がある場合は、2 つのアンインストール展開を作成する必要があります。 1 つ目のアンインストール展開は、デバイスを含むデバイス コレクションを対象とします。 2 つ目のアンインストール展開は、アプリケーションがプロビジョニングされているデバイスに既にサインオンしているユーザーを含むユーザー コレクションを対象とします。 デバイスのプロビジョニングされているアプリをアンインストールしても、Windows では、現在、そのユーザーのアプリはアンインストールされません。 



## <a name="bkmk_uwp"></a> ユニバーサル Windows プラットフォーム (UWP) アプリのサポート  

Windows 10 デバイスで基幹業務アプリをインストールする場合、サイドローディング キーは不要です。 ただし、Windows でサイドローディングを有効にするには、レジストリ キー `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` の値を **1** にする必要があります。  

このレジストリ キーを構成しないと、アプリをデバイスに初めて展開するときに、Configuration Manager によってこの値が自動的に **1** に設定されます。 この値を **0** に設定した場合、Configuration Manager は値を自動的に変更できず、基幹業務アプリの展開は失敗します。  

UWP 基幹業務アプリにデジタル署名します。 アプリを展開する各デバイスで信頼されているコード署名証明書を使用します。 ユーザーの組織の PKI の証明書を使用するか、または Windows によってパブリック ルート証明書が既に信頼されているサード パーティ プロバイダーから証明書を購入します。  

モバイル アプリ パッケージに署名するには、次の表を参考にして、使用するコード署名証明書の種類を決定します。

| パッケージ  | Symantec  | Symantec 以外  |
|---------|---------|---------|
| Windows 10 Mobile デバイス上のユニバーサル **.appx** パッケージ | はい | はい |
| **.xap** パッケージ | はい | いいえ | 
| Windows 10 Mobile デバイスにインストールするために Windows Phone 8.1 用にビルドされた **.appx** パッケージ | はい | いいえ | 



## <a name="bkmk_mdm-msi"></a> MDM 登録済みの Windows 10 デバイスに Windows インストーラー アプリを展開する  

**MDM を介した Windows インストーラー (\*.msi)** の展開種類では、Windows インストーラー ベースのアプリを作成して、Windows 10 を実行する MDM 登録済みデバイスに展開できます。  

この展開の種類を使用するときは、次の点を考慮してください。    

-   拡張子が MSI のファイルを 1 つだけアップロードします。  

-   Configuration Manager では、アプリの検出にファイルの製品コードと製品バージョンが使われます。  

-   Windows では、アプリの既定の再起動動作が使われます。 Configuration Manager では、アプリの再起動動作は制御されません。  

-   ユーザー単位の MSI パッケージは単一のユーザーにインストールされます。  

-   コンピューター単位の MSI パッケージはデバイスのすべてのユーザーにインストールされます。  

-   Configuration Manager ではアプリの更新プログラムがサポートされます。 各バージョンの MSI 製品コードは同じである必要があります。  
