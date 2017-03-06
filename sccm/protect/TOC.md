# 理解と調査
## [概要](understand\protect-data-and-site-infrastructure.md)
## [バックアップと回復](understand/backup-and-recovery.md)
## [高可用性オプション](understand/high-availability-options.md)
## [危険度の高い展開の管理](understand/settings-to-manage-high-risk-deployments.md)

# 計画と設計
## [証明書プロファイルの前提条件](plan-design/prerequisites-for-certificate-profiles.md)
### [証明書プロファイルに関する証明書テンプレート アクセス許可](plan-design/planning-for-certificate-template-permissions.md)
### [証明書プロファイルのセキュリティとプライバシー](plan-design/security-and-privacy-for-certificate-profiles.md)

## [Endpoint Protection の導入計画](plan-design/planning-for-endpoint-protection.md)

## [電子メール、Wi-Fi、VPN プロファイルの計画](plan-design/prerequisites-for-email-profiles.md)
### [電子メールのプロファイルの前提条件](plan-design/prerequisites-for-email-profiles.md)
### [と VPN プロファイルの前提条件](plan-design/prerequisites-for-wifi-vpn-profiles.md)

## [Wi-Fi および VPN プロファイルのセキュリティとプライバシー](plan-design/security-and-privacy-for-wifi-vpn-profiles.md)

## [電子メール プロファイルのセキュリティとプライバシー](plan-design/security-and-privacy-for-email-profiles.md)

## [証明書プロファイルのセキュリティとプライバシー](plan-design/security-and-privacy-for-certificate-profiles.md)

# 展開と使用
## [VPN プロファイル](deploy-use/vpn-profiles.md)
### [VPN プロファイルの作成](deploy-use/create-vpn-profiles.md)
### [アプリごとの VPN のパッケージ ファミリ名 (PFN) の検索](deploy-use/find-a-pfn-for-per-app-vpn.md)

## [Wi-Fi プロファイル](deploy-use/create-wifi-profiles.md)
### [Wi-Fi プロファイルの作成](deploy-use/create-wifi-profiles.md)

## [証明書プロファイル](deploy-use/introduction-to-certificate-profiles.md)
### [証明書プロファイルの作成](deploy-use/create-certificate-profiles.md)
### [PFX 証明書プロファイルの作成](deploy-use/create-pfx-certificate-profiles.md)
### [証明書インフラストラクチャの構成](deploy-use/certificate-infrastructure.md)
### [暗号化コントロールのテクニカル リファレンス](deploy-use/cryptographic-controls-technical-reference.md)

## [Endpoint Protection](deploy-use/endpoint-protection.md)
### [Endpoint Protection の構成](deploy-use/endpoint-protection-configure.md)
#### [サイト システムの役割](deploy-use/endpoint-protection-site-role.md)
#### [警告](deploy-use/endpoint-configure-alerts.md)
#### [定義の更新](deploy-use/endpoint-definition-updates.md)
##### [ConfigMgr の更新](deploy-use/endpoint-definitions-configmgr.md)
##### [WSUS の更新](deploy-use/endpoint-definitions-wsus.md)
##### [Microsoft 更新プログラム](deploy-use/endpoint-definitions-microsoft-updates.md)
##### [マルウェア プロテクション センター](deploy-use/endpoint-definitions-protection-center.md)
##### [ネットワーク共有の更新](deploy-use/endpoint-definitions-network.md)

#### [ポリシーの展開](deploy-use/endpoint-antimalware-policies.md)
#### [クライアントの構成](deploy-use/endpoint-protection-configure-client.md)

### [Windows ファイアウォール ポリシー](deploy-use/create-windows-firewall-policies.md)
### [Windows Defender Advanced Threat Protection](deploy-use/windows-defender-advanced-threat-protection.md)
### [マルウェア対策とファイアウォールのタスク](deploy-use/endpoint-antimalware-firewall.md)
### [Endpoint Protection のシナリオ](deploy-use/scenarios-endpoint-protection.md)
### [Endpoint Protection クライアント ヘルプ](deploy-use/endpoint-protection-client-help.md)
### [クライアントのトラブルシューティング](deploy-use/troubleshoot-endpoint-client.md)

## [電子メール プロファイル](deploy-use/introduction-to-email-profiles.md)
### [電子メール プロファイルの作成](deploy-use/create-exchange-activesync-profiles.md)
### [、VPN、電子メール、および証明書プロファイルの展開](deploy-use/deploy-wifi-vpn-email-cert-profiles.md)

## [サービスへのアクセスの管理](deploy-use/manage-access-to-services.md)
### [デバイス コンプライアンス ポリシー](deploy-use/device-compliance-policies.md)
### [デバイス コンプライアンス ポリシーを作成する](deploy-use/create-compliance-policy.md)
### [電子メールへのアクセスの管理](deploy-use/manage-email-access.md)
### [SharePoint Online アクセスの管理](deploy-use/manage-sharepoint-online-access.md)
### [Skype for Business Online のアクセスの管理](deploy-use/manage-skype-for-business-online-access.md)
### [Dynamics CRM Online アクセスの管理](deploy-use/manage-dynamics-crm-online-access.md)
### [O365 サービスへの PC アクセスの管理](deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)
## [Manage access based on device, network, and application risk](deploy-use/configuration-manager-mobile-threat-defense.md) (デバイス、ネットワーク、アプリケーションのリスクに基づいたアクセスの管理)
### [Configuration Manager の Lookout](deploy-use/lookout-mobile-threat-defense-in-configuration-manager.md)
#### [Set up Lookout device threat protection](deploy-use/set-up-your-subscription-with-lookout.md) (Lookout デバイス脅威保護の設定)
#### [Enable Lookout in Intune](deploy-use/enable-lookout-connection-in-intune.md) (Intune で Lookout を有効にする)
#### [Deploy Lookout for Work apps](deploy-use/configure-and-deploy-lookout-for-work-apps.md) (Lookout for Work アプリを展開する)
#### [Enable device threat protection policy](deploy-use/enable-device-threat-protection-rule-compliance-policy.md) (デバイスの脅威保護ポリシーを有効にする)
#### [Troubleshoot Lookout integration](deploy-use/troubleshoot-lookout-integration.md) (Lookout 統合のトラブルシューティング)

## [Windows Hello for Business の設定](deploy-use/windows-hello-for-business-settings.md)

## [使用条件の設定](../mdm/deploy-use/terms-and-conditions.md)

## モニターの保護
### [Wi-Fi、電子メール、VPN プロファイルの監視](deploy-use/monitor-wifi-email-vpn-profiles.md)
### [証明書プロファイルの監視](deploy-use/monitor-certificate-profiles.md)
### [Endpoint Protection の監視](deploy-use/monitor-endpoint-protection.md)
