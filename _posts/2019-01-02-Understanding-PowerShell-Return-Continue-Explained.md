---

title: "Understanding PowerShell Return and Continue"
excerpt: "Discover how Return and Continue work in PowerShell in this in-depth introduction."
categories:
  - PowerShell
  - Post Series - Statements
tags:
  - PowerShell
  - PowerShell Fundamentals
  - PowerShell Core
  - Loops
  - Return in PowerShell
  - Continue in PowerShell
---

## Demystifying PowerShell's Return, Continue, and Exit Commands

Previously, in [Explained: Understanding the PowerShell Break Statement](https://jeryhhjdfjlive.github.io/powershell-howto/powershell-guide/Understanding-PowerShell-Break-Statement-Explained/), we explored how the *break* command can immediately interrupt script execution. We also briefly touched upon other control-flow statements such as *continue*, *return*, and *exit*. Today, we'll dive deeper into *continue* and *return* and their practical applications.

## The Continue Statement

Much like *break*, the **continue** statement influences the flow inside loops. However, instead of exiting the loop entirely, it skips the current iteration and moves to the next item.

Let’s reference the previous counting example for consistency:

```powershell
# Count from 0 to 100 but stop when counter hits 10
$myNumber = 0

while ($myNumber -lt 100)
{
    Write-Host "Currently inside the loop, value: $myNumber"

    $myNumber++

    if ($myNumber -eq 10)
    {
        Write-Host "Reached $myNumber - breaking the loop!"

        break
    }

    Write-Host "Current value is $myNumber"
}

Write-Host 'Exited the loop'
```

This script counts upwards but terminates when it reaches **10** thanks to *break*.

Now let’s tweak it to use **continue** instead:

```powershell
# Counting to 10 but skip a specific value
$myNumber = 0

while ($myNumber -lt 10)
{
    $myNumber++

    if ($myNumber -eq 5)
    {
        Write-Host "Skipping number 5!"

        continue
    }

    Write-Host "Number is $myNumber"
}

Write-Host 'Loop completed'
```

**Expected output:**

> Number is 1  
> Number is 2  
> Number is 3  
> Number is 4  
> Skipping number 5!  
> Number is 6  
> Number is 7  
> Number is 8  
> Number is 9  
> Number is 10  

As you notice, the number *5* is deliberately skipped without disrupting the loop, which is particularly handy for handling exceptions or specific conditions within a loop.

## The Return Statement

The **return** statement, on the other hand, terminates the *current scope* — this could be a function, script, or script block — and optionally outputs a value.

In simple terms, **return** behaves similarly to *break*, but with the added ability to hand back a result.

Here's how it looks using the same loop:

```powershell
# Counting to 10 but stop and return a value when needed
$myNumber = 0

while ($myNumber -lt 10)
{
    $myNumber++

    if ($myNumber -eq 5)
    {
        return $myNumber
    }

    Write-Host "Current number: $myNumber"
}
```

**Output:**

> Current number: 1  
> Current number: 2  
> Current number: 3  
> Current number: 4  
> 5  

When the counter reaches *5*, the script immediately exits the loop and *returns* the number, instead of merely printing it.  
You'll often use this pattern while working with functions, a topic we'll dig into in future articles.

## Final Thoughts

This wraps up our initial dive into PowerShell's control-flow statements.  
Understanding *break*, *continue*, and *return* provides crucial building blocks for writing more advanced scripts.

In the next series, we'll dive into **PowerShell Functions**, where *return* statements play a central role in structuring clean, efficient code.

---
