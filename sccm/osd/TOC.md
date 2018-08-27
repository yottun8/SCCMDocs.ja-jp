# 理解と調査
## [OS の展開の概要](understand/introduction-to-operating-system-deployment.md)

# 計画と設計
## [OS の展開のインフラストラクチャ要件](plan-design/infrastructure-requirements-for-operating-system-deployment.md)
## [タスクの自動化計画に関する考慮事項](plan-design/planning-considerations-for-automating-tasks.md)
## [OS の展開のセキュリティとプライバシー](plan-design/security-and-privacy-for-operating-system-deployment.md)
## [OS の展開の相互運用性に関する計画](plan-design/planning-for-operating-system-deployment-interoperability.md)

# 作業開始
## [オペレーティング システムの展開用のサイト システムの役割を準備する](get-started/prepare-site-system-roles-for-operating-system-deployments.md)
## [オペレーティング システムの展開の準備](get-started/prepare-for-operating-system-deployment.md)
### [ブート イメージの管理](get-started/manage-boot-images.md)
#### [ブート イメージのカスタマイズ](get-started/customize-boot-images.md)

### [OS イメージの管理](get-started/manage-operating-system-images.md)
#### [OS イメージのカスタマイズ](get-started/customize-operating-system-images.md)

### [OS アップグレード パッケージの管理](get-started/manage-operating-system-upgrade-packages.md)
### [ドライバーの管理](get-started/manage-drivers.md)
### [ユーザー状態の管理](get-started/manage-user-state.md)
### [不明なコンピューターの展開の準備](get-started/prepare-for-unknown-computer-deployments.md)
### [展開先のコンピューターにユーザーを関連付ける](get-started/associate-users-with-a-destination-computer.md)

## [WAN トラフィックを削減するための Windows PE ピア キャッシュの準備](get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)

# 展開と使用
## [エンタープライズ オペレーティング システムを展開するシナリオ](deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)
### [Windows を最新バージョンにアップグレードする](deploy-use/upgrade-windows-to-the-latest-version.md)
### [新しいバージョンの Windows で既存のコンピューターを更新する](deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)
### [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](deploy-use/install-new-windows-version-new-computer-bare-metal.md)
### [既存のコンピューターの置き換えと設定の転送](deploy-use/replace-an-existing-computer-and-transfer-settings.md)

## [エンタープライズ オペレーティング システムを展開する方法](deploy-use/methods-to-deploy-enterprise-operating-systems.md)
### [PXE を使用したネットワーク経由での Windows の展開](deploy-use/use-pxe-to-deploy-windows-over-the-network.md)
### [ソフトウェア センターを使用したネットワーク経由での Windows の展開](deploy-use/use-software-center-to-deploy-windows-over-the-network.md)
### [起動可能なメディアを使用したネットワーク経由での Windows の展開](deploy-use/use-bootable-media-to-deploy-windows-over-the-network.md)
### [ネットワークではなくスタンドアロン メディアを使用した Windows の展開](deploy-use/use-stand-alone-media-to-deploy-windows-without-using-the-network.md)
### [マルチキャストを使用した、ネットワーク経由での Windows の展開](deploy-use/use-multicast-to-deploy-windows-over-the-network.md)
### [工場出荷時の OEM 用、または現地保管場所用のイメージの作成](deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
### [Windows to Go の展開](deploy-use/deploy-windows-to-go.md)

## [サービスとしての Windows の管理](deploy-use/manage-windows-as-a-service.md)
## [段階的な展開の作成](deploy-use/create-phased-deployment-for-task-sequence.md)
## [段階的な展開の管理と監視](deploy-use/manage-monitor-phased-deployments.md)
## [OS の展開の監視](deploy-use/monitor-operating-system-deployments.md)

## [タスクを自動化するためのタスク シーケンスの管理](deploy-use/manage-task-sequences-to-automate-tasks.md)
### [OS をインストールするタスク シーケンスの作成](deploy-use/create-a-task-sequence-to-install-an-operating-system.md)
### [OS をアップグレードするタスク シーケンスの作成](deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
### [OS をキャプチャするタスク シーケンスの作成](deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)
### [ユーザー状態をキャプチャおよび復元するタスク シーケンスの作成](deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)
### [バーチャル ハード ディスクを管理するためのタスク シーケンスの使用](deploy-use/use-a-task-sequence-to-manage-virtual-hard-disks.md)

## カスタム タスク シーケンスのシナリオ
### [カスタム タスク シーケンスの作成](deploy-use/create-a-custom-task-sequence.md)
### [OS 以外の展開用タスク シーケンスの作成](deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)
### [BIOS からUEFI への変換を管理するためのタスク シーケンス手順](deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md)
### [Windows PE での BitLocker の事前準備](deploy-use/preprovision-bitlocker-in-windows-pe.md)

## [タスク シーケンス メディアの作成](deploy-use/create-task-sequence-media.md)
### [スタンドアロン メディアの作成](deploy-use/create-stand-alone-media.md)
### [事前設定されたメディアの作成](deploy-use/create-prestaged-media.md)
### [起動可能なメディアの作成](deploy-use/create-bootable-media.md)
### [キャプチャ メディアを作成する](deploy-use/create-capture-media.md)

# テクニカル リファレンス
## [タスク シーケンスのステップ](understand/task-sequence-steps.md)
## [タスク シーケンス変数の使用方法](understand/using-task-sequence-variables.md)
## [タスク シーケンス変数](understand/task-sequence-variables.md)
## [タスク シーケンス メディアの起動前コマンド](understand/prestart-commands-for-task-sequence-media.md)

