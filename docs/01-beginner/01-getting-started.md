# 🚀 Getting Started with PowerShell

## What is PowerShell?

PowerShell is a cross-platform task automation solution made up of:
- A **command-line shell**
- A **scripting language**
- A **configuration management framework**

Built on the .NET framework, PowerShell allows you to automate tasks and manage configurations through powerful command-line tools.

---

## Why Learn PowerShell?

### 🎯 Key Benefits

1. **Automation at Scale**: Automate repetitive tasks across thousands of servers
2. **System Administration**: Manage Windows, Linux, and macOS systems
3. **Cloud Management**: Work with Azure, AWS, and other cloud platforms
4. **DevOps Integration**: CI/CD pipelines, infrastructure as code
5. **Career Growth**: High demand skill for IT professionals

### 📈 Real-World Use Cases

- Active Directory user management
- Server configuration and monitoring
- Log file analysis and reporting
- Azure resource deployment
- Automated backup and recovery
- Application deployment

---

## Installation

### Windows

**Windows 10/11 and Windows Server 2016+** come with PowerShell pre-installed.

#### Check Your Version

```powershell
$PSVersionTable
```

**Output:**
```
Name                           Value
----                           -----
PSVersion                      5.1.19041.4780
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
```

### PowerShell 7+ (Latest Version)

**Install via Windows Package Manager:**

```powershell
winget install --id Microsoft.Powershell --source winget
```

**Install via MSI Installer:**

