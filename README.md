# Tryout Azure Functions .NET (Isolated)

[<img align="right" alt="Azure Functions and .NET in isolated mode" width="128rem" src="https://raw.githubusercontent.com/Azure/azure-functions-core-tools/master/src/Azure.Functions.Cli/npm/assets/azure-functions-logo-color-raster.png" />][az-funcs-isolated-quickstart]

This template repo serves as a flavor of quick-starter development container for use with [VS Code Remote - Containers][vscode-dev-containers-quickstart] and [GitHub Codespaces][gh-codespaces-quickstart].

> Originally, this dev container was created to tryout cloud native apps and services development using [Azure Functions (Isolated)][az-funcs-isolated-quickstart] and [.NET apps and services][dotnet-quickstart] without having to install locally.

[az-funcs-isolated-quickstart]: https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-cli-csharp?tabs=azure-cli%2Cisolated-process
[vscode-dev-containers-quickstart]: https://www.youtube.com/playlist?list=PLj6YeMhvp2S5G_X6ZyMc8gfXPMFPg3O31
[gh-codespaces-quickstart]: https://docs.github.com/en/codespaces/getting-started/quickstart
[dotnet-quickstart]: https://www.youtube.com/playlist?list=PLdo4fOcmZ0oUc2ShrReCS7KoBbPEONE0p



### What's in it:

- Azure Functions v4 and Core Tools latest binaries
- .NET 6.0 SDK and Runtime
- Azure CLI for publishing and managing cloud resources
- Kubernetes and Helm CLI for container orchestration
- [VS Code Extensions](/.devcontainer/devcontainer.json) for .NET and Azure-related work
- [VS Code Tasks](/.vscode/tasks.json) to build, launch, and debug from source
- [EditorConfig](/.editorconfig) for .NET and C# coding standards
- Git and GitHub CLI for versioning
- ZSH integrated Terminal
- Docker CLI with Compose v2



## Using This Template

If you are completely new to functions, [Awesome Functions - Isolated discussion][awesome-list-az-funcs-isolated] is a good source to start with.

Next, you want to create a copy of this template. It is easy as forking. The repo is marked as a `Template` so you will only have to [Use This Template][gh-use-this] and follow the instructions.

[awesome-list-az-funcs-isolated]: https://
[gh-use-this]: https://github.com/kosalanuwan/vscode-remote-try-azure-functions/generate



## Things to Try

First, you want to ensure source code is Reopened in Container. Then you'll be able to work with it like you would locally.

With VS Code:

1. In a terminal, run `func --version` to verify Azure Functions Core Tool are version 4.x.
2. Run `dotnet --list-sdks` to verify required versions are installed.
3. Run `az --version` to verify Azure CLI version is 2.4 or above.



### Create a functions project

Next, you would want to create a serverless app, say, a functions app `test-project` that response to an HTTP trigger.

With VS Code:

1. Run the `func init` command to create a functions project with specific runtime.

   ```bash
   func init test-project \
             --worker-runtime dotnet-isolated \
             --target-framework net6.0 \
             && cd test-project
   ```

2. Add a function to the project, say, `HttpExample` with HTTP trigger.

   ```bash
   func new -n HttpExample \
            -t "HTTP trigger" \
            --authlevel "anonymous"
   ```



### Build and run from source

VS Code is integrated with the Azure Functions Core Tools to run the functions app on the local development computer, in this case, its this dev container.

With VS Code:

1. Press `F5` to start the functions app project and call the function. The terminal displays the output from the Core Tools.
2. When the function executes locally, a notification is raised in VS Code to spin up your favorite browser.
3. Visit https://localhost:7071/api/httpexample
4. Press `Ctrl+C` to stop Core Tools and disconnect the debugger.



[storage-emulator-connect-vscode-remote]: https://www.maneu.net/blog/use-local-storage-emulator-remote-container/



### Publishing to Azure

Before publishing the functions app to Azure, you want to create supporting resources for the function.

1. Create an Azure account for free, if you haven't already.

2. Run `az login` to sign into your Azure account, if you haven't already.

3. Create a resource group, a general pupose storage account, and a functions app in Azure.

4. When the resources are ready, deploy the functions app to Azure.

   ```bash
   # Publish using Zip deployment
   dotnet build --configuration Release
   dotnet publish --configuration Release --output .publish
   # az functionapp deployment source config-zip -g <resource-group-name> -n <functionapp-name> --src .publish/drop.zip
   az functionapp deployment source config-zip -g az-funcs-sandbox -n vscode-remote-try-azure-functions --src .publish/drop.zip
   ```



[ci-azure-pipelines-docs]: https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-azure-devops?tabs=csharp



## Feedback

If you have any technical problems with GitHub Codespaces or dev containers, you are better off asking [VS Code Support][feedback-channels] directly, since you'll end up getting a much faster response back that way.

[feedback-channels]: https://github.com/microsoft/vscode-dev-containers#contributing-and-feedback



## Contributing

The official repo to contribute would be [@microsoft/vscode-dev-containers][contrib-official-repo].

Have a suggestion or a bug fix? Just open a pull request or an issue. Include the development container with clear and simplest instructions possible.

[contrib-official-repo]: https://github.com/microsoft/vscode-dev-containers#readme



## License

Copyright (c) Kosala Nuwan Perera. All rights reserved.

The source code is license under the [MIT license](LICENSE).