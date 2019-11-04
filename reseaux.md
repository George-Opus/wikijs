<!-- TITLE: Proxy apache2 -->


# La conf 

```sh
 RequestHeader set "X-Forwarded-Proto" "http"
        SetEnv proxy-nokeepalive 1
        ProxyPass / http://127.0.0.1:666/
        ProxyPassReverse / http://127.0.0.1:666
        ProxyErrorOverride off
```