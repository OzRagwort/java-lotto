# java-lotto
로또 미션을 위한 저장소

<br/>

## 👩‍💻 구현할 기능 목록
### 1단계
- [x] 금액을 입력한다.
```
[예외]
🆗 숫자가 아닌 경우
🆗 음수인 경우
🆗 공백인 경우
```
- [x] 금액에 맞게 로또를 구매해야 한다.
- [x] 무작위로 로또 번호를 추첨한다.
- [x] 당첨 번호를 입력한다.
- [x] 보너스 볼을 입력한다.
```
[공통 예외]
🆗 숫자가 아닌 경우
🆗 1~45의 범위가 아닌 경우
🆗 공백인 경우

[당첨 번호 예외]
🆗 6개보다 적거나 많은 숫자를 입력한 경우
🆗 중복되는 숫자를 입력한 경우
🆗 구분자가 콤마(,)가 아닌 경우

[보너스볼 예외]
🆗 당첨 번호 중 하나와 중복되는 숫자를 입력한 경우
```
- [x] 당첨 통계를 계산한다.
  - [x] 몇개를 맞췄는지 구한다.
  - [x] 일치하는 번호 개수에 따른 통계값을 구한다.
      - ex. 3개 일치 - 1개, 4개 일치 - 2개...
  - [x] 맞춘 개수에 따라 상금을 구한다.
- [x] 수익률을 계산한다.

### 2단계
- [x] 수동으로 로또를 구매한다.
  - [x] 수동으로 구매할 로또 수를 입력한다.
  - [x] 수동으로 구매할 로또 번호를 입력한다.
```
[공통 예외]
🆗 숫자가 아닌 경우
🆗 공백인 경우

[로또 수 예외]
🆗 음수인 경우
🆗 구입금액으로 살 수 있는 최대 개수를 초과한 경우

[로또 번호 예외]
🆗 1~45의 범위가 아닌 경우
🆗 6개보다 적거나 많은 숫자를 입력한 경우
🆗 중복되는 숫자를 입력한 경우
🆗 구분자가 콤마(,)가 아닌 경우
```
- [x] 수동으로 구매하고 남은 예산으로는 자동으로 구매한다.

<br/>

## ✅ 확인할 프로그래밍 목록
- [x] indent(인덴트, 들여쓰기) depth를 2단계에서 1단계로 줄여라.
  - depth의 경우 if문을 사용하는 경우 1단계의 depth가 증가한다.
  - if문 안에 while문을 사용한다면 depth가 2단계가 된다.
- [x] else를 사용하지 마라.
- [x] 메소드의 크기가 최대 10라인을 넘지 않도록 구현한다.
  - method가 한 가지 일만 하도록 최대한 작게 만들어라.
- [x] 배열 대신 ArrayList를 사용한다.
- [x] java enum을 적용해 프로그래밍을 구현한다.
- [x] 모든 원시값과 문자열을 포장한다.
- [x] 줄여쓰지 않는다(축약 금지).
- [x] 일급 콜렉션을 쓴다.
- [x] 예외가 발생하는 부분에 대해 자바 Exception을 적용해 예외처리한다.
  - 사용자가 입력한 값에 대한 예외 처리를 철저히 한다.