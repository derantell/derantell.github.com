---
layout: post
title: "Getting started with Octopress on Windows"
date: 2012-12-02 22:56
comments: true
categories: octopress
---

This blog is using the [Octopress](http://octopress.org/) framework for the [Jekyll](https://github.com/mojombo/jekyll) static site generator. When setting everything up I followed the [Octopress setup guide](http://octopress.org/docs/setup/) and [Rob Anderson's instructions](http://blog.zerosharp.com/setting-up-octopress-on-windows/) on how to do this on a Windows 7 machine. In this post I'll describe a few tweaks I had to make to get it all set up.

<!-- More -->

## The hellip command

Cloning the repo and installing the dependencies and the theme went without any problems. I experienced a slight hiccup when running the `setup_github_pages` task. The command

``` ruby
system "echo 'My Octopress Page is coming soon &hellip;' > index.html"
```

failed with the error message 

    'hellip' is not recognized as an internal or external command, operable program or batch file.

So the easy thing to do is to just replace the `&hellip;` with '...' in Rakefile.

``` diff Replacing hellip
@@ -335,7 +335,7 @@ task :setup_github_pages, :repo do |t, args|
   mkdir deploy_dir
   cd "#{deploy_dir}" do
     system "git init"
-    system "echo 'My Octopress Page is coming soon &hellip;' > index.html"
+    system "echo 'My Octopress Page is coming soon ...' > index.html"
     system "git add ."
     system "git commit -m \"Octopress init\""
     system "git branch -m gh-pages" unless branch == 'master'
```

## Using HTTPS instead of SSH

The next problem rose when I tried to run the deploy task to deploy the first time to GitHub. For some reason that I couldn't really figure out, I was denied access when trying to push the site to GitHub. Something to do with the SSH key. 

    ##Pushing generated _deploy website
    Permission denied (publickey).
    fatal: Could not read from remote repository.

    Please make sure you have the correct access rights
    and the repository exists.

So I went back to the Rakefile to change the method from SSH to HTTPS. This meant that I had to change the regular expression that extracted the user name from the repository URL. 

``` diff Changing the repository URL regex
@@ -303,8 +303,8 @@ task :setup_github_pages, :repo do |t, args|
     puts "(For example, 'git@github.com:your_username/your_username.github.com)"
     repo_url = get_stdin("Repository url: ")
   end
-  user = repo_url.match(/:([^\/]+)/)[1]
-  branch = (repo_url.match(/\/[\w-]+.github.com/).nil?) ? 'gh-pages' : 'master'
+  user = repo_url.match(/https:\/\/github\.com\/([^\/]+)/)[1]
+  branch = (repo_url.match(/\/[\w-]+\.github\.com/).nil?) ? 'gh-pages' : 'master'
   project = (branch == 'gh-pages') ? repo_url.match(/\/([^\.]+)/)[1] : ''
   unless `git remote -v`.match(/origin.+?octopress.git/).nil?
     # If octopress is still the origin remote (from cloning) rename it to octopress
```

After that fix the site deployed to GitHub without errors.

## No syntax highlighting

When I started to write the first post I noticed that syntax highlighting didn't work, neither triple-backtick nor codeblocks. Rob Anderson mentioned this in his post and his solution worked for me too, with the twist that I had to reboot my computer after installing Python 2.7.

## Workflow

Even though I just started the blog, I already love the workflow. Editing markdown in a text editor is so much nicer than using some awful web based WYSIWIG tool. I keep my local repository in a dropbox folder, which makes it easy for me to edit posts on devices that do not have Ruby and Git installed. 

To edit posts I use [Sublime Text 2](http://www.sublimetext.com/). Previously I have been using the [Strapdown.js Preview package](https://github.com/michfield/StrapdownPreview) to preview markdown in the browser, but it does not handle the Octopress syntax highlighting extensions very well. 

Today I discovered [LiveReload](http://livereload.com/). LiveReload monitors the file system and refreshes the browser when changes are detected. A [Sublime package for LiveReload](https://github.com/dz0ny/LiveReload-sublimetext2) is available which handles the communication with the browser. Combining this with Octopress' preview task that regenerates the site when markdown changes are detected is pretty cool. When I save the markdown file, the browser refreshes with the updated post. 

Now I just need to customize the theme a little. 