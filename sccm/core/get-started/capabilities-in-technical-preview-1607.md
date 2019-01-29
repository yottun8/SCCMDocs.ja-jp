---
title: Technical Preview 1607 の機能
titleSuffix: Configuration Manager
description: System Center Configuration Manager の Technical Preview バージョン 1607 で使用できる機能について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: b3fb33191f8ae5a33876603e1a3d94ee2ac80860
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896568"
---
# <a name="capabilities-in-technical-preview-1607-for-system-center-configuration-manager"></a>System Center Configuration Manager の Technical Preview 1607 の機能

「オブジェクトの*適用対象: System Center Configuration Manager (Technical Preview)*

この記事では、System Center Configuration Manager の Technical Preview バージョン 1607 で使用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。      このバージョンの Technical Preview をインストールする前に、説明のトピック「[System Center Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、および Technical Preview の機能に関するフィードバックを提供する方法について理解してください。    


**このバージョンでお試しいただける新機能を次に示します。**  

## <a name="dmp_edition"></a>Windows 10 のエディションのアップグレード ポリシーの改善

このリリースでは、次の機能強化がこのポリシーに加えられています。

* Microsoft Intune に登録された Windows 10 PC に加え、Configuration Manager クライアントを実行している Windows 10 PC で、エディションのアップグレード ポリシーを使用できるようになりました。
* Windows 10 Professional から、ハードウェアと互換性がある、ウィザードのプラットフォームのいずれかにアップグレードすることができます。

[Windows 10 のエディションのアップグレード ポリシーについての詳細](/sccm/compliance/deploy-use/upgrade-windows-version)

### <a name="try-it-out"></a>試してみましょう。

1. [既存エディションのアップグレード ポリシーのトピック](/sccm/compliance/deploy-use/upgrade-windows-version)にある情報を使用して、エディションのアップグレード ポリシーを作成します。
2. このポリシーを Configuration Manager クライアントを実行している Windows 10 PC に展開します。
対象の Windows PC にポリシーが到達すると、アップグレードを適用するために PC は 2 時間以内に再起動します。 現在、この再起動を抑制することはできません。 ポリシーを展開するすべてのユーザーに通知するか、ポリシーの実行をユーザーの業務時間外にスケジュール設定します。

### <a name="known-issue-with-this-release"></a>このリリースでの既知の問題
Configuration Manager クライアントの設定で、**エディションのアップグレード**の設定が表示される場合があります。 このリリースでは、これらの設定は機能しません。 上記の手順に従って、Windows 10 を新しいバージョンにアップグレードします。

## <a name="customizable-branding-for-software-center-dialogs"></a>ソフトウェア センター ダイアログにおけるカスタマイズ可能なブランド

ソフトウェア センターのカスタム ブランド設定は、Configuration Manager バージョン 1602 で導入されました。 Technical Preview version 1607 では、ソフトウェア センターのユーザーにより一貫性のあるエクスペリエンスを提供するため、このブランド設定が関連するすべてのダイアログ ボックスとタスク バーの通知に拡張されています。

### <a name="try-it-out"></a>試してみましょう。

ソフトウェア センターのカスタム ブランド設定は、次の規則に従って適用されます。

1. アプリケーション カタログ Web サイトのポイント サイト サーバーの役割がインストールされていない場合は、**[コンピューター エージェント]** クライアント設定 **[ソフトウェア センターに表示される組織名]** に指定された組織名がソフトウェア センターに表示されます。 手順については、「[クライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)」をご覧ください。

2. アプリケーション カタログ Web サイトのポイント サイト サーバーの役割がインストールされている場合は、アプリケーション カタログ Web サイトのポイント サイト サーバーの役割プロパティに指定されている組織名と色がソフトウェア センターに表示されます。 詳細については、「[Configuration options for Application Catalog website point](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)」(アプリケーション カタログ Web サイト ポイントの構成オプション) をご覧ください。

3. Microsoft Intune サブスクリプションが構成されていて Configuration Manager 環境に接続されている場合は、Intune サブスクリプションのプロパティに指定されている組織名、色、および会社のロゴがソフトウェア センターに表示されます。 詳細については、「[Configure the Microsoft Intune subscription](/mdm/deploy-use/configure-intune-subscription)」 (Microsoft Intune サブスクリプションを構成する) をご覧ください。

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>複数の PXE による展開に同一のネットワーク アダプターを使用する
Technical Preview バージョン 1607 では、(複数のデバイスで使用する、USB イーサネット アダプターなど) イーサネット アダプターを使用して複数のデバイスのイメージを作成する際に、イーサネット アダプターにハードウェア識別子を入力できるようにする新しい設定を有効にすることができます。 Configuration Manager は、PXE インストールを実行する際やクライアントの登録で一覧のハードウェア識別子を無視します。

この問題の詳細については、[Configuration Manager OSD サポート チームのブログ](https://blogs.technet.microsoft.com/system_center_configuration_manager_operating_system_deployment_support_blog/2015/08/27/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in-system-center-configuration-manger-osd/)をご覧ください。  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>重複するハードウェア識別子を管理する機能を有効にする  
1. Configuration Manager コンソールで、**[管理]** > **[概要]** > **[Cloud Services]** > **[更新とサービス]** > **[機能]** の順に移動します。
2. 表示ウィンドウで **[重複しているハードウェア識別子の管理]** を選択します。
3. **[ホーム]** タブの **[機能]** グループで、**[有効にする]** をクリックします。

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>無視する Configuration Manager のハードウェア識別子を追加する  
1. Configuration Manager コンソールで、**[管理]** > **[概要]** > **[サイトの構成]** > **[サイト]** の順に移動します。
2. **[ホーム]** タブの **[サイト]** グループで、 **[階層設定]** をクリックします。
3. **[クライアントの承認と競合レコードの処理]** タブに移動します。
4. **[重複するハードウェア ID]** セクションで **[追加]** をクリックして 新しいハードウェア識別子を追加します。
