# 💻 Basic Cmdlets & Syntax

## Understanding Cmdlets

Cmdlets (pronounced "command-lets") are the heart of PowerShell. They are:
- Lightweight commands
- Built on .NET classes
- Follow a **Verb-Noun** naming convention
- Return .NET objects (not text)

### Cmdlet Structure

```powershell
Verb-Noun -Parameter1 Value1 -Parameter2 Value2
```

**Example:**
```powershell
Get-Process -Name chrome -ComputerName localhost
```

---

## Essential Cmdlets Every Beginner Must Know

### 1. File System Navigation

#### Get-Location (pwd)
Get your current directory location.

```powershell
Get-Location
# Output: C:\Users\YourName

# Short alias
pwd
```

#### Set-Location (cd)
Change to a different directory.

```powershell
Set-Location C:\Windows
Set-Location ~\Documents
Set-Location ..

# Using alias
cd C:\Temp
```

#### Get-ChildItem (ls, dir)
List files and directories.

```powershell
# Basic usage
Get-ChildItem

# Show hidden files
Get-ChildItem -Force

# Recursive search
Get-ChildItem -Recurse

# Filter by extension
Get-ChildItem *.txt
Get-ChildItem -Filter *.log

# Include specific files recursively
Get-ChildItem -Path C:\Logs -Include *.log -Recurse

# Exclude patterns
Get-ChildItem -Exclude *.tmp
```

**Real-world examples:**
```powershell
# Find all PowerShell scripts in current directory and subdirectories
Get-ChildItem -Filter *.ps1 -Recurse

# Find large files (>100MB)
Get-ChildItem -Recurse | Where-Object {$_.Length -gt 100MB}

# Find recently modified files (last 7 days)
Get-ChildItem -Recurse | Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(-7)}
```

### 2. File and Folder Operations

#### New-Item
Create files and directories.

```powershell
# Create a directory
New-Item -Path C:\Temp -ItemType Directory

# Create a file
New-Item -Path C:\Temp\test.txt -ItemType File

# Create with content
New-Item -Path C:\Temp\data.txt -ItemType File -Value "Hello PowerShell"
```

#### Copy-Item
Copy files and folders.

```powershell
# Copy file
Copy-Item -Path C:\Source\file.txt -Destination C:\Dest\

# Copy directory recursively
Copy-Item -Path C:\Source -Destination C:\Backup -Recurse

# Copy with new name
Copy-Item -Path file.txt -Destination newfile.txt
```

#### Move-Item
Move or rename files and folders.

```powershell
# Move file
Move-Item -Path C:\Temp\file.txt -Destination C:\Archive\

# Rename file
Move-Item -Path oldname.txt -Destination newname.txt
```

#### Remove-Item
Delete files and directories.

```powershell
# Delete file
Remove-Item -Path C:\Temp\file.txt

# Delete directory
Remove-Item -Path C:\Temp -Recurse

# Delete with confirmation
Remove-Item -Path C:\Temp\*.log -Confirm

# Delete without prompts
Remove-Item -Path C:\Temp -Recurse -Force
```

#### Get-Content
Read file contents.

```powershell
# Read entire file
Get-Content -Path C:\Logs\app.log

# Read first 10 lines
Get-Content -Path C:\Logs\app.log -TotalCount 10

# Read last 50 lines  
Get-Content -Path C:\Logs\app.log -Tail 50

# Monitor file in real-time (like tail -f)
Get-Content -Path C:\Logs\app.log -Wait
```

#### Set-Content
Write content to files.

```powershell
# Write to file (overwrites)
Set-Content -Path C:\Temp\data.txt -Value "New content"

# Write multiple lines
Set-Content -Path C:\Temp\data.txt -Value "Line 1", "Line 2", "Line 3"
```

#### Add-Content
Append content to files.

```powershell
# Append to file
Add-Content -Path C:\Logs\app.log -Value "New log entry"
```

### 3. Process Management

#### Get-Process
View running processes.

```powershell
# All processes
Get-Process

# Specific process
Get-Process -Name chrome
Get-Process -Id 1234

# Multiple processes
Get-Process -Name chrome, firefox, code

# Sort by CPU
Get-Process | Sort-Object CPU -Descending

# Top 10 memory consumers
Get-Process | Sort-Object WorkingSet -Descending | Select-Object -First 10
```

