## 52g 부트캠프 사전학습 정리

- [0주차 지옥에서 온 Git](#지옥에서-온-git)
    - [버전관리의 본질](#버전-관리의-본질)
    - [Git의 원리1](#git의-원리1)
    - [Git branch](#git-branch)
    - [Git의 원리2](#git의-원리2)
    - [Github](#github)


## 지옥에서 온 Git

### 버전 관리의 본질

- Git 설치 완료 (https://git-scm.com)
- 터미널에서 실습 폴더 생성
```bash
$ mkdir 52g
```
- 버전 관리 시작
```bash
$ git init
```
- 터미널에서 파일 생성 및 편집  
※ i누르고 편집 / esc누르고 중지 / wq 저장 및 종료
```bash
$ vim f1.txt
```
- 폴더 내 파일 상태 확인
```bash
$ git status
```
- 만든 사람 정보 설정
```bash
$ git config --global user name joon  
$ git config --global user email junkyu83@gmail.com
```
- 커밋 (커밋 시 메시지도 작성할 것)
```bash
$ git commit
```
- stage : 수정된 파일을 add 시켜놓은 상태 (커밋 대기)
- repository : stage에 있던 파일들이 commit되어 저장되는 장소
- 여태까지 한 이력 보기
```bash
$ git log
```
- 로그에서 출력되는 버전 간의 차이점을 출력
```bash
$ git log -p
```
- 버전 간의 차이점 비교 
```bash
$ git diff 버전id1..버전id2
```
- 이전 버전으로 돌아가기  
※ 원격저장소(공유)에 올리기 전에만 해라
```bash
$ git reset 버전id --hard
```
- 버전id의 커밋을 취소한 내용으로 새로운 버전 만들기
```bash
$ git revert 버전id
```
- 커밋 관련 도움말
```bash
$ git commit -help
```

### Git의 원리1
- gistory 설치
    - 파이썬을 설치해야 함. 어차피 설치할 거 지금 하자
    - gistory 세팅하는데 1시간 걸림.
        - 환경변수 path에 파이썬 설치된 경로 추가해줘야 함.
        - 파이썬 버전문제로 imp모듈을 사용 못함. 3.8버전으로 다운그레이드
        - 알고보니 gistory는 .git 폴더를 들여다보기 위해 egoing이 만든 프로그램임.. 대단하긴 하네.
- 파일을 add하면 index(파일명과 객체가 작성된)와 객체(파일 내용이 작성된)이 생김
- 파일의 내용이 같다면 해당 객체도 같음.. (파일명은 다를지라도)
- git은 sha알고리즘을 통해 변경사항들을 hash값으로 관리함
- 객체파일에는 1) blob : 파일 내용이 작성된.. 2) tree : 파일명과 내용을 담고있는 오브젝트를 가르키는.. 3) commit : 커밋 정보(tree, 이전커밋 parent, 커밋 수행자)가 있는.. 세 가지가 있음
- git 3가지 status : 1) working directory (내 실제 작업) 2) index 또는 staging area 또는 cache (add했을 때) 3) repository (커밋되고 난 후)

### Git branch
- commit 시 에디터 안뜨고 바로 메시지 입력
```bash
$ git commit -m "블라블라"
```
- commit 시 add 안하고 바로 커밋
※ 여기서 한번도 아직 add가 안된 파일은 해당이 안됨
```bash
$ git commit -a
```
- 위 두개 합쳐서
```bash
$ git commit -am "블라블라"
```
- test라는 이름의 브랜치 생성
```bash
$ git branch test
```
- 브랜치 전환
```bash
$ git checkout test
```
- 모든 브랜치를 표시하면서, 그래프 보여주고, 한줄로 표시할 때
```bash
$ git log --branches --graph --decorate --oneline
```
- 브랜치 간 비교할 때 (master에는 없고, test에는 있는 거)
```bash
$ git log master..test
```
- 브랜치 병합 (test를 master에다 병합할 때)
```bash
$ git checkout master  //먼저 master로 체크아웃  
$ git merge test // master <- test
```
- 브랜치 삭제
```bash
$ git checkout master  //먼저 master로 체크아웃  
$ git branch -d test
```
- 병합할 때, 파일이 다르면 자동병합, 같은 파일이더라도 내용이 다르면 자동병합, 그러나 같은 파일 내 같은 부분에 다른내용이 있으면 충돌 발생. 이 때는 수동으로 처리하고, add 시켜준다.
- 브랜치 작업하면서 아직 작업이 끝나지 않았고, 커밋하기도 애매한 상태에서 다른 브랜치로 checkout할 때는 stash라는 기능을 쓴다.
```bash
$ git stash  //stash 적용  
$ git stash apply //stash 가져오기
```

### Git의 원리2
- branch의 원리 : HEAD에 현재 checkout한 branch의 최신 commit이 무엇인지 기록되어 있다.
- reset의 원리 : head의 커밋 id를 바꾼다.
- checkout의 원리 : head의 내용을 바꾼다.
- merge의 원리 : 3 way merge (공통으로 가지고 있는 Base도 포함하여 Base와 다른 것을 기준으로 자동병합)

### Github
- 원격저장소를 지정할 때
```bash
$ git remote add origin 원격저장소경로 //origin은 원격저장소를 지칭하기 위한 별명
```
- 원격저장소 확인
```bash
$ git remote -v
```
- 원격저장소에 밀어넣을 때
```bash
$ git push -u origin master  // -u origin master는 최초 한번만
```
- Github에 있는 걸 가져올 때
```bash
$ git clone https://github.com/~~~~ . // .은 현재 디렉토리..
```
- 커밋 메시지 수정할 때 (원격저장소에 올리기 전)
```bash
$ git commit --amend
```
- 원격 저장소에 있는 걸 로컬로 땡겨올 때
```bash
$ git pull
```





