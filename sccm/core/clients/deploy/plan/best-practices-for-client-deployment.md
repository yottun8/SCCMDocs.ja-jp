---
title: "クライアント展開のベスト プラクティス | Microsoft Docs"
description: "System Center Configuration Manager のクライアント展開のベスト プラクティスを示します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: 11
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 49b2520a82614bedc7bcc077604e0b89885119c2


---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>System Center Configuration Manager のクライアント展開のベスト プラクティス

*適用対象: System Center Configuration Manager (Current Branch)*

以下のベスト プラクティス情報は、System Center Configuration Manager でコンピューターにクライアントを展開する場合に役立ちます。  

## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Active Directory コンピューターには、ソフトウェア更新プログラムを使ったクライアントのインストールを行う  
 このクライアント展開方法は、既存の Windows テクノロジを使用する、Active Directory インフラストラクチャと統合できる、Configuration Manager で最低限の構成しか必要としない、ファイアウォール用の構成が最も容易である、最も安全である、といった利点があります。 グループ ポリシーの構成にセキュリティ グループと WMI フィルターを使用するので、どのコンピューターに Configuration Manager クライアントをインストールするかについても、柔軟に制御できます。  

 詳細については、「 [ソフトウェアの更新に基づいたインストールを使用した Configuration Manager クライアントのインストール方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP)」をご覧ください。  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Active Directory スキーマを拡張してサイトを公開し、コマンドライン オプションなしでCCMSetup が実行できるようにする  
 Active Directory スキーマを Configuration Manager 用に拡張して、サイトが Active Directory Domain Services に公開されるとき、多くのクライアント インストール プロパティが Active Directory Domain Services に公開されます。 コンピューターでこれらのクライアント インストール プロパティを見つけることができる場合は、Configuration Manager クライアントの展開時にそれらを使用できます。 この情報は自動的に生成されるため、インストール プロパティを手動で入力するために発生する人的ミスのリスクが排除されます。  

 詳細については、「[System Center Configuration Manager で Active Directory ドメイン サービスに発行されたクライアント インストールのプロパティについて](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)」を参照してください。  

## <a name="when-you-have-many-clients-to-deploy-plan-a-phased-rollout-outside-business-hours"></a>多くのクライアントを展開する場合は、業務時間外に段階的にロールアウトするよう計画する  
 時間をかけてクライアントを段階的にロールアウトするよう計画することで、CPU 処理の要件によるサイトサーバーへの影響を最小化します。 業務時間外にクライアントを展開すると、日中重要なビジネス サービスに使用できる帯域幅が増え、ユーザーのコンピューターの反応が遅くなったり、インストールを完了するために再起動を必要として、ユーザーに支障をきたすことがありません。  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>主要なクライアント展開が終わったら、自動アップグレードを有効化する  
 自動クライアント アップグレードは、主要なクライアント インストール方法に含まれなかった少数のクライアント コンピューターをアップグレードする場合に役立ちます。 たとえば、最初のクライアント アップグレードを完了したが、アップグレードの展開時に一部のクライアントがオフラインだった場合です。 その場合、この方法を使って、これらのコンピューターが次にアクティブになった時にクライアントをアップグレードすることができます。  

> [!NOTE]  
>  Configuration Manager のパフォーマンスが改善され、プライマリ クライアントのアップグレード方法として自動アップグレードを使用できるようになりました。 ただし、パフォーマンスは、クライアント数など、階層のインフラストラクチャに左右されます。  

 自動クライアント アップグレードの方法の詳細については、「[System Center Configuration Manager で Windows コンピューター用クライアントをアップグレードする方法](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)」を参照してください。  

## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>client.msi プロパティを使ってクライアントをインストールするときは、SMSMP と FSP を使用する  
 SMSMP プロパティはクライアントが通信する最初の管理ポイントを指定し、Active Directory ドメイン サービス、DNS、WINS などの、サービスの場所のソリューションへの依存を排除します。  

 FSP プロパティを使ってフォールバック ステータス ポイントをインストールすると、クライアントのインストールや割り当てを監視し、通信上の問題点を特定できます。  

 これらのオプションの詳細については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../../core/clients/deploy/about-client-installation-properties.md)」を参照してください。  

## <a name="if-you-want-to-use-client-languages-other-than-english-install-the-client-language-packs-before-you-install-the-clients"></a>英語以外のクライアント言語を使用する場合、クライアントの言語パックをインストールしてから、クライアントをインストールしてください。  
 クライアントをインストールしてからサイトにクライアントの言語パックをインストールする場合、追加の言語を使用するには、クライアントを再インストールする必要があります。 モバイル デバイス クライアントの場合、モバイル デバイスをワイプして再登録する必要があります。  

 追加的なクライアント言語のサポートを追加する方法の詳細については、「[System Center Configuration Manager の言語パック](../../../../core/servers/deploy/install/language-packs.md)」を参照してください。  

