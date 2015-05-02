# git 설치및 github을 연동 하는 과정을 위한 예제

##1. git 설치 
windows 버전에서는 windows에서 bash를 사용할 수 있게 해주는 git bash를 활용 합니다. 

git은 형상 관리를 위해 사용하고 , 실제 파일 수정 등에는 editor(eclipse, sublime, editplus, intellij ..)를 사용 합니다 

<a href="http://git-scm.com/download/win">Download</a> 링크에서 최신 버전의 git을 설치 
※ 주의사항 "GitHubSetup.exe" 가 아닌 "Git-1.9.5-preview20150319.exe" 파일을 사용하도록 한다. (by 남궁환)

windows 에서 git gui툴 자체의 충돌이 많은 관계로 gui 툴을 사용하지 않습니다.

설치시 Select Components 메뉴에서는 디폴트 상태로 Next 선택

Adjusting yout PATH environment 메뉴 -> Use Git from Git Bash only 를 선택
Congiguring the line ending conversions 메뉴 -> Checkout windows-style, commit Unix-style line endings 선택

git Bash 실행 

windows 에서 git bash 를 쓸경우 PATH를 추가할 필요 없습니다.

### - 설치 확인 

```
$ git 
```
git 명령 후 enter

<pre>
<code>
➜  mac_linux  git
usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p|--paginate|--no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

The most commonly used git commands are:
   add        Add file contents to the index
   bisect     Find by binary search the change that introduced a bug
   branch     List, create, or delete branches
   checkout   Checkout a branch or paths to the working tree
   clone      Clone a repository into a new directory
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   fetch      Download objects and refs from another repository
   grep       Print lines matching a pattern
   init       Create an empty Git repository or reinitialize an existing one
   log        Show commit logs
   merge      Join two or more development histories together
   mv         Move or rename a file, a directory, or a symlink
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects
   rebase     Forward-port local commits to the updated upstream head
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index
   show       Show various types of objects
   status     Show the working tree status
   tag        Create, list, delete or verify a tag object signed with GPG

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
</code>
</pre>

위와 같이 실행되면 설치 성공 
이외의 별도 git설정은 없음.

### git bash 에서 한글이 깨질 경우 

```
$ vi /c/Users/neod/.inputrc  

set output-meta on
set convert-meta off

$ vi /c/Users/neod/.bashrc
alias ls='ls --show-control-chars'

```


사용자 home directory 위치에  
.inputrc  파일 생성후  

```
set output-meta on
set convert-meta off
```

위 내용 입력 후 저장 

사용자 home directory 위치에  
.bashrc  파일 생성후  

```
alias ls='ls --show-control-chars'
```

위 내용 입력후 저장

 추가 후 저장 



#2. git 계정 설정

local git에서 사용할 user명 과 email을 설정 

```
$ git config --global user.name "이름"
```

```
$ git config --global user.email "이메일"
```

#3. github ssh 연동하기

###이과정은 별도 로그인 없이 편하게 github 과 local git을 연동하기 위한 ssh설정 입니다.

github 에서 local git 과 의 연동을 위해 <a href="http://ko.wikipedia.org/wiki/RSA_%EC%95%94%ED%98%B8">RSA</a> 키를 생성 

### RSA 생성하기
<pre>
<code>
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/neod/.ssh/id_rsa):
Created directory '/c/Users/neod/.ssh'
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/neod/.ssh/id_rsa.
Your public key has been saved in /c/Users/neod/.ssh/id_rsa.pub.
The key fingerprint is:
AAAAB3NzaC1yc2EAA....
</code>
</pre>


ssh-keygen <- 엔터

Enter file in which to save the key (/Users/chosk/.ssh/id_rsa):   <-여기서 엔터

Enter passphrase (empty for no passphrase):    <- RSA 키 사용시 쓸 비밀번호 입력후 엔터 

Enter same passphrase again:   <- 상동 

### RSA 복사하기 

<pre> 
<code>
$  cat /c/Users/neod/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCzYW3Afpug3JG/jqT2ZEqmI40vfou
</code>
</pre>

위 명령 실행후 ssh-rsa 부터 의 코드를 복사 
 
 
github.com 회원 가입 후 로그인 

https://github.com/settings/profile

접속 후 SSH keys 메뉴 접속 -> Add ssh 클릭  -> 생성할 키 이름 정한 후 내용에 복사한 ssh-rsa코드를 붙여 넣기 후 저장

#4. git 초기화 

git 을 생성할 폴더로 이동 

ex) /c/Users/neod/patternofgeek/sample 

