# JS_DeepDive

0627

12장 함수 다 읽으려고 했는데 그러면 시간이 늦을 것 같아서 내일 출근해야 하니까 함수 생성까지만 읽었다.

함수 생성 방법 4가지
1. 함수 선언문

function 함수 이름( 매개변수 ) { 실행문 }

2. 함수 표현식

let 변수명 = function (매개변수) { 실행문 }

3. Function 생성자

let 변수명 = new Function(매개변수, 실행문)

4. 화살표 함수

const 상수명 = (매개변수) => 실행문


함수를 만드는 방법 중 3번 빼고는 이미 몇 번 써봤다.
그런데 쓰면서도 1번과 2번의 차이는 몰랐다.
1번 방식과 2번 방식으로 만든 함수는 각각 생성 시점이 달라서 호이스팅의 결과가 달라진다.
선언문으로 함수를 만들면 런타임 이전에 함수가 먼저 실행되어 함수 선언문 이전에 함수를 참조할 수 있고 호출할 수도 있다.
그런데 표현식으로 만들어진 함수는 런타임 이전에 함수가 실행되는 건 동일하지만 변수에 할당된 것처럼 undefined로 초기화된다.
그래서 함수 표현식 이전에 참조 및 호출이 불가능하다.

간단하게 이해하려면 2번 방식은 그냥 변수라고 생각하는 게 편해 보인다.
변수에 함수가 값으로 저장된 형식으로..

-------------------------------------------------------------------------------------------------------------------------------------

0706 

13장 스코프

스코프 : 식별자의 유효 범위
        즉, 식별자를 참조할 수 있는 범위
        
변수를 참조할 때 자바스크립트 엔진은 변수를 참조하는 코드의 스코프에서 시작해 상위 스코프 방향으로 이동하며 선언된 변수를 검색한다.
그래서 하위 스코프의 변수를 상위 스코프에서 참조할 수 없는 것이다. 대신 반대로 상위 스코프의 변수를 하위 스코프에서 참조할 수는 있다.

자바스크립트 엔진은 렉시컬 스코프를 따른다.
즉, 함수가 정의된 시점에서 스코프를 설정한다.

-------------------------------------------------------------------------------------------------------------------------------------

0707

14장 전역 변수의 문제점

1. 암묵적 결합 : 전역 변수는 어디서든 참조가 가능하기 때문에 의도치 않게 재할당이 되거나 상태가 변경될 수 있다. 

2. 긴 생명 주기 : 생명 주기란 메모리 공간이 확보된 시점부터 메모리 공간이 해제되어 가용 메모리 풀에 반환되는 시점까지의 주기를 말한다.
                 함수가 호출되어 생성될 때부터 함수가 종료될 때까지가 생명 주기인 지역 변수에 비해서 전역 변수의 생명 주기는 웹페이지를 닫을 때까지다.
                 따라서 그만큼 메모리 리소스 소비 시간도 길고 전역 변수의 상태가 변경될 수 있는 시간 또한 길며 기회도 많아진다.
                 
3. 스코프 체인에서 종점 : 하위 스코프에서 상위 스코프로 식별자를 검색하는 방식이기 때문에 전역 변수가 제일 나중에 검색된다. 따라서 속도에 차이가 생긴다.

4. 네임 스페이스 오염 : JS는 파일이 분리되어 있어도 하나의 전역 스코프를 공유한다. 
                       따라서 다른 파일 내에서 동일한 이름으로 된 전역 함수가 같은 스코프 내에 존재할 경우 예상치 못한 결과를 가져올 수 있다.
                       
1~3번까지는 이해가 가는데 4번에서 하나의 전역 스코프를 공유한다는 게 잘 이해가 안 간다.
그리고 전역 변수 사용을 억제하는 방법에서 나온 모듈 패턴 부분도 잘 이해가 안 간다. 

그런데 이 부분에서 강의 때 배운 캡슐화 내용이 나왔다. 생각해 보니까 그 부분 복습을 안 했던 것 같아서 까먹기 전에 한번 훑었다.
강의 내용은 OOP, class, get/set, Jquery에 대한 것이다.

-------------------------------------------------------------------------------------------------------------------------------------

0926

15장 let, const 키워드와 블록 레벨 스코프

1. var

초기화문이 있는 var 키워드는 변수가 중복 선언이 된다. 

또한 전역변수로 선언한 변수를 함수 스코프 내에서 또다시 선언한다면 그 변수는 지역 변수가 아닌 전역 변수로 간주되어 중복 선언이 된다. 
ex) var x = 10;
if(true) { var x = 5; }
console.log(x) = 5

변수 호이스팅에 의해 var 키워드로 선언한 변수는 런타임 이전에 선언 단계와 초기화 단계가 실행되어 변수 선언문 이전에 참조할 수 있다. 
console.log(y) = undefined
var y;

