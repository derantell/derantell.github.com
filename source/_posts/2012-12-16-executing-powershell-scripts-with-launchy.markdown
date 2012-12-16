---
layout: post
title: "Executing Powershell scripts with Launchy"
date: 2012-12-11 18:53
comments: false
categories: Powershell Productivity
---

An app launcher is an application that lets you launch applications without taking your hands off the keyboard. Just hit the hot key, type a few characters to match the application or file you want to open and you are done. Most launchers can do a lot more than just launching applications, e.g. open websites if you type an URL, act as a simple calculator or---as we will explore in this post---execute scripts.

<!-- more -->

## Invoking Powershell via Launchy

I have been using the [Launchy app launcher](http://www.launchy.net/) for a few years, but not for more advanced tasks than the Windows Start button can handle. So I decided to try some more advanced uses. 

Since Launchy can execute batch files, you can use it to perform almost any task you can think of.

The first thing we need to do is to tell Launchy where to look for the batch files we want to execute. You do that in the settings under the Catalog tab. Add the directory where the scripts are located and add `*.cmd` and `*.bat` as file type filters. I keep my scripts in a [Dropbox](http://dropbox.com) folder that is also a [Git repository](https://github.com/derantell/LaunchyScripts). That way I have easy access to my scripts on any Windows computer I use.

Next we need to create a `.bat` or `.cmd` file that will implement our task. This can be just about anything. Launchy also lets you supply parameters to a command by pressing `tab` when you have matched the command you want to execute. 

In this example I will create a batch file that executes a Powershell script that encodes its argument using Base64 encoding. We start with the simple batch file that will bootstrap the Powershell script:
	
``` bat Bootstrap batch file https://github.com/derantell/LaunchyScripts/blob/master/base64.cmd base64.cmd
@echo off
powershell.exe -file .\base64.ps1 %1
```

The batch file just starts a new Powershell process, passing the name of the Powershell script that implements the Base64 encoding task. The first argument of the batch file is passed on to the Powershell script.

[Powershell.exe](http://technet.microsoft.com/en-us/library/dd315276.aspx) offers three different ways to pass code to be executed. 

* A script file via the `-File` parameter
* [Base64 encoded command](http://dmitrysotnikov.wordpress.com/2011/07/06/passing-parameters-to-encodedcommand/) via the `-EncodedCommand` parameter
* A string or script block via the `-Command` parameter

The Powershell script first tests whether its argument is the path to an existing file. If it is a file path, the file's content is read and put in a variable. If it is not a file, the text of the argument is encoded using UTF-8. Then the data is Base64 encoded and the result is piped to the clipboard using the [clip.exe utility](http://blogs.msdn.com/b/tilovell/archive/2011/09/14/work-tool-of-the-day-clip-exe.aspx).

{% codeblock Base64 encoding script lang:ps1 https://github.com/derantell/LaunchyScripts/blob/master/base64.ps1 base64.ps1 %}
param($text)

if(test-path $text) {
    $path = resolve-path $text
    $bytes = [System.IO.File]::ReadAllBytes($path)    
} else {
    $bytes = [System.Text.Encoding]::UTF8.GetBytes($text)    
}

[convert]::ToBase64String($bytes) | clip
{% endcodeblock %}

Now you can just trigger Launchy and type 

`base64 > c:\temp\cute_cat.jpg`

and the Base64 encoded content of the file is ready for you on the clipboard.

If you are interested [my scripts are available on GitHub](https://github.com/derantell/LaunchyScripts) and currently I have implemented four simple text manipulation tasks: [urlencode](https://github.com/derantell/LaunchyScripts/blob/master/urlencode.cmd), [base64](https://github.com/derantell/LaunchyScripts/blob/master/base64.cmd), [slugify](https://github.com/derantell/LaunchyScripts/blob/master/slugify.cmd) and [hash](https://github.com/derantell/LaunchyScripts/blob/master/hash.cmd). 

