---

copyright:
  years: 2020
lastupdated: "2020-08-20"

keywords:
subcollection: vpc-on-classic

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:note: .note}
{:tip: .tip}
{:important: .important}
{:table: .aria-labeledby="caption"}

# Instructions for Migrating from VPC (Gen 1) to VPC (Gen 2)
{: #migrating-vpc}

This topic is a guide for migrating your VPC (Gen 1) infrastructure to VPC (Gen 2). For more information on this migration, refer to [About Migrating from VPC (Gen 1) to VPC (Gen 2)](/docs/vpc-on-classic?topic=vpc-on-classic-migrating-faqs).

IBM has a vendor available, at no cost, to help you with your migration process. Contact your IBM representative for more information on this service.
{: tip}

If you decide to complete this migration without assistance, use this topic as a guide.

## Before you begin
{: #migrating-before}
Refer to the following topics for information on the benefits of migrating and the differences between VPC Gen 1 and Gen 2 environments:

* [About Migrating from VPC (Gen 1) to VPC (Gen 2)](/docs/vpc-on-classic?topic=vpc-on-classic-migrating-faqs)
* [Gen 1 and Gen 2 Quota and Limit Comparisons](/docs/vpc-on-classic?topic=vpc-on-classic-migrating-quotas-limits)
* [Pricing for VPC Gen 1 and Gen 2](https://www.ibm.com/cloud/vpc/pricing){: external}

## Step 1: Gather information about your current Gen 1 environment
{: #migrating-gather-info}

Your first step is to capture configuration details of each resource in your current Gen 1 environment by using the {{site.data.keyword.cloud_notm}} console, {{site.data.keyword.cloud_notm}} API, or the {{site.data.keyword.cloud_notm}} CLI. The APIs or CLI are the most efficient methods to capture this information. Refer to the following information:
* [VPC CLI Reference](/docs/vpc-on-classic?topic=vpc-on-classic-vpc-reference)
* [VPC CLI quick reference](/docs/vpc-on-classic?topic=vpc-on-classic-quick-reference-to-cli-commands-for-resources)
* [Virtual Private Cloud API (Gen 1 compute)](/apidocs/vpc-on-classic)
* [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}

For a full list of parameter values that you need to identify, see [VPC Gen 2 configuration parameters](#gen-2-parameters).

## Step 2: Determine multi-zone region availability
{: #migrating-mzr}
Not all multi-zone regions (MZR) support both Gen 1 and Gen 2. For a list of services available by location, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

If Gen 2 is not available in the same location of your Gen 1 infrastructure, contact your IBM representative.

## Step 3: Create your Gen 2 VPC
{: #migrating-create-vpc}

Refer to:
* [Getting started with Virtual Private Cloud](/docs/vpc?topic=vpc-getting-started)
* [Choosing IP ranges for your VPC](/docs/vpc?topic=vpc-choosing-ip-ranges-for-your-vpc)

You need to provide the following information:
* VPC name
* Region
* Zone
* Resource group
* Default subnet
* Address prefix

## Step 4: Creating your subnets
{: #migrating-subnet}
If your Gen 1 network is flat, you can skip to Step 5.

If your Gen 1 network is more complex and your virtual servers are spread across different subnets, create more subnets in your Gen 2 VPC to match the Gen 1 network architecture.  

For any subnets that require internet access, you need to attach a public gateway. The floating IP for a Gen 2 public gateway is randomly selected and therefore is different from a Gen 1 public gateway.

If the subnets you create in Gen 2 exceed the address prefix size, create more prefixes to accommodate the overflow. In addition, VPC routes can be created to specific route flows.

If your Gen 1 environment has more subnets in other address prefixes, create the additional prefixes in Gen 2 to match Gen 1. Also, check for any specific route flows in Gen 1. You need to configure these route flows in Gen 2.

Refer to:

* [Designing an addressing plan for a VPC](/docs/vpc?topic=vpc-choosing-ip-ranges-for-your-vpc/docs/vpc?topic=vpc-vpc-addressing-plan-design)
* [External connectivity (public gateway)](/docs/vpc?topic=vpc-about-networking-for-vpc#external-connectivity)
* [Setting up advanced routing in VPC](/docs/vpc?topic=vpc-advanced-routing)

## Step 5: Creating ACLs
{: #migrating-acl}
If your Gen 1 environment has ACLs to control traffic between subnets, replicate the same rules in Gen 2.

VPC Gen 1 ACLs are not VPC-specific and must be attached to more than one VPC. In VPC Gen 2, ACLs are specific to each VPC. If you have ACLs that are attached to more than one VPC in Gen 1, add duplicate ACLs for each VPC in Gen 2.
{: note}

Refer to:
* [Security in your VPC](/docs/vpc?topic=vpc-security-in-your-vpc)
* [Setting up network ACLs](/docs/vpc?topic=vpc-using-acls)

## Step 6: Copying your SSH keys
{: #migrating-ssh-keys}

SSH keys are required to access any virtual server instance. Copy all SSH keys from Gen 1 that are needed to access the virtual server instances.

Refer to:
[SSH keys](/docs/vpc?topic=vpc-ssh-keys)

## Step 7: Creating security groups
{: #migrating-security-groups}

If you use security groups to control host access in Gen 1, then you can create the security groups before you create the virtual server instances, or you can create the security groups as you create the virtual servers instances.

If your Gen 1 environment has multiple security groups, complete this step for each security group and the associated rules.

Refer to:
* [Security groups](/docs/vpc?topic=vpc-security-in-your-vpc#sgs-security)
* [Using security groups](/docs/vpc?topic=vpc-using-security-groups)

## Step 8: Migrating virtual servers and volumes
{: #migrating-vsi}

Capture the following information for all virtual server instances in your Gen 1 environment:
* Name
* VPC
* Resource group
* Location
* Profile
* OS type
* User data
* Data volumes
  * Size
  * IOPS
* Network
  * Interface
  * Subnet
  * IP address
  * Security group

There is no guarantee that your Gen 2 virtual servers can obtain the same IP address; it is best to create the virtual servers based on the sequence of the IP assignment. If the virtual servers and IP address do not match, you might need to go back and rename the virtual servers to match Gen 1.

For any virtual servers that have floating IP addresses, you can configure the floating IP after you create the virtual servers by attaching the floating IP to the interface. You can also create the floating IP first and then attach it to the virtual server after it is created. Floating IP addresses are different from Gen 1.

VDH image types are not supported in {{site.data.keyword.vpc_short}}. Only qcow2 is supported.
{: note}

Use one of the following procedures to migrate data from your volumes. If your Gen 1 environment has multiple volumes, complete the steps for each volume.

### Option – 1 (Linux&reg; and Windows)
{: #option1}
1. Provision a VPC Gen 2 virtual machine with the CPU, RAM, and operating system that you want.
2. Create a {{site.data.keyword.cos_full_notm}} bucket. If you already have a {{site.data.keyword.cos_full_notm}} bucket, you can use your existing one.
3. Log in to the VPC Gen 1 virtual machine and upload data to object storage. Refer to [Upload data](/docs/cloud-object-storage?topic=cloud-object-storage-upload).
4. Log in to newly provisioned VPC Gen 2 virtual machine and use download data from the {{site.data.keyword.cos_short}} bucket.

### Option – 2 (Linux Only)
{: #option2}
1. Provision a VPC Gen 2 virtual machine with the CPU, RAM, and operating system that you want.
2. Assign a floating IP, if you have not already, to the newly provisioned virtual machine.
3. Log in to the VPC Gen 1 virtual machine and transfer the data by using an `scp` command. For example:
```
  scp -i /path/to/private-key -r /root/data root@<floating IP>:/root
```

For more information, see:
* [About virtual server instances for VPC](/docs/vpc?topic=vpc-about-advanced-virtual-servers)
* [Getting started with {{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage)


## Step 9: Creating any load balancers that are tied to virtual servers
{: #migrating-lb}

For every load balancer in Gen 1, create a matching load balancer in Gen 2.

The floating IP is different from Gen 1.
{: note}

Refer to:
[Load balancers overview](/docs/vpc?topic=vpc-nlb-vs-elb)


## Step 10: Considerations for related services
{: #migrating-other-services}
You will also need to migrate other related services that you are using, such as:
* IAM Authorizations
* Links or references to KMS (Key Protect/HPCS).
* Kubernetes instances that are tied to your VPC
* CIS tied to VPC load balancer
* VPN
* Custom images
* Terraform templates
* Shell scripts


## Reference: all VPC Gen 2 configuration parameters
{: #gen-2-parameters}

### VPC
{: #migrating-vpc-params}

|Parameter|Sub-parameters and Notes|
|--|--|
|VPC Name||
|Region||
|Zone||
|Resource Group||
|Tags||
|Address Prefix|IP range|
|Subnets||
{: caption="Table 1. VPC parameters" caption-side="top"}

### Access control lists
{: #migrating-vpc-acl-params}

|Parameter|Sub-parameters and Notes|
|--|--|
|VPC||
|Names||
|Rules|Inbound<br>Outbound<br>Rule priority<br>Allow/Deny<br>Protocol<br>Source<br>Destination<br>Value|
{: caption="Table 2. Access control list parameters" caption-side="top"}

### Security groups
{: #migrating-vpc-security-groups-params}

If you have multiple security groups, gather this information for each security group and the associated rules.

|Parameter|Sub-parameters and Notes|
|--|--|
|VPC||
|Resource group||
|Name||
|Network interface||
|Rules|Inbound<br>Outbound<br>Protocol<br>Source<br>Destination<br>Value|
{: caption="Table 3. Security group parameters" caption-side="top"}

### Load balancers
{: #migrating-vpc-load-balancers-params}

If you have multiple load balancers, gather the following information each instance.

|Parameter|Sub-parameters and Notes|
|--|--|
|Name||
|VPC||
|Resource group||
|Type|Public<br>Private||
|Subnet||
|Floating IP||
|Backend pool|Name<br>Protocol<br>Method<br>Health path<br>Virtual server instance|
|Frontend listeners|Protocol<br>Ports<br>SSL certs<br>Backend pool|
|SSL certificates||
{: caption="Table 4. Load balancer parameters" caption-side="top"}

### Public Gateways
{: #migrating-vpc-public-gateway-params}

|Parameter|Sub-parameters and Notes|
|--|--|
|Name||
|Associated floating IP||
{: caption="Table 5. Public gateway parameters" caption-side="top"}

### VPN gateways
{: #migrating-vpc-vpn-gateway-params}

VPN gateway for remote connectivity.

If you have multiple VPN gateways, complete the following steps for each instance.

|Parameter|Sub-parameters and Notes|
|--|--|
|Name||
|VPC||
|Resource group||
|Subnet||
|Connections|Name<br>Peer gateway address<br>Pre-shared key<br>Local Subnet<br>Remote subnet|
|Dead peer detection|Dead peer detection action<br>Interval<br>Timeout|
|IKE policy|Name<br>Resource group<br>IKE version<br>Authentication<br>Encryption<br>DH group<br>Key lifetime|
|IPSec policy|Name<br>Resource group<br>Authentication<br>Encryption<br>PFS and DH group<br>Key lifetime|
{: caption="Table 6. VPN gateway parameters" caption-side="top"}

### Virtual server instances
{: #migrating-vpc-vsi-params}

|Parameter|Sub-parameters and Notes|
|--|--|
|Names||
|VPC||
|Resource group
|Image||
|Profile|Balanced<br>Compute<br>Memory|
|SSH key||
|Boot volume||
|Data volume|<br>Name<br>Profile<br>Size<br>IOPS<br>Encryption|
|Interfaces||
|If more than one interface|Interface name<br>Subnet<br>Security group|
|Attached SSH keys||
|Attached security groups||
{: caption="Table 7. Virtual server instance parameters" caption-side="top"}

### Secondary volumes
{: #migrating-vpc-secondary-volumes-params}

If you have multiple volumes that are attached to an instance, the following steps for each volume.

|Parameter|Sub-parameters and Notes|
|--|--|
|Attached to what instance||
|Mount||
|Download data||
|Extract data||
{: caption="Table 8. Secondary volume parameters" caption-side="top"}

### SSH keys
{: #migrating-vpc-ssh-keys-params}
If you have multiple keys, complete the following steps for each SSH key.

|Parameter|Sub-parameters and Notes|
|--|--|
|Name||
|Resource group||
|Public keys||
{: caption="Table 9. SSH key parameters" caption-side="top"}
