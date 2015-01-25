---
layout: post
title: Why Inyo
---

## Big Type 2.0

I have come up with all kinds of uses for Alfred's Big Type - incorporating it in a bunch of workflows. However, it can only be used as a method of notification - and there is no formatting available. The text size, font, location, etc is all predefined by Alfred.
In working with music software on my machine, I begin to leverage Keyboard Maestro to create custom workflow beyond what the software could do natively. In that process, I used Alfred to display informational messages. When you are holding a guitar and standing across the room, having Big Type messages fill the whole screen lets you see things you would never be able to see if they were displaying at "normal" resolution. To extend the workflows to allow for input, I used the capabilities in KM, but unfortunatley, that meant small, ugly, non-configurable dialogs. I thought, if I could have Big Type input dialogs, blah blah...
Inyo was born from that desire. To have a full screen , input dialog that would "overlay" the entire screen.

During this process, we have pondered if Inyo offers a valuable new paradigm. Is there value in having a "channel" of communication (notifications and queries) that "overlays" the whole desktop/OS experience. Rather than have the information/widgets on a second screen, like Dashboard, Inyo creates a workspace on top of your existing screen. And because you can set the opacity of the Inyo window, you can hide

Having notifications pop full screen ensures that you see the message - but having the dismissal of the window tied to `return` or `exc` means you can instantaneously flick the message away without interrupting what you are currently working on. In fact, the keystrokes (with the two previous exceptions), continue to flow through to your active application.
