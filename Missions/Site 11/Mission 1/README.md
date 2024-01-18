# Mission 1: Deploy the SD-WAN cEdge

The first step is to configure the router as we need site connectivity to be able to onboard the switch and the wireless access-point later on.
Your SD-WAN Router is already reachable by vManage and all the required templates are already preconfigured. However - the router is in CLI-Mode and has therefore no configuration pushed to it.

## Terraform provider

Use the following terraform provider and make sure to use the specified version.

| Specification    | Details                                                              |
| ---------------- | -------------------------------------------------------------------- |
| Provider         | CiscoDevNet/sdwan                                                    |
| Version          | 0.3.3                                                                |
| Documentation    | https://registry.terraform.io/providers/CiscoDevNet/sdwan/0.3.3/docs |
| vManage URL      | https://198.18.128.2                                                 |
| vManage User     | user1                                                                |
| vManage Password | C1sco12345                                                           |

## Step 1: Attach device-template the to router

Your task is to attach a predefined device-template to the router with the required device variables.

| Required parameters         | Value                                    |
| --------------------------- | ---------------------------------------- |
| id (Device Template ID)     | 6cff893d-d4ec-48fa-aa45-f50c565c1e61     |
| id (Device ID)              | C8K-A0C346F4-1B42-C170-9D51-0AE31D6F2450 |
| system_host_name            | site-11-router-1                         |
| system_system_ip            | 10.255.255.11                            |
| system_site_id              | 11                                       |
| vpn0_if_ipv4_address        | 198.18.150.11/18                         |
| vpn20_if_ipv4_address       | 172.20.11.1/24                           |
| dhcp_vlan20_address_pool    | 172.20.11.0/24                           |
| dhcp_vlan20_default_gateway | 172.20.11.1                              |

## Step 2: Verification

Log into the vManage UI and navigate to Configuration -> Devices.
Verify if your Router is now successfully onboarded and in vManage mode:

Example Site-11:

<img src=../../img/sd-wan_mission-1.png/>

<div align="right">
  <a href='../Mission 2/README.md'>Next: Mission 2</a>
</div>
