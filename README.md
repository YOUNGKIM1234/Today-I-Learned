# Today-I-Learned

***

오늘 할 일 :

    1. nginx 서버 뚫기

***

## nginx

1. 재설치

2. reverse proxy 설정
   - 공통 사항 : domain name = viewer
   - 서버 목록 :
     1. web-ui-viewer : location /ui
     2. web-ui : location /server/hyperdata8
     3. web-server : location /server/hyperdata


3. Proxy 설정
    ```
        proxy_pass http://127.0.0.1:8080/hyperdata;
        or 
        proxy_pass http://127.0.0.1:8080/hyperdata8;
        or
        proxy_pass http://localhost:8090/hyperdata8-viewer;

        # redirect off로 한다면 원래 주소 (localhost)가 뜸
        proxy_redirect default;
    ```

4. CORS 설정
    ```
        # CORS
        proxy_hide_header Access-Control-Allow-Origin;
        add_header 'Access-Control-Allow-Origin' '*';
    ```

5. Iframe 뚫기
    ```
        # iframe block
        proxy_hide_header x-frame-options;
        add_header x-frame-options SAMEORIGIN;
    ```
