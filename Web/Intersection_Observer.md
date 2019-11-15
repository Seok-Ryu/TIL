# 개요
수많은 스크롤 이벤트가 발생하며 해당 이벤트에서 무엇인가 처리하려할 때
원하는 타이밍을 체크하는 로직을 보통 넣게 됨.

getBoundingClientRect() 를 통해서 원하는 뷰포트에 진입했는지 확인을 할 수 있는데
해당 함수는 reflow 를 발생시킴

intersection observer 는 비동기적으로 실행되기 때문에 메인 스레드에 영향을 주지 않으면서 변경 사항을 관찰할 수 있음

## 예제 코드
```javascript
// IntersectionObserver 를 등록한다.
const io = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    // 관찰 대상이 viewport 안에 들어온 경우 'tada' 클래스를 추가
    if (entry.intersectionRatio > 0) {
      entry.target.classList.add('tada');
    }
    // 그 외의 경우 'tada' 클래스 제거
    else {
      entry.target.classList.remove('tada');
    }
  })
})

// 관찰할 대상을 선언하고, 해당 속성을 관찰시킨다.
const boxElList = document.querySelectorAll('.box');
boxElList.forEach((el) => {
  io.observe(el);
})
```


### 참고
* http://blog.hyeyoonjung.com/2019/01/09/intersectionobserver-tutorial/?utm_source=gaerae.com&utm_campaign=%EA%B0%9C%EB%B0%9C%EC%9E%90%EC%8A%A4%EB%9F%BD%EB%8B%A4&utm_medium=social&fbclid=IwAR2fdfrX2LqiZx0lPoInLnaRvfpmSsU7biDMggTboEjg0rkipEOM1ieoMHE
