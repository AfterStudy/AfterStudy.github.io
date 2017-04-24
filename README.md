# AfterStudy
---------

### 서울대 입구역 TOZ에서 진행하는 개발 스터디 모임

- 한시간 동안 각자 알고 싶었던 부분들 검색하며 정리
- 남은 한시간동안 서로 정리한 부분 발표

### Git 사용법

- 파일 추가 수정 삭제 후 git add . <- 점까지
- git add commit -m "커밋 메세지"
- git push origin 자신의브랜치명
- 깃헙 와서 pull request생성 및 머지

### 작업전 자신의 원격 브랜치에 수정이 있을수 있으니 pull

- $ git pull origin 자신의브랜치명

### 혹시라도 로컬 내용을 깃헙의 내용으로 바꾸고 싶을때

- $ git fetch --all
- $ git reset --hard origin/자신의브랜치명
