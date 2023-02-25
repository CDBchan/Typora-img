- >### VS Code의 Remote SSH사용하는 이유
  >
  >
  >
  >Local Machine에서 개발 가능하지만 Server 개발일경우 원격으로 개발을 해야하는 경우가 있을수있다. 이럴떈 Local에서 개발을 한후 Server로 이동시켜야한다.  
  >
  >사용하는 Local Machine이 windows인 반면 개발해야하는 환경이 Linux라면 Linux Machine에 접속하여 개발을해야한다. 
  >
  >
  >결론-> VSCode의 Remote Development Extension을 사용하면 Remote Machine을 Local Machine 처럼 생각될수있게 개발하는것이 가능하다. 
  >
  >![](https://velog.velcdn.com/images/cdbchan/post/6e0c5d4d-7b75-451a-bded-b08e18472c05/image.PNG)
  >** VS Code 의 Remote Development Extension 구조도, 출처 : https://code.visualstudio.com/docs/remote/ssh **
  >
  >위 그림처럼 Local OS에서 VSCode로 작업한 것을 SSH Tunnel을 통해 Remote Machine으로 보내는 형태로 작업을 진행할것이다. 
  >(SSH 외 Containers 또는 WSL을 사용하여 개발을 할수있지만 요번 글은 SSH를 사용해보도록 하겠다)
  >
  >---
  >### VS Code에서 SSH를 통한 원격 개발 과정
  >
  >1. VSCode의 확장탭에서 Remote Development를 검색하고 설치한다. ![](https://velog.velcdn.com/images/cdbchan/post/78e6f327-c54f-4f4b-acce-0418a3134155/image.PNG)  
  >
  >2. F1키를 눌러 >Remote-SSH:... 를 클릭한다.![](https://velog.velcdn.com/images/cdbchan/post/4d738ef9-5725-4014-bf85-d27e9ec7701c/image.png)
  >
  >3. 클릭후 UserId@host(ip)를 입력해준다.
  >ex) 저같은경우는 (리눅스 UserId= chanyoun)
  >따라서 -> chanyoun@ip를 입력했습니다.
  >![](https://velog.velcdn.com/images/cdbchan/post/75026692-a6a1-4ce8-94bb-a5f9256d23ed/image.png)
  >
  >4. 그후 Select SSH configuration file to update 라는 text가 보인다. 여기서 우리가 Config File을 저장할 위치를 설정해줘야하는데  
  >** C:\Users\<본인의 윈도우 계정 아이디>\.ssh\<설정파일이름> 식으로 경로를 지정하면된다.  ** 
  >![]
  >(https://velog.velcdn.com/images/cdbchan/post/ef72555c-03f8-4e0b-9c29-03138a0f7d25/image.png)
  >
  >5. 경로를 지정하게되면 VSCode에서 Host added! 라는 알림창이 뜨게되며, Host가 추가될것이다. ![](https://velog.velcdn.com/images/cdbchan/post/5f16ec5a-5711-4e4a-bbeb-0c177ff063c2/image.png)
  >
  >6. 그후 다시 F1키를 눌러 >Remote-SSH를 입력하면 전에는 보이지않았던 host가 보이게되고 클릭하면 아래와같은 새로운 VSCode 창이 뜨게된다. 
  >![](https://velog.velcdn.com/images/cdbchan/post/ccdfecc5-194d-44d9-b3b9-b6eb5524928c/image.png)
  >
  >7. 이후 팔레트 창에 (필자는 Linux사용) 설정해준 Linux hostid에대한 비밀번호를 입력하면
  >아래 사진처럼 왼쪽하단에 SSH-IP 형태로 연결이된다!.
  >![](https://velog.velcdn.com/images/cdbchan/post/a2cbc988-dae5-4e18-8758-11d5e2f0ad55/image.png)
  >
  >8. 마지막으로 ctrl+o를 이용해 원하는 디렉토리에서 작업을 할수있게 된다. ![](https://velog.velcdn.com/images/cdbchan/post/9a6dd64a-42a7-40aa-99b3-7a9d58bdcff4/image.png)
  >
  >### 확인 테스트
  >
  >#### 목표
  >Virtualbox를 통해 Linux를 실행시킨후 Linux의 cs16디렉토리에있는 main.java코드를 수정한다.
  >
  >1. Linux에서 수정하면 -> VSCode로 업데이트가 잘되는지
  >2. VSCode에서 코드 수정시 Linux에서 코드가 업데이트 되는지 확인한다. 
  >
  >
  >1. 현재 main.java의 상태
  >![](https://velog.velcdn.com/images/cdbchan/post/dfb19d0e-6efe-4bc6-b65c-ae860f2b5750/image.PNG)
  >
  >2. Linux에서 코드를 수정할때 VSCode에서 업데이트 되는지 확인한다. 
  >~~~ 
  >// linux connection test 
  >~~~
  >![](https://velog.velcdn.com/images/cdbchan/post/3c791eaa-2f3c-4c93-8015-5fbd41e2ae36/image.PNG)
  >
  >Linux에서 코드 추가후 저장을 누르면 자동적으로 VSCode에도 주석이 추가되는것을 볼수있다.  
  >![](https://velog.velcdn.com/images/cdbchan/post/28e45962-fbb2-41a1-91da-1107a5ad1397/image.PNG)
  >
  >2.  VSCode에서 코드 수정시 Linux에서 코드가 업데이트 되는지 확인한다. 
  >
  >~~~
  >// Windows connection test 
  >~~~
  >주석추가 후 저장
  >
  >![](https://velog.velcdn.com/images/cdbchan/post/7dbea288-f530-4213-9055-09031e7097ec/image.PNG)
  >
  >![](https://velog.velcdn.com/images/cdbchan/post/1c6cdacf-9e21-4a80-874e-b078d04035d4/image.PNG)
  >이번에도 VSCode에서 추가한 주석이 Linux에도 자동적으로 추가가 되는것을 알수있다. 
  >
  >
  >**추후 intellij에서도 SSH를 통해 위 과정을 시도해보겠다!**
  >
  >
  >
  >
  >
  >  