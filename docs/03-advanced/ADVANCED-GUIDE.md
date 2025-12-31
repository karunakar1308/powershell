# 🚀 Advanced PowerShell Guide

Comprehensive guide covering advanced PowerShell topics for professional automation and DevOps.

---

## 📦 Advanced Functions & Script Blocks

### Advanced Function Structure

```powershell
function Get-AdvancedInfo {
    [CmdletBinding(SupportsShouldProcess=$true)]
    param(
        [Parameter(Mandatory,ValueFromPipeline)]
        [ValidateNotNullOrEmpty()]
        [string[]]$ComputerName,
        
        [Parameter()]
        [PSCredential]$Credential
    )
    
    begin {
        Write-Verbose "Starting collection"
    }
    
    process {
        foreach ($computer in $ComputerName) {
            if ($PSCmdlet.ShouldProcess($computer, "Get Info")) {
                # Process each computer
            }
        }
    }
    
    end {
        Write-Verbose "Complete"
    }
}
```

### Script Blocks & Jobs

```powershell
# Background jobs
$job = Start-Job -ScriptBlock {
    Get-Process | Where-Object {$_.CPU -gt 100}
}

# Wait and get results
$job | Wait-Job | Receive-Job

# Parallel execution
1..10 | ForEach-Object -Parallel {
    Start-Sleep 1
    "Task $_ complete"
} -ThrottleLimit 5
```

---

## 💻 .NET Integration

### Using .NET Classes

```powershell
# System.IO
[System.IO.File]::ReadAllText("C:\file.txt")
[System.IO.Directory]::GetFiles("C:\Temp")

# DateTime
[DateTime]::Now
[DateTime]::Now.AddDays(7)

# Math
[Math]::Round(3.14159, 2)
[Math]::Pow(2, 10)

# WebClient
$web = New-Object System.Net.WebClient
$web.DownloadFile("https://example.com/file.zip", "C:\file.zip")
```

### Custom .NET Objects

```powershell
Add-Type -TypeDefinition @"
public class Calculator {
    public static int Add(int a, int b) {
        return a + b;
    }
}
"@

[Calculator]::Add(5, 10)
```

---

## ⚙️ DSC (Desired State Configuration)

### Basic Configuration

```powershell
Configuration WebServerConfig {
    Node "WebServer01" {
        WindowsFeature IIS {
            Ensure = "Present"
            Name   = "Web-Server"
        }
        
        File WebContent {
            Ensure          = "Present"
            DestinationPath = "C:\inetpub\wwwroot\index.html"
            Contents        = "<h1>Hello World</h1>"
        }
    }
}

# Compile
WebServerConfig -OutputPath C:\DSC

# Apply
Start-DscConfiguration -Path C:\DSC -Wait -Verbose
```

---

## 🔒 Security Best Practices

### Credential Management

```powershell
# Secure strings
$securePassword = ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force
$cred = New-Object PSCredential ("Admin", $securePassword)

# Export/Import credentials
$cred | Export-Clixml C:\secure\cred.xml
$cred = Import-Clixml C:\secure\cred.xml
```

### Execution Policy

```powershell
# View policy
Get-ExecutionPolicy

# Set policy (requires admin)
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

# Bypass for single script
powershell.exe -ExecutionPolicy Bypass -File script.ps1
```

### Code Signing

```powershell
# Get certificate
$cert = Get-ChildItem Cert:\CurrentUser\My -CodeSigningCert

# Sign script
Set-AuthenticodeSignature -FilePath script.ps1 -Certificate $cert
```

---

## 🛠️ Advanced Techniques

### Splatting

```powershell
$params = @{
    ComputerName = "Server01"
    Credential   = $cred
    ScriptBlock  = {Get-Service}
}

Invoke-Command @params
```

### Dynamic Parameters

```powershell
function Get-DynamicParam {
    [CmdletBinding()]
    param()
    
    DynamicParam {
        $paramDict = New-Object Management.Automation.RuntimeDefinedParameterDictionary
        # Add dynamic parameters based on context
        return $paramDict
    }
}
```

### Regular Expressions

