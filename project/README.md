# Первые наработки
```msk-sp-01

hostname msk-sp-01
!
interface Ethernet1
 description msk-l-001
 no switchport
 ip address 10.2.1.0/31
 ip ospf network point-to-point
 ip ospf area 0.0.0.0
!
interface Ethernet2
 description msk-l-002
 no switchport
 ip address 10.2.1.2/31
 ip ospf network point-to-point
 ip ospf area 0.0.0.0
!
interface Ethernet3
 description msk-l-003
 no switchport
 ip address 10.2.1.4/31
 ip ospf network point-to-point
 ip ospf area 0.0.0.0
!
interface Ethernet4
 description msk-l-004
 no switchport
 ip address 10.2.1.6/31
 ip ospf network point-to-point
 ip ospf area 0.0.0.0
!
interface Ethernet5
 description msk-bl-253
 no switchport
 ip address 10.2.2.250/31
 ip ospf network point-to-point
 ip ospf area 0.0.0.0
!
interface Ethernet6
 description msk-bl-254
 no switchport
 ip address 10.2.2.252/31
 ip ospf network point-to-point
 ip ospf area 0.0.0.0
!
interface Loopback1
 ip address 10.0.1.1/32
 ip ospf area 0.0.0.0
!
interface Management1
!
ip routing
!
router bgp 65001
 router-id 10.0.1.1
 no bgp default ipv4-unicast
 distance bgp 20 200 200
 neighbor LEAF peer group
 neighbor LEAF remote-as 65001
 neighbor LEAF next-hop-unchanged
 neighbor LEAF update-source Loopback1
 neighbor LEAF bfd
 neighbor LEAF ebgp-multihop 2
 neighbor LEAF route-reflector-client
 neighbor LEAF send-community extended
 neighbor 10.1.1.1 peer group LEAF
 neighbor 10.1.1.1 remote-as 65101
 neighbor 10.1.1.1 description msk-l-001
 neighbor 10.1.1.2 peer group LEAF
 neighbor 10.1.1.2 remote-as 65102
 neighbor 10.1.1.2 description msk-l-002
 neighbor 10.1.1.3 peer group LEAF
 neighbor 10.1.1.3 remote-as 65103
 neighbor 10.1.1.3 description msk-l-003
 neighbor 10.1.1.4 peer group LEAF
 neighbor 10.1.1.4 remote-as 65104
 neighbor 10.1.1.4 description msk-l-004
 neighbor 10.1.1.5 peer group LEAF
 neighbor 10.1.1.5 remote-as 65353
 neighbor 10.1.1.5 description msk-bl-253
 neighbor 10.1.1.6 peer group LEAF
 neighbor 10.1.1.6 remote-as 65354
 neighbor 10.1.1.6 description msk-bl-254
 !
 address-family evpn
    neighbor LEAF activate
!
router ospf 1
 router-id 10.0.1.1
 bfd default
 passive-interface default
 no passive-interface Ethernet1
 no passive-interface Ethernet2
 no passive-interface Ethernet3
 no passive-interface Ethernet4
 no passive-interface Ethernet5
 no passive-interface Ethernet6
 max-lsa 12000
 log-adjacency-changes detail
!
end
wr mem

```
