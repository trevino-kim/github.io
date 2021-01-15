---
title: "터미널 커맨드라인 프롬프트 사용법 기초"
excerpt: "터미널 커맨드라인 프롬프트 사용법 기초를 알아보자."
header:
  overlay_color: "#000"
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Web
tags:
- 웹개발
- 프론트엔드
---


**커맨드 라인(Command Line)이란?**
커맨드 명령어를 입력하여 컴퓨터에게 명령하는 공간이다.

컴퓨터는 사람의 언어를 이해하지 못하므로
컴퓨터가 이해할 수 있는 언어로 명령해야 하는데,
이 때문에 명령어를 배워야 하며,

컴퓨터에게 명령하는 순간 그대로 모든 것을 실행하기 때문에, 신중하게 다뤄야 한다.

Mac OS 는 커맨드 라인을 터미널(terminal)이라고 부른다.
Applications > Utilities 폴더에서 터미널을 찾을 수 있다.


모든 커맨드 명령어는 3가지 파트로 구성되어 있다.

**유틸리티, 플래그, 아규먼트**
**utility, flag, argument**

커맨드 명령어는 항상 utility 가 첫번째에 위치한다.

flag, argument 는 어떤 커맨드를 사용하느냐에 따라 사용이 될 수도 있고 필요 없을 수 도 있다.




**Utility**
유틸리티는 그 자체로 커맨드로 사용이 가능하기 때문에 커맨드(명령어)로 불리기도 한다.

**ls**
**touch**
**rm**
**mkdir**

등등..



**Flag**
플래그로 유틸리티 옵션을 지정할 수 있다.

**rm** 은 파일을 삭제하는 utility 이지만,

**rm -rf**
이렇게 -rf 라는 flag 를 utility 뒤에 붙이면 디렉토리를 삭제하는 명령어로 바뀐다.

flag 는 항상 dash - 또는 two dashes — 로 시작한다.


**-l**
**-rf**



**Argument**
argument 는 utility 를 실행할 때 정확히 어떤 파일/디렉토리/위치에 실행할 지 포인트를 지정하는 역할을 한다.



**dir (window)**
**ls (Mac, linux)**
현재 디렉토리 내에 있는 모든 폴더 리스트를 보고 싶을 때


```
C:\Users\jadek>dir
 Volume in drive C is Windows
 Volume Serial Number is 38E7-7F7C

 Directory of C:\Users\jadek

01/05/2019  10:20 AM    <DIR>          .
01/05/2019  10:20 AM    <DIR>          ..
01/05/2019  10:21 AM    <DIR>          .atom // 폴더 이름 앞에 . 이 있다면 hidden 숨겨진 폴더이다.
01/04/2019  09:10 AM    <DIR>          .idlerc
10/29/2018  09:44 PM    <DIR>          .oracle_jre_usage
12/12/2018  08:03 AM    <DIR>          3D Objects
12/12/2018  08:04 AM    <DIR>          Contacts
01/04/2019  02:52 PM    <DIR>          Desktop
01/02/2019  07:48 PM    <DIR>          Documents
01/05/2019  01:00 PM    <DIR>          Downloads
12/12/2018  08:04 AM    <DIR>          Favorites
12/12/2018  08:04 AM    <DIR>          Links
12/12/2018  08:04 AM    <DIR>          Music
01/05/2019  09:25 AM    <DIR>          OneDrive
12/13/2018  04:20 PM    <DIR>          Pictures
12/12/2018  08:04 AM    <DIR>          Saved Games
12/12/2018  08:04 AM    <DIR>          Searches
12/12/2018  08:04 AM    <DIR>          Videos
               0 File(s)              0 bytes
              18 Dir(s)  701,380,870,144 bytes free
```

**cd 디렉토리이름**
하위 폴더 또는 하위 디렉토리로 이동/변경하고 싶을 때

**cd : change directory**
C:\Users\jadek>cd Documents

C:\Users\jadek\Documents>
디렉토리 이름이 기억나지 않는다면 **cd tab키**를 눌러서 찾을 수 있다.


**cd ..**
상위 폴더 또는 상위 디렉토리로 이동/변경하고 싶을 때



**cls (window)**
**clear (Mac, linux)**
프롬프트 clear 하기




**cd (window)**
**pwd (Mac, linux)**
현재 디렉토리 주소를 보고 싶을 때





**mkdir 디렉토리이름**
현재 디렉토리에 새로운 디렉토리(폴더)를 만들고 싶을 때
(make directory)





**touch 파일이름.확장자**
현재 디렉토리에 새로운 파일을 만들고 싶을 때
C:\Users\jadek>touch abc.html
**※ node.js 를 설치하고, 아래 커맨드를 install 한 후 사용할 수 있다.**
npm install touch-cli -g


**rm 파일이름.확장자**
현재 디렉토리에 특정한 파일을 삭제 하고 싶을 때




**rm -rf 디렉토리이름**
현재 디렉토리에 특정한 디렉토리를 삭제 하고 싶을 때


**디렉토리 내에 있는 모든 파일, 하위 디렉토리까지 전부 삭제하므로 조심하여 사용해야 한다.**

**rm -rf /**
**위 명령어는 루트 디렉토리 까지 모두 삭제하므로 절대 사용하지 말 것**



**copy 파일이름 위치 (window)**
**cp 파일이름 위치**
copy 의 약자로 파일을 지정한 위치에 복사한다.


**move 파일이름 위치 (window)**
**mv 파일이름 위치**
move 의 약자로 파일을 지정한 위치로 이동한다.



**help 유틸리티이름 (window)**
**man 유틸리티이름**

man 은 manual 의 약자로 유틸리티(커맨드)를 어떻게 사용해야 할 지 보여준다.

화살표 위, 아래로 스크롤 할 수 있고, Q 를 누르면 quit 하여 커맨드라인으로 다시 돌아간다.





**sudo 명령어 (linux)**

Super User DO 의 약자. sudo 뒤에 붙인 명령어 전체를 하나의 argument 로 사용한다.

sudo는 컴퓨터 사용자 비밀번호를 요구하는데, 비밀번호 입력과정(****)을 화면에 표시하지 않는다.(Mac)

비밀번호가 맞으면 permission을 얻었으므로 sudo 뒤에 붙인 명령어 전체를 실행한다.
