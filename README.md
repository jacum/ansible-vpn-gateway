# ansible-vpn-gateway
Ansible provisioning of VPN gateway with client certificate management.

## Assumptions and design
- Centos 7.x 
- OpenVPN as foundation
- Minimalistic/hardened setup
- Self-managed CA, client certificates managed by EasyRSA (integrated into this role, no git pulls etc)
- Only traffic to internal (behind gateway) networks is routed through VPN
- DNS proxy (dnsmasq) to provide host names from internal networks (from /etc/hosts or internal DNS)
- TLS auth for additional security
- Systemd service management (one service, not a template)
- Firewalld instead of iptables

## Making client access profiles (.ovpn)
```
$ cd /etc/openvpn/ca
$ ./make_client_ovpn <client_id> > <client_id>.ovpn

```

## Further options
- LDAP/PAM auth
- Identity management with freeipa
