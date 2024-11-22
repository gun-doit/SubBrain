  

https://www.figma.com/design/yvLk04UJqtDG3s03zGyOS8/RC_Car?node-id=0%3A1&t=6dSAKVAkPueOH2q7-1

# RC 카

### 주제

**서라운드 뷰**

1. [3D를 2D에 담는 방법 - Projective Geometry : 네이버 블로그 (naver.com)](https://m.blog.naver.com/hasukmin12/222084951669)

  

## **모듈**

1. **RC카**
    1. **서라운드 뷰**
    2. **주차?**
2. **원격 조정기 ( Raspi5 + LCD )**
    
    ![[Untitled 19.png|Untitled 19.png]]
    
3. **js.기반 web visualizer**
    1. **vue**
4. **로그 데이터 분석 - AI**
    1. 연결정보??

  

## BODY

- [ ] 나무젓가락 범퍼 만들기
- [ ] 버튼 3개 연동
- [ ] OpenAI 잘 모르는디

  

  

## WEB

- 모니터링
    - [x] 연결 셋팅
        - [x] 블루투스
        - [x] 연결정보
    - [ ] 그래프
        - [ ] 구동시간

  

- 라운드
    
    - [x] 스코어
    - [ ] OpenAI
    - [x] 스타트 버튼
    - [x] 리셋 버튼
    
      
    
    - [ ] 게임 종료 시간
- 페이지 2
    - [ ] DB 로그
        - [x] 그래프
            - [x] 로그
    - [ ] GUI 제어버튼
    - [ ] 연결 정보
    - [ ]

- [ ] DB 연동 로그데이터
- [ ] 모터 정보
- [ ] 구동 시간
- [ ] 연결되었는지

## 선택

- [ ] 센스햇 HP
- [ ] 카메라

## 개발 환경

> **RC카 : Raspi 4 + senseHat**
> 
> - 상세내용
>     - 파이썬 버전 3.8.12 - pyenv 사용 버전 변경
>         
>         ```Bash
>         sudo apt update
>         sudo apt install -y make build-essential libssl-dev zlib1g-dev \
>         libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
>         libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python3-openssl \
>         git
>         ```
>         
>         ```Bash
>         git clone https://github.com/pyenv/pyenv.git ~/.pyenv
>         ```
>         
>         ```Bash
>         echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
>         echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
>         ```
>         
>         ```Bash
>         source ~/.bashrc
>         ```
>         
>         ```Bash
>         pyenv install 3.8.12
>         ```
>         
>         ```Bash
>         pyenv global 3.8.12
>         ```
>         
>         ```Bash
>         안될경우
>         eval "$(pyenv init --path)"
>         ```
>         
>     - RTIMULib안될 때
>         
>         ```Bash
>         해당 스레드에서는 그다지 명확하지 않기 때문에 제가 한 일을 공유하고 싶습니다. 기본적으로 다음 bennuttall권장 사항이 트릭을 수행했습니다.
>         
>         virtualenv를 생성합니다:
>         
>         virtualenv -p /usr/bin/python3 ~/.ve/sensorhat
>         source ~/.ve/sensorhat/bin/activate
>         RTIMULib 복제 :
>         
>         git clone https://github.com/RPi-Distro/RTIMULib/ RTIMU
>         cd RTIMU/Linux/python
>         RTIMULib/Linux/python 의 지침을 따르세요 .
>         
>         sudo apt install python3-dev
>         python setup.py build
>         python setup.py install
>         설치하다 libopenjp2-7:
>         
>         sudo apt install libopenjp2-7
>         설치하다 sense-hat:
>         
>         sudo apt install sense-hat
>         ```
>         
> 
> **원격 조정기 : Raaspi 5 + TFT LCD**
> 
> **open api :**
> 
> **DB : Mysql2**
> 
> **Front : Vue3**
> 
> **Back : Node.js Express + AWS**

  

## BACK

> **Express**

- **모니터링 페이지**

- [ ] **자동차 데이터 ( 모터 속도, 각도 )**
    - **id, time, car, speed, direction**

  

- [ ] Command 로그 데이터
    - **id, time, car, cmd_string, is_finishv**

  

- **라운드 페이지**

- [ ] **Score log 데이터**
    - **id, time, round, car, hp_left, hp_right, hp_back, factor**

## DB

> **Mysql2**

- 설정 정보
    - AWS EC2
        - 3.35.169.119
        - hyndrome+aw2@gmail.com
        - SSAFYrccar2@
            
            ![[ssafy_bumper_key.pem]]
            
    - mysql
        - mincoding
        - 1234
        - mysql_native_password
- schema
    
    ```SQL
    CREATE TABLE `command` (
    	`id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    	`time` DATETIME NULL,
    	`car` INT NULL,
    	`cmd_string` VARCHAR(50) NULL DEFAULT NULL,
    	`cmd_value` DECIMAL(3, 2) NULL,
    	`is_finish` INT NULL
    );
    
    CREATE TABLE `score_log` (
    	`id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    	`time` DATETIME NULL,
        `round` INT NULL,
        `car` INT NULL,
        `hp_left` INT NULL, 
        `hp_right` INT NULL, 
        `hp_back` INT NULL,
        `factor` INT NULL
    );
    
    CREATE TABLE `velocity_log` (
    	`id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    	`time` DATETIME NULL,
      `car` INT NULL,
      `speed` INT NULL,
      `direction` INT NULL
    );
    ```
    
- initial data
    
    ```SQL
    INSERT INTO `command` (`time`, `car`, `cmd_string`, `cmd_value`, `is_finish`) VALUES ('2022-05-21 14:10:53', 1, 'right', 0.50,'1');
    
    INSERT INTO `score_log` (`time`, `round`, `car`, `hp_left`, `hp_right`, `hp_back`, `factor`) VALUES ('2022-05-21 14:10:53', '1', '1', '3', '3', '3', '1');
    INSERT INTO `score_log` (`time`, `round`, `car`, `hp_left`, `hp_right`, `hp_back`, `factor`) VALUES ('2022-05-21 14:10:53', '1', '2', '3', '3', '3', '1');
    
    INSERT INTO `velocity_log` (`time`, `car`, `speed`, `direction`) VALUES ('2022-05-21 14:10:53', '1', '0', '0');
    ```
    
- 시간 맞춰주자
    
    ```Bash
     sudo date -s "20240523 18:44:30"
    ```
    

  

## FRONT

> **Vue3**

- [x] 모터 속도
- [x] 모터 각도
- [x] 구동 시간
- [x] OpenAI API
- [x] 로그데이터
    - [ ] 카메라 송신 데이터?
    - [x] 모터 연결 데이터?

  

  

  

> [!important]  
> rc car 2대와 GUI controller는 db에서 최신 시간 순으로 불러오므로 시간을 일치시켜준다 sudo date -s "20240524 10:56:30"  

## RC CAR

- bumpCar1.py
    
    ```Python
    import mysql.connector
    from threading import Timer, Lock, Thread
    from time import sleep
    import signal
    import sys
    from Raspi_MotorHAT import Raspi_MotorHAT, Raspi_DCMotor
    from Raspi_PWM_Servo_Driver import PWM
    from sense_hat import SenseHat
    import datetime
    import evdev
    import time
    from evdev import InputDevice, ecodes, ff
    from gpiozero import Button
    
    
    # DB 종료
    def closeDB(signal, frame):
        print("BYE")
        sense.clear()
        cur.close()
        db.close()
        timer.cancel()
        mh.getMotor(2).run(Raspi_MotorHAT.RELEASE)
        timer2.cancel()
        sys.exit(0)
    
    
    # polling for command 처리 + rc car hp status update + 속력 방향 업데이트(예정)
    def polling():
        global cur, db, ready, car, car_hp_left, car_hp_right, car_hp_back, game_round, car_speed, car_direction
        lock.acquire()  # Mutex lock
        # process received command from GUI
        cur.execute("select * from command where car=1 order by time desc limit 1")
        for (id, time, v_car, cmd_string, cmd_value, is_finish) in cur:
            if is_finish == 1: break
            ready = (cmd_string, cmd_value)
            cur.execute("update command set is_finish=1 where is_finish=0")
        # update rc car hp status
        cur.execute("select * from score_log where car=1 order by time desc limit 1")
        for (id, time, v_round, v_car, hp_left, hp_right, hp_back, factor) in cur:
            game_round = v_round
            car_hp_left = hp_left
            car_hp_right = hp_right
            car_hp_back = hp_back
        # print(f"local hp left: {car_hp_left}")
        # print(f"local hp right: {car_hp_right}")
        # print(f"local hp back: {car_hp_back}")
        # print("===============================")
        # update velocity_log
        c_time = datetime.datetime.now()
        query = "insert into velocity_log(time, car, speed, direction) values (%s, %s, %s, %s)"
        value = (c_time, car, car_speed, car_direction)
        cur.execute(query, value)
        db.commit()
        lock.release()  # Mutex unlock
    
        global timer
        timer = Timer(0.1, polling)
        timer.start()
    
    
    # polling for 데미지 처리 (버튼 처리)
    def polling_damaged():
        global btn_left, btn_right, btn_back
        if btn_left.is_pressed:
            print("left damaged")
            vibrate_controller(1000)
            log_damaged("left")
            sleep(5)  # 충돌은 5초마다 1번씩만 카운팅
        if btn_right.is_pressed:
            print("right damaged")
            vibrate_controller(1000)
            log_damaged("right")
            sleep(5)
        if btn_back.is_pressed:
            print("back damaged")
            vibrate_controller(1000)
            log_damaged("back")
            sleep(5)
    
        global timer2
        timer2 = Timer(0.05, polling_damaged)
        timer2.start()
    
    
    # db에 데미지 기록
    def log_damaged(direction):
        global cur, db, game_round, car, car_hp_left, car_hp_right, car_hp_back
        time = datetime.datetime.now()
        if direction == "left":
            if car_hp_left > 0:
                car_hp_left -= 1
            else:
                return
        elif direction == "right":
            if car_hp_right > 0:
                car_hp_right -= 1
            else:
                return
        elif direction == "back":
            if car_hp_back > 0:
                car_hp_back -= 1
            else:
                return
        hp_left = car_hp_left
        hp_right = car_hp_right
        hp_back = car_hp_back
        query = "insert into score_log(time, round, car, hp_left, hp_right, hp_back, factor) values (%s, %s, %s, %s, %s, %s, %s)"
        value = (time, game_round, car, hp_left, hp_right, hp_back, 1)  # 게임 내 득점인 경우 factor=1
        lock.acquire()  # Mutex lock
        cur.execute(query, value)
        db.commit()
        lock.release()  # Mutex unlock
    
    
    # xboxController 수신
    def joystick_polling():
        global device_path, ready
        try:
            joystick = evdev.InputDevice(device_path)
    
            print(f'Listening on {joystick.path}, device: {joystick.name}')
    
            for event in joystick.read_loop():
                # 컨트롤러 버튼 입력 감지 (버튼은 수치 값이 없음 )
                if event.type == evdev.ecodes.EV_KEY:
                    key_event = evdev.categorize(event)
                    if key_event.keycode == "BTN_TR":
                        ready = ("stop", 0)
                # 컨트롤러 스틱, 트리거 (수치 값이 있음)
                if event.type == evdev.ecodes.EV_ABS:
                    abs_event = evdev.categorize(event)
                    # print(f'Axis: {evdev.ecodes.ABS[abs_event.event.code]}, {abs_event.event.code}, Value: {abs_event.event.value}')
                    # 트리거 처리
                    if evdev.ecodes.ABS[abs_event.event.code] == 'ABS_GAS':  # 우측 아래 트리거 / 최소 0 / 최대 1023 - 전진
                        gas_value = int(abs_event.event.value) / 1023
                        ready = ("go", gas_value)
                    elif evdev.ecodes.ABS[abs_event.event.code] == 'ABS_BRAKE':  # 좌측 아래 트리거 / 최소 0 / 최대 1023 - 후진
                        brake_value = int(abs_event.event.value) / 1023
                        ready = ("back", brake_value)
                    # 왼쪽 스틱 - 좌우 조향
                    elif evdev.ecodes.ABS[
                        abs_event.event.code] == 'ABS_X':  # 좌측 스틱 / 최소 0 (왼쪽) / 최대 65,535 (오른쪽) / 중앙 32,767
                        x_value = int(abs_event.event.value) / 65535
                        ready = ("steer", x_value)
        except KeyboardInterrupt:
            print("Joystick polling interrupted by user.")
        finally:
            print("Cleaning up joystick polling...")
    
    
    # xboxcontroller 진동 전송
    def vibrate_controller(duration_ms):
        controller = InputDevice(device_path)
    
        rumble = ff.Rumble(strong_magnitude=0xFFFF, weak_magnitude=0xFFFF)
        effect_type = ff.EffectType(ff_rumble_effect=rumble)
        # duration_ms = 1000  # 진동 지속 시간 (밀리초)
        effect = ff.Effect(
            ecodes.FF_RUMBLE, -1, 0,
            ff.Trigger(0, 0),
            ff.Replay(duration_ms, 0),
            effect_type
        )
    
        effect_id = controller.upload_effect(effect)
        controller.write(ecodes.EV_FF, effect_id, 1)
        time.sleep(duration_ms / 1000)
        controller.write(ecodes.EV_FF, effect_id, 0)
        controller.erase_effect(effect_id)
    
    
    # senseHAT LED
    def sensehatPrint(word):
        X = [255, 0, 0]  # Red
        O = [0, 0, 0]  # White
        matrix = ""
        if word == "go":
            matrix = [
                O, O, O, X, X, O, O, O,
                O, O, X, X, X, X, O, O,
                O, X, X, X, X, X, X, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O
            ]
        elif word == "back":
            matrix = [
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, X, X, X, X, X, X, O,
                O, O, X, X, X, X, O, O,
                O, O, O, X, X, O, O, O
            ]
        elif word == "stop":
            matrix = [
                O, O, X, X, X, X, O, O,
                O, X, O, O, O, O, X, O,
                X, O, X, O, O, O, O, X,
                X, O, O, X, O, O, O, X,
                X, O, O, O, X, O, O, X,
                X, O, O, O, O, X, O, X,
                O, X, O, O, O, O, X, O,
                O, O, X, X, X, X, O, O
            ]
        elif word == "right":
            matrix = [
                O, O, O, O, O, O, O, O,
                O, O, O, O, O, X, O, O,
                O, O, O, O, O, X, X, O,
                X, X, X, X, X, X, X, X,
                X, X, X, X, X, X, X, X,
                O, O, O, O, O, X, X, O,
                O, O, O, O, O, X, O, O,
                O, O, O, O, O, O, O, O
            ]
        elif word == "left":
            matrix = [
                O, O, O, O, O, O, O, O,
                O, O, X, O, O, O, O, O,
                O, X, X, O, O, O, O, O,
                X, X, X, X, X, X, X, X,
                X, X, X, X, X, X, X, X,
                O, X, X, O, O, O, O, O,
                O, O, X, O, O, O, O, O,
                O, O, O, O, O, O, O, O
            ]
        sense.set_pixels(matrix)
    
    
    # 차량 동작 코드 - 앞
    def go(cmd_value):
        global MAX_SPEED, car_speed
        speed = round(MAX_SPEED * cmd_value)
        myMotor.setSpeed(speed)
        myMotor.run(Raspi_MotorHAT.FORWARD)
        car_speed = round(cmd_value * 100)
        sensehatPrint("go")
    
    
    # 차량 동작 코드 - 뒤
    def back(cmd_value):
        global MAX_SPEED, car_speed
        speed = round(MAX_SPEED * cmd_value)
        myMotor.setSpeed(speed)
        myMotor.run(Raspi_MotorHAT.BACKWARD)
        car_speed = -(round(cmd_value * 100))
        sensehatPrint("back")
    
    
    # 차량 동작 코드 - 정지 (속도 방향 초기화)
    def stop():
        global MIN_SERVO, MAX_SERVO, car_speed, car_direction
        myMotor.run(Raspi_MotorHAT.RELEASE)
        steering = round(0.5 * (MAX_SERVO - MIN_SERVO) + MIN_SERVO)
        servo.setPWM(0, 0, steering)
        car_speed = 0
        car_direction = 0
        sensehatPrint("stop")
        # vibrate_controller()
    
    
    # 차량 동작 코드 - 조타
    def steer(cmd_value):
        global MIN_SERVO, MAX_SERVO, car_direction
        steering = round((MAX_SERVO - MIN_SERVO) * cmd_value + MIN_SERVO)
        servo.setPWM(0, 0, steering)
        car_direction = round(cmd_value * 200 - 100)
        if steering < 300:
            sensehatPrint("left")
        elif steering > 360:
            sensehatPrint("right")
    
    
    # init
    # xboxcontroller 경로 - evtest에서 확인
    device_path = '/dev/input/event5'
    # 차량 정보
    car = 1
    # 차량 정보 - score_log
    car_hp_left = 1
    car_hp_right = 1
    car_hp_back = 1
    game_round = 1
    # 차량 정보 - velocity_log
    MAX_SPEED = 255
    MIN_SERVO = 230
    MAX_SERVO = 430
    car_speed = 0  # -100 ~ 100
    car_direction = 0  # -100 ~ 100
    
    # DB
    db = mysql.connector.connect(host='3.35.169.119', user='mincoding', password='1234', database='minDB',
                                 auth_plugin='mysql_native_password')
    cur = db.cursor()
    ready = None
    
    # 모터
    mh = Raspi_MotorHAT(addr=0x6f)
    myMotor = mh.getMotor(2)  # 핀번호
    # 서보모터
    servo = PWM(0x6F)  # 330 netutral
    servo.setPWMFreq(60)  # Set frequency to 60 Hz
    
    # sensehat
    sense = SenseHat()
    sense.set_rotation(270)
    
    # 버튼 핀 번호 설정
    BUTTON_PIN_LEFT = 17
    BUTTON_PIN_RIGHT = 27
    BUTTON_PIN_BACK = 22
    btn_left = Button(BUTTON_PIN_LEFT, pull_up=True)
    btn_right = Button(BUTTON_PIN_RIGHT, pull_up=True)
    btn_back = Button(BUTTON_PIN_BACK, pull_up=True)
    
    # Mutex - sensing과 polling 메서드 두 쓰레드가 동시에 DB에 접근, 충돌 방지
    lock = Lock()
    # polling for  GUI 제어기 신호처리
    timer = None
    polling()
    # polling for 범퍼 데미지 감지 
    timer2 = None
    polling_damaged()
    
    # 조이스틱 폴링 스레드 시작
    joystick_thread = Thread(target=joystick_polling)
    joystick_thread.start()
    
    # 종료
    signal.signal(signal.SIGINT, closeDB)
    
    # main thread 실제로 차량 작동
    while True:
        sleep(0.1)
        if ready == None: continue
    
        cmd, cmd_value = ready  # (cmd에 해당하는 string, cmd의 강도 0 ~ 1사이의 값)
        ready = None
    
        if cmd == "go": go(cmd_value)
        if cmd == "back": back(cmd_value)
        if cmd == "stop": stop()
        if cmd == "steer": steer(cmd_value)
    ```
    
- bumpCar2.py
    
    ```Python
    import mysql.connector
    from threading import Timer, Lock, Thread
    from time import sleep
    import signal
    import sys
    from Raspi_MotorHAT import Raspi_MotorHAT, Raspi_DCMotor
    from Raspi_PWM_Servo_Driver import PWM
    from sense_hat import SenseHat
    import datetime
    import evdev
    import time
    from evdev import InputDevice, ecodes, ff
    import RPi.GPIO as GPIO
    
    # DB 종료
    def closeDB(signal, frame):
        print("BYE")
        GPIO.cleanup()
        sense.clear()
        cur.close()
        db.close()
        timer.cancel()
        mh.getMotor(1).run(Raspi_MotorHAT.RELEASE)
        timer2.cancel()
        sys.exit(0)
    
    # polling for command 처리 + rc car hp status update + 속력 방향 업데이트(예정)
    def polling():
        global cur, db, ready, car, car_hp_left, car_hp_right, car_hp_back, game_round, car_speed, car_direction
        lock.acquire() # Mutex lock
        # process received command from GUI
        cur.execute("select * from command where car=2 order by time desc limit 1")
        for (id, time, v_car, cmd_string, cmd_value, is_finish) in cur:
            if is_finish == 1 : break
            ready = (cmd_string, cmd_value)
            cur.execute("update command set is_finish=1 where is_finish=0")
        # update rc car hp status
        cur.execute("select * from score_log where car=2 order by time desc limit 1")
        for (id, time, v_round, v_car, hp_left, hp_right, hp_back, factor) in cur:
            game_round = v_round
            car_hp_left = hp_left
            car_hp_right = hp_right
            car_hp_back = hp_back
        # print(f"local hp left: {car_hp_left}")
        # print(f"local hp right: {car_hp_right}")
        # print(f"local hp back: {car_hp_back}")
        # print("===============================")
        # update velocity_log
        c_time = datetime.datetime.now()
        query = "insert into velocity_log(time, car, speed, direction) values (%s, %s, %s, %s)"
        value = (c_time, car, car_speed, car_direction)
        cur.execute(query, value)
        db.commit()
        lock.release() # Mutex unlock
         
        global timer
        timer = Timer(0.1, polling)
        timer.start()
    
    # polling for 데미지 처리 (버튼 처리)
    def polling_damaged():
        global btn_left, btn_right, btn_back
        # if btn_left.is_pressed:
        if GPIO.input(BUTTON_PIN_LEFT) == GPIO.LOW:
            print("left damaged")
            vibrate_controller(1000)
            log_damaged("left")
            sleep(5) # 충돌은 5초마다 1번씩만 카운팅
        # if btn_right.is_pressed:
        if GPIO.input(BUTTON_PIN_RIGHT) == GPIO.LOW:
            print("right damaged")
            vibrate_controller(1000)
            log_damaged("right")
            sleep(5)
        # if btn_back.is_pressed:
        if GPIO.input(BUTTON_PIN_BACK) == GPIO.LOW:
            print("back damaged")
            vibrate_controller(1000)
            log_damaged("back")
            sleep(5)
        
        global timer2
        timer2 = Timer(0.05, polling_damaged)
        timer2.start()
    
    # db에 데미지 기록
    def log_damaged(direction):
        global cur, db, game_round, car, car_hp_left, car_hp_right, car_hp_back
        time = datetime.datetime.now()
        if direction == "left":
            if car_hp_left > 0:
                car_hp_left -= 1
            else:
                return
        elif direction == "right":
            if car_hp_right > 0:
                car_hp_right -= 1
            else:
                return
        elif direction == "back":
            if car_hp_back > 0:
                car_hp_back -= 1
            else:
                return
        hp_left = car_hp_left
        hp_right = car_hp_right
        hp_back = car_hp_back
        query = "insert into score_log(time, round, car, hp_left, hp_right, hp_back, factor) values (%s, %s, %s, %s, %s, %s, %s)"
        value = (time, game_round, car, hp_left, hp_right, hp_back, 1) # 게임 내 득점인 경우 factor=1
        lock.acquire() # Mutex lock
        cur.execute(query, value)
        db.commit()
        lock.release() # Mutex unlock
    
    # xboxController 수신
    def joystick_polling():
        global device_path, ready
        try:
            joystick = evdev.InputDevice(device_path)
    
            print(f'Listening on {joystick.path}, device: {joystick.name}')
    
            for event in joystick.read_loop():
                # 컨트롤러 버튼 입력 감지 (버튼은 수치 값이 없음 )
                if event.type == evdev.ecodes.EV_KEY:
                    key_event = evdev.categorize(event)
                    if key_event.keycode == "BTN_TR":
                        ready = ("stop", 0)
                # 컨트롤러 스틱, 트리거 (수치 값이 있음)
                if event.type == evdev.ecodes.EV_ABS:
                    abs_event = evdev.categorize(event)
                    # print(f'Axis: {evdev.ecodes.ABS[abs_event.event.code]}, {abs_event.event.code}, Value: {abs_event.event.value}')
                    # 트리거 처리
                    if evdev.ecodes.ABS[abs_event.event.code] == 'ABS_GAS': # 우측 아래 트리거 / 최소 0 / 최대 1023 - 전진
                        gas_value = int(abs_event.event.value) / 1023
                        ready = ("go", gas_value)
                    elif  evdev.ecodes.ABS[abs_event.event.code] == 'ABS_BRAKE': # 좌측 아래 트리거 / 최소 0 / 최대 1023 - 후진
                        brake_value = int(abs_event.event.value) / 1023
                        ready = ("back", brake_value)
                    # 왼쪽 스틱 - 좌우 조향
                    elif evdev.ecodes.ABS[abs_event.event.code] == 'ABS_X': # 좌측 스틱 / 최소 0 (왼쪽) / 최대 65,535 (오른쪽) / 중앙 32,767
                        x_value = int(abs_event.event.value) / 65535
                        ready = ("steer", x_value)
        except KeyboardInterrupt:
            print("Joystick polling interrupted by user.")
        finally:
            print("Cleaning up joystick polling...")
    
    # xboxcontroller 진동 전송
    def vibrate_controller(duration_ms):
        controller = InputDevice(device_path)
    
        rumble = ff.Rumble(strong_magnitude=0xFFFF, weak_magnitude=0xFFFF)
        effect_type = ff.EffectType(ff_rumble_effect=rumble)
        # duration_ms = 1000  # 진동 지속 시간 (밀리초)
        effect = ff.Effect(
            ecodes.FF_RUMBLE, -1, 0,
            ff.Trigger(0, 0),
            ff.Replay(duration_ms, 0),
            effect_type
        )
    
        effect_id = controller.upload_effect(effect)
        controller.write(ecodes.EV_FF, effect_id, 1)
        time.sleep(duration_ms / 1000)
        controller.write(ecodes.EV_FF, effect_id, 0)
        controller.erase_effect(effect_id)
    
    # senseHAT LED
    def sensehatPrint(word):
        X = [255, 0, 0]  # Red
        O = [0, 0, 0]  # White
        matrix = ""
        if word == "go":
            matrix = [
                O, O, O, X, X, O, O, O,
                O, O, X, X, X, X, O, O,
                O, X, X, X, X, X, X, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O
            ]
        elif word == "back":
            matrix = [
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, O, O, X, X, O, O, O,
                O, X, X, X, X, X, X, O,
                O, O, X, X, X, X, O, O,
                O, O, O, X, X, O, O, O
            ]
        elif word == "stop":
            matrix = [
                O, O, X, X, X, X, O, O,
                O, X, O, O, O, O, X, O,
                X, O, X, O, O, O, O, X,
                X, O, O, X, O, O, O, X,
                X, O, O, O, X, O, O, X,
                X, O, O, O, O, X, O, X,
                O, X, O, O, O, O, X, O,
                O, O, X, X, X, X, O, O
            ]
        elif word == "right":
            matrix = [
                O, O, O, O, O, O, O, O,
                O, O, O, O, O, X, O, O,
                O, O, O, O, O, X, X, O,
                X, X, X, X, X, X, X, X,
                X, X, X, X, X, X, X, X,
                O, O, O, O, O, X, X, O,
                O, O, O, O, O, X, O, O,
                O, O, O, O, O, O, O, O
            ]
        elif word == "left":
            matrix = [
                O, O, O, O, O, O, O, O,
                O, O, X, O, O, O, O, O,
                O, X, X, O, O, O, O, O,
                X, X, X, X, X, X, X, X,
                X, X, X, X, X, X, X, X,
                O, X, X, O, O, O, O, O,
                O, O, X, O, O, O, O, O,
                O, O, O, O, O, O, O, O
            ]
        sense.set_pixels(matrix)
    
    # 차량 동작 코드 - 앞
    def go(cmd_value):
        global MAX_SPEED, car_speed
        speed = round(MAX_SPEED * cmd_value)
        myMotor.setSpeed(speed)
        myMotor.run(Raspi_MotorHAT.FORWARD)
        car_speed = round(cmd_value * 100) 
        sensehatPrint("go")
    # 차량 동작 코드 - 뒤
    def back(cmd_value):
        global MAX_SPEED, car_speed
        speed = round(MAX_SPEED * cmd_value)
        myMotor.setSpeed(speed)
        myMotor.run(Raspi_MotorHAT.BACKWARD)
        car_speed = -(round(cmd_value * 100))
        sensehatPrint("back")
    # 차량 동작 코드 - 정지 (속도 방향 초기화)
    def stop():
        global MIN_SERVO, MAX_SERVO, car_speed, car_direction
        myMotor.run(Raspi_MotorHAT.RELEASE)
        steering = round(0.5 * (MAX_SERVO - MIN_SERVO) + MIN_SERVO)
        servo.setPWM(0, 0, steering)
        car_speed = 0
        car_direction = 0
        sensehatPrint("stop")
        # vibrate_controller()
    # 차량 동작 코드 - 조타
    def steer(cmd_value):
        global MIN_SERVO, MAX_SERVO, car_direction
        steering = round((MAX_SERVO - MIN_SERVO) * cmd_value + MIN_SERVO)
        servo.setPWM(0, 0, steering)
        car_direction = round(cmd_value * 200 - 100) 
        if steering < 300:
            sensehatPrint("left")
        elif steering > 360:
            sensehatPrint("right")
    
    \#init
    \#xboxcontroller 경로 - evtest에서 확인
    device_path = '/dev/input/event5'
    # 차량 정보
    car = 2
    # 차량 정보 - score_log
    car_hp_left = 1
    car_hp_right = 1
    car_hp_back = 1
    game_round = 1
    # 차량 정보 - velocity_log
    MAX_SPEED = 255
    MIN_SERVO = 230
    MAX_SERVO = 430
    car_speed = 0 # -100 ~ 100
    car_direction = 0 # -100 ~ 100
    
    # DB
    db = mysql.connector.connect(host='3.35.169.119', user='mincoding', password='1234', database='minDB', auth_plugin='mysql_native_password')
    cur = db.cursor()
    ready = None
    
    # 모터
    mh = Raspi_MotorHAT(addr=0x6f)
    myMotor = mh.getMotor(1) #핀번호
    # 서보모터
    servo = PWM(0x6F) # 330 netutral
    servo.setPWMFreq(60)  # Set frequency to 60 Hz
    
    # sensehat
    sense = SenseHat()
    sense.set_rotation(270)
    
    # 버튼 핀 번호 설정
    BUTTON_PIN_LEFT = 17
    BUTTON_PIN_RIGHT = 27
    BUTTON_PIN_BACK = 22
    # GPIO 핀 번호 모드 설정
    GPIO.setmode(GPIO.BCM)
    # 버튼 핀을 입력으로 설정
    GPIO.setup(BUTTON_PIN_LEFT, GPIO.IN, pull_up_down=GPIO.PUD_UP)
    GPIO.setup(BUTTON_PIN_RIGHT, GPIO.IN, pull_up_down=GPIO.PUD_UP)
    GPIO.setup(BUTTON_PIN_BACK, GPIO.IN, pull_up_down=GPIO.PUD_UP)
    # btn_left = Button(BUTTON_PIN_LEFT, pull_up=True)
    # btn_right = Button(BUTTON_PIN_RIGHT, pull_up=True)
    # btn_back = Button(BUTTON_PIN_BACK, pull_up=True)
    
    
    # Mutex - sensing과 polling 메서드 두 쓰레드가 동시에 DB에 접근, 충돌 방지
    lock = Lock()
    # polling for  GUI 제어기 신호처리
    timer = None
    polling()
    # polling for 범퍼 데미지 감지 
    timer2 = None
    polling_damaged()
    
    # 조이스틱 폴링 스레드 시작
    joystick_thread = Thread(target=joystick_polling)
    joystick_thread.start()
    
    # 종료
    signal.signal(signal.SIGINT, closeDB)
    
    # main thread 실제로 차량 작동
    while True:
        sleep(0.1)
        if ready == None : continue
    
        cmd, cmd_value = ready # (cmd에 해당하는 string, cmd의 강도 0 ~ 1사이의 값)
        ready = None
    
        if cmd == "go" : go(cmd_value)
        if cmd == "back" : back(cmd_value)
        if cmd == "stop" : stop()
        if cmd == "steer" : steer(cmd_value)
    ```
    

- [x] 버튼 (데미지 처리)
    - [x] 버튼 처리하는 polling 생성
    - [x] 버튼 눌렀을 경우 컨트롤러 진동
    - [x] 버튼 눌렀을 경우 score_log에 data insert
    - [x] 버튼 눌렸을 경우에 5초간 버튼 입력 중지
- [x] 속도
    - [x] 컨트롤러에서 누르는 감도에 따라서 속력 서서히 변화
    - [x] 컨트롤러 스틱 감도에 따라서 방향 서서히 변화
    - [x] 속도 기록할 데이터 베이스 velocity_log 생성
    - [x] 데이터 베이스에 속도 정보 insert
- [ ] 해야하는 것
    - [ ] 데미지에 따라서 senseHAT 화면 변화
    - [x] 뒷바퀴 축이랑 바퀴 고정하기 (빠져서 앞뒤로 안움직임)
    - [x] 버튼 케이블 차량에 단단히 고정할 방법 찾기
    - [x] 다른 차량에 코드 셋팅
    - [ ] 게임이 끝난 경우 (한쪽의 체력이 0이 된 경우) 죽음 처리

  

## GUI

- main.py
    
    ```Python
    from PySide2.QtWidgets import *
    from PySide2.QtCore import *
    from mainUI import Ui_MainWindow
    import mysql.connector
    
    
    class MyApp(QMainWindow, Ui_MainWindow):
        def __init__(self):
            super().__init__()
            self.setupUi(self)
            self.init()
    
        def init(self):
            print("INIT")
            \#MySQL 접속 코드
            self.db = mysql.connector.connect(host='3.35.169.119', user='mincoding', password='1234', database='minDB', auth_plugin='mysql_native_password')
            self.cur = self.db.cursor()
            # Game info (local)
            self.v_round = 0
            self.v_car1_hp_left = 0
            self.v_car1_hp_back = 0
            self.v_car1_hp_right = 0
            self.v_car2_hp_left = 0
            self.v_car2_hp_back = 0
            self.v_car2_hp_right = 0
    
            \#timer setting
            self.timer = QTimer()
            self.timer.setInterval(100) \#500ms
            self.timer.timeout.connect(self.pollingQuery)
            self.timer.start()
    
        def pollingQuery(self):
            # Car1 체력 업데이트
            self.cur.execute("select * from score_log WHERE car = 1 order by time desc limit 1")
            for (id, time, round, car, hp_left, hp_right, hp_back, factor) in self.cur:
                self.v_car1_hp_left = hp_left
                self.v_car1_hp_back = hp_back
                self.v_car1_hp_right = hp_right
    
            # Car2 체력 업데이트
            self.cur.execute("select * from score_log WHERE car = 2 order by time desc limit 1")
            for (id, time, round, car, hp_left, hp_right, hp_back, factor) in self.cur:
                self.v_car2_hp_left = hp_left
                self.v_car2_hp_back = hp_back
                self.v_car2_hp_right = hp_right
                # 라운드 업데이트
                self.v_round = round
                # str = "%5d | %s | %6s | %6s | %4d" % (id, time.strftime("%Y%m%d %H:%M:%S"), cmd_string, arg_string, is_finish)
                # self.textBrowser.append(str)
            self.db.commit()
            # GUI 업데이트
            self.car1_hp_left.setText(str(self.v_car1_hp_left))
            self.car1_hp_back.setText(str(self.v_car1_hp_back))
            self.car1_hp_right.setText(str(self.v_car1_hp_right))
            self.car2_hp_left.setText(str(self.v_car2_hp_left))
            self.car2_hp_back.setText(str(self.v_car2_hp_back))
            self.car2_hp_right.setText(str(self.v_car2_hp_right))
    
        # def btnStart(self):
        #     print("Start")
        #     \#Timer Start
        #     self.timer.start()
        #
        #
        #     # sensingTable 정보도 가져오기
        #     # 최근 15개 정보만 가져오기
        #     self.cur.execute("select * from sensing order by time desc limit 15")
        #     self.textBrowser_2.clear()
        #     for (id, time, num1, num2, num3, meta_string, is_finish) in self.cur:
        #         str = "%d | %s | %6s | %6s | %6s | %15s | %4d" % (
        #         id, time.strftime("%Y%m%d %H:%M:%S"), num1, num2, num3, meta_string, is_finish)
        #         self.textBrowser_2.append(str)
        #     self.db.commit()
    
        def insertScoreLog(self, round, car, hp_left, hp_right, hp_back, factor):
            print("ok")
            time = QDateTime().currentDateTime().toPython()
            query = "insert into score_log(time, round, car, hp_left, hp_right, hp_back, factor) values (%s, %s, %s, %s, %s, %s, %s)"
            value = (time, round, car, hp_left, hp_right, hp_back, factor)
            print(value)
            self.cur.execute(query, value)
            print("ok")
            self.db.commit()
    
        def insertCommand(self, car, cmd_string, cmd_value):
            # 현재 시간 가져오기
            time = QDateTime().currentDateTime().toPython()
            is_finish = 0
    
            query = "insert into command(time, car, cmd_string, cmd_value, is_finish) values (%s, %s, %s, %s, %s)"
            value = (time, car, cmd_string, cmd_value, is_finish)
    
            self.cur.execute(query, value)
            self.db.commit()
        # New Game Start!
        def btnGameStart(self):
            self.v_round += 1
            self.insertScoreLog(self.v_round, 1, 3, 3, 3, 2)
            self.insertScoreLog(self.v_round, 2, 3, 3, 3, 2)
            print("New Game Start!")
    
        # 차량에 command
        # Car1
        def btnCar1Go(self):
            print("car1 go")
            self.insertCommand(1, "go", 0.4)
    
        def btnCar1Left(self):
            print("car1 left")
            self.insertCommand(1, "steer", 0)
    
        def btnCar1Stop(self):
            print("car1 stop")
            self.insertCommand(1, "stop", 1)
    
        def btnCar1Right(self):
            print("car1 right")
            self.insertCommand(1, "steer", 0.99)
    
        def btnCar1Back(self):
            print("car1 back")
            self.insertCommand(1, "back", 0.4)
        # Car2
        def btnCar2Go(self):
            print("car2 go")
            self.insertCommand(2, "go", 0.4)
    
        def btnCar2Left(self):
            print("car2 left")
            self.insertCommand(2, "steer", 0)
    
        def btnCar2Stop(self):
            print("car2 stop")
            self.insertCommand(2, "stop", 1)
    
        def btnCar2Right(self):
            print("car2 right")
            self.insertCommand(2, "steer", 0.99)
    
        def btnCar2Back(self):
            print("car2 back")
            self.insertCommand(2, "back", 0.4)
    
        # 차량 체력 정보 수정 Car1
        def btnCar1HpLeftUp(self):
            self.v_car1_hp_left += 1
            print("car1 hp left up")
            self.insertScoreLog(self.v_round, 1, self.v_car1_hp_left, self.v_car1_hp_right, self.v_car1_hp_back, 2)
    
        def btnCar1HpLeftDown(self):
            self.v_car1_hp_left -= 1
            print("car1 hp left down")
            self.insertScoreLog(self.v_round, 1, self.v_car1_hp_left, self.v_car1_hp_right, self.v_car1_hp_back, 2)
    
        def btnCar1HpBackUp(self):
            self.v_car1_hp_back += 1
            print("car1 hp back up")
            self.insertScoreLog(self.v_round, 1, self.v_car1_hp_left, self.v_car1_hp_right, self.v_car1_hp_back, 2)
    
        def btnCar1HpBackDown(self):
            self.v_car1_hp_back -= 1
            print("car1 hp back down")
            self.insertScoreLog(self.v_round, 1, self.v_car1_hp_left, self.v_car1_hp_right, self.v_car1_hp_back, 2)
    
        def btnCar1HpRightUp(self):
            self.v_car1_hp_right += 1
            print("car1 hp right up")
            self.insertScoreLog(self.v_round, 1, self.v_car1_hp_left, self.v_car1_hp_right, self.v_car1_hp_back, 2)
    
        def btnCar1HpRightDown(self):
            self.v_car1_hp_right -= 1
            print("car1 hp right down")
            self.insertScoreLog(self.v_round, 1, self.v_car1_hp_left, self.v_car1_hp_right, self.v_car1_hp_back, 2)
    
        # 차량 체력 정보 수정 Car2
        def btnCar2HpLeftUp(self):
            self.v_car2_hp_left += 1
            print("car2 hp left up")
            self.insertScoreLog(self.v_round, 2, self.v_car2_hp_left, self.v_car2_hp_right, self.v_car2_hp_back, 2)
    
        def btnCar2HpLeftDown(self):
            self.v_car2_hp_left -= 1
            print("car2 hp left down")
            self.insertScoreLog(self.v_round, 2, self.v_car2_hp_left, self.v_car2_hp_right, self.v_car2_hp_back, 2)
    
        def btnCar2HpBackUp(self):
            self.v_car2_hp_back += 1
            print("car2 hp back up")
            self.insertScoreLog(self.v_round, 2, self.v_car2_hp_left, self.v_car2_hp_right, self.v_car2_hp_back, 2)
    
        def btnCar2HpBackDown(self):
            self.v_car2_hp_back -= 1
            print("car2 hp back down")
            self.insertScoreLog(self.v_round, 2, self.v_car2_hp_left, self.v_car2_hp_right, self.v_car2_hp_back, 2)
    
        def btnCar2HpRightUp(self):
            self.v_car2_hp_right += 1
            print("car2 hp right up")
            self.insertScoreLog(self.v_round, 2, self.v_car2_hp_left, self.v_car2_hp_right, self.v_car2_hp_back, 2)
    
        def btnCar2HpRightDown(self):
            self.v_car2_hp_right -= 1
            print("car2 hp right down")
            self.insertScoreLog(self.v_round, 2, self.v_car2_hp_left, self.v_car2_hp_right, self.v_car2_hp_back, 2)
    
    
        def closeEvent(self, event):
            event.accept()
            #접속 종료
            self.cur.close()
            self.db.close()
    
    if __name__ == '__main__':
        app = QApplication()
        win = MyApp()
        win.show()
        app.exec_()
    ```
    
- mainUI.py
    
    ```Python
    # -*- coding: utf-8 -*-
    
    ################################################################################
    ## Form generated from reading UI file 'untitled.ui'
    ##
    ## Created by: Qt User Interface Compiler version 6.7.0
    ##
    ## WARNING! All changes made in this file will be lost when recompiling UI file!
    ################################################################################
    
    from PySide2.QtCore import (QCoreApplication, QDate, QDateTime, QLocale,
        QMetaObject, QObject, QPoint, QRect,
        QSize, QTime, QUrl, Qt)
    from PySide2.QtGui import (QBrush, QColor, QConicalGradient, QCursor,
        QFont, QFontDatabase, QGradient, QIcon,
        QImage, QKeySequence, QLinearGradient, QPainter,
        QPalette, QPixmap, QRadialGradient, QTransform)
    from PySide2.QtWidgets import (QApplication, QFrame, QGridLayout, QLabel,
        QMainWindow, QMenuBar, QPushButton, QSizePolicy,
        QStatusBar, QVBoxLayout, QWidget)
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            if not MainWindow.objectName():
                MainWindow.setObjectName(u"MainWindow")
            MainWindow.resize(800, 430)
            MainWindow.setContextMenuPolicy(Qt.ContextMenuPolicy.PreventContextMenu)
            self.centralwidget = QWidget(MainWindow)
            self.centralwidget.setObjectName(u"centralwidget")
            self.vboxLayout = QVBoxLayout(self.centralwidget)
            self.vboxLayout.setObjectName(u"vboxLayout")
            self.pushButton = QPushButton(self.centralwidget)
            self.pushButton.setObjectName(u"pushButton")
    
            self.vboxLayout.addWidget(self.pushButton)
    
            self.gridLayout = QGridLayout()
            self.gridLayout.setObjectName(u"gridLayout")
            self.frame_2 = QFrame(self.centralwidget)
            self.frame_2.setObjectName(u"frame_2")
            self.frame_2.setFrameShape(QFrame.Shape.StyledPanel)
            self.frame_2.setFrameShadow(QFrame.Shadow.Raised)
            self.label_2 = QLabel(self.frame_2)
            self.label_2.setObjectName(u"label_2")
            self.label_2.setGeometry(QRect(10, 10, 251, 16))
            self.btn_car2_left = QPushButton(self.frame_2)
            self.btn_car2_left.setObjectName(u"btn_car2_left")
            self.btn_car2_left.setGeometry(QRect(60, 260, 75, 24))
            self.btn_car2_go = QPushButton(self.frame_2)
            self.btn_car2_go.setObjectName(u"btn_car2_go")
            self.btn_car2_go.setGeometry(QRect(150, 220, 75, 24))
            self.btn_car2_right = QPushButton(self.frame_2)
            self.btn_car2_right.setObjectName(u"btn_car2_right")
            self.btn_car2_right.setGeometry(QRect(240, 260, 75, 24))
            self.btn_car2_back = QPushButton(self.frame_2)
            self.btn_car2_back.setObjectName(u"btn_car2_back")
            self.btn_car2_back.setGeometry(QRect(150, 300, 75, 24))
            self.btn_car2_stop = QPushButton(self.frame_2)
            self.btn_car2_stop.setObjectName(u"btn_car2_stop")
            self.btn_car2_stop.setGeometry(QRect(150, 260, 75, 24))
            self.label_20 = QLabel(self.frame_2)
            self.label_20.setObjectName(u"label_20")
            self.label_20.setGeometry(QRect(10, 80, 21, 16))
            self.label_18 = QLabel(self.frame_2)
            self.label_18.setObjectName(u"label_18")
            self.label_18.setGeometry(QRect(160, 160, 21, 16))
            self.btn_car2_hp_left_down = QPushButton(self.frame_2)
            self.btn_car2_hp_left_down.setObjectName(u"btn_car2_hp_left_down")
            self.btn_car2_hp_left_down.setGeometry(QRect(60, 90, 50, 24))
            self.btn_car2_hp_right_up = QPushButton(self.frame_2)
            self.btn_car2_hp_right_up.setObjectName(u"btn_car2_hp_right_up")
            self.btn_car2_hp_right_up.setGeometry(QRect(320, 60, 50, 24))
            self.btn_car2_hp_back_up = QPushButton(self.frame_2)
            self.btn_car2_hp_back_up.setObjectName(u"btn_car2_hp_back_up")
            self.btn_car2_hp_back_up.setGeometry(QRect(210, 140, 50, 24))
            self.car2_hp_left = QLabel(self.frame_2)
            self.car2_hp_left.setObjectName(u"car2_hp_left")
            self.car2_hp_left.setGeometry(QRect(40, 80, 21, 16))
            self.label_17 = QLabel(self.frame_2)
            self.label_17.setObjectName(u"label_17")
            self.label_17.setGeometry(QRect(270, 80, 21, 16))
            self.btn_car2_hp_right_down = QPushButton(self.frame_2)
            self.btn_car2_hp_right_down.setObjectName(u"btn_car2_hp_right_down")
            self.btn_car2_hp_right_down.setGeometry(QRect(320, 90, 50, 24))
            self.car2_hp_back = QLabel(self.frame_2)
            self.car2_hp_back.setObjectName(u"car2_hp_back")
            self.car2_hp_back.setGeometry(QRect(190, 160, 21, 16))
            self.label_5 = QLabel(self.frame_2)
            self.label_5.setObjectName(u"label_5")
            self.label_5.setGeometry(QRect(170, 30, 51, 91))
            self.label_5.setPixmap(QPixmap(u"image/car2.jpg"))
            self.label_5.setScaledContents(True)
            self.btn_car2_hp_left_up = QPushButton(self.frame_2)
            self.btn_car2_hp_left_up.setObjectName(u"btn_car2_hp_left_up")
            self.btn_car2_hp_left_up.setGeometry(QRect(60, 60, 50, 24))
            self.btn_car2_hp_back_down = QPushButton(self.frame_2)
            self.btn_car2_hp_back_down.setObjectName(u"btn_car2_hp_back_down")
            self.btn_car2_hp_back_down.setGeometry(QRect(210, 170, 50, 24))
            self.car2_hp_right = QLabel(self.frame_2)
            self.car2_hp_right.setObjectName(u"car2_hp_right")
            self.car2_hp_right.setGeometry(QRect(300, 80, 21, 16))
    
            self.gridLayout.addWidget(self.frame_2, 0, 1, 1, 1)
    
            self.frame = QFrame(self.centralwidget)
            self.frame.setObjectName(u"frame")
            self.frame.setFrameShape(QFrame.Shape.StyledPanel)
            self.frame.setFrameShadow(QFrame.Shadow.Raised)
            self.label = QLabel(self.frame)
            self.label.setObjectName(u"label")
            self.label.setGeometry(QRect(10, 10, 121, 16))
            self.btn_car1_go = QPushButton(self.frame)
            self.btn_car1_go.setObjectName(u"btn_car1_go")
            self.btn_car1_go.setGeometry(QRect(140, 220, 75, 24))
            self.btn_car1_stop = QPushButton(self.frame)
            self.btn_car1_stop.setObjectName(u"btn_car1_stop")
            self.btn_car1_stop.setGeometry(QRect(140, 260, 75, 24))
            self.btn_car1_back = QPushButton(self.frame)
            self.btn_car1_back.setObjectName(u"btn_car1_back")
            self.btn_car1_back.setGeometry(QRect(140, 300, 75, 24))
            self.btn_car1_left = QPushButton(self.frame)
            self.btn_car1_left.setObjectName(u"btn_car1_left")
            self.btn_car1_left.setGeometry(QRect(50, 260, 75, 24))
            self.btn_car1_right = QPushButton(self.frame)
            self.btn_car1_right.setObjectName(u"btn_car1_right")
            self.btn_car1_right.setGeometry(QRect(230, 260, 75, 24))
            self.label_3 = QLabel(self.frame)
            self.label_3.setObjectName(u"label_3")
            self.label_3.setGeometry(QRect(170, 30, 51, 91))
            self.label_3.setPixmap(QPixmap(u"image/car1.jpg"))
            self.label_3.setScaledContents(True)
            self.label_4 = QLabel(self.frame)
            self.label_4.setObjectName(u"label_4")
            self.label_4.setGeometry(QRect(10, 80, 21, 16))
            self.car1_hp_left = QLabel(self.frame)
            self.car1_hp_left.setObjectName(u"car1_hp_left")
            self.car1_hp_left.setGeometry(QRect(40, 80, 21, 16))
            self.btn_car1_hp_left_up = QPushButton(self.frame)
            self.btn_car1_hp_left_up.setObjectName(u"btn_car1_hp_left_up")
            self.btn_car1_hp_left_up.setGeometry(QRect(60, 60, 50, 24))
            self.btn_car1_hp_left_down = QPushButton(self.frame)
            self.btn_car1_hp_left_down.setObjectName(u"btn_car1_hp_left_down")
            self.btn_car1_hp_left_down.setGeometry(QRect(60, 90, 50, 24))
            self.car1_hp_right = QLabel(self.frame)
            self.car1_hp_right.setObjectName(u"car1_hp_right")
            self.car1_hp_right.setGeometry(QRect(300, 80, 21, 16))
            self.btn_car1_hp_right_up = QPushButton(self.frame)
            self.btn_car1_hp_right_up.setObjectName(u"btn_car1_hp_right_up")
            self.btn_car1_hp_right_up.setGeometry(QRect(320, 60, 50, 24))
            self.btn_car1_hp_right_down = QPushButton(self.frame)
            self.btn_car1_hp_right_down.setObjectName(u"btn_car1_hp_right_down")
            self.btn_car1_hp_right_down.setGeometry(QRect(320, 90, 50, 24))
            self.label_12 = QLabel(self.frame)
            self.label_12.setObjectName(u"label_12")
            self.label_12.setGeometry(QRect(270, 80, 21, 16))
            self.car1_hp_back = QLabel(self.frame)
            self.car1_hp_back.setObjectName(u"car1_hp_back")
            self.car1_hp_back.setGeometry(QRect(190, 160, 21, 16))
            self.btn_car1_hp_back_up = QPushButton(self.frame)
            self.btn_car1_hp_back_up.setObjectName(u"btn_car1_hp_back_up")
            self.btn_car1_hp_back_up.setGeometry(QRect(210, 140, 50, 24))
            self.btn_car1_hp_back_down = QPushButton(self.frame)
            self.btn_car1_hp_back_down.setObjectName(u"btn_car1_hp_back_down")
            self.btn_car1_hp_back_down.setGeometry(QRect(210, 170, 50, 24))
            self.label_14 = QLabel(self.frame)
            self.label_14.setObjectName(u"label_14")
            self.label_14.setGeometry(QRect(160, 160, 21, 16))
    
            self.gridLayout.addWidget(self.frame, 0, 0, 1, 1)
    
    
            self.vboxLayout.addLayout(self.gridLayout)
    
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QMenuBar(MainWindow)
            self.menubar.setObjectName(u"menubar")
            self.menubar.setGeometry(QRect(0, 0, 800, 22))
            MainWindow.setMenuBar(self.menubar)
            self.statusbar = QStatusBar(MainWindow)
            self.statusbar.setObjectName(u"statusbar")
            MainWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(MainWindow)
            self.btn_car1_go.clicked.connect(MainWindow.btnCar1Go)
            self.btn_car1_left.clicked.connect(MainWindow.btnCar1Left)
            self.btn_car1_stop.clicked.connect(MainWindow.btnCar1Stop)
            self.btn_car1_right.clicked.connect(MainWindow.btnCar1Right)
            self.btn_car1_back.clicked.connect(MainWindow.btnCar1Back)
            self.btn_car1_hp_left_up.clicked.connect(MainWindow.btnCar1HpLeftUp)
            self.btn_car1_hp_left_down.clicked.connect(MainWindow.btnCar1HpLeftDown)
            self.btn_car1_hp_back_up.clicked.connect(MainWindow.btnCar1HpBackUp)
            self.btn_car1_hp_back_down.clicked.connect(MainWindow.btnCar1HpBackDown)
            self.btn_car1_hp_right_down.clicked.connect(MainWindow.btnCar1HpRightDown)
            self.btn_car1_hp_right_up.clicked.connect(MainWindow.btnCar1HpRightUp)
            self.btn_car2_go.clicked.connect(MainWindow.btnCar2Go)
            self.btn_car2_left.clicked.connect(MainWindow.btnCar2Left)
            self.btn_car2_stop.clicked.connect(MainWindow.btnCar2Stop)
            self.btn_car2_hp_right_down.clicked.connect(MainWindow.btnCar2HpRightDown)
            self.btn_car2_hp_right_up.clicked.connect(MainWindow.btnCar2HpRightUp)
            self.btn_car2_right.clicked.connect(MainWindow.btnCar2Right)
            self.btn_car2_back.clicked.connect(MainWindow.btnCar2Back)
            self.btn_car2_hp_left_up.clicked.connect(MainWindow.btnCar2HpLeftUp)
            self.btn_car2_hp_left_down.clicked.connect(MainWindow.btnCar2HpLeftDown)
            self.btn_car2_hp_back_up.clicked.connect(MainWindow.btnCar2HpBackUp)
            self.btn_car2_hp_back_down.clicked.connect(MainWindow.btnCar2HpBackDown)
            self.pushButton.clicked.connect(MainWindow.btnGameStart)
    
            QMetaObject.connectSlotsByName(MainWindow)
        # setupUi
    
        def retranslateUi(self, MainWindow):
            MainWindow.setWindowTitle(QCoreApplication.translate("MainWindow", u"MainWindow", None))
            self.pushButton.setText(QCoreApplication.translate("MainWindow", u"New Game Start!", None))
            self.label_2.setText(QCoreApplication.translate("MainWindow", u"Car2", None))
            self.btn_car2_left.setText(QCoreApplication.translate("MainWindow", u"Left", None))
            self.btn_car2_go.setText(QCoreApplication.translate("MainWindow", u"Go", None))
            self.btn_car2_right.setText(QCoreApplication.translate("MainWindow", u"Right", None))
            self.btn_car2_back.setText(QCoreApplication.translate("MainWindow", u"Back", None))
            self.btn_car2_stop.setText(QCoreApplication.translate("MainWindow", u"Stop", None))
            self.label_20.setText(QCoreApplication.translate("MainWindow", u"HP:", None))
            self.label_18.setText(QCoreApplication.translate("MainWindow", u"HP:", None))
            self.btn_car2_hp_left_down.setText(QCoreApplication.translate("MainWindow", u"Down", None))
            self.btn_car2_hp_right_up.setText(QCoreApplication.translate("MainWindow", u"Up", None))
            self.btn_car2_hp_back_up.setText(QCoreApplication.translate("MainWindow", u"Up", None))
            self.car2_hp_left.setText(QCoreApplication.translate("MainWindow", u"0", None))
            self.label_17.setText(QCoreApplication.translate("MainWindow", u"HP:", None))
            self.btn_car2_hp_right_down.setText(QCoreApplication.translate("MainWindow", u"Down", None))
            self.car2_hp_back.setText(QCoreApplication.translate("MainWindow", u"0", None))
            self.label_5.setText("")
            self.btn_car2_hp_left_up.setText(QCoreApplication.translate("MainWindow", u"Up", None))
            self.btn_car2_hp_back_down.setText(QCoreApplication.translate("MainWindow", u"Down", None))
            self.car2_hp_right.setText(QCoreApplication.translate("MainWindow", u"0", None))
            self.label.setText(QCoreApplication.translate("MainWindow", u"Car1", None))
            self.btn_car1_go.setText(QCoreApplication.translate("MainWindow", u"Go", None))
            self.btn_car1_stop.setText(QCoreApplication.translate("MainWindow", u"Stop", None))
            self.btn_car1_back.setText(QCoreApplication.translate("MainWindow", u"Back", None))
            self.btn_car1_left.setText(QCoreApplication.translate("MainWindow", u"Left", None))
            self.btn_car1_right.setText(QCoreApplication.translate("MainWindow", u"Right", None))
            self.label_3.setText("")
            self.label_4.setText(QCoreApplication.translate("MainWindow", u"HP:", None))
            self.car1_hp_left.setText(QCoreApplication.translate("MainWindow", u"0", None))
            self.btn_car1_hp_left_up.setText(QCoreApplication.translate("MainWindow", u"Up", None))
            self.btn_car1_hp_left_down.setText(QCoreApplication.translate("MainWindow", u"Down", None))
            self.car1_hp_right.setText(QCoreApplication.translate("MainWindow", u"0", None))
            self.btn_car1_hp_right_up.setText(QCoreApplication.translate("MainWindow", u"Up", None))
            self.btn_car1_hp_right_down.setText(QCoreApplication.translate("MainWindow", u"Down", None))
            self.label_12.setText(QCoreApplication.translate("MainWindow", u"HP:", None))
            self.car1_hp_back.setText(QCoreApplication.translate("MainWindow", u"0", None))
            self.btn_car1_hp_back_up.setText(QCoreApplication.translate("MainWindow", u"Up", None))
            self.btn_car1_hp_back_down.setText(QCoreApplication.translate("MainWindow", u"Down", None))
            self.label_14.setText(QCoreApplication.translate("MainWindow", u"HP:", None))
        # retranslateUi
    
    ```
    

![[untitled.ui]]

- [x] QT 다시구성
    
    ![[Untitled 1 9.png|Untitled 1 9.png]]
    
- [x] 버튼에 함수 이어주기
- [x] 구동 command 보내주기
- [x] hp 정보 받아오기