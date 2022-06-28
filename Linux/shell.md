# shell
***

## shell의 기능과 종류

**셸은 사용자와 리눅스 커널 사이에서 중간자 역할을 수행**

### 셸의 기능

* 명령어 해석기 기능
* 프로그래밍 기능
* 사용자 환경 설정 기능

#### 명령어 해석기 기능

**셸은 사용자가 입력한 명령이나 파일에서 읽어들인 명령을 해석하고 적절한 프로그램 실행**
**사용자가 로그인을 하면 셸이 자동으로 실행되어 사용자가 명령을 입력하기를 기다림(명령을 기다리는 표시 -> 프롬프트)**

#### 프로그래밍 기능

**셸 자체 내에 프로그래밍 기능이 있어 프로그램 생성 가능**
**셸의 프로그래밍 기능을 이용하여 작성된 프로그램을 셸 스크립트라고 함**

#### 사용자 환경 설정 기능

**셸은 사용자 환경을 설정할 수 있도록 초기화 파일 기능 제공**
**명령을 찾아오는 경로 설정**
**파일과 디렉터리를 새로 생성할 때 기본 권한 설정**
**다양한 환경 변수 설정**

### 쉘의 종류

* 본 셸
* C 셸
* 콘 셸
* 배시 셸
* 대시 셸

***

## 셸 기본 사용법

### 셸 지정하고 바꾸기

**사용자 정보를 가지고 있는 파일(/etc/passwd)에서 특정 사용자의 정보를 찾아 사용 중인 셸의 종류 확인하기**

