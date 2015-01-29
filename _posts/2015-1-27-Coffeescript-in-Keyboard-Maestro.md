---
layout: post
title: Custom Coffeescript Action
---

## CXA?

JXA is a very, very cool extension to Applescript. But what if you like to write in coffeescript? Well, I created a custom action that allows you to do just that.

![image](https://cloud.githubusercontent.com/assets/968047/5936096/1de999c8-a696-11e4-8f69-71a48323d4e1.png)

Behind the scenes it is creating a quick temp file, and pasting

```sh
#!/bin/bash

source /Users/jaredvogt/.bash_profile  # need this to access coffeescript - there are other ways
cat > /tmp/file.coffee <<EOF

# the following is coffeescript
$KMPARAM_Text
EOF
/Users/jaredvogt/.nvm/v0.11.13/bin/coffee -p /tmp/file.coffee | osascript -l JavaScript
```
