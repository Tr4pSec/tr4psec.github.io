# Filtering and using Comparison operators in PowerShell

This time I figured I could do a write-up on how to filter data in PowerShell and make it display the information you want to see.

Please take note that everything in this post is done with PowerShell.exe, and some examples might not work in ISE or VSCode.

In PowerShell there are two main ways to filter out data:
<ol>
	Using a filter parameter in your first cmdlet (your command)
	Using other cmdlets to filter objects with comparison operators
</ol>
If you don't know what objects are in PowerShell, I recommend you check out my other post "Objects in PowerShell".

Before we start exploring these two options, I'm going to tell you about a "rule of thumb" that I learned from reading the book <a href="https://www.manning.com/books/learn-windows-powershell-in-a-month-of-lunches-third-edition" target="_blank" rel="noopener">"Learning PowerShell in a month of lunches" </a>:

Filter left first.

What this means is that you always want to try and filter/limit the output of your commands as far left in the command as possible. The further left in the command you are able to filter out data, the less resources you are going to use on whatever device you are running commands on. This could be a normal endpoint, or a server. When scripting you always want to use as little resources as possible.

Now exploring the two different ways of filtering commands, I'll show you examples of filtering on the left side and using other cmdlets on the right.

### Using a filter parameter in your first cmdlet

The reason I'm writing "a filter parameter" and not "the `-filter` parameter" is because the parameter in cmdlets for filtering data is not always the same.

Lets look at this command as our first example:

```
Get-LocalGroup
```

<img class="alignnone wp-image-67" src="https://tr4psec.files.wordpress.com/2018/06/get-localgroup.png" width="659" height="301">

Now say we want to filter our objects based on the `Name` property while "filtering left".

We start by looking at all the parameters of the `Get-LocalGroup` cmdlet by running
```
Get-Help Get-LocalGroup -Parameter *
```

We see that `Get-LocalGroup` has a `-Name` parameter, and it accepts wildcards!

<img class="alignnone size-full wp-image-80" src="https://tr4psec.files.wordpress.com/2018/07/get-helpparameter.png" width="902" height="375">

Now lets look back at our first `Get-LocalGroup` cmdlet. Say we want the Administrators group. We can use the `-Name` parameter we found to run:

```
Get-LocalGroup -Name Administrators
```

<img class="alignnone size-full wp-image-69" src="https://tr4psec.files.wordpress.com/2018/06/get-localgroupadmin.png" width="760" height="128">

If we want to be less specific and just filter for anything that contains *admin* (wildcards) we can run this instead:

```
Get-LocalGroup -Name *admin*
```

<img class="alignnone size-full wp-image-70" src="https://tr4psec.files.wordpress.com/2018/06/get-localgroupadmin2.png" width="904" height="142">

Now lets look at the other way to filter objects.

### Using other cmdlets to filter objects with comparison operators

If your first cmdlet doesn't provide with any parameter to filter out data, you can use another PowerShell cmdlet called `Where-Object`, but you'll need to know how to use comparison operators in order to effectively filter out the data you want.

In short, you use comparison parameters inside the `Where-Object` cmdlet in order to compare data. The comparison always returns a Boolean value: `True` or `False`.

These are some of the comparison operators in PowerShell:

* `-eq` (returns `True` when equal, returns `False` when not equal.)

    * Example 1: `'string' -eq 'string'` (would return `True`)
    * Example 2: `13 -eq 37` (would return `False`)


* `-ne` (returns `True`when not equal, returns `False` when equal.)

    * Example 1: `'string' -ne 'hello'` (would return `True`)
	* Example 2: `3 -ne 3` (would return `False`)


* `-ge`

	Greater than or equal to


* `-le`

	Less than or equal to


* `-gt`

	Greater than


* `-lt`

	Less than



When comparing strings using these comparison operators, PowerShell does not care about upper or lower case strings. It's all the same. If you want to be case sensitive, you can add a "c" in front of the operators. (For example `-ceq` or `-cne.`)

To read more about comparison operators and to see the full list, take a look at `Get-Help about_Comparison_Operators`. One of the operators I recommend reading about is `-Like` and `-Contains`.

Now let me show you some examples of using `Where-Object` and comparison operators to find the same Administrator group from before.

```
Get-LocalGroup | Where-Object -FilterScript {$_.Name -eq 'Administrators'}
```

<img class="alignnone size-full wp-image-72" src="https://tr4psec.files.wordpress.com/2018/06/whereobject11.png" width="741" height="124">

I know that looks hard, so let me explain what happens:

* You run the `Get-LocalGroup` cmdlet and fetch ALL the local groups on the computer
* You send all the objects from that command through the pipeline into our new `Where-Object` cmdlet
* With `Where-Object` we use the `-FilterScript` parameter and add a {} script block
* Inside this {} script block, we pass our current object in.
* Then we use a comparison operator and we write our second object so we have something to compare our first object to.
* `$_` is a reference to the current object in the pipeline (in this case all the localgroups).
* `.Name` references the Name property of the current object.
* Combined `$_.Name`references the name property of the local group objects.
* `-eq` does a "Equal to" comparison like we talked about above against the second object we threw into the {} script block which is a 'Administrators' string.
* Our command then spits out objects where the Name property is equal to our string.

Phew..

Now as a last example I want to use the `-Like` comparison operator in order to be less specific. (<a href="https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-6" target="_blank" rel="noopener">I wrote further up in the post where you can read about the -Like operator.</a>)

```
Get-LocalGroup | Where-Object -FilterScript {$_.Name -like "*admin*"}
```

<img class="alignnone size-full wp-image-73" src="https://tr4psec.files.wordpress.com/2018/06/whereobject2.png" width="917" height="188">

I won't go trough how the command flows because it would be pretty much the same as the previous command. Except that we changed our comparison operator and we changed our second object to get the result we wanted.

I hope you found this post useful!


// Tr4p