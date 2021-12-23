%{
title:  "Phoenix LiveView and Internet Explorer",
date: "Wed Jul 17 08:50:59 CEST 2019",
tags: ["2019", "andi", "elixir", "phoenix", "liveview"]
}
---
It is a pain and a shame that we still have to suffer from lousy browser 
implementation. But we do. 

Lately, a big enterprise customer forces me to make a Phoenix.LiveView usable 
with Internet-Explorer 11 (because that's the standard, they say)

Ok, no comments about that. Here is a Workaround:

## Install some 'npm-packages'

```sh
npm install --save --prefix assets mdn-polyfills \
   url-search-params-polyfill formdata-polyfill \
   child-replace-with-polyfill
```

## Patch your `app.js`

```js
// IE11 Support for LiveView
import "mdn-polyfills/NodeList.prototype.forEach"
import "mdn-polyfills/Element.prototype.closest"
import "mdn-polyfills/Element.prototype.matches"
import "child-replace-with-polyfill"
import "url-search-params-polyfill"
import "formdata-polyfill"

//just before 
import "phoenix_html"
//.....
```

## Details

The 'npm-packages' adds some functions, missing in IE.
That's the important fix for IE. But other than that, there is a line in 
LiveView updating the class of the session-div accordingly to
the connection state. When not connected, the class is `phx-disconnected`, and 
when the connection appears, it changes to `phx-connected`. In LiveView-code 
this is definitely an assign with "=" but IE seems to interpret it as "+=" and 
the class-definition ends up in being 'phx-disconnected phx-connected'.

### LiveView Javascript
`assets/node_modules/phoenix_live_view/assets/js/phoenix_live_view.js`
```js
602   showLoader(){
603     clearTimeout(this.loaderTimer)
604     this.el.classList = PHX_DISCONNECTED_CLASS
605     this.loader.style.display = "block"
606     let middle = Math.floor(this.el.clientHeight / LOADER_ZOOM)
607     this.loader.style.top = `-${middle}px`
608   }
```

The workaround handles this by selecting elements with both classes and removes 
the 'phx-disconnected' class. I know, this is ugly! I don't want to do it, but 
I have to. Sure, patching the code in LiveView would be a better fix. However, 
patching good code to support bad code is a nogo for me. Better, I add this 
workaround just where I need it.

Add this at the end of `app.js`

```
// IE11 Workaround
function ie11Workaround()
{
    var targetDivArr = document.getElementsByClassName("phx-disconnected phx-connected");
    if(targetDivArr.length>0)
    {
        var targetDiv= targetDivArr[0];
        targetDiv.classList.remove("phx-disconnected");
        targetDiv.classList.add("phx-connected");
    }
}
setInterval(ie11Workaround, 100); // time in ms
```

## No Comments please

Really, I hate this topic and don't want discuss it. If you suffer from the
same pain, feel free to use this workaround (without any kind of warranty).

