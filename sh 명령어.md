## scp(ssh 서버로 파일 보내기)

```sh
$ scp a.txt user@chu.snu.ac.kr:/home/user/
# 디렉터리를 보낼 때는 -r 옵션을 사용한다.
$ scp -r app user@chu.snu.ac.kr:/home/user/
```

