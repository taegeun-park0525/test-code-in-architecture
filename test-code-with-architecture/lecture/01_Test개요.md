# 테스트란?

* 어떤 시스템이 제대로 동작하는지 검증하는 과정

### 인수테스트

* 사람이 직접 사용해 보면서 준비된 체크리스트를 체크

### 자동 테스트

* 테스트 코드라는 미리 짜여진 코드를 돌려서 결과값과 예상값을 비교하는 자동테스트

```java
// given -> 이런상황이 주어졌을때
...
// when  -> 이런 호출을 하면
...
// then  -> 이렇게 된다
...
```

* 예시코드

```java
    @Test
    public void 덧셈_연산을_할_수_있다() {
        // given
        long num1 = 2;
        String operator = "+";
        long num2 = 3;
        Calculator calculator = new Calculator();

        //when
        long result = calculator.calculate(num1, operator, num2);

        //then
        assertEquals(5, result); // junit assertion
        assertThat(result).isEqualTo(5); // assertJ assertion
    }
```

이렇게 작성된 코드들이 수백 수천개가 존재하고, 이런 코드를 한번에 돌려 시스템에 문제가 있는지 진단한다.

> H2 : MySQL이나 Oracle 같은 RDB를 InMemory에 잠깐 띄워서 테스트를 하게 해주는 솔루션

## TDD

테스트 주도 개발 방법

구현을 바로하는게 아니라 일련의 과정을 거친다.

* **RED**      -> 깨지는 테스트를 먼저 작성한다.
    * 레드 단계에서는 테스트가 실패하는지가지 제대로 확인해야한다.
* **GREEN** -> 깨지는 테스트를 성공시킨다.
    * 실제로 구현을 한다.
* **BLUE**    -> 리펙토링 한다.
    * 코드를 리펙토링하는 작업을 한다.
    * 파괴적인 리펙토링이 가능하다 why? GREEN 단계에서 확인을 했기 때문

### 장점

개발자들이 저지르는 ㄷ다수의 실수가 교정되기 때문에 주묵을 받는다.

대표적인 실수 :

인터페이스를 생각하지 않고 구현체를 만드는 실수인데, TDD에 따르면 RED단계에서는 일단 컴파일이 되는 코드를 만들고, 테스트가 실패하는지까지 확인해야하기 때문에 개발자는 구현체를 만드는 것보다, 인터페이스를 만드는 것에 집중하게 된다.

(객체들이 어떤 책임을 지고, 이 객체는 어디까지 해줘야 하는지 먼저 생각하게됨)

1. 깨지는 테스트를 먼저 작성해야하기 때문에, 인터페이스를 먼저 만드는 것이 강제된다.

    * 인터페이스에 집중한다? -> 객체지향의 핵심원리 중 하나인 행동에 집중하겠다는 것과 같은말

    * What/Who 사이클

      '**어떤 행위(what)를 수행할 것**' 인지를 결정한 후에, '**누가(who) 그 행위를 수행할 것**인지를 결정해야 한다는 것'

2. 장기적인 관점에서 개발 비용 감소
    * 신규개발에 용이함 -> 테스트 코드가 전부 짜여있기 때문에

### 단점

1. 초기 개발 비용이 많이든다.
    * 요구사항이 명확하지 않거나, 서비스의 흥망성쇠가 눈에 보이지 않는 경우에는 이 방법을 적용하기 어려울 수 있다.
2. 난이도
    * 구성원들의 숙련도가 뒷받침 되어야 함.

---

# 개발자의 고민

1. **무의미한 테스트 (Recap)**

* 간단한 코드 -> 커버리지를 위한 테스트
    * 데이터를 찾을 수 있는 경우, 데이터를 반환한다.
    * 데이터를 찾을 수 없는 경우, 에러를 던진다.

=> 이런 명확한 코드에 있어서, 테스트를 해줘야 하는가..

2. **느리고 쉽게 깨지는 테스트**

* 간단한 테스트지만 개당 300ms가 나온다. 이런 테스트코드들이 수백개를 넘어간다면..? 시간이 오래걸릴거다.
* 되던테스트가 안되는 경우도 있다. (ex- h2문제)
* 테스트간의 병렬처리를 제대로 다루지 못해 실패하는 경우

3. **테스트가 불가한 코드**

예를들어 로그인한 시간을 테스트 할 경우, 로그인 시점을 알 수 없어 테스트가 불가함



### 이러한 테스트에 대한 고민을 통해 설계를 고민하는 것은 좋은 코드를 짜기 위한 과정임!