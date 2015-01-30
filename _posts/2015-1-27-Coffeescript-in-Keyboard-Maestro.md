---
layout: post
title: Custom Coffeescript Action
---

## CXA?

JXA is a very, very cool extension allowing you to use Javascript to control Applescript. But what if you like to write in coffeescript? Well, I created a custom action that allows you to do just that.

![image](https://cloud.githubusercontent.com/assets/968047/5936096/1de999c8-a696-11e4-8f69-71a48323d4e1.png)

Behind the scenes the output from processing the coffeescript with the `-p` and `-e` options is piped `\` to `osascript` with the option `-l JavaScript` (note, the J and S do need to be capitalized).

```sh
#!/bin/bash
source /Users/jaredvogt/.bash_profile
coffee -p -e "$KMPARAM_Text" | osascript -l JavaScript
```
