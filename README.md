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

- Open a new Terminal
- Type `az --version` to verify which version is been installed and the Azure CLI works
- Type `func --version` to verify which version is been installed and the  Functions Core Tools work
- Type `dotnet --version` to verify which version is been installed and the `dotnet` CLI works



### Useful Commands

```bash
# Create function apps
func init Greeter --dotnet && cd Greeter
func new -t "HTTP trigger" -n Hello --authlevel "anonymous"
func new -t "HTTP trigger" -n Goodbye --authlevel "anonymous"
```

```bash
# Add dependencies
dotnet add package Microsoft.Azure.Functions.Extensions 
dotnet add package Microsoft.Extensions.Http -v 3.1.10
```

```bash
dotnet new sln -n Greeter
dotnet sln add Greeter/
```

```bash
# Build and run locally
func host start --useHttps
```

```bash
# Publish using Zip deployment
dotnet build --configuration Release
dotnet publish --configuration Release --output .publish
# az functionapp deployment source config-zip -g <resource-group-name> -n <functionapp-name> --src .publish/drop.zip
az functionapp deployment source config-zip -g az-funcs-sandbox -n vscode-remote-try-azure-functions --src .publish/drop.zip
```



### Configuration Options

- [The VS Code Remote - Containers docs][vscode-remote-docs] is a good source to learn more about `.devcontainer.json` configuration options and its usage.
- [See .NET Core CLI page][dotnet-core-cli-docs] to learn the full-blown `dotnet` options.
- [Use local Azure Storage emulator in Remote Containers.][storage-emulator-connect-vscode-remote]
- [See continuous delivery by using Azure DevOps][ci-azure-pipelines-docs] page to learn the YAML scripts.

[devcontainers-repo]: https://github.com/microsoft/vscode-dev-containers
[dotnet-sdk-docker-image]: https://hub.docker.com/_/microsoft-dotnet-sdk/
[azure-cli-docs]: https://docs.microsoft.com/en-us/cli/azure/get-started-with-azure-cli
[node-js-docs]: https://nodejs.dev/learn
[vscode-remote-docs]: https://code.visualstudio.com/docs/remote/containers
[dotnet-core-cli-docs]: https://docs.microsoft.com/en-us/dotnet/core/tools/
[storage-emulator-connect-vscode-remote]: https://www.maneu.net/blog/use-local-storage-emulator-remote-container/
[ci-azure-pipelines-docs]: https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-azure-devops?tabs=csharp



### Connecting to local emulator

Replace the local connection string as below, [if the azurite emulator is running locally][article-tip-connect-local-emulator]:

```json
// local.settings.json
"UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://host.docker.internal"
```

[article-tip-connect-local-emulator]: https://www.maneu.net/blog/use-local-storage-emulator-remote-container/



## License

Copyright (c) Kosala Nuwan Perera. All rights reserved.

The source code is license under the [MIT license][LICENSE].