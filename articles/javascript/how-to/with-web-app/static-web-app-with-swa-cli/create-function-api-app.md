---
title: "5-API: Create Function API"
description: Create an Azure Function API for your React app. The Azure Function service provides serverless APIs. This allows you to focus on your TypeScript code and _not_ have to configure a full back-end web server.
ms.topic: how-to
ms.date: 10/18/2021
ms.custom: devx-track-js
#intent: Create Express.js web app with easy auth configured. 
---

# 5. Create your Azure Function API

Create an Azure Function API for your React app. The Azure Function service provides serverless APIs. This allows you to focus on your TypeScript code and _not_ have to configure a full back-end web server. 

### Create an Azure Function app

1. In the root of the project, create a Function app in a directory named `api`:

    ```bash
    func init api --typescript
    ```

1. Move into the `api` directory to create an API endpoint:

    ```bash
    cd api
    ```

1. Create an http trigger API and its associated files:

    ```bash 
    func new --name hello --template "HTTP trigger" --authlevel "anonymous" 
    ```

    |Setting|Description|
    |--|--|
    |`--name hello`|Creates an API with a route of `/api/hello`|
    |`--template "HTTP trigger"`|The API is triggered by HTTP requests. Other template types allow triggering from other Azure Service integrations.|
    |`--authlevel "anonymous"`|All requests to this API are allowed.|

1. Install dependencies for the Azure Function API:

    ```bash
    npm install 
    ```

## Change the Function API to return JSON

Open the `./api/hello/index.ts` file and replace all the contents with the following so that the function returns a JSON object:
   
:::code language="TypeScript" source="~/../js-e2e-static-web-app-with-cli-1-basic-app-with-api/api/hello/index.ts" highlight="12-15":::  

## Start the Azure Function app

Start the Azure function API:

```bash 
npm start
```

## Use the Function API in the browser

1. Query the API in a browser with the following URL:

    ```bash
    http://localhost:7071/api/hello?name=joesmith
    ```

1. The web browser returns the following successful message. 

    ```json
    {
      "input": "joesmith",
      "message": "Hello, joesmith. This HTTP triggered function executed successfully."
    }
    ```

## Stop the local Function app

Stop the local Azure Function runtime in the terminal with <kbd>Ctrl</kbd> + <kbd>c</kbd>.

## Commit API changes to source control

1. Check the new API code into your repo and push to the remote:
   
   ```bash
   git add . && git commit -m "hello api" && git push origin main
   ```

## Verify your GitHub Action build

1. In a web browser, go back to your GitHub repo, and make sure the next build of your Action succeeds with these new changes. The actions URL should look like:

    ```HTTP
    https://github.com/YOUR-ACCOUNT/staticwebapp-with-api/actions
    ```
   
    View the **Build and Deploy Job** to find the API successfully deployed:

    ```text
    Function Runtime Information. OS: Linux, Functions Runtime: v3, Node version: 12.X
    Finished building function app with Oryx
    Zipping Api Artifacts
    Done Zipping Api Artifacts
    Zipping App Artifacts
    Done Zipping App Artifacts
    Uploading build artifacts.
    Finished Upload. Polling on deployment.
    Status: InProgress. Time: 0.1977171(s)
    Status: InProgress. Time: 15.3964651(s)
    Status: Succeeded. Time: 31.3050572(s)
    Deployment Complete :)
    Visit your site at: https://purple-field-12345678.azurestaticapps.net
    Thanks for using Azure Static Web Apps!
    Exiting
    ```

1. In VS Code, verify the successful build pushed to your Azure Static Web Apps resource. Look at the functions node in your Azure explorer for Static Web Apps. 

   :::image type="content" source="../../../media/static-web-app-with-swa-cli/visual-studio-code-azure-explorer-function-list.png" alt-text="Partial screenshot of VS Code displaying Azure Explorer's Static Web Apps `functions` node with `hello` displayed.":::

    You may need to refresh using the Azure explorer's Static Web app bar in VS Code.

   :::image type="content" source="../../../media/static-web-app-with-swa-cli/visual-studio-code-swa-refresh.png" alt-text="Partial screenshot of VS Code displaying Azure Explorer's Static Web Apps command bar with the refresh icon highlighted.":::

1. In the bash terminal, move back to the root of the project:

    ```bash 
    cd ..
    ```


## Next steps

* [Connect React app to Function API](connect-client-to-api.md)