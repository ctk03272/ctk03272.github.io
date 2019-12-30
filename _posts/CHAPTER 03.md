# CHAPTER 03

# 자바스크립트 데이터 타입과 연산자

 자바 스크립트의 기본 데이터 타입은 기본 타입과 참조 타입으로 나뉘게 된다. ES5 까지는 기본 타입에 숫자, 문자, Boolean, undifined, null 이 있고 참조 타입에 객체(Object)가 있었다. ES6가 되면서 기본 타입에 Symbol이 추가 되게 되었다.

## 3.1 자바스크립트 기본 타입

---

 자바스크립트는 느슨한 타입 체크 언어이다. 그렇기 때문에 변수를 선언할 때 var라는 키워드를 선언한다.(ES6 에서는 let과 const도 사용한다.) 이렇게 선언된 변수에는 타입과 관계없이 값이 저장될 수 있다. 그렇기 때문에 자바스크립트에서의 타입은 선언시에 결정되는 것이 아니라, 어떤 형태의 데이터를 저장하냐에 따라 달라질 수 있다. 

### 3.1.1 숫자

---

 자바스크립트는 모든 숫자를 64비트 부동 소수점 형태로 저장한다. C언어에서의 double과 비슷하다. 그렇기 때문에 자바스크립트에서는 나눗셈 연산을 할 때 주의해야 한다.

### 3.1.2 문자열

---

- 자바스크립트의 문자열은 C와는 다르게 '와 " 모두 사용할 수 있다. C에서처럼 하나의 문자만을 따로 나타내는 데이터타입이 존재하지 않는다. 자바스크립트의 문자열에서 중요한점은 한 번 정의된 문자열은 변하지 않는다는 것이다. 즉, 자바스크립트에서는 한번 생성된 문자열은 읽기만 가능하지 수정은 불가능하다.

    var str='test';
    console.log(str[0],str[1],str[2],str[3]) //출력값 test
    
    str[0]='T';
    console.lg(str) //출력값 test -> 대문자로 변하지 않았음

- 자바스크립트의 문자열은 ' 와 " 외에도 String 전역객체를 사용하여 생성할 수도 있다. String(thing)
- ECMA 2015 이 후 문자열은 소위 템플리트 리터럴이 될 수 있다.

        var a="태경"
        
        var b=`안녕하세요 저는 ${a}입니다.`
        
        console.log(b); // 안녕하세요 저는 태경입니다.

- 긴 문자열을 표현할 때는 역슬래시를 사용할 수 있다.

        let longString = "여러 줄에 걸쳐 작성해야 할 정도로 \
        긴 문자열인데 왜 한 줄에 다 적으면 안되냐면 \
        코드를 읽기 힘들어지니까요.";

- 문자열 원형과 String 객체에는 차이가 있다.
    - 서로의 타입이 다르다

        var s_prim = "foo";
        var s_obj = new String(s_prim);
        
        console.log(typeof s_prim); // Logs "string"
        console.log(typeof s_obj);  // Logs "object"

    - eval() 을 사용할 때의 결과가 다르다.

        var s1 = '2 + 2';               // creates a string primitive
        var s2 = new String('2 + 2');   // creates a String object
        console.log(eval(s1));          // returns the number 4
        console.log(eval(s2));          // returns the string "2 + 2"

### 3.1.3 불린값

---

 자바스크립트에는 true와 false를 나타내는 불린 타입을 가진다.