위 경로에 git 을 생성할 예정 
<pre>
<code>

$ cd /c/Users/neod/patternfogeeks/sample 
$ git init
$ ls -a
.         ..        .git
</code>
</pre>



마지막과 같이 .git 폴더가 생성 되었으면, local git이 해당 폴더에 셋팅된 상태임
참고 : <a href="https://git-scm.com/book/ko/v1/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-Git-%EC%A0%80%EC%9E%A5%EC%86%8C-%EB%A7%8C%EB%93%A4%EA%B8%B0" > git 저장소 </a>

#5. git clone

github에 등록된 프로젝트를 clone할 수 있음 

현재 오픈된 github의 프로젝트를 클론 할 수 있지만 예제로 patternofgeeks의 git tutorials 를 clone

https://github.com/patternofgeeks/git_tutorials

위 주소 접속 후  화면 우측 중단의 
HTTPS clone URL 을 복사 

<pre>
<code>

$ cd /c/Users/neod/patternofgeeks 
$ git clone https://github.com/patternofgeeks/git_tutorials.git
$ ls -a
total 0
drwxr-xr-x  4 sk.cho  staff  136  5  1 18:17 git_tutorials
</code>
</pre>

위와 같이 표시되면 성공

참고 : <a href="https://git-scm.com/book/ko/v1/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-Git-%EC%A0%80%EC%9E%A5%EC%86%8C-%EB%A7%8C%EB%93%A4%EA%B8%B0" > git 저장소 </a> 

#6. git branch
현재 clone혹은 init된 git 을 다른 이름으로 local에 복제 할 수 있음. 

###현재 branch확인 

<pre>
<code>

$ cd /c/Users/neod/patternofgeeks/git_tutorials
$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
</code>
</pre>

###새 branch 생성
<pre>
<code>

$ git branch sampleBranch
$ git branch -a
* master
sampleBranch
remotes/origin/HEAD -> origin/master
remotes/origin/master
</code>
</pre>

###생성한 branch로 변경
<pre>
<code>
$ git checkout sampleBranch
Switched to branch 'sampleBranch'
$ git branch -a
  master
* sampleBranch
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
</code>
</pre>

###원본 branch로 이동 
<pre>
<code>
$ git checkout master
Switched to branch 'master'
$ git branch -a
* master
  sampleBranch
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
</code>
</pre>

###sample branch 삭제 
<pre>
<code>
$ git branch -d sampleBranch
Deleted branch sampleBranch (was e99ace1).
</code>
</pre>

branch 란? 
개발 상황에서 , 모듈별 기능별 개발 진행중 서로 의존성이나 연관성이 있는 모듈들을 수정할 경우 ,  해당 모듈과 연관된 다른 모듈들 역시 
영향을 받기 때문에, 개발 환경에서는 빠른 대응을 위해 작업을 구분 하기 위한 단위
 

#### branch를 나누지 않은 경우 
branch origin  - 원본 에서 c 기능과 연결된 a 기능을 수정중 

c 기능에 대한 수정 요청이 발생 . 

현재 작업 중인 수정을 rollback하고 c 기능을 수정 후 배포 한 뒤 , 다시 a 기능을 수정 

####수정 기능에 대한 branch를 나눈 경우 
branch origin  - 원본 
branch mode_c  - 원본을 복제 후 c 기능과 연결된 a 기능을 수정 

c 기능에 대한 수정 요청이 발생 

branch origin 을 수정후 배포 , branch mode_c는 연관 없음. 
이후 a 기능 수정후 branch origin 에서 branch mode_c 를 merge함으로써 작업을 완료 와 결합 

위와 같이 작업이나 연관이 있는 모듈이 많을 경우 위와 같이 branch 로 분리 후 작업이 대응에 효율적.

#7. git pull
git remote에 등록된 원격지의 repogitory로 부터 최신의 내용을 local git branch 에 적용
```
$ git pull
```
#8. git commit
현재 까지 작업한 내용을 git에 적용 (commit 안될 경우 git 에는 저장되지 않음) 
```
$ git commit -a -m'작업 내용'
```

#9. git push 
현재 까지 작업하고 commit이 완료되 상황에 대해 git remote에 등록된 repogitory로 내용을 merge 시킴
```
$git push
```

#10. git merge
local에서 분리된 branch끼리 내용을 합칠때 사용
```
$ git merge 브랜치명
```

#11 git status
현재 상태에서 git 에 저장되지 않은 내용이나 파일에 대한 내용을 볼수 있음 

#12 git diff
merge 시 충돌이 일어난 사항의 내용을 볼 수 있음 

