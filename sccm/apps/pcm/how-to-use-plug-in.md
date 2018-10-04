---
title: 変換プラグインを使用する方法
titleSuffix: Configuration Manager
description: 分析プロセスと変換プロセスをカスタマイズするには、パッケージ変換マネージャー プラグインを使用します。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 9e670cb6afd7186d7dc248bedd6e2ce7d7746b02
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297196"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>パッケージ変換マネージャー プラグインの使用方法

*適用対象: System Center Configuration Manager (Current Branch)*

<!--1357861-->

パッケージ変換マネージャー プラグインは、分析プロセスと変換プロセスのカスタマイズに役立ちます。 パッケージ変換マネージャー プラグインを使用するには、カスタム操作を実行する実行可能ファイルまたはスクリプト ファイルを記述します。 次に、構成ファイルである Microsoft.ConfigurationManagement.exe.config を編集して実行可能ファイルまたはスクリプトを呼び出します。 スクリプトを書くのに使われる最も一般的な言語は、VBScript または PowerShell です。

パッケージ変換マネージャー プラグインは、パッケージごとに 1 回実行します。 一度に複数のパッケージを分析または変換する場合は、パッケージ変換マネージャー プラグインを毎回実行します。

> [!NOTE]  
> Configuration Manager 構成ファイル内のパッケージ変換マネージャーの要素について詳しくは、「[Technical reference for the Package Conversion Manager plug-in configuration XML](/sccm/apps/pcm/plugin-config-xml)」(パッケージ変換マネージャー プラグイン構成 XML のテクニカル リファレンス) をご覧ください。



## <a name="default-process"></a>既定のプロセス

既定では、パッケージ変換マネージャーは次のアクションを行います。

1.  Configuration Manager パッケージを読み取ります。  

2.  パッケージからアプリケーションを作成して、既定の属性を追加します。  

3.  アプリケーションを分析して、パッケージの準備状態を判断します。  

4.  パッケージ変換マネージャーの操作に応じて、次のいずれかのアクションを実行します。  

    - **分析**: Configuration Manager コンソールにパッケージの準備状態を表示します。  

    - **変換**: Configuration Manager データベースにアプリケーションを書き込みます。  


## <a name="plug-in-based-process"></a>プラグイン ベースのプロセス 

プラグインを使用する場合、パッケージ変換マネージャーは次のアクションを行います。

1.  Configuration Manager パッケージを読み取ります。  

2.  パッケージからアプリケーションを作成して、既定の属性を追加します。  

3.  アプリケーションを XML に変換します。 次に、ファイルをディスクに保存します。  

4.  プラグイン スクリプトを実行してアプリケーション XML を変更します。 詳しくは、「[Technical reference for the Package Conversion Manager plug-in configuration XML](/sccm/apps/pcm/plugin-config-xml)」(パッケージ変換マネージャー プラグイン構成 XML のテクニカル リファレンス) をご覧ください。  

5.  アプリケーション XML を Configuration Manager アプリケーションに変換します。  

6.  アプリケーションを分析して、パッケージの準備状態を判断します。  

7.  パッケージ変換マネージャーの操作に応じて、次のいずれかのアクションを実行します。  

    - **分析**: Configuration Manager コンソールにパッケージの準備状態を表示します。  

    - **変換**: Configuration Manager データベースにアプリケーションを書き込みます。  



## <a name="see-also"></a>関連項目

[Technical reference for the Package Conversion Manager plug-in configuration XML](/sccm/apps/pcm/plugin-config-xml) (パッケージ変換マネージャー プラグイン構成 XML のテクニカル リファレンス)
