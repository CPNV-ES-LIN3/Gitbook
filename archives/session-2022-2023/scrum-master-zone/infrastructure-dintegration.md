---
description: >-
  Cette page décrit l'infrastructure sur laquelle les techniciens valide leur
  implémentation.
---

# Infrastructure d'intégration

L'infrastructure qui va être mise à disposition des techniciens durant ce projet est inspirée de ce modèle :

![Infrastructure d'intégration](<../../../.gitbook/assets/image (7).png>)

### Déploiement

Le déploiement a été réalisé à l'aide du client en ligne de commande d'AWS pour ce qui est de la configuration du réseau.\
Les instances quant à elles ont été déployés à l'aide de code réalisé en C# à l'aide du SDK d'AWS.\
\


#### Configuration du réseau 

* Création du VPC

```bash
aws ec2 create-vpc --cidr-block 10.0.0.0/16 --region eu-west-2

[Response]
{
    "Vpc": {
        "CidrBlock": "10.0.0.0/16",
        "DhcpOptionsId": "dopt-c45381ad",
        "State": "pending",
        "VpcId": "vpc-0f24b529ceb882a63",
        "OwnerId": "709024702237",
        "InstanceTenancy": "default",
        "Ipv6CidrBlockAssociationSet": [],
        "CidrBlockAssociationSet": [
            {
                "AssociationId": "vpc-cidr-assoc-0ba9e2a821e15a91c",
                "CidrBlock": "10.0.0.0/16",
                "CidrBlockState": {
                    "State": "associated"
                }
            }
        ],
        "IsDefault": false
    }
}
```

* Création d'une internet gateway

```bash
aws ec2 create-internet-gateway --region eu-west-2

[Response]
{
    "InternetGateway": {
        "Attachments": [],
        "InternetGatewayId": "igw-0032b56168d5f074d",
        "OwnerId": "709024702237",
        "Tags": []
    }
}
```

* Connecter l'internet gateway au bon vpc

```bash
aws ec2 attach-internet-gateway --internet-gateway-id igw-0032b56168d5f074d --vpc-id vpc-0f24b529ceb882a63 --region eu-west-2

[Response]
<none>
```

* Création du sous-réseau publique

```bash
aws ec2 create-subnet --vpc-id vpc-0f24b529ceb882a63 --cidr-block 10.0.0.0/24 --availability-zone eu-west-2a --region eu-west-2

[Response]
{
    "Subnet": {
        "AvailabilityZone": "eu-west-2a",
        "AvailabilityZoneId": "euw2-az2",
        "AvailableIpAddressCount": 251,
        "CidrBlock": "10.0.0.0/24",
        "DefaultForAz": false,
        "MapPublicIpOnLaunch": false,
        "State": "available",
        "SubnetId": "subnet-023d0dfc5cc3707b3",
        "VpcId": "vpc-0f24b529ceb882a63",
        "OwnerId": "709024702237",
        "AssignIpv6AddressOnCreation": false,
        "Ipv6CidrBlockAssociationSet": [],
        "SubnetArn": "arn:aws:ec2:eu-west-2:709024702237:subnet/subnet-023d0dfc5cc3707b3"
    }
}
```

* Création des sous-réseaux privés. Prévoir un sous-réseau privé par dev ops teams en modifiant l'intervalle d'adressage.

```bash
aws ec2 create-subnet --vpc-id vpc-0f24b529ceb882a63 --cidr-block 10.0.1.0/24 --availability-zone eu-west-2a --region eu-west-2

[Response]
{
    "Subnet": {
        "AvailabilityZone": "eu-west-2a",
        "AvailabilityZoneId": "euw2-az2",
        "AvailableIpAddressCount": 251,
        "CidrBlock": "10.0.1.0/24",
        "DefaultForAz": false,
        "MapPublicIpOnLaunch": false,
        "State": "available",
        "SubnetId": "subnet-061438118c77e90dd",
        "VpcId": "vpc-0f24b529ceb882a63",
        "OwnerId": "709024702237",
        "AssignIpv6AddressOnCreation": false,
        "Ipv6CidrBlockAssociationSet": [],
        "SubnetArn": "arn:aws:ec2:eu-west-2:709024702237:subnet/subnet-061438118c77e90dd"
    }
}
```

* Création des tables de routage. Prévoir une table par sous-réseau.&#x20;

```bash
aws ec2 create-route-table --vpc-id vpc-0f24b529ceb882a63 --region eu-west-2

[Response]
{
    "RouteTable": {
        "Associations": [],
        "PropagatingVgws": [],
        "RouteTableId": "rtb-041ef8cd8166c1a08",
        "Routes": [
            {
                "DestinationCidrBlock": "10.0.0.0/16",
                "GatewayId": "local",
                "Origin": "CreateRouteTable",
                "State": "active"
            }
        ],
        "Tags": [],
        "VpcId": "vpc-0f24b529ceb882a63",
        "OwnerId": "709024702237"
    }
}
```

* Ajouter la route permettant au trafic de sortir du réseau publique (et du vpc)

```bash
aws ec2 create-route --route-table-id rtb-0e69af3d995d97c30 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-0032b56168d5f074d --region eu-west-2

[Response]
{
    "Return": true
}
```

###

### Déploiement des instances

* Création des clés asymétriques

```bash
aws ec2 create-key-pair --key-name LIN3_EKIP --region eu-west-2
{
    "KeyFingerprint": "01:6d:96:a6:*:*:*:*:*:*:*:*",
    "KeyMaterial": "-----BEGIN RSA PRIVATE KEY--**--END RSA PRIVATE KEY-----",
    "KeyName": "LIN3_EKIP",
    "KeyPairId": "key-021fa01ee9f8a7eb6"
}
```

* Configuration des groupes de sécurité

```bash
aws ec2 create-security-group --description SSH_NAT --group-name SSH_NAT --vpc-id vpc-0f24b529ceb882a63 --region eu-west-2

[Response]
{
    "GroupId": "sg-04d24bff3d76dd065"
}

```

### Spécificités au  niveau des instances

Sur les instances Linux, le package "chrony" doit être désinstallé pour permettre aux techniciens de partir sur une base propre.\
\
` ```bash `

```
//on Debian Buster
sudo apt-get autoremove --purge chrony

//on Centos 8
sudo yum remove chrony
```

` ``` `

### Maintenance et réduction des coûts

Les instances ne sont disponibles que lors des livraisions. Pas besoin des scripts concernant les arrêts/démarrages/backups.





