---
title: 証明書テンプレートのアクセス許可の計画
titleSuffix: Configuration Manager
description: System Center Configuration Manager で使用する証明書テンプレートを構成する必要があるアクセス許可の計画について説明します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8c885920fa1e413468d09201ddaecc728ffb7b53
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135376"
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager の証明書プロファイルに関する証明書テンプレート アクセス許可の計画

*適用対象: System Center Configuration Manager (Current Branch)*


証明書プロファイルを展開する場合に、System Center Configuration Manager で使用する証明書テンプレートのアクセス許可の構成を計画するときに、次の情報を参考にしてください。  

## <a name="default-security-permissions-and-considerations"></a>既定のセキュリティ アクセス許可と考慮事項  
 ユーザーとデバイスの証明書を要求するために System Center Configuration Manager で使用する証明書テンプレートに必要な既定のセキュリティ アクセス許可は次のとおりです。  

- ネットワーク デバイス登録サービスのアプリケーション プールで使用するアカウント: 読み取りと登録  

- System Center Configuration Manager コンソールを実行するアカウント: 読み取り  

  これらのセキュリティ アクセス許可の詳細については、「[証明書インフラストラクチャ](../deploy-use/certificate-infrastructure.md)」を参照してください。  

  上記の既定の構成を使うと、ユーザーとデバイスは証明書テンプレートから直接証明書を要求することはできず、すべての要求が、必ず、ネットワーク デバイス登録サービスから発信されるようになります。 この制限は、セキュリティ上、重要なことです。というのは、これらの証明書テンプレートでは、証明書のサブジェクトを **[要求に含まれる]** に構成しなければならないので、権限のないはずのユーザーやデバイスが正規ユーザーになりすまして証明書を要求する可能性があるからです。 既定の構成では、必ず、ネットワーク デバイス登録サービスが要求を開始しなければなりません。 ただし、ネットワーク デバイス登録サービスを実行するサービスが侵害された場合、依然として、このなりすましのリスクがあります。 このリスクを回避するには、ネットワーク デバイス登録サービスおよびこの役割サービスを実行するコンピューターに対する、セキュリティ上のすべてのベスト プラクティスに従ってください。  

  既定のセキュリティ アクセス許可のままでは業務上支障がある場合は、ユーザーとコンピューターに、証明書テンプレートの読み取りと登録のアクセス許可を付与するという方法もあります。  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>ユーザーとコンピューターに証明書テンプレートの読み取りと登録アクセス許可を付与する  
 ユーザーとコンピューターに読み取りと登録アクセス許可を付与するのは、会社の証明機関 (CA) を管理しているチームが別にあり、そのチームが、ユーザー証明書要求用の証明書プロファイルがユーザーに送信される前に、そのユーザーが Active Directory Domain Services アカウントを持っていることを System Center Configuration Manager で検証したい場合に適しています。 このためには、ユーザーを含む 1 つまたは複数のセキュリティ グループを指定して、これらのグループに証明書テンプレートの読み取りと登録アクセス許可を付与する必要があります。 この場合は、CA 管理者がセキュリティを制御します。  

 同様に、コンピューター アカウントを含む 1 つまたは複数のセキュリティ グループを指定して、これらのグループに証明書テンプレートの読み取りアクセス許可と登録アクセス許可を付与できます。 ドメインに参加しているコンピューターにコンピューター証明書プロファイルを展開する場合は、このコンピューターのコンピューター アカウントに読み取りと登録アクセス許可を付与する必要があります。 ワークグループ コンピューターや個人のモバイル デバイスなど、コンピューターがドメインに参加していない場合は、これらのアクセス許可は必要ありません。  

 この構成では、セキュリティ制御が用いられていますが、ベスト プラクティスとしてお勧めできません。 というのは、指定されたユーザー、またはデバイスの所有者が、System Center Configuration Manager とは独立して証明書を要求し、別のユーザーやデバイスになりすますために証明書のサブジェクトの値を送る可能性があるからです。  

 さらに、証明書要求の発生時に認証できないアカウントを指定すると、既定で証明書認証に失敗します。 たとえば、ネットワーク デバイス登録サービスを実行しているサーバーが証明書登録ポイント サイト サーバーを含むフォレストによって信頼されていない Active Directory フォレストにある場合は、証明書要求に失敗します。 ドメイン コントローラーが応答しないためアカウントを認証できない場合に、証明書登録ポイントで処理を続行するように構成することもできますが、 これは、セキュリティ上、ベスト プラクティスとはいえません。  

 アカウントのアクセス許可を確認するように証明書登録ポイントを構成しており、ドメイン コントローラーが応答し、認証要求が拒否された場合 (アカウントがロックアウトされている、アカウントが削除されているなど)、証明書登録要求は失敗します。  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>ユーザーおよびドメインに参加しているコンピューターの読み取りと登録アクセス許可を確認するには  

1.  証明書登録ポイントをホストするサイト システム サーバーで、次の DWORD レジストリ キー値を 0 に設定して作成します。HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  ドメイン コントローラーから応答がないためアカウントを認証できない場合に、アクセス許可の確認をバイパスするには、次の操作行います。  

    -   証明書登録ポイントをホストするサイト システム サーバーで、次の DWORD レジストリ キー値を 1 に設定して作成します。HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessDenied  

3.  発行元 CA の証明書テンプレートのプロパティの **[セキュリティ]** タブで、ユーザー アカウントまたはデバイス アカウントに読み取りと登録アクセス許可を付与する 1 つまたは複数のセキュリティ グループを追加します。  
