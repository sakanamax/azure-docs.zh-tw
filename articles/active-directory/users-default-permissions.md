---
title: "在 Azure Active Directory 中比較預設使用者權限 | Microsoft Docs"
description: "比較成員、來賓、應用程式擁有者和群組擁有者權限"
services: active-directory
documentationcenter: 
author: curtand
manager: mtillman
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 01/29/2018
ms.author: curtand
ms.reviewer: vincesm
ms.openlocfilehash: 83d23323f050f670680499ecb428c07c94096418
ms.sourcegitcommit: 9d317dabf4a5cca13308c50a10349af0e72e1b7e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2018
---
# <a name="default-user-permissions-in-azure-active-directory"></a>Azure Active Directory 中的預設使用者權限

在 Azure Active Directory (Azure AD) 中，所有使用者都會獲得一組預設權限。 使用者的存取權包含使用者類型、其[角色成員資格](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-assign-role-azure-portal)，以及個別物件的擁有權。 本文說明這些預設權限，並包含成員與來賓使用者預設值的比較。

## <a name="member-and-guest-users"></a>成員和來賓使用者
使用者所收到的預設權限集取決於使用者是租用戶的原生成員 (成員使用者)，還是 B2B 共同作業來賓 (來賓使用者)。 如需 B2B 共同作業的詳細資訊，請參閱[什麼是 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)。 
* 成員使用者可以註冊應用程式、管理自己的設定檔相片和行動電話號碼、變更自己的密碼，以及邀請 B2B 來賓。 此外，使用者還可讀取所有目錄資訊 (但有一些例外狀況)。 
* Azure AD B2B 來賓使用者具有受限的目錄權限。 例如，來賓使用者無法瀏覽其本身的設定檔資訊以外的租用戶資訊。 不過，來賓使用者可藉由提供使用者主體名稱或 objectId 來擷取另一位使用者的相關資訊。 來賓無法檢視其他租用戶物件 (例如群組和應用程式) 的任何相關資訊。

預設會限制來賓的預設權限。 您可將來賓新增至系統管理員角色，將角色內含的完整讀取和寫入權限授予他們。 另外還有一項可用限制，就是來賓邀請其他來賓的能力。 將 [來賓可邀請] 設為 [否]，可防止來賓邀請其他來賓。 請參閱[委派 B2B 共同作業的邀請](active-directory-b2b-delegate-invitations.md)以了解詳情。 若要將與成員使用者相同的預設權限授予來賓使用者，請將 [來賓使用者權限受限] 設定為 [否]。 此設定預設會將所有成員使用者權限授予來賓使用者，以及允許將來賓新增至系統管理角色。

## <a name="compare-member-and-guest-default-permissions"></a>比較成員與來賓預設的權限

**領域** | **成員使用者權限** | **來賓使用者權限**
------------ | --------- | ----------
使用者和連絡人 | 讀取使用者和連絡人的所有公用屬性<br>邀請來賓<br>變更自己的密碼<br>管理自己的行動電話號碼<br>管理自己的相片<br>使自己的重新整理權杖失效 | 讀取自己的屬性<br>讀取顯示名稱、電子郵件、登入名稱、相片、使用者主體名稱，以及其他使用者和連絡人的使用者類型屬性<br>變更自己的密碼
群組   | 建立安全性群組<br>建立 Office 365 群組<br>讀取群組的所有屬性<br>讀取非隱藏的群組成員資格<br>讀取已加入群組的隱藏 Office 365 群組成員資格<br>管理擁有之群組的屬性、擁有權及成員資格<br>將來賓新增至擁有的群組<br>管理動態成員資格設定<br>刪除擁有的群組<br>還原擁有的 Office 365 群組 | 讀取群組的所有屬性<br>讀取非隱藏的群組成員資格<br>讀取已加入群組的隱藏 Office 365 群組成員資格<br>管理擁有的群組<br>將來賓新增至擁有的群組 (如果允許)<br>刪除擁有的群組<br>還原擁有的 Office 365 群組           
[應用程式] | 註冊 (建立) 新的應用程式<br>讀取已註冊和企業應用程式的屬性<br>管理擁有之應用程式的應用程式屬性、指派及認證<br>建立或刪除使用者的應用程式密碼<br>刪除擁有的應用程式<br>還原擁有的應用程式 | 讀取已註冊和企業應用程式的屬性<br>管理擁有之應用程式的應用程式屬性、指派及認證<br>刪除擁有的應用程式<br>還原擁有的應用程式
裝置 | 讀取裝置的所有屬性<br>管理擁有之裝置的所有屬性<br> | 沒有權限<br>刪除擁有的裝置<br>
目錄 | 讀取所有公司資訊<br>讀取所有網域<br>讀取所有夥伴合約 | 讀取顯示名稱和已驗證的網域
角色和範圍 | 讀取所有系統管理角色和成員資格<br>讀取系統管理單元的所有屬性和成員資格 | 沒有權限              
訂用帳戶 | 讀取所有訂用帳戶<br>啟用服務方案成員 | 沒有權限
原則 | 讀取原則的所有屬性<br>管理擁有之原則的所有屬性 | 沒有權限

