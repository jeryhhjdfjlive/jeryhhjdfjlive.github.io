---

title: "How to Automatically Delete Old Files and Folders with PowerShell (Step-by-Step Guide)"  
excerpt: "Discover how to create PowerShell scripts that automatically find and delete files and folders older than a specific number of days. Improve storage management and automate file cleanup with this easy tutorial."  
categories:
  - PowerShell
tags:
  - PowerShell
  - Automation
---

## Understanding the Need for File Cleanup Automation

In the world of automation scripting, it’s critical to log every action performed. This helps in quickly diagnosing issues and tracking script execution timelines.  
However, storing log files indefinitely can consume valuable disk space — and it's rarely necessary to keep them forever.

Luckily, PowerShell provides a straightforward way to **automatically delete files** that are older than a set number of days.  
In this tutorial, I’ll walk you through how to automate old file removal using simple PowerShell scripts.

## Defining the Cleanup Goal

Our objective is to identify and delete files from a specified directory that were created over **90 days** ago.  
I'll demonstrate this process using a sample folder filled with outdated files.

Before we dive into writing the script, here are a few critical decisions to make:

- Should we search within subfolders as well?
- What file types should be targeted for deletion?
- How long should files be retained before removal?

Here’s the configuration setup we'll use:

| Include Subfolders | File Extension | Retention Period |
| ------------------- |:--------------:| ----------------:|
| Yes                 | .log            | 90 days          |

## How to Find Files for Deletion

Once the parameters are clear, let’s start coding. The first step is defining the essential variables:

```powershell
[string]$filePath = 'C:\TestCleanup\'
[string]$fileExtension = '*.log'
[int]$fileAge = 90
[datetime]$ageTimeSpan = (Get-Date).AddDays(-$fileAge)
```

These variables guide the script on what to look for.  
The *$ageTimeSpan* calculates the threshold date by subtracting 90 days from the current date.

Now, retrieve a list of files that meet the age and extension criteria using *Get-ChildItem*:

```powershell
# Collect eligible files
[array]$filesToPurge = Get-ChildItem -Path $filePath -Filter $fileExtension -File |
        Where-Object { $_.LastWriteTime -lt $ageTimeSpan }
```

This command filters for all *.log* files that are older than the specified 90-day threshold.

## How to Delete Old Files with PowerShell

After gathering the files, loop through them and delete each outdated file:

```powershell
foreach ($file in $filesToPurge)
{
    # Capture full file path
    [string]$fileName = $file.FullName

    # Delete the file without prompting
    Remove-Item $fileName -Confirm:$false
}
```

However, it’s good practice to check if any files actually exist before trying to delete them. Let’s improve the code with a simple conditional check:

```powershell
if ($filesToPurge.Count -gt 0)
{
    foreach ($file in $filesToPurge)
    {
        # Capture full file path
        [string]$fileName = $file.FullName

        # Delete the file without prompting
        Remove-Item $fileName -Confirm:$false
    }
}
else
{
    # Optional: Add proper logging mechanism
    Write-Host -Object 'No outdated files found to delete!'
}
```

## Expanding the File Cleanup Script

The PowerShell script shared above is a minimal example — you can expand it based on your specific needs, such as:

- Scanning multiple directories
- Excluding specific subfolders
- Implementing centralized configuration files for flexible management

There are plenty of additional features you could incorporate to make the script even more powerful.  
I'm currently developing an enhanced version of this script and will share it as soon as it’s tested and ready.
