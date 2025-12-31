# 🔄 Control Flow

## If-ElseIf-Else

```powershell
$age = 25

if ($age -lt 18) {
    "Minor"
} elseif ($age -lt 65) {
    "Adult"
} else {
    "Senior"
}
```

## Switch Statement

```powershell
$status = "Running"

switch ($status) {
    "Running" { "Service is active" }
    "Stopped" { "Service is inactive" }
    "Paused" { "Service is paused" }
    default { "Unknown status" }
}

# With wildcards
switch -Wildcard ($filename) {
    "*.txt" { "Text file" }
    "*.log" { "Log file" }
    default { "Other file" }
}

# With regex
switch -Regex ($input) {
    "^[0-9]+$" { "Number" }
    "^[A-Za-z]+$" { "Letters" }
    default { "Mixed" }
}
```

## For Loop

```powershell
for ($i = 0; $i -lt 10; $i++) {
    Write-Host "Count: $i"
}

# Nested loops
for ($i = 1; $i -le 3; $i++) {
    for ($j = 1; $j -le 3; $j++) {
        "$i x $j = $($i * $j)"
    }
}
```

## ForEach Loop

```powershell
$services = Get-Service

foreach ($service in $services) {
    if ($service.Status -eq 'Running') {
        $service.Name
    }
}

# With hashtable
$hash = @{a=1; b=2; c=3}
foreach ($key in $hash.Keys) {
    "$key = $($hash[$key])"
}
```

## While Loop

```powershell
$count = 0
while ($count -lt 5) {
    "Count: $count"
    $count++
}

# Do-While (executes at least once)
$input = ""
do {
    $input = Read-Host "Enter 'quit' to exit"
} while ($input -ne 'quit')
```

## Break & Continue

```powershell
# Break - exit loop
for ($i = 0; $i -lt 10; $i++) {
    if ($i -eq 5) { break }
    $i
}

# Continue - skip iteration
for ($i = 0; $i -lt 10; $i++) {
    if ($i % 2 -eq 0) { continue }
    $i  # Only odd numbers
}
```

## Comparison Operators

```powershell
-eq  # Equal
-ne  # Not equal
-gt  # Greater than
-ge  # Greater or equal
-lt  # Less than
-le  # Less or equal
-like # Wildcard match
-notlike # Not wildcard match
-match # Regex match
-notmatch # Not regex match
-contains # Collection contains
-in # Item in collection
```

## Logical Operators

```powershell
-and  # AND
-or   # OR
-not  # NOT
!     # NOT (alternative)
-xor  # XOR
```

➡️ Next: [Advanced Topics](../03-advanced/01-remoting.md)
