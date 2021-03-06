# OS 관련 정의

- 의문
- General
  - Booting
  - Firmware
  - BIOS
  - Virtualization
- File system
  - File system
  - Mount
- Process
  - Process
  - Daemon

## 의문

- File system
  - *다음 설명은 참인가?*
    - 각 저장장치는 어떤 File system에 형식에 따라 데이터를 저장하는지 지정 가능(포맷)
    - 컴퓨터의 OS는 그 저장장치를 인식하면 지원하는 File system인지 확인한 후에, 지원한다면 해당 저장장치 내의 파일들에 접근 및 수정 가능
  - *unix-like os에서 장치 혹은 socket을 file로 관리한다는 것은 어떤것을 의미하는가?*
  - 우리가 그럼 commandline에서 보는 디렉터리 구조들과 같은 것들은 결국 정체가 무엇인가?
    - 하드 디스크 내부의 파일들의 메타 데이터
      - 우리는 데이터 저장장치의 Meta Area속에 존재하는 인덱싱된 파일 혹은 디렉터리의 메타 데이터를 보고 있는 것임
  - *파일 시스템의 부팅 영역이란*
    - *무엇에 대한 부팅을 의미하는가? 컴퓨터? 아니면 저장장치? 애초에 부팅이 뭐지?*
  - *애초에 파일 시스템의 파일과 드리아브 크기 제한을 빵빵하게 만들면 될텐데 왜 제한이 빡빡하게 만들어서 계속 확장하게 되었는가?*
  - *구체적으로 Inode란 무엇인가?*
    - 무엇을 저장하는가?

## General

### Booting(운영체제를 initializing(메모리에 올리는 것))

Bootstrap

![](./images/os/bootstrap1.png)

- 정의
- 과정
  - ① 컴퓨터 전원버튼을 누르고, 메인보드에 전력이 들어오며, 메인보드에 부착된 장치들에게 전력이 공급
  - ② CPU가 ROM에 저장된 펌웨어인 BIOS(Basic Input/Output System)를 실행시킴
  - ③ 실행된 BIOS는 POST(Power On Self Test)즉, 컴퓨터 주변 하드웨어를 체크
    - POST
      - 컴퓨터를 킬 때, 문제가 있나 자가검사 하는 것
  - ④ BIOS가 부팅매체(하드디스크, USB, SSD, ...)를 선택하고, 부팅매체의 MBR(부팅 프로그램이 저장된 영역)에 저장된 부트로더를 RAM으로 읽어오는 Bootstrap을 실행
    - 부팅 우선순위가 존재함(e.g 하드디스크 -> USB -> CD -> Network -> ...)
    - MBR(Master Boot Record)
      - 모든 기억장치(USB, 하드디스크 등)은 첫 번째 섹터(512바이트)에 MBR영역을 갖고 있음
      - Primary partition에 대한 정보 4개를 기록할 수 있는 64바이트 공간 + 운영체제(커널) 코드를 복사해서 메모리에 올려주는 부트 로더가 저장
        - 부트 로더를 RAM 메모리에 올리는 것을 **부트스트랩 과정** 이라 함
  - ⑤ Bootstrap 과정으로 RAM에 Bootloader가 올라가고, 부트로더는 디스크에 있는 OS(커널) 코드를 복사해 RAM에 올려 OS 실행
    - Bootloader
      - 운영체제를 initializing(메모리에 올림) 해주는 역할
  - ⑥ OS가 부팅됨

### Firmware

- 정의
- 특징
  - ROM과 같은 비휘발성 메모리에 저장해 사용
- 종류
  - BIOS, ...

### BIOS(Basic Input Output System)

- 정의
- 특징
  - 하드웨어들의 Input / Output을 관리하는 소프트웨어
  - 운영체제가 컴퓨터 하드웨어의 입출력을 컨트롤 할 경우에 사용

### Virtualization

- 정의
  - 가상의 무엇인가를 만드는 기술
