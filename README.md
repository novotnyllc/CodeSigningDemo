# Sign CLI CI sample workflows

Code signing is a complex process that may involve multiple signing formats and artifact types. Some artifacts are containers that contain other signable file types. For example, NuGet Packages (`.nupkg`) frequently contain `.dll` files. The signing tool will sign all files inside-out, starting with the most nested files and then the outer files, ensuring everything is signed in the correct order.

Signing `.exe`/`.dll` files, and other Authenticode file types is only possible on Windows at this time. The recommended solution is to use a multi-stage/job build where the signing steps run on Windows. Running code signing on a separate stage to ensure secrets aren't exposed to the build stage.

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

### Azure DevOps Pipelines

The `azure-pipelines.yml` shows how you can use a multi-stage build with code signing for Azure DevOps

### GitHub Actions

The `.github/workflows/build-and-sign.yml` contains a multi-job build 
