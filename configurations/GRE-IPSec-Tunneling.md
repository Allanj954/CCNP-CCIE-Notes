# IPsec over GRE
## Crypto maps

1. Configure crypto ACL to classify VPN traffic:

```
ip access-list extended acl_name
permit gre host {tunnel-source IP} host {tunnel-destination IP}
```

2. Configure ISAKMP policy for IKE SA using:
**crypto isakmp policy** priority

encryption, hash, authentication and DH group can be specified:

```
encryption {des | 3des | aes | aes 192 | aes 256}
hash {sha | sha256 | sha384 | md5}
authentication {rsa-sig | rsa-encr | pre-share}
group {1 | 2 | 5 | 14 | 15 | 16 | 19 | 20 | 24}
```

3. Configure PSK:

    **crypto isakmp key** keystring **address** peer-address [mask]

4. Create transform set and enter transform set configuration mode:

    **crypto ipsec transform-set** transform-set-name transform1 [transform2 [transform3]]
    
        mode [tunnel | transport ]
    
5. Configure crypto map and enter crpto map config:
*crypto map* map-name seq-num [ipsec-isakmp]

    In crypto map config mode:

    **match address** acl-name

    **set peer** {hostname | ip-address}

    **set transform-set** transform-set-name1 [transform-set-name2...tran

6. Apply crypto map to outside interface:

    **crypto map** map name

## Profiles

## Example

```
R1
crypto isakmp policy 10
authentication pre-share
hash sha256
encryption aesgroup 14
!
crypto isakmp key CISCO123 address 100.64.2.2
!
crypto ipsec transform-set AES_SHA esp-aes esp-sha-hmac
mode transport
!
ip access-list extended GRE_IPSEC_VPN
permit gre host 100.64.1.1 host 100.64.2.2
!
crypto map VPN 10 ipsec-isakmp
match address GRE_IPSEC_VPN
set transform AES_SHA
set peer 100.64.2.2
!
interface GigabitEthernet0/1
ip address 100.64.1.1 255.255.255.252
crypto map VPN
!
interface Tunnel100
bandwidth 4000
ip address 192.168.100.1 255.255.255.0
ip mtu 1400
tunnel source GigabitEthernet0/1
tunnel destination 100.64.2.2
router ospf 1
router-id 1.1.1.1
network 10.1.1.1 0.0.0.0 area 1
network 192.168.100.1 0.0.0.0 area 0
R2
crypto isakmp policy 10
authentication pre-share
hash sha256encryption aes
group 14
crypto isakmp key CISCO123 address 100.64.1.1
crypto ipsec transform-set AES_SHA esp-aes esp-sha-hmac
mode transport
crypto ipsec profile IPSEC_PROFILE
set transform-set AES_SHA
interface GigabitEthernet0/1
ip address 100.64.2.2 255.255.255.252
interface Tunnel100
bandwidth 4000
ip address 192.168.100.2 255.255.255.0
ip mtu 1400
tunnel source GigabitEthernet0/1
tunnel destination 100.64.1.1
tunnel protection ipsec profile IPSEC_PROFILE
router ospf 1
router-id 2.2.2.2
network 10.2.2.0 0.0.0.255 area 2
network 192.168.100.2 0.0.0.0 area 0