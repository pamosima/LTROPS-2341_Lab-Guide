# Infrastructure as Code for Cisco Catalyst Center and Catalyst SD-WAN Manager with Terraform - LTROPS-2341

:warning:
:exclamation: To get started with your missions, open the <a href='../Missions/README.md'>README.md</a> in the Missions directory.

## How to get started

Beneath you will find information how to [connect to the lab](#connect-laptop-to-dcloud-session-using-cisco-anyconnect) and [working with your pod (Wkst)](#connect-to-your-pod-wkst-using-remote-desktop-client).

### Connect Laptop to dCloud Session Using Cisco AnyConnect

#### Use Cisco AnyConnect Client Already Installed on Your Laptop

Access to this lab sessions in Cisco dCloud requires a VPN connection between your laptop and the dCloud data center that is hosting your session.

To use the Cisco AnyConnect client already installed on your laptop:

1. For the AnyConnect credentials, please refer to the information provided in your printed lab getting started guide.
2. Start Cisco AnyConnect on your laptop.
3. Retrieve the Host URL details as outlined in the AnyConnect section of the printed lab getting started guide. Write this information into the URL Connection box within the AnyConnect login window, and subsequently, click on the Connect button.
4. Obtain the user ID (User) and password from the AnyConnect section in the printed lab getting started guide. Write each credential into the corresponding fields within the Cisco AnyConnect login window.
5. Click OK.
6. Click Accept on the window confirming your connection.
7. When connected to your AnyConnect VPN session, the AnyConnect VPN icon is displayed in the system tray (Windows).
8. To view connection details or to disconnect, click the AnyConnect VPN icon and then choose Disconnect.

### Connect to your Pod (Wkst) Using Remote Desktop Client

#### Add a Remote PC connection

Use Remote Desktop Client Already Installed on Your Laptop:

1. For the Remote Desktop credentials, scroll to the [Remote Desktop section](#remote-desktop-section).
2. Start Remote Desktop Client on your laptop.
3. Create a Remote PC connection:
   1. In the Connection Center, tap + Add, and then tap PCs.
   2. PC name: Copy the IP Address from the [Remote Desktop section](#remote-desktop-section), paste it in the PC name box in the PC add window.
   3. User account: Tap + to add a new account. Copy a username and the password from the [Remote Desktop section](#remote-desktop-section) and then paste each into the Add a User Account window. User account – The user account to use to access the remote PC.
      - Click Add.
   4. Tap Save.
4. Now you can Connect to your Pod (Wkst)

### Remote Desktop section

| Site    | IP Address     | Username | Password   |
| ------- | -------------- | -------- | ---------- |
| Site 11 | 198.18.133.141 | user1    | C1sco12345 |
| Site 12 | 198.18.133.142 | user2    | C1sco12345 |
| Site 13 | 198.18.133.143 | user3    | C1sco12345 |
| Site 14 | 198.18.133.144 | user4    | C1sco12345 |
| Site 15 | 198.18.133.145 | user5    | C1sco12345 |

<div align="right">
  <a href='../General Information/README.md'>Prev: General Information</a> - <a href='../Missions/README.md'>Next: Missions</a>
</div>
