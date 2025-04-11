# yude.jp

## Subnet / Naming conventions for service hosts

- Tailscale: 100.64.0.0/16
    - `*.tail5b1c5.ts.net`
- Private gateway: 192.168.30.0/24
    - `*.*.yude.jp`
- Guest: 192.168.200.0/24
- The Internet
    - `*.yude.jp`

## NOC
### nrt.yude.jp (Chiba, Japan)

#### Connectivity

- AS2519 (ARTERIA Networks Corporation)

#### Subnet

- Home: 192.168.100.0/24

#### Topology

```mermaid
graph LR
    gw[
        gw.nrt.yude.jp<br />
        Internet / private gateway
        NEC Platforms, Inc.
        UNIVERGE IX2215
    ]
    gw --> l2

    l2[
        L2 aggregate switch
        NETGEAR, Inc.
        JGS516
    ]
    l2 --> wheel[
        wheel.yude.jp
        wheel.tail5b1c5.ts.net<br />
        Kubernetes master
        Trigkey
        TRIGKEY S5
    ]
    l2 --> kvm-wheel[
        kvm-wheel.yude.jp
        kvm-wheel.tail5b1c5.ts.net<br />
        KVM over IP
        Raspberry Pi Foundation
        Raspberry Pi 3 Model B
    ]
    l2 --> maple[
        maple.yude.jp
        maple.tail5b1c5.ts.net<br />
        Hypervisor
        Hand-made computer
    ]
    l2 --> kvm-maple[
        kvm-maple.yude.jp
        kvm-maple.tail5b1c5.ts.net<br />
        KVM over IP
        Sipeed
        NanoKVM PCIe
    ]
    l2 --> rakka[
        rakka.yude.jp
        rakka.tail5b1c5.ts.net<br />
        Kubernetes master
        GMK Technology Co., Ltd
        GMKtec G3
    ]
    l2 --> kvm-rakka[
        kvm-rakka.yude.jp
        kvm-rakka.tail5b1c5.ts.net<br />
        KVM over IP
        Raspberry Pi Foundation
        Raspberry Pi 3 Model B
    ]
    l2 --> apc[
        apc.nrt.yude.jp<br />
        Power supplier
        Schneider Electric
        APC Smart-UPS SMT750J
    ]
    l2 --> voip[
        voip.nrt.yude.jp<br />
        VoIP router
        Yamaha Corporation
        NetViolante RT58i
    ]
    l2 --> kvm-zen[
        kvm-zen.yude.jp
        kvm-zen.tail5b1c5.ts.net<br />
        KVM over IP
        Sipeed
        NanoKVM PCIe
    ]
    l2 --> ap-slave[
        ap-slave.nrt.yude.jp<br />
        Wi-Fi AP
        TP-Link Corporation Pte. Ltd.
        AX1500
    ]
    
    l2 --> l3
    l3[
        vlanagr.nrt.yude.jp<br />
        VLAN-aware aggregate switch
        NEC Platforms, Inc.
        QX-S810EP-PW
    ]
    l3 --> ap-master[
        ap-master.nrt.yude.jp<br />
        VLAN-aware Wi-Fi AP
        ELECOM CO., LTD.
        WAB-I1750-PS
    ]
    l3 --> devil[
        devil.yude.jp<br />
        FreeBSD machine
        Raspberry Pi Foundation
        Raspberry Pi 2 Model B
    ]

    ap-master --> pikachu[
        pikachu.yude.jp<br />
        B-route fetcher
        Raspberry Pi Foundation
        Raspberry Pi Model A
    ]
```
