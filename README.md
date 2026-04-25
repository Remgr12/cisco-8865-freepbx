
### Enterprise Cisco 8865 with FreePBX

### 1. Prerequisites (TFTP Server & Firmware)
1. **TFTP Server:** A reliable TFTP server is required. On Linux, `tftpd-hpa` is highly recommended (`sudo apt install tftpd-hpa`). Ensure the TFTP root directory has the correct permissions.
2. **Download Firmware:** * Go to the Cisco Software Download portal.
   * Navigate to Unified IP Phone 8800 Series > IP Phone 8865.
   * Download the latest **Enterprise SIP** firmware ZIP file.
3. **Extract Files:** Unzip the downloaded firmware and place all extracted files directly into your TFTP root directory.

### 2. Prepare the Configuration File
1. **Find the MAC Address:** On the phone, press **Applications** (Gear) > **Admin Settings** > **Network Setup** > **Ethernet Setup** and note the **MAC Address** (e.g., `AABBCCDDEEFF`).
2. **Rename the Template:** Locate the template XML configuration file included in this repository. Rename it to **`SEPAABBCCDDEEFF.cnf.xml`** (all uppercase, using your phone's specific MAC address) and place it in your TFTP root directory.
3. **Update the Firmware Variable:** Look inside your extracted firmware files in the TFTP directory for a file ending in `.loads`. Copy the exact name *without* the `.loads` extension and update the `<loadInformation>` tag inside the XML file.
4. **Update Placeholders:** Open the XML file and replace the included placeholders with your specific FreePBX environment details:
   * `YOUR_FREEPBX_IP` (Your PBX/TFTP Server IP)
   * `YOUR_SSH_PASSWORD` (For remote phone administration)
   * `YOUR_PHONE_LABEL`, `YOUR_DISPLAY_NAME` (On-screen names)
   * `YOUR_EXTENSION_NUMBER`, `YOUR_EXTENSION_LABEL` (Your FreePBX SIP Extension)
   * `YOUR_SIP_PASSWORD` (Your FreePBX SIP Secret)
   * `SPEED_DIAL_X_NAME`, `SPEED_DIAL_X_NUMBER` (For programmable line keys)
   * `YOUR_CONTACTS_NUMBER`, `YOUR_CONF_NUMBER` (For feature buttons)

### 3. Connect the Phone to TFTP
1. On the phone, press **Applications** (Gear) > **Admin Settings** > **Network Setup** > **IPv4 Setup**.
2. Scroll down to **Alternate TFTP** and set it to **On**.
3. Scroll to **TFTP Server 1** and enter your TFTP Server IP address.
4. Press **Apply/Save**. The phone will reboot, download the firmware, pull the configuration file, and register to your FreePBX server.
