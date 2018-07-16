# ansible-vpn-gateway
Minimalistic hardened and convenient self-contained provisioning of a VPN gateway, with client certificate management and a DNS proxy for CentOS.

Roles:
 - `vpn-gateway` installs gateway host on a gateway VM

On the physical host, execute the following line to enable port forwarding to the gateway VM
```
firewall-cmd --zone=public --add-forward-port=port=1194:proto=tcp:toport=1194:toaddr=<gateway VM IP>
```
(when using default port/protocol values)

## Assumptions and design
- Centos 7.5+ 
- OpenVPN as foundation
- Systemd service management (one service, not a template)
- Firewalld instead of iptables
- DNS proxy (dnsmasq) to provide host names from internal networks (from /etc/hosts or internal DNS)

## Security setup
- Self-managed CA, co-located at gateway
- Client certificates managed by EasyRSA (integrated into this role, no git pulls etc) 
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
