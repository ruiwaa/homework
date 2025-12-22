🐙 Git 협업 및 충돌 해결 워크플로우

1. 작업 브랜치 Push
   작업한 이슈 브랜치(예: feat/login)를 원격 저장소(Remote)에 올립니다.
   bashgit push origin feat/login

2. PR(Pull Request) 생성
   GitHub 페이지로 이동하여 main 브랜치로 합쳐달라는 PR을 생성합니다.

3. 💥 충돌(Conflict) 발생 시 로컬 동기화
   GitHub에서 충돌 알림이 뜨면, 로컬(내 컴퓨터)에서 원격의 최신 내용을 가져와 합칩니다.
   bash# 1) 내 작업 브랜치로 이동 (확인용)
   git checkout feat/login

# 2) 원격 저장소의 최신 정보를 가져옴 (업데이트 확인)

git fetch origin

# 3) 가져온 원격의 최신 main 내용을 내 브랜치에 병합 시도

git merge origin/main

4. 충돌 해결 및 커밋
   VS Code에서 충돌난 파일들을 수정합니다. 수정이 완료되면 다시 스테이징하고 커밋합니다.
   bash# 충돌 수정 후 저장
   git add .
   git commit -m "Fix: 충돌 해결 및 코드 병합"

5. 재전송 (Push)
   수정한 내용을 다시 원격 브랜치로 보냅니다. 이렇게 하면 열려있는 PR에 자동으로 수정 사항이 반영됩니다. (PR을 새로 만들 필요가 없습니다!)
   bashgit push origin feat/login

6. 최종 병합 (Merge)
   GitHub PR 페이지에서 충돌이 해결된 것을 확인하고, 승인 후 [Merge pull request] 버튼을 클릭하여 main 브랜치에 병합합니다.
