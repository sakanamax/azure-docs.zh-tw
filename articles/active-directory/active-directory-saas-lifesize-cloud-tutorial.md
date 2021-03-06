---
title: "教學課程：Azure Active Directory 與 Lifesize Cloud 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Lifesize Cloud 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 47ae2c59d672c00b466d13aad1d304f4669a38c7
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a>教學課程：Azure Active Directory 與 Lifesize Cloud 整合

在本教學課程中，您會了解如何整合 Lifesize Cloud 與 Azure Active Directory (Azure AD)。

Lifesize Cloud 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 Lifesize Cloud 的人員
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Lifesize Cloud (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Lifesize Cloud 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Lifesize Cloud 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二項主要的基本工作組成：

1. 從資源庫新增 Lifesize Cloud
2. 設定並測試 Azure AD 單一登入

## <a name="adding-lifesize-cloud-from-the-gallery"></a>從資源庫新增 Lifesize Cloud
若要設定將 Lifesize Cloud 整合到 Azure AD 中，您需要從資源庫將 Lifesize Cloud 新增到受控 SaaS 應用程式清單。

**若要從資源庫新增 Lifesize Cloud，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![[應用程式]][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![[應用程式]][3]

4. 在搜尋方塊中，輸入 **Lifesize Cloud**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. 在結果面板中，選取 [Lifesize Cloud]，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Lifesize Cloud 搭配運作的 Azure AD 單一登入。

若要讓單一登入能夠運作，Azure AD 必須知道 Lifesize Cloud 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者與 Lifesize Cloud 中的相關使用者之間建立連結關聯性。

在 Lifesize Cloud 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。

若要設定及測試與 Lifesize Cloud 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Lifesize Cloud 測試使用者](#creating-a-lifesize-cloud-test-user)** - 使 Lifesize Cloud 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您將在 Azure 入口網站中啟用 Azure AD 單一登入，並在 Lifesize Cloud 應用程式中設定單一登入。

**若要使用 Lifesize Cloud 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [Lifesize Cloud] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. 在 [Lifesize Cloud 網域及 URL] 區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    a. 在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://login.lifesizecloud.com/ls/?acs`

    b. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://login.lifesizecloud.com/<companyname>`

     
4. 勾選 [顯示進階的 URL 設定]，然後執行下列步驟：    
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    在 [轉送狀態] 文字方塊中，輸入使用下列模式的 URL：`https://webapp.lifesizecloud.com/?ent=<identifier>`
   
   > [!NOTE] 
   >請注意這些不是真正的值。 您必須使用實際的登入 URL、轉送狀態及識別碼來更新這些值。 連絡 [Lifesize Cloud 用戶端支援小組](https://www.lifesize.com/support)，以取得登入 URL 和識別碼值，以及 SSO 設定 (本教學課程後面部分將說明) 中的 [轉送狀態] 值。

4. 在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. 在 [Lifesize Cloud 設定] 區段中，按一下 [設定 Lifesize Cloud] 以開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 **SAML 實體識別碼和 SAML 單一登入服務 URL**。

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. 若要取得為您的應用程式設定的 SSO，請使用系統管理員權限登入 Lifesize Cloud 應用程式。

8. 在右上角按一下您的名稱，然後按一下 [進階設定]。
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. 在 [進階設定] 中，現在按一下 [SSO 組態] 連結。 這會開啟您的執行個體的 [SSO 設定] 頁面。
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. 現在設定 SSO 組態 UI 中的下列值。    
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    a. 在 [識別提供者簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。

    b.  在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。

    c. 在從 Azure 入口網站下載的記事本檔案中開啟您的 base-64 編碼憑證，將憑證的內容複製到剪貼簿，再貼到 [X.509 憑證]  文字方塊。
  
    d. 在 [名字] 文字方塊的 SAML 屬性對應中，輸入以下格式的值：**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**
    
    e. 在 [姓氏] 文字方塊的 SAML 屬性對應中，輸入以下格式的值：**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**
    
    f. 在 [電子郵件] 文字方塊的 SAML 屬性對應中，輸入以下格式的值：**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**

11. 若要檢查組態，您可以按一下 [測試] 按鈕。
   
    >[!NOTE]
    >為使測試成功，您需要在 Azure AD 中完成組態精靈，同時提供存取權給可執行測試的使用者或群組。

12. 檢查 [啟用 SSO] 按鈕以啟用 SSO。

13. 現在按一下 [更新] 按鈕，以儲存所有設定。 這會產生 RelayState 值。 複製文字方塊中產生的 RelayState 值，貼到 [Lifesize Cloud 網域及 URL] 區段下方的 [轉送狀態] 文字方塊。 

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b. 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下頁面底部的 [新增] 。
 
### <a name="creating-a-lifesize-cloud-test-user"></a>建立 Lifesize Cloud 測試使用者

在本節中，您要在 Lifesize Cloud 中建立名為 Britta Simon 的使用者。 Lifesize Cloud 支援自動使用者佈建。 在 Azure AD 驗證成功後，使用者將自動佈建於應用程式中。 

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您將把 Lifesize Cloud 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派給 Lifesize Cloud，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Lifesize Cloud]。 

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

按一下存取面板中的 [Lifesize Cloud] 圖格，應會顯示 Lifesize Cloud 應用程式的登入頁面。
如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

