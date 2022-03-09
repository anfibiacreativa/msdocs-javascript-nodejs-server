## Requirements

- Node.js LTS and npm
- Create Azure resources
    - Azure App Service  + Cosmos DB for MongoDB API
        - [Create resource](https://ms.portal.azure.com/#create/Microsoft.AppServiceWebAppDatabaseV3) in Azure portal
        - Create database
        - Create collection
        - Make a copy of the `.env.example` file and rename it to `.env`
        - Copy the following information to the `.env` file:
            - Connection string. (This [link](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb/connect-mongodb-account#get-the-mongodb-connection-string-by-using-the-quick-start) explains you how to retrieve the connection string from the portal.)
            - Database name
            - Collection name
    - Azure Storage (for images)
        - [Create resource](https://ms.portal.azure.com/#create/Microsoft.StorageAccount)
            - Make sure `Blob public access` is enabled
        - Create container
        - Copy the following to the `.env` file:
            - Connection string (This [link](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal) explains you how to retrieve the connection string, from the portal.)
            - Container name
    - Azure Web App
        - [Create resource](https://ms.portal.azure.com/#create/Microsoft.WebSite)

## Local development

- Fork and checkout this repository
- Install npm dependencies running `npm install`
- Verify environment variables are set in `.env`
    - PORT=8080 - default port for Azure App Service. If you need to change the port, you can do it in `.env` file, changing the value for PORT.
    - MONGODB_URI=
    - MONGODB_URI_DATABASE_NAME=
    - MONGODB_URI_COLLECTION_NAME=
    - AZURE_STORAGE_BLOB_CONNECTIONSTRING=
    - AZURE_STORAGE_BLOB_CONTAINER_NAME=
- Start the server: `npm start`
- Access Web App at: `http://localhost:8080`, or the assigned port

## Configure git to push to Azure App Service using the Azure Portal

- Go to the Web App overview in the Azure portal and select **Deployment -> Deployment Center** from the side menu.
- Follow the configuration steps to link to your GitHub account and select your repository fork

This will generate the workflow file and push it to your repository. Once the workflow file is automatically pushed upstream, CI/CD will be enabled. Everytime you push to the selected branch, a new build and deploy process will start.


