---
layout: default
---

Inyo is a scriptable (AppleScript) dialog utility optimized for high-visibility messaging and data entry. Inyo's display is a full-screen, modal "overlay" that requires you to intentionally acknowledge notifications or requests for input (hence "in yo' face" - btw, [icon = inyo](#icon)). Example use cases:

* full screen notification
* prompt for field input
* I/O for a custom workflow
* pop an external webpage
* kiosk mode (with text and input fields formatted large)

Formatting can range from simple plain text, to markdown or full html. If you have used the awesome [Alfred](http://www.alfredapp.com/), this is essentially "Large Type", with **all** the bells and whistles.

### Quick Example
(it should look like [this](https://cloud.githubusercontent.com/assets/968047/5717560/93be41ac-9ab7-11e4-8d4d-d84a20c25a64.png))
Inyo is accessed via AppleScript. It can be invoked from the shell with `osascript`, run from Script Editor (or valid saved file formats - `.applescript`, `.scpt`, etc) or accessed in any application that can call AppleScript.
Try this Inyo [_query_](#query) with customized options.

#### At shell prompt
```shell
osascript -e 'tell application "Inyo"' -e 'query  "Please enter a value" windowcolor "red" windowopacity 80 fontcolor "0,255,0" fieldcolor "#0000ff" fieldvalue "a value"' -e 'end tell'
```
#### In Script Editor using AppleScript
```applescript
tell application "PopForm"
  query "Please enter a value" windowcolor "red" windowopacity 80 fontcolor "0,255,0" fieldcolor "#0000ff" fieldvalue "a value"
end tell
```
#### In Script Editor using [JXA](https://developer.apple.com/library/mac/releasenotes/InterapplicationCommunication/RN-JavaScriptForAutomation/index.html)
```javascript
params = {
  windowcolor: 'red',  // Tip: bc is short form for background color
  windowopacity: 80,
  fontcolor: '0,255,0',
  fieldcolor: "#0000ff",
  fieldvalue: "a value"
}
Application('Inyo').query('Please enter a value', params)
// FIXME: there is a bug in this code. The last two fields are ignored
```
