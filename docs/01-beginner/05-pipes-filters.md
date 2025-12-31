# 🔧 Pipes & Filters

## The PowerShell Pipeline

The pipeline (`|`) is PowerShell's most powerful feature! It passes objects from one command to another.

### Basic Concept

```powershell
Command1 | Command2 | Command3
```

Objects flow left to right, each command processing and passing results to the next.

---

## Simple Pipeline Examples

```powershell
# Get processes, sort by CPU, show top 5
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5

# Get files, filter by size, count them
Get-ChildItem | Where-Object {$_.Length -gt 1MB} | Measure-Object

# Get services, filter running, export to CSV
Get-Service | Where-Object {$_.Status -eq 'Running'} | Export-Csv running.csv
```

---

## The Pipeline Variable: $_

Inside a pipeline, `$_` represents the current object.

```powershell
# $_ is each process object
Get-Process | Where-Object {$_.CPU -gt 10}

# $_ is each file object
Get-ChildItem | Where-Object {$_.Extension -eq '.txt'}

# $_ is each service object
Get-Service | ForEach-Object { $_.DisplayName }
```

---

## Where-Object: Filtering

### Comparison Operators

```powershell
-eq   # Equal
-ne   # Not equal
-gt   # Greater than
-ge   # Greater than or equal
-lt   # Less than
-le   # Less than or equal
-like # Wildcard match
-match # Regex match
-contains # Collection contains
```

### Examples

```powershell
# Exact match
Get-Service | Where-Object {$_.Status -eq 'Running'}

# Greater than
Get-Process | Where-Object {$_.WorkingSet -gt 100MB}

# Wildcard
Get-Service | Where-Object {$_.Name -like 'Win*'}

# Multiple conditions (AND)
Get-Process | Where-Object {$_.CPU -gt 5 -and $_.WorkingSet -gt 50MB}

# Multiple conditions (OR)
Get-Service | Where-Object {$_.Status -eq 'Running' -or $_.Status -eq 'Paused'}
```

---

## ForEach-Object: Processing Each Item

```powershell
# Simple property access
Get-Process | ForEach-Object {$_.Name}

# Multiple statements
Get-ChildItem | ForEach-Object {
    Write-Host "File: $($_.Name)"
    Write-Host "Size: $($_.Length) bytes"
}

# Calculations
Get-Process | ForEach-Object {$_.WorkingSet / 1MB}

# Call methods
Get-Service | ForEach-Object {$_.Refresh()}
```

---

## Select-Object: Shaping Output

```powershell
# Select specific properties
Get-Process | Select-Object Name, CPU, WorkingSet

# First N items
Get-Process | Select-Object -First 10

# Last N items
Get-ChildItem | Select-Object -Last 5

# Unique values
Get-Process | Select-Object -Property Company -Unique

# Calculated/Custom properties
Get-Process | Select-Object Name, @{Name='MemMB'; Expression={$_.WS / 1MB}}

# Expand property values
Get-Process | Select-Object -ExpandProperty Name
```

---

## Sort-Object: Ordering

```powershell
# Ascending (default)
Get-Process | Sort-Object CPU

# Descending
Get-Process | Sort-Object CPU -Descending

# Multiple properties
Get-Process | Sort-Object Company, Name

# Unique sorted
Get-Process | Sort-Object Company -Unique
```

---

## Group-Object: Grouping Data

```powershell
# Group by property
Get-Service | Group-Object Status

# With count
Get-Process | Group-Object Company | Sort-Object Count -Descending

# Group files by extension
Get-ChildItem | Group-Object Extension
```

**Output:**
```
Count Name
----- ----
   45 Running
   12 Stopped
```

---

## Measure-Object: Statistics

```powershell
# Count
Get-Process | Measure-Object

# Sum, Average, Min, Max
Get-Process | Measure-Object -Property WorkingSet -Sum -Average -Min -Max

# Total file size
Get-ChildItem | Measure-Object -Property Length -Sum
```

---

## Tee-Object: Split Output

Send output to a file AND continue the pipeline.

```powershell
# Save to file and continue
Get-Process | Tee-Object -FilePath processes.txt | Where-Object {$_.CPU -gt 10}

# Save variable and continue
Get-Service | Tee-Object -Variable services | Where-Object {$_.Status -eq 'Running'}
```

---

## Out-* Cmdlets

```powershell
# Display in grid view (GUI)
Get-Process | Out-GridView

# Save to file
Get-Process | Out-File processes.txt

# Print
Get-Content report.txt | Out-Printer

# Suppress output
Get-Process | Out-Null
```

---

## Export/Import

### CSV Files

```powershell
# Export to CSV
Get-Process | Export-Csv processes.csv
Get-Service | Export-Csv -Path services.csv -NoTypeInformation

# Import from CSV
$data = Import-Csv processes.csv
$data | Where-Object {$_.CPU -gt 10}
```

### JSON

```powershell
# Export to JSON
Get-Process | Select Name, CPU | ConvertTo-Json | Out-File procs.json

# Import JSON
$json = Get-Content procs.json | ConvertFrom-Json
```

### XML

```powershell
# Export to XML
Get-Service | Export-Clixml services.xml

# Import XML
$services = Import-Clixml services.xml
```

---

## Real-World Pipeline Chains

### Find Large Files

```powershell
Get-ChildItem -Recurse | 
    Where-Object {$_.Length -gt 100MB} |
    Sort-Object Length -Descending |
    Select-Object Name, @{Name='SizeMB';Expression={[math]::Round($_.Length/1MB,2)}} |
    Format-Table -AutoSize
```

### System Report

```powershell
Get-Process |
    Sort-Object WorkingSet -Descending |
    Select-Object -First 10 |
    Select-Object Name, @{N='MemMB';E={[math]::Round($_.WS/1MB,2)}}, CPU |
    Export-Csv top10procs.csv -NoTypeInformation
```

### Service Status Summary

```powershell
Get-Service |
    Group-Object Status |
    Select-Object Count, Name |
    Sort-Object Count -Descending
```

---

## Practice Exercises

```powershell
# 1. Top 10 memory users with formatted output
Get-Process | 
    Sort-Object WorkingSet -Descending | 
    Select-Object -First 10 Name, @{N='MemMB';E={[int]($_.WS/1MB)}}

# 2. Count .txt files in Documents
(Get-ChildItem ~\Documents -Filter *.txt -Recurse).Count

# 3. Running services grouped by start type
Get-Service | 
    Where-Object {$_.Status -eq 'Running'} | 
    Group-Object StartType

# 4. Files modified in last 7 days, sorted by date
Get-ChildItem -Recurse |
    Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(-7)} |
    Sort-Object LastWriteTime -Descending

# 5. Export stopped services to CSV
Get-Service |
    Where-Object {$_.Status -eq 'Stopped'} |
    Export-Csv stopped-services.csv -NoTypeInformation
```

---

## Best Practices

1. **Filter early**: Use `Where-Object` early in the pipeline
2. **Sort before Select**: Sort before selecting top N items
3. **Use -First/-Last**: More efficient than array indexing
4. **Chain efficiently**: Each step should reduce or transform data
5. **Use calculated properties**: Transform data in `Select-Object`

---

➡️ Next: [Functions & Modules](../02-intermediate/01-functions-modules.md)
