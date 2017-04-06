---
title: "Windows 10 更新プログラムに対する高速インストール ファイルの管理 | Microsoft Docs"
description: "Configuration Manager では Windows 10 用の高速インストール ファイルがサポートされます。これを使用すると、クライアント上でのダウンロード量を少なくし、インストールに要する時間を短縮できます。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 459ad5a428102b5e040bec2eaf2a70fc89789dff
ms.lasthandoff: 03/27/2017

---

## <a name="manage-express-installation-files-for-windows-10-updates"></a>Windows 10 更新プログラムに対する高速インストール ファイルの管理
Configuration Manager バージョン 1702 以降、Configuration Manager では Windows 10 更新プログラムに対する高速インストール ファイルがサポートされています。 サポートされているバージョンの Windows 10 を使用する場合は、当月の Windows 10 累積的な更新プログラムと、前月の更新プログラムとの差分のみをダウンロードする Configuration Manager 設定を使用できます。 高速インストール ファイルを使用しない場合、Configuration Manager では完全な Windows 10 累積的な更新プログラム (以前の月の更新プログラムをすべて含む) が毎月ダウンロードされます。 高速インストール ファイルを使用すると、クライアント上でのダウンロード量を少なくし、インストールに要する時間を短縮できます。

> [!IMPORTANT]
> 高速インストール ファイルの使用をサポートする設定は Configuration Manager バージョン 1702 で使用できますが、オペレーティング システム クライアント サポートは Windows Update エージェントの更新プログラムが適用された Windows 10 バージョン 1607 でサポートされます。 この更新プログラムは、2017 年 4 月 11 日リリースの更新プログラム (月例パッチ) に含まれています。 <!--For more information about these updates, see [support article 4015217](http://support.microsoft.com/kb/4015217).--> 今後の更新プログラムでは、高速の活用によりダウンロード量をさらに少なくすることができます。 この更新プログラムが適用されていない Windows 10 バージョン 1607 および以前のバージョンでは、高速インストール ファイルをサポートしていません。

### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Windows 10 更新プログラム用の高速インストール ファイルの、サーバー上へのダウンロードを有効にするには
Windows 10 高速インストール ファイルのメタデータの同期を開始するには、ソフトウェアの更新ポイントのプロパティで同期を有効にする必要があります。
1.    Configuration Manager コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** に移動します。
2.    中央管理サイトまたはスタンドアロン プライマリ サイトを選択します。
3.    [ホーム **** ] タブの [設定 **** ] グループで [サイト コンポーネントの構成 ****] をクリックし、[ソフトウェアの更新ポイント ****] を選択します。 **[更新ファイル]** タブで **[Windows 10 のすべての承認済み更新プログラムの全部のファイルと高速インストール ファイルをダウンロードする]** を選択します。

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>クライアントが高速インストール ファイルをダウンロードしてインストールするためのサポートを有効にするには
クライアント上で高速インストール ファイルのサポートを有効にするには、クライアント設定の [ソフトウェア更新プログラム] セクションでクライアントでの高速インストール ファイルを有効にする必要があります。 これにより、指定したポートへの高速インストール ファイルのダウンロード要求をリッスンする新しい HTTP リスナーが作成されます。 クライアント上でこの機能を有効にするようにクライアント設定を展開すると、当月の Windows 10 累積的な更新プログラムと、前月の更新プログラムとの間の差分のダウンロードが試みられます (クライアントでは、高速インストール ファイルをサポートする Windows 10 のバージョンが実行されている必要があります)。
1.    ソフトウェアの更新ポイント コンポーネントのプロパティで高速インストール ファイルのサポートを有効にします(前の手順を参照)。
2.    Configuration Manager コンソールで、**[管理]** > **[クライアント設定]** の順に移動します。
3.    適切なクライアント設定を選択し、**[ホーム]** タブで **[プロパティ]** をクリックします。
4.    **[ソフトウェア更新プログラム]** ページを選択し、**[Express の更新プログラムのクライアントでのインストールを有効にする]** 設定で **[はい]** を構成し、**[Express の更新プログラムのコンテンツをダウンロードするために使用するポート]** 設定で HTTP リスナーが使用するポートを構成します。

