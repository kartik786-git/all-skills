# AI Coding Assistant Skills for .NET

A comprehensive collection of **90+ reusable skills** (107 SKILL.md files across plugin packages) for AI coding assistants — purpose-built for .NET development, diagnostics, testing, performance analysis, and cross-platform debugging.

This repository is designed to work with **any AI coding assistant** that supports custom instructions, rules, or skills. Just copy the skill folders you need into the right directory for your tool, and your AI assistant will instantly have deep expertise in that domain.

---

## Quick Start

```bash
# Clone the repository
git clone <this-repo> all-skills
cd all-skills

# Choose your AI assistant and pick the install method below
```

---

## Skill Installation by Assistant

Each AI coding assistant looks for skills/instructions in specific locations. Copy the skill folders from `skills/` into one of the paths below.

### Priority Order (for assistants that support multiple locations)

Project-level paths override global paths. Global paths override built-in defaults.

---

### Codebuff

| Level | Path |
|-------|------|
| **Global** | `~/.agents/skills/<skill-name>/SKILL.md` |
| **Global (Claude compat)** | `~/.claude/skills/<skill-name>/SKILL.md` |
| **Project** | `.agents/skills/<skill-name>/SKILL.md` |
| **Project (Claude compat)** | `.claude/skills/<skill-name>/SKILL.md` |

**Install:**
```bash
# Project-level (recommended)
mkdir -p .agents/skills
cp -r skills/<skill-folder> .agents/skills/

# Or global level
mkdir -p ~/.agents/skills
cp -r skills/<skill-folder> ~/.agents/skills/
```

> **Note:** Restart Codebuff after adding skills. Skills are auto-discovered on startup.

---

### Claude Code (Anthropic)

| Level | Path |
|-------|------|
| **Global** | `~/.claude/skills/<skill-name>/SKILL.md` |
| **Global rules** | `~/.claude/rules/*.md` |
| **Global instructions** | `~/.claude/CLAUDE.md` |
| **Project** | `.claude/skills/<skill-name>/SKILL.md` |
| **Project rules** | `.claude/rules/*.md` |
| **Project instructions** | `.claude/CLAUDE.md` |

**Install:**
```bash
# Project-level
mkdir -p .claude/skills
cp -r skills/<skill-folder> .claude/skills/

# Or global (all projects)
mkdir -p ~/.claude/skills
cp -r skills/<skill-folder> ~/.claude/skills/
```

> **Note:** Skills in `.claude/skills/` are automatically available. Rules in `.claude/rules/*.md` can be scoped with glob patterns. `CLAUDE.md` provides project-level system instructions.

---

### GitHub Copilot

Copilot supports two separate mechanisms for custom skills:

**A) Repository Instructions** — project-level guidance via Markdown files

| Level | Path |
|-------|------|
| **Project** | `.github/copilot-instructions.md` |
| **Project path-specific** | `.github/instructions/*.instructions.md` |

**B) Copilot Extensions / Agent Skills** — reusable skill modules (global)

| Level | Path |
|-------|------|
| **Global (Windows)** | `%USERPROFILE%\.copilot\skills\<skill-name>\` |
| **Global (macOS/Linux)** | `~/.copilot/skills/<skill-name>/` |
| **Project** | `.github/skills/<skill-name>/` |

**Install:**
```bash
# Option A: Repository instructions
mkdir -p .github/instructions
cat skills/<skill-folder>/SKILL.md >> .github/copilot-instructions.md
# Or as separate files:
cp skills/<skill-folder>/SKILL.md .github/instructions/<skill-name>.instructions.md

# Option B: Agent Skills (global — Windows)
mkdir "%USERPROFILE%\.copilot\skills\<skill-name>"
xcopy /E skills\<skill-folder> "%USERPROFILE%\.copilot\skills\<skill-name>\"

