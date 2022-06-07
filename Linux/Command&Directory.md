## 목차
+ **리눅스 명령 사용**

  + 명령 행 편집 방법
  
  + 기초 명령 사용법
  
  
+ **리눅스 파일의 종류와 특징**

  + 파일의 종류
  
  + 디렉터리 계층 구조
  
  ___

# 리눅스 명령 사용
### 1. 명령 행 편집 방법
+ 리눅스 명령 행에서 문자를 지울 때는 주로 "◀-"키를 사용(우분투)
+ 리눅스 명령 행에서 단어를 지울 때는 "Ctrl + w"키를 사용 이때 단어는 공백으로 구분
+ 리눅스 명령 행에서 문장을 지울 때는 "Ctrl + u"키를 사용

#### 명령 행에서 단어 지우기("Ctrl + w" 키 사용)

![코드](https://user-images.githubusercontent.com/42503786/172365449-ea7c0c75-238a-49eb-80a3-bb4395a97295.png)
![코드2](https://user-images.githubusercontent.com/42503786/172366089-70956345-8638-4c83-b834-0958b6e46d19.png)

#### 명령 행에서 문장 지우기("Ctrl + u" 키 사용)
![코드](https://user-images.githubusercontent.com/42503786/172365449-ea7c0c75-238a-49eb-80a3-bb4395a97295.png)
![결과리눅스](https://user-images.githubusercontent.com/42503786/172366876-5178e608-7868-4d73-ba56-214188d539fe.png)

### 기초 명령 사용법
#### date command
<strong> date - print or set the system date and time ( 시스템 날짜 및 시간을 출력하거나 설정  )</strong>

![date](https://user-images.githubusercontent.com/42503786/172367725-68705080-63cb-4f81-b3f0-29a62d34b172.png)


#### clear command 
<strong> clear - clear the terminal screen (터미널 스크린을 깨끗하게 해줌)

![clear](https://user-images.githubusercontent.com/42503786/172368127-fde25897-757b-4a1e-b843-3c07a77a5727.png)
![결과리눅스](https://user-images.githubusercontent.com/42503786/172366876-5178e608-7868-4d73-ba56-214188d539fe.png)

### passwd command
<strong> passwd - change user password (사용자 비밀번호 변경)</strong>
<p>비밀번호 자리 수를 짧게 설정하면 변경이 되지 않음</p>

![비밀번호 변경](https://user-images.githubusercontent.com/42503786/172369077-1a2a8631-3f87-4ea7-8dd1-1c3f8b7653f3.png)


# 리눅스 파일의 종류와 특징
### 파일의 종류
리눅스에서 파일은 사용 목적에 따라 "**일반 파일**", "**디렉터리**", "**심벌릭 링크**", "**장치 파일**"로 구분 

#### 일반 파일(regular file)
+ 데이터를 저장하는데 주로 사용
+ 텍스트 파일, 실행 파일, 이미지 파일 등 리눅스에서 사용하는 대부분의 파일은 일반파일
+ 파일 내용을 확인하는 명령어를 통해 확인 가능하고 편집기를 사용하여 내용을 보거나 편집 가능
+ 실행 파일이나 이미지 파일의 경우 데이터가 바이너리 형태로 저장되고 특정 응용프로그램이 있어야 내용 확인 가능 (바이너리 파일)

#### 디렉터리(directory)
+ 리눅스에는 디렉터리도 파일로 취급 

#### 심벌릭 링크(symbolic link)
+ 원본 파일을 대신하도록 원본 파일을 다른 파일명으로 지정한 것

#### 장치 파일(device file)
+ 리눅스 시스템에 부착된 장치를 관리하기 위한 특수 파일 
+ 대부분의 장치 파일은 /dev 디렉터리 아래에 위치 

#### file command 
file - determine file type (파일 종류 확인)

![파일명령어](https://user-images.githubusercontent.com/42503786/172371125-babc39bb-1028-4448-9122-1485b0ec474f.png)

./.bash_history: ASCII text -> ASCII 코드를 사용하는 텍스트 파일이라는 의미

![elf실행파일](https://user-images.githubusercontent.com/42503786/172372278-14462763-d347-49d4-bf5f-d2ba42f1ffba.png)

#### ELF(Excuatable and Linkable Format) 
직역하자면 실행가능하고 링킹가능한 포멧이라는 의미이다. 여기서 링킹이란 여러 개의 코드와 데이터를 모아서 연결하여 메모리에 로드 될 수 있고 실행될 수 있는 한 개의 파일로 만드는 작업을 의미.

실행은 디스크에 저장되어 있던 프로그램이 메모리영역에 올라가서 컴퓨팅 자원을 사용해 서비스를 제공해 주는 것(실행 중인 프로그램을 프로세스라고 함)

### 디렉터리 계층 구조

![linux-filesystem](https://user-images.githubusercontent.com/42503786/172382272-59cd596a-b824-46b9-86a8-ef348f9ec914.png)

### 디렉터리 주요 기능

|디렉터리|기능|
|--------------|----------------------------------------------------------------------------------------|
|dev|장치 파일이 담긴 디렉터리|
|home|사용자 홈 디렉터리가 생성되는 디렉터리|
|media|CD-ROM이나 USB같은 외부 장치를 연결(마운트라고 함)하는 디렉터리|
|opt|추가 패키지가 설치되는 디렉터리|
|root|root 계정의 홈 디렉터리. 루트(/) 디렉터리와 다름|
|sys|리눅스 커널과 관련된 파일이 있는 디렉터리|
|usr|기본 실행 파일과 라이브러리 파일, 헤더 파일 등 많은 파일이 있음.|
|boot|부팅에 필요한 커널 파일이 있음|
|etc|리눅스 설정을 위한 각종 파일이 있음|
|lost+found|파일 시스템에 문제가 발생하여 복구할 경우, 문제가 되는 파일이 저장되는 디렉터리|
|mnt|파일 시스템을 임시로 마운트하는 디렉터리|
|proc|프로세스 정보 등 커널 관련 정보가 저장되는 디렉터리|
|run|실행 중인 서비스와 관련된 파일이 저장됨|
|tmp|시스템 사용중에 발생하는 임시 데이터 저장. 디렉터리에 있는 파일은 재시작하면 모두 삭제됨|
|var|시스템 운영 중에 발생하는 데이터나 로그 등 내용이 자주 바뀌는 파일이 주로 저장됨|
