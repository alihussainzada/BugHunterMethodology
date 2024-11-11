# Methodology

How to find XSS in a scope?

- important phase? discover hidden parameters
- Search for the reflections, it doesn't matter its stored or not. Work manually on the reflection
- Download JS and HTML files then grep JavaScript keywords
    - Search for the eventListener `addEventListener\((?:’|\”)message(?:’|\”)”`
    - Search for the JavaScript sources or sinks
- Search for the postMessages and try to find misconfiguraion
- Blind XSS → Spray everywhere!!!
- Some tools (Gxss, kxss, dalfox, etc) use them all