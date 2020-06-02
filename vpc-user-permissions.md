---

copyright:
  years: 2017, 2020

lastupdated: "2020-06-01"

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
{:external: target="\_blank" .external}

# Giving user permissions to manage VPC resources
{: #managing-user-permissions-for-vpc-resources}

{{site.data.keyword.vpc_full}} uses role-based access control that enables account administrators to control their users' access to VPC infrastructure service resources. To manage access or assign new access for users by using [IAM](/docs/iam?topic=iam-iamoverview) policies, you must be the account owner, administrator on all services in the account, or the assigned administrator for the particular service or service instance.

This document shows you how the administrator of the account can add additional users to the account and give them the correct permissions to manage [VPC infrastructure service resources](/docs/vpc-on-classic?topic=vpc-on-classic-about-vpc-infrastructure-resources). It covers two common scenarios for a VPC administrator:

* **Simple access scenario:** Shows how to assign an access policy to a user, so the user can create and use VPC infrastructure service resources.

* **Team access scenario:** Shows how to set up resource groups and access policies that allow two separate teams to create and use the VPC resources assigned to their team.

Changes to IAM access policies for VPC infrastructure service resources may take up to 10 minutes to take effect.
{: note}

Not all VPC resources can be assigned to a resource group. See the [resource table](/docs/vpc-on-classic?topic=vpc-on-classic-about-vpc-infrastructure-resources) for specifics.
{: important}

## Simple access scenario
{: #simple-access-scenario}

This scenario covers the basic steps needed to set up an individual user. We will cover two cases, inviting a new user to the account and modifying an existing user's permissions.

### Inviting a new user to create or manage infrastructure service resources
{: #inviting-a-new-user-to-create-or-manage-vpc-resources}

Invite an IBM Cloud user to your account so that they can view, create, and update VPC resources.

1. Go to the [IAM Users](https://cloud.ibm.com/iam/users){: external} page in the IBM Cloud console and click **Invite users**.
2. In the **Enter Email addressess** field, enter the email addresses of the users that you want to invite.
3. In the **Assign users additional access** section, select **IAM services** and complete the following information:
   * From the **What type of access do you want to assign?** list, select a specific service that you want to assign the users, or select **All Identity and Access enabled services** for all IAM-enabled services.
   * In the adjacent **in** field, select where you want this access granted. For example, select **Account**.
   * In the **Regions** list, select a specific region to grant access, or keep **All regions** (default).
   * In the **Platform access** and **Service access** areas, select to apply one or more access levels.   
4. Scroll to the end of the page and click **Add**.

If you want to give the user permissions to create their own resource groups, learn about [Creating and managing resource groups](/docs/resources?topic=resources-rgs#create_rgs).

### Giving an existing user permission to manage VPC resources
{: #giving-an-existing-user-permission-to-manage-vpc-resources}

This scenario covers the basic steps needed to give an existing user in your account permission to edit VPC resources.

1. Navigate to the [IAM Users UI](https://{DomainName}/iam/users){: external} in the IBM Cloud console.
2. Select the user whose authorization you're enabling.
3. Under the **Access policies** tab, select **Assign access**. 
5. In the **Assign users additional access** section, select **IAM services** and complete the following information:
   * From the **What type of access do you want to assign?** list, select **All Identity and Access enabled services** for all IAM-enabled services.
   * In the adjacent **in** field, select **All resource groups**.
   * If you want to grant access to a specific region, select it from the list; otherwise, keep **All regions** (default).
   * In the **Platform access** area, select at least **Viewer** to allow the user to create new resources in a resource group. See [Roles required to manage VPC resources](/docs/vpc-on-classic?topic=vpc-on-classic-resource-authorizations-required-for-api-and-cli-calls) to determine which permissions are needed.
   * In the **Service access** area, select at least **Reader** to give the user read access to [VPC resource types](/docs/vpc-on-classic?topic=vpc-on-classic-about-vpc-infrastructure-resources). YOu can click **View more** to select additional roles.
   * In the **Resource group access** area, select **Viewer**.
6. Scroll to the end of the page and click **Add**.

## Team access scenario
{: #team-access-scenario}

This scenario covers how an account administrator can assign authorization so that different teams have access to separate VPC resources. The example uses [resource groups](/docs/resources?topic=resources-rgs#create_rgs) to set up separate resource access for two teams. For the purposes of this example, resources are not shared across teams.

The example takes you through the process of creating resource groups, creating access groups, and assigning the appropriate policies to provide your teams with access to separate VPC resources.

Imagine you're setting up two different project teams to use two separate Virtual Private Clouds. You'll assign access to team members so that each team has access to their team's VPC resources only.

* Your first team is a test team. You've decided to assign that team access to VPCs in a resource group named `test_vpcs`.
* The second team is your production team. They'll be assigned access to VPCs in a resource group named `production_vpcs`.

This strategy can be used to assign separate VPC resources to any number of teams. However all resources share the same VPC quotas for the account. For more information about quotas and limits, see [VPC quotas](/docs/vpc-on-classic?topic=vpc-on-classic-quotas#quotas).
{: tip}

### Step 1: Create resource groups
{: #step-1-create-resource-groups}

By default, account administrators have access to create new resource groups. Other users first must be assigned the **Editor** role for **All Account Management Services**, which allows them to create resource groups.

Your first task is to create resource groups that will contain each of your teams' VPC resources.

1. Create a resource group called `test_team`.  
2. Create a resource group called `production_team`.  

For more information on how to create resource groups, see [Managing resource groups](/docs/resources?topic=resources-rgs).

### Step 2: Create access groups
{: #step-2-create-access-groups}

Resource access can be assigned to individual users, or to groups of users. Groups of users with the same access permissions are called _access groups_. In this scenario, you'll create an access group to represent each grouping of team members who require a specific type of VPC access, a total of four unique access groups.

**Task:** Create four access groups with the following names: 

* `test_team_manage_vpcs`
* `test_team_view_vpcs`
* `production_team_manage_vpcs`
* `production_team_view_vpcs`

For help creating access groups, see [Create access groups](/docs/iam?topic=iam-groups#create_ag).

### Step 3: Add IAM policies to the access groups 
{: #step-3-add-iam-policies-to-the-access-groups-you-just-created}

Add the necessary VPC access policies for each access group. For example, add a policy so members of the `test_team_manage_vpcs` access group can create, update, and delete all VPC resources in the `test_team` resource group. 

1. Navigate to the [IAM Group UI](https://{DomainName}/iam/groups){: external} in the IBM Cloud console.
2. Select an access group. Let's start with the `test_team_manage_vpcs` access group.
3. On the **Access policies** tab, click **Assign access**.
4. Select **Assign access within a resource group**.
5. Select the corresponding resource group. In this case, select the `test_team` resource group. 
6. Make sure that the **Assign access to a resource group** option remains set to **Viewer**.
7. Select the service **Infrastructure Service**.
8. Make sure that **Resource type** remains set to **All resource types**.
9. In the **Assign platform access roles** area, select **Editor**.
10. Select **Assign**.

Repeat the previous steps to add access policies for the remaining three access groups.

The teams are now set up to use VPCs. Members of the test_team_manage_vpcs and production_team_manage_vpcs access groups can now create VPCs in their assigned resource groups (that is, in the test_team_manage_vpcs and production_team_manage_vpcs resource groups).

When you create a VPC or other resources, make sure that you specify the resource group in which to create the resource. If you don't specify a resource group, the resource is created in the Default resource group.
{: tip}

### Step 4: Add users to the access groups
{: #step-4-add-users-to-the-access-groups}

Now you can assign team members (users) to the appropriate access groups. Follow these steps to add each member of the test team to the access group that allows test team VPC management:

1. Navigate to the [IAM Group UI](https://{DomainName}/iam/groups){: external} in the IBM Cloud console.
2. Select the wanted access group (start with: `test_team_manage_vpcs`).
3. Under the **Users** tab, click **Add users**.
4. Select each user you wish to add to the access group.
5. Click **Add to group**.

Repeat the previous steps to accomplish these tasks:
* Assign the wanted users to the `test_team_view_vpcs` access group.
* Assign the wanted users to the `production_team_manage_vpcs` access group.
* Assign the wanted users to the `production_team_view_vpcs` access group.

## Next steps
{: #permissions-next-steps}

The two example teams are now set up to use VPCs. At this point, members of the `test_team_manage_vpcs` and `production_team_manage_vpcs` access groups can create VPCs in their assigned resource groups.

## Related links
{: #related-links}

- Learn how to [Managing IAM access, API keys, service IDs, and access groups using the CLI](/docs/cli?topic=cli-ibmcloud_commands_iam).
