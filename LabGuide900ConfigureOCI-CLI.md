<table class="tbl-heading"><tr><td class="td-logo">![](images/obe_tag.png)

Feb 10 2019
</td>
<td class="td-banner">
# Lab 5: Configure Oracle Cloud Infrastructure Command Line Interface
</td></tr><table>
 

## Introduction

This lab walks you through some examples using the Oracle Cloud Infrastructure Command Line Interface for Autonomous Transaction Processing.

The CLI is a small footprint tool that you can use on its own or with the Console to complete Oracle Cloud Infrastructure tasks. The CLI provides the same core functionality as the Console, plus additional commands. Some of these, such as the ability to run scripts, extend the Console's functionality.

This CLI and sample is dual-licensed under the Universal Permissive License 1.0 and the Apache License 2.0; third-party content is separately licensed as described in the code.

The CLI is built on Python (version 2.7.5 or later), running on Mac, Windows, or Linux. The Python code makes calls to Oracle Cloud Infrastructure APIs to provide the functionality implemented for the various services. These are REST APIs that use HTTPS requests and responses. For more information, see [About the API](https://docs.cloud.oracle.com/iaas/Content/API/Concepts/usingapi.htm)


To **log issues**, click [here](https://github.com/alexblyth/atp-roadshow-2019/issues) to go to the github oracle repository issue submission form.

## Objectives

- Configure Oracle Cloud Infrastructure Command Line Interface
- Run examples using OCI-CLI for Autonomous Transaction Processing database

## Steps

### **STEP 1: Install Oracle Cloud Infrastructure Command Line Interface (OCI-CLI)**

The OCI CLI has already been installed on the Windows Terminial Server environment provided by your instructor. Please proceed to the next step.


### **STEP 2: Configure OCI CLI**

- This step describes the required configuration for the CLI and includes optional configurations that enable you to extend CLI functionality. 

- Before using the CLI, you have to create a config file that contains the required credentials for working with Oracle Cloud Infrastructure. You can create this file using a setup dialog or manually, using a text editor.

- To have the CLI walk you through the first-time setup process, step by step, use

```
oci setup config
```

- The command prompts you for the information required for the config file and the API public/private keys. The setup dialog generates an API key pair and creates the config file.


![](./images/900/OCI-Setup-Config.png)

- Once you run the above command, you will need to enter the following:

    - **Enter a location for your config [/Users/tejus/.oci/config]**: Press Return key
    - **Enter a user OCID**: This is located on your user information page in OCI console

    Login to OCI console and click on Menu, Identity and Users. Click on the User and navigate to User Details page. Copy the User OCID.

    ![](./images/900/UserOCID1.png)

    ![](./images/900/UserOCID2.png)


    - **Enter a tenancy OCID**: This is located in the bottom left of your OCI console
    
    Login to OCI console click on User icon on top right corner on the page and click on Tenancy and copy Tenancy OCID

    ![](./images/900/TenancyOCID1.png)

    ![](./images/900/TenancyOCID2.png)

    - **Enter a region (e.g. eu-frankfurt-1, uk-london-1, us-ashburn-1, us-phoenix-1)**: Select a region

    - **Do you want to generate a new RSA key pair? (If you decline you will be asked to supply the path to an existing key.) [Y/n]**: Y
    - **Enter a directory for your keys to be created [/Users/tejus/.oci]**: Press Return key
    - **Enter a name for your key [oci_api_key]**: Press Return key
    - **Enter a passphrase for your private key (empty for no passphrase)**: Press Return key
    
### **STEP 3: Add public key to Oracle Cloud Infrastructure**

- Now that you have a private / public key combo , you must add it to OCI Console:

Add public key to OCI User setting

- Open Terminal and navigate to folder containing **oci_api_key_public.pem**. Copy the public key.

```
cat oci_api_key_public.pem
```

![](./images/900/OCIPublicKeycleare.png)

- Login to your OCI console and click on Menu and select Identity and Users. Select a User and navigate to User Detial page.

- Click on Add Public Key under API Keys section.

![](./images/900/APIKeys.png)

- Paste Public key which you copied from CLI in Add Public Key

![](./images/900/AddPublicKey.png)


Once you add the key run the below command to autocomplete OCI setup.

```
oci setup autocomplete
```

### **STEP 4: Interacting with Oracle Autonomous Database**

Now that you have setup OCI CLI, let us now look at examples of using Autonomous Transaction Processing Database. 

#### Creating Database

Open your command line interface and run the following command to create an Autonomous Transaction Processing Database

```
oci db autonomous-database create --admin-password [password] --compartment-id [OCID] --cpu-core-count [integer] --data-storage-size-in-tbs [integer] --db-name [Database Name]
```

For example:

```
oci db autonomous-database create --admin-password "WElcome_123#" -c ocid1.compartment.oc1..aaaaaaaahnmqede4hg2sdom74lpljjwyu6nc6o2jr77rc5wagez3cwutu57a --cpu-core-count 1 --data-storage-size-in-tbs 1 --db-name "TejusDB"
```

You are expected to see the following output in the command line interface

![](./images/900/CreateDBOutput.png)

#### Get Database

Open your command line interface and run the following command to get details of an Autonomous Transaction Processing Database

```
oci db autonomous-database get --autonomous-database-id [OCID]
```

For Example:

```
oci db autonomous-database get --autonomous-database-id ocid1.autonomousdatabase.oc1.phx.abyhqljrbfftoc3spn4aepi32ihhlhesfwztsjpjkwz2cgppexf3ercpu7ja
```

You are expected to see the following output in the command line interface

![](./images/900/GetDBOutput.png)

#### Listing Database

Open your command line interface and run the following command to List all Autonomous Transaction Processing Database

```
oci db autonomous-database list --compartment-id [OCID]
```

For example:

```
oci db autonomous-database list -c ocid1.compartment.oc1..aaaaaaaahnmqede4hg2sdom74lpljjwyu6nc6o2jr77rc5wagez3cwutu57a
```

You are expected to see the following output in the command line interface

![](./images/900/ListDBOutput.png)

#### Deleting Database

Open your command line interface and run the following command to delete an Autonomous Transaction Processing Database

```
 oci db autonomous-database delete --autonomous-database-id [OCID]
```

For example:

```
oci db autonomous-database delete --autonomous-database-id ocid1.autonomousdatabase.oc1.phx.abyhqljrbfftoc3spn4aepi32ihhlhesfwztsjpjkwz2cgppexf3ercpu7ja
```

You are expected to see the following output in the command line interface.

You will be asked **Are you sure you want to delete this resource? [y/N]** type Y to comfirm.

![](./images/900/DeleteDBOutput.png)

Login to OCI console and naviagte to Autonomous Transaction Processing Database from Menu and confirm that the database is **Terminating**.

![](./images/900/TerminateDBOutput.png)


#### Bonus Step: In similar way you can try the follwing examples

#### Restore Databse 

Open your command line interface and run the following command to Restore Autonomous Transaction Processing Database

```
oci db autonomous-database restore --autonomous-database-id [OCID] --timestamp [datetime]
```

#### Start Database

Open your command line interface and run the following command to Start Autonomous Transaction Processing Database

```
oci db autonomous-database start --autonomous-database-id [OCID]
```

#### Stop Database

Open your command line interface and run the following command to Stop Autonomous Transaction Processing Database

```
oci db autonomous-database stop --autonomous-database-id [OCID]
```

#### Update Database

```
oci db autonomous-database update --autonomous-database-id [OCID] --cpu-core-count [integer]
```

For further examples on how to work with OCI CLI with different services please refer to Oracle documentation [here](https://docs.cloud.oracle.com/iaas/tools/oci-cli/latest/oci_cli_docs/cmdref/db.html).


You have successfully configured Oracle Cloud Infrastructure Command Line Interface and ran examples on Autonomous Transaction Processing Database.

-   You are now ready to move to the next lab.

<table>
<tr><td class="td-logo">[![](images/obe_tag.png)](#)</td>
<td class="td-banner">
## Great Work - All Done!
</td>
</tr>
<table>