Download from: [https://github.com/PowerShell/PowerShell/releases](https://github.com/PowerShell/PowerShell/releases)

### Linux

**Ubuntu/Debian:**
```bash
sudo apt-get update
sudo apt-get install -y wget apt-transport-https software-properties-common
wget -q https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
sudo apt-get update
sudo apt-get install -y powershell
```

**Launch PowerShell:**
```bash
pwsh
```

### macOS

**Using Homebrew:**
```bash
brew install --cask powershell
```

**Launch PowerShell:**
```bash
pwsh
```

---

## Your First PowerShell Session

### Opening PowerShell

**Windows:**
- Press `Win + X`, select "Windows PowerShell" or "Terminal"
- Or search for "PowerShell" in Start Menu

**For PowerShell 7:**
- Search for "pwsh" or "PowerShell 7"

### The PowerShell Console

When you open PowerShell, you'll see a prompt like:

```
PS C:\Users\YourName>
```

This indicates:
- `PS` = PowerShell
- `C:\Users\YourName` = Current directory
- `>` = Ready for input

---

## Essential Commands to Start

### 1. Get-Command - Discover Available Commands

```powershell
Get-Command
```

Find specific commands:
```powershell
Get-Command *Process*
Get-Command -Verb Get
Get-Command -Noun Service
```

### 2. Get-Help - Your Built-in Documentation

```powershell
Get-Help Get-Process
```

**Get detailed help:**
```powershell
Get-Help Get-Process -Detailed
Get-Help Get-Process -Examples
Get-Help Get-Process -Full
Get-Help Get-Process -Online
```

**Update help files:**
```powershell
Update-Help
```

### 3. Get-Member - Explore Objects

```powershell
Get-Process | Get-Member
```

This shows you all properties and methods available on an object.

---

## Your First Commands

### Get Current Directory

```powershell
Get-Location
# or shorthand
pwd
```

### Change Directory

```powershell
Set-Location C:\Windows
# or shorthand
cd C:\Windows
```

### List Files and Folders

```powershell
Get-ChildItem
# or shorthand
ls
dir
```

**With filters:**
```powershell
Get-ChildItem -Path C:\Windows\System32 -Filter *.exe
Get-ChildItem -Recurse -Include *.log
```

### View Running Processes

```powershell
Get-Process
```

**Filter by name:**
```powershell
Get-Process -Name chrome, firefox
Get-Process | Where-Object {$_.CPU -gt 100}
```

### View Services

```powershell
Get-Service
Get-Service | Where-Object {$_.Status -eq 'Running'}
```

---

## PowerShell ISE and VS Code

### PowerShell ISE (Integrated Scripting Environment)

**Launch ISE:**
```powershell
ise
```

Features:
- Script pane for writing scripts
- Console pane for running commands
- IntelliSense autocomplete
- Built-in debugger

### Visual Studio Code (Recommended)

**Install VS Code:**
- Download from [https://code.visualstudio.com/](https://code.visualstudio.com/)

**Install PowerShell Extension:**
1. Open VS Code
2. Go to Extensions (Ctrl+Shift+X)
3. Search for "PowerShell"
4. Install the official Microsoft PowerShell extension

**Features:**
- Advanced IntelliSense
- Integrated terminal
- Git integration
- Extensions ecosystem
- Cross-platform support

---

## PowerShell Basics

### Cmdlet Syntax

PowerShell cmdlets follow a **Verb-Noun** pattern:

```powershell
Get-Process
Set-Location
New-Item
Remove-Item
```

**Common Verbs:**
- `Get` - Retrieve information
- `Set` - Change configuration
- `New` - Create new resources
- `Remove` - Delete resources
- `Start` - Begin operations
- `Stop` - End operations
- `Test` - Validate conditions

### Parameters

```powershell
Get-Process -Name chrome
Get-ChildItem -Path C:\Windows -Recurse -Filter *.log
```

**Named Parameters:**
```powershell
Get-Process -Name "chrome"
```

**Positional Parameters:**
```powershell
Get-Process chrome  # Name is positional
```

### Aliases

PowerShell includes aliases for common commands:

```powershell
ls   # Get-ChildItem
cd   # Set-Location
pwd  # Get-Location
cls  # Clear-Host
cat  # Get-Content
```

**View all aliases:**
```powershell
Get-Alias
Get-Alias -Name ls
```

---

## Hands-On Practice

### Exercise 1: Exploring Your System

```powershell
# Get your PowerShell version
$PSVersionTable.PSVersion

# Check current location
Get-Location

# List files in current directory
Get-ChildItem

# View running processes
Get-Process

# Check Windows services
Get-Service
```

### Exercise 2: Using the Pipeline

```powershell
# Get top 5 processes by CPU usage
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5

# Get all stopped services
Get-Service | Where-Object {$_.Status -eq 'Stopped'}

# List only .txt files in Documents
Get-ChildItem -Path $env:USERPROFILE\Documents -Filter *.txt
```

### Exercise 3: Getting Help

```powershell
# Get help for Get-Process
Get-Help Get-Process

# See examples
Get-Help Get-Process -Examples

# Open online help
Get-Help Get-Process -Online
```

---

## Common Beginner Mistakes

### 1. **Not Using Tab Completion**

❌ Wrong: Typing full command names

✅ Correct: Use Tab to autocomplete
```powershell
Get-Ch<TAB>  # Completes to Get-ChildItem
```

### 2. **Forgetting the Pipeline**

❌ Wrong:
```powershell
$procs = Get-Process
$filtered = Where-Object {$_.CPU -gt 100} $procs
```

✅ Correct:
```powershell
Get-Process | Where-Object {$_.CPU -gt 100}
```

### 3. **Not Reading Error Messages**

Always read the error message - PowerShell errors are descriptive!

---

## PowerShell vs Other Shells

| Feature | PowerShell | Bash | CMD |
|---------|-----------|------|-----|
| Object-based | ✅ | ❌ | ❌ |
| Cross-platform | ✅ | ✅ | ❌ |
| .NET Integration | ✅ | ❌ | ❌ |
| Pipeline | ✅ | ✅ | Limited |
| Scripting | ✅ | ✅ | Basic |

---

## 📚 Additional Resources

- [🔗 Official PowerShell Documentation](https://docs.microsoft.com/powershell/)
- [🔗 PowerShell GitHub](https://github.com/PowerShell/PowerShell)
- [🔗 PowerShell Gallery](https://www.powershellgallery.com/)
- [🔗 SS64 PowerShell Reference](https://ss64.com/ps/)

---

## 👉 Next Steps

Now that you've set up PowerShell and learned the basics, continue to:

➡️ [Basic Cmdlets & Syntax](./02-basic-cmdlets.md)

---

**Practice Tip:** Spend at least 30 minutes each day running these commands. Muscle memory is key! 💪
