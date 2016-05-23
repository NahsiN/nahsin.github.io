---
layout: post
title: Remaining up-to-date with the original Beautiful Jekyll project
subtite: Tracking a remote branch in git
---

To keep my markdown knowledge updated, I decided to start posting today
after a five month hiatus. My first post on [ssh/sshfs hanging](http://nahsin.github.io/2016-05-22-ssh-sshfs-stop-hanging/) didn't show
up as expected, both on mobile and desktop. You can view a screenshot of how the
post looked like on my mobile (on desktop it was the same)  [here](https://lh3.googleusercontent.com/Y7fLpwSqZ8UgmNsG6VAYlcrtKeXvhXyRpV0VfRgPiGm6hMlWfK7Q5_ekhtrrTM3KrJnoG6NmE89v6tk92-d6GpuHavw7PDdZieW-KfgjR96SqLkD2DXVrosY-DliPFrKDNWs2_Q29b5F64jB_Rh_3j2wnJLPHYr_0eINVlJ7jASMLbPsJUjxLRa45O3tKfUvkcxQy-HUkU3qVmrcdoLpSU9jILsKC726faLucN5-phAwsxIp9TOqezEZNznmrXx144350cnk0LNPLW3PQ45RvEbGTCbYh4Uumr9NycjW3iFbT_jrHEr3AmSEqKivX5ta-Lau3UswyUjSfoGXvIY2WyEfI3iDb3zr7qvoz46jCMe6I9OiP6J42B9a4yoYguDMDPV6HZXJKF4k-gEJz4qSxaElFWJR7e1SSj3y0z8AHjsTXb6700gZTboI_STVfXakC04I8015nZ3LR1DJfGmkVGByrHFwQlPOsnaflEe3OcBCxTVqyLcdrv3l2ev3EO-FwgdyZeQRoKXhObIwlamYJmCqq6WMnyD1hFRw9vIZMUeH5MRbQJ_qONAT5iK2WFy6bD5WLEo-FuCAPBC47PsRmASX7er6Tlw=w655-h1091-no)
and [here](https://lh3.googleusercontent.com/-knDZ1VNKWEV52_6u9RCYtYtUH_mmq6QO7ngZYIVQfaZGqWZaFsMjNApysAEe9C9shGbVqIGg70MyK5Y8e1B_qkp41p4fbgsQTC2NL5ohjjl-zJZrX4visbdbVAGj9YFgqigvgmBFdLMmtpCVLST1FYhhdE7eMTWmLHqspawDE7LeFvKiBkcYyw3PXEwus6A_TV0avhoMiCC-1oeN1HHxlrZIynMvHLupqy7HeuH-xbBMC4CAl8wLaQBBm7ntIv9_ky3uhvMjVwyvxYMVJkezd5RNYubA6ppXOWSJt2Hs-0YRxJKwx3DCbskKTVBh5dW23VVaZdmnEN_v8DsxveeYWidOddZiWyt6dXz6jhbd4Eeq0M3X2xPLT5edAdMCFruJK6fIIUSXIggXgPCNe1_Y-jKeCEweqWk-OP5KA4RQ31gBlpSWaDVPps83VGcNjSdcwlUD2tCAW_o9HlILgNnew3emYiqlF4mVzx6T5QXcFJdgEzSU3dX-uL8bGH5ioeMtuZ-M8VSIyoe3HgDS8zI3emrx0VQZYs7T_TW5HqFxYqe-e7WlkPjEIzBdUHqj0pB9QGTbgFCPvu-i30rUGVpAsoaMjS8Rng=w655-h1091-no). I tried various things but nothing worked. everything
my previous posts looked like crap.

At that point, I decided to merge the upstream commits from daattali's
beautiful-jekyll repository hoping that would fix the issue.
And it did! So here goes a lesson
for myself in git. I assume you have a local clone of your repository.
For me, I ran  
~~~
git clone https://github.com/NahsiN/nahsin.github.io ~/nahsin.github.io
~~~
Now we add the beautiful-jekyll repository as a remote branch named
jekyll_remote
~~~
git remote add jekyll_remote https://github.com/daattali/beautiful-jekyll
~~~
Next we create and then checkout a new local branch called jekyll_local.
~~~
git branch jekyll_local
git checkout jekyll_local
~~~
Now that we are on the jekyll_local branch which you verify with
```
git status
```
we fetch the changes from jekyll_remote branch onto our local branch. I guess
one can call it as 'tracking' the remote branch.
~~~
git fetch jekyll_remote
~~~

Now we have a local copy of the [beautiful-jekyll](https://github.com/daattali/beautiful-jekyll)
repository and all it's commits.
Next we are going to checkout our master branch and attempt to merge the changes from
jekyll_local into master.
~~~
git checkout master
git merge jekyll_local
~~~
Chances are you are going to have some merge conflicts that git cannot auto-resolve.
To manually resolve conflicts,
please see section [2.3 from the Pro Git book](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging).
After the conficts are resolved and a merge commit created, you can optionally
delete the branch you just created
~~~
git branch -d jekyll_local
~~~
and then push the contents onto github so your site can be rebuilt
~~~
git push origin master
~~~

That's it! For me, merging the latest changes from beautiful-jekyll repository
resolved the display issues and my posts once again look nice.
Good luck!