[자바스크립트 자료형별 true false](https://www.notion.so/913ac618cf134427b9d42c52c2c86c87)

### 3.1.4 null 과 undefined

---

  이 두 타입은 모두 '값이 비어있음' 을 나타낸다. 자바 스크립트에서 값이 할당 되지 않은 변수는 undifined 타입이며, 자체 값 또한 undifined 이다. 이 때 주의 할 점은 null의 typeof 결과는 object라는 것이다. 그렇기 때문에 자바스크립트에서는 null 을 확인 할 때 undifined 가아닌 ===을 통해 해주어야 한다.

    var nullvar= null;
    
    console.log(typeof nullvar) // false
    console.log(nullvar===null) // true

## 3.2 자바스크립트 참조 타입(객체 타입)

---

 자바스크립트 객체는 단순히 '이름 (key): 값(value)' 의 형태로 프로퍼티들을 저장하는 컨테이너다. (다른 분야의 해시라는 자료구조와 비슷한 형태를 가진다.) 참조 타입 객체는 여러 개의 프로퍼티들을 포함할 수 있으며, 이러한 객체의 프로퍼티는 기본 타입의 값을 포함하거나, 다른 객체를 가리킬 수도 있다. 

### 3.2.1 객체 생성

---

 자바스크립트의 객체 생성은 다른 언어와는 다르다. 자바스크립트의 객체 생성방법에는 크게 세 가지가 있다.

1. 기본 제공 Object() 객체 생성자 함수를 이용하는 방법
2. 객체 리터러를 이용하는 방법
3. 생성자 함수를 이용하는 방법

### 3.2.1.1 Object() 생성자 함수 이용

---

 Object 생성자 함수를 이용하여 빈 객체를 생성한 후, 프로퍼티를 추가한다.

    var foo=new Object();
    
    foo.name='foo';
    foo.age=30;
    foo.gender='male';
    
    console.log(typeof foo); //object
    console.log(foo); //{name: "foo", age: 30, gender: "male"}

### 3.2.1.2 객체 리터럴 방식 이용

---

 객체 리터럴이란 객체를 생성하는 표기법을 의미한다. 이 경우 중괄호를 이용하여 객체를 생성한다. 중괄호 안에 "이름":"값" 형태로 표기한다. 위의 예제를 리터럴을 이용하여 해보면 아래와 같다.

    var foo={
    	name:'foo',
    	age:30,
    	gender:'male'
    }
    
    console.log(typeof foo); //object
    console.log(foo); //{name: "foo", age: 30, gender: "male"}

### 3.2.1.3 생성자 함수 이용

---

 → 이 경우는 4장에서 다룬다.

### 3.2.2 객에 프로퍼티 읽기/쓰기/생신

---

객체 프로퍼티에 접근하는 방법은 두가지이다.

1. 대괄호([]) 표기법
2. 마침표(.) 표기법

    let foo={
      name:'foo',
      major:'computer science'
    };
    
    console.log(foo.name); //foo
    console.log(foo['name']); //foo
    console.log(foo.nickName); //undifined
    
    foo.major='electronic engineer';
    console.log(foo.major); // electronic engineer
    console.log(foo['major']); // electronic engineer
    
    foo.age=30;
    console.log(foo.age) // 30
    
    foo['full-name']='foo bar';
    console.log(foo['full-name']); //foo bar
    console.log(foo.full-name); // NaN
    console.log(foo.full); // undefined
    console.log(name); // undefined

- 마침표 표기법에서는 foo['name']과 같이 '을 빼먹으면 안된다.(단, 숫자가 사용될 경우 자바 스크립트 엔진이 해당 숫자를 자동으로 문자열 형태로 바꾸어 준다.)
- 객체의 프로퍼티는 동적으로 생성될 수 있다.
- 객체의 이름에 "-"가 들어 있을 경우 대괄호 표긱법만을 사용하여야 한다. 마침표 표기법을 사용할 경우 foo.full-name의 뺄셈으로 처리되어 NaN이 출력된다.(undefined - undefined의 연산 결과가 NaN 이기 때문이다.)

### 3.2.3 for in 문과 객체 프로퍼티 출력

---

for in 문을 사용하면 객체에 포함된 모든 프로퍼티에 대해 루프를 수행할 수 있다. 

    let foo={
      name:'foo',
      major:'computer science'
    };
    
    foo.major='electronic engineer';
    foo.age=30;
    
    for (prop in foo){
      console.log(prop + " : " + foo[prop])
    }
    
    [출력 결과]
    name : foo
    main.js:24 major : electronic engineer
    main.js:24 age : 30
    main.js:24 full-name : foo bar

### 3.2.4 객체 프로퍼티 삭제

---

객체 프로퍼티는 delete를 이용하여 즉시 삭제 할 수 있다. 단 객체의 프로퍼티를 삭제하는 것이지, 객체 자체를 삭제하는 것이 아니다.

## 3.3 참조 타입의 특성

---

 자바스크립트에서 기본 타입을 제외한 모든 타입이 참조 타입이다. 그렇기 때문에 배열이나 함수 또한 객체로 취급된다. 이러한 타입은 참조타입이라고 불리는데 그 이유는 객체의 모든 연산이 실제 값이 아닌 참조값으로 처리되기 때문이다.

    let objA={
      val:40
    };
    
    let objB=objA;
    
    console.log(objA.val);
    console.log(objB.val);
    
    objB.val=50;
    
    console.log(objA.val);
    console.log(objB.val);
    
    [출력 결과]
    40
    40
    50
    50
    

 위 예제처럼 변수는 실제로 객체를 참조하는 값을 저장할 뿐 실제 객체를 나타내지 않는다. 

### 3.3.1 객체 비교

---

 동등 연산자를 사용하여 두 객체를 비교할 때도 객체의 참조값을 비교한다.

    let a=100;
    let b=100;
    
    let objA={
      value:100
    };
    let objB={
      value:100
    };
    let objC=objB;
    
    console.log(a == b);
    console.log(objA == objB);
    console.log(objB == objC);
    
    [출력값]
    true
    false
    true

- 기본 타입의 경우 동등 연산자를 이용하여 비교할 때 값을 비교한다.
- 참조 타입의 경우 동등 연산자를 이용하여 비교할 때 참조 값을 비교한다.

### 3.3.2 참조에 의한 호출 방식

---

- 기본 타입의 경우 Call by value 방식 → 함수를 호출할 때 인자로 기본 타입의 값을 넘길 경우, 매개변수로 복사된 값이 전달된다.
- 참조 타입의 경우 Call by reference 방식 → 함수를 호출할 때 인자로 참조 타입인 객체를 전달할 경우, 인자로 넘긴 객체의 참조값이 그대로 함수 내부로 전달된다.

    let a=100;
    let objA={value:100};
    
    function changeArg(num,obj){
      num=200;
      obj.value=200;
    
      obj={value:300};
    
      console.log(num);
      console.log(obj);
    }
    
    changeArg(a,objA);
    
    console.log(a);
    console.log(objA);

- 위 예제를 볼 경우 함수 내부에서 객체의 프로퍼티를 바꿀 경우 함수 호출 이후에도 그 값은 변경이 되는 것을 확인 할 수 있다. (객체 자체를 변경할 수는 없다.)

## 3.4 프로토타입

---

 자바스크립트의 모든 객체는 자신의 부모 역할을 하는 객체와 연결되어 있다. 이러한 부모 객체를 프로토타입 객체(프로토 타입) 이라고 한다. 프로토 타입 객체를 확인하는 방법은 객체의 _proto_ 프러퍼티를 확인하는 것이다.

 ECMAScript 명세에 있는 [[Prototype]] 이라는 숨겨진 프로퍼티가 이 _proto_ 를 의미한다. 객체 리터럴 방식으로 생성된 객체의 경우 Object.prototype 객체가 프로토타입 객체가 되게 된다. 객체는 자신의 프로토타입 객체에 있는 다양한 메서드를 마치 자신의 프로퍼티인 것처럼 상속받아 사용할 수 있다.

## 3.5 배열

---

### 3.5.1 배열 리터럴

---

  대괄호를 이용한 배열 생성 방법이다. 배열은 프로퍼티의 이름이 아니라 배열 내 위치 인덱스 값을 통하여 배열 내의 값에 접근한다.

    let colorArr=['orange','red','blue']

 

### 3.5.2 배열의 요소 생성

---

객체와 마찬가지로 배열도 동적으로 요소를 추가할 수 있다. 다른 언어의 배열과 다른 점은 순차적이 아니라 아무 인덱스에나 값을 동적으로 추가 할 수 있다. 이 때 자바스크립트 배열의 크기는 현재 배열의 인덱스 중 가장 큰 값을 기준으로 정해진다. 값이 할당되지 않은 인덱스 요소는 undefined를 기본으로 한다.

### 3.5.3 배열의 length 프로퍼티

---

자바스크립트의 모든 배열은 length 프로퍼티가 있다. length 프로퍼니는 배열 내에 가장 큰 인덱스에 1을 더한 값이다. 실제 메모리도 length크기처럼 할당되지는 않는다. 배열의 length는 코드를 통해 명시적으로 값을 변경할 수도 있다.

### 3.5.3.1 배열 표준 메서드와 length 프로퍼티

---

 자바스크립트 배열에는 다양한 표준 메서드들이 존재하는데, 이러한 메서드들은 length 프로퍼티 기반으로 동작하고 있다. 아래 push의 예를 보자.

    let arr=['zero','one','two','three'];
    arr.push("new");
    console.log(arr);
    
    arr.length=10;
    arr.push("newTwo");
    
    console.log(arr);
    
    [출력]
    ["zero", "one", "two", "three", "new"]
    ["zero", "one", "two", "three", "new", empty × 5, "newTwo"]

### 3.5.4 배열과 객체

---

 배열은 객체이지만, 배열은 일반 객체와는 차이가 있다.

- 배열과 객체는 모두 객체이다
- 객체에는 length 프로퍼티가 존재하지 않는다.
- 리터럴 방식으로 객체를 생성할 경우 Object.prototype 객체가 프로토타입이다. 반면에 배열의 경우 Array.prototpye 객체가 부모 객체인 프로토타입이 된다.

### 3.5.5 배열의 프로퍼티 동적 생성

---

배열도 자바스크립트 객체이기 때문에, 인덱스가 숫자인 배열원소 이외에도 객체처럼 동적으로 프로퍼티를 추가할 수 있다. 다만 배열의 length프로퍼티는 배열 원소의 가장 큰 인덱스가 변했을 경우만 변경된다.

### 3.5.6 배열의 프로퍼티 열거

---

 배열의 경우에도 for in 문을 사용해서 배열 내의 모든 프로퍼티를 열거할 수 있다. 하지만 인덱스에 들어있는 값 외에 다른 값들이 출력될 수 있으므로, 배열의 요소만 출력하고 싶다면 for 문을 사용해야 한다.

    let arr=[0,1,2];
    console.log(arr.length);
    
    arr.color='red';
    arr.name='array';
    console.log(arr.length);
    
    arr[3]=3;
    console.log(arr.length);
    
    for (let prop in arr){
      console.log(prop,arr[prop]);
    }
    console.log("============================");
    for (let i=0;i<arr.length;i++){
      console.log(i,arr[i]);
    }
    
    [출력결과]
    3
    3
    4
    0 0
    1 1
    2 2 
    3 3
    color red
    name array
    ============================
    0 0
    1 1 
    2 2
    3 3

### 3.5.7 배열 요소 삭제

---

- 배열도 객체이므로 프로퍼티를 삭제하는데 delete연산자를 사용할 수 있다. 단, delete로 배열의 요소를 삭제할 경우 length는 변하지 않는다. delete 연산자는 단지 해당 요소의 값을 undefined로 설정할 뿐이다.
- 배열의 요소를 완전히 삭제할 경우 splice() 배열 메서드를 사용한다.
    - splice(start,deleteCount,item...)
        - start : 배열에서 시작위치
        - deleteCount : 삭제할 요소의 수
        - item : 삭제할 위치에 추가할 요소

    let arr=[0,1,2,3];
    
    arr.splice(2,1);
    console.log(arr)
    console.log(arr.length)
    
    [출력 결과]
    [0,1,3]
    3

### 3.5.8 Array() 생성자 함수

---

 배열의 경우도 배열 리터럴 외에 Array() 생성자 함수로 생성할 수 있다.(사실 리터럴이 생성자 함수로 생성하는 과정을 단순화 시킨 것이다.) 

주의 사항
- 호출된 인자가 1개이고, 숫자 일 경우 : 인자를 length로 갖는 빈 배열
- 그 외의 경우 : 호출된 인자를 요소로 갖는 배열 생성

### 3.5.9 유사 배열 객체

---

 앞에서 말했듯이 배열의 length 프로퍼티는 배열의 동작에 있어서 중요하다. 자바스크립트에서는 일반 객체에 length프로퍼티를 가진 객체를 유사 배열 객체라고 부른다. 이러한 유사 배열 객체의 특징은 객체임에도 불구하고, 자바스크립트 표준 배열 메서드를 사용하는게 가능하다는 것이다.

    let att=['bar'];
    att.length=1;
    att.push('baz');
    console.log(att);
    
    [출력 결과]
    ["bar", "baz"]
    obj.push is not a function

 하지만 위의 결과를 보게 되면 유사 배열 객체 obj는 바로 push() 메서드를 호출할 경우 에러가 발생한다. 이 경우 사용하는 것이 apply() 메서드이다(4장에서 더 자세히 배운다.)

    let att=['bar'];
    let obj={
      name:'foo',
      length:1
    };
    att.length=1;
    att.push('baz');
    console.log(att);
    
    Array.prototype.push.apply(obj,['baz']);
    console.log(obj);
    
    [출력 결과]
    ["bar", "baz"]
    {1: "baz", name: "foo", length: 2}

## 3.6 기본 타입과 표준 메서드

---

자바스크립트는 각 타입별로 호출 가능한 표준 메서드를 정의학고 있다. 이 경우 객체로 변환된 다음 각 표준메서드를 호출하고 그 후 다시 기본값으로 복귀한다.

## 3.7 연산자

---

- + 연산자 → 숫자일 경우 더하기, 문자일 경우 문자열 연결 연산이 이루어진다
- typeof 연산자 → 타입을 문자열 형태로 리턴한다
- == 와 === → ==의 경우 값만 일치하면 되지만 ===의 경우 타입도 일치하여야 한다.
- !! → 피연산자를 불린값으로 변환한다.