---
title: 条件付きアクセス
titleSuffix: Configuration Manager
description: System Center Configuration Manager で条件付きアクセスを使用して、電子メールおよびその他のサービスをセキュリティで保護する方法について説明します。
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f354647ba9376ff18db1a4b63944ef31272308e1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>System Center Configuration Manager でサービスへのアクセスを管理する

*適用対象: System Center Configuration Manager (Current Branch)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>System Center Configuration Manager での条件付きアクセス
条件付きアクセスを使用して、Microsoft Intune に登録されているデバイスで、電子メールやその他のサービスをセキュリティで保護するための条件を指定します。  

 Configuration Manager で管理されているデバイスの条件付きアクセスに関する詳細は、「[System Center Configuration Manager で管理されている PC の O365 サービスへのアクセスを管理する](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)」を参照してください。  


 条件付きアクセスの一般的なフローは、次のようになります。  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 条件付きアクセスを使用すると、次のサービスへのアクセスを管理できます。  

-   Microsoft Exchange On-premises  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated  

-   SharePoint Online  

-   Skype for Business Online

-   Dynamics CRM Online

 条件付きアクセスを実装するには、Configuration Manager で次の 2 種類のポリシーを構成します。  

-   **コンプライアンス ポリシー** 。ユーザー コレクションに展開できるオプションのポリシーで、次のような設定を評価します。  

    -   パスコード  

    -   暗号化  

    -   デバイスが脱獄またはルート化されているかどうか  

    -   Configuration Manager または Microsoft Intune ポリシーでデバイス上の電子メールを管理するかどうか  

     コンプライアンス ポリシーを展開しない場合、デバイスは該当するすべての条件付きアクセス ポリシーに対して対応を報告します。

-   **条件付きアクセス ポリシー**は、特定のサービス向けです。 これらのポリシーは、どの Azure Active Directory セキュリティ ユーザー グループまたは Configuration Manager のユーザー コレクションを対象とするか、または除外するかなどのルールを定義します。  

     Configuration Manager コンソールから、オンプレミスの Exchange 条件付きアクセス ポリシーを構成します。 ただし、Exchange Online または SharePoint Online のポリシーを構成する場合は、そのポリシーを構成するための Microsoft Intune コンソールが開きます。  

     その他の Microsoft Intune または Configuration Manager ポリシーとは異なり、条件付きアクセス ポリシーは展開しません。 その代わり、これらのポリシーを 1 回構成すると、すべての対象ユーザーに適用されます。  

 デバイスが構成済みの条件を満たしていない場合、デバイスの登録と、デバイスの準拠問題の修正を行うプロセスがユーザーに案内されます。  

条件付きアクセスの使用を開始する前に、次の該当する要件を満たしていることを確認してください。  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Exchange Online (共有マルチテナント環境を使用) の要件
Exchange Online への条件付きのアクセスでは、次を実行するデバイスがサポートされます。
-   Windows 8.1 以降 (Intune に登録されている場合)
-   Windows 7.0 または Windows 8.1 (ドメインに参加している場合)
-   Windows Phone 8.1 以降
-   iOS 7.1 以降
-   Android 4.0 以降、Samsung KNOX Standard 4.0 以降

 **補足**:
-   デバイスをワークプレース参加させる必要があります。ワークプレース参加させると、デバイスは Azure Active Directory Device Registration Service (AAD DRS) に登録されます。<br />     
- ドメインに参加した PC は、グループ ポリシーまたは MSI によって自動的に Azure Active Directory に登録されるはずです。

  この記事の「**PC の条件付きアクセス**」セクションに、PC の条件付きアクセスを有効にするためのすべての要件が説明されています。<br />     
  AAD DRS は、Microsoft Intune や Office 365 のお客様に対して自動的にアクティブ化されます。 ADFS Device Registration Service を展開済みのお客様には、オンプレミスの Active Directory で登録されたデバイスは表示されません。
-   Exchange Online (E3 など) が含まれる、Office 365 のサブスクリプションを使用します。 ユーザーは、Exchange Online のライセンスを取得している必要があります。
-   Exchange Server コネクタはオプションで、Configuration Manager を Microsoft Exchange Online に接続します。 このコネクタは、Configuration Manager コンソールでデバイス情報を監視するのに役立ちます。 詳細については、「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください。
コンプライアンス ポリシーまたは条件付きアクセス ポリシーを使用するためにコネクタは不要です。 条件付きアクセスの影響に関するレポートを実行するには、コネクタが必要です。

## <a name="requirements-for-exchange-online-dedicated"></a>Exchange Online Dedicated の要件
Exchange Online Dedicated への条件付きのアクセスでは、次を実行するデバイスがサポートされます。
-   Windows 8 以降 (Intune に登録されている場合)
-   Windows 7.0 または Windows 8.1 (ドメインに参加している場合)

  新しい Exchange Online 専用環境にあるテナント専用のドメイン参加 PC への条件付きアクセス
-   Windows Phone 8 以降
-   Exchange ActiveSync (EAS) 電子メール クライアントを使用する iOS デバイス
-   Android 4 以降
-   従来の Exchange Online Dedicated 環境のテナントの場合:    

  Configuration Manager を Microsoft Exchange On-premises に接続する Exchange Server コネクタを使用します。 コネクタを使用すると、モバイル デバイスを管理でき、条件付きアクセスが有効になります。 詳細については、「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください。
