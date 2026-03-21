# AIoT-
라즈베리파이를 이용한 신호등 만들기

# gpiozero 라이브러리에서 LED 클래스를 가져옴
# 라즈베리파이에서 LED를 쉽게 제어하기 위한 라이브러리
from gpiozero import LED  

# time 라이브러리에서 sleep 함수 가져옴
# 프로그램을 일정 시간 동안 멈추기 위해 사용
from time import sleep  


# GPIO 핀 번호 설정
# 각 변수에 연결된 GPIO 핀 번호를 저장
carLedRed = 2         # 자동차용 빨강 LED → GPIO 2번
carLedBlue = 3        # 자동차용 파랑 LED → GPIO 3번
carLedGreen = 4       # 자동차용 초록 LED → GPIO 4번
humanLedRed = 20      # 보행자용 빨강 LED → GPIO 20번
humanLedGreen = 21    # 보행자용 초록 LED → GPIO 21번


# LED 객체 생성
# 위에서 지정한 GPIO 핀을 실제 LED 객체로 변환
#  .on(), .off(), .value 등을 통해 제어 가능

carLedRed = LED(2)        # GPIO 2번 핀에 연결된 LED 객체 생성
carLedBlue = LED(3)       # GPIO 3번 핀 LED
carLedGreen = LED(4)      # GPIO 4번 핀 LED
humanLedRed = LED(20)     # GPIO 20번 핀 LED
humanLedGreen = LED(21)   # GPIO 21번 핀 LED


# 예외 처리 시작
# Ctrl + C로 프로그램 종료 시 오류 없이 종료하기 위해 사용
try:
    # 무한 반복 → 신호등은 계속 동작해야 하므로
    while True:
        # 1. 자동차 초록, 보행자 빨강 신호일 때
        carLedRed.value = 0       # 자동차 빨강 OFF
        carLedBlue.value = 0      # 자동차 파랑 OFF
        carLedGreen.value = 1     # 자동차 초록 ON → 차량 통행 가능
        humanLedRed.value = 1     # 보행자 빨강 ON → 보행 금지
        humanLedGreen.value = 0   # 보행자 초록 OFF
        sleep(3.0)                # 몇초 동안 유지를 할 것 인가 (3초 설정)
       # 2. 자동차 파랑, 보행자 빨강 신호일 때 
        carLedRed.value = 0       # 자동차 빨강 OFF
        carLedBlue.value = 1      # 자동차 파랑 ON → 곧 정지 준비
        carLedGreen.value = 0     # 자동차 초록 OFF
        humanLedRed.value = 1     # 보행자 빨강 유지
        humanLedGreen.value = 0   # 보행자 초록 OFF
        sleep(1.0)                # 몇초 동안 유지를 할 것 인가 (1초 설정)
        # 3. 자동차 빨강, 보행자 초록 신호일 떄
        carLedRed.value = 1       # 자동차 빨강 ON → 차량 정지
        carLedBlue.value = 0    # 자동차 노랑 OFF
        carLedGreen.value = 0     # 자동차 초록 OFF
        humanLedRed.value = 0     # 보행자 빨강 OFF
        humanLedGreen.value = 1   # 보행자 초록 ON → 보행 가능
        sleep(3.0)                # 몇초 동안 유지를 할 것 인가 (3초 설정)

# Ctrl + C 입력 시 실행되는 부분
except KeyboardInterrupt:
    # 아무 동작 없이 종료 (에러 방지)
    pass

# 프로그램 종료 시 실행
# 모든 LED를 OFF 상태로 만들어서 안전하게 종료
carLedRed.off()         # 자동차 빨강 LED 끄기
carLedBlue.off()        # 자동차 파랑 LED 끄기
carLedGreen.off()       # 자동차 초록 LED 끄기
humanLedRed.off()       # 보행자 빨강 LED 끄기
humanLedGreen.off()     # 보행자 초록 LED 끄기
