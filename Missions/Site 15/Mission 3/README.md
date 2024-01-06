# Mission 3: Add a new VPN to the router and add a new VLAN to the switch.

This mission requires a few different steps:

- Create a new SDWAN VPN feature template and a new SDWAN VPN interface feature template
- Clone existing SDWAN device template and add the VPN feature, as well as the VPN interface feature template
- Attach the new SDWAN device template to your router
- Create a new CLI template on the Catalyst Center
- Deploy the CLI template to your switch

## Terraform providers

Use the following terraform providers and make sure to use the specified version.

### SDWAN

| Specification    | Details                                                              |
| ---------------- | -------------------------------------------------------------------- |
| Provider         | CiscoDevNet/sdwan                                                    |
| Version          | 0.3.3                                                                |
| Documentation    | https://registry.terraform.io/providers/CiscoDevNet/sdwan/0.3.3/docs |
| vManage URL      | https://198.18.128.2                                                 |
| vManage User     | user5                                                                |
| vManage Password | C1sco12345                                                           |

### DNACENTER (Catalyst Center)

| Specification | Details                                                                                     |
| ------------- | ------------------------------------------------------------------------------------------- |
| Provider      | cisco-en-programmability/dnacenter                                                          |
| Version       | 1.1.31-beta                                                                                 |
| Documentation | https://registry.terraform.io/providers/cisco-en-programmability/dnacenter/1.1.31-beta/docs |
| DNAC URL      | https://198.18.129.100                                                                      |
| DNAC User     | user5                                                                                       |
| DNAC Password | C1sco12345                                                                                  |

## Step 1: Create a new SDWAN feature templates and assign them to your router

Your task is to create a new SDWAN device template with a new VPN feature template and a new SDWAN VPN interface feature template. Then attach it to the router with the required device variables.

| Required parameters         | Value                                    |
| --------------------------- | ---------------------------------------- |
| device_template_id          | 6cff893d-d4ec-48fa-aa45-f50c565c1e61     |
| device_id                   | C8K-A0C346F4-1B42-C170-9D51-0AE31D6F2450 |
| system_host_name            | site-15-router-1                         |
| system_system_ip            | 10.255.255.15                            |
| system_site-id              | 15                                       |
| vpn0_if_ipv4_address        | 198.18.150.15/18                         |
| vpn20_if_ipv4_address       | 172.20.15.1/24                           |
| dhcp_vlan20_address_pool    | 172.20.15.0/24                           |
| dhcp_vlan20_default_gateway | 172.20.15.1                              |
| vpn_id                      | 21                                       |
| vpn_name                    | 21                                       |
| vpn21_if_name               | GigabitEthernet2.21                      |
| vpn21_if_ipv4_address       | 172.21.15.1/24                           |

## Step 2: Verification

Log into the vManage UI and navigate to Configuration -> Devices.
Verify if your Router is now successfully onboarded and in vManage mode:

Example Site21:

<img src=../../img/sd-wan.jpg/>

## Step 3: Create a new CLI template on the Catalyst Center and deploy it to your switch

Your task is to create a new CLI template on the Catalyst Center and deploy it to your switch

| Required parameters | Value                              |
| ------------------- | ---------------------------------- |
| site_name           | Site-15                            |
| switch_hostname     | site-15-switch-1                   |
| device_uuid         | $ID from device_list "hostname.\*" |

Please find a simple example of the CLI template blow:

```
vlan 21
 name Data
interface range Gig1/0/2-8
 switchport mode access
 switchport access vlan 21
```

## Step 4: Verification

Log into the Catalyst Center UI and navigate to Tools -> Command Runner.
Select your switch and run the following command:

```
show vlan
```

Verify if vlan has been created and if it's assigned to the interfaces Gig1/0/2-8.

<img src=../../img/show_vlan.png/>

<div align="right">
  <a href='../Mission 2/README.md'>Prev: Mission 2</a>
</div>
