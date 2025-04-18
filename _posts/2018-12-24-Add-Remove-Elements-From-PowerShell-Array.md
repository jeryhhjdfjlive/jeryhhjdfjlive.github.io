---
title: "How to Easily Add or Remove Items in a PowerShell Array (Step-by-Step Guide)"
excerpt: Learn how to add and remove elements from a PowerShell array using list objects."
categories:
  - PowerShell-howto
tags:
  - PowerShell
  - Arrays
  - PowerShell Basics
  - HowTo

toc: true
---

If you've ever wondered how to modify a PowerShell array after you’ve set it up, you’re not alone! This is a common question — and today, I’m breaking it down into super simple steps.

## What Is an Array in PowerShell?

Straight from the PowerShell docs:

> An array is a special structure designed to store groups of items — they can be all alike or completely different.  
> Starting with PowerShell 3.0, even a single object behaves like an array sometimes!

Creating one? It's easier than you think. Here’s an example you’ve probably already used:

```powershell
$adUsers = Get-AdUser -Filter '*' -Server $adDomainController
```

This command pulls a full list of Active Directory users into an array.

Want to create an empty array? Here’s how:

```powershell
$myArray = @()

# Or, declare the type explicitly
[array]$myArray = @()
```

You can also preload it with values:

```powershell
$myArray = (1,2,3,4,5)
```

Boom! You’ve got an array packed with five numbers.

## Adding Items to an Existing PowerShell Array

Now, what if you want to sneak a 6 into that array? If you try this:

```powershell
$myArray.Add(6)
```

You’ll hit an error saying the array size is fixed — it can’t stretch!

Instead, use the trusty **+=** operator:

```powershell
$myArray += 6

# Verify it
$myArray.length

6
```

**Behind the scenes:**  
PowerShell builds a brand-new array with your new addition and swaps it in place of the old one — all invisibly.

## Want More Flexibility? Meet ArrayList

If you need to dynamically add or remove elements without the "fixed size" drama, you’ll love **ArrayList**:

```powershell
# Create an ArrayList
$myArrayList = New-Object System.Collections.ArrayList($null)

# Add items easily
[void]($myArrayList.Add(1))
[void]($myArrayList.Add(2))

# Check the count
2
```

Need to delete something?

```powershell
# Remove item by index
$myArrayList.RemoveAt(1)
```

**Pro Tip:**  
Use `[void]` when adding items to keep your console clean from unwanted outputs.

### Faster Way to Create ArrayList

Skip the slightly slower *New-Object* method! Instead:

```powershell
[System.Collections.ArrayList]$myArray = @()
```

This shortcut saves resources and speeds up your scripts — a huge win for bigger projects!

Or, simply cast a regular array:

```powershell
$myArray = [System.Collections.ArrayList]@()
```

## Wrapping Up

Here’s a personal best practice:  
Even though PowerShell doesn’t *require* you to define types, I recommend it for better clarity — especially when your scripts stretch into hundreds of lines!

Compare:

```powershell
[string]$myString = 'Some Text'
```

to

```powershell
$myString = 'Some Text'
```

**Bottom line:**  
Specifying types helps your future self (and anyone else) understand your scripts way faster!

---
