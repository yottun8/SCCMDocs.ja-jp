---
title: Intune でのユーザーの移行を準備する
titleSuffix: Configuration Manager
description: ハイブリッド MDM. からユーザーを移行するため、Azure で Intune を準備する方法について説明します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/26/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.collection: M365-identity-device-management
ms.openlocfilehash: e217c7afc2910a23fe3f29fa215d58574f3d79d8
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137815"
---
# <a name="prepare-intune-for-user-migration"></a>Intune でのユーザーの移行を準備する 

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*    
ユーザーをハイブリッド MDM から Intune スタンドアロンに移行する前に、Intune を準備する手順を実行します。 次の手順は、移行されたユーザーとそのデバイスが継続して管理することを確認するのに役立ちます。 次の手順し、Intune への移行を開始すると、ユーザーへの影響を大幅はありません。  

## <a name="fix-issues-found-during-data-collection-and-import"></a>データの収集とインポート中に見つかった問題の修正
Intune Data Importer ツールを使用している場合[を Microsoft Intune に Configuration Manager のデータをインポート](migrate-import-data.md)、それをインポートできませんでしたオブジェクトを集計します。 Intune では、それを修正する手順と一般的な問題は、の一部は、次の表に示します。 

|問題  |修正プログラム  |
|---------|---------|
|ダイレクト メンバーシップまたは、複雑なに基づいてコレクションを自動的に移行されません。|Azure インポートされなかったコレクションを置き換えるには、Azure Active Directory (Azure AD) グループを作成します。 次に、オブジェクトをグループに割り当てます。|
|ポリシーがインポート可能なでした。 |Intune でポリシーを再作成します。|
|インポートされないオブジェクトのデプロイ|オブジェクトをグループに割り当てます。 グループは、展開のコレクションから同じユーザーを含める必要があります。|

## <a name="create-intune-objects"></a>Intune オブジェクトの作成 
場合する[を Microsoft Intune に Configuration Manager のデータをインポート](migrate-import-data.md)プロセス中に問題を修正、インポートされたオブジェクトが正しく構成されていることを確認します。 また、組織で必要な intune (ポリシー、プロファイル、およびアプリ) の追加のオブジェクトを作成します。 

## <a name="assign-intune-licenses-to-migrated-users"></a>Intune ライセンスを移行されたユーザーに割り当てる
Configuration Manager では、Intune サブスクリプションにコレクションを追加して、コレクションのメンバーが自分のデバイスを登録できます。 登録済みデバイスの Intune のライセンスが予約されているときに、ユーザーまたはデバイスに関連付けられていないこれらのライセンス。 たとえばを登録されたデバイスを持つユーザーの Azure AD で Intune のライセンスを検索はありません。 

