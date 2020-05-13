---
layout:     post
title:      Summary of Studying Redux
date:       2020-05-12 18:00:00
summary:    This is a summary of Studying Redux with some blog and books.
categories: JavaScript
---

# Redux 개념 미리 정리하기
1. 액션
   - 상태에 어떤 변화가 필요할 떄 발생 하는 것
```
    {
        type : 'ADD_TODO',
        data : {
            id :1 ,
        }
    }
```

2. 액션 생성 함수
    - 액션 객체를 만들어 주는 함수
```
    const changeInput=text=>({
        type : 'CHANGE_INPUT',
        text
    })
```

3. 리듀서 
   - 변화를 일으키는 함수, 액션 발생시 리듀서가 새로운 상태를 반환해줌
```
    const initialState = {
        counter : 1
    }
    function reducer(state = initialState ,action){
        switch(action.type){
            case INCREMENT :
                return {
                    counter : state.counter + 1
                }
            default :
                return state;
        }
    }
```

4. 스토어
   - 스토어 안에는 현재 어플리케이션 상태와 리듀서가 들어 있다  

5. 디스패치
   - 스토어의 내장함수로 액션을 발생시키는 것, 이 함수가 호출시 스토어는 리듀서를 통하여 새로운 상태를 만들어 준다.

<center><img src="https://kevinorigin.al/static/reduxflow2-b85ebe28cfe109ecb52ba1b069e1ff14-fb8a0.png"></center>

   

# 리덕스의 세 가지 규칙
1. 단일 스토어
   1. 하나의 어플리케이션에는 하나의 스토어
   2. 여러개를 사용할 수 있지만, 상태 관리가 복잡해지므로 권장하지 않는다
2. 읽기 전용 상태
   1. 상태를 업데이트 할 때 기존의 객체는 건드리지 않고 새로운 객체를 생성해 주어야 한다.
   2. 내부 데이터 변경을 얕은 비교를 통해서 검사하기 때문이다 (성능의 향상을 꾀할 수 있다.)
3. 리듀서는 순수 함수여야 한다.
   1. 리듀서 함수는 이전 상태와 액션 객체를 파라미터로 받음
   2. 파라미터 이외의 값에는 의존 하지 않음
   3. 변화를 준 새로운 객체 상태를 만들어 반환
   4. 똑같은 파라미터에 대하여 언제느 똑같은 결과 값을 반환해야 한다.
> 리듀 서 함수 내부에서 랜덤 값을 만들거나, DATE를 통하여 현재 시간을 가져오거나, 네트워크 요청을 하거나 하면 파라미터가 같아도 다른 결과를 만들 수 있기 떄문에 사용하면 안된다.

> 네트워크 요청의 경우 미들웨어를 통하여 관리한다.


# FLUX 아키텍쳐란 무엇인가
## 기존 MVC 구조에 대한 이해
---
&nbsp; 기존의 MVC 패턴에서는 데이터가 **양방향**으로 전송되기 때문에 그 구조가 상당히 복잡해 질 수 밖에 없다. model에 있는 데이터와 로직을 통해 컨트롤러가 View의 상태를 변화 시키고, view에서의 사용자 상호 작용을 통하여 model의 데이터를 바꾸게 된다. 


<center><img src="https://i.stack.imgur.com/E5ynk.png"></center>

&nbsp; 이 경우 애플리케이션의 크기가 커질 경우 복잡도가 중가하게 되고, 특히나 컨트롤러가 비대화되는 문제가 생길 수 있다. 페이스북 개발자들에 의하면 *"하나의 기능을 추가할 때마다그 complexity 는 expotential(지수함수 적으로, 기하 급수적으로 )하게 증가를 한다고합 니다."* 특히나 페이스북과 같이 USER와의 상호작용이 많은 앱의 경우 앱의 여러 다른 곳에서 view가 update되어야 하기 때문에 어려움이 있었다. 이러한 배경에서 등장한 아키텍쳐가 flux 아키텍쳐 이다.

## MVC와 FLUX의 차이점
---
&nbsp; Flux아키 텍쳐의 MVC와의 가장 큰 다른 점은 Flux는 **단방향 데이터** 흐름이라는 점이다. 

**Action** 이란 앱 내의 변화

**Dispatcher** 액션을 받아 스토어에 변화를 일으킨다

**Store** 앱 내의 state의 저장소


<center><img src="https://kevinorigin.al/static/flux%20flow1-f688bbf71e547d3f67f90939b02dfa6d-fb8a0.png"></center>

&nbsp; 액션이 생길 때마다 앱 내의 cycle이 돌게 되고 이에 따라 React는 re-render를 진행한다. 이러한 re-render는 엄청난 퍼포먼스 저하를 일으키게 된다. 이러한 re-render의 퍼포먼스 저하를 해결하기 위해 나온것이 virtual-dom이다.


# 리덕스를 사용하는 패턴
&nbsp; 리덕스를 사용할 떄 가장 많이 사용하는 패턴은 프리젠테이셔널 컴포턴트와 컨테이너 컴포넌트를 분리하는 것이다.

- 프리젠테이셔널 컴포넌트 : 화면에 UI를 보여주는 컴포넌트
- 컨테이너 컴포넌트 :  리덕스와 연동되어 있는 컴포넌트 
<center><img src="https://user-images.githubusercontent.com/22091610/81603495-65196100-9409-11ea-851b-ee564a59ce5c.png"></center>


# 리덕스 관련 코드 작성 방법
- 리덕스를 사용할 때는 액션, 액션 생성 함수, 리듀서 코드의 작성이 필요한데 이 코드들을 서로 다른 파일에 작성하는 방법과, 기능별로 묶어서 파일 하나에 작성하는 방법이 있다.
  
<center><img src="https://user-images.githubusercontent.com/22091610/81594226-86735080-93fb-11ea-9468-1c388a628871.jpg"></center>

- 왼쪽이 세개의 디렉토리를 만들고 그 안에 기능별로 파일을 하나씩 만드는 방식, 리덕스 공식 문서에도 사용되는 가장 기본적인 방식이다.
- 오른쪽이 하나에 몰아서 작성하는 Ducks 패턴이다. 이 하나의 파일을 *모듈* 이라고 한다.

# 리액트에서 API 서버에 요청 할경우
&nbsp; 리덕스를 사용할 경우 이러한 비동기 작업을 관리해야 할 때 미들웨어를 사용하여야 한다. 미들웨어는 액션을 디스패치 했을 때 리듀서에서 이를 처리하기에 앞서 사전에 지정된 작업을 실햅한다. 
- redux - thunk
  - 비동기 작업을 처리할 때 가장 많이 사용하는 미들웨어. 함수 형태의 액션을 디스패치한다.
- redux - saga
  - 특정 액션이 디스패치되었을 때 정해진 로직에 따라 다른 액션을 디스패치시키는 규칙을 작성하여 비동기 처리 작업 가능

# 참고문헌
    - https://kevinorigin.al/posts/redux-01/2017-05-09-redux1/
    - 리액트를 다루는 기술  
