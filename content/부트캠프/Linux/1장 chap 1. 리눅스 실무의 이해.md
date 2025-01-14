
### 운영체제의 개요

운영체제는 컴퓨터 하드웨어와 컴퓨터 사용자 간의 매개체, 사용자가 프로그램을 수행할 수 있는 환경을 제공


운영체제의 역할

1. 컴퓨터의 하드웨어를 제어
2. 작업의 순서를 정하며 입출력 연산을 제어
3. 프로그램의 실행을 제어, 데이터와 파일의 저장 관리
4. 사용자들 간의 하드웨어 자원을 공유할 수 있도록 한다.
5. 시스템 자원을 스케줄링하여 효율적으로 활용할 수 있게 한다.
6. 입출력을 쉽게 한다
7. 응용 프로그램의 작성과 실행을 편리하게 한다.
8. 오류의 발생을 막고 복구를 지원
9. 데이터의 조직화, 네트워크 통신 처리 기능을 수행
10. 편리한 사용자 인터페이스를 제공

최근 운영체제의 특징

1. 다중 사용자 시스템
2. 다중 작업 시스템
3. 강력한 네트워크 지원
4. 편리한 사용자 인터페이스 제공
5. ***계층적 파일 시스템***
6. 가상 메모리 지원
7. 고성능의 프로세서에 최적화
8. 개방형 운영체제화
9. 뛰어난 이식성 지원
10. 가상화 기술 지원



### 운영체제의 분류

1. UNIX

1969년 ***켄 톰슨***과 ***데니스 리치***에 의해 만들어졌다.
대표적인 계열로는 System V계열과 BSD계열이 있다.

System V : 주로 상업적인 목적을 가진 업체들
- IBM, HP, Sun Microsystem, SGI

BSD
- NetBSD, FreeBSD, OpenBSD, SunOS, NextStep, Mac OS X, GNU/Linux


2. 윈도(Windows)

빌 게이츠와 폴 앨런이 설립한 마이크로소프트사가 개발

3. Mac OS X

애플에서 개발한 OS
스티브 잡스는 최초의 GUI 방식의 운영체제가 탑제된 애플 리사를 개발

4. 모바일 운영체제

배터리 사용 , 무선 기반

---

리눅스 기반 모바일 운영체제 - Android, 바다 OS(삼성) , 마에모, 모블린, 미고, 리모, 타이젠

IVI(In-Vehicle Infotainment) - 자동차 내 운영체제

**QNX  비리눅스 IVI 운영체제**


---

### 리눅스의 특징

장점

1. 다중 사용자, 다중 처리 시스템
2. 완전히 공개된 시스템
3. 뛰어난 네트워크 환경
4. 다양한 파일시스템
5. 뛰어난 이식성
6. 유연성과 확장성
7. 뛰어난 안정성과 보안성
8. 우수한 가격대 성능비
9. 다양한 응용 프로그램 제공



단점

1. 사용자의 숙련된 기술이 요구


특징

1. **계층적인 파일 구조**
2. **장치의 파일화**
3. **가상메모리 사용**
4. 동적 라이브러리 제공
5. 가상 콘솔
6. 파이프
7. 리다이렉션




**리눅스의 철학**

GNU - GNU's Not Unix
GNU는 유닉스가 아니다, 소프트웨어에 상업화에 반대해 소프트웨어를 자유롭게 사용하도록 하는데 목적이 있다.


FSF(Free Software Foundation) 자유 소프트웨어의 생산, 보급, 발전을 위해 리처드 스톨먼이 세운 비영리 조직

- 실행의 자유
- 학습하고 개작할 자유
- 무료 또는 유료로 프로그램을 재배포할 수 있는 자유
- 프로그램을 개선시킬 수 있는 자유, 개선된 이점을 공동체 전체가 누릴 수 있도록 발표할 수 있는 자유


카피레프트(Copyleft)

저작권을 뜻하는 Copyright의 반대, 소프트웨어를 자유로운 상태로 유지시키는 것



### 주요 라이센스


`FSF 기반 라이센스들은 무료이용 가능하고 배포 또한 가능하다`

**GPL**

FSF의 창시자인 리처드 스톨먼은 GNU GLP에서 다섯 가지의 의무를 저작권의 한 부분으로서 강제

- 어떠한 목적으로든 사용할 수 있다.
- 실행 복사본은 언제나 프로그램의 소스코드와 함께 판매하거나 소스코드를 무료로 배포해야 한다.
- 소스코드를 용도에 맞게 변경할 수 있다.
- 변경된 프로그램 역시 소스코드를 공개 해야한다.
- 변경된 프로그램 역시 GPL 라이센스를 사용해야 한다.


**LGPL**

GPL + 독점 소프트웨어에서도 사용 가능


**BSD**

2차적 파생물에 대한 원시 소스코드의 비공개를 허용한다.
GPL + 독점 소프트웨어 사용 가능 + 2차 저작물 소스코드 비공개 가능


**Apache**

아파치 소프트웨어 재단에서 자체적으로 만든 소프트웨어 규정
BSD와 유사하지만 재배포시 아파치 라이센스를 포함시켜야 한다.

**MPL**

모질라 재단에서 만든 라이센스로 BSD와 GPL 라이센스의 혼합적인 성격
MPL라이센스를 가진 소스코드를 재배포한 경우 MPL 코드는 공개해야 하지만 수정한 코드는 비공개 가능하다.

**MIT**

MIT대학에서 만든 라이센스 BSD를 기초로 작성


---

### 리눅스 배포판

패키지 관리 기법에 따라 슬랙웨어, 데비안, 레드햇 계열로 나뉜다.

![![부트캠프/Linux/#^Table]]


---

### 리눅스 클러스터링
\
**고계산용 클러스터(HPC)**

- 고성능의 계산 능력을 제공하기 위한 목적
- 여러 노드를 병렬로 연결하여 하나의 작업을 처리


![[스크린샷 2024-07-19 오후 4.12.03.png]]


**부하분산 클러스터(LVS)**

- 이용자가 많을 떄 부하를 분산시키 위함
- 여러 서버에서 부하 분산(로드밸런싱) 가능

![[스크린샷 2024-07-19 오후 4.13.46.png]]


**고가용성 클러스터(HA)**

- 지속적인 서비스를 위해 사용
- LVS의 단점을 보완
- Backup Node를 사용

![[스크린샷 2024-07-19 오후 4.15.09.png]]



임베디드 시스템 
컴퓨터 기능을 내장 시킴

임베디드 리눅스
무료, 커널이 안정적, 많은 메모리 차지


---

### 클라우드 컴퓨팅

IT 자원은 어디엔가 존재하고 사용자는 필요할 때 활용하기만 하면 된다는 의미
as a service로 제공되는 컴퓨팅 환경

**IaaS(Infrastructure)**
- 서버, 컴퓨터, 스토리지 등 IT 하드웨어 자원을 클라우드 서비스로 빌려쓰는 형태
- EC2

**PaaS(Platform)**
- 소프트웨어를 개발할 수 있는 환경을 제공 받음
- Lambda, Elastic Beanstalk

**SaaS(Software)**
- 기업에서 사용하는 소프트웨어를 통째로 클라우드 서비스 사업자에게 빌려 쓰는 개념
- 메일, 클라우드 서비스

