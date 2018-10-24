---
title: CMG についてよくあるご質問
description: この記事を使用して、クラウド管理ゲートウェイについてよくあるご質問に回答します。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 16cb80efe5ad082d8624452c01dcd54a5eca27f2
ms.sourcegitcommit: 2badee2b63ae63687795250e298f463474063100
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2018
ms.locfileid: "45600941"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>クラウド管理ゲートウェイについてよくあるご質問

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、クラウド管理ゲートウェイについてよくあるご質問に回答します。 詳細については、「[クラウド管理ゲートウェイの計画](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)」を参照してください。


## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="what-certificates-do-i-need"></a>どの証明書が必要ですか?

詳細については、「[クラウド管理ゲートウェイの証明書](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)」を参照してください。


### <a name="do-i-need-azure-expressroute"></a>Azure ExpressRoute は必要ですか?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) では、Microsoft クラウドにオンプレミス ネットワークを拡張することができます。 Configuration Manager クラウド管理ゲートウェイでは、ExpressRoute などの仮想ネットワーク接続は必要ありません。 クラウド管理ゲートウェイの設計では、インターネット ベースのクライアントは、Azure サービス経由でオンプレミス サイト システムと通信を行うことができます。追加のネットワーク構成は必要ありません。 詳細については、「[クラウド管理ゲートウェイの計画](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)」を参照してください。

組織で ExpressRoute を使用する場合、セキュリティのベスト プラクティスはクラウド管理ゲートウェイの Azure サブスクリプションを分離することです。 この構成により、クラウド管理ゲートウェイ サービスがこの方法で誤って接続されることがなくなります。 詳細については、「[Security and privacy for cloud management gateway](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)」(クラウド管理ゲートウェイのセキュリティとプライバシー) を参照してください。


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Azure 仮想マシンを維持する必要がありますか?

維持する必要はありません。 クラウド管理ゲートウェイの設計では、PaaS (サービスとしてのプラットフォーム) として Azure が使用されます。 指定されたサブスクリプションを使用して、Configuration Manager では必要な仮想マシン (VM)、ストレージ、ネットワークを作成します。 Azure は仮想マシンをセキュリティで保護し、更新します。 IaaS (サービスとしてのインフラストラクチャ) と同様に、これらの VM はオンプレミス環境には含まれません。 クラウド管理ゲートウェイは、クラウドに Configuration Manager 環境を拡張する PaaS です。 


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>既に IBCM を使用しています。 CMG を追加した場合、クライアントはどのように動作しますか?

[インターネット ベースのクライアント管理](/sccm/core/clients/manage/plan-internet-based-client-management) (IBCM) を既に展開している場合は、クラウド管理ゲートウェイを展開することもできます。 クライアントは両方のサービスのポリシーを受け取ります。 インターネットへのローミング時に、これらのインターネット ベースのサービスのいずれかをランダムに選択して使用します。


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-subscription-as-the-subscription-that-hosts-the-cmg-cloud-service"></a>ユーザー アカウントは、CMG クラウド サービスをホストするサブスクリプションと同じ Azure サブスクリプションにある必要がありますか。
<!--SCCMDocs-pr issue #2873--> 環境内に複数のサブスクリプションがある場合は、Azure クラウド サービスをホストできる任意のサブスクリプションに CMG をデプロイできます。 

この質問は、次のシナリオで共通です。  

- 個別のテストおよび実稼働の Active Directory と Azure AD 環境はあるが、集中管理の Azure ホスティング サブスクリプションが 1 つしかない  

- Azure の使用がさまざまなチームにわたって有機的に増加している  

Resource Manager デプロイを使用しているときに、関連付けられている Azure AD テナントをオンボードします。 この接続により、Configuration Manager が Azure への認証を行い、CMG の作成、デプロイ、管理ができるようになります。  

CMG 経由で管理されているユーザーとデバイスに対して Azure AD Authentication を使用している場合は、その Azure AD テナントをオンボードします。 クラウド管理用の Azure サービスの詳細については、[Azure サービスの構成](/sccm/core/servers/deploy/configure/azure-services-wizard)に関するページを参照してください。 各 Azure AD テナントをオンボードすると、ホスティング場所に関係なく、1 つの CMG で Azure AD Authentication を複数のテナントに提供することができます。



## <a name="next-steps"></a>次のステップ

- [クラウド管理ゲートウェイの計画](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Set up cloud management gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway) (クラウド管理ゲートウェイの設定)
- [クラウド管理ゲートウェイの証明書](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [クラウド管理ゲートウェイのセキュリティとプライバシー](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [クラウド管理ゲートウェイのサイズとスケールの数値](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)