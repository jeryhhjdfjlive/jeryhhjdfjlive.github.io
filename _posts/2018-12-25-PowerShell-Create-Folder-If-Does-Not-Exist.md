---

title: "PowerShell Create a Directory If It’s Missing"  
excerpt: "Discover how PowerShell can verify a folder’s existence and create it automatically if missing."  
categories:
  - PowerShell
  - HowTo
  - powershell-howto
tags:
  - PowerShell
  - PowerShell Basics
  - HowTo

toc: true  
comments: true  
---

Today’s post will be a quick guide about a commonly asked question that's definitely worth addressing.

## How to Verify a Folder Exists Using PowerShell

When working with file systems — like saving a log file — it's crucial to ensure the target directory already exists. If not, PowerShell could throw errors or, even worse, cause data loss.

Thankfully, both PowerShell and PowerShell Core include a native cmdlet that makes checking a path simple:

```powershell
Test-Path -Path 'C:\Temp\'
```

The *Test-Path* cmdlet takes a path input and returns *True* if it finds it. You can use this easily in your scripts to validate a folder's presence and create one if missing:

```powershell
# Set up log storage location
[string]$logPath = 'C:\MyLogPath\'

# Create directory if missing
if (!(Test-Path -Path $logPath))
{
    $paramNewItem = @{
        Path      = $logPath
        ItemType  = 'Directory'
        Force     = $true
    }

    New-Item @paramNewItem
}
```

I rely on this pattern so often that I’ve baked it into my script templates — saving time and avoiding repeated coding.

## How to Check Folder Existence via .NET

Underneath, *Test-Path* relies on built-in .NET methods. If you want to flex your .NET skills, you can swap it out with something like this:

```powershell
# Set up log storage location
[string]$logPath = 'C:\MyLogPath\'

# Create directory if missing
if (!([System.IO.Directory]::Exists($logPath)))
{
    [System.IO.Directory]::CreateDirectory($logPath)
}
```

## Final Thoughts

Both approaches — using *Test-Path* or tapping directly into .NET — achieve the same goal.  
While the .NET method offers a slight performance boost, it could make your code less intuitive for others.

Personally, I favor the first method. It keeps the script clean and easy for future collaborators (or even my future self!) to quickly understand and update.

---
