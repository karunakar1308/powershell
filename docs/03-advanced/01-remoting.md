# 🌐 PowerShell Remoting

## Enable Remoting

```powershell
# Enable on local machine (requires admin)
Enable-PSRemoting -Force

# Check if enabled
Test-WSMan -ComputerName localhost
```

## Invoke-Command (One-to-Many)

```powershell
# Single computer
Invoke-Command -ComputerName Server01 -ScriptBlock {
    Get-Service
}

# Multiple computers
$servers = "Server01", "Server02", "Server03"
Invoke-Command -ComputerName $servers -ScriptBlock {
    Get-Process | Where-Object {$_.CPU -gt 100}
}

# With credentials
$cred = Get-Credential
Invoke-Command -ComputerName Server01 -Credential $cred -ScriptBlock {
    Get-EventLog -LogName System -Newest 10
}
```

## Enter-PSSession (Interactive)

```powershell
# Connect to remote session
Enter-PSSession -ComputerName Server01

# Exit remote session
Exit-PSSession
```

## Persistent Sessions

```powershell
# Create session
$session = New-PSSession -ComputerName Server01

# Use session
Invoke-Command -Session $session -ScriptBlock {
    $process = Get-Process
}

Invoke-Command -Session $session -ScriptBlock {
    $process | Where-Object {$_.CPU -gt 50}
}

# Remove session
Remove-PSSession $session
```

## Passing Arguments

```powershell
$processName = "powershell"
Invoke-Command -ComputerName Server01 -ScriptBlock {
    param($name)
    Get-Process -Name $name
} -ArgumentList $processName

# Using $using:
Invoke-Command -ComputerName Server01 -ScriptBlock {
    Get-Process -Name $using:processName
}
```

## Copy Files to Remote

```powershell
$session = New-PSSession -ComputerName Server01
Copy-Item -Path C:\Local\file.txt -Destination C:\Remote\ -ToSession $session

# From remote
Copy-Item -Path C:\Remote\file.txt -Destination C:\Local\ -FromSession $session
```

## Configuration

```powershell
# Set trusted hosts (for non-domain)
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "Server01,Server02" -Force

# View configuration
Get-PSSessionConfiguration

# Disable remoting
Disable-PSRemoting -Force
```

➡️ [Advanced Functions](./02-advanced-functions.md)
