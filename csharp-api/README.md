# c-sharp-api

## File Structure

```text
c-sharp-api/
├── .dockerignore
├── .vscode/
│   ├── launch.json
│   └── tasks.json
├── appsettings.Development.json
├── appsettings.json
├── bin/
│   └── Debug/
├── c-sharp-api.csproj
├── c-sharp-api.http
├── Dockerfile
├── obj/
│   ├── c-sharp-api.csproj.nuget.dgspec.json
│   ├── c-sharp-api.csproj.nuget.g.props
│   ├── c-sharp-api.csproj.nuget.g.targets
│   ├── Debug/
│   ├── project.assets.json
│   └── project.nuget.cache
├── Program.cs
├── Properties/
│   └── launchSettings.json
└── README.md
```

## Windows POST caveat (Kubernetes ingress)

When testing through host-based ingress (for example `csharp-api.localhost`), command behavior differs between `curl.exe` and PowerShell cmdlets on Windows.

- `curl.exe` can call `http://csharp-api.localhost:8080`, but use `--%` so JSON is passed unchanged.
- `Invoke-RestMethod` may fail to resolve `csharp-api.localhost`; use `http://localhost:8080` and send the ingress host in the `Host` header.

### `curl.exe` example

```powershell
curl.exe --% -i http://csharp-api.localhost:8080/besttimetobyorsellstock -H "Content-Type: application/json" -d "{\"prices\":[7,1,5,3,6,4]}"
```

### `Invoke-RestMethod` example

```powershell
Invoke-RestMethod -Method Post -Uri "http://localhost:8080/besttimetobyorsellstock" -Headers @{ Host = "csharp-api.localhost" } -ContentType "application/json" -Body '{"prices":[7,1,5,3,6,4]}'
```

Expected response body for both commands: `5`
