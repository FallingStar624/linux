# File Permissions - chmod

- Linux는 UNIX의 파일 접근 및 소유 컨셉을 이어받았다.
  - 다중 사용자 방식(`multi-user concept`)의 네트워크 시스템을 위해 고안되었기 때문이다.
  - 접근 권한과 소유권을 관리를 통해 시스템 정돈 및 안정화가 필요하다.



### File permission symbols

command 창에 아래 명령어를 치면 현재 접속된 경로의 permission 상태를 확인할 수 있다.

``` linux
ls -l
```

```linux
//output
-rw-r--r--  1 FallingStar user   62 Aug 10 14:46 permission_test.txt
```



command의 출력을 해석해보면, `permission_test.txt`라는 파일이 8월 10일 14시 46분에 만들어졌고 크기는 62 bytes라는 의미이다. 또한, 해당 컴퓨터의 사용자 그룹에 속해 있으며 그 중에서도 특히 FallingStar라는 유저의 파일이라는 의미이다. 파일의 개수는 하나이며 앞의 문자들은 권한에 대한 부호들이다.

