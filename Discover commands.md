PowerShell commands use a verb-noun syntax. This makes understanding and remembering (and guessing) PowerShell commands easier. Actually, PowerShell has a <a href="https://msdn.microsoft.com/en-us/library/ms714428(v=vs.85).aspx" target="_blank" rel="noopener">list of approved verbs</a>. These can also be viewed in the Shell by running `Get-Verb`.

(The verb list that `Get-Verb` returns might not be complete. For an updated list of approved Windows PowerShell verbs with descriptions, see the link above!)

I have two main ways of discovering commands. Using `Get-Help` and `Get-Command`.

PowerShell has a excellent help system (I'll do a post specifically on Get-Help later!) that provides a detailed description, shows the syntax, shows examples etc. You can search through these help files using wildcards, and that's a really good way of discovering commands.

Secondly I'll show how to use `Get-Command`, which is a more straight forward way to list available commands.

With `Get-Help` you can search for anything you'd like using wildcards. Say for example I want to find out more about the local user accounts on my computer. I would run

```
Get-Help *user*
```

to find relevant commands. This will list everything within the help files that contains "user".

<img class="alignnone size-full wp-image-30" src="https://tr4psec.files.wordpress.com/2018/06/screenshot_2.png" width="786" height="377" />

I've marked the most interesting ones. Now, all these results are the help files within `Get-Help` that contains "user" in one way or another. And if I wanted to read the specific help file of any of these commands, say for example `Get-LocalUser`, I would have to type-in:

```
Get-Help Get-LocalUser
```
Like I said, I'll do a longer post on using the `Get-Help` system later, but I suggest you read the help files of any command you are interested in. If you want to go more into detail, you can add the `-full` parameter:

```
Get-Help Get-LocalUser -full
```

<img class="alignnone size-full wp-image-31" src="https://tr4psec.files.wordpress.com/2018/06/get-help-get-localuser.png" width="612" height="289" />

Now let's take a look at using `Get-Command` instead.

<img class="alignnone size-full wp-image-32" src="https://tr4psec.files.wordpress.com/2018/06/get-help-get-commands.png" width="340" height="174" />

As you can see, the description is pretty straight forward. But Get-Command has two very useful parameters: `-Verb` and `-Noun`.

From our previous `Get-Help` search, we could see that a lot of commands use the Noun `LocalUser`.

So a easy way to list those same commands using `Get-Command` would be to run `Get-Command` and specifying the `-Noun` parameter like this:

```
Get-Command -Noun LocalUser
```

You could also run

```
Get-Command -Noun *User*
```

because the `-Noun` parameter of `Get-Command` also accepts wildcard-input like `Get-Help` did.

<img class="alignnone size-full wp-image-33" src="https://tr4psec.files.wordpress.com/2018/06/get-command-localusers.png" width="942" height="583" />

Above, the first search is looking for commands that has the specific `-Noun LocalUser`.

In the second search we look for any `-Noun` that contains "user" in some way. Notice how we get more results?

You could turn it around and search using the `-Verb` parameter too, for example:

```
Get-Command -Verb Get
```

(You can read more about wildcards in PowerShell by running `get-help about_wildcards`. Another useful `Get-Help` tip is the `-ShowWindow` parameter, which sometimes makes the help files easier to read.)

The point of this post was to describe how I discover commands within PowerShell. Did I miss something? Should I have written/explained something in a different way? Do I seem drunk? Leave a comment!

// Tr4p
