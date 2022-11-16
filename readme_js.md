# John Savill Video Notes

## Table of Contents

- [John Savill Video Notes](#john-savill-video-notes)
  - [Table of Contents](#table-of-contents)
  - [About](#about)
  - [Identity and Azure AD](#identity-and-azure-ad)
  - [Cost management](#cost-management)
  - [Tagging](#tagging)
  - [Regions, cloud and Availability Zones](#regions-cloud-and-availability-zones)
  - [Azure firewall](#azure-firewall)
  - [Azure DNS Services](#azure-dns-services)
  - [Vnet to on-prem](#vnet-to-on-prem)
  - [ExpressRoute](#expressroute)
  - [Storage](#storage)
    - [Performance tiers](#performance-tiers)

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

## Cost management

Inside the azure portal you can go into cost management and use the tools provided to allow you to have insight into where the costs are coming from.

Inside the cost management tool you can create a budget for example when a certain percentage of the budget is sent, send an email to a specific group so that you are always aware of what is being spent.

With the cost management tool you can also view cost forecasts which is an estimate of how much you will spend this month based on your previous usage, this will help with cost planning.

You can also use advisor recommendations which will help you to scale appropriately to your uses and minimise costs where neccesary.

## Tagging

Tags are an option to add some metadata to a resource, resource group or subscription this will allow you to easily find specific resources for example having a dev tag on a resource so that you know it is not contributing to the prod or the costcenter tag so finance knows what specific areas of the company are spending.

Using policies you can force tags to be added based on the definitions rules.

## Regions, cloud and Availability Zones

Regions are the geographic breakdown of the azure network for example west US and east US.

There are multiple clouds inside of Azure for example 'Azure china cloud' or 'Azure US Government cloud' these are used by the respective communities for example the us government use the US government cloud and not the public Azure instance.

Regions breakdown in to availability zones.

## Azure firewall

Azure firewall is deployed into a vNet into its own /26 subnet, this is an azure native firewall.

The firewall rules are different to NSG rules.

Rules:
    - Nat > DNAT
    - Network - Level 4 rules
    - Application - Level 7 Rules

Implemented by routing as the next hop in the routing table.

Best practice to have a firewall per region due to latency issues.

## Azure DNS Services

Azure has public and internal DNS Solutions.

A virtual network can be configured to automatically register any resource with the private DNS Zone.

If you want to talk to an Azure private zone from an on prem network you will need to set up some form of dns forwarding from azure.

## Vnet to on-prem

You will need a VPN Gateway, it is recommended for the Gateway subnet to be /27.

There are two types of VPN -
    - **Policy / Static routing**
      - This only supports 1 tunnel and only used on the basic VPN SKU
    - **Route based**
      - Any amount of tunnels
      - Point 2 Site VPN supported
      - ExpressRoute Supported

VPN connections are over the internet using IPSec.

Bandwidth is aggregate not per user.

## ExpressRoute

This is a private connection to the Azure backbone network a result of this is that communication to the network does not go over the internet.

Price is based on the speed and egress (Outbound data), ingress is always unlimited with no cost attached.

## Storage

### Performance tiers

The higher the tier you store the more it cools but the transactions are lower cost.

Tiers can be manually set but there are also automation options that can be set through the lifecycle management.

Lifecycle management rules can be set so that after X days a file will change the access tier automatically so that you aren't always paying the highest price.

