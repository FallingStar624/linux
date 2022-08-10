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



command의 출력을 해석해보면, `permission_test.txt`라는 파일이 **8월 10일 14시 46분**에 만들어졌고 크기는 **62 bytes**라는 의미이다. 또한, 해당 컴퓨터의 **유저 그룹**에 속해 있으며 그 중에서도 특히 **FallingStar**라는 유저의 파일이라는 의미이다. **파일의 개수**는 하나이며 앞의 문자들은 권한에 대한 symbol들이다. (만약 폴더라면 숫자에는 해당 폴더가 가지고 있는 파일들의 수가 표시됨)



symbol들에 대해 좀 더 자세히 알아보자

![image-20220810211140981](README.assets/image-20220810211140981.png)



우선, 가장 앞에 있는 symbol은 해당 file이 그냥 **파일인지 아니면 폴더(directory)인지** 알려주는 역할을 한다. 하나의 파일이라면 `-` 가 표시되고 directory에 해당하면 `d`가 표시된다.



그 다음으로 등장하는 두 개의 symbol은 접속한 계정(유저)의 read와 write에 관한 권한을 의미한다.

![image-20220810211647672](README.assets/image-20220810211647672.png)

보이는 것 처럼 `r`은 read 권한, `w`는 write 권한을 의미한다.



그 다음 dash로 구분되는 부분은 해당 유저의 그룹이 파일에 대해 가지는 권한을 의미한다. linux는 그룹별로 file access에 관한 권한을 구분할 수 있기에 이러한 기능을 표시하기 위해 해당 symbol이 사용되었다.

![image-20220810212233682](README.assets/image-20220810212233682.png)



user 그룹이 이 파일에 write 권한이 있었다면 `r`옆에 `w`가 함께 출력되었겠지만, 그러한 권한이 없기에 `-`로 표현되었다.

마지막으로 남은 부분은 해당 컴퓨터에 접속한 모두에게 해당 파일을 read할 권한이 있다는 것을 의미한다. 

![image-20220810212822930](README.assets/image-20220810212822930.png)



### Other symbols

위의 경우가 일반적으로 볼 수 있는 permission 표시이지만, `/bin` dierectory의 경우에는 다른 형태의 permission 표시를 볼 수 있다. linux의 압축 유틸 프로그램인 `gzip`을 `ls -l`명령어를 통해 확인해보면 아래와 같은 출력을 볼 수 있다.

```linux
-rwxr-xr-x  1 root    root        53468 May  1  1999 gzip
```

 우선, 파일의 소유자와 유저 그룹이 **root**로 바뀐 것을 확인 할 수 있다(root는 root 그룹의 유일한 멤버). `x`가 의미하는 것은 해당 파일이 **실행가능(executable)한 파일**이라는 것을 의미한다.  `-rwxr-xr-x`는 root라는 유저와 root가 속한 root 그룹 그리고 해당 파일에 접근하는 모든 사용자가 해당 파일을 실행할 수 있다는 것을 의미한다. 또한, 해당 파일은 실행파일이기 때문에 해당 파일을 소유한 root 유저를 제외하고는 **write** 권한이 존재하지 않는다.

만약, `/sbin`이라는 root만 사용할 수 있는 파일의 접근 권한을 확인해보면 아래와 같이 출력이 된다.

```linux
-rwxr--r--  1 root    root        1065 Jan 14  1999 cron
```

 root만 실행할 수 있으므로 permission에서 유저권한에서만 `x`를 찾아볼 수 있다.

> 참고
>
> `cron`은 linux에서 프로그램을 특정 시간과 특정 조건에서 자동으로 실행하도록 해주는 프로그램



### chmod

`chmod` 는 파일의 permission을 지정해주는 명령어이다.

```linux
chmod permissions file

chmod permission1_permission2_permission3 file
```

`chmod`를 통해 파일의 소유자는 `소유자 자신`/ `자신이 속한 유저 그룹`/ `전체 사용자`에 대해 permission을 설정해줄 수 있다. 

```linux
chmod 644 myDoc.txt
```

 실제 코드는 위와 같이 작성하는데, 숫자를 통해 권한 범위를 설정할 수 있다.

4	read (r)

2	write(w)

1	execute(x)

각각의 숫자들이 특정 권한을 의미하고 이들을 조합하여 권한 범위를 설정해줄 수 있다.

7 = 4+2+1 (read/write/execute)

6 = 4+2 (read/write)

5 = 4+1 (read/execute)

4 = 4 (read)

3 = 2+1 (write/execute)

2 = 2 (write)

1 = 1 (execute)

예를 들어, 아래와 같은 코드를 실행하면

```linux
chmod 766 myDoc.txt
```

파일의 소유자는 자신에게는 모든 권한을 부여하고, 자신이 속한 유저 그룹과 전체 사용자에 대해서는 실행권한을 제외한 read, write 권한만을 부여한다.
