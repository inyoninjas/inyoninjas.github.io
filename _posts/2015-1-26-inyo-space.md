---
layout: post
title: Inyo Space
---

## A new layer to exploit

Inyo Space is the layer that sits above everything else on your computer. It is different than the "active application" because it may or may not have input focus. It is actively capturing all input and passing it through to underlying application that is the true "active" application. In this layer, you can notify, query for input, augment, display notes - all of these can be contextually related to the active application and be dismissed with a simple keystroke. Further, they will update based on the active app.

It is the top visual layer, but not the current "active application."

Inyo knows all the active applications (their respective windows) and where they fall in the z-layer space. It could be used as an application switcher. 

inyo is the "window" above all of your running apps. That window "overlays" everything else in your environment. In this window, you can display messages, ask for user input, show a web page, pop a widget. The window can be shortlived, or it can hang around for a while. It can visually block everything underlying, or you can set the opacity to see through it. You can have it "block" user input until the content is dealt with/dismissed - or it can simply set there visually while you continue to work on all of your underlying applications.
