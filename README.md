### **도커(Docker)란?**
![image](https://github.com/user-attachments/assets/72507968-99ce-4ee3-876a-67c27436acd9)
리눅스 컨테이너에 리눅스 어플리케이션을 프로세스 격리기술을 사용해 쉽게 **컨테이너**로 실행, 관리할 수 있게 해주는 오픈소스 프로젝트.

도커는 일반적으로 도커 엔진(Docker Engine) 혹은 도커에 관련된 모드 프로젝트를 말한다.

**도커 엔진(Docker Engine)** 은 컨테이너를 생성하고 관리하는 주체로서, 자체로도 컨테이너를 제어할 수 있고 다양한 기능을 제공해준다.

도커의 생태계에 있는 여러 프로젝트들은 도커 엔진을 좀 더 효율적으로 사용하기 위한 것에 불과하기 때문에, 도커의 핵심은 도커 엔진이라고 할 수 있다.

<br/><br/>
### **Vitrual Machine(가상 머신) vs Docker Container(도커 컨테이너)**
![image](https://github.com/user-attachments/assets/848d2fb9-3283-456c-9212-e5fccf4fcad6)
<br/><br/>
#### **가상 머신(Virtual Machine)**

![image](https://github.com/user-attachments/assets/b4377783-fe32-4118-ba0a-8db18c00d31b)

가상 머신은 하이퍼바이저를 이용해 여러 개의 운영체제를 하나의 호스트에서 생성해 사용하는 방식을 사용한다.

이러한 여러 개의 운영체제는 가상 머신이라는 단위로 구별되고 각 가상머신에는 우분투, CentOS 등의 운영체제가 설치되어 사용된다.

그래서 하이퍼바이저에 의해 생성되고 관리되는 운영체제는 게스트 운영체제(Guest OS)라고 하며, 각 게스트 운영체제는 다른 게스트 운영체제와는 완전히 독립된 공간과 시스템 자원을 할당받아 사용한다.

이러한 가상화 방식을 사용하는 툴로는 VitrualBox, VMWare 등이 있다.

그러나 각종 시스템 자원을 가상화하고 독립된 공간을 생성하는 작업은 하이퍼바이저를 반드시 거치기 때문에, 일반 호스트에 비해 성능의 손실이 발생한다. 또한 가상 머신은 게스트 운영체제를 사용하기 위한 라이브러리, 커널 등을 전부 포함하기 때문에 가상 머신을 배포하기 위한 이미지로 만들었을 때 이미지의 크기 또한 커진다는 단점이 있다.

즉, 가상 머신은 **완벽한 운영체제를 생성할 수 있다는 장점**은 있지만 일반 호스트에 비해 **성능 손실**이 있으며 수 기가바이트에 달하는 가상 머신 이미지를 어플리케이션으로 배포하기는 부담스럽다는 단점이 있다.
<br/><br/>
정리하자면,

> 가상 머신은 하이퍼바이저(Hypervisor)를 통해 여러 개의 운영체제가 생성되고 관리됨(Guest OS)  
> 시스템 자원을 가상화하고 독립된 공간을 생성하는 작업은 Hypervisor를 거치므로 성능 손실이 큼  
> 가상 머신은 Guest OS를 사용하기 위한 라이브러리, 커널 등을 포함하므로 배포할 때 용량이 큼

<br/>

#### **도커 컨테이너(Docker Container)**
![image](https://github.com/user-attachments/assets/d0728389-6712-4ccd-96fd-7f2254d00acc)

도커 컨테이너는 가상화된 공간을 생성하기 위해 리눅스 자체 기능인 chroot, 네임스페이스(namespace), cgroup을 사용함으로써 프로세스 단위의 격리 환경을 만들기 위해 성능 손실이 거의 없다.

컨테이너에 필요한 커널을 공유해서 사용하고 컨테이너 안에는 어플리케이션을 구동하는 데 필요한 라이브러리 및 실행 파일만 존재하기 때문에, 컨테이너를 이미지로 만들었을 때 이미지의 용량 또한 가상 머신에 비해 대푹 줄어든다.

따라서 컨테이너를 이미지로 만들어 배포하는 시간이 가상 머신에 비해 빠르며 가상화된 공간을 사용할 때의 성능 손실도 거의 없다는 장점을 가지고 있다.
<br/><br/>
정리하자면,

> 도커 컨테이너는 가상화된 공간을 생성할 때 리눅스 자체 기능을 사용해 프로세스 단위의 격리 환경을 만드므로 성능 손실이 거의 없음  
> 가상머신과 달리 커널을 공유해서 사용, 컨테이너에는 라이브러리 및 실행파일만 있으므로 용량이 작음  
> 따라서 컨테이너를 이미지로 만들었을 때 배포하는 시간이 빠르고 성능 손실 또한 거의 없음



<br/><br/>
### **도커 구성요소**
![image](https://github.com/user-attachments/assets/9846c843-a2fa-4b39-ad00-4ee94868999d)

**\[ Docker Client \]**

도커를 설치하면 그것이 Client며 build, pull, run 등의 도커 명령어를 수행한다.

**\[ DOCKER\_HOST \]**

도커가 띄워져있는 서버를 의미, DOCKER\_HOST에서 컨테이너와 이미지를 관리한다.

**\[ Docker daemon \]**

도커 엔진

**\[ Registry \]**

외부 이미지 저장소. 다른 사람들이 공유한 이미지를 내부 도커 호스트에 pull할 수 있다. 이렇게 가져온 이미지를 run하면 컨테이너가 된다.

\- public 저장소 : Docker Hub, QUAY

\- private 저장소 : AWS ECR 혹은 Docker Registry를 직접 띄워서 비공개로 사용하는 방법 등이 존재

<br/><br/>
### **도커 이미지와 도커 컨테이너**
![image](https://github.com/user-attachments/assets/b82301d7-ffa4-4635-b969-dfa5679fede8)

도커 엔진에서 사용하는 기본 단위는 이미지와 컨테이너이며 **도커 엔진의 핵심** 이다.

도커 이미지와 컨테이너는 1:N 관계이다.

도커 이미지와 컨테이너의 관계는 운영체제에서 프로그램 <-> 프로세스, 객체지향 프로그래밍에서 클래스 <-> 인스턴스의 관계와 비슷하다고 생각하면 된다.

**\[ Docker File -> Docker Image \]**

Docker File은 도커 이미지를 만들때 사용하는 파일. **docker build 명령어를 실행**시키면 도커 이미지를 만들 수 있댜.

**\[ Docker Image -> Docker Container \]**

Docker Image를 **docker run 명령어를 실행**시키면 Docker Container를 만들 수 있다.

<br/><br/>

#### **도커 이미지**

도커 이미지는 컨테이너를 생성할 때 필요한 요소이며 가상 머신을 생성할 때 사용하는 iso 파일과 비슷한 개념이다.

이미지는 컨테이너를 생성하고 실행할 때 읽기 전용으로 사용되며 여러 계층으로 된 바이너리 파일로 존재한다.

도커에서 사용하는 이미지의 이름은 기본적으로 아래의 형태로 구성된다.

> \[저장소 이름\]/\[이미지 이름\]:\[태그\]

\- 저장소 이름 : 이미지가 저장된 장소. 저장소 이름이 명시되지 않은 이미지는 도커 허브의 공식 이미지를 뜻한다.

\- 이미지 이름 : 해당 이미지가 어떤 역할을 하는지 나타내며 필수로 설정해야 한다.

\- 태그 : 이미지의 버전. 태그를 생략하면 도커 엔진은 latest로 인식한다.
<br/><br/>

#### **도커 컨테이너**

도커 이미지로 생성할 수 있으며 컨테이너를 생성하면 해당 이미지의 목적에 맞는 파일이 들어 있는, 호스트와 다른 컨테이너로부터 격리된 시스템 자원 및 네트워크를 사용할 수 있는 독립된 공간(프로세스)이 생성된다.

대부분의 도커 컨테이너는 생성될 때 사용된 도커 이미지의 종류에 따라 알맞은 설정과 파일을 가지고 있기 때문에 도커 이미지의 목적에 맞도록 사용되는 것이 일반적이다.

ex) 웹 서버 도커 이미지로부터 여러 개의 도커 컨테이너를 생성하면, 생성된 컨테이너의 개수만큼 웹 서버가 생성되고 이 컨테이너들은 외부에 웹 서비스를 제공하는 데에 사용된다.

컨테이너는 이미지를 읽기 전용으로 사용하되 이미지에서 변경된 사항만 컨테이너 계층에 저장하므로, 컨테이너에서 무엇을 하든지 원래 이미지는 영향을 받지 않는다.

또한 생성된 각 컨테이너는 각기 독립된 파일시스템을 제공받으며 호스트와 분리되어 있으므로 특정 컨테이너에서 어떤 어플리케이션을 설치하거나 삭제해도 다른 컨테이너와 호스트는 변화가 없다.
