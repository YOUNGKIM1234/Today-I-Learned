# Today-I-Learned


오늘 할 일 :

    1. nginx 서버 뚫기



## nginx

1. 재설치 : https://velog.io/@byjihye/ubuntu2

2. reverse proxy 설정
   - 옵션 참고 : https://12bme.tistory.com/367
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

6. response pending 문제
   nginx는 upstream 서버로 프록시 요청을 보낼 때 http version이 1.0으로 변경한다.
   그런데 http 1.0에서는 connection close가 default라서 커넥션이 닫히는 바람에 계속 response가 오지 않았던 것.

   proxy_http_version 1.1 로, connection을 삭제해서 해결.
   참고 : https://seungtaek-overflow.tistory.com/10
   ```
        proxy_http_version 1.1;
        proxy_set_header Connection "";
   ```



## TIL
git repo 생성, ssh key 만들어서 /TIL/ 폴더만 개인 계정으로 로그인할 수 있도록 git config 설정하기
https://jeunna.tistory.com/109