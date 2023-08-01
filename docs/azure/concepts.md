
## Private endpoint
A `private endpoint` is a network interface that uses a private IP address from your virtual network. This network interface connects you privately and securely to a service that's powered by `Azure Private Link`. By enabling a private endpoint, you're bringing the service into your virtual network.

The service could be an Azure service such as:
    - Azure Storage
    - Azure Cosmos DB
    - Azure SQL Database


##  SPN Auth
- A `service principal name` (SPN) is a unique identifier of a service instance. SPNs are used by `Kerberos authentication` to associate a service instance with a service logon account.
- This allows a client application to request that the service authenticate an account even if the client does not have the account name.
- If you install multiple instances of a service on computers throughout a forest, each instance must have its own SPN. A given service instance can have multiple SPNs if there are multiple names that clients might use for authentication.
    

!!! tip "Did you registered your SPN?"
    Before the `Kerberos authentication service` can use an SPN to authenticate a service, the SPN must be registered on the account object that the service instance uses to log on. ==A given SPN can be registered on only one account== 


## SAS URI

SAS is a secure way to grant limited access to the resources in your storage account to the external world (clients, apps), without compromising your account keys. Shared Access Signature (SAS) is used for controlling access to blob, file, table, and queue storage containers. 


!!! warning "Never share the access key"
    You would not want to share an access key since it is like a root password to all the containers existing within the Azure Storage account.A shared access signature (SAS) provides secure delegated access to resources in your storage account.

It gives you the granular control over the type of access you grant to clients, which includes -

- **Interval** – You can specify how long the SAS token should be valid by mentioning the start time and the expiry time.
- **Permission** – You can specify the permission at the granular level, for example, your clients just want to read the blob so grant them only read permission.
- **IP Address** – If you want `Azure Storage Account` to be accessed from a particular IP or range of IPs then you can specify an optional IP Address or range of IP addresses in your `SAS token`.
- **Protocol** – If you want Azure Storage account to be accessed by either `HTTPS` or `HTTP & HTTPS`, you can specify the same in the SAS token.

### Types of shared access signatures
Azure Storage supports three types of `shared access signatures` as shown below:

#### User delegation SAS (Recommended)
A user delegation SAS is secured with Azure Active Directory (Azure AD) credentials and also by the permissions specified for the SAS. ==A user delegation SAS applies to Blob storage only.==

!!! remember "Recommended approach"
    A user delegation SAS provides superior security to a service SAS or an account SAS. A user delegation SAS is secured with Azure AD credentials, so that you do not need to store your account key with your code.

#### Service SAS
A service SAS is secured with the `storage account key`. A service SAS delegates access to a resource in only one of the Azure Storage services:

- `Blob` 
- `Queue`
- `Table`
- `Files`

#### Account SAS
An account SAS is secured with the `storage account key`. An account SAS delegates access to resources in one or more of the storage services. All of the operations available via a service or user delegation SAS are also available via an account SAS.

You can also delegate access to the following:

- Service-level operations (For example, the Get/Set Service Properties and Get Service Stats operations).
- Read, write, and delete operations that aren't permitted with a service SAS.

!!! warning "Do you have access to Account Key?" 
    Both a service SAS and an account SAS are signed with the storage account key. To create a SAS that is signed with the account key, an application must have access to the account key.


### SAS token

!!! question "What is SAS Token?"
    The SAS token is a string that you generate on the client side, for example by using one of the Azure Storage client libraries. The SAS token is not tracked by Azure Storage in any way. You can create an unlimited number of SAS tokens on the client side. After you create a SAS, you can distribute it to client applications that require access to resources in your storage account.

Client applications provide the SAS URI to Azure Storage as part of a request. Then, the service checks the SAS parameters and the signature to verify that it is valid. If the service verifies that the signature is valid, then the request is authorized. Otherwise, the request is declined with error code 403 (Forbidden).

<center> <img src="../images/Demystifying_SAS_Token.png" width="90%"> </center>

