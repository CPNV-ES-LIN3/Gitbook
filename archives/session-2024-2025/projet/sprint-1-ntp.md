# Sprint 1 - NTP

## Objectif du sprint

Mise en place de NTP.

#### Infrastructure d'intégration

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

DIAGRAM AS CODE (eraser)

```ssh-config
//eraser
ADMIN-SYS [icon: user]
INTERNET GATEWAY [icon: aws-internet-gateway]

VPC LN3 [icon: aws-vpc] {
  SUBNET PUBLIC{
    SSH-SRV [icon: vpn]
    NAT-SRV [icon: gcp-cloud-nat]
  }

  SUBNET PRIVATE{
    NTP-SRV-LIN[icon: linux]
    NTP-CLI-LIN[icon: linux]
    NTP-CLI-WIN[icon: windows]
  }
}

//INBOUND
ADMIN-SYS -> INTERNET GATEWAY
INTERNET GATEWAY -> SSH-SRV : SSH-22
SSH-SRV -> SUBNET PRIVATE : SSH-22, RDP-3389, NTP-123

NTP-SRV-LIN -> NTP-CLI-LIN : UDP-123
NTP-SRV-LIN -> NTP-CLI-WIN : UPD-123

//OUTBOUND
SUBNET PRIVATE -> NAT-SRV : ALL TRAFFIC
NAT-SRV -> INTERNET GATEWAY: ALL TRAFFIC
```

## Backlog

{% embed url="https://github.com/orgs/CPNV-ES-LIN3/projects/9" %}