- 구체적 예시
  - NAT(Network Address Translation)
    - 존재하지 않는 IP를 가상으로 만들어서 배정
  - VPN(Virtual Private Network)
    - 같은 공용 통신망을 통해 통신을 하지만, 패킷을 암호화해서 주고 받아, 마치 사설 네트워크를 만드는 것과 같은 기술
  - RAID, LVM

### Server Virtualization

- 정의
- 사용하는 이유
  - 서버의 자원을 효율적으로 최대한 사용하기 위함
- 구현에 따른 분류
  - 전 가상화(Bare-metal/hypervisor)
    - 개요
      - 순수한 하드웨어 위에 운영체제나 BIOS가 아닌 Hypervisor가 있는 구조로 이루어지는 가상화
        - 하이퍼바이저는 가상머신을 만들고 관리하는 프로그램
    - 특징
      - VM의 입장에서 하드웨어 자원은 무조건 하이퍼바이저를 통해서 사용 가능
  - 반(더 진보한) 가상화(Para-virtualization)
    - 개요
      - 전 가상화와 달리, VM이 하드웨어 자원을 직접적으로 사용 가능
  - 호스트 기반 가상화
    - VMware나 VirtualBox와 같은 가상화 구현 프로그램을 이용한 가상화
- 세대 별 분류(기술 수준)
  - 1세대
    - 하나의 물리적인 서버에 하이퍼바이저로 여러 개의 가상머신을 생성하는 수준
    - 예시
      - VirtualBox
  - 2세대
    - 다수의 물리적인 서버의 자원들을 하나로 묶어서 서버 풀을 구성하고 관리할 수 있는 수준
      - 특정 서버에 문제가 생겼을 때, 문제 있던 서버에서 실행중이던 가상머신들을 다른 정상 작동하고 있는 서버로 옮기는 실시간 마이그레이션 기술 사용
  - 3세대
    - 다른 하이퍼바이저끼리도 서버 풀을 구성하고 관리가 가능
    - 예시
      - OpenStack, CloudStack, Eucalyptus, OpenNebula, ...

## File system

### File system

- 정의
  - **저장장치의 파티션 내에서 클러스터 단위의 데이터를 배치하고 관리하기 위한 논리적 체계(저장장치의 파티션 별로 하나씩 둘 수 있음)**
    - 특정 데이터가 하드웨어 파티션 상에서 어디서부터 어디까지 저장된 것인지 파악
    - 사실상, 저장장치의 데이터를 인덱싱하는 것
      - 인덱싱 할 때, 키(파일 이름: case sensitivity, suffix의 길이)와 value(파일 내용 or 내용 크기 등)에 관한 스펙을 다 정해줌
    - 파일에 대한 메타데이터도 다 가지고 있고, 따로 관리
      - 메타데이터는 Unix-like 시스템에서 `inode`의 데이터 구조로 저장됨
      - *우리가 윈도우즈 탐색기로 파일들을 파악하는 것은 다 메타데이터로 하는 일(?)*
