# javascript-calculator-precourse

# 1. 기능 구현 목록

### 1. 프로그램의 시작점이 되는 run() 함수~~에 시작 메세지 구현.~~

- 프로그램 시작 시 메세지 출력 "덧셈할 문자열을 입력해 주세요." (->"문자열 덧셈 계산기가 실행되었습니다." )

### 2. @woowacourse/mission-utils에서 제공하는 Console API를 이용해 사용자 입력을 비동기로 받는 기능 구현.

- 사용자 입력 받기
- 입력값이 비어있을 경우 ~~또는 잘못된 형식일 경우~~ 에러 처리 (-> 형식 검증은 3번 파싱 함수에서 처리 )

### 3. 쉼표(,)와 콜론(:)을 기본 구분자로 하는 문자열 파싱 기능 구현.

- 기본 구분자를 기준으로 입력 문자열을 분리
- 커스텀 구분자가 존재하는 경우, "//"와 "\n" 사이에 있는 문자를 커스텀 구분자로 사용하여 문자열을 분리
- 커스텀 구분자를 정의할 때, 맨 앞에 정의하지 않는 경우 파싱에러 출력 후 프로그램 종료
- 분리된 값이 숫자로 변환 가능한지 검증 -> 불가할 경우 "[ERROR] 숫자열로 변환되지 않는 입력이 포함됐습니다." 에러 메시지 출력 후 프로그램 종료
- 성공적으로 변환된 값이 음수일 경우 "[ERROR] 음수가 포함되어있습니다. 양수를 입력해주세요." 에러 메시지 출력 후 프로그램 종료
- 검증된 숫자열들을 배열로 반환

### 4. 숫자로 이루어진 배열을 모두 더하여 값을 반환하는 기능 구현

- 덧셈 계산 후 숫자열인 결과값 반환

### 5. 결과 출력

- 사용자에게 결과 값을 출력하는 기능 구현 (예: "결과 : 6").

### 6. 프로그램 종료

- 프로그램의 종료 메시지 없이 자연스럽게 종료되도록 처리
- 프로그램 종료 시 process.exit()를 호출하지 않기
- npm run test 통과

# 2. 테스트 케이스

- 숫자 사이에 띄어쓰기를 했을 경우 -> [ERROR]
- 입력값에 음수가 포함된 경우 -> [ERROR]
- 공백만 입력했을 경우 -> [ERROR]
- 아무 것도 입력하지 않을 경우 -> [ERROR]
- 입력값에 0이 포함된 경우 -> [ERROR] 입력 요구사항이 구분자와 "양수"이므로
- 커스텀 구분자 시작이나 끝에 숫자가 있는 경우 -> ~~[ERROR] ~사용자의 의도를 해석하기 어려우므로~~ -> 정상출력. 구분할 수 있음
- 커스텀 구분자가 숫자가 문자열로 감싸져있는 형태인 경우("a3a") -> 정상출력
- 커스텀 구분자가 시작이나 끝은 문자열(공백 포함)이고 중간이 숫자인 경우
  -> [ERROR] "// 3 \n"라는 커스텀 구분자를 만들었을 때, "3,3,3"을 의도한 입력으로
  "3 3 3 3 3"을 입력할 경우 의도한 값 9가 아닌 0이 출력될 것이므로
- 커스텀 구분자 정의를 맨 앞부분이 아닌 중간에 할 경우 -> [ERROR]
- //와 \n 사이에 구분자의 length가 2이상인 경우 -> //와 \n 사이 입력한 문자열 전체를 모두 똑같이 써야 구분자로 적용
  -> 즉, 입력: '//!@\\n1!2@3'은 [ERROR] 반환하고 '//!@\\n1!@2!@3' 는 정상적으로 6을 출력함
- 커스텀 구분자에 서로게이트페어를 넣은 경우 -> 정상출력
- 커스텀 구분자에 백슬래시 등 이스케이프 처리가 될 문자를 넣은 경우 -> 정상출력
- 커스텀 구분자에 \\n을 넣은 경우 -> 마지막 \\n 바로 뒤 숫자부터만 정상출력
- 커스텀 구분자 정의가 비어있을 경우 -> 커스텀 구분자 추가하지 않음(RegExp() 인자 특성상 자동처리)
- 커스텀 구분자에 띄어쓰기를 넣은 경우 -> 띄어쓰기를 구분자 추가 (정상출력)
- 커스텀 구분자와 기본 구분자의 혼합 사용 -> 정상 출력
- 중복 구분자 사용(4,,1) -> ,와 , 사이 빈 값은 0으로 계산 (결과 : 5)
- 구분자없이 여러 숫자가 붙어있는 경우(1324) -> 한 숫자로 판단(결과 : 1324)
- 소수 처리 여부 -> 정상 출력
- 구분자와 숫자 사이에 띄어쓰기를 한 경우 -> 공백을 무시하고 정상 출력
- 자바스크립트가 처리할 수 없는 너무 큰 숫자를 입력했을 경우

# 3. 기능 구현 중 메모

- 3번 기능 구현할 때, \n 이스케이프 처리 문제
- 여러 구분자를 포함한 정규표현식을 생성하는 법 => new RegExp() 사용
- a.every(x => x < 0) 메서드 <-> a.some(x => x <0) 메서드
