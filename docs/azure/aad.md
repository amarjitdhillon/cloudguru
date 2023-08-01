# Auzre Active Directory

## What is Azure AD tenant?
An Azure AD tenant is a reserved Azure AD service instance that an organization receives and owns once it signs up for a Microsoft cloud service such as Azure, Microsoft Intune, or Microsoft 365.

!!! remember
    Each tenant represents an organization, and is distinct and separate from other Azure AD tenants.

## SCP (Service Connection Point)
The Active Directory Schema defines a `serviceConnectionPoint (SCP)` object class to make it easy for a service to publish service-specific data in the directory. Clients of the service use the data in an SCP to locate, connect to, and authenticate an instance of your service.


## Service Principal
An `Azure service principal` is an identity created for use with applications, hosted services, and automated tools to access Azure resources. This access is restricted by the `roles` assigned to the service principal, giving you control over which resources can be accessed and at which level.


!!! info ""
    For security reasons, it's always recommended to use service principals with automated tools rather than allowing them to log in with a user identity.

There are two types of authentication available for service principals: 

1. Password-based authentication
2. Certificate-based authentication.

## SP VS Managed Identity

???+ quote "SP and Managed Identity"
    The difference between managed identities and service principals is subtle. ==Service principals are no longer recommended for services that support managed identities. Managed identities are effectively “managed service principals” and remove the need for storing credentials in the application’s configuration and instead inject certificates into the resource that the managed identity is created into.==