#### Stop-Process
Terminate processes.

```powershell
# Stop by name
Stop-Process -Name notepad

# Stop by ID
Stop-Process -Id 1234

# Force stop
Stop-Process -Name chrome -Force

# Stop with confirmation
Stop-Process -Name notepad -Confirm
```

#### Start-Process
Start new processes.

```powershell
# Start application
Start-Process notepad.exe

# Start with arguments
Start-Process notepad.exe -ArgumentList "C:\Temp\file.txt"

# Start elevated (as admin)
Start-Process powershell.exe -Verb RunAs
```

### 4. Service Management

#### Get-Service
View Windows services.

```powershell
# All services
Get-Service

# Specific service
Get-Service -Name Spooler

# Running services only
Get-Service | Where-Object {$_.Status -eq 'Running'}

# Stopped services
Get-Service | Where-Object {$_.Status -eq 'Stopped'}
```

#### Start-Service / Stop-Service / Restart-Service

```powershell
# Start service (requires admin)
Start-Service -Name Spooler

# Stop service
Stop-Service -Name Spooler

# Restart service
Restart-Service -Name Spooler
```

### 5. System Information

#### Get-ComputerInfo
Detailed system information.

```powershell
Get-ComputerInfo
Get-ComputerInfo | Select-Object CsName, OsArchitecture, WindowsVersion
```

#### Get-EventLog (Windows PowerShell 5.1)

```powershell
# Get recent errors
Get-EventLog -LogName System -EntryType Error -Newest 10

# Application log
Get-EventLog -LogName Application -Newest 50
```

#### Get-WinEvent (PowerShell 7+)

```powershell
# System log errors
Get-WinEvent -LogName System -MaxEvents 10 | Where-Object {$_.LevelDisplayName -eq 'Error'}
```

---

## Common Parameters

All cmdlets support these common parameters:

```powershell
-Verbose      # Show detailed information
-Debug        # Show debugging information
-ErrorAction  # Control error behavior
-WarningAction # Control warning behavior
-WhatIf       # Preview changes without executing
-Confirm      # Ask for confirmation
```

**Examples:**

```powershell
# Preview without executing
Remove-Item C:\Temp\*.log -WhatIf

# Ask before each deletion
Remove-Item C:\Temp\*.log -Confirm

# Verbose output
Copy-Item C:\Source -Destination C:\Dest -Recurse -Verbose
```

---

## Practice Exercises

### Exercise 1: File Management

```powershell
# 1. Create a new folder called "PSTest" in your Documents
New-Item -Path ~\Documents\PSTest -ItemType Directory

# 2. Create 5 text files in that folder
1..5 | ForEach-Object { New-Item -Path ~\Documents\PSTest\file$_.txt -ItemType File }

# 3. List all files
Get-ChildItem -Path ~\Documents\PSTest

# 4. Copy the folder to Desktop
Copy-Item -Path ~\Documents\PSTest -Destination ~\Desktop\PSTest -Recurse

# 5. Delete the original folder
Remove-Item -Path ~\Documents\PSTest -Recurse
```

### Exercise 2: Process Investigation

```powershell
# 1. Find all running processes
Get-Process

# 2. Find the top 5 CPU consumers
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5

# 3. Find all Chrome processes
Get-Process -Name chrome -ErrorAction SilentlyContinue

# 4. Count total running processes
(Get-Process).Count
```

### Exercise 3: Service Management

```powershell
# 1. List all running services
Get-Service | Where-Object {$_.Status -eq 'Running'}

# 2. Find services with 'Windows' in the name
Get-Service | Where-Object {$_.DisplayName -like '*Windows*'}

# 3. Check the status of a specific service
Get-Service -Name Spooler
```

---

## 📚 Quick Reference

| Task | Cmdlet |
|------|--------|
| List files | `Get-ChildItem` |
| Create folder | `New-Item -ItemType Directory` |
| Copy file | `Copy-Item` |
| Delete file | `Remove-Item` |
| Read file | `Get-Content` |
| Write file | `Set-Content` |
| View processes | `Get-Process` |
| Stop process | `Stop-Process` |
| View services | `Get-Service` |
| Restart service | `Restart-Service` |

---

## 👉 Next Steps

➡️ [Variables & Data Types](./03-variables-datatypes.md)

---

**Pro Tip:** Use `Get-Command *keyword*` to discover related cmdlets!
