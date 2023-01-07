# Creating your own PowerShell profile

PowerShell provides a great way of making the shell "your own" by using profile scripts. These are basically a .ps1 script that loads every time you open the shell.

I usually customize the shell background, change the starting directory, load modules or add custom functions to my profile. I'm gonna show you how to get up and running with your own PowerShell profile-script.

If you want to learn more about Profiles, please see `help about_profiles` in your shell.

The first thing you might want to do is to check if you already have a profile script or not. You can check this by running:

```text
Test-Path $Profile
```

If `Test-Path $Profile` returns `False`, you don't have a profile created. You can then create your profile by running:

```text
New-Item –Path $Profile –Type File –Force
```

Now if you run `Test-Path $Profile` again it should return `True`.

You can open up your profile script by running `ise $Profile` \(or `code $Profile` if you have Visual Studio Code installed\).

You can find my PowerShell profile [here](https://github.com/Tr4pSec/Microsoft.PowerShell_profile.ps1). You can paste this into your profile and play around with it.

My profile adds two custom functions: One that rolls a dice, and one that fetches a random excuse from a webpage. It also changes the background and foreground color of the shell, changes the prompt, changes the starting directory and adds a nice ASCII alien head.

I think I'm gonna try to use this blog as my personal PowerShell/Security notebook, while writing in a way that can benefit others.

I know there's no screenshots in this post, and the topic is pretty boring unless you've never heard of PowerShell profiles before but it's a start! Another post is scheduled for tomorrow.

If you have any suggestions or questions drop a comment.

// Tr4p

