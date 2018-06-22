---
title: Microsoft Edge の設定の構成
titleSuffix: Configuration Manager
description: Windows 10 クライアントで Microsoft Edge Web ブラウザーの設定を構成する
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/28/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 81bd0a59a24cab446668911f714548581c1347df
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32343798"
---
# <a name="configure-microsoft-edge-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager で Microsoft Edge 設定を構成する

*適用対象: System Center Configuration Manager (Current Branch)*

<!-- 1357310 -->
バージョン 1802 以降、Windows 10 クライアントで [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) Web ブラウザーを使用する場合、Configuration Manager のコンプライアンス設定ポリシーを作成し、Microsoft Edge の一部の設定を構成します。 

このポリシーは、Windows 10 バージョン 1703 以降のクライアントにのみ適用されます。 <!--511552-->


## <a name="policy-settings"></a>ポリシー設定
現在、このポリシーには次の設定が含まれます。
- **[Set Microsoft Edge browser as default]\(Microsoft Edge ブラウザーを既定として設定する\)**: Windows 10 既定アプリの設定で、Web ブラウザーを Microsoft Edge に構成します
- **[アドレス バーのドロップダウンを許可する]**: Windows 10 バージョン 1703 以降が必要です。 詳細については、[AllowAddressBarDropdown ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)に関する説明を参照してください。
- **[Microsoft のブラウザー間でお気に入りの同期を許可する]**: Windows 10 バージョン 1703 以降が必要です。 詳細については、[SyncFavoritesBetweenIEAndMicrosoftEdge ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)に関する説明を参照してください。
- **[終了時に閲覧データをクリアすることを許可する]**: Windows 10 バージョン 1703 以降が必要です。 詳細については、[ClearBrowsingDataOnExit ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)に関する説明を参照してください。
- **[トラッキング拒否ヘッダーを許可する]**: 詳細については、[AllowDoNotTrack ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)に関する説明を参照してください。
- **[オートフィルを許可する]**: 詳細については、[AllowAutofill ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)に関する説明を参照してください。
- **[Cookie を許可する]**: 詳細については、[AllowCookies ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)に関する説明を参照してください。
- **[ポップアップ ブロックを許可する]**: 詳細については、[AllowPopups ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)に関する説明を参照してください。
- **[アドレス バーで検索候補を許可する]**: 詳細については、[AllowSearchSuggestionsinAddressBar ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)に関する説明を参照してください。
- **[Internet Explorer へのイントラネット トラフィックの送信を許可する]**: 詳細については、[SendIntranetTraffictoInternetExplorer ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)に関する説明を参照してください。
- **[Password Manager を許可する]**: 詳細については、[AllowPasswordManager ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)に関する説明を参照してください。
- **[開発者ツールを許可する]**: 詳細については、[AllowDeveloperTools ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)に関する説明を参照してください。
- **[拡張機能を許可する]**: 詳細については、[AllowExtensions ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)に関する説明を参照してください。



## <a name="create-the-microsoft-edge-browser-profile"></a>Microsoft Edge ブラウザー プロファイルを作成する

1. Configuration Manager コンソールで、**[資産とコンプライアンス]** ワークスペースに移動します。 **[コンプライアンス設定]** を展開し、新しい **[Microsoft Edge ブラウザーのプロファイル]** ノードを選びます。 リボンの **[Microsoft Edge ブラウザー ポリシーの作成]** オプションをクリックします。
2. ポリシーの **[名前]** を指定し、必要に応じて **[説明]** を入力してから、**[次へ]** をクリックします。
3. **[設定]** ページで、このポリシーに含める設定の値を **[構成済み]** に変更して、**[次へ]** をクリックします。
4. **[サポートされているプラットフォーム]** ページで、このポリシーを適用するオペレーティング システムのバージョンとアーキテクチャを選び、**[次へ]** をクリックします。 
5. ウィザードを完了します。



## <a name="deploy-the-policy"></a>ポリシーを展開する

1. ポリシーを選び、リボンのオプション **[展開]** をクリックします。
2. **[参照]** をクリックして、ポリシーを展開するユーザー コレクションまたはデバイス コレクションを選びます。 
3. 必要に応じて、追加のオプションを選びます。 
    a. ポリシーに準拠していない場合は、アラートを生成します。 
    b. クライアントがこのポリシーについてデバイスのコンプライアンスを評価するスケジュールを設定します。
4. **[OK]** をクリックして展開を作成します。



## <a name="next-steps"></a>次のステップ

他のコンプライアンス設定ポリシーと同様に、クライアントは指定されたスケジュールで設定を修復します。 Configuration Manager コンソールで、[デバイスのコンプライアンス対応を監視およびレポート](/sccm/compliance/deploy-use/monitor-compliance-settings)します。
