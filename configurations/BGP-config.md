# BGP
## Basic Configuration

1. Initialize BGP routing process: router bgp as-number

2. (Optional) Define BGP router ID (RID): bgp router-id router-id

3. Identify BGP neighbor's IP and ASN: neighbor ip-address remote-as as-number

4. Initialize address family: assdress-family afi safi (afi values are IPv4 and IPv6, and examples
of safi values are unicast and multicast)

5. Activate address family for BGP neighbor: ip-address activate

```

R1 (Default IPv4 Address-Family Enabled)
router bgp 65100
neighbor 10.12.1.2 remote-as 65200R2 (Default IPv4 Address-Family Disabled)
router bgp 65200
    no bgp default ipv4-unicast
    neighbor 10.12.1.1 remote-as 65100
    !
    address-family ipv4
        neighbor 10.12.1.1 activate
    exit-address-family

```