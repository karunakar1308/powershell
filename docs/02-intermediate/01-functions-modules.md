# 🎯 Functions & Modules

## Functions

### Basic Function

```powershell
function Get-Greeting {
    "Hello, PowerShell!"
}

Get-Greeting
```

### Function with Parameters

```powershell
function Get-Greeting {
    param(
        [string]$Name
    )
    "Hello, $Name!"
}

Get-Greeting -Name "Alice"
```

### Advanced Function

```powershell
function Get-SystemInfo {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory=$true)]
        [string]$ComputerName,
        
        [Parameter()]
        [switch]$IncludeServices
    )
    
    begin {
        Write-Verbose "Starting system info collection"
    }
    
    process {
        $os = Get-CimInstance -ClassName Win32_OperatingSystem
        
        [PSCustomObject]@{
            Computer = $ComputerName
            OS = $os.Caption
            Version = $os.Version
            Memory = "$([math]::Round($os.TotalVisibleMemorySize/1MB,2)) GB"
        }
    }
    
    end {
        Write-Verbose "Completed"
    }
}

Get-SystemInfo -ComputerName "localhost" -Verbose
```

### Parameter Validation

```powershell
function Set-UserAge {
    param(
        [Parameter(Mandatory)]
        [ValidateRange(18,120)]
        [int]$Age,
        
        [ValidateSet("Admin","User","Guest")]
        [string]$Role = "User",
        
        [ValidatePattern('^[A-Z][a-z]+$')]
        [string]$Name
    )
    
    "Age: $Age, Role: $Role, Name: $Name"
}
```

##  Modules

### Creating a Module

**MyModule.psm1:**
```powershell
function Get-Greeting {
    param([string]$Name)
    "Hello, $Name!"
}

function Get-Farewell {
    param([string]$Name)
    "Goodbye, $Name!"
}

Export-ModuleMember -Function Get-Greeting, Get-Farewell
```

### Using Modules

```powershell
# Import module
Import-Module .\MyModule.psm1

# List available modules
Get-Module -ListAvailable

# Remove module
Remove-Module MyModule
```

### Module Manifest

```powershell
# Create manifest
New-ModuleManifest -Path .\MyModule.psd1 `
    -Author "Your Name" `
    -Description "My PowerShell Module" `
    -ModuleVersion "1.0.0"
```

## Best Practices

1. Use approved verbs (`Get-Verb`)
2. Add comment-based help
3. Use `[CmdletBinding()]` for advanced functions
4. Validate parameters
5. Use consistent naming

➡️ [Error Handling](./02-error-handling.md)
