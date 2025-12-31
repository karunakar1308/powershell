# 📁 File System Operations

## Advanced File Reading

```powershell
# Read with encoding
Get-Content -Path file.txt -Encoding UTF8

# Stream large files
Get-Content -Path large.log -ReadCount 1000 | ForEach-Object {
    # Process in batches
}

# Monitor file changes
Get-Content -Path app.log -Wait -Tail 50
```

## File Searching

```powershell
# Find files by pattern
Get-ChildItem -Path C:\ -Filter *.log -Recurse -ErrorAction SilentlyContinue

# Find by last write time
Get-ChildItem -Recurse | Where-Object {
    $_.LastWriteTime -gt (Get-Date).AddDays(-7)
}

# Find large files
Get-ChildItem -Recurse -File | Where-Object {$_.Length -gt 100MB} | 
    Sort-Object Length -Descending
```

## Bulk File Operations

```powershell
# Rename multiple files
Get-ChildItem -Filter *.txt | ForEach-Object {
    Rename-Item $_ -NewName ($_.Name -replace '.txt', '.log')
}

# Move files by date
Get-ChildItem | Group-Object {$_.LastWriteTime.ToString('yyyy-MM')} | 
    ForEach-Object {
        $folder = New-Item -Path $_.Name -ItemType Directory -Force
        $_.Group | Move-Item -Destination $folder
    }
```

## File Compression

```powershell
# Compress
Compress-Archive -Path C:\Logs\* -DestinationPath C:\Backup\logs.zip

# Extract
Expand-Archive -Path logs.zip -DestinationPath C:\Extracted
```

## CSV/JSON Operations

```powershell
# Import CSV
$data = Import-Csv users.csv
$data | Where-Object {$_.Age -gt 25}

# Export CSV
Get-Process | Select Name, CPU | Export-Csv procs.csv -NoTypeInformation

# JSON
$object = @{Name="John"; Age=30}
$object | ConvertTo-Json | Out-File data.json
$imported = Get-Content data.json | ConvertFrom-Json
```

## File Watching

```powershell
$watcher = New-Object System.IO.FileSystemWatcher
$watcher.Path = "C:\Temp"
$watcher.Filter = "*.txt"
$watcher.EnableRaisingEvents = $true

Register-ObjectEvent $watcher "Created" -Action {
    Write-Host "File created: $($Event.SourceEventArgs.Name)"
}
```

➡️ [Collections](./04-collections.md)
