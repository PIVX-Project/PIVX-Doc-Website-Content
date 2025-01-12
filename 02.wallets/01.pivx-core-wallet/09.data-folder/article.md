---
title: 'Wallet Data Folder'
taxonomy:
    category:
        - 'PIVX Core Wallet'
    author:
        - 'The PIVX Team'
sitemap:
    lastmod: '11-01-2025 15:13'
autoseo:
    enabled: true
media_order: pivx-data-folder.png
---

### Default Data Folder

The PIVX Core Wallet stores it's data in a folder that is different from the installation folder. The default location varies based on your operating system.

*  **WINDOWS**: `C:\Users\%username%\AppData\Roaming\PIVX`
*  **MAC**: `~/Library/Application Support/PIVX` _or_ `~/.pivx`
*  **LINUX**: `~/.pivx`

### Custom Data Folder

When installing the QT wallet for the first time, you are presented with a dialog to set the PIVX Core Wallet data folder.

![pivx-data-folder](pivx-data-folder.png?classes=center,img-fluid,py-4 "pivx-data-folder")

If you later decide to change this data folder location, follow these steps:
1. **Close the Wallet**: Ensure that the PIVX wallet is not running.
3. **Create New Folder**: Create a new folder on your computer where you want to store the wallet data.
4. **Copy Wallet Files**: Copy the existing wallet files from the default or current location to the new custom folder.
5. **Delete Old Files**: Delete all the original files except pivx.conf
6. **Edit Configuration**: Edit the pivx.conf file in the original default folder with notepad or text editor adding the following line at the bottom:
  * `datadir=xxx` where xxx = complete path to the new data folder
8. **Start Wallet**: Start the PIVX wallet the usual way. It should now be using the custom data folder you specified.

#### Alternative Start Method
* **Add Startup Parameter**: Adjust the wallet startup command to include `-datadir=xxx` parameter, where xxx = complete path to new data folder.
