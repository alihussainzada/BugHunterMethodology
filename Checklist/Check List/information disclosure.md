# information disclosure

- js secret finding command

```bash
cat all-js-tosecret | while read url ; do python3 SecretFinder.py -i $url -o cli >> secret.txt; done
```