## 바이트 패딩

- CPU의 연산 부하량을 줄여줄 목적으로 클래스(구조체)에 바이트(패디드 바이트)를 추가하는 기법이다.
~~~ java
class A
{
	char a;
    int  b;
};
A ex;
sizeof(ex);
~~~
-  이때 class A의 크기는 char(1byte) + int(4byte) = 5byte지만 
sizeof(ex)를해보면 5byte가 아닌 8byte가 나오는것을 확인할수있다. 

- 이렇게 5byte가 아닌 8byte가 나오는 이유를 알아보자. 

---

- 32bit 컴퓨터를 사용한다고 가정하면, CPU는 메모리에서 한번에 32bit 즉 4byte 씩 가져와 연산을한다. 

- 그렇다면 CPU가 위 예시에서 ex 에 대한 정보를 가져올때 4byte를 가져온다하면 a를 가져오고 (1byte) b 를 가져올때 (3byte) ->  a(3byte) + b(1bye) = 4byte  
그후 b의 1byte를 추가적으로 가져와야한다. 즉 int b에 관한 정보를 가져올때 4byte 단위로 가져오는 32bit컴퓨터 임에도 데이터를 2번 분활해서 가져오는 비효율적인 일이 발생한다.

- 따라서 이때 바이트패딩 즉 char a가 1byte이지만 3byte 패딩바이트를 붙여 cpu가 ex에 대한 정보를 가져올때  
char a(1byte) + padding byte(3byte), int b(4byte) 식으로 하나의 데이터를 끊어서 가져오는게 아닌 한번에 하나의 데이터씩 가져올수 있도록 한다. 

---
- **Reference**
https://supercoding.tistory.com/37