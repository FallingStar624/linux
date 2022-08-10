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



command의 출력을 해석해보면, `permission_test.txt`라는 파일이 **8월 10일 14시 46분**에 만들어졌고 크기는 **62 bytes**라는 의미이다. 또한, 해당 컴퓨터의 **사용자 그룹**에 속해 있으며 그 중에서도 특히 **FallingStar**라는 유저의 파일이라는 의미이다. **파일의 개수**는 하나이며 앞의 문자들은 권한에 대한 symbol들이다. (만약 폴더라면 숫자에는 해당 폴더가 가지고 있는 파일들의 수가 표시됨)



symbol들에 대해 좀 더 자세히 알아보자

![image-20220810211140981](README.assets/image-20220810211140981.png)



우선, 가장 앞에 있는 symbol은 해당 file이 그냥 **파일인지 아니면 폴더(directory)인지** 알려주는 역할을 한다. 하나의 파일이라면 `-` 가 표시되고 directory에 해당하면 `d`가 표시된다.



그 다음으로 등장하는 두 개의 symbol은 read와 write에 관한 권한을 의미한다.

![image-20220810211647672](README.assets/image-20220810211647672.png)

보이는 것 처럼 `r`은 read 권한, `w`는 write 권한을 의미한다.



그 다음 dash로 구분되는 부분은 해당 접속자의 그룹이 파일에 대해 가지는 권한을 의미한다. linux는 그룹별로 file access에 관한 권한을 구분할 수 있기에 이러한 기능을 표시하기 위해 해당 symbol이 사용되었다.

![image-20220810212233682](README.assets/image-20220810212233682.png)



user 그룹이 이 파일에 write 권한이 있었다면 `r`옆에 `w`가 함께 출력되었겠지만, 그러한 권한이 없기에 `-`로 표현되었다.

마지막으로 남은 부분은 해당 컴퓨터에 접속한 모두에게 해당 파일을 read할 권한이 있다는 것을 의미한다. 

![image-20220810212822930](README.assets/image-20220810212822930.png)



### Other sybols



```linux
-rwxr-xr-x  1 root    root        53468 May  1  1999 gzip
```

