---
title: チュートリアル:Azure Active Directory シングル サインオン (SSO) と 8x8 の統合 | Microsoft Docs
description: Azure Active Directory と 8x8 の間でシングル サインオンを構成する方法について説明します。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: tutorial
ms.date: 02/20/2020
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: f49c2b445af9acb0761d01b731250e068cb96a36
ms.sourcegitcommit: dd3db8d8d31d0ebd3e34c34b4636af2e7540bd20
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2020
ms.locfileid: "77562321"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-8x8"></a>チュートリアル:Azure Active Directory シングル サインオン (SSO) と 8x8 の統合

このチュートリアルでは、8x8 と Azure Active Directory (Azure AD) を統合する方法について説明します。 Azure AD と 8x8 を統合すると、次のことができます。

* 8x8 にアクセスできるユーザーを Azure AD で制御できます。
* ユーザーが自分の Azure AD アカウントを使用して 8x8 に自動的にサインインできるように設定できます。
* 1 つの中央サイト (Azure Portal) で自分のアカウントを管理します。

SaaS アプリと Azure AD の統合の詳細については、「[Azure Active Directory でのアプリケーションへのシングル サインオン](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)」を参照してください。

## <a name="prerequisites"></a>前提条件

開始するには、次が必要です。

* Azure AD サブスクリプション。 サブスクリプションがない場合は、[無料アカウント](https://azure.microsoft.com/free/)を取得できます。
* 8x8 サブスクリプション。

## <a name="scenario-description"></a>シナリオの説明

このチュートリアルでは、テスト環境で Azure AD の SSO を構成してテストします。

* 8x8 では、**SP Initiated SSO と IDP Initiated SSO** がサポートされます

* 8x8 を構成したら、組織の機密データを流出と侵入からリアルタイムで保護するセッション制御を適用することができます。 セッション制御は、条件付きアクセスを拡張したものです。 [Microsoft Cloud App Security でセッション制御を強制する方法](https://docs.microsoft.com/cloud-app-security/proxy-deployment-any-app)をご覧ください。

> [!NOTE]
> このアプリケーションの識別子は固定文字列値であるため、1 つのテナントで構成できるインスタンスは 1 つだけです。

## <a name="adding-8x8-from-the-gallery"></a>ギャラリーからの 8x8 の追加

Azure AD への 8x8 の統合を構成するには、ギャラリーからマネージド SaaS アプリの一覧に 8x8 を追加する必要があります。

1. 職場または学校アカウントか、個人の Microsoft アカウントを使用して、[Azure portal](https://portal.azure.com) にサインインします。
1. 左のナビゲーション ウィンドウで **[Azure Active Directory]** サービスを選択します。
1. **[エンタープライズ アプリケーション]** に移動し、 **[すべてのアプリケーション]** を選択します。
1. 新しいアプリケーションを追加するには、 **[新しいアプリケーション]** を選択します。
1. **[ギャラリーから追加する]** セクションで、検索ボックスに、「**8x8**」と入力します。
1. 結果パネルで **[8x8]** を選択し、アプリを追加します。 お使いのテナントにアプリが追加されるのを数秒待機します。

## <a name="configure-and-test-azure-ad-single-sign-on-for-8x8"></a>8x8 の Azure AD シングル サインオンの構成とテスト

**B.Simon** というテスト ユーザーを使用して、8x8 に対する Azure AD SSO を構成してテストします。 SSO を機能させるために、Azure AD ユーザーと 8x8 の関連ユーザーとの間にリンク関係を確立する必要があります。

8x8 で Azure AD SSO を構成してテストするには、次の構成要素を完了します。

1. **[Azure AD SSO の構成](#configure-azure-ad-sso)** - ユーザーがこの機能を使用できるようにします。
    1. **[Azure AD のテスト ユーザーの作成](#create-an-azure-ad-test-user)** - B.Simon で Azure AD のシングル サインオンをテストします。
    1. **[Azure AD テスト ユーザーの割り当て](#assign-the-azure-ad-test-user)** - B.Simon が Azure AD シングル サインオンを使用できるようにします。
1. **[8x8 の SSO の構成](#configure-8x8-sso)** - アプリケーション側でシングル サインオン設定を構成します。
    1. **[8x8 のテスト ユーザーの作成](#create-8x8-test-user)** - 8x8 で B.Simon に対応するユーザーを作成し、Azure AD の B.Simon にリンクさせます。
1. **[SSO のテスト](#test-sso)** - 構成が機能するかどうかを確認します。

## <a name="configure-azure-ad-sso"></a>Azure AD SSO の構成

これらの手順に従って、Azure portal で Azure AD SSO を有効にします。

1. [Azure portal](https://portal.azure.com/) の **8x8** アプリケーション統合ページで、 **[管理]** セクションを見つけて、 **[シングル サインオン]** を選択します。
1. **[シングル サインオン方式の選択]** ページで、 **[SAML]** を選択します。
1. **[SAML でシングル サインオンをセットアップします]** ページで、 **[基本的な SAML 構成]** の編集 (ペン) アイコンをクリックして設定を編集します。

   ![基本的な SAML 構成を編集する](common/edit-urls.png)

1. **[基本的な SAML 構成]** セクションで、次の手順を実行します。

    a. **[識別子]** ボックスに、次のいずれかのパターンで URL を入力します。

    |||
    |-|-|
    | `https://sso.8x8.com/saml2`|
    | `https://sso.8x8pilot.com/saml2`|

    b. **[応答 URL]** ボックスに、次のいずれかのパターンを使用して URL を入力します。

    |||
    |-|-|
    | `https://sso.8x8.com/saml2`|
    | `https://sso.8x8pilot.com/saml2`|


1. **[SAML でシングル サインオンをセットアップします]** ページの **[SAML 署名証明書]** セクションで、 **[証明書 (Base64)]** を見つけて、 **[ダウンロード]** を選択し、証明書をダウンロードして、お使いのコンピューターに保存します。 この証明書は、チュートリアルの後半の「**8x8 の SSO の構成**」セクションで使用します。

    ![証明書のダウンロードのリンク](common/certificatebase64.png)

1. **[8x8 のセットアップ]** セクションで、URL をコピーします。これらの URL 値は、チュートリアルの後半で使用します。

    ![構成 URL のコピー](./media/8x8virtualoffice-tutorial/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Azure AD のテスト ユーザーの作成

このセクションでは、Azure portal 内で B.Simon というテスト ユーザーを作成します。

1. Azure portal の左側のウィンドウから、 **[Azure Active Directory]** 、 **[ユーザー]** 、 **[すべてのユーザー]** の順に選択します。
1. 画面の上部にある **[新しいユーザー]** を選択します。
1. **[ユーザー]** プロパティで、以下の手順を実行します。
   1. **[名前]** フィールドに「`B.Simon`」と入力します。  
   1. **[ユーザー名]** フィールドに「username@companydomain.extension」と入力します。 たとえば、「 `B.Simon@contoso.com` 」のように入力します。
   1. **[パスワードを表示]** チェック ボックスをオンにし、 **[パスワード]** ボックスに表示された値を書き留めます。
   1. **Create** をクリックしてください。

### <a name="assign-the-azure-ad-test-user"></a>Azure AD テスト ユーザーの割り当て

このセクションでは、B.Simon に 8x8 へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

1. Azure portal で **[エンタープライズ アプリケーション]** を選択し、 **[すべてのアプリケーション]** を選択します。
1. アプリケーションの一覧で **[8x8]** を選択します。
1. アプリの概要ページで、 **[管理]** セクションを見つけて、 **[ユーザーとグループ]** を選択します。

   ![[ユーザーとグループ] リンク](common/users-groups-blade.png)

1. **[ユーザーの追加]** を選択し、 **[割り当ての追加]** ダイアログで **[ユーザーとグループ]** を選択します。

    ![[ユーザーの追加] リンク](common/add-assign-user.png)

1. **[ユーザーとグループ]** ダイアログの [ユーザー] の一覧から **[B.Simon]** を選択し、画面の下部にある **[選択]** ボタンをクリックします。
1. **[割り当ての追加]** ダイアログで、 **[割り当て]** をクリックします。

## <a name="configure-8x8-sso"></a>8x8 の SSO の構成

このチュートリアルの次の部分は、8x8 で使用しているサブスクリプションの種類によって異なります。

* 管理に Configuration Manager を使用している 8x8 エディションおよび X シリーズのお客様の場合は、「[8x8 Configuration Manager の構成](#configure-8x8-configuration-manager)」を参照してください。
* 管理に Account Manager を使用している Virtual Office のお客様の場合は、「[8x8 Account Manager の構成](#configure-8x8-account-manager)」を参照してください。

### <a name="configure-8x8-configuration-manager"></a>8x8 Configuration Manager の構成

1. 8x8 [Configuration Manager](https://vo-cm.8x8.com/) にログインします。

1. ホーム ページで、 **[Identity Management]\(ID 管理\)** をクリックします。

1. **[Single Sign On (SSO)]\(シングル サインオン (SSO)\)** をオンにし、 **[Microsoft Azure AD]** を選択します。

1. 3 つの URL と署名証明書を、Azure AD の **[SAML でシングル サインオンをセットアップします]** ページから、8x8 Configuration Manager の **[Microsoft Azure AD SAML Settings]\(Microsoft Azure AD SAML 設定\)** セクションにコピーします。

    a. **ログイン URL** を **[IDP Login URL]\(IDP ログイン URL\)** にコピーします。

    b. **Azure AD 識別子**を **[IDP Issuer URL/URN]\(IDP 発行者 URL/URN\)** にコピーします。

    c. **ログアウト URL** を **[IDP Logout URL]\(IDP ログアウト URL\)** にコピーします。

    d. **証明書 (Base64)** をダウンロードし、 **[Certificate]\(証明書\)** にアップロードします。

    e. **[保存]** をクリックします。

### <a name="configure-8x8-account-manager"></a>8x8 Account Manager の構成

1. 8x8 Virtual Office テナントに管理者としてサインオンします。

1. アプリケーション パネルで **[Virtual Office Account Mgr (Virtual Office アカウント マネージャー)]** を選択します。

1. 管理する **[Business (ビジネス)]** アカウントを選択し、 **[Sign In (サインイン)]** をクリックします。

1. メニュー リストの **[ACCOUNTS]\(アカウント\)** タブをクリックします。

1. アカウントの一覧で **[Single Sign On (シングル サインオン)]** をクリックします。

1. [Authentication methods]\(認証方法\) の **[Single Sign On]\(シングル サインオン\)** を選択し、 **[SAML]** をクリックします。

1. **[SAML Single Sign-On]\(SAML シングル サインオン\)** セクションで、次の手順に従います。

    a. **[Sign In URL]\(サインイン URL\)** テキストボックスに、Azure portal からコピーした**ログイン URL** の値を貼り付けます。

    b. **[Sign Out URL]\(サインアウト URL\)** テキストボックスに、Azure portal からコピーした**ログアウト URL** の値を貼り付けます。

    c. **[Issuer URL]\(発行者 URL\)** テキストボックスに、Azure portal からコピーした、**Azure AD ID** の値を貼り付けます。

    d. **[Browse]\(参照\)** ボタンをクリックして、Azure portal からダウンロードした証明書をアップロードします。

    e. **[保存]** ボタンをクリックします。

### <a name="create-8x8-test-user"></a>8x8 のテスト ユーザーの作成

このセクションでは、8x8 で Britta Simon というユーザーを作成します。 [8x8 サポート チーム](https://www.8x8.com/about-us/contact-us)と連携して、8x8 プラットフォームにユーザーを追加してください。 シングル サインオンを使用する前に、ユーザーを作成し、有効化する必要があります。

## <a name="test-sso"></a>SSO のテスト

このセクションでは、アクセス パネルを使用して Azure AD のシングル サインオン構成をテストします。

アクセス パネル上で [8x8] タイルをクリックすると、SSO を設定した 8x8 に自動的にサインインします。 アクセス パネルの詳細については、[アクセス パネルの概要](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)に関する記事を参照してください。

## <a name="additional-resources"></a>その他のリソース

- [SaaS アプリと Azure Active Directory を統合する方法に関するチュートリアルの一覧](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Azure Active Directory でのアプリケーション アクセスとシングル サインオンとは](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Azure Active Directory の条件付きアクセスとは](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Azure AD で 8x8 を試す](https://aad.portal.azure.com/)

- [Microsoft Cloud App Security におけるセッション制御とは](https://docs.microsoft.com/cloud-app-security/proxy-intro-aad)

- [高度な可視性と制御によって 8x8 を保護する方法](https://docs.microsoft.com/cloud-app-security/proxy-intro-aad)