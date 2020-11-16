# Try out Azure Functions (C#)

Develop in .NET Core 3.1, includes minimal required set up to get started with dependency injection. In case you were wondering, this `.devcontainer` is:

- Based on `azure-functions-dotnetcore-3.1` development container found in [@microsoft/vscode-dev-containers][devcontainers-repo]
- Ideal for serverless microservices development with Azure Functions in .NET Core 3.1, and
- Include Azure Storage support for local development using Azurite emulator.

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

## Configuration Options

- [The VS Code Remote - Containers docs][vscode-remote-docs] is a good source to learn more about `.devcontainer.json` configuration options and its usage.
- [See .NET Core CLI page][dotnet-core-cli-docs] to learn the full-blown `dotnet` options.

[devcontainers-repo]: https://github.com/microsoft/vscode-dev-containers
[dotnet-sdk-docker-image]: https://hub.docker.com/_/microsoft-dotnet-sdk/
[azure-cli-docs]: https://docs.microsoft.com/en-us/cli/azure/get-started-with-azure-cli
[node-js-docs]: https://nodejs.dev/learn
[vscode-remote-docs]: https://code.visualstudio.com/docs/remote/containers
[dotnet-core-cli-docs]: https://docs.microsoft.com/en-us/dotnet/core/tools/