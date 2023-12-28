# react-intersection-observer

### Intersection Observer API 란?
어떤 Element가 화면(viewport)에 노출되었는지를 감지할 수 있는 API이다. 무한 스크롤(Infinite Scroll)을 만들수 있다.

### 무한 스크롤을 구현하는 이유

- Scroll Event를 사용해서 구현할 때 사용하는 debounce & throttle 을 사용하지 않아도 됩니다..
- Scroll Event를 사용해서 구현할 때 구하는 offsetTop 값을 구할 때 는 정확한 값을 구하기 위해서 매번 layout을 새로 그리는데 이를 Reflow라 합니다. Intersection Observer를 사용하면 Reflow를 하지 않습니다.
- Scroll Event를 사용하는것 보다 비교적 이해 및 사용하기가 쉽습니다.

### Intersection Observer - Options

```
let observer = new IntersectionObserver(callback, options);
```

Intersection Observer를 생성할 때는 옵션을 설정할 수 있습니다.
옵션에는 root, rootMargin, threshold가 있습니다.

![](https://velog.velcdn.com/images/bunny/post/819b328a-2298-40f5-b4d1-4f71d52bfbd0/image.png)


### root
- 이 옵션에 정의된 Element를 기준으로 Target Element가 노출되었는지 노출 되지 않았는지를 판단합니다. </br>
- 기본값은 Browser Viewport이며, root 값이 null 또는 지정되지 않았을 때 기본값으로 설정됩니다.</br>
### rootMargin
- root에 정의된 Element가 가진 마진값을 의미합니다. 사용법은 CSS의 margin 속성과 매우 유사합니다. </br>
- threshold를 계산할 때 rootMargin 만큼 더 계산합니다.</br>
### threshold
- Target Element가 root에 정의된 Element에 얼만큼 노출되었을 때 Callback함수를 실행시킬지 정의하는 옵션입니다. </br>
- number 또는 number[]로 정의할 수 있습니다.</br>
- number 로 정의할 경우, Target Element 의 노출 비율에 따라 Callback Function을 한번 호출할 수 있지만, number[] 로 정의할 경우, 각각의 비율로 노출될 때마다 Callback Function을 호출합니다.</br>

# debounce & throttle
스로틀(Throttle)과 디바운스(Debounce)란 무엇일까?

이 두 가지 방법 모두 DOM 이벤트를 기반으로 실행하는 **자바스크립트를 성능상의 이유**로 **JS의 양적인 측면, 즉 이벤트(event)를 제어(제한)하는 방법**입니다.
Throttle 과 Debounce 는 이벤트 핸들러가 많은 연산(예 : 무거운 계산 및 기타 DOM 조작)을 수행(이벤트 핸들러의 과도한 횟수가 발생하는 것)하는 경우에 대해 제약을 걸어 시간이 지남에 따라 함수를 몇 번이나 실행 할지를 제어하는 유사한 기술이지만 서로 다릅니다.

사용 예는 아래와 같습니다.
- 사용자가 창 크기 조정을 멈출 때까지 기다렸다가 resizing event 사용하기 위해
- 사용자가 키보드 입력을 중지(예: 검색창) 할 때까지 ajax 이벤트를 발생시키지 않기 위해
- 페이지의 스크롤 위치를 측정하고 최대 50ms 마다 응답하기를 바랄 경우에
- 앱에서 요소를 드래그 할 때 좋은 성능을 보장하기 위해

## Debounce    
Debounce 는 이벤트를 그룹화하여 특정시간이 지난 후 이벤트를 한번 발생하도록 하는 기술입니다. 즉, 순차적 호출을 하나의 그룹으로 "그룹화"할 수 있습니다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F994614365C17654319"/>

## Throttle

Throttle은 이벤트를 일정한 주기마다 발생하도록 하는 기술입니다. 예를 들어 Throttle의 설정시간으로 1ms를 주게되면 해당 이벤트는 1ms 동안 최대 한번만 발생하게 됩니다. 

특성 자체가 실행 횟수에 제한을 거는 것이기 때문에 일반적으로 성능 문제 때문에 많이 사용합니다. </br>
스크롤을 올리거나 내릴 때 scroll 이벤트 핸들러 경우에 매우 많이 발생합니다. </br>
scroll 이벤트가 발생할 때 뭔가 복잡한 작업을 하도록 설정했다면 매우 빈번하게 실행되기 때문에 큰 버퍼링이 걸릴 지도 모를 것입니다. </br>
그럴 때 쓰로틀링을 사용할 수 있스빈다. 몇 초에 한 번, 또는 몇 밀리초에 한 번씩만 실행되게 제한을 두는 것입니다. </br>
    
## Debounce 와 Throttle 차이점
디바운싱과 스로틀의 가장 큰 차이점은 스로틀은 적어도 X 밀리 초마다 정기적으로 기능 실행을 보장한다는 것입니다. </br>
Debounce 는 아무리 많은 이벤트가 발생해도 모두 무시하고 특정 시간사이에 어떤 이벤트도 발생하지 않았을 때 딱 한번만 마지막 이벤트를 발생시키는 기법입니다.  </br>
따라서 5ms가 지나기전에 계속 이벤트가 발생할 경우 콜백에 반응하는 이벤트는 발생하지 않고 계속 무시됩니다. </br>



# Reflow

# react-query 

```shell
npm i @tanstack/react-query @tanstack/react-query-devtools
```

https://tanstack.com/query/v5/docs/react/guides/queries

revalidatePath('/home) > home 폴더에 있는 캐시 전체 삭제
revalidateTag
