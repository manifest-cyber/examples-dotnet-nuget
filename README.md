# SBOM Generation for C#/.NET

## Overview

SBOM generation has become essential for detecting vulnerabilities, ensuring compliance, and addressing license issues. Although it may seem straightforward, the quality of results varies based on ecosystems, generators, formats, and specific project files.

By utilizing this repository, a fork from [unosquare/embedio](https://github.com/unosquare/embedio/tree/master), which is an open-source C#/.NET library, we aim to demonstrate different outputs and guide you through the SBOM generation process and its expected results. This will assist you in reproducing the process in your own projects with Manifest.

<aside>
⚠️ This repository assumes the use of NuGet. .NET Core codebases should function the same. However, different output and supported features are expected.

</aside>

## Prerequisites

- Install Manifest CLI by following the [installation guide](https://github.com/manifest-cyber/cli).
- **dotnet** and **nuget** are installed and configured
- The [global packages cache folder](https://learn.microsoft.com/en-us/nuget/consume-packages/managing-the-global-packages-and-cache-folders) is configured to defaults; if not, the NUGET_PACKAGES environment variable is set accordingly.
- (optional) Node, NPM installed (**cdxgen** only)

## Generate

In this example, we would compare the results of **syft**, **trivy,** and **cdxgen** to **sbom-tool,** which is currently not supported by **manifest-cli.**

### Installing Generators

The **manifest-cli** cannot function without the proper installation of the underlying generators. Fortunately, you can install them using the following command.

```bash
manifest-cli install -g cdxgen
manifest-cli install -g syft
manifest-cli install -g trivy
```

<aside>
💡 For more information on the ***install*** command, use `manifest-cli install --help` , It may be required to use `sudo` to install generators under `/usr/local/bin/`

</aside>

For **sbom-tool** installation guide, follow the the [official documentation](https://github.com/microsoft/sbom-tool)

### Project files

.NET projects have different configurations, some use `.sln` , some `.csproj` or `.vsproj` , others includes `*Packages.props` or `packages.config` .

### Generation with Manifest

The example project uses a mix of those, lets attempt to generate an SBOM and compare the results.

**Syft**

```tsx
manifest-cli sbom --name=embedio --version=0.0.0-dev --generator=syft -f test-syft.json .
```

The output should look like this:

```tsx
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "version": 1,
  "metadata": {
    "tools": {
      "components": [
        {
          "type": "application",
          "author": "anchore",
          "name": "syft",
          "version": "1.3.0"
        }
      ]
    },
    "component": {
      "bom-ref": "embedio@0.0.0-dev",
      "type": "application",
      "name": "embedio",
      "version": "0.0.0-dev"
    }
  },
  "components": [
    {
      "bom-ref": ".@:af63bd4c8601b7f1",
      "type": "file",
      "name": ".",
      "components": [
        {
          "bom-ref": ".@:pkg:github/actions/cache@v1?package-id=ced8e658a04afb49",
          "type": "library",
          "name": "actions/cache",
          "version": "v1",
          "cpe": "cpe:2.3:a:actions\\/cache:actions\\/cache:v1:*:*:*:*:*:*:*",
          "purl": "pkg:github/actions/cache@v1",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "github-actions-usage-cataloger"
            },
            {
              "name": "syft:package:type",
              "value": "github-action"
            },
            {
              "name": "syft:location:0:path",
              "value": "/.github/workflows/build.yml"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:github/actions/checkout@v2?package-id=be19ea402c8c3b52",
          "type": "library",
          "name": "actions/checkout",
          "version": "v2",
          "cpe": "cpe:2.3:a:actions\\/checkout:actions\\/checkout:v2:*:*:*:*:*:*:*",
          "purl": "pkg:github/actions/checkout@v2",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "github-actions-usage-cataloger"
            },
            {
              "name": "syft:package:type",
              "value": "github-action"
            },
            {
              "name": "syft:location:0:path",
              "value": "/.github/workflows/build.yml"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:github/actions/checkout@v3?package-id=202b85b09304779e",
          "type": "library",
          "name": "actions/checkout",
          "version": "v3",
          "cpe": "cpe:2.3:a:actions\\/checkout:actions\\/checkout:v3:*:*:*:*:*:*:*",
          "purl": "pkg:github/actions/checkout@v3",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "github-actions-usage-cataloger"
            },
            {
              "name": "syft:package:type",
              "value": "github-action"
            },
            {
              "name": "syft:location:0:path",
              "value": "/.github/workflows/codeql.yml"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:github/actions/setup-java@v1?package-id=bc90e91ad7a30dfb",
          "type": "library",
          "name": "actions/setup-java",
          "version": "v1",
          "cpe": "cpe:2.3:a:actions\\/setup-java:actions\\/setup-java:v1:*:*:*:*:*:*:*",
          "purl": "pkg:github/actions/setup-java@v1",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "github-actions-usage-cataloger"
            },
            {
              "name": "syft:package:type",
              "value": "github-action"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:actions\\/setup-java:actions\\/setup_java:v1:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:actions\\/setup_java:actions\\/setup-java:v1:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:actions\\/setup_java:actions\\/setup_java:v1:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:actions\\/setup:actions\\/setup-java:v1:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:actions\\/setup:actions\\/setup_java:v1:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:location:0:path",
              "value": "/.github/workflows/build.yml"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:github/github/codeql-action@v2?package-id=63a750ee7527399f#analyze",
          "type": "library",
          "name": "github/codeql-action/analyze",
          "version": "v2",
          "cpe": "cpe:2.3:a:github\\/codeql-action\\/analyze:github\\/codeql-action\\/analyze:v2:*:*:*:*:*:*:*",
          "purl": "pkg:github/github/codeql-action@v2#analyze",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "github-actions-usage-cataloger"
            },
            {
              "name": "syft:package:type",
              "value": "github-action"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql-action\\/analyze:github\\/codeql_action\\/analyze:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql_action\\/analyze:github\\/codeql-action\\/analyze:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql_action\\/analyze:github\\/codeql_action\\/analyze:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql:github\\/codeql-action\\/analyze:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql:github\\/codeql_action\\/analyze:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:location:0:path",
              "value": "/.github/workflows/codeql.yml"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:github/github/codeql-action@v2?package-id=272c907fc4f3286a#autobuild",
          "type": "library",
          "name": "github/codeql-action/autobuild",
          "version": "v2",
          "cpe": "cpe:2.3:a:github\\/codeql-action\\/autobuild:github\\/codeql-action\\/autobuild:v2:*:*:*:*:*:*:*",
          "purl": "pkg:github/github/codeql-action@v2#autobuild",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "github-actions-usage-cataloger"
            },
            {
              "name": "syft:package:type",
              "value": "github-action"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql-action\\/autobuild:github\\/codeql_action\\/autobuild:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql_action\\/autobuild:github\\/codeql-action\\/autobuild:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql_action\\/autobuild:github\\/codeql_action\\/autobuild:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql:github\\/codeql-action\\/autobuild:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql:github\\/codeql_action\\/autobuild:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:location:0:path",
              "value": "/.github/workflows/codeql.yml"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:github/github/codeql-action@v2?package-id=50a9488b839dcc33#init",
          "type": "library",
          "name": "github/codeql-action/init",
          "version": "v2",
          "cpe": "cpe:2.3:a:github\\/codeql-action\\/init:github\\/codeql-action\\/init:v2:*:*:*:*:*:*:*",
          "purl": "pkg:github/github/codeql-action@v2#init",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "github-actions-usage-cataloger"
            },
            {
              "name": "syft:package:type",
              "value": "github-action"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql-action\\/init:github\\/codeql_action\\/init:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql_action\\/init:github\\/codeql-action\\/init:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql_action\\/init:github\\/codeql_action\\/init:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql:github\\/codeql-action\\/init:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:cpe23",
              "value": "cpe:2.3:a:github\\/codeql:github\\/codeql_action\\/init:v2:*:*:*:*:*:*:*"
            },
            {
              "name": "syft:location:0:path",
              "value": "/.github/workflows/codeql.yml"
            }
          ]
        }
      ]
    }
  ],
  "dependencies": [
    {
      "ref": "embedio@0.0.0-dev",
      "dependsOn": [
        ".@:af63bd4c8601b7f1"
      ]
    }
  ]
}

```

At a quick glance, it seems like **syft** is unable to pick the project files, this means it completely disregards `.sln` files, by looking at source files it’s easy to see that **syft** supports `**/*.deps.json` , `.dll` and `.exe` only.

To generate the `*.deps.json` file for the project, we must build it first:

```tsx
dotnet build
```

Now rerun the generation command, the output would look far more complete.

For simplicity lets run the generator on a specific folder:

```tsx
manifest-cli sbom --name=embedio --version=0.0.0-dev --generator=syft -f test-syft.json src/EmbedIO
```

The output will now properly detect all dependencies:

```tsx
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "version": 1,
  "metadata": {
    "tools": {
      "components": [
        {
          "type": "application",
          "author": "anchore",
          "name": "syft",
          "version": "1.3.0"
        }
      ]
    },
    "component": {
      "bom-ref": "embedio@0.0.0-dev",
      "type": "application",
      "name": "embedio",
      "version": "0.0.0-dev"
    }
  },
  "components": [
    {
      "bom-ref": "src/EmbedIO@:7bdbe2307496f87f",
      "type": "file",
      "name": "src/EmbedIO",
      "components": [
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/EmbedIO@3.5.0?package-id=3320ecff22689a90",
          "type": "library",
          "name": "EmbedIO",
          "version": "3.5.0",
          "cpe": "cpe:2.3:a:EmbedIO:EmbedIO:3.5.0:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/EmbedIO@3.5.0",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-deps-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-deps-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.deps.json"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/EmbedIO@3.5.0.0?package-id=dcf4c470ea7cabd2",
          "type": "library",
          "name": "EmbedIO",
          "version": "3.5.0.0",
          "cpe": "cpe:2.3:a:EmbedIO:EmbedIO:3.5.0.0:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/EmbedIO@3.5.0.0",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-portable-executable-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-portable-executable-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.dll"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/EmbedIO@3.5.0.0?package-id=ee4417a844c37d70",
          "type": "library",
          "name": "EmbedIO",
          "version": "3.5.0.0",
          "cpe": "cpe:2.3:a:EmbedIO:EmbedIO:3.5.0.0:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/EmbedIO@3.5.0.0",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-portable-executable-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-portable-executable-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/obj/Debug/netstandard2.0/EmbedIO.dll"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2?package-id=8105633d94a2916b",
          "type": "library",
          "name": "Microsoft.CodeAnalysis.FxCopAnalyzers",
          "version": "3.3.2",
          "cpe": "cpe:2.3:a:Microsoft.CodeAnalysis.FxCopAnalyzers:Microsoft.CodeAnalysis.FxCopAnalyzers:3.3.2:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-deps-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-deps-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.deps.json"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2?package-id=a009b61091a0808e",
          "type": "library",
          "name": "Microsoft.CodeAnalysis.VersionCheckAnalyzer",
          "version": "3.3.2",
          "cpe": "cpe:2.3:a:Microsoft.CodeAnalysis.VersionCheckAnalyzer:Microsoft.CodeAnalysis.VersionCheckAnalyzer:3.3.2:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-deps-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-deps-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.deps.json"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2?package-id=2d9c26bc38f24100",
          "type": "library",
          "name": "Microsoft.CodeQuality.Analyzers",
          "version": "3.3.2",
          "cpe": "cpe:2.3:a:Microsoft.CodeQuality.Analyzers:Microsoft.CodeQuality.Analyzers:3.3.2:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-deps-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-deps-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.deps.json"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.NETCore.Platforms@1.1.0?package-id=40a8e4d253d070b1",
          "type": "library",
          "name": "Microsoft.NETCore.Platforms",
          "version": "1.1.0",
          "cpe": "cpe:2.3:a:Microsoft.NETCore.Platforms:Microsoft.NETCore.Platforms:1.1.0:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/Microsoft.NETCore.Platforms@1.1.0",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-deps-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-deps-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.deps.json"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2?package-id=068dcaf4da15ad50",
          "type": "library",
          "name": "Microsoft.NetCore.Analyzers",
          "version": "3.3.2",
          "cpe": "cpe:2.3:a:Microsoft.NetCore.Analyzers:Microsoft.NetCore.Analyzers:3.3.2:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-deps-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-deps-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.deps.json"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2?package-id=d66cd7a60af1df3c",
          "type": "library",
          "name": "Microsoft.NetFramework.Analyzers",
          "version": "3.3.2",
          "cpe": "cpe:2.3:a:Microsoft.NetFramework.Analyzers:Microsoft.NetFramework.Analyzers:3.3.2:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-deps-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-deps-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.deps.json"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/NETStandard.Library@2.0.3?package-id=cecc6fc254e4b656",
          "type": "library",
          "name": "NETStandard.Library",
          "version": "2.0.3",
          "cpe": "cpe:2.3:a:NETStandard.Library:NETStandard.Library:2.0.3:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/NETStandard.Library@2.0.3",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-deps-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-deps-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.deps.json"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Nullable@1.3.0?package-id=466ebfa4fd0562f7",
          "type": "library",
          "name": "Nullable",
          "version": "1.3.0",
          "cpe": "cpe:2.3:a:Nullable:Nullable:1.3.0:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/Nullable@1.3.0",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-deps-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-deps-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.deps.json"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/StyleCop.Analyzers@1.1.118?package-id=663957b502d509d9",
          "type": "library",
          "name": "StyleCop.Analyzers",
          "version": "1.1.118",
          "cpe": "cpe:2.3:a:StyleCop.Analyzers:StyleCop.Analyzers:1.1.118:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/StyleCop.Analyzers@1.1.118",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-deps-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-deps-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.deps.json"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/System.ValueTuple@4.5.0?package-id=ae2bc68cf106dabf",
          "type": "library",
          "name": "System.ValueTuple",
          "version": "4.5.0",
          "cpe": "cpe:2.3:a:System.ValueTuple:System.ValueTuple:4.5.0:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/System.ValueTuple@4.5.0",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-deps-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-deps-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.deps.json"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Unosquare.Swan.Lite@3.1.0?package-id=7ca23da7cf58a9e2",
          "type": "library",
          "name": "Unosquare.Swan.Lite",
          "version": "3.1.0",
          "cpe": "cpe:2.3:a:Unosquare.Swan.Lite:Unosquare.Swan.Lite:3.1.0:*:*:*:*:*:*:*",
          "purl": "pkg:nuget/Unosquare.Swan.Lite@3.1.0",
          "properties": [
            {
              "name": "syft:package:foundBy",
              "value": "dotnet-deps-cataloger"
            },
            {
              "name": "syft:package:language",
              "value": "dotnet"
            },
            {
              "name": "syft:package:type",
              "value": "dotnet"
            },
            {
              "name": "syft:package:metadataType",
              "value": "dotnet-deps-entry"
            },
            {
              "name": "syft:location:0:path",
              "value": "/bin/Debug/netstandard2.0/EmbedIO.deps.json"
            }
          ]
        }
      ]
    }
  ],
  "dependencies": [
    {
      "ref": "src/EmbedIO@:pkg:nuget/EmbedIO@3.5.0?package-id=3320ecff22689a90",
      "dependsOn": [
        "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2?package-id=8105633d94a2916b",
        "src/EmbedIO@:pkg:nuget/NETStandard.Library@2.0.3?package-id=cecc6fc254e4b656",
        "src/EmbedIO@:pkg:nuget/Nullable@1.3.0?package-id=466ebfa4fd0562f7",
        "src/EmbedIO@:pkg:nuget/StyleCop.Analyzers@1.1.118?package-id=663957b502d509d9",
        "src/EmbedIO@:pkg:nuget/Unosquare.Swan.Lite@3.1.0?package-id=7ca23da7cf58a9e2"
      ]
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2?package-id=8105633d94a2916b",
      "dependsOn": [
        "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2?package-id=a009b61091a0808e",
        "src/EmbedIO@:pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2?package-id=2d9c26bc38f24100",
        "src/EmbedIO@:pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2?package-id=068dcaf4da15ad50",
        "src/EmbedIO@:pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2?package-id=d66cd7a60af1df3c"
      ]
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/NETStandard.Library@2.0.3?package-id=cecc6fc254e4b656",
      "dependsOn": [
        "src/EmbedIO@:pkg:nuget/Microsoft.NETCore.Platforms@1.1.0?package-id=40a8e4d253d070b1"
      ]
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Unosquare.Swan.Lite@3.1.0?package-id=7ca23da7cf58a9e2",
      "dependsOn": [
        "src/EmbedIO@:pkg:nuget/System.ValueTuple@4.5.0?package-id=ae2bc68cf106dabf"
      ]
    },
    {
      "ref": "embedio@0.0.0-dev",
      "dependsOn": [
        "src/EmbedIO@:7bdbe2307496f87f"
      ]
    }
  ]
}
```

Unfortuatly, **syft** does not support licenses parsing, however, it is able to detect transitive dependencies, however, dev dependencies are detected since the nature of of `deps.json` works.

Notable remarks, **syft** generates CPEs which are valuable for vulnerabilities and license issues detections.

**Cdxgen**

```tsx
manifest-cli sbom --name=embedio --version=0.0.0-dev --generator=cdxgen -f test-cdxgen.json .
```

`.sln` files, alongside other files used as at this project, are supported. the full list extended to `.cproj` , `.fproj`, `.vcxproj` , `*.package.config` , `project.assets.json` and `*.nupkg`

In addition, a two notable lockfiles are supported `packages.lock.json` and `paket.lock` .

Since the SBOM itself is long, re-run on the src folder:

```tsx
manifest-cli sbom --name=embedio --version=0.0.0-dev --generator=cdxgen -f test-cdxgen.json src/EmbedIO
```

Output should look like:

```tsx
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "version": 1,
  "metadata": {
    "tools": {
      "components": [
        {
          "bom-ref": "pkg:npm/@cyclonedx/cdxgen@10.6.1",
          "type": "application",
          "author": "OWASP Foundation",
          "publisher": "OWASP Foundation",
          "group": "@cyclonedx",
          "name": "cdxgen",
          "version": "10.6.1",
          "purl": "pkg:npm/%40cyclonedx/cdxgen@10.6.1"
        }
      ]
    },
    "component": {
      "bom-ref": "embedio@dev",
      "type": "application",
      "name": "embedio",
      "version": "dev"
    }
  },
  "components": [
    {
      "bom-ref": "EmbedIO@latest:pkg:nuget/EmbedIO@latest",
      "type": "application",
      "name": "EmbedIO",
      "version": "latest",
      "purl": "pkg:nuget/EmbedIO@latest",
      "components": [
        {
          "bom-ref": "EmbedIO@latest:pkg:nuget/EmbedIO@3.5.0",
          "type": "application",
          "name": "EmbedIO",
          "version": "3.5.0",
          "purl": "pkg:nuget/EmbedIO@3.5.0"
        },
        {
          "bom-ref": "EmbedIO@latest:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.CodeAnalysis.FxCopAnalyzers",
          "version": "3.3.2",
          "hashes": [
            {
              "alg": "SHA-512",
              "content": "42568fd928299225797e70e00b55b01b76e57d722fcf95923e403f47f023291c0e2d3194d582c4dcf02b92f4f3d59b4b0ae5ecdbd429de26367e36bbc05d2212"
            }
          ],
          "purl": "pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
            },
            {
              "name": "PackageFiles",
              "value": ""
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 1,
              "methods": [
                {
                  "technique": "manifest-analysis",
                  "confidence": 1,
                  "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "EmbedIO@latest:pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
          "type": "library",
          "name": "Microsoft.CodeAnalysis.VersionCheckAnalyzer",
          "version": "3.3.2",
          "hashes": [
            {
              "alg": "SHA-512",
              "content": "293a9e5498c67f00d7eff0060e005712b617ffc12d8f0bbc660d938269a354f651795664e0a2efe5fa44893b680578acdc03be38cfd0bb87107f3f36f114a60d"
            }
          ],
          "purl": "pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
            },
            {
              "name": "PackageFiles",
              "value": "Microsoft.CodeAnalysis.VersionCheckAnalyzer.dll, Microsoft.CodeAnalysis.VersionCheckAnalyzer.resources.dll"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 1,
              "methods": [
                {
                  "technique": "manifest-analysis",
                  "confidence": 1,
                  "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "EmbedIO@latest:pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.CodeQuality.Analyzers",
          "version": "3.3.2",
          "hashes": [
            {
              "alg": "SHA-512",
              "content": "5b047de9a6e9a302ca089ffe85112e06ee7ccdb4c10a214b431e458c050062b82db8842c83e8d1b6fe27f602b0eb3c727673be8dde5a14907a1fe7aa1aa42e7f"
            }
          ],
          "purl": "pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
            },
            {
              "name": "PackageFiles",
              "value": "Humanizer.dll, Microsoft.CodeQuality.Analyzers.dll, Microsoft.CodeQuality.CSharp.Analyzers.dll, Microsoft.CodeQuality.Analyzers.resources.dll, Microsoft.CodeQuality.VisualBasic.Analyzers.dll"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 1,
              "methods": [
                {
                  "technique": "manifest-analysis",
                  "confidence": 1,
                  "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "EmbedIO@latest:pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.NetCore.Analyzers",
          "version": "3.3.2",
          "hashes": [
            {
              "alg": "SHA-512",
              "content": "2fd954d84f5268af339e7f1992cb4ec7c8e3a589ac053beddf1216e9bb4f33f162f26ef348af348ad1d5d29e9fdb7abce2ebf25d2f226c40a33f456b6bdf73b1"
            }
          ],
          "purl": "pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
            },
            {
              "name": "PackageFiles",
              "value": "Microsoft.NetCore.Analyzers.dll, Microsoft.NetCore.CSharp.Analyzers.dll, Microsoft.NetCore.Analyzers.resources.dll, Microsoft.NetCore.VisualBasic.Analyzers.dll"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 1,
              "methods": [
                {
                  "technique": "manifest-analysis",
                  "confidence": 1,
                  "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "EmbedIO@latest:pkg:nuget/Microsoft.NETCore.Platforms@1.1.0",
          "type": "library",
          "name": "Microsoft.NETCore.Platforms",
          "version": "1.1.0",
          "hashes": [
            {
              "alg": "SHA-512",
              "content": "933d0f116da586aca07a123f77a5ec3c24330fb7dfee050969518f5444d7eb5d5e69d1ac03703cefb19d4a55342d154c0931fff8fde8da20d36a4f92d3c576f8"
            }
          ],
          "purl": "pkg:nuget/Microsoft.NETCore.Platforms@1.1.0",
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
            },
            {
              "name": "PackageFiles",
              "value": ""
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 1,
              "methods": [
                {
                  "technique": "manifest-analysis",
                  "confidence": 1,
                  "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "EmbedIO@latest:pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.NetFramework.Analyzers",
          "version": "3.3.2",
          "hashes": [
            {
              "alg": "SHA-512",
              "content": "35f982f0da31ad1b70d8f4a6a92bbe9154dcb09b8c86ca7158a6d5cebb4fc70f8ef218e908fcc3d08b6d09425c9437f7eaa92649cbef775060447604d7bcc5f6"
            }
          ],
          "purl": "pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2",
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
            },
            {
              "name": "PackageFiles",
              "value": "Microsoft.NetFramework.Analyzers.dll, Microsoft.NetFramework.CSharp.Analyzers.dll, Microsoft.NetFramework.Analyzers.resources.dll, Microsoft.NetFramework.VisualBasic.Analyzers.dll"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 1,
              "methods": [
                {
                  "technique": "manifest-analysis",
                  "confidence": 1,
                  "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "EmbedIO@latest:pkg:nuget/NETStandard.Library@2.0.3",
          "type": "library",
          "name": "NETStandard.Library",
          "version": "2.0.3",
          "hashes": [
            {
              "alg": "SHA-512",
              "content": "b2de3b3e8b19487ae3102763788cd941bce2bd804916fe8fda7bf8723db2a5d236d380cefaf67b979ada18c897e1e5cc279dd17ce220fbfb380c7559e7836ed8"
            }
          ],
          "purl": "pkg:nuget/NETStandard.Library@2.0.3",
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
            },
            {
              "name": "PackageFiles",
              "value": "Microsoft.Win32.Primitives.dll, System.AppContext.dll, System.Collections.Concurrent.dll, System.Collections.NonGeneric.dll, System.Collections.Specialized.dll, System.Collections.dll, System.ComponentModel.Composition.dll, System.ComponentModel.EventBasedAsync.dll, System.ComponentModel.Primitives.dll, System.ComponentModel.TypeConverter.dll, System.ComponentModel.dll, System.Console.dll, System.Core.dll, System.Data.Common.dll, System.Data.dll, System.Diagnostics.Contracts.dll, System.Diagnostics.Debug.dll, System.Diagnostics.FileVersionInfo.dll, System.Diagnostics.Process.dll, System.Diagnostics.StackTrace.dll, System.Diagnostics.TextWriterTraceListener.dll, System.Diagnostics.Tools.dll, System.Diagnostics.TraceSource.dll, System.Diagnostics.Tracing.dll, System.Drawing.Primitives.dll, System.Drawing.dll, System.Dynamic.Runtime.dll, System.Globalization.Calendars.dll, System.Globalization.Extensions.dll, System.Globalization.dll, System.IO.Compression.FileSystem.dll, System.IO.Compression.ZipFile.dll, System.IO.Compression.dll, System.IO.FileSystem.DriveInfo.dll, System.IO.FileSystem.Primitives.dll, System.IO.FileSystem.Watcher.dll, System.IO.FileSystem.dll, System.IO.IsolatedStorage.dll, System.IO.MemoryMappedFiles.dll, System.IO.Pipes.dll, System.IO.UnmanagedMemoryStream.dll, System.IO.dll, System.Linq.Expressions.dll, System.Linq.Parallel.dll, System.Linq.Queryable.dll, System.Linq.dll, System.Net.Http.dll, System.Net.NameResolution.dll, System.Net.NetworkInformation.dll, System.Net.Ping.dll, System.Net.Primitives.dll, System.Net.Requests.dll, System.Net.Security.dll, System.Net.Sockets.dll, System.Net.WebHeaderCollection.dll, System.Net.WebSockets.Client.dll, System.Net.WebSockets.dll, System.Net.dll, System.Numerics.dll, System.ObjectModel.dll, System.Reflection.Extensions.dll, System.Reflection.Primitives.dll, System.Reflection.dll, System.Resources.Reader.dll, System.Resources.ResourceManager.dll, System.Resources.Writer.dll, System.Runtime.CompilerServices.VisualC.dll, System.Runtime.Extensions.dll, System.Runtime.Handles.dll, System.Runtime.InteropServices.RuntimeInformation.dll, System.Runtime.InteropServices.dll, System.Runtime.Numerics.dll, System.Runtime.Serialization.Formatters.dll, System.Runtime.Serialization.Json.dll, System.Runtime.Serialization.Primitives.dll, System.Runtime.Serialization.Xml.dll, System.Runtime.Serialization.dll, System.Runtime.dll, System.Security.Claims.dll, System.Security.Cryptography.Algorithms.dll, System.Security.Cryptography.Csp.dll, System.Security.Cryptography.Encoding.dll, System.Security.Cryptography.Primitives.dll, System.Security.Cryptography.X509Certificates.dll, System.Security.Principal.dll, System.Security.SecureString.dll, System.ServiceModel.Web.dll, System.Text.Encoding.Extensions.dll, System.Text.Encoding.dll, System.Text.RegularExpressions.dll, System.Threading.Overlapped.dll, System.Threading.Tasks.Parallel.dll, System.Threading.Tasks.dll, System.Threading.Thread.dll, System.Threading.ThreadPool.dll, System.Threading.Timer.dll, System.Threading.dll, System.Transactions.dll, System.ValueTuple.dll, System.Web.dll, System.Windows.dll, System.Xml.Linq.dll, System.Xml.ReaderWriter.dll, System.Xml.Serialization.dll, System.Xml.XDocument.dll, System.Xml.XPath.XDocument.dll, System.Xml.XPath.dll, System.Xml.XmlDocument.dll, System.Xml.XmlSerializer.dll, System.Xml.dll, System.dll, mscorlib.dll, netstandard.dll"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 1,
              "methods": [
                {
                  "technique": "manifest-analysis",
                  "confidence": 1,
                  "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "EmbedIO@latest:pkg:nuget/Nullable@1.3.0",
          "type": "library",
          "name": "Nullable",
          "version": "1.3.0",
          "hashes": [
            {
              "alg": "SHA-512",
              "content": "c4702f8937536379feb759c43cde093d1411e65235db8a91295c3e53d1fb74ee6c0cd3e9ce859ea3f310cbb752526bfd783de4fc22552a8933d6d14af893b347"
            }
          ],
          "purl": "pkg:nuget/Nullable@1.3.0",
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
            },
            {
              "name": "PackageFiles",
              "value": ""
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 1,
              "methods": [
                {
                  "technique": "manifest-analysis",
                  "confidence": 1,
                  "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "EmbedIO@latest:pkg:nuget/StyleCop.Analyzers@1.1.118",
          "type": "library",
          "name": "StyleCop.Analyzers",
          "version": "1.1.118",
          "hashes": [
            {
              "alg": "SHA-512",
              "content": "3a7c7aa2f192a9748ad3b9ffd1e33766eb2235d07a70894975a6d08561a0269dd5a28cbd01a2d2fed8a07b26ce240a1ba9bb608136a6a169ddcfbd89b1c641bf"
            }
          ],
          "purl": "pkg:nuget/StyleCop.Analyzers@1.1.118",
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
            },
            {
              "name": "PackageFiles",
              "value": "StyleCop.Analyzers.CodeFixes.dll, StyleCop.Analyzers.dll, StyleCop.Analyzers.resources.dll"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 1,
              "methods": [
                {
                  "technique": "manifest-analysis",
                  "confidence": 1,
                  "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "EmbedIO@latest:pkg:nuget/System.ValueTuple@4.5.0",
          "type": "library",
          "name": "System.ValueTuple",
          "version": "4.5.0",
          "hashes": [
            {
              "alg": "SHA-512",
              "content": "a24bab4093ba35113f6a90c83f6dda8c9d21a6236627e7f40703a507f712a932d0970e6ea647fee7ef7afa21b6270e341b57c2542c8fcff1612000548cc47e45"
            }
          ],
          "purl": "pkg:nuget/System.ValueTuple@4.5.0",
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
            },
            {
              "name": "PackageFiles",
              "value": "System.ValueTuple.dll"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 1,
              "methods": [
                {
                  "technique": "manifest-analysis",
                  "confidence": 1,
                  "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
                }
              ]
            }
          }
        },
        {
          "bom-ref": "EmbedIO@latest:pkg:nuget/Unosquare.Swan.Lite@3.1.0",
          "type": "library",
          "name": "Unosquare.Swan.Lite",
          "version": "3.1.0",
          "hashes": [
            {
              "alg": "SHA-512",
              "content": "5f7b39404fca323dd600f16a16f7bb4adf83b35d01079d2ef245bc3e62889fb155927ef21177bd631af686db75595f390d1a9f151d0c37f0543479061ed2f839"
            }
          ],
          "purl": "pkg:nuget/Unosquare.Swan.Lite@3.1.0",
          "properties": [
            {
              "name": "SrcFile",
              "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
            },
            {
              "name": "PackageFiles",
              "value": "Swan.Lite.dll"
            }
          ],
          "evidence": {
            "identity": {
              "field": "purl",
              "confidence": 1,
              "methods": [
                {
                  "technique": "manifest-analysis",
                  "confidence": 1,
                  "value": "/Users/oriavraham/Development/examples/dotnet/embedio/src/EmbedIO/obj/project.assets.json"
                }
              ]
            }
          }
        }
      ]
    }
  ],
  "dependencies": [
    {
      "ref": "EmbedIO@latest:pkg:nuget/EmbedIO@3.5.0",
      "dependsOn": [
        "EmbedIO@latest:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
        "EmbedIO@latest:pkg:nuget/NETStandard.Library@2.0.3",
        "EmbedIO@latest:pkg:nuget/Nullable@1.3.0",
        "EmbedIO@latest:pkg:nuget/StyleCop.Analyzers@1.1.118",
        "EmbedIO@latest:pkg:nuget/Unosquare.Swan.Lite@3.1.0"
      ]
    },
    {
      "ref": "EmbedIO@latest:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
      "dependsOn": [
        "EmbedIO@latest:pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
        "EmbedIO@latest:pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
        "EmbedIO@latest:pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
        "EmbedIO@latest:pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2"
      ]
    },
    {
      "ref": "EmbedIO@latest:pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "EmbedIO@latest:pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "EmbedIO@latest:pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "EmbedIO@latest:pkg:nuget/Microsoft.NETCore.Platforms@1.1.0",
      "dependsOn": []
    },
    {
      "ref": "EmbedIO@latest:pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "EmbedIO@latest:pkg:nuget/NETStandard.Library@2.0.3",
      "dependsOn": [
        "EmbedIO@latest:pkg:nuget/Microsoft.NETCore.Platforms@1.1.0"
      ]
    },
    {
      "ref": "EmbedIO@latest:pkg:nuget/Nullable@1.3.0",
      "dependsOn": []
    },
    {
      "ref": "EmbedIO@latest:pkg:nuget/StyleCop.Analyzers@1.1.118",
      "dependsOn": []
    },
    {
      "ref": "EmbedIO@latest:pkg:nuget/System.ValueTuple@4.5.0",
      "dependsOn": []
    },
    {
      "ref": "EmbedIO@latest:pkg:nuget/Unosquare.Swan.Lite@3.1.0",
      "dependsOn": [
        "EmbedIO@latest:pkg:nuget/System.ValueTuple@4.5.0"
      ]
    },
    {
      "ref": "embedio@dev",
      "dependsOn": [
        "EmbedIO@latest:pkg:nuget/EmbedIO@latest"
      ]
    }
  ]
}

```

Results are pretty similar to **syft,** can we improve them if we generate a lockfile?

```tsx
dotnet restore --use-lock-file .
```

Rerunning the command would yield the same results, can building help?

```tsx
dotnet build
```

Unfortunatly, results are the same. It seems like licenses are absent from the final SBOM. both generators yielded just about the same packages (11-13).

**Trivy**

```tsx
manifest-cli sbom --name=embedio --version=0.0.0-dev --generator=trivy -f test-trivy.json .
```

Just like **cdxgen** most project files are [supported](https://aquasecurity.github.io/trivy/v0.52/docs/coverage/language/dotnet/), thus, running this command would yield a large SBOM, however, the results seems to only pick up some of the packages (compared to cdxgen)

```tsx
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "version": 1,
  "metadata": {
    "component": {
      "bom-ref": "embedio@0.0.0-dev",
      "type": "application",
      "name": "embedio",
      "version": "0.0.0-dev"
    }
  },
  "components": [
    {
      "bom-ref": ".@:eadb491b-2d6c-4aca-b684-d47a6dfaf985",
      "type": "application",
      "name": ".",
      "properties": [
        {
          "name": "aquasecurity:trivy:SchemaVersion",
          "value": "2"
        }
      ],
      "components": [
        {
          "bom-ref": ".@:7cb14795-3436-4c21-bf28-d724e2cf3f49",
          "type": "application",
          "name": "Directory.Packages.props",
          "properties": [
            {
              "name": "aquasecurity:trivy:Class",
              "value": "lang-pkgs"
            },
            {
              "name": "aquasecurity:trivy:Type",
              "value": "packages-props"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.CodeAnalysis.FxCopAnalyzers",
          "version": "3.3.2",
          "purl": "pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "packages-props"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:nuget/Microsoft.NET.Test.Sdk@16.8.3",
          "type": "library",
          "name": "Microsoft.NET.Test.Sdk",
          "version": "16.8.3",
          "purl": "pkg:nuget/Microsoft.NET.Test.Sdk@16.8.3",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Microsoft.NET.Test.Sdk@16.8.3"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "packages-props"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:nuget/NUnit3TestAdapter@3.17.0",
          "type": "library",
          "name": "NUnit3TestAdapter",
          "version": "3.17.0",
          "purl": "pkg:nuget/NUnit3TestAdapter@3.17.0",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "NUnit3TestAdapter@3.17.0"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "packages-props"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:nuget/NUnit@3.13.1",
          "type": "library",
          "name": "NUnit",
          "version": "3.13.1",
          "purl": "pkg:nuget/NUnit@3.13.1",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "NUnit@3.13.1"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "packages-props"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:nuget/Nullable@1.3.0",
          "type": "library",
          "name": "Nullable",
          "version": "1.3.0",
          "purl": "pkg:nuget/Nullable@1.3.0",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Nullable@1.3.0"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "packages-props"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:nuget/StyleCop.Analyzers@1.1.118",
          "type": "library",
          "name": "StyleCop.Analyzers",
          "version": "1.1.118",
          "purl": "pkg:nuget/StyleCop.Analyzers@1.1.118",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "StyleCop.Analyzers@1.1.118"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "packages-props"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:nuget/Tubular.ServerSide@4.0.0",
          "type": "library",
          "name": "Tubular.ServerSide",
          "version": "4.0.0",
          "purl": "pkg:nuget/Tubular.ServerSide@4.0.0",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Tubular.ServerSide@4.0.0"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "packages-props"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:nuget/Unosquare.Swan.Lite@3.1.0",
          "type": "library",
          "name": "Unosquare.Swan.Lite",
          "version": "3.1.0",
          "purl": "pkg:nuget/Unosquare.Swan.Lite@3.1.0",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Unosquare.Swan.Lite@3.1.0"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "packages-props"
            }
          ]
        },
        {
          "bom-ref": ".@:pkg:nuget/coverlet.msbuild@3.0.2",
          "type": "library",
          "name": "coverlet.msbuild",
          "version": "3.0.2",
          "purl": "pkg:nuget/coverlet.msbuild@3.0.2",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "coverlet.msbuild@3.0.2"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "packages-props"
            }
          ]
        }
      ]
    }
  ],
  "dependencies": [
    {
      "ref": ".@:7cb14795-3436-4c21-bf28-d724e2cf3f49",
      "dependsOn": [
        ".@:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
        ".@:pkg:nuget/Microsoft.NET.Test.Sdk@16.8.3",
        ".@:pkg:nuget/NUnit3TestAdapter@3.17.0",
        ".@:pkg:nuget/NUnit@3.13.1",
        ".@:pkg:nuget/Nullable@1.3.0",
        ".@:pkg:nuget/StyleCop.Analyzers@1.1.118",
        ".@:pkg:nuget/Tubular.ServerSide@4.0.0",
        ".@:pkg:nuget/Unosquare.Swan.Lite@3.1.0",
        ".@:pkg:nuget/coverlet.msbuild@3.0.2"
      ]
    },
    {
      "ref": ".@:eadb491b-2d6c-4aca-b684-d47a6dfaf985",
      "dependsOn": [
        ".@:7cb14795-3436-4c21-bf28-d724e2cf3f49"
      ]
    },
    {
      "ref": ".@:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:nuget/Microsoft.NET.Test.Sdk@16.8.3",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:nuget/NUnit3TestAdapter@3.17.0",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:nuget/NUnit@3.13.1",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:nuget/Nullable@1.3.0",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:nuget/StyleCop.Analyzers@1.1.118",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:nuget/Tubular.ServerSide@4.0.0",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:nuget/Unosquare.Swan.Lite@3.1.0",
      "dependsOn": []
    },
    {
      "ref": ".@:pkg:nuget/coverlet.msbuild@3.0.2",
      "dependsOn": []
    },
    {
      "ref": "embedio@0.0.0-dev",
      "dependsOn": [
        ".@:eadb491b-2d6c-4aca-b684-d47a6dfaf985"
      ]
    }
  ]
}
```

This project includes two `.props` files, Trivy doesn’t support transitive dependencies, graph dependencies and it excludes dev dependencies.

If you project include `packages.config` you will be able to get transitive dependencies and licenses data as well.

What happen if we attempt to generate for a folder?

```tsx
manifest-cli sbom --name=embedio --version=0.0.0-dev --generator=trivy -f test-trivy.json src/EmbedIO
```

Would output:

```tsx
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "version": 1,
  "metadata": {
    "component": {
      "bom-ref": "embedio@0.0.0-dev",
      "type": "application",
      "name": "embedio",
      "version": "0.0.0-dev"
    }
  },
  "components": [
    {
      "bom-ref": "src/EmbedIO@:161ad80e-c507-492b-8cc5-e9199b136fcf",
      "type": "application",
      "name": "src/EmbedIO",
      "properties": [
        {
          "name": "aquasecurity:trivy:SchemaVersion",
          "value": "2"
        }
      ],
      "components": []
    }
  ],
  "dependencies": [
    {
      "ref": "src/EmbedIO@:161ad80e-c507-492b-8cc5-e9199b136fcf",
      "dependsOn": []
    },
    {
      "ref": "embedio@0.0.0-dev",
      "dependsOn": [
        "src/EmbedIO@:161ad80e-c507-492b-8cc5-e9199b136fcf"
      ]
    }
  ]
}

```

Just like syft, Trivy is unable to find anything without .deps.json

```tsx
dotnet build
```

Rerun:

```tsx
manifest-cli sbom --name=embedio --version=0.0.0-dev --generator=trivy -f test-trivy.json src/EmbedIO
```

Output:

```tsx
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "version": 1,
  "metadata": {
    "component": {
      "bom-ref": "embedio@0.0.0-dev",
      "type": "application",
      "name": "embedio",
      "version": "0.0.0-dev"
    }
  },
  "components": [
    {
      "bom-ref": "src/EmbedIO@:703d375d-52a1-4bad-90b8-93e81d86fd8a",
      "type": "application",
      "name": "src/EmbedIO",
      "properties": [
        {
          "name": "aquasecurity:trivy:SchemaVersion",
          "value": "2"
        }
      ],
      "components": [
        {
          "bom-ref": "src/EmbedIO@:f2daf5a4-97c0-4e39-badc-efe93e4c1b33",
          "type": "application",
          "name": "bin/Debug/netstandard2.0/EmbedIO.deps.json",
          "properties": [
            {
              "name": "aquasecurity:trivy:Class",
              "value": "lang-pkgs"
            },
            {
              "name": "aquasecurity:trivy:Type",
              "value": "dotnet-core"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.CodeAnalysis.FxCopAnalyzers",
          "version": "3.3.2",
          "purl": "pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "dotnet-core"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
          "type": "library",
          "name": "Microsoft.CodeAnalysis.VersionCheckAnalyzer",
          "version": "3.3.2",
          "purl": "pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "dotnet-core"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.CodeQuality.Analyzers",
          "version": "3.3.2",
          "purl": "pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "dotnet-core"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.NETCore.Platforms@1.1.0",
          "type": "library",
          "name": "Microsoft.NETCore.Platforms",
          "version": "1.1.0",
          "purl": "pkg:nuget/Microsoft.NETCore.Platforms@1.1.0",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "dotnet-core"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.NetCore.Analyzers",
          "version": "3.3.2",
          "purl": "pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "dotnet-core"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.NetFramework.Analyzers",
          "version": "3.3.2",
          "purl": "pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "dotnet-core"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/NETStandard.Library@2.0.3",
          "type": "library",
          "name": "NETStandard.Library",
          "version": "2.0.3",
          "purl": "pkg:nuget/NETStandard.Library@2.0.3",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "dotnet-core"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Nullable@1.3.0",
          "type": "library",
          "name": "Nullable",
          "version": "1.3.0",
          "purl": "pkg:nuget/Nullable@1.3.0",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "dotnet-core"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/StyleCop.Analyzers@1.1.118",
          "type": "library",
          "name": "StyleCop.Analyzers",
          "version": "1.1.118",
          "purl": "pkg:nuget/StyleCop.Analyzers@1.1.118",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "dotnet-core"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/System.ValueTuple@4.5.0",
          "type": "library",
          "name": "System.ValueTuple",
          "version": "4.5.0",
          "purl": "pkg:nuget/System.ValueTuple@4.5.0",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "dotnet-core"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Unosquare.Swan.Lite@3.1.0",
          "type": "library",
          "name": "Unosquare.Swan.Lite",
          "version": "3.1.0",
          "purl": "pkg:nuget/Unosquare.Swan.Lite@3.1.0",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "dotnet-core"
            }
          ]
        }
      ]
    }
  ],
  "dependencies": [
    {
      "ref": "src/EmbedIO@:703d375d-52a1-4bad-90b8-93e81d86fd8a",
      "dependsOn": [
        "src/EmbedIO@:f2daf5a4-97c0-4e39-badc-efe93e4c1b33"
      ]
    },
    {
      "ref": "src/EmbedIO@:f2daf5a4-97c0-4e39-badc-efe93e4c1b33",
      "dependsOn": [
        "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
        "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
        "src/EmbedIO@:pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
        "src/EmbedIO@:pkg:nuget/Microsoft.NETCore.Platforms@1.1.0",
        "src/EmbedIO@:pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
        "src/EmbedIO@:pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2",
        "src/EmbedIO@:pkg:nuget/NETStandard.Library@2.0.3",
        "src/EmbedIO@:pkg:nuget/Nullable@1.3.0",
        "src/EmbedIO@:pkg:nuget/StyleCop.Analyzers@1.1.118",
        "src/EmbedIO@:pkg:nuget/System.ValueTuple@4.5.0",
        "src/EmbedIO@:pkg:nuget/Unosquare.Swan.Lite@3.1.0"
      ]
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.NETCore.Platforms@1.1.0",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/NETStandard.Library@2.0.3",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Nullable@1.3.0",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/StyleCop.Analyzers@1.1.118",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/System.ValueTuple@4.5.0",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Unosquare.Swan.Lite@3.1.0",
      "dependsOn": []
    },
    {
      "ref": "embedio@0.0.0-dev",
      "dependsOn": [
        "src/EmbedIO@:703d375d-52a1-4bad-90b8-93e81d86fd8a"
      ]
    }
  ]
}

```

Results seems far better, however, depedency graph seems flat and no dev dependencies listed as expected.

Can we try and fix it with a lockfile?

```tsx
dotnet restore --use-lock-file .
```

This generated `package.lock.json` under `src/EmbedIO` .

Rerun:

```tsx
manifest-cli sbom --name=embedio --version=0.0.0-dev --generator=trivy -f test-trivy.json src/EmbedIO
```

Output:

```tsx
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "version": 1,
  "metadata": {
    "component": {
      "bom-ref": "embedio@0.0.0-dev",
      "type": "application",
      "name": "embedio",
      "version": "0.0.0-dev"
    }
  },
  "components": [
    {
      "bom-ref": "src/EmbedIO@:03c6d404-5207-47b3-9856-29b488b9adf0",
      "type": "application",
      "name": "src/EmbedIO",
      "properties": [
        {
          "name": "aquasecurity:trivy:SchemaVersion",
          "value": "2"
        }
      ],
      "components": [
        {
          "bom-ref": "src/EmbedIO@:d9769f71-996c-401e-bde8-d86e97eb9a86",
          "type": "application",
          "name": "packages.lock.json",
          "properties": [
            {
              "name": "aquasecurity:trivy:Class",
              "value": "lang-pkgs"
            },
            {
              "name": "aquasecurity:trivy:Type",
              "value": "nuget"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.CodeAnalysis.FxCopAnalyzers",
          "version": "3.3.2",
          "licenses": [
            {
              "license": {
                "name": "Apache-2.0"
              }
            }
          ],
          "purl": "pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "nuget"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
          "type": "library",
          "name": "Microsoft.CodeAnalysis.VersionCheckAnalyzer",
          "version": "3.3.2",
          "licenses": [
            {
              "license": {
                "name": "Apache-2.0"
              }
            }
          ],
          "purl": "pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "nuget"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.CodeQuality.Analyzers",
          "version": "3.3.2",
          "licenses": [
            {
              "license": {
                "name": "Apache-2.0"
              }
            }
          ],
          "purl": "pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Microsoft.CodeQuality.Analyzers@3.3.2"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "nuget"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.NETCore.Platforms@1.1.0",
          "type": "library",
          "name": "Microsoft.NETCore.Platforms",
          "version": "1.1.0",
          "purl": "pkg:nuget/Microsoft.NETCore.Platforms@1.1.0",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Microsoft.NETCore.Platforms@1.1.0"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "nuget"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.NetCore.Analyzers",
          "version": "3.3.2",
          "licenses": [
            {
              "license": {
                "name": "Apache-2.0"
              }
            }
          ],
          "purl": "pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Microsoft.NetCore.Analyzers@3.3.2"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "nuget"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2",
          "type": "library",
          "name": "Microsoft.NetFramework.Analyzers",
          "version": "3.3.2",
          "licenses": [
            {
              "license": {
                "name": "Apache-2.0"
              }
            }
          ],
          "purl": "pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Microsoft.NetFramework.Analyzers@3.3.2"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "nuget"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/NETStandard.Library@2.0.3",
          "type": "library",
          "name": "NETStandard.Library",
          "version": "2.0.3",
          "purl": "pkg:nuget/NETStandard.Library@2.0.3",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "NETStandard.Library@2.0.3"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "nuget"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Nullable@1.3.0",
          "type": "library",
          "name": "Nullable",
          "version": "1.3.0",
          "licenses": [
            {
              "license": {
                "name": "MIT"
              }
            }
          ],
          "purl": "pkg:nuget/Nullable@1.3.0",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Nullable@1.3.0"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "nuget"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/StyleCop.Analyzers@1.1.118",
          "type": "library",
          "name": "StyleCop.Analyzers",
          "version": "1.1.118",
          "licenses": [
            {
              "license": {
                "name": "Apache-2.0"
              }
            }
          ],
          "purl": "pkg:nuget/StyleCop.Analyzers@1.1.118",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "StyleCop.Analyzers@1.1.118"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "nuget"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/System.ValueTuple@4.5.0",
          "type": "library",
          "name": "System.ValueTuple",
          "version": "4.5.0",
          "purl": "pkg:nuget/System.ValueTuple@4.5.0",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "System.ValueTuple@4.5.0"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "nuget"
            }
          ]
        },
        {
          "bom-ref": "src/EmbedIO@:pkg:nuget/Unosquare.Swan.Lite@3.1.0",
          "type": "library",
          "name": "Unosquare.Swan.Lite",
          "version": "3.1.0",
          "purl": "pkg:nuget/Unosquare.Swan.Lite@3.1.0",
          "properties": [
            {
              "name": "aquasecurity:trivy:PkgID",
              "value": "Unosquare.Swan.Lite@3.1.0"
            },
            {
              "name": "aquasecurity:trivy:PkgType",
              "value": "nuget"
            }
          ]
        }
      ]
    }
  ],
  "dependencies": [
    {
      "ref": "src/EmbedIO@:03c6d404-5207-47b3-9856-29b488b9adf0",
      "dependsOn": [
        "src/EmbedIO@:d9769f71-996c-401e-bde8-d86e97eb9a86"
      ]
    },
    {
      "ref": "src/EmbedIO@:d9769f71-996c-401e-bde8-d86e97eb9a86",
      "dependsOn": [
        "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
        "src/EmbedIO@:pkg:nuget/NETStandard.Library@2.0.3",
        "src/EmbedIO@:pkg:nuget/Nullable@1.3.0",
        "src/EmbedIO@:pkg:nuget/StyleCop.Analyzers@1.1.118",
        "src/EmbedIO@:pkg:nuget/Unosquare.Swan.Lite@3.1.0"
      ]
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2",
      "dependsOn": [
        "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
        "src/EmbedIO@:pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
        "src/EmbedIO@:pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
        "src/EmbedIO@:pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2"
      ]
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.NETCore.Platforms@1.1.0",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/NETStandard.Library@2.0.3",
      "dependsOn": [
        "src/EmbedIO@:pkg:nuget/Microsoft.NETCore.Platforms@1.1.0"
      ]
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Nullable@1.3.0",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/StyleCop.Analyzers@1.1.118",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/System.ValueTuple@4.5.0",
      "dependsOn": []
    },
    {
      "ref": "src/EmbedIO@:pkg:nuget/Unosquare.Swan.Lite@3.1.0",
      "dependsOn": [
        "src/EmbedIO@:pkg:nuget/System.ValueTuple@4.5.0"
      ]
    },
    {
      "ref": "embedio@0.0.0-dev",
      "dependsOn": [
        "src/EmbedIO@:03c6d404-5207-47b3-9856-29b488b9adf0"
      ]
    }
  ]
}
```

The results includes **licenses, graph depedencies,** and **dev dependencies.**

**sbom-tool**

A tool developed by Microsoft, it generate SPDX 2.2 only, however, its worth mentioning due to deeper integration with NuGet.

```tsx
sbom-tool generate -b . -bc . -ps none  -pn test-sbom-tool -pv 1.0.0
```

The output should look like this:

```tsx
{
  "files": [
    {
      "fileName": "./Directory.Build.props",
      "SPDXID": "SPDXRef-File--Directory.Build.props-A185B8FE61B98549C2CC401AA5761AE62EF3A0CD",
      "checksums": [
        {
          "algorithm": "SHA256",
          "checksumValue": "8e771baa8c9883821e36e26436d9d405e8ccd2017fe78a998fc8050ac3ae9cb0"
        },
        {
          "algorithm": "SHA1",
          "checksumValue": "a185b8fe61b98549c2cc401aa5761ae62ef3a0cd"
        }
      ],
      "licenseConcluded": "NOASSERTION",
      "licenseInfoInFiles": [
        "NOASSERTION"
      ],
      "copyrightText": "NOASSERTION"
    },
    {
      "fileName": "./EmbedIO.sln.DotSettings",
      "SPDXID": "SPDXRef-File--EmbedIO.sln.DotSettings-072468DDD020D203450CE81AF916A693A715330A",
      "checksums": [
        {
          "algorithm": "SHA256",
          "checksumValue": "3e6920b6e0ede0f7fc8fd64bc5f949a4470907cab6ac80dfdc85fd76ac83168a"
        },
        {
          "algorithm": "SHA1",
          "checksumValue": "072468ddd020d203450ce81af916a693a715330a"
        }
      ],
      "licenseConcluded": "NOASSERTION",
      "licenseInfoInFiles": [
        "NOASSERTION"
      ],
      "copyrightText": "NOASSERTION"
    },
    ...
    ...
    ...
  ],
  "packages": [
    {
      "name": "Microsoft.NetCore.Analyzers",
      "SPDXID": "SPDXRef-Package-C6D08745A01E5768789F7336947C2F95A9AA434D8D3306C689C82D69E8F6A16E",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "3.3.2",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Microsoft.NetCore.Analyzers@3.3.2"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Microsoft.DotNet.InternalAbstractions",
      "SPDXID": "SPDXRef-Package-BE81CAD2FFD8AE7908F1AAB2DAD5A57984A518D56B6273446E3A7534F6479803",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "1.0.0",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Microsoft.DotNet.InternalAbstractions@1.0.0"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Tubular.ServerSide",
      "SPDXID": "SPDXRef-Package-50D975328CA1C4FF12863549F4DC7468E12D39B32AC5367525B5D30B088D6037",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "4.0.0",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Tubular.ServerSide@4.0.0"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Microsoft.CodeCoverage",
      "SPDXID": "SPDXRef-Package-6749A6401B0F20517D91787BD129A9BA4B75C2874B0A96F69A17D2476683F895",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "16.8.3",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Microsoft.CodeCoverage@16.8.3"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Microsoft.CodeAnalysis.VersionCheckAnalyzer",
      "SPDXID": "SPDXRef-Package-F2F4C0E260F287DBD785B1ABCA39F1E1D27C07AADD71DFF7E83C0A5F16327707",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "3.3.2",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Microsoft.CodeAnalysis.VersionCheckAnalyzer@3.3.2"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Unosquare.Swan.Lite",
      "SPDXID": "SPDXRef-Package-B458072059F54518C1B25496F3D09765CF472A492FD7108B5FCB9E3545DD6237",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "3.1.0",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Unosquare.Swan.Lite@3.1.0"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Nullable",
      "SPDXID": "SPDXRef-Package-23A6B66FF601D949E3AC28A6A392DC5F01458AB6F9CEDFCD3A17091B2F26BDD5",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "1.3.0",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Nullable@1.3.0"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "System.Linq.Dynamic.Core",
      "SPDXID": "SPDXRef-Package-622AFA62783284D54C08FAB39928AAB502604CE350ED14CA42BC8D0B858552B0",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "1.2.7",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/System.Linq.Dynamic.Core@1.2.7"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "StyleCop.Analyzers",
      "SPDXID": "SPDXRef-Package-95988ACE14A368B8C3409E145AA92C0F93D243DD95C5FB89A6CAABAAD0D1115D",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "1.1.118",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/StyleCop.Analyzers@1.1.118"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "NUnit",
      "SPDXID": "SPDXRef-Package-9E33C25A33A148C7F507C2F5039687C71E645F0B3596D83484C775AF7A8BFBAE",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "3.13.1",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/NUnit@3.13.1"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Microsoft.NetFramework.Analyzers",
      "SPDXID": "SPDXRef-Package-E3502C1021CBB5BB09BFCC676ABD160F59F2168C35D9FB6FF2DAC3CE9A17AD23",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "3.3.2",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Microsoft.NetFramework.Analyzers@3.3.2"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Microsoft.TestPlatform.TestHost",
      "SPDXID": "SPDXRef-Package-449FA483DAB78707360B58441C2D5BD4E2F5E683A4806E05A111D6EE505B81EA",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "16.8.3",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Microsoft.TestPlatform.TestHost@16.8.3"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Microsoft.TestPlatform.ObjectModel",
      "SPDXID": "SPDXRef-Package-781C50A98A285B9BB69D0050795F91134F1A14E59C6CA75F06BE606F1F8F89D6",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "16.8.3",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Microsoft.TestPlatform.ObjectModel@16.8.3"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Microsoft.CodeAnalysis.FxCopAnalyzers",
      "SPDXID": "SPDXRef-Package-068BFA3B59591FD6452F69A2EEBBE970BAB7A4FB982604A61DA03CB9B5D0091E",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "3.3.2",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Microsoft.CodeAnalysis.FxCopAnalyzers@3.3.2"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "coverlet.msbuild",
      "SPDXID": "SPDXRef-Package-E410F042AA2A506E114A7862764CA009254E81AB885859709107C80D95928B65",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "3.0.2",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/coverlet.msbuild@3.0.2"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Newtonsoft.Json",
      "SPDXID": "SPDXRef-Package-930A940927E2F2ACCFB50E7E3C1DE7170F84695F12046CB49ED006AFAD78E6A1",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "9.0.1",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Newtonsoft.Json@9.0.1"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "System.ValueTuple",
      "SPDXID": "SPDXRef-Package-C1475C5380732C85127A15B8BADF74D2619786E90578875B650082AE4497BC14",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "4.5.0",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/System.ValueTuple@4.5.0"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "NuGet.Frameworks",
      "SPDXID": "SPDXRef-Package-3D762E0F169506279F40A11F69CB7F7E9DA3F36F47D6E7C2E17C3161DADB7FE8",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "5.0.0",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/NuGet.Frameworks@5.0.0"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Microsoft.CodeQuality.Analyzers",
      "SPDXID": "SPDXRef-Package-E5EE6EA84A72B4995DB540420D83E79A943C54DAEBF1D9032BD5B56DD003445E",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "3.3.2",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Microsoft.CodeQuality.Analyzers@3.3.2"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "System.Xml.XPath.XmlDocument",
      "SPDXID": "SPDXRef-Package-52358C2D014206CBB069F497F1733F57788AAAB3507E4A6417069998F3B486DF",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "4.3.0",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/System.Xml.XPath.XmlDocument@4.3.0"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "NUnit3TestAdapter",
      "SPDXID": "SPDXRef-Package-AC43CF918CC0478383611B7AAD3EBFC9B023CD761B5AC8D5208286EFBE599015",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "3.17.0",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/NUnit3TestAdapter@3.17.0"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "Microsoft.NET.Test.Sdk",
      "SPDXID": "SPDXRef-Package-2ADE5DBB828ACE8FA25CDCEB77507D26A832BC3F7580A468FA0AAE065CC237AD",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "licenseConcluded": "NOASSERTION",
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "16.8.3",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:nuget/Microsoft.NET.Test.Sdk@16.8.3"
        }
      ],
      "supplier": "NOASSERTION"
    },
    {
      "name": "demo",
      "SPDXID": "SPDXRef-RootPackage",
      "downloadLocation": "NOASSERTION",
      "packageVerificationCode": {
        "packageVerificationCodeValue": "7c5ffbc4934c89da87116dbea904dca731472a4d"
      },
      "filesAnalyzed": true,
      "licenseConcluded": "NOASSERTION",
      "licenseInfoFromFiles": [
        "NOASSERTION"
      ],
      "licenseDeclared": "NOASSERTION",
      "copyrightText": "NOASSERTION",
      "versionInfo": "1.0.0",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:swid/none/spdx.org/demo@1.0.0?tag_id=d834fdfb-3103-4f27-b846-17516c86164c"
        }
      ],
      "supplier": "Organization: none",
      "hasFiles": [
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample-MainPage.xaml.cs-1D6C01A998459A1E1F59D724AD0DD89C872782EF",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon120.png-72ECE031649FFCA6A2A0FFAA613C67DB0909D49A",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Properties-AssemblyInfo.cs-1D2EE7B60B4DBE5B525C86E4F793427CDAA2E894",
        "SPDXRef-File--src-EmbedIO.Samples-html-scripts-app.directives.js-FDD8DE1052EB72D4902BE23DB1A1C32A6CC5DB73",
        "SPDXRef-File--src-EmbedIO.Samples-Person.cs-AC4FE5300B4E8A64568032735F8F8D76E0569DDB",
        "SPDXRef-File--src-EmbedIO.Testing-Internal-TestContext.cs-6FFCBC85F6FD2540D8CD7312A0106640A315326B",
        "SPDXRef-File--src-EmbedIO.Samples-html-favicon.ico-1577CACAEA9EDE5EA96C3E4E707C61BE86581C08",
        "SPDXRef-File--src-EmbedIO.Testing-Resources-sub-index.html-28B03D31FDB23778BFBA0799B7574FD9E75C437D",
        "SPDXRef-File--src-EmbedIO.Samples-EmbedIO.Samples.csproj-DA9C5D97E694D7EF269DD1EDA3143D0E316E667A",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.csproj-78718EB21F137AA4917853DAFD4A7A73C61893FF",
        "SPDXRef-File--src-EmbedIO.Testing-Internal-TestMessageHandler.cs-BE32F92BBBAF802F508B04590911E7E8F5DECAB3",
        "SPDXRef-File--src-EmbedIO.Testing-Internal-TestMessageHandler.ResponseHeaderType.cs-B269A9F380EC4E78DFAB713443E80AF88137AD9E",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-mipmap-mdpi-icon.png-DEC0FEB5349FF85849950D8BFE927CE6F2C8929B",
        "SPDXRef-File--src-EmbedIO.Testing-obj-EmbedIO.Testing.csproj.nuget.g.props-5FF0C84F07348B4C617C5AC10204F5CB3AF5ADF4",
        "SPDXRef-File--src-EmbedIO.Testing-TestHttpClient.cs-D1991479248EB0658B2C7A0A2876927E70764B92",
        "SPDXRef-File--src-EmbedIO.Testing-TestWebServerOptions.cs-C0345EFFB3073711B7856E644FAF105DEF43905E",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Resources-Default-2x.png-644E0FE40EAF5C06670C9599818F090908B2BA45",
        "SPDXRef-File--src-EmbedIO.Testing-HttpResponseMessageExtensions.cs-7151A52D0B016E7888C4C2169352A6E9A79A516B",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Resources-Default-Portrait-2x.png-CF01892F6BC36AF0669FAD13594004B843D849B4",
        "SPDXRef-File--src-EmbedIO.Testing-TestWebServer.cs-204959EECC73A4A57C4F707C4020721D20531CDA",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Properties-AndroidManifest.xml-2910D57D05167F8112DFE310E502B851D2644121",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-mipmap-anydpi-v26-icon.xml-AB17E2C40AEA2C03A97111ACD89F76C9A0DAB4BE",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon152.png-830F8CED47F0FB670B73CC4CB8C94CF098F80DF6",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-EmbedIO.Forms.Sample.iOS.csproj-B4F4596B0219CA0D9D35065C1745CA978CAC9078",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-mipmap-hdpi-launcher-foreground.png-7D74859C1D7552B6054F9CF40C9C09AF616D8E6E",
        "SPDXRef-File--src-EmbedIO-Authentication-BasicAuthenticationModuleBase.cs-10BDC7DFC32F922B44726A7CEAB15AFB0D2BAFE7",
        "SPDXRef-File--src-EmbedIO-WebApi-IRequestDataAttribute-1.cs-074247BBD6CE7EAC9385B5FEF12B19E98DA237A2",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample-html-index.html-074D1531F0AC995DC5F19AD38A486E95C7332674",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Resources-LaunchScreen.storyboard-32AA3E872557B7D2A41C662DE282E025FCB4EBEE",
        "SPDXRef-File--src-EmbedIO-WebApi-WebApiModuleExtensions.cs-D310F75743C9E9D7FFC1463A7EE6F9F4A0CFC5C7",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-EmbedIO.Forms.Sample.Android.csproj-2B490FEA0AE7AA600403A47E1402D346FF9F1692",
        "SPDXRef-File--src-EmbedIO-Routing-RoutingModuleExtensions-AddHandlerFromBaseOrTerminalRoute.cs-EBEDB434460A8A12C4AAA32D2C5D73A3834F6C5B",
        "SPDXRef-File--src-EmbedIO-Routing-SyncRouteHandlerCallback.cs-28C50AD422BA58070C85A0D4BD212DD9D400E51B",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Resources-Default-568h-2x.png-9C14BAFAE08B95F61A5510F18E8E4A417C98170F",
        "SPDXRef-File--src-EmbedIO-WebApi-QueryFieldAttribute.cs-74463C362FD45E7F2A49AA44541D7D190C25AA43",
        "SPDXRef-File--src-EmbedIO-Files-Internal-MappedResourceInfoExtensions.cs-09794970B5C032673FD304651B5D9F0758480EE2",
        "SPDXRef-File--src-EmbedIO-Routing-RouteResolutionResult.cs-3D23663D963607379C4E821EE0D3699A1870B3CC",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample-App.xaml.cs-131B903D2BAE33160B8EBABF4E4016E060977D97",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon76.png-C2EB5A8FF277716115E437E9B4C8E86FDBF7AA8C",
        "SPDXRef-File--src-EmbedIO-Routing-RouteMatcher.cs-F2B5AD924804F8033F21A311703C4CC9D572EFA0",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Resources-Default-Portrait.png-785AC441C25120EAA1EA557A749B88315D4D82CB",
        "SPDXRef-File--src-EmbedIO-Cors-CorsModule.cs-B81B7ED13BCA81920927AF1A703E1B4471EDC7E6",
        "SPDXRef-File--src-EmbedIO.Samples-obj-project.assets.json-10728E779765068C2C7DFCF11C6C0D5C24179AD4",
        "SPDXRef-File--src-EmbedIO.Samples-html-scripts-app.routes.js-0935CDAD7CB7CB59AF6B59AE33A0FBCA0ACDB674",
        "SPDXRef-File--src-EmbedIO.Samples-html-scripts-app.controllers.js-127B20D378FD0BD4FD346FD8D9A74C06698A075D",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-mipmap-anydpi-v26-icon-round.xml-AB17E2C40AEA2C03A97111ACD89F76C9A0DAB4BE",
        "SPDXRef-File--src-EmbedIO.Samples-html-scripts-app.js-B6BEC427FF28D0BEB4E2C6543149863867BA8828",
        "SPDXRef-File--src-EmbedIO.Samples-obj-project.nuget.cache-9C45BC4182CE4F6ECA6A5B9338E5DA38AF626126",
        "SPDXRef-File--src-EmbedIO.Samples-html-css-embedio.png-54F9D3E8354F0099FD23227279A3804839EAF3D9",
        "SPDXRef-File--src-EmbedIO.Samples-Program.cs-8E1E2B851373D068D79AFB5855E22AAC13A06BAE",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon1024.png-78079CB774F8F3FA8B110377115240297CDD730A",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-mipmap-xxhdpi-Icon.png-4FBEAD11E60082D2162CF8F3616A85CF761BFEE7",
        "SPDXRef-File--src-EmbedIO.Samples-obj-EmbedIO.Samples.csproj.nuget.g.targets-C2697180DD7A73BCBD5B8CB82B733D0E329E1554",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon180.png-7CDAB81A4CA14E9F8C9AB13EA80A3071768E8012",
        "SPDXRef-File--src-EmbedIO.Testing-obj-project.assets.json-88D587C857C3E57382CB1AAF9F640DF2E5327EF8",
        "SPDXRef-File--src-EmbedIO.Testing-HttpClientExtensions.cs-6ABC19FC0F953B53DF6FEE70563F11C4FD31EB61",
        "SPDXRef-File--src-EmbedIO.Testing-obj-project.nuget.cache-2E9908FF9BF8C18930553C4561071F0A94B2A6A9",
        "SPDXRef-File--src-EmbedIO.Testing-StockResource.cs-08365ABC99581CF82DB5DD86FC016435F4C3A6C1",
        "SPDXRef-File--src-EmbedIO.Testing-MockFileProvider.cs-BFC9C27A810CD42708AC0B28C03D3CF004E07629",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample-MainPage.xaml-10B8784462A5BA0FFF6C02363E20F918585492C1",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon58.png-2A73B9A1754DCF5C213F9D0749FDC57AB5C54DAB",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-values-styles.xml-69A6B2756B65B70038529F41A6A13AC5F252ECA4",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon60.png-C26E8D1E436B0F20A90FD7E7F44FA2AC1EA827E8",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-mipmap-xxhdpi-launcher-foreground.png-21F790ECDD1CEEC7B3662F54CE511703ADB91C2D",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-layout-Tabbar.axml-BAF89D9F2E9D0A5660E5D44E1563F930E636D078",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-mipmap-xhdpi-Icon.png-5D07FAD00DE01B41073C8FB87B5C8FED9284D67E",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Properties-AssemblyInfo.cs-0DD69D0685F4FB026662DFA4718E02FCCB433B80",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-Resource.designer.cs-29C3270AF8C126EB8B633D097EFB0A8E76B5B034",
        "SPDXRef-File--src-EmbedIO-WebApi-IRequestDataAttribute-2.cs-2CDA413D4227B42FB18D5559C04B7F17B5711032",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-mipmap-xxxhdpi-Icon.png-2E8221D64B0A2152EB0AB44DF450A689818990BA",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon40.png-B3DFD2CCF709DA022E5D05A71AE3317818A17388",
        "SPDXRef-File--src-EmbedIO-Routing-RouteVerbResolver.cs-524734C03CD9A2ECBA79BF7B316C89842BEE20E1",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-mipmap-mdpi-launcher-foreground.png-693426399905F5A8BDF6777EA8C02A6323D03C6F",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.sln-722A6E630A8A9A9D8A7D89BE04123D3BE95BA523",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample-ViewModel.cs-FEDC1F1D39DB2B055E4566A4B2E2DB103064A6D3",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon20.png-2302E3954C6A50EA22E3C8D79A927AD57821CDCC",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Entitlements.plist-72CE4A2D94A537DA777E3F294056EB5C89DCC828",
        "SPDXRef-File--src-EmbedIO-Files-FileCache.Section.cs-0BBEEC9535714C4916ED358F659C29124B2CB5CD",
        "SPDXRef-File--src-EmbedIO-Routing-RoutingModuleBase.cs-A07587678A97C96C36C3F8DF0F7775C3EC8C2E18",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon80.png-5307DBB769406A320C565ED5FD443B8EDBFA6804",
        "SPDXRef-File--src-EmbedIO-Routing-RouteMatch.cs-81CE429407A3DCEE55C5264106F468F423FD9C09",
        "SPDXRef-File--src-EmbedIO.Samples-html-views-chat.html-7E9914A0189556C13066FEC64D38117A71E76979",
        "SPDXRef-File--src-EmbedIO.Samples-html-scripts-tubular-tubular-bundle.min.js-943AA9ED8BD20C00ABF45D4573081538B730E89F",
        "SPDXRef-File--src-EmbedIO-WebApi-WebApiModule.cs-E7742B18D78653389934732C2A6E6939439A7D80",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Resources-Default.png-2E2E2FA0667DFB5A817D28C18A8E77792658F2F6",
        "SPDXRef-File--src-EmbedIO-Routing-Route.cs-511F4054149BA3819CA8012EBA7895E086C977CC",
        "SPDXRef-File--src-EmbedIO-Files-FileModule.cs-99B8DBEDD82FF6CDE9130A1C66174D4C8BAA32D8",
        "SPDXRef-File--src-EmbedIO-Sessions-ISessionProxy.cs-CC857E1F5E157CAD08FBD6231E91E0E89002BA07",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-README.md-4E0B92CE4A623A2FD570ED62ED3C042E33DE0048",
        "SPDXRef-File--src-EmbedIO-WebApi-FormDataAttribute.cs-7C0C000CF56754C65B3A26795BBDEC37910F71C4",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-AppDelegate.cs-32A37F520548B4AEAF79EA34D8A573E0B708722A",
        "SPDXRef-File--src-EmbedIO-WebApi-WebApiModuleBase.cs-27E62EB1B913AB4B448FB9973F7441E64D0E3AEC",
        "SPDXRef-File--src-EmbedIO.Samples-html-css-github-logo.svg-AFB361CFC0C97B1A68CCE025936795D0A48BF015",
        "SPDXRef-File--src-EmbedIO-WebApi-WebApiController.cs-2D7BC4DC654ED633E08DB5CE1055E52F847BC439",
        "SPDXRef-File--src-EmbedIO-Routing-BaseRouteAttribute.cs-1EC5A8427730E616E824E1FC3E6BE1743F645633",
        "SPDXRef-File--src-EmbedIO-Utilities-Validate-Route.cs-E9B1EC27D29820A56D5FC054590AC0573D966D93",
        "SPDXRef-File--src-EmbedIO-Utilities-Validate-MimeType.cs-AF6A10D62EE458E2642278D751B74422769ACD62",
        "SPDXRef-File--src-EmbedIO-Files-MappedResourceInfo.cs-D8EB20621175FEE1341065E9514C118584B943C9",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample-TestController.cs-8A88F5D088734F920E8C2337F208D073BAFEB9ED",
        "SPDXRef-File--src-EmbedIO-Files-FileSystemProvider.cs-3075A6883B8A3523B9D3E532F3AE70EF45E291D2",
        "SPDXRef-File--src-EmbedIO-Routing-RoutingModule.cs-949E0B8FED4A9E4C485BFD36B33FF0750B6267E6",
        "SPDXRef-File--src-EmbedIO-Authentication-Auth.cs-6B831A2C77EB039162203122D85F0609E487A656",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-Fin.cs-394F68630E024CF465C88AEA52169712612CEC8D",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon87.png-1A3FE065F6DAF4B2A22B974424FCD9ED4D2FE841",
        "SPDXRef-File--src-EmbedIO-Files-Internal-HtmlDirectoryLister.cs-D47E43B8932F686DE3DB658CDDC96679C6571A5E",
        "SPDXRef-File--src-EmbedIO-Routing-RouteHandlerCallback.cs-781125857D84BA9A2A406EB3EAE4CD1A2D9A8951",
        "SPDXRef-File--src-EmbedIO.Samples-obj-EmbedIO.Samples.csproj.nuget.g.props-5FF0C84F07348B4C617C5AC10204F5CB3AF5ADF4",
        "SPDXRef-File--src-EmbedIO-WebApi-JsonDataAttribute.cs-D0C0B4C99E8FCDD8E41005C6B3AC818D2AE11D08",
        "SPDXRef-File--src-EmbedIO-Files-ZipFileProvider.cs-E149B2AE8C127780EC9CBBA8111EC47E571072F4",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-WebSocketContext.cs-2A853F966C0B6E04CDAF892A8B5B6C3755F2B462",
        "SPDXRef-File--src-EmbedIO-Routing-RouteResolverBase-1.cs-C1CAFAD268B30C267D0186F404395FA26EDB40CF",
        "SPDXRef-File--src-EmbedIO-Files-ResourceFileProvider.cs-1E6F10E731B4107D223E14E6A81CF5824677378A",
        "SPDXRef-File--src-EmbedIO-Sessions-SessionProxy.cs-547DA34408AE7ED7B9EAA0B19218246EB433637D",
        "SPDXRef-File--src-EmbedIO-Utilities-ComponentCollectionExtensions.cs-03B9BBC376B7368600D1F1504018AFAE815DDB86",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon29.png-147EB8E13C1EE1DEA60C84C6E3394A1A037C6C95",
        "SPDXRef-File--src-EmbedIO-WebSockets-WebSocketModule.cs-C6B4C270A61CB1C72DEA32B7F519E9D42E4EA6DD",
        "SPDXRef-File--src-EmbedIO-Sessions-LocalSessionManager.SessionImpl.cs-3A6FF935622E952FC22F9CFB0EB71711785EFE15",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Info.plist-15BC604B058BF7F75F20E11CF664826061DA5528",
        "SPDXRef-File--src-EmbedIO-Routing-RoutingModuleExtensions-AddHandlerFromTerminalRoute.cs-AA9C8689C32B64BBE97DF668984D77488E22614C",
        "SPDXRef-File--src-EmbedIO-Routing-RoutingModuleExtensions-AddHandlerFromRouteMatcher.cs-8342BF0CDB86310ED9E13FA4669A6F6D0360CDFE",
        "SPDXRef-File--src-EmbedIO-Actions-RedirectModule.cs-894870F286521B03297A79E3D6EF50321D33CBA9",
        "SPDXRef-File--src-EmbedIO.Samples-PeopleController.cs-4E7D38FC72595E0B482DE996A1BDDE347DA4020D",
        "SPDXRef-File--src-EmbedIO.Testing-Resources-index.html-DCD15194C04C8B5BBF04B91B76D826F57B2106EC",
        "SPDXRef-File--src-EmbedIO-Utilities-UniqueIdGenerator.cs-4F27C8430AAD12EA4394634F4F04FF89F955283B",
        "SPDXRef-File--src-EmbedIO-Utilities-UrlPath.cs-6E35F54BEA91898E839D63DC33B43DD093B1B210",
        "SPDXRef-File--src-EmbedIO-Files-FileCache.cs-60E24E545BE4C937BF7991A70A0F912F4B9118F2",
        "SPDXRef-File--src-EmbedIO-Files-DirectoryLister.cs-424A7B00404FBCEFDEC52BF45F41B57AE46C3E21",
        "SPDXRef-File--src-EmbedIO-Internal-CompressionStream.cs-9FA51CC81BD2D0E832A17CA4F435199EF08A76A3",
        "SPDXRef-File--src-EmbedIO-Security-IPBanningModule.cs-C1F2635FE979A672EB4379E97B74ED0D06C13C81",
        "SPDXRef-File--src-EmbedIO-Utilities-Validate-Rfc2616.cs-E5BD60C42AABC9FF462A3957808FA83AD1B42926",
        "SPDXRef-File--src-EmbedIO-Utilities-HttpDate.cs-DBD6883708B5D76047E591E0D10769C83E6F00B7",
        "SPDXRef-File--src-EmbedIO-Sessions-SessionExtensions.cs-450F7C95D8A2FFAB20CC80AF18027FBBC0AAB32D",
        "SPDXRef-File--src-EmbedIO-Utilities-IPParser.cs-16DB32AE6753B198D4BAAA11119A3F1D1851707F",
        "SPDXRef-File--src-EmbedIO-Utilities-IComponentCollection-1.cs-44D14DEFF23AC54273F918F061747A374E90362D",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-WebSocket.cs-8DB694E817F1C00A4C36F6E67CA5E5D81CDACB2A",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-Rsv.cs-5A0E27CCCA7E0EF17C46227D9BA50CDED08D06B7",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-WebSocketFrame.cs-A160263FECF84504B00FF6AC9D0E660CAB840B27",
        "SPDXRef-File--src-EmbedIO-Internal-UriUtility.cs-DE8492E7D9937E17DACE1DD302043120E08EA6DB",
        "SPDXRef-File--src-EmbedIO.Testing-MockMimeTypeProvider.cs-C81962DFFD1719D37D2DB4003FFA4C7A81EA17B4",
        "SPDXRef-File--src-EmbedIO.Testing-MockFileProvider.MockDirectoryEntry.cs-2E22CE489C2B297B5AB123D960FBF2723B410EED",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-mipmap-xhdpi-launcher-foreground.png-2F73781A8C83456EA59236E3B809AE5755C9A9ED",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-mipmap-xxxhdpi-launcher-foreground.png-4FC24377C958104A87312919B3061F8D8CAF626D",
        "SPDXRef-File--src-EmbedIO-Sessions-Internal-DummySessionProxy.cs-0239BC39BA80FFE4DF64BB66BA911101666F79D9",
        "SPDXRef-File--src-EmbedIO-Sessions-ISessionManager.cs-5FBFA62BA236910E7D8A1BB35D8DAAF1D4BF8D1A",
        "SPDXRef-File--src-EmbedIO-Utilities-NameValueCollectionExtensions.cs-6497F79B474E7E331BE628A227472C47F990C9CA",
        "SPDXRef-File--src-EmbedIO-Utilities-DisposableComponentCollection-1.cs-7A59A7BC9CE6863FAA09B7E5386BE18FB1714F88",
        "SPDXRef-File--src-EmbedIO-Authentication-BasicAuthenticationModule.cs-11498E8CA2A06E7651F6539BC4F96F1564613AB2",
        "SPDXRef-File--src-EmbedIO-WebApi-FormFieldAttribute.cs-B0296ECF0855AFAA8A885A74CD4C6DAFD3456A4B",
        "SPDXRef-File--src-EmbedIO-Routing-RouteAttribute.cs-F16ABD56540E4B8317FD32FF677200400BC69130",
        "SPDXRef-File--src-EmbedIO-Routing-RouteResolverCollectionBase-2.cs-62FA470FCBB9BD3BAAC62FD513C97BA80C36AFE1",
        "SPDXRef-File--src-EmbedIO-Files-Internal-FileCacheItem.cs-36B6871B0D33D86053346D38D08247D3D982CC01",
        "SPDXRef-File--src-EmbedIO-Files-Internal-Base64Utility.cs-63FD0FCAC1B9B12513CD363FA341AC9E7A56E3BB",
        "SPDXRef-File--src-EmbedIO-Files-FileRequestHandler.cs-9AF6C07DAEA38973B93B1E5B65DE15CA4B5CA8B0",
        "SPDXRef-File--src-EmbedIO-Actions-ActionModule.cs-7BEFE6D9A8752A6A1C6351D3106326A692625837",
        "SPDXRef-File--src-EmbedIO-Sessions-Session.cs-D32268378AAD083AAECA74AB9134F39D959F4379",
        "SPDXRef-File--src-EmbedIO-Utilities-Validate.cs-43B0E3B7654996ED51960F4CD3600DC8BFE2FD01",
        "SPDXRef-File--src-EmbedIO-Utilities-MimeTypeProviderStack.cs-462CE85058F53C669CE9544A6FF9F47023919F5F",
        "SPDXRef-File--src-EmbedIO-Net-Internal-WebSocketHandshakeResponse.cs-432A54DB2336EF503622E3A7B1686610A23D94A4",
        "SPDXRef-File--src-EmbedIO-Net-Internal-HttpConnection.LineState.cs-A5149D55264A1A2404D98B5782A68E7B60369A54",
        "SPDXRef-File--src-EmbedIO-Net-Internal-HttpConnection.cs-3C76E903A429FD0AA5C0D754F45963DF6FD4F321",
        "SPDXRef-File--src-EmbedIO-obj-project.nuget.cache-19E3C699C4B546B4C20E65F986802B259A243A8B",
        "SPDXRef-File--src-EmbedIO-IHttpResponse.cs-C68E02863C3BB24EE976D8A267BFEF8676790F97",
        "SPDXRef-File--src-EmbedIO-Utilities-StringExtensions.cs-D2C2717050F660EE796B114046EBB52C737F953B",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-StreamExtensions.cs-7478F2615B7356DC4AB93A18BEF1A2025F1D4BF3",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-WebSocketReceiveResult.cs-1F085C781062BE9B6C2AB927B5A60FCFC548FCBE",
        "SPDXRef-File--src-EmbedIO-WebSockets-IWebSocket.cs-76401C33D14FABDB2C85EFBC41C61EE6F374D5C6",
        "SPDXRef-File--src-EmbedIO-Internal-DummyWebModuleContainer.cs-AE23E9241696ADBE4C3BD5FF3CB4F1A743C779F2",
        "SPDXRef-File--src-EmbedIO-Security-IIPBanningCriterion.cs-83908CA2441C500E97B442D3C2DC0CCA85AC5C5C",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-Mask.cs-36A12E17D7CDFF72748A6C772CF7CA09950B1199",
        "SPDXRef-File--src-EmbedIO-WebSockets-Opcode.cs-B2D114B3E36223BB1423C11364990BE2C08A1678",
        "SPDXRef-File--src-EmbedIO-Internal-TimeKeeper.cs-2ABABB21B51D62EDB919E4BB78BA6B169870C099",
        "SPDXRef-File--src-EmbedIO-Files-FileRequestHandlerCallback.cs-8DB520B227F162E98FA8CC019DD237F152186A06",
        "SPDXRef-File--src-EmbedIO-Files-IDirectoryLister.cs-1B545A4CB45F85DE81640674A60EDFBC6F0E1D65",
        "SPDXRef-File--src-EmbedIO-Sessions-LocalSessionManager.cs-D8F3E45F3F9E78CB30A4224ACE756638CFCF35D3",
        "SPDXRef-File--src-EmbedIO-Utilities-QValueList.cs-2F41FABDC5431E6FF06877738197534AFD52193D",
        "SPDXRef-File--src-EmbedIO-Internal-MimeTypeCustomizer.cs-01C69C6C5FD354D1F072C438C12C1EA6AFC30B21",
        "SPDXRef-File--src-EmbedIO-Security-BanInfo.cs-EDAC7E5620481797503147E39E400B052FF217EA",
        "SPDXRef-File--src-EmbedIO-Net-Internal-HttpListenerResponse.cs-E81863EECF942D25CF42DA2858A14E3D75169D62",
        "SPDXRef-File--src-EmbedIO-Net-Internal-EndPointListener.cs-BE875C50B4DD80DDCA0908247C42EAFD2D8497B9",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-FragmentBuffer.cs-848AB0162310F4029CFE8C9EAD377B8E4EEA48CF",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-MessageEventArgs.cs-10C7278110965C05FD49A3AECB26C2DC55629591",
        "SPDXRef-File--src-EmbedIO-WebSockets-IWebSocketContext.cs-E1E24D8E9C588DDDAE254A3FA020CBACD367DBA6",
        "SPDXRef-File--src-EmbedIO-Internal-WebModuleCollection.cs-71448DBC372B4FFA78FDFC1093E211B1A1EB7B65",
        "SPDXRef-File--src-EmbedIO-Security-IPBanningRegexCriterion.cs-AA37A0CC3FE7B7E6D33B7072DF550CF639CCBDFA",
        "SPDXRef-File--src-EmbedIO-Net-Internal-SystemHttpResponse.cs-0549704F635F053A6A4E16D986631F2919B8F56D",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-MainActivity.cs-20254247415B1EE1FD285F1909EF0971F764B6A9",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample-App.xaml-49F7AC39122DF20E138330A1EF3F3CCD671B8858",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Contents.json-A926986452684C2C6867DF68A8B93F374883C83A",
        "SPDXRef-File--src-EmbedIO-Net-Internal-HeaderUtility.cs-E8F0397F41AE14D304DB44DA6BE4E9EBB9F2D426",
        "SPDXRef-File--src-EmbedIO-Net-Internal-StringExtensions.cs-B3DA98C89F91BBA09B4946556E7F04434CB61200",
        "SPDXRef-File--src-EmbedIO-Net-CookieList.cs-7C681EC3A7E1EBB969F522F01A701DA8A16AF446",
        "SPDXRef-File--src-EmbedIO-HttpContextExtensions-Redirect.cs-1AF90E81AE0091F06D561F59A3F887E8E5726E85",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-WebSocketStream.cs-E323F023C95D25879B209CC0583A277F42B690C4",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-SystemWebSocketReceiveResult.cs-6DEFDEE419FAEFA8934E15766B645E9850F14222",
        "SPDXRef-File--src-EmbedIO-WebSockets-CloseStatusCode.cs-9097BF6C3C8B3EF8F40381804FD082AE7C1BA3AE",
        "SPDXRef-File--src-EmbedIO-Internal-BufferingResponseStream.cs-BBDE189EA83C7A3C7B035F476B81193302E3C673",
        "SPDXRef-File--src-EmbedIO-WebModuleBase.cs-A301770EF0BE355418F3918CB0FE1F6CE76055E3",
        "SPDXRef-File--src-EmbedIO-ExceptionHandlerCallback.cs-15734682EA704CC3F5C45F7E310B97F38EA7A5FC",
        "SPDXRef-File--src-EmbedIO-IWebServer.cs-E0D7A95EF805DC74C42272FBDA8F2E68FF60F235",
        "SPDXRef-File--src-EmbedIO-Security-IPBanningModuleExtensions.cs-FD7D378AA20D235E3CF95078E04E855D597677F2",
        "SPDXRef-File--src-EmbedIO-Net-Internal-HttpListenerContext.cs-F38A6C8B8955659083564D1D0F5092C859D0B2FF",
        "SPDXRef-File--src-EmbedIO-Net-Internal-NetExtensions.cs-99A2A3950A7CDE29E11D4CE0F43A52A8F0CA5469",
        "SPDXRef-File--src-EmbedIO-Net-Internal-SystemHttpListener.cs-424D7222C5163F685AF30B3A6B46198D13B3F991",
        "SPDXRef-File--src-EmbedIO-Net-Internal-ListenerPrefix.cs-6D2C6E61133F55BC4566DBC9E7EB05D469E8EB49",
        "SPDXRef-File--src-EmbedIO-HttpHeaderNames.cs-A93E9C06482DBDD259ED6859CF5D553AA0FB9ADA",
        "SPDXRef-File--src-EmbedIO-Security-IPBanningConfiguration.cs-3DEA6A73A21EE203D4750328B74317214CD0E4CC",
        "SPDXRef-File--src-EmbedIO-Net-Internal-RequestStream.cs-D4C28863967ACF8702AF23AF1167765F36F36C7B",
        "SPDXRef-File--src-EmbedIO-obj-EmbedIO.csproj.nuget.dgspec.json-D809364263C4EFD72092DA208A08C48804B1D666",
        "SPDXRef-File--src-EmbedIO-WebServerOptions.cs-90E3E57E61AE6D73E4C73D8820AC5239AA095D17",
        "SPDXRef-File--src-EmbedIO-IHttpRequest.cs-D73E74C31EF60E59CC95579271A4C177E86C4469",
        "SPDXRef-File--src-EmbedIO-MimeType.Associations.cs-3C1C0843AFF50FCF3C3A07B69C2979A2A1F6A223",
        "SPDXRef-File--src-EmbedIO-Net-EndPointManager.cs-0A99E247936C05CD986EDC2A232E0930F71D6E10",
        "SPDXRef-File--src-EmbedIO-HttpExceptionHandlerCallback.cs-A9FB48643AE9FA537AAB847E36FC52E1EC73E92F",
        "SPDXRef-File--src-EmbedIO-HttpException-Shortcuts.cs-5171091B94BA6025C5F2E022BB021B429BE9A000",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Assets.xcassets-AppIcon.appiconset-Icon167.png-9A82E75E576BE26CAB6A5317061BF592B8F0A3F3",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.iOS-Main.cs-227EF31EBBDFB71FA84AD26C103F22B9FFBC3A0F",
        "SPDXRef-File--src-EmbedIO-Authentication-BasicAuthenticationModuleExtensions.cs-12B6E1935B9D04F0317BC74BEEC99023E4DA1E68",
        "SPDXRef-File--src-EmbedIO-Utilities-ComponentCollection-1.cs-959C99136897AD7282F490E0BD307388D633430F",
        "SPDXRef-File--src-EmbedIO-Utilities-UrlEncodedDataParser.cs-11AA87D0FD107B0209B1BB8D312F896A663FD531",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-PayloadData.cs-335372739F174CCF2086D9A1261BFB5978B7C107",
        "SPDXRef-File--src-EmbedIO-Net-Internal-SystemCookieCollection.cs-D8A73FEDD04D0F1CCCBDD9953C229436FC379E86",
        "SPDXRef-File--src-EmbedIO-Net-Internal-HttpListenerRequest.cs-3CA417680C63CD594E0A1B0F8A7856CA5EAE584B",
        "SPDXRef-File--src-EmbedIO-Net-Internal-SystemHttpContext.cs-1495705CD398B8EDAD1077947934ACC1B9933B97",
        "SPDXRef-File--src-EmbedIO-WebModuleContainerExtensions-WebApi.cs-9B74D1CB05F510D85934D78623CE14EFF22049E1",
        "SPDXRef-File--src-EmbedIO-HttpContextExtensions-RequestStream.cs-7D96E74748741E96D30D1D7670A4562F06F9D29D",
        "SPDXRef-File--src-EmbedIO-EmbedIOInternalErrorException.cs-6E158382BAF53C6AC7F3EDE8BB725BD3A8D6FB4A",
        "SPDXRef-File--src-EmbedIO-WebApi-QueryDataAttribute.cs-40BE64D2CD9CA9799DCF4D579754CACB50E172B2",
        "SPDXRef-File--src-EmbedIO-Routing-RouteVerbResolverCollection.cs-52F50BC0D841FDB0BCD58F5AFB883C857CB42105",
        "SPDXRef-File--src-EmbedIO-obj-EmbedIO.csproj.nuget.g.targets-686D765C5ADC16ABCEA1BD4C9B47ED5B5CD293D0",
        "SPDXRef-File--src-EmbedIO-WebServerExtensions-SessionManager.cs-66E40A4B4466AE24B1BE67BA4E273B096CD2F84C",
        "SPDXRef-File--src-EmbedIO-ExceptionHandler.cs-5144B09F86C7E21C9426F36567B64525766C22F4",
        "SPDXRef-File--src-EmbedIO-WebServerBase-1.cs-0F3439892463211671713CF66D5D8F2E3501A07A",
        "SPDXRef-File--src-EmbedIO-Routing-RoutingModuleExtensions.cs-D6B6439E3FEFB45CACCCD522246A788996FD4A94",
        "SPDXRef-File--src-EmbedIO-obj-EmbedIO.csproj.nuget.g.props-EC6F7168FDA0662A34E18ACC11D321AD70497CE7",
        "SPDXRef-File--src-EmbedIO-WebSockets-WebSocketException.cs-A217DA2DF273B18257426B0FAFF9B67E58766E0D",
        "SPDXRef-File--src-EmbedIO-Internal-LockableNameValueCollection.cs-FD38EAA680BF614193CDA1DCAF83D58085BD2859",
        "SPDXRef-File--src-EmbedIO-ModuleGroup.cs-CF72E341DD4A1AE28CE495005B7B9800AC11C80A",
        "SPDXRef-File--src-EmbedIO-CompressionMethod.cs-7B6F5DDB8947465F0572E2E184717A532D5B0AB2",
        "SPDXRef-File--src-EmbedIO-Files-Internal-EntityTag.cs-B9F87E7999191C2AB90A78BBCBB0C3C906BFD896",
        "SPDXRef-File--src-EmbedIO-WebModuleContainerExtensions-Files.cs-E7865D8B2F05032C601ACA87407849ECE3338A92",
        "SPDXRef-File--src-EmbedIO-Internal-RequestHandlerPassThroughException.cs-A375EFD15C924AFFAC7C30404898DCD6B1B09915",
        "SPDXRef-File--src-EmbedIO-WebServer.cs-4D9940C13D500ADD8CEA439672C0C0C182778399",
        "SPDXRef-File--src-EmbedIO-Files-FileModuleExtensions.cs-973295B692F4C0063E4403815E8EA0FA057C96EE",
        "SPDXRef-File--src-EmbedIO-ResponseSerializer.cs-B97334407BCCF2C2C61750161E333A8E1D71E378",
        "SPDXRef-File--src-EmbedIO-RequestDeserializer.cs-607678B7DEB951796C5993D42D309CAC84F6602C",
        "SPDXRef-File--src-EmbedIO-WebServerExtensions.cs-51A04499B38F83446B71A4DDA217542CF5681489",
        "SPDXRef-File--src-EmbedIO-Security-IPBanningRequestsCriterion.cs-BF0D615384B51D9457F4C6AF10F47E9743330CA6",
        "SPDXRef-File--src-EmbedIO-WebModuleExtensions-ExceptionHandlers.cs-F251E6673024AED6E423F2314ED1BA9CD31EB61F",
        "SPDXRef-File--src-EmbedIO-HttpStatusDescription.cs-97EC02E267857AE125EE23C2314A4626535E13B2",
        "SPDXRef-File--src-EmbedIO-Net-Internal-HttpConnection.InputState.cs-563EEC70BA5FA163B9FE5A43CDBEA15AA9624E22",
        "SPDXRef-File--src-EmbedIO-IHttpContext.cs-7B8B0139810C5415670673850CF60A3F5D200517",
        "SPDXRef-File--src-EmbedIO-IHttpListener.cs-76336271935DBEEA04437E67E9C8CD19C5879C69",
        "SPDXRef-File--src-EmbedIO-MimeTypeCustomizerExtensions.cs-8D3FA762C28A230C81EDE665C4A9F23648CEFA7C",
        "SPDXRef-File--src-EmbedIO-IMimeTypeProvider.cs-3FE9B0564971775B9FE87329B07AE96545450E48",
        "SPDXRef-File--src-EmbedIO-HttpRangeNotSatisfiableException.cs-BEF9FA02A44E4E555EB52E7F68E916C484777810",
        "SPDXRef-File--src-EmbedIO-WebServer-Constants.cs-EFAD1BF369D7A477FBCFCB6B8E705D36653427A0",
        "SPDXRef-File--src-EmbedIO-RequestHandler.cs-B33924C61C9A3A41E65904C6181CE315720AB43D",
        "SPDXRef-File--src-EmbedIO-WebServerStateChangedEventHandler.cs-37ED20CF883FFB29585228D3FAE319D477ABA7A6",
        "SPDXRef-File--src-EmbedIO-Files-IFileProvider.cs-AC6A8F9CB0F1CC129699B0422C6273D251A0E9B1",
        "SPDXRef-File--src-EmbedIO-CompressionMethodNames.cs-D90E78E6EC743F540F03A78143D02FB0949DE077",
        "SPDXRef-File--src-EmbedIO-Net-Internal-HttpListenerPrefixCollection.cs-5EE711E23525E05C85E51F7BC0FB761374EDC750",
        "SPDXRef-File--src-EmbedIO-RequestHandlerCallback.cs-715EC8B428D6A4B917B401B7A8F56BD1688A2E73",
        "SPDXRef-File--src-EmbedIO-WebModuleContainerExtensions-Security.cs-D2A048FA4C75F4A5701DC3BFD0F3CAE151968CAC",
        "SPDXRef-File--src-EmbedIO-WebServerState.cs-7F458912FD4C9E155D37195814E584B286C3868F",
        "SPDXRef-File--src-EmbedIO-Net-HttpListener.cs-AFAD16DB163A378A014CD45A98531533B67728AE",
        "SPDXRef-File--src-EmbedIO-HttpNotAcceptableException.cs-F8BDC3172C7046843DE83D78A63729B92945C9A6",
        "SPDXRef-File--src-EmbedIO-HttpContextExtensions-Responses.cs-0D8447FE0084C75451329953C55B9109227EC5B6",
        "SPDXRef-File--src-EmbedIO-Sessions-ISession.cs-8124BB010B6E622653708DECCAEB107345904CC8",
        "SPDXRef-File--src-EmbedIO-WebModuleContainerExtensions-Actions.cs-BB5B6B03E7452CFE3E3186F97F7998558ACAFEF1",
        "SPDXRef-File--src-EmbedIO-WebModuleContainer.cs-4A885A1EE84E095F1981F6958311657247E6AED1",
        "SPDXRef-File--src-EmbedIO-HttpExceptionHandler.cs-EF9A8276B69DD1ACC0EFF3E4C3CB04DC9D4F7D10",
        "SPDXRef-File--src-EmbedIO-ICookieCollection.cs-F93E55ED5AA46C31D7F2D148DE55086A8E0023A5",
        "SPDXRef-File--src-EmbedIO-IWebModuleContainer.cs-EA27C15E05E3B681FB46D19A9BF76A8FB683E39F",
        "SPDXRef-File--src-EmbedIO-WebServerStateChangedEventArgs.cs-422468B24055D7BD53EDFF7C9D90F114E6F42A99",
        "SPDXRef-File--.git-hooks-pre-merge-commit.sample-04C64E58BC25C149482ED45DBD79E40EFFB89EB7",
        "SPDXRef-File--.git-hooks-pre-push.sample-A599B773B930CA83DBC3A5C7C13059AC4A6EAEDC",
        "SPDXRef-File--.git-hooks-pre-commit.sample-A79D057388EE2C2FE6561D7697F1F5EFCFF96F23",
        "SPDXRef-File--src-EmbedIO-Utilities-Validate-Paths.cs-B7623C2D1BD1BAAE0A57353071686387C7519B10",
        "SPDXRef-File--src-EmbedIO-Utilities-QValueListExtensions.cs-EF6BA5BAF1A6DEA26A29F34937153B24B5E9A960",
        "SPDXRef-File--src-EmbedIO-HttpRedirectException.cs-77CF3CE828565230FB2D80065ACDB31EA26C816F",
        "SPDXRef-File--src-EmbedIO-IHttpMessage.cs-71ECAF01C18F306F423193CE760A55D210099EBC",
        "SPDXRef-File--src-EmbedIO-HttpListenerMode.cs-DE72A79EE76ED309FE198A4293D14635C0168DD8",
        "SPDXRef-File--src-EmbedIO-IHttpContextHandler.cs-2205B514F029002DBC9DBE2841338B893C3BD379",
        "SPDXRef-File--src-EmbedIO-HttpVerbs.cs-5B9FE142C4D638B3AEDCB2A3CBAEE74DB804BBAE",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-SystemWebSocket.cs-ACBDB0129BA5B963DC40461FF8E6A6F3A18D8CEB",
        "SPDXRef-File--src-EmbedIO-IHttpException.cs-554F267960791B72EC4C46BC9D1A0F3C949A509B",
        "SPDXRef-File--src-EmbedIO-IWebModule.cs-AB068B3DE1CEEAF154953BB40B2FFF188503725B",
        "SPDXRef-File--.git-objects-22-b68017778a83d4be4c2095de7f19216220d6c3-73613DB4F624BDEC25EF251CF0A50F809438C968",
        "SPDXRef-File--src-EmbedIO-HttpContextExtensions-Items.cs-815C52FB5469CB8ECC24621815FAC0E90D49A737",
        "SPDXRef-File--.git-hooks-post-update.sample-B614C2F63DA7DCA9F1DB2E7ADE61EF30448FC96C",
        "SPDXRef-File--.git-hooks-commit-msg.sample-EE1ED5AAD98A435F2020B6DE35C173B75D9AFFAC",
        "SPDXRef-File--.git-objects-14-f6b20c22d37b975f4053913a98aeb44c77ba10-2686034923FC4BBCB9283ED59F3CA36C77A22DB5",
        "SPDXRef-File--.git-objects-8b-e326380934ec272a96452f76f1eaecec2b71cb-F4ECAE6D22F6E67F2759B3EFF985437F8AFDB1EC",
        "SPDXRef-File--src-EmbedIO-WebServerOptionsBaseExtensions.cs-4F50B5C3E2758996118E6829FA04603084730149",
        "SPDXRef-File--src-EmbedIO-MimeType.cs-830EA888AB6B16AF43E3666129B3B6F409C6871B",
        "SPDXRef-File--.git-objects-8b-4f559732d4c0e0170062c028f140dc28d3b89c-CDE721AE6EB3BDC1A535186E2F778D6E46975D49",
        "SPDXRef-File--.git-objects-40-96f58843a25f53cfeb7da8cd4d7793ff8fe949-105388DBA2D5F5CEEBE06F3DA8BC78044CF08AD7",
        "SPDXRef-File--.git-objects-82-f21cffd6be8b9ef5329d2a5734a1482a202081-12C44C49B262A5781A0ED35D7A7AF6E4B4E2979B",
        "SPDXRef-File--.git-objects-85-24768f8d764da7e9c452a444208708f2d18ff1-DD853C7C944C6B8F37F0F2C720660885DF155CF0",
        "SPDXRef-File--src-EmbedIO-WebSockets-Internal-WebSocketFrameStream.cs-C30B2F9B3F76090DC5006D250DC4BB1B159E1D7B",
        "SPDXRef-File--src-EmbedIO-WebSockets-IWebSocketReceiveResult.cs-7774B1D8E361007C51ED305170ABC7E5385CF9E7",
        "SPDXRef-File--src-EmbedIO-Internal-CompressionUtility.cs-A0F9D95E25078B281FE060F20F35A6128041E8A6",
        "SPDXRef-File--src-EmbedIO-Security-Internal-IPBanningExecutor.cs-BFC05974CB03BA06D7F387726E0CFDDE1A74B0F4",
        "SPDXRef-File--src-EmbedIO-ResponseSerializerCallback.cs-06CC60712FB5D045AD49E3EC22569FF0710E2800",
        "SPDXRef-File--src-EmbedIO-WebServerOptionsExtensions.cs-121655B5B4EB898EF981CD3C73E08487AF8BB16D",
        "SPDXRef-File--src-EmbedIO-HttpResponseExtensions.cs-FB6280EF54E62960E46C50938327A21219F83B54",
        "SPDXRef-File--src-EmbedIO-EmbedIO.csproj-FA8F37C77C648207EAF03846AE5B2A90AC360515",
        "SPDXRef-File--src-EmbedIO-WebModuleExtensions.cs-76D19AF56725B99AA5FF2F97526835FE74BC1250",
        "SPDXRef-File--src-EmbedIO-HttpRequestExtensions.cs-C03FDB5A7AB4D3F0AE96257075DBCD0440D55537",
        "SPDXRef-File--src-EmbedIO-HttpContextExtensions-ResponseStream.cs-4930A9A82799163B6B449B4F4E243AE0032BC3CA",
        "SPDXRef-File--.git-hooks-push-to-checkout.sample-508240328C8B55F8157C93C43BF5E291E5D2FBCB",
        "SPDXRef-File--.git-hooks-pre-applypatch.sample-F208287C1A92525DE9F5462E905A9D31DE1E2D75",
        "SPDXRef-File--.git-hooks-pre-rebase.sample-288EFDC0027DB4CFD8B7C47C4AEDDBA09B6DED12",
        "SPDXRef-File--.git-objects-8e-4bbbdc2fba6390c5a82e9bb36f4c60b47f089f-07966880949CEF0EDC03DC56A7A00F5A55EED85D",
        "SPDXRef-File--.git-objects-8b-5c1a9807ae2f721e23997ca487e90cad227069-F486509816242F9665946318F1EECD48CFCA3453",
        "SPDXRef-File--.git-logs-refs-remotes-origin-main-9B15C53EF538984A5B37B6F8249BC00681FDC628",
        "SPDXRef-File--.git-objects-7a-8c4afc35487f01395da18c080373c3649e9f13-D9DBBA639D950069DF682100E4635DE862BBD89E",
        "SPDXRef-File--.git-objects-78-aa18e9c5d20bb98a218b5ba8bb6a3dfd92168a-6E97A4F03381C551723340C716274BCEFBEC9AD5",
        "SPDXRef-File--.git-objects-49-12ce2a03eff94fbd2690afedcd28156a0e9c72-D86A08A8DC5D964A06F5FEE8B5DBC2B63654A240",
        "SPDXRef-File--.git-hooks-update.sample-730E6BD5225478BAB6147B7A62A6E2AE21D40507",
        "SPDXRef-File--.git-hooks-applypatch-msg.sample-4DE88EB95A5E93FD27E78B5FB3B5231A8D8917DD",
        "SPDXRef-File--.git-objects-40-6dda207f3f0211b89a6c1f3efff1d89993e7e1-B755A8CBB50E5DCFD2F45A6A3F857DDAD6CE0943",
        "SPDXRef-File--.git-objects-82-d6905a9136574c8835fa9861c7d38d97a06497-D0C151DD821F1D08B486A140096E40C5EB9C8B9E",
        "SPDXRef-File--.git-objects-15-5632405b4e73b545b75921dffb224e0b3066d2-927BBEC5771076A4C6D20AA44E8879A1588C5D2C",
        "SPDXRef-File--src-EmbedIO-Net-Internal-SystemHttpRequest.cs-1D332DD0E233F71178129749473E067266227E4E",
        "SPDXRef-File--src-EmbedIO-Net-Internal-HttpListenerResponseHelper.cs-03231A005A5E1D8A2E881A86D6921E12125727F9",
        "SPDXRef-File--src-EmbedIO-Net-Internal-ResponseStream.cs-76B649CB4A988F5890252D0D8A70837378970224",
        "SPDXRef-File--.git-objects-40-22825bb1eaa82fc43a4512a1bdd3c75d0fc984-275357BB00A5D1F6EDCE06B644CBF3AA9CBEE629",
        "SPDXRef-File--.git-objects-82-e7b5a86172146b5ccf4c51cdfecd969181d8d5-5AF652C6FDAEA1473F8672C31035799925F2F0EF",
        "SPDXRef-File--.git-objects-8c-f6583ad053891ae6463439ac5018a37d9d32ad-F68B757DB7C311C04183F0072B11706FEF597D88",
        "SPDXRef-File--.git-objects-4a-19aa31892f74415235750dc6995f94529e7f68-DDEB080C79C89388C8DB15599228C7273366F32D",
        "SPDXRef-File--.git-objects-48-b89a73fc16a815dfd14ec100dd74f2d1433f41-F1FBBE99F250BCCAA877D187C93B72075D72C773",
        "SPDXRef-File--.git-hooks-fsmonitor-watchman.sample-0EC0EC9AC11111433D17EA79E0AE8CEC650DCFA4",
        "SPDXRef-File--.git-info-exclude-C879DF015D97615050AFA7B9641E3352A1E701AC",
        "SPDXRef-File--.git-objects-13-4493ca8dc5be15f5571cc597594c7d3b7603c8-BEB6ECAE704D9D4F735188CEA80B1F28703CF6A4",
        "SPDXRef-File--.git-objects-2e-058febbed10cc48679d3a5f2216addf34445be-3305CF4DAC2E650D6DCE205459F60B798512FC64",
        "SPDXRef-File--.git-objects-49-54a4bd33f613d45f74dc0b12beb516e3b38661-9F630DEE5E770C12056D9E255DA1AFF77CFB0FB1",
        "SPDXRef-File--.git-objects-1c-8121d20cc700d5f25ed9b965129bc53b3fc3f1-4229DAB481DE29B0419683F951C20AD4A53FCF43",
        "SPDXRef-File--.git-objects-8d-60b7bf878096291c3e573c4a5c00a333997d83-431790DC951A7A08C588BDDC3DFAD0F9B214090C",
        "SPDXRef-File--.git-objects-84-4dfe544ec4a28824bf6aab870a7456dd76a6e3-D9E1D239C0CAE46CD1B1DE5BF6CD57297ECC7EC8",
        "SPDXRef-File--.git-objects-4a-3feca51a7f4468d4c1494eafbd11a0c9a9c14e-42608791263ED6C00A39A990230F2A5B33BED1AC",
        "SPDXRef-File--.git-objects-48-8f6d7a8aa2969d39b266a66f75c5d639a2f91d-1D3DCB2A14ACE19EB08B82C2CEB2B6FB57E279BE",
        "SPDXRef-File--.git-objects-83-c6a439f9b12c5976e3ed0dc7f12a7d72646091-D76A365D9666ACD85DD4726C0E1393C7A5791195",
        "SPDXRef-File--.git-objects-46-23ca2c42f2a8574089377b0419413605ae977e-27D5BAA57E02582E97D2B04AD8F35391B329C6AB",
        "SPDXRef-File--src-EmbedIO-IHttpContextImpl.cs-A7C26F7CBD480FE65A6F9F4D835AF22836ED864C",
        "SPDXRef-File--src-EmbedIO-WebServerOptionsBase.cs-C0B33725C9CEA894BF362D5D5F2580B8568D372C",
        "SPDXRef-File--.git-refs-remotes-origin-main-E5BF3C5736D4F68163E281808DE5E0AC65AFC026",
        "SPDXRef-File--.git-hooks-prepare-commit-msg.sample-2584806BA147152AE005CB675AA4F01D5D068456",
        "SPDXRef-File--.git-objects-25-b3a089566547173879931648a95483811de9bd-36BD7F543B986A632E65E7A55525DB53F1ACD9DD",
        "SPDXRef-File--.git-objects-13-27c41ae2d5b804bccda3757073a0339e13d15a-B5AD28567CDCB9AEAFF3FB5BC01D3165681BF6DE",
        "SPDXRef-File--.git-objects-2e-23fc099b9ed3100f214fd11cb31eda2fa38644-D0584A3C7E60FA446FDD08EE362829414786984A",
        "SPDXRef-File--.git-objects-49-90be937e3b0247c2c4480e54f8e2965812717b-CCB45A7B982E34F44E73F80BEB3B3ED0944D2D73",
        "SPDXRef-File--.git-objects-4a-5dd9804f46b5248293e4142d4a3749ae46d5d6-41EB3EE2D4E57688BD08AF77F953D8FDE37D2021",
        "SPDXRef-File--.git-objects-48-f4f8ff933c02ff45f2e73f8cf8eaa63d00420c-0C8BADBDF2CB462864F78E4B9364946FE5EA11C9",
        "SPDXRef-File--.git-logs-refs-heads-main-51885E9A0EA7B843016A78BC28F685FDACE4149B",
        "SPDXRef-File--.git-objects-48-04103afcde4de502ae993a0e77e290577ebeda-6D683E5944DF121C375E203C691DDFB48CD2E62E",
        "SPDXRef-File--.git-objects-76-9b7df43fd02ecbe7374cff9ed95747f61a35ec-C0C9D48373FD460F1C3045C031955F72901577F3",
        "SPDXRef-File--.git-objects-23-d5c7d6f7ad684805e5b908090b82a1674c062d-AF07FAF456CFFA69811A3D99BD530C6DF7019803",
        "SPDXRef-File--src-EmbedIO-obj-project.assets.json-58661AA7C1A5C39B8F1148EE50367CE96BB84510",
        "SPDXRef-File--src-EmbedIO-WebModuleContainerExtensions-Cors.cs-CEC21F99ADB544A0B2040F57B2A586B5DB0849B7",
        "SPDXRef-File--.git-objects-83-a62692e5cc1228586422d7cadb8f42a3cf60a4-2BF49B602218A8F8ACCCA0489458EF7E8FFDA5EF",
        "SPDXRef-File--.git-objects-46-81474d9f40c80762f5085b34dc8eb5b8aa77fe-FFEAEF741019E318AE50AF2C17836BC852BDF04E",
        "SPDXRef-File--.git-objects-1d-39224a77e24bd641a2d59d1dd105c482d30d94-44C6F1F52395D984206A5B948811EC002846D698",
        "SPDXRef-File--.git-objects-23-0f3915f52d56d49128cd95e079c59f5903fa39-E35ADF0CAE14E05ACB6102414EA4F873CCB76A5E",
        "SPDXRef-File--.git-objects-ce-506ad914f63e8dbec23553a798d088a0deb639-B778DB592549D1AE2FB8F15076C495971A468357",
        "SPDXRef-File--.git-objects-f6-8382d9a9ca43528a728261ee45de2aa80ecec3-9808F94C1498584954A43BFA1878C547AA96859A",
        "SPDXRef-File--.git-objects-41-a13315b64894264c529fd1be23c11e831f8a8a-E1162835BC95B22EC2873D13DF6EBC442E1C9E44",
        "SPDXRef-File--.git-objects-46-c1de36b6dff9a953ca4de9fd5a1e4c5e26004d-AA3671B7B5BA3B0FCDCAA56DC72CD6BA78F8EB77",
        "SPDXRef-File--.git-objects-f8-4cca1ff7565ad112d6bd212e9e63e9705ee11c-FD2A915309BAA1E5286DE93741315171CDF37260",
        "SPDXRef-File--.git-objects-41-76e4c7c0de23202822bae484309e475fd4dafc-95BD4E417F993E89F5E1D324D4226FA900E1E318",
        "SPDXRef-File--src-EmbedIO-WebModuleContainerExtensions-Routing.cs-82E3EFAEBE5E01A135B16B7F36AEB27CA0BDB2A5",
        "SPDXRef-File--.git-objects-f8-4f47e4603dc1d5c09fe9a28c0d5883e553081f-B7C7EC4B39D12987CF674575641310A9C3BBC18A",
        "SPDXRef-File--.git-objects-f6-848923066d0d9e8a55e3f1d7fd22c9358966ee-647C2E72A24E7F0C6252CFD8003A0EA0671924BD",
        "SPDXRef-File--.git-objects-c2-66a35f2055726f2048838a3a0765009d7a33a3-EFF64765358F437EA60B1EC0A8A96A8EB676A85D",
        "SPDXRef-File--.git-objects-f0-d9bf83b9dbec484a23b1cd74cdd99c558dd779-269A11BE3A256E7D03412EDFC6F2BF80395B9DB3",
        "SPDXRef-File--.git-objects-cd-40ded42ac7df298f8926951475b71991855c1c-96ECF8BEA993ADD0A273AAD554EC43E071BC650C",
        "SPDXRef-File--.git-objects-70-e55aa33f8e130a8c11d12b50d4f766435196b2-03151E0310DFE9B30901203A23ADA0BEA4E7AD12",
        "SPDXRef-File--.git-objects-83-97e1be564278a79c76f5f8225c6c4a87cec0c9-2F733804E95B0A8B4E3D6BD524AC3319AE7E911D",
        "SPDXRef-File--.git-objects-7a-3de94ebb93e9de9e04263fdaae4c4f216fdb1e-BD84F15C82F608F21861BDB634DCA98ACD63A434",
        "SPDXRef-File--.git-objects-78-4c51a07b985be8b434a029c247e0df45ac16e3-AFAA77F740A07215C8FFECE158FB749EDCA90314",
        "SPDXRef-File--.git-objects-1e-184d0f62d6076d987f30b050351a5f6232d66a-E88F0AC6D68DF9AF1E62C619226AABB33FFC68C0",
        "SPDXRef-File--.git-objects-1b-bb04d9c63d0f492140ae206300d5a85b3805d6-DC774A962EF689F7F5BE715EE82E78C6994578E7",
        "SPDXRef-File--.git-objects-46-8f8d64e672a105304d99c6801dc0dac35f672d-0289D0250864D57E8D3ECA4CA7B691C474FD8FC3",
        "SPDXRef-File--.git-objects-cb-30f20b1cb6d72c3ce39064e08ee66d1b9e8756-D965E24A43C6E070C5FE72B54549F80A33E992C9",
        "SPDXRef-File--.git-objects-ef-c54c56371cb252455c157eec636b2a93d5e9b9-433308710AABDCA006A16B1DE3D757B6DADDF323",
        "SPDXRef-File--.git-objects-49-08c6480db2407cb0d0e046880c4ce1d8c62d57-B1DBF78E72A550B04722F42ABA3D86509852003F",
        "SPDXRef-File--.git-objects-2d-4f49d1392b9993a14dbd9a6043f00f73d24dc8-BA6EFAB9852C65D7E8E9AF3B083FD338262095FC",
        "SPDXRef-File--.git-objects-ff-9c70cf08fbeb8935d2c1f0832dfc9490a92b18-003929E8B3833C43B0F46B24048B11F8B03020B1",
        "SPDXRef-File--src-EmbedIO-IMimeTypeCustomizer.cs-34BE28C8E52BDC32C37AD2E575BD97D377EF929C",
        "SPDXRef-File--.git-objects-f9-a3876254b85e9392fdb44603c831cce584d032-7124F7DBF267DE0A0733DB141175A246DF5750EE",
        "SPDXRef-File--.git-objects-79-d1525b06c3ced047bac78eef6268957e7f35f0-38078D4564ADCE03396C596BCCEAFD08ED892DCE",
        "SPDXRef-File--.git-objects-f9-53c6031ff2e4024c871c4b4257a06a6350296e-0330CF07B15FB432F1A9567C3D90A24E4F59A552",
        "SPDXRef-File--.git-objects-e6-29d32fb3923463240f08f2e3b7f65061fd3121-C0ACE80BF2876DDEC7D64097E343266419039CCE",
        "SPDXRef-File--.git-objects-de-bdb5aa66e43a5bcc11052d0b48869031b8c5d0-E52174F6AFC6B61C172EC2741E200C5F3DA3A316",
        "SPDXRef-File--.git-objects-76-5b01eb0316ea20029aa92af7d5026258388a2c-1E06F1F87678ABCE83E6F21B34BD61E571001BFF",
        "SPDXRef-File--.git-objects-cd-d989c9ad4bf2cfd7e7828c312e08a1bc1336c4-AEC3C13F484392B31962273176F3701C5633FDEC",
        "SPDXRef-File--src-EmbedIO-WebServerExtensions-ExceptionHandliers.cs-195FC076B0899080F9A4409E545323F4BE2216B2",
        "SPDXRef-File--.git-objects-e0-bcd0ded55d19dff343e30022f5ada0881ca1c9-84B6E78ED4D91F2007DBE47A115FBF5DBAF3E1E3",
        "SPDXRef-File--.git-objects-ce-eff171df1cd584ca71d2f0d73246ff975b9d8e-D21DA991347941D817C794F96CEA888EA79AE22A",
        "SPDXRef-File--.git-objects-e1-00eed178c3ed93ef4daf204b340fac70778c9d-CE83EBC372507EC21BF984D6264B964545822381",
        "SPDXRef-File--.git-objects-4f-71816b1ea94c58e0630ac30d042513516de240-4A199A2075BE946CC5F48A359F36A565005A3C29",
        "SPDXRef-File--.git-objects-a1-003064c8a21118ce526e027b1f5b8af3263c7f-ED3BE933729BC5B6AEF42308D2DFD194D7E15CA7",
        "SPDXRef-File--.git-objects-e1-33f1433cb175b5ae24c3e9e8f2168783008651-ACDB7CE441E17A38A7689C5E964C5524900B9270",
        "SPDXRef-File--.git-objects-b7-92aef01e9ed95cd525b13e45497c99979d188b-EFFCC6CF92DA0400BC42F8758D6328B3F1CD1FCD",
        "SPDXRef-File--.git-objects-de-061bbabb8da6127a8d5395b90094e8a5f08f39-5649CEF60544FE140AD839AF7F94E2AECE78C206",
        "SPDXRef-File--src-EmbedIO-RequestDeserializerCallback-1.cs-B40EBF32C768E8E4E5449B7B3ED603E9918CDBD5",
        "SPDXRef-File--.git-objects-1e-01cde7e5017bac640e0bda431eebf9b851213c-BB0DCB83AC78DCE21D05A8804DC04419B1280B1B",
        "SPDXRef-File--.git-objects-b0-81e2dc5919b3c2028d75baa33abfc4c22de55c-1B5B8B4C1D44AABB90DA604097CA160D445B7B01",
        "SPDXRef-File--.git-objects-d2-f4105a037859fb64663ddf638db8f4decc6ff5-7CBB96EC58419C4BC1AACD5AB00D085A39F47508",
        "SPDXRef-File--.git-objects-e9-a3005f78316cb795962f9c108275e2d88b173a-ADDDFD1AAC242767FD7A38CB9D2124BB9B96064C",
        "SPDXRef-File--.git-objects-f1-2b936801327075f89d691b4eb1bbb4b9d23a27-6CDF40F6C8A969291188212BE702C50E66A13BFB",
        "SPDXRef-File--.git-objects-a6-8abee71f2f7625cba6aebf416011b0af5860a6-D5D2D428DE2877A12B295277B6950170697B6369",
        "SPDXRef-File--.git-objects-f0-2fdf2cfa74ce2fd2e9bfda537ee71d39a26483-E561A6883226826DEF385107B474033670758255",
        "SPDXRef-File--src-EmbedIO-HttpContextExtensions-Requests.cs-83795493BC2A7052405C3F660523CE6CA448D3F3",
        "SPDXRef-File--.git-objects-f7-bedb658e009fb2d28bc73baec56dd56e189fad-AE1035A896877D6A3E0F898563385EC6E077E326",
        "SPDXRef-File--.git-objects-a8-9e5bbce622e5899ea4efd719a94e96dac1a9c6-0B7EAD389CC6BFCC5409AC5BF42A6A1B147085A1",
        "SPDXRef-File--.git-objects-dc-90e5a1c3aad4818a813606b52fdecd2fdf6782-DBEC4322CC14DB0262D878F03B2527061D5AE1B4",
        "SPDXRef-File--.git-objects-de-4992f2e32f0622799940704b4109eeed80b5a4-CB9878A274E7B717DE1D77DA74ED556845A8D268",
        "SPDXRef-File--.git-objects-48-d8b21277694ba0df37d5919547546c8ae89f38-016E9E34186B4150A8D7601B61B5E920D2271458",
        "SPDXRef-File--.git-objects-b7-e21ce377fee51018796d4183c3cba2629f819f-3A293AC81D93024409E88600B0E08E3D3FCF2CC2",
        "SPDXRef-File--.git-objects-b7-8133f0f0115ed31f8bc255108c0234f36e1dd2-AFAF0074E96AE9FFB55B3BC66C1467F595795339",
        "SPDXRef-File--.git-objects-cc-7edcf5cb47d55bcd90dd20694555e7cc40e08f-46A6EDFB651036C7F6A6385C449D43F4D0FBA852",
        "SPDXRef-File--.git-objects-a7-24005fd19facf45415f22cc5f8f1b529459072-F2A7807A0E23A56FE11589C14271092FEE770FCB",
        "SPDXRef-File--src-EmbedIO-HttpException.cs-4D4941763D0C55F2CA959DAEC3EBE089FC0239ED",
        "SPDXRef-File--.git-objects-d2-490d1b1306a0cd92d2e81c6949c3bcf5c1e5f6-69A0A41EB15BF763D2B36DEA5D45E5B5B936C8D2",
        "SPDXRef-File--.git-objects-d2-9a04096ab91f7f789b5234d6852de224fe6bd7-0C447F6E3802B580A7FBB962CA430C9AFA3282AA",
        "SPDXRef-File--.git-objects-2d-d52620a8f15577e56ec7fe8e671988dd17ab0f-DB5DE2ACB1596F9A45C426C43F68C8A30AD514B2",
        "SPDXRef-File--.git-objects-c3-18aa5539a8dbbb1c1f85e85a6acd4f05e1d400-ED278D97D0384764CB98E424B32CF29CA1247129",
        "SPDXRef-File--.git-objects-dc-975456f5c4af0b3b11c0d5da664f59c8239016-07E7CE4ADBF37F9D00A593FF9D7143B559BF5C45",
        "SPDXRef-File--.git-objects-0a-a540b7932524b4e02676e44389453b794f2f26-DAB34948E0BE0EA4D58835287723A4A12CC9B39F",
        "SPDXRef-File--src-EmbedIO-HttpContextExtensions.cs-1167C2CB9490E89B02385A9AF366BD83D681E144",
        "SPDXRef-File--.git-objects-46-da20c9250e04579dc6e6291f4e9e8148e6190e-BF987DBAAB18CC5C49D461A1A7C6583A9D1D09E9",
        "SPDXRef-File--.git-objects-b7-4643c0aa3e30cd830d8c57a6612cade727411c-ED91B6CBFFC2D14E80D1E7B3C89581B3C7C72672",
        "SPDXRef-File--.git-objects-de-f936f1bfed3ddfed3d626acab871f595cd9392-C3D8813FBF1640D8213CAD9237E9CD334F62B9F5",
        "SPDXRef-File--.git-objects-dd-4790ab8cd88bd66af0de793bc62c2030dc4af7-A9511D9508CB0A1D2A618626FA152C1C7DFF1B2D",
        "SPDXRef-File--.git-objects-a0-07ca16a55bbf19e9d27946d908a3a98dba8b3c-3C687C1CCE5100BD1A534ECF34FB33495F2D5BBB",
        "SPDXRef-File--.git-objects-cc-fefbda065e407747a25216c2d6e1f17419e2dd-C2D722D9946DDC52BA71FEC8A2762F8A938F9C2A",
        "SPDXRef-File--.git-objects-db-d45aa0e287d8dced8515d6e03e56f0fd120641-AEB34D0323163EC470F160ABA6BBAB6CC5AD14F8",
        "SPDXRef-File--.git-objects-a0-89dca8d4c7cef5c09d00d62218d1c2210389d7-DFAC59145F986830C42E200B801A7655A2AC2709",
        "SPDXRef-File--.git-objects-52-9e4f0b7556667e996c88f291f267eb0e1b2d81-876329D855C9C3DD43DE5DD7D8E9488344BE2E93",
        "SPDXRef-File--.git-objects-0a-c44cc94d635346746334212ba5d61f9a193cd2-8ED6B93AA79D85B736195FBC03C8172143D5B7ED",
        "SPDXRef-File--src-EmbedIO-WebModuleContainerExtensions.cs-9027B934CF6767645E7AB6BB2AE86244D3806D15",
        "SPDXRef-File--.git-objects-af-0cf314346ef4a61cacc5339ea277155af2bd97-523A7E9A731BA1509E2A033E08E388FBB0F6B375",
        "SPDXRef-File--.git-objects-99-94e4a66e6a807f29e4be7b5b349174717361ea-C240C2BC3F2F4BE798BA60A411E02D7DAEE00A96",
        "SPDXRef-File--.git-objects-6d-0a7667aab21f76c27cccf5a8595becc75b1bc5-9D80D35A3EF920F0108A745BA2915DE6961E1174",
        "SPDXRef-File--.git-objects-3f-405ec9f9cefc85ba080c4b520e39c5f00e8cea-1144E7B043DE08973F5D2B9A85F33488BEDD9CA2",
        "SPDXRef-File--.git-objects-0a-2ba9a7e08f48ac79034cdace33ab6beb627749-BE14F3715F3D3FE412615D444CC89EA0FED3AD8D",
        "SPDXRef-File--.git-objects-99-058ae983b200bb87c838ea08a31705428d4c52-4615E3FE9C7DDFA67D7EEC78ACF30BC3B7B77577",
        "SPDXRef-File--.git-objects-ef-bd1cff414591282ec64d882d59a1872c562f37-75C7D68FB2AE72739768E5B8BAA32B23C565C1E7",
        "SPDXRef-File--.git-objects-de-d3ecea0897e8731aa8feb8105f9d13155352b0-A5CDC29D3C1F7E742D163A61CC9DEC17789E3F88",
        "SPDXRef-File--.git-objects-db-d6bd3e8646fe4dfa515cf345cbcb30271ae103-CA3EFAB9D1C0DA9F6EBAF587ED264ED4D11B96C3",
        "SPDXRef-File--.git-objects-a9-e143e1edeece30a76f8b0a7af1a5b21a30b44f-9AAD9B8270E0177E0FAE80F88C47A3785CFFD6EC",
        "SPDXRef-File--.git-objects-b1-d5e5225332aebe4a956c7e80867c05e0163e03-7BA73D1FC4D510550D86DD96BF1810E2FD18E6F6",
        "SPDXRef-File--.git-objects-a0-0820b6bb2f62d210a6619c3da77d6e620fcc45-E950218A1D8555B7562CEE2B88307FE126893311",
        "SPDXRef-File--.git-objects-cb-ef82a6019c70849112ef4b422f238a77e26fdb-712E87B2B909B67D237A92BCD5C39D7FB1ADC3DA",
        "SPDXRef-File--.git-objects-ff-0291030e9ec348312dd981b0266802873674a1-156F0A73582CAB34E63C2DDB55E553BA00863FF9",
        "SPDXRef-File--.git-objects-e6-18c9a896abd064d7b1ff16c9b59438c9617e04-760F1AA62EF117E600C91BF64FC2E146FCC455B4",
        "SPDXRef-File--.git-objects-e1-295ddd417893060355de1f9ab81da0df6450a4-1D9AD620FFBC59C90828BDD7E9E2B4523875BB42",
        "SPDXRef-File--.git-refs-heads-main-E5BF3C5736D4F68163E281808DE5E0AC65AFC026",
        "SPDXRef-File--.git-hooks-pre-receive.sample-705A17D259E7896F0082FE2E9F2C0C3B127BE5AC",
        "SPDXRef-File--.git-objects-d2-47ed4ddc7bdafe7187f9de28bc1ff66398933f-C04C3DC4C5C37ACE53D74FB0F987B061BDDF9865",
        "SPDXRef-File--.git-objects-dc-820082a71233bbf07662a27bd96f21bae46712-C8429646C17E3861BD145AD24D5FBBDD69B115B8",
        "SPDXRef-File--.git-objects-65-95c5f0b58ff26fe9a68f9a2b5803c3552e94dc-E5B27D095627B79A39D06F0A58254ADB324AC74C",
        "SPDXRef-File--.git-objects-b6-8b28d8cad127ae30195da43a89890c850dc9e2-EEB5C40C9390B51DF7A76B904EF14FF6AD190ED7",
        "SPDXRef-File--.git-objects-a7-06cfc388cbdb86e28be52d2c8071d63c71d8a6-D249201EC79D08E460D6C14702B4C34A57E3E906",
        "SPDXRef-File--.git-objects-08-c706026c8be53988665f7e46e6262a54811a99-39AA1697B25B4AAD8525B6550E835CC8306B7484",
        "SPDXRef-File--.git-objects-98-f4d035c84dacf83736b6bb57ec979cef9fa79a-58068EC2607D5A986ADDA177CC54AF6C7866DD0F",
        "SPDXRef-File--.git-objects-6d-9458d496fa65d8ed2c773015e41ebe772e83da-51EFC67A1EDA7B0494ECF7A7E578D3677B606383",
        "SPDXRef-File--.git-objects-53-8e8e8f5bd819a977ed0f33dc320ab7e5948e03-DC12357E1B049CC2429EE3EB10C86BAAA906C7D3",
        "SPDXRef-File--.git-objects-0f-d09ac8a90bc62fedb72b9167c2091f30c16330-E4A908F55C54F4EE60D67E700A7873892478F252",
        "SPDXRef-File--.git-objects-99-e990bee490e7b01ecb6d9d5f547e44c777a554-1CEB0B842C16AFBC86E66960808BE935194D1836",
        "SPDXRef-File--.git-objects-b0-e0455455b09e26552951010e379d526074c5ca-9E432D8CE09A9C3A2A3EC9214587641DAF599BC4",
        "SPDXRef-File--.git-objects-a8-7547497d6737f0ba58176ab6a32ae471644b03-B60E11D17B5C12FD99231AD9F5B4EA993FA98232",
        "SPDXRef-File--.git-objects-bf-e00b4d030808bc6e74d9c3c8e1459552855989-2E7B8622FA988EF949F77E5FC2844D2DE9C21DD5",
        "SPDXRef-File--.git-objects-a7-a97a7521587195966eaff6bff026e5d121009f-C660C121C046AC2CBEBCD83AB90DBA156EA9FC61",
        "SPDXRef-File--.git-objects-5d-c3693e70425744edf3685ac066ea71125c8906-BE7DCCFAC3E007D0A785988434730FF1CCF8F8E2",
        "SPDXRef-File--.git-objects-08-b17580da08beeb57a83489b60b54fe6d19ec4e-D0336268AC969229F9AA41D80147F7F3A9EF4BB3",
        "SPDXRef-File--.git-objects-b7-775663957ae8c4eca8ffc39a63fd83a4186c28-70E4CF669976ED4E32072955176FFBEFB9541C6E",
        "SPDXRef-File--.git-objects-91-758a1caf203cbdda556a8564bdea24770f66ee-5FCA0E3298ACC34BE2EB97E6AEA8B12B02BDEFB5",
        "SPDXRef-File--.git-logs-HEAD-51885E9A0EA7B843016A78BC28F685FDACE4149B",
        "SPDXRef-File--.git-objects-7a-13ee182239d9670c2e937176a9417dab1e8083-A6A5E9BC7E36A01166DEEB755017FCE95BC8AD40",
        "SPDXRef-File--.git-objects-65-844a84dcc5751c148f99310f01634dda307edc-37781987FD0C7FA5E239FD178A5417E262985013",
        "SPDXRef-File--.git-objects-0a-49693804dd5fba5dbbd0dd427c6adcca3bdf66-EF15CA95BC89F095F2B323E32B8F40D814B999CA",
        "SPDXRef-File--.git-objects-a9-1b89fad4b87543b980f9774e660aecf864c12f-4999B47B3A6D45436B3650F7F89D1E9B801AB44D",
        "SPDXRef-File--.git-objects-5c-55bad0770513497c83db285cf8337311b52317-F7ABBE686C2A76711D8F193A46D586F43A60AF85",
        "SPDXRef-File--.git-objects-52-557fe02370200642bbb174c7a24a3bd6f243b0-AA099806E29512B3E447679019FB643EA55B852D",
        "SPDXRef-File--.git-objects-5d-0d1ab4c6d8041fda08c2835cfdfe1aa5da3506-655B674133672541042D3C9770695D8618CC7761",
        "SPDXRef-File--.git-objects-78-9c012d15c664579ceb845fb4129aad0f3a8a0e-08EE7F71E9D9D72CD7F77970F3B161B6AB95049A",
        "SPDXRef-File--.git-objects-5d-ccd56d08485247207f61dc3b1abb4331286f5d-FA47E256A7F2C0D0A2E9E5F2B4578C9457FCCD4C",
        "SPDXRef-File--.git-objects-98-ce67f18ea125fd3064b083e7a6ed5851818a07-E46BD477FF18E834B3B0AE1E006852D9B06842B4",
        "SPDXRef-File--.git-objects-52-226870f9e47ff3cf38c9f616571c348d81cb4e-2CBD3B04DA29A408871DAC56C78BA17032B28739",
        "SPDXRef-File--.git-objects-06-6b2d920a28db73b4ba3a0b35e6905eeeef5772-52DD2712F5B357B4E0288C9FC85BF304151221AE",
        "SPDXRef-File--.git-objects-6e-95234d819f0a2001d6fa9b744c4993b32ca173-F1E4EC666203D273DB4F3C54B401448939EA3FB1",
        "SPDXRef-File--.git-objects-9f-1ab7baf144858c03103531c66575de0f26d13e-451BC761E280D817BD217CE3343494C4C8A92FE4",
        "SPDXRef-File--.git-objects-6c-3733a6c2704bbf47e1f68bc0f03f89d9722900-60A4BE635581FD7F2FAD16066C056DA304A0BD9E",
        "SPDXRef-File--.git-objects-b8-2b8ba372aea831f97e977ced9da709d08b5ddb-00AFAA60E7812D32851DC863CBF84F9E20E9687D",
        "SPDXRef-File--.git-objects-d4-807d94335fc17e9fbce88f510341e92728d641-C42C17AC45E57F8DE269E6802AD558E62B8A24ED",
        "SPDXRef-File--.git-objects-5c-2db09fff817f090c74c6b7deace81701efca8b-0B5B798FD00FDF81AF4E24CF996C291A1D19295E",
        "SPDXRef-File--.git-objects-5b-06063bfa6c0ebcc921adf838eb733d6c182d85-876F86D382361DC6D4D9C44BABBC12FDD59F9F67",
        "SPDXRef-File--.git-objects-5c-c7ff933d039a26b84ccce2e21ad27aeaa55268-D9C5AD6C9DA3F480735590F58345E43A7E52925B",
        "SPDXRef-File--.git-objects-49-97897a8749ae476f94e737213280705ffad7e0-AB3B6A29C9580358EDCD8006E7918058885E97A1",
        "SPDXRef-File--.git-objects-38-a467821d9b4ed942991619394063cd99d5826d-906267C9EB7443F536615724DD078BAF2D9A48C3",
        "SPDXRef-File--.git-objects-91-4bc7a87413c5e37e0762e9a090db6911ae672f-AD18D1DAF2E849BC94A3A2D77D9C1ACBE6DF26C7",
        "SPDXRef-File--.git-objects-43-d58befb9bc12c19aa9a2b3d29c42a14ea16cf8-B0BC21D9E69483FBC7E93F190EA583C16873252E",
        "SPDXRef-File--.git-objects-76-eec0ff10f3930fbef3f50517528646cc6aa41b-F1298A974DCD8E370CCBA6F37747813B2EE476BA",
        "SPDXRef-File--.git-objects-5d-14883164da03104293df9cca7df36d9c07513f-82F7FE0C9FD44D77D9F8EF1306A2D9A3872A8DDD",
        "SPDXRef-File--.git-objects-30-f97a846c8b61f837481e1768de966c58f1e783-F6CBD5D81916128F51CFFC4A57DF0FA34411405E",
        "SPDXRef-File--.git-objects-63-9b33cfcddb2294fc4c4edcd254f2c0393b5755-3B4CB352DE8A32192D626B41F593D417F330E941",
        "SPDXRef-File--.git-objects-38-e3d492601ef9ccfd8cbcd0fa5cde1367dc80f7-BC99F3C17C164EED5EF0F2BD895B125EB21A8D23",
        "SPDXRef-File--.git-objects-62-48b6fd5cf57c27b7d3e8c3081d249596f1fa1f-3966455C2BBB4CB41FFA50C92BB0F19E05686CBA",
        "SPDXRef-File--.git-objects-31-1d4adc66c71152c23e7139a3b718c91cc56f89-FA585145B80A851E40EE5CBF22D917779738A021",
        "SPDXRef-File--.git-objects-9f-9158e7068d9e3170cfa82c852923221e57f1d5-E0BAF0F8F75C5B20833246C14E31A520A3CCE752",
        "SPDXRef-File--.git-objects-36-9e3fe9b578fb62fe343a8dc21780b1007edf53-E688316E9D877002336BBD0067437968FA3D7931",
        "SPDXRef-File--.git-objects-23-0a46de688968493f7c85544d6d87804c6b8320-83EB3B74D1C0089E2D23300A8C484931F0C5950C",
        "SPDXRef-File--.git-objects-9f-b383c48dcffce3a92d55cd7e83b9b58bf52766-212D5E1C5A794470CA21E2BAA29A926D35240035",
        "SPDXRef-File--.git-objects-39-bc218f57f92e92c2e5ea556b8b349e9abfb570-43F1DE28E8F1845E7B746CB398764F359FC700E6",
        "SPDXRef-File--.git-objects-09-bf398bdcbb85597e08031421cbe32c55364329-8198C8EF1CA1A09834348965965D79DFF822B53E",
        "SPDXRef-File--.git-objects-07-1407c393d88973ec45fe506fbaf9a80cb4bfb5-D19719DCA506DA693830B0E1B4E756E1808B926C",
        "SPDXRef-File--.git-objects-1e-e107937b80c2255e9b3286938d654d5ae54fe2-02BF083E7AFED6C3811F32C1D621AC10C86E6692",
        "SPDXRef-File--.git-objects-62-30bc6e4d4e1ade5a6b421f79d541cac932002b-48E2448BF840CDBCE0753BDAB1506344BBF68AF0",
        "SPDXRef-File--.git-objects-43-1a8a053d0f4af31542c02acc616834b5bfaed2-46F4313EB956FE6B6F21EB81BEE6040B614C3453",
        "SPDXRef-File--.git-objects-37-05fd785ab2eb654886cb064cc8fe0abd794268-F2C88F06483D5B72AD5341C0A7EA47D4C4E7D758",
        "SPDXRef-File--.git-objects-77-95ff5e70341d8d6cdf33ebe549d081cca22d2c-D038AB116DD431C5833941909EBC3A7388FB8767",
        "SPDXRef-File--.git-objects-43-ea378d8cc3bec50c39aa942c1ef6085abea8c5-4266B1CB11E51F39B5065A4D45AB98335279ADDD",
        "SPDXRef-File--.git-objects-9a-c40db15db5a4c84002ecd3263a7ddc9c61c4e5-1E5D497FC27FBB5714EB6370943CD15C1AEA340C",
        "SPDXRef-File--.git-objects-31-36dfa928d5ed433bbfaad94177e96084602b4f-95804871AFB185F05240E6CE4FF24CF9CB01E134",
        "SPDXRef-File--.git-objects-44-8ecec7ba64ff3b91aa1582be2475e634c00ff2-EDE7CA01DAF653907A722D7E37B8F429D9A7EE9F",
        "SPDXRef-File--.git-objects-88-d1d0a16c179dd75b13353ac96660b2bc7d1e54-384B427F10E5A0A68D85EF00E634F37C150BCC58",
        "SPDXRef-File--.git-objects-43-b54297c5094a6c8be728d4d0c4907cddc42b41-60712BA499DC921BA22C0C35D39B67C7830855F0",
        "SPDXRef-File--.git-objects-98-d85cc218f3a981b2985f247b37a8a039363fc3-563F1975FB4B71FCF621173C60A4E12049820C0C",
        "SPDXRef-File--.git-objects-91-74c989a9c8b8a5ca133228f4ed7c173fffd2ee-401422401331BAD1A7281ECD7D7C826A70438620",
        "SPDXRef-File--.git-objects-09-3c5e1b2317cfe807b8f19a492a5598efc11cdd-CC4DC442F597496A1758734228552A5253BE5F3E",
        "SPDXRef-File--.git-objects-07-88e548766a04f8f6756c110e3a4f3f06d706ae-33C6F95810661B17DEA67765383DA765E64C82EA",
        "SPDXRef-File--.git-objects-44-8d6efb577d07e227a5c62545173ddf6bd86b55-D22B18947B4D0923EFF243E8EFD65FEF7760DEAF",
        "SPDXRef-File--.git-objects-44-390ef9505b9867667f58c86c23c4cd58f43373-17FA6033E5126AC117FF35ADD6F144BC7C20009A",
        "SPDXRef-File--.git-objects-75-853f7736f22cc0ed319c5f85d3ed752a624984-3D250D5E217207B025A9CE81CA4EF77E8D3222BD",
        "SPDXRef-File--.git-objects-2d-e842e61664e60bf532ec4f9f29fdf970fed64d-1E40F73C442BC746F1F376029488B4270CF84A34",
        "SPDXRef-File--.git-objects-e0-4e579029cc7d8a220a25f1ee3311a1e75f4f2a-75B80B46C0E0D161F1F8EB678CB7201E6B61A6F0",
        "SPDXRef-File--.git-objects-75-bf4a41d5a3cc6f6dc8ba7621043763ad163520-3407FA973B5DD2E22E14ABA3A1FE01984A3B0AD8",
        "SPDXRef-File--.git-objects-26-f8f2131b852ace987d21d33b732de8eb90cf60-36E34E856F5A5179BEB34A856758BB16B73FB0E9",
        "SPDXRef-File--.git-objects-6e-24e11cc7b1eb9314ba07371b83d539185cfd6d-642DD783368B890E783C3B6898BD2F1473BEEE07",
        "SPDXRef-File--.git-objects-6b-f0288a8ad5a81e8b485e83a9bcf2995bf4d636-CA574E4B9520B957CB0FCC300BDE71B152EA732E",
        "SPDXRef-File--.git-objects-75-96b88ba91e5aa1231e6b5141d8e96214789e56-5F6E4D1A3811D7C73233A13A6B0D2BD547E9BD4D",
        "SPDXRef-File--.git-objects-2a-ac22dbc4ce9c898cc13658c6c5712ac24f2e2a-B24053129A35D212369D7BB0686D06D031A73DB8",
        "SPDXRef-File--.git-objects-81-c3a73bcd5cbf8d03b128780362f379729889fa-5F4D37FA808FC216C7930BE98A0FCE66F1543086",
        "SPDXRef-File--.git-objects-5d-4329984ed73fd9a7733b6a7dc6bb6faa7c922c-DBBBB371A677BE57CD1D4F1AFE277B4A4C187AC3",
        "SPDXRef-File--.git-objects-21-0331294bab7c07adf2b338276e5b49e829a3d0-656730DBA69BFE647B9E81CE11AD4EBB8E9BE034",
        "SPDXRef-File--.git-objects-19-5cf5363c940b925ff2e47121428940236ca7fa-5047307429479112BDFEBB293CB2981C9AF26F93",
        "SPDXRef-File--.git-objects-e7-6e34f679daae8d87f42ae6bf6142abc78d190b-1D47CE148688171797F881D09087D74B2401352B",
        "SPDXRef-File--.git-objects-fa-b8333f6f3c5600f37c0e82353f134cc7da3a3a-322852A8A0EF570D2DA72530F7DEDFBDFAC1AB8C",
        "SPDXRef-File--.git-objects-10-835b0a4e66631d5ea4a3b1793e95cb23d4cdd5-117C3F469F8384C9E11558BE94A33505F26112E8",
        "SPDXRef-File--.git-objects-8f-72f90051d65a853d6e966d7eeaa7298719bfe6-5F900AEFD5610A5AA75FB9986CC8448353D2BC6B",
        "SPDXRef-File--.git-objects-43-7ea7f279a0c487cf910b7459222a590c2ceb12-8497DF03434683C81713191E88FB2A1C850A71B1",
        "SPDXRef-File--.git-objects-43-aaec26e970e81d95ca1cfa71a05029c139419c-D0762449DD6246998A361BBD6F25D59841404862",
        "SPDXRef-File--.git-objects-2f-4729c5ba19ede08786ab9c54a8e85d8c02b795-5196323238129DB79AD0E4EFDE85D596148ABFB0",
        "SPDXRef-File--.git-objects-80-5917ce76b1e755f6edf9bbf386e6af4d606287-877818EA62A6F16E1538132B4BFF1EB624DFF186",
        "SPDXRef-File--.git-objects-26-8ce24d91c3ce205927aa6fb32d3426af5f7e26-9F0F875DC4DBE22A5959DBC1A82D786381454B04",
        "SPDXRef-File--.git-objects-cc-46710437560823b21100b32c87a5b3ef7561d8-CA2031BE987B177AE5BA79B96BBC78155B3EB19D",
        "SPDXRef-File--.git-objects-36-513d8396ad865025d1ded5296764c09f2c8cec-C8B5075F6F0A86E20D99B22F0A2B884E49AD975B",
        "SPDXRef-File--.git-objects-07-ae2e09440f43db8c0e69f8b418b051b2021a68-C934D91C7638C176E0A5DDBB58D9E3F2A63661CF",
        "SPDXRef-File--.git-objects-86-37f39e00aadf730d73240508a0a030bf42288a-0A1235B9B7BB3B7C1CCC4390C06781198F701548",
        "SPDXRef-File--.git-objects-2f-664738e78154628f58842efea70906e764a6ff-72F64C55B94F639FD9805F741AA1281AB8382418",
        "SPDXRef-File--.git-objects-21-e850a0365bf886842b7ed41b94561a53c2c601-359AAA2FD6746654ED01FD30BD6A64EEA585F85B",
        "SPDXRef-File--.git-objects-8f-b57d71f22b17fd74590038e0c56cc1c7040ea5-7F141D60B753B4311C531EF66A069E84160284E9",
        "SPDXRef-File--.git-objects-89-b4c8d57c9c7ea4c7721a48f0d0943c23d68891-5B08EA2838705DEE67FA7354CEEBB06250F2733E",
        "SPDXRef-File--.git-objects-4d-80bd0397effa27e80c73979f0497dca92b5003-C71F7CD9A54B9177DD4D7984C83306BE1DBC9B8C",
        "SPDXRef-File--.git-objects-88-6e44a20a70f88a8536578ad9e210bbc4bb12dc-558FB2F2C28AC500EF6532E86C921A1123F4A693",
        "SPDXRef-File--.git-objects-10-c217ce5ff66c7dc5fe397fb6d3b9cbb475d211-B107A0B1D817B3D0D9719064B1669647AC685232",
        "SPDXRef-File--.git-objects-81-0d1bb9c658b575fea1844979f84ce9675843da-D6D790535F4DA0A907D7C15A3401E5C297007399",
        "SPDXRef-File--.git-objects-74-ea8088930afc80485489f3c13e08e6c0c98fce-CC38AD178CDC5003532FBEA31D9AE1D17DD9CE94",
        "SPDXRef-File--.git-objects-19-63cca4d5ddb789bab5981b05abbced70dce351-7E4BE1B2392406C5BC48F4D3CD73452D98F1A15C",
        "SPDXRef-File--.git-objects-7c-8c50b9b2fc5d7fbbec5b6b76b178f47bfd3fc5-EBD79045630776890C172A04D6CCA0D77721EBEB",
        "SPDXRef-File--.git-objects-c4-d609794b44c0b65cf8dfca606f8c157d0b984b-60F0B45DAFF246876C40795D185E55A16E59CEAC",
        "SPDXRef-File--.git-objects-b0-58cae2f440e5a5875e45c036c99f1fb6356046-FFEE7B7ECA358C9C95B63B629EB16ACE602A1D80",
        "SPDXRef-File--.git-objects-45-39f7c20322ef819d1867d9b0233e77481d6540-1EAE0247F9B3C20F229FA80644417CAC0E021B83",
        "SPDXRef-File--.git-objects-2f-96ffb203cbbad36d9184c6f813d73515bf302e-B20735A775A813D881FAF83C341997D8C343C94C",
        "SPDXRef-File--.git-objects-8f-5659419f9ed5df19b493342ad54a7046bdd948-FFE7855233040AE59A73C30AFE76501E00151252",
        "SPDXRef-File--.git-objects-8f-17e4e61cf4309db5edd1b449e90001d87558c1-003EAF0BD28FE5559DD40BA9B296FD982FCBD04C",
        "SPDXRef-File--.git-objects-19-d157982df6ff45729fa3466efd19856f5980a4-08D141EBA1290C7A1B2AE67DBBE204AD91E7F708",
        "SPDXRef-File--.git-objects-16-fbd03f1e97c74ef5c949da9deae6a08da54cb4-38A921EF824D9D41CD1FD85A9C0517A2224E0AF8",
        "SPDXRef-File--.git-objects-11-7c08c7a07396625b7cae41d710d871541a5153-35064FB356DB8B9D898300A550A7A6A95AD0EF91",
        "SPDXRef-File--.git-objects-44-0c4269ae633218dc452dcb0c7d0b6665648855-47BD18BAEA57D5734EA41D66FA6B48D7BF105220",
        "SPDXRef-File--.git-objects-4d-bd71e769a317aa530dad7fbf57ec8be09b201d-DC7DAB997E55909AC13E6D6C4F0DFB3DFF4D2FEB",
        "SPDXRef-File--.git-objects-4d-800b8d9c12a8a7e2231f305894072e1007f67b-B6B9166568F86FB541C665EE817A4E72F29E2F9B",
        "SPDXRef-File--.git-objects-19-8d0598b68408adfa4c4eaab569f105b6c10763-2E607931F08A1F3EA6E10895590046D5FA77B408",
        "SPDXRef-File--.git-objects-8a-08bf75e7ac122842f1fb5d23eec66232be5c0e-237C488F71E44424BDA33BE352DED09D68FCDAEE",
        "SPDXRef-File--.git-objects-4b-825dc642cb6eb9a060e54bf8d69288fbee4904-F9ACAEAD3E977C3D0FB7AD604631D5D838950772",
        "SPDXRef-File--.git-objects-c6-e4b119922b6fc61a70a733aafc5299afa20c55-83D8736FA2C25F0D3221E118A3DCD53DAA7DF246",
        "SPDXRef-File--.git-objects-a8-14cbaeb30b214f3379f0888b4ccff807c68a1b-05033312AFC0E64C21384DFA7EBE459988812AF9",
        "SPDXRef-File--.git-objects-b7-35373365bc7172f141853a93d0a5eea3733440-4B2623A6513B5D29F334B5A4E08816DCB189AEBC",
        "SPDXRef-File--.git-objects-1a-d04f004b638bf781012290d78e4138f97bbe5e-DCC931D7215CEC315A8B8E2BC6FC75131DBE7BEE",
        "SPDXRef-File--.git-objects-45-382b1420a9e94ba7bfa772c8feb30e81a7b6af-E8B42EEC834246F6BB628BBAFFB09A2142FE5B58",
        "SPDXRef-File--.git-objects-16-bdabcfcbf5f9d8ca9c79c148c85cfba07e7eca-0EA4A472C8E33FDF3820E5B9138E6DF94E99607D",
        "SPDXRef-File--.git-objects-80-89d5198bead6a41acabd7eaba65125e193e39c-EA7EF9FF3DD00641E025BB91807CFAF328BD989E",
        "SPDXRef-File--.git-objects-42-6d59cabe1039c55b8b64a0f830fd6f44dd4278-8488B550ED781ECB4FFD7558DD37E8904EB2B498",
        "SPDXRef-File--.git-objects-26-c6461e50acdf5342b6d3de82513ad48e562c4c-FED9CF3573AE4D7D2BBCE8C2312CD8C26509F145",
        "SPDXRef-File--.git-objects-c8-d2efa1552a994d61b16070e353e74ceaa25d9d-F44738739D79C5177FF05850F24590872BDF9277",
        "SPDXRef-File--.git-objects-ca-ab9c7dea47373d71f4fc59a6b30fc521c13de1-DB14002AA3F8501314CB23ED92577FE4940EE444",
        "SPDXRef-File--.git-objects-c9-35869be230e163f54ddb8b4862d6c537e64646-7FB2E9263040651FD2DC0AC866F81C5ED85E01B1",
        "SPDXRef-File--.git-objects-8a-e72746fb510cdcce588702d144dbd95c34501e-24479285F87A7EB3FEED5A4528FA1A0E249D4349",
        "SPDXRef-File--.git-objects-28-75677ca70527f8f8a4e4dfdb82a4c1196e9070-D6A9EE81BEA3E3B107715548AC329E802AB1BB9F",
        "SPDXRef-File--.git-objects-1f-9e9c54e48974cc494e48a2aefefd6d4c19615f-325A0A3681A9A32B457EEFC54F61979662E95CC0",
        "SPDXRef-File--.git-objects-16-5e44e4a6e0da9554b9f631f76be86f9c4c1703-A4D250E47DD2707AB2CCACC73ECE272C7590B0B0",
        "SPDXRef-File--.git-objects-7d-c1f7ef4b5ae1ac81717f477d0e7736447805c9-CE33F99DAAE80536C4C241A8917D88B84B84A413",
        "SPDXRef-File--.git-objects-b6-91abbf62a9a0c7dba526de82c06c0677ef9870-61EE3CBAB22554C3FB0EFDDD84555D9F2941C044",
        "SPDXRef-File--.git-objects-a7-81a41556893f630aba7247e441843d1b716da2-0BB161324EE3F67002F57D45EDB912B7A967B85C",
        "SPDXRef-File--.git-objects-d3-f97f2a939076851b20b18602999a58d6e07b65-476B343A6C1CF288AA60763A771F975674753466",
        "SPDXRef-File--.git-objects-55-f86f7a45dfe5346db2f7f94278b18bb9fc0dc2-05E49373B11E38D6D9E59805ACDF456B994640C7",
        "SPDXRef-File--.git-objects-7c-6f23a732f39af6b495f4c1a4dfe72593bc09c9-27030A344C9B77BB5DFBBFBEAEED6B1E4D54A7CF",
        "SPDXRef-File--.git-objects-4b-e99d38946c6f6ddbf0308c8c3c80572ca60364-F76244ED33EA6CA683D01E66F8ED64CB9B40B496",
        "SPDXRef-File--.git-objects-c6-3b3b87753c1a6283d2e619ad4ed536aab213e5-1485C82BA76A4EF269004922B26340A378559B8C",
        "SPDXRef-File--.git-objects-c8-83f1de2b5d9276f4809166f5b0595577b2eb14-74D96020963A4C08B544CC9FF2A866DC4C57711C",
        "SPDXRef-File--.git-objects-8a-7035eb20d4595b2026aacd27f3037cb5c96174-716103A6335398FB9CFCC2AF9D5CF03ADB8FB9E5",
        "SPDXRef-File--.git-objects-28-b9a3dfdf3fe3c379c1afbf1f9ea62b45188ff2-73AA5C1CF5792657236842436631FBD5909F5699",
        "SPDXRef-File--.git-objects-1f-f0c423042b46cb1d617b81efb715defbe8054d-CA2CEEB9761862E89AD47689D7DAEF3E03A5C3DD",
        "SPDXRef-File--.git-objects-42-58b533636f6da0b90b8bef94ee89f85cf4c9fb-234AFDFA5C3E3A33ABA61EB1BE203FCDFB362294",
        "SPDXRef-File--.git-objects-29-eca3ceca31817053ba9271c1fe760e30bcc294-33C2D78A1E01D18C7FE7B559E53D9E00DFD37711",
        "SPDXRef-File--.git-objects-11-8dee7289974c48b272e2d5b46332dca1a41b89-7963F16C09A2C63BD056035882A47077125C2FCC",
        "SPDXRef-File--.git-objects-4e-bd0978b4638a7577673814fcecd33bca4034dc-69030B8CC3BD289CB9A42F527DDF1E097BF3787A",
        "SPDXRef-File--.git-objects-fb-0e2552806fc82adbe2a2e2580a854e56eaa79f-0C44D00B538483133DF31FFBB3989190F88096E7",
        "SPDXRef-File--.git-objects-ca-bfca72ba176bd51d85b0c8476dcd27e9bcfa4e-84198477A1D4977D73C443C4C69701642B00EC60",
        "SPDXRef-File--.git-objects-28-26a49cd0da58f3fb2c752d6c9fa0ba25b016b5-4E9CC618618544FAF24239537344BED8E9568426",
        "SPDXRef-File--.git-objects-45-268a641c5c882d87711832b161f5f5084b2d42-9014A04A9743F6C3F46C94B01395CE11CEE986F9",
        "SPDXRef-File--.git-objects-16-92493005fdfa29299c59541a83d0ccf9688515-B410C52FA490F9A703E1CC93D2335607F8EE3E15",
        "SPDXRef-File--.git-objects-11-bfc47e5b31eaa4d5fd5a57c6e002e55969a47c-3AA97D490CA705FD55BF95D46BB51F016E9D0317",
        "SPDXRef-File--.git-objects-20-d062e63c917e2420fa15fb8f2dd570234272a3-2233DF97F598C0E6F8B568F541483C07B4EC4296",
        "SPDXRef-File--.git-objects-4e-34ae7395fd4f4c2b071ddaaee36f0911381121-CBACE3D6536E8F1A2DA528F79A76E94E98C862F1",
        "SPDXRef-File--.git-objects-fb-363fea57823cae1b4ab2a2d08aeef14a361895-FBD733B24E9AB911D35A14BEABDBF3B873A75EBA",
        "SPDXRef-File--.git-objects-ca-f909e3c90831eeb7364fdeefd7935d0e20298b-ED4EC57D73A5AAD7312B03D4F093BBE5CB166CDE",
        "SPDXRef-File--.git-objects-fd-716b8a055bce8017e05619d87b5248141987fb-472397DE11B103EA9D45BA21B60CF576F358D52C",
        "SPDXRef-File--.git-objects-18-36ae8f2c7e4158d5b4c2fbe44113038448a375-415F99BC6FEA61D222DD790BEF2DFCB5237019D1",
        "SPDXRef-File--.git-objects-fb-19cbebf480f78114be31cf499ec346a2434f98-068546FC9F977909C7D993DC281ECF578A9356E0",
        "SPDXRef-File--.git-objects-fe-e953a668a524de687ea1e04fe04b2cc8f930c5-24B7DC295D6446E72AE56626474DB59A1A7E4238",
        "SPDXRef-File--.git-objects-f3-684f9bc94843a2936f5a1377c4f71bba241147-F07F9FD797217957802C885E0A2C7CC5FEABB214",
        "SPDXRef-File--.git-objects-d8-ab33a65a2361a1820fb3fad0c42c3be3e23c1b-B7CACD357B3017584BD4645B40A75A924D8D810F",
        "SPDXRef-File--.git-objects-f3-948ee2b88c608361ec0a5cc7501b7ab96b6445-678D696DD79C3C6492D53462345781C8BAA61BD7",
        "SPDXRef-File--.git-objects-fb-e97366f1fd209337eb7fb3f95939024834721e-BC62C19CE470B0BBF43B6339FD23290B03E7D722",
        "SPDXRef-File--.git-objects-fe-2364f4e1f9d4c6c0e4562728de753731fbc3d5-53E8EBFC61B0AA3425F6878D431B5C83D57B940B",
        "SPDXRef-File--.git-objects-fd-0d9a092464fa053f111f1a9b62e5f970e862dc-363E82E12E17C88FA6EFDF5E89F3B0843DCF73F0",
        "SPDXRef-File--.git-objects-f3-24f7b5ef2451e0120e39d9c1b7b3f87ab16301-79F09B3C2289C8874F1ADD4C1513FB52C30164D6",
        "SPDXRef-File--.git-objects-d8-2f88fb932568ea743e4bb04da975d08124917e-4787034DB1DE1357AD2EFDC4295EC9A8791C8FD1",
        "SPDXRef-File--.git-objects-6c-ce6757c23acd5bc3cc1ef27588d0114a6b88f6-85A16EBA678347B8FC819831F6F50E40C1DF6627",
        "SPDXRef-File--.git-objects-5b-2913fb4c1acee4d2db4d01793849b99ff0d3e2-D61F77BB7DD7F237597CEECE3A02BC247734372F",
        "SPDXRef-File--.git-objects-54-d2cebd29f52946ff593b4fba4e3b5bc0cc5180-8C70CDE73B0330483081A006CBEAC10AA979792A",
        "SPDXRef-File--.git-objects-91-a06612b2c44b12fa73db67c0df330e67ce1b5f-07B0BEB6CFC1D95737C93DC4A3AB30660F8EF63D",
        "SPDXRef-File--.git-objects-27-1c005267ed633dd38befe90ecbc0b4404d7668-AEB2B3D455185A9EE0859C442FC2D453455735EA",
        "SPDXRef-File--.git-objects-c6-3adcc17c68928e41dda0bea3e8720b88f88801-8D31E0A75DCC171C936EDF8B20EBAD9B54802E26",
        "SPDXRef-File--.git-objects-c8-1e17776145d7cffc16316cc0f8686822a25299-771934FDA5D9880EBA57D70BD89E9E606D273761",
        "SPDXRef-File--.git-objects-ca-77d05a32a28fabeba66343554b524bca1d7857-6F08258DE894CF2B2C36CDA20E38FCACE5B190BB",
        "SPDXRef-File--.git-objects-ee-3156df1d6af3a2a0d33e0a5248e82f1d52dfc0-488BF229D2D8A8603E9892BDC116F81A1E50523C",
        "SPDXRef-File--.git-objects-f4-a356f9e2bd8a9d90d488a338b27ed244285d57-9FBB3F5F9F33FEA2AB2769432CC454121560C69E",
        "SPDXRef-File--.git-objects-bd-5076b792f74e8b73efdc2581282ef6792fdb77-E5025057413F633E5D8CE00E085BE94FCCDF931B",
        "SPDXRef-File--.git-objects-df-f8a438f0544edb7b97fb0d1f0de873c46c8450-9444418BC8837E91DFBCEF12F8D715D23B02AF98",
        "SPDXRef-File--.git-objects-d6-099a633de9101514d4efb8e7d930dc75e5c15b-98C5DF3BC74A9EC52ED6C0076FA6EDA6CC895296",
        "SPDXRef-File--.git-objects-a2-9846f2c3baba40eef69873e0c34d3d0d5b0370-92233359371811D051718AC6830D133DBC3AC356",
        "SPDXRef-File--.git-objects-bc-8d99071afa381f88bcfbef4afc9242988d9952-CFB1F1AE5EB3CC54934C9E1BFDE08D6F4F4BB2D0",
        "SPDXRef-File--.git-objects-a5-b58b397d927d78c6e062160c6123a776eec0ec-0F2BF3F1DB13F6EDC139C77A66BB8E28C4BE6419",
        "SPDXRef-File--.git-objects-b3-157477ce79e18214cad1ff7eecc16386f7f1b0-733D56E3906A69CA8E5CB2596E5544D536F1A231",
        "SPDXRef-File--.git-objects-ae-d3b88f1c76eae2ed8c32680893180b934da74f-51E91D8F540066C21CC811F512FD0BC4E78ABCC3",
        "SPDXRef-File--.git-objects-bd-d44a8371ceee2bfcb3e5c93666bc5b133eb2e1-B962699627664BE7A78491DFF379EFC6741AF9BD",
        "SPDXRef-File--.git-objects-df-449fb04da1b8ec1c7aed237cfdda2b71b40761-454567B5788249B13CE5967B6FAFD72211ECFC0A",
        "SPDXRef-File--.git-objects-f5-5acf7f52b4c1c2d19593a4fa106731f62472b7-6FE774CF610A32D0D8E5DC4DD84DB06BD049AF7A",
        "SPDXRef-File--.git-objects-eb-c98fb9a6cc824326d8cb43323379a2993c7ec5-E82382D4CBD6E89361C94385C7C310D2014A5B7B",
        "SPDXRef-File--.git-objects-ab-4c3a4dbf1c2ca46bf50db7fdd9faf3d0e83e75-E9B4A6D28B7B1446A845A37C62901CF672DD3C11",
        "SPDXRef-File--.git-objects-d6-a9eceb8836e9ec27384ddba24a919b46c13e90-15CD5E6FF6A743E892CCECCFF4C38FBE6BB5D177",
        "SPDXRef-File--.git-objects-a5-cc5f5190d92a1cc50b104b0ca71bc306cb9ed4-78FFAA7EDE4FDCCE40BA424D859FD374F90E39AF",
        "SPDXRef-File--.git-objects-be-d7695346d08df7ce062a175b1eaae998d66761-8BF5D1E5FD0ADF354EF717CF177C1843FAD542FE",
        "SPDXRef-File--.git-objects-ca-673c644b010ef6e614a202a2cbd5d0aa0cf9f6-2F9C958A92078D0C4D61C1851871C8A0190609BF",
        "SPDXRef-File--.git-objects-ee-9bafdb84f860ea04f5a03bfab99ea37aa997dc-05B20B41779DF1FBE1784EAA10CD698F8E30175F",
        "SPDXRef-File--.git-objects-e2-0ec9ae226ea60c41231eac61b425f82ff33888-7B72A4D1FE5FC3C7ADF55CE7B30A8D8DD5DD0415",
        "SPDXRef-File--.git-objects-bc-b29818b99f698e8a72dcb941dab0ce79f61c69-ADF13240CC17F2AAA1FF72E94846D6EA6B8B7F6C",
        "SPDXRef-File--.git-objects-a5-6a44d278f1a61429f839e54ae4b35e8dc91aab-AD44F26DD68408BBF5CFD8769DBBE1596A99BFFF",
        "SPDXRef-File--.git-objects-be-26a20c69fcbc6451816768fd78349306e5dd00-B949FA4D72E1338BF7AF17C9E342107C57983C35",
        "SPDXRef-File--.git-objects-fd-c06ccd4d9630f6eaa1c6a1bfd14f0975be62ea-5B6AD1A7C40DA2E162E0C64E3A7015260626B7FC",
        "SPDXRef-File--.git-objects-eb-3513623b99426dcb35a79d95298c1e4fc8500c-718D65B4D13CFA71555612417C7019FCCB69332E",
        "SPDXRef-File--.git-objects-ab-583de69bf4aad65fdd2ef1c1168f46468bea89-3A06D1DD2C28355FA164E1D31EA88BCFDD44CF24",
        "SPDXRef-File--.git-objects-d6-352cce321b71fff65b8bda2ac74c98d254a17a-97182AB7CB30B58B641F0A15E11B8626AA0DBD48",
        "SPDXRef-File--.git-objects-a2-b8fc1356e2630db4e765bcef437b6657eaa88f-C9696D0A81A8DF8457D8ED77F0880D47ADA9E2E9",
        "SPDXRef-File--.git-objects-d0-cc4445effb3c7df96ee80d258f923b681bcadf-362A6E4B12BD2F8F5342C8372850DC612F3D6645",
        "SPDXRef-File--.git-objects-09-3fed3b924faff6661471ea79b86f569cdd69bb-648018F5363515332005ED9EDC5820BF4B32C0E3",
        "SPDXRef-File--.git-objects-36-573fbb0fa8e92398d0107de527bc3b1d0e3817-FB107B6233738FC34E6C19F8EF56DEDD49881301",
        "SPDXRef-File--.git-objects-07-d1b9438f4570b463ea5ea61cf5867ce7f9310a-96CBBC144ACCAB7804C89A8FE084B9AC4EAB53A5",
        "SPDXRef-File--.git-objects-88-4d3058ed141691d3f381239c76ae1bcb0e3a8e-354A2EEEFE5F6F6B759E47543657CAE0099FDB2F",
        "SPDXRef-File--.git-objects-2f-94285f0c3e12a9ad68dfb6501af520ead1a351-D66191165B62276BC1565AD97ED4673B77C5D012",
        "SPDXRef-File--.git-objects-86-ff0d0cb69fbe6ab2c14ca77bc0b3ed04a5c405-18FDB176BBAE18256D66E74E0DEF7D2AB7234E5C",
        "SPDXRef-File--.git-objects-4d-780d4525ef2b89961a55da70f67f7ab4fc480a-7C72BE40C2ED14D574CFC437AEA2A6B6B7DB20E2",
        "SPDXRef-File--.git-objects-4c-90bba6d9392e1c4ccdb2cd6d48339e73701e4f-21A8EE10ADEE002085A8394A6355306A43F47101",
        "SPDXRef-File--.git-objects-8a-265dc6783489a2664c035ad641da09b5c4229f-9A836EF2EBA74A4679DD4F12862275416A075BA2",
        "SPDXRef-File--.git-objects-28-8d5942ea9c9e6863921670c4ad4832953cd75c-E5B82F61578A6CC662B042B570591279C8F7DF23",
        "SPDXRef-File--.git-objects-1f-369ba5c3b0da81b6644b7dba6ad5f2b86d5986-57A2E216424E4EB7B29A6C1C9A65C7B591271DC0",
        "SPDXRef-File--.git-objects-42-3e1867e345498567d3461325b6d790fc428b4c-CBC6F69BB9E800D18066A23B26450538BF9692EA",
        "SPDXRef-File--.git-objects-29-9b8ad32b5f51a231fff3e9118a3e6d346624ac-406E7F38861B5AF44697CE22E7F4F9C4510D669F",
        "SPDXRef-File--.git-objects-27-00a9f59913807f4a4d02b0e6446ec00bda55ca-53CC762AB9448641BDA60EC1B6D1531E76BE0FCF",
        "SPDXRef-File--.git-objects-ed-0f311c7d11f653f477967db9cc655828738a1f-9AB724095BF88CAB4E6486A9B8B5BC7149CE6A53",
        "SPDXRef-File--.git-objects-c8-58b9f0d535f502a2fb448ff27be3acb5c62f11-613125C613C66F401B836E384BB6FA293B65802E",
        "SPDXRef-File--.git-objects-cf-ed1c04d1768599c58dbb3d7162640469557201-CBE40CCABD31574922788F4D4B6507AAB7E07691",
        "SPDXRef-File--.git-objects-c7-be352ebf24bffefdc53988e07f24262b547fe4-33733A5836C70D9AF7470DFF4D0C546B5A01A0F6",
        "SPDXRef-File--.git-objects-e2-ac576688faa94c27e37d7439be3d01fbd6a32c-D0D1B9E44A438E6F3451E4F1252FB7F01334C11B",
        "SPDXRef-File--.git-objects-d6-6ec96dc24bb441b71bd8faf4b24a4a982d6d19-453DC2ED040B338EB5F662137456F96D564E0465",
        "SPDXRef-File--.git-objects-a5-dee5286bb81148247d75cb32f7b59502fd54c5-D9F7B095FDF3632DFB015A1AB3CD0E00F744F37E",
        "SPDXRef-File--.git-objects-be-3e635add23dd2db9388e1667e4b14ea5ced8a1-979B25F2B1E6D99E90BCA5BDEA059926F5D391C7",
        "SPDXRef-File--.git-objects-ad-4c6c4d5e3c848a35487ac0d13b77f392ce434c-AE20B5A968D67E891B69178BB5F1D0E4283A1F79",
        "SPDXRef-File--.git-objects-b2-d08688123b1201e69796d0a2d2f55e3c06803e-8992D16F50457815725C419E8407C42F7AEC92E2",
        "SPDXRef-File--.git-objects-9c-60a1761dbf62cc2a45ff98b9fdb63ade16e4d9-EAF53AA8C357A2C023CFF59D323B1AA0A143FC47",
        "SPDXRef-File--.git-objects-5a-ed07b3b2cdfa8a70ee4b63df19fbf343e18d51-6D5F138B5A9D7F19FE87C6C435CA66E47A883444",
        "SPDXRef-File--.git-objects-93-7430bca04c4b023a0e475f60c6da187ef17920-B6EFB76BDA0A7AB7785102EA857D9167AF0F1A0C",
        "SPDXRef-File--.git-objects-51-29badba30ebe31fb36e401201f2e47b4d3a965-92B54AA23057C984FB95CF87AE62BD534A032EDF",
        "SPDXRef-File--.git-objects-32-1a73835b9585d5deff6c70aba9685513ec5fdf-A760CCC39074AD6EE528BB2345FE2CF92448DC37",
        "SPDXRef-File--.git-objects-9e-84235afca71c07afbceb55d5d5a464493b45a2-E39C3C0A3D5DFD5016B01C90C85B6EE66CB9E3EA",
        "SPDXRef-File--.git-objects-03-40e14bc8bbe33f5c7fe60145cdfd2ee9bfbde0-18F8D953529DE9AD45202505EDFF65010C8D4FCB",
        "SPDXRef-File--.git-objects-3e-1010796007077cd803b27dd0e9cff6492e8341-C53E0F04582DBFFFCB9E49BEA60D3EB3F3B22D53",
        "SPDXRef-File--.git-objects-59-d58f1cd585200fff3144ca7040665e15df2741-102E0ED43471E90AA5DCB4C76852BECD65797CBF",
        "SPDXRef-File--.git-objects-d7-231bf61b7c9608a7894edf7ef9a4d7e45be63e-191366F680DF84ADE8A0C180508A42AA6A5043DF",
        "SPDXRef-File--.git-objects-ac-a9f8d1c0b09a152488cdb90f190db28022f729-94D2FF8F3A8892110EA13E736216AB7A582BBF56",
        "SPDXRef-File--.git-objects-b5-e4a79a7e823aa48a2409a203ed148bcf7eb7aa-E3FFC5E01FF188A06F0561A62E2983AE44D9982D",
        "SPDXRef-File--.git-objects-33-23c6abde5f2ee3f6335febc2e233acea6941f5-B6EB793E545B53129F52CF35AA3EFB9CE9F41C88",
        "SPDXRef-File--.git-objects-0e-8c04612795e5a41f851b40600fe6154792603d-CD4D5D72EB2784016DCDD0641A48E00AA75A85D5",
        "SPDXRef-File--.git-objects-0b-703ed7260ceb48b9aeb20196b1d89f2c4a9ee6-92A18D8B00F4EDCDB836998D678B2B1C133A49CD",
        "SPDXRef-File--.git-objects-35-d83c6979ff4788df7fdb10c1f7e543577b2cb0-D960E54EDF0B96992D10B946821E15B0FEBD732B",
        "SPDXRef-File--.git-objects-6a-6c77a8b4c457a56c463ba024be6f4a50755d30-99930F53D41224C2DFE7A128DC5A0F2BB9437A92",
        "SPDXRef-File--.git-objects-03-e90517eb49f1817b081ab36bfabe70e658ed91-74B3A36A53B1FAC2431DE05E76F2DD293C8746E7",
        "SPDXRef-File--.git-objects-57-323e73da4d7c64b07f1f73a298e0b304886d94-F6EB37309BAFE9B8D7835D855810DC423A5015DC",
        "SPDXRef-File--.git-objects-0c-b229465db750dce7819a3a221d85ae7cebdc32-4425BE10DA9E75865DC90C4E813CC532D8724173",
        "SPDXRef-File--.git-objects-61-a5dde9ca8b7a1c9af9910271e4f6258e796ce1-F6D5A6E184D779366DF20587EC3DD0D7E2889EB4",
        "SPDXRef-File--.github-ISSUE-TEMPLATE-Bug-report.md-F3A5AF2CDF1EB03DDB349E1948501B648D72EED5",
        "SPDXRef-File--test-EmbedIO.Tests-TestObjects-TestRegexModule.cs-15FF4A6A964DC6ECB850144898F0152A91253EFE",
        "SPDXRef-File--test-EmbedIO.Tests-Issues-Issue389-RequestContentLength.cs-5EC872BF42A0B50285DB0FA1A6E3F14FD7CB6AEF",
        "SPDXRef-File--test-EmbedIO.Tests-Utilities-IPParserTest.cs-EE36CFAECE4ED2D8F637B76045BFB91E21BE4FAE",
        "SPDXRef-File--test-EmbedIO.Tests-GlobalSuppressions.cs-C77A2DD4CF05C70D62B717E341B34973A927C6D8",
        "SPDXRef-File--test-EmbedIO.Tests-BasicAuthenticationModuleTest.cs-9C660CA80DAC4310183D83F9FABFEC434B053B2D",
        "SPDXRef-File--test-EmbedIO.Tests-EndToEndFixtureBase.cs-DF455BB8D5F96483811002A87E76EA1B0BD61F67",
        "SPDXRef-File--.gitignore-0F8B71B205345F74E1DEA2C4D51B36D34A732ACA",
        "SPDXRef-File--embedio.png-AAC80334397312AD9323DC3DBF2E3DD4A957BF32",
        "SPDXRef-File--src-EmbedIO.Samples-WebSocketChatModule.cs-DC5E6789D08CCF807634540A8FDCAADFEA585C90",
        "SPDXRef-File--src-EmbedIO.Samples-html-index.html-79F3F4D7F55D70BE2F04CF2531B8F0D940DB3735",
        "SPDXRef-File--src-EmbedIO.Testing-ITestWebServer.cs-E2A88B11BCB5180E2B29B399C164E88A675C6C09",
        "SPDXRef-File--src-EmbedIO.Testing-Internal-AdditionalHttpMethods.cs-8E938FEB2F1E886D6B4C119668D6AABE2AB98BEE",
        "SPDXRef-File--src-EmbedIO.Testing-obj-EmbedIO.Testing.csproj.nuget.dgspec.json-3A8FCBB27214C8C468E03CBFBF74B6A2AF503535",
        "SPDXRef-File--src-EmbedIO.Testing-Internal-TestRequest.cs-E16DCBF1F7CEBC9EF9BEE9092297E459120BAAA6",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Assets-AboutAssets.txt-9BF33A55DEAB5A3BD5CC53FCA4EFB27281C21945",
        "SPDXRef-File--src-EmbedIO.Samples-html-views-cmd.html-7E4C7DAB7E032E25EE47F0C6C1D81410963B3DF5",
        "SPDXRef-File--.git-objects-ac-11343c48ea2db874eef821ac99f35349ce63ca-3E35F7F076CC22FE0CBA1346AFFF8A87CCDF4DCF",
        "SPDXRef-File--.git-objects-b2-0dad98e7a87bd5a23d80f34cfdd6e5449cbad9-AEA4A0D24FA09B8A482C4FCC642DE88E0981E8DE",
        "SPDXRef-File--.git-objects-9d-31c44f036b279decd21c2a7f0befdaa3d7959c-EE089E1E971D1165F2579B65FE3A3D8972E3F4FB",
        "SPDXRef-File--.git-objects-34-47ad42075e5f731d1179954d1ba39deb98d0be-241B6795D7542BE358A6934C2A228162C5281328",
        "SPDXRef-File--.git-objects-93-c0dfe18893e520f4a9b151be2f50ea0befa4b6-D1624CD91B27DB94EC8492EC60DB94D8547A236F",
        "SPDXRef-File--.git-objects-56-e9cc92069b7df238fded6ce99f5fa1185c2736-605A462C7935E7988208C5537C8C066B0FF91884",
        "SPDXRef-File--.git-objects-32-181587254bd916fb11c5fee633d00b71ae56a4-477143711D5A781923BA7C98AD23E5591EB65B0E",
        "SPDXRef-File--.git-objects-9e-9234d4a9a87beb211d699040bc95f3e396dbda-8F19C7D3E8B8B8A8E190A63E45940DA97E1611F4",
        "SPDXRef-File--.git-objects-6f-102672544048cde97c7e7a517f9e62417c59fd-B6ADE89695FCE603301BF8955DC5D93A948FDA68",
        "SPDXRef-File--.git-objects-3e-c376c73d5edf0f4838b3a452fdfc88cccfdc26-671425613AE05F04500319E1587697842214D650",
        "SPDXRef-File--.git-objects-59-dd4be8a409417a4828aa4ce9c18a6db37144a6-DDF1361B13E112A1FD11D980E35BE54AF7075BF9",
        "SPDXRef-File--.git-HEAD-9F1DF7EEA4156BE8A871C292B549B3325E425AA2",
        "SPDXRef-File--images-embedio-icon.png-AAC80334397312AD9323DC3DBF2E3DD4A957BF32",
        "SPDXRef-File--test-EmbedIO.Tests-TestObjects-PersonEndToEndFixtureBase.cs-1246411803C985D8EDA8E3B0F345B04075B91DCF",
        "SPDXRef-File--test-EmbedIO.Tests-Issues-Issue319-FileModuleDisposeException.cs-22EF19A8842FA17C4AB373C92FC180EF166AF15D",
        "SPDXRef-File--test-EmbedIO.Tests-Issues-Issue452-CompressedContentLength.cs-7744B953CD226DF5344463F9E9CCB95FC7DA1DA2",
        "SPDXRef-File--.git-objects-ac-398a1bcdecc2d4f413aa4639a6a236b2b81569-40AA5C050BF3A2622C42126566A306201CC7791B",
        "SPDXRef-File--.git-objects-b2-cc0583fa931380444cb8393a6f47ed8a4b2311-4BEA766BEC962E97CC39FA67FB84ED951D872A47",
        "SPDXRef-File--.git-objects-05-3c495844f0ac44c30792776612c66344fba5f1-297906F1BC2A6E232E9F2AC610D789D97DB0A67F",
        "SPDXRef-File--.git-objects-60-ebd7d3c15b2b9130638e2070bdfd13339cdfcb-33B1D34E58E382DD244CFE48A7A0F72FC4839906",
        "SPDXRef-File--.git-objects-93-ba66fba3502730d05f2ef42d4c451d1936d648-77ED57B9A8161158CC10187DC42ADC33CAFEA914",
        "SPDXRef-File--.git-objects-69-277dd72e9213122736b9bf4a2626eefc026bc0-CBF71EA5E070A21F3390C56C6BA6934F51FFB18A",
        "SPDXRef-File--.git-objects-32-440653b882521a80835914d952a209fbba988f-34E73A0FE58A7EF413CF39FA7445CA5F48A09560",
        "SPDXRef-File--.git-objects-9b-953618f643e859a3623316ed1b5732df835bce-376B5C22D3AD5ED905CC9CA2C60DBFAB3C73B07C",
        "SPDXRef-File--.git-objects-3b-60d8d14d35b5126b380cb3b3a95548abdde8ef-4E5F2B44ED18A6E5572F8F752DCBEDA7E035CDBB",
        "SPDXRef-File--.git-objects-66-b5ba9528ea5116695e2191aa4650a6b7b5e264-BAA636FE7F2CEE40E5A31C3B2838D82A37CEEE56",
        "SPDXRef-File--.git-objects-59-02d5c54443343cb36fea771ec3404eb2e726e7-EA8214B5728169C72DBA315C8FF1129AE3FF91A5",
        "SPDXRef-File--.git-config-03C944CB31F16751B53A7AE9CD859DD55AC11966",
        "SPDXRef-File--images-embedio-icon32.png-27F0C726556ED6FF6B4D88800E2A3A1164B97EA5",
        "SPDXRef-File--test-EmbedIO.Tests-TestObjects-TestRegexModule.Controller.cs-24DE44B69F0ABFD2C865B9D1173F608547E57785",
        "SPDXRef-File--test-EmbedIO.Tests-Issues-Issue355-ContentResponseLength.cs-F09472423247547BF0909BE74333058C140CBE58",
        "SPDXRef-File--test-EmbedIO.Tests-Utilities-UniqueIdGeneratorTest.cs-9D585DCA215CBD1168D213D69FDF5AF7F67DB2B1",
        "SPDXRef-File--test-EmbedIO.Tests-IPBanningModuleTest.cs-2E3F5ABCEA7421839492E3A94F9E263A98503DF1",
        "SPDXRef-File--test-EmbedIO.Tests-FileModuleTest.cs-3B62826A7FED1B004A02F82CC7BD725201249BC6",
        "SPDXRef-File--test-EmbedIO.Tests-WebSocketModuleTest.cs-05D1294CDE2EF1B5E3634B601186269FE16D5A28",
        "SPDXRef-File--EmbedIO.sln.DotSettings-072468DDD020D203450CE81AF916A693A715330A",
        "SPDXRef-File--Directory.Build.props-A185B8FE61B98549C2CC401AA5761AE62EF3A0CD",
        "SPDXRef-File--src-EmbedIO.Samples-html-scripts-bundle.js-84BA978A57D5C272ABF96694908DF6189EA443CA",
        "SPDXRef-File--src-EmbedIO.Testing-Internal-TestResponse.cs-7642A0E3B153658619BF585DBBA84B8FA50EB329",
        "SPDXRef-File--.git-objects-d7-303bf67f94ec0734b273c3a28b352284fdf310-8993EE67438647A0D29FE21E39BF15CCC27E0DA0",
        "SPDXRef-File--.git-objects-ac-f530a2537a51f06304053440c3aa68ce168fa9-567AB1FD33BDAA4ADADE3C8BCC045504C11B3D50",
        "SPDXRef-File--.git-objects-b2-7718201f5bb289362b12baf8f41f1fb8978096-DA3CE903A0AA73F798838857AA2EC8D172642A9C",
        "SPDXRef-File--.git-objects-05-66a340953ff58b75df2858abb37e2644d90509-5FB44173E2BF9C78E2DE2865D920F1230FD74B5A",
        "SPDXRef-File--.git-objects-60-a64703c0f11d08705cd607f7751338707f5919-3495995033666A825387054DBF3AEF4E63888E11",
        "SPDXRef-File--.git-objects-0b-e9d591a5c802f8180f1864e0c9fcc71acaffc6-39034FC2439153BABA6CE9BA5E58526FC60AAA2B",
        "SPDXRef-File--.git-objects-69-c2b3697be51189ac2bd82596a6441bd292081c-77CA85440E1615FBB0FA4DE0B37D4C53C5EE3ECE",
        "SPDXRef-File--.git-objects-32-eabe6edc7bf3f3784a8244cd66bd77622abf6c-351FCAEFB023952A92213A3A2A81BB09E72BC154",
        "SPDXRef-File--.git-objects-9b-1d25e25de64c1ee12f91c9b41f85b0e84664e3-068A715EA8DB8C879C8F4988D2A5EE3E29B53975",
        "SPDXRef-File--.git-objects-3b-50dabf4a02fb912289a92d2bbc2b96f8d601b0-87F8D6EB89BF80BD277E41D6AF16A07F1521891F",
        "SPDXRef-File--.git-objects-0c-33af9369b1a00c0b1311d1ae454c11ee771797-90E93677ED56525AF9306912C4874ECA1D6C16BD",
        "SPDXRef-File--.git-objects-0d-8d5427c4c959595cea690957122e2844167b58-DCE17EDBAEC2045465C486AC738371C09E9BA979",
        "SPDXRef-File--.github-ISSUE-TEMPLATE-config.yml-154D025F938071B5419DC4409FA1E5EAC42C08DB",
        "SPDXRef-File--images-embedio.png-703CB600060BDF80BF89B2949EA2FE981BF7605F",
        "SPDXRef-File--test-EmbedIO.Tests-TestObjects-TestController.cs-C4EB341097F329E761F8D32D3B108339A84C502F",
        "SPDXRef-File--test-EmbedIO.Tests-Issues-Issue394-AcceptEncoding.cs-83476B7515A6F60C2596632AABE1FA95C0764D8A",
        "SPDXRef-File--test-EmbedIO.Tests-Utilities-UrlPathTests.cs-78F56E45815D1B0EC9B62A47918AAC44EC30EB78",
        "SPDXRef-File--test-EmbedIO.Tests-IPv6Test.cs-A195751DFFD0612F17BCD099382E52F864CD3133",
        "SPDXRef-File--test-EmbedIO.Tests-WebApiModuleTest.cs-DF923AA8E41D1C57B992F3E4B55043C5052C3532",
        "SPDXRef-File--test-EmbedIO.Tests-RoutingTest.cs-61F7461E5D0F7F21C9ADEFF7CC73DB2DD345139B",
        "SPDXRef-File--CONTRIBUTING.md-618215987CC9A774C37CC70EFA1CB8545457A49C",
        "SPDXRef-File--LICENSE-6437B67E8E9929A8B279EDB129353310E5225AA9",
        "SPDXRef-File--src-EmbedIO.Samples-html-scripts-tubular-tubular-bundle.js-47F3ABC427123CB1B7F2DF44C7762D126BC109D2",
        "SPDXRef-File--src-EmbedIO.Samples-html-views-people.html-C10D39CD00EB117C7CC78A674C9FB0E232187B29",
        "SPDXRef-File--.git-objects-bb-3e6fb731dcd883a63f6722325806fc79ebbbff-F3316E285D62E1BF1E1E6ECB2ED76D7A7A7CAA71",
        "SPDXRef-File--.git-objects-d9-e50fa38e28d2895d7965561547568628881226-9D16EB5BE6D84FF38B14411B648B405CAAC6DAEC",
        "SPDXRef-File--.git-objects-02-381f15a4c50153d5697c56c44b33c27473bd2e-AD19AFC613D381205D4E6385203873250A3388AD",
        "SPDXRef-File--.git-objects-5f-1e1356eb65f82e97dfa23bb28a7e596ec02aad-8ABF5FD7E6825C3FF71A2C7897243548F8330652",
        "SPDXRef-File--.git-objects-94-3e2bf7601a0e2ad8f3696e7a4ccd24a376e8c0-7BB0CE1E4AF87D6E326DCA0085F11A3B5EA25B2B",
        "SPDXRef-File--.git-objects-58-5ba42e1daed2e2d0b3a2ac44913d6e013b0fea-71AF7826CDA69E7371D957518B97579617D8DA51",
        "SPDXRef-File--.git-objects-32-2ee9a5dca5df2b1ae93b81cb9ea0750c8016b3-7463D95DAA667F6862708C998015DACE0F81358F",
        "SPDXRef-File--.git-objects-9e-9e4f8e4cd36a6424321c1f7bab9a70b4911da4-F28DEB44D3E6025DA7EDD653C2362879E8F77695",
        "SPDXRef-File--.git-objects-03-24b124a402ae7d63f547bad30436abfdab44a7-0EF7C45EF9C18E9325215ED1861C465FD2273F52",
        "SPDXRef-File--.git-objects-57-4b04721c4cdc9361421cd993779108abf13888-310A7743C701DCC574B6540123127CD6DCFF21C0",
        "SPDXRef-File--.git-objects-59-4f101be3b123fe758efda1cfe0472ea6b0805a-AA404B0443C148C78E7B603F9BAA0551C2EA9650",
        "SPDXRef-File--.git-COMMIT-EDITMSG-3ABD7D808A3A3BB89A3B62FC5264862EBBBDDF58",
        "SPDXRef-File--.github-workflows-build.yml-C102903BC48C7C03110C362C86262008407CD4E6",
        "SPDXRef-File--test-EmbedIO.Tests-TestObjects-Resources.cs-E886F67B820B2512E11EDC9E52EF6AD296AF2896",
        "SPDXRef-File--test-EmbedIO.Tests-TestObjects-StaticFolder.cs-6F81BF6A9354BAE6D16FC59825B1A5009AA0205E",
        "SPDXRef-File--test-EmbedIO.Tests-Issues-Issue427-PassHttpException.cs-DB007458E05CFDD244EF65E3152012BD96945757",
        "SPDXRef-File--test-EmbedIO.Tests-obj-EmbedIO.Tests.csproj.nuget.g.targets-BF0BD90392A487758D4C0BA5DD1557D0B5B3A392",
        "SPDXRef-File--test-EmbedIO.Tests-ContentEncodingNegotiationTest.cs-9F39A7E30FFCB647A25F2D0B472099EBD9A701F6",
        "SPDXRef-File--test-EmbedIO.Tests-CorsModuleTest.cs-33174E71F10B8E23B48BBE6032930B24AD5115DB",
        "SPDXRef-File--test-EmbedIO.Tests-ResourceFileProviderTest.cs-FE7B1836655CBDCD54FC9F26B023CF313AC14ED8",
        "SPDXRef-File--EmbedIO.sln-DAF76765687FCC64B48685DC5472BD871117C660",
        "SPDXRef-File--docfx.json-227DFA2BCCFB7F8733B22F04ABAD5C5482FF8815",
        "SPDXRef-File--src-EmbedIO.Testing-MockFileProvider.MockDirectory.cs-4EA6BB7247589FE949B8BEE6C113D8B0978062D1",
        "SPDXRef-File--src-EmbedIO.Samples-JsonGridDataRequestAttribute.cs-54ACBD720ECB9F17FF399454C2DD13B22BA1BD3F",
        "SPDXRef-File--src-EmbedIO.Samples-html-scripts-tubular-tubular-bundle.min.css-BE88C04FFFFC34F7FB23CB2D7E456CB2B6027D7D",
        "SPDXRef-File--src-EmbedIO.Testing-EmbedIO.Testing.csproj-CA9B471508A975365BEFEA07124A3CEC8139B6C6",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-AboutResources.txt-A47737D1F2B0EC65B8C337484D255C8A5FE0B6C7",
        "SPDXRef-File--src-EmbedIO.Testing-MockFileProvider.MockFile.cs-D867A2D3CEB9F4FDDF1D4355ECB401790A82312C",
        "SPDXRef-File--src-EmbedIO.Samples-html-scripts-app.services.js-B4F7294E69B72C71EDDD76C45B52FD6820335AFC",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-values-colors.xml-8EBD923F75734AA4C8447D1CE9C0BFFFA5C4E0AA",
        "SPDXRef-File--src-EmbedIO.Samples-html-views-home.html-ABB1082AE85584036BDAC8D1C6BBC14832C91B28",
        "SPDXRef-File--src-EmbedIO.Samples-html-css-theme.css-A24CADB327D143D24F2895A526339430D55D4738",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-mipmap-hdpi-Icon.png-16B9445C8EC91A3B48BF6FF738B8A12551DB5BB0",
        "SPDXRef-File--test-EmbedIO.Tests-obj-EmbedIO.Tests.csproj.nuget.dgspec.json-3C9DA4C1FFDBC673F44A53DBC3EBE7331CA10EBD",
        "SPDXRef-File--test-EmbedIO.Tests-MimeTypeTest.cs-E9FFB334DAD22864A5343F3B4687BF9402645721",
        "SPDXRef-File--test-EmbedIO.Tests-HttpsTest.cs-B4B03353A4461CCEF8FD25BC82B49EE6669444C7",
        "SPDXRef-File--.gitattributes-2C1741FB1014D41275CF6193F806AE86CC951F25",
        "SPDXRef-File--Directory.Packages.props-B977A95DE766FCF8C9041B2417AB76295FFB371A",
        "SPDXRef-File--src-EmbedIO.Samples-obj-EmbedIO.Samples.csproj.nuget.dgspec.json-28F25ED96EAD1D6ED1BC21D550A9A73ABA49C6D5",
        "SPDXRef-File--src-EmbedIO.Samples-html-partials-app-menu.html-E24F80346EBD7ADE3D1295043F1F8DEAA44EBFC2",
        "SPDXRef-File--src-EmbedIO.Samples-WebSocketTerminalModule.cs-899918C5D0617B6B8B297FDF7B3531FE378490AF",
        "SPDXRef-File--src-EmbedIO.Forms.Sample-EmbedIO.Forms.Sample.Android-Resources-layout-Toolbar.axml-C11F3FB8BC53948BC35C3B2B1328DC6F0AB00CAF",
        "SPDXRef-File--src-EmbedIO.Testing-obj-EmbedIO.Testing.csproj.nuget.g.targets-15B1BE874D4D7AB827BD18044B74AF8FEF6D0E5C",
        "SPDXRef-File--src-EmbedIO.Samples-html-css-embedio-icon.png-AAC80334397312AD9323DC3DBF2E3DD4A957BF32",
        "SPDXRef-File--src-EmbedIO.Samples-html-views-tubular.html-4A3119164D7D6E8E97BB94EC23FC069ABAAC3980",
        "SPDXRef-File--.git-objects-ad-4db327f5555268d51478273a64948fa8ccdd67-AF110D67A554FBDE8B68081EEAE718A1577950ED",
        "SPDXRef-File--.git-objects-d9-9ee895064ed0935249d51b10ba0a0f19b262c9-79938A951C3E6C92DE0AAC001ABF4C83FC930E36",
        "SPDXRef-File--.git-objects-02-e47a261154ed39af857a1b8475475b5507fb18-4D46553808CF48E0D1396BDF2D5928BEFF37A1F8",
        "SPDXRef-File--.git-objects-5a-9c82da9ae8740e5067333501e98408d6d0d0c3-B3F237E6D20A2698F7D259468A933B8257E4A4F5",
        "SPDXRef-File--.git-objects-94-4a1b6c44d05fca01cf1145721f63e2f6671022-C30B7F3AD4892E6A21748C9AC6140DB7F2B2B099",
        "SPDXRef-File--.git-objects-58-fe4ab95f812297a273684bfa5a92a9c6342814-29CA4AA2DA717289D332B4DC65D6488ABE0F93A3",
        "SPDXRef-File--.git-objects-32-1fa6c4c6023f1d6444bac56d43d44f567a0bb4-A7A59512287CAD02B1A1EA3DA5DD98AB6F06805E",
        "SPDXRef-File--.git-objects-9e-7fbd66b3d0d9947e7a18a3e32325a7dfc6b9e0-712870CDF3896D1F218AE3CEE27D2ECDFBE07189",
        "SPDXRef-File--.git-objects-03-49a16e219e6bc871e9e2959fe2c605462e1f4a-24208F04D1448ECCA31DACFE8C7CD760EC234E35",
        "SPDXRef-File--.git-objects-50-43efe25119a19e54cf0c9a9290294c9834125f-741AFDD97B5163C34B1893F65F2114BD43D02589",
        "SPDXRef-File--.git-objects-59-d174d7f946da457f4732b7eae30f83ac7ce3bb-2A32C0FE78C838460037019EE6CEF9458988C87E",
        "SPDXRef-File--.git-index-37078D778CCFCAE8869DE6536305F471D1EA3849",
        "SPDXRef-File--.github-workflows-codeql.yml-3F79AFF6A620FF8E7FB2792AA0606CEA0F8A26A5",
        "SPDXRef-File--test-EmbedIO.Tests-TestObjects-TestWebSocket.cs-EEAA870CB5D98835F7AFB5D7D78694D6AF5170BA",
        "SPDXRef-File--test-EmbedIO.Tests-Issues-Issue318-StartupDeadlock.cs-B5C857D7B12B5736026167035F834FEB12836096",
        "SPDXRef-File--test-EmbedIO.Tests-Issues-Issue351-WebApi.cs-57BACC102F19EA47607E61E3FE5136AB3DA6126D",
        "SPDXRef-File--test-EmbedIO.Tests-obj-EmbedIO.Tests.csproj.nuget.g.props-B00F33995C3BF45CFE9BFB63D1135B9692920B3C",
        "SPDXRef-File--test-EmbedIO.Tests-LocalSessionManagerTest.cs-ED1CB69A6D4F7D88071D42282BC0694AF060874B",
        "SPDXRef-File--test-EmbedIO.Tests-WebServerTest.cs-4DC3D5F8EE0B7DA51D2ED565301F964C51CB8F63",
        "SPDXRef-File--test-EmbedIO.Tests-FluentTest.cs-7C8315C60C5871DAE7D70D9FCBF3B3EF2140BD9D",
        "SPDXRef-File--README.md-BDA2701E870D24DF4B31DEB128F3F6844DFAD76E",
        "SPDXRef-File--CODE-OF-CONDUCT.md-D96481579F8B552BD86A3433BF24BD774844C4D3",
        "SPDXRef-File--src-EmbedIO.Samples-html-partials-app-person.html-ACBE098943C96E44573FE1ED54BAF335A218F44D",
        "SPDXRef-File--.git-objects-bb-fff0e0b327732136338f9b41ca3818fce656cc-C9FB2AD5BCBD9801F2B99490FD32FA2FE5080332",
        "SPDXRef-File--.git-objects-ac-cf545e2bfa78f9c64f0add3ed43f7de1ef2682-7532D4DF8C0AF20BD050D6D8380FBD6AE62E6845",
        "SPDXRef-File--.git-objects-a3-496f63d66212c5b0d1d0979a439a35f5cc6c12-C9A9D8C303B1E19925D81882420409DA9CDD59F9",
        "SPDXRef-File--.git-objects-5f-05481943af4f757b158bc8530246b85b138275-AC0D6BC7F041A3B0D1B7CD2DA2DE569478F74EC1",
        "SPDXRef-File--.git-objects-0e-e2688e8f18d750a6c28cc8ab795509bdd2c392-22738953662229F511EFC385FB2EA526E422FE43",
        "SPDXRef-File--.git-objects-0b-647022e24134da27b6e46d00099fb9e8bab981-E97DC8DBFF8E820FCF3C4CB03DBD95A3B197A931",
        "SPDXRef-File--.git-objects-35-11b96f3837071cd495c75c73fdda83109b8b4f-1B0EF21E64231670120660E64CEEB61C33DDD54C",
        "SPDXRef-File--.git-objects-04-8265cf8b68ce5a9192802c2cbb801a2d90139b-BF4F1AA9E6B16835153C0131D193B55F7AF7FB55",
        "SPDXRef-File--.git-objects-03-cde8ccfad8e7a3896ecd539f1cda3e55e8aa1c-5FE8E6F0154114447D2DE91874EE25679AA44D89",
        "SPDXRef-File--.git-objects-57-bc2c5e5c58a601b476cdf7d10b44c325774bba-A9215F70CBC6A227D7B142192F42EEB40DBEE1A1",
        "SPDXRef-File--.git-objects-92-0d0f26f61a908b4ea086d2062bb354c283008f-6504FB312B47B35EC0BEB43DA2A537B196682CA3",
        "SPDXRef-File--.git-FETCH-HEAD-752E26B0B005C3B746AB751C9211141BA47B4C53",
        "SPDXRef-File--.github-ISSUE-TEMPLATE-Feature-request.md-73A98280892B1A46317DAD9721B6DE5244DED398",
        "SPDXRef-File--test-EmbedIO.Tests-TestObjects-PeopleRepository.cs-EE9232924EBC086E51ABD2A4721C907A584BF779",
        "SPDXRef-File--test-EmbedIO.Tests-TestObjects-ObjectExtensions.cs-27A4864A371734F0B042FED66F434256215B7081",
        "SPDXRef-File--test-EmbedIO.Tests-Issues-Issue330-PreferCompressionFalse.cs-6EBE1BB9BF5884C75A73B7DEE9CF3BB33AD60C1B",
        "SPDXRef-File--test-EmbedIO.Tests-obj-project.assets.json-83976D2A36EB9CC6502FE487FF74411BA0682C57",
        "SPDXRef-File--test-EmbedIO.Tests-ExceptionHandlingTest.cs-2DBEE805D1EA7D7E36EC4B7463465C7B73940CD9",
        "SPDXRef-File--test-EmbedIO.Tests-IWebServerTest.cs-4F84617F921A4DA8DD60F567C17B1646EDCC4BEF",
        "SPDXRef-File--test-EmbedIO.Tests-ActionModuleTest.cs-25E38EA2DF7DA5CF13631CA6D30E63910CE86F9C",
        "SPDXRef-File--appveyor.yml-D56872C80AE0167EC9107EF30EF9B90B6B3D1ACB",
        "SPDXRef-File--StyleCop.Analyzers.ruleset-91B7F2320CAF6D3600BB411CA4104FA95A16BFF5",
        "SPDXRef-File--src-EmbedIO.Samples-html-scripts-tubular-tubular-bundle.css-5CC89E6D1FCE4049932C330F67DBCAAB12255726",
        "SPDXRef-File--.git-description-9635F1B7E12C045212819DD934D809EF07EFA2F4",
        "SPDXRef-File--.github-stale.yml-E3C90EA19F7A09533555E437AFF7C067EF613A4B",
        "SPDXRef-File--test-EmbedIO.Tests-TestObjects-TestLocalSessionController.cs-4F262309F05A88D6F98E5DAFE798DA2FCB1EF4F8",
        "SPDXRef-File--test-EmbedIO.Tests-Issues-Issue352-FileSystemProviderEscapedString.cs-B215528292793AE497FD5A39AF30D37ACDB3C8CF",
        "SPDXRef-File--test-EmbedIO.Tests-Issues-Issue409-CookiePath.cs-E4CA9B2CE7753E53FA7C0025CE48E8FF732D43B0",
        "SPDXRef-File--test-EmbedIO.Tests-obj-project.nuget.cache-DCC16A3570530C4C5A1DD65E182A2E725A36D8AE",
        "SPDXRef-File--test-EmbedIO.Tests-EmbedIO.Tests.csproj-EE1481C32006170B600AA1EA6E0ACD4397361BE4",
        "SPDXRef-File--test-EmbedIO.Tests-RegexRoutingTest.cs-EC0F4F583D27542205633DDFF8E88B107E83A0FD",
        "SPDXRef-File--test-EmbedIO.Tests-DirectoryBrowserTest.cs-254AE166693BD8EAEA6A9B338C4E5E39F7B4D2EE",
        "SPDXRef-File--toc.yml-9DB57F8BC45868B6A0F88AD49D7C4474408D0158"
      ]
    }
  ],
  "externalDocumentRefs": [],
  "relationships": [
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-930A940927E2F2ACCFB50E7E3C1DE7170F84695F12046CB49ED006AFAD78E6A1",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DESCRIBES",
      "relatedSpdxElement": "SPDXRef-RootPackage",
      "spdxElementId": "SPDXRef-DOCUMENT"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-E410F042AA2A506E114A7862764CA009254E81AB885859709107C80D95928B65",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-068BFA3B59591FD6452F69A2EEBBE970BAB7A4FB982604A61DA03CB9B5D0091E",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-781C50A98A285B9BB69D0050795F91134F1A14E59C6CA75F06BE606F1F8F89D6",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-449FA483DAB78707360B58441C2D5BD4E2F5E683A4806E05A111D6EE505B81EA",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-E3502C1021CBB5BB09BFCC676ABD160F59F2168C35D9FB6FF2DAC3CE9A17AD23",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-52358C2D014206CBB069F497F1733F57788AAAB3507E4A6417069998F3B486DF",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-3D762E0F169506279F40A11F69CB7F7E9DA3F36F47D6E7C2E17C3161DADB7FE8",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-95988ACE14A368B8C3409E145AA92C0F93D243DD95C5FB89A6CAABAAD0D1115D",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-AC43CF918CC0478383611B7AAD3EBFC9B023CD761B5AC8D5208286EFBE599015",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-E5EE6EA84A72B4995DB540420D83E79A943C54DAEBF1D9032BD5B56DD003445E",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-622AFA62783284D54C08FAB39928AAB502604CE350ED14CA42BC8D0B858552B0",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-2ADE5DBB828ACE8FA25CDCEB77507D26A832BC3F7580A468FA0AAE065CC237AD",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-C1475C5380732C85127A15B8BADF74D2619786E90578875B650082AE4497BC14",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-23A6B66FF601D949E3AC28A6A392DC5F01458AB6F9CEDFCD3A17091B2F26BDD5",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-9E33C25A33A148C7F507C2F5039687C71E645F0B3596D83484C775AF7A8BFBAE",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-B458072059F54518C1B25496F3D09765CF472A492FD7108B5FCB9E3545DD6237",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-F2F4C0E260F287DBD785B1ABCA39F1E1D27C07AADD71DFF7E83C0A5F16327707",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-6749A6401B0F20517D91787BD129A9BA4B75C2874B0A96F69A17D2476683F895",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-50D975328CA1C4FF12863549F4DC7468E12D39B32AC5367525B5D30B088D6037",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-BE81CAD2FFD8AE7908F1AAB2DAD5A57984A518D56B6273446E3A7534F6479803",
      "spdxElementId": "SPDXRef-RootPackage"
    },
    {
      "relationshipType": "DEPENDS_ON",
      "relatedSpdxElement": "SPDXRef-Package-C6D08745A01E5768789F7336947C2F95A9AA434D8D3306C689C82D69E8F6A16E",
      "spdxElementId": "SPDXRef-RootPackage"
    }
  ],
  "spdxVersion": "SPDX-2.2",
  "dataLicense": "CC0-1.0",
  "SPDXID": "SPDXRef-DOCUMENT",
  "name": "demo 1.0.0",
  "documentNamespace": "https://spdx.org/spdxdocs/sbom-tool-2.2.6-3502372f-197f-4601-8a2d-28845cbfd7c6/demo/1.0.0/xNyG-JCA-EqFCrrBSdGVlw",
  "creationInfo": {
    "created": "2024-06-16T09:27:30Z",
    "creators": [
      "Organization: none",
      "Tool: Microsoft.SBOMTool-2.2.6"
    ]
  },
  "documentDescribes": [
    "SPDXRef-RootPackage"
  ]
}
```

This is the only generator that appends all files into the SBOM, including dev dependencies and the dependency tree. However, it doesn’t properly parse licenses and, as mentioned, it generates SPDX 2.2 only.

It is worth mentioning that generating the SBOM was simple and did not require any build or lockfile generation. Performing those additional steps would yield the same results.

## Conclusion

It’s safe to say that lockfiles are the key for the most complete SBOMs. Make sure to generate, update and maintain your project when you add or remove dependencies.

As mentioned, different projects have different needs, so be sure to choose the generator that works best for you. If licenses are important to you, we recommend using **trivy**. It generates either SPDX or CDX, supports transitive dependencies, and generates a dependency tree. Ensure you use the correct configurations and prefer the `nuget` cataloger over the `dotnet-core` cataloger. Otherwise, **syft** is still a viable choice, providing great coverage and CPE generation. If you only need CDX or SPDX SBOMs, **cdxgen** and **sbom-tool** generate decent results with a hassle-free process, where **sbom-tool** also adds all files detected to the SBOM as well.
