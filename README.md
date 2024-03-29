# 파이썬 기초 2024
부경대학교 2024 IoT 개발자 과정 기초 프로그래밍 언어 - 파이썬

## 1일차
- 개발환경 구축
    - 코딩폰트 - 나눔고딕코딩
    - Notepad++ 설치
    - Python 설치
    - Visual Studio Code 설치
    - Git 설치
        - TortoiseGit 설치
        - Github 가입
        - Github Desktop 설치

- 파이썬 기초
    - 콘솔출력
    - 주석
    - 변수
    - 자료형
    - 연산자

    ```python
    # 이 부분은 주석입니다.
    var01 = 10 # 정수, 실수, 불, 문자열 모두 가능
    print(var01)
    print(type(var01))

    print(5 + 4 / 2) # 7.0
    print(5 == 4) # False
    ```

## 2일차
- 파이썬 기초
    - 흐름제어
        - if : Ture/False로 조건 분기 (다른 언어 switch)
        - for : 반복문 기본 (다른 언어 foreach)
        - while : 반복문 변형 (다른 언어 do~while)
    - 복합자료형 + 연산자
        - 리스트, 튜플, 딕셔너리
    - 출력 포맷
    - 구구단 + 디버깅

    ```python
    # debugging
    # F9(중단점 토글), F5(디버그 시작), F10(한줄씩 실행), F11(함수안으로 진입)
    # Shift + F5(디버깅 종료)
    print('구구단 시작!')
    for x in range(2, 9+1): # 2부터 9까지 반복
        print(f'{x}단------>')
        for y in range(1, 9+1): # 1부터 9까지 반복
            print(f'{x} x {y} = {x*y:2d}', end=' ') # end=' ' : 엔터 대신 공백으로 변경
        print() # 안쪽 for 문이 끝나면 마지막 엔터를 하나 추가
    ```

## 3일차
- 파이썬 기초
    - 입력 방법
    - 별찍기(피라미드 만들기)
    - 함수(람다함수는 나중에)
    - 객체지향(OOP:Object Oriented Programming)
        - 객체는 명사와 동사의 집합
        - 명사는 변수, 동사는 함수
        - 변수와 함수를 모두 모아둔 곳 : 클래스(class)
        - 클래스에서 하나씩 생성하는 것 : 객체(object)
        - 클래스(class)는 설계도, 객체(object)는 설계도로 구현한 대상
        - 캡슐화(test22 : __plate_num 참조)
    - 패키지, 모듈

## 4일차
- 파이썬 기초
    - 패키지, 모듈 계속
        - pip 사용

        ```shell
        > pip --version # pip 버전 확인
        > pip list # 현재 설치된 라이브러리 목록 확인
        > pip install 패키지명 # 패키지를 내 컴퓨터에 설치, Successfully installed 문구 확인할 것
        > pip unistall 패키지명 # 패키지를 내 컴퓨터에서 삭제
        ```
    - 예외처리 : 비정상적인 프로그램 종료 방지


## 5일차
- 파이썬 응용
    - 주피터 노트북 활용 - 구글 코랩(Colab:브라우저 내에서 Python 스크립트를 작성하고 실행)
    - folium 계속
    - json 사용법
    - 응용예제 연습(10개)
        - IP 주소 확인
        - QRcode 만들기

## 6일차
- Python 라이브러리 경로 : C:\DEV\Langs\Python311\Lib\site-packages
- 파이썬 응용
    - Window App(PyQt)만들기

    ```shell
    > pip install PyQt5
    > pip install PyQt5Designer
    ```

    - PyQt5 기본실행
    - QtDesigner 사용법
    - ☆☆☆ 쓰레드 학습 : UI 쓰레드와 Background쓰레드 분리
        - [ ] GiL, 병렬프로세스 더 학습할 것

    ![쓰레드 예제](https://raw.githubusercontent.com/YooWangGwon/basic-python-2024/main/images/python_003.gif)

    ```python
    # 쓰레드 클래스에서 시그널 선언
    class BackWorker(QThread): # PyQt에서 스레드 클래스 상속
        initSignal = pyqtSignal(int) # 시그널을 밑에 있는 UI스레드로 전달하기 위한 변수객체
        setSignal = pyqtSignal(int)
        # ...

        def run(self) -> None: # 스레드 실행
        # 스레드로 동작할 내용
            maxVal = 1000001
            self.initSignal.emit(maxVal) # UI스레드로 보내기
            # ...

    class qtwin_exam(QWidget): # UI 스레드
        # ...
        def btnStartClicked(self):
            th = BackWorker(self)
            th.start() # BackWorker 내의 self.run()이 실행됨
            th.initSignal.connect(self.initPgbTask) # 스레드에서 초기화 시그널이 오면 initPgbTask실행
            th.setSignal.connect(self.setPgbTask)
            # ...

    # 스레드에서 시그널이 넘어오면 ui처리를 대신 해주는 슬롯함수
    @pyqtSlot(int) # BackWorker스레드에서 self.initSignal.emit() 동작해서 실행
    def initPgbTask(self, maxVal):
        self.pgbTask.setValue(0)
        self.pgbTask.setRange(0, maxVal-1)
    ```

## 7일차
- 파이썬 응용
    - 객체지향
        - 상속, 오버라이딩(재정의), 오버로딩(같은 이름의 함수를 마음대로 골라쓰자)
    - 가상환경 Virtualenv
        - 다른 버전의 파이썬도 설치해야 사용 가능
        - 현재 3.11에서 3.9 가상환경을 만들려면 3.9버전 파이썬을 설치해야함
    - PyQt5와 응용예제 연습
        - 이미지 뷰어
        - 이미지 에디터

    ![PyQt예제](https://raw.githubusercontent.com/YooWangGwon/basic-python-2024/main/images/python_004.png)

## 8일차
- 파이썬 응용
    - PyQt5 응용예제 계속

- 파이썬 기본 코딩 테스트
    - 주피터 노트북 활용

## 추후 학습예정 내용
- 객체지향
    - 상속, 오버라이딩(재정의), 오버로딩(같은 이름의 함수를 마음대로 골라쓰자)
    - 오버로드 : 같은 이름의 함수를 매개변수의 종류가 다르면 하나의 이름으로 여러종류의 함수처럼 사용  가능
    - 상속, 다중상속
    - 추상클래스c

## 추가(2024.02,20)
- 파이썬 실행파일 만들기
    - PyQt ui 파일이나 이미지파일의 경로가 절대경로가 지정
    - pip install pyinstaller 패키지  설치
    - pyinstaller -w -F '파이썬 파일명'.py (-w : 콘솔창 없애기, -F: 실행파일 하나로 만들기)