# Option B: Agent Skills (global — macOS/Linux)
mkdir -p ~/.copilot/skills/<skill-name>
cp -r skills/<skill-folder>/* ~/.copilot/skills/<skill-name>/
```

> **Note:** Option A injects instruction text into Copilot Chat. Option B (global skills) registers reusable agent skills that Copilot can invoke — this is the mechanism the user referenced with `%USERPROFILE%\.copilot\skills`. For the latest details, check [Copilot Extensions documentation](https://docs.github.com/en/copilot/using-github-copilot/using-extensions-to-integrate-external-tools-with-copilot-chat).

---

### Cursor

| Level | Path |
|-------|------|
| **Project rules** | `.cursor/rules/*.mdc` |
| **Project (legacy)** | `.cursorrules` |
| **Project (legacy)** | `AGENTS.md` |

**Install:**
```bash
mkdir -p .cursor/rules

# Convert SKILL.md to .mdc format
# Each skill becomes a rule file:
cp skills/<skill-folder>/SKILL.md .cursor/rules/<skill-name>.mdc
```

> **Note:** Cursor's `.mdc` files support YAML frontmatter for glob-based scoping (e.g., `when: "*.cs"`). You can add frontmatter to each `.mdc` file to control when the rule activates.

---

### Windsurf (Cascade)

| Level | Path |
|-------|------|
| **Project rules** | `.windsurf/rules/*.md` |
| **Project (legacy)** | `.windsurfrules` |

**Install:**
```bash
mkdir -p .windsurf/rules
cp skills/<skill-folder>/SKILL.md .windsurf/rules/<skill-name>.md
```

---

### Continue.dev

| Level | Path |
|-------|------|
| **Global config** | `~/.continue/config.json` (or `config.yaml`) |
| **Project rules** | `.continue/rules/*.md` |

**Install:**
```bash
mkdir -p .continue/rules
cp skills/<skill-folder>/SKILL.md .continue/rules/<skill-name>.md
```

> **Note:** To reference these rules in your config, add a `rules` entry pointing to the `.continue/rules/` directory.

---

### Aider

| Level | Path |
|-------|------|
| **Project** | `CONVENTIONS.md` |
| **Project config** | `.aider.conf.yml` |
| **Global** | `~/.CONVENTIONS.md` |
| **Global config** | `~/.aider.conf.yml` |

**Install:**
```bash
# Append skill content to CONVENTIONS.md
cat skills/<skill-folder>/SKILL.md >> CONVENTIONS.md
```

> **Note:** Aider reads `CONVENTIONS.md` from the repo root and injects it as context. You can reference multiple skills by concatenating them.

---

### OpenCode (Sourcegraph Cody)

| Level | Path |
|-------|------|
| **Global config** | `~/.opencode/config.json` |
| **Project config** | `.opencode.json` or `.vscode/settings.json` |
| **Project instructions** | `.github/copilot-instructions.md` (compatible) |
| **Cody custom commands** | `.vscode/cody.json` |

**Install:**
```bash
# OpenCode respects .github/copilot-instructions.md and similar files
# Copy skill content into your project instructions file:
cat skills/<skill-folder>/SKILL.md >> .github/copilot-instructions.md

# Or configure a custom Cody command in .vscode/cody.json:
echo '{"commands": {"my-skill": {"prompt": "..."}}}' > .vscode/cody.json
```

> **Note:** OpenCode is Sourcegraph's open-source CLI coding agent. It reads project context from standard instruction files, and can be configured via `~/.opencode/config.json` for global settings or `.opencode.json` for per-project overrides.

---

## Available Skills

<details>
<summary><b>📍 Performance & Benchmarking</b> (3 skills)</summary>

| Skill | Description |
|-------|-------------|
| [microbenchmarking](skills/microbenchmarking/) | Design, run, and analyze BenchmarkDotNet microbenchmarks — project setup, configuration, comparison strategies, and diagnosers |
| [analyzing-dotnet-performance](skills/analyzing-dotnet-performance/) | Scan C#/.NET code for 50+ performance anti-patterns across async, memory, strings, collections, LINQ, regex, serialization, and I/O |
| [optimizing-ef-core-queries](skills/optimizing-ef-core-queries/) | Identify and fix Entity Framework Core query performance issues |

</details>
<details>
<summary><b>🔍 Diagnostics & Debugging</b> (5 skills)</summary>

| Skill | Description |
|-------|-------------|
| [dotnet-trace-collect](skills/dotnet-trace-collect/) | Collect .NET traces using dotnet-monitor, dotnet-trace, perfcollect, and PerfView |
| [dump-collect](skills/dump-collect/) | Collect .NET crash/memory dumps — CoreCLR, NativeAOT, and container environments |
| [clr-activation-debugging](skills/clr-activation-debugging/) | Debug CLR activation and loading issues — COM activation, hosting logs, and activation flow |
| [apple-crash-symbolication](skills/apple-crash-symbolication/) | Symbolicate Apple crash reports (.ips format) with PowerShell scripts |
| [android-tombstone-symbolication](skills/android-tombstone-symbolication/) | Symbolicate Android NDK tombstone crash dumps with PowerShell scripts |

</details>

<details>
<summary><b>⚙️ .NET Development</b> (4 skills)</summary>

| Skill | Description |
|-------|-------------|
| [csharp-scripts](skills/csharp-scripts/) | Write and run C# scripts (.csx) for automation and prototyping |
| [dotnet-pinvoke](skills/dotnet-pinvoke/) | Author P/Invoke declarations with correct type mappings and diagnostics |
| [nuget-trusted-publishing](skills/nuget-trusted-publishing/) | Set up and configure trusted NuGet publishing workflows |
| [dotnet-aot-compat](skills/dotnet-upgrade/skills/dotnet-aot-compat/) | Enable Native AOT compatibility for .NET projects |

</details>

<details>
<summary><b>🔄 Framework Upgrades</b> (6 skills)</summary>

| Skill | Description |
|-------|-------------|
| [migrate-dotnet8-to-dotnet9](skills/dotnet-upgrade/skills/migrate-dotnet8-to-dotnet9/) | Migrate projects from .NET 8 to .NET 9 |
| [migrate-dotnet9-to-dotnet10](skills/dotnet-upgrade/skills/migrate-dotnet9-to-dotnet10/) | Migrate projects from .NET 9 to .NET 10 |
| [migrate-dotnet10-to-dotnet11](skills/dotnet-upgrade/skills/migrate-dotnet10-to-dotnet11/) | Migrate projects from .NET 10 to .NET 11 |
| [migrate-nullable-references](skills/dotnet-upgrade/skills/migrate-nullable-references/) | Enable nullable reference types and fix warnings |
| [thread-abort-migration](skills/dotnet-upgrade/skills/thread-abort-migration/) | Migrate code away from deprecated Thread.Abort API |
| [system-text-json-net11](skills/dotnet11/skills/system-text-json-net11/) | Use new System.Text.Json features in .NET 11 |

</details>

<details>
<summary><b>🌐 ASP.NET Core & Web</b> (4 skills)</summary>

| Skill | Description |
|-------|-------------|
| [dotnet-webapi](skills/dotnet-aspnetcore/skills/dotnet-webapi/) | Build RESTful APIs with ASP.NET Core controllers and minimal APIs |
| [minimal-api-file-upload](skills/dotnet-aspnetcore/skills/minimal-api-file-upload/) | Implement file uploads in ASP.NET Core minimal APIs |
| [configuring-opentelemetry-dotnet](skills/dotnet-aspnetcore/skills/configuring-opentelemetry-dotnet/) | Set up OpenTelemetry for .NET applications |
| [convert-blazor-server-to-webapp](skills/dotnet-aspnetcore/skills/convert-blazor-server-to-webapp/) | Convert Blazor Server to the unified Blazor Web App model |

</details>

<details>
<summary><b>🖥️ Blazor</b> (9 skills)</summary>

| Skill | Description |
|-------|-------------|
| [create-blazor-project](skills/dotnet-blazor/skills/create-blazor-project/) | Scaffold new Blazor projects with the right render mode and configuration |
| [author-component](skills/dotnet-blazor/skills/author-component/) | Build Blazor components with best practices for lifecycle, disposal, and async |
| [collect-user-input](skills/dotnet-blazor/skills/collect-user-input/) | Handle forms, validation, and user input in Blazor |
| [configure-auth](skills/dotnet-blazor/skills/configure-auth/) | Set up authentication and authorization in Blazor |
| [coordinate-components](skills/dotnet-blazor/skills/coordinate-components/) | Manage component communication and state coordination |
| [fetch-and-send-data](skills/dotnet-blazor/skills/fetch-and-send-data/) | Implement data access patterns in Blazor apps |
| [plan-ui-change](skills/dotnet-blazor/skills/plan-ui-change/) | Plan and structure UI changes in Blazor applications |
| [support-prerendering](skills/dotnet-blazor/skills/support-prerendering/) | Add prerendering support to Blazor components |
| [use-js-interop](skills/dotnet-blazor/skills/use-js-interop/) | Integrate JavaScript interop in Blazor applications |

</details>

<details>
<summary><b>📱 .NET MAUI</b> (8 skills)</summary>

| Skill | Description |
|-------|-------------|
| [dotnet-maui-doctor](skills/dotnet-maui/skills/dotnet-maui-doctor/) | Diagnose and fix .NET MAUI installation and environment issues |
| [maui-app-lifecycle](skills/dotnet-maui/skills/maui-app-lifecycle/) | Manage MAUI application lifecycle events |
| [maui-collectionview](skills/dotnet-maui/skills/maui-collectionview/) | Build performant CollectionView controls in MAUI |
| [maui-data-binding](skills/dotnet-maui/skills/maui-data-binding/) | Implement data binding patterns in MAUI |
| [maui-dependency-injection](skills/dotnet-maui/skills/maui-dependency-injection/) | Configure DI in .NET MAUI applications |
| [maui-safe-area](skills/dotnet-maui/skills/maui-safe-area/) | Handle safe area insets in MAUI layouts |
| [maui-shell-navigation](skills/dotnet-maui/skills/maui-shell-navigation/) | Implement Shell-based navigation in MAUI |
| [maui-theming](skills/dotnet-maui/skills/maui-theming/) | Apply theming and styling in MAUI apps |

</details>

<details>
<summary><b>🏗️ MSBuild</b> (18 skills)</summary>

| Skill | Description |
|-------|-------------|
| [binlog-failure-analysis](skills/dotnet-msbuild/skills/binlog-failure-analysis/) | Analyze MSBuild binary logs to diagnose build failures |
| [binlog-generation](skills/dotnet-msbuild/skills/binlog-generation/) | Generate MSBuild binary logs for debugging |
| [build-parallelism](skills/dotnet-msbuild/skills/build-parallelism/) | Optimize MSBuild parallel build configuration |
| [build-perf-baseline](skills/dotnet-msbuild/skills/build-perf-baseline/) | Establish build performance baselines |
| [build-perf-diagnostics](skills/dotnet-msbuild/skills/build-perf-diagnostics/) | Diagnose MSBuild build performance issues |
| [check-bin-obj-clash](skills/dotnet-msbuild/skills/check-bin-obj-clash/) | Detect and resolve bin/obj directory conflicts |
| [directory-build-organization](skills/dotnet-msbuild/skills/directory-build-organization/) | Organize Directory.Build.props/targets across projects |
| [eval-performance](skills/dotnet-msbuild/skills/eval-performance/) | Optimize MSBuild evaluation performance |
| [extension-points](skills/dotnet-msbuild/skills/extension-points/) | Use MSBuild extension points effectively |
| [including-generated-files](skills/dotnet-msbuild/skills/including-generated-files/) | Include auto-generated files in MSBuild projects |
| [incremental-build](skills/dotnet-msbuild/skills/incremental-build/) | Optimize incremental builds with correct inputs/outputs |
| [item-management](skills/dotnet-msbuild/skills/item-management/) | Manage MSBuild items effectively |
| [msbuild-antipatterns](skills/dotnet-msbuild/skills/msbuild-antipatterns/) | Detect and fix common MSBuild anti-patterns |
| [msbuild-modernization](skills/dotnet-msbuild/skills/msbuild-modernization/) | Modernize legacy MSBuild projects to SDK-style |
| [msbuild-server](skills/dotnet-msbuild/skills/msbuild-server/) | Configure and use MSBuild server for faster builds |
| [property-patterns](skills/dotnet-msbuild/skills/property-patterns/) | Apply MSBuild property patterns correctly |
| [resolve-project-references](skills/dotnet-msbuild/skills/resolve-project-references/) | Resolve and simplify project reference issues |
| [target-authoring](skills/dotnet-msbuild/skills/target-authoring/) | Write correct MSBuild targets with proper conditions |

</details>

<details>
<summary><b>🧪 Testing</b> (17 skills)</summary>

| Skill | Description |
|-------|-------------|
| [run-tests](skills/dotnet-test/skills/run-tests/) | Run .NET tests via `dotnet test` with automatic platform/framework detection |
| [code-testing-agent](skills/dotnet-test/skills/code-testing-agent/) | Multi-agent pipeline that generates tests for any language |
| [writing-mstest-tests](skills/dotnet-test/skills/writing-mstest-tests/) | Best practices for writing MSTest 3.x/4.x tests |
| [test-anti-patterns](skills/dotnet-test/skills/test-anti-patterns/) | Scan tests for common anti-patterns (polyglot) |
| [test-smell-detection](skills/dotnet-test/skills/test-smell-detection/) | Deep audit using academic test smell taxonomy (polyglot) |
| [assertion-quality](skills/dotnet-test/skills/assertion-quality/) | Measure assertion variety and depth (polyglot) |
| [test-gap-analysis](skills/dotnet-test/skills/test-gap-analysis/) | Pseudo-mutation analysis to find test blind spots (polyglot) |
| [test-tagging](skills/dotnet-test/skills/test-tagging/) | Tag tests with standardized traits (polyglot) |
| [grade-tests](skills/dotnet-test/skills/grade-tests/) | Grade individual test methods A–F (polyglot) |
| [coverage-analysis](skills/dotnet-test/skills/coverage-analysis/) | Collect coverage and compute CRAP scores (.NET) |
| [crap-score](skills/dotnet-test/skills/crap-score/) | Calculate Change Risk Anti-Pattern scores (.NET) |
| [detect-static-dependencies](skills/dotnet-test/skills/detect-static-dependencies/) | Find hard-to-test static dependencies (.NET) |
| [generate-testability-wrappers](skills/dotnet-test/skills/generate-testability-wrappers/) | Generate wrappers for static APIs (.NET) |
| [migrate-static-to-wrapper](skills/dotnet-test/skills/migrate-static-to-wrapper/) | Bulk-replace static calls with injected wrappers (.NET) |
| [mtp-hot-reload](skills/dotnet-test/skills/mtp-hot-reload/) | Rapid test-fix iteration using MTP hot reload |
| [filter-syntax](skills/dotnet-test/skills/filter-syntax/) | Test filter syntax reference for VSTest and MTP |
| [platform-detection](skills/dotnet-test/skills/platform-detection/) | Detect VSTest vs MTP and test framework from project files |

</details>

<details>
<summary><b>🔄 Test Migration</b> (5 skills)</summary>

| Skill | Description |
|-------|-------------|
| [migrate-mstest-v1v2-to-v3](skills/dotnet-test-migration/skills/migrate-mstest-v1v2-to-v3/) | Upgrade MSTest v1/v2 to v3 |
| [migrate-mstest-v3-to-v4](skills/dotnet-test-migration/skills/migrate-mstest-v3-to-v4/) | Upgrade MSTest v3 to v4 |
| [migrate-xunit-to-xunit-v3](skills/dotnet-test-migration/skills/migrate-xunit-to-xunit-v3/) | Upgrade xUnit.net v2 to v3 |
| [migrate-xunit-to-mstest](skills/dotnet-test-migration/skills/migrate-xunit-to-mstest/) | Convert xUnit projects to MSTest v4 |
| [migrate-vstest-to-mtp](skills/dotnet-test-migration/skills/migrate-vstest-to-mtp/) | Migrate from VSTest to Microsoft.Testing.Platform |

</details>

<details>
<summary><b>🤖 .NET AI / MCP</b> (5 skills)</summary>

| Skill | Description |
|-------|-------------|
| [mcp-csharp-create](skills/dotnet-ai/skills/mcp-csharp-create/) | Create MCP servers in C# |
| [mcp-csharp-test](skills/dotnet-ai/skills/mcp-csharp-test/) | Test MCP server implementations |
| [mcp-csharp-debug](skills/dotnet-ai/skills/mcp-csharp-debug/) | Debug MCP servers with IDE config and MCP Inspector |
| [mcp-csharp-publish](skills/dotnet-ai/skills/mcp-csharp-publish/) | Publish MCP servers to NuGet, Docker, or Azure |
| [technology-selection](skills/dotnet-ai/skills/technology-selection/) | Evaluate and select AI/ML technologies for .NET projects |

</details>

<details>
<summary><b>🏗️ .NET Template Engine</b> (6 skills)</summary>

| Skill | Description |
|-------|-------------|
| [template-authoring](skills/dotnet-template-engine/skills/template-authoring/) | Author .NET project templates |
| [template-instantiation](skills/dotnet-template-engine/skills/template-instantiation/) | Instantiate .NET templates with correct parameters |
| [template-discovery](skills/dotnet-template-engine/skills/template-discovery/) | Discover installed and available templates |
| [template-comparison](skills/dotnet-template-engine/skills/template-comparison/) | Compare template outputs side-by-side |
| [template-validation](skills/dotnet-template-engine/skills/template-validation/) | Validate template correctness and structure |
| [template-smart-defaults](skills/dotnet-template-engine/skills/template-smart-defaults/) | Configure smart defaults for template parameters |

</details>

<details>
<summary><b>📦 NuGet</b> (1 skill)</summary>

| Skill | Description |
|-------|-------------|
| [convert-to-cpm](skills/dotnet-nuget/skills/convert-to-cpm/) | Convert projects to Central Package Management |

</details>

---

## Skill Format

Each skill is a directory containing:

```
<skill-name>/
├── SKILL.md          # Main skill definition with YAML frontmatter
├── references/       # (optional) Reference documents loaded by the skill
└── scripts/          # (optional) Helper scripts for automation
```

### SKILL.md Frontmatter

```yaml
---
name: <skill-name>
description: >-
  Brief description of when and why to use this skill.
license: MIT
---
```

### Naming Rules

- 1–64 characters
- Lowercase letters, numbers, and hyphens only
- Must match the directory name exactly

---

## Why Use This Repository

- **One-time setup, universal knowledge** — Install once, and your AI assistant instantly gains deep .NET expertise without needing to learn from scratch
- **Up-to-date** — Skills cover the latest .NET versions including .NET 11, C# 14, and modern APIs
- **Assistant-agnostic** — Works with Codebuff, Claude Code, Cursor, GitHub Copilot, Windsurf, Continue.dev, Aider, and more
- **Production-ready** — Each skill includes battle-tested workflows, reference documents, and validation steps
- **Modular** — Install only the skills you need. No bloated configuration
- **Polyglot testing** — Many test analysis skills work across C#, Python, TypeScript, Java, Go, Ruby, Rust, Kotlin, Swift, and C++

---

## Repository Structure

```
all-skills/
├── README.md                          # This file
├── skills/                            # All skills organized by category
│   ├── microbenchmarking/             # Standalone skills (top-level)
│   ├── analyzing-dotnet-performance/
│   ├── ...
│   ├── dotnet/                        # Plugin groups with sub-skills
│   │   ├── skills/
│   │   │   ├── csharp-scripts/
│   │   │   ├── dotnet-pinvoke/
│   │   │   └── nuget-trusted-publishing/
│   │   └── plugin.json
│   ├── dotnet-test/
│   │   ├── skills/                    # 20+ test skills
│   │   ├── agents/                    # Orchestrator agents
│   │   └── plugin.json
│   ├── dotnet-aspnetcore/
│   ├── dotnet-blazor/
│   ├── dotnet-maui/
│   ├── dotnet-msbuild/                # 18 MSBuild skills
│   ├── dotnet-upgrade/                # Migration skills
│   └── ...
```

---

## FAQ

**Q: Do I need to install all 90+ skills?**
No. Pick the skills relevant to your project. Start with the ones for your tech stack and add more as needed.

**Q: Will skills conflict with each other?**
No. Each skill is independently scoped. Your AI assistant loads only the skills whose names match what it needs.

**Q: How do I update a skill?**
Pull the latest from this repo and overwrite the skill folder in your installation directory.

**Q: Can I create my own skills?**
Absolutely. Follow the SKILL.md format above. Place custom skills in the same directories alongside the ones from this repo.
