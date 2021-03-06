## icarus-android
Maybe the best rich text editor on android platform. Base on [Simditor](https://github.com/mycolorway/simditor)

![demo](demo.gif)	


## Features
* Alignment (left/center/right)
* Bold
* Blockquote
* Code
* Horizontal ruler
* Italic
* Image
* Indent
* Link
* Outdent
* Ordered List
* Unordered List
* Underline
* Raw html (Insert anything to any selection range that you want via API)

## Usage
Add this line to your `build.gradle` file under your module directory.
```groovy
compile 'com.github.mr5:icarus:0.1.12-SNAPSHOT'
```
Java codes:
```java
import android.app.Activity;
import android.webkit.WebView;
import android.widget.TextView;

import com.github.mr5.icarus.entity.Options;
import com.github.mr5.icarus.button.TextViewButton;
class EditorActivity extends Activity {
	protected WebView webView;
    protected Icarus icarus;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // Get WebView from your layout, or create it manually.
        setContentView(R.layout.activity_main);
        webView = (WebView) findViewById(R.id.editor);
        // I offered a toolbar to manage editor buttons which implements TextView that with icon fonts. 
        // It's just a collection, not a Android View implementation. 
        // TextViewToolbar will listen click events on all buttons that added to it. 
        // You can implement your own `Toolbar`, to prevent these default behaviors.
        TextViewToolbar toolbar = new TextViewToolbar();
        Options options = new Options();
        options.setPlaceholder("Placeholder...");
        icarus = new Icarus(toolbar, options, webView);
        TextView boldButton = new TextViewButton()
        boldButton.setName("bold");
		toolbar.addButton(boldButton);
        icarus.render();
    }
 }
```

[Sample](https://github.com/mr5/icarus-android/tree/master/samples)

## Button Names
* title
* bold
* italic
* underline
* strikethrough
* fontScale
* color
* ol             # ordered list
* ul             # unordered list
* blockquote
* code           # code block
* table
* link
* image
* hr             # horizontal ruler
* indent
* outdent
* alignLeft
* alignCenter
* alignRight

## Options
#### placeholder: String

> Placeholder of Editor. Use the placeholder attribute value of the textarea by default.

default: "Icarus editor."


Example:

```java
options.setPlaceholder("Input something...");
```

#### defaultImage: String

> Default image placeholder. Used when inserting pictures in Edtior.

default: "images/image.png"

Example:

```java
options.setDefaultImage("file:///android_asset/xxx.jpg");
```

#### cleanPaste: Boolean

> Remove all styles in paste content automatically.

default:  false

Example:

```java
options.setCleanPaste(true);
```

#### allowedTags: String[]

> Tags that are allowed in Editor

default: {"br", "span", "a", "img", "b", "strong", "i", "strike", "u", "font", "p", "ul", "ol", "li", "blockquote", "pre", "code", "h1", "h2", "h3", "h4", "hr"}

Example:

```java
// option replacement.
options.setAllowedTags(new String[]{"a", "span", "img"});
// add tag to current tag list.
options.addAllowedTag("pre");
```

#### allowedAttributes: Map&lt;String, List&lt;String&gt;&gt;


> Whitelist of tag attributes.  Note that custom whitelist will be merged into the default one.

default:

```javascript
img: {"src", "alt", "width", "height", "data-non-image"}
a: {"href", "target"}
font: {"color"}
code: {"class"}
```

Example:

```java
// option replacement.
options.setAllowedAttributes(new HashMap<String, List<String>>());
// add new attribute to current tag list.
options.addAllowedAttributes("a", Arrays.asList("class", "src", "alt", "data-type"));
```

#### Load Javascript or Stylesheet files.

```java
icarus.loadCSS("file:///android_asset/editor.css");
icarus.loadJs("file:///android_asset/test.js");
```

## License
[MIT](https://opensource.org/licenses/MIT)



[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-icarus--android-green.svg?style=true)](https://android-arsenal.com/details/1/3601)

