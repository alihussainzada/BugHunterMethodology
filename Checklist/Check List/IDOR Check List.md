# IDOR Check List

- [ ]  Try parameter pollution 
- [ ]  Add parameters to the endpoints which return the information  | make you own list (JavaScript)
- [ ]  Use Extension /user/01 → /user/02.json
- [ ]  Special Characters 
- [ ]  Try old version `/api/v3/users/01` → `/api/v1/users/02`
- [ ]  Change Request method → GET, POST, PATCH, DELETE, PUT
- [ ]  Check Referrer or some other Headers are used to validated the IDs. | click here
- [ ]  Encrypted IDs, Try to decode using [hashes.com](http://hashes.com) or other tool
- [ ]  Swap GUID with Numeric ID or email
- [ ]  Try GUIDs such as: 0000-0000-000-00000000 and 1111-11111-11111111-111111
- [ ]  GUID Enumeration: Try to disclose GUIDs using Google Dorks, GitHub and so on 
- [ ]  If none of the GUID Enumeration methods work then try: Sign Up, Reset Password, Other endpoints within app and analyze response. These endpoints mostly disclose user’s GUID (or their profile)
- [ ]  403/401 Bypasses: If server responds back with a 403/401 then try to use burp intruder and send 50-100 request having different IDs: from /user/01 → /user/100
- [ ]  If server response with a 403/401, double check the function within the app. Sometimes 403/401 is thrown but the action is performed.
- [ ]  Chain IDOR with XSS for account takeover