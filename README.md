# 배열

### 메소드(Method) 오버로딩

- C에서는 sum이란 함수를 만들 때 int형들을 더하는 것과 double 형을 더하는 함수를 만드려면 함수를 두개 만들어서 int_sum() , double_sum()과 같은 식으로 만들어야 함
- 하지만 Java에서는 메소드 오버로딩이 되어 같은 이름이어도 매개변수의 개수나 타입이 다르면 같은 이름으로 여러 함수를 정의할 수 있다.
  - sum(int a,int b)와 sum(double a, double b)와 같은 식으로 같은 이름을 사용해도 됨
  - 둘은 같은 이름이지만 들어오는 매개변수에 따라 작동하는 메소드가 달라짐



### 배열(Array)

##### 1. 배열(Array)이란?

- 자바는 배열을 하나의 클래스로 취급.
- 배열은 동일한 데이터유형만 저장 가능 and 배열은 생성 된 후 크기 변경 불가능.
- Call by Value : 값이 전달되는 경우. 이 경우엔 메소드에 전달 했을 때 값이 복사되어 전달됨.
- Call by Reference : 주소값이 전달되는 경우. 배열은 주소값이 전달되어 복사가 아닌 실제로 전달됨. 이를 이용하면 return 없이도 값 변경이 가능함.

##### 2. 기본 데이터타입의 배열 처리

- 선언에서 "int[]" 를 클래스 이름이라고 생각하자!

- int[] p; 를 하면 p라는 이름의 주소값을 저장할 수 있는 공간이 생김

  - int[5] p; 라 선언하면 에러발생!!

- p = new int[5]; 를 하면 5개의 int 공간을 가진 인스턴스가 만들어지고 그 주소값이 p에 저장됨. 

- 여기선 int형이므로 '0'으로 초기화 됨

- p.length 로 배열의 길이를 알 수 있음.

- int[] p = new int[5] {5,4,3,2,1}; 

  int[]p = {5,4,3,2,1};

  와 같은 방법으로 선언/생성/초기화를 동시에 가능함.

- 확장 for문

  - 기존 for문보다 빠르게 작동함.
  - Java 1.5버전부터 추가됨.

  ```Java
  for(int value : p){
      System.out.println(value);
  }
  ```

  - 위 코드는 p 배열의 원소들에 각각 접근해 value라는 int 타입의 변수에 차례차례 받아온다.

  결과 :

  ```
  5
  4
  3
  2
  1
  ```



##### 3. 참조 데이터타입의 배열 처리

- 앞의 기본 데이터 타입에서 배열 처리 하던 것처럼 참조형 데이터 타입에 배열 처리를 하는 방법

  ```Java
  Student[] students; // 선언
  students = new Student[10];// 생성
  // 초기화
  students[0] = new Student(“kim”, “1”, 80);
  students[1] = new Student(“lee”, “2”, 88);
  students[2] = new Student(“park”, “3”, 90);
  students[3] = new Student(“choi”, “4”, 50);
  ```

  - 이 경우에 students에 4바이트의 주소값을 저장하기 위한 공간이 생기고
  - 길이 10짜리의 null이 담겨있는 배열이 생기며
  - 각각의 배열에 Student라는 인스턴스가 생겨 그 주소값이 지정된다.
  - 그리고 초기화 과정을 통 해 각각의 students 배열에 인스턴스들이 초기화된다.
  - ![1534924641925](C:\Users\KOSTA\AppData\Local\Temp\1534924641925.png)

- 다음 코드의 결과 예측해보기.

  ```Java
  public class ArrayExample4 {
  	public static void main(String[] args) {
  //		Account account = new Account("1111-2222-3333", "정지원", 123456, 100000);
  		Account[] accounts = new Account[100];
  		int index = 0;
  		
  		// 은행 계좌 개설
  		accounts[index] = new Account("1111-2222-3333", "정지원", 123456, 100000);
  		index++;
  
  		accounts[index] = new Account("2222-2222-3333", "김기정", 123456, 200000);
  		index++;
  
  		accounts[index] = new Account("3333-2222-3333", "박지성", 123456, 200000);
  		index++;
  		
  		// 전체 계좌 목록 출력
  		for (Account account : accounts) {
  			System.out.println(account); // 출력 결과 예상해보기
  		}
  	}
  
  }
  ```

- 결과 :

  ```
  Account@7852e922
  Account@4e25154f
  Account@70dea4e
  ```

  - 이 결과는 주소값은 아니고 해시값으로 인스턴스를 대변하는 값이라고 생각하면 된다.

