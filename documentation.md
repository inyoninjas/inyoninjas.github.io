---
layout: default
---

# Key Concepts (to quickly orient)
NOTE: this section needs editing

#### Inyo Types
* [**notify**](#notify) - plain-text, read-only notification dialog
* [**query**](#query) - plain-text, data entry dialog
* [**html**](#html) - HTML-format dialog, for notification or data entry
Colloquially, one would refer to a "**notify** inyo".

#### "Dismissing" Inyo
All inyos are modal and can be dismissed with a `left-mouse` click, the `Return` or `Escape` key, or the `Submit` button. Input-enabled inyos (e.g. [_query_](#query), or [_html_](#html)) will only return data entered by the user if dismissed with `Return` or `Submit`.

#### Keyboard Focus
Inyo is an "overlay" on top of your existing desktop. With a **notify** inyo, keyboard focus remains with the application that was active when the inyo popped. If the Inyo window is transparent enough, you will still be able to see the active app and continue to type away on your document! A couple of exceptions - Inyo is always listening for the `esc` and `return` keys, as it uses them to dismiss/submit its window. Also, **query** and **html** (if it has input elements) grab keyboard focus and direct it to input fields/controls.

#### Formatting
You have lots of options for formatting. For **notify**/**query** inyos, text is autosized to fit on the screen - less text, bigger font. There are default option values for font, color, opacity, alignment, etc. In general, we have used the same format tag names as html (specific details below). For an **html** inyo, formatting is wide open, including complete control over text/font/layout (caveats apply - dicussed more below).

#### Options
Each type has a collection of available options. The [Quick Example](quick example) shows how those options are appended to the overall AppleScript command - syntax veries dramatically between osascript, AppleScript and JXA. Pick your poison. For example, JXA allows you to create organized array of properties as an alternative to a long, complicated command string.

#### html - **experimental**
We have given you a big ol' coil of rope here. You can use html to format your content, including input controls. Behind the scenes we are using WebKit window. However, because this isn't an actual browser, there is likely html and css that will be entirely broken. We have inlcuded a couple of examples that work. If you extrapolate from those examples, no promises made about expected functionality.

#### Timeout
In general, intended behavior is to explicilty dismiss a window. However, there are use cases where a timed presentation of content is preferrable. The ``timer|t TIMEOUT` option will display a window for a designated time - then, poof, the window disappears.

#### Returned Data
Returned data is blah, blah. You will have to parse it. blah, blah

#### History
Not yet implemented

#### The List of Caveats
This project was inspired by Alfred's Big Type - we loved the modal, "take over the screen,"" nature of it - but wanted more functionality. In particular, the ability to prompt for input, extending the concept beyond messaging to utiilty in workflow. Inyo, scripted directly, or in conjunction with a "workflow" type engine (like Keyboard Maestro), lets you create "kiosk" type workflows on top of existing applications. [Here is how we have used it - write up example]

That said, this first version of Inyo is only an initial cut at implementing a handful of our wishes. There are things that will be broken, that could be implemented better/differently and lots of additional functionality that could be added. To be frank, while we have used Inyo to create some incredibly cool/useful workflow applications in our recording studio, we only believe that it can be useful to a wider audience. If it can get a little traction, we are ready to add to it - your feedback is essential to Inyo's evolution.

#### Help, Inyo has taken over
If Inyo crashes when it is the top window, you will need to kill it. `cmd-opt-esc` will bring up the "Force Quite Applications" window (it will likely still be behind Inyo) - navigate to Inyo and kill it.

# All the Details

## <a name="notify">Notify</a>
`notify MESSAGE [modal|m {true|false}] [timer|t TIMEOUT] [background color|bc COLOR] [background opacity|bo {0-100}] [font name|fn NAME] [font color|fc COLOR] [align|a {left,center,right}]`

A _notify_ Inyo is intended for displaying plain-format high-visibility notifications. Some basic formatting is applied to the message text. A notification will be displayed in the largest font size that will not cause text clipping, or excessive line-wrapping (a minimum font size is enforced to ensure text remains visible).

### Parameter
`MESSAGE`
Specifies the plain-text format message to be displayed. Other than line breaks, which can be specified directly as linefeed characters or encoded as '`\n`', the contents of `MESSAGE` are displayed literally.

### Options

`[display: text]` : (default: active) Select the display screen. "Active" is the screen with the current active application. "Mouse" is the screen where the mouse is. "NUMBER" refers to a specific screen.
* `[screensaver: boolean]` : (default: false) Window will position over the top of screensaver (or login) screen.
* `[timer: integer]` : Dialog will automatically dismiss itself after specificed time (in seconds).
* `[windowcolor: text]` : (default: black) Window color - specified as a system catalog color name (e.g. red) or as an RGB triplet encoded hexadecimally (e.g. #00ff00) or decimally (e.g. 128,128,128).
* `[windowopacity: integer]` : Percentage opacity of background, where 100 represents complete opacity, and 0 is completely transparent.
* `[block: boolean]` : (default: true) Calling source waits for response (conversely, "fire and forget")
* `[fontalign: text]` : (default: center) Set alignment of notification text.
* `[fontcolor: text]` : (default: black) Font color used to display notification text, where `COLOR` may be specified as a system catalog color (e.g. red), or as an RGB triplet encoded hexadecimally (e.g. #00ff00) or decimally (e.g. 128,128,128).
* `[fontname: text]` : (default: system font) Font used to display notification text.
* `[fontsize: integer]` : (default: autosized) Font size to display notification text.
* `[loadtimeout: integer]` : (default: 10) Time (in seconds) to allow html page to load.

### Examples
#### Simple
A simple notification.

```sh
osascript -e 'tell application "Inyo"' -e 'notify "Alert!"' -e 'end tell'
```

#### Non-modal
A non-modal notification [[screenshot](http://puturlhere)].

```sh
osascript -e 'tell application "Inyo"' -e 'notify "Non-Modal!" modal false' -e 'end tell'
```

#### All Fancy
Customized notification having a partial transparent red background and blue Times-Roman text.

```sh
osascript -e 'tell application "Inyo"' -e 'notify "This is BLUE" background color "red" background opacity 80 font color "0,0,255" font name "Times-Roman"' -e 'end tell'
```

## <a name="query">Query</a>
`query PROMPT [timer|t TIMEOUT] [field value VALUE] [field width WIDTH] [field color COLOR] [field font color COLOR] [background color|bc COLOR] [background opacity|bo {0-100}] [font name|fn NAME] [font color|fc COLOR] [align|a {left,center,right}]`

A `query` Inyo is intended for gathering user input with a plain-format prompt and single data entry field. The prompt message will be displayed in the largest font size that will not cause text clipping, or excessive line-wrapping (a minimum font size is enforced to ensure text remains visible). This Inyo type is always modal. Data is returned to the script caller exactly as it is entered in the text field.

```sh
osascript -e 'tell application "Inyo"' -e 'query "Enter value" background color "red" background opacity 80 font color "0,255,0" field color "#0000ff" default value "default value" font name "Times-Roman"' -e 'end tell'
```

### Parameter
`PROMPT`
Specifies the plain-text format message to be displayed. Other than line breaks, which can be specified directly as linefeed characters or encoded as '`\n`', the contents of `PROMPT` are displayed literally.

### Options

* `[focus: boolean]` : (default: false). Set to true to focus keystrokes on input fields immediately. Otherwise, focus requires a mouse click on input field.
* `[display: text]` : (default: active) Select the display screen. "Active" is the screen with the current active application. "Mouse" is the screen where the mouse is. "NUMBER" refers to a specific screen.
* `[screensaver: boolean]` : (default: false) Window will position over the top of screensaver (or login) screen.
* `[timer: integer]` : Dialog will automatically dismiss itself after specificed time (in seconds).
* `[windowcolor: text]` : (default: black) Window color - specified as a system catalog color name (e.g. red) or as an RGB triplet encoded hexadecimally (e.g. #00ff00) or decimally (e.g. 128,128,128).
* `[windowopacity: integer]` : Percentage opacity of background, where 100 represents complete opacity, and 0 is completely transparent.
* `[fontalign: text]` : (default: center) Set alignment of text.
* `[fontname: text]` : (default: system font) Font used to display notification text.
* `[fontsize: integer]` : (default: autosized) Font size to display notification text.
* `[fontcolor: text]` : (default: black) Font color used to display notification text, where `COLOR` may be specified as a system catalog color (e.g. red), or as an RGB triplet encoded hexadecimally (e.g. #00ff00) or decimally (e.g. 128,128,128).
* `[inputmaxlength: integer]` : Maximum allowable characters.
* `[inputplaceholder: text]` : Text to display as prompt for input.
* `[inputvalue: text]` : Default string in input field.
* `[inputsize: integer]` : Width of input box in characters.
* `[inputcolor: text]` : Background color of input field, where `COLOR` may be specified as a system catalog color (e.g. red), or as an RGB triplet encoded hexadecimally (e.g. #00ff00) or decimally (e.g. 128,128,128).
* `[inputfontcolor: text]` : (default: black) Font color used to display notification text, where `COLOR` may be specified as a system catalog color (e.g. red), or as an RGB triplet encoded hexadecimally (e.g. #00ff00) or decimally (e.g. 128,128,128).
* `[loadtimeout: integer]` : (default: 10) Time (in seconds) to allow html page to load.
* `[submit: boolean]` : (default: false) NOTE: need to finish this description
* `[json: boolean]` : (default: false). Mutli-value response is "|" delimted. If set to true, output is formatted as JSON.
→ text : result

### Result
All content in the data entry field is returned to the caller.

### Examples
#### Simple
A simple query.

```sh
osascript -e 'tell application "Inyo"' -e 'query "Enter something"' -e 'end tell'
```

#### Custom Field Value and Length
A customized entry field with a preset value and increased width.

```sh
osascript -e 'tell application "Inyo"' -e 'query "Enter something" field value "something something something" field width 32' -e 'end tell'
```

#### All Fancy
A customized entry field with black background, decreased width and white, non-proportional text.

```sh
osascript -e 'tell application "Inyo"' -e 'query "Enter (white)" field value "WHITE" field font color "white" field color "black" field width 10 font name "Courier"' -e 'end tell'
```

## Html
`html {HTML|URL} [load timer|lt TIMEOUT] [delimiter|d DELIM] [modal|m {true|false}] [timer|t TIMEOUT] [background color|bc COLOR] [background opacity|bo {0-100}]`

An _html_ Inyo displays an HTML-formatted document supplied directly as a parameter, or indirectly from a local or remote path. Input capture is supported by this Inyo type, the values of all HTML form fields in the document are returned to the caller as a collection of pipe-delimited name-value pairs. Note: a `Submit` button will appear if any form fields are discovered in the HTML document (unless the form is _non-modal_).

### Parameter
`HTML|URL`
Specifies the HTML document to be displayed. This parameter may directly supply the content or may be a local path or remote URL reference to a document. If the first character of the parameter is not a `<` (i.e. left-angle bracket) it is assumed to be a path or URL.

### Options
* `delimiter|d DELIM` (default: "|")
Assigns delimiter used to separate result key-value pairs.
`modal|m {true|false}` (default: _true_)
When set _true_, the utility will not relinquish control to the caller until the user has dismissed the notification (e.g. left-mouse click). If false, the command will return immediately and a `Submit` button will not be displayed.
* `load timer|lt TIMEOUT`
Before HTML document is fully loaded, dialog will automatically dismiss itself after TIMEOUT seconds. This sets a limit on how long the application will wait for a document to load.
* `timer|t TIMEOUT`
After HTML document is fully loaded, dialog will automatically dismiss itself after TIMEOUT seconds. A timer will be displayed in the lower right-hand corner.
* `background color|bc COLOR` (default: _black_)
Background color, where `COLOR` may be specified as a system catalog color name (e.g. red) or as an RGB triplet encoded hexadecimally (e.g. #00ff00) or decimally (e.g. 128,128,128).
* `background opacity|bo OPACITY` (default: _80_)
Percentage opacity of background, where 100 represents complete opacity, and 0 is completely transparent.

### Result
The data from all form elements are encoded as a contiguous sequence of pipe-delimited `name=value` pairs. For instance, the following HTML document

```html
<body style='color:white;font-size:64'>
  Radio 1 <input name='radio1' type='radio' value='1'/><br>
  Input 1 <input name='input1' value="input #1"/><br>
  Input 2 <input name='input2' value="input #2"/><br>
  Radio 2 <input name='radio1' type='radio' value='2' checked/><br>
  Checkbox 1 <input name='checkbox1' type='checkbox'/><br>
  Text Area 1 <textarea name='texarea1'>text from textarea #1</textarea><br>
  Text Area 2 <textarea name='texarea2'>text from textarea #2</textarea><br>
  Select 1 <select name="select1">
    <option>selection 1</option>
    <option>selection 2</option>
    <option>selection 3</option>
  </select>
</body>
```

produces the output

```
input1=input #1|input2=input #2|radio1=2|checkbox1=off|select1=selection 1|
texarea1=text from textarea #1|texarea2=text from textarea #2
```

### Examples

#### Simple
An html Inyo using parameter-supplied HTML content.

```sh
osascript -e 'tell application "Inyo"' -e 'html "<h1>HTML dialog!</h1>"' -e 'end tell'
```

#### Local document
An html Inyo using an HTML document loaded from the local filesystem.

```sh
osascript -e 'tell application "Inyo"' -e 'html "~/username/Documents/index.html"' -e 'end tell'
```

#### Remote document
An html Inyo using an HTML document loaded from a web service.

```sh
osascript -e 'tell application "Inyo"' -e 'html "http://www.apple.com/"' -e 'end tell'
```

Same thing using AppleScript

```applescript
tell application "Inyo"
  html "http://www.apple.com" lt 10
end tell
```