```powershell
# Match
"test@example.com" -match "^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$"

# Replace
$text = "Hello 123 World 456"
$text -replace "\d+", "NUM"

# Extract
$text = "Server: WebServer01"
if ($text -match "Server: (\w+)") {
    $serverName = $matches[1]
}
```

---

## 👨‍💻 DevOps with PowerShell

### CI/CD Integration

```powershell
# Azure DevOps
- task: PowerShell@2
  inputs:
    targetType: 'inline'
    script: |
      Write-Host "Deploying"

# GitHub Actions
- name: Run PowerShell
  run: |
    Get-Date
    Write-Host "Running tests"
```

### Infrastructure as Code

```powershell
# Terraform with PowerShell
$tfvars = @{
    location      = "eastus"
    vm_size       = "Standard_DS2_v2"
    instance_count = 3
}

Set-Content terraform.tfvars ($tfvars | ConvertTo-Json)
terraform apply -auto-approve
```

---

## ☁️ Cloud Automation (Azure)

### Azure PowerShell

```powershell
# Install Az module
Install-Module -Name Az -AllowClobber

# Connect
Connect-AzAccount

# Create Resource Group
New-AzResourceGroup -Name "MyRG" -Location "EastUS"

# Create VM
$vmConfig = New-AzVMConfig -VMName "MyVM" -VMSize "Standard_DS2_v2"
New-AzVM -ResourceGroupName "MyRG" -Location "EastUS" -VM $vmConfig

# Get resources
Get-AzResource | Where-Object {$_.ResourceType -eq "Microsoft.Compute/virtualMachines"}
```

### Azure Automation

```powershell
# Runbook example
param(
    [string]$ResourceGroupName
)

# Authenticate
$connection = Get-AutomationConnection -Name AzureRunAsConnection
Connect-AzAccount -ServicePrincipal -Tenant $connection.TenantID `
    -ApplicationId $connection.ApplicationID `
    -CertificateThumbprint $connection.CertificateThumbprint

# Automation logic
Get-AzVM -ResourceGroupName $ResourceGroupName | Stop-AzVM -Force
```

---

## 📊 Performance Optimization

### Measure Performance

```powershell
# Measure-Command
Measure-Command {
    Get-Process | Where-Object {$_.CPU -gt 10}
}

# Stopwatch
$sw = [System.Diagnostics.Stopwatch]::StartNew()
# Code to measure
$sw.Stop()
$sw.ElapsedMilliseconds
```

### Optimize Loops

```powershell
# Slow
$result = @()
foreach ($i in 1..10000) {
    $result += $i
}

# Fast
$result = [System.Collections.ArrayList]@()
foreach ($i in 1..10000) {
    [void]$result.Add($i)
}
```

---

## 📝 Logging & Monitoring

```powershell
# Write to Event Log
Write-EventLog -LogName Application -Source "MyApp" `
    -EventId 1000 -Message "Script completed"

# Custom logging
function Write-Log {
    param([string]$Message)
    $timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
    "$timestamp - $Message" | Out-File -Append C:\Logs\script.log
}

Write-Log "Starting process"
```

---

## 🛡️ Error Handling Advanced

```powershell
try {
    # Risky operation
    Get-Content "C:\missing.txt" -ErrorAction Stop
}
catch [System.IO.FileNotFoundException] {
    Write-Error "File not found"
}
catch [System.UnauthorizedAccessException] {
    Write-Error "Access denied"
}
catch {
    Write-Error "Unexpected error: $_"
}
finally {
    # Cleanup
    Write-Verbose "Cleanup complete"
}
```

---

## 📖 Additional Resources

- [🔗 PowerShell GitHub](https://github.com/PowerShell/PowerShell)
- [🔗 Azure PowerShell Docs](https://docs.microsoft.com/powershell/azure/)
- [🔗 DSC Resources](https://docs.microsoft.com/powershell/dsc/)
- [🔗 PowerShell Gallery](https://www.powershellgallery.com/)

---

**🎉 Congratulations!** You've completed the advanced PowerShell guide. You're now equipped with professional-level PowerShell skills for enterprise automation, DevOps, and cloud management.