- 등장 배경
  - ① 클러스터와 블록개념의 도입
    - 하드 디스크를 단순히 실린더로 관리하면 큰 파일의 데이터를 읽고 쓰는데 너무 느린 문제가 발생
      - e.g) 10MB 파일 하드디스크로부터 읽기
        - 2 * 1024 * 10 개의 섹터(0.5KB)를 불러와야 함
    - **클러스터, 블록의 도입** (섹터들을 한 번에 여러 개를 읽는 기술 도입)
      - 섹터 한개 단위가아니라, 다수의 섹터 단위로 묶어서 읽고 저장
      - 대신, 한번에 여러 섹터를 읽으면 빈 섹터를 읽어버리는 경우가 존재(e.g 한 번에 4개의 섹터를 읽는데, 마지막엔 2개만 읽어도 충분한경우)
        - **Slack space**
      - 클러스터 => 윈도우 운영체제에서 사용되는 용어
      - 블록 => 유닉스 계열 운영체제에서 사용되는 용어
    - 블록(클러스터)를 몇 개의 섹터로 계싼하는 지는 파일 시스템 마다 다름!
    - **물리적으로는 클러스터, 또는 블록이라는 대응체가 없으므로, 블록이라는 것을 파일시스템이 소프트웨어적으로 계산해줘서 운영체제가 사용할 수 있는게 함**
      - 클러스터, 블록 이라는 단위를 계산해주는 것도 파일시스템의 역할 중 하나
    - 파일 시스템 덕분에 운영체제는 블록(클러스터) 단위로 데이터를 사용할 수 있는 것
      - 파일 시스템은 운영체제에 포함되어있음
  - ② 효율적으로 디스크의 데이터를 관리하는것의 필요성(파일의 삭제, 편집)
    - 섹터에 저장된 기존 파일의 크기가 더 커지면?
      - 같은 트랙에 데이터가 꽉 찼다면, 다른 빈 트랙에 넣어야 하는데, 컴퓨터가 다른 트랙의 어디에 저장되어있는지 어떻게 알 수 있는가?
    - 섹터에 저장된 기존 파일의 크기가 줄어들거나, 지워졌을 때는?
      - 트랙 중간중간에 빈 섹터가 생겨남
      - 디스크 모음의 필요성
- 역할
  - Each different filesystem provides the host operating system with metadata so that it knows how to read and write data. When the medium
  - 디스크의 데이터를 더 빠르게 읽고 저장할 수 있는 블록(클러스터)를 소프트웨어적으로 계산
  - 분산 저장된 연관 데이터들을 빠르게 찾게 해줌(인덱싱)
  - 디스크 조각(섹터) 모음과 같이 디스크 공간을 효율적으로 사용하게 해줌
- 블록(클러스터) 계산 방식(Addressing)
  - CHS(Cylinder-Head-Sector)
    - 물리적 주소 지정 방식
    - 실린더와 헤드 섹터 순으로 주소를 지정
    - 초창기에 사용
  - LBA(Logical Block Addressing)
    - 논리적 주소 지정 방식
      - 마치 3D 디스크 공간이 한 줄인양 할당이 됨
    - BIOS(Basic Input/Output System)
      - 실제 디스크 섹터 위치 <--> 논리적 섹터 위치 변환
    - 파일 시스템은 BIOS가 구현한 LBA를 이용해서 데이터를 효율적이게 관리하고 사용할 수 있게 블록(클러스터)계산
      - 블록(클러스터)은 LBA에서 논리적인 개념이 되어버림
    - 현재에도 사용중
    - **LBA에 의해서, 파일시스템은 섹터, 트랙, 실린더를 다루는 것이 아닌, 블록(클러스터) 기준으로 데이터를 다룸**

파일 시스템의 추상화 구조

![](./images/os/file_system_abstraction1.png)

- 파일시스템의 추상화 구조(Meta Area, Data Area)
  - Meta Area
    - 데이터에 대한 데이터들이 저장되는 장소(인덱싱)
      - Linux의 I-node
      - 데이터의 블록 위치를 효율적으로 파악 가능
  - Data Area
    - 데이터를 저장하는 장소
- 특징
  - 저장공간을 사용한다면 무조건 필요한 소프트웨어이며, 운영체제에 무조건 필수적으로 포함 되어야 함
  - 저장장치의 종류마다 각자의 파일 시스템을 사용
    - 파일 하나의 크기 제한, 전체 디스크에 대한 크기 제한, 파일에 대한 저장 방식 등이 다 다름
  - local data storage 뿐 아니라, Network protocol을 이용한 파일 시스템을 사용하여 원격 서버의 파일을 제어가능
  - 특정 유저나 유저의 그룹만 파일이나 폴더를 읽고 쓸 수 있게 설정 가능

FAT 파일 시스템의 구조

![](./images/os/file_system_fat_example1.png)

NTFS의 구조

![](./images/os/file_system_ntfs_example1.png)

