# 📊 Variables & Data Types

## Variables in PowerShell

Variables store data that can be used and manipulated in your scripts.

### Creating Variables

```powershell
# Variable assignment
$name = "John"
$age = 30
$salary = 75000.50
$isActive = $true

# Multiple assignment
$x, $y, $z = 1, 2, 3
```

### Variable Names

- Start with `$`
- Can contain letters, numbers, underscores
- Case-insensitive (`$Name` = `$name`)
- Use descriptive names

```powershell
$firstName = "Jane"     # Good
$fn = "Jane"           # Avoid abbreviations
$first_name = "Jane"   # Snake case (less common)
```

---

## Data Types

### String

```powershell
$text = "Hello PowerShell"
$path = 'C:\Windows\System32'  # Single quotes - literal
$greeting = "Hello, $name"     # Double quotes - variable expansion

# Multi-line strings
$multiline = @"
Line 1
Line 2
Line 3
"@

# String methods
$text.Length
$text.ToUpper()
$text.ToLower()
$text.Replace("PowerShell", "PS")
$text.Substring(0, 5)
$text.Split(" ")
```

### Numbers

```powershell
# Integer
$count = 100
$negative = -50

# Decimal
$price = 99.99
$pi = 3.14159

# Math operations
$sum = 10 + 5
$diff = 10 - 5
$product = 10 * 5
$quotient = 10 / 5
$remainder = 10 % 3
$power = [Math]::Pow(2, 10)
```

### Boolean

```powershell
$isTrue = $true
$isFalse = $false
$result = (5 -gt 3)  # True
```

### Arrays

```powershell
# Create array
$colors = @("Red", "Green", "Blue")
$numbers = 1, 2, 3, 4, 5
$mixed = @(1, "two", 3.0, $true)

# Access elements
$colors[0]        # Red
$colors[-1]       # Blue (last)
$colors[0..2]     # Red, Green, Blue

# Array operations
$colors.Count
$colors += "Yellow"  # Add
$colors -contains "Red"  # Check
```

### Hash Tables

```powershell
# Create hash table
$person = @{
    Name = "John"
    Age = 30
    City = "New York"
}

# Access values
$person["Name"]
$person.Age

# Add/Update
$person["Email"] = "john@example.com"
$person.Age = 31

# Keys and values
$person.Keys
$person.Values
```

---

## Type Conversion

```powershell
# Explicit casting
[int]"123"
[string]100
[double]"99.99"

# Get type
$num = 42
$num.GetType().Name  # Int32

# Check type
$num -is [int]  # True
```

---

## Variable Scope

```powershell
# Global (entire session)
$global:var = "Global"

# Script (entire script)
$script:var = "Script"

# Local (current scope)
$local:var = "Local"

# Default is local
$var = "Default Local"
```

---

## Special Variables

```powershell
$PSVersionTable  # PowerShell version
$HOME           # User home directory
$PWD            # Current directory
$PID            # Process ID
$_              # Current pipeline object
$?              # Last command success
$LASTEXITCODE   # Last exit code
$Error          # Error history
```

---

## String Formatting

```powershell
# String interpolation
$name = "Alice"
"Hello, $name"

# Format operator
"Today is {0}" -f (Get-Date)
"Name: {0}, Age: {1}" -f $name, $age

# Here-string
$html = @"
<html>
  <body>$name</body>
</html>
"@
```

---

## Practice

```powershell
# Create and manipulate variables
$firstName = "John"
$lastName = "Doe"
$fullName = "$firstName $lastName"
$age = 25
$futureAge = $age + 5

# Array practice
$fruits = @("Apple", "Banana", "Cherry")
$fruits += "Date"
$fruitCount = $fruits.Count

# Hash table practice
$car = @{
    Make = "Toyota"
    Model = "Camry"
    Year = 2020
}
$car.Color = "Blue"
```

➡️ [Working with Objects](./04-objects.md)