## <a name="to-restrict-the-default-permissions-for-member-users"></a>限制成員使用者的預設權限


您可利用下列方式限制成員使用者的預設權限。 如需詳細資訊，請參閱 [Azure Active Directory 中的應用程式、權限及同意](active-directory-apps-permissions-consent.md)。

權限 | 設定說明
---------- | ------------
建立安全性群組的能力 | 將此選項設定為 [否] 可防止使用者建立安全性群組。 全域管理員和使用者帳戶管理員仍可建立安全性群組。 請參閱[用於進行群組設定的 Azure Active Directory Cmdlet](active-directory-accessmanagement-groups-settings-cmdlets.md) 以了解詳情。
建立 Office 365 群組的能力 | 將此選項設定為 [否] 可防止使用者建立 Office 365 群組。 將此選項設定為 [部分] 可允許一組特定使用者建立 Office 365 群組。 全域管理員和使用者帳戶管理員仍可建立 Office 365 群組。 請參閱[用於進行群組設定的 Azure Active Directory Cmdlet](active-directory-accessmanagement-groups-settings-cmdlets.md) 以了解詳情。
同意應用程式的能力 | 將此選項設定為 [否] 可防止使用者同意應用程式。 全域管理員仍可同意應用程式。 如需詳細資訊，請參閱 [Azure Active Directory 中的應用程式、權限及同意](active-directory-apps-permissions-consent.md)。
將資源庫應用程式新增至存取面板的能力 | 將此選項設為 [否] 可防止使用者在其存取面板中新增資源庫應用程式。
註冊 (建立) 應用程式的能力 | 將此選項設為 [否] 可防止非系統管理員建立應用程式。 全域管理員仍可建立應用程式。 如需詳細資訊，請參閱 [Azure Active Directory 中的應用程式、權限及同意](active-directory-apps-permissions-consent.md)。
系統管理員與具備「來賓邀請者角色」的使用者可邀請來賓 | 將此選項設為 [否] 可防止所有使用者邀請來賓。 請參閱「設定成員使用者的預設權限」。 如需詳細資訊，請參閱 [Azure Active Directory 中的應用程式、權限及同意](active-directory-apps-permissions-consent.md)。
成員可邀請來賓 | 將此選項設為 [否] 可防止使用者邀請來賓。 全域管理員、使用者帳戶管理員及來賓邀請者仍可邀請來賓。 如需詳細資訊，請參閱 [Azure Active Directory 中的應用程式、權限及同意](active-directory-apps-permissions-consent.md)。
限制 Azure AD 系統管理入口網站的存取 | 將此選項設定為 [否] 可防止使用者存取 Azure Active Directory 入口網站。
讀取其他使用者的能力 | 如需詳細資訊，請參閱 [Azure Active Directory 中的應用程式、權限及同意](active-directory-apps-permissions-consent.md)。

## <a name="object-ownership"></a>物件擁有權

### <a name="application-registration-owner-permissions"></a>應用程式註冊擁有者權限
當使用者註冊應用程式時，系統會將他們自動新增為應用程式的擁有者。 身為擁有者的他們可以管理應用程式的中繼資料，例如應用程式要求的名稱和權限。 他們也可以管理應用程式的租用戶專屬設組態定，例如 SSO 組態和使用者指派。 擁有者也可以新增或移除其他擁有者。 不同於全域管理員，擁有者只能管理自己的應用程式。 若要指派應用程式註冊擁有者，請參閱 [Azure Active Directory 應用程式註冊](active-directory-app-registration.md)。

<!-- ### Enterprise application owner permissions

When a user adds a new enterprise application, they are automatically added as an owner for the tenant-specific configuration of the application. As an owner, they can manage the tenant-specific configuration of the application, such as the SSO configuration, provisioning, and user assignments. An owner can also add or remove other owners. Unlike Global Administrators, owners can manage only the applications they own. <!--To assign an enterprise application owner, see *Assigning Owners for an Application*.-->

### <a name="group-owner-permissions"></a>群組擁有者權限

當使用者建立群組時，他們會自動新增為該群組的擁有者。 身為擁有者的他們可以管理群組的屬性 (例如名稱)，以及管理成員資格。 擁有者也可以新增或移除其他擁有者。 不同於全域管理員和使用者帳戶管理員，擁有者只能管理自己的群組。 若要指派群組擁有者，請參閱[管理群組的擁有者](active-directory-accessmanagement-managing-group-owners.md)。

## <a name="next-steps"></a>後續步驟

* 若要深入了解如何變更 Azure 訂用帳戶的系統管理員，請參閱 [如何新增或變更 Azure 系統管理員角色](../billing-add-change-azure-subscription-administrator.md)
* 若要深入了解如何在 Microsoft Azure 中控制資源存取，請參閱 [了解 Azure 中的資源存取](active-directory-understanding-resource-access.md)
* 如需 Azure Active Directory 如何與您 Azure 訂用帳戶產生關聯的詳細資訊，請參閱 [Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](active-directory-how-subscriptions-associated-directory.md)
* [管理使用者](active-directory-create-users.md)
