# Mission 2: Create site in Catalyst Center and deploy your Switch

In this mission you first deploy your Site in Catalyst Center and then onboard your Switch and assign it to your newly created site.

## Terraform provider

:warning:
:exclamation: Even if we are running Catalyst Center Version 2.3.7.4 in this lab we are still using the dnacenter terraform provider. As there are missing ressources in the new catalystcenter provider. Make sure to use the following terraform provider and use the exact specified version (as we tested the lab with this version).

| Specification | Details                                                                                     |
| ------------- | ------------------------------------------------------------------------------------------- |
| Provider      | cisco-en-programmability/dnacenter                                                          |
| Version       | 1.1.31-beta                                                                                 |
| Documentation | https://registry.terraform.io/providers/cisco-en-programmability/dnacenter/1.0.12-beta/docs |
| DNAC URL      | https://198.18.129.100                                                                      |
| DNAC User     | user4                                                                                       |
| DNAC Password | C1sco12345                                                                                  |

## Step 1: Create Catalyst Center site

Create a subarea, building and floor using Terraform with your Site-specific values.

:exclamation: :warning: Despite the documentation - you need to create your area, building and floor in separate steps. It's not possible to create everything in one step.

### Step 1a: Create an area

| Required parameters | Value              |
| ------------------- | ------------------ |
| name                | Site-14            |
| parent_name         | Global/LTROPS-2341 |

### Step 1b: Create a building

| Required parameters | Value                                          |
| ------------------- | ---------------------------------------------- |
| name                | 14-1                                           |
| parent_name         | Global/LTROPS-2341/Site-14                     |
| address             | Richtistrasse 7, 8304 Wallisellen, Switzerland |
| latitude            | 47.409871                                      |
| longitude           | 8.590509                                       |

### Step 1c: Create a floor

| Required parameters | Value                           |
| ------------------- | ------------------------------- |
| name                | 14-1-1                          |
| parent_name         | Global/LTROPS-2341/Site-14/14-1 |
| rf_model            | Cubes And Walled Offices        |
| height              | 100                             |
| length              | 100                             |
| width               | 100                             |

Log in to Catalyst Center and verify your newly created site under Design -> Network Hierarchy.
Example Site21:

<img src=../../img/network_hierarchy.jpg/ width=30%>

## Step 2: Onboard your Switch

After you successfully created your site the next step is to onboard your Switch using Plug-and-Play.
While claiming the device it should get assigned to your Site(building) and get configured with a predefined PNP onboarding template.

:bulb: There is only one terraform resource that claims the device and assigns it to a site!

:exclamation: Your **Switch Serial Number** is: **CML14SW1**

| Required parameters | Value                                           |
| ------------------- | ----------------------------------------------- |
| device_id           | _$Switch ID from PNP Devices_                   |
| site_id             | _$Building ID from your newly created building_ |
| type                | Default                                         |
| config_id           | _$Template ID - see below_                      |
| config_parameters   | key: HOSTNAME, value: site-14-switch-1          |

:bulb: To get the configuration template id use the following data source:

```terraform
data "dnacenter_configuration_template" "pnp_template" {
  provider           = dnacenter
  latest_version     = "false"
  software_version   = "17.6.1"
  un_committed       = "true"
}
```

## Step 3: Verification

Verify that your Switch got claimed, configured and assigned to your Site by navigating to Provision -> Inventory and choose your site in the Catalyst Center UI:

<img src=../../img/site-switch.jpg/ width=80%>

<div align="right">
  <a href='../Mission 1/README.md'>Prev: Mission 1</a> - <a href='../Mission 3/README.md'>Next: Mission 3</a>
</div>
