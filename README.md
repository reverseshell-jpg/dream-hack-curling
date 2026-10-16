# dream-hack-curling
## 1. RECON
+ ```ALLOWED_HOSTS = ['dreamhack.io', 'tools.dreamhack.io']```
+ ```/api/v1/test/curl```
<img width="565" height="402" alt="image" src="https://github.com/user-attachments/assets/87af7e74-e894-45d9-961b-08263f6e5fc8" />

This endpoint accepts the POST method and takes input via the `url` parameter.
It checks whether the supplied `url` starts with `http://` combined with one of the entries in the `ALLOWED_HOSTS` list; if not, it returns an error (1).
If the `url` ends with the string `/test/internal`, it also returns an error (2).
Finally, it uses `curl` to connect to the supplied url.
+ ```/api/v1/test/internal```
<img width="553" height="130" alt="image" src="https://github.com/user-attachments/assets/8e4bdc65-1eac-41e3-b311-af0c7d1787b8" />

This endpoint accepts the GET method.
It checks the requester's IP; if it is `127.0.0.1`, it returns the flag — otherwise it returns `Only local access is allowed` (3).

## 2. EXPLOIT
To get the flag we need to bypass 3 layers of filtering:

(1): the supplied url must start with http://dreamhack.io or http://tools.dreamhack.io

(2): for the ending of the url, we can append special characters that don't break the url, such as `?` or `#`

(3): According to [RFC 3986](https://www.rfc-editor.org/rfc/rfc3986.txt), the authority syntax of a URL is: scheme://[userinfo@]host[:port]/path — the way the url parser/curl works, everything before the `@` is ignored when determining the host to connect to; the real host is the part after the `@`

## 3. GET FLAG
`DH{S5Rf_1s_funNy:DB3uS*************==}`
