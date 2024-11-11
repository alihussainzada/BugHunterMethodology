# Dom Based XSS

There are two important concepts:

- Source
    - Location that the data is taken by the application
    - Examples
        - `document.url`, `document.location.hash` and etc.
        - `document.refere`r,`window.name` and etc.
        - `Ajax`, `Websockets` and `Webmessaging`
        - `Cookies`, `localstorage` and `sessionStorage`
- Sink
    - Location that the data is passed into and get executed
    - Example
        - Javascript execution sinks as: `eval(payload)`, `setTimeout(payload,100)`, `<div onclick=”payload”>`
        - Javascript URI sinks as: `document.loacation = payload`, `location.href = payload`, `window.open=payload`
        - HTML execution sinks as: `htmlElement.innerHTML=payload,` `document.write(payload)`
        - HTML modification to behavior change: `(element).src` or `(element).href` (in certain elements)

More Sinks:

```html
document.write //Works with <script> & Make sure to close the existing elements before running payload.
someDOMElement.innerHTML //Doesnt accept <script> or <svg> & works with <img>,<iframe> + eventhandler(onerror, onload)
window.location //In location sinks use javascript: protocol
window.open //In location sinks use javascript: protocol
someDOMElement.insertAdjacentHTML
someDomElement.onevent
eval
Function
setTimeout
setInterval
setImmediate
execScript
crypto.generateCRMFRequest
ScriptElement.src
ScriptElement.text
ScriptElement.textContent
ScriptElement.innerText
anyTag.onEventName
anyElement.innerHTML
Range.createContextualFragment
```