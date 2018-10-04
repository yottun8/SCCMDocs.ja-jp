---
title: Intune スタンドアロンまたはハイブリッド MDM の選択
titleSuffix: Configuration Manager
description: Intune と Configuration Manager を使用してハイブリッド モバイル デバイス管理を展開するか、Intune スタンドアロンを実行するかを選択します。
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 153c1208cef8a940cc06412322e8112d53d17e58
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584415"
---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mdm-with-configuration-manager"></a>Microsoft Intune スタンドアロンまたは Configuration Manager とのハイブリッド MDM を選択する

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Intune によるモバイル デバイス管理 (MDM) について最もよく寄せられる質問の 1 つは、"Intune と Configuration Manager を統合するべきか (ハイブリッド MDM)、クラウドのみの構成で Intune スタンドアロンを実行すべきか" というものです。 

Azure 上の Intune は、Microsoft が推奨する MDM ソリューションです。     


> [!Important]  
> 2018 年 8 月 14 日の時点では、ハイブリッド モバイル デバイス管理は[非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)です。 詳細については、[ハイブリッド MDM の概要](/sccm/mdm/understand/hybrid-mobile-device-management)に関するページを参照してください。<!--Intune feature 2683117-->  


 
## <a name="intune-standalone"></a>Intune スタンドアロン

Intune スタンドアロンは、Microsoft が推奨する展開トポロジです。 Intune スタンドアロンはクラウドのみの MDM ソリューションであり、世界中のどこからでもアクセスできる Web コンソールを使用して管理します。 Intune のデータ センターは、北米、ヨーロッパ、アジアでホストされています。 Intune はクラウド サービスであるため、すばやくデバイスに Intune 管理を展開できます。

オンプロミスのコンポーネントへの依存関係がないため、スタンドアロン トポロジの方が早く簡単に展開できると感じるお客様は多くおられます。 現在、Intune スタンドアロンは Microsoft Azure クラウド プラットフォームに移行し、次のような高度な機能を数多く提供しています。  

- 統合エンタープライズ モビリティ管理プラットフォーム: Intune、Azure AD Premium、Azure Information Protection 向けの Azure portal での統合されたクラウド プラットフォームおよび管理者エクスペリエンスです  

- モバイル デバイス管理: モバイル デバイスの豊富な管理機能および情報保護機能です  

- スケーリング: スケーリングの心配をすることなく、モバイル デバイスの展開および管理が可能です  

- ロール ベースのアクセス制御: 割り当てられた役割やスコープに基づき、管理機能へのアクセスを制限します  

- プログラムによるアクセス (API): Microsoft Graph API サポート、および SDK と PowerShell の管理オプションです  

- Web コンソール: 最新の Web ブラウザーに対応した、Web 標準を基盤とする HTML 5 ベースのコンソールです  

- 高度なレポート機能: カスタマイズされたレポートを作成する機能です  

- 機敏性: 新しい機能を簡単にセットアップし、迅速に配信できます  



## <a name="hybrid-mdm-with-configuration-manager"></a>Configuration Manager とのハイブリッド MDM

> [!Important]  
> 2018 年 8 月 14 日の時点では、ハイブリッド モバイル デバイス管理は[非推奨の機能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)です。 詳細については、[ハイブリッド MDM の概要](/sccm/mdm/understand/hybrid-mobile-device-management)に関するページを参照してください。  

ハイブリッド MDM は、Intune のモバイル デバイス管理機能を Configuration Manager に統合するソリューションです。 ポリシー、プロファイル、アプリケーションをデバイスに配信するためのチャネルとして Intune を利用し、Configuration Manager のオンプレミス インフラストラクチャを使用してコンテンツとデバイスを管理します。 ハイブリッドを導入すると、"1 枚のガラス窓" から制御できます。 これはつまり、同じオンプレミス インフラストラクチャと管理コンソールを利用して、Intune でモバイル デバイスを管理しつつ、従来の Configuration Manager クライアントで PC やサーバーを管理できるということです。 

ハイブリッド MDM を選択する理由には、次のようなものが挙げられます。  

- Intune に登録されているモバイル デバイスと、Configuration Manager クライアントで管理しているデバイスの両方を、同じ管理コンソールから管理したい  

- ご利用のインフラストラクチャで、モバイル デバイスへの証明書の配信に複数の NDES サーバーが必要  

- ご利用のインフラストラクチャで、複数の Exchange コネクタが必要  

- S/MIME 暗号化サポートが必要

> [!Note]  
> オンプレミスの Exchange による条件付きアクセスのために Configuration Manager でハイブリッド MDM を設定した場合でも、ユーザーは Outlook for iOS 用および Outlook for Android でメールにアクセスできます。 Intune スタンドアロンでこれと同じように構成すると、メールはこれらのクライアントに対してブロックされます。<!--Intune bug 2285890-->  



## <a name="change-the-mdm-authority"></a>MDM 機関を変更する

MDM 機関の設定を変更する必要がある場合は、Microsoft サポートに連絡しなくても、また、既存のマネージド デバイスの登録を解除して再登録しなくても、お客様自身で変更できます。 詳細については、「[Change your MDM authority](/sccm/mdm/deploy-use/change-mdm-authority)」(MDM 機関を変更する) を参照してください。

