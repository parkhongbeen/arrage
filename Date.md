# Date

Date 객체는 날짜와 시간(년, 월, 일, 시, 분, 초, 밀리초(천분의 1초(millisecond, ms)))을 위한 메소드를 제공하는 빌트인 객체이면서 생성자 함수이다.

Date 생성자 함수로 생성한 Date 객체는 내부적으로 숫자값을 갖는다. 이 값은 1970년 1월 1일 00:00(UTC)을 기점으로 현재 시간까지의 밀리초를 나타낸다.

UTC는 GMT로 불리기도 하는데 UTC와 GMT는 초의 소숫점 단위에서만 차이가 나기 때문에 일상에서는 혼용되어 사용된다.기술적인 표기에서는 UTC가 사용된다.



### newDate(year,month)

인수로 년, 월, 일, 시, 분, 초, 밀리초를 의미하는 숫자를 전달하면 지정된 날짜와 시간을 가지는 인스턴스를 반환한다. 이때 년, 월은 반드시 지정하여야 한다. 지정하지 않은 옵션 정보는 0 또는 1으로 초기화된다.

| 인수        | 내용                                                         |
| :---------- | :----------------------------------------------------------- |
| year        | 1900년 이후의 년                                             |
| month       | 월을 나타내는 **0 ~ 11**까지의 정수 (주의: 0부터 시작, 0 = 1월) |
| day         | 일을 나타내는 1 ~ 31까지의 정수                              |
| hour        | 시를 나타내는 0 ~ 23까지의 정수                              |
| minute      | 분을 나타내는 0 ~ 59까지의 정수                              |
| second      | 초를 나타내는 0 ~ 59까지의 정수                              |
| millisecond | 밀리초를 나타내는 0 ~ 999까지의 정수                         |

년,월을 지정하지 않은 경우 1979년 1월1일 00:00(UTC)를 가지는 인스턴스를 반환한다.

```
// 월을 나타내는 4는 5월을 의미한다.
// 2019/5/1/00:00:00:00
let date = new Date(2019, 4);
console.log(date); // Wed May 01 2019 00:00:00 GMT+0900 (한국 표준시)

// 월을 나타내는 4는 5월을 의미한다.
// 2019/5/16/17:24:30:00
date = new Date(2019, 4, 16, 17, 24, 30, 0);
console.log(date); // Thu May 16 2019 17:24:30 GMT+0900 (한국 표준시)

// 가독성이 훨씬 좋다.
date = new Date('2019/5/16/17:24:30:10');
console.log(date); // Thu May 16 2019 17:24:30 GMT+0900 (한국 표준시)
```

### Date 생성자 함수를 new연산자없이 호출

```
let date = Date();
console.log(typeof date, date); // string Thu May 16 2019 17:33:03 GMT+0900 (한국 표준시)
```