![check](https://user-images.githubusercontent.com/42503786/176118145-656bca16-b631-4e39-ac16-d3f36f901e87.png)

**가장 앞에 나온 정보가 로그인 ID 가장 마지막에 나온 /bin/bash가 사용자의 기본 셸**

#### 기본 셸 바꾸기

**chsh 명령어를 사용하여 사용자 로그인 셸 바꾸기**

**현재 바꿀 수 있는 셸의 종류는 /etc/shells 파일에 저장되어 있음**

![shell](https://user-images.githubusercontent.com/42503786/176118537-18d97d7d-41c9-44c3-b558-b1e5b2e62d7a.png)

**/bin/dash 셸로 바꾸기**
**sudo 명령어를 사용하고 tail /etc/passwd 명령어를 사용하여 사용자 기본 셸 확인**

![dash](https://user-images.githubusercontent.com/42503786/176119121-9108ea31-140c-4428-a6fb-a1c954c5f4e8.png)

**reboot한 후 사용자 기본 셸이 /bin/dash로 되어 있는지 확인**

![reboot](https://user-images.githubusercontent.com/42503786/176119581-f9be2334-6f85-43af-b82c-7cb0d83ded9c.png)

**서브 셸 만들고 /etc/passwd 파일에서 서브 셸로 변경되어 있는지 확인**

![change](https://user-images.githubusercontent.com/42503786/176120940-724b7a6d-40e8-4220-a71c-46648833bfb1.png)
***

### 셸 내장 명령

**셸은 자체적으로 내장 명령을 가지고 있음(대표적인 걸로 cd 명령어가 있음)**

**file 명령어를 이용하여 일반적인 실행파일이 어떻게 출력되는가**
**shared object나 executable로 출력되면 실행파일을 의미**
![hey](https://user-images.githubusercontent.com/42503786/176126120-bfd0b700-dacd-4a08-966a-97189d67172d.png)


### 출력하기

**bash 셸의 출력 명령으로 echo와 printf가 있음**

**echo 명령어를 사용하여 문자열 출력해보기**

![minsu](https://user-images.githubusercontent.com/42503786/176122173-2b23f82c-45c7-42ba-9087-b22910b450b4.png)

**printf 명령어를 사용하여 문자열 출력해보기(줄 바꿈(\n)을 하지 않으면 줄 바꿈되지 않은 채로 출력됨)**

![minsu1](https://user-images.githubusercontent.com/42503786/176122585-ccba7f87-85c8-4a79-bea9-bb94bcbea697.png)

### 특수문자 사용하기

**셸은 사용자가 더욱 편리하게 명명을 입력하고 실행할 수 있도록 다양한 특수문자를 제공**

**?,*,|,;,[],~,'',"",`` 주요 특수문자가 있음**

사용자가 명령을 입력하면 셸은 먼저 입력한 내용 중에 특수문자가 있는지 확인하고 해독하여 적절한 형태로 변경

#### 특수 문자 '*'

**임의의 문자열을 나타내는 특수문자 0개 이상의 문자로 대체됨**

**ls -F t* 명령어를 입력하여 파일명이 t로 시작하는 모든 파일의 이름과 파일 종류 출력해보기**

![lsF](https://user-images.githubusercontent.com/42503786/176123873-664f0910-afe7-4e00-bba0-aeefc20d9d67.png)

#### 특수 문자 '?'와 '[]'

**하나의 문자를 나타나는 데 사용**

**?는 길이가 1인 임의의 한 문자를 []는 괄호 안에 포함된 문자 중 하나를 나타냄**
현재 위치에 ls 명령어를 입력하여 어떤 파일이 있는지 확인하고 특수문자 ?를 이용하여 다시 출력해보기

![backup](https://user-images.githubusercontent.com/42503786/176125232-7622cc51-9b36-4e46-a1d6-41aad491c351.png)

특수문자 []를 사용하여 확인해보기

![backup1](https://user-images.githubusercontent.com/42503786/176125400-1df39d1e-4b6f-45ed-b2a1-4aac898727ab.png)

#### 특수문자 '~' 와 '-'

**디렉터리를 나타내는 특수문자 '~'만 사용하면 현재 작업 중인 사용자의 홈 디렉터리를 나타내고 '-'는 디렉터리를 이전하기 직전의 작업 디렉터리를 나타냄**


![check](https://user-images.githubusercontent.com/42503786/176125904-beae423b-d3b2-4c8e-9fbe-ffa3d32817b1.png)

#### 특수문자 ';'과 '|'

**명령과 명령을 연결 ';'는 연결된 명령을 왼쪽부터 차례로 실행 '|'는 왼쪽 명령의 실행 결과를 오른쪽 명령의 입력으로 전달**

왼쪽 date명령어부터 차례대로 실행

![connect](https://user-images.githubusercontent.com/42503786/176126645-538ad409-05a7-441e-acfe-d2dabf595baf.png)

루트 디렉터리에 있는 파일의 inode를 한 화면씩 출력 -> ls -l / 명령의 결과가 more 명령의 입력으로 전달

![connect1](https://user-images.githubusercontent.com/42503786/176126761-94ac2d2b-ce62-4e3b-99bb-9fcb187b14a5.png)

#### 특수문자 ''와 ""

**문자를 감싸서 문자열로 만들고 문자열 안에 사용된 특수문자의 기능을 없앰**

''특수문자를 사용하여 $SHELL 문자열 출력해보기

![step](https://user-images.githubusercontent.com/42503786/176127665-ffd04b58-64e4-4d45-97c7-e996a883a3ab.png)

""특수문자를 사용하여 쉘 변수에 저장된 값을 알아보기

![step1](https://user-images.githubusercontent.com/42503786/176127797-6947c580-22d1-402e-ba9d-930d75eee0bd.png)

#### 특수문자 ``(백쿼터)

**셸은 ``로 감싸인 문자열을 명령으로 해석해 명령의 실행결과로 바뀌게 됨**

``로 감싼 date가 명령으로 해석되어 date 명령의 실행되는지 확인해보기

![date](https://user-images.githubusercontent.com/42503786/176128489-1cc06e18-53f9-466f-bc6b-d095175af0d0.png)

#### 특수문자 \

**특수문자 바로 앞에 사용해 해당 특수문자의 효과를 없애고 일반 문자처럼 처리**

특수문자 \를 사용하여 비교해보기

![differ](https://user-images.githubusercontent.com/42503786/176129049-a01b06b7-e001-4089-9aab-64fb5053d455.png)

#### 특수문자 >

**입출력의 방향을 바꾸는 특수문자**

ls -l 명령의 실행 결과를 test.txt 파일에 저장해보기

![redir](https://user-images.githubusercontent.com/42503786/176130058-ff64c708-5866-4208-9569-3c48c009e88c.png)


















