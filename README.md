# Cumulus ZTP for HCS with Nutanix
This is the home of the [Zero Touch Provisioning](https://docs.cumulusnetworks.com/display/DOCS/Zero+Touch+Provisioning+-+ZTP) script to provision a pair of Cumulus Linux switches with [Cumulus Hyperconverged Service](https://docs.cumulusnetworks.com/display/DOCS/Cumulus+Hyperconverged+Service+with+Nutanix) to support a single, dual-attached rack of Nutanix nodes.

## Usage
This script is designed to be used with [Nutanix on a Stick](http://www.cumulusnetworks.com/noas) to build a USB stick to deploy Cumulus Linux with the latest software image, license and configuration. 

If you wish to manually modify the ZTP script or wish to deploy via an HTTP server for ZTP, you may freely modify this script and configuration. 

### ztp_config.txt
This file is the configuration settings that are loaded at run time to provide specific configurations for the Nutanix service. The file contains the following settings
* `NUTANIX_USERNAME=admin` -- The username that is used to access Prism or AOS API
* `NUTANIX_PASSWORD=nutanix/4u` -- The password of the configured user for Prism
* `NUTANIX_IP=10.1.1.123` -- The IP address of a specific CVM node or the IP address of the CVM cluster IP. Using the cluster IP is recommended.
* `SWITCH_CVM_IP=10.1.1.254/24` -- The IP and subnet mask the switch will use in the same subnet as the CVM IP. This IP must be unique on every switch.
* `SWITCH_MANAGEMENT_IP=10.0.0.11/24` -- If you are using eth0 and want to statically assign an IP, enter the IP address and subnet mask here. This setting is optional. DHCP is the default.
* `SWITCH_DEFAULT_GATEWAY=10.1.1.1` -- If you manually defined an eth0 IP address, you may also define the eth0 default gateway. This setting is optional. 
* `UPLINKS=swp51,swp52` -- One or more interfaces that are connections into existing infrastructure. This is a comma separated list. This is optional. The default is none.
* `PEERLINK=swp49,swp50` -- The ports that connect between the two switches connecting to Nutanix nodes. This is a comma separated list. The default is `swp49,swp50`

### cumulus-ztp
This is the python script that is executed as a ZTP script. The lack of file extension is intentional.

If you are manually executing this ZTP script, you must replace the line `LICENSE_KEY_GOES_HERE` on line 83 with your full license key string.

## Troubleshooting
The HCS ZTP script will write to `/var/log/syslog` during the ZTP process. Use `cat /var/log/syslog | grep ZTP` to view any HCS ZTP syslog lines from the ZTP process.

You can view the ZTP process status with `ztp -s`

## More Information
For more information about Cumulus HCS and Nutanix integration visit the [Cumulus HCI portal](https://cumulusnetworks.com/networking-solutions/converged-infrastructure/)