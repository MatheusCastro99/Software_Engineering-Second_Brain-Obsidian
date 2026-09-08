---
tags:
  - shipping-solutions
  - powershell
  - automation
category: Shipping Solutions
related: Docker commands, Docker Basics, CI-CD Pipeline
---

# ForEach-Object `$_.` and Other Useful PowerShell Tricks

PowerShell pipelines pass objects from one command to the next. `ForEach-Object` runs a script block for each incoming object, and `$_` represents the current object inside that script block.

## Basic Syntax

```powershell
Get-Process | ForEach-Object {
	"Process: $($_.Name), ID: $($_.Id)"
}
```

The long form is useful when the operation contains multiple statements. For simple property selection, use the shorter alias carefully:

```powershell
Get-Process | ForEach-Object Name
```

`$_` is an automatic variable scoped to the current pipeline script block. It is not a general-purpose variable outside that context.

## Filtering and Transforming

```powershell
Get-ChildItem -Filter '*.log' |
	Where-Object Length -gt 1MB |
	ForEach-Object {
		[PSCustomObject]@{
			File = $_.FullName
			SizeMB = [math]::Round($_.Length / 1MB, 2)
		}
	}
```

Prefer `Where-Object` for filtering and `ForEach-Object` for transformation or side effects. When a cmdlet supports a direct filter parameter, use it because it is usually clearer and more efficient.

## Docker Automation

```powershell
docker ps -aq |
	ForEach-Object { docker stop $_ }
```

The command above stops all container IDs returned by `docker ps -aq`; use it only when stopping every container is intentional. A safer targeted version is:

```powershell
docker ps --filter "label=project=demo" -q |
	ForEach-Object { docker stop $_ }
```

For bulk operations, preview the pipeline before adding a destructive command such as `docker rm`, `docker rmi`, or `Remove-Item`.

## Useful Automatic Variables

| Variable | Meaning |
|----------|---------|
| `$_` | Current pipeline object |
| `$PSItem` | Readable alias for `$_` |
| `$args` | Arguments passed to a script or function |
| `$?` | Whether the previous command succeeded |
| `$LASTEXITCODE` | Exit code from the last native application |
| `$null` | Represents no value |
| `$PWD` | Current working directory object |

## Pipeline Alternatives

Use native cmdlets where they express the operation directly:

```powershell
Get-ChildItem -File | Select-Object Name, Length
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-Service | Where-Object Status -eq 'Running'
```

Avoid converting objects to strings too early. Object properties remain searchable, sortable, and selectable until formatting commands such as `Format-Table` or `Format-List` are used.

## Error Handling

```powershell
Get-Item 'missing.txt' -ErrorAction Stop
```

For operations that must fail clearly, use `-ErrorAction Stop` and handle the exception:

```powershell
try {
	docker inspect example-api -ErrorAction Stop
}
catch {
	Write-Error "Container inspection failed: $($_.Exception.Message)"
}
```

Check native command exit codes when a script depends on Docker, Git, or another executable:

```powershell
docker build -t example-api:1.0.0 .
if ($LASTEXITCODE -ne 0) { throw 'Docker build failed.' }
```

## Script Safety

- Use `Set-StrictMode` in scripts where appropriate.
- Quote paths that may contain spaces.
- Prefer `-LiteralPath` when wildcards should not be expanded.
- Validate input before invoking destructive commands.
- Use `-WhatIf` when supported.
- Keep credentials out of scripts and command history.
- Make scripts return a non-zero exit code when automation fails.

## Related Concepts

- [[Docker commands]] - Commands commonly automated with PowerShell
- [[Docker Basics]] - Container concepts and resources
- [[CI-CD Pipeline]] - Use scripts in automated delivery
- [[File IO]] - PowerShell file and directory operations
