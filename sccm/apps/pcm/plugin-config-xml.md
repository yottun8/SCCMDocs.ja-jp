---
title: プラグイン構成 XML
titleSuffix: Configuration Manager
description: Package Conversion Manager プラグインの XML 要素のテクニカル リファレンス。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 8fda0e2cc2d820904e1fb9ec893c4453fe26bfc2
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897444"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Package Conversion Manager プラグイン構成 XML のテクニカル リファレンス

「オブジェクトの*適用対象: System Center Configuration Manager (Current Branch)*

<!--1357861-->

この記事では、Package Conversion Manager プラグインの動作を制御する Configuration Manager 構成ファイル (Microsoft.ConfigurationManagement.exe.config) の XML 要素について説明します。 このプラグインの使用方法の詳細については、「[Package Conversion Manager プラグインの使用方法](/sccm/apps/pcm/how-to-use-plug-in)」を参照してください。



## <a name="xml-configuration-elements"></a>XML 構成要素

次の表は、Package Conversion Manager プラグインに関する Configuration Manager 構成ファイルの XML 要素を示します。

|要素  |「  |[説明]  |
|---------|---------|---------|
|**PcmPlugIn**|文字列型|Package Conversion Manager プラグインとして使用するスクリプトまたは実行可能ファイルの名前。|
|**PcmPlugInTimeoutMilliseconds**|整数型|Package Conversion Manager プラグインのスクリプトまたは実行可能ファイルがパッケージの処理を完了するのを待つ最大の時間 (ミリ秒単位)。|
|**PcmPluginExitCode**|整数型|プラグインのプロセスからの予想される終了コード。 この値は成功を示します。 その他のコードはエラーとみなされます。|
|**ForceRequirementsExtraction**|ブール型|パッケージに関連付けられているコレクション要件を自動変換で使用可能にします。 どの要求を使用するかを判断するように設計されている Package Conversion Manager プラグインを使用するときには、「True」に設定されている必要があります。|



## <a name="sample-configuration-xml"></a>サンプルの構成 XML

このセクションでは、Configuration Manager 構成ファイル、**Microsoft.ConfigurationManagement.exe.config** 内にある Package Conversion Manager 構成の XML 要素の例を示します。既定では、このファイルは次のパスに配置されています。  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

サンプルでは、Package Conversion Manager に関連する要素は、`Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings` 要素内にあります。

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

