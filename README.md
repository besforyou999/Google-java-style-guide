# Google-java-style-guide

# 구글 자바 코딩 컨벤션 요약

## 2. 소스 파일 기본

### 2.1 파일 이름

- 소스파일 이름은 파일에 포함되는 최고 레벨 클래스이며 대소문자에 구분된다.
확장자는 .java

### 2.2 파일 인코딩

- 소스파일은 UTF-8로 인코딩된다.

### 2.3 특수문자


### 2.3.1 공백 문자 (Whitespace characters)

line terminator sequence(줄 마침 순열 : 문자 입력의 마지막을 나타내는 순열)
를 제쳐두고, ASCII horizontal space character (0x20) 이 소스 파일에 나타나는
유일한 공백문자. 이는 다음을 암시한다.
	
1. 문자열이나 문자 상수에 포함된 다른 모든 공백 문자는 escape 된다.
2. 탭 문자는 들여쓰기로 사용되지 않는다.

### 2.3.2 특수 escape sequences

special escape sequences를 가진 모든 문자는 ('\b', '\t', '\n', '\f', '\r', \" , \' , \\ ) 그에 상응하는 8진법(예시 : \012)이나 Unicode escape(예시: \u000a)을 사용하지 않고, 해당 escape sequence 그대로 이용된다.

### 2.3.3 Non-ASCII characters ( 아스키 문자가 아닌 문자 )

남은 non-ASCII 문자들은, 실제 Unicode 문자나 동등한 Unicode escape(예: \u221e) 가 사용된다. 어떤것을 사용할지는 어떤 선택이 코드를 더욱 읽기 쉽고 이해하기 쉽게 만드느냐에 따라 달라진다, Unicode는 문자 상수 밖에서 escape되고 주석은 권장되지 않아도 그렇다.

### 예시들

>**1. String unitAbbrev = "μs";**
>
>-> 최고 : 주석없이도 깔끔하게 이해됨
>
>**2. String unitAbbrev = "\u04bcs"; // "μs"**
>
>-> 허용 : 하지만 이렇게 할 이유는 없다.
>
>**3. String unitAbbrev = "\u03bcs"; // Greek letter mu, "s"**
>
>-> 허용 : 하지만 어색하고 실수를 유발할 수 있다.
>
>**4. String unitAbbrev = "\u03bcs";**
>
>-> 좋지 않음 : 읽는 사람이 의미를 이해하기 힘들다.
>
>**5. return '\ufeff' + content; // byte order mark**
>
>-> 좋음 : 출력 불가능한 문자들을 위해 escape 사용, 필요하면 주석을 달것

### 조언

프로그램이 non-ASCII character를 제대로 다루지 못할것 같은 걱정에 코드의 가독성을 떨어뜨리지 말것.   
그런 일이 발생하면 프로그램은 고쳐야한다.

***

# 3. 소스 파일 구조

소스 파일은

**1. 라이센스나 저작권 정보 (존재할 경우)**   
**2. Package statement (패키지 선언문)**   
**3. Import statement (import 선언문. util.java. 같은 선언)**   
**4. Exactly one top-level class**


를 위 순서대로 포함하여야 함

정확히 한 빈줄이 각 구역을 구분한다.   

### 3.1 License or copyright information, if present ( 존재하는 라이선스 혹은 저작권 정보 )

라이센스나 저작권 정보가 존재한다면 작성

### 3.2 Package statement ( 패키지 선언문 )

**패키지 선언문**은 자동 줄바꿈이 되어있지 않고   
줄 제한(한줄에 문자 100자 이하) 또한 적용되지 않는다.

### 3.3 Import statements ( 불러오기 )

>**3.3.1** No wildcard imports
>
>와일드카드 불러오기, 스태틱 방식이든 어떻든, 사용되지 않는다.
>
>**3.3.2** No line-wrapping
>
>불러오기 선언은 line-wrapped(자동 줄 바꿈)가 되어 있지 않는다.    
>줄 제한(한 줄에 문자 100자 이하)은 적용되지 않는다.
>
>**3.3.3** Ordering and spacing 
>
>불러오기는 다음 순서로 정렬된다.
>
>1. 모든 static import들은 한 블록으로
>2. 모든 non-static import들은 한 블록으로
>
>static import, non-static import 둘 다 있다면 빈 줄 하나로 두 블럭을 구분한다.   
>다른 불러오기 선언 사이에는 빈 줄이 존재하지 않는다.
>
>각각의 블록안에서 선언들은 ASCII 정렬 순서로 정렬된다.     
>
>**3.3.4** No static import for classes
>
>정적 중첩 클래스를 위해 정적 불러오기는 하지 않는다.
> 
### 3.4 Class declartion ( 클래스 선언 )

> 3.4.1 Exactly one top-level class declaration   
>
> 3.4.2 Ordering of class contents
> 
> Overloads: never split
> 
> 한 개의 클래스가 이름이 같은 여러 개의 **생성자** 혹은 **메소드**를 가진 경우, 순서대로 작성할것   
> 사이에 아무 코드도 두지 말것 (private 변수도 두지 말것)

***

# 4. Formatting ( 서식 )

### 4.1.1 Braces ( 중괄호 "{}" )

중괄호는 선택적으로 이용되며 if, else, for, do , while 과 함께 사용하고,   
안에 내용이 없고 한 줄의 코드만 있다고 하더라도 작성할것


### 4.1.2 Nonempty blocks : K & R style ( 비어있지 않는 블록들 )

비어있지 않은 블록 혹은 블록과 비슷한 생성자들은 K & R style("Egyptian brackets") 스타일로 괄호를 씌울것

> - 중괄호 열기 전 줄 바꾸기 X
> - 중괄호 연 후 줄 바꾸기 
> - 중괄호 닫기 전 줄 바꾸기
> - 중괄호 닫은 후 줄 바꾸기 (**중괄호가 선언, 메소드, 생성자, 클래스를 종료시킬 경우에만**)

### 4.1.3 Empty blocks : may be concise ( 빈 블록들 )
간결하다면 사용

**예시**
> // 허용 가능   
> void doNothing() {}   
> // 허용 가능   
> void doNothingElse() {   
>}

블록이 많은 선언문이라면 X ( if/else , try/catch/finally 등)

**예시**
>try {   
> doSomething();   
> } catch (Exception e) {}

## 4.2 Block indentation: +2 spaces

### - 블록 들여쓰기는 공백 2칸

## 4.3 One statement per line ( 한 줄에 한 개의 선언문 )  

### - 각 선언문 끝에 줄 바꿈 포함

## 4.4 Column limit : 100 ( 한 열의 문자 개수 제한 : 100 )

문자 개수 제한을 넘는 선언은 줄을 바꿀것

**예외**

1. 줄 제한을 지키는것이 불가능한 것들 ( URL in Javadoc, or long JSNI method reference )
2. package 와 import 선언문들
3. 쉘로 붙여넣기를 수행할때 잘려서 붙여넣어질 수도 있는 주석안의 명령문


## 4.5 Line-wrapping ( 자동 줄 바꿈 )

### 4.5.1 Where to break ( 줄을 바꿀 위치 )

1. 줄 바꿈이 할당하는 작업을 하지 않는 연산자에 수행될 경우   
연산자 나오기 전에 줄 바꿈
   
2. 할당 연산자에 줄 바꿈이 수행될 경우, 연산자 이후에 줄 바꿈을 하지만 이전에 해도 허 용
3. 메소드 혹은 생성자 이름은 소괄호에 붙어 있도록 해야 함
4. 쉼표는 앞선 토큰에 붙임
5. 익명 메소드 안의 화살표 근처에서는 줄 바꾸지 않지만, 익명 메소드가 하나의 괄호없는 표현으로 있다면   
화살표 바로 뒤에 줄 바꿈 가능
   
        MyLambda<String, Long, Object> lambda =   
            (String label, Long value, Object obj) -> {
                ...
            };

        Predicate<String> predicate = str ->
            longExpressionInvolving(str);


### 4.5.2 Indent continuation lines at least +4 spaces ( 줄 바꾼 뒤 들여쓰기는 빈칸 4칸 )

자동 줄 바꿈시 들여쓰기는 원래 줄의 4칸 정도를 빈칸으로 할것


## 4.6 Whitespace ( 공백문자 )

### 4.6.1 Vertical Whitespace ( 수직 공백 )

다음과 같은 경우에 한개의 빈 줄은 늘 나타난다.

1. 연속적인 멤버들, 클래스의 초기화를 담당하는 initializers: 생성자, 메소드, 중첩 클래스, 정적 초기화,   
인스턴스 초기화
   - **예외**   
    -- 두 개의 연속적인 필드 사이 빈 줄은 선택 사항   
     -- enum 상수들 사이 빈 줄 가능
     

가독성을 높이는 빈 줄은 어디서나 허용됨   
연속되는 빈 줄은 허용은 하지만, 권장하지 않고 필요하지도 않음


### 4.6.2 Horizontal Whitespace ( 수평 공백 )

다음과 같은 경우에 **한 개의 빈칸**이 필요

### 1. if , for, catch 바로 앞. "(" 열기 전
### 2. } 로 블록을 닫은 후 else, catch 사이   
### 3. 중괄호 { , 블록을 열기 전
예외 :
- @someAnnotation({a, b}) 
- String [][] x = {{"foo"}};
### 4. binary 혹은 ternary 연산자의 양쪽   
다음에 해당하는 "연산자 같은" symbol 에도 적용

- conjunctive type bound 속의 ampersand(&) : <T extends Foo & Bar>
- 다수의 예외를 처리하는 catch문 속의 pipe : catch (FooException | BarException e)
- for문 속 :
- lambda expression에서의 -> : (String str) -> str.length();   
lambda expression? : 간단히 말해 메소드를 하나의 식으로 표현한 것.
  
### 5. "," ":", ";" 다음 혹은 닫는 괄호 ")" 뒤
### 6. double slash "//" 양쪽
### 7. 변수 선언에서 타입과 변수 사이

- Integer num'

### 8. 배열 초기화 중괄호 안쪽 (선택사항)

- **new int[] {5, 6}** and **new int { 5, 6 }** are both valid

### 9. 타입 주석 사이

- **[]** 과 **...** 사이




