# java-lotto

로또 미션 저장소

## 우아한테크코스 코드리뷰

- [온라인 코드 리뷰 과정](https://github.com/woowacourse/woowacourse-docs/blob/master/maincourse/README.md)

---

## 기능 요구 사항

- [x] 구입 금액을 입력받는다.
    - [x] 숫자를 입력받는다.
    - [x] <예외> 숫자 외 다른 문자를 입력한다.
    - [x] <예외> 공백 또는 빈 문자열을 입력한다.
    - [x] <예외> 음수를 입력한다.
- [x] 로또를 구매한다.
    - 로또 1장의 가격은 1000원이다.
    - 1 ~ 45의 숫자를 무작위로 중복 없이 6개 뽑는다.
    - 무작위로 선택된 6개의 숫자를 오름차순으로 정렬한다.
    - [x] <예외> 숫자가 6개가 아니다.
    - [x] <예외> 중복된 숫자가 입력된다.
    - [X] <예외> 숫자가 1 ~ 45 사이가 아니다.
- [x] 로또를 출력한다.
- [x] 당첨 번호를 입력한다.
    - [x] 1 ~ 45 사이의 중복되지 않는 숫자 6개를 ‘,‘ 로 구분하여 적는다. ( 컴마간의 띄어쓰기는 허용한다. )
    - [x] <예외> 입력된 숫자가 6개가 아니다.
    - [x] <예외> 중복된 숫자가 입력된다.
    - [x] <예외> 숫자가 1 ~ 45 사이가 아니다.
    - [x] <예외> 숫자 외 다른 문자를 입력한다.
    - [x] <예외> 공백 또는 빈 문자열을 입력한다.
- [x] 보너스볼을 입력한다.
    - [x] 당첨번호와 중복되지 않은 1 ~ 45 까지의 숫자를 입력한다.
    - [x] <예외> 숫자가 1 ~ 45 사이가 아니다.
    - [x] <예외> 앞서 입력한 당첨번호와 중복된 숫자가 입력된다.
    - [x] <예외> 숫자 외 다른 문자를 입력한다.
    - [x] <예외> 공백 또는 빈 문자열을 입력한다.
- [x] 당첨 통계를 낸다.
    - [x] 구매한 로또번호와 당첨번호, 보너스 볼을 비교한다.
        - 3개가 일치한 경우 5000원이 당첨된다.
        - 4개가 일치한 경우 50000원(5만원)이 당첨된다.
        - 5개가 일치할 경우 1500000원(150만원)이 당첨된다.
        - 5개가 일치하고 보너스 볼이 일치한 경우 30000000원(3000만원)이 당첨된다.
        - 6개가 일치한 경우 2000000000원(20억원)이 당첨된다.
- [x] 당첨 통계를 출력한다.
    - [x] <예외> LottoResults에 null로 생성한다.
- [x] 수익률을 낸다.
    - 수익률은 총 당첨 금액 / 구입 금액 이다.
    - 소숫점 2자리까지 출력하고 나머지는 버린다.
- [x] 수익률을 출력한다.

---

## 1단계 자동 피드백, 수정

- [x] `ResultView`의 `printResults`에서 `(기준이 1이기 때문에 결과적으로 손해라는 의미임)`문구가 꼭 필요한가?
    - 고정적으로 이 문구를 포함하면 1을 넘어도 이 문구가 출력되기 때문에 사용자 입장에서 볼 때 결과가 잘못된건지 이 문구가 잘못된건지 모를 수 있다.
    - 클라이언트 사이드를 고려하는 것도 굉장히 중요한 포인트가 된다!
- [x] VO 패키지에 다른 것들이 섞여 있는 것 같다. VO의 정의가 무엇일까?
    - [x] VO가 아닌 클래스를 VO 패키지 밖으로 이동
    - [x] VO라면 꼭 고려해야 할 것이 무엇이 있을까?
        - VO 클래스들에 equals, hashCode, toString 재정의 추가
        - [자동차 미션을 하며 생각해본 VO](https://github.com/woowacourse/java-racingcar/pull/387#issuecomment-1046303133)
        - 이전 미션을 하면서 처음으로 VO에 대해 생각해본적이 있는데 이때 VO는 불변하고 equals와 hashCode를 재정의해야한다는 것을 보고도 잊어버린것같다.
        - 다시 한번 간단하게 정리
            - 왜 불변해야하는가? 의도하지 않은 수정(사이드 이펙트)을 막기 위해
            - 왜 equals, hashCode를 재정의 해야하는가? 동등성 검사를 위해(하다보면서 알게 되었는데 contains 같은것들도 equals를 재정의하지 않으면 제대로 동작하지 않음)
            - 왜 validate를 해야하는가? VO가 가진 값을 VO 내부에서 검증하여 응집도가 높아진다.
- [x] 500원을 입력하면 수익률이 NaN이 나오는데 어떻게 해결할 수 있을까요?
    - 이 문제를 해결하기 위한 방법은 세 가지정도 있을 것 같다.
        - 1000원 미만의 금액이 입력되면 예외 발생
        - 1000원 미만의 금액이 입력되면 구매한 로또의 수가 0이므로 당첨번호를 입력받지 않고 종료/예외 발생
        - 수익률을 계산할 때 오류가 발생하지 않도록 수정(기존엔 0으로 나누어 발생한 문제)
    - 로또를 사지 못하는 상황에서 생각할 것들
        - 돈이 부족하여 로또를 사지 못하면 (예외 발생 <-> 0개 구매 후 진행)
        - 로또를 0개 가지고 있을 때 (당첨 번호 입력 <-> 미입력)
        - 로또를 0개 가지고 있을 때 (당첨 통계 출력 <-> 미출력)
    - 결국은 돈이 부족하여도 0개를 구매한 후 당첨 번호와 통계는 입/출력하지 않고 종료하도록 수정하였다.
    - 돈이 부족한 것은 입력에서 금액을 음수/문자로 입력하는 등 예외를 발생시킬 상황은 아니라고 생각하게 되었고, 로또의 수가 0개라면 당첨이 될 수 없기 때문에 당첨 번호를 입력받거나 결과를 출력하지 않았다.
- [x] `Lottos`에서 `purchase()`의 과정이 자연스러울까?
    - `Lottos`를 만들고 그곳에서 구매를 하는 것 vs 구매를 하여 그것으로 `Lottos`를 만드는 것 무엇이 자연스러울까?
    - 기존 Lottos의 `purchase()`는 Lottos에 새로운 Lotto를 추가하는 방식이다. 지금 다시 생각해보니 이것은 setter나 add와 같이 Lottos의 상태를 변경하게 되어 불변해야하는
      조건을 만족하지 않는 것 같다.
    - 그래서 Lottos의 `purchase()`를 사용하는 LottoGame에서 `List<Lotto>`를 만들고 이것을 이용하여 Lottos를 만드는 것이 더 적절한 것 같다.
    - 수정 하면서 Lottos가 가지던 로또의 가격 상수를 LottoGame이 가지게 되었다. 이것도 Lottos가 아닌 LottoGame이 가지는 것이 더 자연스러운 것 같다.
        - LottoResults의 수익률 계산을 하는 코드에서 로또의 가격을 하드코딩했다. 이 코드를 LottoGame이 가진 로또 가격을 주어 수정했다.
- [x] `LottoGenerator`에서 사용하는 상수는 다른 클래스가 가져야 할 상수가 아닐까?
    - 이미 더 적절한 곳에 상수로 정의되어있지만 private이기 때문에 사용하지 못했었다. 이것을 사용하기위해 getter를 사용할까 생각했었는데 Integer.MAX_VALUE처럼 public 상수를
      사용하도록 수정했다.
- [x] `WinningNumber`의 `List<LottoNumber>`는 이미 있는 일급 컬렉션을 사용해보면 어떨까?
    - `WinningNumber`의 `validateLottoNumbersDuplication()`은 `Lotto`에서 체크하고 있는 validate와 다른가?
    - 완전 같은 기능이다. `List<LottoNumber>`를 Lotto 일급 컬렉션을 사용하면 WinningNumber가 하던 일부 검증을 Lotto가 하게된다.
- [x] `LottoPrize`에서 `checkMatches`의 조건 분기를 합칠 수 있지 않을까?
- [x] LottoGame의 `purchase()`를 테스트하기위해 LottoGenerator를 인터페이스 분리, 전략 패턴 적용
- [x] 테스트의 핵심 역할 중 하나는 프로덕션 코드에 대한 명세(문서)라는 것을 고려하며 전체적으로 테스트를 다시 확인해보자!
    - 테스트를 작성할 때 명세는 추상적인 표현보다 구체적인 문장으로 표현하는 게 좋다.
    - 테스트를 보면 해당 코드의 동작, 기능 들을 알 수 있어야 한다.
    - 명세에 맞는 테스트가 제대로 되는지도 확인해보면 좋을 것 같다.
- [x] `LottosTest`의 `confirmWinnings_test`와 같은 방식보다 좋은 테스트 방식이 있을까?
    - private 메서드가 너무 과하게 생기는 것 같다.
    - 전략 패턴으로 인터페이스를 분리하여 로또 번호가 (1,2,3,4,5,6)으로 고정인 CustomLottoGenerator를 만들어 테스트한다.
- getter를 이용한 테스트
    - getter는 데이터가 필요한 시점에 사용할 수밖에 없기 때문에 테스트에서도 getter를 사용한다.
    - `LottosTest`의 경우도 내부의 데이터가 잘 생성되었는지 검증하려면 어쩔 수 없이 사용할 것 같다.
    - 그래서 미래에 사용할 가능성이 크다면 getter를 미리 만들어도 괜찮을 수도 있다.
