# DISCLAIMER
This project and all contained code is provided as-is with no guarantee or warranty concerning the usability or impact on systems. This content may be used, distributed, and modified, provided all parties involved agree that Microsoft and Microsoft Partners are not responsible for the produced outcome. Microsoft will not provide any support through any means.

# Apps Admin Center Health Check for Device Onboarding
This health check is designed to help identify devices that are not appearing in the Apps Admin Center Inventory page. The health check is compiled as a [Configuration Baseline](https://docs.microsoft.com/en-us/mem/configmgr/compliance/deploy-use/create-configuration-baselines#configuration-baselines) to be deployed using Microsoft Endpoint Configuration Manager.

## Importing the Configuration Baseline
1. Download the latest version of the **[Apps Admin Center Health Check for Device Onboarding.cab](https://github.com/bobclements-msft/M365A-AAC-Device-Onboarding/raw/main/Apps%20Admin%20Center%20Health%20Check%20for%20Device%20Onboarding.cab)**.
2. Open the **Configuration Manager** console.
3. From the **Assets and Compliance** workspace, expand **Compliance Settings**.
4. Right-click on **Configuration Baselines** and select **Import Configuration Data**.
5. On the **Import Configuration Data** Wizard, click **Add** and select **Apps Admin Center Health Check for Device Onboarding.cab**. 
6. Click **Yes** on the publisher notification.
7. With the baseline selected, click **Next**.
8. On the **Summary** page, confirm the Configuration Baseline and Configuration Items match the following list. Click **Next** to complete the import.
    - Configuration Baselines (1)
      - Apps Admin Center Health Check for Device Onboarding
    - Configuration Items (5)
      - M365A AAC - Onboarding - AutoProvisioning
      - M365A AAC - Onboarding - Minimum Office Version
      - M365A AAC - Onboarding - Scheduled Task
      - M365A AAC - Onboarding - TenantAssociationKey
      - M365A AAC - Inventory - Inventory File
      - M365A AAC - ServicingProfile - Update Policies
9. On the Confirmation page, click **Close**.

## Automatic Remediation - TenantAssociationKey
The following configuration item contains a remediation script:
  - M365A AAC – Onboarding – TenantAssociationKey
The script will stamp your TenantAssociationKey in the proper location and force the device to checkin with the service. If you choose to enable automatic remediation you will need to update configuration item remediation script with your TenantAssociationKey, which can be retrieved by navigating to https://config.office.com/ and clicking on **Settings**.

_**WARNING:**_ **DO NOT generate a new key**. Simply copy the existing key and paste it into the configuration item remediation script. Generating a new key will break communication with existing devices until they receive the updated key.

# Apps Admin Center Health Check for Servicing Profiles
This health check is designed to help identify devices that are not appearing in the Apps Admin Center Servicing Profile page and/or processing the Servicing Profile. The health check is compiled as a [Configuration Baseline](https://docs.microsoft.com/en-us/mem/configmgr/compliance/deploy-use/create-configuration-baselines#configuration-baselines) to be deployed using Microsoft Endpoint Configuration Manager.

## Importing the Configuration Baseline
1. Download the latest version of the **[Apps Admin Center Health Check for Servicing Profiles.cab](https://github.com/bobclements-msft/M365A-AAC-Device-Onboarding/raw/main/Apps%20Admin%20Center%20Health%20Check%20for%20Servicing%20Profiles.cab)**.
2. Open the **Configuration Manager** console.
3. From the **Assets and Compliance** workspace, expand **Compliance Settings**.
4. Right-click on **Configuration Baselines** and select **Import Configuration Data**.
5. On the **Import Configuration Data** Wizard, click **Add** and select **Apps Admin Center Health Check for Servicing Profilesg.cab**. 
6. Click **Yes** on the publisher notification.
7. With the baseline selected, click **Next**.
8. On the **Summary** page, confirm the Configuration Baseline and Configuration Items match the following list. Click **Next** to complete the import.
    - Configuration Baselines (1)
      - Apps Admin Center Health Check for Servicing Profiles
    - Configuration Items (1)
      - M365A AAC - ServicingProfile - Update Policies
9. On the Confirmation page, click **Close**.

# Importing Baseline Updates
Rrefer to the [Change Log](https://github.com/bobclements-msft/M365A-AAC-Device-Onboarding#change-log) section for updates to this project. If a new version of the Configuration Baseline is published, use the following steps to update your environment.
1. Download the latest version of the baseline you wish to update.
2. Open the **Configuration Manager** console.
3. From the **Assets and Compliance** workspace, expand **Compliance Settings**.
4. Right-click on **Configuration Baselines** and select **Import Configuration Data**.
5. On the **Import Configuration Data** Wizard, click **Add** and select cab file for the baseline you are importing. 
6. Click **Yes** on the publisher notification.
7. With the baseline selected, click **Next**.
8. On the **Summary** page, confirm the Configuration Baseline and Configuration Items are correct. Click **Next** to complete the import. 

If you receive an error message during the import process you can dismiss the prompt. Select the **Configuration Items** node and confirm the CI versions match those shown in the change log for the baseline you are importing.

# PowerShell Execution Policy
The configuration items contained in these baselines use PowerShell scripts. These scripts are not signed as part of this offering. Before deploying the baseline consider the following options:

- Configure the [PowerShell execution policy](https://docs.microsoft.com/en-us/mem/configmgr/core/clients/deploy/about-client-settings#powershell-execution-policy) in Client Settings to bypass sript signing requirements.
- [Sign the scripts](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_signing?view=powershell-7.1) used in each configuration item.

# Deploying the Configuration Baseline
1. From the **Assets and Compliance** workspace, expand **Compliance Settings** > **Configuration Baselines**.
2. Right-click on the new baseline and select **Deploy**.
3. On the deployment dialog window, select the appropriate values and click **OK**. 
    - Check the boxes for automatic remediation as appropriate for your environment. Consider deploying without remediation first to monitor impacted devices, then enable remediation after 1-2 days.
    - Select the device collection containing devices that require detection and remediation.
    - Set the deployment schedule appropriately for your environment.

# Log Collection
An application is provided that can be imported and deployed to target devices for collecting logs relative to onboarding.

## Application Import (CollectSMLogs)
1. Download **[MECM Application - M365 Apps - CollectSMLogs.zip](https://github.com/bobclements-msft/M365A-AAC-Device-Onboarding/raw/main/MECM%20Application%20-%20M365%20Apps%20-%20CollectSMLogs.zip)** and extract the contents to your Configuration Manager source package location.
2. Open the **Configuration Manager** console.
3. From the **Software Library** workspace, right-click on **Applications** and select **Import Application**.
4. On the Import Application Wizard, click **Browse** and select **M365 Apps - CollectSMLogs.zip** (contained in the original ZIP file). 
5. Click **Next** on the publisher notification.
6. On the **File Content** page, click **Next**.
7. On the **Summary** page, click **Next**.
8. On the **Completion** page, click **Close**.

## Application Deployment (CollectSMLogs)
1. From the **Software Library** workspace, expand **Application Management** > **Applications**.
2. Right-click on the **M365 Apps - CollectSMLogs** application and select **Distribute Content**.
3. Complete the Distribute Content Wizard, adding the content to all DPs that will be in scope for delivering this application.
4. Right-click on the **M365 Apps - CollectSMLogs** application and select **Deploy**. 
5. Complete the Deploy Software Wizard, targeting 2-3 devices identified by the Apps Admin Center health check baseline as non-compliant.

Following execution, the logs can be collected under **%windir%\Temp\ officesvcmgr_computername.zip**. If you need to rerun the application, make sure the zip file does not exist or has been renamed and rerun an application evaluation cycle.

# Change Log (sorted newest first)
- 03.08.21
    - Scheduled Task CI renamed and updated to report compliant if the task has not executed yet.
        | Configuration Item                        | Version |
        |-------------------------------------------|---------|
        | M365A AAC - Onboarding - Scheduled Task   | 5       |
    - Update Policies CI moved into a dedicated Servicing Profiles baseline to reduce the # of devices reporting non-compliant in environments where Inventory has been enabled but Servicing Profiles have not.

        | Configuration Baseline                                 | Version |
        |--------------------------------------------------------|---------|
        | Apps Admin Center Health Check for Device Onboarding   | 2       |
        | Apps Admin Center Health Check for Servicing Profiles  | 1       |
    - README.md updated to reflect the latest baseline changes.

- 03.04.21
    - Updated the AutoProvisioning CI for improved accuracy.
        | Configuration Item                        | Version |
        |-------------------------------------------|---------|
        | M365A AAC - Onboarding - AutoProvisioning | 8       |
        
- 02.25.21
    - Initial release
        | Configuration Item                              | Version |
        |-------------------------------------------------|---------|
        | M365A AAC - Onboarding - AutoProvisioning       | 7       |
        | M365A AAC - Onboarding - Minimum Office Version | 9       |
        | M365A AAC - Onboarding - TenantAssociationKey   | 9       |
        | M365A AAC - Inventory - Inventory File          | 4       |
        | M365A AAC - ServicingProfile - Scheduled Task   | 2       |
        | M365A AAC - ServicingProfile - Update Policies  | 2       |
