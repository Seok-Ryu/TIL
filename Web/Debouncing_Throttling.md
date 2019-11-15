# 개요
디바운싱과 쓰로틀링은 필요이상으로 과도하게 반복되는 이벤트로 인한 부하를 완충하는 방법이다.

## Debouncing
### 설명
3초의 시간을 설정해두고,
3초 내에는 버튼이 눌려도 폭죽이 발사되지 않도록 조정해두었다.

마구 연타시 폭죽은 발사되지 않고 마지막 버튼을 떼는 순간 3초 뒤 발사된다.

### 대표 케이스
ID 중복검사

## Throttling
### 설명
일단 버튼이 눌리면 3초간 먹통이 된다.
그리고 3초 후에는 다시 폭죽이 발사되도록 초기화가 된다.

이제 버튼을 마구 연타를 해도 3초의 발사 간격을 보장해준다.

### 대표 케이스
스크롤 이벤트시 핸들

## 차이
3초의 시간을 설정해두고, 버튼을 쉼없이 연타한다고 가정해보자.

디바운싱의 경우 버튼을 누르는 동작이 3초내에 계속 반복될 경우,
이벤트는 절대 실행되지 않는다.
마지막 릴리즈 후 3초 후 이벤트가 발생한다.

쓰로틀링의 경우 일단 3초라는 시간이 지나면, 대기가 풀려 다시 이벤트를 처리할 수 있게 된다.
곧, 연속되는 이벤트의 경우 3초 단위로 반드시 실행이 되는 것이다.

## 예제 코드
```javascript
/*
 * 디바운싱 : Interval 내 반복되는 이벤트를 무시함.
 */
const debounce = (f, interval = 30) => {
    let now = null;

    return (...param) => {
        if (now) clearTimeout(now);

        now = setTimeout(() => {
            f(...param);
        }, interval);
    }
}

/*
 * 쓰로틀링 : 연이은 이벤트의 Interval 단위 실행을 보장.
 */
const throttling = (f, interval = 300) => {
    let isPending = false;

    return (...param) => {
        if (!isPending) {
            isPending = !!setTimeout(
                () => {
                    f(...param);
                    isPending = false;
                }, interval);
        }
    }
}

```

### 참고
* https://www.httpvshttps.com/