## <a name="plan-and-prepare-any-required-pki-certificates-in-advance"></a>必要な PKI 証明書の事前計画および準備  
 インターネット上のデバイス、登録済みモバイル デバイス、および Mac コンピューターを管理するには、サイト システム (管理ポイントと配布ポイント) とクライアント デバイスに PKI 証明書が必要です。 多くのユーザーにとって、この構成には高度な計画と準備が必要です。PKI を管理する専門チームがいる場合は特に必要です。 運用ネットワークでは、状況に応じて、管理者が新しい証明書を使用するために管理承認を変更したり、サイト システム サーバーを再起動する必要があります。また、ユーザーは新しいグループ メンバーシップのためにログオフおよびログオンが必要になる場合があります。 さらに、セキュリティ アクセス許可のレプリケーションと新しい証明書テンプレートのために、十分な時間を見込む必要があります。  

 必要な PKI 証明書の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../../../core/plan-design/network/pki-certificate-requirements.md)」を参照してください。  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>クライアントをインストールする前に必要なクライアント設定とメンテナンス期間を構成する  
 クライアント設定とメンテナンス期間は、クライアントをインストールする前または後に構成できますが、クライアントをインストールしてすぐにこれらの設定を使用できるように、クライアントをインストールする前に必要な設定を構成しておいてください。 詳細については、「 [System Center Configuration Manager でクライアント設定を構成する方法](../../../../core/clients/deploy/configure-client-settings.md)」をご覧ください。  

 サーバーや Windows Embedded デバイスといった業務に不可欠なコンピューターでは、業務の継続性を確保するために、メンテナンス期間を構成します。 たとえば、必要なソフトウェア更新プログラムとマルウェア対策ソフトウェアによってコンピューターが営業時間内に再起動しないように、メンテナンス期間を設定することができます。  

> [!IMPORTANT]  
>  Unified Write Filter (UWF) で保護する予定の Windows 10 コンピューターでは、クライアントをインストールする前に UWF のデバイスを構成する必要があります。 これにより、メンテナンス モード中に権限の低いユーザーをロックアウトしてデバイスにログインできなくするカスタム資格情報プロバイダーを使用して、Configuration Manager がクライアントをインストールできるようになります。  

## <a name="for-mac-computers-and-mobile-devices-that-are-enrolled-by-configuration-manager-plan-your-user-enrollment-experience"></a>Configuration Manager に登録されている Mac コンピューターおよびモバイル デバイス用にユーザー登録エクスペリエンスを計画する  
 ユーザーが Configuration Manager を使用して自分の Mac コンピューターとモバイル デバイスを登録する場合、ユーザー エクスペリエンスを計画および準備します。 たとえば、Web ページを使用してインストールおよび登録プロセスをスクリプト化し、ユーザーが入力する情報を必要最小限に抑えたり、手順とリンクを電子メールでユーザーに送信したりすることができます。  

## <a name="when-you-manage-windows-embedded-devices-use-file-based-write-filters-fbwf-rather-than-enhanced-write-filters-ewf-for-higher-scalability"></a>Windows Embedded デバイスを管理する場合、スケーラビリティを高くするために、Enhanced Write Filter (EWF) ではなく、File-Based Write Filter (FBWF) を使用する  
 Enhanced Write Filter (EWF) を使用する組み込みデバイスでは、状態メッセージの再同期が発生しやすくなります。 Enhanced Write Filter を使用する組み込みデバイスが少数の場合は、この問題に気がつかない可能性があります。 ただし、差分のインベントリではなく完全なインベントリを送信する場合など、情報を再同期する組み込みデバイスが多数ある場合、ネットワーク パケットが大幅に増え、サイト サーバーの CPU 処理量が多くなる可能性があります。  

 有効にする書き込みフィルターの種類を選択できる場合は、Configuration Manager クライアント上のネットワークと CPU の効率のために、ファイル ベースの書き込みフィルターを選択し、デバイスの再起動から次の再起動までクライアントの状態とインベントリ データを維持する例外を構成します。 書き込みフィルターについて詳しくは「   [System Center Configuration Manager での Windows Embedded デバイスへのクライアント展開の計画](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)」をご覧ください。  

 プライマリ サイトでサポートできる Windows Embedded クライアントの最大数の詳細については、「[クライアントとデバイスでサポートされるオペレーティング システム](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)」を参照してください。  



<!--HONumber=Dec16_HO3-->


