# UDM IGMP Proxy

## Install and Configure `igmpproxy`

**Your UDM must be updated to at least version 1.11.0 to use `igmpproxy`.**

1. SSH into your UDM. Replace 192.168.1.1 with your UDM's IP.

   ```sh
   ssh root@192.168.1.1 -o HostKeyAlgorithms=+ssh-rsa
   unifi-os shell
   ```

2. Download and install `igmpproxy` and configuration file.

   ```sh
   # Download a recent igmpproxy version
   curl -O -L http://ftp.debian.org/debian/pool/main/i/igmpproxy/igmpproxy_0.3-1_arm64.deb
   # Install udm-iptv and igmpproxy
   apt install ./igmpproxy_0.3-1_arm64.deb
   ```

3. The default `udm-igmpproxy` uses eth4 (WAN2 SFP+ port) for the upstream network, and br2 (VLAN 2) for the downstream network. If you are using a different VLAN for TV traffic than VLAN 2, change the one instance of br2 to brX, where X is your VLAN number (br0 = default LAN).

   ```sh
   # Create directory for udm-igmpproxy
   mkdir /usr/lib/udm-igmpproxy
   # Download udm-igmpproxy
   curl -L -o /usr/lib/udm-igmpproxy2/udm-igmpproxy https://raw.githubusercontent.com/Poremski/udm-igmpproxy/HEAD/src/udm-igmpproxy
   # Download the udm-igmpproxy.service
   curl -L -o /etc/systemd/system/udm-igmpproxy.service https://raw.githubusercontent.com/Poremski/udm-igmpproxy/HEAD/src/udm-igmpproxy.service
   # Start and enable the service
   systemctl start udm-igmpproxy.service && systemctl enable udm-igmpproxy.service
   ```