이러한 단점을 보완하기 위해 let과 const가 생겼다. 

2. let과 const
let과 const는 중복 선언이 안 된다. 만약 변수를 또다시 선언하려고 하면 에러가 난다. 

그리고 모든 코드 블록을 지역 스코프로 인정하는 블록 레벨 스코프를 따른다. 
let x = 10;
if(true) { let x = 5; }
console.log(x) = 10

또한 호이스팅이 일어나지 않는 것처럼 동작하여 참조 에러를 낸다. 
console.log(y) = ReferenceError : y is not defined
let y;
var 키워드와 달리 선언 단계와 초기화 단계가 따로 일어난다. 런타임 이전에 자바스크립트 엔진에 의해 선언 단계는 이루어지지만 초기화 단계는 변수 선언문에 도달했을 때 일어난다. 이렇게 따로 선언 단계와 초기화 단계가 따로 일어나기 때문에 일시적 사각지대가 생긴다. 
일시적 사/각지대(TDZ)란 스코프의 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간을 의미한다. 

선언 단계 - console.log(y) = ReferenceError : y is not defined
TDZ - console.log(y) = ReferenceError : y is not defined
초기화 단계 ( let y; ) - console.log(y) = undefined
할당 단계( y = 2; ) - console.log(y) = 2

3. const
const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 한다. 그렇지 않으면 에러를 낸다. 
const x; - SyntaxError

또한 let과 달리 원시값을 재할당할 수 없다. 따라서 상수를 저장할 때 사용할 수 있다. 
const x = 2;
x = 4; - TypeError

원시값은 재할당할 수 없지만 객체는 변경이 가능하다. 

const name = { First : 'James', Last : 'Lee'};
name.Last = 'Kim';
console.log(name) = { First : 'James', Last : 'Kim'};


ES6 이후에는 var 키워드 사용은 지양하는 것이 좋으며 재할당이 필요한 경우를 제외하고 const를 사용하여 예기치 않게 일어날 수 있는 재할당을 막아 에러 발생 확률을 낮추는 것이 좋다. 

-------------------------------------------------------------------------------------------------------------------------------------

0927 16장 프로퍼티 어트리뷰트

내부 슬롯과 내부 메서드는 자바스크립트 엔진의 내부 로직.  원칙적으로는 직접 접근하거나 호출 불가하지만 일부 내부 슬롯과 내부 메

서드에 한하여 간접적으로 접근할 수 있는 수단이 있다. 

프로퍼티 어트리뷰트 : 프로퍼티의 상태를 나타냄. 
프로퍼티의 상태 : 값(value), 값의 갱신 가능 여부(writable), 열거 가능 여부(enumerable), 재정의 가능 여부(configurable)
Object.getOwnPropertyDescriptor을 사용하여 이러한 프로퍼티 어트리뷰트를 간접적으로 확인할 수 있다. 이때 첫 번째 매개 변수에는 

객체의 참조를 전달하고 두 번째 매개 변수에는 프로퍼티 키를 문자열로 전달한다. 

데이터 프로퍼티 : 키와 값으로 구성된 일반적인 프로퍼티. 
                       값(value), 값의 갱신 가능 여부(writable), 열거 가능 여부(enumerable), 재정의 가능 여부(configurable)
접근자 프로퍼티 : 자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼

티. 
                       get(읽을 때), set(저장할 때), enumerable, configurable

프로퍼티 정의 : Object.defineProperty를 사용하여 프로퍼티를 정의 또는 재정의할 수 있다. 
                    여러 개의 프로퍼티를 정의 또는 재정의할 때는 Object.defineProperties를 사용하면 된다. 
                    이때 정의해주지 않은 어트리뷰트는 undefined 또는 false로 기본값이 적용된다. 

객체 변경 방지 메서드 - Object.preventExtensions : 프로퍼티 추가 금지.  삭제, 읽기, 쓰기(값 갱신), 재정의 가능
                                                                  Object.isExtensible 메서드로 확장 가능 여부를 확인할 수 있다. 
                            - Object.seal : 읽고 쓰기만 가능
                                               Object.isSealed 메서드로 밀봉 여부 확인 가능
                            - Object.freeze : 읽기만 가능  
                                                  Object.isFrozen 메서드로 동결 여부 확인 가능
이 세 가지 변경 방지 메서드는 얕은 변경 방지 메서드이기 때문에 직속 프로퍼티에만 적용되고 중첩된 객체의 프로퍼티에는 적용되지 

않는다. 중첩된 객체의 프로퍼티까지 변경하기 위해서는 객체이면서 동결되지 않은 객체라는 조건의 함수를 만들어서 적용하면 된다. 

[16장 프로퍼티 어트리뷰트.txt](https://github.com/hyounji375/JS_DeepDive/files/9651207/16.txt)

