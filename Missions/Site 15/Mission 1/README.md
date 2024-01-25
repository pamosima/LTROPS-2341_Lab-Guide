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
| vManage User     | user5                                                                |
| vManage Password | C1sco12345                                                           |

## Step 1: Attach device-template the to router

Your task is to attach a predefined device-template to the router with the required device variables. Use the prepared .csv file in this directory.

| Required parameters         | Value                                    |
| --------------------------- | ---------------------------------------- |
| id (Device Template ID)     | 6cff893d-d4ec-48fa-aa45-f50c565c1e61     |
| id (Device ID)              | C8K-C191341E-108D-5CDC-6220-BA6228D716A6 |
| system_host_name            | site-15-router-1                         |
| system_system_ip            | 10.255.255.15                            |
| system_site_id              | 15                                       |
| vpn0_if_ipv4_address        | 198.18.150.15/18                         |
| vpn20_if_ipv4_address       | 172.20.15.1/24                           |
| dhcp_vlan20_address_pool    | 172.20.15.0/24                           |
| dhcp_vlan20_default_gateway | 172.20.15.1                              |

:exclamation: :warning: Use a data source to get the id (Device Template ID) for the device-template **"C8Kv_Branch"**

## Step 2: Verification

Log into the vManage UI and navigate to Configuration -> Devices.
Verify if your Router is now successfully onboarded and in vManage mode:

Example Site-11:

<img src=../../img/sd-wan_mission-1.png/>

---

<div align="right">
  <a href='../Missions/README.md'>Prev: Missions</a> - <a href='../Mission 2/README.md'>Next: Mission 2</a>
</div>

---

<div align="center">
 Are you feeling stuck? Would you like a <a href='../../../Hints/1/Mission 1/README.md' target="_blank">hint</a> to help you out?
</div>
