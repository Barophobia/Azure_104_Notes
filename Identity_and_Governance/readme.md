# Identity & Governance

## Table of Contents

- [Identity & Governance](#identity--governance)
  - [Table of Contents](#table-of-contents)
  - ['New' Identity and Governance Portal](#new-identity-and-governance-portal)
  - [General](#general)
  - [Bulk import of users into AAD](#bulk-import-of-users-into-aad)
  - [Azure AD Joined Devices](#azure-ad-joined-devices)
    - [Joining a device](#joining-a-device)
  - [Azure Registered Devices](#azure-registered-devices)
    - [Registering a device](#registering-a-device)
  - [Azure Multi-Factor Authentication (MFA)](#azure-multi-factor-authentication-mfa)
    - [How to enable MFA](#how-to-enable-mfa)
  - [Azure Self-Service Password Reset (SSPR)](#azure-self-service-password-reset-sspr)
    - [Enabling SSPR](#enabling-sspr)


## 'New' Identity and Governance Portal

Whilst this is being written there is a new portal that can be used to manage security, Identity and governance named 'Entra', this is currently in preview (27-10-22) depending on when you see this it may be a production feature and required for the exam. Link: [Entra Portal](https://entra.microsoft.com)

## General

Azure admins implement, manage, monitor and organise the azure environment.

Cloud Identity - A Local azure user or external azure AD user

Hybrid Identity - A directory synced user

Guest Identity - External users invited to the domain

## Bulk import of users into AAD

To bulk import go to the Azure AD portal > Users and go to the 3 dots menu and choose bulk operations shown in the image below.
![x](images/bulk_create_option.png)

Once you select the bulk add operation you can download the CSV file provided by microsoft and edit as needed.
![x](images/bulk_create_users_form.png)

The required values have 'Required' in the header of the table.

## Azure AD Joined Devices

This is a device that has been joined to Azure AD using an organizational account. This will require the user to use their AD username and password when logging into their device.

This is suitable for both cloud and hybrid environments.

This method is supported by All versions of Windows 10 and 11 except Home edition.

### Joining a device

You can join a device that has already been setup or used by going into the settings and selecting 'accounts' then 'Access work or school', this will bring up the screen below.

![x](images/ad_join_settings.png)

Once you have clicked 'Connect' you will need to click 'Join this device to Azure Active Directory' shown in the screenshot below.

![x](images/join_aad_setting.png)

Now you will be asked for your account details and to check that you are joining the correct domain.

Once you click 'Join' your device will be added to the Azure Active Directory and is can be fully managed by that domain.

## Azure Registered Devices

This is used to support users for BYOD (Bring Your Own Device) or a mobile device. In this situation it is recommended to use this when the user wants to use their personal device and wants to retain ownership.

This is a device that is registered with Azure AD but does not require an organizational account to login.

### Registering a device

You can register a device that has already been setup or used by going into the settings and selecting 'accounts' then 'Access work or school', this will bring up the screen below.

![x](images/ad_join_settings.png)

Once you have clicked 'Connect' enter your email address and password to the domain you are trying to join and sign-in, once this is complete the device will be registered.

## Azure Multi-Factor Authentication (MFA)

Multi-factor is used as an additional authentication layer during a sign-in event. An example of this is when a user is prompted to input a code sent to their mobile device.

MFA and conditional access policies give the flexibility to require MFA from users in specific circumstances.

The following additional forms of verification can be used with Azure AD Multi-Factor Authentication:

- Microsoft Authenticator app
- Windows Hello for Business
- FIDO2 security key
- OATH hardware token (preview)
- OATH software token
- SMS
- Voice call

To enable MFA there are some pre-requisites:

- A working Azure AD Tenant with Azure AD Premium P1 license
- An account with 'Conditional access administrator', 'Security Administrator' or 'Global adminsitrator' privileges.

### How to enable MFA

## Azure Self-Service Password Reset (SSPR)

SSPR allows users to change/reset their own account password without having to log a call with the local helpdesk.

To enable SSPR for the environment there are some pre-requisites:

- A working Azure AD Tenant, with a free or trial license.*
- An account with Global Administrator or Authentication Policy Administrator

*Password change is supported in the free tier but password reset is not. For on-prem writeback a Azure AD Premium P1 license is requried.

### Enabling SSPR

To enable SSPR go to the Azure AD blade in the portal and select 'Password Reset' > 'Properties'

Under 'Self service password reset enabled' select the option required - 'None', 'Selected' or 'All'

If you choose 'selected' you will need to choose the groups that are allowed to use SSPR, shown below.

![x](images/enable_sspr.png)
