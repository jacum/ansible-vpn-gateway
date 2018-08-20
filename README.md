# ansible-vpn-gateway
Minimalistic hardened and convenient self-contained provisioning of a VPN gateway, with client certificate management and a DNS proxy for CentOS.

## Prerequisites
 - On the physical host, enable VPN port forwarding (default 1194/udp) to the VM running the gateway. This may require some ad-hoc changes, assuming that virtualisation frameworks do their own firewall management.

## Assumptions and design
- Running in a dedicated VM
- Centos 7.5+ 
- OpenVPN as foundation
- UDP for less overhead (encapsulated protocol is TCP most of the time, anyway)
- Systemd service management (one service, not a template, for simplicity)
- Firewalld instead of iptables
- DNS proxy (dnsmasq) to provide host names from internal networks (from /etc/hosts or internal DNS)

## Security setup
- Self-managed CA, co-located at gateway
- Client certificates managed by EasyRSA 
- Safe ciphers by default
- HMAC firewall for additional security

## Making client access profiles (.ovpn)
```
$ cd /etc/openvpn/ca
$ ./make_client_ovpn <client_id> > <client_id>.ovpn

```

## Further options for extension
- Integrating LDAP/PAM auth for external user registries/CAs
- Identity management with freeipa
