## 52g 부트캠프 사전교육 정리

- [0주차 지옥에서 온 Git](#지옥에서-온-git)
    - [버전관리의 본질](#버전-관리의-본질)
    - [Git의 원리](#git의-원리)


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
- 터미너에서 파일 생성 및 편집
```bash
$ vim f1.txt
```
i누르고 편집 / esc누르고 중지 / wq 저장 및 종료
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

### Git의 원리
- gistory 설치
    - 파이썬을 설치해야 함. 어차피 설치할 거 지금 하자
    - gistory 세팅하는데 1시간 걸림.
        - 환경변수 path에 파이썬 설치된 경로 추가해줘야 함.
        - 파이썬 버전문제로 imp모듈을 사용 못함. 3.8버전으로 다운그레이드
- 파일을 add하면 index(파일명과 객체가 작성된)와 객체(파일 내용이 작성된)이 생김
- 파일의 내용이 같다면 해당 객체도 같음.. (파일명은 다를지라도)