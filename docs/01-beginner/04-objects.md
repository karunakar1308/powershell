# 🎯 Working with Objects

## PowerShell is Object-Based

Unlike traditional shells that work with text, PowerShell works with **.NET objects**. This is PowerShell's superpower!

### What is an Object?

An object has:
- **Properties**: Data/attributes (like variables)
- **Methods**: Actions it can perform (like functions)

```powershell
# Get a process object
$proc = Get-Process -Name powershell | Select-Object -First 1

# Properties (data)
$proc.Name
$proc.CPU
$proc.WorkingSet

# Methods (actions)
$proc.Kill()  # Terminates the process
```

---

## Exploring Objects with Get-Member

The most important command for learning PowerShell!

```powershell
# See what an object can do
Get-Process | Get-Member

# See only properties
Get-Process | Get-Member -MemberType Property

# See only methods
Get-Process | Get-Member -MemberType Method
```

**Example Output:**
```
Name        MemberType Definition
----        ---------- ----------
CPU         Property   double CPU {get;}
Id          Property   int Id {get;}
Kill        Method     void Kill()
WaitForExit Method     bool WaitForExit(int milliseconds)
```

---

## Accessing Object Properties

### Dot Notation

```powershell
$service = Get-Service -Name Spooler

# Access properties
$service.Name
$service.Status
$service.DisplayName
$service.StartType
```

### All Objects from Pipeline

```powershell
# Get specific property from all objects
Get-Process | Select-Object -Property Name, CPU, WorkingSet

# Just names
Get-Process | Select-Object -ExpandProperty Name
```

---

## Common Object Types

### FileInfo Objects

```powershell
$file = Get-Item C:\Windows\System32\notepad.exe

$file.Name
$file.Length          # Size in bytes
$file.LastWriteTime
$file.Extension
$file.Directory
$file.Exists

# Methods
$file.Delete()
$file.CopyTo("C:\Backup\notepad.exe")
```

### Process Objects

```powershell
$proc = Get-Process -Name chrome | Select-Object -First 1

$proc.Id
$proc.ProcessName
$proc.CPU
$proc.WorkingSet64
$proc.StartTime

# Methods
$proc.Kill()
$proc.WaitForExit()
```

### Service Objects

```powershell
$svc = Get-Service -Name Spooler

$svc.Name
$svc.Status
$svc.StartType

# Methods
$svc.Start()
$svc.Stop()
$svc.Refresh()
```

---

## Select-Object: Choosing Properties

```powershell
# Select specific properties
Get-Process | Select-Object Name, CPU, WorkingSet

# First 5 items
Get-Process | Select-Object -First 5

# Last 3 items  
Get-Process | Select-Object -Last 3

# Unique values
Get-Process | Select-Object -Property Company -Unique

# Calculated properties
Get-Process | Select-Object Name, @{Name='MemoryMB';Expression={$_.WorkingSet / 1MB}}
```

---

## Where-Object: Filtering Objects

```powershell
# Processes using more than 100MB
Get-Process | Where-Object {$_.WorkingSet -gt 100MB}

# Running services
Get-Service | Where-Object {$_.Status -eq 'Running'}

# Files larger than 1GB
Get-ChildItem | Where-Object {$_.Length -gt 1GB}

# Multiple conditions (AND)
Get-Process | Where-Object {$_.CPU -gt 10 -and $_.WorkingSet -gt 100MB}

# Multiple conditions (OR)
Get-Service | Where-Object {$_.Status -eq 'Running' -or $_.Status -eq 'Paused'}
```

---

## Sort-Object: Ordering Objects

```powershell
# Sort by property
Get-Process | Sort-Object CPU

# Descending
Get-Process | Sort-Object CPU -Descending

# Multiple properties
Get-Process | Sort-Object Company, Name

# Top 10 memory consumers
Get-Process | Sort-Object WorkingSet -Descending | Select-Object -First 10
```

---

## Measure-Object: Statistics

```powershell
# Count
Get-Process | Measure-Object

# Sum, Average, Min, Max
Get-Process | Measure-Object -Property WorkingSet -Sum -Average -Minimum -Maximum

# File sizes
Get-ChildItem | Measure-Object -Property Length -Sum
```

---

## Group-Object: Grouping

```powershell
# Group by property
Get-Process | Group-Object Company

# Group services by status
Get-Service | Group-Object Status

# Count by extension
Get-ChildItem | Group-Object Extension
```

---

## Creating Custom Objects

```powershell
# PSCustomObject
$user = [PSCustomObject]@{
    Name = "John Doe"
    Age = 30
    Department = "IT"
}

$user.Name
$user | Get-Member

# Array of objects
$users = @(
    [PSCustomObject]@{Name="Alice"; Age=25}
    [PSCustomObject]@{Name="Bob"; Age=30}
    [PSCustomObject]@{Name="Carol"; Age=35}
)

$users | Where-Object {$_.Age -gt 28}
```

---

## Practice Exercises

```powershell
# 1. Find top 5 CPU consumers
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5 Name, CPU

# 2. Count running services
(Get-Service | Where-Object {$_.Status -eq 'Running'}).Count

# 3. Find files modified today
Get-ChildItem | Where-Object {$_.LastWriteTime.Date -eq (Get-Date).Date}

# 4. Total size of all files in directory
(Get-ChildItem | Measure-Object -Property Length -Sum).Sum / 1MB

# 5. Group processes by company
Get-Process | Group-Object Company | Sort-Object Count -Descending
```

➡️ [Pipes & Filters](./05-pipes-filters.md)
