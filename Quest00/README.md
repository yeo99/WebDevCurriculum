# Quest 00. 형상관리 시스템

## Introduction
* git은 2021년 현재 개발 생태계에서 가장 각광받고 있는 버전 관리 시스템입니다. 이번 퀘스트를 통해 git의 기초적인 사용법을 알아볼 예정입니다.

## Topics
* git
  * `git clone`, `git add`, `git commit`, `git push`, `git pull`, `git branch`, `git stash` 명령
  * `.git` 폴더
* GitHub

## Resources
* [Resources to learn Git](https://try.github.io)
* [Learn Git Branching](https://learngitbranching.js.org/?locale=ko)
* [Inside Git: .Git directory](https://githowto.com/git_internals_git_directory)

## Checklist
* 형상관리 시스템은 왜 나오게 되었을까요?
  > 변경사항을 체계적으로 추적하고 통제하기 위해서(소스 코드 뿐 아니라 개발환경, 빌드 구조 등 전반적인 환경의 내역에 대한 관리 체계를 의미함)

  > 기능, 성능, 제약 조건 등의 추상적인 관리 대상을 형상화하여 정하고 변경 사항에 대해서 통제 
  및 확인하며 이를 관련된 사람들에게 보고하기 위해서



* git은 어떤 형상관리 시스템이고 어떤 특징을 가지고 있을까요? 분산형 형상관리 시스템이란 무엇일까요?
  > git은 분산형 버전관리 시스템(Distributed Version Control System).

  > 파일을 서버에 저장하고, 수정을 위해 프로젝트 전체를 로컬에 다운 받은 뒤 수정한다. 서버에 문제가 생기면 아무 클라이언트의 복제물로 서버를 복원할 수 있다.
  * git은 어떻게 개발되게 되었을까요? git이 분산형 시스템을 채택한 이유는 무엇일까요?
  > git은 사유 소스 관리 시스템인 비트키퍼의 자유 이용이 막히면서 개발되었다. git은 빠른 속도, 단순한 구조, 비선형적인 개발, 완벽한 분산을 위해서 분산형 시스템을 채택하였다.


* git과 GitHub은 어떻게 다를까요?
  > Git은 소스 코드 기록을 관리하고 추적할 수 있는 버전 제어 시스템(기술)이고, Github는 git 저장소를 관리할 수 있는 클라우드 기반 호스팅 서비스이다.
* git의 clone/add/commit/push/pull/branch/stash 명령은 무엇이며 어떨 때 이용하나요? 그리고 어떻게 사용하나요?


  >clone: Repository를 새로운 디렉토리로 복제한다.

  >add: 다음의 commit을 기록할 때까지 변경분을 모아놓기 위해서 사용. (commit될 대상을 추가)

  >commit: add로 추가된 파일 및 폴더의 추가/변경 사항을 로컬 저장소에 기록

  >push: commit으로 로컬 저장소에 기록된 사항들을 원격 저장소에 업로드

  >pull: 원격 저장소의 최신 내용들을 로컬 저장소로 가져옴

  >branch: 독립된 작업 영역(저장소)를 만들어 내기 위한 기능. 각각의 branch는 다른 branch의 영향을 받지 않기 때문에, 여러 작업을 동시에 진행 가능

  >stash: 마무리 하지 않은 작업을 스택에 잠시 저장. stash를 이용하면 현재 까지의 작업을 따로 저장하고, working directory는 깨끗해진다. git stash list를 통해 stash 목록 확인 가능
* git의 Object, Commit, Head, Branch, Tag는 어떤 개념일까요? git 시스템은 프로젝트의 히스토리를 어떻게 저장할까요?
  > Object: Git은 Key-Value 데이터 저장소. Git에 데이터를 추가 시 Git은 Object를 생성한 후 해당 Object 내용의 SHA-1 해시값을 Key로써 사용하게 된다.

  > Head: HEAD는 해당 브랜치의 마지막 커밋을 뜻한다. 모든 브랜치는 HEAD 값이 존재한다.

  > Branch: 코드를 통째로 복사하고 나서 원래 코드와는 상관없이 개발을 진행할 수 있는데, 이렇게 독립적으로 개발하는 것이 브랜치이다.

  > Tag: 커밋을 참조하기 쉽도록 이름을 붙이는 것. 한번 붙인 태그는 브랜치처럼 위치가 이동하지 않고 고정됨. 일반 태그(Lightweight tag)는 이름만 붙일 수 있고, 주석 태그(Annotated Tag)는 이름, 태그에 대한 설명, 서명, 태그 생성자 이름, 이메일, 생성 날짜 포함 가능하다.

  > Git 시스템은 SHA-1 해시를 사용하여 체크섬을 만든다. 만든 체크섬은 40자 길이의 16진수 문자열이다. 파일의 내용이나 디렉토리 구조를 이용하여 체크섬을 구한다. SHA-1은 아래처럼 생겼다. Git은 파일을 이름으로 저장하지 않고 해당 파일의 해시로 저장한다.

* 리모트 git 저장소에 원하지 않는 파일이 올라갔을 때 이를 되돌리려면 어떻게 해야 할까요?
  > git rm [File Name] 을 입력하여 원격, 로컬 저장소 파일을 삭제하거나

  > git rm --cached [File Name] 을 입력하여 원격 저장소 파일만 삭제한다.
  
  > 삭제 후 commit, push하여 원격 저장소에 적용한다.

## Quest
* GitHub에 가입한 뒤, [이 커리큘럼의 GitHub 저장소](https://github.com/KnowRe-Dev/WebDevCurriculum)의 우상단의 Fork 버튼을 눌러 자신의 저장소에 복사해 둡니다.
* Windows의 경우 같이 설치된 git shell을, MacOSX의 경우 터미널을 실행시켜 커맨드라인에 들어간 뒤, 명령어를 이용하여 복사한 저장소를 clone합니다.
  * 앞으로의 git 작업은 되도록 커맨드라인을 통해 하는 것을 권장합니다.
* 이 문서가 있는 폴더 바로 밑에 있는 sandbox 폴더에 파일을 추가한 후 커밋해 보기도 하고, 파일을 삭제해 보기도 하고, 수정해 보기도 하면서 각각의 단계에서 커밋했을 때 어떤 것들이 저장되는지를 확인합니다.
* `clone`/`add`/`commit`/`push`/`pull`/`branch`/`stash` 명령을 충분히 익혔다고 생각되면, 자신의 저장소에 이력을 push합니다.

## Advanced
* Mercurial은 어떤 형상관리 시스템일까요? 어떤 장점이 있을까요?
* 실리콘밸리의 테크 대기업들은 어떤 형상관리 시스템을 쓰고 있을까요?
