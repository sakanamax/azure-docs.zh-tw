---
title: "搭配 Linux 使用 Azure 檔案 | Microsoft Docs"
description: "了解如何透過 Linux 上的 SMB 掛接 Azure 檔案共用。"
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/20/2017
ms.author: renash
ms.openlocfilehash: cca0d315a815faca5db07099b8e8e451ef55fad5
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="use-azure-files-with-linux"></a>搭配 Linux 使用 Azure 檔案
[Azure 檔案服務](storage-files-introduction.md)是 Microsoft 易於使用的雲端檔案系統。 可以使用 [CIFS 核心用戶端](https://wiki.samba.org/index.php/LinuxCIFS)將 Azure 檔案共用掛接在 Linux 發行版本中。 本文將說明掛接 Azure 檔案共用的兩種方式：使用 `mount` 命令的隨選掛接，以及建立項目 `/etc/fstab` 的開機掛接。

> [!NOTE]  
> 若要在 Azure 區域之外掛接 Azure 檔案共用，例如內部部署或是在不同的 Azure 區域，作業系統必須支援 SMB 3.0 的加密功能。

## <a name="prerequisites-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a>以 Linux 掛接 Azure 檔案共用和 cifs-utils 套件的必要條件
* **挑選可以安裝 cifs-utils 套件的 Linux 發行版本。**  
    下列 Linux 發行版本適用於 Azure 資源庫：

    * Ubuntu Server 14.04+
    * RHEL 7+
    * CentOS 7+
    * Debian 8+
    * openSUSE 13.2+
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**已安裝 cifs-utils 套件。**  
    可使用套件管理員將 cifs-utils 套件安裝在所選擇的 Linux 發行版本上。 

    在 **Ubuntu** 和 **Debian 型**發行版本上，請使用 `apt-get` 封裝管理員：

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    在 **RHEL** 和 **CentOS** 上，請使用 `yum` 封裝管理員：

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    在 **openSUSE** 上，請使用 `zypper` 封裝管理員：

    ```
    sudo zypper install samba*
    ```

    在其他發行版本上，請使用適當的封裝管理員或[從來源編譯](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download)。

* <a id="smb-client-reqs"></a>**了解 SMB 用戶端需求。**  
    Azure 檔案服務可以透過 SMB 2.1 和 SMB 3.0 掛接。 對於來自用戶端內部部署或其他 Azure 區域的連線，Azure 檔案服務會拒絕 SMB 2.1 (或是沒有加密的 SMB 3.0)。 如果已針對儲存體帳戶啟用「需要安全傳輸」，則 Azure 檔案服務僅允許使用具有加密的 SMB 3.0 之連線。
    
    SMB 3.0 加密支援是在 Linux 核心版本 4.11 導入，並且針對熱門的 Linux 發行版本反向導入到舊版核心版本。 在本文件發行時，Azure 資源庫的下列發行版本支援此功能：

    - Ubuntu Server 16.04+
    - openSUSE 42.3+
    - SUSE Linux Enterprise Server 12 SP3+
    
    如果此處未列出您的 Linux 發行版本，您可以使用下列命令查看 Linux 核心版本：

    ```
    uname -r
    ```

* **對於掛接的共用決定目錄/檔案權限**：下列範例使用權限 `0777` 提供所有使用者的讀取、寫入和執行權限。 您可以視需要將它取代為其他 [chmod 權限](https://en.wikipedia.org/wiki/Chmod)。 

* **儲存體帳戶名稱**：若要掛接 Azure 檔案共用，您需要儲存體帳戶的名稱。

* **儲存體帳戶金鑰**：若要掛接 Azure 檔案共用，您需要主要 (或次要) 儲存體金鑰。 掛接目前不支援 SAS 金鑰。

* **請確定已開啟連接埠 445**：SMB 透過 TCP 通訊埠 445 進行通訊 - 請檢查您的防火牆不會將 TCP 通訊埠 445 從用戶端電腦封鎖。

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a>使用 `mount` 隨需掛接 Azure 檔案共用
1. **[在您的 Linux 發行版本上安裝 cifs-utils 封裝](#install-cifs-utils)**。

2. **建立掛接點的資料夾**：掛接點的資料夾可以在檔案系統上任何位置建立，但是常見慣例是在 `/mnt` 資料夾底下建立這個資料夾。 例如︰

    ```
    mkdir /mnt/MyAzureFileShare
    ```

3. **使用 mount 命令掛接 Azure 檔案共用**：請記得針對您的環境使用適當的資訊來取代 `<storage-account-name>`、`<share-name>`、`<smb-version>`、`<storage-account-key>` 和 `<mount-point>`。 如果您的 Linux 發行版本支援具有加密的 SMB 3.0 (請參閱[了解 SMB 用戶端需求](#smb-client-reqs)以取得詳細資訊)，請針對 `<smb-version>` 使用 `3.0`。 對於不支援具有加密的 SMB 3.0 之 Linux 發行版本，請針對 `<smb-version>` 使用 `2.1`。 請注意，Azure 檔案共用只能使用 SMB 3.0 掛接在 Azure 區域外部 (包括內部部署或不同的 Azure 區域)。 

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> <mount-point> -o vers=<smb-version>,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> 使用 Azure 檔案共用後，即可使用 `sudo umount <mount-point>` 取消掛接共用。

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a>使用 `/etc/fstab` 建立 Azure 檔案共用的持續掛接點
1. **[在您的 Linux 發行版本上安裝 cifs-utils 封裝](#install-cifs-utils)**。

2. **建立掛接點的資料夾**：掛接點的資料夾可以在檔案系統上任何位置建立，但是常見慣例是在 `/mnt` 資料夾底下建立這個資料夾。 每當您建立這個資料夾，請記下資料夾的完整路徑。 例如，下列命令會在 `/mnt` 底下建立新的資料夾 (路徑為完整路徑)。

    ```
    sudo mkdir /mnt/MyAzureFileShare
    ```

3. **使用下列命令將下列一行附加至 `/etc/fstab`**：請記得針對您的環境使用適當的資訊來取代 `<storage-account-name>`、`<share-name>`、`<smb-version>`、`<storage-account-key>` 和 `<mount-point>`。 如果您的 Linux 發行版本支援具有加密的 SMB 3.0 (請參閱[了解 SMB 用戶端需求](#smb-client-reqs)以取得詳細資訊)，請針對 `<smb-version>` 使用 `3.0`。 對於不支援具有加密的 SMB 3.0 之 Linux 發行版本，請針對 `<smb-version>` 使用 `2.1`。 請注意，Azure 檔案共用只能使用 SMB 3.0 掛接在 Azure 區域外部 (包括內部部署或不同的 Azure 區域)。 

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> <mount-point> cifs nofail,vers=<smb-version>,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> 您可以使用 `sudo mount -a` 在編輯 `/etc/fstab` 之後掛接 Azure 檔案共用而不需要重新開機。

## <a name="feedback"></a>意見反應
Linux 使用者，歡迎您提供相關資訊！

適用於 Linux 的 Azure 檔案使用者群組提供了一個論壇，讓您在 Linux 上評估並採用檔案儲存體之際，得以分享意見反應。 請寄電子郵件至 [Azure 檔案 Linux 使用者](mailto:azurefileslinuxusers@microsoft.com)，以加入使用者的群組。

## <a name="next-steps"></a>後續步驟
請參閱這些連結，以取得 Azure 檔案服務的詳細資訊。
* [Azure 檔案服務簡介](storage-files-introduction.md)
* [規劃 Azure 檔案部署](storage-files-planning.md)
* [常見問題集](../storage-files-faq.md)
* [疑難排解](storage-troubleshoot-linux-file-connection-problems.md)