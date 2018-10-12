---
title: Windows Analytics でクライアントを監視する
titleSuffix: Configuration Manager
description: Windows Analytics は、環境の現在の状態に関する有益な分析情報が得られるソリューションのセットです。
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8405a212f9e4cd845ac7591767eb27e5425f404e
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893653"
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Configuration Manager で Windows Analytics を使用する

*適用対象: System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://docs.microsoft.com/windows/deployment/update/windows-analytics-overview) は、環境の現在の状態に関する有益な分析情報が得られるソリューションのセットです。 環境内の Windows デバイスによって Microsoft に報告されたデータに、ソリューションからアクセスして分析できます。 たとえば、[Upgrade Readiness](/sccm/core/clients/manage/upgrade-readiness) を Configuration Manager と接続することで、Configuration Manager コンソールの**監視**ワークスペースでデータに直接アクセスすることができます。

Windows Analytics によって使用されるデータは、Configuration Manager サイト サーバーに直接転送されることはありません。 クライアント コンピューターは、Windows クラウド サービスにデータを送信します。 その後、このサービスにより関連するデータが、組織のワークスペースのいずれかでホストされている Windows Analytics ソリューションに転送されます。 その後 Configuration Manager は、コンテキスト内リンクで Web ポータル内の関連データにユーザーを誘導します。 Configuration Manager に接続するソリューションの一部であるデータを直接表示することもできます。

> [!Important]  
> Configuration Manager では、診断と使用状況のデータが Microsoft に報告されます。 このデータは、Windows Analytics のデータとは別のものです。 詳細については、「[診断結果と使用状況データ](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)」を参照してください。  



## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Windows Analytics にデータをレポートするようにクライアントを構成する

クライアント デバイスが Windows Analytics にデータを報告するには、"*商用 ID キー*" でデバイスを構成します。 このキーは、Windows Analytics のデータをホストする Azure Log Analytics ワークスペースです。 また、使用する特定のソリューションに適したレベルでデータをレポートするようにデバイスを構成します。 

### <a name="configure-windows-analytics-client-settings"></a>Windows Analytics クライアント設定の構成
Windows Analytics を構成するには: 
1. Configuration Manager コンソールで、**[管理]** ワークスペースに移動して、**[クライアント設定]** ノードを選択します。  
2. リボンで **[カスタム クライアント デバイス設定の作成]** を選択します。  
3. **Windows Analytics** グループをこのカスタム デバイス クライアント設定ポリシーに追加します。  

カスタム デバイス クライアント設定の作成方法について詳しくは、「[クライアント設定を構成する方法](/sccm/core/clients/deploy/configure-client-settings)」をご覧ください。

**[Windows Analytics]** 設定タブを選択し、次の設定を構成します。  

#### <a name="manage-windows-telemetry-settings-with-configuration-manager"></a>Configuration Manager を使用して、Windows テレメトリ設定を管理します
Windows クライアントで Windows 診断データの設定を構成するには、この設定を **[はい]** に構成します。   

#### <a name="commercial-id-key"></a>商用 ID キー
商用 ID キーは、管理するデバイスから組織の Windows Analytics データをホストする Log Analytics ワークスペースに情報をマップします。 使用する商用 ID キーを Upgrade Readiness で既に構成している場合は、その ID を使用します。 まだ商用 ID キーがない場合は、「[Copy your commercial ID key](https://docs.microsoft.com/windows/deployment/update/windows-analytics-get-started#copy-your-commercial-id-key)」(商用 ID キーをコピーする) をご覧ください。

#### <a name="windows-10-telemetry"></a>Windows 10 テレメトリ
詳しくは、「[組織内の Windows 診断データの構成](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization##diagnostic-data-level)」をご覧ください。

> [!Note]  
> Windows 10 データ コレクション レベルを **[拡張 (制限あり)]** に設定することもできます。 この設定を行うと、デバイスから **[拡張]** レベルのデータのすべてを報告されなくても、Windows 10 バージョン 1709 以降で、ご利用の環境のデバイスに関する、アクションにつながる有用な情報を得ることができます。 [拡張 (制限あり)] レベルには、基本レベルから収集されたメトリックとともに、Windows Analytics に関連する [拡張] レベルから収集されたデータのサブセットも含まれます。

#### <a name="windows-81-and-earlier-telemetry"></a>Windows 8.1 以前のテレメトリ   
詳細については、[Windows 7、Windows 8、Windows 8.1 の利用統計情報のイベントとフィールドに関するドキュメント (PDF ファイル)](https://go.microsoft.com/fwlink/?LinkID=822965) を参照してください。

#### <a name="enable-windows-81-and-earlier-internet-explorer-data-collection"></a>Windows 8.1 以前の Internet Explorer データ コレクションを有効化
Windows 8.1 以前を実行しているデバイスでは、Internet Explorer で Web アプリに関するデータを収集できます。 このデータによって、Upgrade Readiness は、Windows 10 へのスムーズなアップグレードが妨げられる可能性のある Web アプリケーションの非互換性を検出できます。 インターネット ゾーンに基づく Internet Explorer のデータ収集を有効にします。 インターネット ゾーンの詳細については、「[About URL Security Zones (セキュリティ ゾーンについて)](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537183\(v=vs.85\))」をご覧ください。



## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Upgrade Readiness を使用して Windows 10 の互換性の問題を特定する

Upgrade Readiness を使用すると、デバイスの準備と Windows 10 との互換性を分析できます。 この評価ではスムーズなアップグレードが可能です。 Configuration Manager と Upgrade Readiness を接続すると、Configuration Manager コンソールからこのクライアントのアップグレードの互換性データに直接アクセスできます。 その後、デバイス リストからアップグレードまたは修復対象のデバイスを指定できます。

Upgrade Readiness を構成および接続する方法の詳細については、[Upgrade Readiness](/sccm/core/clients/manage/upgrade-readiness)に関するページを参照してください。



## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Windows Analytics を使用して Windows 情報保護ポリシー内のギャップを識別する

[Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) ポリシーで Windows 10 バージョン 1703 以降のデバイスを構成できます。 これにより、環境内の会社データにアクセスしているのにポリシー適用規則に含まれないアプリケーションについての診断データが報告されます。 ユーザーがこれらのアプリケーションの生産性を維持する必要があっても、WIP によってユーザーのアクセスがブロックされます。 この情報は、Configuration Manager において Windows Information Protection ポリシーを維持するのに役立ちます。 

