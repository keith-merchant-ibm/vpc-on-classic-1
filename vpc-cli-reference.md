---

copyright:
  years: 2017, 2020
lastupdated: "2020-10-20"

keywords:

subcollection: vpc-on-classic

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}
{:external: target="_blank" .external}

# VPC CLI reference
{: #vpc-reference}

This document provides a reference of the command line interface (CLI) commands available for the functionality of the {{site.data.keyword.cloud}} Virtual Private Cloud (Gen 1 compute).

This VPC CLI is for use with generation 1 compute resources. Generation 1 resources aren't compatible with generation 2 resources. To view the CLI for generation 2 resources, see the [CLI for VPC for generation 2 compute](/docs/vpc?topic=vpc-infrastructure-cli-plugin-vpc-reference).
{:important}

The commands are organized into the following sections. Similar commands to execute these functions also are available as [API commands](https://{DomainName}/apidocs/vpc-on-classic){: external}.

* [Target commands](#target)
* [Compute commands](#compute-section)
* [Network commands](#network-cli-section)
* [Regions and zones commands](#geography-section)
* [Storage commands](#storage-cli-section)
* [VPN commands](#vpn-section)


## Prerequisites
{: #cli-prerequisites}

1. Install the [IBM Cloud CLI](/docs/cli?topic=cli-install-ibmcloud-cli).
2. Install or update the `vpc-infrastructure` plug-in.

  ```
  ibmcloud plugin install vpc-infrastructure
  ```
  {: pre}

  To update:

  ```
  ibmcloud plugin update
  ```
  {: pre}

  To view installed plug-ins and versions:

  ```
  ibmcloud plugin list
  ```
  {: pre}

3. Set target generation for compute resources as `1`.

   ```
   ibmcloud is target --gen 1
   ```
   {: pre}


## TARGET COMMANDS
{: #target}
This command targets the generation of compute resources, (Gen 1) or ( Gen 2).


### ibmcloud is target
{: #ibmcloud-is-target}

Target the generation of compute resources.

```
ibmcloud is target [--gen 2 | 1] [--output JSON] [-q, --quiet]
```

#### Command options
{: #ibmcloud-is-target-command-options}

- **--gen**: Generation of compute resources. Default is **2**. You must set the value to **1** to access generation 1 resources. One of: **2**, **1**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #ibmcloud-is-target-examples}

- `ibmcloud is target`
- `ibmcloud is target --gen 1`

---

## COMPUTE COMMANDS
{: #compute-section}
This section contains a reference for the CLI commands related to compute functionality in the IBM Cloud VPC, including profiles, images, keys, and instances.

## Profiles
{: #profiles-section}
The following section provides information about CLI commands for profiles.

### ibmcloud is instance-profiles
{: #instance-profiles}

List all virtual server instance profiles in the region.

```
ibmcloud is instance-profiles [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-profiles-command-options}

- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-profile
{: #instance-profile}

View details of a virtual server instance profile.

```
ibmcloud is instance-profile PROFILE_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-profile-command-options}

- **PROFILE_NAME**: Name of the profile.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

## Images
{: #images-section}
The following section provides information about CLI commands for images.

### ibmcloud is operating-systems
{: #operating-systems}

List all operating systems.

```
ibmcloud is operating-systems [--output JSON] [-q, --quiet]
```

#### Command options
{: #operating-systems-command-options}

- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is operating-system
{: #operating-system}

View details of an operating system.

```
ibmcloud is operating-system OPERATING_SYSTEM_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #operating-system-command-options}

- **OPERATING_SYSTEM_NAME**: Name of the operating system.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is images
{: #images}

List all images in the region.

```
ibmcloud is images [--visibility public | private] [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME | --all-resource-groups] [--output JSON] [-q, --quiet]
```

#### Command options
{: #images-command-options}

- **--visibility**: List images with given visibility. Valid visibility is: **public** or **private**.
- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--all-resource-groups**: Query all resource groups.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is image
{: #image}

View details of an image.

```
ibmcloud is image IMAGE [--output JSON] [-q, --quiet]
```

#### Command options
{: #image-command-options}

- **IMAGE**: ID of the image.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is image-create
{: #image-create}

Create an image.

```
ibmcloud is image-create IMAGE_NAME --file IMAGE_FILE_LOCATION --os-name OPERATING_SYSTEM_NAME [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #image-create-command-options}

- **IMAGE_NAME**: Name of the image.
- **--file**: The Cloud Object Store (COS) location of the image file, for example: **cos://us-south/custom-image-vpc-bucket/customImage-0.vhd**.
- **--os-name**: The name of the operating system for this image.
- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #image-create-examples}

- `ibmcloud is image-create My-ubuntu-16-amd64 --file cos://us-south/custom-image-vpc-bucket/customImage-0.vhd --os-name ubuntu-16-amd64`
- `ibmcloud is image-create My-ubuntu-16-amd64 --file cos://us-south/custom-image-vpc-bucket/customImage-0.vhd --os-name ubuntu-16-amd64 --resource-group-id fee82deba12e4c0fb69c3b09d1f12345`
- `ibmcloud is image-create My-ubuntu-16-amd64 --file cos://us-south/custom-image-vpc-bucket/customImage-0.vhd --os-name ubuntu-16-amd64 --resource-group-name Default`
- `ibmcloud is image-create My-ubuntu-16-amd64 --file cos://us-south/custom-image-vpc-bucket/customImage-0.vhd --os-name ubuntu-16-amd64 --output JSON`

---

### ibmcloud is image-update
{: #image-update}

Update an image.

```
ibmcloud is image-update IMAGE --name NEW_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #image-update-command-options}

- **IMAGE**: ID of the image.
- **--name**: New name of the image.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #image-update-examples}

`ibmcloud is image-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --name my-image`

---

### ibmcloud is image-delete
{: #image-delete}

Delete images.

```
ibmcloud is image-delete (IMAGE1 IMAGE2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #image-delete-command-options}

- **IMAGE1**: ID of the image.
- **IMAGE2**: ID of the image.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

## Keys
{: #keys-section}
The following section provides information about CLI commands for keys.

### ibmcloud is keys
{: #keys}

List all keys.

```
ibmcloud is keys [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME | --all-resource-groups] [--output JSON] [-q, --quiet]
```

#### Command options
{: #keys-command-options}

- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--all-resource-groups**: Query all resource groups.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is key
{: #key}

View details of a key.

```
ibmcloud is key KEY [--output JSON] [-q, --quiet]
```

#### Command options
{: #key-command-options}

- **KEY**: ID of the key.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is key-create
{: #key-create}

Import an RSA public key.

```
ibmcloud is key-create KEY_NAME (KEY | @KEY_FILE) [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #key-create-command-options}

- **KEY_NAME**: Name of the key.
- **KEY**: **key**|**@key-file**. The public SSH key to import into the system.
- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #key-create-examples}

- `ibmcloud is key-create my-key "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDL9osaBrUD8uCBzIJo5YBvX8wtGrE+kcC7YZtID/nNYrjeCB26eFASHia5tmqmuCo434UygGSd5qj3t/3v/a7NZoMr/0+qspQF+dUVIl+xIsKTWYQ+gtYbJlvW+FIlNTOA4vbOXLg+nGGUCoaV79azmny4mYJbbo15i+Q3CI+w9bwOAwzqeGKaeOjpo5hdDcFW0QLDxKmQHKMLX8slsx3kB9I5wPe8C/ZBBDBBkZKK2y3RJBjaKxi0beFueo6ngUKOLooReefiBGpdoOJIi6Gf7vRduoBTmbyVvSv08wcrANtYSzGwDpqrEshEafv8bKo42MYHsPT2OwAbsFyqWQj5 test@example"`
- `ibmcloud is key-create my-key @/tmp/my_id_rsa.pub`
- `ibmcloud is key-create my-key @/tmp/my_id_rsa.pub --output JSON`

---

### ibmcloud is key-update
{: #key-update}

Update the name of a key.

```
ibmcloud is key-update KEY --name NEW_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #key-update-command-options}

- **KEY**: ID of the key.
- **--name**: New name for the key.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #key-update-examples}

- `ibmcloud is key-update e9e7655e-0000-0000-0000-0000001a957a  --name my-new-name`
- `ibmcloud is key-update e9e7655e-0000-0000-0000-0000001a957a  --name my-new-name --output JSON`

---

### ibmcloud is key-delete
{: #key-delete}

Delete keys.

```
ibmcloud is key-delete (KEY1 KEY2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #key-delete-command-options}

- **KEY1**: ID of the key.
- **KEY2**: ID of the key.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

## Instances
{: #instances-section}
The following section provides information about CLI commands for instances.

### ibmcloud is instances
{: #instances}

List all virtual server instances.

```
ibmcloud is instances [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME | --all-resource-groups] [--output JSON] [-q, --quiet]
```

#### Command options
{: #instances-command-options}

- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--all-resource-groups**: Query all resource groups.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance
{: #instance}

View details of a virtual server instance.

```
ibmcloud is instance INSTANCE [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-command-options}

- **INSTANCE**: ID of the instance.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-create
{: #instance-create}

Create a virtual server instance.

```
ibmcloud is instance-create INSTANCE_NAME VPC ZONE_NAME PROFILE_NAME SUBNET --image-id IMAGE_ID [--boot-volume BOOT_VOLUME_JSON | @BOOT_VOLUME_JSON_FILE] [--volume-attach VOLUME_ATTACH_JSON | @VOLUME_ATTACH_JSON_FILE] [--key-ids IDS] [--user-data DATA] [([--security-group-ids SECURITY_GROUP_IDS] [--ipv4 IPV4_ADDRESS]) | --primary-network-interface PRIMARY_NETWORK_INTERFACE_JSON | @PRIMARY_NETWORK_INTERFACE_JSON_FILE] [--network-interface NETWORK_INTERFACE_JSON | @NETWORK_INTERFACE_JSON_FILE] [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME] [--output JSON] [-i, --interactive] [-q, --quiet]
```

#### Command options
{: #instance-create-command-options}

- **INSTANCE_NAME**: Name of the instance.
- **VPC**: ID of the VPC.
- **ZONE_NAME**: Name of the zone.
- **PROFILE_NAME**: Name of the profile.
- **SUBNET**: ID of the subnet.
- **--image-id**: ID of the image.
- **--boot-volume**: BOOT_VOLUME_JSON|@BOOT_VOLUME_JSON_FILE, boot volume attachment in JSON or JSON file.
- **--volume-attach**: VOLUME_ATTACH_JSON|@VOLUME_ATTACH_JSON_FILE, volume attachment in JSON or JSON file, list of volumes.
- **--key-ids**: Comma-separated IDs of SSH keys.
- **--user-data**: data|@data-file. User data to transfer to the virtual server instance.
- **--security-group-ids**: Comma-separated security group IDs for primary network interface.
- **--ipv4**: Primary IPv4 address for the primary network interface.
- **--primary-network-interface**: PRIMARY_NETWORK_INTERFACE_JSON|@PRIMARY_NETWORK_INTERFACE_JSON_FILE, primary network interface in JSON or JSON file.
- **--network-interface**: NETWORK_INTERFACE_JSON|@NETWORK_INTERFACE_JSON_FILE, network interface attachment in JSON or JSON file.
- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--interactive, -i**: Supply the parameters under interactive mode. This option is mutually exclusive with all other arguments and options.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #instance-create-examples}

- `ibmcloud is instance-create my-instance-name 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 us-south-1 bc1-4x16 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --image-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8`
- `ibmcloud is instance-create my-instance-name 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 us-south-1 bc1-4x16 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --image-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --volume-attach '[{"volume": {"name":"my-volume-name", "capacity":10, "profile": {"name": "general-purpose"}}}]'`
Create instance with volume attachment.
- `ibmcloud is instance-create my-instance-name 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 us-south-1 bc1-4x16 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --image-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --volume-attach '[{"volume": {"id":"67531475-bd8a-478e-bcfe-2e53365cd0aa"}}]'`
Create instance with existing volume in volume attachment.
- `ibmcloud is instance-create my-instance-name 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 us-south-1 bc1-4x16 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --image-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --key-ids 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8,72b27b5c-f4b0-48bb-b954-5becc7c1dcb3`
Create instance with multiple SSH keys.
- `ibmcloud is instance-create my-instance-name 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 us-south-1 bc1-4x16 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --image-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --boot-volume '{"name": "boot-vol-name", "volume": {"profile": {"name": "general-purpose"},"encryption_key": {"crn": "crn:v1:bluemix:public:kms:us-south:adffc98a0f1f0f95f6613b3b752286b87:e4a29d1a-2ef0-42a6-8fd2-350deb1c647e:key:5437653b-c4b1-447f-9646-b2a2a4cd6179"}}}'`
Create instance with encrypted boot volume.
- `ibmcloud is instance-create my-instance-name 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 us-south-1 bc1-4x16 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --image-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --network-interface '[{"name": "secondary-nic", "subnet": {"id":"72b27b5c-f4b0-48bb-b954-5becc7c1dcb3"}, "security_groups": [{"id": "72b27b5c-f4b0-48bb-b954-5becc7c1dcb8"}, {"id": "72b27b5c-f4b0-48bb-b954-5becc7c1dcb3"}]}]'`
Create instance that is attached to secondary network interface.
- `ibmcloud is instance-create my-instance-name 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 us-south-1 bc1-4x16 --image-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --primary-network-interface '{"name": "primary-nic", "subnet": {"id":"72b27b5c-f4b0-48bb-b954-5becc7c1dcb3"}, "primary_ipv4_address": "10.240.129.10", "security_groups": [{"id": "72b27b5c-f4b0-48bb-b954-5becc7c1dcb8"}, {"id": "72b27b5c-f4b0-48bb-b954-5becc7c1dcb3"}]}'`
Create instance with primary network interface configuration in JSON.
- `ibmcloud is instance-create my-instance-name 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 us-south-1 bc1-4x16 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --image-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --security-group-ids 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8,72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --ipv4 10.240.129.10`
Create instance with primary network interface configuration that includes security groups and primary IPv4 address
- `ibmcloud is instance-create --interactive`
Create instance interactively.

---

### ibmcloud is instance-update
{: #instance-update}

Update a virtual server instance.

```
ibmcloud is instance-update INSTANCE --name NEW_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-update-command-options}

- **INSTANCE**: ID of the instance.
- **--name**: New name of the virtual server instance.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #instance-update-examples}

- `ibmcloud is instance-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --name my-instance`
- `ibmcloud is instance-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --name my-instance --output JSON`

---

### ibmcloud is instance-delete
{: #instance-delete}

Delete virtual server instances.

```
ibmcloud is instance-delete (INSTANCE1 INSTANCE2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #instance-delete-command-options}

- **INSTANCE1**: ID of the instance.
- **INSTANCE2**: ID of the instance.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-initialization-values
{: #instance-initialization-values}

View initialization details of a virtual instance.

```
ibmcloud is instance-initialization-values INSTANCE [--private-key (KEY | @KEY_FILE)] [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-initialization-values-command-options}

- **INSTANCE**: ID of the instance.
- **--private-key**: **key**|**@key-file**. The private key in PEM format to decrypt Windows administrator default password.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-start
{: #instance-start}

Start a virtual server instance.

```
ibmcloud is instance-start INSTANCE [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-start-command-options}

- **INSTANCE**: ID of the instance.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-stop
{: #instance-stop}

Stop a virtual server instance.

```
ibmcloud is instance-stop INSTANCE [-f, --force] [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-stop-command-options}

- **INSTANCE**: ID of the instance.
- **--force, -f**: Force the operation without confirmation.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-reboot
{: #instance-reboot}

Restart the operating system of an instance.

```
ibmcloud is instance-reboot INSTANCE [-f, --force] [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-reboot-command-options}

- **INSTANCE**: ID of the instance.
- **--force, -f**: Force the operation without confirmation.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-reset
{: #instance-reset}

Power off and then power on an instance.

```
ibmcloud is instance-reset INSTANCE [-f, --force] [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-reset-command-options}

- **INSTANCE**: ID of the instance.
- **--force, -f**: Force the operation without confirmation.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-network-interfaces
{: #instance-network-interfaces}

List all network interfaces of a virtual server instance.

```
ibmcloud is instance-network-interfaces INSTANCE [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-network-interfaces-command-options}

- **INSTANCE**: ID of the instance.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-network-interface
{: #instance-network-interface}

View details of a network interface of a virtual server instance.

```
ibmcloud is instance-network-interface INSTANCE NIC [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-network-interface-command-options}

- **INSTANCE**: ID of the instance.
- **NIC**: ID of the network interface.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-network-interface-floating-ips
{: #instance-network-interface-floating-ips}

List all floating IPs associated with a network interface.

```
ibmcloud is instance-network-interface-floating-ips INSTANCE NIC [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-network-interface-floating-ips-command-options}

- **INSTANCE**: ID of the instance.
- **NIC**: ID of the network interface.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-network-interface-floating-ip
{: #instance-network-interface-floating-ip}

View details of a floating IP associated with a network interface.

```
ibmcloud is instance-network-interface-floating-ip INSTANCE NIC FLOATING_IP [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-network-interface-floating-ip-command-options}

- **INSTANCE**: ID of the instance.
- **NIC**: ID of the network interface.
- **FLOATING_IP**: ID of the floating IP.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-network-interface-floating-ip-add
{: #instance-network-interface-floating-ip-add}

Associate a floating IP with a network interface.

```
ibmcloud is instance-network-interface-floating-ip-add INSTANCE NIC FLOATING_IP [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-network-interface-floating-ip-add-command-options}

- **INSTANCE**: ID of the instance.
- **NIC**: ID of the network interface.
- **FLOATING_IP**: ID of the floating IP.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #instance-network-interface-floating-ip-add-examples}

- `ibmcloud is instance-network-interface-floating-ip-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 1a6b7274-678d-4dfb-8981-c71dd9d4daa5 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3`
- `ibmcloud is instance-network-interface-floating-ip-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 1a6b7274-678d-4dfb-8981-c71dd9d4daa5 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --output JSON`

---

### ibmcloud is instance-network-interface-floating-ip-remove
{: #instance-network-interface-floating-ip-remove}

Disassociate a floating IP from a network interface.

```
ibmcloud is instance-network-interface-floating-ip-remove INSTANCE NIC FLOATING_IP [-f, --force] [-q, --quiet]
```

#### Command options
{: #instance-network-interface-floating-ip-remove-command-options}

- **INSTANCE**: ID of the instance.
- **NIC**: ID of the network interface.
- **FLOATING_IP**: ID of the floating IP.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-volume-attachment
{: #instance-volume-attachment}

View details of a volume attachment.

```
ibmcloud is instance-volume-attachment INSTANCE VOLUME_ATTACHMENT [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-volume-attachment-command-options}

- **INSTANCE**: ID of the instance.
- **VOLUME_ATTACHMENT**: ID of the volume attachment.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-volume-attachment-add
{: #instance-volume-attachment-add}

Create a volume attachment, connecting a volume to an instance.

```
ibmcloud is instance-volume-attachment-add NAME INSTANCE VOLUME [--auto-delete false | true] [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-volume-attachment-add-command-options}

- **NAME**: Name of the volume attachment.
- **INSTANCE**: ID of the instance.
- **VOLUME**: ID of the volume.
- **--auto-delete**: The attached volume is deleted when the instance is deleted. One of: **false**, **true**. (default: **false**).
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #instance-volume-attachment-add-examples}

- `ibmcloud is instance-volume-attachment-add data-vol-name 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 1a6b7274-678d-4dfb-8981-c71dd9d4daa5`
- `ibmcloud is instance-volume-attachment-add data-vol-name 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 1a6b7274-678d-4dfb-8981-c71dd9d4daa5 --auto-delete true`
- `ibmcloud is instance-volume-attachment-add data-vol-name 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 1a6b7274-678d-4dfb-8981-c71dd9d4daa5 --auto-delete true --output JSON`

---

### ibmcloud is instance-volume-attachment-detach
{: #instance-volume-attachment-detach}

Delete volume attachments, detaching volume from an instance.

```
ibmcloud is instance-volume-attachment-detach INSTANCE (VOLUME_ATTACHMENT1 VOLUME_ATTACHMENT2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #instance-volume-attachment-detach-command-options}

- **INSTANCE**: ID of the instance.
- **VOLUME_ATTACHMENT1**: ID of the volume attachment.
- **VOLUME_ATTACHMENT2**: ID of the volume attachment.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is instance-volume-attachment-update
{: #instance-volume-attachment-update}

Update a volume attachment.

```
ibmcloud is instance-volume-attachment-update INSTANCE VOLUME_ATTACHMENT [--name NEW_NAME] [--auto-delete true | false] [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-volume-attachment-update-command-options}

- **INSTANCE**: ID of the instance.
- **VOLUME_ATTACHMENT**: ID of the volume attachment.
- **--name**: New name of the volume.
- **--auto-delete**: The attached volume is deleted when the instance is deleted. One of: **true**, **false**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #instance-volume-attachment-update-examples}

- `ibmcloud is instance-volume-attachment-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 1a6b7274-678d-4dfb-8981-c71dd9d4daa5 --name name2`
- `ibmcloud is instance-volume-attachment-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 1a6b7274-678d-4dfb-8981-c71dd9d4daa5 --auto-delete true`
- `ibmcloud is instance-volume-attachment-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 1a6b7274-678d-4dfb-8981-c71dd9d4daa5 --name name2 --auto-delete true --output JSON`

---

### ibmcloud is instance-volume-attachments
{: #instance-volume-attachments}

List all volume attachments to an instance.

```
ibmcloud is instance-volume-attachments INSTANCE [--output JSON] [-q, --quiet]
```

#### Command options
{: #instance-volume-attachments-command-options}

- **INSTANCE**: ID of the instance.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

## NETWORK COMMANDS
{: #network-cli-section}
This section provides a reference to the command line interface (CLI) commands available for the network functionality and resources, including floating IPs, public gateways, network ACLs, subnets, security groups, and VPCs.

## Floating IPs
{: #floating-ips-section}
The following section provides information about CLI commands for floating IPs.

### ibmcloud is floating-ips
{: #floating-ips}

List all floating IPs.

```
ibmcloud is floating-ips [--output JSON] [-q, --quiet]
```

#### Command options
{: #floating-ips-command-options}

- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is floating-ip
{: #floating-ip}

View details of a floating IP.

```
ibmcloud is floating-ip FLOATING_IP [--output JSON] [-q, --quiet]
```

#### Command options
{: #floating-ip-command-options}

- **FLOATING_IP**: ID of the floating IP.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is floating-ip-reserve
{: #floating-ip-reserve}

Reserve a floating IP.

```
ibmcloud is floating-ip-reserve FLOATING_IP_NAME (--zone ZONE_NAME | --nic-id NIC_ID) [--output JSON] [-q, --quiet]
```

#### Command options
{: #floating-ip-reserve-command-options}

- **FLOATING_IP_NAME**: Name of the floating IP.
- **--zone**: Name of the target zone. This option is mutually exclusive with **--nic-id**.
- **--nic-id**: ID of the target network interface. This option is mutually exclusive with **--zone**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #floating-ip-reserve-examples}

- `ibmcloud is floating-ip-reserve my-ip --zone us-south-1`
- `ibmcloud is floating-ip-reserve my-ip --nic-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3`
- `ibmcloud is floating-ip-reserve my-ip --nic-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --output JSON`

---

### ibmcloud is floating-ip-release
{: #floating-ip-release}

Release floating IPs.

```
ibmcloud is floating-ip-release (FLOATING_IP1 FLOATING_IP2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #floating-ip-release-command-options}

- **FLOATING_IP1**: ID of the floating IP.
- **FLOATING_IP2**: ID of the floating IP.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is floating-ip-update
{: #floating-ip-update}

Update a floating IP.

```
ibmcloud is floating-ip-update FLOATING_IP [--name NEW_NAME] [--nic-id NIC_ID] [--output JSON] [-q, --quiet]
```

#### Command options
{: #floating-ip-update-command-options}

- **FLOATING_IP**: ID of the floating IP.
- **--name**: New name of the floating IP.
- **--nic-id**: ID of the network interface to bind.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #floating-ip-update-examples}

- `ibmcloud is floating-ip-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --name my-ip`
- `ibmcloud is floating-ip-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --nic-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3`
- `ibmcloud is floating-ip-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --nic-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --output JSON`

---

## Load balancers
{: #load-balancers-section}
This section gives details about the CLI commands available for working with load balancers, listeners, and pools.

### ibmcloud is load-balancers
{: #load-balancers}

List all load balancers.

```
ibmcloud is load-balancers [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME | --all-resource-groups] [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancers-command-options}

- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--all-resource-groups**: Query all resource groups.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer
{: #load-balancer}

View details of a load balancer.

```
ibmcloud is load-balancer LOAD_BALANCER_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-create
{: #load-balancer-create}

Create a load balancer.

```
ibmcloud is load-balancer-create LOAD_BALANCER_NAME LOAD_BALANCER_TYPE (--subnet SUBNET_ID1 --subnet SUBNET_ID2 ...) [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-create-command-options}

- **LOAD_BALANCER_NAME**: Name of the load balancer.
- **LOAD_BALANCER_TYPE**: Type of the load balancer, **public** or **private**.
- **--subnet**: ID of the subnets to provision this load balancer. This option can be specified multiple times to provision load balancer in multiple subnets.
- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #load-balancer-create-examples}

- `ibmcloud is load-balancer-create lb-name public --subnet 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --subnet 7ec86020-1c6e-4889-b3f0-a15f2e50f87e`
- `ibmcloud is load-balancer-create lb-name public --subnet 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --subnet 7ec86020-1c6e-4889-b3f0-a15f2e50f87e --resource-group-id fee82deba12e4c0fb69c3b09d1f12345`
- `ibmcloud is load-balancer-create lb-name public --subnet 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --subnet 7ec86020-1c6e-4889-b3f0-a15f2e50f87e --resource-group-name Default`
- `ibmcloud is load-balancer-create lb-name public --subnet 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --subnet 7ec86020-1c6e-4889-b3f0-a15f2e50f87e --output JSON`

---

### ibmcloud is load-balancer-delete
{: #load-balancer-delete}

Delete load balancers.

```
ibmcloud is load-balancer-delete (LOAD_BALANCER_ID1 LOAD_BALANCER_ID2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #load-balancer-delete-command-options}

- **LOAD_BALANCER_ID1**: ID of the load balancer.
- **LOAD_BALANCER_ID2**: ID of the load balancer.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-update
{: #load-balancer-update}

Update a load balancer.

```
ibmcloud is load-balancer-update LOAD_BALANCER_ID --name NEW_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-update-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **--name**: New name of the Load balancer.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #load-balancer-update-examples}

- `ibmcloud is load-balancer-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --name my-loadBalancer`
- `ibmcloud is load-balancer-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --name my-loadBalancer --output JSON`

---

### ibmcloud is load-balancer-listeners
{: #load-balancer-listeners}

List all load balancer listeners.

```
ibmcloud is load-balancer-listeners LOAD_BALANCER_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-listeners-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-listener
{: #load-balancer-listener}

View details of a load balancer listener.

```
ibmcloud is load-balancer-listener LOAD_BALANCER_ID LISTENER_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID**: ID of the listener.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-listener-create
{: #load-balancer-listener-create}

Create a load balancer listener.

```
ibmcloud is load-balancer-listener-create LOAD_BALANCER_ID PORT PROTOCOL [--default-pool DEFAULT_POOL_ID] [--connection-limit LIMIT] [--certificate-instance-crn CERTIFICATE_INSTANCE_CRN] [--policies LISTENER_POLICIES_JSON | @LISTENER_POLICIES_JSON_FILE] [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-create-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **PORT**: The listener port number. Range 1-65535.
- **PROTOCOL**: The listener protocol. One of: **http**, **https**, **tcp**.
- **--default-pool**: ID of the default pool.
- **--connection-limit**: The maximum number of connections of the listener.
- **--certificate-instance-crn**: CRN of the certificate instance. Required when protocol is **https**.
- **--policies**: **LISTENER_POLICIES_JSON** | **@LISTENER_POLICIES_JSON_FILE**, listener policies in JSON or JSON file.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #load-balancer-listener-create-examples}

- `ibmcloud is load-balancer-listener-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 443 http`
- `ibmcloud is load-balancer-listener-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 443 https --certificate-instance-crn crn:v1:bluemix:public:cloudcerts:us-south:a/123456:b8866ea4-b8df-467e-801a-da1db7e020bf:certificate:78ff9c4c97d013fb2a95b21dddde7758`
- `ibmcloud is load-balancer-listener-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 443 http --connection-limit 2000`
- `ibmcloud is load-balancer-listener-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 443 http --default-pool 70294e14-4e61-11e8-bcf4-0242ac110004`
- `ibmcloud is load-balancer-listener-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 443 http --policies '[{"name": "my-policy", "priority": 5, "action": "reject" }]'`
The priority of the policy can have a range of 1 to 10, where a lower value indicates a higher priority. The possible values for _action_ are "forward", "redirect", or "reject".
- `ibmcloud is load-balancer-listener-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 443 http --policies '[{"priority": 5, "action": "forward", "target": { "id": 70294e14-4e61-11e8-bcf4-0242ac110004 }}]'`
When the action is _forward_, the pool identity is required to specify which pool the load balancer forwards the traffic to.
- `ibmcloud is load-balancer-listener-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 443 http --policies '[{"priority": 5, "action": "redirect", "target": { "http_status_code": 301, "url": "https://www.redirect.com"}}]'`
When the action is _redirect_, the "url" and "http_status_code" are required. Possible values for _http_status_code_ are "301", "302", "303", "307", or "308". The "url" is the redirect target URL.
- `ibmcloud is load-balancer-listener-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 443 http --policies '[{"priority": 5, "action": "reject", "rules": { "condition": "equals", "type": "header", "field": "My-app-header", "value": "value"}}]'`
Possible values for _condition_ are "contains", "equals", or "matches_regex". Possible values for _type_ are "header", "hostname", or "path". _field_ is an HTTP header field that is applicable only to the "header" rule type. The _value_ parameter is the value to match the rule condition.
- `ibmcloud is load-balancer-listener-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 443 http --output JSON`

---

### ibmcloud is load-balancer-listener-delete
{: #load-balancer-listener-delete}

Delete load balancer listeners.

```
ibmcloud is load-balancer-listener-delete LOAD_BALANCER_ID (LISTENER_ID1 LISTENER_ID2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-delete-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID1**: ID of the listener.
- **LISTENER_ID2**: ID of the listener.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-listener-update
{: #load-balancer-listener-update}

Update a load balancer listener.

```
ibmcloud is load-balancer-listener-update LOAD_BALANCER_ID LISTENER_ID [--protocol http | https | tcp] [--port PORT] [--default-pool DEFAULT_POOL_ID] [--connection-limit LIMIT] [--certificate-instance-crn CERTIFICATE_INSTANCE_CRN] [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-update-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID**: ID of the listener.
- **--protocol**: The listener protocol. One of: **http**, **https**, **tcp**.
- **--port**: The listener port number. Range 1-65535.
- **--default-pool**: ID of the default pool.
- **--connection-limit**: The maximum number of connections of the listener.
- **--certificate-instance-crn**: CRN of the certificate instance. Required when protocol is **https**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #load-balancer-listener-update-examples}

- `ibmcloud is load-balancer-listener-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --certificate-instance-crn crn:v1:bluemix:public:cloudcerts:us-south:a/123456:b8866ea4-b8df-467e-801a-da1db7e020bf:certificate:78ff9c4c97d013fb2a95b21dddde7758`
- `ibmcloud is load-balancer-listener-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --connection-limit 2000`
- `ibmcloud is load-balancer-listener-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --default-pool 70294e14-4e61-11e8-bcf4-0242ac110004`
- `ibmcloud is load-balancer-listener-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --protocol https`
- `ibmcloud is load-balancer-listener-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --port 222`
- `ibmcloud is load-balancer-listener-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --output JSON`

---

### ibmcloud is load-balancer-listener-policies
{: #load-balancer-listener-policies}

List all load balancer policies.

```
ibmcloud is load-balancer-listener-policies LOAD_BALANCER_ID LISTENER_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-policies-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID**: ID of the listener.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-listener-policy
{: #load-balancer-listener-policy}

View details of load balancer listener policy.

```
ibmcloud is load-balancer-listener-policy LOAD_BALANCER_ID LISTENER_ID POLICY_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-policy-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID**: ID of the listener.
- **POLICY_ID**: ID of the policy.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-listener-policy-create
{: #load-balancer-listener-policy-create}

Create a load balancer listener policy.

```
ibmcloud is load-balancer-listener-policy-create LOAD_BALANCER_ID LISTENER_ID --priority PRIORITY (--action forward | redirect | reject) [--name NEW_NAME] [--target-id TARGET_ID | (--target-http-status-code TARGET_HTTP_STATUS_CODE --target-url TARGET_URL)] [--rules LISTENER_POLICY_RULES_JSON | @LISTENER_POLICY_RULES_JSON_FILE] [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-policy-create-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID**: ID of the listener.
- **--priority**: Priority of the policy. Lower value indicates higher priority, for example: **5**, range: [**1-10**].
- **--action**: The policy action. One of: **forward**, **redirect**, **reject**.
- **--name**: The new name of the policy.
- **--target-id**: The unique identifier for this load balancer pool that is specified with **forward** action.
- **--target-http-status-code**: The HTTP status code in the redirect response, one of [**301**, **302**, **303**, **307**, **308**], specified with **redirect** action.
- **--target-url**: The redirect target URL, specified with **redirect** action.
- **--rules**: **LISTENER_POLICY_RULES_JSON** | **@LISTENER_POLICY_RULES_JSON_FILE**, listener policy rules in JSON or JSON file.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #load-balancer-listener-policy-create-examples}

- `ibmcloud is load-balancer-listener-policy-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --name my-policy --action reject --priority 5`
The priority of the policy can have a range of 1 to 10, where a lower value indicates a higher priority. The possible values for _action_ are "forward", "redirect", or "reject".
- `ibmcloud is load-balancer-listener-policy-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --action forward --priority 2 --target-id 70294e14-4e61-11e8-bcf4-0242ac110004`
When the action is _forward_, the pool identity is required to specify which pool the load balancer forwards the traffic to.
- `ibmcloud is load-balancer-listener-policy-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --action redirect --priority 1 --target-http-status-code 301 --target-url "https://www.redirect.com"`
When the action is _redirect_, the "url" and "http_status_code" are required. Possible values for _http_status_code_ are "301", "302", "303", "307", or "308". The "url" is the redirect target URL.
- `ibmcloud is load-balancer-listener-policy-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --action reject --priority 4 --rules '[{"rules": { "condition": "equals", "type": "header", "field": "My-app-header", "value": "value"}}]'`
Possible values for _condition_ are "contains", "equals", or "matches_regex". Possible values for _type_ are "header", "hostname", or "path". _field_ is an HTTP header field that is applicable only to the "header" rule type. The _value_ parameter is the value to match the rule condition.
- `ibmcloud is load-balancer-listener-policy-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --action reject --priority 3 --name my-policy --output JSON`

---

### ibmcloud is load-balancer-listener-policy-delete
{: #load-balancer-listener-policy-delete}

Delete policies from a load balancer listener.

```
ibmcloud is load-balancer-listener-policy-delete LOAD_BALANCER_ID LISTENER_ID (POLICY_ID1 POLICY_ID2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-policy-delete-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID**: ID of the listener.
- **POLICY_ID1**: ID of the policy.
- **POLICY_ID2**: ID of the policy.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-listener-policy-update
{: #load-balancer-listener-policy-update}

Update a policy of a load balancer listener.

```
ibmcloud is load-balancer-listener-policy-update LOAD_BALANCER_ID LISTENER_ID POLICY_ID [--name NEW_NAME] [--priority PRIORITY] [--target-id TARGET_ID] [--target-http-status-code TARGET_HTTP_STATUS_CODE] [--target-url TARGET_URL] [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-policy-update-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID**: ID of the listener.
- **POLICY_ID**: ID of the policy.
- **--name**: The user-defined name for this policy. Policy names must be unique within the load balancer listener.
- **--priority**: Priority of the policy. Lower value indicates higher priority, for example: **5**, range: [**1-10**].
- **--target-id**: The unique identifier for this load balancer pool that is specified with **forward** action.
- **--target-http-status-code**: The HTTP status code in the redirect response, one of [**301**, **302**, **303**, **307**, **308**], specified with **redirect** action.
- **--target-url**: The redirect target URL, specified with **redirect** action.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #load-balancer-listener-policy-update-examples}

- `ibmcloud is load-balancer-listener-policy-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --name my-policy --priority 5`
- `ibmcloud is load-balancer-listener-policy-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --action forward --target-id 70294e14-4e61-11e8-bcf4-0242ac110004`
When the action is _forward_, the pool identity is required to specify which pool the load balancer forwards the traffic to.
- `ibmcloud is load-balancer-listener-policy-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --target-http-status-code 301 --target-url "https://www.redirect.com"`
When the action is _redirect_, the "url" and "http_status_code" are required. Possible values for _http_status_code_ are "301", "302", "303", "307", or "308". The "url" is the redirect target URL.
- `ibmcloud is load-balancer-listener-policy-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --name my-policy --output JSON`

---

### ibmcloud is load-balancer-listener-policy-rules
{: #load-balancer-listener-policy-rules}

List all load balancer policy rules.

```
ibmcloud is load-balancer-listener-policy-rules LOAD_BALANCER_ID LISTENER_ID POLICY_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-policy-rules-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID**: ID of the listener.
- **POLICY_ID**: ID of the policy.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-listener-policy-rule
{: #load-balancer-listener-policy-rule}

List single load balancer policy rule.

```
ibmcloud is load-balancer-listener-policy-rule LOAD_BALANCER_ID LISTENER_ID POLICY_ID RULE_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-policy-rule-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID**: ID of the listener.
- **POLICY_ID**: ID of the policy.
- **RULE_ID**: ID of the rule.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-listener-policy-rule-create
{: #load-balancer-listener-policy-rule-create}

Create a load balancer listener policy rule.

```
ibmcloud is load-balancer-listener-policy-rule-create LOAD_BALANCER_ID LISTENER_ID POLICY_ID (--condition contains | equals | matches_regex) (--type header | hostname | path) --value VALUE [--field FIELD] [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-policy-rule-create-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID**: ID of the listener.
- **POLICY_ID**: ID of the policy.
- **--condition**: The condition of the rule. One of: **contains**, **equals**, **matches_regex**.
- **--type**: The type of the rule. One of: **header**, **hostname**, **path**.
- **--value**: Value to match the rule condition.
- **--field**: HTTP header field. This is applicable only to **header** rule type.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #load-balancer-listener-policy-rule-create-examples}

`ibmcloud is load-balancer-listener-policy-rule-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --condition equals --type header --field my-app-header --value  match-value --output JSON`

---

### ibmcloud is load-balancer-listener-policy-rule-update
{: #load-balancer-listener-policy-rule-update}

Update a rule of a load balancer listener policy.

```
ibmcloud is load-balancer-listener-policy-rule-update LOAD_BALANCER_ID LISTENER_ID POLICY_ID RULE_ID [--condition contains | equals | matches_regex] [--type header | hostname | path] [--value VALUE] [--field FIELD] [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-policy-rule-update-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID**: ID of the listener.
- **POLICY_ID**: ID of the policy.
- **RULE_ID**: ID of the rule.
- **--condition**: The condition of the rule. One of: **contains**, **equals**, **matches_regex**.
- **--type**: The type of the rule. One of: **header**, **hostname**, **path**.
- **--value**: Value to match the rule condition.
- **--field**: HTTP header field. This is applicable only to **header** rule type.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #load-balancer-listener-policy-rule-update-examples}

`ibmcloud is load-balancer-listener-policy-rule-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 70294e14-4e61-11e8-bcf4-0242ac110004 --condition equals --type header --field my-app-header --value  match-value --output JSON`

---

### ibmcloud is load-balancer-listener-policy-rule-delete
{: #load-balancer-listener-policy-rule-delete}

Delete policies from a load balancer listener.

```
ibmcloud is load-balancer-listener-policy-rule-delete LOAD_BALANCER_ID LISTENER_ID POLICY_ID (RULE_ID1 RULE_ID2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #load-balancer-listener-policy-rule-delete-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **LISTENER_ID**: ID of the listener.
- **POLICY_ID**: ID of the policy.
- **RULE_ID1**: ID of the rule.
- **RULE_ID2**: ID of the rule.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-pools
{: #load-balancer-pools}

List all pools of a load balancer.

```
ibmcloud is load-balancer-pools LOAD_BALANCER_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-pools-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-pool
{: #load-balancer-pool}

View details of a load balancer pool.

```
ibmcloud is load-balancer-pool LOAD_BALANCER_ID POOL_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-pool-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **POOL_ID**: ID of the pool.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-pool-create
{: #load-balancer-pool-create}

Create a load balancer pool.

```
ibmcloud is load-balancer-pool-create POOL_NAME LOAD_BALANCER_ID ALGORITHM PROTOCOL HEALTH_DELAY HEALTH_RETRIES HEALTH_TIMEOUT HEALTH_TYPE (--members MEMBERS_JSON | @MEMBERS_JSON_FILE) [--health-monitor-url URL] [--health-monitor-port PORT] [--session-persistence-type source_ip] [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-pool-create-command-options}

- **POOL_NAME**: Name of the pool.
- **LOAD_BALANCER_ID**: ID of the load balancer.
- **ALGORITHM**: The load balancing algorithm. One of: **round_robin**, **weighted_round_robin**, **least_connections**.
- **PROTOCOL**: The pool protocol. One of: **http**, **https**, **tcp**.
- **HEALTH_DELAY**: The health check interval in seconds. The interval must be greater than the timeout value. Minimum: **2**, maximum: **60**.
- **HEALTH_RETRIES**: The health check maximum retries. Minimum: **1**, maximum: **10**.
- **HEALTH_TIMEOUT**: The health check timeout in seconds. Minimum: **1**, maximum: **59**.
- **HEALTH_TYPE**: The health check protocol. One of: **http**, **https**, **tcp**.
- **--health-monitor-url**: The health check URL. This option is applicable only to HTTP type of **HEALTH_TYPE**.
- **--health-monitor-port**: The health check port number. If specified, the specified ports in the server member resources are overridden.
- **--session-persistence-type**: The session persistence type. One of: **source_ip**.
- **--members**: MEMBERS_JSON|@MEMBERS_JSON_FILE, members in JSON or JSON file.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #load-balancer-pool-create-examples}

- `ibmcloud is load-balancer-pool-create my-lb-pool 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 round_robin http 20 2 5 http`
- `ibmcloud is load-balancer-pool-create my-lb-pool 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 round_robin http 20 2 5 http --health-monitor-url / --health-monitor-port 4001`
- `ibmcloud is load-balancer-pool-create my-lb-pool 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 round_robin http 20 2 5 http --session-persistence-type source_ip --output JSON`
- `ibmcloud is load-balancer-pool-create my-lb-pool 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 round_robin http 20 2 5 http --members '[{"port": 80, "target": { "address": "10.10.1.4"}, "weight": 20 }, {"port": 80, "target": { "address": "10.240.0.6"}, "weight": 30 }]'`
Create application load balancer pool with members
- `ibmcloud is load-balancer-pool-create my-lb-pool 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 round_robin http 20 2 5 http --members '[{"port": 80, "target": { "id": "0736_63b9233c-812e-4d65-9ee3-fa61172afa37"}, "weight": 20 }, {"port": 80, "target": { "id": "0716_4b30a833-6f10-46a9-a4b8-13871f3559b8"}, "weight": 30 }]'`
Create network load balancer pool with members

---

### ibmcloud is load-balancer-pool-delete
{: #load-balancer-pool-delete}

Delete pools from a load balancer.

```
ibmcloud is load-balancer-pool-delete LOAD_BALANCER_ID (POOL_ID1 POOL_ID2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #load-balancer-pool-delete-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **POOL_ID1**: ID of the pool.
- **POOL_ID2**: ID of the pool.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-pool-update
{: #load-balancer-pool-update}

Update a pool of a load balancer.

```
ibmcloud is load-balancer-pool-update LOAD_BALANCER_ID POOL_ID [--algorithm round_robin | weighted_round_robin | least_connections] [--health-delay DELAY --health-max-retries RETRIES --health-timeout TIMEOUT --health-type https | http | tcp] [--health-monitor-url URL] [--health-monitor-port PORT] [--protocol https | http | tcp] [--session-persistence-type source_ip | none] [--name NEW_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-pool-update-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **POOL_ID**: ID of the pool.
- **--algorithm**: The load balancing algorithm. One of: **round_robin**, **weighted_round_robin**, **least_connections**.
- **--health-delay**: The health check interval in seconds. The interval must be greater than the timeout value. Minimum: **2**, maximum: **60**.
- **--health-max-retries**: The health check maximum retries. Minimum: **1**, maximum: **10**.
- **--health-timeout**: The health check timeout in seconds. Minimum: **1**, maximum: **59**.
- **--health-type**: The health check protocol. One of: **http**, **https**, **tcp**.
- **--health-monitor-url**: The health check URL. This option is applicable only to HTTP type of **--health-type**.
- **--health-monitor-port**: The health check port number. If specified, the specified ports in the server member resources are overridden.
- **--protocol**: The pool protocol. One of: **http**, **https**, **tcp**.
- **--session-persistence-type**: The session persistence type. One of: **source_ip**, **none**.
- **--name**: The new name of the pool.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #load-balancer-pool-update-examples}

- `ibmcloud is load-balancer-pool-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --algorithm round_robin`
- `ibmcloud is load-balancer-pool-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --health-delay 20 --health-max-retries 2 --health-timeout 5 --health-type http`
- `ibmcloud is load-balancer-pool-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --health-monitor-url / --health-monitor-port 4001`
- `ibmcloud is load-balancer-pool-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --session-persistence-type source_ip`
- `ibmcloud is load-balancer-pool-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --protocol http`
- `ibmcloud is load-balancer-pool-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --name lb-rule-name --output JSON`

---

### ibmcloud is load-balancer-pool-members
{: #load-balancer-pool-members}

List all the members of a load balancer pool.

```
ibmcloud is load-balancer-pool-members LOAD_BALANCER_ID POOL_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-pool-members-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **POOL_ID**: ID of the pool.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-pool-member
{: #load-balancer-pool-member}

View details of load balancer pool member.

```
ibmcloud is load-balancer-pool-member LOAD_BALANCER_ID POOL_ID MEMBER_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-pool-member-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **POOL_ID**: ID of the pool.
- **MEMBER_ID**: ID of the member.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-pool-member-create
{: #load-balancer-pool-member-create}

Create a load balancer pool member.

```
ibmcloud is load-balancer-pool-member-create LOAD_BALANCER_ID POOL_ID PORT TARGET [--weight WEIGHT] [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-pool-member-create-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **POOL_ID**: ID of the pool.
- **PORT**: The port number of the running application in the server member.
- **TARGET**: The IP address of the pool member.
- **--weight**: Weight of the server member. This option is applicable only when the load balancer algorithm of its pool is **weighted_round_robin**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #load-balancer-pool-member-create-examples}

- `ibmcloud is load-balancer-pool-member-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 3000 192.168.100.5`
- `ibmcloud is load-balancer-pool-member-create 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 3000 192.168.100.5 --weight 100 --output JSON`

---

### ibmcloud is load-balancer-pool-member-update
{: #load-balancer-pool-member-update}

Update a member of a load balancer pool.

```
ibmcloud is load-balancer-pool-member-update LOAD_BALANCER_ID POOL_ID MEMBER_ID [--target-address TARGET_ADDRESS] [--port PORT] [--weight WEIGHT] [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-pool-member-update-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **POOL_ID**: ID of the pool.
- **MEMBER_ID**: ID of the member.
- **--target-address**: The IP address of the pool member.
- **--port**: The port number of the application that is running in the server member.
- **--weight**: Weight of the server member. This option is applicable only when the load balancer algorithm of its pool is **weighted_round_robin**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #load-balancer-pool-member-update-examples}

- `ibmcloud is load-balancer-pool-member-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --target-address 192.168.100.5 --port 3001`
- `ibmcloud is load-balancer-pool-member-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --target-address 192.168.100.5 --port 3001 --weight 100 --output JSON`

---

### ibmcloud is load-balancer-pool-member-delete
{: #load-balancer-pool-member-delete}

Delete members from a load balancer pool.

```
ibmcloud is load-balancer-pool-member-delete LOAD_BALANCER_ID POOL_ID (MEMBER_ID1 MEMBER_ID2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #load-balancer-pool-member-delete-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **POOL_ID**: ID of the pool.
- **MEMBER_ID1**: ID of the member.
- **MEMBER_ID2**: ID of the member.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is load-balancer-statistics
{: #load-balancer-statistics}

List all statistics of a load balancer.

```
ibmcloud is load-balancer-statistics LOAD_BALANCER_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #load-balancer-statistics-command-options}

- **LOAD_BALANCER_ID**: ID of the load balancer.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

## Public gateways
{: #public-gateways-section}
The following section provides information about CLI commands for public gateways.

### ibmcloud is public-gateways
{: #public-gateways}

List all public gateways.

```
ibmcloud is public-gateways [--output JSON] [-q, --quiet]
```

#### Command options
{: #public-gateways-command-options}

- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is public-gateway
{: #public-gateway}

View details of a public gateway.

```
ibmcloud is public-gateway GATEWAY [--output JSON] [-q, --quiet]
```

#### Command options
{: #public-gateway-command-options}

- **GATEWAY**: ID of the public gateway.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is public-gateway-create
{: #public-gateway-create}

Create a public gateway.

```
ibmcloud is public-gateway-create GATEWAY_NAME VPC ZONE_NAME [--floating-ip-id IP_ID | --floating-ip-address IP_ADDRESS] [--output JSON] [-q, --quiet]
```

#### Command options
{: #public-gateway-create-command-options}

- **GATEWAY_NAME**: Name of the public gateway.
- **VPC**: ID of the VPC.
- **ZONE_NAME**: Name of the zone.
- **--floating-ip-id**: ID of the floating IP bound to the public gateway.
- **--floating-ip-address**: IP address of the floating IP bound to the public gateway.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #public-gateway-create-examples}

- `ibmcloud is public-gateway-create my-public-gateway 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 us-south-1`
- `ibmcloud is public-gateway-create my-public-gateway 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 us-south-1 --floating-ip-id 39300233-9995-4806-89a5-3c1b6eb88689`
- `ibmcloud is public-gateway-create my-public-gateway 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 us-south-1 --floating-ip-address 203.0.113.1`
- `ibmcloud is public-gateway-create my-public-gateway 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 us-south-1 --output JSON`

---

### ibmcloud is public-gateway-update
{: #public-gateway-update}

Update a public gateway.

```
ibmcloud is public-gateway-update GATEWAY --name NEW_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #public-gateway-update-command-options}

- **GATEWAY**: ID of the public gateway.
- **--name**: New name of the public gateway.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #public-gateway-update-examples}

`ibmcloud is public-gateway-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb8 --name my-gateway --output JSON`

---

### ibmcloud is public-gateway-delete
{: #public-gateway-delete}

Delete public gateways.

```
ibmcloud is public-gateway-delete (GATEWAY1 GATEWAY2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #public-gateway-delete-command-options}

- **GATEWAY1**: ID of the public gateway.
- **GATEWAY2**: ID of the public gateway.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

## Network ACLs
{: #network-acls-section}
The following section provides information about CLI commands for network ACLs.

### ibmcloud is network-acls
{: #network-acls}

List all network ACLs.

```
ibmcloud is network-acls [--output JSON] [-q, --quiet]
```

#### Command options
{: #network-acls-command-options}

- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is network-acl
{: #network-acl}

View details of a network ACL.

```
ibmcloud is network-acl ACL [--output JSON] [-q, --quiet]
```

#### Command options
{: #network-acl-command-options}

- **ACL**: ID of the network ACL.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is network-acl-create
{: #network-acl-create}

Create a network ACL.

```
ibmcloud is network-acl-create ACL_NAME [--rules (RULES_JSON|@RULES_JSON_FILE) | --source-acl-id SOURCE_ACL_ID] [--output JSON] [-q, --quiet]
```

#### Command options
{: #network-acl-create-command-options}

- **ACL_NAME**: Name of the network ACL.
- **--rules**: RULES_JSON|@RULES_JSON_FILE, rules for the ACL in JSON or JSON file.
- **--source-acl-id**: ID of the network ACL to copy rules from.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #network-acl-create-examples}

- `ibmcloud is network-acl-create my-acl`
- `ibmcloud is network-acl-create my-acl --source-acl-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3`
- `ibmcloud is network-acl-create my-acl --rules '[{ "action": "allow", "destination": "192.168.0.0/24", "direction": "inbound", "source": "10.0.0.0/24",  "protocol": "tcp" }]'`
'action' Eum [ allow, deny ].
'destination', 'source': IP or CIDR. The CIDR block 0.0.0.0/0 applies to all addresses.
'direction' - Enum [ inbound, outbound ].
'protocol' Enum [ tcp, udp, icmp, all ].
- `ibmcloud is network-acl-create my-acl --output JSON`

---

### ibmcloud is network-acl-update
{: #network-acl-update}

Update a network ACL.

```
ibmcloud is network-acl-update ACL --name NEW_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #network-acl-update-command-options}

- **ACL**: ID of the network ACL.
- **--name**: New name of the network ACL.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #network-acl-update-examples}

- `ibmcloud is network-acl-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --name my-acl`
- `ibmcloud is network-acl-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --name my-acl --output JSON`

---

### ibmcloud is network-acl-delete
{: #network-acl-delete}

Delete network ACLs.

```
ibmcloud is network-acl-delete (ACL1 ACL2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #network-acl-delete-command-options}

- **ACL1**: ID of the network ACL.
- **ACL2**: ID of the network ACL.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is network-acl-rules
{: #network-acl-rules}

List all rules of a network ACL.

```
ibmcloud is network-acl-rules ACL [--output JSON] [-q, --quiet]
```

#### Command options
{: #network-acl-rules-command-options}

- **ACL**: ID of the network ACL.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is network-acl-rule
{: #network-acl-rule}

View details of a network ACL rule.

```
ibmcloud is network-acl-rule ACL RULE [--output JSON] [-q, --quiet]
```

#### Command options
{: #network-acl-rule-command-options}

- **ACL**: ID of the network ACL.
- **RULE**: ID of the rule.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is network-acl-rule-add
{: #network-acl-rule-add}

Add a rule to a network ACL.

```
ibmcloud is network-acl-rule-add ACL ACTION DIRECTION PROTOCOL SOURCE DESTINATION [--name NAME] [--icmp-type ICMP_TYPE] [--icmp-code ICMP_CODE] [--source-port-min PORT_MIN] [--source-port-max PORT_MAX] [--destination-port-min PORT_MIN] [--destination-port-max PORT_MAX] [--before-rule-id RULE_ID] [--output JSON] [-q, --quiet]
```

#### Command options
{: #network-acl-rule-add-command-options}

- **ACL**: ID of the network ACL.
- **ACTION**: One of: **allow**, **deny**.
- **DIRECTION**: Direction of traffic to enforce. One of: **inbound**, **outbound**.
- **PROTOCOL**: Protocol to enforce. One of: **all**, **icmp**, **tcp**, **udp**.
- **SOURCE**: Source IP address or CIDR block.
- **DESTINATION**: Destination IP address or CIDR block.
- **--name**: The name of the ACL rule.
- **--icmp-type**: ICMP traffic type to allow. Valid values from **0** to **254**. This option is specified only when protocol is set to **icmp**. If unspecified, all types are allowed.
- **--icmp-code**: ICMP traffic code to allow. Valid values from **0** to **255**. This option is specified only when protocol is set to **icmp**. If unspecified, all codes are allowed.
- **--source-port-min**: Minimum source port number. Valid values are from **1** to **65535**. This option is specified only when protocol is set to **tcp** or **udp** (default: **1**).
- **--source-port-max**: Maximum source port number. Valid values are from **1** to **65535**. This option is specified only when protocol is set to **tcp** or **udp** (default: **65535**).
- **--destination-port-min**: Minimum destination port number. Valid values are from **1** to **65535**. This option is specified only when protocol is set to **tcp** or **udp** (default: **1**).
- **--destination-port-max**: Maximum destination port number. Valid values are from **1** to **65535**. This option is specified only when protocol is set to **tcp** or **udp** (default: **65535**).
- **--before-rule-id**: ID of the rule that this rule is inserted before.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #network-acl-rule-add-examples}

- `ibmcloud is network-acl-rule-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 allow inbound all 10.2.2.2 10.2.2.3`
- `ibmcloud is network-acl-rule-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 allow inbound all 10.2.2.2 10.2.2.3 --name my-acl`
- `ibmcloud is network-acl-rule-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 allow inbound icmp 10.2.2.2 10.2.2.3 --icmp-type 8 --icmp-code 0`
- `ibmcloud is network-acl-rule-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 allow inbound tcp 10.2.2.2 10.2.2.3 --source-port-min 555  --source-port-max 666 --destination-port-min 11 --destination-port-max 55`
- `ibmcloud is network-acl-rule-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 allow inbound all 10.2.2.2 10.2.2.3 --before-rule-id 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479`
- `ibmcloud is network-acl-rule-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 allow inbound all 10.2.2.2 10.2.2.3 --output JSON`

---

### ibmcloud is network-acl-rule-update
{: #network-acl-rule-update}

Update a rule of a network ACL.

```
ibmcloud is network-acl-rule-update ACL RULE [--name NEW_NAME] [--direction inbound | outbound] [--action allow | deny] [--before-rule-id RULE_ID] [--source SOURCE] [--dest DEST] [--protocol all | icmp | tcp | udp] [--icmp-type ICMP_TYPE] [--icmp-code ICMP_CODE] [--source-port-min PORT_MIN] [--source-port-max PORT_MAX] [--destination-port-min PORT_MIN] [--destination-port-max PORT_MAX] [--output JSON] [-q, --quiet]
```

#### Command options
{: #network-acl-rule-update-command-options}

- **ACL**: ID of the network ACL.
- **RULE**: ID of the rule.
- **--name**: New name of the rule.
- **--direction**: Direction of traffic to enforce. One of: **inbound**, **outbound**.
- **--action**: One of: **allow**, **deny**.
- **--before-rule-id**: ID of the rule that this rule is inserted before.
- **--source**: Source IP address or CIDR block.
- **--dest**: Destination IP address or CIDR block.
- **--protocol**: Protocol to enforce. One of: **all**, **icmp**, **tcp**, **udp**.
- **--icmp-type**: ICMP traffic type to allow. Valid values from **0** to **254**. This option is specified only when protocol is set to **icmp**. If unspecified, all types are allowed.
- **--icmp-code**: ICMP traffic code to allow. Valid values from **0** to **255**. This option is specified only when protocol is set to **icmp**. If unspecified, all codes are allowed.
- **--source-port-min**: Minimum source port number. Valid values are from **1** to **65535**. This option is specified only when protocol is set to **tcp** or **udp** (default: **1**).
- **--source-port-max**: Maximum source port number. Valid values are from **1** to **65535**. This option is specified only when protocol is set to **tcp** or **udp** (default: **65535**).
- **--destination-port-min**: Minimum destination port number. Valid values are from **1** to **65535**. This option is specified only when protocol is set to **tcp** or **udp** (default: **1**).
- **--destination-port-max**: Maximum destination port number. Valid values are from **1** to **65535**. This option is specified only when protocol is set to **tcp** or **udp** (default: **65535**).
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #network-acl-rule-update-examples}

- `ibmcloud is network-acl-rule-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 8daca77a-4980-4d33-8f3e-7038797be8f9 --action allow --direction inbound --protocol all --source 10.2.2.2 --dest 10.2.2.3`
- `ibmcloud is network-acl-rule-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 8daca77a-4980-4d33-8f3e-7038797be8f9 --action allow --direction inbound --protocol all --source 10.2.2.2 --dest 10.2.2.3 --name my-acl`
- `ibmcloud is network-acl-rule-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 8daca77a-4980-4d33-8f3e-7038797be8f9 --action allow --direction inbound --protocol icmp --source 10.2.2.2 --dest 10.2.2.3 --icmp-type 8 --icmp-code 0`
- `ibmcloud is network-acl-rule-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 8daca77a-4980-4d33-8f3e-7038797be8f9 --action allow --direction inbound --protocol tcp --source 10.2.2.2 --dest 10.2.2.3 --source-port-min 555 --source-port-max 666 --destination-port-min 11 --destination-port-max 55`
- `ibmcloud is network-acl-rule-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 8daca77a-4980-4d33-8f3e-7038797be8f9 --action allow --direction inbound --protocol all --source 10.2.2.2 --dest 10.2.2.3 --before-rule-id 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479`
- `ibmcloud is network-acl-rule-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 8daca77a-4980-4d33-8f3e-7038797be8f9 --action allow --direction inbound --protocol all --source 10.2.2.2 --dest 10.2.2.3 --output JSON`

---

### ibmcloud is network-acl-rule-delete
{: #network-acl-rule-delete}

Delete rules from a network ACL.

```
ibmcloud is network-acl-rule-delete ACL (RULE1 RULE2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #network-acl-rule-delete-command-options}

- **ACL**: ID of the network ACL.
- **RULE1**: ID of the rule.
- **RULE2**: ID of the rule.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

## Subnets
{: #subnets-section}
The following section provides information about CLI commands for subnets.

### ibmcloud is subnets
{: #subnets}

List all subnets.

```
ibmcloud is subnets [--output JSON] [-q, --quiet]
```

#### Command options
{: #subnets-command-options}

- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is subnet
{: #subnet}

View details of a subnet.

```
ibmcloud is subnet SUBNET [--show-attached] [--output JSON] [-q, --quiet]
```

#### Command options
{: #subnet-command-options}

- **SUBNET**: ID of the subnet.
- **--show-attached**: View details of resources (instances, load balancers, VPN gateways) attached to the subnet.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is subnet-create
{: #subnet-create}

Create a subnet.

```
ibmcloud is subnet-create SUBNET_NAME VPC (--ipv4-cidr-block CIDR_BLOCK | (--ipv4-address-count ADDR_COUNT --zone ZONE_NAME)) [--network-acl-id NETWORK_ACL_ID] [--public-gateway-id PUBLIC_GATEWAY_ID] [--output JSON] [-q, --quiet]
```

#### Command options
{: #subnet-create-command-options}

- **SUBNET_NAME**: Name of the subnet.
- **VPC**: ID of the VPC.
- **--ipv4-cidr-block**: the IPv4 range of the subnet. This option is mutually exclusive with **--ipv4-address-count**.
- **--ipv4-address-count**: The total number of IPv4 addresses required, must be a power of 2 and minimum value is **8**. This option is mutually exclusive with **--ipv4-cidr-block**.
- **--zone**: Name of the zone.
- **--network-acl-id**: The ID of the network ACL.
- **--public-gateway-id**: The ID of the public gateway.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #subnet-create-examples}

- `ibmcloud is subnet-create my-subnet 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --ipv4-cidr-block 10.10.10.0/24`
- `ibmcloud is subnet-create my-subnet 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --ipv4-address-count 256 --zone us-south-2`
- `ibmcloud is subnet-create my-subnet 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --ipv4-address-count 256 --zone us-south-2 --network-acl-id 8daca77a-4980-4d33-8f3e-7038797be8f9`
- `ibmcloud is subnet-create my-subnet 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --ipv4-address-count 256 --zone us-south-2 --public-gateway-id 8daca77a-4980-4d33-8f3e-7038797be8f9`
- `ibmcloud is subnet-create my-subnet 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --ipv4-address-count 256 --zone us-south-2 --public-gateway-id 8daca77a-4980-4d33-8f3e-7038797be8f9 --output JSON`

---

### ibmcloud is subnet-update
{: #subnet-update}

Update a subnet.

```
ibmcloud is subnet-update SUBNET [--name NEW_NAME] [--network-acl-id NETWORK_ACL_ID] [--public-gateway-id PUBLIC_GATEWAY_ID] [--output JSON] [-q, --quiet]
```

#### Command options
{: #subnet-update-command-options}

- **SUBNET**: ID of the subnet.
- **--name**: New name of the subnet.
- **--network-acl-id**: The ID of the network ACL.
- **--public-gateway-id**: The ID of the public gateway.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #subnet-update-examples}

- `ibmcloud is subnet-update ec8bb350-d802-4f1b-b362-b848abd5bb65 --name my-subnet`
- `ibmcloud is subnet-update ec8bb350-d802-4f1b-b362-b848abd5bb65 --network-acl-id 8daca77a-4980-4d33-8f3e-7038797be8f9`
- `ibmcloud is subnet-update ec8bb350-d802-4f1b-b362-b848abd5bb65 --public-gateway-id 8daca77a-4980-4d33-8f3e-7038797be8f9`
- `ibmcloud is subnet-update ec8bb350-d802-4f1b-b362-b848abd5bb65 --name my-subnet --output JSON`

---

### ibmcloud is subnet-delete
{: #subnet-delete}

Delete subnets.

```
ibmcloud is subnet-delete (SUBNET1 SUBNET2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #subnet-delete-command-options}

- **SUBNET1**: ID of the subnet.
- **SUBNET2**: ID of the subnet.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is subnet-public-gateway-detach
{: #subnet-public-gateway-detach}

Detach the public gateway from a subnet.

```
ibmcloud is subnet-public-gateway-detach SUBNET [-q, --quiet]
```

#### Command options
{: #subnet-public-gateway-detach-command-options}

- **SUBNET**: ID of the subnet.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is subnet-public-gateway
{: #subnet-public-gateway}

View details of public gateway attached to the subnet.

```
ibmcloud is subnet-public-gateway SUBNET [--output JSON] [-q, --quiet]
```

#### Command options
{: #subnet-public-gateway-command-options}

- **SUBNET**: ID of the subnet.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

## Security groups
{: #security-groups-section}
The following section provides information about CLI commands for security groups.

### ibmcloud is security-groups
{: #security-groups}

List all security groups.

```
ibmcloud is security-groups [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME | --all-resource-groups] [--output JSON] [-q, --quiet]
```

#### Command options
{: #security-groups-command-options}

- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--all-resource-groups**: Query all resource groups.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is security-group
{: #security-group}

View details of a security group.

```
ibmcloud is security-group GROUP [--output JSON] [-q, --quiet]
```

#### Command options
{: #security-group-command-options}

- **GROUP**: ID of the security group.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is security-group-create
{: #security-group-create}

Create a security group.

```
ibmcloud is security-group-create GROUP_NAME VPC [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #security-group-create-command-options}

- **GROUP_NAME**: Name of the security group.
- **VPC**: ID of the VPC.
- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #security-group-create-examples}

- `ibmcloud is security-group-create my-security-group 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3`
- `ibmcloud is security-group-create my-security-group 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --resource-group-id fee82deba12e4c0fb69c3b09d1f12345`
- `ibmcloud is security-group-create my-security-group 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --resource-group-name Default`
- `ibmcloud is security-group-create my-security-group 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --output JSON`

---

### ibmcloud is security-group-update
{: #security-group-update}

Update a security group.

```
ibmcloud is security-group-update GROUP [--name NEW_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #security-group-update-command-options}

- **GROUP**: ID of the security group.
- **--name**: New name of the security group.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #security-group-update-examples}

`ibmcloud is security-group-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --name my-security-group-name --output JSON`

---

### ibmcloud is security-group-delete
{: #security-group-delete}

Delete security groups.

```
ibmcloud is security-group-delete (GROUP1 GROUP2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #security-group-delete-command-options}

- **GROUP1**: ID of the security group.
- **GROUP2**: ID of the security group.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is security-group-network-interfaces
{: #security-group-network-interfaces}

List all network interfaces of a security group.

```
ibmcloud is security-group-network-interfaces GROUP [--output JSON] [-q, --quiet]
```

#### Command options
{: #security-group-network-interfaces-command-options}

- **GROUP**: ID of the security group.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is security-group-network-interface
{: #security-group-network-interface}

View details of a network interface of a security group.

```
ibmcloud is security-group-network-interface GROUP NIC [--output JSON] [-q, --quiet]
```

#### Command options
{: #security-group-network-interface-command-options}

- **GROUP**: ID of the security group.
- **NIC**: ID of the network interface.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is security-group-network-interface-add
{: #security-group-network-interface-add}

Add a network interface to a security group.

```
ibmcloud is security-group-network-interface-add GROUP NIC [--output JSON] [-q, --quiet]
```

#### Command options
{: #security-group-network-interface-add-command-options}

- **GROUP**: ID of the security group.
- **NIC**: ID of the network interface.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #security-group-network-interface-add-examples}

`ibmcloud is security-group-network-interface-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 8daca77a-4980-4d33-8f3e-7038797be8f9 --output JSON`

---

### ibmcloud is security-group-network-interface-remove
{: #security-group-network-interface-remove}

Remove network interfaces from a security group.

```
ibmcloud is security-group-network-interface-remove GROUP (NIC1 NIC2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #security-group-network-interface-remove-command-options}

- **GROUP**: ID of the security group.
- **NIC1**: ID of the network interface.
- **NIC2**: ID of the network interface.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is security-group-rules
{: #security-group-rules}

List all rules of a security group.

```
ibmcloud is security-group-rules GROUP [--output JSON] [-q, --quiet]
```

#### Command options
{: #security-group-rules-command-options}

- **GROUP**: ID of the security group.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is security-group-rule
{: #security-group-rule}

View details of a security group rule.

```
ibmcloud is security-group-rule GROUP RULE_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #security-group-rule-command-options}

- **GROUP**: ID of the security group.
- **RULE_ID**: ID of the security group rule.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is security-group-rule-add
{: #security-group-rule-add}

Add a rule to a security group.

```
ibmcloud is security-group-rule-add GROUP DIRECTION PROTOCOL [--remote REMOTE_ADDRESS | CIDR_BLOCK | SECURITY_GROUP_ID] [--icmp-type ICMP_TYPE [--icmp-code ICMP_CODE]] [--port-min PORT_MIN] [--port-max PORT_MAX] [--output JSON] [-q, --quiet]
```

#### Command options
{: #security-group-rule-add-command-options}

- **GROUP**: ID of the security group.
- **DIRECTION**: Direction of traffic to enforce. One of: **inbound**, **outbound**.
- **PROTOCOL**: Protocol to enforce. One of: **all**, **icmp**, **tcp**, **udp**.
- **--remote**: The set of network interfaces from which this rule allows traffic, Can be specified as either an REMOTE_ADDRESS, CIDR_BLOCK and SECURITY_GROUP_ID. If unspecified, then traffic is allowed from any source (or to any source, for outbound rules).
- **--icmp-type**: ICMP traffic type to allow. Valid values from **0** to **254**. This option is specified only when protocol is set to **icmp**. If unspecified, all types are allowed.
- **--icmp-code**: ICMP traffic code to allow. Valid values from **0** to **255**. This option is specified only when protocol is set to **icmp**. If unspecified, all codes are allowed.
- **--port-min**: Minimum port number. Valid values are from **1** to **65535**. This option is specified only when protocol is set to **tcp** or **udp**. If unspecified, all ports are allowed (default: **1**).
- **--port-max**: Maximum port number. Valid values are from **1** to **65535**. This option is specified only when protocol is set to **tcp** or **udp**. If unspecified, all ports are allowed (default: **65535**).
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #security-group-rule-add-examples}

- `ibmcloud is security-group-rule-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 inbound all`
- `ibmcloud is security-group-rule-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 inbound icmp --icmp-type 8 --icmp-code 0`
- `ibmcloud is security-group-rule-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 inbound all --remote 12.2.2.3`
- `ibmcloud is security-group-rule-add 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 inbound tcp --port-min 4 --port-max 22 --output JSON`

---

### ibmcloud is security-group-rule-update
{: #security-group-rule-update}

Update a rule of a security group.

```
ibmcloud is security-group-rule-update GROUP RULE_ID [--direction inbound | outbound] [--remote REMOTE_ADDRESS | CIDR_BLOCK | SECURITY_GROUP_ID] [--icmp-type ICMP_TYPE [--icmp-code ICMP_CODE]] [--port-min PORT_MIN] [--port-max PORT_MAX] [--output JSON] [-q, --quiet]
```

#### Command options
{: #security-group-rule-update-command-options}

- **GROUP**: ID of the security group.
- **RULE_ID**: ID of the security group rule.
- **--direction**: Direction of traffic to enforce. One of: **inbound**, **outbound**.
- **--remote**: The set of network interfaces from which this rule allows traffic, Can be specified as either an REMOTE_ADDRESS, CIDR_BLOCK and SECURITY_GROUP_ID. If unspecified, then traffic is allowed from any source (or to any source, for outbound rules).
- **--icmp-type**: ICMP traffic type to allow. Valid values from **0** to **254**. This option is specified only when protocol is set to **icmp**. If unspecified, all types are allowed.
- **--icmp-code**: ICMP traffic code to allow. Valid values from **0** to **255**. This option is specified only when protocol is set to **icmp**. If unspecified, all codes are allowed.
- **--port-min**: Minimum port number. Valid values are from **1** to **65535**. This option is specified only when protocol is set to **tcp** or **udp**. If unspecified, all ports are allowed (default: **1**).
- **--port-max**: Maximum port number. Valid values are from **1** to **65535**. This option is specified only when protocol is set to **tcp** or **udp**. If unspecified, all ports are allowed (default: **65535**).
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #security-group-rule-update-examples}

- `ibmcloud is security-group-rule-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 8daca77a-4980-4d33-8f3e-7038797be8f9 --direction inbound`
- `ibmcloud is security-group-rule-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 8daca77a-4980-4d33-8f3e-7038797be8f9 --direction inbound --icmp-type 8 --icmp-code 0`
- `ibmcloud is security-group-rule-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 8daca77a-4980-4d33-8f3e-7038797be8f9 --direction inbound --port-min 4 --port-max 22`
- `ibmcloud is security-group-rule-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 8daca77a-4980-4d33-8f3e-7038797be8f9 --direction inbound --remote 12.2.2.3`
- `ibmcloud is security-group-rule-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 8daca77a-4980-4d33-8f3e-7038797be8f9 --direction inbound --output JSON`

---

### ibmcloud is security-group-rule-delete
{: #security-group-rule-delete}

Delete rules from a security group.

```
ibmcloud is security-group-rule-delete GROUP (RULE_ID1 RULE_ID2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #security-group-rule-delete-command-options}

- **GROUP**: ID of the security group.
- **RULE_ID1**: ID of the security group rule.
- **RULE_ID2**: ID of the security group rule.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

## VPCs
{: #vpcs-section}
The following section provides information about CLI commands for VPC functionality.

### ibmcloud is vpcs
{: #vpcs}

List all VPCs.

```
ibmcloud is vpcs [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME | --all-resource-groups] [--classic-access true | false] [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpcs-command-options}

- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--all-resource-groups**: Query all resource groups.
- **--classic-access**: This flag lists VPCs that have classic access enabled. If unspecified, it returns all VPCs with and without classic access enabled. One of: **true**, **false**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpc
{: #vpc}

View details of a VPC.

```
ibmcloud is vpc VPC [--show-attached] [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpc-command-options}

- **VPC**: ID of the VPC.
- **--show-attached**: View details of resources (subnets, VPC routes and address prefix) attached to this VPC.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpc-create
{: #vpc-create}

Create a VPC.

```
ibmcloud is vpc-create VPC_NAME [--classic-access] [--address-prefix-management auto | manual] [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpc-create-command-options}

- **VPC_NAME**: Name of the VPC.
- **--classic-access**: This flag indicates whether the VPC should be connected to Classic Infrastructure. The default value is false.
- **--address-prefix-management**: This flag indicates if a default address prefix is automatically created for each zone in this VPC. If **manual**, this VPC is created with no default address prefixes. One of: **auto**, **manual**. (default: **auto**).
- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #vpc-create-examples}

- `ibmcloud is vpc-create my-vpc --classic-access`
- `ibmcloud is vpc-create my-vpc --address-prefix-management auto`
- `ibmcloud is vpc-create my-vpc --resource-group-id fee82deba12e4c0fb69c3b09d1f12345`
- `ibmcloud is vpc-create my-vpc --resource-group-name Default --output JSON`

---

### ibmcloud is vpc-update
{: #vpc-update}

Update a VPC.

```
ibmcloud is vpc-update VPC --name NEW_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpc-update-command-options}

- **VPC**: ID of the VPC.
- **--name**: New name of the VPC.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #vpc-update-examples}

`ibmcloud is vpc-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 --name my-vpc`

---

### ibmcloud is vpc-delete
{: #vpc-delete}

Delete VPCs.

```
ibmcloud is vpc-delete (VPC1 VPC2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #vpc-delete-command-options}

- **VPC1**: ID of the VPC.
- **VPC2**: ID of the VPC.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpc-default-security-group
{: #vpc-default-security-group}

View details of the default security group of a VPC.

```
ibmcloud is vpc-default-security-group VPC [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpc-default-security-group-command-options}

- **VPC**: ID of the VPC.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpc-address-prefix
{: #vpc-address-prefix}

View details of a VPC address prefix.

```
ibmcloud is vpc-address-prefix VPC PREFIX [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpc-address-prefix-command-options}

- **VPC**: ID of the VPC.
- **PREFIX**: ID of the VPC address prefix.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpc-address-prefix-create
{: #vpc-address-prefix-create}

Create an address prefix.

```
ibmcloud is vpc-address-prefix-create PREFIX_NAME VPC ZONE_NAME CIDR [--default false | true] [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpc-address-prefix-create-command-options}

- **PREFIX_NAME**: Name of the VPC address prefix.
- **VPC**: ID of the VPC.
- **ZONE_NAME**: Name of the zone.
- **CIDR**: The CIDR block for this address prefix. It must not overlap with any existing address prefixes in the VPC, or the reserved CIDR blocks 169.254.0.0/16 and 161.26.0.0/16.
- **--default**: This flag indicates whether this is the default prefix for this zone in this VPC. One of: **false**, **true**. (default: **false**).
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #vpc-address-prefix-create-examples}

`ibmcloud is vpc-address-prefix-create my-prefix 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 us-south-2 10.0.0.0/24 --default true --output JSON`

---

### ibmcloud is vpc-address-prefix-delete
{: #vpc-address-prefix-delete}

Delete address prefixes.

```
ibmcloud is vpc-address-prefix-delete VPC (PREFIX1 PREFIX2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #vpc-address-prefix-delete-command-options}

- **VPC**: ID of the VPC.
- **PREFIX1**: ID of the VPC address prefix.
- **PREFIX2**: ID of the VPC address prefix.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpc-address-prefix-update
{: #vpc-address-prefix-update}

Update an address prefix.

```
ibmcloud is vpc-address-prefix-update VPC PREFIX [--name NEW_NAME] [--default false | true] [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpc-address-prefix-update-command-options}

- **VPC**: ID of the VPC.
- **PREFIX**: ID of the VPC address prefix.
- **--name**: New name of the address prefix.
- **--default**: This flag indicates whether this is the default prefix for this zone in this VPC. One of: **false**, **true**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #vpc-address-prefix-update-examples}

`ibmcloud is vpc-address-prefix-update 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479 fee82deba12e4c0fb69c3b09d1f12345 --name my-prefix --default false --output JSON`

---

### ibmcloud is vpc-address-prefixes
{: #vpc-address-prefixes}

List all address prefixes.

```
ibmcloud is vpc-address-prefixes VPC [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpc-address-prefixes-command-options}

- **VPC**: ID of the VPC.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpc-routes
{: #vpc-routes}

List all routes.

```
ibmcloud is vpc-routes VPC [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpc-routes-command-options}

- **VPC**: ID of the VPC.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpc-route
{: #vpc-route}

View details of a VPC route.

```
ibmcloud is vpc-route VPC ROUTE [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpc-route-command-options}

- **VPC**: ID of the VPC.
- **ROUTE**: ID of the VPC route.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpc-route-create
{: #vpc-route-create}

Create a route.

```
ibmcloud is vpc-route-create ROUTE_NAME VPC --zone ZONE_NAME --destination DESTINATION_CIDR --next-hop-ip NEXT_HOP_IP [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpc-route-create-command-options}

- **ROUTE_NAME**: Name of the VPC route.
- **VPC**: ID of the VPC.
- **--zone**: Name of the zone.
- **--destination**: The destination CIDR of the route.
- **--next-hop-ip**: The IP address of the next hop to which to route packets.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #vpc-route-create-examples}

`ibmcloud is vpc-route-create my-vpc-route 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 --zone us-south-1 --destination  10.2.2.0/24 --next-hop-ip 10.0.0.2 --output JSON`

---

### ibmcloud is vpc-route-update
{: #vpc-route-update}

Update a route.

```
ibmcloud is vpc-route-update VPC ROUTE --name NEW_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpc-route-update-command-options}

- **VPC**: ID of the VPC.
- **ROUTE**: ID of the VPC route.
- **--name**: New name of the route.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #vpc-route-update-examples}

`ibmcloud is vpc-route-update 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3 72b27b5c-f4b0-48bb-b954-5becc7c1d456 --name my-vpc-route --output JSON`

---

### ibmcloud is vpc-route-delete
{: #vpc-route-delete}

Delete routes.

```
ibmcloud is vpc-route-delete VPC (ROUTE1 ROUTE2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #vpc-route-delete-command-options}

- **VPC**: ID of the VPC.
- **ROUTE1**: ID of the VPC route.
- **ROUTE2**: ID of the VPC route.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

## REGIONS & ZONES COMMANDS
{: #geography-section}
This section gives details about the CLI commands available for working with regions and zones.

## Regions
{: #vpc-regions-commands-section}
This section contains commands related to the functionality of geographical regions.

### ibmcloud is regions
{: #regions}

List all regions.

```
ibmcloud is regions [--output JSON] [-q, --quiet]
```

#### Command options
{: #regions-command-options}

- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is region
{: #region}

View details of a region.

```
ibmcloud is region REGION_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #region-command-options}

- **REGION_NAME**: Name of the region.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

## Zones
{: #zones-cli-section}
The following section provides information about CLI commands for zones.

### ibmcloud is zones
{: #zones}

List all zones in the target region.

```
ibmcloud is zones [--output JSON] [-q, --quiet]
```

#### Command options
{: #zones-command-options}

- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is zone
{: #zone}

View details of a zone in the target region.

```
ibmcloud is zone ZONE_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #zone-command-options}

- **ZONE_NAME**: Name of the zone.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

## VPN COMMANDS
{: #vpn-section}
This section gives details about the CLI commands available for working with VPN, including IKE and IPsec policies.

## IKE policies
{: #ike-policies-cli-section}
The following section provides information about CLI commands for IKE policies.

### ibmcloud is ike-policies
{: #ike-policies}

List all IKE policies.

```
ibmcloud is ike-policies [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME | --all-resource-groups] [--output JSON] [-q, --quiet]
```

#### Command options
{: #ike-policies-command-options}

- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--all-resource-groups**: Query all resource groups.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is ike-policy
{: #ike-policy}

View details of an IKE policy.

```
ibmcloud is ike-policy IKE_POLICY_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #ike-policy-command-options}

- **IKE_POLICY_ID**: ID of the IKE policy.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is ike-policy-create
{: #ike-policy-create}

Create an IKE policy.

```
ibmcloud is ike-policy-create IKE_POLICY_NAME AUTHENTICATION_ALGORITHM DH_GROUP ENCRYPTION_ALGORITHM IKE_VERSION [--key-lifetime KEY_LIFETIME] [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #ike-policy-create-command-options}

- **IKE_POLICY_NAME**: Name of the IKE policy.
- **AUTHENTICATION_ALGORITHM**: The authentication algorithm. One of: **md5**, **sha1**, **sha256**.
- **DH_GROUP**: The Diffie-Hellman group. One of: **2**, **5**, **14**.
- **ENCRYPTION_ALGORITHM**: The encryption algorithm. One of: **triple_des**, **aes128**, **aes256**.
- **IKE_VERSION**: The IKE protocol version. One of: **1**, **2**.
- **--key-lifetime**: The key lifetime in seconds. Maximum: **86400**, Minimum: **1800**. (default: **28800**).
- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #ike-policy-create-examples}

- `ibmcloud is ike-policy-create my-ike-policy md5 2 aes128 2`
- `ibmcloud is ike-policy-create my-ike-policy md5 2 aes128 2 --key-lifetime 28000`
- `ibmcloud is ike-policy-create my-ike-policy md5 2 aes128 2 --resource-group-name Default`
- `ibmcloud is ike-policy-create my-ike-policy md5 2 aes128 2 --resource-group-id fee82deba12e4c0fb69c3b09d1f12345 --output JSON`

---

### ibmcloud is ike-policy-delete
{: #ike-policy-delete}

Delete IKE policies.

```
ibmcloud is ike-policy-delete (IKE_POLICY_ID1 IKE_POLICY_ID2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #ike-policy-delete-command-options}

- **IKE_POLICY_ID1**: ID of the IKE policy.
- **IKE_POLICY_ID2**: ID of the IKE policy.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is ike-policy-update
{: #ike-policy-update}

Update an IKE policy.

```
ibmcloud is ike-policy-update IKE_POLICY_ID [--name NEW_NAME] [--authentication-algorithm md5 | sha1 | sha256] [--dh-group 2 | 5 | 14] [--encryption-algorithm triple_des | aes128 | aes256] [--ike-version 1 | 2] [--key-lifetime KEY_LIFETIME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #ike-policy-update-command-options}

- **IKE_POLICY_ID**: ID of the IKE policy.
- **--name**: New name of the IKE policy.
- **--authentication-algorithm**: The authentication algorithm. One of: **md5**, **sha1**, **sha256**.
- **--dh-group**: The Diffie-Hellman group. One of: **2**, **5**, **14**.
- **--encryption-algorithm**: The encryption algorithm. One of: **triple_des**, **aes128**, **aes256**.
- **--ike-version**: The IKE protocol version. One of: **1**, **2**.
- **--key-lifetime**: The key lifetime in seconds. Maximum: **86400**, Minimum: **1800**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #ike-policy-update-examples}

- `ibmcloud is ike-policy-update fee82deba12e4c0fb69c3b09d1f12345 --name my-ike-policy`
- `ibmcloud is ike-policy-update fee82deba12e4c0fb69c3b09d1f12345 --authentication-algorithm md5`
- `ibmcloud is ike-policy-update fee82deba12e4c0fb69c3b09d1f12345 --dh-group 2`
- `ibmcloud is ike-policy-update fee82deba12e4c0fb69c3b09d1f12345 --encryption-algorithm aes128`
- `ibmcloud is ike-policy-update fee82deba12e4c0fb69c3b09d1f12345 --ike-version 2`
- `ibmcloud is ike-policy-update fee82deba12e4c0fb69c3b09d1f12345 --key-lifetime 28000 --output JSON`

---

### ibmcloud is ike-policy-connections
{: #ike-policy-connections}

List all connections that use the IKE policy.

```
ibmcloud is ike-policy-connections IKE_POLICY_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #ike-policy-connections-command-options}

- **IKE_POLICY_ID**: ID of the IKE policy.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

## IPsec policies
{: #ipsec-policies-cli-section}
The following section provides information about CLI commands for IPsec functionality.

### ibmcloud is ipsec-policies
{: #ipsec-policies}

List all IPsec policies.

```
ibmcloud is ipsec-policies [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME | --all-resource-groups] [--output JSON] [-q, --quiet]
```

#### Command options
{: #ipsec-policies-command-options}

- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--all-resource-groups**: Query all resource groups.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is ipsec-policy
{: #ipsec-policy}

View details of an IPsec policy.

```
ibmcloud is ipsec-policy IPSEC_POLICY_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #ipsec-policy-command-options}

- **IPSEC_POLICY_ID**: ID of the IPsec policy.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is ipsec-policy-create
{: #ipsec-policy-create}

Create an IPsec policy.

```
ibmcloud is ipsec-policy-create IPSEC_POLICY_NAME AUTHENTICATION_ALGORITHM ENCRYPTION_ALGORITHM PFS [--key-lifetime KEY_LIFETIME] [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #ipsec-policy-create-command-options}

- **IPSEC_POLICY_NAME**: Name of the IPsec policy.
- **AUTHENTICATION_ALGORITHM**: The authentication algorithm. One of: **md5**, **sha1**, **sha256**.
- **ENCRYPTION_ALGORITHM**: The encryption algorithm. One of: **triple_des**, **aes128**, **aes256**.
- **PFS**: The Diffie-Hellman group. One of: **disabled**, **group_2**, **group_5**, **group_14**.
- **--key-lifetime**: The key lifetime in seconds. Maximum: **86400**, Minimum: **1800**. (default: **3600**).
- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #ipsec-policy-create-examples}

- `ibmcloud is ipsec-policy-create my-ipsec-policy md5 aes128 group_2`
- `ibmcloud is ipsec-policy-create my-ipsec-policy md5 aes128 group_2 --key-lifetime 3600`
- `ibmcloud is ipsec-policy-create my-ipsec-policy md5 aes128 group_2 --resource-group-name Default`
- `ibmcloud is ipsec-policy-create my-ipsec-policy md5 aes128 group_2 --resource-group-id fee82deba12e4c0fb69c3b09d1f12345 --output JSON`

---

### ibmcloud is ipsec-policy-delete
{: #ipsec-policy-delete}

Delete an IPsec policies.

```
ibmcloud is ipsec-policy-delete (IPSEC_POLICY_ID1 IPSEC_POLICY_ID2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #ipsec-policy-delete-command-options}

- **IPSEC_POLICY_ID1**: ID of the IPsec policy.
- **IPSEC_POLICY_ID2**: ID of the IPsec policy.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is ipsec-policy-update
{: #ipsec-policy-update}

Update an IPsec policy.

```
ibmcloud is ipsec-policy-update IPSEC_POLICY_ID [--name NEW_NAME] [--authentication-algorithm md5 | sha1 | sha256] [--pfs disabled | group_2 | group_5 | group_14] [--encryption-algorithm triple_des | aes128 | aes256] [--key-lifetime KEY_LIFETIME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #ipsec-policy-update-command-options}

- **IPSEC_POLICY_ID**: ID of the IPsec policy.
- **--name**: New name of the IPsec policy.
- **--authentication-algorithm**: The authentication algorithm. One of: **md5**, **sha1**, **sha256**.
- **--pfs**: Perfect Forward Secrecy. One of: **disabled**, **group_2**, **group_5**, **group_14**.
- **--encryption-algorithm**: The encryption algorithm. One of: **triple_des**, **aes128**, **aes256**.
- **--key-lifetime**: The key lifetime in seconds. Maximum: **86400**, Minimum: **1800**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #ipsec-policy-update-examples}

- `ibmcloud is ipsec-policy-update fee82deba12e4c0fb69c3b09d1f12345 --name my-ipsec-policy`
- `ibmcloud is ipsec-policy-update fee82deba12e4c0fb69c3b09d1f12345 --authentication-algorithm md5`
- `ibmcloud is ipsec-policy-update fee82deba12e4c0fb69c3b09d1f12345 --pfs group_2`
- `ibmcloud is ipsec-policy-update fee82deba12e4c0fb69c3b09d1f12345 --encryption-algorithm aes128`
- `ibmcloud is ipsec-policy-update fee82deba12e4c0fb69c3b09d1f12345 --key-lifetime 3600 --output JSON`

---

### ibmcloud is ipsec-policy-connections
{: #ipsec-policy-connections}

List all connections that use the IPsec policy.

```
ibmcloud is ipsec-policy-connections IPSEC_POLICY_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #ipsec-policy-connections-command-options}

- **IPSEC_POLICY_ID**: ID of the IPsec policy.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

## VPN gateways
{: #vpn-gateway-commands-section}
This section contains commands available for working with VPN for VPC gateways.

### ibmcloud is vpn-gateways
{: #vpn-gateways}

List all VPN gateways.

```
ibmcloud is vpn-gateways [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME | --all-resource-groups] [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpn-gateways-command-options}

- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--all-resource-groups**: Query all resource groups.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpn-gateway
{: #vpn-gateway}

View details of a VPN gateway.

```
ibmcloud is vpn-gateway VPN_GATEWAY_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-command-options}

- **VPN_GATEWAY_ID**: ID of the VPN gateway.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpn-gateway-create
{: #vpn-gateway-create}

Create a VPN gateway.

```
ibmcloud is vpn-gateway-create VPN_GATEWAY_NAME SUBNET [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-create-command-options}

- **VPN_GATEWAY_NAME**: Name of the VPN gateway.
- **SUBNET**: ID of the subnet.
- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #vpn-gateway-create-examples}

- `ibmcloud is vpn-gateway-create my-vpc-gateway fee82deba12e4c0fb69c3b09d1f12345`
- `ibmcloud is vpn-gateway-create my-vpc-gateway fee82deba12e4c0fb69c3b09d1f12345 --resource-group-name Default`
- `ibmcloud is vpn-gateway-create my-vpc-gateway fee82deba12e4c0fb69c3b09d1f12345 --resource-group-id fee82deba12e4c0fb69c3b09d1f12345 --output JSON`

---

### ibmcloud is vpn-gateway-delete
{: #vpn-gateway-delete}

Delete VPN gateways.

```
ibmcloud is vpn-gateway-delete (VPN_GATEWAY_ID1 VPN_GATEWAY_ID2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-delete-command-options}

- **VPN_GATEWAY_ID1**: ID of the VPN gateway.
- **VPN_GATEWAY_ID2**: ID of the VPN gateway.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpn-gateway-update
{: #vpn-gateway-update}

Update a VPN gateway.

```
ibmcloud is vpn-gateway-update VPN_GATEWAY_ID [--name NEW_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-update-command-options}

- **VPN_GATEWAY_ID**: ID of the VPN gateway.
- **--name**: New name of the VPN gateway.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #vpn-gateway-update-examples}

`ibmcloud is vpn-gateway-update fee82deba12e4c0fb69c3b09d1f12345 --name my-gateway --output JSON`

---

### ibmcloud is vpn-gateway-connections
{: #vpn-gateway-connections}

List all VPN gateway connections.

```
ibmcloud is vpn-gateway-connections VPN_GATEWAY_ID [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-connections-command-options}

- **VPN_GATEWAY_ID**: ID of the VPN gateway.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpn-gateway-connection-create
{: #vpn-gateway-connection-create}

Create a VPN gateway connection.

```
ibmcloud is vpn-gateway-connection-create CONNECTION_NAME VPN_GATEWAY_ID PEER_ADDRESS PRESHARED_KEY --local-cidr CIDR1 --local-cidr CIDR2 ... --peer-cidr CIDR1 --peer-cidr CIDR2 ... [--admin-state-up true | false] [--dead-peer-detection-action restart | clear | hold | none] [--dead-peer-detection-interval INTERVAL] [--dead-peer-detection-timeout TIMEOUT] [--ike-policy IKE_POLICY_ID] [--ipsec-policy IPSEC_POLICY_ID] [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-connection-create-command-options}

- **CONNECTION_NAME**: Name of the connection.
- **VPN_GATEWAY_ID**: ID of the VPN gateway.
- **PEER_ADDRESS**: The IP address of the peer VPN gateway.
- **PRESHARED_KEY**: The preshared key.
- **--admin-state-up**: If set to false, the VPN gateway connection is shut down. One of: **true**, **false**. (default: **true**).
- **--dead-peer-detection-action**: Dead Peer Detection actions. One of: **restart**, **clear**, **hold**, **none**. (default: **restart**).
- **--dead-peer-detection-interval**: Dead Peer Detection interval in seconds (default: **2**).
- **--dead-peer-detection-timeout**: Dead Peer Detection timeout in seconds (default: **10**).
- **--ike-policy**: ID of the IKE policy.
- **--ipsec-policy**: ID of the IPsec policy.
- **--local-cidr**: Local CIDR for the resource.
- **--peer-cidr**: Peer CIDRs for the resource.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #vpn-gateway-connection-create-examples}

- `ibmcloud is vpn-gateway-connection-create my-connection fee82deba12e4c0fb69c3b09d1f12345 169.21.50.5 lkj14b1oi0alcniejkso --local-cidr 10.240.0.0/24 --peer-cidr 192.168.1.0/24`
- `ibmcloud is vpn-gateway-connection-create my-connection fee82deba12e4c0fb69c3b09d1f12345 169.21.50.5 lkj14b1oi0alcniejkso --local-cidr 10.240.0.0/24 --peer-cidr 192.168.1.0/24 --admin-state-up true`
- `ibmcloud is vpn-gateway-connection-create my-connection fee82deba12e4c0fb69c3b09d1f12345 169.21.50.5 lkj14b1oi0alcniejkso --local-cidr 10.240.0.0/24 --peer-cidr 192.168.1.0/24 --dead-peer-detection-action clear --dead-peer-detection-interval 33 --dead-peer-detection-timeout 100`
- `ibmcloud is vpn-gateway-connection-create my-connection fee82deba12e4c0fb69c3b09d1f12345 169.21.50.5 lkj14b1oi0alcniejkso --local-cidr 10.240.0.0/24 --peer-cidr 192.168.1.0/24 --ipsec-policy 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479`
- `ibmcloud is vpn-gateway-connection-create my-connection fee82deba12e4c0fb69c3b09d1f12345 169.21.50.5 lkj14b1oi0alcniejkso --local-cidr 10.240.0.0/24 --peer-cidr 192.168.1.0/24 --ike-policy 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479`
- `ibmcloud is vpn-gateway-connection-create my-connection fee82deba12e4c0fb69c3b09d1f12345 169.21.50.5 lkj14b1oi0alcniejkso --local-cidr 16.3.4.5 --local-cidr 12.3.4.5 --peer-cidr 16.3.4.5 --peer-cidr 12.3.4.5  --output JSON`

---

### ibmcloud is vpn-gateway-connection
{: #vpn-gateway-connection}

View details of a VPN gateway connection.

```
ibmcloud is vpn-gateway-connection VPN_GATEWAY_ID (CONNECTION_ID1 CONNECTION_ID2 ...) [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-connection-command-options}

- **VPN_GATEWAY_ID**: ID of the VPN gateway.
- **CONNECTION_ID1**: ID of the VPN connection.
- **CONNECTION_ID2**: ID of the VPN connection.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpn-gateway-connection-delete
{: #vpn-gateway-connection-delete}

Delete VPN gateway connections.

```
ibmcloud is vpn-gateway-connection-delete VPN_GATEWAY_ID (CONNECTION_ID1 CONNECTION_ID2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-connection-delete-command-options}

- **VPN_GATEWAY_ID**: ID of the VPN gateway.
- **CONNECTION_ID1**: ID of the VPN connection.
- **CONNECTION_ID2**: ID of the VPN connection.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpn-gateway-connection-update
{: #vpn-gateway-connection-update}

Update a VPN gateway connection.

```
ibmcloud is vpn-gateway-connection-update VPN_GATEWAY_ID CONNECTION_ID [--admin-state-up true | false] [--dead-peer-detection-action restart | clear | hold | none] [--dead-peer-detection-interval INTERVAL] [--dead-peer-detection-timeout TIMEOUT] [--ike-policy IKE_POLICY_ID] [--ipsec-policy IPSEC_POLICY_ID] [--peer-address ADDRESS] [--psk PSK] [--name NEW_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-connection-update-command-options}

- **VPN_GATEWAY_ID**: ID of the VPN gateway.
- **CONNECTION_ID**: ID of the VPN connection.
- **--admin-state-up**: If set to false, the VPN gateway connection is shut down. One of: **true**, **false**.
- **--dead-peer-detection-action**: Dead Peer Detection actions. One of: **restart**, **clear**, **hold**, **none**.
- **--dead-peer-detection-interval**: Dead Peer Detection interval in seconds.
- **--dead-peer-detection-timeout**: Dead Peer Detection timeout in seconds.
- **--ike-policy**: ID of the IKE policy.
- **--ipsec-policy**: ID of the IPsec policy.
- **--peer-address**: The IP address of the peer VPN gateway.
- **--psk**: The preshared key.
- **--name**: New name of the connection.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #vpn-gateway-connection-update-examples}

`ibmcloud is vpn-gateway-connection-update fee82deba12e4c0fb69c3b09d1f12345 gfe82deba12e4c0fb69c3b09d1f23456 --admin-state-up true --dead-peer-detection-action clear --dead-peer-detection-interval 33 --dead-peer-detection-timeout 100  --ipsec-policy 72251a2e-d6c5-42b4-97b0-b5f8e8d1f479  --ipsec-policy 05251a2e-d6c5-42b4-97b0-b5f8e8d1f445 --peer-address 234.3.4.5 -psk rweirjgiort --name my-new-connection --output JSON`

---

### ibmcloud is vpn-gateway-connection-local-cidr-delete
{: #vpn-gateway-connection-local-cidr-delete}

Remove a local CIDR from the VPN gateway connection.

```
ibmcloud is vpn-gateway-connection-local-cidr-delete VPN_GATEWAY_ID CONNECTION_ID PREFIX_ADDRESS PREFIX_LENGTH [-f, --force] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-connection-local-cidr-delete-command-options}

- **VPN_GATEWAY_ID**: ID of the VPN gateway.
- **CONNECTION_ID**: ID of the VPN connection.
- **PREFIX_ADDRESS**: The prefix address part of the CIDR.
- **PREFIX_LENGTH**: The prefix length part of the CIDR.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpn-gateway-connection-local-cidr-add
{: #vpn-gateway-connection-local-cidr-add}

Add a local CIDR to a VPN gateway connection.

```
ibmcloud is vpn-gateway-connection-local-cidr-add VPN_GATEWAY_ID CONNECTION_ID PREFIX_ADDRESS PREFIX_LENGTH [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-connection-local-cidr-add-command-options}

- **VPN_GATEWAY_ID**: ID of the VPN gateway.
- **CONNECTION_ID**: ID of the VPN connection.
- **PREFIX_ADDRESS**: The prefix address part of the CIDR.
- **PREFIX_LENGTH**: The prefix length part of the CIDR.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpn-gateway-connection-peer-cidr-delete
{: #vpn-gateway-connection-peer-cidr-delete}

Remove a peer CIDR from the VPN gateway connection.

```
ibmcloud is vpn-gateway-connection-peer-cidr-delete VPN_GATEWAY_ID CONNECTION_ID PREFIX_ADDRESS PREFIX_LENGTH [-f, --force] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-connection-peer-cidr-delete-command-options}

- **VPN_GATEWAY_ID**: ID of the VPN gateway.
- **CONNECTION_ID**: ID of the VPN connection.
- **PREFIX_ADDRESS**: The prefix address part of the CIDR.
- **PREFIX_LENGTH**: The prefix length part of the CIDR.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is vpn-gateway-connection-peer-cidr-add
{: #vpn-gateway-connection-peer-cidr-add}

Add a peer CIDR to a VPN gateway connection.

```
ibmcloud is vpn-gateway-connection-peer-cidr-add VPN_GATEWAY_ID CONNECTION_ID PREFIX_ADDRESS PREFIX_LENGTH [--output JSON] [-q, --quiet]
```

#### Command options
{: #vpn-gateway-connection-peer-cidr-add-command-options}

- **VPN_GATEWAY_ID**: ID of the VPN gateway.
- **CONNECTION_ID**: ID of the VPN connection.
- **PREFIX_ADDRESS**: The prefix address part of the CIDR.
- **PREFIX_LENGTH**: The prefix length part of the CIDR.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

## STORAGE COMMANDS
{: #storage-cli-section}
This section gives details about the CLI commands available for working with block storage volumes.

## Volumes
{: #volume-cli}
The following section provides information about CLI commands for volumes.

### ibmcloud is volume
{: #volume}

View details of a volume.

```
ibmcloud is volume VOLUME [--output JSON] [-q, --quiet]
```

#### Command options
{: #volume-command-options}

- **VOLUME**: ID of the volume.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is volumes
{: #volumes}

List all volumes.

```
ibmcloud is volumes [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME | --all-resource-groups] [--output JSON] [-q, --quiet]
```

#### Command options
{: #volumes-command-options}

- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--all-resource-groups**: Query all resource groups.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is volume-create
{: #volume-create}

Create a volume.

```
ibmcloud is volume-create VOLUME_NAME PROFILE_NAME ZONE_NAME [--capacity CAPACITY] [--iops IOPS] [--encryption-key ENCRYPTION_KEY] [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME] [--output JSON] [-q, --quiet]
```

#### Command options
{: #volume-create-command-options}

- **VOLUME_NAME**: Name of the volume.
- **PROFILE_NAME**: Name of the profile.
- **ZONE_NAME**: Name of the zone.
- **--capacity**: The capacity of the volume in gigabytes. Range 10-2000. (default: **100**).
- **--iops**: Input/Output Operations Per Second for the volume, it is only applicable for custom profile volumes. For the IOPS range, refer to https://cloud.ibm.com/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-profiles-gen1#custom-gen1.
- **--encryption-key**: The CRN of the Key Management Service root key.
- **--resource-group-id**: ID of the resource group. This option is mutually exclusive with **--resource-group-name**.
- **--resource-group-name**: Name of the resource group. This option is mutually exclusive with **--resource-group-id**.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Examples
{: #volume-create-examples}

- `ibmcloud is volume-create my-volume general-purpose us-south-1`
- `ibmcloud is volume-create my-volume general-purpose us-south-1 --capacity 500`
- `ibmcloud is volume-create my-volume custom us-south-1 --iops 10000 --capacity 1000`
- `ibmcloud is volume-create my-volume general-purpose us-south-1 --encryption-key crn:v1:bluemix:public:kms:us-south:adffc98a0f1f0f95f6613b3b752286b87:e4a29d1a-2ef0-42a6-8fd2-350deb1c647e:key:5437653b-c4b1-447f-9646-b2a2a4cd6179`
- `ibmcloud is volume-create my-volume general-purpose us-south-1 --resource-group-id 72b27b5c-f4b0-48bb-b954-5becc7c1dcb3`
- `ibmcloud is volume-create my-volume general-purpose us-south-1 --resource-group-name Default`
- `ibmcloud is volume-create my-volume general-purpose us-south-1 --output JSON`

---

### ibmcloud is volume-delete
{: #volume-delete}

Delete volumes.

```
ibmcloud is volume-delete (VOLUME1 VOLUME2 ...) [--output JSON] [-f, --force] [-q, --quiet]
```

#### Command options
{: #volume-delete-command-options}

- **VOLUME1**: ID of the volume.
- **VOLUME2**: ID of the volume.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **--force, -f**: Force the operation without confirmation.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is volume-update
{: #volume-update}

Update a volume.

```
ibmcloud is volume-update VOLUME --name NEW_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #volume-update-command-options}

- **VOLUME**: ID of the volume.
- **--name**: New name of the volume.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

#### Example
{: #volume-update-examples}

`ibmcloud is volume-update 64bec87d-d175-4fa5-b240-b092fdbcedd6 --name my-volume --output JSON`

---

## Volume profiles
{: #volume-profile-cli}
The following section provides information about CLI commands for volume profiles.

### ibmcloud is volume-profile
{: #volume-profile}

View details of a volume profile.

```
ibmcloud is volume-profile PROFILE_NAME [--output JSON] [-q, --quiet]
```

#### Command options
{: #volume-profile-command-options}

- **PROFILE_NAME**: Name of the profile.
- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---

### ibmcloud is volume-profiles
{: #volume-profiles}

List all volume profiles.

```
ibmcloud is volume-profiles [--output JSON] [-q, --quiet]
```

#### Command options
{: #volume-profiles-command-options}

- **--output**: Specify output format, only JSON is supported now. One of: **JSON**.
- **-q, --quiet**: Suppress verbose output.

---
