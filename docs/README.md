# 🌉 4주차 미션 - 다리 건너기 (Bridge)

<br>

## 👦 [작성자] : 김동우(DongWooKim97)

<br>

## 🎯 구현 목표

<br>

- [x] **1. 다리의 사이즈를 입력받고, 해당 크기의 다리를 만들어 게임을 진행**

- [x] **2. 건널 수 있는 다리의 길을 랜덤으로 정하고, 이에 맞게 건너도록 유도**

- [x] **3. 건너고 싶은 길을 입력받고, 건널 수 없으면 재시작, 건널 수 있으면 진행**

- [x] **4. 게임 종료시, 게임 진행 횟수와 최종 다리 루트, 성공여부를 출력**

<br>

## 📝 구현할 기능 목록

<br>

- [x] **1. 입력받은 다리 길이를 통해 랜덤으로 건널 수 있는 다리 루트 생성 기능(객체)**

  - 게임을 진행하기에 앞서, 다리 사이즈를 유저로부터 입력받는다.

  - 입력받은 다리 길이를 통해, 위/아래 건널 수 있는 다리를 랜덤으로 생성

    - `InputView`객체를 통해, 유저로부터 다리 사이즈 입력받음.

    - `OutputView`객체를 통해 게임 시작을 알리고, 사이즈를 입력받는다.

<br>

- [x] **2. 재사용성 증대를 위한 상수값 관리 기능**

  - 게임을 진행하기 위해서는 특정 값들이 빈번하게 재사용됨.

  - 그렇기에 `Constants.js`객체를 통해 재사용되는 값들을 생성.

    - `GAME_MESSAGES` -> 게임 진행에 필요한 출력문을 저장하는 객체.

<br>

- [x] **3. 게임을 실질적으로 진행하는 기능(클래스)**

  - 각 단계에서의 입력을 통해, 게임을 실질적으로 진행하는 클래스 `BridgeGame`생성

  - 이 클래스를 통해, 이동하고 재시도를 하는 기능 생성.

  - 클래스 내부적으로 입력받은 이동루트 및 시도 횟수를 저장.

<br>

- [x] **4. 게임 정보를 저장하고 게임관련 로직을 수행하는 기능(클래스)**

  - `BridgeInformation`은 `BridgeGame`을 통해서 수행하는 로직들을 저장하는 기능

    - 대표적으로, `size`를 입력받아 다리를 생성 및 저장하고, 정답 루트와 입력한 루트를 비교하는 로직들 저장.

    - 또한 출력에 필요하거나 비교에 필요한 정보들을 저장하는 클래스.

  - `BridgeGame`의 프라이빗 필드`this.#info`에 인스턴스를 생성하여 해당 클래스에 연결

  - 생성한 인스턴스를 통해 내부적 로직 및 동작을 거친 후 , 메시지를 통해 외부에 알리는 클래스.

<br>

- [x] **5. 입력값에 대한 예외를 처리하는 객체 추가**

  - `InputView`에서만 `Console.readLine`이 사용가능 하기에, `InputView`객체에서 입력한 값들을 예외처리하는 `Validate`객체 추가

  - 게임에 필요한 입력한 대표적으로 3가지.

    - 1\_ 다리 길이 사이즈
    - 2\_ 다리 이동 루트 ("U" / "D")
    - 3\_ 게임 재시작 명령 ("R" / "Q")

  - 다리 길이는 3~20 사이 입력과 숫자 외의 입력 확인
  - 다리 이동 루트는 U / D 을 제외한 입력 확인
  - 게임 재시작 명령은 R / Q 를 제외한 입력 확인

<br>

- [x] **6. 특정한 값들을 출력하는 기능(객체)**

  - 게임을 진행하기 위해 필요한 값들을 출력하는 객체 `OutputView`.

  - 게임 시작 문구부터, 이동 루트 및 성공 여부 , 시도 횟수등 게임에 필요한 문구를 출력하는 객체.

    - `printInitGame` -> 게임 시작 문구 출력

    - `printMap` -> 유저의 이동 루트를 출력

    - `printError` -> 예외 처리를 통한 에러를 출력

    - `printEndGame` -> 게임 종료 문구 출력

    - `printResult` -> 게임 결과 출력

<br>

- [x] **7. 작성한 기능 및 코드에 대한 테스트 코드**

  - 작성한 모듈 및 클래스별로 테스트 코드를 작성

  - 작성 코드는 두 가지 범주에서 진행

    - 1\_ 도메인 로직 단위

    - 2\_ 기능 로직 단위

  - 전체 흐름에 대한 최종 결과값을 도메인 로직 단위에서 테스트 진행

  - 개별적 단위의 결과값을 기능 로직 단위에서 테스트 진행

    - `ApplicationTest.js`

      - : 도메인 로직 단위의 테스트로, 제공된 입출력을 통해 전체적인 흐름을 테스트
      - : 정상 작동함을 파악하기 위해 나만의 입력을 제공항 결과값이 맞는지 테스트

    - `ValidateTest.js`

      - : 3 가지의 입력값에 대한 예외처리를 담당하는 객체
      - : 다리 길이 / 이동 경로 / 재시작 명령어

    - `BridgeMakerTest.js`

      - : 유저로부터 다리 길이를 입력받아 올바른 이동 경로 배열을 생성하는지 확인하는 테스트
      - : 입력받은 숫자만큼의 길이가 생성되는지 테스트

    - `BridgeInformationTest.js`

      - : 입력받은 입력값을 직접으로 활용하는 클래스에 대한 테스트
      - : 올바른 경로와 입력 경로의 비교, 입력 경로에 맞는 출력값 설정 등이 올바르게 제공되는지 테스트.