-   新しい Exchange Online Dedicated 環境のテナントの場合:     
  Exchange Server コネクタはオプションで、Configuration Manager を Microsoft Exchange Online に接続し、デバイス情報の管理に役立ちます。 詳細については、「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください。 コンプライアンス ポリシーまたは条件付きアクセス ポリシーを使用するためにコネクタは不要です。 条件付きアクセスの影響に関するレポートを実行するには、コネクタが必要です。  

## <a name="requirements-for-exchange-on-premises"></a>Exchange On-premises の要件
Exchange On-premises に対する条件付きアクセスでは、次のデバイスをサポートします。
-   Windows 8 以降 (Intune に登録されている場合)
-   Windows Phone 8 以降
-   iOS のネイティブ電子メール アプリ
-   Android 4 以降のネイティブ電子メール アプリ
-   Microsoft Outlook アプリはサポートされていません (Android および iOS)

**補足**:

- Exchange のバージョンは、Exchange 2010 以降である必要があります
- Exchange Server クライアント アクセス サーバー (CAS) アレイがサポートされています

> [!TIP]
> Exchange 環境が CAS サーバー構成にある場合は、CAS サーバーのいずれかを指すようにオンプレミスの Exchange コネクタを構成する必要があります。
- Configuration Manager を Microsoft Exchange On-premises に接続する Exchange Server コネクタを使用します。 コネクタを使用すると、モバイル デバイスを管理でき、条件付きアクセスが有効になります。 詳細については、「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください。
  - 最新バージョンのオンプレミスの Exchange コネクタを使用していることを確認してください。 オンプレミスの Exchange コネクタは、Configuration Manager コンソールから構成します。 詳細な手順の説明については、「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください。
  - Configuration Manager プライマリ サイトでコネクタのみを構成します。

- Exchange ActiveSync は、証明書ベースの認証またはユーザーの資格情報のエントリで構成できます。


## <a name="requirements-for-skype-for-business-online"></a>Skype for Business Online の要件
SharePoint Online への条件付きアクセスでは、次を実行するデバイスがサポートされます。
 -   iOS 7.1 以降
 -   Android 4.0 以降
 -   Samsung KNOX Standard 4.0 以降

Skype for Business Online の[先進認証](https://aka.ms/SkypeModernAuth)を有効にします。 

すべてのユーザーが Skype for Business Online を使用する必要があります。 Skype for Business Online と Skype for Business オンプレミスの両方が含まれている展開の場合は、条件付きアクセス ポリシーはオンプレミスのユーザーに適用されません。

## <a name="requirements-for-sharepoint-online"></a>SharePoint Online の要件
SharePoint Online への条件付きアクセスでは、次を実行するデバイスがサポートされます。
 -   Windows 8.1 以降 (Intune に登録されている場合)
 -   Windows 7.0 または Windows 8.1 (ドメインに参加している場合)
 -   Windows Phone 8.1 以降
 -   iOS 7.1 以降
 -   Android 4.0 以降、Samsung KNOX Standard 4.0 以降

 **補足**:
 -   デバイスをワークプレース参加させる必要があります。ワークプレース参加させると、デバイスは Azure Active Directory Device Registration Service (AAD DRS) に登録されます。

 ドメインに参加した PC は、グループ ポリシーまたは MSI によって自動的に Azure Active Directory に登録されるはずです。 この記事の「**PC の条件付きアクセス**」セクションに、PC の条件付きアクセスを有効にするためのすべての要件が説明されています。

 AAD DRS は、Microsoft Intune や Office 365 のお客様に対して自動的にアクティブ化されます。 ADFS Device Registration Service を展開済みのお客様には、オンプレミスの Active Directory で登録されたデバイスは表示されません。
 -   SharePoint Online サブスクリプションが必要です。ユーザーには、SharePoint Online のライセンスが必要です。

 ### <a name="conditional-access-for-pcs"></a>PC の条件付きアクセス

 Office デスクトップ アプリケーションを実行する PC に対して条件付きアクセスを構成し、Exchange Online または SharePoint Online にアクセスすることができます。 PC は、次の要件を満たす必要があります。
 -   Windows 7.0 または Windows 8.1 を実行している PC であること
 -   ドメインに参加しているか、ドメイン対応の PC であること

 準拠するためには、PC は Microsoft Intune に登録済みで、ポリシーに準拠している必要があります。

 ドメインに参加する PC の場合、Azure Active Directory に [デバイスを自動的に登録](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/) するように設定する必要があります。
 -   [Office 365 の最新の認証が有効化](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)されていて、最新の Office 更新プログラムがすべて適用されている必要があります。<br />     最新の認証により、Active Directory Authentication Library (ADAL) ベースのサインインが Office 2013 Windows クライアントに導入され、多要素認証および証明書ベースの認証などのより強力なセキュリティが有効になります。
 -   最新ではない認証プロトコルをブロックするように ADFS 要求規則を設定します。  

## <a name="next-steps"></a>次のステップ  
 必要なシナリオのコンプライアンス ポリシーと条件付きアクセス ポリシーを構成する方法については、次のトピックを参照してください。  

-   [System Center Configuration Manager でのデバイス コンプライアンス ポリシーの管理](../../protect/deploy-use/device-compliance-policies.md)  

-   [System Center Configuration Manager でのメール アクセスの管理](../../protect/deploy-use/manage-email-access.md)  

-   [System Center Configuration Manager での SharePoint Online アクセスの管理](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Skype for Business Online のアクセスの管理](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>関連項目  

 [System Center Configuration Manager のコンプライアンス設定を使ってみる](../../compliance/get-started/get-started-with-compliance-settings.md)
