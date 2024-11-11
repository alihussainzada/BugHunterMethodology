# Flaws of SMS auth

There are some tests:

- [ ]  SMS flood
- [ ]  Lack of rate limit
- [ ]  Response Manipulation
- [ ]  Users get disable (Ddos)
- [ ]  Response Disclosure

## How to test them

- SMS flood
    - can you send the code many times,
- Lack of rate limit
    - it should be expiredable bcz it is easy to guess 4-6 digits
- Response Manipulation
    - Enter an arbitrary code, copy the success response and paste it to wrong request
- Ddos
    - send so many requests from victim and make them to be not login
- Response Disclosure
    - Check the response sometimes the response reveals the code