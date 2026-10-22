# OxyKit

[![Docs](https://img.shields.io/badge/docs-oxykit.dev-1f6f5b)](https://oxykit.dev)
[![NuGet](https://img.shields.io/nuget/v/OxyKit.Render.Client.svg?label=Render.Client)](https://www.nuget.org/packages/OxyKit.Render.Client)
[![NuGet](https://img.shields.io/nuget/v/OxyKit.Mail.Client.svg?label=Mail.Client)](https://www.nuget.org/packages/OxyKit.Mail.Client)
[![License: MIT](https://img.shields.io/badge/code-MIT-blue.svg)](https://oxykit.dev/guide/license)
[![Docs license](https://img.shields.io/badge/docs-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![.NET](https://img.shields.io/badge/.NET-10-512BD4.svg)](https://dotnet.microsoft.com/download)

Toolkit for **document rendering**, **email delivery**, and **job orchestration** — process-isolated engines you wire yourself.

**Website:** [oxykit.dev](https://oxykit.dev) · **GitHub:** [oxykit-dev](https://github.com/oxykit-dev)

## Products

| Product | Role |
|---------|------|
| **[OxyKit.Render](https://github.com/oxykit-dev/OxyKit.Render)** | HTTP sidecar: JSON in, PDF / XLSX / CSV / HTML out. Typed .NET client. |
| **[OxyKit.Mail](https://github.com/oxykit-dev/OxyKit.Mail)** | Email delivery API — queue, retries, DKIM, JWT and API keys. Typed .NET client. |
| **[oxykit-mail-web](https://github.com/oxykit-dev/oxykit-mail-web)** | Vue dashboard companion for Mail. |
| **[OxyKit.Flow](https://github.com/oxykit-dev/OxyKit.Flow)** | Job orchestrator — uses `OxyKit.Render.Client`; delivers via file or Mail. |

```text
  [data / triggers]
         |
         v
   OxyKit.Flow  ----render---->  OxyKit.Render
         |
         +----file----> disk
         |
         +----mail---->  OxyKit.Mail  ----SMTP----> inbox
```

Flow never embeds generators. Render stays isolated so alternate engines can sit beside it. Mail owns SMTP — callers must not re-send on `accepted`. Flow talks to Mail over HTTP (not Mail.Client).

## NuGet & releases

| Artifact | Where |
|----------|--------|
| `OxyKit.Render.Client` (+ Contracts) | [nuget.org](https://www.nuget.org/packages/OxyKit.Render.Client) · [Releases](https://github.com/oxykit-dev/OxyKit.Render/releases) |
| `OxyKit.Mail.Client` (+ Contracts) | [nuget.org](https://www.nuget.org/packages/OxyKit.Mail.Client) · [Releases](https://github.com/oxykit-dev/OxyKit.Mail/releases) |
| Runnable hosts (Render / Mail / Flow) | Per-repo Releases — linux-x64 / win-x64 / osx-arm64 zips (needs [.NET 10](https://dotnet.microsoft.com/download/dotnet/10.0)) |

```bash
dotnet add package OxyKit.Render.Client
dotnet add package OxyKit.Mail.Client
```

Hosts and Core stay out of NuGet — Client + Contracts only. Flow has no NuGet package.

## Docs

- [oxykit.dev](https://oxykit.dev) — landing + guides
- Per-repo `README.md` for quick start

## Boundaries

- **Render** = engine only (no tenancy / billing)
- **Mail** = mail API (UI is oxykit-mail-web)
- **Flow** = orchestration only (uses Render’s client + HTTP to Mail)

## Stack

.NET 10 · FastEndpoints (Mail / Flow) · Minimal API (Render) · Vue 3 (mail-web)
