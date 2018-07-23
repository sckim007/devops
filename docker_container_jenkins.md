1. Jenkins Image Pull
<pre>
$ docker pull jenkins
Using default tag: latest
latest: Pulling from library/jenkins
55cbf04beb70: Already exists
1607093a898c: Already exists
9a8ea045c926: Already exists
d4eee24d4dac: Already exists
c58988e753d7: Already exists
794a04897db9: Already exists
70fcfa476f73: Already exists
0539c80a02be: Already exists
54fefc6dcf80: Already exists
911bc90e47a8: Pull complete
38430d93efed: Pull complete
7e46ccda148a: Pull complete
c0cbcb5ac747: Pull complete
35ade7a86a8e: Pull complete
aa433a6a56b1: Pull complete
841c1dd38d62: Pull complete
b865dcb08714: Pull complete
5a3779030005: Pull complete
12b47c68955c: Pull complete
1322ea3e7bfd: Pull complete
Digest: sha256:eeb4850eb65f2d92500e421b430ed1ec58a7ac909e91f518926e02473904f668
Status: Downloaded newer image for jenkins:latest
</pre>

2. Jenkins 이미지 실행
<pre>
$ docker run -d -p 8080:8080 -v /jenkins:/var/jenkins_home --name jenkins -u root jenkins
08a47bf93ca697b2bfe8012b275ca1a2eeebe2251b64deb15b2073efceeb819e

options
-d : 데몬 상태로 실행한다는 뜻이다. 이 옵션을 주지 않으면, 실행되는 로그를 바로 보여준다.
-p : 컨테이너 내부의 포트를 외부로 내보낼 포트로 연결시켜준다.
-v : 호스트에 볼륨을 지정해 주는 것이다. 만약 해당 컨테이너가 삭제되면 내부에 작성했던 스크립트 등의 데이터가 다 없어지기 때문에 볼륨을 지정해 외부에 백업하는 용도로 볼륨을 잡았다.
--name : 해당 컨테이너의 이름을 지정해준다.
-u : root 사용자로 실행되게 하기 위해 지정해 줬다.
</pre>

3. 컨테이너 실행 확인
<pre>
root@N-181:~# docker ps
CONTAINER ID        IMAGE   ...STATUS              PORTS                               NAMES
08a47bf93ca6        jenkins ...Up 18 seconds       0.0.0.0:8080->8080/tcp, 50000/tcp   jenkins
...
</pre>

4. 브라우저로 접속
<pre>
Unlock Jenkins
To ensure Jenkins is securely set up by the administrator, a password has been written to the log (not sure where to find it?) and this file on the server:

/var/jenkins_home/secrets/initialAdminPassword

Please copy the password from either location and paste it below.

Administrator password

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

