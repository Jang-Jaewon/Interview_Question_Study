# InfraStructure

- [Docker를 사용하는 이유](#%EF%B8%8F-docker를-사용하는-이유)
- [Docker-compose를 사용하는 이유](#%EF%B8%8F-docker-compose를-사용하는-이유)
- [EC2,RDS,S3 관련 설명해보세요.](#%EF%B8%8F-ec2,rdS,s3-관련-설명해보세요)
- [서버 아키텍쳐란](#%EF%B8%8F-서버-아키텍쳐란)
- [Apache와 Nginx의 차이](#%EF%B8%8F-apache와-nginx의-차이)
 
<br>

## 💡️ Docker를 사용하는 이유
> Docker는 사용하면 여러 사람들과 협업을 하는 경우에 발생하는 언어나 프레임워크 등의 버전 차이로 발생하는 문제를 해결해준다. 프로젝트에 필요한 언어나 프레임워크의 버전을 Dockerfile에 미리 명시해두고, 이에 따라 생성된 이미지를 컨테이너화되어 실행되기 때문에 OS가 다르더라도 동일한 독립적인 환경을 공유 가능하기 때문이다. 이런 장점은 서버가 갑작스럽게 확장되어야하는 상황에서 재빠른 대처를 가능하게하고, 이러한 일련의 과정이 빠르고 간편하다. 또한 과거 사용했던 VM과 달리 가볍고 빠른 실행속도를 가지기 때문에 독립적인 환경을 구축하는데 가장 대중화되어 사용되고 있다.


### 추가적인 내용 기술
- Docker는 runtime에 필요한 소스코드, 패키지 뿐만아니라 환경(OS)까지 포함시켜 이미지로 build가 가능하고, 이를 독립적인 환경에서 conatiner화하여 실행시키는 기술이다.
- Docker를 사용하면, OS수준에서 build가 가능하기 때문에 다른 환경에서 발생되는 문제로부터 자유롭고 수평적 확장이 필요한 경우 손쉽게 서버를 확장할 수 있다.
- 또한 Docker는 어떤 프로그램도 build하여 이미지로 만들 수 있고, 어디서든 실행시킬 수 있는 장점이 있다.
- Docker는 VM처럼 독립적인 환경 내에서 실행되지만, VM처럼 성능저하가 발생하지 않는다.
- VM의 경우 Hypervisor 위에 Guest OS라는 영역에 OS를 설치하하는데 독립적인 환경을 구축할 때마다 Guest OS 영역에 OS를 설치해야 한다.
- Guest OS 영역에 설치된 OS들은 PC의 자원을 서로 공유하기 때문에 이 과정에서 성능 저하가 발생한다.
- 이에 반해 Docker의 경우, 프로세스 격리 방법식이기 때문에 VM 처럼 Hypervisor와 Guest OS 영역이 필요없다. 실행에 필요한 모든 환경을 이미지화하여 파일로 가지고 있다가 어디서든 불러와 실행시킬 수 있다.
- 또한 Docker를 사용하지 않는 경우, 각 프로그래밍 언어에 따른 서비스 배포 방식의 차이가 존재하지만, Dockerfile로 이미지를 만든 뒤, 실행시키면 되기 때문에 간편하고 표준적인 방식을 제공한다.


<br>

## 💡️ Docker-compose를 사용하는 이유
> Docker Compose를 사용하면, docker 실행에 필요한 명령 및 옵션들을 명시적인 파일로 관리함으로써 컨테이너화시키기 위해 여러 옵션을 일일이 입력하는 번거로움을 해결한다. 또한 여러 이미지를 컨테이너화하면서 서로 연결시키기 위해 가상 네트워크를 지정해야 하는데, Docker-compose를 사용하면 서로 가상 통로를 자동으로 확보해주기 때문에 컨테이너 간 연결이 손쉽고, 보안의 취약점도 해결해준다.


### 추가적인 내용 기술
- Docker Compose를 사용하면, Dockr Container를 실행하기 위한 명령어, 옵션들을 일일이 입력할 필요가 없다.
- 특히, Docker로 실행시킬 이미지가 여러개인 경우, 여러 옵션들을 일일이 지정하여 개별적으로 이미지를 실행시켜야 한다.
- 이런 경우, Docker-compose를 사용하면 하나의 문서 내에서 이를 명시함으로써 손쉽게 제어가 가능하다.
- 또한 각 각의 컨테이너 간 연결이 필요할 때 가상 네트워크를 설정하여 network 옵션으로 지정해주어야 하는데, Docker-compose 내에 이를 명시함으로써 각 컨테이너 간에 서로를 인식하고 통신을 확립하기 간편하다.
- 뿐만아니라, DB를 docker로 띄우고 서버를 여러개 컨테이너 시켜서 DB에 연결시킬 수 있는데, 이는 반대로 누구든 연결이 가능하기 때문에 보안에 취약점으로 볼 수 있다.
- Docker-compose를 사용하면 해당 명시된 컨테이너들 끼리만 연결되기 때문에 보안적 측면에서도 장점을 가진다.

<br>

## 💡️ EC2,RDS,S3 관련 설명해보세요.
> EC2는 클라우드 환경으로 원격으로 제어할 수 있는 가상의 PC를 한 대 빌리는 것이다. RDS는 AWS에서 제공하는 RDBMS으로 MySQL, Oracle, SQL Server, PostgreSQL, MariaDB, Aurora(MySQL과 호환) 등의 데이터베이스를 지원한다. S3는 스토리지 웹 서비스로 파일 서버의 역할을하는 기능이다. 

### 추가적인 내용 기술
- EC2는 Elastic Compute Cloud 약자로, 서버를 위한 실제 기기들을 구입하고 설치할 필요없이 손쉽게 서버를 증설하고 사용한 만큼 비용을 지불하는 AWS 클라우드 서비스이다.
- EC2이 이 PC 1대를 인스턴스라는 개념으로 불리는데, 갑작스런 트랙픽 증가에 따라 신속하게 규모를 확장하거나 축소할 수 있어 서버 운영에 트래픽 예측의 필요성을 줄어들었다.
- 무엇보다 EC2는 물리적으로 PC를 구매하는 것에 비해 필요한 시간을 감소시켰고, 운영체제 뿐만아니라 CPU, RAM 용량까지도 필요에 따라 즉각적으로 조정할 수 있다.
- RDS는 Relational Database Service의 약자로, 관계형 데이터 베이스를 구축할 때 초기 설정과 데이터를 관리하는 일을 제외하고는 데이터베이스 유지보수와 관련된 일을 AWS에서 관리해준다.
- 또한 다양한 데이터베이스 엔진의 선택이 가능하고, 추가로 조정 가능한 용량을 지원하여 예상치 못한 양의 데이터가 쌓여도 비용만 추가로 내면 정상적으로 서비스가 가능하다.
- 특히, Amazon에서 Aurora라는 자체 데이터베이스를 제공하는데, AWS에서 MySQL과 PostgreSQL을 클라우드 기반에 맞게 재구성한 데이터베이스로 AWS에서 직접 엔지니어링하고 있기 때문에 더 향상된 성능을 제공한다.
- S3는 Simple Storage Service의 약자로 버킷이라는 저장소를 생성하여, 여러 파일 데이터를 객체로 저장할 수 있고 버킷에 포함된 모든 객체에 대한 인증과 접속 제한을 설정할 수 있다.
- S3는 Google Drive, MS Onedrive와 유사한 기능이며, 확장성이 높고 사용한 만큼 비용을 지불하기 때문에 비용 측면에서 효율적이다.
- 뿐만아니라 정적 웹사이트 호스팅을 지원하고, key와 value 형태로 데이터를 저장하는데, 여기서 value는 파일 데이터가되고 key는 객체를 식별하게 만드는 식별자 역할을 한다.

<br>

## 💡️ 서버 아키텍쳐란
>  Architecture 란 시스템의 구조, 행위, 더 많은 뷰를 정의하는 개념적 모형(conceptual model)이다. Web Service의 목적을 달성하기 위해 Server와 관련된 각 컴포넌트가 무엇이며, 어떻게 상호작용하는지에 대한 Server Architectur에 대한 이해가 필요하다. DNS, Load Balence, Web Server, WAS, Database Server, Chaching, Cloud Storage 등 각 컴포넌트에 대해 아래 정리하겠다.

![](https://velog.velcdn.com/images/jewon119/post/c8e29349-2e4d-4131-a773-f22688c47a4c/image.png)


### Domain Name Server
- DNS(Domain Name Server)는 도메인 이름(google.com)을 IP주소(168.126.63.1)로 반한한다.
- 전화번호에 비유하면 도메인 이름과 IP주소의 차이는 “Jae-Won에게 전화를 걸기”와 “010-1234-5678”과의 차이이다.
- 웹브라우저를 통해 어떤 도메인에 요청이 이뤄지면, 실제는 IP주소를 통해 해당 요청이 보내진다.
- 즉, Domain Name과 IP주소 간의 관계를 Key-Value 형태로 관리하는 서버가 DNS이다.

### Load Balence
- Load Balence를 이해하기 앞서, 수직적 확장(Scale-up)과 수평적 확장(Scale-out)에 대한 이해가 필요하다. 수직적 확장은 이미 사용하던 장치의 성능을 높이는 것이고, 수평적 확장은 더 많은 장치를 추가하는 것이다.
- 서버를 안정적으로 운영하기 위해서는 수평적 확장이 더 효과적인데 그 이유는 서비스 중단을 막기 위해서 이다. 서버는 언제든지 고장나고, 느려질 수 있으며 데이터 센터의 문제가 발생할 수 도 있기 때문에 1대 이상의 서버를 가짐으로써 이런 상황에 대비할 수 있다.
- 또한 수직적 확장은 언제나 한계에 부딪친다. 모든 요청을 처리할 수 있을 만큼 강력한 성능을 가진 컴퓨터는 없기 때문에 여러 대를 운영함으로써 많은 요청에 효과적으로 대응할 수 있다.
- 수평적으로 확장된 여러대의 서버는 특정 요청을 같은 방식으로 처리해야 하는데, Load Balence가 이 앞단에서 여러 서버 중 특정 서버에 과부하가 발생하지 않도록 적절하게 요청을 분산시키는 역할을 한다.
- 수평적으로 확장된 여러대의 서버는 특정 요청을 같은 방식으로 처리해야 하는데, Load Balence가 이 앞단에서 여러 서버 중 특정 서버에 과부하가 발생하지 않도록 적절하게 요청을 분산시키는 역할을 한다.

### Web Server
- 클라이언트 측에서 서버에 페이지 요청을 하면 요청을 받아 정적 컨텐츠(html, css, png 등)를 제공하는 서버
- 대표적인 Web Server는 Apache, Nginx, IIS 등이 있다.
- 정적 컨텐츠만 처리할 수 있고, 동적 컨텐츠 및 처리가 필요한 경우에는 WAS에 전달한다.
- Nginx와 Apache의 관계
    > Apache는 오픈소스 웹 서버로 웹의 산증인이며, 1996년 이후 한번도 웹서버의 영역에서 1등 자리를 놓친적이 없다. 하지만 Apache는 오래 전에 만들어진 소프트웨어로 시대 요구사항에 유효하지 않은 것도 있고, 새로운 요구사항과 충돌하는 것도 있다. 이에 Nginx는 새로운 시대의 요청에 부응해 만들어진 웹서버로 개발의 모든 목적이 높은 성능에 맞춰져 있다. 덕분에 폭발적인 증가세에 있는 인터넷 서비스를 지탱하는 적합하고 더 적은 자원으로 더 빠르게 데이터를 서비스할 수 있다.
- Django는 웹서버 인가?
    > Django는 개발 환경에서 사용할 목적으로 python으로 짜여진 가벼운 wsgi를 사용한다. 따라서 Web Application Framework이면서 Web Server이다. 하지만 배포 환경에서는 Django에 내장된 wsgi를 사용하는 것을 지양하고 있다. 이에 Web Application Framework 로써 보는 것이 적절하다.

### WAS(Web Application Server)
- WAS는 정적처리 뿐 아니라 동적처리까지 가능한 서버로 Web Server와 CGI를 합친 것이다.
- 예를들어, Web Server(ex. Nginx)는 Python을 해석할 수 없기 때문에 동적 처리에 필요한 HTTP요청을 WAS가 웹 애플리케이션 프레임워크(ex. Django)으로 중계한다. 또는 Django로부터 받은 응답을 Nginx가 이해할 수 있도록 변환하는 역할도 WAS의 역할이다.
- 대표적인 WAS로는 Tomcat, Jboss, Jeus 등이 있다.
- Web Server와 WAS를 분리하는 이유는?
    > WAS도 정적 요청에 대한 처리가 가능하지만, WAS의 비지니스 로직은 Database에 접근하는 경우가 많고, 이에 따른 수행 시간이 필요하기 때문에 정적 처리일 경우 Web Server에서 처리하는 것이 로드 분산에 효율적이다.
- WSGI는?
  > WSGI(Web Server Gateway Interface)는 Python으로 만들어진 Application Framework에서 사용하는 Web Server와 Web Application 간 인터페스를 제공하는 미들웨어이다. 즉, Web Server와 외부 프로그램을 연결하는 미들웨어가 WAS라면, Django와 같은 Python으로 만든 Web Application Framework가  WAS와 연결되는 경우, Web Server와 WAS를 연결하는 미들웨어 역할을 하는 것이 WSGI이다. 대표적인 WSGI는 Gunicorn, uWSGI 등이 있다.
- 왜 WSGI가 중요할까?
    > 전통적인 Web Server는 Python과 같은 어플리케이션을 이해하거나 실행할 수 없기 때문에 mod_python 이라는 모듈이 개발되었지만, 보안 이슈와 개발 지연 등의 이유로 새로운 방법이 필요하게 되었다. 이에 Python 커뮤니티에서 WSGI라는 미들웨어를 통해 표준 인터페이스를 만들게 되었다. WSGI는 사용하게 되면 Web Server를 다른 것으로 교체하더라도 Web Application의 코드를 수정할 필요가 없고, WSGI를 바꾸더라도 상관이 없다는 유연성을 가진다. 또한 WSGI는 같은 프로세스 내에서 여러 Application과 Framework가 실행되기 때문에 수 천 건의 request를 처리하는 것을 Framework가 아닌 WSGI의 역할이기 때문에 역할 분담에 따라 확장성에 유리하다.

### Database Server
- 모든 웹 애플리케이션은 데이터를 저장하고 이를 제공하기 위해 1개 이상의 Database를 사용한다.
- Database는 데이터의 구조를 정의하고, 데이터에 대한 CRUD를 수행한다.
- 대표적인 Database Server는 SQL과 NoSQ로 나뉘게 된다.

### Chaching Service
- Chaching Service는 데이터를 거의 O(1) 내에 찾을 수 있는 단순한 Key-Value 형식의 저장소를 제공한다.
- 애플리케이션은 Chaching Service를 통해 자원이 많이 소모되는 연산의 결과를 다시 처리하지 않고 Chache에서 가져옴으로써 서비스의 효율을 높인다.
- 보통 애플리케이션은 데이터베이스의 쿼리 결과, 외부 서비스 호출 결과, URL에 해당하는 HTML 등을 Chache에 저장한다.
- 이 때 주로 사용하는 Chaching Service 기술은 Redis와 Memcache로 HTML, 검색 결과, 검색어 입력 자동완성 결과 등을 Chache시켜 둔다.

### Cloud Storage
- Cloud Storage는 인터넷을 통해 파일을 저장, 접근 공유할 수 있는 저장소 시스템으로 AWS S3가 여기에 해당한다.
- 특히, RESTful API를 사용해서 Cloud Storage를 제어할 수 있고, 비디오, 사진, 오디오 데이터, Javascript, CSS 등 모든 파일을 관리할 수 있다.

<br>

## 💡️ Apache와 Nginx의 차이

### 추가적인 내용 기술
- Apache는 전통적으로 사용되어 온 대표적인 웹서버 중 하나로, HTTP 요청이 올 때 마다 프로세스를 복제하여 각 각 별도의 프로세스 내에서 해당 HTTP 요청을 처리한다. 이 기술을 Prefork MPM(Multi Processing Module) 방식이라 한다.
- 또한 Apache는 Worker MPM(Multi Processing Module)라 하여, 하나의 HTTP요청 연결 후, 여러 요청을 처리하기 위해 프로세스 내에서 여러 쓰레드를 생성하여 여러 HTTP 요청을 처리하는 방식도 지원한다.
- Nginx는 차세대 웹서버로 하나의 프로세스를 동작하며, HTTP 요청이 오면 이를 event라 부르는데, 프로세스 내에서 여러 event로 병렬적, 비동기 방식으로 처리한다. 이를 Event Driven 방식이라 한다.
- 즉, HTTP 응답은 결국 html 파일을 제공하는 것이므로 대부분의 CPU 작업이 아닌, IO 작업(저장매체에 접급)으로 볼 수 있는데, IO 작업을 event로 포워딩하고 요청 순이 아닌 요청 작업이 끝난 순으로 처리한다.
- 이에 Nginx는 HTTP 요청마다 프로세스나 쓰레드의 생성이 없기 때문에 시스템 자원 관리에 장점이 있다.
- 보통 사용자 접속이 많은 경우에 시스템 자원 관리의 효율성 때문에 일반적으로 Nginx가 더 좋은 성능을 보이고 있다. 

<br>
