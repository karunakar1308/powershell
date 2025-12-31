# ⚠️ Error Handling

## Try-Catch-Finally

```powershell
try {
    Get-Content "C:\nonexistent.txt" -ErrorAction Stop
    Write-Host "File read successfully"
}
catch {
    Write-Host "Error: $($_.Exception.Message)" -ForegroundColor Red
}
finally {
    Write-Host "Cleanup operations"
}
```

## Error Action Preference

```powershell
# Stop on error
Get-Item "C:\missing.txt" -ErrorAction Stop

# Continue silently
Get-Item "C:\missing.txt" -ErrorAction SilentlyContinue

# Global preference
$ErrorActionPreference = "Stop"
```

## Throw Custom Errors

```powershell
function Divide-Numbers {
    param([int]$a, [int]$b)
    
    if ($b -eq 0) {
        throw "Cannot divide by zero!"
    }
    return $a / $b
}

try {
    Divide-Numbers 10 0
}
catch {
    Write-Error $_.Exception.Message
}
```

## Error Variables

```powershell
# Last error
$Error[0]

# All errors
$Error

# Clear errors
$Error.Clear()

# Error record properties
$Error[0].Exception.Message
$Error[0].ScriptStackTrace
```

## Best Practices

1. Always use Try-Catch for critical operations
2. Use `-ErrorAction Stop` to catch non-terminating errors
3. Log errors appropriately
4. Clean up resources in Finally block
5. Provide meaningful error messages

➡️ [File Operations](./03-file-operations.md)
