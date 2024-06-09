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
s{
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

**TODO**:

Add **sbom-tool** results.

## Conclusion

It’s safe to say that lockfiles are the key for the most complete SBOMs. Make sure to generate, update and maintain your project when you add or remove dependencies.

As mentioned, different projects have different needs, make sure to pick the generator that works best for you.