ext2의 구조

![](./images/os/file_system_ext2_example1.png)

- 파일 시스템의 종류와 역사
  - FAT(File Allocation Table)
    - 종류 및 특징
      - FAT12
        - 2^12개수의 클러스터를 가질 수 있음
      - FAT32
        - USB에 자주 쓰임
        - 지원하는 최대 드라이브 크기는 32GB, 한 파일당 4GB
          - 4GB 이상 크기의 파일을 USB에 옮기려 하면, 파일 시스템을 바꿔야 함
    - 구조
      - Reserved Area
        - 예약된 행위 정보들이 들어있는 곳
        - Boot Block
          - 컴퓨터 부팅에 관련된 정보들이 들어있는 블록
        - FSINFO(File System INFOrmation) Block
          - 운영체제에게 알려줄 파일 시스템 정보가 있는 블록
        - 추가 예약 공간 블록
      - FAT Area
        - Meta Area
        - 파일에 얼마나 클러스터가 할당 됐는지 적혀있는 테이블(File Allocation Table)
          - 어떤 파일에 얼마나 많은 클러스터가 할당됐는지, 어디 있는지, 언제 수정되고 만들어졌는지 등의 정보 존재
      - Data Area
        - 데이터가 저장된 공간
  - NTFS(New Technology File System)
    - 특징
      - 디스크 크기 256TB
      - 한 파일 크기 제한 16TB
      - 디스크 복구 기능 존재
      - 서버용으로 사용 가능
    - 구조
      - VBR(Volume Boot Record)
        - 부팅에 관련된 정보들이 저장된 공간
      - MFT(Master File Table)
        - Meta Area
        - FAT Area와 유사
      - Data Area
        - 데이터가 저장된 공간
  - ext(extended file system)
    - 종류 및 특징
      - ext1
        - 2GB까지 용량 지원 파일 이름 255글자까지 지원
        - VFS 시스템 도입
          - 각각 파일 시스템의 정보들을 일관되게 가상적으로 같은 정보처럼 만들어서 운영체제에서 같이 사용할 수 있게 함
          - *구체적인 예시?*
        - 단편화 문제
          - 디스크 저장 공간 중간중간에 빈 공간이 생기는 현상
      - ext2
        - 2TB까지 용량 지원
        - 한 파일 크기 16GB까지 지원
        - i-node 기능 지원
        - 리눅스의 본격적인 파일 시스템 형태
        - 데이터를 저장하는 동안 전원이 끊기면 심각한 손상이 일어남
        - 블록 그룹 사용
          - 블록들의 집합
        - 구조
          - Boot Sector
            - 블록크기 까지는 필요 없는 부팅에 관한 정보들이 저장된 공간
          - Block Group
            - Super Block
              - 모든 블록에 해당되는 공통 정보들을 관리하는 블록
              - 블록의 크기, 총 블록의 개수, 블록 그룹의 개수, 블록 그룹 내 블록과 아이노드 개수
              - 중요하므로, 모든 블록 그룹의 맨 앞에 복사본을 만들어놓음. 사용은 첫번째 블록그룹에 속한 것만 함
            - Group Descriptor Table
              - 블록 그룹들의 데이터들이 어떻게 저장 됐는지 알려주는 데이터가 들어있음
                - Block Bitmap의 번호(위치)
                - Inode Bitmap의 번호(위치)
                - 블록 그룹안에 있는 빈 블록, 빈 디렉토리 수
                - Inode 수
                - Inode 테이블 번호(위치)
              - 모든 블록 그룹에 복사본이 존재
            - Block Bitmap
              - 사용되고 있는 블록이 몇개인지 기록
            - Inode Bitmap
              - 사용되고 있는 Inode가 몇개인지 기록
            - Inode Table
              - Inode들이 기록된 테이블
              - Inode한 개의 크기가 128Byte
            - DATA
      - ext3
        - 저널링 기술 도입
          - 디스크에 정보를 변경하기 전에 변경사항들을 저널이라고 부르는 로그 공간에 미리 기록
          - 디스크에 정보를 저장하던 도중에 전원이 끊겨도, 저널 로그를 보고 복구 가능
      - ext4
        - 1엑사 바이트 디스크 크기
        - 파일당 16테비 바이트 지원 2^40
  - XFS
    - 64비트 저널링 파일시스템
    - Redhat Linux 7버전 부터 기본 파일 시스템으로 채택
    - Centos 7 버전 부터 기본 파일 시스템으로 채택
    - 속도가 매우 빠름
