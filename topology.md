# yude.jp

## Subnet / Naming conventions for hosts in this network

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
    - Default route of all VLANs

#### VLAN

- VLAN 10
    - Home: 192.168.100.0/24
- VLAN 20
    - Guest

#### Topology

```mermaid
graph TD
    gw[
        gw.nrt.yude.jp<br />
        Internet / private gateway
        NEC Platforms, Inc.
        UNIVERGE IX2215
    ]
    gw --> |access: VLAN 10; Home| l2

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
        Netvolante RT58i
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
    
    gw --> |trunk: VLAN 10; Home + VLAN 20; Guest| l3
    l3[
        vlanagr.nrt.yude.jp<br />
        VLAN-aware aggregate switch
        NEC Platforms, Inc.
        QX-S810EP-PW
    ]
    l3 --> |trunk: VLAN 10; Home + VLAN 20; Guest| ap-master[
        ap-master.nrt.yude.jp<br />
        VLAN-aware Wi-Fi AP
        ELECOM CO., LTD.
        WAB-I1750-PS
    ]
    l3 --> |access: VLAN 10; Home| devil[
        devil.yude.jp<br />
        FreeBSD machine
        Raspberry Pi Foundation
        Raspberry Pi 2 Model B
    ]

    ap-master --> |access: VLAN 10; Home| pikachu[
        pikachu.yude.jp<br />
        B-route fetcher
        Raspberry Pi Foundation
        Raspberry Pi Model A
    ]
```

### hnd.yude.jp (Tokyo, Japan)

#### Connectivity

- AS2516 (KDDI Corporation)
    - Default route of Native VLAN
- AS150363 (SoftEther Corporation)
    - Default route of VLAN 20

#### VLAN

- Native
    - Home: 192.168.0.0/24
- VLAN 20
    - Guest

#### Topology

```mermaid
graph TD
    gw[
        gw.hnd.yude.jp<br />
        Internet / private gateway
        NEC Platforms, Inc.
        UNIVERGE IX2215
    ]
    gw --> bway[
        bway.yude.jp
        bway.tail5b1c5.ts.net<br />
        Hypervisor
        Fujitsu Limited
        ESPRIMO D586/P
    ]
    gw --> kvm-bway[
        kvm-bway.yude.jp
        kvm-bway.tail5b1c5.ts.net<br />
        KVM over IP
        Raspberry Pi Foundation
        Raspberry Pi 3 Model B
    ]
    gw --> whale[
        whale.yude.jp
        whale.tail5b1c5.ts.net<br />
        Hypervisor
        UNIT.COM INC.
        GALLERIA RT5
    ]
    gw --> kvm-whale[
        kvm-whale.yude.jp
        kvm-whale.tail5b1c5.ts.net<br />
        KVM over IP
        Sipeed
        NanoKVM Cube
    ]
    gw --> snom220[
        snom220.hnd.yude.jp<br />
        VoIP phone
        Snom Technology GmbH
        snom 220
    ]
```

### ibr.yude.jp (Ibaraki, Japan)

#### Connectivity

- AS2518 (BIGLOBE)
    - Default route of Native VLAN

#### VLAN

- Native
    - Home: (redacted)
    - PPP: 192.168.100.0/24

#### Topology

```mermaid
graph LR
    gw[
        ?<br />
        Internet gateway
        Out of management scope
        pepepper.net
    ]
    gw --> hitachi[
        hitachi.yude.jp
        hitachi.tail5b1c5.ts.net<br />
        Hypervisor
        Hand-made computer
    ]
    gw --> kvm-hitachi[
        kvm-hitachi.yude.jp
        kvm-hitachi.tail5b1c5.ts.net<br />
        KVM over IP
        Sipeed
        NanoKVM Cube
    ]

    pppgw[
        pppgw.ibr.yude.jp<br />
        Internet gateway
        Yamaha Corporation
        RT107e
    ]
    pppgw --> hitachi
```

### ttj.yude.jp (Tottori, Japan)

#### Connectivity

- AS131925 (FAMILY NET JAPAN INCORPORATED)
    - Default route of Native VLAN

#### VLAN

- Native
    - Home: (redacted)

#### Topology

```mermaid
graph LR
    gw[
        ?<br />
        Internet gateway
        Out of management scope
    ]
    gw --> dune[
        dune.yude.jp
        dune.tail5b1c5.ts.net<br />
        Resource server
        Raspberry Pi Foundation
        Raspberry Pi 4 Model B
    ]
    gw --> priv-gate

    priv-gate[
        priv-gate.ttj.yude.jp<br />
        Private gateway
        Yamaha Corporation
        RTX810
    ]
    priv-gate --> voip[
        voip.ttj.yude.jp<br />
        VoIP router
        Yamaha Corporation
        Netvolante RT57i
    ]
```

### izo.yude.jp (Shimane, Japan)

#### Connectivity

- AS2516 (KDDI Corporation)
    - Default route of Native VLAN

#### VLAN

- Native
    - MKNET: (redacted)

#### Topology

```mermaid
graph LR
    gw[
        ?<br />
        Internet gateway
        Out of management scope
    ]
    gw --> ruby[
        ruby.yude.jp
        ruby.tail5b1c5.ts.net<br />
        Resource server
        Fujitsu Limited
        ARROWS Tab Q616/P
    ]
```

### toy.yude.jp (Toyama, Japan)

#### Connectivity

- AS55392 (INTERNET MULTIFEED CO.)
    - Default route of Native VLAN

#### VLAN

- Native
    - Home: (redacted)

#### Topology

```mermaid
graph LR
    gw[
        ?<br />
        Internet gateway
        Out of management scope
    ]
    gw --> ruby[
        shrimp.yude.jp
        shrimp.tail5b1c5.ts.net<br />
        Resource server
        Fortinet
        FortiGate 50E
    ]
```


### toy.yude.jp (Toyama, Japan)

#### Connectivity

- AS55392 (INTERNET MULTIFEED CO.)
    - Default route of Native VLAN

#### VLAN

- Native
    - Home: (redacted)

#### Topology

```mermaid
graph LR
    gw[
        ?<br />
        Internet gateway
        Out of management scope
    ]
    gw --> ruby[
        shrimp.yude.jp
        shrimp.tail5b1c5.ts.net<br />
        Resource server
        Fortinet
        FortiGate 50E
    ]
```

### oci.yude.jp (Oracle Cloud Infrastructure; Osaka, Japan)

#### Connectivity

- AS31898 (Oracle Corporation)

#### Topology

```mermaid
graph LR
    mikan[
        mikan.yude.jp
        mikan.tail5b1c5.ts.net<br />
        Resource server
        IaaS
    ]

    ponkan[
        ponkan.yude.jp
        ponkan.tail5b1c5.ts.net<br />
        Resource server
        IaaS
    ]
```