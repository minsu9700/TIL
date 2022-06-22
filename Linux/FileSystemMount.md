# 파일 시스템(File System)
***

**1. 파일과 디렉터리의 집합을 구조적으로 관리하는 체계**
**2. 어떤 구조를 구성하여 파일이나 디렉터리를 관리하느냐에 따라 다양한 형식의 파일 시스템이 존재**

### 리눅스 고유의 디스크 기반 파일 시스템

1. ext(ext1)
2. ext2
3. ext3
4. ext4
5. XFS

### 리눅스에서 지원하는 기타 디스크 기반 파일 시스템

|파일 시스템 | 기능|
|-----------| ---------------------------------------------------|
|nfs| network file system으로 원격 서버의 디스크를 연결할 때 사용|
|ntfs | 윈도의 NTFS를 지원하기 위한 파일 시스템 | 


### 특수 용도의 가상 파일 시스템

**리눅스에는 디스크가 아니라 메모리에서 생성되어 사용되는 가상 파일 시스템 존재**

|파일 시스템 | 기능 | 
|------------| ---------------------------------------------------------|
|swap | 스왑 영역을 관리하기 위한 스왑 파일 시스템|
|tmpfs | temporary file system으로 메모리에 임시 파일을 저장하기 위한 파일 시스템, 시스템이 재시작 할 때마다 기존 내용 사라짐|
|proc | proc 파일 시스템으로 /proc 디렉터리, 커널의 현재 상태를 나타내는 파일을 가지고 있음|
|roots | root file system으로 / 디렉터리이다. 시스템 초기화 및 관리에 필요한 내용을 관리 | 

### 현재 시스템이 지원하는 파일 시스템 확인하기

**/proc/filesystems는 현재 커널이 지원하는 파일 시스템의 종류를 알려줌**  
**nodev는 해당 파일 시스템이 블록 장치(ex. 디스크)와 연결되어 있지 않다는 것으로 가상 파일 시스템을 의미함**

