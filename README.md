# Redis Template

An [IBM Cloud Schematics](https://console.bluemix.net/docs/services/schematics/index.html) template that allocates a virtual machine instance and provisions Redis onto that instance.

Schematics uses [Terraform](https://www.terraform.io/) as the infrastructure as code engine. With this template, you can provision and manage infrastructure as a single unit.

See the [Terraform provider docs](https://ibm-bluemix.github.io/tf-ibm-docs/) for available resources for the IBM Cloud. **Note**: To create the resources that this template requests, your [IBM Cloud Infrastructure (Softlayer) account](https://console.bluemix.net/docs/iam/mnginfra.html#managing-infrastructure-access) and [IBM Cloud account](https://console.bluemix.net/docs/iam/mngiam.html#iammanidaccser) must have sufficient permissions.

## Create an environment with this template

Environments can be used to separate software components into development tiers (e.g. staging, QA, and production).

1. In IBM Cloud, go to the menu and select the [Schematics dashboard](https://console.bluemix.net/schematics).
2. In the left navigation menu, select **Templates** to access the template catalog.
3. Click **Create** on the Redis template. You are taken to a configuration page where you can define metadata about your environment.
4. In the **Variables** section:
  a. Set the value of `temp_public_key` to `$SCHEMATICS.SSHKEYPUBLIC` to use the Schematics generated key pair for the environment.
  b. Set the value of `temp_private_key` to `$SCHEMATICS.SSHKEYPRIVATE` to use the Schematics generated key pair for the environment.
  c. If you want to be able to SSH into the virtual machine provide a value for `public_key`
5. Define values for your [variables](#variables).
6. The Redis instance has `bind 127.0.0.1` set to bind it only to localhost. SSH and modify the `/etc/redis/6379.conf` file to open Redis up for external access. You will need to restart Redis on any changes made to the configuration file.

## Variables

|Variable Name|Description|Default Value|
|-------------|-----------|-------------|
|cores|The number of CPU cores to allocate.|1|
|datacenter   |Which data center the VM is to be provisioned in. You can run `bluemix cs locations` to see a list of all data centers in your region.|wdc01|
|disk_size|Numeric disk sizes in GBs.|25|
|domain       |Domain for the computing instance.|domain.dev|
|hostname     |Hostname for the computing instance.|hostname|
|memory|The amount of memory to allocate, expressed in megabytes.|1026|
|network_speed|The connection speed (in Mbps) for the instance’s network components.|100|
|os_reference_code|An operating system reference code that is used to provision the computing instance. [Get a complete list of the OS reference codes available](https://api.softlayer.com/rest/v3/SoftLayer_Virtual_Guest_Block_Device_Template_Group/getVhdImportSoftwareDescriptions.json?objectMask=referenceCode) (use your API key as the password to log in).|CENTOS_7|
|private_network_only|When set to `true`, a compute instance only has access to the private network.|false|
|softlayer_api_key|Your IBM Cloud Infrastructure (SoftLayer) API key.| |
|softlayer_username|Your IBM Cloud Infrastructure (SoftLayer) user name.||
|ssh_key|Your public SSH key to use for access to virtual machine.||
|ssh_label|An identifying label to assign to the SSH key.|public ssh key - Schematics VM|
|ssh_notes|Notes to store with the SSH key.||
|ssh_user|The provisioning user name.|root|
|tags|Set tags on the VM instance. Permitted characters include: A-Z, 0-9, whitespace, _ (underscore), - (hyphen), . (period), and : (colon). All other characters are removed.||

## Next steps

After setting up your environment with this template, you can run **Plan** to preview how Schematics will deploy resources to your environment. When you are ready to deploy the cluster, run **Apply**.
