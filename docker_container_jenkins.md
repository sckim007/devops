1. Jenkins 이미지 Pull 및 실행
<pre>
docker run -d -p 7071:8080 \
-v /jenkins_dind2:/var/jenkins_home \
-v /var/run/docker.sock:/var/run/docker.sock \
--name jenkins-dind2 \
getintodevops/jenkins-withdocker:lts
...
6fc9abb57d1bd071e8fd98717ec0a03e135e2321e89d0aca2368c4208b89dc76

[options]
-d : 데몬 상태로 실행한다는 뜻이다. 이 옵션을 주지 않으면, 실행되는 로그를 바로 보여준다.
-p : 컨테이너 내부의 포트를 외부로 내보낼 포트로 연결시켜준다.
-v : 호스트에 볼륨을 지정해 주는 것이다. 만약 해당 컨테이너가 삭제되면 내부에 작성했던 스크립트 등의 데이터가 다 없어지기 때문에 볼륨을 지정해 외부에 백업하는 용도로 볼륨을 잡았다.
--name : 해당 컨테이너의 이름을 지정해준다.
-u : root 사용자로 실행되게 하기 위해 지정해 줬다.
</pre>

2. 컨테이너 실행 확인
<pre>
root@N-181:~# docker ps
CONTAINER ID        IMAGE   ...STATUS              PORTS                               NAMES
6fc9abb57d1b        getintode...                   50000/tcp, 0.0.0.0:7071->8080/tcp   jenkins-dind2
...
</pre>

4. 브라우저로 접속
<pre>
Unlock Jenkins
To ensure Jenkins is securely set up by the administrator, a password has been written to the log (not sure where to find it?) and this file on the server:

/var/jenkins_home/secrets/initialAdminPassword

Please copy the password from either location and paste it below.

Administrator password

[Copy and Paste]
아래 명령으로 파일을 읽고 복사 후 붙임
docker exec jenkins-dind2 cat /var/jenkins_home/secrets/initialAdminPassword
43d2879a97cf46eab12d301044b803fa
</pre>

5. jenkins 로그를 확인해 보자.
<pre>
docker logs jenkins
Running from: /usr/share/jenkins/jenkins.war
webroot: EnvVars.masterEnvVars.get("JENKINS_HOME")
...
*************************************************************
*************************************************************
*************************************************************

Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

312b2996923d4e3e82a89c69d355cc2c

This may also be found at: /var/jenkins_home/secrets/initialAdminPassword

*************************************************************
*************************************************************
*************************************************************

--> setting agent port for jnlp
</pre>

출력된 비밀번호를 웹페이지의 "Administrator password"란에 복사한다.

6. 플러그인 설치
<pre>
"Install suggested plugins", "Select plugins to install"에서 우선 "Install suggested plugins"을 설치
</pre>

7. First Admin User 생성
<pre>
계정명 : admin
암호 : wkfgkwk
암호확인: wkfgkwk
이름: administrator
이메일주소: sckim007@gmail.com
</pre>

8. Jenkins 시작
<pre>
"Start using Jenkins" 버튼 클릭
</pre>
