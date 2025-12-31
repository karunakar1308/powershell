# 📚 PowerShell: From Beginner to Advanced

> **Master Windows automation and system administration with PowerShell**

Welcome to your comprehensive PowerShell learning journey! This repository contains everything you need to go from beginner to advanced PowerShell scripting and automation.

---

## 📖 Table of Contents

### 🌱 [Beginner Level](./docs/01-beginner/)

- [Getting Started](./docs/01-beginner/01-getting-started.md)
- [Basic Cmdlets & Syntax](./docs/01-beginner/02-basic-cmdlets.md)
- [Variables & Data Types](./docs/01-beginner/03-variables-datatypes.md)
- [Working with Objects](./docs/01-beginner/04-objects.md)
- [Pipes & Filters](./docs/01-beginner/05-pipes-filters.md)

### 🌿 [Intermediate Level](./docs/02-intermediate/)

- [Functions & Modules](./docs/02-intermediate/01-functions-modules.md)
- [Error Handling](./docs/02-intermediate/02-error-handling.md)
- [File System Operations](./docs/02-intermediate/03-file-operations.md)
- [Working with Arrays & Hash Tables](./docs/02-intermediate/04-collections.md)
- [Control Flow (If, Switch, Loops)](./docs/02-intermediate/05-control-flow.md)

### 🌳 [Advanced Level](./docs/03-advanced/)

- [PowerShell Remoting](./docs/03-advanced/01-remoting.md)
- [Advanced Functions & Script Blocks](./docs/03-advanced/02-advanced-functions.md)
- [Working with .NET Classes](./docs/03-advanced/03-dotnet-integration.md)
- [DSC (Desired State Configuration)](./docs/03-advanced/04-dsc.md)
- [Advanced Scripting Techniques](./docs/03-advanced/05-advanced-techniques.md)
- [Security & Best Practices](./docs/03-advanced/06-security-practices.md)
- [PowerShell for DevOps](./docs/03-advanced/07-devops.md)
- [Azure & Cloud Automation](./docs/03-advanced/08-cloud-automation.md)

### 📦 [Examples & Projects](./examples/)

- [Hello World Script](./examples/hello-world/)
- [System Info Gatherer](./examples/system-info/)
- [Log Analyzer](./examples/log-analyzer/)
- [AD User Management](./examples/ad-management/)
- [Azure Resource Automation](./examples/azure-automation/)

---

## 🚀 Quick Start

### Installation

PowerShell comes pre-installed on Windows 10/11 and Windows Server 2016+.

For the latest version (PowerShell 7+):

```powershell
winget install --id Microsoft.Powershell --source winget
```

### Your First Command

```powershell
Get-Process | Where-Object {$_.CPU -gt 100}
```

---

## 🎯 Learning Path

1. **Week 1-2**: Master the fundamentals (Cmdlets, Variables, Objects)
2. **Week 3-4**: Build working scripts (Functions, Error Handling, File Operations)
3. **Week 5-6**: Advanced topics (Remoting, DSC, .NET Integration)
4. **Week 7-8**: Real-world projects and automation

---

## 💻 Key Concepts

### PowerShell Philosophy

- **Object-Based**: Unlike traditional shells that work with text, PowerShell works with .NET objects
- **Verb-Noun Naming**: Cmdlets follow a consistent `Verb-Noun` pattern (e.g., `Get-Process`, `Set-Item`)
- **Pipeline Power**: Chain commands together to create powerful one-liners
- **Discoverable**: Use `Get-Command`, `Get-Help`, and `Get-Member` to explore

### Common Cmdlets

```powershell
Get-Command    # Find available cmdlets
Get-Help       # Get help for any cmdlet
Get-Member     # Explore object properties and methods
Where-Object   # Filter results
Select-Object  # Choose specific properties
ForEach-Object # Loop through items
```

---

## 📑 Resources

### Official Documentation

- [🔗 Microsoft PowerShell Docs](https://docs.microsoft.com/powershell/)
- [🔗 PowerShell Gallery](https://www.powershellgallery.com/)
- [🔗 PowerShell GitHub](https://github.com/PowerShell/PowerShell)

### Community Resources

- [🔗 PowerShell.org](https://powershell.org/)
- [🔗 r/PowerShell](https://reddit.com/r/PowerShell)
- [🔗 PowerShell Slack](https://aka.ms/psslack)

### Recommended Books

- "Learn PowerShell in a Month of Lunches" by Don Jones
- "PowerShell for Sysadmins" by Adam Bertram
- "Windows PowerShell in Action" by Bruce Payette

---

## 🧐 Best Practices

1. **Always use approved verbs** (`Get-Verb` to see the list)
2. **Write comment-based help** for your functions
3. **Use parameter validation** to make scripts robust
4. **Implement proper error handling** with Try-Catch-Finally
5. **Follow naming conventions** (PascalCase for functions, camelCase for variables)
6. **Use meaningful variable names** instead of abbreviations
7. **Test scripts in non-production** environments first
8. **Version control your scripts** with Git

---

## 🔧 Tools & Extensions

### VS Code Extensions

- **PowerShell Extension** - Official Microsoft extension
- **PowerShell Preview** - Latest features and improvements
- **PSScriptAnalyzer** - Code quality and style checker

### Helpful Modules

```powershell
# Azure modules
Install-Module -Name Az -AllowClobber -Scope CurrentUser

# Active Directory
Install-Module -Name ActiveDirectory

# Pester (Testing framework)
Install-Module -Name Pester -Force
```

---

## 🤝 Contributing

Contributions are welcome! Feel free to:

- Add new examples
- Improve documentation
- Report issues
- Suggest improvements

---

## 📜 License

This repository is for educational purposes. Feel free to use and modify the scripts for your needs.

---

## 👉 Next Steps

Ready to dive in? Start with:

1. 📘 [Getting Started Guide](./docs/01-beginner/01-getting-started.md)
2. 💡 [Basic Cmdlets Tutorial](./docs/01-beginner/02-basic-cmdlets.md)
3. 💡 [First PowerShell Script](./examples/hello-world/)

**Happy Scripting! 🚀💪**
