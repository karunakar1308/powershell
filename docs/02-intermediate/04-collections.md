# 📦 Collections: Arrays & Hash Tables

## ArrayList (Dynamic)

```powershell
$list = [System.Collections.ArrayList]@()
$list.Add("Item1") | Out-Null
$list.AddRange(@("Item2", "Item3"))
$list.Remove("Item1")
$list.RemoveAt(0)
```

## Hash Tables (Dictionaries)

```powershell
# Create
$hash = @{}
$hash["Name"] = "John"
$hash.Age = 30

# Ordered hash table
$ordered = [ordered]@{
    First = 1
    Second = 2
    Third = 3
}

# Iterate
$hash.Keys | ForEach-Object {
    Write-Host "$_: $($hash[$_])"
}

foreach ($key in $hash.Keys) {
    "$key = $($hash[$key])"
}
```

## Generic Lists

```powershell
$list = New-Object 'System.Collections.Generic.List[string]'
$list.Add("Item1")
$list.AddRange(@("Item2", "Item3"))
$list.Contains("Item1")
$list.Count
```

## Advanced Array Operations

```powershell
# Join
$arr = @("a", "b", "c")
$arr -join ","  # "a,b,c"

# Split string to array
$text = "one,two,three"
$arr = $text -split ","

# Filter
$numbers = 1..10
$even = $numbers | Where-Object {$_ % 2 -eq 0}

# Transform
$doubled = $numbers | ForEach-Object {$_ * 2}

# Sum
($numbers | Measure-Object -Sum).Sum
```

## Stack & Queue

```powershell
# Stack (LIFO)
$stack = New-Object System.Collections.Stack
$stack.Push("Item1")
$stack.Push("Item2")
$item = $stack.Pop()

# Queue (FIFO)
$queue = New-Object System.Collections.Queue
$queue.Enqueue("Item1")
$queue.Enqueue("Item2")
$item = $queue.Dequeue()
```

➡️ [Control Flow](./05-control-flow.md)
