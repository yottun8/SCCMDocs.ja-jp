---
title: ビジネス向け Microsoft Store
titleSuffix: Configuration Manager
description: Configuration Manager を使用してビジネス向け Microsoft Store のアプリを管理および展開する
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ae137cae29d49413ca11668ff0cc744168e91e21
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383679"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-configuration-manager"></a>Configuration Manager を使用してビジネス向け Microsoft Store のアプリを管理する

[ビジネス向け Microsoft Store ](https://www.microsoft.com/business-store) では、組織向けの Windows アプリを検索して取得できます。 Configuration Manager にストアを接続すると、取得したアプリの一覧が同期されます。 Configuration Manager コンソールでこれらのアプリを表示し、他のアプリと同様に展開します。


## <a name="bkmk_apps"></a> オンライン アプリとオフライン アプリ

ビジネス向け Microsoft Store は、次の 2 種類のアプリをサポートしています。

- **オンライン**: この種類のライセンスでは、ユーザーとデバイスはストアに接続してアプリとそのライセンスを取得する必要があります。 Windows 10 デバイスは、Azure Active Directory (Azure AD) ドメインに参加している必要があります。  

- **オフライン**: アプリとライセンスをキャッシュし、オンプレミス ネットワーク内で直接展開できます。 デバイスをストアに接続したり、インターネットに接続したりする必要はありません。

ビジネス向け Microsoft Store の詳細については、[こちら](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview)を参照してください。

Configuration Manager では、Configuration Manager クライアントを使用した Windows 10 デバイスと、Microsoft Intune に登録されている Windows 10 デバイスの両方でビジネス向け Microsoft Store アプリを管理できます。 Configuration Manager は、オンラインおよびオフライン アプリ向けに次の機能を提供します。


|機能|オフライン アプリ|オンライン アプリ|
|------------|------------|------------|
|アプリ データと Configuration Manager の同期<br>(同期は 24 時間ごとに発生)|はい|はい|
|ストア アプリからの Configuration Manager アプリケーションの作成|はい|はい|
|ストアからの無料アプリのサポート|はい|はい|
|ストアからの有料アプリのサポート|いいえ|○<sup>1</sup>|
|ユーザーまたはデバイス コレクションへの必要な展開のサポート|はい|はい|
|ユーザーまたはデバイス コレクションへの利用可能な展開のサポート|はい|はい|
|ストアからの基幹業務アプリのサポート|はい|はい|
|デバイス上のすべてのユーザーに対するストア アプリのプロビジョニング<sup>2</sup><!--1358310-->|はい|はい|

- <sup>1</sup> 構成マネージャー クライアントで Windows 10 デバイスにオンライン ライセンス アプリを展開するには、Windows 10 バージョン 1703 以降を実行している必要があります。  

- <sup>2</sup> バージョン 1806 以降。 詳しくは、「[Windows アプリケーションを作成する](/sccm/apps/get-started/creating-windows-applications#bkmk_provision)」をご覧ください。  


### <a name="deploying-online-apps-using-the-microsoft-store-for-business-to-devices-that-run-the-configuration-manager-client"></a>構成マネージャー クライアントを実行しているデバイスへのビジネス向け Microsoft Store を使用したオンライン アプリの展開

完全な構成マネージャー クライアントを実行しているデバイスにビジネス向け Microsoft Store アプリを展開する前に、次のことを考慮してください。

- フル機能のためには、デバイスが Windows 10 バージョン 1703 以降を実行している必要があります。  

- デバイスは、管理ツールとしてビジネス向け Microsoft Store を登録したのと同じテナントにある Azure AD に参加する必要があります。  

- ローカル Administrator アカウントがデバイスでサインインしたときは、ビジネス向け Microsoft Store アプリにアクセスできません。  

- デバイスにはビジネス向け Microsoft Store へのライブ インターネット接続が必要です。 プロキシの構成などについて詳しくは、[前提条件](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business)に関するページをご覧ください。  


### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>以前のバージョンの Windows 10 を実行しているデバイスに関する注意

構成マネージャー クライアントがあり、Windows 10 バージョン 1607 以前を実行しているデバイスでは、次の機能が適用されます。  

次のいずれかの方法で、デバイスへのアプリのインストールを強制するとき:  

- ユーザーがアプリをインストールする  

- 展開がインストールの期限に達する   

- 必要な展開のインストール後の再評価  

以下の動作が発生します。  

- 構成マネージャー クライアントはビジネス向け Microsoft Store アプリを起動することによってアプリを "強制" します  

- ユーザーはストアからのインストールを完了する必要があります  

- Configuration Manager コンソールではアプリ展開の状態は失敗と報告され、"Microsoft Store アプリをクライアント PC で開いています。ユーザーがインストールを完了するのを待機しています" というエラーが表示されます。  

次のアプリケーションの評価サイクル時:  

- ユーザーがストアからアプリケーションをインストールした場合、そのアプリケーションは**成功**状態を報告します。  

- ユーザーがストアからのアプリのインストールを試みなかった場合:  

    - 必要な展開の場合、構成マネージャー クライアントはストア アプリの起動をもう一度試みます  

    - 利用可能な展開は再強制されません


#### <a name="further-notes-for-devices-running-earlier-versions-of-windows-10"></a>以前のバージョンの Windows 10 を実行しているデバイスに関するその他の注意:

- ビジネス向け Microsoft Store から基幹業務アプリを展開することはできません。  

- ストアから有料アプリを展開する場合、ユーザーはストアにサインインし、アプリ自体を取得する必要があります  

- コンシューマー バージョンの Microsoft Store へのアクセスを無効にするグループ ポリシーを展開する場合、ビジネス向け Microsoft Store から展開することはできません。 この動作は、ビジネス向け Microsoft Store が有効な場合でも発生します。  



## <a name="bkmk_setup"></a> ビジネス向け Microsoft Store の同期を設定する

組織が取得したアプリの一覧を同期すると、Configuration Manager コンソールでこれらのアプリを確認できます。

Configuration Manager サイトを Azure AD とビジネス向け Microsoft Store に接続します。 このプロセスについて詳しくは、「[Azure サービスの構成](/sccm/core/servers/deploy/configure/azure-services-wizard)」をご覧ください。 **ビジネス向け Microsoft Store** サービスへの接続を作成します。


### <a name="bkmk_config"></a> 補足情報と構成 

Azure サービス ウィザードの **[アプリ]** ページで、最初に **[Azure 環境]** と **[Web アプリ]** を構成します。 その後、ページの下部にある **[詳細情報]** セクションを読みます。 この情報には、ビジネス向け Microsoft Store ポータルでの次の追加アクションが含まれます。  

- ストア管理ツールとして Configuration Manager を構成します。 詳しくは、[管理プロバイダーの構成](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business)に関するページをご覧ください。  

- オフラインのライセンスされたアプリのサポートを有効にします。 詳しくは、「[オフライン アプリの配布](https://docs.microsoft.com/microsoft-store/distribute-offline-apps)」をご覧ください。  

- 少なくとも 1 つのアプリを取得します。 詳しくは、「[アプリを探して入手する](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview)」をご覧ください。  

Azure サービス ウィザードの **[構成]** ページで、次の情報を指定します。  

- **[ビジネス向け Microsoft ストア アプリのコンテンツの記憶域のパス]**: フォルダーを含む共有ネットワーク パスを指定します。 たとえば、`\\server\share\folder` となります。 サイト サーバーは、ストアと同期するとき、この場所にコンテンツをキャッシュします。 Configuration Manager でアプリケーションを作成すると、サイト サーバーはこのローカル キャッシュからサイトのコンテンツ ライブラリにアプリのコンテンツをコピーします。  

- **[選択した言語]**: ストアから同期し、ソフトウェア センターのユーザーに表示する言語を選択します。 たとえば、ユーザーが Windows をドイツ語用に構成している場合、ソフトウェア センターはストア アプリにドイツ語の文字列を表示します。 この動作では、その言語が同期されていて、特定のアプリケーションに存在している必要があります。    

- **[既定の言語]**: ユーザーの言語が利用できない場合に使用する既定の言語を選択します。  



## <a name="bkmk_deploy"></a> ビジネス向け Microsoft Store アプリから Configuration Manager アプリケーションを作成して展開する

同期後、他のアプリと同様に、ストア アプリを作成して展開します。

1.  Configuration Manager コンソールの **[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** を展開し、**[ストア アプリのライセンス情報]** をクリックします。  

2.  展開するアプリを選んでから、リボンの **[アプリケーションの作成]** をクリックします。  

ビジネス向け Microsoft Store アプリを含む Configuration Manager アプリケーションがサイトで作成されます。 

他の Configuration Manager のアプリケーションと同様に、このアプリケーションを展開して監視します。 詳細については、以下の記事を参照してください。  
- [アプリケーションの展開](/sccm/apps/deploy-use/deploy-applications)
- [コンソールからのアプリケーションの監視](/sccm/apps/deploy-use/monitor-applications-from-the-console)

> [!IMPORTANT]  
> Microsoft Intune に登録されたデバイスの場合、展開されたアプリは当初デバイスを登録したユーザーのみが利用できます。 それ以外のユーザーはアプリにアクセスできません。



## <a name="next-steps"></a>次のステップ

**[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** を展開し、**[ストア アプリのライセンス情報]** をクリックします。

管理するストア アプリごとに、アプリに関する次の情報を表示します。
- アプリ名
- アプリのプラットフォーム
- アプリの所有しているライセンス数
- 使用可能なライセンス数

オンライン アプリを展開した後、そのアプリに対する更新プログラムは Microsoft Store から直接提供されます。 さらに、Configuration Manager はオンライン アプリのバージョンの準拠状況をチェックしません。アプリがインストール済みであることが Windows によって報告されるだけです。  

オフライン アプリを構成マネージャー クライアントを使用した Windows 10 デバイスに展開する場合、Configuration Manager の展開の外部のアプリケーションをユーザーが更新できないようにしてください。 オフライン アプリの更新の制御は、教室などのマルチ ユーザー環境で特に重要です。 Microsoft Store を無効にする 1 つのオプションは、[グループ ポリシー](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy)を使用することです。 

ビジネス向け Microsoft Store 管理者がオフライン アプリを取得した後に、そのアプリをストアを経由してユーザーに公開しないでください。 この構成は、ユーザーがオンラインでインストールまたは更新できないようにします。 ユーザーは Configuration Manager を介してオフライン アプリの更新プログラムのみを受信します。 
