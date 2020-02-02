# How to create a PSCustomObject

As I wrote in a previous blog post, everything in PowerShell are objects.

There is also a custom PowerShell object with the type `PSCustomObject`.

This post is just gonna be a quick and dirty "How to". 

If you want to read the docs, you'll find them <a href="https://docs.microsoft.com/en-us/dotnet/api/system.management.automation.psobject?view=powershellsdk-1.1.0" target="_blank" rel="noopener">here</a>.

"Wraps an object providing alternate views of the available members and ways to extend them. Members can be methods, properties, parameterized properties, etc."


There are several ways of creating a `PSCustomObject`.

You can create it using `New-Object` and specifying `PSCustomObject` as the type:

```
$myObject = New-Object -Typename PSCustomObject
```

<img class="alignnone size-full wp-image-109" src="https://tr4psec.files.wordpress.com/2019/02/c1.png" width="716" height="169" />

You then add properties and data like shown above.

Another way of doing it is by declaring it as a `PSCustomObject` like this:

<img class="alignnone size-full wp-image-110" src="https://tr4psec.files.wordpress.com/2019/02/c2.png" width="415" height="144" />

Now calling `$myObject` will show you your new object. And running `Get-Member` will show you that it's of the type `System.Management.Automation.PSCustomObject`.

<img class="alignnone size-full wp-image-111" src="https://tr4psec.files.wordpress.com/2019/02/c3.png" width="692" height="602" />

That's it! :)

Quick and dirty post, I'll try to think of some good topics to do longer write-ups on later. This can be a good and quick reference page if you forget how to construct your custom objects!

// Tr4p ❤