# CSV Files in PowerShell

If you work in IT, you have most likely stumbled upon a CSV-file. CSV stands for Comma-separated values. You can read more about CSV-files <a href="https://en.wikipedia.org/wiki/Comma-separated_values" target="_blank" rel="noopener">here</a>.

Two IT-related examples of what data a CSV-file can contain would be a list of AD-users or network traffic. I'll use network traffic as my example. I'm not going to spend more time explaining what a CSV-file is, but I will show you how to read its content with PowerShell!

Please take note that everything in this post is done with PowerShell.exe, and some examples might not work in ISE or VSCode.

Let's say you got a file called traffic.csv. The raw content of the file looks like this:

<img class="alignnone size-full wp-image-87" src="https://tr4psec.files.wordpress.com/2018/07/csv11.png" width="357" height="217">

In this case the file is located under `$home\documents\traffic.csv`

In order to read this CSV-file in PowerShell, we'll have to use the `Import-CSV` cmdlet. If you don't know how to discover PowerShell commands, you can read about that in my previous post Discover Commands.

There is a twist tho. First we need to create a variable that we assign the `Import-CSV` command to. By storing the output objects in a variable, we can more easily play around with the data:

```
$data = Import-Csv .\traffic.csv -Delimiter ","
```

The parameter that we are adding is `-Delimiter`, delimiter is saying what character is separating the data within the CSV-file. In our example it's a comma.

Now if we just run our variable `$data` we'll see the contents of the file.

<img class="alignnone size-full wp-image-88" src="https://tr4psec.files.wordpress.com/2018/07/data1.png" width="343" height="220">

If we pipe our `$data` variable into `Get-Member` we can see what kind of properties and methods we have available. (Properties being the most interesting right now.)

<img class="alignnone size-full wp-image-89" src="https://tr4psec.files.wordpress.com/2018/07/data2gm.png" width="519" height="314">

Notice that `sourceIP`, `destinationIP`, `port` and `action` are all available for us to play with. If you don't know how, check out my previous post Filtering and using Comparison operators in PowerShell.

Back to our CSV-file: :Let's say that we only want to display the events where the traffic was allowed. We would then run:

```
$data | Where-Object {$_.action -eq 'Allow'}
```

<img class="alignnone size-full wp-image-90" src="https://tr4psec.files.wordpress.com/2018/07/csv2.png" width="444" height="202">

What if we want to see all the traffic that is `not` on port 80?

```
$data | Where-Object {$_.port -ne '80'}
```

<img class="alignnone size-full wp-image-91" src="https://tr4psec.files.wordpress.com/2018/07/csv3.png" width="377" height="137">

(Again, if you don't know what `{$_.port -ne '80'}` means, check out my previous post.)

Besides using `Where-Object` to filter out the data, you can also use `Sort-Object `to sort the data. Say we wanted to sort on the action property. We would run this:

```
$data | Sort-Object -Property action
```

<img class="alignnone size-full wp-image-92" src="https://tr4psec.files.wordpress.com/2018/07/csv4.png" width="381" height="235">

You can also use `Select-Object` to select the properties you'd like:

```
$data | Select-Object -Property destinationIP,port 
```

<img class="alignnone size-full wp-image-101" src="https://tr4psec.files.wordpress.com/2018/07/csv6.png" width="472" height="235">

You can also combine these cmdlets:

```
$data | Where-Object {$_.destinationIP -like "*0.0.1"} | Sort-Object -Property action,port
```

<img class="alignnone size-full wp-image-93" src="https://tr4psec.files.wordpress.com/2018/07/csv5.png" width="765" height="207">

Alright. That was my very short, but very straight forward write-up on how to read CSV-files in PowerShell. I hope you found this post helpful. 

// Tr4p