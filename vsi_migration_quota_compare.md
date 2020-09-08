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

# Gen 1 and Gen 2 quota and limit comparisons
{: #migrating-quotas-limits}

These tables list the {{site.data.keyword.cloud}} Virtual Private Cloud resources and their Gen 1 and Gen 2 quotas and limits.

## Virtual Server Instances
{: #migrating-vsi-quotas}

|Resource|Gen 1 Quotas|Gen 2 Quotas|
|-----|-----|-----|
|vCPU|---|200 per region|
|RAM|---|1600 GB per region|
|Floating IP addresses|100 per zone per account|20 per zone|
|SSH keys|100 per account|200 per account|
|Virtual server instances|20 per region|---|
|vNICs per instance|5 per instance|---|

## VPCs
{: #migrating-vpc-quotas}

|Resource|Gen 1 Quotas|Gen 2 Quotas|
|-----|-----|-----|
|Virtual private clouds|5 per region (can request an increase)|10 per region|
|Subnets|15 per Virtual Private Cloud (can request an increase)|15 per VPC|
|Address prefixes|5 per VPC per zone|15 per VPC|
|VPCs with Classic access|1 per region|--|
|Public Gateways|1 per VPC per zone|--|

## Access Control Lists
{: #migrating-acl-quotas}

|Resource|Gen 1 Quotas|Gen 2 Quotas|
|-----|-----|-----|
|ACLs|2 x number of subnets per VPC|50 per VPC|
|Inbound rules|20 per ACL|---|
|Outbound rules|20 per ACL|---|

In Gen 2,  you can use the ACL quota for inbound rules, outbound rules, or both. For example, you might have 40 inbound rules and 10 outbound rules per ACL.

## Security Groups
{: #migrating-secgrp-quotas}

|Resource|Gen 1 Quotas|Gen 2 Quotas|
|-----|-----|-----|
|Security groups|5 per network instance<br> 500 per account|25 per VPC<br>---|
|Rules|50 per security group|25 per security group|
|Remote rules|5 per security group|5 per security group|
|Network interfaces|100 per security group|5 per security group|


## VPNs
{: #migrating-vpns-quotas}

|Resource|Gen 1 Quotas|Gen 2 Quotas|
|-----|-----|-----|
|VPN gateways|9 per region, 3 per zone|9 per region, 3 per zone|
|VPN connections|10 per VPN gateway|10 per VPN gateway|
|IKE policies|20 per region|20 per region|
|IPsec policies|20 per region|20 per region|
|Peer subnets|50 across all connections of a VPN gateway, 15 per individual VPN connection|50 across all connections of a VPN gateway, 15 per individual VPN connection|
|Local subnets|50 across all connections of a VPN gateway, 15 per individual VPN connection|50 across all connections of a VPN gateway, 15 per individual VPN connection|

## Load Balancers
{: #migrating-lbs-quotas}

|Resource|Gen 1 Quotas|Gen 2 Quotas|
|-----|-----|-----|
|Load balancers|20 per account|20 per region|
|Listeners|10 per Load Balancer|10 per load balancer|
|Pools|10 per Load balancer|10 per load balancer|
|Members|50 per Pool |50 per pool|
|Policies|----|10 per listener|
|Rules|----|10 per policy|

## Custom Routing Tables and Routes
{: #migrating-routing-quotas}

|Resource|Gen 1 Quotas|Gen 2 Quotas|
|-----|-----|-----|
|User-defined custom routing tables per VPC|----|Default limit: 15<br>Maximum limit: 200|
|User-defined routes per custom routing table|----|Default limit: 100<br>Maximum limit: 400|

## Block Storage Volumes
{: #migrating-storage-quotas}

|Resource|Gen 1 Quotas|Gen 2 Quotas|
|-----|-----|-----|
|Boot and secondary volumes|300 total volumes per account in a region |300 total volumes per account in a region|
|Secondary volumes per instance, when creating an instance|4 secondary volumes|----|
|Secondary volumes per instance, for existing instances with fewer than 4 cores|4 secondary volumes|----|
|Secondary volumes per instance, for existing instances with 4 cores or more|Up to 12 secondary volumes|----|


## Service Limits
{: #migrating-service-limits}

|Resource|Gen 1 Limits|Gen 2 Limits|
|-----|-----|-----|
|VPCs with classic access|----|1 per region|
|Network interfaces|----|5 per instance|
|Public Gateways|----|1 per zone per VPC|
|Secondary volumes per instance, attached when creating an instance|----|4 secondary volumes|
|Secondary volumes per instance, for existing instances with fewer than 4 cores|----|4 secondary volumes|
|Secondary volumes per instance, for existing instances with 4 cores or more|----|Up to 12 secondary volumes|
|Instance groups for auto scale and more|----|200 per account|
|Instance group memberships|----|1000 per instance group|
