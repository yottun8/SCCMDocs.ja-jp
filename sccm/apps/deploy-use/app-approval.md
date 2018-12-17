---
title: アプリケーションの承認
titleSuffix: Configuration Manager
description: Configuration Manager でのアプリケーション承認の設定と動作について説明します。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f19146da963055ffc20b274e1017802274844698
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52458128"
---
# <a name="approve-applications-in-configuration-manager"></a>Configuration Manager でアプリケーションを承認する

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager で[アプリケーションを展開する](/sccm/apps/deploy-use/deploy-applications)ときに、インストールする前に承認を要求することができます。 ソフトウェア センターでユーザーからアプリケーションを要求されたら、その要求を Configuration Manager コンソールで確認します。 要求を承認または拒否することができます。 



## <a name="bkmk_approval"></a> 承認設定

アプリケーションの承認動作は、Configuration Manager のバージョンによって異なります。 次の承認設定のいずれかが、アプリケーション展開の **[展開の設定]** ページに表示されます。  

#### <a name="require-administrator-approval-if-users-request-this-application"></a>ユーザーがこのアプリケーションを要求した場合に管理者の承認を必要とする
*適用対象: バージョン 1710 以前*

管理者がアプリケーションに対するユーザー要求を承認するまで、ユーザーはそのアプリケーションをインストールできません。 展開目的が **[必須]** である場合、またはアプリケーションをデバイス コレクションに展開する場合は、このオプションは淡色表示されます。  

アプリケーション承認要求は、**[ソフトウェア ライブラリ]** ワークスペースの **[アプリケーション管理]** の下にある **[承認要求]** ノードに表示されます。 要求は、30 日以内に承認されなければ削除されます。 クライアントを再インストールすると、保留承認要求が取り消される可能性があります。  

アプリケーションのインストールを承認した後は、Configuration Manager コンソールで要求を**拒否**することができます。 この操作によってクライアントがデバイスからアプリケーションをアンインストールすることはありません。 ユーザーは、ソフトウェア センターからアプリケーションの新しいコピーをインストールできなくなります。  


#### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a>管理者は、デバイス上のこのアプリケーションへの要求を承認する必要があります
*適用対象: バージョン 1802 以降 <sup>[注 1](#bkmk_note1)</sup>*

<a name="bkmk_note1"></a>

> [!Note]  
> **注 1**: Configuration Manager では、このオプション機能は既定で無効になっています。 この機能は、使用する前に有効にする必要があります。 詳細については、「[Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)」 (更新プログラムのオプション機能の有効化) を参照してください。 
> 
> この機能を有効にしない場合、前のエクスペリエンスが表示されます。  

管理者がアプリケーションに対するユーザー要求を承認するまで、ユーザーは要求したデバイスにそのアプリケーションをインストールできません。 管理者が要求を承認した場合、ユーザーはそのデバイスにのみアプリケーションをインストールできます。 別のデバイスにアプリケーションをインストールするには、ユーザーは別の要求を送信する必要があります。 展開目的が **[必須]** である場合、またはアプリケーションをデバイス コレクションに展開する場合は、このオプションは淡色表示されます。 <!--1357015-->  

> [!Note]  
> Configuration Manager の新機能を利用するには、最初にクライアントを最新バージョンに更新します。 サイトとコンソールを更新すると Configuration Manager コンソールに新しい機能が表示されますが、クライアントのバージョンも最新になるまでは完全なシナリオは機能しません。<!--SCCMDocs issue 646-->  

Configuration Manager コンソールの **[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** の **[承認要求]** を確認します。 各要求のリストに、**[デバイス]** 列が追加されています。 要求に対するアクションを実行するとき、[アプリケーションの要求] ダイアログ ボックスには、ユーザーが要求を送信したデバイスの名前も表示されます。  

要求は、30 日以内に承認されなければ削除されます。 クライアントを再インストールすると、保留承認要求が取り消される可能性があります。  

アプリケーションのインストールを承認した後は、Configuration Manager コンソールで要求を**拒否**することができます。 この操作によってクライアントがデバイスからアプリケーションをアンインストールすることはありません。 ユーザーは、ソフトウェア センターからアプリケーションの新しいコピーをインストールできなくなります。  

> [!Important]  
> バージョン 1806 以降、以前に承認してインストールしていたアプリケーションに対する承認を取り消した場合の "*動作が変更されました*"。 アプリケーションの要求を **[拒否]** すると、クライアントによってユーザーのデバイスからアプリケーションがアンインストールされるようになりました。<!--1357891-->  



## <a name="bkmk_email-approve"></a> メール通知
<!--1321550-->

バージョン 1810 以降では、アプリケーションの承認を要求するメール通知を構成します。 ユーザーがアプリケーションを要求すると、管理者はメールを受け取ります。 メールのリンクをクリックして、要求を承認または拒否できます。Configuration Manager コンソールは必要ありません。


### <a name="prerequisites"></a>[前提条件]

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>メール通知を送信し、内部ネットワーク上でアクションを実行するには
これらの前提条件により、受信者は要求の通知メールを受け取ります。 受信者が内部ネットワーク上にいる場合、メールから要求を承認または拒否することができます。

- [オプション機能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)の **[デバイスごとにユーザーのアプリケーション要求を承認します]** を有効にします。  

- [アラートのメール通知](/sccm/core/servers/manage/use-alerts-and-the-status-system#to-configure-email-notification-for-alerts)を構成します。  



#### <a name="to-take-action-from-internet"></a>インターネットからアクションを実行するには
これら追加オプションの前提条件により、受信者はインターネットにアクセスできる任意の場所から要求を承認または拒否することができます。

- クラウド管理ゲートウェイ経由で SMS プロバイダーの管理サービスを有効にします。 Configuration Manager コンソールで、**[管理]** ワークスペースに移動し、**[サイトの構成]** を展開して **[サーバーとサイト システムの役割]** ノードを選択します。 SMS プロバイダーの役割を持つサーバーを選択します。 詳細ウィンドウで **[SMS プロバイダー]** 役割を選択して、[サイトの役割] タブのリボンで **[プロパティ]** を選択します。**[管理サービスで Configuration Manager クラウド管理ゲートウェイ トラフィックを許可する]** のオプションを選択します。  

    - SMS プロバイダーでは **.NET 4.5.2** 以降が必要です。  

- [クラウド管理ゲートウェイ](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)  

- **クラウド管理**のために [Azure サービス](/sccm/core/servers/deploy/configure/azure-services-wizard)にサイトをオンボードします  

    - [Azure AD ユーザー探索](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)を有効にします  

    - Azure AD で設定を手動で構成します。  

        1. [Azure portal](https://portal.azure.com) に移動して、**[Azure Active Directory]**、**[アプリの登録]** の順に選択します。  

        2. Configuration Manager **クラウド管理**の統合用に作成した**ネイティブ**の種類のアプリケーションを選択します。  

        3. アプリのプロパティで **[設定]**、**[リダイレクト URI]** の順に選択します。  

            1. [リダイレクト URI] ウィンドウで、次のパスを貼り付けます。`https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

            2. `<CMG FQDN>` をクラウド管理ゲートウェイ (CMG) サービスの完全修飾ドメイン名 (FQDN) で置き換えます。 例: GraniteFalls.Contoso.com。  

            3. 次に、**[保存]** を選択します。 **[設定]** ウィンドウを閉じます。  

        4. アプリのプロパティで、**[マニフェスト]** を選択します。  

            1. [マニフェストの編集] ウィンドウで、**oauth2AllowImplicitFlow** プロパティを探します。  

            2. その値を **true** に変更します。 たとえば、行全体が次の行のようになります。`"oauth2AllowImplicitFlow": true,`   

            3. **[保存]** を選択します。  


### <a name="configure-email-approval"></a>メールの承認を構成する

1. Configuration Manager コンソールで、ユーザー コレクションに使用できるように[アプリケーションを展開](/sccm/apps/deploy-use/deploy-applications)します。 **[展開の設定]** ページで、承認に対して有効にします。 通知を受け取るアドレスを 1 つ以上入力します。 メール アドレスはセミコロン (`;`) で区切ります。  

     > [!Note]  
     > Azure AD 組織内でメールを受け取るすべてのユーザーが、要求を承認できます。 他のユーザーにアクションを実行させるのでない限り、他のユーザーにメールを転送しないでください。  

2. ユーザーが、ソフトウェア センターでアプリケーションを要求します。  

3. 5 分以内に通知メールが届きます。 メールの内容は、次の例のようになります。  

![アプリケーション承認のメール通知の例](media/1321550-email.png)

> [!Note]  
> 承認または拒否のためのリンクは、1 回しか使用できません。 たとえば、通知を受け取るためのグループの別名を構成します。 あるユーザーが要求を承認します。 その場合、別のユーザーは要求を拒否できません。  

トラブルシューティングのため、サイト サーバーで **NotiCtrl.log** ファイルを確認します。


## <a name="maintenance"></a>メンテナンス 

Configuration Manager により、アプリケーション承認要求に関する情報がサイト データベースに保存されます。 取り消された要求または拒否された要求については、30 日を経過すると、サイトによって要求履歴から削除されます。 削除動作は、**[期限切れのアプリケーション要求データの削除]** [サイトのメンテナンス タスク](/sccm/core/servers/manage/maintenance-tasks)で構成できます。 承認済みまたは保留中のアプリケーション要求がサイトで削除されることはありません。

