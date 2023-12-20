# Mission 1: Deploy the SD-WAN cEdge

The first step is to configure the router as we need site connectivity to be able to onboard the switch and the wireless access-point later on.
Your SD-WAN Router is already reachable by vManage and all the required templates are already preconfigured. However - the router is in CLI-Mode and has therefore no configuration pushed to it.

## Terraform provider

Use the following terraform provider and make sure to use the specified version.

| Specification    | Details                                                               |
| ---------------- | --------------------------------------------------------------------- |
| Provider         | CiscoDevNet/sdwan                                                     |
| Version          | 0.1.0                                                                 |
| Documentation    | https://registry.terraform.io/providers/CiscoDevNet/sdwan/latest/docs |
| vManage URL      | https://198.18.128.2                                                  |
| vManage User     | user3                                                                 |
| vManage Password | C1sco12345                                                            |

## Step 1: Attach device-template the to router

Your task is to attach a predefined device-template to the router with the required device variables. Use the prepared .csv file in this directory.

| Required parameters | Value                                    |
| ------------------- | ---------------------------------------- |
| device_template_id  | _$ID from device-template "C8Kv_Branch"_ |
| file                | device_vars.csv                          |
| chassis_number      | C8K-C74E1F90-C146-12BB-9B15-2542E9D20884 |

:exclamation: :warning: Use a data source to get the device_template_id for the device-template **"C8Kv_Branch"**

## Step 2: Verification

Log into the vManage UI and navigate to Configuration -> Devices.
Verify if your Router is now successfully onboarded and in vManage mode:

Example Site21:

<img src=../../img/sd-wan.jpg/>

<div align="right">
  <a href='../Mission 2/README.md'>Next: Mission 2</a>
</div>
