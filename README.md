# CodeSigningDemo
Skeleton for demonstrating use of the Sign CLI tool

## Azure Setup

You'll need to create a ServicePrincipal in Azure and grant certificate `get` certificate and key `sign` permissions. For GitHub Actions, use of OIDC authentication is recommended, to remove use of authentication secrets.

- [GitHub Actions Azure OIDC configuration](https://learn.microsoft.com/en-us/azure/developer/github/connect-from-azure?tabs=azure-portal%2Cwindows#use-the-azure-login-action-with-openid-connect)
- [Create a ServicePrincipal using the Azure portal](https://learn.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#assign-the-application-to-a-role)

Note that you do not need to assign any subscription-level roles to this identity. Only access to Key Vault is required.

## Build Variables
The following variables are used by the signing build:
- `Tenant Id` Azure AD tenant
- `Client Id` / `Application Id` ServicePrincipal identifier
- `Key Vault Url` Url to Key Vault. Must be a Premium Sku for EV code signing certificates and all certificates issued after June 2023
- `Certificate Id` Id of the certificate in Key Vault. 
- `Client Secret` for Azure DevOps Pipelines
- `Subscription Id` for GitHub Actions

### Azure DevOpps Pipelines

The `azure-pipelines.yml` shows how you can use a multi-stage build with code signing for Azure DevOps

### GitHub Actions

The `.github/workflows/build-and-sign.yml` contains a multi-job build 
