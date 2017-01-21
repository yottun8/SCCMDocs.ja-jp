---
title: "Intune スタンドアロンまたはハイブリッド MDM の選択 | Microsoft Docs"
description: "Intune と Configuration Manager を使用してハイブリッド モバイル デバイス管理を展開するか、Intune スタンドアロンを実行するかを選択します。"
ms.custom: na
ms.date: 11/07/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a5c9e312641d91ff297fbcfa6066a93c2a0e1ee0
ms.openlocfilehash: 3480484a96e96a191b4f02208fcf838db5cb6ba7

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Microsoft Intune スタンドアロンか System Center Configuration Manager を使用するハイブリッド モバイル デバイス管理を選択する

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Intune によるモバイル デバイス管理 (MDM) について最もよく寄せられる質問の 1 つは、"Intune と Configuration Manager を統合するべきか (ハイブリッド MDM)、クラウドのみの構成で Intune スタンドアロンを実行すべきか" というものです。 その答えを見つけるためには、2 つの選択肢を注意深く比較してください。また、2017 年の早い段階で導入される Intune スタンドアロンの更新プログラムを考慮してください。

## <a name="what-is-intune-standalone"></a>Intune スタンドアロンとは何ですか。

Intune スタンドアロンはクラウドのみの MDM ソリューションであり、オンプレミス リソースは関係しません。世界中のどこからでもアクセスできる Web コンソールで管理されます。 Intune データセンターは、北米、ヨーロッパ、アジアでホストされています。 Intune はクラウド サービスであるため、比較的短期間でデバイスに Intune 管理を展開できます。 組織がクラウドに移行する場合、Intune スタンドアロンも選択できます。

## <a name="what-is-hybrid-mdm-with-configuration-manager"></a>Configuration Manager とのハイブリッド MDM とは何ですか。

ハイブリッド MDM は、ポリシー、プロファイル、アプリケーションをデバイスに配信するためのチャンネルとして Intune を利用し、コンテンツを保存し、管理し、デバイスを管理するためにオンプレミス インフラストラクチャで Configuration Manager を使用するソリューションです。 Configuration Manager に既に大きな投資を行っており、それを拡大し、モバイル デバイスを管理する場合、ハイブリッド MDM を選択できます。 ハイブリッドを導入すると、“1 枚のガラス窓” から制御できます。つまり、同じオンプレミス インフラストラクチャと管理コンソールを利用して Intune でモバイル デバイスを管理し、従来の Configuration Manager クライアントで PC やサーバーを管理できます。

## <a name="whats-coming-to-intune-standalone-in-early-2017"></a>2017 年の早い段階で予定されている Intune スタンドアロンの更新

スタンドアロンとハイブリッドのいずれかを選択するとき、2017 年の早い段階で予定されている Intune スタンドアロンの新機能を考慮してください。 現在、ハイブリッド MDM には、一部のお客様が Intune スタンドアロンではなく、ハイブリッド MDM でデバイスを管理することを選択した理由となってきた高度な機能があります。

-   プログラムによるアクセス (API) – SDK と PowerShell の管理オプション。

-   カスタム レポート – レポートをカスタマイズして作成します。

-   ロール ベースのアクセス制御 – 割り当てられた役割に基づき、管理機能へのアクセスを制限します。

-   規模 – 50,000 台以上のモバイル デバイスを展開し、管理します。

-   1 枚のガラス窓 – 同じコンソールを利用し、従来の PC クライアントと Intune 管理デバイスの両方を管理します。

Intune 展開の計画を開始するとき、試作、受け入れテスト、展開のために数か月の期間が確保されているのであれば、これからクラウド サービスに新しい機能が追加されることを考慮し、Intune スタンドアロンを選択するのも良い考えです。 2017 年の前半を通して、Intune スタンドアロンに更新プログラムが与えられます。そのプログラムで、Configuration Manager とのハイブリッド展開を構成する高度な機能の多くが提供されます。 Intune スタンドアロンは間もなく Microsoft Azure クラウド プラットフォームに移行します。拡張性が強化され、Azure Portal によるロール ベースのアクセス、カスタム レポート、Azure Graph API によるプログラミング アクセスといった機能が与えられます。

ハイブリッドから Intune スタンドアロンに切り替えたり、スタンドアロンからハイブリッドに切り替えたりできますが、Microsoft のサポートと操作ヘルプが必要になります。 また、管理権限の変更後、あらゆるデバイスの登録を解除し、再登録する必要があります。  Microsoft は、今後のサービス更新で、更新切り替え機能の改善に取り組みます。



<!--HONumber=Dec16_HO3-->


