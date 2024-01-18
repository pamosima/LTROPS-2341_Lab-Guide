# Mission 3: Add a new VPN to the router and add a new VLAN to the switch.

This mission is divided into two tasks and requires a few different steps:

- [Task 1: Create the needed SDWAN feature templates and assign them to your router](#task-1-create-the-needed-sdwan-feature-templates-and-assign-them-to-your-router)
  - Create a new SDWAN VPN feature template and a new SDWAN VPN interface feature template
  - Clone existing SDWAN device template and add the VPN feature, as well as the VPN interface feature template
  - Attach the new SDWAN device template to your router
- [Task 2: Create a new CLI template on the Catalyst Center and deploy it to your switch](#task-2-create-a-new-cli-template-on-the-catalyst-center-and-deploy-it-to-your-switch)
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
| vManage User     | user3                                                                |
| vManage Password | C1sco12345                                                           |

### DNACENTER (Catalyst Center)

| Specification | Details                                                                                     |
| ------------- | ------------------------------------------------------------------------------------------- |
| Provider      | cisco-en-programmability/dnacenter                                                          |
| Version       | 1.1.31-beta                                                                                 |
| Documentation | https://registry.terraform.io/providers/cisco-en-programmability/dnacenter/1.1.31-beta/docs |
| DNAC URL      | https://198.18.129.100                                                                      |
| DNAC User     | user3                                                                                       |
| DNAC Password | C1sco12345                                                                                  |

## Task 1: Create the needed SDWAN feature templates and assign them to your router

Your first task is to create a new SDWAN device template with a new VPN feature template and a new SDWAN VPN interface feature template. Then attach this new SDWAN device feature template to the router.

### Step 1: Create a new SDWAN VPN feature template

| Required parameters | Value         |
| ------------------- | ------------- |
| name                | site-13_vpn21 |
| description         | site-13_vpn21 |
| device_types        | ["C8000v"]    |
| vpn_id              | 21            |
| vpn_name            | 21            |

### Step 2: Create a new SDWAN VPN interface feature template

| Required parameters     | Value                 |
| ----------------------- | --------------------- |
| name                    | site-13_vpn21-eth     |
| description             | site-13_vpn21-eth     |
| device_types            | ["C8000v"]            |
| shutdown                | false                 |
| interface_name_variable | vpn21_if_name         |
| address_variable        | vpn21_if_ipv4_address |

### Step 3: Create a new SDWAN device feature template

| Required parameters | Value                                                  |
| ------------------- | ------------------------------------------------------ |
| name                | site-13                                                |
| description         | site-13                                                |
| device_type         | C8000v                                                 |
| device_role         | SDWAN Edge                                             |
| general_templates   | a list of the existing templates and the new templates |

### Step 4: Assign the new SDWAN device feature template to your router

| Required parameters         | Value                                    |
| --------------------------- | ---------------------------------------- |
| id (Device Template ID)     | 6cff893d-d4ec-48fa-aa45-f50c565c1e61     |
| id (Device ID)              | C8K-C74E1F90-C146-12BB-9B15-2542E9D20884 |
| system_host_name            | site-13-router-1                         |
| system_system_ip            | 10.255.255.13                            |
| system_site_id              | 13                                       |
| vpn0_if_ipv4_address        | 198.18.150.13/18                         |
| vpn20_if_ipv4_address       | 172.20.13.1/24                           |
| dhcp_vlan20_address_pool    | 172.20.13.0/24                           |
| dhcp_vlan20_default_gateway | 172.20.13.1                              |
| vpn_id                      | 21                                       |
| vpn_name                    | 21                                       |
| vpn21_if_name               | GigabitEthernet2.21                      |
| vpn21_if_ipv4_address       | 172.21.13.1/24                           |

### Step 5: Verification

Log into the vManage UI and navigate to Configuration -> Devices.
Verify if your Router is now successfully onboarded and in vManage mode:

Example Site-11:

<img src=../../img/sd-wan_mission-3.png/>

## Task 1: Create a new CLI template on the Catalyst Center and deploy it to your switch

Your task is to create a new CLI template on the Catalyst Center and deploy it to your switch

### Step 1: Create a configuration template project

| Required parameters | Value           |
| ------------------- | --------------- |
| name                | Site-13_Project |

### Step 2: Create a configuration template

| Required parameters | Value                                                 |
| ------------------- | ----------------------------------------------------- |
| name                | Site-13_DayN                                          |
| project_id          | $ID from the created template project                 |
| software_type       | IOS                                                   |
| device_types        | Switches and Hubs                                     |
| template_content    | Please find a simple example of the CLI template blow |

```
vlan 21
 name Data
interface range Gig1/0/2-8
 switchport mode access
 switchport access vlan 21
```

### Step 3: Create a new version of the configuration template

| Required parameters | Value                                       |
| ------------------- | ------------------------------------------- |
| template_id         | $ID from the created configuration template |

### Step 4: Deploy the template

| Required parameters   | Value                                       |
| --------------------- | ------------------------------------------- |
| hostname              | site-13-switch-1                            |
| force_push_template   | false                                       |
| is_composite          | false                                       |
| id                    | $ID from device_list "hostname.\*"          |
| type                  | MANAGED_DEVICE_UUID                         |
| versioned_template_id | $ID from the created configuration template |
| template_id           | $ID from the created configuration template |

## Step 5: Verification

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
