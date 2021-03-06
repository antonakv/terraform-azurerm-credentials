# Terraform Azurerm provider credentials 

## Intro

This manual is dedicated to setup Azure credentials for AzureRM Terraform plugin. Tested on Mac OS X.

## Requirements

- Credentials for http://portal.azure.com/ 
Ask helpdesk@ to provide access

- Your team group subscription access
If you belong to Support group then your subscription name for example will be ```Team support Engineering```
Ask helpdesk@ to provide access

- Terraform recent version installed
[Terraform installation manual](https://learn.hashicorp.com/tutorials/terraform/install-cli)

- Azure cli installed
[Azure cli installation manual](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)

## Preparation

- Clone git repository. 

```bash
git clone https://github.com/antonakv/terraform-azurerm-credentials
```

Expected command output looks like this:

```bash
Cloning into 'terraform-azurerm-credentials'...
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (12/12), done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 12 (delta 1), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (12/12), done.
Resolving deltas: 100% (1/1), done.
```

## Setup

- Login to https://portal.azure.com/ with your credentials

- Click ```Azure Active Directory```

![Azure login](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image1.png)

- Select ```App registrations```

![Azure active directory](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image2.png)

- Click ```New registration```

![App registrations](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image3.png)

- Enter application name and add it to your notes. It will be required later.

![Enter name](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image5.png)

- Click ```Register```

![Register](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image6.png)

- Copy ```Application (client) ID``` value and add it to the end of your local  ~/.zshrc file in a following format, 
so value is enclosed with double quotes.

Example
```bash 
export ARM_CLIENT_ID="aaaaaaaa-bbbb-cccc-9999-aaaaaaaaaaaa"
```

- Copy ```Application (tenant) ID``` value and add it to the end of your local  ~/.zshrc file in a following format, 
so value is enclosed with double quotes.

Example
```bash 
export ARM_TENANT_ID="aaaaaaaa-bbbb-cccc-9999-aaaaaaaaaaaa"
```


- Click Home -> Subscriptions and then click on your team subscription

![Subscription](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image7.png)

- Copy ```Subscription ID``` value and add it to the end of your local  ~/.zshrc file in a following format, 
so value is enclosed with double quotes.

Example
```bash 
export ARM_SUBSCRIPTION_ID="aaaaaaaa-bbbb-cccc-9999-aaaaaaaaaaaa"
```

- Click Access control (IAM)

![Subscription](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image8.png)

- Click ```Add``` and Click ```Add role assignment```

![Add role assignment](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image9.png)

Sample result

![Add role assignment 2](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image10.png)

- Select Role called ```Owner``` and in field ```Select``` enter name saved in your notes on the previous step
Sample result

![Enter app name](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image11.png)

- Select application which appears in the list

Sample result

![Select app](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image12.png)

- Click Save

You will see notification that Save was successful 

- Click ```Home - Azure Active Directory```

![Azure login](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image1.png)

- Select ```App registrations```

![Azure active directory](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image2.png)

- Click ```Owned applications``` and click on app name you created before

![Owned applications](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image13.png)

- Click ```Certificates and secrets``` 

![Certificates and secrets](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image14.png)

- Click ```New client secret``` 

![New secret](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image15.png)

- Click ```Add```

![Add secret](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image16.png)

- Copy created secret value and add it to the end of your local  ~/.zshrc file in a following format, 
so value is enclosed with double quotes.

![Add secret](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image17.png)

Example
```bash 
export ARM_CLIENT_SECRET="aaaaaaaa-bbbb-cccc-9999-aaaaaaaaaaaa"
```

- Reload your ~/.zshrc file

```bash
source ~/.zshrc
```

- In terminal app open folder created in the preparation stage

```bash
cd terraform-azurerm-credentials
```

Sample result

```bash
$ cd terraform-azurerm-credentials
$
```

- Initialize terraform providers
```bash
terraform init
```

Sample result
```bash
$ terraform init

Initializing the backend...

Initializing provider plugins...
- Finding hashicorp/azurerm versions matching "2.55.0"...
- Installing hashicorp/azurerm v2.55.0...
- Installed hashicorp/azurerm v2.55.0 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

- Run terraform plan

```bash 
terraform plan
```

Sample result
```bash
$ terraform plan

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.example will be created
  + resource "azurerm_resource_group" "example" {
      + id       = (known after apply)
      + location = "westeurope"
      + name     = "aakulov-example"
    }

Plan: 1 to add, 0 to change, 0 to destroy.

------------------------------------------------------------------------

Note: You didn't specify an "-out" parameter to save this plan, so Terraform
can't guarantee that exactly these actions will be performed if
"terraform apply" is subsequently run.

```

- Run terraform apply

```bash
terraform apply
```

Sample result

```bash
$ terraform apply

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.example will be created
  + resource "azurerm_resource_group" "example" {
      + id       = (known after apply)
      + location = "westeurope"
      + name     = "aakulov-example"
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

azurerm_resource_group.example: Creating...
azurerm_resource_group.example: Creation complete after 2s [id=/subscriptions/9f9b362c-0ced-42f9-8327-987494fd7c26/resourceGroups/aakulov-example]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```
