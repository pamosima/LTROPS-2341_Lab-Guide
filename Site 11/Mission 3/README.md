# Mission 3: Onboard your Access-Point and provision your SSID

This mission requires a few different steps:
- Create SSID
- Create wireless profile 
- Provision WLC
- Claim AP with PnP
- Provision AP

## Terraform provider

Use the following terraform provider and make sure to use the specified version.

Specification | Details
------------- | --- 
Provider      | cisco-en-programmability/dnacenter
Version       | :warning: 1.1.2-beta
Documentation | https://registry.terraform.io/providers/cisco-en-programmability/dnacenter/1.1.2-beta/docs
DNAC URL      | https://dnac.its-best.ch

## Step 1: Create SSID

Required parameters                   | Value
------------------------------------- | ----------------------------------------
basic_service_set_client_idle_timeout | 0
client_exclusion_timeout              | 0
enable_basic_service_set_max_idle     | true
enable_broadcast_ssi_d                | true
enable_client_exclusion               | true
enable_directed_multicast_service     | true
enable_fast_lane                      | true
enable_mac_filtering                  | false
enable_neighbor_list                  | true
enable_session_time_out               | true
fast_transition                       | Adaptive
mfp_client_protection                 | Optional
name                                  | Devnet Site-11
passphrase                            | *$YOUR PASSPHRASE*
radio_policy                          | Dual band operation (2.4GHz and 5GHz)
security_level                        | WPA2_PERSONAL
session_time_out                      | 0
ssid_name                             | Devnet Site-11
traffic_type                          | voicedata

Navigate to Design -> Network Settings -> Wireless in DNA-C to verify.

## Step 2: Create wireless profile

Required parameters                   | Value
------------------------------------- | ----------------------------------------
name                                  | Wireless DevNet Site-11
sites                                 | Global/DevNet/Site-11
enable_fabric                         | false
enable_flex_connect                   | false
local_to_vlan                         | 1
interface_name                        | VLAN0020
name                                  | Devnet Site-11
type                                  | Enterprise
wireless_profile_name                 | Wireless DevNet Site-11

## Step 3: Provision WLC

Required parameters                   | Value
------------------------------------- | ----------------------------------------
device_name                           | C9800.its-best.ch
managed_aplocations                   | Global/DevNet
persistbapioutput                     | true

## Step 4: Claim Access-Point

:exclamation: Your **Access-point Serial Number** is **FCW2428P6GA**

Required parameters                   | Value
------------------------------------- | ----------------------------------------
device_id                             | *$PNP Device ID from AP*
site_id                               | *$Floor ID*
type                                  | AccessPoint
rf_profile                            | TYPICAL

## Step 5: Provision AP

Your Access-Point has to be successfully onboarded for this step. Please verify in DNAC.

:exclamation: :warning: Depending on the version - wrap the parameters into a "payload {}". Needed for 1.1.2-beta.

Required parameters                   | Value
------------------------------------- | ----------------------------------------
device_name                           | site-11-ap-1
rf_profile                            | TYPICAL
site_id                               | Global/DevNet/Site-11/11-1/11-1-1
site_name_hierarchy                   | Global/DevNet/Site-11/11-1/11-1-1
type                                  | ApWirelessConfiguration

## Step 6: Verification

After the successful provisioning of your Access-Point you’re SSID should now be broadcasted.

Verification:
- Connect to your SSID with your phone
- Your phone should have an IP in the range: 172.20.200.0/24
- You should access the internet via the dCloud DC in London, therefore you should see a Cisco Public ip when you access https://bgp.he.net/.


<div align="right">
    [Prev](../Mission 2/README.md)
</div> 