---
title: Windows デバイスを別のバージョンにアップグレードする
titleSuffix: Configuration Manager
description: Configuration Manager を利用し、Windows 10 Desktop または Windows 10 Mobile を実行するデバイスを自動的に別のエディションにアップグレードします。
ms.date: 01/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0c15e919978ae8458f426511dd9a0e6d7c311b4b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333290"
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>System Center Configuration Manager でエディションのアップグレード ポリシーを使用して、Windows デバイスをアップグレードする

*適用対象: System Center Configuration Manager (Current Branch)*


**エディションのアップグレード ポリシー**を使って、以下の Windows 10 のバージョンのいずれかを実行するデバイスを自動的に別のエディションにアップグレードできます。

- Windows 10 Desktop
- Windows 10 Mobile

次のアップグレード パスがサポートされます。

- Windows 10 Pro から Windows 10 Enterprise
- Windows 10 Home から Windows 10 Education
- Windows 10 Mobile から Windows 10 Mobile Enterprise

デバイスは Microsoft Intune に登録するか、Configuration Manager クライアント ソフトウェアを実行する必要があります。 現在、このポリシーは、オンプレミス MDM で管理されている PC と互換性はありません。

## <a name="before-you-start"></a>開始する前に  
 デバイスを最新バージョンにアップグレードし始める前に、次の前提条件を確認する必要があります。  

-   Windows 10 のデスクトップ エディションの場合: ポリシーの対象とするすべてのデバイスでの Windows の新しいバージョンに対する有効なプロダクト キー。 このプロダクト キーは、マルチ ライセンス認証キー (MAK) または汎用ボリューム ライセンス キー (GVLK) でもかまいません。 GVLK は、キー管理サービス (KMS) クライアント セットアップ キーとも呼ばれます。 詳細については、「[ボリューム ライセンス認証の計画](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)」を参照してください。 KMS クライアント セットアップ キーの一覧については、Windows Server のライセンス認証ガイドの「[付録 A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)」を参照してください。 <!--496871-->  

-   Windows 10 Mobile の場合: Microsoft ボリューム ライセンス サービス センター (VLSC) から入手した XML ライセンス ファイル。 このファイルには、ポリシーの対象とするすべてのデバイスでの Windows の新しいバージョンに対するライセンス情報が含まれます。

- この種類のポリシーを管理するには、Configuration Manager の**完全な権限を持つ管理者**のセキュリティ ロールである必要があります。

## <a name="configure-the-edition-upgrade-policy"></a>エディションのアップグレード ポリシーを構成する  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[Windows 10 エディションのアップグレード]** の順にクリックします。  

3.  **[ホーム]** タブの **[作成]** グループで、 **[エディション アップグレード ポリシーの作成]** をクリックします。  

4.  **[ポリシーを作成する]** をクリックします。  

5.  **エディション アップグレード ポリシーの作成ウィザード** の **[全般]** ページで、次の情報を指定します。  

    -   **名前** - エディションのアップグレード ポリシーの名前を入力します  

    -   **説明** (省略可能) - 必要に応じて、Intune コンソールでの識別に役立つポリシーの説明を入力します  

    -   **デバイスを以下のようにアップグレードする SKU** - ドロップダウン リストから、Windows 10 デスクトップまたは Windows 10 Mobile の対象エディションを選びます  

    -   **ライセンス情報** - 次のいずれかを選びます。  

        -   **プロダクト キー** - 対象の Windows 10 デスクトップ エディションの有効なプロダクト キーを入力します  

            > [!NOTE]  
            >  プロダクト キーを含むポリシーを作成した後でプロダクト キーを編集することはできません。 セキュリティ上の理由からキーは表示されません。 プロダクト キーを変更するには、キー全体を再入力する必要があります。  

        -   **ライセンス ファイル** - **[参照]** をクリックして、XML 形式の有効なライセンス ファイルを選びます。 Configuration Manager はこのライセンス ファイルを使って、Windows 10 Mobile デバイスをアップグレードします。  

6.  ウィザードを完了します。  


## <a name="deploy-the-edition-upgrade-policy"></a>エディションのアップグレード ポリシーを展開する  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[Windows 10 エディションのアップグレード]** の順にクリックします。  

3.  展開する Windows 10 のエディションのアップグレード ポリシーを選び、 **[ホーム]** タブの **[展開]** グループで **[展開]** をクリックします。  

4.  **[Windows 10 エディションのアップグレード ポリシーの展開]** ダイアログ ボックスで、最初に、ポリシーを展開するコレクションを選びます。 クライアントがポリシーを評価するスケジュールを選び、**[OK]** をクリックします。 Configuration Manager クライアントで管理されている PC の場合は、デバイス コレクションにポリシーを展開する必要があります。 Intune で登録されている PC の場合は、ユーザーまたはデバイス コレクションにポリシーを展開できます。 



## <a name="next-steps"></a>次のステップ

**[監視]** ワークスペースの **[展開]** ノードから、この展開を監視します。 展開失敗を示す次のようなエラーが表示される場合があります。
- **このデバイスには該当しません**
- **データ型を変換できませんでした**

これらのエラーは、展開が失敗したことを意味しているわけではありません。 対象の PC で、アップグレードが正常に実行されたことを確認してください。

クライアントは、対象ポリシーを評価した後、2 時間以内に再起動してアップグレードを適用します。 ポリシーを展開するすべてのユーザーに通知するか、ポリシーの実行をユーザーの業務時間外にスケジュール設定します。

クライアントの **DcmWmiProvider.log** に次のエラーが記録される場合は、ライセンス認証シナリオに適切なキーを使っていることを確認します。 詳細については、「[開始する前に](#before-you-start)」セクションを参照してください。 ライセンス認証にキー管理サービスを使っている場合は、必ず [KMS クライアント セットアップ キー](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)を使うようにしてください。  <!-- 496871 -->   

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`
