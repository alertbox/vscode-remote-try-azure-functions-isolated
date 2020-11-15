```bash
func init Greeter --dotnet && cd Greeter
func new -t "HTTP trigger" -n Hello --authlevel "anonymous"
func new -t "HTTP trigger" -n Goodbye --authlevel "anonymous"
//
dotnet add package Microsoft.Azure.Functions.Extensions Microsoft.Extensions.Http
//
func host start --useHttps
```