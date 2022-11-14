# John Savill Video Notes

## Table of Contents

- [Table of Contents](#table-of-contents)

## About

Notes taken from this video - [https://www.youtube.com/watch?v=VOod_VNgdJk&list=PLlVtbbG169nGlGPWs9xaLKT1KfwqREHbs](AZ-104 Microsoft Azure Administrator Associate Certification SUPER Study Cram)

## Identity and Azure AD

Azure AD is the Identity provider for the cloud services and communicates in cloud protocols for example SAML, OAUTH. These protocols work well over HTTPS.

Restful API's can be utilised to take advantage of the previously mentioned protocols and services.

Azure AD is not AD in the cloud as the on site AD uses different protocols with different capabilities, but you do have the option to use AD Connect so that you can replicate the environment into the Azure AD and leverage other options like SAAS. In the portal you can look at a user and see the status of 'directory synced' to see if the user is replicated from an on site AD.

You can add your own custom domain to your tenant for example - company.com, by default it will be x.onmicrosoft.com.

You have the option to customise the login portal with 'company branding' for example a company logo or a background when logging in.

Guest accounts allow you to invite someone external into your tenant.

You can bulk invite, create and delete inside the portal or powershell.

When giving permissions, ideally you want to create the correct groups required and then give users access based on those groups and not each individual user as this requires a lot more effort and leads to config stray.
You can use dynamic membership rules to automatically grant access to groups based on whatever syntax you set within the options.

Registered devices allow a device to be known and managed by a tenant for example using intune.

Joined devices grant all the options of a registered device but also allows the user to login using their AAD account.

