# Network Infrastructure
Documentation on the configuration of the networking devices for my home network.

# DD-WRT Configuration
At the time of writing, all DD-WRT devices are running DD-WRT v3.0-r49392 std (06/29/22).

## Features
 - DynDNS (Namecheap) - Updates a DNS record to that of the WAN IP, even if the IP changees. Largely used to ensure that the VPN is always accessible
 - OpenVPN server providing full network access to the local network
 - Wireless repeater bridge connected to the main gateway via a dedicated Backhaul network

## Usage
[`roles`](roles)/[`devices`](devices) contain settings that will need to be changed from the defaults when configuring from a fresh DD-WRT install. Instructions on which files to use are provided in the Devices section. Secret values are listed in [`secrets.yaml`](secrets.yaml), which is encrypted with [Mozilla SOPS](https://github.com/mozilla/sops)

## Role Descriptions
- `gateway` - Primary Internet gateway, along with other services such as DHCP, DNSmasq, OpenVPN, etc.
- `ap` - Additional access points used to extend wireless coverage
- `repeater` - Largely extends the `ap` role, but broadcasts only on the 2.4GHz band and uses the 5GHz as a wireless backhaul

## Devices
- Netgear R8500 `gateway` at 192.168.1.1
  - [`roles/common.yaml`](roles/common.yaml)
  - [`devices/r8500.yaml`](devices/r8500.yaml)
  - [`roles/gateway.yaml`](roles/gateway.yaml)
- Netgear R7000 `repeater` at 192.168.1.3
  - [`roles/common.yaml`](roles/common.yaml)
  - [`devices/r7000.yaml`](devices/r7000.yaml)
  - [`roles/ap.yaml`](roles/ap.yaml)
  - [`roles/repeater.yaml`](roles/repeater.yaml)
- Netgear WNDR3700v1 `ap` at 192.168.1.4
  - [`roles/common.yaml`](roles/common.yaml)
  - [`devices/wndr3700v1.yaml`](devices/wndr3700v1.yaml)
  - [`roles/ap.yaml`](roles/ap.yaml)
- External DNS server at 192.168.1.9
