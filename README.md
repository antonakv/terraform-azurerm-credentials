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
git clone https://github.com/antonakv/azurerm-credentials-setup
```

Expected command output looks like this:

```bash
Cloning into 'azurerm-credentials-setup'...
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

Sample result
![Azure active directory](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image2.png)

- Click ```New registration```

Sample result
![App registrations](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image3.png)

- Enter application name and add it to your notes. It will be required later.

Sample result
![Enter name](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image5.png)

- Click ```Register```

Sample result
![Register](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image6.png)

- Copy ```Application (client) ID``` value and add it to the end of your local  ~/.zshrc file in a following format, 
so value is enclosed with double quotes.

Example
```bash 
export ARM_CLIENT_ID="aaaaaaaa-bbbb-cccc-9999-aaaaaaaaaaaa"
```

- Click Home -> Subscriptions and then click on your team subscription
Sample result
![Subscription](https://github.com/antonakv/azurerm-credentials-setup/raw/main/images/image7.png)

- Copy ```Subscription ID``` value and add it to the end of your local  ~/.zshrc file in a following format, 
so value is enclosed with double quotes.

Example
```bash 
export ARM_SUBSCRIPTION_ID="aaaaaaaa-bbbb-cccc-9999-aaaaaaaaaaaa"
```

- Click Access control (IAM)

Sample result
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

