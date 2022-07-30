# Azure Functions .NET (Isolated)
[<img align="right" alt="Azure Functions and .NET in isolated mode" width="128rem" src="https://raw.githubusercontent.com/Azure/azure-functions-core-tools/master/src/Azure.Functions.Cli/npm/assets/azure-functions-logo-color-raster.png" />][az-funcs-isolated-docs]

This template repo serves as a flavor of quick-starter to develop [Azure Functions (Isolated)][az-funcs-isolated-quickstart] and [.NET apps and services][aspnet-webapi-quickstart] in C#.

> If you already have a [dev container][gh-codespaces-quickstart], you can jump to the [Things to try](#things-to-try) section.

### What's in it:

- Azure Functions v4 and Core Tools latest binaries
  > [Learn more about isolated vs in-proc functions][az-funcs-implementations-docs]
- .NET 6.0 SDK and Runtime
- Azure CLI for publishing and managing cloud resources
- [GitHub Codespaces][gh-codespaces-docs] and [VS Code Remote - Containers][vscode-dev-containers-docs]
- [VS Code Extensions](/.devcontainer/devcontainer.json) for .NET and Azure-related work
- [VS Code Tasks](/.vscode/tasks.json) to build, launch, and run from source
- Git and GitHub CLI for versioning
- ZSH integrated Terminal for shell scripting
- Docker CLI with Compose v2

[az-funcs-isolated-doc]: https://
[az-funcs-isolated-quickstart]: https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-cli-csharp?tabs=azure-cli%2Cisolated-process
[aspnet-webapi-quickstart]: https://

[awesome-list-bun]: https://github.com/apvarun/awesome-bun#videos

[gh-codespaces-quickstart]: https://docs.github.com/en/codespaces/getting-started/quickstart
[gh-codespaces-docs]: https://docs.github.com/en/codespaces
[vscode-dev-containers-docs]: https://code.visualstudio.com/docs/remote/remote-overview

## Using This Template

Using this repo is easy as cloning the repo. Just click on [Use this template][gh-use-this] and you are good to go.

[gh-use-this]: https://github.com/kosalanuwan/vscode-remote-try-bun/generate

[az-funcs-docs]: https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-cli-csharp?tabs=azure-cli%2Cbrowser
[az-serverless-video-series]: https://www.youtube.com/playlist?list=PLlrxD0HtieHjU-gOB3ifnFaqikI2kGxUW
[az-funcs-implementations-docs]: https://docs.microsoft.com/en-us/azure/azure-functions/dotnet-isolated-process-guide#differences-with-net-class-library-functions
[azurite-docs]: https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azurite#install-and-run-the-azurite-docker-image
[vscode-tasks]: .vscode/tasks.json

## Build and Run
With VS Code:
- `local.settings.json`: Change connection strings, create a [local settings file][az-funcs-docs-local-settings] if doesn't exists.
- `tasks.json`: Change the start up project path in `func start` task.
- Run task: `func start` to run the azure function in watch mode.

[az-funcs-docs-local-settings]: https://docs.microsoft.com/en-us/azure/azure-functions/functions-develop-vs-code?tabs=csharp#local-settings-file

### Debugging the source
VS Code is configured to prompt the processor to attach when debugging the code.
```json
// launch.json
"processId": "${command:pickProcess}"
```

### Connecting to local emulator
Replace the local connection string as below, [if the emulator is running locally][article-tip-connect-local-emulator]:
```json
// local.settings.json
"UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://host.docker.internal"
```

[article-tip-connect-local-emulator]: https://www.maneu.net/blog/use-local-storage-emulator-remote-container/

## License

Copyright :copyright: Kosala Nuwan Perera. All rights reserved.

The source code is license under the [MIT license][lic].

[lic]: ../LICENSE

## Useful Commands

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

## Configuration Options

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