![파일시스템](https://user-images.githubusercontent.com/42503786/174559692-bb35900d-38ff-40a0-99dd-c6b55f4e3745.png)
***

# 리눅스 파일 시스템
***

**리눅스의 모든 파일 시스템은 다음과 같이 3가지의 공통의 개념을 바탕으로 구현됨**

1. 파일은 inode로 관리된다.
2. 디렉터리는 단순히 파일의 목록을 가지고 있는 파일일 뿐이다.
3. 특수 파일을 통해 장치에 접근할 수 있다. 

### ext4 파일 시스템의 구조

**ext4 파일 시스템은 효율적으로 디스크를 사용하기 위해 저장 장치를 논리적인 블록의 집합(블록 그룹)으로 구분 일반적으로 블록은 4KB 실제 크기는 시스템 설정에 따라 달라짐**

![파일시스템 구조](https://user-images.githubusercontent.com/42503786/174561804-5e6af536-e4c2-4a67-9a1b-d0b9f7b66b1d.png)

**블록 그룹에는 3가지 유형이 있음**

* 블록그룹 0: 파일 시스템의 첫 번째 블록 그룹. 특별하게 그룹 0 패딩과 슈퍼블록, 그룹 디스크립터를 가지고 있음
* 블록그룹 a: 파일 시스템에서 첫 번째 블록 그룹이 아닌 블록 그룹으로 그룹 0 패딩이 없으나 슈퍼블록과 그룹 디스크립터의 복사본을 가지고 있음
* 블록그룹 b: 파일 시스템에서 첫 번째 블록 그룹이 아닌 블록 그룹으로 그룹 0 패딩, 슈퍼블록, 그룹 디스크립터가 없고 바로 데이터 블록 비트맵으로 시작

**그룹 0 패딩**
* 블록 그룹 0의 첫 1,024바이트는 x86 부트 섹터와 부가 정보를 저장하는 특별한 용도로 사용됨

**슈퍼블록**

* 전체 inode 개수
* 할당되지 않은 블록의 개수
* 첫 번째 데이터 블록의 주소
* 그룹당 블록의 개수
* 파일 시스템의 생태
* 전체 블록의 개수
* 할당되지 않은 inode의 개수
* 블록의 크기
* 마운트 시간
* 그룹 디스크립터의 크기
* 슈퍼블록에는 파일 시스템과 관련된 다양한 정보가 저장됨
* 슈퍼블록에 문제가 생기면 전체 파일 시스템을 사용할 수 없게 되기 때문에 다른 블록 그룹에 복사해놓고 블록 그룹 0의 슈퍼블록을 읽을 수 없을 경우 복사본을 사용하여 복구

**그룹 디스크립터와 GDT 예약 블록**

* 블록 비트맵의 주소
* inode테이블의 주소
* 할당되지 않은 inode의 개수
* 블록 비트맵, inode 비트맵 체크섬
* inode 비트맵의 주소
* 할당되지 않은 블록의 개수
* 디렉터리의 개수
* GDT 예약 블록은 그룹 디스크립터의 확장을 위한 예비 공간

**데이터 블록 비트맵과 inode 비트맵**

* 데이터 블록 비트맵은 블록 그룹에 포함된 데이터 블록의 사용 여부를 확인하는데 쓰임
* inode 비트맵은 inode 테이블의 항목이 사용 중인지를 표시
* 비트맵에서 각 데이터 블록과 inode 테이블 항목은 1bit로 표현됨

**inode 테이블과 데이터 블록**

* inode에는 파일 정보를 저장
* 데이터 블록에는 실제 데이터 저장
***

### 파일 시스템과 디렉터리 계층 구조

**한 파일 시스템으로 구성**

![1파일](https://user-images.githubusercontent.com/42503786/174564938-82ad05b1-da60-46c6-82b3-1dc091a456d0.png)

**여러 파일 시스템으로 구성**

![2파일](https://user-images.githubusercontent.com/42503786/174565101-6377b800-9588-4b80-b601-d34cb3eb9c68.jpg)

**파일 시스템1을 / 디렉터리에 파일 시스템2를 /usr 디렉터리에 파일 시스템3을 /home 디렉터리에 연결**

***

# 파일 시스템 마운트

***


**마운트: 파일 시스템을 디렉터리 계층 구조의 특정 디렉터리와 연결하는 것**

**디렉터리 계층 구조에 파일 시스템을 마운트하지 않으면 사용자가 접근할 수 없음(마운트 하지 않은 파일 시스템의 디렉터리로 이동 불가)**

#### /etc/fstab 파일 기능

**/etc/fstab 파일은 파일 시스템의 마운트 설정 정보를 가지고 있음**

#### /etc/fstab 파일의 구조

![구조](https://user-images.githubusercontent.com/42503786/174566277-a1c0b36b-1127-4b1a-8d26-5462b2f60758.png)

**/etc/fstab 파일 구성**

![구성](https://user-images.githubusercontent.com/42503786/174566601-d6fcbb59-f243-41ff-a1e3-f1990c06ec0b.png)

**실제 내용 구분**

* 1. 장치명 -> UUID=7B43-5F57
* 2. 마운트포인트 -> /boot/efi
* 3. 파일 시스템의 종류 -> vfat
* 4. 옵션 -> umask=0077
* 5. 덤프 관련 설정 -> 0
* 6. 파일 점검 옵션 -> 1

**장치명**
* 파일 시스템 장치명 설정(특정 디스크 지정)

**마운트 포인트**
* /boot/efi 설정 다시 한번 말하자면 마운트는 파일 시스템을 디렉터리 계층 구조의 특정 디렉터리와 연결하는 것

**파일 시스템의 종류**
* ext2, ext3, ext4 등 파일 시스템 종류가 있음

**옵션**
* 파일 시스템의 속성을 지정하는 옵션

**덤프 관련 설정**
* 0의 경우 dump 명령으로 파일 시스템 내용이 덤프되지 않는 파일 시스템
* 1의 경우 데이터 백업 등을 위해 dump 명령의 사용이 가능한 파일 시스템

**파일 점검 옵션**
* 0 또는 1이나 2 지정
* 0은 부팅할 때 fsck 명령으로 파일 시스템을 점검하지 않도록 하는 설정
* 1은 루트 파일 시스템을 의미 (루트 파일 시스템이 fsck 명령으로 파일 시스템 점검 수행)
* 2는 루트 파일 시스템 이외의 파일 시스템을 의미 (나열된 순서대로 fsck 명령 사용하여 점검)
***

### 마운트 관련 명령

**옵션이나 인자를 지정하지 않고 mount 명령을 사용하여 다음과 같이 현재 마운트되어 있는 정보가 출력됨**

![마운트](https://user-images.githubusercontent.com/42503786/174568720-ed8c6bae-9ff4-4ca3-bf9a-8efcbe5ffc49.png)

***

# 디스크 추가 설지
***

### 디스크 추가 단계

![디스크 추가 단계](https://user-images.githubusercontent.com/42503786/174570097-cbfc09a4-adb6-4140-a41e-494b1a6dae6a.png)

### 가상 머신에 디스크 추가하기

![디스크추가](https://user-images.githubusercontent.com/42503786/174570630-8a4cbe85-c9b9-4051-bd6d-0fb2a2df3733.png)

### 디스크 파티션 나누기

**방금 디스크 2개를 새로 만들었다 ls -l /dev/sd* 명령어를 입력하면 디스크 목록이 나타난다**

![디스크순서](https://user-images.githubusercontent.com/42503786/174571776-5d19bd7d-8d09-4935-81e0-6d6586752754.png)

* /dev/sda: 첫 번째 디스크 -> 첫 번째 디스크 전체를 의미하는 장치명
* /dev/sdb: 두 번째 디스크 -> 디스크의 첫 번째 파티션
* /dev/sdc: 세 번째 디스크 -> 디스크의 두 번째 파티션

**fdisk command**

* 디스크를 파티션으로 나누는 작업
* fdisk -l 명령을 사용하면 전체 디스크의 파티션 정보를 볼 수 있음

**fdisk 명령으로 파티션 나누기**

![1-1](https://user-images.githubusercontent.com/42503786/174573367-b7eff06c-be38-4056-bb42-e503ca84ff70.png)

![1-2](https://user-images.githubusercontent.com/42503786/174573400-3b345b81-9245-45fe-ba26-92c5a0490f31.png)

**이후 w를 누르면 저장되면서 생성됨(default는 Enter누르면 됨) 두번째 파티션(/dev/sdc)도 똑같이 생성**

**sudo fdisk -l를 입력하여 파티션이 올바르게 생성되었는지 확인**

![파티션](https://user-images.githubusercontent.com/42503786/174573897-bd41b4d7-1a83-4d9e-a6ce-68030deeb03f.png)

***

### 파일 시스템 생성하기

**mkfs command(리눅스 파일 시스템을 만듬)**
**mke2fs command(리눅스 개정판 확장 파일 시스템(ext2, ext3, ext4)를 만듬**

**mkfs 명령으로 파일 시스템 생성**

![mkfs](https://user-images.githubusercontent.com/42503786/174574652-e90ccee5-da83-4f6a-a225-261cb7a01add.png)

**mke2fs 명령으로 ext3 파일 시스템 생성**

![mk2fs](https://user-images.githubusercontent.com/42503786/174574719-503c33bc-34e2-44b2-a837-70c169c3e150.png)

### 디스크 마운트하기

**파일 시스템을 마운트하기 위해서는 마운트 포인트를 미리 준비해야 한다.**

**디렉터리 2개 생성**

**sudo mkdir /mnt/hdd1**

**sudo mkdir /mnt/hdd2**

#### 파일 시스템 마운트

![지정](https://user-images.githubusercontent.com/42503786/174578223-5925e694-da6b-47c1-b419-7da70396db90.png)

**마운트 결과(mount command 사용)**

![결과](https://user-images.githubusercontent.com/42503786/174578363-89e7e6a0-be3a-4e25-9444-29e2d101b00b.png)

**lost+found가 생성되면 성공**

![lostfound](https://user-images.githubusercontent.com/42503786/174578533-0ac6d0c9-3d54-41aa-a44f-5dd268850ab4.png)

**/mnt/hdd2에 연결된 파일 시스템 마운트 해제**

**sudo umount /mnt/hdd2 명령어 입력 lost+found가 없어야 함(연결 끊음)**

![umount](https://user-images.githubusercontent.com/42503786/174578971-44911635-9c15-437e-8017-9d8ef8ad894d.png)

### 여러 디스크를 하나처럼 사용하기

#### LVM이란

**독립적으로 구성된 디스크 파티션을 하나로 연결하여 한 파티션처럼 사용할 수 있도록 해주는 것**

* pv(physical volume) : /dev/sdb1, /dev/sdc1 같은 실제 하드디스크 파티션
* vg(volume group) : 여러 개의 pv를 하나로 묶은 것 예를들어 /dev/sdb1 /dev/sdc1이 GRP1이라는 그룹을 만들 때 GRP1이 VG임
* LV(logical volume) : VG를 다시 적절한 크기의 파티션으로 나눌 때 각 파티션을 LV라고 함
* PE(physical extent) : PV가 가진 일정한 블록
* LE(logical extent) : LV가 가진 일정한 블록

#### LVM 기본 개념

![lvm](https://user-images.githubusercontent.com/42503786/174976097-eadbc260-0715-4117-90b7-08afc06fcde1.png)

#### LVM 생성 과정

![LVM생성](https://user-images.githubusercontent.com/42503786/174976469-37511086-1f65-4d56-bfd5-fc4a0631d61a.png)

#### 기존 파일시스템 종류 변경하는 방법

**/dev/sdb1 기존 파일시스템 83(Linux)에서 8e(Linux LVM)으로 변경하기**

##### 1. fdisk 명령어 사용

![1](https://user-images.githubusercontent.com/42503786/174977527-a504c624-f0aa-4952-9450-4dec1580902b.png)


##### 2. p 옵션을 사용하여 파티션 테이블 출력

![2](https://user-images.githubusercontent.com/42503786/174977700-8afe7fd0-f1a0-4118-8ce0-110054e0ff66.png)

##### 3. t 옵션을 사용하여 파티션 타입 변경(8e -> Linux LVM)

![3](https://user-images.githubusercontent.com/42503786/174977852-2e90e189-85d4-4165-8456-e266f6eef3a6.png)

##### 4. 파티션 테이블 출력하고 w 옵션을 사용하여 저장하고 나가기

![4](https://user-images.githubusercontent.com/42503786/174978020-6e78fa7d-e131-47aa-b397-444496a80798.png)


#### pv 생성하기

##### pvcreate 명령어를 사용하여 /dev/sdb1 /dev/sdb2에 pv 생성

**만약 이런 에러가 나온다면 "sudo umount /dev/sdb1" 명령어 입력하여 해결**

![pv](https://user-images.githubusercontent.com/42503786/174986846-eb4c1651-560e-406b-8cc4-a32238f0f028.png)

**경고가 뜨는건 아직 해결 못함**

![pv2](https://user-images.githubusercontent.com/42503786/174987285-a9f90106-50b7-44b0-9f9e-c5f69044aaff.png)

![pv2-1](https://user-images.githubusercontent.com/42503786/174987336-a85e67ce-de47-4adf-bd95-c6463650405e.png)

##### pvscan 명령어를 입력하여 pv 상태 확인

![pv3](https://user-images.githubusercontent.com/42503786/174987555-39f2c08f-02a6-4b12-b513-34ffbc5a4a36.png)

##### 두 pv를 통합해 vg 생성 : vg 이름 -> grp1

![lv](https://user-images.githubusercontent.com/42503786/174987834-b5c2f625-2fce-4181-ad64-337b971ccd4c.png)

##### vgchange 명령어를 입력하여 생성한 vg 활성화

![lv 2](https://user-images.githubusercontent.com/42503786/174988152-60429109-7da0-4bab-8046-89b2a6963a30.png)

##### 활성화된 vg grp1 상태를 vgdisplay 명령어를 입력하여 확인

![lv3](https://user-images.githubusercontent.com/42503786/174988378-e504d918-9e0a-470b-a480-bc556792f90d.png)

##### Total PE(pv가 가진 일정한 블록)은 총 248개 있으며 모두 합해 하나의 lv 생성

![lv4](https://user-images.githubusercontent.com/42503786/174988820-0486159b-b1b5-4162-824d-8b3acab2cafb.png)

##### 생성한 lv 상태 확인하기

![lv5](https://user-images.githubusercontent.com/42503786/174988977-b1db514a-ad96-4201-a98d-ed5966c0f431.png)

##### lv mylvm1에 ext4 파일시스템 생성하기 (장치명은 /dev/grp1/mylvm1)

![lv6](https://user-images.githubusercontent.com/42503786/174989238-0d5555a4-e123-43d2-9354-05f72330ec73.png)

##### lv를 /mnt/lvm 디렉터리에 마운트하고 파일 복사해보기

![lv result](https://user-images.githubusercontent.com/42503786/174989688-f2c80ec7-caed-4374-a258-b80bf2f1e860.png)

***

##  디스크 관리
***

### 디스크 사용량 확인하기

**df(disk free) 명령어를 입력하여 디스크의 남은 공간에 대한 정보 출력**

![df](https://user-images.githubusercontent.com/42503786/174990282-06aa11c8-621f-4ef7-93a9-8d4f20608f65.png)

**df명령으로 출력되는 항목**

* 파일 시스템 장치명
* 파일 시스템 전체 용량
* 파일 시스템 사용량
* 파일 시스템의 사용가능한 남은 용량
* 퍼센트로 나타낸 용량
* 마운트 포인트

**du 명령어를 입력하여 디스크의 사용 공간에 대한 정보 출력**

![du](https://user-images.githubusercontent.com/42503786/174990723-10db43cc-9b09-48e1-8a75-e3982b586ac9.png)
***

### 파일 시스템 검사하고 복구하기

**파일 시스템은 부적절한 시스템 종료나 전원의 불안정, 소프트웨어 오류, 하드웨어 오작동 등 다양한 이유로 손상될 수 있음**
**손상된 파일 시스템 용량을 확인해야 할 뿐만 아니라 파일 시스템의 상태를 점검하고 문제가 있을 때 복구해야 함**

#### fsck 명령으로 파일 시스템 검사하기

**fsck 명령으로 /dev/sdc1 파일 시스템 검사하기

![fsck](https://user-images.githubusercontent.com/42503786/174991617-a342ff53-1200-408a-9d30-03e0118d2a72.png)

**아직 사용한 적이 없어 파일시스템의 상태가 깨끗하다고 출력됨**

#### e2fsck 명령으로 파일 시스템 검사하기

**e2fsck 명령은 fsck 명령처럼 inode 및 블록, 디렉터리, 파일 링크 등을 검사하고 필요시 복구 작업 수행(건드린적이 없어 깨끗하다고 출력됨)**

![e2fsck](https://user-images.githubusercontent.com/42503786/174992125-d00c1b85-e160-4719-a752-7d7b0e40ec19.png)

#### badblocks 명령을 통해 배드 블록 검사하기

**디스크에 발생하는 심각한 문제 중 하나는 배드 블록으로 인한 데이터 유실**
**따라서 배드 블록을 검사하는 것도 중요함 -v 옵션을 사용하여 자세히 출력**

![badblocks](https://user-images.githubusercontent.com/42503786/174992506-c2561627-3318-46b1-af91-5df75b5eb805.png)



* 현재 디렉터리와 서브 디렉터리, 파일 용량 출력(기본 단위 KB)
* 가장 마지막에 있는 현재 디렉터리(.)의 크기가 해당 디렉터리 전체의 디스크 사용량


