# c-sharp-api-demo

## NuGet source configuration

This workspace includes [NuGet.Config](NuGet.Config) with a cleared source list and a single `nuget.org` feed:

- `https://api.nuget.org/v3/index.json`

This avoids package resolution issues in the C# language server and ensures consistent restore behavior across environments.