Intune スタンドアロンにでは、各ユーザーの Intune のライセンスを構成します。 ライセンス構成*する前に*ユーザーを Intune スタンドアロンに移行します。 このアクションは、ユーザーとそのデバイスを MDM 機関の変更後の Intune で管理されていることを確認します。 詳細については、「[ユーザー アカウントに Intune のライセンスを割り当てる](https://docs.microsoft.com/intune/licenses-assign)」を参照してください。 

## <a name="verify-intune-user-groups"></a>Intune ユーザー グループの確認
ユーザーとグループは、ディレクトリ同期を構成する必要があるため、Azure AD で既に可能性があります。 ユーザーが適切なユーザー グループに含まれていることを確認するには、Intune ユーザー グループを確認することをお勧めします。 ポリシー、プロファイル、およびこれらのグループにアプリを対象とします。 Intune スタンドアロンに移行するユーザーが正しいグループに含まれていることを確認します。 

## <a name="configure-role-based-administration-control-rbac"></a>ロール ベースの管理制御 (RBAC) の構成
移行の一環として、Intune で必要なすべての RBAC ロールを構成して、これらのロールにユーザーを割り当てます。 RBAC in Configuration Manager と Intune 間の違いをリソースのスコープの設定などがあります。 詳細については、次を参照してください。 [Intune でのロール ベース管理制御 (RBAC)](https://docs.microsoft.com/intune/role-based-access-control)します。

## <a name="assign-apps-and-policies-to-aad-groups"></a>AAD グループにアプリとポリシーを割り当てる
場合する[を Microsoft Intune に Configuration Manager のデータをインポート](migrate-import-data.md)オブジェクトの多くは Azure AD グループに既に割り当て可能性があります。 (アプリ、ポリシー、およびプロファイル) のすべてのオブジェクトが適切に割り当てられていることを確認します。 Azure AD のグループ。 オブジェクトを正しく割り当てると、ユーザーが移行され、移行には、ユーザーへの大幅影響はありません。 ユーザーのデバイスが自動的に構成します。 Azure AD グループへのオブジェクトの割り当ての詳細については、次の記事を参照してください。 
- [ポリシーの割り当て](https://docs.microsoft.com/intune/get-started-policies)  
- [プロファイルの割り当て](https://docs.microsoft.com/intune/device-profile-assign)  
    > [!NOTE]  
    > Intune では、新しい電子メール プロファイルを展開、ユーザーは自分のパスワードを再入力を求めるメッセージを受け取ります。 この動作は、電子メールがユーザーのデバイスに矛盾する結果します。 ユーザーによって行われた任意のカスタム変更は、もう一度実行する必要があります。 
- [アプリの割り当て](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>使用条件ポリシー
その他のテナント レベルのポリシーと同じように、ご利用のテナントに対して混在機関を有効にすると、使用条件ポリシーが Intune に自動的に移行されます。  ただし、条件を割り当てる必要があります、条件を含むグループを正確に移行されたユーザーの同意をレポートし、条項および条件が将来の条項および条件の更新プログラムまたはデバイスの正しく対象とするかどうかを確認するユーザーを移行します。登録します。 ユーザーは、Configuration Manager コンソールで、ポリシーに加えられた変更がある場合を除き、条件を承諾する必要はありません。 詳細については、次を参照してください。[使用条件を割り当てる](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions)します。

## <a name="configure-the-exchange-connector"></a>Exchange Connector の構成
Exchange を使用して Configuration Manager でオンプレミスの Exchange Connector を設定する場合は、[Intune でオンプレミスの Exchange Connector を構成する](https://docs.microsoft.com/intune/exchange-connector-install)必要があります。 移行後の条件付きアクセスが正常かどうかを確認して、Intune Exchange Connector に移行する際に、次のセクションの情報も検討してください。

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Intune Exchange Connector への移行に役立つ PowerShell スクリプト 
お使いの Exchange デバイスを Configuration Manager Exchange Connector から Intune Exchange Connector に移行する準備に役立つ、PowerShell スクリプトを利用できます。 これらのスクリプトの実行は任意ですが、実行して不要なデバイスを Exchange から削除することをお勧めします。これによって、Intune が不要なデバイスを検出することを防ぎます。 スクリプトを実行することで、Exchange を介して検出されたデバイスを、Intune で登録されたデバイスとできるだけ円滑にマージできます。 これらのスクリプトは Intune Exchange Connector をセットアップする前に実行します。 この PowerShell スクリプトは Intune Data Importer のインストールに含まれており、次の記事で [Configuration Manager のデータを Microsoft Intune にインポート](migrate-import-data.md)するのに使用します。 詳細についておよびスクリプトをダウンロードするには、GitHub の [Microsoft Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer) のページに移動します。

### <a name="steps-to-make-sure-conditional-access-works-properly-after-user-migration"></a>ユーザー移行後に正しく確実に条件付きアクセスの動作を作成する手順
ユーザーを移行した後に適切に機能して、ユーザーが自分の電子メール サーバーにアクセスを継続するかどうかを確認する条件付きアクセスは、次の構成が設定されていることを確認します。
- Exchange ActiveSync の既定のアクセス レベルの設定 (DefaultAccessLevel) がブロックまたは検疫に設定されている場合、デバイスが電子メールへのアクセスを失う可能性があります。 
- Exchange Connector には、Configuration Manager がインストールされている場合、**ルールでは、モバイル デバイスは管理されていないときに、アクセス レベル**設定の値を持つ**アクセスを許可する**、インストール、 [オンプレミス Exchange connector](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access)で Intune ユーザーを移行する前にします。 Intune で既定のアクセス レベルの設定を構成、 **、オンプレミスの Exchange**ページ**Exchange ActiveSync の高度なアクセス設定**。 詳細については、次を参照してください。[構成 Exchange オンプレミス アクセス](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access)します。
- 両方のコネクタに同じ構成を使用します。 構成した最後のコネクタにより、他のコネクタによって以前に書き込まれた ActiveSync の組織設定が上書きされます。 コネクタを異なる方法で構成すると、予期しない条件付きアクセスの変更が発生する可能性があります。
- ユーザーが Intune スタンドアロンに移行されたら、Configuration Manager での条件付きアクセスの対象からそれらのユーザーを削除します。

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Microsoft Intune Certificate Connector の構成
NDES を使用して SCEP を使用する証明書を発行する場合は、Microsoft Intune Certificate Connector を構成する必要があります。 Intune で NDES コネクタをホストするコンピューターは、Configuration Manager で NDES コネクタをホストする同じコンピューターにすることはできません。 詳細については、次を参照してください。[構成し、Intune で SCEP 証明書を管理](https://docs.microsoft.com/intune/certificates-scep-configure)します。 

> [!Important]    
> コネクタを構成した後、新しいサーバーの URL を参照するインポートした SCEP プロファイルを変更します。

## <a name="next-step"></a>次のステップ
移行のために Intune を準備した後は、一連のテスト ユーザーを Intune スタンドアロンに移行する準備ができました。 詳細については、次を参照してください。[特定のユーザー (混在機関) の MDM 機関を変更](migrate-mixed-authority.md)します。


