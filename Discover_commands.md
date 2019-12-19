PowerShell commands use a verb-noun syntax. This makes understanding and remembering (and guessing) PowerShell commands easier. Actually, PowerShell has a <a href="https://msdn.microsoft.com/en-us/library/ms714428(v=vs.85).aspx" target="_blank" rel="noopener">list of approved verbs</a>. These can also be viewed in the Shell by running Get-Verb.

(The verb list that Get-Verb returns might not be complete. For an updated list of approved Windows PowerShell verbs with descriptions, see the link above!)

I have two main ways of discovering commands. Using <strong>Get-Help</strong> and <strong>Get-Command</strong>.

PowerShell has a excellent help system (I'll do a post specifically on Get-Help later!) that provides a detailed description, shows the syntax, shows examples etc. You can search through these help files using wildcards, and that's a really good way of discovering commands.

Secondly I'll show how to use <strong>Get-Command</strong>, which is a more straight forward way to list available commands.

With <strong>Get-Help</strong> you can search for anything you'd like using wildcards. Say for example I want to find out more about the local user accounts on my computer. I would run

[code language="powershell" light="True" ]Get-Help *user* [/code]

to find relevant commands. This will list everything within the help files that contains "user".

<img class="alignnone size-full wp-image-30" src="https://tr4psec.files.wordpress.com/2018/06/screenshot_2.png" alt="Get-help user" width="786" height="377" />

I've marked the most interesting ones. Now, all these results are the help files within <strong>Get-Help </strong> that contains "user" in one way or another. And if I wanted to read the specific help file of any of these commands, say for example <strong>Get-LocalUser</strong>, I would have to type-in:

[code language="powershell" light="True" ]Get-Help Get-LocalUser[/code]

Like I said, I'll do a longer post on using the <strong>Get-Help </strong>system later, but I suggest you read the help files of any command you are interested in. If you want to go more into detail, you can add the <strong>-full </strong>parameter:

[code language="powershell" light="True" ]Get-Help Get-LocalUser -full[/code]

<img class="alignnone size-full wp-image-31" src="https://tr4psec.files.wordpress.com/2018/06/get-help-get-localuser.png" alt="get-help get-localuser" width="612" height="289" />

Now let's take a look at using <strong>Get-Command</strong> instead.

<img class="alignnone size-full wp-image-32" src="https://tr4psec.files.wordpress.com/2018/06/get-help-get-commands.png" alt="get-help get-commands.png" width="340" height="174" />

As you can see, the description is pretty straight forward. But Get-Command has two very useful parameters: <strong>-Verb </strong>and <strong>-Noun</strong>.

From our previous <strong>Get-Help </strong>search, we could see that a lot of commands use the Noun <strong>LocalUser</strong>.

So a easy way to list those same commands using <strong>Get-Command </strong>would be to run <strong>Get-Command </strong>and specifying the <strong>-Noun </strong>parameter like this:

[code language="powershell" light="True" ]
Get-Command -Noun LocalUser
[/code]

You could also run

[code language="powershell" light="True" ]Get-Command -Noun *User* [/code]

because the <strong>-Noun </strong>parameter of <strong>Get-Command </strong>also accepts wildcard-input like <strong>Get-Help</strong> did.

<img class="alignnone size-full wp-image-33" src="https://tr4psec.files.wordpress.com/2018/06/get-command-localusers.png" alt="get-command localusers" width="942" height="583" />

Above, the first search is looking for commands that has the specific <strong>-Noun LocalUser</strong>.

In the second search we look for any <strong>-Noun </strong>that contains "user" in some way. Notice how we get more results?

You could turn it around and search using the <strong>-Verb </strong>parameter too, for example:

[code language="powershell" light="True" ]
Get-Command -Verb Get
[/code]

(You can read more about wildcards in PowerShell by running <strong>get-help about_wildcards</strong>. Another useful <strong>Get-Help </strong>tip is the <strong>-ShowWindow </strong>parameter, which sometimes makes the help files easier to read.)

The point of this post was to describe how I discover commands within PowerShell. Did I miss something? Should I have written/explained something in a different way? Do I seem drunk? Leave a comment!

// Tr4p
