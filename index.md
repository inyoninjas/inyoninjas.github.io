---
layout: default
---

Inyo is a scriptable (AppleScript) dialog utility optimized for high-visibility messaging and data entry. Inyo's display is a full-screen, modal "overlay" that requires you to intentionally acknowledge notifications or input requests (hence "in yo' face" - btw, [icon = inyo](#icon)). Example use cases:

* full screen notification
* prompt for user input
* I/O for a custom workflow
* display an external webpage
* kiosk mode (with text and input fields formatted large)

Content formatting can range from simple plain text, to markdown or full html. If you have used the awesome [Alfred](http://www.alfredapp.com/), Inyo was inspired from its "Large Type" functionality, but we added **all** the bells and whistles.

### Quick Example (it should look like [this](https://cloud.githubusercontent.com/assets/968047/5717560/93be41ac-9ab7-11e4-8d4d-d84a20c25a64.png))
Inyo is accessed via AppleScript. It can be invoked from the shell with `osascript`, run from Script Editor (or valid saved file formats - `.applescript`, `.scpt`, etc) or accessed with any application that can call AppleScript.
Try this Inyo [_query_](#query) with customized options.

#### At shell prompt

```sh
osascript -e 'tell application "Inyo"' -e 'query  "Enter your name" windowcolor "red" windowopacity 40 inputcolor "#0000ff" inputplaceholder "first name" focus true' -e 'end tell'
```

#### In Script Editor using AppleScript

```applescript
tell application "Inyo"
  query "Enter your name" windowcolor "red" windowopacity 40 inputplaceholder "first name" focus true
end tell
```

#### In Script Editor using [JXA](https://developer.apple.com/library/mac/releasenotes/InterapplicationCommunication/RN-JavaScriptForAutomation/index.html)

```javascript
params = {
  windowcolor: 'red',
  windowopacity: 40,
  inputplaceholder: "first name",
  focus: true
}
Application('Inyo').query('Enter your name', params)
```

### Additional Examples

#### Notification


#### Query


#### HTML Page


#### HTML Form

<p>
<a href="images/maschine.png" data-lightbox="image-1" data-title="My caption"><img src="images/maschine_thumbnail.png"/></a>
</p>
