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