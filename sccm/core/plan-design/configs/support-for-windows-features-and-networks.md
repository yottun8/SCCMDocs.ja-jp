---
title: Windows 機能のサポート
titleSuffix: Configuration Manager
description: Configuration Manager でサポートされる Windows とネットワークの機能について説明します。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 915a8ac1d20ca288b2b830791c8a3b79c65ffbce
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383649"
---
# <a name="support-for-windows-features-and-networks-in-configuration-manager"></a>Configuration Manager での Windows 機能とネットワークのサポート

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、Configuration Manager による一般的な Windows とネットワークの機能のサポートを示します。  



##  <a name="bkmk_branchcache"></a> BranchCache  

配布ポイントで Windows BranchCache を有効にしているときは Configuration Manager で BranchCache を使用し、分散キャッシュ モードでそれを使用するようにクライアントを構成します。

アプリケーションの展開の種類、パッケージの展開、およびタスク シーケンスに関する BranchCache の設定を構成します。 バージョン 1802 以降では、BranchCache は既定で有効になります。 

BranchCache の要件を満たしている場合、リモートの場所にあるクライアントは、この機能を使用して、コンテンツの最新のキャッシュを持っているローカルのクライアントからコンテンツを取得できます。  

たとえば、BranchCache が有効な最初のクライアントが、BranchCache サーバーとして構成されている配布ポイントからコンテンツを要求するとき、クライアントはコンテンツをダウンロードしてキャッシュします。 これと同じコンテンツを要求する同じサブネット上のクライアントは、このコンテンツを利用できるようになります。

これらのクライアントもそのコンテンツをキャッシュします。 同じサブネット上の他のクライアントは、配布ポイントからコンテンツをダウンロードする必要はありません。 コンテンツは、今後の転送に備えて複数のクライアントに分散されます。  


### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Configuration Manager で BranchCache をサポートするための要件

#### <a name="configure-distribution-points"></a>配布ポイントを構成する
配布ポイントとして構成されたサイト システム サーバーに **Windows BranchCache** 機能を追加します。    
- BranchCache をサポートするように構成されたサーバー上の配布ポイントには、追加の構成は必要ありません。   
- Windows BranchCache をクラウド ベースの配布ポイントに追加することはできません。 クラウドベースの配布ポイントは、Windows BranchCache が構成されているクライアントによるコンテンツのダウンロードをサポートしています。  

#### <a name="configure-clients"></a>クライアントを構成する    
- BranchCache に対応したクライアントが、BranchCache 分散キャッシュ モード用に構成されている必要があります。  
- BranchCache をサポートするには、BITS クライアント設定に対する OS 設定を有効にする必要があります。  

詳細については、Windows ドキュメントの[BranchCache のクライアントの構成](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache)に関するページを参照してください。


### <a name="configuration-manager-supported-os-versions-with-windows-branchcache"></a>Configuration Manager でサポートされている OS バージョンと Windows BranchCache

