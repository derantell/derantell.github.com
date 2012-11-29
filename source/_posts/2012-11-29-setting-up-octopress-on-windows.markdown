---
layout: post
title: "Setting up Octopress on windows"
date: 2012-11-29 20:30
comments: true
categories: octopress
published: false
---

This blog is using the [Octopress](http://octopress.org/) framework for the [Jekyll](https://github.com/mojombo/jekyll) static site generator. When setting everything up I followed [Rob Anderson's instructions](http://blog.zerosharp.com/setting-up-octopress-on-windows/) on how to do this on a Windows 7 machine. In this post I'll describe a few tweaks I had to make to get it all set up.

<!-- More -->

## The hellip command

Cloning the repo and installing the dependencies and the theme went without any problems. It was when I tried to deploy to GitHub that I had my first problem. The `setup_github_pages` task a message somthing like hellip is not a command. This happend to be the line

	system "echo 'My Octopress Page is coming soon &hellip;' > index.html"

So the easy thing to do is to just replace the `&hellip;` with '...'.

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

## Ssh had no permissions

The next problem rose when I tried to run the deploy task to deploy the first time to GitHub. For some reason that I couldn't really figure out, I was denied access when trying to push the site to GitHub. Something to do with the SSH key. So I went back to the Rakefile to change the method from SSH to HTTPS. This meant that I had to change the regular expression that extracted the user name from the repository URL. 

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

## No syntax highlighting

When I started to compose the first post I noticed that syntax highlighting didn't work, neither triple-backtick nor codeblocks. 