# Objects in PowerShell

PowerShell is full of objects. And dealing with different types of objects is something you'll spend a lot of time doing if you want to get into PowerShell.

But what really are objects in PowerShell? The answer is "pretty much everything".

Every command you run in PowerShell returns an object, or an array of objects. If you don't know what an array is, it's basically a data type that contains a group of objects. You have tons of different types of objects. Don't think too hard about different object types, just know that every "type" of object is different. I'll show you how to check what kind of object you're dealing with.

So, every time you run a command in PowerShell, it returns an object. And that object has an object-type, properties and methods. Properties is something that describes the object, methods are "actions" or code that you can execute against the object.

Time for an example! Let's create a variable called test and then assign a string to that variable:

``` 
$Test = "This is a string." 
```

Now if we just run `$Test` in our Shell, PowerShell returns "This is a string.".

<img class="alignnone size-full wp-image-46" src="https://tr4psec.files.wordpress.com/2018/06/teststring.png" width="284" height="139" />

Now I'm going to show you the most important command of them all:

``` 
Get-Member 
```

When you pipe something into `Get-Member`, PowerShell is gonna spit out what type of object you're dealing with, all the methods, and all the properties of the object.

So let's pipe our `$Test` variable into `Get-Member` and see what we're dealing with:

``` 
$Test | Get-Member 
```

<img class="alignnone size-full wp-image-47" src="https://tr4psec.files.wordpress.com/2018/06/testgm.png" width="695" height="262" />

First thing we see is the `TypeName`. This is basically telling you what type of object you're dealing with. A `System.String object`. Or just a String object for short.

Next `Get-Member` lists all the Methods and Properties of the object.

<img class="alignnone size-full wp-image-48" src="https://tr4psec.files.wordpress.com/2018/06/testgm2.png" width="311" height="962" />

So let's first focus on the Properties of our String Object. As you can see in the very long list above, this object only has one Property: `Length`. You can invoke properties by writing:

``` 
$Test.Length 
```

<img class="alignnone size-full wp-image-49" src="https://tr4psec.files.wordpress.com/2018/06/lenght.png" width="195" height="105" />

Methods are invoked the same way, but they end with a `( )` after the method name. Some methods require input inside the `( )`.

Let's try the `ToUpper` method:

``` 
$Test.ToUpper() 
```

<img class="alignnone size-full wp-image-50" src="https://tr4psec.files.wordpress.com/2018/06/toupper.png" width="224" height="208" />

See what our `ToUpper` method did to our string?

Now listen, calling a method on a object does not change the object itself. It merely outputs a new modified version of the object. That means if you run `$Test` again after previously running the `ToUpper` method, you'll see that your string remains unchanged.

If your goal was to actually change the object stored in the `$Test` variable, you would have to declare it again like this:

``` 
$Test = $Test.ToUpper() 
```

Now your `$Test` would look a bit different:

<img class="alignnone size-full wp-image-51" src="https://tr4psec.files.wordpress.com/2018/06/touppernew.png" width="267" height="210" />

Using `Get-Help `and `Get-Command `from my previous post Discover commands combined with looking at the Object type, properties and methods using `Get-Member `should make you a pretty great PowerShell explorer!

This is my first time trying to explain objects in PowerShell in writing. If any of this didn't make sense, please let me know! I'll answer any question you might have on Twitter!

// Tr4p