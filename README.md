# react-intersection-observer

## Intersection Observer API 란?
어떤 Element가 화면(viewport)에 노출되었는지를 감지할 수 있는 API이며 이런 유용한 점을 이용해서 우리들은 무한 스크롤(Infinite Scroll)을 만들어볼 수 있습니다.

## 무한 스크롤을 구현하는 이유

- Scroll Event를 사용해서 구현할 때 사용하는 debounce & throttle 을 사용하지 않아도 됩니다..
- Scroll Event를 사용해서 구현할 때 구하는 offsetTop 값을 구할 때 는 정확한 값을 구하기 위해서 매번 layout을 새로 그리는데 이를 Reflow라 합니다. Intersection Observer를 사용하면 Reflow를 하지 않습니다.
- Scroll Event를 사용하는것 보다 비교적 이해및 사용하기가 쉽습니다.

## Intersection Observer Options

간단한 Intersection Observer 생성 예제
```
let observer = new IntersectionObserver(callback, options);
```

Intersection Observer를 생성할 때는 옵션을 설정할 수 있습니다.
옵션에는 root, rootMargin, threshold가 있는데요,

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

