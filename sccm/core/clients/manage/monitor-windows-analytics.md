---
title: Windows Analytics でクライアントを監視する
titleSuffix: Configuration Manager
description: Windows Analytics は、Operations Management Suite 上で実行するソリューションのセットで、環境内のデバイスによってレポートされる Windows 利用統計情報を利用して、環境の現在の状態に有益な洞察を導くことができます。
ms.custom: na
ms.date: 01/02/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: 23
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 15b1d07f35f774f3ec8f082a86c90ecb989a438e
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2018
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Configuration Manager で Windows Analytics を使用する

*適用対象: System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) は、[Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview) (OMS) 上で実行するソリューションのセットです。 これらのソリューションにより、環境の現在の状態に関する分析情報を得ることができます。 環境内のデバイスから Windows のテレメトリ データがレポートされます。[Operations Management Suite の Web ポータル](https://mms.microsoft.com)のソリューションを通して、このデータにアクセスし、分析できます。 [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) を Configuration Manager と接続することで、Configuration Manager コンソールの**監視**ノードでデータに直接アクセスすることができます。

Windows Analytics によって使用される Windows 利用統計情報は、Configuration Manager サイト サーバーに直接転送されることはありません。 クライアント コンピューターは、Windows 利用統計情報を Windows 利用統計情報のサービスに送信します。 その後、このサービスにより関連するデータが、組織の OMS ワークスペースのいずれかでホストされている Windows Analytics ソリューションに転送されます。 Configuration Manager では、コンテキスト内リンクを持つ Web ポータルの関連するデータにユーザーを誘導したり、Configuration Manager に接続しているソリューションの一部であるデータを直接表示したりできます。 また、Operation Management Suite の Web ポータルからデータを直接クエリすることもできます。

>[!Important]
>Configuration Manager サイト サーバーから Microsoft にレポートされる、[Configuration Manager の診断と利用状況データ](../../plan-design/diagnostics/diagnostics-and-usage-data.md)は、Windows Analytics と Windows 利用統計情報とは区別されています。

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Windows Analytics にデータをレポートするようにクライアントを構成する

クライアント デバイスで Windows Analytics にデータをレポートするには、Windows Analytics データをホストする OMS ワークスペースに関連付けられた商用 ID キーでデバイスを構成する必要があります。 また、使用する特定のソリューションに適切な利用統計情報のレベルで、利用統計情報をレポートするようにデバイスを構成する必要もあります。 

### <a name="configure-windows-analytics-client-settings"></a>Windows Analytics クライアント設定の構成
Windows Analytics を構成するには、Configuration Manager コンソールで、**[管理]** > **[クライアント設定]** を選択し、**[Create Custom Device Client Settings]\(カスタム デバイス クライアント設定の作成\)** をダブルクリックして、**[Windows Analytics]** を選択します。  

**[Windows Analytics]** 設定タブに移動した後に、次の設定を構成します。
  -  **商用 ID キー**  
商用 ID キーは、管理するデバイスから組織の Windows Analytics データをホストする OMS ワークスペースに情報をマップします。 使用する商用 ID キーを Upgrade Readiness で既に構成している場合は、その ID を使用します。 まだ商用 ID キーがない場合は、「[Generate your commercial ID key (商用 ID キーを生成する)]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key)」をご覧ください。

  -  **Windows 10 デバイスの利用統計情報のレベル**   
Windows 10 の利用統計情報の各レベルに関する情報については、「[組織内の Windows 利用統計情報の構成](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels)」をご覧ください。

   > [!Note]
   > 1710 更新プログラムでは、Windows 10 テレメトリ データ コレクション レベルを **[拡張 (制限あり)]** に設定できます。 この設定を行うと、デバイスから **[拡張]** テレメトリ レベルのデータのすべてを報告されなくても、Windows 10 バージョン 1709 以降で、ご利用の環境のデバイスに関する、アクションにつながる有用な情報を得ることができます。 [拡張 (制限あり)] テレメトリ レベルには、基本レベルから収集されたメトリックとともに、Windows Analytics に関連する [拡張] レベルから収集されたデータのサブセットも含まれます。


  -  **Windows 7、8、8.1 デバイスでの商用データ収集のオプトイン**   
詳細については、[Windows 7、Windows 8、Windows 8.1 の利用統計情報のイベントとフィールドに関するドキュメント (PDF ファイル)](https://go.microsoft.com/fwlink/?LinkID=822965) を参照してください。

  -  **インターネット エクスプ ローラーのデータ収集を構成する**  
Windows 8.1 以前のバージョンが動作しているデバイスでは、Internet Explorer で収集されるデータによって、Upgrade Readiness が Web アプリケーションの非互換性を検出できるため、Windows 10 へのスムーズなアップグレードが妨げられる可能性が排除されます。 Internet Explorer のデータ収集は、インターネット ゾーンごとに有効にできます。 インターネット ゾーンの詳細については、「[About URL Security Zones (セキュリティ ゾーンについて)](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx)」をご覧ください。

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Upgrade Readiness を使用して Windows 10 の互換性の問題を特定する

Upgrade Readiness (旧称 Upgrade Analytics) を使用すると、デバイスの準備と Windows 10 との互換性を分析できます。 この評価ではスムーズなアップグレードが可能です。 Configuration Manager と Upgrade Readiness を接続すると、Configuration Manager コンソールからこのクライアントのアップグレードの互換性データに直接アクセスできます。 その後、デバイス リストからアップグレードまたは修復対象のデバイスを指定できます。

Upgrade Readiness を構成および接続する方法の詳細については、[Upgrade Readiness](../../clients/manage/upgrade/upgrade-analytics.md)に関するページを参照してください。

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Windows Analytics を使用して Windows 情報保護ポリシー内のギャップを識別する

[Windows 情報保護](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) ポリシーで構成される Windows 10 バージョン 1703 以降のデバイスは、環境内の会社のデータにはアクセスするが、WIP ポリシー アプリケーション規則に含まれないアプリケーションの利用統計情報をレポートします。 ユーザーがこれらのアプリケーションの生産性を維持する必要があっても、WIP によってユーザーのアクセスがブロックされます。 ユーザーが会社のデータにアクセスしていることを知ることは、Configuration Manager での Windows 情報保護ポリシーのメンテナンスに役立ちます。 

この Windows 情報保護データには、この [Operations Management Suite クエリ](https://go.microsoft.com/fwlink/?linkid=849952)を使用してアクセスします。