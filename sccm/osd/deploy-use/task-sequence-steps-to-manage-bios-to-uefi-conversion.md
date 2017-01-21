---
title: "BIOS からUEFI への変換を管理するためのタスク シーケンス手順 | Configuration Manager"
description: "UEFI への移行用に FAT32 パーティションを準備するために、オペレーティング システム展開タスク シーケンスをカスタマイズする方法について説明します。"
ms.custom: na
ms.date: 11/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 54089ac8aa95154534d010bee8c7e2cbd70d1c7e
ms.openlocfilehash: 30838ed3ad045f781a748f96c874bf543ea05462


---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>BIOS からUEFI への変換を管理するためのタスク シーケンス手順
Configuration Manager バージョン 1610 以降では、**コンピューターの再起動**の手順で、UEFI への移行に備えてハード ドライブに FAT32 パーティションを準備するため、新しい変数 TSUEFIDrive を使って、オペレーティング システムの展開タスク シーケンスをカスタマイズできるようになりました。 次の手順では、タスク シーケンスのステップを作成して BIOS からUEFI への変換のためにハード ドライブを準備する方法の例を示します。

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>UEFI への変換のために FAT32 パーティションを準備するには:
オペレーティング システムをインストールする既存のタスク シーケンスでは、BIOS からUEFI への変換を実行する手順を含む新しいグループを追加します。

1. ファイルと設定をキャプチャする手順を完了したら、新しいタスク シーケンス グループを作成してから、オペレーティング システムをインストールするステップを実行します。 たとえば、[**キャプチャ ファイルと設定**] グループの後に、[**BIOS-to-UEFI**] という名前のグループを作成します。
2. 新しいグループの [**オプション**] タブで、新しいタスク シーケンス変数を条件 **_SMSTSBootUEFI** is **not equal** to **true** (_SMSTSBootUEFI は true と等しくない) として追加します。 これにより、コンピューターが既に UEFI モードになっている場合に、グループのステップが実行されないようにします。
![BIOS-to-UEFI グループ](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. 新しいグループの下に、[**コンピューターの再起動**] タスク シーケンスのステップを追加します。 [**再起動後に実行するものを指定してください**] で、[**このタスク シーケンスに割り当てられているブート イメージ**] をオンにして、Windows PE でコンピューターを起動します。  
4. [**オプション**] タブで、タスク シーケンス変数を条件 (**_SMSTSInWinPE equals false**) として追加します。 これにより、コンピューターが既に Windows PE にある場合に、このステップが実行されないようにします。

    ![コンピューターの再起動のステップ](../../core/get-started/media/restart-in-windows-pe.png)
5. ファームウェアを BIOS から UEFI に変換する OEM ツールを起動するステップを追加します。 これは一般に、OEM ツールを起動するコマンド ラインを含む**コマンドラインの実行**タスク シーケンスのステップになります。
6.  ハード ドライブをパーティションに分割してフォーマットするディスクのフォーマットとパーティション作成タスク シーケンスのステップを追加します。 このステップでは、次の操作を行います。
    1.  オペレーティング システムをインストールする前に、UEFI に変換される FAT32 パーティションを作成します。 [**ディスクの種類**] で [**GPT**] を選びます。
    ![ディスクのフォーマットとパーティション作成のステップ](../../core/get-started/media/format-and-partition-disk.png)
    2.  FAT32 パーティションのプロパティに移動します。 [**変数**] フィールドに「**TSUEFIDrive**」を入力します。 タスク シーケンスでこの変数を検出すると、コンピューターを再起動する前に UEFI 移行のための準備をします。
    ![パーティションのプロパティ](../../core/get-started/media/partition-properties.png)
    3. タスク シーケンス エンジンがその状態を保存し、ログ ファイルを保存するために使用する NTFS パーティションを作成します。
6.  **コンピューターの再起動**タスク シーケンスのステップを追加します。 [**再起動後に実行するものを指定してください**] で、[**このタスク シーケンスに割り当てられているブート イメージ**] をオンにして、Windows PE でコンピューターを起動します。  



<!--HONumber=Dec16_HO3-->