- OOP에서는 외부에서 값을 접근하는 것을 좋아하지 않는다. 즉,

  ```JAVA
  // 전체 계좌 목록 출력
  for (Account account : accounts) {
  	System.out.println(account.getAccountNum()+"\t"+account.getAccountOwner());
  }
  ```

  와 같은 코드로 바꾸는 것을 권장하지 않는다.

  이를 행하기 위해서 대신 Account 클래스에 관련 메소드를 만드는 것을 권장한다.



##### 4. 다차원 배열 처리

- 2차원 배열을 만들기 위해선 다음과 같이 하면 된다.

  ```Java
  char[][] array; // 선언
  array = new char[2][3]; // 생성
  ```

- 그런데 자바에서는 배열도 클래스로 만들어지기 때문에 정방형 모양의 배열을 만드는 것이 아니다.

  - array를 주소값을 저장하기 위한 공간을 만들고,
  - array[2] 를 만들어 주소값을 가지기 위한 1차원 배열을 만든뒤 (2개를)
  - 다시 크기 3개 짜리의 char를 담기 위한 1차원 배열을 만든 뒤
  - 이 배열의 주소값을 array[2]를 이용해 만든 배열에 저장시킨다.

- 이때 배열의 값에 접근하기 위해선 C 똑같다.

  ```Java
  array[0][0] = 'A';
  array[1][2] = 'Z';
  ```

- 다차원 배열을 선언/생성/초기화를 동시에 하려면

  ```Java
  // 3x3 배열을 만드는 경우
  int[][] twoDim1 = new int[][] {{1,2,3,},{4,5,6},{7,8,9}};
  int[][] twoDim2 = {{1,2,3},{4,5,6},{7,8,9}};
  ```

- 다차원 배열을 동적으로 생성할 수 있다. (정방행렬일 필요 없음)

  ```java
  int[][] twoDim; // 선언
  twoDim = new int[3][]; // 생성
  // 서로 다른 크기의 배열 생성
  twoDim[0] = new int[2]; 
  twoDim[1] = new int[4];
  twoDim[2] = new int[1];
  // 초기화
  twoDim[0][0] = 1;
  twoDim[0][1] = 2;
  twoDim[1][0] = 3;
  twoDim[1][1] = 4;
  ```

  아래와 같이도 가능하다.

  ```java
  int twoDim[][] = {{1,2},{3,4,5,6},{7}};
  ```



##### 5. 자바의 명령행 인자 처리 (FileReader.java)

- 자바의 main은 main(String[] args) 와 같이 이루어져 있다.
- 이는 JVM이 실행할 때 여러 개의 String을 받아 올 수 있게 한 것.
- ' java Exam 정지원 박지성 ' 이라고 java로 실행하면 '정지원'과 '박지성'이 인자로 들어가는 것.
  - 정지원이나 박지성은 command argument라고 부름
- Eclipse 에서 인자를 입력하기 위해선 ' Run Configurations - Arguments - Program arguments ' 에서 입력하면 된다.



##### & 참고사항들

- 우리가 사용하는 ' == ' 은 기본 타입을 비교 할 때 사용하는 것.

  ```Java
  String java = "재밋어";
  if(java == "재밋어"){
      System.out.println("true");
  }else{
      System.out.println("false");
  }
  
  ===== 결과 =====
  false
  ```

  - 위와 같은 이유가 발생하는 것은 java가 클래스를 이용해 만들어지는 레퍼런스 변수이므로 java 와 "재밋어"를 비교하면 제대로 비교가 되지 않는다.





### 과제

- 데이터 구조는 배열로부터 시작함.
- 배열을 이용해 데이터 구조를 만들 것.
- 지역 변수가 할당되는 스택(stack) 영역을 만들어 볼 것.
- 클래스 다이어그램
  - ![1534902461378](C:\Users\KOSTA\AppData\Local\Temp\1534902461378.png)
- 먼저 집어넣은 놈이 마지막에 나오는 구조를 만들 것.
  - LIFO(Last in, First out) 구조, 이불 쌓는 것처럼 나중에 들어온 게 먼저 나감.
- 담는 것는 push 라고 하고 가져오는 건 pop이라고 함.
  - pop은 그냥 복사해서 가져오는 것이 아니라 제거하면서 가져옴.
- 다이어그램엔 안나와 있지만 세터 게터도 만들고 생성자도 만들 것.
- 변수는 더 추가해도 괜찮음.