- c.f) 포맷
  - 저장장치의 파일 시스템을 설정하여, 데이터 저장 장치를 준비하는 작업
  - 다만, 파일 시스템을 변경할 때, 저장 장치의 내용을 모조리 삭제하므로 보통은 이런 의미로 잘못되어 사용됨
- c.f) I-node
  - 개요
    - `ls -li` 이라는 명령어로 확인 가능
      - `i`는 i-node의 번호 조회
    - i-node list table에 i-node정보를 저장
  - 구성
    - 파일 형식
    - 파일 권한
    - 링크 수
    - 파일 소유주
    - 파일 그룹
    - 파일 크기
    - 파일이 만들어진 시간

### Mount

- 정의
  - OS가, storage device에 있는 파일과 디렉터리를, 유저가 컴퓨터의 파일 시스템을 통해서 접근할 수 있도록 만드는 과정
    - *근데 결국 디렉터리 구조에 편입시킨다는 것은 다른 파일 시스템(메인 파일 시스템??)과 연결 시킨다는것 아닌가?*
      - e.g) 리눅스에 usb를 연결 시키면, 특정 위치의 디렉터리가 생겨서 usb에 접근 가능(usb 내부의 경로도 인터페이스 변경 없이 터미널로 접근 가능)
- 과정
  - storage device에 접근 권한 획득
  - 인식
  - 읽기
  - 파일 시스템 구조와 메타데이터 processing
  - VFS(Virtual File System) 컴포넌트로 등록
- mount point
  - 새로 마운트 된 저장 장치 파티션의 VFS상의 location
    - *애초에 우리가 아는 절대경로 / 등은 그냥 VFS의 인터페이스?*
  - 마운트 프로세스가 끝나면 이 장소에서 파일과 디렉터리를 접근 가능
- unmount
  - OS가 mount point에 있는 파일과 디렉터리에 대한 모든 유저접근을 막음
  - 큐에 남아있는 유저데이터를 스토리지 디바이스에 넘겨줌
  - file system metadata를 refresh 해줌
  - 디바이스에 접근을 포기함
    - 안전한 디바이스 제거 가능하게 함

## Process

### Process

- 정의
  - 하나 혹은 그 이상의 스레드에 의해서 실행되고 있는 컴퓨터 프로그램의 인스턴스
- 분류
  - fg
    - 사용자가 직접적으로 제어 하는 프로세스
  - bg
    - 사용자가 직접적으로 제어 하지 않는 프로세스

### Daemon

- 정의
  - 사용자가 직접적으로 제어하지 않고, 부팅 때 자동으로 initialize되어, 백그라운드에서 동작하면서 여러 작업을 수행하는 프로그램
- 특징
  - 유닉스에서 부모 프로세스가 PID 1(init process) 이고, 제어하는 터미널이 없을 때, 그 프로세스를 데몬이라고 부름
    - 자식 프로세스를 fork 하여 생성 -> 자식을 분기한 자신을 죽임 -> init이 고아가 된 자식 프로세스를 자기 밑으로 데려감
  - MS 계열에서는 서비스라고 부름
- Daemon vs Service
  - Daemon
    - 최초 프로세스인 `init(or systemd)`가 initialize할 때, 실행하는 스크립트 디렉토리에 두면 바로 "데몬"이 됨
  - Service
    - `sc.exe`와 같은 프로그램으로 윈도우 API 함수를 이용해 등록해야 함
