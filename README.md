# JavaScript on Azure Learn Path - Module 2 - Deploying a basic app to Azure

This Learn module requires the following Azure resources to deploy correctly:

* Azure App Service
* Azure Cosmos DB with MongoDB API

## Requirements

- Node.js LTS

## Local development

- Create Azure resources
    - Azure App Service  + Cosmos DB for MongoDB API
        - [Create resource](https://ms.portal.azure.com/#create/Microsoft.AppServiceWebAppDatabaseV3) in Azure portal
        - Create database
        - Create collection
        - Copy the following to the `.env` file:
            - Connection string
            - Database name
            - Collection name
    - Azure Storage (for images)
        - [Create resource](https://ms.portal.azure.com/#create/Microsoft.StorageAccount)
            - Make sure `Blob public access` is enabled
        - Create container
        - Copy the following to the `.env` file:
            - Connection string
            - Container name
- Install npm dependencies: `npm install`
- Verify environment variables are set in `.env`
    - PORT=8080 - default port for Azure App Service
    - MONGODB_URI=
    - MONGODB_URI_DATABASE_NAME=
    - MONGODB_URI_COLLECTION_NAME=
    - AZURE_STORAGE_BLOB_CONNECTIONSTRING=
    - AZURE_STORAGE_BLOB_CONTAINER_NAME=
- Start the server: `npm start`
- Access Web App at: `http://127.0.0.1:8080`

## Azure portal: Configure git to push to Azure App Service

1. In the Azure portal, for your web app, select **Deployment -> Deployment Center**.
1. On the **Settings** tab, copy the **Git Clone URI**. This will become your local git value for your remote named `Azure`.
1. On the **Local Git/FTPS credentials** tab, copy the **Username** and **Password** under the application scope. These credentials allow you to deploy _only_ to this web app.  

## Azure CLI: Configure git to push to Azure App Service

1. Create a user scope credential for the web app.

    ```azurecli
    az webapp deployment user set --user-name <username> --password <password>
    ```

1. After app is created, configure deployment from local git

    ```azurecli
    az webapp deployment source config-local-git --name <app-name> --resource-group <group-name>
    ```

    The output contains a URL like: https://<deployment-username>@<app-name>.scm.azurewebsites.net/<app-name>.git. Use this URL to deploy your app in the next step.

## Create local git remote to Azure App Service

1. In a local terminal window, change the directory to the root of your Git repository, and add a Git remote using the URL you got from your app. If your chosen method doesn't give you a URL, use https://<app-name>.scm.azurewebsites.net/<app-name>.git with your app name in <app-name>.

    ```bash
    git remote add azure <url>
    ```

1. Push to the Azure remote with:

    ```bash
    git push azure <branchname>
    ```

1. In the Git Credential Manager window, enter your user-scope or application-scope credentials, not your Azure sign-in credentials.

    If your Git remote URL already contains the username and password, you won't be prompted.

1. Review the output. You may see runtime-specific automation.

1. Browse to your cloud app to verify that the content is deployed:

    ```http
    http://<app-name>.azurewebsites.net
    ```