|オペレーティング&nbsp;システム|サポートの詳細|  
|----------------------|---------------------|  
|Windows 7 SP1|既定でサポート|  
|Windows 8|既定でサポート|  
|Windows 8.1|既定でサポート|  
|Windows 10|既定でサポート|  
|Windows Server 2008 SP2|**BITS 4.0 が必要**: BITS 4.0 リリースを構成マネージャー クライアントにインストールするには、ソフトウェアの更新プログラムまたはソフトウェアの配布を使用します。 詳細については、「[Windows Management Framework Core](https://support.microsoft.com/help/968929/windows-management-framework-windows-powershell-2-0-winrm-2-0-and-bits)」を参照してください。<br /><br /> この OS では、BranchCache クライアント機能はネットワークから実行されるソフトウェアの配布または SMB ファイル転送ではサポートされません。 加えてこの OS では、BranchCache の機能をクラウド ベースの配布ポイントで使用することができません。|  
|Windows Server 2008 R2|既定でサポート|  
|Windows Server 2012|既定でサポート|  
|Windows Server 2012 R2|既定でサポート|  
|Windows Server 2016|既定でサポート|  

BranchCache の詳細については、Windows Server ドキュメントの [Windows の BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) に関するページを参照してください。  



##  <a name="bkmk_Workgroups"></a> ワークグループ内のコンピューター  

Configuration Manager では、ワークグループ内のクライアントがサポートされます。  

- Configuration Manager では、ワークグループとドメインとの間でのクライアントの移動がサポートされます。 詳しくは、[構成マネージャー クライアントをワークグループ コンピューターに手動でインストール方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientWorkgroup)に関するページをご覧ください。  

> [!NOTE]  
>  ワークグループのクライアントはサポートされますが、すべてのサイト システムは、サポートされた Active Directory ドメインのメンバーである必要があります。  



##  <a name="bkmmk_datadedup"></a> データ重複除去  

Configuration Manager は、次に示すオペレーティング システム上の配布ポイントで、データ重複除去の使用をサポートしています。  

-   Windows Server 2016
-   Windows Server 2012 R2  
-   Windows Server 2012  


> [!IMPORTANT]  
>  パッケージ ソース ファイルをホストするボリュームは、データ重複除去の対象としてマークできません。 この制限は、データ重複除去で再解析ポイントが使用されることから発生します。 Configuration Manager では、再解析ポイントで保存したファイルが含まれるコンテンツ ソースの場所の使用はサポートされていません。  

詳細については、Configuration Manager チームのブログ「[ Configuration Manager Distribution Points and Windows Server 2012 Data Deduplication](https://cloudblogs.microsoft.com/enterprisemobility/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication/)」(Configuration Manager の配布ポイントと Windows Server 2012 のデータ重複除去) および Windows Server ドキュメントの「[データ重複除去の概要](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview)」を参照してください。  



##  <a name="bkmk_DA"></a> DirectAccess  

Configuration Manager では、クライアントとサイト サーバー システム間の通信用に DirectAccess 機能をサポートしています。  

- DirectAccess の要件がすべて満たされている場合、DirectAccess を使用することで、インターネット上の Configuration Manager クライアントは、イントラネット上にいるかのように割り当て先のサイトと通信できます。  

- リモート コントロールやクライアント プッシュ インストールなど、サーバーで開始されるアクションについては、開始するコンピューターで IPv6 が実行されている必要があります。 介在するネットワーク デバイスのすべてで、このプロトコルがサポートされている必要があります。  

Configuration Manager では、次に示す DirectAccess を利用した機能はサポートされていません。  

-   OS の展開   

-   Configuration Manager サイト間の通信  

-   サイト内の Configuration Manager サイト システム サーバー間の通信  



##  <a name="bkmk_dualboot"></a> デュアル ブート コンピューター  

Configuration Manager では、1 台のコンピューター上の複数の OS を管理できません。 1 台の管理対象コンピューターに複数の OS がある場合は、管理対象の OS のみに構成マネージャー クライアントがインストールされるようにするためにサイトの探索方法およびインストール方法を調整します。  



##  <a name="bkmk_IPv6"></a> IPv6  

Configuration Manager では、インターネット プロトコル バージョン 4 (IPv4) に加えて、インターネット プロトコル バージョン 6 (IPv6) をサポートしています。ただし次の例外があります。  

|機能| IPv6 のサポートの例外|  
|--------------|-------------------------------|  
|クラウドベースの配布ポイント|Microsoft Azure とクラウド ベースの配布ポイントをサポートするには、IPv4 が必要です。|  
|クラウド管理ゲートウェイ|Microsoft Azure とクラウド管理ゲートウェイをサポートするには、IPv4 が必要です。|  
|Microsoft Intune および Microsoft サービス コネクタで登録されるモバイル デバイス|Microsoft Intune および Microsoft サービス コネクタで登録されるモバイル デバイスをサポートするには、IPv4 が必要です。|  
|ネットワーク探索|ネットワーク探索で検索するように DHCP サーバーを構成した場合は、IPv4 が必要です。|  
|OS の展開|バージョン 1802 以前では、OS の展開をサポートするには IPv4 が必要です。  </br> </br> バージョン 1806 以降では、Windows 展開サービスなしで、配布ポイントで PXE レスポンダーを有効にします。 この新しい PXE レスポンダー サービスは、IPv6 をサポートします。 タスク シーケンス中の静的 IP アドレスのキャプチャや設定など、OS 展開機能の他の部分では、引き続き IPv4 が必要です。 |  
|ウェイクアップ プロキシ通信|クライアントのウェイクアップ プロキシ パケットをサポートするには、IPv4 が必要です。|  
|Windows CE|Windows CE デバイスで Configuration Manager クライアントをサポートするには、IPv4 が必要です。|  



##  <a name="bkmk_NAT"></a> ネットワーク アドレス変換  

Configuration Manager では、ネットワーク アドレス変換 (NAT) はサポートされていません。ただし、サイトがインターネット上のクライアントをサポートしていて、クライアントがインターネットに接続されていることを検出する場合を除きます。 インターネットベースのクライアント管理の詳細については、[インターネット ベースのクライアント管理の計画](/sccm/core/clients/deploy/plan/plan-for-managing-internet-based-clients)に関するページを参照してください。  



##  <a name="bkmk_storage"></a> 特殊なストレージ技術  

Configuration Manager は、Configuration Manager コンポーネントがインストールされている OS のバージョン用の Windows ハードウェア互換性リストで認定されているハードウェアで動作するように設計されています。

System Center Configuration Manager でディレクトリとファイルのアクセス許可を設定できるようにするために、サイト サーバーの役割では NTFS が必要です。 Configuration Manager では、論理ドライブの完全な所有権が与えられていることを前提としています。 個別のコンピューター上で実行されているサイト システムは、ストレージ技術を問わず論理パーティションを共有できません。 ただし、各コンピューターは、共有ストレージ デバイスの同じ物理パーティションにある個別の論理パーティションを使用できます。  

### <a name="support-considerations"></a>サポートに関する考慮事項

- **記憶域ネットワーク**: 記憶域ネットワーク (SAN) は、サポート対象の Windows ベースのサーバーが、SAN でホストされているボリュームに直接接続されている場合にサポートされます。  

- **単一インスタンス記憶域**: Configuration Manager では、単一インスタンス記憶域 (SIS) が有効なボリューム上の配布ポイント パッケージと署名フォルダーの構成はサポートされていません。  

     さらに、構成マネージャー クライアントのキャッシュは、SIS が有効なボリュームではサポートされていません。  

- **リムーバブル ディスク ドライブ**: Configuration Manager では、リムーバブル ディスク ドライブへの Configuration Manager サイト システムまたはクライアントのインストールはサポートされていません。  
